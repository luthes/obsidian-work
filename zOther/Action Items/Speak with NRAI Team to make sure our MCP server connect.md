---
status:
  - done
due date: 2026-03-20T10:32:00
source: meeting
priority: 2
---
Docs:
* https://newrelic.atlassian.net/wiki/spaces/EPD/pages/4744872118/Onboarding+Tools+onto+Remote+MCP+Server

Add here: https://staging-one.newrelic.com/new-relic-ai/mcp-registry/home?duration=1800000&state=1b697e4a-b429-8524-7514-a32a84390034
Transport: HTTP
Authentication Method: None

This requires adding to Github, I think. 

We can do both Claude Marketplace so things are available to Claude, then the Agentic Platform.
* HEre is [Agentic Platform](https://source.datanerd.us/mind/agentic-platform) repo, [this config](https://source.datanerd.us/mind/agentic-platform/blob/master/src/agentic_platform/config/mcp_allowed_endpoints.yml) file. 
* Here is [Claude Plugin](https://source.datanerd.us/commune/claude-plugin-marketplace) Repo

Basically as long as our MCP server is there, it can work.

So my message to them is: 

hi @hero we're building an mcp server for acess to our datalake, but need oauth for tool calls for the added security/rbac to those systems. Is there a standardized schema for our tools that the agentic platforms frontend knows how to handle? The existing providers (jira/confluence) return this from authenticate graphql mutation which providers auth_url to the caller. Can I reuse that pattern with an external mcp server? How does the callback get routed to my mcp server? 

What do you send to our MCP server?
1. How does the agentic platform authenticate to our mcp server?
2. what identity headers does it forward to our mcp server when auth type is none? something from service gateway I assume, email, login context, account id, etc

What do we own?
1. Token storage similar to 


# Claude Notes
# Agentic Platform Auth Research — CDDS MCP Server

**Date:** 2026-03-16
**Sources:** Confluence (IAM, EPD, PF, DATA spaces), `mind/agentic-platform` source code

---

## Context

Our MCP server architecture is external to the MIND Agentic Platform — similar to Atlassian, GitHub, and PagerDuty in `src/agentic_platform/config/mcp_allowed_endpoints.yml`. Tools need user-scoped auth to downstream systems (Snowflake, Datalake, Airflow, etc.).

---

## How External MCP Servers Connect to the Agentic Platform

External MCP servers must be added to `mcp_allowed_endpoints.yml` (SSRF allowlist) via PR with security review to `mind/agentic-platform`. Contact **#help-mind** before submitting.

The platform supports four auth types when connecting to an external MCP server:

| Auth Type        | What it does                                                                         | User identity forwarded? |
| ---------------- | ------------------------------------------------------------------------------------ | ------------------------ |
| `NONE`           | Passes caller's login context headers through to your server                         | Yes                      |
| `BEARER_TOKEN`   | Resolves a static token from NerdGraph secrets, adds `Authorization: Bearer <token>` | No                       |
| `GENERIC_HEADER` | Resolves a static value from NerdGraph secrets, adds a custom header                 | No                       |
| `OAUTH`          | Full OAuth 2.1 PKCE flow (used by Atlassian, GitHub)                                 | Yes                      |

---

## Recommended Approach: `NONE` Auth with Per-Tool OAuth

Since we need user-scoped tokens for downstream systems, `NONE` is the right auth type. The platform forwards user identity headers on every request, including:

- `service-gateway-email`
- `x-login-context`
- `x-account-id`
- `service-gateway-login-context`

This means **we don't need an auth layer at the MCP server level at all**. Each tool handles its own auth against its own downstream system independently:

```
1. Agentic Platform connects to our MCP server (NONE auth, forwards user headers)
2. LLM decides to call a tool (e.g., snowflake_query)
3. Tool reads `service-gateway-email` from request context
4. Tool checks its own token store for that user's Snowflake OAuth token
   a. Token exists + valid → execute
   b. Token missing/expired → return auth URL for user to complete browser flow
5. User authenticates via Okta in browser
6. Callback stores token scoped to that user
7. LLM retries tool → executes
```

Token storage key pattern (per tool, per user): `{system}_{user_email}_{token_key}`
e.g. `snowflake_user@newrelic.com_oauth_token`

### What each tool needs

- Its own Okta OAuth client registered for that downstream system
- A callback endpoint on our MCP server (e.g. `/oauth/callback/snowflake`)
- Its own token store (see below)

### Token storage

We cannot use the Agentic Platform's internal `SecretStoreService` (Vault-backed, requires `AGENTIC_PLATFORM_SECRET_STORE_TOKEN`). Options:

- NerdGraph secrets (if our server has NerdGraph access)
- Our own Vault
- TBD based on infra

---

## What the Agentic Platform Does NOT Own (Our Problem)

- Per-user token storage for Snowflake/Airflow/etc.
- OAuth callback endpoints for each downstream system
- Surfacing "this tool needs auth" back through the MCP protocol to the calling UI
- Token refresh logic per downstream system

---

## Open Questions for MIND

1. **What headers are guaranteed with `NONE` auth?**
   Is `service-gateway-email` always present, or only when the caller is a logged-in user? Are there cases (e.g., service-to-service agent calls) where it's absent?

2. **Is there a standard MCP response schema for "tool needs auth"?**
   When a tool doesn't have a token yet and needs to return an auth URL, is there a response contract the Agentic Platform frontend knows how to handle (similar to how `authenticate` mutation surfaces `auth_url`)? Or is that entirely up to our UI?

### Answers from MIND Team
Hey Steven! Good questions  
**1.** Not always present. Gate (our auth layer) only injects `service-gateway-email` and `service-gateway-user-id` when the request comes from a logged-in human user. If the caller is an agent or service making an automated call (no human behind it), those headers won't be there but you will still get `service-gateway-principal-type` and `service-gateway-client-ip` regardless of who's calling.  
So don't assume email being always present with NONE auth.  
**2.** No separate callback needed. Our platform routes all traffic through Gate first, and Gate is what injects those headers , they can't be spoofed by callers hitting your service through the platform. If the header is there, Gate put it there after verifying auth. You can trust them as-is.  
The caveat: if your route is configured as `unauthenticated` in our routing config, Gate skips all checks and forwards nothing , in that case you'd be on your own. But if you're on a standard authenticated route, the headers are your signal.  
**3.** There's no MCP-level contract for this today. The way the platform handles OAuth is _before_ tool calls happen, not inside them. The flow is:  

- The UI calls `authenticateMcpServer` first → if OAuth is needed, it gets back an `authorization_url` → opens a popup → user authorizes → popup closes → _then_ tools get called with a valid token

So the intended pattern is: check/initiate OAuth **before** calling tools via the `authenticateMcpServer` mutation. If your tool tries to return "hey I need auth, here's a URL" mid-call, the frontend has no built-in way to handle that today. You'd have to build custom frontend handling for it , there's no standard contract for that case yet.  
Short answer: design your server to require auth be completed upfront via `authenticateMcpServer`, not reactively from inside a tool response.  
Hope that helps! Feel free to ping if anything's unclear. (edited)
---

## References

- `mind/agentic-platform` — `src/agentic_platform/service/mcp/`
- `mind/agentic-platform` — `src/agentic_platform/config/mcp_allowed_endpoints.yml`
- [MCP Server Setup Guide](https://newrelic.atlassian.net/wiki/spaces/EPD/pages/4781934646) (EPD)
- [Onboarding Tools onto Remote MCP Server](https://newrelic.atlassian.net/wiki/spaces/EPD/pages/4744872118) (EPD)
- [MCP Server Integration with NRAI Agentic Platform](https://newrelic.atlassian.net/wiki/spaces/DATA/pages/5237375199) (DATA)
- [MCP Server API Analysis](https://newrelic.atlassian.net/wiki/spaces/PF/pages/5010227500) (PF)
- [Existing MCP Flow](https://newrelic.atlassian.net/wiki/spaces/IAM/pages/5193138365) (IAM)






---
date: 2026-03-11
type: Meeting
meetingType: general
summary:
teams:
projects:
attendees:
  - "[[Steven]]"
tags:
---
## Preperation
- [ ] Prepare for Meeting

## Agenda & Files
- Simple Presentation
- Demo
## Notes
* Note
	* Some notes



![[Meetings Action Items.base]]

---

## Presentation Slides

> **Audience:** VP + Managers · **Time:** 30 minutes · **Format:** Slides + Live Demo

### Agenda

| # | Section | Time |
|---|---|---|
| 1 | Current MCP Servers | 5 min |
| 2 | Architecture Overview | 8 min |
| 3 | Registry & Tools Demo | 12 min |
| 4 | Next Steps | 5 min |

---

### Section 1: Current MCP Servers — 5 min

#### Slide 1 — The MCP Landscape

**Title:** Where MCP Servers Are Today at New Relic

The NR Agentic Platform today has two types of MCP servers:

```
NR Agentic Platform today:
  → One internal custom MCP server (monolith) — all tools, single auth level
      Any authenticated NR user can call any tool in that service
  → Many SaaS MCP servers — third-party, external tooling
```

Within the internal monolith, authorization is uniform across all tools — if you can reach the server, you can use any tool in it. That works for observability and product data. It doesn't work for what we're building.

**The data platform is different.**

We are giving AI agents access to:

- **Snowflake** — production data warehouse, query results can contain PII, financial data, customer records
- **Airflow** — controls production pipelines; a bad tool call can trigger a DAG
- **AWS** — infrastructure and ingestion controls
- **Fivetran** — manages data connectors and sync schedules

> *"The data we're protecting is categorically different — so the controls have to match."*

---

#### Slide 2 — Our Security Bar

**Title:** Why We Need a Stricter Model

|                               | General MCP Servers                                  | Platform MCP (ours)                                                             |
| ----------------------------- | ---------------------------------------------------- | ------------------------------------------------------------------------------- |
| **Data sensitivity**          | Observability, metrics, product data                 | PII, financial data, pipeline triggers, infrastructure                          |
| **Authorization granularity** | "Is this a NR employee?" — presence in AMS is enough | Specific AMS capability required per tool — opt-in only, not granted by default |
| **Caller restriction**        | Any authenticated NR identity                        | System identity allowlist — IAM PR required per authorized caller               |
| **Audit logging**             | Varies                                               | Every call logged: who, what tool, record count, response size, denials         |

**The distinction isn't whether AMS is involved — it is for everyone. It's what AMS is being asked.** Most MCP servers verify identity. We verify identity *and* require an explicit, per-tool capability grant. Accessing our tools requires something more than a NR badge.

---

### Section 2: Architecture Overview — 8 min

#### Slide 3 — Two-Service Design

**Title:** How It's Built

```
┌─────────────────────────────────────────────┐
│  Clients                                    │
│  NRAI Orchestrator · Claude · Data Portal   │
└─────────────────────┬───────────────────────┘
                      │ MCP Protocol
                      ▼
┌─────────────────────────────────────────────┐
│  MCP Gateway  (FastAPI)                     │
│                                             │
│  · Gate authentication (NR Login Service)  │
│  · AMS capability check per tool           │
│  · Audit logging                           │
│  · Tool dispatch                           │
└─────────────────────┬───────────────────────┘
                      │
                      ▼
┌─────────────────────────────────────────────┐
│  MCP Server  (FastMCP)                      │
│                                             │
│  · Tool Registry                           │
│  · Tool execution (in-process, Phase 1)    │
│  · MCP protocol handler                   │
└─────────────────────┬───────────────────────┘
                      │
                      ▼
      Snowflake · Airflow · AWS · Fivetran
```

*"Gateway never touches tools. The MCP Server never touches auth. Each service has one job."*

---

#### Slide 4 — Security Stack

**Title:** Defense in Depth

**Layer 1 — Authentication (NR Login Service / Gate)**
- Gate validates every token before requests reach our code
- Our service never validates tokens directly — reads Gate-injected headers:
	- `Service-Gateway-Principal-Id` — user ID or system identity UUID
	- `Service-Gateway-Principal-Type` — `user` or `system_identity`
	- `Service-Gateway-Organization-Id`
- `useSystemIdentity: true` supports both human users and machine callers

**Layer 2 — Authorization (AMS)**
- Every tool has a declared AMS capability string (e.g. `data_platform.execute.snowflake_query`)
- Gateway calls Authorization Service at invocation to verify the caller has that capability
- Capabilities are opt-in — not assigned to any role by default
- Each authorized calling service must be provisioned via IAM PR
- No capability grant = 403, logged

**Audit**
- Every invocation logged: `principal_id`, `tool_name`, `status`, `duration_ms`, `record_count`, `response_size_bytes`, `denial_reason`

---

#### Slide 5 — Where We Are Today

**Title:** Current Status

| Component                                      | Status               | Notes                                               |
| ---------------------------------------------- | -------------------- | --------------------------------------------------- |
| `mcp_mesh` — Gateway service                   | ✅ Running locally    | Session management, tool registry, health checks    |
| `mcp_poc` — MCP Server service                 | ✅ Running locally    | Dynamic tool loading, BaseAsyncTool framework       |
| Tool registry + namespacing                    | ✅ Working            | `tools/list` aggregates from downstream servers     |
| Session management                             | ✅ Working            | Redis-backed, returns `Mcp-Session-Id`              |
| Health monitoring                              | ✅ Working            | Removes unhealthy servers automatically             |
| Hot-reload config                              | ✅ Working            | New tool server in YAML = picked up without restart |
| `BaseAsyncTool` framework                      | ✅ Working            | Rate limiting, circuit breaker, retry on every tool |
| Demo tool (WeatherAPI)                         | ✅ Demo-ready         | Exercises full resilience stack                     |
| Staging deployment                             | ⏳ Pending SLC Review | Ready to deploy — awaiting SLC sign-off             |
| `tools/call` forwarding through gateway        | 🔧 In progress       | Phase 1                                             |
| Gate / AMS auth integration                    | 🔧 In progress       | Phase 1                                             |
| Real tools (Snowflake, Airflow, AWS, Fivetran) | 🔧 In progress       | Phase 1                                             |

**Bottom line:** Both services are fully functional locally. Staging deployment is ready — blocked on SLC Review.

---

### Section 3: Registry & Tools Demo — 12 min

#### Demo Part A — Registry (6 min) · `mcp_mesh`

**Step 1 — Health Check (30 sec)**

```bash
curl https://staging-dataos-mcp-mesh-server.vip.cf.nr-ops.net/status/check
```

> *"Both services are up. The gateway monitors the downstream MCP Server — if it goes unhealthy, it's removed from the registry automatically."*

**Step 2 — Tool Discovery / `tools/list` (2 min)**

```bash
curl -X POST https://staging-dataos-mcp-mesh-server.vip.cf.nr-ops.net/mcp \
  -H 'Content-Type: application/json' \
  -d '{"jsonrpc":"2.0","method":"tools/list","id":1}'
```

Point out the namespaced tool name (`mcp_poc:get_weather`).

> *"The gateway aggregates tools from all downstream MCP servers and namespaces them. Add a new server to the config YAML and its tools appear here automatically — no code changes, no restart."*

**Step 3 — Session Init (2 min)**

```bash
curl -X POST https://staging-dataos-mcp-mesh-server.vip.cf.nr-ops.net/mcp \
  -H 'Content-Type: application/json' \
  -d '{"jsonrpc":"2.0","method":"initialize","params":{"protocolVersion":"2024-11-05","clientInfo":{"name":"demo","version":"1.0"}},"id":1}'
```

Show the `Mcp-Session-Id` in the response header.

> *"Session state is Redis-backed. When we wire in Gate auth, principal context attaches to the session here — every downstream tool call carries that identity forward."*

**Close:** *"This is the gateway layer — session management, tool discovery, routing. The plumbing is all here. Auth is the next piece we wire in."*

---

#### Demo Part B — Tools (6 min) · `mcp_poc` directly

**Step 1 — Tool Schema (1 min)**

```bash
curl -X POST http://mcp_poc:8001/mcp \
  -H 'Content-Type: application/json' \
  -d '{"jsonrpc":"2.0","method":"tools/list","id":1}'
```

> *"Each tool self-describes its inputs and outputs. The gateway reads this schema — tools don't need to know anything about the gateway."*

**Step 2 — Happy Path (1 min)**

```bash
curl -X POST http://mcp_poc:8001/mcp \
  -H 'Content-Type: application/json' \
  -d '{"jsonrpc":"2.0","method":"tools/call","params":{"name":"get_weather","arguments":{"city":"New York","units":"metric"}},"id":1}'
```

> *"Tool call, result back. When wired through the gateway, auth and audit happen before this call is ever made."*

**Step 3 — Resilience Demo (3 min)**

```bash
for i in {1..15}; do
  curl -s -X POST http://mcp_poc:8001/mcp \
    -H 'Content-Type: application/json' \
    -d '{"jsonrpc":"2.0","method":"tools/call","params":{"name":"get_weather","arguments":{"city":"New York","units":"metric"}},"id":'$i'}' | jq .
done
```

Point out: rate limiter slowing requests → retry on random failures → circuit breaker trip → recovery.

> *"This is `BaseAsyncTool`. Every tool we build inherits rate limiting, circuit breaker, retry, and telemetry. A Snowflake tool author writes query logic. They don't write any of this."*

**Close:** *"When we build Snowflake, Airflow, and AWS tools — they all get this for free."*

---

### Section 4: Next Steps — 5 min

#### Slide 6 — Roadmap

**Title:** What's Next

| Phase        | Work                                                                                                               | Status     |
| ------------ | ------------------------------------------------------------------------------------------------------------------ | ---------- |
| **Phase 0**  | Two services in staging, tool framework, session management, health monitoring                                     | ✅ Complete |
| **Phase 1**  | Gate + AMS auth, `tools/call` forwarding, real tools (Snowflake, Airflow, AWS, Fivetran), rate limiting at ingress | 🔧 Now     |
| **Phase 2**  | Machine identity for NRAI Orchestrator, Domain Tool Services (standalone per platform)                             | Planned    |
| **Phase 3+** | Credential passthrough, fine-grained permissions                                                                   | Future     |

**Phase 1 is the critical path.** Gate + AMS integration unlocks everything — real principals, real capability checks, real audit logs. Once that's in, tools are additive.

---

#### Slide 7 — Dependencies

**Title:** What We Need

| Dependency                    | Team       | What's Needed                                                                           |
| ----------------------------- | ---------- | --------------------------------------------------------------------------------------- |
| Gate configuration            | IAM        | Enable Gate auth (`platformAuth` + `useSystemIdentity`) for our service                 |
| AMS capability registration   | IAM        | PR to `authorization_management_service/batches.yml` for `data_platform.*` capabilities |
| System identity provisioning  | IAM + MIND | System identity for NRAI Orchestrator granted `data_platform.access.mcp_server`         |
| SLC Review                    | Security   | Formal SLC review for production sign-off                                               |
| NRAI Orchestrator integration | MIND Team  | MCP client registration, `tools/list` + `tools/call` support                            |

**The ask:** Alignment and introductions to unblock IAM and MIND team coordination.

---

### Presenter Notes

**Presenters:**
- **Zach** — Gateway demo (`mcp_mesh`: health check, `tools/list`, session init)
- **Shreya / Kethan** — Tools demo (`mcp_poc` directly: tool schema, happy path, resilience)

Note: The two demos are **independent** — the gateway does not call through to tools yet (session wiring is in progress). Present them as separate working pieces, not an end-to-end flow.

**One-liner per section:**
- **Current MCP Servers:** *"The data we're protecting is categorically different — so the controls have to match."*
- **Architecture:** *"Two services. Gateway handles security. MCP Server handles tools. Neither knows about the other's job."*
- **Demo:** *"The infrastructure is running locally. Auth and end-to-end tool dispatch are what Phase 1 delivers."*
- **Next Steps:** *"Phase 1 is Gate + AMS. Once auth is in, tools are additive."*

**Demo prep checklist:**
- [ ] Both services running locally (`mcp_mesh` on port 8000, `mcp_poc` on port 8001)
- [ ] Two terminal windows — Zach on `localhost:8000`, Shreya/Kethan on `localhost:8001`
- [ ] Health check pre-run so services are warm
- [ ] 15-call loop script ready to paste (Shreya/Kethan)
- [ ] `jq` installed on both machines for readable JSON output
- [ ] Screenshots ready as fallback if local services go down

**What NOT to say:**
- Don't reference other teams' MCP servers by name as a negative comparison
- Don't say "SLC approved" — say "security-reviewed design"
- Don't attempt `tools/call` through `mcp_mesh` — session wiring isn't complete, it won't work end-to-end
- Don't frame the two separate demos as a gap — frame them as two services demoed independently, which is accurate

---

##### Confluence/Google Doc Template
###### Purpose
Why we are here
###### Inputs
Doc / backlog / design / decisions
###### Questions to answer
The 2–4 things that must be resolved
###### Decisions needed
What should be finalized today
###### Next steps / owners
Who does what by when
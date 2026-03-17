---
date: 2026-03-11
type: Meeting
meetingType: general
summary:
teams:
  - dataos
projects:
  - agentic ai
attendees:
  - "[[Steven]]"
tags:
---
## Preperation
- [ ] Prepare for Meeting

## Agenda & Files

  **AuthN + AuthZ (FastAPI layer)**
  - Validate the incoming token and confirm the principal's identity
  - Extract principal context (`principal_id`, `principal_type`, roles)
  - Check if the principal is allowed to call the requested tool (whitelist/policy)

  **Audit + Dispatch (FastMCP layer)**
  - Log `request_id`, `principal`, `tool` for every call
  - Route `tool_name` to the correct handler

  **Aggregation does not belong in the gateway.** In a traditional API gateway,
  aggregation exists because the client needs composed data in a single call. In
  MCP, the LLM is the orchestrator — it decides what tools to call, in what order,
  and how to combine results. Moving aggregation into the gateway means the gateway
  has to understand tool semantics. That's the wrong layer.

  **Caching tool results does not belong in the gateway.** Tools are calling
  Snowflake, Airflow, Fivetran — the LLM needs fresh data to reason correctly.
  Caching at the gateway gives the agent stale state to make decisions on.

  **Caching `tools/list` is not worth the complexity.** Cache invalidation risk
  (stale tool lists causing the LLM to call tools that no longer exist, or miss
  newly added ones) outweighs the performance benefit on a low-traffic internal
  server. Pass it through and revisit only if there's a demonstrated performance
  problem.

  ## Where the Sr. Engineer's concerns have partial merit
  - **Rate limiting** — the gateway is the right place for this if needed
  - **Tool registry metadata caching** — schemas and descriptions are stable enough
    to cache, but not a priority at this stage
  - **Connection pooling** — valid concern but belongs at the Domain Tool Services
    layer (L6), not the gateway
### Agenda

**1. Frame the purpose — 5 min**
“Today’s goal is to review the concerns, decide what is truly required for MVP/Phase 0, and document what we are intentionally deferring.”

**2. Recap the proposed design — 5–10 min**
Very short. Only enough so everyone is anchored.

**3. Review concerns one by one — 20–25 min**
Create a table live if needed:

| Concern                     | Why it matters | Needed in Phase 0? | If deferred, what risk do we accept? |
| --------------------------- | -------------- | ------------------ | ------------------------------------ |
| caching                     |                |                    |                                      |
| tool aggregation            |                |                    |                                      |
| registry behavior           |                |                    |                                      |
| auth / role mapping         |                |                    |                                      |
| latency / scale assumptions |                |                    |                                      |
| failure handling            |                |                    |                                      |
**4. Explicitly separate must-have vs should-have — 10 min**
Use language like:
* required for first production path
* useful but deferrable
* future-state capability
* not needed unless assumption changes

**5. End with decisions and next steps — 5–10 min**
Capture:
* what is in Phase 0
* what is deferred to Phase 1+
* what assumptions make Phase 0 viable
* what spikes or follow-ups are needed
## Notes
* Zach is leading this meeting
* High Level - What we're doing for Phase 0
	* Docs are not all up to date, we're learning
* If the Gateway handles many MCP servers, would that solve Shreya's issues of latency she was bringing up in standup?
	* RCA use case --> No. We need multiple MCP Servers
	* Do we want more endpoints? Or nah...
* MCP Tool RBAC
* 

Questions:
* Kethan - Entirely on MCP, we can offload to a skill so that we can reference, this guides the Orchestrator to point ot the MCP Server
	* Does NRAI support these skills?


Demo Items -> 
* We're going to drive towards the demo for next Thursday with Gateway.

Phase 0 : Deploy Gateway to MCP 

## Action Items
`button-meeting-action-item`

![[Meetings Action Items.base]]
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

## Notes
* Note
	* Some notes

## Action Items
`button-meeting-action-item`

![[Meetings Action Items.base]]
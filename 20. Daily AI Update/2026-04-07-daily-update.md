---
date: 2026-04-07
type: director-update
updateType: daily
sprint: E30MAR2026-DP
status: draft
summary: Zach moved NR-539893 (tool/call support for non-streaming MCP) from Backlog to In Progress this morning, resolving the sequential dependency flagged yesterday; Shreya's Airflow deploy PR came unstale with Apr 6 commits.
teams:
  - Data Platform
projects:
tags:
---

> [!INFO] Sprint
> **Sprint**: `=this.sprint` | **Day 9 of 12** (sprint ends 2026-04-10 · 4 working days remain)
> 
> Stevens Manual Notes:

> [!SUCCESS] Progress Delta
> **Tickets advanced**:
> - [NR-539893](https://new-relic.atlassian.net/browse/NR-539893) — mesh 0.1: tool/call support for downstream MCP (Backlog → In Progress, Zach · updated 2026-04-07 05:10 PDT)
> - [NR-541438](https://new-relic.atlassian.net/browse/NR-541438) — IAM Audit (In Progress → In Review, Saravana · updated 2026-04-06 22:59 PDT)
> - [NR-542797](https://new-relic.atlassian.net/browse/NR-542797) — CAS: Modify Paging hours charts (→ Closed, Rakshith · Apr 6)
> - [NR-540150](https://new-relic.atlassian.net/browse/NR-540150) — Hero 1 (→ Closed, Rakshith · Apr 6)
> - [NR-540151](https://new-relic.atlassian.net/browse/NR-540151) — Hero 2 (→ Closed, Sumedh · Apr 6)
>
> **Tickets regressed / blocked**: —
>
> **PRs opened**: —
>
> **PRs merged**: —
>
> **Blockers resolved**:
> - [sjayaram/platform-ai #69](https://source.datanerd.us/dataos/platform-ai/pull/69) (NR-536803 Airflow deploy) — was flagged stale since Apr 2; received commits Apr 6 17:52Z — no longer stale
>
> **New blockers**:
> - [NR-539893](https://new-relic.atlassian.net/browse/NR-539893) now In Progress but has no open PR (Zach)

## Yesterday
> [!CHECK] Direct Team
> - **Zach** — NR-539892 (session mgmt) still In Progress (last ticket update Apr 3, no PR); NR-539893 (tool/call support) moved to In Progress this morning — sequential dependency path is now unblocked in intent
> - **Kethan** — [NR-540735](https://new-relic.atlassian.net/browse/NR-540735) "Deploy MCP Mesh to Staging" holding In Staging (updated Apr 6); [NR-536183](https://new-relic.atlassian.net/browse/NR-536183) gateway health service In Progress (last updated Apr 3); sprint tracking tickets (NR-540149, NR-540154) touched Apr 6
> - **Shreya** — [sjayaram/platform-ai #69](https://source.datanerd.us/dataos/platform-ai/pull/69) "NR-536803 - Deploy airflow mcp server" had commits Apr 6 17:52Z (was stale since Apr 2); [NR-536203](https://new-relic.atlassian.net/browse/NR-536203) Airflow service account still In Review; [NR-542217](https://new-relic.atlassian.net/browse/NR-542217) dbt Core spike In Progress (last updated Apr 2); sprint tracking tickets (NR-540147, NR-540148) updated Apr 6
> - **Steven** — [NR-542145](https://new-relic.atlassian.net/browse/NR-542145) Gateway Human Auth SLC Review In Progress (updated Apr 6 07:48); NR-542144 / NR-542143 (Airflow + dbt SLC Reviews) still In Progress with no recent updates

> [!WARNING] Blockers / Needs Attention
> - **Zach** — [NR-539892](https://new-relic.atlassian.net/browse/NR-539892) In Progress since Apr 3 with no PR; NR-539893 just moved to In Progress with no PR — both mesh session mgmt tickets unlinked to any open PR
> - **Kethan** — [NR-536183](https://new-relic.atlassian.net/browse/NR-536183) gateway health service In Progress since Apr 3 with no PR
> - **Shreya** — [sjayaram/airflow-mcp-server #1](https://source.datanerd.us/dataos/airflow-mcp-server/pull/1) "Initial GC and mcp server setup" still open, stale since Apr 2, no ticket ref — needs triage
> - **Kumar Aryan** — 15+ stale open PRs (pre-Apr 4) across DataOS, all unlinked to tickets — bulk closure recommended

> [!ERROR]- Broader Team
> - **Saravana** — [NR-541438](https://new-relic.atlassian.net/browse/NR-541438) IAM Audit advanced to In Review (Apr 6 22:59); [NR-541439](https://new-relic.atlassian.net/browse/NR-541439) Multiple AWS Accounts In Review (updated today); [NR-541440](https://new-relic.atlassian.net/browse/NR-541440) New AWS Account In Review (updated today)
> - **Rakshith** — [NR-542797](https://new-relic.atlassian.net/browse/NR-542797) Closed + [NR-540150](https://new-relic.atlassian.net/browse/NR-540150) Closed (both Apr 6); NR-540117 + NR-540114 still In Review
> - **Shameek** — [NR-545781](https://new-relic.atlassian.net/browse/NR-545781) "Propagate Login Context — A2Q" In Review (updated Apr 6); NR-540137, NR-540136 In Review
> - **Kumar Aryan** — NR-540110 + NR-539745 (Spark Observability) both In Review (updated Apr 6)
> - **Sumedh** — [NR-540151](https://new-relic.atlassian.net/browse/NR-540151) Closed (Apr 6)

## Today

> [!CHECK] Direct Team
> - **Zach** — Target: first PR up for NR-539892 (session mgmt); move NR-539893 forward now that it's unblocked
> - **Kethan** — Continue NR-536183 (health service) and validate NR-540735 staging — both need PRs; [NR-542139](https://new-relic.atlassian.net/browse/NR-542139) dbt Core spike is In Staging (deliverable due this sprint)
> - **Shreya** — Triage airflow-mcp-server PR #1 (unlinked, stale); advance NR-536203 from In Review → Closed; continue deploy work on NR-536803 / PR #69
> - **Steven** — Drive NR-542145 (Gateway Human Auth SLC) toward completion; check in on NR-542144 / NR-542143 which haven't moved since Mar 31

> [!QUESTION] Today's Focus
> Day 9 of 12 — 4 working days remain (Apr 7–10). Critical path: mesh session mgmt + tool/call PRs from Zach, Airflow MCP deploy closure from Shreya, and SLC reviews from Steven. NR-540733 / NR-540734 (Airflow Mesh Config + Tool Validation) remain Backlog — scope confirmation still needed.

> [!ERROR]- Broader Team
> - Saravana: IAM Audit (NR-541438) now In Review; multiple AWS account tickets moving
> - Shameek: A2Q Login Context (NR-545781) In Review — watch for review turnaround
> - Kumar Aryan: Spark observability (NR-540110, NR-539745) in review — no other changes

## Activity

> [!TODO] Confluence Activity
> No pages modified in DATA space by direct sprint team on 2026-04-06.

> [!WARNING] GitHub — Stale PRs
> PRs open with no update since before 2026-04-04:
> - [sjayaram/airflow-mcp-server #1](https://source.datanerd.us/dataos/airflow-mcp-server/pull/1) — "Initial GC and mcp server setup" · last updated 2026-04-02 · **no ticket ref** · needs triage
> - [karyan/dataos-otel #15](https://source.datanerd.us/dataos/dataos-otel/pull/15) — "changed scapping port" · last updated 2026-03-29 · no ticket ref
> - [karyan/spark-operator #34](https://source.datanerd.us/dataos/spark-operator/pull/34) — "enabled pod monitor" · last updated 2026-03-26 · no ticket ref
> - karyan has 15+ additional stale open PRs (pre-2026) across DataOS repos — recommend bulk triage/close

> [!ERROR]- GitHub — PR Activity
> **Merged (2026-04-06):**
> - [karyan: dataos/data-portal-telemetrygen #235 "Static alerts"](https://source.datanerd.us/dataos/data-portal-telemetrygen/pull/235) — merged 2026-04-06T06:46Z · no ticket ref in body
>
> **Open PRs (direct team, active):**
> - [sjayaram/platform-ai #69](https://source.datanerd.us/dataos/platform-ai/pull/69) — "NR-536803 - Deploy airflow mcp server" · updated 2026-04-06T17:52Z · linked to NR-536803 · previously stale, now active

## Cross-References

> [!WARNING] Orphans
> **Unlinked PRs** — open PRs with no ticket reference:
> - [sjayaram/airflow-mcp-server #1](https://source.datanerd.us/dataos/airflow-mcp-server/pull/1) — "Initial GC and mcp server setup"
> - [karyan/dataos-otel #15](https://source.datanerd.us/dataos/dataos-otel/pull/15) — "changed scapping port"
> - [karyan/spark-operator #34](https://source.datanerd.us/dataos/spark-operator/pull/34) — "enabled pod monitor"
> - [karyan: 12+ older PRs (2025)](https://source.datanerd.us/dataos) — pre-2026, no ticket refs, bulk closure recommended
>
> **Unlinked tickets** — In Progress/In Review with no associated PR:
> - [NR-539892](https://new-relic.atlassian.net/browse/NR-539892) (Zach) — mesh downstream session creation, no PR found
> - [NR-539893](https://new-relic.atlassian.net/browse/NR-539893) (Zach) — mesh tool/call support, newly In Progress, no PR
> - [NR-536183](https://new-relic.atlassian.net/browse/NR-536183) (Kethan) — gateway health service, no PR found
> - [NR-542217](https://new-relic.atlassian.net/browse/NR-542217) (Shreya) — dbt Core MCP spike, no PR (spike — expected)
> - [NR-536803](https://new-relic.atlassian.net/browse/NR-536803) (Shreya) — Airflow MCP deploy, PR #69 exists and is now active

> [!ABSTRACT]- Connections
> | PR | Ticket | Confluence |
> |----|--------|------------|
> | [sjayaram/platform-ai #69](https://source.datanerd.us/dataos/platform-ai/pull/69) | [NR-536803](https://new-relic.atlassian.net/browse/NR-536803) | — |
> | [karyan/data-portal-telemetrygen #235](https://source.datanerd.us/dataos/data-portal-telemetrygen/pull/235) (merged) | — (unlinked) | — |
> | [sjayaram/airflow-mcp-server #1](https://source.datanerd.us/dataos/airflow-mcp-server/pull/1) | — (unlinked) | — |
> | [karyan/manual_snowflake_sql #400](https://source.datanerd.us/dataos/manual_snowflake_sql/pull/400) | NR-499435 (not in sprint) | — |

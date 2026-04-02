I have all the data I need. Now I'll build the cross-reference map and generate the output.

**Data summary:**
- Sprint: `E16MAR2026-DP`, Day 6 (started Mon Mar 16)
- Yesterday was Sunday Mar 22 → no Confluence edits, no GH PR activity
- Direct team: Zach (1 Closed, 1 In Progress), Kethan (2 In Progress + 1 Needs Review), Shreya (**all 6 tickets Backlog**)
- Broader team: Kaushik, Rakshith, Rohit, Saravana, Kumar Aryan all have In Review work
- GH stale PRs: karyan & ksarma have months-old open PRs; no PRs opened/merged yesterday
- No unlinked PR has ticket refs in most cases; many In Progress/In Review tickets have no visible PR

---
date: 2026-03-23
type: director-update
updateType: daily
sprint: E16MAR2026-DP
status: draft
summary: Shreya's MCP Tools work remains fully in Backlog at Day 6 of sprint with no active tickets assigned.
teams:
  - Data Platform
projects:
tags:
---

> [!INFO] Sprint
> **Sprint**: `=this.sprint` | **Day 6 of sprint**
> 
> Stevens Manual Notes:

> [!SUCCESS] Progress Delta
> **Tickets advanced**: No prior update available for comparison
> **Tickets regressed / blocked**: —
> **PRs opened**: No PR activity (yesterday was Sunday)
> **PRs merged**: No PR activity (yesterday was Sunday)
> **Blockers resolved**: —
> **New blockers**: —

## Yesterday
> [!CHECK] Direct Team
> Yesterday was Sunday — no activity expected.
> 
> As of Friday close:
> - **Zach** (Gateway Phase 0): [NR-536182](https://new-relic.atlassian.net/browse/NR-536182) gateway initial session support → Closed. [NR-536185](https://new-relic.atlassian.net/browse/NR-536185) mcp server registry service → In Progress
> - **Kethan** (Tool Registry + Docker Compose): [NR-536819](https://new-relic.atlassian.net/browse/NR-536819) MCP Tool Registry and [NR-536832](https://new-relic.atlassian.net/browse/NR-536832) Docker Compose + Deployment both In Progress
> - **Shreya** (MCP Tools): No active tickets — all 6 sprint tickets remain in Backlog ([NR-536823](https://new-relic.atlassian.net/browse/NR-536823) GitHub Tools, [NR-536824](https://new-relic.atlassian.net/browse/NR-536824) dbt Tools, [NR-536826](https://new-relic.atlassian.net/browse/NR-536826) Confluence+RAG, [NR-536828](https://new-relic.atlassian.net/browse/NR-536828) Local Orchestrator)

> [!WARNING] Blockers / Needs Attention
> - **Shreya — 0 active tickets at Day 6**: All MCP Tools tickets are Backlog. Needs tickets pulled into active states or clarification on scope.
> - **Zach — no PR linked to in-progress work**: [NR-536185](https://new-relic.atlassian.net/browse/NR-536185) mcp server registry service is In Progress with no visible PR in DataOS org.
> - **Kethan — stale PRs in GHE**: Has open PRs in `dataos/ml_digital_analytics_assistant` and `dataos/spark-kafka-apps` from mid-2025 that are unreviewed.

> [!ERROR]- Broader Team
> Activity as of Friday, summarized:
> - **Kaushik**: [NR-538272](https://new-relic.atlassian.net/browse/NR-538272) Noise Reduction Weekly Reports 2 (In Review), [NR-534170](https://new-relic.atlassian.net/browse/NR-534170) Noise Reduction Weekly Reports 1 (In Review); multiple AWS/DB stories In Progress
> - **Kumar Aryan**: [NR-538356](https://new-relic.atlassian.net/browse/NR-538356) A2Q PROD Test Expansion (In Review), [NR-534144](https://new-relic.atlassian.net/browse/NR-534144) Hero 1 (In Review)
> - **Rakshith**: [NR-533481](https://new-relic.atlassian.net/browse/NR-533481) Data Portal CAS UI Changes (In Review), [NR-531940](https://new-relic.atlassian.net/browse/NR-531940) CAS OpEx Dashboard (In Review)
> - **Rohit**: [NR-533482](https://new-relic.atlassian.net/browse/NR-533482) Data Portal Agentic UI Dev (In Review), [NR-532470](https://new-relic.atlassian.net/browse/NR-532470) Agents & Tools Dashboard (In Review)
> - **Saravana**: [NR-534174](https://new-relic.atlassian.net/browse/NR-534174) Hero 2 (In Review); Airflow Infra/Terraform/Deployment in review
> - **Veera**: Airflow Image & Deployment, E2E Testing, Observability — all In Progress, last updated Mar 18
> - **Shameek**: [NR-527999](https://new-relic.atlassian.net/browse/NR-527999) Platform v2 DBT OSS + Spark 4.0 In Progress, no update since Mar 12

## Today

> [!CHECK] Direct Team
> - **Zach**: Expected to continue [NR-536185](https://new-relic.atlassian.net/browse/NR-536185) mcp server registry service and pick up [NR-536186](https://new-relic.atlassian.net/browse/NR-536186) support mcp list/tools rpc method (Backlog)
> - **Kethan**: Drive [NR-536819](https://new-relic.atlassian.net/browse/NR-536819) and [NR-536832](https://new-relic.atlassian.net/browse/NR-536832) toward In Review; [NR-537141](https://new-relic.atlassian.net/browse/NR-537141) Work Intake updated today (Needs Review)
> - **Shreya**: Needs to pull at least one MCP Tools ticket into active state today

> [!QUESTION] Today's Focus
> - Confirm Shreya's MCP Tools sprint plan — are tickets properly scoped and ready to start?
> - Zach to open PR for [NR-536185](https://new-relic.atlassian.net/browse/NR-536185) to maintain traceability
> - Broader team: several In Review stories ripe for merge/close this week

> [!ERROR]- Broader Team
> - Kaushik active on AWS IAM + Snowflake DB pool work; Noise Reduction stories should close this week
> - Kumar Aryan: A2Q PROD expansion in review — needs reviewer attention
> - Rakshith: Data Portal CAS close to done — both stories In Review
> - Rohit: Agentic UI work approaching merge
> - Saravana: Airflow stack has several In Review items dating back to Mar 18 — need to close or identify blocker
> - Shameek: No activity since Mar 12 — follow up needed

## Activity

> [!TODO] Confluence Activity
> No pages modified in DATA space by direct team members on 2026-03-22 (Sunday). No Confluence activity to report.

> [!WARNING] GitHub — Stale PRs
> - [karyan — "Static alert" in data-portal-telemetrygen](https://source.datanerd.us/dataos/data-portal-telemetrygen/pull/224) — open since Mar 16, last updated Mar 17, no ticket link
> - [karyan — "Create v0.0.253_NR-499435_role_grant_access.sql"](https://source.datanerd.us/dataos/manual_snowflake_sql/pull/400) — open since Dec 2025, references NR-499435 (closed sprint)
> - [ksarma — "test commit" in ml_digital_analytics_assistant](https://source.datanerd.us/dataos/ml_digital_analytics_assistant/pull/312) — open since Aug 2025, no ticket link
> - Several additional karyan PRs open since mid-2025 across spark-kafka-apps, cube_dev, dosp-playground — all stale, no ticket links

> [!ERROR]- GitHub — PR Activity
> No PRs opened or merged by team members on 2026-03-22 (Sunday).
> 
> Most recent open PRs as of search time are all stale (last active Mar 17 at latest for karyan; Aug 2025 for ksarma).

## Cross-References

> [!WARNING] Orphans
> **Unlinked PRs** — open PRs with no ticket reference
> - [karyan — "Static alert"](https://source.datanerd.us/dataos/data-portal-telemetrygen/pull/224) (data-portal-telemetrygen) — no NR-* in title/body/branch
> - [ksarma — "test commit"](https://source.datanerd.us/dataos/ml_digital_analytics_assistant/pull/312) — no ticket ref
> - Multiple additional karyan stale PRs (cube_dev, dosp-playground, spark-kafka-apps) — no ticket refs
> 
> **Unlinked tickets** — In Progress/In Review with no PR
> - [NR-536185](https://new-relic.atlassian.net/browse/NR-536185) Zach — gateway mcp server registry (In Progress)
> - [NR-536819](https://new-relic.atlassian.net/browse/NR-536819) Kethan — MCP Tool Registry (In Progress)
> - [NR-536832](https://new-relic.atlassian.net/browse/NR-536832) Kethan — Docker Compose + Deployment (In Progress)
> - [NR-538272](https://new-relic.atlassian.net/browse/NR-538272) Kaushik — Noise Reduction Weekly Reports 2 (In Review)
> - [NR-534170](https://new-relic.atlassian.net/browse/NR-534170) Kaushik — Noise Reduction Weekly Reports 1 (In Review)
> - [NR-538356](https://new-relic.atlassian.net/browse/NR-538356) Kumar Aryan — A2Q PROD Test Expansion (In Review)
> - [NR-533481](https://new-relic.atlassian.net/browse/NR-533481) Rakshith — Data Portal CAS UI Changes (In Review)
> - [NR-531940](https://new-relic.atlassian.net/browse/NR-531940) Rakshith — CAS OpEx Dashboard (In Review)
> - [NR-533482](https://new-relic.atlassian.net/browse/NR-533482) Rohit — Data Portal Agentic UI Dev (In Review)
> - [NR-532470](https://new-relic.atlassian.net/browse/NR-532470) Rohit — Agents & Tools Dashboard (In Review)
> - [NR-534174](https://new-relic.atlassian.net/browse/NR-534174) Saravana — Hero 2 (In Review)

> [!ABSTRACT]- Connections
> | PR | Ticket | Confluence |
> |----|--------|------------|
> | [karyan — NR-499435 SQL](https://source.datanerd.us/dataos/manual_snowflake_sql/pull/400) | NR-499435 (prior sprint, closed) | — |
> | [ksarma — NR-379770 BCM projection](https://source.datanerd.us/dataos/ml_bcm_metric_projection/pull/17) | NR-379770 (prior sprint) | — |
> | All other open PRs | No ticket linkage found | No Confluence linkage found |

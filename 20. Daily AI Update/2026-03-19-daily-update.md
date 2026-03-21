---
date: 2026-03-19
type: director-update
updateType: daily
sprint: E16MAR2026-DP
status: draft
summary: Sprint E16MAR2026-DP launched yesterday with MCP Platform stories created across all three substreams; Zach has one story In Progress, Saravana's Airflow work advanced to In Review.
teams:
  - Data Platform
projects:
tags:
---

> [!INFO] Sprint
> **Sprint**: `=this.sprint` | **Day 2 of 10** (2026-03-18 → 2026-03-28)

## Yesterday

> [!CHECK] Direct Team
> - **Zach Schweinfurth**: [NR-536182](https://new-relic.atlassian.net/browse/NR-536182) gateway initial session support — In Progress; 3 additional gateway stories seeded to Backlog ([NR-536185](https://new-relic.atlassian.net/browse/NR-536185), [NR-536186](https://new-relic.atlassian.net/browse/NR-536186), [NR-536354](https://new-relic.atlassian.net/browse/NR-536354))
> - **Katta Kethan Sarma**: Sprint tickets created — [NR-536819](https://new-relic.atlassian.net/browse/NR-536819) Tool Registry, [NR-536832](https://new-relic.atlassian.net/browse/NR-536832) Docker Compose Deployment (Backlog)
> - **Shetty Shreya Jayaram**: Sprint tickets created — [NR-536823](https://new-relic.atlassian.net/browse/NR-536823) GitHub Tools, [NR-536824](https://new-relic.atlassian.net/browse/NR-536824) dbt Tools, [NR-536826](https://new-relic.atlassian.net/browse/NR-536826) Confluence+RAG, [NR-536828](https://new-relic.atlassian.net/browse/NR-536828) Local Orchestrator (all Backlog)

> [!WARNING] Blockers / Needs Attention
> - 8 of 9 direct-team sprint tickets still in Backlog — expected for Day 1 sprint kickoff, but team should pull stories into Dev today
> - No PRs opened yet for any active sprint work

> [!ERROR]- Broader Team
> - **Saravana Kumar Angamuthu**: [NR-533900](https://new-relic.atlassian.net/browse/NR-533900) Airflow Infra/Pre-reqs, [NR-533898](https://new-relic.atlassian.net/browse/NR-533898) Terraform Codes, [NR-529194](https://new-relic.atlassian.net/browse/NR-529194) Airflow Deployment — all advanced to In Review
> - **Veera Sekhar Kodavali**: 4 Airflow/Hero stories In Progress — [NR-534177](https://new-relic.atlassian.net/browse/NR-534177) Hero 3, [NR-533905](https://new-relic.atlassian.net/browse/NR-533905) Image & Deployment, [NR-533928](https://new-relic.atlassian.net/browse/NR-533928) E2E Testing, [NR-533929](https://new-relic.atlassian.net/browse/NR-533929) Observability
> - **Kaushik Kallichetty**: [NR-533927](https://new-relic.atlassian.net/browse/NR-533927) New DEV Database setup — Backlog

## Today

> [!CHECK] Direct Team
> - **Zach**: Continue [NR-536182](https://new-relic.atlassian.net/browse/NR-536182) (gateway session/Redis); pull additional gateway stories into Dev
> - **Katta**: Begin [NR-536819](https://new-relic.atlassian.net/browse/NR-536819) Tool Registry scaffolding; set up Docker Compose skeleton
> - **Shreya**: Begin GitHub and dbt MCP tool implementation

> [!QUESTION] Today's Focus
> MCP Platform Day 2: team transitions from ticket creation to active development across all three substreams (Gateway, Tool Registry, MCP Tools). Expect first PRs to appear.

> [!ERROR]- Broader Team
> - **Saravana**: Airflow PRs awaiting review/merge across 3 In Review stories
> - **Veera**: Continuing Airflow E2E testing, observability, and image deployment progress

## Activity

> [!TODO] Confluence Activity
> Nothing to report — no pages modified in DATA space yesterday by direct team members

> [!WARNING] GitHub — Stale PRs
> - **Kumar Aryan (karyan)**: 20 open PRs in DataOS org with no activity since Dec 2025 or earlier. Repos: `manual_snowflake_sql`, `cube_dev`, `spark-kafka-apps`, `dosp-playground`, `digital-assistant-vector-index`, `trino-query-engine`, others. Needs triage/closure.

> [!ERROR]- GitHub — PR Activity
> Nothing to report — no open PRs updated and no merges yesterday (sprint Day 1)

## Cross-References

> [!WARNING] Orphans
> **Unlinked PRs** — karyan's 20 stale PRs have empty bodies or PR-template placeholders with no real ticket references
> **Unlinked tickets** — All In Progress/In Review sprint tickets lack associated PRs: [NR-536182](https://new-relic.atlassian.net/browse/NR-536182), [NR-533900](https://new-relic.atlassian.net/browse/NR-533900), [NR-533898](https://new-relic.atlassian.net/browse/NR-533898), [NR-529194](https://new-relic.atlassian.net/browse/NR-529194), [NR-534177](https://new-relic.atlassian.net/browse/NR-534177), [NR-533905](https://new-relic.atlassian.net/browse/NR-533905), [NR-533928](https://new-relic.atlassian.net/browse/NR-533928), [NR-533929](https://new-relic.atlassian.net/browse/NR-533929)

> [!ABSTRACT]- Connections
> | PR | Ticket | Confluence |
> |----|--------|------------|
> | karyan: [Create v0.0.253_NR-499435_role_grant_access.sql](https://source.datanerd.us/dataos/manual_snowflake_sql/pull/400) (stale, Dec 2025) | NR-499435 (not in active sprint) | — |

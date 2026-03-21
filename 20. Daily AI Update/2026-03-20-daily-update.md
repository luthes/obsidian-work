---
date: 2026-03-20
type: director-update
updateType: daily
sprint: E16MAR2026-DP
status: draft
summary: Day 3 of sprint and Katta and Shreya still have all stories in Backlog — no progress since ticket creation on Day 1; Zach continues as the only direct-team member actively in development.
teams:
  - Data Platform
projects:
tags:
---

> [!INFO] Sprint
> **Sprint**: `=this.sprint` | **Day 3 of 10** (2026-03-18 → 2026-03-28)

> [!SUCCESS] Progress Delta
> **Tickets advanced**: [NR-537877](https://new-relic.atlassian.net/browse/NR-537877) — Create a terraform user for AWS account (Backlog → In Progress, Kaushik Kallichetty)
> **Tickets regressed / blocked**: None
> **PRs opened**: None
> **PRs merged**: None yesterday; karyan merged [tf-dataos-aws#246](https://source.datanerd.us/dataos/tf-dataos-aws/pull/246) ("added s3 bucket") this morning (2026-03-20, no ticket reference)
> **Blockers resolved**: None — Day 1 blocker (Katta/Shreya stories in Backlog) persists into Day 3
> **New blockers**: Katta and Shreya have had zero story movement through Day 3 — sprint execution risk

## Yesterday

> [!CHECK] Direct Team
> - **Zach Schweinfurth**: [NR-536182](https://new-relic.atlassian.net/browse/NR-536182) gateway initial session support — still In Progress, no status change; [NR-536185](https://new-relic.atlassian.net/browse/NR-536185), [NR-536186](https://new-relic.atlassian.net/browse/NR-536186), [NR-536354](https://new-relic.atlassian.net/browse/NR-536354) remain Backlog
> - **Katta Kethan Sarma**: No activity — [NR-536819](https://new-relic.atlassian.net/browse/NR-536819) Tool Registry and [NR-536832](https://new-relic.atlassian.net/browse/NR-536832) Docker Compose still in Backlog
> - **Shetty Shreya Jayaram**: No activity — [NR-536823](https://new-relic.atlassian.net/browse/NR-536823), [NR-536824](https://new-relic.atlassian.net/browse/NR-536824), [NR-536826](https://new-relic.atlassian.net/browse/NR-536826), [NR-536828](https://new-relic.atlassian.net/browse/NR-536828) all remain Backlog

> [!WARNING] Blockers / Needs Attention
> - **Katta and Shreya — Day 3, zero movement**: Both engineers have had no story activity since tickets were seeded on Day 1. At Day 3 this is an active sprint execution risk — need confirmation they are working and pulling stories today
> - **No PRs for any active sprint work**: Still no code submitted across the entire direct team

> [!ERROR]- Broader Team
> - **Kaushik Kallichetty**: [NR-537877](https://new-relic.atlassian.net/browse/NR-537877) Create a terraform user for AWS account — newly In Progress (updated 2026-03-19)
> - **Saravana Kumar Angamuthu**: [NR-533900](https://new-relic.atlassian.net/browse/NR-533900), [NR-533898](https://new-relic.atlassian.net/browse/NR-533898), [NR-529194](https://new-relic.atlassian.net/browse/NR-529194) remain In Review — no change; [NR-534174](https://new-relic.atlassian.net/browse/NR-534174) Hero 2 and [NR-534173](https://new-relic.atlassian.net/browse/NR-534173) Operational Excellence Weekly Reports also In Progress
> - **Veera Sekhar Kodavali**: [NR-534177](https://new-relic.atlassian.net/browse/NR-534177), [NR-533905](https://new-relic.atlassian.net/browse/NR-533905), [NR-533928](https://new-relic.atlassian.net/browse/NR-533928), [NR-533929](https://new-relic.atlassian.net/browse/NR-533929) — all remain In Progress, no change

## Today

> [!CHECK] Direct Team
> - **Zach**: Continue [NR-536182](https://new-relic.atlassian.net/browse/NR-536182); open first PR for gateway session work
> - **Katta**: Must pull [NR-536819](https://new-relic.atlassian.net/browse/NR-536819) Tool Registry into Dev today — Day 3 is the latest acceptable start
> - **Shreya**: Must pull at least [NR-536823](https://new-relic.atlassian.net/browse/NR-536823) GitHub Tools into Dev today

> [!QUESTION] Today's Focus
> Sprint execution gap: Katta and Shreya need to begin active development immediately. Priority is confirming both engineers are unblocked and have stories in flight before EOD. Saravana's Airflow In Review tickets need a reviewer assigned.

> [!ERROR]- Broader Team
> - **Saravana**: Three stories In Review ([NR-533900](https://new-relic.atlassian.net/browse/NR-533900), [NR-533898](https://new-relic.atlassian.net/browse/NR-533898), [NR-529194](https://new-relic.atlassian.net/browse/NR-529194)) awaiting review/merge — confirm reviewers are assigned
> - **Veera**: Continuing Airflow E2E testing, observability, image deployment

## Activity

> [!TODO] Confluence Activity
> Nothing to report — no pages modified in DATA space yesterday by direct team members

> [!WARNING] GitHub — Stale PRs
> - **Kumar Aryan (karyan)**: ~20 open PRs with no activity since Dec 2025 or earlier across `manual_snowflake_sql`, `cube_dev`, `spark-kafka-apps`, `dosp-playground`, `digital-assistant-vector-index`, `trino-query-engine`, and others — still unresolved, same as yesterday; needs triage/closure

> [!ERROR]- GitHub — PR Activity
> - No open PRs updated by any team member yesterday
> - **karyan** merged [tf-dataos-aws#246](https://source.datanerd.us/dataos/tf-dataos-aws/pull/246) "added s3 bucket" this morning (2026-03-20T13:46Z) — empty body, no ticket reference

## Cross-References

> [!WARNING] Orphans
> **Unlinked PRs** — [karyan tf-dataos-aws#246](https://source.datanerd.us/dataos/tf-dataos-aws/pull/246) "added s3 bucket" (empty body, no ticket); karyan's ~20 stale open PRs remain unlinked
> **Unlinked tickets** — All In Progress/In Review sprint tickets lack associated PRs: [NR-536182](https://new-relic.atlassian.net/browse/NR-536182), [NR-533900](https://new-relic.atlassian.net/browse/NR-533900), [NR-533898](https://new-relic.atlassian.net/browse/NR-533898), [NR-529194](https://new-relic.atlassian.net/browse/NR-529194), [NR-534177](https://new-relic.atlassian.net/browse/NR-534177), [NR-533905](https://new-relic.atlassian.net/browse/NR-533905), [NR-533928](https://new-relic.atlassian.net/browse/NR-533928), [NR-533929](https://new-relic.atlassian.net/browse/NR-533929)

> [!ABSTRACT]- Connections
> | PR | Ticket | Confluence |
> |----|--------|------------|
> | karyan: [tf-dataos-aws#246 "added s3 bucket"](https://source.datanerd.us/dataos/tf-dataos-aws/pull/246) (merged 2026-03-20, empty body) | None | — |

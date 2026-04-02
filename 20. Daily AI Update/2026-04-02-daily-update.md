---
date: 2026-04-02
type: director-update
updateType: daily
sprint: E30MAR2026-DP
status: draft
summary: Shreya moved Airflow service account to In Review; Zach continuing mesh http pooling; Kethan has no In Progress items with sprint half elapsed.
teams:
  - Data Platform
projects:
tags:
---

> [!INFO] Sprint
> **Sprint**: `=this.sprint` | **Day 4 of 10** (2026-03-30 → 2026-04-11)
> 
> Stevens Manual Notes:

> [!SUCCESS] Progress Delta
> **Tickets advanced**: No prior update available for comparison
> **Tickets regressed / blocked**: —
> **PRs opened**: —
> **PRs merged**: —
> **Blockers resolved**: —
> **New blockers**: —
## Yesterday
> [!CHECK] Direct Team
> - **Zach** — [NR-538795](https://new-relic.atlassian.net/browse/NR-538795) mesh 0.1: http pooling + downstream session model changes (In Progress, updated)
> - **Shreya** — [NR-536203](https://new-relic.atlassian.net/browse/NR-536203) Airflow service account (Viewer role) moved to In Review; [NR-541901](https://new-relic.atlassian.net/browse/NR-541901) Work Intake ticket updated (Needs Review)
> - **Kethan** — No ticket activity; all 6 sprint stories remain in Backlog (none In Progress)
> - **Steven** — SLC Reviews in progress: [NR-542145](https://new-relic.atlassian.net/browse/NR-542145) Gateway Auth, [NR-542144](https://new-relic.atlassian.net/browse/NR-542144) Airflow MCP, [NR-542143](https://new-relic.atlassian.net/browse/NR-542143) dbt MCP

> [!WARNING] Blockers / Needs Attention
> - **Kethan** — All sprint stories still in Backlog at Day 4 of 10. No In Progress items. Needs triage/check-in.
> - **Kumar Aryan** — [PR: "Static alerts"](https://source.datanerd.us/dataos/data-portal-telemetrygen/pull/230) open since 2026-03-26, updated yesterday, no ticket linked. Multiple additional stale PRs (some from Dec 2025).

> [!ERROR]- Broader Team
> - **Rakshith** — [NR-540117](https://new-relic.atlassian.net/browse/NR-540117) Data Portal UI via Claude → In Review; [NR-540114](https://new-relic.atlassian.net/browse/NR-540114) Analytics Work → In Review
> - **Rohit** — [NR-540129](https://new-relic.atlassian.net/browse/NR-540129) Data Portal Agentic UI → In Review; [NR-540134](https://new-relic.atlassian.net/browse/NR-540134) Claude Integration continuing (In Progress)
> - **Shameek** — [NR-541896](https://new-relic.atlassian.net/browse/NR-541896) Platform v2: Spark-Jupyter POC → In Review
> - **Kumar Aryan** — [NR-543415](https://new-relic.atlassian.net/browse/NR-543415) A2Q Alerts Tuning updated (In Progress)
> - **Veera** — [NR-541444](https://new-relic.atlassian.net/browse/NR-541444) Japan DC info gathering, [NR-541442](https://new-relic.atlassian.net/browse/NR-541442) Airflow Support, [NR-541443](https://new-relic.atlassian.net/browse/NR-541443) Game Day all updated (In Progress)

## Today

> [!CHECK] Direct Team
> - **Zach** — Complete NR-538795 (http pooling); begin session creation/mgmt backlog items
> - **Shreya** — Progress [NR-536803](https://new-relic.atlassian.net/browse/NR-536803) Astro Airflow MCP Server Deployment; address NR-536203 review feedback
> - **Kethan** — Move sprint backlog items into In Progress (spike on dbt MCP hosting + staging Redis cluster)
> - **Steven** — Advance SLC reviews; check in with Kethan

> [!QUESTION] Today's Focus
> - Kethan sprint backlog concern — needs sync to unblock before mid-sprint
> - SLC reviews for Airflow, dbt, and Gateway Auth MCP servers (3 open, all In Progress)
> - Broader team: 4 stories pending In Review across Rakshith, Rohit, Shameek — watch for review bottleneck

> [!ERROR]- Broader Team
> - **Kaushik** — IAM automation stories (NR-541436, NR-541437, NR-541438 cluster) In Progress; NR-541860 Operational Excellence in In Review
> - **Saravana** — 4 IAM/AWS account stories all In Progress (NR-541438–NR-541441)
> - **Sumedh** — Multiple Data Portal stories In Progress (NR-540140–NR-540145); NR-540151 Hero 2 updated today
> - **Rohit** — NR-528110 Work Intake flow request In Review (updated today)

## Activity

> [!TODO] Confluence Activity
> Nothing to report — no pages modified in DATA space by direct team members on 2026-04-01.

> [!WARNING] GitHub — Stale PRs
> All stale PRs are from **Kumar Aryan (karyan)**. No stale PRs from direct sprint team.
> - [changed scapping port](https://source.datanerd.us/dataos/dataos-otel/pull/15) — dataos-otel, last updated 2026-03-29
> - [enabled pod monitor](https://source.datanerd.us/dataos/spark-operator/pull/34) — spark-operator, last updated 2026-03-26
> - [Create v0.0.253_NR-499435_role_grant_access.sql](https://source.datanerd.us/dataos/manual_snowflake_sql/pull/400) — manual_snowflake_sql, last updated **2025-12-09** (4 months stale)
> - Multiple additional stale PRs in cube_dev, dosp-playground, spark-kafka-apps from mid-2025

> [!ERROR]- GitHub — PR Activity
> **Open PRs updated yesterday (2026-04-01):**
> - [Static alerts](https://source.datanerd.us/dataos/data-portal-telemetrygen/pull/230) — karyan, data-portal-telemetrygen, open since 2026-03-26, no ticket linked
>
> **Merged yesterday:** None

## Cross-References

> [!WARNING] Orphans
> **Unlinked PRs** — open PRs with no ticket reference
> - [Static alerts](https://source.datanerd.us/dataos/data-portal-telemetrygen/pull/230) (karyan) — no NR-\d+ in title or body
> - [changed scapping port](https://source.datanerd.us/dataos/dataos-otel/pull/15) (karyan) — empty body, no ticket
> - [enabled pod monitor](https://source.datanerd.us/dataos/spark-operator/pull/34) (karyan) — empty body, no ticket
>
> **Unlinked tickets** — In Progress/In Review with no PR
> - [NR-538795](https://new-relic.atlassian.net/browse/NR-538795) Zach — mesh http pooling (In Progress)
> - [NR-536203](https://new-relic.atlassian.net/browse/NR-536203) Shreya — Airflow service account (In Review)
> - [NR-536803](https://new-relic.atlassian.net/browse/NR-536803) Shreya — Astro Airflow MCP deployment (In Progress)
> - [NR-541896](https://new-relic.atlassian.net/browse/NR-541896) Shameek — Spark-Jupyter POC (In Review)
> - [NR-540117](https://new-relic.atlassian.net/browse/NR-540117) / [NR-540114](https://new-relic.atlassian.net/browse/NR-540114) Rakshith — Data Portal/Analytics (In Review)
> - [NR-540129](https://new-relic.atlassian.net/browse/NR-540129) Rohit — Agentic UI (In Review)

> [!ABSTRACT]- Connections
> | PR | Ticket | Confluence |
> |----|--------|------------|
> | [Create v0.0.253_NR-499435…](https://source.datanerd.us/dataos/manual_snowflake_sql/pull/400) (karyan, Dec 2025, stale) | [NR-499435](https://new-relic.atlassian.net/browse/NR-499435) (referenced in body) | — |
> | All other team PRs | No cross-reference found | — |

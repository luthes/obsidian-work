---
date: 2026-03-31
type: director-update
updateType: daily
sprint: E30MAR2026-DP
status: draft
summary: Shetty closed the Airflow MCP deployment ticket and published the Phase-0 demo recording on day 1 of sprint E30MAR2026-DP, marking completion of the MCP Phase 0 milestone.
teams:
  - Data Platform
projects:
tags:
---

> [!INFO] Sprint
> **Sprint**: `=this.sprint` | **Day 2 of sprint** (2026-03-30 → 2026-04-10, 40 SP committed)
>
> Stevens Manual Notes:

> [!SUCCESS] Progress Delta
> **Tickets advanced**: No prior update available for comparison.
> **Tickets regressed / blocked**: —
> **PRs opened**: —
> **PRs merged**: —
> **Blockers resolved**: —
> **New blockers**: —

## Yesterday

> [!CHECK] Direct Team
>
> - **Shetty Shreya Jayaram**: Closed [NR-540731](https://new-relic.atlassian.net/browse/NR-540731) (Airflow MCP: Server Deployment with Airflow v3). Published [Phase-0: Demo Recording](https://newrelic.atlassian.net/wiki/spaces/DATA/pages/5380964520) on Confluence with a full video walkthrough covering Airflow MCP + DBT tools integration.
> - **Zach Schweinfurth**: [NR-539870](https://new-relic.atlassian.net/browse/NR-539870) In Progress — mesh CI/CD pipeline (lint + unit tests). No PR activity.
> - **Katta Kethan Sarma**: No In Progress tickets — all sprint items remain in Backlog.

> [!WARNING] Blockers / Needs Attention
>
> - **Katta has zero In Progress tickets** on sprint day 1. Sprint items (Docker Compose deploy, MCP Registry) still in Backlog — needs a kickoff.
> - **3 SLC reviews** ([NR-542143](https://new-relic.atlassian.net/browse/NR-542143), [NR-542144](https://new-relic.atlassian.net/browse/NR-542144), [NR-542145](https://new-relic.atlassian.net/browse/NR-542145)) assigned to Steven Luther are Backlog — need scheduling before MCP servers progress further.

> [!ERROR]- Broader Team
>
> - **Kumar Aryan**: Merged 2 PRs in `dbt-thrift-servers` ([Update spark_application.yaml](https://source.datanerd.us/dataos/dbt-thrift-servers/pull/77), [enabling metrics](https://source.datanerd.us/dataos/dbt-thrift-servers/pull/63)); published [DBT Core - Spark Observability](https://newrelic.atlassian.net/wiki/spaces/DATA/pages/5379686588) Confluence page. [NR-541874](https://new-relic.atlassian.net/browse/NR-541874), [NR-540110](https://new-relic.atlassian.net/browse/NR-540110) In Progress.
> - **Veera Sekhar Kodavali**: Published [Vault Secrets](https://newrelic.atlassian.net/wiki/spaces/DATA/pages/5378113628) page documenting Japan DC Vault setup.
> - **Saravana Kumar Angamuthu**: Comment on [Lakehouse AWS Accounts](https://newrelic.atlassian.net/wiki/spaces/DATA/pages/5095063802); 4 IAM/AWS tickets In Progress ([NR-541438](https://new-relic.atlassian.net/browse/NR-541438)–[NR-541441](https://new-relic.atlassian.net/browse/NR-541441)).
> - **Kaushik Kallichetty**: [NR-541860](https://new-relic.atlassian.net/browse/NR-541860) In Review (Operational Excellence Weekly Reports); 4 IAM automation tickets In Progress.
> - **Rakshith Lakshmikantha** / **Rohit Ghosh** / **Sumedh Rotti**: Data Portal work advancing across multiple In Progress tickets (STG/PROD deploy, Agentic UI, release notes).
> - **Shameek Agarwal**: [NR-541896](https://new-relic.atlassian.net/browse/NR-541896) In Progress (Spark Jupyter POC); Platform v2 onboarding tickets active.

## Today

> [!CHECK] Direct Team
>
> - **Shetty**: Expected to move to [NR-540734](https://new-relic.atlassian.net/browse/NR-540734) (Airflow MCP: Tool Validation & Integration Testing) and [NR-540733](https://new-relic.atlassian.net/browse/NR-540733) (Mesh Config & Registration).
> - **Zach**: Continuing [NR-539870](https://new-relic.atlassian.net/browse/NR-539870) — mesh CI/CD pipeline.
> - **Katta**: Should pick up first sprint item from Backlog (likely [NR-540735](https://new-relic.atlassian.net/browse/NR-540735) — Gateway: Deploy MCP Mesh to Staging Cells or [NR-536176](https://new-relic.atlassian.net/browse/NR-536176) — Redis cluster).

> [!QUESTION] Today's Focus
>
> - Phase 0 → Phase 1 gate: Shreya's Airflow MCP closed; next milestone is mesh registration + tool validation.
> - SLC reviews for MCP servers need to be scheduled by Steven Luther.
> - Katta sprint kickoff — needs to pull in first task.

> [!ERROR]- Broader Team
>
> - Kumar Aryan: Continuing dbt + Spark observability work.
> - Data Portal team (Rakshith, Rohit, Sumedh): STG/PROD deployments and Agentic UI in progress.
> - Kaushik / Saravana: AWS IAM automation continuing.

## Activity

> [!TODO] Confluence Activity
>
> - **Shetty Shreya Jayaram**: [Phase-0: Demo Recording](https://newrelic.atlassian.net/wiki/spaces/DATA/pages/5380964520) — Phase 0 MCP demo documentation + video upload (Airflow MCP + DBT tools)
> - **Kumar Aryan**: [DBT Core - Spark Observability](https://newrelic.atlassian.net/wiki/spaces/DATA/pages/5379686588) — new page covering Spark Thrift JMX metric pipeline
> - **Veera Sekhar Kodavali**: [Vault Secrets](https://newrelic.atlassian.net/wiki/spaces/DATA/pages/5378113628) — Japan DC Vault secrets inventory (Claude-assisted)
> - **Steven Luther**: [FY26Q4 Sprint Plan - E30MAR2026-DP](https://newrelic.atlassian.net/wiki/spaces/DATA/pages/5365596164) — sprint plan page updated (40 SP, 2026-03-30 → 2026-04-10)
> - **Saravana Kumar Angamuthu**: Comment on [Lakehouse AWS Accounts](https://newrelic.atlassian.net/wiki/spaces/DATA/pages/5095063802) — asking about historical Glue call data

> [!WARNING] GitHub — Stale PRs
>
> - karyan (Kumar Aryan) has multiple stale open PRs with no ticket references:
>   - [Static alerts](https://source.datanerd.us/dataos/data-portal-telemetrygen/pull/230) — `data-portal-telemetrygen`, last updated 2026-03-26
>   - [enabled pod monitor](https://source.datanerd.us/dataos/spark-operator/pull/34) — `spark-operator`, last updated 2026-03-26
>   - [Create v0.0.253_NR-499435_role_grant_access.sql](https://source.datanerd.us/dataos/manual_snowflake_sql/pull/400) — `manual_snowflake_sql`, open since Dec 2025
>   - Several PRs in `cube_dev`, `dosp-playground`, `test-data-platform`, `spark-kafka-apps` from mid-2025 — likely abandoned

> [!ERROR]- GitHub — PR Activity
> **Merged (2026-03-30):**
>
> - [Update spark_application.yaml](https://source.datanerd.us/dataos/dbt-thrift-servers/pull/77) — karyan → `dbt-thrift-servers` (no ticket ref)
> - [enabling metrics](https://source.datanerd.us/dataos/dbt-thrift-servers/pull/63) — karyan → `dbt-thrift-servers` (no ticket ref)
>
> **Opened (2026-03-30):** None

## Cross-References

> [!WARNING] Orphans
> **Unlinked PRs** — open PRs with no ticket reference
>
> - All stale karyan PRs listed above contain no `NR-` or `ENTERPRISE-` references
> - Both merged karyan PRs have empty bodies — no ticket linkage
>
> **Unlinked tickets** — In Progress/In Review with no PR
>
> - [NR-539870](https://new-relic.atlassian.net/browse/NR-539870) (Zach — mesh CI/CD) — In Progress, no PR found
> - [NR-541874](https://new-relic.atlassian.net/browse/NR-541874) / [NR-540110](https://new-relic.atlassian.net/browse/NR-540110) (Kumar Aryan — dbt/Spark observability) — merged PRs have no ticket ref
> - Most Data Portal In Progress tickets (Rakshith, Rohit, Sumedh) — no PRs found in DataOS org

> [!ABSTRACT]- Connections
>
> | PR | Ticket | Confluence |
> |----|--------|------------|
> | [Update spark_application.yaml](https://source.datanerd.us/dataos/dbt-thrift-servers/pull/77) (karyan, merged) | None found | [DBT Core - Spark Observability](https://newrelic.atlassian.net/wiki/spaces/DATA/pages/5379686588) (inferred) |
> | [enabling metrics](https://source.datanerd.us/dataos/dbt-thrift-servers/pull/63) (karyan, merged) | None found | [DBT Core - Spark Observability](https://newrelic.atlassian.net/wiki/spaces/DATA/pages/5379686588) (inferred) |
> | — | [NR-540731](https://new-relic.atlassian.net/browse/NR-540731) Closed (Shreya — Airflow MCP deploy) | [Phase-0: Demo Recording](https://newrelic.atlassian.net/wiki/spaces/DATA/pages/5380964520) |
> | — | [NR-539870](https://new-relic.atlassian.net/browse/NR-539870) In Progress (Zach — mesh CI/CD) | — |

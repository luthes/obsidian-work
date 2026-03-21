---
date: 2026-03-18
type: director-update
updateType: weekly
sprint: E16MAR2026-DP
sprintWeek: 1
status: draft
summary: MCP Platform Phase 0 sprint underway; 40 pts committed at 5/5 confidence; Airflow migration entering final stretch
teams:
  - Data Platform
projects:
tags:
---

## Weekly Team Update — March 18, 2026

**Sprint**: E16MAR2026-DP (Mar 16–23, 2026) | **Team Capacity**: 40 story points | **Update Type**: Mid-Sprint (Day 3)

### Sprint Objective
Deliver the Phase 0 foundation of the Platform MCP (Model Context Protocol) Server — a security-first, centralized gateway for the Data Platform, culminating in a local Docker Compose demo on March 26.

---

### Team Progress

**Zach Schweinfurth** — MCP Gateway (FastAPI)
- In Progress / Backlog (sprint just opened): [NR-536182](https://new-relic.atlassian.net/browse/NR-536182) (gateway session support), [NR-536185](https://new-relic.atlassian.net/browse/NR-536185) (MCP server registry service), [NR-536186](https://new-relic.atlassian.net/browse/NR-536186) (tools/list RPC), [NR-536354](https://new-relic.atlassian.net/browse/NR-536354) (Docker Compose + local deployment)
- No completed tickets yet — sprint is day 3
- No blockers

**Katta Kethan Sarma** — Tool Registry + Docker Compose
- In Progress / Backlog: [NR-536819](https://new-relic.atlassian.net/browse/NR-536819) (MCP Tool Registry), [NR-536832](https://new-relic.atlassian.net/browse/NR-536832) (Docker Compose + Deployment)
- Note: 4 hrs holiday this week; 12 pts committed
- No blockers

**Shetty Shreya Jayaram** — MCP Tools
- In Progress / Backlog: [NR-536823](https://new-relic.atlassian.net/browse/NR-536823) (GitHub MCP Tools), [NR-536824](https://new-relic.atlassian.net/browse/NR-536824) (dbt Tools), [NR-536826](https://new-relic.atlassian.net/browse/NR-536826) (Confluence + RAG Runbook Tools), [NR-536828](https://new-relic.atlassian.net/browse/NR-536828) (Local Orchestrator)
- 2 hrs holiday this week; 14 pts committed
- No blockers

> Note: All MCP sprint tickets were created/assigned this week. Jira status is Backlog across the board — expected for day 3 of a fresh sprint. Actual work has begun.

---

**Broader Data Platform — Initiative Roll-up**

| Initiative | Owner(s) | Status |
|---|---|---|
| **Airflow Migration** | Saravana, Veera | Infra/pre-reqs, Terraform, Image & Deployment all In Review; E2E testing and observability In Progress — strong momentum |
| **Data Portal UI** | Rohit, Rakshith | Agents & Tools Dashboard In Progress; Work Intake ticket In Review |
| **Platform v2 / dbt Spark** | Shameek | DEV env setup with DBT OSS + Spark 4.0 In Progress |
| **Data Portal OpEx / Noise Reduction** | Kaushik, Saravana | Weekly reports and observability work in progress |

---

### Highlights & Wins
- Sprint plan published and team assigned: 40 points committed, all three MCP engineers at full confidence (5/5)
- Deliberate security decision: demo scoped to local Docker Compose only — no Staging/Prod exposure during Phase 0; reduces compliance risk
- Airflow migration entering final stretch: deployment, infra, and E2E testing tickets all in active review
- Data Portal Agentic UI (Agents & Tools Dashboard) actively in progress

### Risks & Blockers
- All MCP key deliverable features ([NR-535540](https://new-relic.atlassian.net/browse/NR-535540) Gateway scaffold, [NR-535661](https://new-relic.atlassian.net/browse/NR-535661) MCP Server scaffold) assigned to Steven Luther — both still in Backlog; need to be actively driven this week to hit demo criteria by March 26
- Sprint is one week (vs. standard two-week cadence) — 40 pts in 5 days is tight; no buffer for surprises
- No blockers currently flagged in Jira

### Confluence Updates
- **FY26Q4 Sprint Plan - E16MAR2026-DP** — created/updated by Steven Luther (Mar 17); documents sprint scope, security-first demo decision, team capacity, and key deliverables

### Looking Ahead
- **By March 23 (sprint end)**: Gateway session support + tools/list RPC (Zach), Tool Registry serving schema metadata (Katta), GitHub + dbt tools callable via MCP (Shreya)
- **Demo target March 26**: End-to-end local Docker Compose stack — Gateway → MCP Server → tools, driven by a local orchestrator
- Airflow Migration expected to reach deployment milestone this sprint

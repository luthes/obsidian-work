Platform V2

Platform V2 Aims to:
- Eliminate Snowflake as a primary compute engine
- Standardize Apache Iceberg as the data lake across all data zones
- Use Spark + dbt Fusion as the primary transformation engine
- Preserve (or create) strong developer experience and cost controls
- Unified UI and Agentic AI Layer for discoverability, operations, and self service

Non Goals:
- Complete [[Snowflake]] feature parity
- Support multiple SQL dialects (Trino, Spark, Postgres, Snowflake, etc)
- Replace BI Layer

Jira Epic - [https://new-relic.atlassian.net/browse/NR-506742](https://new-relic.atlassian.net/browse/NR-506742)

Other Docs:
- [https://docs.google.com/document/d/16PxwigPBOhagkyHMlnl1-MoY7hfqlX_AQmWP51zRC_E/edit?tab=t.0#heading=h.opp2cn109vsi](https://docs.google.com/document/d/16PxwigPBOhagkyHMlnl1-MoY7hfqlX_AQmWP51zRC_E/edit?tab=t.0#heading=h.opp2cn109vsi)
- [https://docs.google.com/spreadsheets/d/1wDZDjQ5D5SqUU0C_iN34yKsIrHxtLr5KMlGLmQCYrII/edit?gid=654586140#gid=654586140](https://docs.google.com/spreadsheets/d/1wDZDjQ5D5SqUU0C_iN34yKsIrHxtLr5KMlGLmQCYrII/edit?gid=654586140#gid=654586140)

## 2. Core Architecture

### 2.1 Storage Layer

Generally we should support more Iceberg features. Currently we use Apache Iceberg just a flat data store, and we don’t use (explicitly) schema evolution, snapshots, or time travel, even though they’re features of [[Apache Iceberg]].
#### Apache Iceberg (Upgrade to v3)

- [Docs](https://iceberg.apache.org/), [Blog](https://www.ryft.io/blog/apache-iceberg-v3-is-it-ready)
- Single storage format for all zones (Raw, Conformed, Transformed)
- S3 Object Storage + Glue Data Catalog
- Support Schema Evolution, Snapshots and Time Travel (UI things here?)

### 2.2. Ingestion Layer

There isn’t much at this point we can do to reduce costs for Kafka Connect. Most of the cost comes from billing topics, and those aren’t going anywhere. We do, however, have a need to move the Compacted topics off of Kafka Connect if Iceberg will become the de facto storage layer. Fivetran is the best solution there, as there is no (current) plan to move off of Fivetran.

#### Kafka Connect
- Stream from Kafka to Raw Layer (Same as current)
- Standardized configs + naming conventions
- Move Compacted Topics to Fivetran (DB → Iceberg, rather than DB  →  KC  →  Iceberg)

#### Fivetran
- DB to Iceberg
- Lands data directly to Raw Zone

#### Ingestion Wishlist
- Unified metadata for all ingestions jobs (Kafka Connect, Fivetran in Open Metadata)
- Standardized and Documented Raw -> Conformed -> Transformed promotion patterns.
- Self-service on Fivetran Job Creation (Data Portal?)
- Better/Centralized Ingestion Observability

### 2.3 Transformation and Compute Layer

Our greatest cost savings are going to come from removing transformations from Snowflake. Transformations running in warehouses are our biggest cost in Snowflake, storage coming in second.  My guess is that over 60% of tables in Snowflake are not used, anyways, so migrating from Snowflake to Iceberg is mostly eliminating unused data, and moving from Snowflake SQL to Spark SQL.

#### Spark ([Upgrade to 4.0)](https://spark.apache.org/releases/spark-release-4-0-0.html)

- Use Official [[Apache Spark Operator]] (new in v4)
    - Gives us Thrift Server CRD, SparkCluster CRD, SparkApplication CRD
- Thrift Server Endpoints for Airflow
- Only SQL Dialect for Transformations
- Better Iceberg support than Trino (Supports Iceberg V3)
- Refactor/Schedule/Automate Iceberg Maintenance

#### dbt Fusion

- Primary transformation framework
- Uses Spark Thrift Server
- Scheduled and orchestrated with Airflow
- Standard incremental, snapshot and materialization patterns
- Migration away from dbt Core to [dbt Fusion](https://docs.getdbt.com/docs/fusion/about-fusion)

Wishlist:

- Strong isolation between dbt jobs.
- Team-based resource pools for predictable performance and cost allocation.
- Clear failures & retries 

### 2.4 Orchestration
Apache Airflow has released v3.0, which is the next major version with a significant amount of changes making it more cost effective to run on Kubernetes with the Kubernetes Executor, which gives dynamic worker pod creation), better backfilling logic, Service-oriented Architecture and event driven scheduling.. This makes it a much more flexible service. 
#### Apache Airflow

- Upgrade to Apache 3.x
- Team Isolation, Team-owned DBT, Platform Owned template
- Standardized Orchestration of dbt, Spark for both transformations and Iceberg maintenance

Wishlist
- Limit use of cross-dag sensors, in favor of [Airflow dataset](https://airflow.apache.org/docs/apache-airflow/2.9.0/authoring-and-scheduling/datasets.html) or data contracts
### 2.5 BI/Consumers
#### Snowflake
- Read-only access to curated/transformed Iceberg data
- Tableau requires limited write access for some caching and extracts that will be required
- Guardrails
    - No transformations executed in Snowflake.
    - No raw data landing in Snowflake
    - Heavily monitored to prevent cost overruns of any kind.
    - Everything in Snowflake considered “BI Ready”

Wishlist:
- Large table optimization in Iceberg for Tableau access (rather than Snowflake storage)
- Warehouse Cost Attribution
- Path to store data in Snowflake, on a case by case basis, if performance needs demand it

## 3. Data Portal - Platform UI

For a good user experience, and to somewhat replicate what we have with dbt Cloud and Snowflake, we’ll want a UI to manage both dbt runs and Spark “Warehouses” or long running clusters. We should allow users to create their own long running clusters, but with guard rails to keep costs down. This should also abstract a significant amount of infrastructure work away from the end user, to allow for an easy to create, easy to clean up, environment with clear costs and team cost allocations.

### 3.1 Core UI Sections

##### 3.1.1.Long-runningCompute&DevEnvironment
- ViewactiveThriftEndpoints&SparkClusters
- CreateandManageDevEnvironments
- Viewown/team/orgclusterresourcesandestimatedcosts
- Extend/TerminateClusters
   
##### 3.1.2. Pipelines & Jobs
- List dbt jobs and Airflow DAGs
    - Last run status
    - Duration
    - Failure reason
- One click:
    - Rerun
    - Logs
    - SQL & Model Lineage
##### 3.1.3. Data Catalog
- Browse Iceberg Tables
- Metadata
    - Owner
    - Freshness
    - Schema
    - Row Counts
    - Snapshots
- Links to:
    - Upstream/Downstream Sources/Consumers
##### 3.1.4. Cost & Usage Dashboard
- Cost by:
    - Team
    - Pipeline
    - Spark Job
- Active Resources
- Trends
- “Most Expensive” Leaderboard
## 4. Agentic AI
Our Agentic AI framework should include both the ability for a chatbot (either through slack similar to Relic Assist, through Data Portal) as well as more autonomous actions through Github and Claude. 
##### 4.1 Platform Chat Bot
- Unified entrypoint across UI:
    - Context Aware and knows:
        - Logged in User
        - Team
        - Environment (Dev, Staging, Permanent)
    - Can Answer:
        - Why did a dbt Job fail?
        - What is the status of this Spark Cluster?
        - What upstream data feeds N Table
        - What has changed with this table, job, cluster, etc. since n time?
- Agent Actions
    - Chat Bot can:
        - Trigger a dbt Job, with confirmation
        - Restart failed Spark jobs
        - Create a dev Spark endpoint
        - Generate dbt model stubs
        - Propose/run Iceberg Maintenance for tables
##### 4.2 AI-Assisted Development
This can use Claude AI and Github PRs as suggested by the AI team. It’s fairly straightforward to set up in Github Actions (if we’re able to use those now)
- Generate dbt model templates from:
    - Source tables
    - Natural language descriptions
- Suggest:
    - Incremental strategies
    - Partitioning schemes
    - Performance optimizations
- Flag non-standard SQL patterns
##### 4.3 AI for Ops & Reliability
- Detection
    - SLA breaches
    - Schema Drift
    - Job runtime increases
- Explain failures in human readable reports
- Recommend next steps/fixes (reruns, backfills, escalate, etc.)
# Databricks Certified Data Analyst Associate — Study Guide

Complete topic-by-topic guide for the **August 2026 exam version** (exam published October 19, 2026; exam guide updated October 8, 2026 — terminology updates). Built from the official exam guide PDF, the official Azure Databricks documentation, and three exam-prep videos.

---

## Exam Facts

| Item | Detail |
|---|---|
| Scored questions | 45 multiple-choice |
| Unscored questions | Up to 10 (not identified, don't affect score, time already factored in) |
| Time limit | 90 minutes |
| Fee | USD $200 + taxes |
| Delivery | Online proctored or test center |
| Language | English only |
| Test aides | **None allowed** |
| Prerequisite | None required; related training highly recommended |
| Recommended experience | 6 months hands-on with the exam outline topics |
| Validity | 2 years — recertify by taking the full current exam |

**Key facts to remember:**
- Databricks SQL follows **ANSI SQL standards** — you don't need Python for this exam.
- The exam guide uses both new and legacy terminology: **OpenSharing** (formerly Delta Sharing), **Genie Agents** (formerly Genie Spaces), **Lakeflow Spark Declarative Pipelines** (formerly Delta Live Tables / DLT). Learn both names — questions may use either.

**Primary sources:**
- Exam guide: `resources/Databricks-Certified-Data-Analyst-Associate-Exam-Guide-August-2026.pdf`
- Official docs root: https://learn.microsoft.com/en-us/azure/databricks/

**Section weights (where to spend your time):**

| # | Section | Weight |
|---|---|---|
| 4 | Executing queries (Databricks SQL + SQL Warehouses) | **20%** |
| 6 | Dashboards & Visualizations | **16%** |
| 5 | Analyzing Queries (performance) | 15% |
| 7 | Genie Agents | 12% |
| 1 | Data Intelligence Platform | 11% |
| 2 | Managing Data | 8% |
| 9 | Securing Data | 8% |
| 3 | Importing Data | 5% |
| 8 | Data Modeling | 5% |

The top four sections (4, 6, 5, 7) are **63%** of the exam. Master those first.

---

## Section 1: Databricks Data Intelligence Platform (Lakehouse Platform) — 11%

### 1.1 Core platform components

The Databricks Data Intelligence Platform combines a lakehouse architecture with an AI-powered Data Intelligence Engine. It runs on cloud object storage and separates compute from storage.

**Components you must be able to describe:**

| Component | What it is |
|---|---|
| **Data Intelligence Engine** | The AI layer at the center of the platform. It learns from your data, metadata, and usage to power features like Genie Agents and natural-language interactions. |
| **Delta Lake** | Open-source storage layer that brings ACID transactions, schema enforcement/evolution, and time travel to data stored in cloud object storage (Parquet files + transaction log). |
| **Lakeflow Jobs** | The orchestration/scheduling platform for running jobs (notebooks, SQL, pipelines) in production. |
| **Lakeflow Spark Declarative Pipelines** (formerly Delta Live Tables / DLT) | Declarative framework for building reliable batch/streaming data pipelines; you declare expected results, it manages the processing. |
| **Lakebase** | Managed, Postgres-compatible online transaction processing (OLTP) engine integrated with Unity Catalog. |
| **Unity Catalog (UC)** | Unified governance layer for all data and AI assets: catalogs, schemas, tables, views, volumes, permissions, lineage, and sharing. |
| **Databricks SQL** | The SQL analytics engine and experience (SQL warehouses + SQL editor) for BI and query workloads. |
| **Mosaic AI** | The umbrella name for Databricks' AI/ML and generative AI tooling on the platform. |

**Examples — component-to-scenario matching (classic exam question style):**
1. *"Which component brings ACID transactions to cloud object storage?"* → Delta Lake.
2. *"Which component is the governance layer with catalogs, schemas, and permissions?"* → Unity Catalog.
3. *"Which component schedules production pipelines?"* → Lakeflow Jobs.
4. *"Which component is a managed Postgres-compatible OLTP engine?"* → Lakebase.
5. *"Which AI layer learns from usage and powers natural-language features?"* → Data Intelligence Engine.

**Docs:**
- Platform overview & layers: https://learn.microsoft.com/en-us/azure/databricks/introduction/ and https://learn.microsoft.com/en-us/azure/databricks/lakehouse-architecture/scope
- Data Intelligence Engine definition: https://learn.microsoft.com/en-us/azure/databricks/resources/glossary
- Delta Lake: https://learn.microsoft.com/en-us/azure/databricks/delta/
- Lakeflow Jobs: https://learn.microsoft.com/en-us/azure/databricks/jobs/
- Declarative pipelines: https://learn.microsoft.com/en-us/azure/databricks/ldp/concepts/spark-declarative-pipelines
- Lakebase: https://learn.microsoft.com/en-us/azure/databricks/oltp/projects/
- Unity Catalog: https://learn.microsoft.com/en-us/azure/databricks/data-governance/unity-catalog/
- Databricks SQL: https://learn.microsoft.com/en-us/azure/databricks/sql/

> Note: **Mosaic AI** has no dedicated page in the Azure Databricks documentation (verified) — the platform overview and glossary pages above are the closest official references. Know the one-line definition and move on; it's a small part of this objective.

### 1.2 Catalog Explorer objects

Catalog Explorer is the UI for browsing and managing Unity Catalog data objects. You must understand: **catalogs, schemas, managed tables, external tables, views, certified tables, metric views, lineage, and access controls.**

**Examples — objects you can see and manage in Catalog Explorer:**
1. **Catalogs and schemas** — the top two levels of the Unity Catalog namespace (e.g., `sales` catalog containing `prod` schema).
2. **Managed tables** — data and metadata fully managed by Unity Catalog; stored in the catalog's managed storage.
3. **External tables** — data stored in a location you control; Databricks manages only the metadata.
4. **Views** — saved query definitions over tables; also **metric views**, which define central, reusable business metrics (e.g., "revenue") on UC tables.
5. **Certified tables** — tables labeled "Certified" so analysts know they are trusted; lineage tab shows upstream/downstream dependencies, and Permissions tab controls access.

**Docs:**
- Catalog Explorer: https://learn.microsoft.com/en-us/azure/databricks/catalog-explorer/
- Database objects overview: https://learn.microsoft.com/en-us/azure/databricks/database-objects/
- Managed vs external tables: https://learn.microsoft.com/en-us/azure/databricks/tables/managed and https://learn.microsoft.com/en-us/azure/databricks/tables/external
- Metric views: https://learn.microsoft.com/en-us/azure/databricks/uc-semantics/metric-views/create
- Lineage: https://learn.microsoft.com/en-us/azure/databricks/data-lineage
- Permissions (manage privileges): https://learn.microsoft.com/en-us/azure/databricks/manage-privileges/
- Certified data: https://learn.microsoft.com/en-us/azure/databricks/data-governance/unity-catalog/certify-deprecate-data

### 1.3 Databricks Marketplace

The Marketplace is an exchange for finding and installing data and AI assets published by Databricks, partners, and customers: datasets, dashboards, notebooks, and more.

**Examples — how the Marketplace works:**
1. Install a free partner dataset listing to instantly get provider data into your workspace.
2. Install a sample dashboard or notebook listing to get started with analytics patterns.
3. Providers can publish listings free or paid, to specific recipients or publicly.
4. Installed listings appear in your catalog so you can query them like any other UC data.
5. Contrast: Marketplace is for *acquiring data/assets from providers*; OpenSharing is for *sharing your own data out* to others.

**Docs:** https://learn.microsoft.com/en-us/azure/databricks/marketplace/

---

## Section 2: Managing Data — 8%

### 2.1 Discover, query, and manage certified datasets with Unity Catalog

Certified datasets are tables/views labeled as trusted so analysts can distinguish sanctioned data from ad-hoc copies.

**Examples:**
1. Use the **Discover** page (search) to find datasets across catalogs by name, columns, tags, or owners.
2. A certified table displays a **"Certified"** label/badge in Catalog Explorer so users know it's trusted.
3. In the SQL editor, query a certified dataset like any other table: `SELECT * FROM sales.prod.orders LIMIT 10;`
4. A data owner certifies a table (and can later deprecate it) via the UI's asset labels, keeping the catalog trustworthy.

**Docs:**
- Discover page: https://learn.microsoft.com/en-us/azure/databricks/discover/discover-page
- Certify/deprecate data: https://learn.microsoft.com/en-us/azure/databricks/data-governance/unity-catalog/certify-deprecate-data

### 2.2 Governed tags and lineage (including external lineage)

Governed tags are **account-level** tags managed centrally (with tag policies), used for classification, discovery, and access control. They apply to Unity Catalog objects *and* workspace objects such as dashboards, Genie Agents, and notebooks.

**Examples:**
1. An admin creates a governed tag `PII` with allowed values (e.g., `true`) and a policy requiring it on sensitive tables.
2. Tag an asset in Catalog Explorer: open the table → Add tag → choose `PII`.
3. Governed tags are limited (max 1,000 tags per account) and only admins manage them — unlike informal tags any user can add.
4. Use tags in search on the Discover page to find all assets tagged `PII`.
5. **Lineage**: view the lineage graph in Catalog Explorer to see which upstream tables feed a table, and which dashboards/queries consume it downstream; **external lineage** shows lineage for data pipelines that originate outside Databricks (external systems/tools).

**Docs:**
- Governed tags: https://learn.microsoft.com/en-us/azure/databricks/admin/governed-tags/
- Tags on database objects: https://learn.microsoft.com/en-us/azure/databricks/database-objects/tags
- Lineage: https://learn.microsoft.com/en-us/azure/databricks/data-lineage
- External lineage: https://learn.microsoft.com/en-us/azure/databricks/external-lineage

### 2.3 Data cleaning in SQL

Remove invalid data and handle missing values in Unity Catalog tables using SQL.

**Examples:**
1. Filter out invalid rows in a query (don't mutate): `SELECT * FROM orders WHERE order_total > 0 AND status IN ('open','closed');`
2. Handle NULLs with `coalesce`: `SELECT coalesce(phone, 'UNKNOWN') AS phone FROM customers;`
3. Clean text with `regexp_replace`: `SELECT regexp_replace(phone, '[^0-9]', '') AS phone_digits FROM customers;`
4. Drop untrustworthy rows permanently: `DELETE FROM sales WHERE quantity < 0;`
5. Profile data first: use data profile/preview features (notebook data profile shows summary statistics + histograms for numeric, string, and date columns) to spot quality issues before cleaning.

**Docs:**
- WHERE clause: https://learn.microsoft.com/en-us/azure/databricks/sql/language-manual/sql-ref-syntax-qry-select-where
- `coalesce`: https://learn.microsoft.com/en-us/azure/databricks/sql/language-manual/functions/coalesce
- `regexp_replace`: https://learn.microsoft.com/en-us/azure/databricks/sql/language-manual/functions/regexp_replace
- Data profiling: https://learn.microsoft.com/en-us/azure/databricks/data-quality-monitoring/data-profiling/

---

## Section 3: Importing Data — 5%

### 3.1 Approaches for bringing data into Databricks

| Approach | When to use it |
|---|---|
| **S3 / cloud object storage ingestion** | Batch-loading files (CSV, Parquet, JSON) staged in a bucket; query directly with `read_files`/paths or load into tables. |
| **OpenSharing (Delta Sharing)** | Receiving data shared from external systems or other organizations via the open protocol — works even if the provider doesn't use Databricks. |
| **API-driven data intake** | Pulling data from services/APIs programmatically into the lakehouse. |
| **Auto Loader** | Incremental, streaming ingestion of new files as they arrive in cloud storage; the standard way to ingest file streams. |
| **Lakeflow Connect** | Managed connectors for external systems (databases, SaaS applications) — Databricks manages the pipeline. |
| **Marketplace** | Install ready-made datasets and assets published by providers. |

**Examples:**
1. Auto Loader (streaming file ingestion): `read_files('s3://bucket/path', format => 'csv')` with `cloudFiles` structured streaming to process new files incrementally.
2. Batch: `CREATE TABLE raw AS SELECT * FROM read_files('s3://bucket/sales/');`
3. A partner shares a Delta table with you via OpenSharing; you query it in place without copying data.
4. Use a Lakeflow Connect managed connector to sync data from an external database into your catalog.
5. Install a Marketplace listing to get a curated dataset in minutes.

**Docs:**
- Auto Loader: https://learn.microsoft.com/en-us/azure/databricks/ingestion/cloud-object-storage/auto-loader/
- Lakeflow Connect: https://learn.microsoft.com/en-us/azure/databricks/ingestion/lakeflow-connect/
- OpenSharing (formerly Delta Sharing): https://learn.microsoft.com/en-us/azure/databricks/opensharing/
- Marketplace: https://learn.microsoft.com/en-us/azure/databricks/marketplace/

### 3.2 Upload a file via the workspace UI

**Examples — UI upload workflow:**
1. In Catalog Explorer, use **Create or modify a table from file** ("Upload file") to create a UC table from a local CSV/JSON.
2. The UI previews the data and lets you confirm column names/types before creating the table.
3. Good for small one-off files (e.g., a 1 MB mapping CSV) — not for production pipelines.
4. Alternatively, upload a file to a **volume** (UC-managed storage location) and query it with a path.

**Docs:** https://learn.microsoft.com/en-us/azure/databricks/ingestion/create-or-modify-table

---

## Section 4: Executing Queries — Databricks SQL & SQL Warehouses — 20% (biggest section)

### 4.1 Genie Code (Databricks Assistant) in Notebooks and SQL Editor

An AI assistant inside notebooks and the SQL editor that generates, explains, fixes, and documents code.

**Examples — commands:**
1. `/explain` — step-by-step explanation of the code in a cell/query and what may be wrong with it. *(Sample question 2 answer.)*
2. `/fix` — automatically fix errors in the selected code.
3. `/doc` — add documentation/comments to code.
4. `/findTables` — find Unity Catalog tables relevant to what you're working on.

**Docs:** https://learn.microsoft.com/en-us/azure/databricks/notebooks/code-assistant

### 4.2 Role of the SQL Warehouse in query execution

A SQL warehouse is the compute resource that runs your Databricks SQL queries. Compute is **decoupled from storage** — warehouses run against data in UC/cloud storage and can scale independently.

**Examples:**
1. You write SQL in the editor; the **warehouse** compiles and executes it against the tables and returns results.
2. Warehouse types: **Serverless** (fast startup, no cluster management), **Pro** (includes Photon, scales well), **Classic** (fixed-size, you can toggle Photon).
3. Warehouses auto-stop after idle time (saves cost) and can auto-scale to handle concurrent queries.
4. Every query you run in the SQL editor is recorded in **Query History** for the warehouse, with metrics.

**Docs:**
- Warehouse types: https://learn.microsoft.com/en-us/azure/databricks/compute/sql-warehouse/warehouse-types
- Data warehousing concepts: https://learn.microsoft.com/en-us/azure/databricks/sql/get-started/data-warehousing-concepts
- SQL editor: https://learn.microsoft.com/en-us/azure/databricks/sql/user/sql-editor/

### 4.3 Cross-system analytics: joining Delta + federated sources (Lakehouse Federation)

Unity Catalog federation lets you query data in external systems (e.g., PostgreSQL, MySQL, Snowflake) without moving it, using foreign catalogs.

**Examples:**
1. Create a connection to a PostgreSQL database in Unity Catalog, then create a foreign catalog over it.
2. Join in one query: `SELECT d.*, p.region FROM delta_orders d JOIN postgres_catalog.public.customers p ON d.customer_id = p.id;`
3. Federated tables appear in Catalog Explorer like normal tables — you just query them.
4. Use case: combine local Delta analytics data with an external system of record without an ETL copy.

**Docs:** https://learn.microsoft.com/en-us/azure/databricks/query-federation/

### 4.4 Materialized Views vs Streaming Tables vs Dynamic Views

| Object | What it does | When to use |
|---|---|---|
| **Materialized view (MV)** | Precomputes and stores query results; refreshed on a schedule or manually | Frequent, complex queries on relatively static data (BI dashboards) |
| **Streaming table (ST)** | Built incrementally from streaming/continuously arriving data; processed once | Real-time analysis of continuously arriving data (e.g., sensor feeds) |
| **Dynamic view** | A view evaluated at query time, often using functions to control row/column visibility | Row-level/column-level security without copying or materializing data |

**Examples:**
1. `CREATE MATERIALIZED VIEW mv_daily_sales AS SELECT date, sum(amount) FROM sales GROUP BY date;` — results stored, refresh keeps them current; great for dashboards.
2. `CREATE STREAMING TABLE st_events AS SELECT * FROM STREAM read_files('s3://bucket/events/');` — processes each new file once.
3. Dynamic view for row-level security: `CREATE VIEW secure_orders AS SELECT * FROM orders WHERE is_account_group_member('sales') AND region = current_account_region();` — filtering happens per user, at query time.
4. Rule of thumb (sample question 3): **streaming table = continuously arriving data; materialized view = complex queries over static data.**

**Docs:**
- Materialized views: https://learn.microsoft.com/en-us/azure/databricks/sql/mv-st/materialized
- Streaming tables: https://learn.microsoft.com/en-us/azure/databricks/sql/mv-st/streaming
- CREATE VIEW: https://learn.microsoft.com/en-us/azure/databricks/sql/language-manual/sql-ref-syntax-ddl-create-view

### 4.5 Aggregate operations

**Examples:**
1. Count rows per group: `SELECT region, count(*) AS customers FROM customers GROUP BY region;` *(Note sample question 7: selecting `region` with `count(*)` requires `GROUP BY region`.)*
2. Average: `SELECT avg(price) FROM products;`
3. Approximate distinct count for big data speed: `SELECT approx_count_distinct(user_id) FROM events;` — faster than `COUNT(DISTINCT ...)` with a small accuracy trade-off.
4. Summary statistics: `SELECT min(x), max(x), avg(x), stddev(x) FROM sensors;`
5. Notebook **data profile** (sample question 1): automatic summary stats for numeric, string, and date columns plus value-distribution histograms.

**Docs:**
- `count`: https://learn.microsoft.com/en-us/azure/databricks/sql/language-manual/functions/count
- `avg`: https://learn.microsoft.com/en-us/azure/databricks/sql/language-manual/functions/avg
- `approx_count_distinct`: https://learn.microsoft.com/en-us/azure/databricks/sql/language-manual/functions/approx_count_distinct
- Aggregation guide: https://learn.microsoft.com/en-us/azure/databricks/transform/aggregation

### 4.6 Joins and set operations

**Examples:**
1. Inner join — only matching rows: `SELECT o.id, c.name FROM orders o JOIN customers c ON o.customer_id = c.id;`
2. Left join — all left rows, NULLs where no match: `... FROM customers c LEFT JOIN orders o ON c.id = o.customer_id;` (right join is the mirror).
3. Multi-key join: `ON a.order_id = b.order_id AND a.line_no = b.line_no;`
4. `UNION` removes duplicates across the combined result; `UNION ALL` keeps everything (faster, no dedup).
5. Join differences in one line: **inner** = matches only; **left** = all left + matches; **right** = all right + matches; **full** = everything from both sides.

**Docs:**
- SELECT JOIN reference: https://learn.microsoft.com/en-us/azure/databricks/sql/language-manual/sql-ref-syntax-qry-select-join
- JOIN types guide: https://learn.microsoft.com/en-us/azure/databricks/transform/join

### 4.7 Sorting and filtering

**Examples:**
1. `SELECT * FROM employees ORDER BY salary DESC;`
2. Multi-column sort: `ORDER BY department, salary DESC;`
3. Filter rows: `SELECT * FROM orders WHERE status = 'closed' AND total > 100;`
4. Pattern filter: `WHERE name LIKE 'A%';` or ranges: `WHERE order_date BETWEEN '2026-01-01' AND '2026-03-31';`
5. Filter groups with `HAVING` (after aggregation): `... GROUP BY region HAVING count(*) > 100;`

**Docs:**
- ORDER BY: https://learn.microsoft.com/en-us/azure/databricks/sql/language-manual/sql-ref-syntax-qry-select-orderby
- WHERE: https://learn.microsoft.com/en-us/azure/databricks/sql/language-manual/sql-ref-syntax-qry-select-where

### 4.8 Managed tables, external tables, and creating unified datasets

**Examples:**
1. Managed table (Databricks controls data + metadata): `CREATE TABLE warehouse_db.product_inventory (width INT, length INT, height INT);`
2. `CREATE OR REPLACE TABLE ...` replaces an existing table while **retaining history and privileges** *(sample question 6 answer)*; `DROP TABLE` + `CREATE TABLE` loses them.
3. External table (you control the storage location): `CREATE EXTERNAL TABLE catalog.schema.logs (...) LOCATION 's3://my-bucket/logs/';`
4. **DROP behavior (sample question 9):** dropping a **managed** table deletes the underlying data; dropping an **external** table removes only the metadata — the files remain in storage.
5. Build a unified dataset joining multiple sources (CTAS — create table as select): `CREATE TABLE unified AS SELECT c.*, p.part_name FROM read_files('s3://bucket/customers.csv') c JOIN catalog.parts.parquet_data p ON c.part_id = p.part_id;`

**Docs:**
- CREATE TABLE reference: https://learn.microsoft.com/en-us/azure/databricks/sql/language-manual/sql-ref-syntax-ddl-create-table
- Managed tables: https://learn.microsoft.com/en-us/azure/databricks/tables/managed
- External tables: https://learn.microsoft.com/en-us/azure/databricks/tables/external

### 4.9 Delta Lake time travel

Delta's transaction log keeps versions of a table; you can query data as of a version or timestamp.

**Examples:**
1. Query by version: `SELECT * FROM events VERSION AS OF 5;`
2. Query by timestamp: `SELECT * FROM events TIMESTAMP AS OF '2026-10-01T00:00:00Z';`
3. See the version history (for audit/validation): `DESCRIBE HISTORY events;`
4. Compare versions to validate results or trends: count rows today vs. version 30 vs. last week's timestamp.
5. **Limits (sample question 4):** time travel fails when `VACUUM` has deleted the data/log files for that version. Default retention is short — 7 days — so querying "30 days ago" fails if the files were vacuumed.

**Docs:** https://learn.microsoft.com/en-us/azure/databricks/tables/history (Delta time travel, `VERSION AS OF`, `DESCRIBE HISTORY`, retention) and https://learn.microsoft.com/en-us/azure/databricks/tables/operations/vacuum

---

## Section 5: Analyzing Queries — 15%

### 5.1 Photon

Photon is Databricks' vectorized, C++-accelerated query engine that speeds up SQL and data workloads, typically with no code changes.

**Examples:**
1. Photon speeds up long-running scans/joins/aggregations on the same SQL — you usually change nothing in your queries.
2. It's enabled on **Serverless and Pro** SQL warehouses; on **Classic** warehouses it's a toggle.
3. Best fit: large analytical scans and aggregations; less benefit for tiny queries.
4. Exam angle: "queries are slow on a warehouse — which engine accelerates SQL execution without code changes?" → Photon.

**Docs:** https://learn.microsoft.com/en-us/azure/databricks/compute/photon

### 5.2 Identifying poorly performing queries

**Examples — tools:**
1. **Query History** — filter queries by user, date, compute, and status; see duration and other metrics per query (sample question 10: B and D are the true features).
2. **Query profile** — inspect a query's execution plan, stage timings, and operators to find the slow step.
3. **Performance insights (Query Insights)** — highlights expensive/slow queries and workload patterns on a warehouse.
4. Workflow: find the slow query in Query History → open its profile → spot the expensive operator (e.g., full scan, shuffle) → fix (add a filter, cluster the table, etc.).

**Docs:**
- Query History: https://learn.microsoft.com/en-us/azure/databricks/sql/user/queries/query-history
- Query profile: https://learn.microsoft.com/en-us/azure/databricks/query-profile
- Performance insights: https://learn.microsoft.com/en-us/azure/databricks/performance-insights

### 5.3 Delta Lake history, audit, and validation

**Examples:**
1. `DESCRIBE HISTORY table;` — every version with operation, timestamp, user: an audit trail of changes.
2. Time travel to compare current vs. historical results to validate a pipeline fix: compare `count(*)` today vs. `VERSION AS OF 30`.
3. Compare trends: query the table as of several timestamps to see how a metric changed.
4. Use history to debug: a bad write shows up as a version/operation — restore or query just before it.

**Docs:** https://learn.microsoft.com/en-us/azure/databricks/tables/history

### 5.4 Query History and caching to reduce latency

**Examples:**
1. Query History details include duration, user, warehouse, and status — use it to see what developers/analysts actually ran (reduces re-development: find and rerun past queries).
2. Filter Query History by user, date range, compute resource, and query status (sample question 10, answer B).
3. Query History shows detailed execution metrics including duration and I/O performance (sample question 10, answer D).
4. **Caching**: Databricks SQL caches results — rerunning an identical query can return cached results faster, reducing latency during development iterations.

**Docs:**
- Query History: https://learn.microsoft.com/en-us/azure/databricks/sql/user/queries/query-history
- Query caching: https://learn.microsoft.com/en-us/azure/databricks/query-caching

### 5.5 Predictive Optimization and Automatic Liquid Clustering

**Examples:**
1. **Predictive Optimization** — Unity Catalog automatically runs table maintenance (such as `OPTIMIZE`) on UC tables based on observed usage patterns; no manual scheduling.
2. **Liquid clustering** — `CREATE TABLE t (...) CLUSTER BY (customer_id);` — data is incrementally clustered on chosen keys for faster filtered queries; replaces Z-ordering/Hive partitioning.
3. Re-clustering happens incrementally as data arrives; you can change clustering keys with `ALTER TABLE ... CLUSTER BY (...)`.
4. When to use: queries repeatedly filter on a column (e.g., date, region) → clustering; table has heavy scan/maintenance patterns → predictive optimization.

**Docs:**
- Predictive Optimization: https://learn.microsoft.com/en-us/azure/databricks/optimizations/predictive-optimization
- Liquid clustering: https://learn.microsoft.com/en-us/azure/databricks/tables/clustering

### 5.6 Fix a query to achieve the desired results

**Examples — classic fixes the exam tests:**
1. Missing `GROUP BY` (sample question 7): `SELECT region, count(*) FROM customers ORDER BY region;` fails the requirement — add `GROUP BY region`. Selecting a non-aggregated column with an aggregate requires grouping.
2. `ORDER BY` **is** allowed with aggregation; `HAVING` is not always required — don't "fix" what isn't broken.
3. Wrong join type: rows disappear → you needed `LEFT JOIN`, not `INNER JOIN`.
4. Duplicates after combining → you used `UNION ALL` where `UNION` (deduplicating) was needed.
5. Aggregate over the wrong grain: add/remove columns in `GROUP BY` to match the required level.

---

## Section 6: Dashboards and Visualizations — 16%

### 6.1 Building AI/BI Dashboards

AI/BI Dashboards are Lakehouse-native dashboards built on Unity Catalog datasets, supporting multiple pages, multiple datasets, and widget types.

**Examples:**
1. Create a dashboard from the SQL editor ("Add to dashboard") or from the Dashboards UI.
2. Add multiple **pages/tabs** — e.g., "Overview", "Regional detail".
3. Each visualization can use its own **dataset** (query); a dashboard commonly uses several datasets across widgets.
4. Widget types: visualizations (charts), text boxes (titles/annotations), images (logos).
5. Datasets are defined per dashboard (dataset = the query + schema powering widgets); multiple widgets can share one dataset.

**Docs:**
- Concepts: https://learn.microsoft.com/en-us/azure/databricks/dashboards/concepts
- Datasets: https://learn.microsoft.com/en-us/azure/databricks/dashboards/manage/data-modeling/datasets

### 6.2 Creating visualizations in notebooks and the SQL editor

**Examples:**
1. In the SQL editor: run a query, then click **+ (Add visualization)** below the result to build a chart from it.
2. In a notebook: display() a DataFrame or run SQL, then use the chart icon under the result to create a visualization.
3. Choose chart type, X/Y columns, aggregations (sum, avg, count), grouping, and labels in the visualization editor.
4. Visualizations created in the editor/notebook can be added to dashboards ("Add to dashboard").
5. Result grid options also include sorting and profiling — but charts are created from the same result set.

**Docs:** https://learn.microsoft.com/en-us/azure/databricks/visualizations/ (Databricks visualizations, formerly the notebook visualizations page)

### 6.3 Parameters in SQL queries and dashboards

Parameters make queries dynamic; dashboard widgets supply the values.

**Examples:**
1. SQL editor named parameter: `SELECT * FROM orders WHERE order_date BETWEEN :start_date AND :end_date;` — the editor prompts for values at run time.
2. Dashboard parameters: define a parameter (e.g., Date), attach a widget (date picker), and bind it to the query — the widget's start/end values are substituted into the query's `WHERE` clause. *(Sample question 8, answer C: the Date widget feeds the WHERE clause of the query populating the chart.)*
3. A single parameter can filter **multiple** visualizations that reference it.
4. Widget types include text, dropdown, date, number — value lists can be static or query-driven.
5. Testing: change the widget value and verify the visualization updates (that's the "testing parameters" workflow).

**Docs:** https://learn.microsoft.com/en-us/azure/databricks/dashboards/manage/filters/parameters

### 6.4 Sharing dashboards: permissions, links, embedding

**Examples:**
1. Share with workspace users/groups: configure dashboard permissions through the UI (e.g., CAN VIEW / CAN MANAGE rights for users and groups).
2. Share with people outside the workspace via **shareable links**.
3. **Embed** dashboards in external applications (external embed) for consumption outside Databricks.
4. Recipients see the dashboard, but data access still flows through Unity Catalog governance.

**Docs:**
- Share dashboards: https://learn.microsoft.com/en-us/azure/databricks/dashboards/share/share
- External embedding: https://learn.microsoft.com/en-us/azure/databricks/dashboards/share/embedding/external-embed

### 6.5 Scheduled refresh

**Examples:**
1. Configure a dashboard refresh schedule so datasets re-run automatically (e.g., every morning at 6 AM) on a chosen warehouse.
2. Subscribers receive an email when the refreshed dashboard is delivered.
3. Use case: stakeholders always see yesterday's numbers without opening Databricks.
4. The schedule runs the dashboard's dataset queries — no manual refresh needed.

**Docs:** https://learn.microsoft.com/en-us/azure/databricks/dashboards/share/schedule-subscribe

### 6.6 Alerts (threshold + destination)

An alert periodically evaluates a query and notifies you when the result crosses a threshold.

**Examples:**
1. Create an alert from a saved SQL query; set the trigger condition (e.g., `>`, `<`, `!=`) and the threshold value.
2. Set the evaluation frequency (e.g., every 15 minutes) — sample question 5: a query computing 15-minute average temperature that triggers when it exceeds the critical threshold and notifies via email/Slack is the correct design.
3. Choose **notification destinations** (email, Slack, webhook — configured by admins).
4. Alerts can notify when triggered, when resolved, and on failures.
5. Alerts complement dashboards: dashboards show state, alerts **push** notifications when thresholds break.

**Docs:**
- Alerts: https://learn.microsoft.com/en-us/azure/databricks/sql/user/alerts/
- Create an alert: https://learn.microsoft.com/en-us/azure/databricks/sql/user/alerts/create
- Notification destinations: https://learn.microsoft.com/en-us/azure/databricks/admin/workspace-settings/notification-destinations

### 6.7 Choosing the effective visualization type

**Examples — pick the chart that communicates the insight:**
1. **Bar chart** — compare values across categories (sales by region).
2. **Line chart** — show a trend over time (monthly revenue).
3. **Pie chart** — show parts of a whole for a few categories (traffic by source); poor for many slices.
4. **Scatter plot** — relationship/correlation between two numeric values.
5. **Table/heatmap** — exact values or a matrix of values by two dimensions.

**Docs:** https://learn.microsoft.com/en-us/azure/databricks/dashboards/manage/visualizations/types

---

## Section 7: AI/BI Genie Agents (formerly Genie Spaces) — 12%

### 7.1 Purpose, key features, components

Genie Agents are conversational AI agents that let business users ask natural-language questions about governed Unity Catalog data and get accurate answers (tables, charts, text).

**Key facts:**
- Built on **Unity Catalog datasets** (tables/views), **instructions**, **sample questions**, and **trusted assets**.
- Users need **CAN USE** permission on the SQL warehouse and appropriate UC data permissions.
- **Each end user's permissions apply**: Genie respects per-user Unity Catalog access — people can't see data they aren't allowed to see.

**Examples:**
1. A sales analyst asks "What was revenue by region last quarter?" and gets a chart plus the SQL Genie used.
2. Components you configure: dataset(s) + context/instructions (e.g., "fiscal year starts in February") + sample questions to guide users.
3. Trusted assets: vetted example queries the team curated so recurring questions are answered consistently and correctly.
4. Genie (like other AI/BI features) is powered by the Data Intelligence Engine and works on governed data.
5. Contrast with a dashboard: dashboards answer *predefined* questions; Genie answers *ad-hoc* natural-language questions.

**Docs:**
- Genie Agents overview: https://learn.microsoft.com/en-us/azure/databricks/genie-agents/
- Concepts: https://learn.microsoft.com/en-us/azure/databricks/genie-agents/concepts

### 7.2 Creating Genie Agents

**Examples — the setup workflow:**
1. Create a new Genie Agent; select the **Unity Catalog datasets** (tables/views) it should answer questions about.
2. Choose the **SQL warehouse** it will use to run queries.
3. Write **domain-specific instructions** (definitions, business rules, synonyms — e.g., "active customer means...").
4. Add **sample questions** users are likely to ask, with expected answers, to teach the agent.
5. Vet SQL queries as **Trusted Assets** so known-good logic is reused for recurring questions.

**Docs:** https://learn.microsoft.com/en-us/azure/databricks/genie-agents/set-up

### 7.3 Sharing Genie Agents (permissions, embed, channels)

**Examples:**
1. Assign permissions via the UI — give workspace users/groups access to the Genie Agent.
2. Ensure users have **CAN USE** on the warehouse and SELECT on the underlying tables; Genie answers within each user's UC permissions.
3. Distribute Genie via **embedded links** in internal sites/portals.
4. Integrate into external apps or channel apps (e.g., in messaging/app surfaces where users already work).

**Docs:** https://learn.microsoft.com/en-us/azure/databricks/genie-agents/embed

### 7.4 Optimizing and maintaining Genie Agents

**Examples:**
1. **Monitor** user questions, response accuracy, and feedback (thumbs up/down) to find weak spots.
2. Update **instructions** and add/adjust **trusted assets** based on stakeholder input and recurring questions.
3. Add sample questions where users struggled, so future asks route to vetted answers.
4. **Validate accuracy with benchmarks** — curated question sets you run to check answer quality.
5. **Refresh Unity Catalog metadata** — if tables/comments change, keep Genie's context in sync (good table/column comments in UC improve Genie answers).

**Docs:**
- Tune quality: https://learn.microsoft.com/en-us/azure/databricks/genie-agents/tune-quality
- Monitor: https://learn.microsoft.com/en-us/azure/databricks/genie-agents/monitor

---

## Section 8: Data Modeling with Databricks SQL — 5%

### 8.1 Star, snowflake, and data vault schemas

**Star schema (dimensional model):** a central **fact** table (measurable events: sales rows) surrounded by **dimension** tables (context: customer, product, date). Star schemas **perform well** for analytics on Databricks and are the recommended default.

**Examples:**
1. Fact `sales` (date_key, product_key, qty, amount) + dimensions `dim_customer`, `dim_product`, `dim_date` — join on keys in queries.
2. **Snowflake schema**: dimensions are further normalized into sub-dimensions (e.g., `dim_customer` → `dim_city` → `dim_country`); fewer joins in fact queries but more normalization.
3. **Data vault**: an industry modeling style built from **hubs** (business keys), **links** (relationships), and **satellites** (descriptive attributes/context), designed for auditability and agile integration. (Note: the Azure Databricks docs document star/snowflake dimensional modeling; data vault has no dedicated Azure docs page — know the hub/link/satellite definition from your exam guide and general modeling knowledge.)
4. Choose star for query performance and simplicity; snowflake when dimension redundancy matters; data vault when auditability/flexibility in integration is the priority.
5. On Databricks, denormalized/star-style tables work well because storage is cheap and joins are fast (Photon + Delta).

**Docs:**
- Data modeling guidance (star/snowflake perform well): https://learn.microsoft.com/en-us/azure/databricks/transform/data-modeling
- Dimensional modeling best practices (star schema at the gold layer): https://learn.microsoft.com/en-us/azure/databricks/ldp/best-practices/dimensional-modeling

### 8.2 How models align with the Medallion Architecture

Medallion = **Bronze** (raw ingested data) → **Silver** (cleaned, validated, conformed) → **Gold** (business-level aggregates ready for analytics). Each layer refines the previous.

**Examples:**
1. Bronze: raw CSVs from source systems landed as-is.
2. Silver: cleaned/deduplicated, validated tables (matching schema rules).
3. Gold: star-schema/dimensional models and aggregate tables that dashboards and Genie Agents query.
4. Raw → refined → curated mapping: bronze = raw, silver = refined, gold = curated.
5. A star schema naturally lives at **gold** — that's where dimensional modeling best practices point you.

**Docs:** https://learn.microsoft.com/en-us/azure/databricks/lakehouse/medallion

---

## Section 9: Securing Data — 8%

### 9.1 Unity Catalog roles and sharing settings

**Examples:**
1. Grant least privilege: `GRANT SELECT ON SCHEMA sales_prod TO analysts;` — SELECT on a schema covers current **and future** tables in it (least-privilege pattern; users can read but not modify).
2. `REVOKE` removes privileges; permissions can be granted to workspace users, groups (preferred), or service principals.
3. Manage privileges in the Catalog Explorer UI (Permissions tab) or with `GRANT`/`REVOKE` SQL.
4. Share data outside your organization with OpenSharing shares (governed by UC).
5. Ownership: the owner of an object has full control over it — see 9.3.

**Docs:**
- Manage privileges: https://learn.microsoft.com/en-us/azure/databricks/manage-privileges/
- OpenSharing: https://learn.microsoft.com/en-us/azure/databricks/opensharing/

### 9.2 The 3-level namespace

All UC data objects live in **`catalog.schema.object`**: catalogs contain schemas; schemas contain tables, views, and volumes.

**Examples:**
1. Fully qualified table: `sales.prod.orders` (catalog `sales`, schema `prod`, table `orders`).
2. Volume path form: `catalog.schema.volume_name/path/to/file`.
3. In queries you can write just `orders` if the current catalog/schema is set, or fully qualify for clarity/permissions.
4. Why three levels: group and secure data by catalog (top level) and schema (sub-level) — finer-grained governance across teams/projects.
5. Setting context: `USE CATALOG sales; USE SCHEMA prod;` then `SELECT * FROM orders;`.

**Docs:** https://learn.microsoft.com/en-us/azure/databricks/data-governance/unity-catalog/

### 9.3 Storage/management best practices: ownership and PII

**Examples:**
1. **Table ownership**: assign owners deliberately — the owner can alter/drop/grant on the table; don't leave ownership with a random creator account (use groups/service principals as owners).
2. **PII protection — row filters and column masks**: UC row-level security and column masking hide sensitive values (e.g., mask `email` for non-privileged users) without duplicating tables. Dynamic views also implement per-user filtering.
3. **Data classification**: classify/tag sensitive data (e.g., governed tag `PII`) to enable discovery and governance.
4. Prefer **managed tables** under UC governance for sensitive data (metadata + lifecycle under control) and grant least privilege by group.
5. Governed tags + certified labels keep the catalog trustworthy: certified, well-described, properly tagged assets reduce misuse of stale/sensitive data.

**Docs:**
- Row filters & column masks: https://learn.microsoft.com/en-us/azure/databricks/filters-and-masks/
- Data classification: https://learn.microsoft.com/en-us/azure/databricks/data-classification
- Managed tables: https://learn.microsoft.com/en-us/azure/databricks/tables/managed

---

## Sample Questions — Answers and Lessons

| # | Answer | Lesson |
|---|---|---|
| 1 | **B** | Notebook data profile gives summary statistics (numeric, string, and date columns) **plus** distribution histograms. |
| 2 | **C** | Genie Code `/explain` = step-by-step query explanation. `/help` lists commands, `/generate` writes SQL, `/optimize` tunes. |
| 3 | **D** | Streaming Table = continuously arriving data; Materialized View = frequent complex queries on static data. |
| 4 | **B** | Time travel fails after `VACUUM` removes the needed data/log files (default retention ≈ 7 days). |
| 5 | **A** | SQL Alert = query + threshold + scheduled evaluation + instant notifications (email/Slack). |
| 6 | **B** | `CREATE OR REPLACE TABLE` keeps history and privileges; `IF NOT EXISTS` won't replace; `DROP`+`CREATE` loses them. |
| 7 | **A** | Selecting a non-aggregated column with an aggregate requires `GROUP BY`. |
| 8 | **C** | A dashboard Date widget parameter's values are substituted into the query's `WHERE` clause. |
| 9 | **B** | Dropping an **external** table removes only metadata; files remain in your storage location. |
| 10 | **B, D** | Query History: filter by user/date/compute/status, and see detailed execution metrics (duration, I/O). |

---

## Study Tips from the Prep Videos

**From the "Open Exam Prep" video (exam-domain focus):**
- The top 4 sections (SQL execution, dashboards, query analysis, Genie) are 63% of the exam — spend most of your time there.
- Practice hands-on: dashboard parameters, scheduling, alerts, sharing; Genie trustworthiness (trusted assets, instructions, benchmarks); Photon + liquid clustering; Unity Catalog security scenarios.
- Use a 5-phase plan: (1) assess with a practice exam, (2) study weakest domains, (3) hands-on labs, (4) timed practice questions, (5) final review + rest.

**From the "Data Mastery" video (hands-on and exam tactics):**
- Hands-on practice in **Databricks Free Edition** is essential — do every workflow at least once.
- Compute patterns: **all-purpose compute** for ad hoc/exploration, **job compute** for scheduled production work, **SQL warehouses** for SQL analytics, **serverless** for zero-overhead.
- Know defaults: managed tables store data in UC-managed locations (drop deletes data); external tables point to your storage (drop keeps data).
- Least privilege: grant `SELECT ON SCHEMA` (covers future tables) rather than broad `ALL PRIVILEGES`.
- Exam day: read the constraint in the question first, eliminate clearly wrong options, then pick the best remaining answer. Watch for words like "empty", "retains history", "least privilege".

**From the "MindMajix" video (fundamentals refresh):**
- Delta Lake brings **ACID** transactions to the lakehouse.
- Time travel use cases: auditing changes, debugging bad writes, recovering older data.
- **Schema enforcement** (reject mismatched writes) vs **schema evolution** (merge/append new columns).
- Z-ordering vs **liquid clustering**: liquid clustering is the modern, incremental replacement — prefer it on new tables.
- Unity Catalog governs all assets; MLflow tracks ML experiments (background awareness, rarely central to this exam).

---

## Preparation Plan (2–3 weeks suggested)

1. **Days 1–2 — Foundations (Sections 1–3, 24%)**: platform components, Catalog Explorer objects, Marketplace, governed tags, lineage, ingestion approaches. Read the linked docs for each.
2. **Days 3–6 — SQL execution (Section 4, 20%)**: run every SQL pattern above in a workspace (Free Edition is fine): joins, unions, aggregates, `approx_count_distinct`, managed vs external tables, `CREATE OR REPLACE`, time travel (`VERSION AS OF`, `DESCRIBE HISTORY`), MV vs streaming table vs dynamic view, a federated join, Genie Code `/explain`.
3. **Days 7–9 — Dashboards + Genie (Sections 6–7, 28%)**: build a two-page dashboard with parameters, schedule, shareable link; create an alert with a threshold and destination; create a small Genie Agent with instructions, sample questions, and a trusted asset; check its permissions.
4. **Days 10–11 — Performance (Section 5, 15%)**: inspect Query History and a query profile; explain when you'd use Photon, liquid clustering, predictive optimization; run `DESCRIBE HISTORY` and `VACUUM` on a test table to see time-travel limits.
5. **Days 12–13 — Modeling + security (Sections 8–9, 13%)**: sketch a star schema over a sample dataset; medallion bronze/silver/gold; 3-level namespace, `GRANT SELECT ON SCHEMA`, row filters/column masks for PII.
6. **Days 14+ — Practice**: redo the 10 sample questions cold, take a timed practice exam if available, review weak spots, rest before exam day.

**Exam-day reminders:** 90 minutes / 45 scored questions ≈ 2 minutes per question — flag and return. No test aides: memorize the defaults (7-day time-travel retention, `CREATE OR REPLACE` retains history, external drop keeps files, `GRANT ON SCHEMA` covers future tables). Read each question's constraint before the options.

---

*Every documentation link above was verified against the official Azure Databricks documentation (learn.microsoft.com) as of November 2026. Two honesty notes: "Mosaic AI" and "data vault" have no dedicated Azure Databricks doc pages — those entries cite the closest official pages and clearly say so.*

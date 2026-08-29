## What Problem Does It Solve?

[[Redshift]] is AWS's:

**Fully managed cloud data warehouse**

It is designed for:

- Large-scale analytics
- Business intelligence
- Complex SQL queries
- Aggregations across large datasets
- Reporting workloads

Architecture:

Data Sources  
↓  
Redshift  
↓  
SQL Analytics / BI Tools

> [!tip] Memory Trick
> **Redshift = Data Warehouse**
>
> Think:
>
> **BIG SQL ANALYTICS**

---

## Core Concept

Redshift is built for:

**OLAP — Online Analytical Processing**

That means:

- Large scans
- Aggregations
- Reporting
- Historical analysis
- BI workloads

It is NOT primarily designed for:

**High-frequency transactional OLTP workloads**

### Killer Exam Clue

> **Need a managed cloud data warehouse for analytics**
>
> → **Redshift**

---

# Redshift Architecture

Traditional architecture:

Operational Databases  
↓  
ETL / ELT  
↓  
Redshift  
↓  
BI / Analytics

Redshift centralizes large datasets for:

**Analytical SQL queries**

---

# Columnar Storage

Redshift stores data using:

**Columnar storage**

Instead of reading every field in every row:

Redshift can focus on:

**The columns needed by the query**

This improves performance for:

- Aggregations
- Reporting
- Analytical queries

### Memory Trick

**Analytics Loves Columns**

---

# Massively Parallel Processing

Redshift uses:

**Massively Parallel Processing — MPP**

Queries are distributed across:

**Multiple compute resources**

Architecture:

Large Query  
↓  
Split Work  
↓  
Parallel Processing  
↓  
Combine Results

### Killer Exam Concept

> **Redshift speeds large analytical queries using parallel processing**

---

# Redshift Cluster

A traditional Redshift deployment uses a:

**Cluster**

consisting of:

- Leader node
- Compute nodes

---

## Leader Node

The:

**Leader Node**

coordinates:

- Client connections
- SQL parsing
- Query planning
- Distribution of work

### Memory Trick

**Leader = Coordinator**

---

## Compute Nodes

Compute nodes:

**Store and process data**

They execute portions of the query in parallel.

### Memory Trick

**Compute Nodes = Workers**

---

# Node Types

Redshift node families are optimized for different needs.

A major modern architecture choice is:

**RA3**

RA3 separates:

**Compute**

from:

**Managed storage**

This provides more flexibility when:

**Storage and compute requirements grow differently**

---

# Redshift Managed Storage

With RA3:

Frequently accessed data can benefit from:

**Local high-performance storage**

while additional data can use:

**Redshift Managed Storage**

This reduces the need to size the cluster solely around:

**Total data volume**

### Killer Exam Clue

> **Need independent scaling of Redshift compute and storage**
>
> → **RA3 / Redshift Managed Storage**

---

# Redshift Serverless

[[Redshift Serverless]] lets you run:

**Redshift analytics without managing clusters**

AWS manages:

- Capacity
- Scaling
- Infrastructure

You focus on:

- Data
- SQL
- Analytics

### Killer Exam Clue

> **Need Redshift analytics with minimal infrastructure management**
>
> → **Redshift Serverless**

---

# Provisioned Redshift vs Serverless

| Requirement | Provisioned Redshift | Redshift Serverless |
|---|---:|---:|
| Manage Cluster Capacity | ✅ | ❌ |
| Predictable Dedicated Environment | ✅ | ✅ |
| Minimal Infrastructure Management | ❌ | ✅ |
| Automatic Capacity Management | Limited | ✅ |
| Data Warehouse SQL | ✅ | ✅ |

### Memory Trick

**Provisioned = Manage Warehouse Capacity**

**Serverless = Just Run Analytics**

---

# OLAP vs OLTP

This distinction is critical.

## OLAP

Think:

- Analytics
- Aggregations
- Historical data
- Large scans
- Reports

→ **Redshift**

## OLTP

Think:

- Transactions
- Individual row updates
- Application database
- Frequent small reads/writes

→ **RDS / Aurora**

### Killer Shortcut

**Analytics**
→ Redshift

**Transactions**
→ RDS / Aurora

---

# Redshift vs RDS

## Redshift

Designed for:

**Analytics**

## [[RDS]]

Designed for:

**Transactional applications**

Example:

Customer places order  
→ RDS

Executives analyze 5 years of order history  
→ Redshift

---

# Redshift vs Athena

This is a major SAA comparison.

## Redshift

Think:

- Data warehouse
- Repeated analytics
- Complex BI queries
- Structured warehouse workloads
- High-performance SQL analytics

## [[Athena]]

Think:

- Serverless ad hoc SQL
- Query S3 directly
- Pay per data scanned
- No warehouse required

### Killer Shortcut

**Ad hoc SQL on S3**
→ Athena

**Dedicated/managed analytical warehouse**
→ Redshift

---

# Redshift Spectrum

**Redshift Spectrum**

allows Redshift to query:

**Data stored directly in S3**

without loading all of it into:

**Redshift local storage**

Architecture:

Redshift  
↓  
Spectrum  
↓  
[[S3]]

### Killer Exam Clue

> **Redshift users need to query large datasets in S3 without loading them into Redshift**
>
> → **Redshift Spectrum**

---

# Why Spectrum Matters

Suppose:

Frequently queried data  
→ Redshift

Huge historical archive  
→ S3

Redshift Spectrum can query:

**Both**

without moving the entire archive into:

**The warehouse**

### Memory Trick

**Spectrum = Redshift reaches into S3**

---

# Spectrum + Glue Data Catalog

Spectrum can use:

[[Glue Data Catalog]]

for metadata describing:

**External S3 tables**

Architecture:

S3 Data  
↓  
Glue Data Catalog  
↓  
Redshift Spectrum

---

# Redshift vs Athena for S3

Both can query S3.

### Athena

Think:

**Serverless ad hoc S3 SQL**

### Redshift Spectrum

Think:

**Redshift warehouse extending queries into S3**

### Killer Distinction

Already using Redshift and need S3 data?

→ **Spectrum**

Need standalone ad hoc SQL on S3?

→ **Athena**

---

# COPY Command

A common way to load data into Redshift is:

**COPY**

Example architecture:

S3  
↓  
COPY  
↓  
Redshift

COPY is optimized for:

**Bulk loading data**

into Redshift.

### Killer Exam Clue

> **Efficiently load large amounts of S3 data into Redshift**
>
> → **COPY command**

---

# UNLOAD Command

Redshift can export query results using:

**UNLOAD**

Architecture:

Redshift  
↓  
UNLOAD  
↓  
S3

Use for:

- Exporting analytical results
- Archiving query output
- Downstream processing

### Memory Trick

**COPY = INTO Redshift**

**UNLOAD = OUT to S3**

---

# Redshift Distribution Styles

Redshift distributes table data across:

**Compute nodes**

The way data is distributed affects:

**Query performance**

Important concepts include:

- EVEN
- KEY
- ALL
- AUTO

For SAA, focus on the principle:

> **Good data distribution reduces unnecessary movement between nodes**

---

# Distribution Key

A:

**Distribution Key**

determines how rows are distributed among:

**Compute nodes**

If frequently joined tables share compatible distribution keys:

Redshift can reduce:

**Data movement during joins**

### Killer Exam Concept

> **Choose distribution strategy based on joins and access patterns**

---

# Sort Keys

A:

**Sort Key**

controls how data is physically ordered.

Queries that frequently filter or sort by:

**The sort key**

can perform more efficiently.

Example:

Timestamp-based analytics  
↓  
Sort Key = EventDate

### Memory Trick

**Distribution = Where Data Lives**

**Sort = How Data Is Ordered**

---

# Compression

Redshift uses:

**Column compression**

to reduce:

- Storage
- I/O
- Query processing

Compression is especially valuable for:

**Large analytical datasets**

---

# Redshift Automatic Optimization

Modern Redshift can automate many optimization choices.

The exam principle remains:

> **Redshift is optimized for analytical workloads through columnar storage, parallelism, and data-layout optimization**

---

# Redshift Concurrency Scaling

If many users run queries simultaneously:

**Concurrency Scaling**

can add temporary query-processing capacity.

Architecture:

Query Load ↑  
↓  
Additional Redshift Capacity  
↓  
More Queries Processed

### Killer Exam Clue

> **Redshift query concurrency suddenly increases and users are waiting**
>
> → **Concurrency Scaling**

---

# Workload Management

Redshift:

**Workload Management — WLM**

helps control how query resources are allocated among:

**Different workloads**

Example:

Executive Dashboards  
↓  
Higher Priority

Ad Hoc Analyst Queries  
↓  
Different Queue

### Killer Exam Clue

> **Prioritize different classes of Redshift queries**
>
> → **Workload Management**

---

# WLM vs Concurrency Scaling

## WLM

Controls:

**How existing resources are prioritized**

## Concurrency Scaling

Adds:

**Additional temporary capacity**

### Memory Trick

**WLM = Prioritize**

**Concurrency Scaling = Add Capacity**

---

# Materialized Views

A:

**Materialized View**

stores:

**Precomputed query results**

This can accelerate:

**Repeated expensive queries**

Example:

Large Aggregation  
↓  
Materialized View  
↓  
Fast Dashboard Query

### Killer Exam Clue

> **Same expensive aggregation is run repeatedly**
>
> → **Materialized View**

---

# Result Caching

Redshift can reuse:

**Previously computed query results**

when appropriate.

This can reduce:

**Repeated query execution**

for identical requests.

---

# Redshift + QuickSight

Architecture:

Redshift  
↓  
[[09-Analytics/QuickSight]]  
↓  
Dashboard

This is a common:

**Business intelligence architecture**

### Killer Exam Clue

> **Create BI dashboards from a Redshift warehouse**
>
> → **QuickSight + Redshift**

---

# Redshift + Glue

[[09-Analytics/Glue]] can:

- Discover data
- Catalog datasets
- Perform ETL
- Prepare data

before loading or querying through:

**Redshift**

Architecture:

Raw Data  
↓  
Glue  
↓  
Redshift

---

# Redshift + S3 Data Lake

A common architecture:

Operational Data  
↓  
S3 Data Lake  
↓  
Glue Catalog  
↓  
Redshift Spectrum  
↓  
BI Tools

This allows Redshift to participate in:

**Data lake analytics**

---

# Redshift + Kinesis

Streaming data can eventually feed:

**Redshift analytics**

through supported ingestion architectures.

Think:

Streaming Events  
↓  
Analytics Pipeline  
↓  
Redshift

For SAA, the broader concept is:

> **Redshift is commonly the analytical destination for large datasets**

---

# Redshift Security

Redshift integrates with:

- IAM
- KMS
- VPC
- Security Groups
- CloudTrail
- CloudWatch

Security design still follows:

**Least privilege**

---

# Encryption at Rest

Redshift supports:

**Encryption at rest**

with:

[[06-Security/KMS]]

This protects:

**Warehouse data**

---

# Encryption in Transit

Client connections can use:

**TLS**

to encrypt:

**Data in transit**

---

# VPC Deployment

Provisioned Redshift clusters are typically deployed inside:

**A VPC**

This lets you control:

- Subnets
- Routing
- Security groups
- Network access

---

# Publicly Accessible

A Redshift cluster can be configured as:

**Publicly accessible**

or:

**Private**

For production architectures:

Private networking is often preferred when:

**Public access is unnecessary**

---

# Redshift Enhanced VPC Routing

Enhanced VPC Routing forces certain Redshift traffic to external data sources through:

**Your VPC**

This can provide greater control through:

- VPC routes
- Security controls
- Network monitoring

### Exam Concept

> **Need tighter network control over Redshift data traffic**
>
> → Consider **Enhanced VPC Routing**

---

# Redshift Snapshots

Redshift supports:

**Snapshots**

for backups.

Snapshots can be:

- Automated
- Manual

They can be used for:

- Restore
- Recovery
- Migration
- Copying environments

---

# Automated Snapshots

Redshift automatically creates:

**Snapshots**

according to configured retention.

This protects against:

**Data loss**

---

# Manual Snapshots

Manual snapshots are retained until:

**Explicitly deleted**

This can be useful for:

- Long-term retention
- Pre-change backups
- Migration

---

# Cross-Region Snapshot Copy

Redshift snapshots can be copied:

**Across Regions**

This can support:

- Disaster recovery
- Regional migration
- Backup strategy

### Killer Exam Clue

> **Need Redshift backup copies in another Region**
>
> → **Cross-Region Snapshot Copy**

---

# Redshift High Availability

Traditional provisioned Redshift architecture differs from:

**RDS Multi-AZ**

Do NOT assume Redshift works exactly like:

**An OLTP database**

For availability, modern Redshift capabilities and cluster design should be evaluated based on:

**Warehouse requirements**

The key exam point:

> **Redshift is an analytics warehouse, not a traditional Multi-AZ RDS database**

---

# Redshift Multi-AZ

Modern Redshift supports:

**Multi-AZ deployment options**

for supported provisioned architectures.

The important exam concept is:

> **If the question explicitly requires higher warehouse availability across AZs, consider Redshift Multi-AZ where supported**

Do not confuse this with:

**RDS Multi-AZ mechanics**

---

# Redshift Data Sharing

Redshift supports:

**Data Sharing**

which allows multiple Redshift consumers to access:

**Live data**

without copying the underlying dataset.

Architecture:

Producer Warehouse  
↓  
Shared Data  
↓  
Consumer Warehouse

### Killer Exam Clue

> **Multiple Redshift environments need access to the same live data without duplicating it**
>
> → **Redshift Data Sharing**

---

# Zero-ETL Integrations

AWS supports architectures where certain operational databases can replicate data into:

**Redshift**

with reduced traditional ETL work.

The broad exam concept:

> **Zero-ETL integrations reduce the need to build custom pipelines before analytics in Redshift**

---

# Architecture Thinking

## Scenario 1 — Enterprise BI Warehouse

Company has:

- Years of sales data
- Complex analytical queries
- BI dashboards
- Many aggregations

Choose:

**Redshift**

---

## Scenario 2 — Ad Hoc S3 Logs

Need occasional SQL queries on:

**S3 log files**

Do NOT automatically create Redshift.

Choose:

**Athena**

---

## Scenario 3 — Query S3 from Existing Warehouse

Company already uses Redshift.

Need to analyze:

**Petabytes of archived S3 data**

without loading all of it.

Choose:

**Redshift Spectrum**

---

## Scenario 4 — Bulk Load

Terabytes of data are stored in S3.

Need efficient loading into:

**Redshift**

Choose:

**COPY**

---

## Scenario 5 — Export Results

Need to export Redshift analytical results to:

**S3**

Choose:

**UNLOAD**

---

## Scenario 6 — Query Queueing

Hundreds of analysts run queries simultaneously.

Queries are delayed.

Need additional processing capacity.

Choose:

**Concurrency Scaling**

---

## Scenario 7 — Priority Workloads

Executive dashboard queries must take priority over:

**Ad hoc analyst jobs**

Choose:

**WLM**

---

## Scenario 8 — Repeated Aggregation

Same complex monthly revenue query runs:

**Thousands of times**

Choose:

**Materialized View**

---

## Scenario 9 — Separate Compute and Storage

Company stores enormous datasets but does not need proportionally massive compute.

Choose:

**RA3 / Managed Storage**

---

## Scenario 10 — No Cluster Management

Team wants:

**Redshift data warehousing without managing cluster capacity**

Choose:

**Redshift Serverless**

---

## Scenario 11 — BI Dashboard

Need dashboards from warehouse data.

Choose:

Redshift  
↓  
[[09-Analytics/QuickSight]]

---

## Scenario 12 — OLTP Application

Application processes:

Thousands of individual transactions.

Need foreign keys and relational transactions.

Do NOT choose Redshift.

Think:

**RDS / Aurora**

---

# Scenario Recognition

Immediately think:

**Redshift**

when you see:

- Data warehouse
- OLAP
- BI analytics
- Complex SQL analytics
- Historical reporting
- Columnar storage
- Massive parallel processing
- Large aggregations

---

## Think Spectrum When You See

- Redshift querying S3
- External S3 tables
- Data lake + Redshift
- Avoid loading all S3 data

---

## Think Athena When You See

- Ad hoc SQL on S3
- No warehouse
- Pay per data scanned
- Occasional queries

---

## Think RA3 When You See

- Separate compute and storage
- Managed warehouse storage
- Large datasets

---

## Think Serverless When You See

- No cluster management
- Variable warehouse demand
- Minimal operational overhead

---

# Exam Traps

## Trap 1 — Redshift Is an OLTP Database

❌

Redshift is:

**OLAP / Data Warehouse**

---

## Trap 2 — Redshift Is Best for Individual Transaction Processing

❌

Think:

**RDS / Aurora**

---

## Trap 3 — Spectrum Requires Loading S3 Data into Redshift First

❌

Spectrum queries:

**S3 directly**

---

## Trap 4 — Athena and Redshift Are Identical

❌

Athena:

**Ad hoc SQL on S3**

Redshift:

**Data warehouse**

---

## Trap 5 — Redshift Uses Row-Oriented Storage Primarily

❌

Think:

**Columnar storage**

---

## Trap 6 — COPY Exports Data to S3

❌

COPY:

**Loads INTO Redshift**

UNLOAD:

**Exports OUT**

---

## Trap 7 — WLM Adds New Compute Capacity

❌

WLM:

**Prioritizes workloads**

Concurrency Scaling:

**Adds temporary capacity**

---

## Trap 8 — RA3 Requires Compute to Scale Exactly With Storage

❌

RA3 helps:

**Separate compute and storage scaling**

---

# Quick Cheat Sheet

| Exam Clue | Answer |
|---|---|
| Cloud Data Warehouse | Redshift |
| OLAP | Redshift |
| Columnar Analytics | Redshift |
| Parallel SQL Processing | MPP |
| Query S3 from Redshift | Spectrum |
| Load S3 → Redshift | COPY |
| Export Redshift → S3 | UNLOAD |
| Separate Compute / Storage | RA3 |
| No Cluster Management | Redshift Serverless |
| High Query Concurrency | Concurrency Scaling |
| Prioritize Query Classes | WLM |
| Repeated Expensive Query | Materialized View |
| BI Visualization | QuickSight |
| Ad Hoc SQL on S3 | Athena |
| Transaction Database | RDS / Aurora |
| Cross-Region Backup | Snapshot Copy |

---

# Redshift vs Athena vs RDS

| Requirement | Redshift | Athena | RDS |
|---|---:|---:|---:|
| Data Warehouse | ✅ | ❌ | ❌ |
| Ad Hoc SQL on S3 | Spectrum | ✅ | ❌ |
| OLTP | ❌ | ❌ | ✅ |
| Serverless Option | ✅ | ✅ | Some Engines/Options |
| Complex BI Queries | ✅ | Possible | Limited Fit |
| Data Stored Primarily in S3 | Spectrum | ✅ | ❌ |

---

# Performance Shortcut

Need:

**Repeated warehouse analytics**

→ Redshift

Need:

**More concurrent warehouse queries**

→ Concurrency Scaling

Need:

**Query prioritization**

→ WLM

Need:

**Repeated expensive aggregation**

→ Materialized View

Need:

**Less data movement between nodes**

→ Good Distribution Strategy

Need:

**Efficient filtering**

→ Sort Keys

---

# Final Exam Rapid-Fire

> **DATA WAREHOUSE**
> → REDSHIFT
>
> **OLAP**
> → REDSHIFT
>
> **COLUMNAR**
> → REDSHIFT
>
> **PARALLEL PROCESSING**
> → MPP
>
> **REDSHIFT → S3 QUERY**
> → SPECTRUM
>
> **S3 → REDSHIFT LOAD**
> → COPY
>
> **REDSHIFT → S3 EXPORT**
> → UNLOAD
>
> **SEPARATE COMPUTE/STORAGE**
> → RA3
>
> **NO CLUSTER MANAGEMENT**
> → REDSHIFT SERVERLESS
>
> **TOO MANY CONCURRENT QUERIES**
> → CONCURRENCY SCALING
>
> **PRIORITIZE QUERIES**
> → WLM
>
> **REPEATED EXPENSIVE QUERY**
> → MATERIALIZED VIEW
>
> **DASHBOARD**
> → QUICKSIGHT
>
> **AD HOC S3 SQL**
> → ATHENA
>
> **TRANSACTIONAL DATABASE**
> → RDS / AURORA

---

## Master Memory Trick

> [!tip] Redshift Master Memory Trick
> Imagine a giant corporate analytics warehouse.
>
> Data arrives from:
>
> **Operational Systems**
>
> It gets organized for:
>
> **REPORTING + ANALYTICS**
>
> Thousands of workers can process large questions:
>
> **MPP**
>
> The shelves are organized by columns:
>
> **COLUMNAR STORAGE**
>
> Historical boxes stay cheaply in S3:
>
> **SPECTRUM**
>
> The warehouse can expand query capacity during rush hour:
>
> **CONCURRENCY SCALING**
>
> Managers decide which analysts get priority:
>
> **WLM**
>
> Frequently requested reports are precomputed:
>
> **MATERIALIZED VIEWS**

So remember:

> **REDSHIFT**
> → DATA WAREHOUSE
>
> **SPECTRUM**
> → QUERY S3
>
> **COPY**
> → LOAD IN
>
> **UNLOAD**
> → EXPORT OUT
>
> **RA3**
> → SEPARATE COMPUTE + STORAGE
>
> **CONCURRENCY SCALING**
> → MORE QUERY CAPACITY
>
> **WLM**
> → PRIORITIZE
>
> **MATERIALIZED VIEW**
> → PRECOMPUTE

And the killer SAA question:

> **"Does the company need a managed analytical data warehouse for large-scale SQL and BI workloads?"**
>
> YES
>
> → **Redshift**

---

## Related Notes

- [[Athena]]
- [[S3]]
- [[09-Analytics/Glue]]
- [[Glue Data Catalog]]
- [[09-Analytics/QuickSight]]
- [[RDS]]
- [[Aurora]]
- [[20-SAA/10-Messaging/Kinesis Data Streams]]
## What Problem Does It Solve?

[[Athena]] is a:

**Serverless interactive query service**

that lets you analyze data stored in:

**Amazon S3**

using:

**Standard SQL**

Architecture:

Data in S3  
↓  
Athena  
↓  
SQL Query  
↓  
Results

> [!tip] Memory Trick
> **Athena = SQL on S3**
>
> No database server to manage.

---

## Core Concept

Athena lets you query:

**Data directly where it already lives in S3**

You do NOT need to:

- Load the data into RDS
- Provision database servers
- Manage a data warehouse
- Create an EC2 analytics cluster

Instead:

S3 Data  
↓  
Define Schema  
↓  
Run SQL  
↓  
Get Results

### Killer Exam Clue

> **Run ad hoc SQL queries directly against data stored in S3**
>
> → **Athena**

---

## Serverless

Athena is:

**Serverless**

AWS manages:

- Compute infrastructure
- Query execution resources
- Scaling
- Underlying servers

You manage:

- S3 data
- Table definitions
- Queries
- Permissions
- Data organization

### Memory Trick

**Athena = Query, Don't Manage**

---

# Common Use Cases

Athena is useful for:

- Ad hoc analytics
- Log analysis
- Security log queries
- Clickstream analysis
- Application log analysis
- Cost and usage analysis
- Data lake querying
- One-time investigations

---

# Athena + S3

This is the fundamental architecture.

[[S3]]  
↓  
Athena  
↓  
SQL

Athena reads data:

**Directly from S3**

### SAA Principle

> **S3 stores the data**
>
> **Athena analyzes the data**

---

# SQL Queries

Athena lets analysts use:

**SQL**

to query S3-based datasets.

Example concept:

`SELECT customer_id, SUM(amount) FROM orders GROUP BY customer_id;`

Athena reads the relevant objects from:

**S3**

and returns:

**Query results**

---

# Schema-on-Read

Athena commonly uses a:

**Schema-on-read**

approach.

This means:

Data can already exist in S3  
↓  
Schema is defined when querying

rather than requiring all data to be loaded into a rigid database schema first.

### Memory Trick

**S3 stores first**

**Athena understands later**

---

# Supported Data Formats

Athena can query many structured and semi-structured data formats.

Common examples:

- CSV
- JSON
- Apache Parquet
- Apache ORC
- Avro

For the exam, two especially important formats are:

- Parquet
- ORC

because they are:

**Columnar formats**

---

# Columnar Formats

Parquet and ORC organize data by:

**Columns**

rather than storing every row together.

This can make analytical queries:

**Much more efficient**

when only certain columns are needed.

### Killer Exam Clue

> **Reduce Athena query cost and improve performance**
>
> → **Convert data to Parquet or ORC**

---

# Why Columnar Formats Help

Suppose a dataset contains:

50 columns

but the query only needs:

3 columns.

With a columnar format:

Athena can often read:

**Only the needed columns**

instead of scanning:

**Every column**

This reduces:

- Data scanned
- Query time
- Cost

---

# Athena Pricing

Athena is generally priced based on:

**The amount of data scanned by queries**

This creates a major optimization principle:

> **Scan less data = pay less**

### Memory Trick

**Athena Cost = Bytes Scanned**

---

# Reduce Athena Cost

Important ways to reduce:

**Data scanned**

include:

- Use columnar formats
- Compress data
- Partition data
- Avoid `SELECT *`
- Query only required columns
- Filter early

### Killer Exam Pattern

> **Athena costs are too high because queries scan too much S3 data**
>
> → **Partition + Compress + Convert to Parquet/ORC**

---

# Compression

Compressing S3 data can reduce:

**The amount of data Athena must scan**

Common compressed analytical datasets can significantly improve:

- Query cost
- Storage efficiency
- Performance

### SAA Principle

> **Compress data before querying large datasets**

---

# Partitioning

Partitioning organizes data into:

**Logical groups**

Example:

S3:

`logs/year=2026/month=08/day=27/`

Instead of scanning:

**All logs**

Athena can scan only:

`year=2026/month=08/day=27`

### Killer Exam Clue

> **Queries usually filter by date**
>
> → **Partition S3 data by date**

---

# Partition Example

Bad layout:

`S3://logs/file1`

`S3://logs/file2`

`S3://logs/file3`

Better:

`S3://logs/year=2026/month=08/day=27/`

`S3://logs/year=2026/month=08/day=28/`

`S3://logs/year=2026/month=09/day=01/`

Query concept:

`WHERE year = 2026 AND month = 8 AND day = 27`

Athena can scan:

**Only the matching partition**

---

# Partitioning + Columnar Format

A powerful optimization combination:

S3  
↓  
Partitioned by Date  
↓  
Stored as Parquet  
↓  
Athena

This reduces:

- Rows scanned
- Columns scanned
- Query cost
- Query latency

### Memory Trick

**Partition = Read fewer files**

**Parquet = Read fewer columns**

---

# AWS Glue Data Catalog

Athena commonly integrates with:

[[Glue Data Catalog]]

to store:

**Table metadata and schemas**

Architecture:

S3 Data  
↓  
Glue Data Catalog  
↓  
Athena

The catalog describes:

- Databases
- Tables
- Columns
- Data locations
- Partitions

### Killer Exam Clue

> **Athena needs centralized metadata/schema definitions for S3 data**
>
> → **Glue Data Catalog**

---

# Glue Crawlers

A:

**Glue Crawler**

can inspect data stored in places such as S3 and:

**Automatically infer schema**

Then it can populate:

**Glue Data Catalog**

Architecture:

S3  
↓  
Glue Crawler  
↓  
Discover Schema  
↓  
Glue Data Catalog  
↓  
Athena

### Killer Exam Clue

> **Automatically discover the schema of data in S3 for Athena**
>
> → **Glue Crawler**

---

# Athena + Glue Workflow

S3 Data  
↓  
Glue Crawler  
↓  
Glue Data Catalog  
↓  
Athena  
↓  
SQL Query

### Memory Trick

**S3 = Data**

**Glue = Metadata**

**Athena = Query**

---

# Query Results

Athena query results are typically stored in:

**S3**

Architecture:

Athena Query  
↓  
Results  
↓  
S3 Output Location

This means appropriate:

**S3 permissions**

are important.

---

# Athena Permissions

Athena access usually involves permissions for:

- Athena actions
- S3 source data
- S3 query-results location
- Glue Data Catalog
- KMS where encryption is used

### Exam Thinking

If an Athena query gets:

**AccessDenied**

check more than just:

**Athena IAM permissions**

The user may also need access to:

**The underlying S3 data**

---

# Encryption

Athena can work with:

**Encrypted S3 data**

depending on the encryption method and permissions.

Possible encryption architectures may involve:

- SSE-S3
- SSE-KMS

If KMS is involved:

The principal also needs:

**KMS permissions**

---

# Athena + CloudTrail Logs

A common security architecture:

[[06-Security/CloudTrail]]  
↓  
Logs Stored in S3  
↓  
Athena  
↓  
SQL Investigation

Use cases:

- Security analysis
- Audit queries
- Investigating API activity

### Killer Exam Clue

> **Use SQL to analyze CloudTrail logs stored in S3**
>
> → **Athena**

---

# Athena + ALB Logs

Architecture:

[[Application Load Balancer]]  
↓  
Access Logs  
↓  
S3  
↓  
Athena

Use Athena to answer questions such as:

- Which URLs receive most traffic?
- Which IPs generate errors?
- Which requests are slow?

---

# Athena + CloudFront Logs

Architecture:

[[CloudFront]]  
↓  
Logs  
↓  
S3  
↓  
Athena

Useful for:

- Request analysis
- Traffic patterns
- Geographic analysis
- Error investigation

---

# Athena + VPC Flow Logs

When VPC Flow Logs are stored in:

**S3**

Athena can query them with:

**SQL**

Use cases:

- Network troubleshooting
- Security analysis
- Traffic investigation

---

# Athena + Cost and Usage Reports

AWS Cost and Usage Reports can be delivered to:

**S3**

Athena can then query:

**Detailed billing data**

Architecture:

Cost and Usage Report  
↓  
S3  
↓  
Athena

### Killer Exam Clue

> **Run custom SQL analysis on detailed AWS cost reports stored in S3**
>
> → **Athena**

---

# Athena Federated Query

Athena can query data from:

**Sources beyond S3**

through supported federated-query connectors.

Conceptually:

Athena  
↓  
Connector  
↓  
External Data Source

For SAA, the key association remains:

> **Athena's classic use case is serverless SQL on S3**

---

# Athena vs Redshift

This is an important comparison.

## Athena

Think:

- Serverless
- Ad hoc SQL
- Data stays in S3
- Pay per data scanned
- No cluster

## [[04-Databases/Redshift]]

Think:

- Data warehouse
- Complex analytics
- Repeated BI queries
- Large-scale structured analytics
- Provisioned/serverless warehouse architecture

### Killer Shortcut

**Ad hoc SQL directly on S3**
→ Athena

**Enterprise data warehouse**
→ Redshift

---

# Athena vs RDS

## Athena

Think:

**Analytics on S3**

## [[RDS]]

Think:

**Transactional relational database**

Do NOT use Athena as:

**Your application's transactional SQL database**

---

# Athena vs EMR

## Athena

Think:

- SQL
- Serverless
- Minimal setup
- Ad hoc querying

## [[09-Analytics/EMR]]

Think:

- Big data processing
- Spark
- Hadoop
- Large distributed analytics frameworks
- More control over processing

### Killer Shortcut

**Simple SQL on S3**
→ Athena

**Spark/Hadoop big-data processing**
→ EMR

---

# Athena vs Glue

## Athena

**Queries data**

## [[09-Analytics/Glue]]

**Discovers, catalogs, transforms, and prepares data**

### Memory Trick

**Glue = Prepare**

**Athena = Ask Questions**

---

# Athena vs QuickSight

## Athena

Runs:

**SQL queries**

## [[09-Analytics/QuickSight]]

Provides:

**BI dashboards and visualizations**

Architecture:

S3  
↓  
Athena  
↓  
QuickSight

### Memory Trick

**Athena = Query**

**QuickSight = Visualize**

---

# Athena + QuickSight

Architecture:

S3 Data  
↓  
Athena  
↓  
QuickSight  
↓  
Dashboard

This allows organizations to build:

**Visual analytics**

on top of:

**S3-based datasets**

---

# Ad Hoc Analytics

Athena is especially strong when analysts need to:

**Ask occasional questions**

without maintaining:

**A dedicated database cluster**

Example:

> "How many failed logins occurred yesterday?"

CloudTrail Logs  
↓  
S3  
↓  
Athena SQL

---

# Data Lake Architecture

Athena is commonly part of an:

**S3 data lake**

Architecture:

Data Sources  
↓  
S3 Data Lake  
↓  
Glue Data Catalog  
↓  
Athena / EMR / Redshift Spectrum / QuickSight

Athena provides:

**Interactive SQL access**

to the data lake.

---

# Workgroups

Athena:

**Workgroups**

help separate:

- Users
- Teams
- Workloads
- Query settings
- Cost controls

They can help enforce:

**Query limits and configurations**

### Exam Concept

> **Separate Athena workloads and control query usage**
>
> → **Athena Workgroups**

---

# Query Cost Controls

Because Athena charges by:

**Data scanned**

organizations may want to control:

**How much data users can scan**

Workgroups can help with:

**Usage governance**

---

# Performance Optimization

Important Athena optimization strategies:

1. Partition data
2. Use Parquet/ORC
3. Compress files
4. Avoid scanning unnecessary columns
5. Avoid many tiny files
6. Filter on partition keys

---

# Small Files Problem

Huge numbers of:

**Tiny S3 objects**

can reduce analytics efficiency.

Better data organization often uses:

**Reasonably sized analytical files**

rather than millions of:

**Very small objects**

### SAA Principle

> **Optimize both file format and file layout**

---

# CTAS

Athena supports:

**CREATE TABLE AS SELECT — CTAS**

This can create a new table from:

**Query results**

A useful use case is converting data into:

**A more efficient format**

Example concept:

CSV Data  
↓  
Athena CTAS  
↓  
Parquet Data

This can improve future:

**Query performance and cost**

---

# Architecture Thinking

## Scenario 1 — Query Logs

Security team has:

10 TB of logs stored in S3.

Need occasional:

**SQL investigations**

without managing servers.

Choose:

**Athena**

---

## Scenario 2 — Reduce Cost

Athena queries scan:

**Huge CSV files**

and cost too much.

Choose:

- Convert to Parquet/ORC
- Partition data
- Compress data

---

## Scenario 3 — Date-Based Queries

Queries almost always filter by:

**Year/month/day**

Choose:

**Partition S3 dataset by date**

---

## Scenario 4 — Unknown Schema

Millions of JSON files exist in S3.

Need to automatically discover:

**Columns and data types**

Choose:

**Glue Crawler**

---

## Scenario 5 — CloudTrail Investigation

Need to find:

**Who deleted an AWS resource**

CloudTrail logs are in S3.

Choose:

**Athena**

---

## Scenario 6 — Dashboard

Need executives to view:

**Visual dashboards**

based on S3 data.

Choose:

S3  
↓  
Athena  
↓  
[[09-Analytics/QuickSight]]

---

## Scenario 7 — Transaction Processing

Application needs:

- Row updates
- Transactions
- Frequent OLTP queries

Do NOT choose Athena.

Think:

**RDS / Aurora**

---

## Scenario 8 — Data Warehouse

Company needs:

**Repeated complex BI queries**

over a managed warehouse.

Think:

**Redshift**

rather than defaulting to Athena.

---

## Scenario 9 — Spark Processing

Need:

**Large Spark transformations**

Choose:

**EMR**

rather than Athena.

---

# Scenario Recognition

Immediately think:

**Athena**

when you see:

- SQL on S3
- Ad hoc queries
- Serverless analytics
- Log analysis
- CloudTrail analysis
- ALB logs
- CloudFront logs
- Cost and Usage Report
- S3 data lake

---

## Think Glue When You See

- Schema discovery
- Data catalog
- ETL
- Crawlers
- Metadata

---

## Think Parquet/ORC When You See

- Athena cost optimization
- Reduce scanned data
- Faster analytical queries

---

## Think Partitioning When You See

- Query filters by date
- Large S3 dataset
- Reduce scanned files
- Reduce Athena cost

---

# Exam Traps

## Trap 1 — Athena Requires a Database Cluster

❌

Athena is:

**Serverless**

---

## Trap 2 — Athena Loads All Data into a Database Before Querying

❌

It commonly queries:

**S3 directly**

---

## Trap 3 — Athena Pricing Is Mainly Based on Running EC2 Instances

❌

Think:

**Data scanned**

---

## Trap 4 — CSV Is Always the Most Efficient Athena Format

❌

For analytics:

**Parquet / ORC**

are often better.

---

## Trap 5 — Partitioning Increases the Amount of Data Scanned

❌

Good partitioning helps:

**Reduce scanning**

---

## Trap 6 — Athena Is an OLTP Database

❌

It is designed for:

**Analytics**

not transactional application workloads.

---

## Trap 7 — Glue and Athena Are the Same Service

❌

Glue:

**Catalog / ETL**

Athena:

**SQL Queries**

---

## Trap 8 — Query Results Exist Only Temporarily in Memory

❌

Athena query results can be stored in:

**S3**

---

# Quick Cheat Sheet

| Exam Clue | Answer |
|---|---|
| SQL on S3 | Athena |
| Serverless Ad Hoc Analytics | Athena |
| Analyze CloudTrail Logs | Athena |
| Analyze ALB/CloudFront Logs | Athena |
| Cost Based On | Data Scanned |
| Reduce Query Cost | Partition + Parquet/ORC + Compression |
| Discover S3 Schema | Glue Crawler |
| Store Metadata | Glue Data Catalog |
| Dashboard | QuickSight |
| Enterprise Data Warehouse | Redshift |
| Spark/Hadoop | EMR |
| Transactional SQL Database | RDS/Aurora |

---

# Optimization Cheat Sheet

| Problem | Optimization |
|---|---|
| Too Much Data Scanned | Partition |
| Too Many Columns Read | Parquet / ORC |
| Large Raw Files | Compression |
| Queries Use Date Filters | Date Partitions |
| Unknown Schema | Glue Crawler |
| Excessive User Query Spend | Workgroups |

---

# Service Decision

Need:

**Ad hoc SQL directly on S3**

→ Athena

Need:

**ETL / schema discovery**

→ Glue

Need:

**Dashboards**

→ QuickSight

Need:

**Data warehouse**

→ Redshift

Need:

**Spark / Hadoop**

→ EMR

---

# Final Exam Rapid-Fire

> **SQL ON S3**
> → ATHENA
>
> **SERVERLESS ANALYTICS**
> → ATHENA
>
> **COST MODEL**
> → DATA SCANNED
>
> **REDUCE DATA SCANNED**
> → PARTITION
>
> **COLUMNAR FORMAT**
> → PARQUET / ORC
>
> **DISCOVER SCHEMA**
> → GLUE CRAWLER
>
> **STORE METADATA**
> → GLUE DATA CATALOG
>
> **CLOUDTRAIL LOG QUERY**
> → ATHENA
>
> **COST & USAGE REPORT ANALYSIS**
> → ATHENA
>
> **DASHBOARD**
> → QUICKSIGHT
>
> **WAREHOUSE**
> → REDSHIFT
>
> **SPARK / HADOOP**
> → EMR
>
> **OLTP**
> → NOT ATHENA

---

## Master Memory Trick

> [!tip] Athena Master Memory Trick
> Imagine S3 is:
>
> **A giant warehouse full of files**
>
> You do not want to move all the boxes into a database just to ask:
>
> **"How many blue boxes were shipped yesterday?"**
>
> Athena walks into the warehouse and says:
>
> **"I'll run SQL right here."**
>
> That's:
>
> **ATHENA**
>
> To make Athena cheaper:
>
> **PARTITION**
> → Tell Athena which aisle to search
>
> **PARQUET / ORC**
> → Tell Athena which columns on the boxes to inspect
>
> **COMPRESSION**
> → Make the warehouse smaller
>
> **GLUE CATALOG**
> → Give Athena a map of the warehouse
>
> So remember:
>
> **S3**
> → DATA
>
> **GLUE**
> → SCHEMA
>
> **ATHENA**
> → SQL
>
> **QUICKSIGHT**
> → DASHBOARD
>
> And the killer SAA clue:
>
> **"Query data already stored in S3 using SQL without provisioning infrastructure."**
>
> → **Athena**

---

## Related Notes

- [[S3]]
- [[09-Analytics/Glue]]
- [[Glue Data Catalog]]
- [[09-Analytics/QuickSight]]
- [[04-Databases/Redshift]]
- [[09-Analytics/EMR]]
- [[06-Security/CloudTrail]]
- [[CloudFront]]
- [[Application Load Balancer]]
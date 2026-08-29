## What Problem Does It Solve?

[[Glue]] is AWS's:

**Serverless data integration and ETL service**

It helps discover, prepare, transform, and move data for:

- Analytics
- Data lakes
- Data warehouses
- Machine learning
- Reporting

Architecture:

Raw Data  
↓  
Glue  
↓  
Clean / Transform / Catalog  
↓  
Analytics Services

> [!tip] Memory Trick
> **Glue = Prepare and connect data**
>
> Think:
>
> **DISCOVER → CATALOG → TRANSFORM**

---

## Core Concept

Glue helps solve the problem:

> **"How do I understand and prepare data before analytics?"**

Typical flow:

S3 Raw Data  
↓  
Glue Crawler  
↓  
Glue Data Catalog  
↓  
Glue ETL Job  
↓  
Clean Data  
↓  
Athena / Redshift / QuickSight

### Killer Exam Clue

> **Need a serverless ETL service to discover and transform data**
>
> → **Glue**

---

# Serverless

Glue is:

**Serverless**

AWS manages:

- Infrastructure
- Capacity
- Scaling
- Underlying servers

You focus on:

- Data sources
- Schemas
- ETL logic
- Jobs
- Workflows

### Memory Trick

**Glue = ETL without managing servers**

---

# ETL

ETL stands for:

**Extract, Transform, Load**

### Extract

Read data from:

- S3
- Databases
- Data stores

### Transform

Clean or modify the data.

Examples:

- Rename columns
- Convert formats
- Filter rows
- Join datasets
- Remove bad records

### Load

Write transformed data to:

- S3
- Redshift
- Other supported targets

### Memory Trick

**E = GET**

**T = CHANGE**

**L = PUT**

---

# Glue Data Catalog

The:

[[Glue Data Catalog]]

is a centralized:

**Metadata repository**

It stores information about:

- Databases
- Tables
- Columns
- Data types
- Partitions
- Data locations

Architecture:

S3 Data  
↓  
Glue Data Catalog  
↓  
Athena / EMR / Redshift Spectrum

### Killer Exam Clue

> **Need a central metadata catalog for an S3 data lake**
>
> → **Glue Data Catalog**

---

# Metadata vs Data

The Glue Data Catalog stores:

**Metadata**

not:

**The actual dataset**

Example:

Actual files  
→ S3

Table definition  
→ Glue Data Catalog

### Memory Trick

**S3 = Data**

**Glue Catalog = Map of the Data**

---

# Glue Crawlers

A:

**Glue Crawler**

automatically scans data sources and:

**Infers schema**

It can then create or update:

**Glue Data Catalog tables**

Architecture:

S3  
↓  
Glue Crawler  
↓  
Discover Schema  
↓  
Glue Data Catalog

### Killer Exam Clue

> **Automatically discover schemas in S3**
>
> → **Glue Crawler**

---

# What Crawlers Discover

A crawler can identify:

- Columns
- Data types
- Partitions
- File formats
- Table structure

This reduces:

**Manual schema definition**

---

# Glue Crawler + Athena

Classic architecture:

S3  
↓  
Glue Crawler  
↓  
Glue Data Catalog  
↓  
[[Athena]]

Athena then uses:

**The catalog metadata**

to query:

**The S3 data**

### Memory Trick

**Crawler = Discover**

**Catalog = Remember**

**Athena = Query**

---

# Glue Crawler + Redshift Spectrum

Architecture:

S3  
↓  
Glue Crawler  
↓  
Glue Data Catalog  
↓  
[[Redshift]] Spectrum

Spectrum can use the catalog to understand:

**External S3 tables**

---

# Glue Crawler + EMR

[[EMR]] can also use:

**Glue Data Catalog**

for shared table metadata.

This helps multiple analytics services use:

**The same schema definitions**

---

# Glue ETL Jobs

A:

**Glue ETL Job**

performs:

**Data transformation**

Architecture:

Source Data  
↓  
Glue Job  
↓  
Transform  
↓  
Target Data

Use cases:

- Clean data
- Join datasets
- Convert formats
- Filter records
- Normalize fields

---

# Glue ETL Engine

Glue ETL commonly uses:

**Apache Spark**

under the hood for distributed processing.

This allows:

**Large-scale transformation**

without manually operating:

**A Spark cluster**

### Killer Exam Clue

> **Need serverless Spark-based ETL**
>
> → **Glue**

---

# Glue vs EMR for Spark

Both can use:

**Spark**

but the use cases differ.

## Glue

Think:

- Serverless ETL
- Data preparation
- Managed jobs
- Minimal infrastructure management

## [[EMR]]

Think:

- Broader big data platform
- More framework flexibility
- Cluster-level control
- Spark/Hadoop ecosystem

### Killer Shortcut

**Serverless ETL**
→ Glue

**Full big data platform**
→ EMR

---

# Glue Job Scripts

Glue can generate or run:

**ETL scripts**

commonly using languages such as:

- Python
- Scala

For SAA, the important concept is:

> **Glue executes managed data-transformation jobs**

---

# Glue Studio

Glue Studio provides:

**Visual ETL authoring**

This can help users build:

**Data transformation pipelines**

with less manual code.

### Exam Concept

> **Need a visual interface for building Glue ETL jobs**
>
> → **Glue Studio**

---

# Glue DataBrew

Glue DataBrew focuses on:

**Visual data preparation**

for analysts and data users.

It helps perform tasks such as:

- Cleaning
- Normalization
- Transformation

without writing extensive code.

### Memory Trick

**DataBrew = Prepare data visually**

---

# Glue Workflows

Glue Workflows can coordinate:

**Multiple Glue activities**

Examples:

Crawler  
↓  
ETL Job  
↓  
Another Job

This provides:

**Managed orchestration for Glue-specific pipelines**

---

# Glue Triggers

Glue:

**Triggers**

can start jobs based on:

- Schedule
- Event
- Completion of another job

Architecture:

Trigger  
↓  
Glue Job

---

# Scheduled ETL

Example:

Every Night  
↓  
Glue Trigger  
↓  
ETL Job  
↓  
S3 Curated Data

### Killer Exam Clue

> **Run a nightly serverless ETL transformation**
>
> → **Glue Job + Schedule/Trigger**

---

# Glue + EventBridge

[[20-SAA/10-Messaging/EventBridge]] can participate in:

**Event-driven data-processing workflows**

Example:

Data Event  
↓  
EventBridge  
↓  
Glue Job / Workflow

This can help make pipelines:

**Event driven**

rather than purely scheduled.

---

# Glue + Step Functions

[[Step Functions]] can orchestrate:

**Glue jobs**

inside larger workflows.

Architecture:

Step Functions  
↓  
Glue ETL Job  
↓  
Wait for Completion  
↓  
Next Step

### Killer Exam Clue

> **Glue transformation is one step inside a larger multi-service workflow**
>
> → **Step Functions + Glue**

---

# Glue + S3

One of the most common patterns:

Raw Data  
↓  
[[S3]] Raw Zone  
↓  
Glue ETL  
↓  
S3 Curated Zone

This is common in:

**Data lake architectures**

---

# Raw vs Curated Data

### Raw Zone

Contains:

**Original incoming data**

### Curated Zone

Contains:

**Cleaned, transformed, analytics-ready data**

Architecture:

Raw S3  
↓  
Glue  
↓  
Curated S3

---

# Format Conversion

Glue can convert:

**Raw row-oriented formats**

into:

**Efficient analytical formats**

Example:

CSV  
↓  
Glue  
↓  
Parquet

This can greatly improve:

[[Athena]]

query performance and cost.

### Killer Exam Clue

> **Convert CSV files in S3 to Parquet for cheaper Athena queries**
>
> → **Glue ETL**

---

# Partitioning Data

Glue ETL jobs can organize output using:

**Partitions**

Example:

`s3://data/year=2026/month=08/day=27/`

This helps Athena:

**Scan less data**

### Memory Trick

**Glue prepares the layout**

**Athena benefits from it**

---

# Glue + Redshift

Architecture:

Source Data  
↓  
Glue ETL  
↓  
[[Redshift]]

Glue can prepare and load data into:

**A data warehouse**

### Killer Exam Pattern

> **Serverless ETL before loading into Redshift**
>
> → **Glue + Redshift**

---

# Glue + Athena

Architecture:

Raw S3  
↓  
Glue ETL  
↓  
Optimized S3  
↓  
Athena

Use Glue to:

- Clean
- Partition
- Compress
- Convert to Parquet

Then use Athena to:

**Query**

---

# Glue + QuickSight

Typical architecture:

S3  
↓  
Glue  
↓  
Athena / Redshift  
↓  
[[QuickSight]]

Glue prepares:

**The data**

QuickSight:

**Visualizes**

---

# Glue + JDBC Data Sources

Glue can connect to supported relational data sources through:

**JDBC**

Examples can include:

- RDS
- Databases in VPCs
- External relational databases

This allows ETL jobs to move data between:

**Databases and analytics platforms**

---

# Glue in a VPC

If Glue needs to access:

**Private resources**

such as:

[[RDS]]

inside a VPC,

the Glue job can be configured with:

**VPC networking**

Architecture:

Glue  
↓  
VPC  
↓  
Private Database

---

# Connections

Glue:

**Connections**

store information needed to connect to:

**External data stores**

Examples:

- JDBC configuration
- Network information

For sensitive credentials:

Use secure integration with:

**Secrets Manager**

where appropriate.

---

# Glue + Secrets Manager

Database credentials should not be:

**Hardcoded in ETL scripts**

Better:

Glue  
↓  
[[Secrets Manager]]  
↓  
Credential  
↓  
Database

### SAA Principle

> **Keep secrets outside ETL code**

---

# Job Bookmarks

Glue:

**Job Bookmarks**

help track:

**Previously processed data**

This allows subsequent ETL job runs to process:

**Only new data**

instead of reprocessing:

**Everything**

### Killer Exam Clue

> **Glue job should process only newly arrived data**
>
> → **Job Bookmarks**

### Memory Trick

**Bookmark = Remember where you stopped**

---

# Incremental ETL

Without job bookmarks:

Day 1 Data  
Day 2 Data  
Day 3 Data  
↓  
Every Job Reprocesses Everything

With bookmarks:

Previous Data  
→ Already Processed

New Data  
→ Process Now

This can reduce:

- Processing time
- Cost
- Duplicate work

---

# Glue DynamicFrames

Glue commonly uses:

**DynamicFrames**

for ETL operations.

They are designed to handle:

**Semi-structured data**

and evolving schemas.

For SAA, the broad takeaway is:

> **Glue is designed for flexible data-transformation workflows**

---

# Schema Evolution

Data structures can change over time.

Glue can help manage:

**Changing schemas**

through:

- Crawlers
- Catalog updates
- Flexible ETL processing

This is useful in:

**Data lakes**

where source data may evolve.

---

# Glue Schema Registry

Glue Schema Registry can help manage:

**Schemas for streaming applications**

This can support:

- Schema versioning
- Compatibility
- Structured streaming data

### Exam Concept

> **Need centralized schema management for streaming data**
>
> → **Glue Schema Registry**

---

# Data Quality

Glue provides capabilities for:

**Data quality checks**

to help identify:

- Missing values
- Invalid data
- Rule violations
- Unexpected changes

For SAA, remember the broader architecture concept:

> **Glue can prepare and validate data before analytics**

---

# Glue Data Catalog as Shared Catalog

A major AWS analytics pattern:

S3  
↓  
Glue Data Catalog  
↓  
├── Athena
├── EMR
└── Redshift Spectrum

This avoids maintaining:

**Separate schemas in every analytics service**

### Killer Exam Clue

> **Multiple AWS analytics services need a common metadata catalog**
>
> → **Glue Data Catalog**

---

# Glue vs Athena

## [[Athena]]

Think:

**Query data**

## Glue

Think:

**Prepare/catalog data**

### Memory Trick

**Glue = Prepare**

**Athena = Query**

---

# Glue vs Redshift

## [[Redshift]]

Think:

**Data warehouse**

## Glue

Think:

**ETL into or around the warehouse**

Architecture:

Raw Data  
↓  
Glue  
↓  
Redshift

---

# Glue vs EMR

## Glue

Think:

- Serverless ETL
- Minimal operations
- Catalog
- Crawlers

## [[EMR]]

Think:

- Full Spark/Hadoop ecosystem
- Large distributed applications
- Greater cluster/runtime control

---

# Glue vs Lambda

## [[Lambda]]

Think:

- Event-driven functions
- Short tasks
- 15-minute maximum

## Glue

Think:

- ETL
- Large datasets
- Distributed Spark processing
- Data preparation

### Killer Shortcut

**Small event-driven transformation**
→ Lambda

**Large ETL dataset**
→ Glue

---

# Glue vs Step Functions

## Glue

Does:

**Data transformation**

## [[Step Functions]]

Coordinates:

**Workflow steps**

They can work together.

### Memory Trick

**Glue = Worker**

**Step Functions = Manager**

---

# Glue vs DataSync

Do not confuse:

**Data movement**

with:

**Data transformation**

### DataSync

Think:

**Move files/data**

### Glue

Think:

**Transform data**

---

# Glue vs DMS

### DMS

Think:

**Database migration / replication**

### Glue

Think:

**ETL and analytics preparation**

### Killer Shortcut

**Move/replicate database**
→ DMS

**Transform database data**
→ Glue

---

# Cost Thinking

Glue charges based on:

**Resources consumed by jobs and related services**

For SAA, the key cost idea is:

> **Use efficient incremental processing rather than repeatedly transforming all historical data**

Job Bookmarks can help.

---

# Architecture Thinking

## Scenario 1 — Discover S3 Schema

Millions of JSON files arrive in S3.

Need to automatically determine:

- Fields
- Data types
- Partitions

Choose:

**Glue Crawler**

---

## Scenario 2 — Shared Analytics Catalog

Athena, EMR, and Redshift Spectrum all need:

**The same S3 table metadata**

Choose:

**Glue Data Catalog**

---

## Scenario 3 — CSV to Parquet

Athena costs are high because data is:

**Large CSV**

Need efficient transformation.

Choose:

Glue ETL  
↓  
Parquet  
↓  
Athena

---

## Scenario 4 — Nightly ETL

Every night:

Raw S3 files  
↓  
Clean and transform  
↓  
Load to Redshift

Choose:

**Glue ETL Job**

---

## Scenario 5 — Only New Data

Daily job currently reprocesses:

**Three years of historical data**

Need to process:

**Only new records**

Choose:

**Glue Job Bookmarks**

---

## Scenario 6 — Spark with Minimal Ops

Need:

**Distributed Spark ETL**

but do not want to manage:

**EMR clusters**

Choose:

**Glue**

---

## Scenario 7 — Full Hadoop Ecosystem

Need:

- Hadoop
- HBase
- Deep cluster customization

Think:

**EMR**

rather than Glue.

---

## Scenario 8 — Query Only

Data is already clean and cataloged in S3.

Need:

**Ad hoc SQL**

Do NOT run Glue unnecessarily.

Choose:

**Athena**

---

## Scenario 9 — Complex Workflow

After Glue job:

1. Run Athena validation
2. Start ML job
3. Notify operations

Choose:

**Step Functions**

to orchestrate the overall process.

---

## Scenario 10 — Private RDS Source

Glue ETL job must extract from:

**Private RDS**

Choose:

**Glue VPC connectivity**

with appropriate:

- Networking
- Security groups
- Permissions

---

# Scenario Recognition

Immediately think:

**Glue**

when you see:

- ETL
- Data integration
- Data preparation
- Serverless Spark ETL
- Schema discovery
- Data catalog
- Crawlers
- Transform S3 data
- Convert CSV to Parquet

---

## Think Glue Crawler When You See

- Automatically discover schema
- Detect partitions
- Populate catalog
- Unknown S3 structure

---

## Think Glue Data Catalog When You See

- Central metadata
- Shared schema
- Athena metadata
- Spectrum external tables
- Shared analytics catalog

---

## Think Job Bookmarks When You See

- Incremental ETL
- Only process new data
- Avoid reprocessing old files

---

# Exam Traps

## Trap 1 — Glue Data Catalog Stores the Actual Dataset

❌

It stores:

**Metadata**

Actual data may live in:

**S3 or another data store**

---

## Trap 2 — Glue Crawler Transforms Data

❌

Crawler:

**Discovers schema**

ETL Job:

**Transforms data**

---

## Trap 3 — Glue and Athena Are the Same Service

❌

Glue:

**Prepare / Catalog**

Athena:

**Query**

---

## Trap 4 — Glue Is Only a Database Migration Tool

❌

That points more toward:

**DMS**

Glue is:

**Data integration / ETL**

---

## Trap 5 — Every Spark Workload Should Use Glue

❌

For broader cluster control and Hadoop ecosystem workloads:

Think:

**EMR**

---

## Trap 6 — Job Bookmarks Improve Dashboard Visualization

❌

They help:

**Incremental ETL processing**

---

## Trap 7 — Glue Crawler Is Required Before Every Athena Query

❌

Schemas can also be:

**Defined manually**

Crawler is useful for:

**Automatic discovery**

---

## Trap 8 — Glue Is Primarily a BI Dashboard Service

❌

Think:

**QuickSight**

---

# Quick Cheat Sheet

| Exam Clue | Answer |
|---|---|
| Serverless ETL | Glue |
| Discover Schema | Glue Crawler |
| Central Metadata Catalog | Glue Data Catalog |
| Transform Data | Glue ETL Job |
| CSV → Parquet | Glue |
| Incremental ETL | Job Bookmarks |
| Visual ETL Design | Glue Studio |
| Visual Data Preparation | DataBrew |
| Shared Athena/EMR/Spectrum Metadata | Glue Data Catalog |
| SQL on S3 | Athena |
| Big Data Platform | EMR |
| Data Warehouse | Redshift |
| BI Dashboard | QuickSight |

---

# Glue Component Cheat Sheet

| Component | Think |
|---|---|
| Crawler | DISCOVER |
| Data Catalog | REMEMBER |
| ETL Job | TRANSFORM |
| Job Bookmark | CONTINUE |
| Studio | BUILD VISUALLY |
| DataBrew | CLEAN VISUALLY |
| Workflow | COORDINATE GLUE TASKS |

---

# Analytics Pipeline Shortcut

> **RAW DATA**
> → S3
>
> **DISCOVER**
> → GLUE CRAWLER
>
> **CATALOG**
> → GLUE DATA CATALOG
>
> **TRANSFORM**
> → GLUE ETL
>
> **QUERY**
> → ATHENA
>
> **WAREHOUSE**
> → REDSHIFT
>
> **VISUALIZE**
> → QUICKSIGHT

---

# Final Exam Rapid-Fire

> **SERVERLESS ETL**
> → GLUE
>
> **DISCOVER S3 SCHEMA**
> → GLUE CRAWLER
>
> **CENTRAL METADATA**
> → GLUE DATA CATALOG
>
> **TRANSFORM DATA**
> → GLUE ETL JOB
>
> **CSV → PARQUET**
> → GLUE
>
> **ONLY NEW DATA**
> → JOB BOOKMARK
>
> **VISUAL ETL**
> → GLUE STUDIO
>
> **VISUAL DATA CLEANING**
> → DATABREW
>
> **SHARED ATHENA/EMR/SPECTRUM SCHEMA**
> → GLUE DATA CATALOG
>
> **SQL ON S3**
> → ATHENA
>
> **SPARK/HADOOP PLATFORM**
> → EMR
>
> **WAREHOUSE**
> → REDSHIFT
>
> **DASHBOARD**
> → QUICKSIGHT

---

## Master Memory Trick

> [!tip] Glue Master Memory Trick
> Imagine a huge warehouse full of messy data.
>
> First someone walks through and identifies:
>
> **WHAT'S IN EVERY BOX**
>
> That's:
>
> **GLUE CRAWLER**
>
> They write everything into:
>
> **THE MASTER INVENTORY**
>
> That's:
>
> **GLUE DATA CATALOG**
>
> Then workers:
>
> **CLEAN, CONVERT, AND REORGANIZE THE BOXES**
>
> That's:
>
> **GLUE ETL**
>
> They leave a bookmark so tomorrow they know:
>
> **WHERE THEY STOPPED**
>
> That's:
>
> **JOB BOOKMARKS**

So remember:

> **CRAWLER**
> → DISCOVER
>
> **CATALOG**
> → METADATA
>
> **ETL**
> → TRANSFORM
>
> **BOOKMARK**
> → PROCESS ONLY NEW DATA
>
> **ATHENA**
> → QUERY
>
> **REDSHIFT**
> → WAREHOUSE
>
> **QUICKSIGHT**
> → VISUALIZE
>
> **EMR**
> → BIG DATA PLATFORM

And the killer SAA question:

> **"Does the data need to be discovered, cataloged, or transformed before analytics?"**
>
> YES
>
> → **Glue**

---

## Related Notes

- [[Athena]]
- [[Redshift]]
- [[EMR]]
- [[QuickSight]]
- [[Glue Data Catalog]]
- [[S3]]
- [[Step Functions]]
- [[20-SAA/10-Messaging/EventBridge]]
- [[RDS]]
- [[Secrets Manager]]
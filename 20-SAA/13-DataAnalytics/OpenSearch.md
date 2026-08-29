## What Problem Does It Solve?

[[OpenSearch]] is AWS's managed service for:

**Search, indexing, log analytics, and near-real-time data analysis**

It is commonly used when applications need to:

- Search large amounts of text
- Index application data
- Analyze logs
- Search product catalogs
- Perform full-text search
- Build operational analytics dashboards

Architecture:

Data Sources  
↓  
OpenSearch  
↓  
Index + Search  
↓  
Search Results / Dashboards

> [!tip] Memory Trick
> **OpenSearch = SEARCH**
>
> Think:
>
> **INDEX → SEARCH → ANALYZE**

---

## Core Concept

Traditional relational databases are excellent for:

**Structured queries**

But they are not always ideal for:

**Complex full-text search**

Example:

User searches:

`"wireless noise cancelling headphones"`

OpenSearch can search:

**Indexed documents**

and return:

**Relevant matching results**

### Killer Exam Clue

> **Need full-text search across large amounts of application data**
>
> → **OpenSearch**

---

# What Is an Index?

OpenSearch stores searchable data in:

**Indexes**

An index contains:

**Documents**

Architecture:

OpenSearch  
↓  
Index  
↓  
Documents

Think of an index like:

**A searchable collection of related data**

---

# Documents

A:

**Document**

is a searchable unit of data.

Example:

`{"product":"Wireless Headphones","brand":"ExampleBrand","category":"Electronics","description":"Noise cancelling wireless headphones"}`

OpenSearch indexes fields so applications can:

**Search them efficiently**

---

# Full-Text Search

One of OpenSearch's strongest use cases is:

**Full-text search**

Example:

Product Catalog  
↓  
OpenSearch  
↓  
Customer searches "black running shoes"  
↓  
Relevant Products

### Killer Exam Clue

> **Add a search box to an application that searches product descriptions**
>
> → **OpenSearch**

---

# Search Relevance

OpenSearch can rank results based on:

**Relevance**

This differs from a simple database lookup.

Example:

Search:

`cloud architecture`

OpenSearch can return documents that are:

**Most relevant**

rather than only performing:

**Exact-value matching**

---

# OpenSearch Dashboards

OpenSearch includes:

**OpenSearch Dashboards**

for visualizing and exploring:

**Indexed data**

Common uses:

- Log analysis
- Operational dashboards
- Security analytics
- Search analytics

### Memory Trick

**OpenSearch = Search Engine**

**OpenSearch Dashboards = Visualize Search Data**

---

# Log Analytics

A major OpenSearch use case is:

**Centralized log analytics**

Architecture:

Applications  
↓  
Logs  
↓  
OpenSearch  
↓  
OpenSearch Dashboards

Teams can:

- Search logs
- Filter errors
- Investigate incidents
- Visualize trends

### Killer Exam Clue

> **Need centralized searchable application logs**
>
> → **OpenSearch**

---

# Near-Real-Time Analytics

OpenSearch is designed for:

**Near-real-time search and analytics**

Data can be:

1. Generated
2. Ingested
3. Indexed
4. Searched shortly afterward

This makes it useful for:

**Operational analytics**

---

# OpenSearch + Kinesis Data Firehose

A classic streaming architecture:

Applications  
↓  
[[Kinesis Data Firehose]]  
↓  
OpenSearch  
↓  
OpenSearch Dashboards

Firehose provides:

**Managed streaming delivery**

OpenSearch provides:

**Search and analytics**

### Killer Exam Clue

> **Continuously deliver logs into a searchable analytics platform**
>
> → **Firehose + OpenSearch**

---

# OpenSearch + Kinesis Data Streams

Architecture:

Applications  
↓  
[[Kinesis Data Streams]]  
↓  
Consumer  
↓  
OpenSearch

Use Data Streams when you need:

- Custom processing
- Replay
- Multiple consumers

before or alongside:

**OpenSearch indexing**

---

# OpenSearch + Lambda

[[Lambda]] can process events and write:

**Documents**

into OpenSearch.

Architecture:

Event  
↓  
Lambda  
↓  
Transform  
↓  
OpenSearch

Useful when:

**Custom event transformation**

is needed before indexing.

---

# OpenSearch + S3

A common pattern:

Application Data  
↓  
[[S3]]  
↓  
Processing / Ingestion  
↓  
OpenSearch

S3 is useful for:

**Durable storage**

while OpenSearch provides:

**Fast search**

### Memory Trick

**S3 = Store**

**OpenSearch = Search**

---

# OpenSearch + CloudWatch Logs

Operational logs can be moved through supported integrations into:

**OpenSearch**

for:

**Advanced searching and visualization**

Architecture:

Application  
↓  
[[07-Monitoring/CloudWatch]] Logs  
↓  
Processing / Subscription  
↓  
OpenSearch

### Killer Exam Pattern

> **Search and analyze application logs beyond basic log storage**
>
> → **OpenSearch**

---

# OpenSearch + DynamoDB

A common architecture:

Application  
↓  
[[DynamoDB]]  
↓  
DynamoDB Streams  
↓  
Lambda  
↓  
OpenSearch

Why?

DynamoDB provides:

**Primary application storage**

OpenSearch provides:

**Advanced search**

### Killer Exam Clue

> **DynamoDB application needs full-text search**
>
> → **DynamoDB Streams + Lambda + OpenSearch**

---

# Why Not Search DynamoDB Directly?

DynamoDB is optimized for:

**Known access patterns using keys and indexes**

It is not primarily designed for:

**Arbitrary full-text search**

Therefore:

DynamoDB  
→ Store application records

OpenSearch  
→ Search those records

### Memory Trick

**DynamoDB = FIND BY KEY**

**OpenSearch = SEARCH BY WORDS**

---

# OpenSearch + RDS

Similar architecture:

[[RDS]]  
↓  
Data Replication / Processing  
↓  
OpenSearch

RDS remains:

**System of record**

OpenSearch provides:

**Search capability**

---

# Search Engine vs Primary Database

OpenSearch should generally not be treated as:

**The primary transactional database**

Instead:

Primary Database  
↓  
Replicate / Index  
↓  
OpenSearch

Example:

DynamoDB  
↓  
OpenSearch

### SAA Principle

> **Use the database as the system of record and OpenSearch as the search/index layer**

---

# OpenSearch Cluster Architecture

Traditional managed OpenSearch deployments use:

**OpenSearch domains**

A domain contains the infrastructure required to run:

**An OpenSearch cluster**

Architecture:

OpenSearch Domain  
↓  
Data Nodes  
↓  
Indexes  
↓  
Documents

---

# Data Nodes

Data nodes handle:

- Indexing
- Searching
- Data storage
- Query processing

They hold:

**The indexed data**

---

# Dedicated Cluster Manager Nodes

Dedicated cluster manager nodes help manage:

**Cluster state**

They coordinate tasks such as:

- Index management
- Node tracking
- Cluster coordination

They do NOT primarily exist to:

**Handle application search traffic**

### Memory Trick

**Cluster Manager = Manage**

**Data Node = Store + Search**

---

# Multi-AZ Deployment

OpenSearch can distribute nodes across:

**Multiple Availability Zones**

This improves:

- Availability
- Fault tolerance
- Resilience

### Killer Exam Clue

> **Need highly available OpenSearch cluster**
>
> → **Multi-AZ deployment**

---

# Zone Awareness

OpenSearch:

**Zone Awareness**

distributes cluster resources across:

**Availability Zones**

This reduces the impact of:

**An AZ failure**

### Memory Trick

**Zone Awareness = Don't put the whole search cluster in one AZ**

---

# Replicas

OpenSearch indexes can use:

**Replica shards**

Replica shards provide:

- Redundant copies
- Higher availability
- Additional read/search capacity

### Killer Exam Concept

> **Replicas improve availability and can improve read/search performance**

---

# Primary Shards

An index is divided into:

**Primary shards**

These distribute:

**Indexed data**

across the cluster.

Architecture:

Index  
↓  
├── Primary Shard 1  
├── Primary Shard 2  
└── Primary Shard 3

---

# Primary vs Replica Shards

## Primary Shard

Contains:

**Original indexed data partition**

## Replica Shard

Contains:

**Copy of a primary shard**

### Memory Trick

**Primary = Original**

**Replica = Copy**

---

# Scaling

OpenSearch can scale by adjusting:

- Instance types
- Number of data nodes
- Storage
- Shard architecture

For read-heavy workloads:

**Replica shards**

can help distribute searches.

---

# Storage

OpenSearch domains commonly use:

**EBS volumes**

for persistent storage attached to:

**Data nodes**

Storage design depends on:

- Dataset size
- Performance requirements
- Retention requirements

---

# UltraWarm

OpenSearch provides:

**UltraWarm**

for:

**Older, less frequently accessed data**

It provides lower-cost storage compared with keeping all data on:

**Hot data nodes**

### Killer Exam Clue

> **Keep older searchable OpenSearch data at lower cost**
>
> → **UltraWarm**

---

# Hot Storage

Hot data is stored on:

**Data nodes**

and is optimized for:

**Frequently accessed data**

Think:

Recent Logs  
→ Hot

Older Logs  
→ UltraWarm

---

# Cold Storage

OpenSearch can provide:

**Cold storage**

for even less frequently accessed data.

This helps reduce costs for:

**Long-term searchable datasets**

### Memory Trick

**HOT = Frequent**

**WARM = Less Frequent**

**COLD = Rare**

---

# Hot-Warm-Cold Architecture

Example:

Today's Logs  
↓  
Hot

Last Month's Logs  
↓  
UltraWarm

Historical Logs  
↓  
Cold

### Killer Exam Pattern

> **Large log analytics environment needs lower-cost retention for older data**
>
> → **Hot / UltraWarm / Cold architecture**

---

# OpenSearch Serverless

OpenSearch also provides:

**OpenSearch Serverless**

This allows you to run search and analytics workloads without manually managing:

**Clusters**

AWS manages much of:

- Infrastructure
- Scaling
- Capacity

### Killer Exam Clue

> **Need OpenSearch without provisioning and managing clusters**
>
> → **OpenSearch Serverless**

---

# Provisioned vs Serverless

## Provisioned OpenSearch

Think:

- Domain
- Nodes
- Instance sizing
- More infrastructure control

## OpenSearch Serverless

Think:

- No cluster management
- Automatic scaling
- Lower operational overhead

### Memory Trick

**Provisioned = Control**

**Serverless = Simplicity**

---

# Security

OpenSearch supports security controls involving:

- IAM
- Encryption
- Network access
- Fine-grained access control

For SAA, recognize:

**Search clusters may contain sensitive application and log data**

---

# IAM

IAM can control:

**Who can access OpenSearch APIs and resources**

Use:

**Least privilege**

---

# Fine-Grained Access Control

OpenSearch can provide:

**Fine-grained permissions**

for controlling access to:

- Indexes
- Documents
- Fields

depending on configuration.

### Exam Principle

> **Different users may require different levels of access to search data**

---

# Encryption at Rest

OpenSearch supports:

**Encryption at rest**

using:

[[06-Security/KMS]]

This protects:

**Stored indexes and associated data**

---

# Encryption in Transit

OpenSearch supports:

**HTTPS / TLS**

for protecting data:

**In transit**

---

# VPC Deployment

OpenSearch domains can be deployed inside:

**A VPC**

This allows:

**Private network access**

Architecture:

Application  
↓  
Private VPC Network  
↓  
OpenSearch

### Killer Exam Clue

> **OpenSearch must not be publicly accessible**
>
> → **Deploy it inside a VPC**

---

# Security Groups

When OpenSearch is deployed inside a VPC:

**Security groups**

can help control:

**Network access**

to the domain.

---

# Cognito Integration

OpenSearch Dashboards can integrate with:

[[Cognito]]

for:

**User authentication**

This can provide controlled access to:

**Dashboards**

### Killer Exam Clue

> **Need user authentication for OpenSearch Dashboards**
>
> → **Cognito integration**

---

# OpenSearch vs CloudWatch Logs

## [[07-Monitoring/CloudWatch]]

Think:

- Collect logs
- Store logs
- Monitor AWS resources
- Metrics
- Alarms

## OpenSearch

Think:

- Advanced log searching
- Indexing
- Analytics
- Search dashboards

### Killer Shortcut

**Monitor AWS metrics**
→ CloudWatch

**Search/index huge volumes of logs**
→ OpenSearch

---

# OpenSearch vs Athena

## [[Athena]]

Think:

**SQL queries against data in S3**

## OpenSearch

Think:

**Indexed search**

Example:

Need:

SQL analysis of historical Parquet files  
→ Athena

Need:

Full-text search across log messages  
→ OpenSearch

### Memory Trick

**Athena = SQL**

**OpenSearch = SEARCH**

---

# OpenSearch vs Redshift

## [[Redshift]]

Think:

**Data warehouse / OLAP**

## OpenSearch

Think:

**Search and log analytics**

### Killer Shortcut

**Business warehouse**
→ Redshift

**Full-text/log search**
→ OpenSearch

---

# OpenSearch vs QuickSight

## [[QuickSight]]

Think:

**Business intelligence dashboards**

## OpenSearch

Think:

**Search/log analytics dashboards**

### Memory Trick

**QuickSight = Business BI**

**OpenSearch = Search / Logs**

---

# OpenSearch vs DynamoDB

## [[DynamoDB]]

Think:

- NoSQL database
- Millisecond key-value/document access
- Known access patterns

## OpenSearch

Think:

- Full-text search
- Flexible search
- Search relevance
- Log analytics

### Killer Exam Pattern

> **Need both high-scale NoSQL storage and full-text search**
>
> → **DynamoDB + OpenSearch**

---

# OpenSearch vs RDS

## [[RDS]]

Think:

- Relational database
- SQL
- Transactions
- Structured relationships

## OpenSearch

Think:

- Search engine
- Text search
- Indexed documents
- Log analytics

---

# OpenSearch vs S3

## [[S3]]

Think:

**Durable object storage**

## OpenSearch

Think:

**Fast indexed search**

A common architecture uses:

**Both**

S3  
→ Durable archive

OpenSearch  
→ Searchable index

---

# OpenSearch vs Kinesis

## [[Kinesis Data Streams]]

Think:

**Transport streaming data**

## OpenSearch

Think:

**Index and search the data**

Architecture:

Kinesis  
↓  
Processing / Firehose  
↓  
OpenSearch

---

# OpenSearch vs Firehose

## [[Kinesis Data Firehose]]

Think:

**Deliver streaming data**

## OpenSearch

Think:

**Search delivered data**

Architecture:

Logs  
↓  
Firehose  
↓  
OpenSearch

### Memory Trick

**Firehose = Deliver**

**OpenSearch = Search**

---

# Architecture Thinking

## Scenario 1 — Product Search

E-commerce website stores product information.

Customers need to search:

`"men's waterproof black boots"`

Choose:

**OpenSearch**

---

## Scenario 2 — DynamoDB Full-Text Search

Application stores records in:

DynamoDB.

Need:

**Full-text search**

Choose:

DynamoDB  
↓  
DynamoDB Streams  
↓  
Lambda  
↓  
OpenSearch

---

## Scenario 3 — Log Analytics

Thousands of servers generate:

**Application logs**

Need:

- Centralized ingestion
- Search
- Dashboards

Choose:

Firehose  
↓  
OpenSearch  
↓  
OpenSearch Dashboards

---

## Scenario 4 — Historical SQL

Company stores:

Parquet files in S3.

Need:

**Ad hoc SQL queries**

Choose:

**Athena**

not OpenSearch.

---

## Scenario 5 — BI Dashboard

Executives need:

**Sales dashboards from Redshift**

Choose:

**QuickSight**

not OpenSearch.

---

## Scenario 6 — High Availability

Production search workload cannot tolerate:

**Single-AZ failure**

Choose:

**Multi-AZ / Zone Awareness**

---

## Scenario 7 — Older Logs

Company needs:

Recent logs  
→ Fast access

Old logs  
→ Searchable but lower cost

Choose:

**UltraWarm**

for older data.

---

## Scenario 8 — Private Search Cluster

Search data contains:

**Sensitive customer information**

and must not be exposed publicly.

Choose:

**VPC deployment**

with appropriate:

- Security groups
- IAM
- Encryption

---

## Scenario 9 — No Cluster Management

Team wants:

**Search capability**

without provisioning:

- Nodes
- Instances
- Cluster capacity

Choose:

**OpenSearch Serverless**

---

## Scenario 10 — Primary Transaction Database

Application requires:

- ACID transactions
- Relational joins
- Referential integrity

Do NOT choose OpenSearch as the primary database.

Think:

**RDS / Aurora**

---

# Scenario Recognition

Immediately think:

**OpenSearch**

when you see:

- Full-text search
- Search engine
- Search relevance
- Product search
- Log analytics
- Indexed documents
- Near-real-time search
- OpenSearch Dashboards

---

## Think UltraWarm When You See

- Older OpenSearch data
- Lower-cost searchable logs
- Infrequently accessed indexes

---

## Think Serverless When You See

- No cluster management
- Automatically scaling search
- Minimal infrastructure administration

---

## Think Athena When You See

- SQL on S3
- Historical analytical files
- Serverless ad hoc SQL

---

## Think QuickSight When You See

- BI
- Executive dashboard
- Business analytics

---

# Exam Traps

## Trap 1 — OpenSearch Is a Relational Database

❌

It is primarily:

**A search and analytics engine**

---

## Trap 2 — OpenSearch Should Always Be the System of Record

❌

A database such as:

- DynamoDB
- RDS

may remain:

**The primary system of record**

while OpenSearch provides:

**Search**

---

## Trap 3 — DynamoDB Provides Native Full-Text Search Like OpenSearch

❌

For advanced full-text search:

**OpenSearch**

---

## Trap 4 — OpenSearch Is the Best Service for SQL on S3

❌

Think:

**Athena**

---

## Trap 5 — OpenSearch Dashboards and QuickSight Solve Exactly the Same Problem

❌

OpenSearch Dashboards:

**Search/log analytics**

QuickSight:

**Business intelligence**

---

## Trap 6 — Firehose Searches Data

❌

Firehose:

**Delivers**

OpenSearch:

**Searches**

---

## Trap 7 — UltraWarm Is for the Hottest Data

❌

UltraWarm:

**Older / less frequently accessed searchable data**

---

## Trap 8 — VPC OpenSearch Must Be Publicly Accessible

❌

VPC deployment is specifically useful for:

**Private access**

---

# Quick Cheat Sheet

| Exam Clue | Answer |
|---|---|
| Full-Text Search | OpenSearch |
| Product Search | OpenSearch |
| Log Analytics | OpenSearch |
| Search Dashboards | OpenSearch Dashboards |
| DynamoDB Full-Text Search | DynamoDB Streams + Lambda + OpenSearch |
| Stream Logs to Search | Firehose + OpenSearch |
| Older Searchable Data | UltraWarm |
| High Availability | Multi-AZ / Zone Awareness |
| No Cluster Management | OpenSearch Serverless |
| SQL on S3 | Athena |
| BI Dashboard | QuickSight |
| Data Warehouse | Redshift |

---

# Search Architecture Shortcut

Need:

**Primary application storage**

→ DynamoDB / RDS

Need:

**Full-text search**

→ OpenSearch

Need:

**Streaming delivery into search**

→ Firehose

Need:

**Search visualization**

→ OpenSearch Dashboards

Need:

**Historical archive**

→ S3

---

# Analytics Service Decision

> **SQL ON S3**
> → ATHENA
>
> **BIG DATA PROCESSING**
> → EMR
>
> **ETL**
> → GLUE
>
> **DATA LAKE GOVERNANCE**
> → LAKE FORMATION
>
> **BUSINESS INTELLIGENCE**
> → QUICKSIGHT
>
> **STREAM INGESTION**
> → KINESIS DATA STREAMS
>
> **STREAM DELIVERY**
> → FIREHOSE
>
> **REAL-TIME STREAM PROCESSING**
> → KINESIS DATA ANALYTICS
>
> **FULL-TEXT SEARCH / LOG ANALYTICS**
> → OPENSEARCH

---

# Final Exam Rapid-Fire

> **FULL-TEXT SEARCH**
> → OPENSEARCH
>
> **PRODUCT SEARCH**
> → OPENSEARCH
>
> **LOG SEARCH**
> → OPENSEARCH
>
> **SEARCH VISUALIZATION**
> → OPENSEARCH DASHBOARDS
>
> **DYNAMODB + FULL-TEXT SEARCH**
> → DYNAMODB STREAMS + LAMBDA + OPENSEARCH
>
> **STREAM → SEARCH**
> → FIREHOSE → OPENSEARCH
>
> **OLDER SEARCHABLE DATA**
> → ULTRAWARM
>
> **AZ RESILIENCE**
> → ZONE AWARENESS
>
> **NO SEARCH CLUSTER MANAGEMENT**
> → OPENSEARCH SERVERLESS
>
> **SQL ON S3**
> → ATHENA
>
> **BUSINESS BI**
> → QUICKSIGHT
>
> **WAREHOUSE**
> → REDSHIFT

---

## Master Memory Trick

> [!tip] OpenSearch Master Memory Trick
> Imagine Amazon has millions of products stored in:
>
> **A DATABASE**
>
> But a customer doesn't know:
>
> - Product ID
> - Exact key
> - Exact database field
>
> They just type:
>
> **"black waterproof running shoes"**
>
> The system needs to:
>
> **SEARCH WORDS**
>
> **RANK MATCHES**
>
> **RETURN RELEVANT RESULTS**
>
> That's:
>
> **OPENSEARCH**
>
> Now imagine millions of server logs.
>
> An engineer types:
>
> **"ERROR payment timeout"**
>
> and needs to instantly find matching events.
>
> Again:
>
> **OPENSEARCH**

So remember:

> **DATABASE**
> → STORE THE RECORD
>
> **OPENSEARCH**
> → SEARCH THE RECORD
>
> **FIREHOSE**
> → DELIVER THE RECORD
>
> **OPENSEARCH DASHBOARDS**
> → VISUALIZE SEARCH DATA
>
> **ULTRAWARM**
> → OLDER SEARCHABLE DATA
>
> **ZONE AWARENESS**
> → HIGH AVAILABILITY
>
> **SERVERLESS**
> → NO CLUSTER MANAGEMENT

And the killer SAA question:

> **"Does the application need fast full-text search, relevance-based results, or searchable log analytics?"**
>
> YES
>
> → **OpenSearch**

---

## Related Notes

- [[Kinesis Data Streams]]
- [[Kinesis Data Firehose]]
- [[Kinesis Data Analytics]]
- [[DynamoDB]]
- [[Lambda]]
- [[S3]]
- [[Athena]]
- [[Redshift]]
- [[QuickSight]]
- [[07-Monitoring/CloudWatch]]
- [[Cognito]]
- [[06-Security/KMS]]
## Database Exam Strategy

For SAA questions, do NOT start by asking:

**"Which database is best?"**

Instead ask:

> **"What type of data and access pattern does this workload have?"**

Use this decision framework:

| Requirement | Immediately Think |
|---|---|
| Traditional relational database | [[RDS]] |
| AWS-optimized relational database | [[Aurora]] |
| Read scaling | [[RDS Read Replicas]] |
| Relational database high availability | [[RDS Multi-AZ]] |
| Serverless relational database | [[Aurora Serverless]] |
| Connection pooling | [[RDS Proxy]] |
| NoSQL key-value database | [[04-Databases/DynamoDB]] |
| Microsecond in-memory cache | [[ElastiCache]] |
| Redis-compatible cache | [[ElastiCache for Redis]] |
| Simple distributed cache | [[ElastiCache for Memcached]] |
| Data warehouse / OLAP | [[04-Databases/Redshift]] |
| MongoDB-compatible document database | [[DocumentDB]] |
| Graph database | [[Neptune]] |
| Cassandra-compatible database | [[Keyspaces]] |
| Time-series database | [[Timestream]] |
| Immutable cryptographic ledger | [[QLDB]] |
| Search / indexing / log analytics | [[20-SAA/05-Databases/OpenSearch]] |

> [!tip] Master Database Question
> Ask:
>
> **RELATIONAL?**
>
> **KEY-VALUE?**
>
> **CACHE?**
>
> **WAREHOUSE?**
>
> **DOCUMENT?**
>
> **GRAPH?**
>
> **CASSANDRA?**
>
> **TIME SERIES?**
>
> **LEDGER?**
>
> **SEARCH?**

---

## OLTP vs OLAP

This distinction immediately eliminates many wrong exam answers.

### OLTP

**Online Transaction Processing**

Think:

- Application transactions
- Small reads/writes
- Individual records
- Frequent INSERT / UPDATE
- Customer-facing applications

Examples:

- [[RDS]]
- [[Aurora]]
- [[04-Databases/DynamoDB]]

### OLAP

**Online Analytical Processing**

Think:

- Analytics
- Reporting
- Aggregations
- Huge datasets
- Complex queries

Primary AWS answer:

[[04-Databases/Redshift]]

### Memory Trick

**OLTP = RUN the business**

**OLAP = ANALYZE the business**

---

# RDS

[[RDS]] is AWS's managed:

**Relational Database Service**

Supported engines include:

- PostgreSQL
- MySQL
- MariaDB
- Oracle
- SQL Server
- Db2

AWS manages tasks such as:

- Provisioning
- OS maintenance
- Database patching
- Backups
- Monitoring

### Immediately Think RDS When You See

- SQL
- Relational
- Joins
- Transactions
- Existing relational application
- Managed MySQL/PostgreSQL/Oracle/SQL Server

---

# RDS Storage Auto Scaling

[[RDS Storage Auto Scaling]] automatically increases database storage when:

**Free storage becomes low**

Think:

Database Grows  
↓  
Storage Threshold Reached  
↓  
RDS Automatically Adds Storage

Useful when database growth is:

**Unpredictable**

---

# RDS Read Replicas

[[RDS Read Replicas]] solve:

**READ SCALING**

Architecture:

Primary RDS  
↓  
Asynchronous Replication  
↓  
Read Replica

Applications can send:

Writes  
↓  
Primary

Reads  
↓  
Read Replicas

### Key Exam Facts

Read Replicas:

- Scale reads
- Use asynchronous replication
- Can be promoted
- Can be cross-AZ
- Can be cross-Region

> [!tip] Memory Trick
> **Read Replica = PERFORMANCE**

---

# RDS Multi-AZ

[[RDS Multi-AZ]] solves:

**HIGH AVAILABILITY**

Architecture:

Primary DB  
↓  
Synchronous Replication  
↓  
Standby DB

If the primary fails:

Standby  
↓  
Promoted Automatically

### Critical Rule

The standby is:

**NOT used for normal read scaling**

> [!tip] Memory Trick
> **Multi-AZ = SURVIVAL**
>
> **Read Replica = SPEED**

---

# Multi-AZ vs Read Replica

| Requirement | Multi-AZ | Read Replica |
|---|---:|---:|
| High Availability | ✅ | ❌ |
| Disaster Recovery | ✅ | Possible use |
| Read Scaling | ❌ | ✅ |
| Synchronous Replication | ✅ | ❌ |
| Asynchronous Replication | ❌ | ✅ |
| Standby Serves Reads | ❌ | N/A |
| Can Be Cross-Region | ❌ for classic Multi-AZ standby | ✅ |
| Automatic Failover | ✅ | ❌ |

### Killer Exam Distinction

**"Database must survive AZ failure"**  
→ Multi-AZ

**"Database has too many read requests"**  
→ Read Replica

---

# RDS Multi-AZ DB Cluster

A Multi-AZ DB Cluster uses:

**1 Writer + 2 Readable Standbys**

across:

**3 Availability Zones**

This provides:

- High availability
- Read capacity
- Faster failover

Do not confuse this with the traditional:

**Single standby Multi-AZ deployment**

---

# RDS Backups

RDS supports:

**Automated Backups**

These provide:

**Point-in-Time Recovery**

within the configured retention period.

Think:

> **"Restore database to a specific time."**

→ Automated Backup / PITR

---

# RDS Snapshots

Snapshots are:

**User-initiated backups**

They remain until:

**You delete them**

### Exam Decision

**Continuous recovery / specific time**
→ Automated Backups

**Long-term manually controlled backup**
→ Snapshot

---

# RDS Snapshot Restore

Restoring a snapshot creates:

**A new database**

It does NOT restore directly over the existing DB.

### Memory Trick

**Snapshot Restore = NEW DB**

---

# Aurora

[[Aurora]] is AWS's cloud-optimized relational database.

Compatible with:

- MySQL
- PostgreSQL

Aurora is designed for:

- High performance
- High availability
- Automatic storage growth
- Fast replication

---

# Aurora Storage Architecture

Aurora maintains:

**6 copies of data**

across:

**3 Availability Zones**

Think:

3 AZs  
×  
2 Copies  
=  
6 Copies

### Memory Trick

**Aurora = 6 across 3**

---

# Aurora Availability

Aurora can tolerate:

**Loss of 2 copies for writes**

and:

**Loss of 3 copies for reads**

This architecture provides strong fault tolerance.

---

# Aurora Replicas

Aurora supports:

**Up to 15 Aurora Replicas**

Replication is designed to be:

**Very fast**

Use Aurora Replicas for:

**Read scaling**

---

# Aurora Endpoints

Know these.

## Writer Endpoint

Points to:

**Current Writer**

Use for:

- INSERT
- UPDATE
- DELETE

---

## Reader Endpoint

Provides:

**Load balancing across Aurora Replicas**

Use for:

**Read scaling**

### Memory Trick

**Writer Endpoint = WRITE**

**Reader Endpoint = READ FARM**

---

# Aurora Auto Scaling

Aurora can automatically adjust:

**The number of Aurora Replicas**

based on demand.

Architecture:

Read Traffic Increases  
↓  
Aurora Auto Scaling  
↓  
More Replicas  
↓  
Reader Endpoint

---

# Aurora Serverless

[[Aurora Serverless]] automatically manages database capacity.

Best for:

- Unpredictable workloads
- Intermittent workloads
- Variable database demand

### Exam Pattern

> **Relational database + unpredictable capacity**
>
> → **Aurora Serverless**

---

# Aurora Global Database

[[Aurora Global Database]] is designed for:

**Multi-Region relational architectures**

Think:

Primary Region  
↓  
Cross-Region Replication  
↓  
Secondary Regions

Use for:

- Global applications
- Low-latency global reads
- Cross-Region disaster recovery

### Memory Trick

**Aurora Global = Relational database around the world**

---

# RDS Proxy

[[RDS Proxy]] pools and manages:

**Database connections**

Architecture:

Application / Lambda  
↓  
RDS Proxy  
↓  
RDS / Aurora

Use when:

- Many database connections
- Lambda creates connection spikes
- Need connection pooling
- Want better database failover handling

> [!tip] Exam Pattern
> **Lambda + too many DB connections**
>
> → **RDS Proxy**

---

# ElastiCache

[[ElastiCache]] provides:

**Managed in-memory caching**

Use when an application repeatedly requests the same data.

Without cache:

Application  
↓  
Database  
↓  
Application

Every request hits database.

With cache:

Application  
↓  
ElastiCache  
↓  
Cache Hit

Database traffic decreases.

### Memory Trick

**Cache = Don't ask the database twice**

---

# Cache-Aside Pattern

Common architecture:

Application  
↓  
Check Cache

If HIT:

Cache  
↓  
Return Data

If MISS:

Database  
↓  
Return Data  
↓  
Store in Cache  
↓  
Application

---

# ElastiCache for Redis

[[ElastiCache for Redis]] supports advanced features such as:

- Replication
- High availability
- Persistence
- Read Replicas
- Multi-AZ
- Automatic failover
- Sorted sets

Use when you need:

**More than simple caching**

---

# ElastiCache for Memcached

[[ElastiCache for Memcached]] is:

**Simple distributed caching**

Characteristics:

- Multi-node partitioning
- No replication
- No high availability
- No persistence
- Multi-threaded architecture

### Memory Trick

**Redis = Rich features**

**Memcached = Minimal cache**

---

# Redis vs Memcached

| Requirement | Redis | Memcached |
|---|---:|---:|
| In-Memory Cache | ✅ | ✅ |
| Replication | ✅ | ❌ |
| High Availability | ✅ | ❌ |
| Automatic Failover | ✅ | ❌ |
| Persistence | ✅ | ❌ |
| Read Replicas | ✅ | ❌ |
| Multi-Threaded | ❌ traditionally | ✅ |
| Simple Distributed Cache | Possible | ✅ |

---

# DynamoDB

[[04-Databases/DynamoDB]] is a:

**Serverless NoSQL key-value and document database**

Designed for:

- Massive scale
- Very low latency
- Automatic scaling
- High availability

Think:

Application  
↓  
DynamoDB

No database servers to manage.

---

# DynamoDB Core Architecture

DynamoDB tables contain:

**Items**

Items contain:

**Attributes**

Each item is identified using a:

**Primary Key**

---

# DynamoDB Partition Key

A:

**Partition Key**

determines how data is distributed.

Good partition keys should have:

**High cardinality**

and distribute traffic evenly.

### Exam Trap

Bad partition key  
↓  
Too much traffic on one partition  
↓  
**Hot Partition**

---

# DynamoDB Capacity Modes

## Provisioned Mode

You define:

- Read Capacity
- Write Capacity

Best when traffic is:

**Predictable**

---

## On-Demand Mode

DynamoDB automatically handles capacity.

Best when traffic is:

- Unpredictable
- Spiky
- Difficult to forecast

### Memory Trick

**Predictable → Provisioned**

**Unpredictable → On-Demand**

---

# DynamoDB Accelerator

[[DAX]] provides:

**In-memory caching for DynamoDB**

Architecture:

Application  
↓  
DAX  
↓  
DynamoDB

Provides:

**Microsecond read performance**

### Killer Exam Pattern

> **DynamoDB reads need microsecond latency**
>
> → **DAX**

---

# DAX vs ElastiCache

## DAX

Purpose-built for:

**DynamoDB**

---

## ElastiCache

General-purpose cache that can be used with:

- RDS
- Aurora
- Applications
- Other workloads

### Memory Trick

**DynamoDB cache → DAX**

**General cache → ElastiCache**

---

# DynamoDB Streams

[[DynamoDB Streams]] capture:

**Item-level changes**

Examples:

- Insert
- Update
- Delete

Architecture:

DynamoDB  
↓  
Stream  
↓  
Lambda

Use for:

- Event-driven applications
- Replication logic
- Notifications
- Derived data

---

# DynamoDB Global Tables

[[DynamoDB Global Tables]] provide:

**Multi-Region active-active replication**

Architecture:

Region A  
↕  
Region B  
↕  
Region C

Applications can:

**Read + Write in multiple Regions**

### Critical Requirement

Global Tables require:

[[DynamoDB Streams]]

### Memory Trick

**Global Tables = Multi-Region Active-Active DynamoDB**

---

# DynamoDB TTL

[[DynamoDB TTL]] automatically removes items after:

**An expiration timestamp**

Use for:

- Session data
- Temporary records
- Expiring application data

### Memory Trick

**TTL = Expiration Date for DynamoDB Item**

---

# DynamoDB Backups

DynamoDB supports:

**Point-in-Time Recovery**

for continuous backup and recovery.

Also supports:

**On-demand backups**

---

# Redshift

[[04-Databases/Redshift]] is AWS's:

**Data Warehouse**

Use for:

- OLAP
- Analytics
- Reporting
- Business intelligence
- Large analytical datasets

### Memory Trick

**RDS = Transactions**

**Redshift = Analytics**

---

# Redshift Architecture

Redshift uses:

**Columnar Storage**

and:

**Massively Parallel Processing**

or:

**MPP**

This makes it efficient for large analytical queries.

### Memory Trick

**Columns + Parallelism = Analytics**

---

# Redshift Spectrum

[[Redshift Spectrum]] allows Redshift to query:

**Data directly in S3**

without loading all of it into Redshift first.

Architecture:

Redshift  
↓  
Spectrum  
↓  
S3

### Exam Pattern

> **Redshift query data directly in S3**
>
> → **Redshift Spectrum**

---

# Redshift Serverless

[[Redshift Serverless]] provides data warehousing without manually managing:

**Redshift cluster infrastructure**

Use when you want:

**Serverless analytics / warehousing**

---

# DocumentDB

[[DocumentDB]] is AWS's:

**MongoDB-compatible document database**

Use when:

- Application uses document data
- MongoDB compatibility is required
- JSON-like document structures are natural

### Memory Trick

**MongoDB → DocumentDB**

---

# Neptune

[[Neptune]] is AWS's:

**Graph Database**

Use when relationships between data are the important part.

Examples:

- Social networks
- Recommendation engines
- Fraud detection
- Knowledge graphs

### Memory Trick

**Relationships → Neptune**

---

# Neptune Graph Thinking

Traditional database:

User Table  
Product Table  
Transaction Table

Graph database:

User  
↓ FRIEND_OF  
User  
↓ PURCHASED  
Product  
↓ RELATED_TO  
Product

When the question emphasizes:

**Connections / Relationships**

Think:

[[Neptune]]

---

# Neptune High Availability

Neptune can use:

**Read Replicas**

across multiple Availability Zones.

This provides:

- Read scaling
- High availability

---

# Neptune Streams

[[Neptune Streams]] capture:

**Changes made to a Neptune graph**

Think:

Graph Change  
↓  
Neptune Streams  
↓  
Downstream Consumer

Use when another application needs to react to:

**Graph database changes**

### Memory Trick

**Neptune Streams = Change log for the graph**

---

# Keyspaces

[[Keyspaces]] is AWS's:

**Apache Cassandra-compatible database**

It is:

**Serverless**

Use when:

- Migrating Cassandra workloads
- Cassandra Query Language compatibility is required
- Wide-column NoSQL architecture is needed

### Memory Trick

**Cassandra → Keyspaces**

---

# Timestream

[[Timestream]] is AWS's:

**Time-Series Database**

Use when data naturally revolves around:

**Time**

Examples:

- IoT sensor readings
- Application metrics
- Industrial telemetry
- Monitoring data

Architecture:

Device / Application  
↓  
Timestamped Data  
↓  
Timestream

### Memory Trick

**TIME → Timestream**

---

# Timestream Architecture Thinking

If records look like:

Timestamp | Temperature  
Timestamp | CPU  
Timestamp | Pressure  
Timestamp | Heartbeat

Think:

[[Timestream]]

---

# QLDB

[[QLDB]] is AWS's:

**Ledger Database**

QLDB provides:

**Immutable + Cryptographically Verifiable transaction history**

Use when you need:

- Complete transaction history
- Verifiable history
- Append-only journal
- Centralized ledger

### Memory Trick

**QLDB = Digital Accounting Book**

---

# QLDB vs Blockchain

QLDB is:

**Centralized**

It is not a decentralized blockchain network.

### Exam Trap

If the requirement says:

**Decentralized parties that do not trust one another**

QLDB is probably not the answer.

If it says:

**Central authority + immutable verifiable ledger**

Think:

[[QLDB]]

---

# OpenSearch

[[20-SAA/05-Databases/OpenSearch]] provides:

**Search + Indexing + Analytics**

Use for:

- Full-text search
- Application search
- Log analytics
- Search dashboards
- Near real-time analysis

### Memory Trick

**Need SEARCH → OpenSearch**

---

# OpenSearch Architecture

Common pattern:

Application Logs  
↓  
Ingestion  
↓  
OpenSearch  
↓  
Search / Analyze / Visualize

Another:

Application Data  
↓  
OpenSearch Index  
↓  
Fast Search

---

# OpenSearch vs Database

OpenSearch is NOT usually the primary transactional database.

Instead:

Primary Database  
↓  
Application Data  
↓  
OpenSearch  
↓  
Search Index

### Exam Trap

Do not replace:

[[RDS]]

or:

[[04-Databases/DynamoDB]]

with OpenSearch simply because users need a search bar.

A common architecture is:

Database  
+  
OpenSearch

---

# Database Type Decision Tree

Need SQL / relational relationships?  
↓ YES  
[[RDS]] / [[Aurora]]

Need serverless relational capacity?  
↓ YES  
[[Aurora Serverless]]

Need key-value NoSQL at massive scale?  
↓ YES  
[[04-Databases/DynamoDB]]

Need microsecond DynamoDB reads?  
↓ YES  
[[DAX]]

Need in-memory caching?  
↓ YES  
[[ElastiCache]]

Need analytical data warehouse?  
↓ YES  
[[04-Databases/Redshift]]

Need MongoDB compatibility?  
↓ YES  
[[DocumentDB]]

Need graph relationships?  
↓ YES  
[[Neptune]]

Need Cassandra compatibility?  
↓ YES  
[[Keyspaces]]

Need timestamped data?  
↓ YES  
[[Timestream]]

Need immutable ledger?  
↓ YES  
[[QLDB]]

Need search / indexing?  
↓ YES  
[[20-SAA/05-Databases/OpenSearch]]

---

# Architecture Thinking

## Scenario 1 — Relational Application

An application requires:

- SQL
- Joins
- ACID transactions

**Choose → [[RDS]] or [[Aurora]]**

---

## Scenario 2 — Database Must Survive AZ Failure

The requirement emphasizes:

**High availability**

Choose:

[[RDS Multi-AZ]]

Not:

Read Replica

---

## Scenario 3 — Database Has Too Many Reads

Primary database CPU is overloaded by:

**SELECT queries**

Choose:

[[RDS Read Replicas]]

---

## Scenario 4 — Lambda Overwhelms Database Connections

Thousands of Lambda executions create database connections.

Choose:

[[RDS Proxy]]

---

## Scenario 5 — Repeated Database Queries

Application repeatedly requests the same information.

Choose:

[[ElastiCache]]

---

## Scenario 6 — Massive Serverless Key-Value Workload

Application requires:

- NoSQL
- Massive scale
- Millisecond latency
- No servers

Choose:

[[04-Databases/DynamoDB]]

---

## Scenario 7 — DynamoDB Needs Microsecond Reads

Choose:

[[DAX]]

---

## Scenario 8 — Multi-Region Active-Active NoSQL

Users must read and write DynamoDB data in several Regions.

Choose:

[[DynamoDB Global Tables]]

---

## Scenario 9 — Data Warehouse

Company needs:

- BI
- Reporting
- Huge analytical queries

Choose:

[[04-Databases/Redshift]]

---

## Scenario 10 — Query S3 From Redshift

Company has analytical data stored in S3 and does not want to load all of it into Redshift.

Choose:

[[Redshift Spectrum]]

---

## Scenario 11 — MongoDB Migration

Application currently uses MongoDB.

Company wants an AWS-managed compatible database.

Choose:

[[DocumentDB]]

---

## Scenario 12 — Social Network Relationships

Application frequently asks:

> Which users are connected to which users?

Choose:

[[Neptune]]

---

## Scenario 13 — Cassandra Migration

Application uses Cassandra and CQL.

Choose:

[[Keyspaces]]

---

## Scenario 14 — IoT Sensor Measurements

Millions of timestamped readings arrive from devices.

Choose:

[[Timestream]]

---

## Scenario 15 — Immutable Financial Journal

Company requires:

- Complete transaction history
- Cryptographic verification
- Central authority

Choose:

[[QLDB]]

---

## Scenario 16 — Search Engine

Application needs:

- Full-text search
- Indexing
- Search analytics

Choose:

[[20-SAA/05-Databases/OpenSearch]]

---

# Scenario Recognition

## Immediately Think RDS When You See

- SQL
- Relational
- Joins
- Transactions
- MySQL
- PostgreSQL
- Oracle
- SQL Server

---

## Immediately Think Aurora When You See

- AWS-optimized relational database
- MySQL/PostgreSQL compatibility
- High performance
- 6 copies across 3 AZs
- 15 Read Replicas
- Reader Endpoint
- Global relational database

---

## Immediately Think DynamoDB When You See

- Key-value
- Serverless NoSQL
- Massive scale
- Millisecond latency
- Partition key
- Global Tables

---

## Immediately Think ElastiCache When You See

- Cache
- Reduce database load
- In-memory
- Redis
- Memcached
- Repeated reads

---

## Immediately Think Redshift When You See

- Data warehouse
- OLAP
- BI
- Analytics
- Columnar storage
- MPP

---

## Immediately Think DocumentDB When You See

- MongoDB
- Document database
- JSON-like documents

---

## Immediately Think Neptune When You See

- Graph
- Relationships
- Social network
- Fraud detection
- Knowledge graph
- Recommendation engine

---

## Immediately Think Keyspaces When You See

- Cassandra
- CQL
- Wide-column database

---

## Immediately Think Timestream When You See

- Time-series
- IoT
- Metrics
- Telemetry
- Timestamped measurements

---

## Immediately Think QLDB When You See

- Ledger
- Immutable history
- Cryptographic verification
- Transaction journal

---

## Immediately Think OpenSearch When You See

- Search
- Full-text search
- Indexing
- Log analytics
- Search dashboard

---

# Biggest Database Exam Traps

## Trap 1 — Multi-AZ Improves Read Scaling

False.

Traditional RDS Multi-AZ is primarily:

**High Availability**

For read scaling:

[[RDS Read Replicas]]

---

## Trap 2 — Read Replica Provides Automatic HA Failover

False.

Read Replicas primarily provide:

**Read Scaling**

Multi-AZ provides:

**Automatic failover**

---

## Trap 3 — Multi-AZ Replication Is Asynchronous

False.

Traditional Multi-AZ:

**Synchronous**

Read Replica:

**Asynchronous**

---

## Trap 4 — Aurora Reader Endpoint Points to Writer

False.

Reader Endpoint:

**Read Replicas**

Writer Endpoint:

**Writer**

---

## Trap 5 — Aurora Is Compatible With Every RDS Engine

False.

Aurora is compatible with:

- MySQL
- PostgreSQL

---

## Trap 6 — ElastiCache Is a Permanent Database Replacement

Usually false.

Caching typically sits:

**In front of the database**

---

## Trap 7 — Memcached Provides Multi-AZ Failover

False.

For advanced HA and replication features:

Think:

**Redis**

---

## Trap 8 — DAX Caches RDS

False.

DAX is purpose-built for:

[[04-Databases/DynamoDB]]

---

## Trap 9 — DynamoDB Global Tables Are Read-Only Replicas

False.

Global Tables provide:

**Multi-Region Active-Active**

---

## Trap 10 — Redshift Is for OLTP Transactions

False.

Redshift is:

**OLAP / Data Warehousing**

---

## Trap 11 — Redshift Spectrum Requires Loading S3 Data First

False.

Spectrum can query:

**S3 directly**

---

## Trap 12 — Neptune Is a Relational Database

False.

Neptune is:

**Graph**

---

## Trap 13 — Timestream Is General-Purpose Relational Storage

False.

Timestream is specialized for:

**Time-series data**

---

## Trap 14 — QLDB Is Decentralized Blockchain

False.

QLDB is:

**Centralized**

with:

**Cryptographically verifiable immutable history**

---

## Trap 15 — OpenSearch Should Replace Primary Transaction Database

Usually false.

OpenSearch is optimized for:

**Search + Indexing + Analytics**

---

# Quick Cheat Sheet

| Exam Clue | Best Answer |
|---|---|
| SQL / Relational | RDS |
| AWS-Optimized MySQL/PostgreSQL | Aurora |
| Database HA | Multi-AZ |
| Read Scaling | Read Replica |
| Serverless Relational | Aurora Serverless |
| Global Relational | Aurora Global Database |
| Connection Pooling | RDS Proxy |
| In-Memory Cache | ElastiCache |
| Redis Features | ElastiCache for Redis |
| Simple Distributed Cache | Memcached |
| Serverless Key-Value NoSQL | DynamoDB |
| Microsecond DynamoDB Reads | DAX |
| Multi-Region Active-Active NoSQL | DynamoDB Global Tables |
| Expiring DynamoDB Items | DynamoDB TTL |
| Data Warehouse | Redshift |
| Query S3 from Redshift | Redshift Spectrum |
| MongoDB Compatible | DocumentDB |
| Graph Relationships | Neptune |
| Graph Change Stream | Neptune Streams |
| Cassandra Compatible | Keyspaces |
| Time-Series | Timestream |
| Immutable Ledger | QLDB |
| Search / Indexing | OpenSearch |

---

## Database Comparison Table

| Service | Database Type | Strongest Exam Clue |
|---|---|---|
| RDS | Relational | SQL |
| Aurora | Relational | AWS-optimized MySQL/PostgreSQL |
| DynamoDB | Key-Value / Document | Serverless NoSQL |
| ElastiCache | In-Memory | Cache |
| Redshift | Data Warehouse | OLAP |
| DocumentDB | Document | MongoDB |
| Neptune | Graph | Relationships |
| Keyspaces | Wide-Column | Cassandra |
| Timestream | Time-Series | Time |
| QLDB | Ledger | Immutable Journal |
| OpenSearch | Search Engine | Search / Index |

---

## Master Memory Trick

> [!tip] Database Master Memory Trick
> Imagine AWS has a different filing system for every type of data.
>
> **RDS**
> → Spreadsheet with relationships
>
> **Aurora**
> → AWS supercharged relational database
>
> **DynamoDB**
> → Giant key-value dictionary
>
> **ElastiCache**
> → Information kept in memory for speed
>
> **Redshift**
> → Analytics warehouse
>
> **DocumentDB**
> → Filing cabinet full of JSON-like documents
>
> **Neptune**
> → Relationship map
>
> **Keyspaces**
> → Cassandra
>
> **Timestream**
> → Timeline
>
> **QLDB**
> → Permanent accounting ledger
>
> **OpenSearch**
> → Search engine

---

## Final Exam Rapid-Fire

> **SQL → RDS**
>
> **AWS-OPTIMIZED SQL → Aurora**
>
> **HIGH AVAILABILITY → Multi-AZ**
>
> **READ SCALING → Read Replica**
>
> **UNPREDICTABLE RELATIONAL CAPACITY → Aurora Serverless**
>
> **GLOBAL RELATIONAL → Aurora Global Database**
>
> **TOO MANY DB CONNECTIONS → RDS Proxy**
>
> **CACHE → ElastiCache**
>
> **ADVANCED CACHE / HA → Redis**
>
> **SIMPLE DISTRIBUTED CACHE → Memcached**
>
> **SERVERLESS NOSQL → DynamoDB**
>
> **MICROSECOND DYNAMODB → DAX**
>
> **GLOBAL ACTIVE-ACTIVE NOSQL → Global Tables**
>
> **DATA WAREHOUSE → Redshift**
>
> **QUERY S3 FROM REDSHIFT → Spectrum**
>
> **MONGODB → DocumentDB**
>
> **RELATIONSHIPS → Neptune**
>
> **CASSANDRA → Keyspaces**
>
> **TIME → Timestream**
>
> **IMMUTABLE LEDGER → QLDB**
>
> **SEARCH → OpenSearch**

---

## Related Notes

- [[RDS]]
- [[RDS Storage Auto Scaling]]
- [[RDS Read Replicas]]
- [[RDS Multi-AZ]]
- [[RDS Backups]]
- [[RDS Snapshots]]
- [[RDS Proxy]]
- [[Aurora]]
- [[Aurora Replicas]]
- [[Aurora Serverless]]
- [[Aurora Global Database]]
- [[ElastiCache]]
- [[ElastiCache for Redis]]
- [[ElastiCache for Memcached]]
- [[04-Databases/DynamoDB]]
- [[DAX]]
- [[DynamoDB Streams]]
- [[DynamoDB Global Tables]]
- [[DynamoDB TTL]]
- [[04-Databases/Redshift]]
- [[Redshift Spectrum]]
- [[Redshift Serverless]]
- [[DocumentDB]]
- [[Neptune]]
- [[Neptune Streams]]
- [[Keyspaces]]
- [[Timestream]]
- [[QLDB]]
- [[20-SAA/05-Databases/OpenSearch]]
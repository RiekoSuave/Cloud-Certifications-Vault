## What Problem Does It Solve?

[[DynamoDB]] is AWS's:

**Fully managed serverless NoSQL database**

It is designed for applications that need:

- Very low latency
- Massive scale
- Automatic scaling
- High availability
- No database server management

Architecture:

Application  
↓  
DynamoDB Table  
↓  
Items

> [!tip] Memory Trick
> **DynamoDB = Serverless NoSQL at massive scale**

---

## Core Concept

DynamoDB stores data in:

**Tables**

A table contains:

**Items**

Each item contains:

**Attributes**

Think:

Table  
↓  
Item  
↓  
Attributes

Example:

Users Table  
↓  
User Item  
↓  
- UserId
- Name
- Email
- Country

---

## NoSQL Model

DynamoDB is:

**Not a relational database**

It does not use:

- Traditional joins
- Foreign keys
- Relational table normalization

Instead, you design data around:

**Access patterns**

### SAA Principle

> With DynamoDB, design the table around how the application will read and write data.

---

## Primary Keys

Every DynamoDB table requires a:

**Primary Key**

There are two main types:

1. Partition Key
2. Partition Key + Sort Key

---

## Partition Key

A table can use only a:

**Partition Key**

Example:

`UserId`

Each item must have:

**A unique partition key value**

Architecture:

Users Table  
↓  
Partition Key = UserId

---

## Composite Primary Key

A table can also use:

**Partition Key + Sort Key**

Example:

Partition Key:

`CustomerId`

Sort Key:

`OrderDate`

This allows multiple items to share:

**The same partition key**

as long as the combination of:

Partition Key + Sort Key

is unique.

### Memory Trick

**Partition Key = Group**

**Sort Key = Order Within Group**

---

## Composite Key Example

Orders Table

Partition Key:

`CustomerId`

Sort Key:

`OrderTimestamp`

Customer 123  
↓  
├── 2026-08-01
├── 2026-08-05
└── 2026-08-20

This makes it efficient to retrieve:

**All orders for one customer**

in sort-key order.

---

# Partitioning

DynamoDB distributes data across:

**Partitions**

The partition key helps determine:

**Where data is stored**

A good partition key should distribute requests:

**Evenly**

### Killer Exam Principle

> **Choose high-cardinality partition keys that distribute traffic well**

---

## Hot Partition

A:

**Hot Partition**

occurs when too much traffic targets:

**The same partition key or small set of partitions**

Example:

Partition Key:

`Country`

Most traffic:

`USA`

Result:

**Uneven traffic distribution**

### Memory Trick

**Bad Partition Key = Hot Spot**

---

## Good Partition Key

Better partition keys often have:

**High cardinality**

Examples:

- UserId
- OrderId
- DeviceId

These spread workload more evenly.

---

# Items

A DynamoDB:

**Item**

is similar conceptually to:

**A row**

in a relational database.

But DynamoDB items can have:

**Different attributes**

within the same table.

Example:

Item A:

- UserId
- Name
- Email

Item B:

- UserId
- Name
- Phone
- MembershipType

DynamoDB is:

**Schema-flexible**

except for:

**Primary key attributes**

---

# Attributes

An:

**Attribute**

is a field within an item.

Examples:

- Name
- Age
- Status
- Timestamp
- Price

DynamoDB supports multiple data types.

---

# Read Capacity Modes

DynamoDB supports two primary capacity modes:

- Provisioned
- On-Demand

This is a major SAA distinction.

---

## Provisioned Capacity

With:

**Provisioned Capacity Mode**

you specify:

- Read Capacity
- Write Capacity

Think:

> **Predictable workload**

You provision expected throughput.

### Killer Exam Clue

> **Traffic is predictable and cost optimization matters**
>
> → **Provisioned Capacity**

---

## Auto Scaling with Provisioned Capacity

Provisioned capacity can use:

**Auto Scaling**

to adjust:

- Read capacity
- Write capacity

based on demand.

This gives:

**More flexibility**

while retaining provisioned-mode economics.

---

# On-Demand Capacity

With:

**On-Demand Capacity Mode**

DynamoDB automatically handles:

**Changing traffic levels**

You pay based on:

**Actual requests**

Think:

- Unpredictable workloads
- Spiky traffic
- New applications
- Minimal capacity planning

### Killer Exam Clue

> **Unpredictable traffic with minimal capacity management**
>
> → **DynamoDB On-Demand**

---

## Provisioned vs On-Demand

| Requirement | Provisioned | On-Demand |
|---|---:|---:|
| Predictable Traffic | ✅ | ✅ |
| Unpredictable Traffic | Possible | ✅ Best Fit |
| Capacity Planning | ✅ | ❌ |
| Pay Per Request | ❌ | ✅ |
| Auto Scaling | ✅ | Built-In Behavior |
| Minimum Ops | Lower | ✅ |

### Memory Trick

**Provisioned = Predict**

**On-Demand = Surprise Me**

---

# Read Consistency

DynamoDB supports:

- Eventually Consistent Reads
- Strongly Consistent Reads

---

## Eventually Consistent Reads

Default behavior for many DynamoDB read operations.

A read may briefly return:

**Older data**

after a write.

Benefits:

- Lower cost
- Higher effective read throughput

### Memory Trick

**Eventually = Cheaper + May Be Slightly Stale**

---

## Strongly Consistent Reads

A strongly consistent read returns:

**The most up-to-date data**

after a successful write.

Tradeoff:

**Higher read capacity cost**

than eventual consistency.

### Killer Exam Clue

> **Application must immediately read the latest committed value**
>
> → **Strongly Consistent Read**

---

# Consistency Comparison

| Requirement | Eventually Consistent | Strongly Consistent |
|---|---:|---:|
| Lowest Read Cost | ✅ | ❌ |
| Latest Data Required | ❌ | ✅ |
| Slight Staleness Acceptable | ✅ | ❌ |
| Default Read Choice | Common | Optional |

---

# Global Secondary Index

A:

**Global Secondary Index — GSI**

provides:

**An alternate partition key and optional sort key**

This allows efficient queries using:

**Different attributes**

than the table's primary key.

Example:

Main Table Key:

`UserId`

Need to query by:

`Email`

Create:

GSI  
Partition Key = Email

### Killer Exam Clue

> **Need to query DynamoDB efficiently using a different partition key**
>
> → **GSI**

---

## GSI Characteristics

A GSI:

- Can use a different partition key
- Can use a different sort key
- Has its own capacity considerations in provisioned mode
- Can be created after the table exists
- Is eventually consistent for reads

### Memory Trick

**GLOBAL = Different Partition Key**

---

# Local Secondary Index

A:

**Local Secondary Index — LSI**

uses:

**The same partition key**

as the base table

but:

**A different sort key**

Example:

Table:

Partition Key = CustomerId

Sort Key = OrderDate

LSI:

Partition Key = CustomerId

Sort Key = OrderAmount

### Memory Trick

**LOCAL = Same Partition, Different Sort**

---

## LSI Characteristics

An LSI:

- Uses same partition key as table
- Uses different sort key
- Must be created when the table is created
- Shares table partitioning
- Can support strongly consistent reads

### Killer Exam Clue

> **Need a different sort key but the same partition key**
>
> → **LSI**

---

# GSI vs LSI

| Feature | GSI | LSI |
|---|---:|---:|
| Different Partition Key | ✅ | ❌ |
| Different Sort Key | ✅ | ✅ |
| Same Partition Key as Table | Not Required | ✅ |
| Create After Table Creation | ✅ | ❌ |
| Strongly Consistent Reads | ❌ | ✅ |
| Alternate Access Pattern | ✅ | ✅ |

### Memory Trick

**GSI = Global Key Change**

**LSI = Local Sort Change**

---

# Query

A:

**Query**

efficiently retrieves items based on:

**Partition Key**

and optionally:

**Sort Key conditions**

Example:

CustomerId = 123

and:

OrderDate BETWEEN A AND B

### SAA Principle

> **Query is efficient when you know the partition key**

---

# Scan

A:

**Scan**

reads:

**Every item in the table or index**

then applies filtering.

This can be:

- Slow
- Expensive
- Inefficient

especially for:

**Large tables**

### Killer Exam Trap

> **Need to retrieve data efficiently**
>
> Avoid Scan when a Query/index can solve it.

### Memory Trick

**Query = Targeted**

**Scan = Search Everything**

---

# Query vs Scan

| Feature | Query | Scan |
|---|---:|---:|
| Uses Partition Key | ✅ | ❌ Required |
| Efficient | ✅ | Less Efficient |
| Reads Whole Table | ❌ | ✅ |
| Best for Known Access Pattern | ✅ | ❌ |

---

# DynamoDB Streams

**DynamoDB Streams**

captures:

**Item-level changes**

such as:

- Insert
- Update
- Delete

Architecture:

DynamoDB Table  
↓  
Stream  
↓  
Consumer

A common consumer is:

[[Lambda]]

---

## DynamoDB Streams + Lambda

Architecture:

DynamoDB Change  
↓  
DynamoDB Stream  
↓  
Lambda Event Source Mapping  
↓  
Lambda

Use cases:

- Notifications
- Data replication
- Audit workflows
- Search-index updates
- Downstream processing

### Killer Exam Clue

> **Run code whenever DynamoDB data changes**
>
> → **DynamoDB Streams + Lambda**

---

# DynamoDB Streams Ordering

Changes for a given item are preserved in:

**The order they occurred**

This helps event-driven processing maintain:

**Change sequence**

---

# DynamoDB Time to Live

DynamoDB:

**TTL**

lets you define an attribute containing:

**Expiration time**

After expiration:

DynamoDB automatically removes:

**Expired items**

### Killer Exam Clue

> **Automatically delete old/session data after a set time**
>
> → **DynamoDB TTL**

---

## TTL Use Cases

Good examples:

- Sessions
- Temporary tokens
- Expiring records
- Short-lived cache metadata

### Memory Trick

**TTL = Automatic Expiration**

---

# DynamoDB Transactions

DynamoDB supports:

**ACID transactions**

across multiple items/tables where supported.

Use when:

**Multiple DynamoDB operations must succeed or fail together**

### Killer Exam Clue

> **Need all-or-nothing updates across multiple DynamoDB items**
>
> → **DynamoDB Transactions**

---

# Conditional Writes

DynamoDB supports:

**Conditional expressions**

Example:

Update item only if:

`Version = 5`

This helps implement:

- Optimistic locking
- Duplicate protection
- Business rules

---

# Optimistic Locking

Pattern:

Read Version = 5  
↓  
Update Only If Version Still = 5  
↓  
Success

If another process changed the item:

Condition fails.

This prevents:

**Silent overwrite conflicts**

---

# DynamoDB Accelerator

[[DAX]] stands for:

**DynamoDB Accelerator**

It is an:

**In-memory cache specifically for DynamoDB**

Architecture:

Application  
↓  
DAX  
↓  
DynamoDB

Goal:

**Microsecond read latency**

---

## DAX Use Cases

Think DAX when:

- DynamoDB reads are very frequent
- Read latency must be extremely low
- Same items are repeatedly accessed
- Application is read-heavy

### Killer Exam Clue

> **Reduce DynamoDB read latency from milliseconds to microseconds**
>
> → **DAX**

---

# DAX Is Not for Write Acceleration

DAX primarily accelerates:

**Reads**

Do not choose DAX when the main requirement is:

**Improve DynamoDB write throughput**

---

# DAX vs ElastiCache

### DAX

Purpose:

**DynamoDB-specific cache**

### ElastiCache

Purpose:

**General-purpose application cache**

### Memory Trick

**DAX = DynamoDB Cache**

**ElastiCache = General Cache**

---

# DynamoDB Global Tables

**Global Tables**

provide:

**Multi-Region, active-active DynamoDB replication**

Architecture:

Region A  
↔  
Region B  
↔  
Region C

Applications can read and write:

**Locally in multiple Regions**

### Killer Exam Clue

> **Multi-Region active-active NoSQL database**
>
> → **DynamoDB Global Tables**

---

## Why Use Global Tables?

Use for:

- Global applications
- Multi-Region low latency
- Disaster recovery
- Active-active architectures

### Memory Trick

**Global Tables = Write Anywhere, Replicate Everywhere**

---

# Global Tables and Streams

Global Tables use:

**DynamoDB Streams technology**

to help replicate changes between:

**Regions**

The major exam takeaway:

> **Global Tables require Streams-related replication capability**

---

# DynamoDB High Availability

DynamoDB automatically stores data across:

**Multiple Availability Zones**

within a Region.

You do NOT manually:

- Configure replicas
- Build Multi-AZ
- Manage database servers

### SAA Principle

> **DynamoDB is inherently highly available within a Region**

---

# DynamoDB Backups

DynamoDB supports:

- On-demand backups
- Point-in-Time Recovery

---

# Point-in-Time Recovery

**PITR**

allows continuous backups and restoration to:

**A point in time**

within the supported recovery window.

### Killer Exam Clue

> **Recover DynamoDB table to a previous point in time**
>
> → **PITR**

---

# On-Demand Backup

An:

**On-Demand Backup**

creates a:

**Full table backup**

when requested.

Useful for:

- Compliance
- Planned backup points
- Long-term backup workflows

---

# DynamoDB Encryption

DynamoDB supports:

**Encryption at rest**

with integration with:

[[06-Security/KMS]]

You can use:

- AWS-owned keys
- AWS-managed keys
- Customer managed keys

depending on configuration.

---

# Encryption in Transit

Applications connect to DynamoDB using:

**HTTPS**

providing encryption:

**In transit**

---

# IAM Access Control

DynamoDB access is controlled using:

**IAM**

You can grant permissions such as:

- GetItem
- PutItem
- Query
- Scan
- UpdateItem

### SAA Principle

> **Use least privilege**

---

# Fine-Grained Access Control

IAM conditions can restrict access based on:

**Partition key values**

in supported scenarios.

Example:

User can only access items where:

`UserId = their own ID`

This supports:

**Fine-grained DynamoDB authorization**

---

# DynamoDB + Cognito

A common serverless pattern:

User  
↓  
Cognito  
↓  
API Gateway  
↓  
Lambda  
↓  
DynamoDB

This can provide:

- Authentication
- Serverless API
- Serverless compute
- Serverless database

---

# DynamoDB + API Gateway + Lambda

Classic architecture:

Client  
↓  
[[API Gateway]]  
↓  
[[Lambda]]  
↓  
DynamoDB

This architecture is:

**Fully serverless**

and can scale automatically.

### Killer Exam Pattern

> **Build a highly scalable serverless application backend**
>
> → **API Gateway + Lambda + DynamoDB**

---

# DynamoDB + S3

Use:

[[S3]]

when the data is:

**Large objects**

Use DynamoDB when the data is:

**Structured NoSQL application data**

Example:

Image File  
→ S3

Image Metadata  
→ DynamoDB

---

# DynamoDB vs RDS

This is a major exam comparison.

## DynamoDB

Think:

- NoSQL
- Serverless
- Key-value/document
- Massive scale
- Low latency
- No joins
- Access-pattern-driven design

## [[RDS]]

Think:

- Relational
- SQL
- Joins
- Transactions
- Structured relationships
- Traditional database model

### Killer Shortcut

**Need SQL/joins**
→ RDS

**Need massive serverless key-value scale**
→ DynamoDB

---

# DynamoDB vs Aurora Serverless

Both can provide:

**Serverless-style database capacity**

but the data models differ.

### DynamoDB

NoSQL

### Aurora Serverless

Relational SQL

### Exam Shortcut

**Relational**
→ Aurora/RDS

**NoSQL**
→ DynamoDB

---

# DynamoDB vs ElastiCache

### DynamoDB

Persistent:

**Database**

### ElastiCache

In-memory:

**Cache**

Do NOT choose ElastiCache as:

**The durable primary database**

unless architecture explicitly accepts that behavior.

---

# DynamoDB vs DAX

### DynamoDB

Persistent database

### DAX

Cache in front of DynamoDB

Architecture:

App  
↓  
DAX  
↓  
DynamoDB

---

# DynamoDB vs S3

### DynamoDB

Think:

**Low-latency application records**

### S3

Think:

**Objects/files**

---

# Architecture Thinking

## Scenario 1 — Serverless Shopping Cart

Need:

- Key-value data
- Millisecond latency
- Automatic scaling
- No servers

Choose:

**DynamoDB**

---

## Scenario 2 — Unpredictable Traffic

New application traffic may spike dramatically.

Team does not want capacity planning.

Choose:

**On-Demand Capacity**

---

## Scenario 3 — Predictable Traffic

Application has steady usage and wants:

**Cost-efficient planned capacity**

Choose:

**Provisioned Capacity + Auto Scaling**

---

## Scenario 4 — Latest Value Required

Financial workflow must immediately read:

**The latest successful write**

Choose:

**Strongly Consistent Read**

---

## Scenario 5 — Alternate Query

Table primary key is:

`UserId`

Application must efficiently query by:

`Email`

Choose:

**GSI**

---

## Scenario 6 — Different Sort Key

Table uses:

CustomerId + OrderDate

Need another view by:

CustomerId + OrderAmount

Choose:

**LSI**

if designed at table creation.

---

## Scenario 7 — Expiring Sessions

Session records should automatically disappear after:

24 hours.

Choose:

**TTL**

---

## Scenario 8 — Microsecond Reads

Read-heavy DynamoDB application needs:

**Microsecond latency**

Choose:

[[DAX]]

---

## Scenario 9 — Global Application

Users in:

- North America
- Europe
- Asia

need:

**Local reads and writes**

Choose:

**Global Tables**

---

## Scenario 10 — React to Changes

When DynamoDB item changes:

Run Lambda.

Choose:

DynamoDB Streams  
↓  
Lambda

---

## Scenario 11 — Multi-Item Atomic Update

Three DynamoDB items must:

**All update or none update**

Choose:

**DynamoDB Transactions**

---

## Scenario 12 — Efficient Retrieval

Application knows:

**Partition key**

Choose:

**Query**

not:

Scan

---

# Scenario Recognition

Immediately think:

**DynamoDB**

when you see:

- NoSQL
- Key-value
- Document database
- Serverless database
- Millisecond latency
- Massive scale
- No database servers
- Automatic scaling
- Partition key
- Sort key

---

## Think GSI When You See

- New access pattern
- Different partition key
- Query using non-primary key attribute

---

## Think LSI When You See

- Same partition key
- Different sort key
- Defined at table creation

---

## Think DAX When You See

- DynamoDB cache
- Microsecond reads
- Read-heavy DynamoDB workload

---

## Think Global Tables When You See

- Multi-Region
- Active-active
- Local reads/writes worldwide

---

# Exam Traps

## Trap 1 — DynamoDB Is Relational

❌

It is:

**NoSQL**

---

## Trap 2 — DynamoDB Requires Database Servers

❌

It is:

**Serverless / fully managed**

---

## Trap 3 — Scan Is the Most Efficient Way to Retrieve Known Data

❌

Use:

**Query**

and good key design.

---

## Trap 4 — GSI Must Use the Same Partition Key

❌

That describes:

**LSI**

GSI can use:

**Different partition key**

---

## Trap 5 — LSI Can Be Added Anytime

❌

LSI must be defined:

**At table creation**

---

## Trap 6 — GSI Supports Strongly Consistent Reads

❌

GSI reads are:

**Eventually consistent**

---

## Trap 7 — DAX Replaces DynamoDB

❌

DAX is:

**A cache in front of DynamoDB**

---

## Trap 8 — TTL Deletes Items at the Exact Expiration Second

❌

TTL deletion is:

**Automatic but asynchronous**

Do not depend on:

**Second-perfect deletion timing**

---

## Trap 9 — Global Tables Are Read-Only Replicas

❌

They support:

**Active-active multi-Region writes**

---

## Trap 10 — DynamoDB Streams Are the Same as Kinesis Data Streams

❌

DynamoDB Streams capture:

**DynamoDB item changes**

Kinesis is:

**General-purpose streaming data**

---

# Quick Cheat Sheet

| Exam Clue | Answer |
|---|---|
| Serverless NoSQL | DynamoDB |
| Primary Key Only | Partition Key |
| Composite Key | Partition + Sort Key |
| Unpredictable Traffic | On-Demand |
| Predictable Traffic | Provisioned |
| Latest Data Required | Strongly Consistent Read |
| Alternate Partition Key | GSI |
| Same Partition, New Sort Key | LSI |
| Efficient Key Lookup | Query |
| Reads Entire Table | Scan |
| Table Change Events | DynamoDB Streams |
| Automatic Expiration | TTL |
| Microsecond Reads | DAX |
| Multi-Region Active-Active | Global Tables |
| Atomic Multi-Item Update | Transactions |
| Point-in-Time Recovery | PITR |

---

# Key Design Cheat Sheet

| Requirement | Feature |
|---|---|
| Group Related Items | Partition Key |
| Order Items Within Group | Sort Key |
| Avoid Hot Partitions | High-Cardinality Partition Key |
| Query by New Partition Key | GSI |
| Same Partition + New Sort | LSI |

---

# Capacity Decision

Traffic is:

**Unpredictable / Spiky**

→ On-Demand

Traffic is:

**Predictable / Steady**

→ Provisioned + Auto Scaling

---

# Read Decision

Can tolerate slightly stale data?

→ Eventually Consistent

Must read latest write?

→ Strongly Consistent

---

# Index Decision

Need:

**Different Partition Key**

→ GSI

Need:

**Same Partition Key, Different Sort Key**

→ LSI

---

# Final Exam Rapid-Fire

> **SERVERLESS NOSQL**
> → DYNAMODB
>
> **UNPREDICTABLE TRAFFIC**
> → ON-DEMAND
>
> **PREDICTABLE TRAFFIC**
> → PROVISIONED
>
> **LATEST DATA**
> → STRONGLY CONSISTENT
>
> **DIFFERENT PARTITION KEY**
> → GSI
>
> **SAME PARTITION + DIFFERENT SORT**
> → LSI
>
> **KNOWN PARTITION KEY**
> → QUERY
>
> **READ ENTIRE TABLE**
> → SCAN
>
> **ITEM CHANGE**
> → DYNAMODB STREAMS
>
> **AUTO EXPIRE**
> → TTL
>
> **MICROSECOND READ**
> → DAX
>
> **GLOBAL ACTIVE-ACTIVE**
> → GLOBAL TABLES
>
> **ALL-OR-NOTHING MULTI-ITEM WRITE**
> → TRANSACTION
>
> **RECOVER TO EARLIER TIME**
> → PITR

---

## Master Memory Trick

> [!tip] DynamoDB Master Memory Trick
> Imagine a giant warehouse with no traditional relational filing cabinets.
>
> Every item needs:
>
> **A shelf location**
>
> That's:
>
> **PARTITION KEY**
>
> Items on the same shelf can be ordered by:
>
> **SORT KEY**
>
> Need another way to find things?
>
> **GSI**
> → Build another global lookup path
>
> **LSI**
> → Keep the same shelf but sort differently
>
> Need ultra-fast repeated reads?
>
> **DAX**
> → Put a cache at the front desk
>
> Need items to disappear automatically?
>
> **TTL**
> → Expiration date
>
> Need every warehouse around the world to accept updates?
>
> **GLOBAL TABLES**
> → Active-active worldwide warehouses

So remember:

> **DYNAMODB**
> → SERVERLESS NOSQL
>
> **PARTITION KEY**
> → DISTRIBUTE
>
> **SORT KEY**
> → ORGANIZE
>
> **GSI**
> → NEW PARTITION KEY
>
> **LSI**
> → SAME PARTITION, NEW SORT
>
> **DAX**
> → MICROSECOND CACHE
>
> **TTL**
> → EXPIRE
>
> **STREAMS**
> → REACT TO CHANGES
>
> **GLOBAL TABLES**
> → MULTI-REGION ACTIVE-ACTIVE

And the killer SAA question:

> **"Do I need a serverless NoSQL database that can scale massively with very low latency?"**
>
> YES
>
> → **DynamoDB**

---

## Related Notes

- [[Lambda]]
- [[Lambda Event Source Mapping]]
- [[API Gateway]]
- [[DAX]]
- [[RDS]]
- [[S3]]
- [[20-SAA/10-Messaging/Kinesis Data Streams]]
- [[IAM]]
- [[06-Security/KMS]]
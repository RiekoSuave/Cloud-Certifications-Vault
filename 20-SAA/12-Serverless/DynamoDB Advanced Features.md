## What Problem Does It Solve?

[[DynamoDB Advanced Features]] covers the features that help DynamoDB handle:

- Multi-Region applications
- Caching
- Item expiration
- Event-driven workflows
- Transactions
- Backups
- Recovery
- Advanced access patterns

The big SAA goal is to recognize:

> **Which DynamoDB feature solves which architecture problem?**

> [!tip] Master Memory Trick
> **DAX = CACHE**
>
> **TTL = EXPIRE**
>
> **STREAMS = REACT**
>
> **GLOBAL TABLES = MULTI-REGION**
>
> **TRANSACTIONS = ALL OR NOTHING**
>
> **PITR = RECOVER**

---

## DynamoDB Accelerator

[[DAX]] stands for:

**DynamoDB Accelerator**

It is a:

**Fully managed in-memory cache for DynamoDB**

Architecture:

Application  
↓  
DAX  
↓  
DynamoDB

The goal is to reduce:

**Read latency**

from milliseconds to:

**Microseconds**

---

## When to Use DAX

Think DAX when an application has:

- Heavy read traffic
- Repeated reads of the same items
- Very low-latency requirements
- Read-heavy DynamoDB workloads

### Killer Exam Clue

> **Reduce DynamoDB read latency to microseconds**
>
> → **DAX**

---

## DAX Is DynamoDB-Specific

DAX is designed specifically for:

**DynamoDB**

It is not a general-purpose cache for:

- RDS
- APIs
- Arbitrary application objects

For general-purpose caching, think:

**ElastiCache**

### Memory Trick

**DAX = DynamoDB Cache**

**ElastiCache = General Cache**

---

## DAX Read Path

Without DAX:

Application  
↓  
DynamoDB

With DAX:

Application  
↓  
DAX  
↓  
Cache Hit?

Yes  
→ Return Cached Data

No  
→ DynamoDB  
→ Cache Result  
→ Return Data

---

## DAX Is Not a Write Scaling Tool

DAX mainly improves:

**Read performance**

Do NOT choose DAX when the requirement is:

- Increase write throughput
- Reduce write throttling
- Improve write capacity

For those problems, think about:

- Capacity mode
- Partition-key design
- Auto Scaling
- Write patterns

---

## DAX and Eventually Consistent Reads

DAX is best associated with:

**Eventually consistent reads**

because cached data may not always reflect:

**The newest write immediately**

If the application requires:

**Strictly up-to-date reads**

consider whether DAX is appropriate for that access path.

---

# Time to Live

DynamoDB:

**Time to Live — TTL**

automatically removes items after:

**A configured expiration timestamp**

Architecture:

Item  
↓  
TTL Attribute  
↓  
Expiration Time Reached  
↓  
DynamoDB Removes Item

### Killer Exam Clue

> **Automatically expire old DynamoDB items**
>
> → **TTL**

---

## TTL Use Cases

Common uses include:

- User sessions
- Temporary tokens
- Old event records
- Expiring cache data
- Temporary application state

Example:

Session Created  
↓  
TTL = 24 Hours  
↓  
Eventually Removed Automatically

---

## TTL Attribute

TTL uses an attribute containing:

**A Unix epoch timestamp**

representing when the item should expire.

The attribute is configured as:

**The table's TTL attribute**

---

## TTL Deletion Is Asynchronous

An important exam trap:

TTL does NOT guarantee:

**Deletion at the exact expiration second**

Expired items are removed:

**Asynchronously**

### Memory Trick

**TTL = Eligible for deletion, not instant deletion**

---

## TTL + DynamoDB Streams

When TTL removes an item:

That deletion can appear in:

**DynamoDB Streams**

This can enable downstream workflows.

Architecture:

TTL Expiration  
↓  
Item Deleted  
↓  
DynamoDB Stream  
↓  
Lambda

---

# DynamoDB Streams

DynamoDB Streams captures:

**Item-level changes**

Examples:

- INSERT
- MODIFY
- REMOVE

Architecture:

DynamoDB Table  
↓  
DynamoDB Stream  
↓  
Consumer

A common consumer is:

[[Lambda]]

---

## Stream Record Contents

Depending on configuration, stream records can contain:

- Keys only
- New image
- Old image
- New and old images

This lets downstream consumers understand:

**What changed**

---

## DynamoDB Streams + Lambda

Classic architecture:

DynamoDB Change  
↓  
DynamoDB Streams  
↓  
Lambda Event Source Mapping  
↓  
Lambda

Use cases:

- Trigger notifications
- Update search indexes
- Replicate data
- Maintain derived data
- Run business logic

### Killer Exam Clue

> **Run code when DynamoDB items change**
>
> → **DynamoDB Streams + Lambda**

---

## Streams Retention

DynamoDB Streams retains change records for:

**A limited period**

The key SAA point:

> **Streams are for near-real-time change processing, not long-term event storage**

If long-term event retention is required:

Think about:

- Kinesis
- S3
- EventBridge archive

depending on architecture.

---

## Streams Ordering

Changes to the same item are delivered in:

**The order they occurred**

This is important for:

**Consistent event processing**

---

# Global Tables

**DynamoDB Global Tables**

provide:

**Multi-Region active-active replication**

Architecture:

Region A DynamoDB  
↔  
Region B DynamoDB  
↔  
Region C DynamoDB

Applications can:

**Read and write locally in multiple Regions**

### Killer Exam Clue

> **Multi-Region active-active NoSQL database**
>
> → **DynamoDB Global Tables**

---

## Why Use Global Tables?

Global Tables are useful for:

- Global applications
- Low-latency regional access
- Disaster recovery
- Multi-Region writes
- Regional resilience

### Memory Trick

**Global Tables = Active-Active Everywhere**

---

## Active-Active

Active-active means:

**Multiple Regions can accept writes**

This is different from:

**Read-only replica architectures**

### Exam Trap

Global Tables are NOT:

**Primary Region + read-only secondary Region**

They are:

**Multi-Region active-active**

---

## Global Tables and Replication

Changes made in one Region are replicated to:

**Other participating Regions**

Architecture:

Write in Region A  
↓  
Replicate  
↓  
Region B + Region C

This gives globally distributed applications:

**Local database access**

---

## Conflict Resolution

In multi-Region writes:

Conflicts can occur.

DynamoDB resolves replication conflicts using:

**Service-managed conflict resolution**

For SAA, the important point is:

> **Global Tables support active-active writes without you building replication yourself**

---

## Global Tables vs Aurora Global Database

### DynamoDB Global Tables

Think:

- NoSQL
- Active-active writes
- Serverless
- Key-value/document

### Aurora Global Database

Think:

- Relational SQL
- Cross-Region replication
- Primary-writer architecture with secondary Regions

### Killer Shortcut

**Global NoSQL active-active**
→ DynamoDB Global Tables

**Global relational SQL**
→ Aurora Global Database

---

# DynamoDB Transactions

DynamoDB supports:

**ACID transactions**

for multiple item operations.

Use when:

**Several operations must succeed or fail together**

Architecture:

Update Item A  
+  
Update Item B  
+  
Update Item C  
↓  
Transaction

Either:

All Succeed

or:

All Fail

### Killer Exam Clue

> **All-or-nothing updates across multiple DynamoDB items**
>
> → **DynamoDB Transactions**

---

## Transaction Use Case

Example:

Transfer $100:

Account A  
→ Subtract $100

Account B  
→ Add $100

These operations must:

**Both succeed**

or:

**Neither succeed**

Use:

**Transaction**

---

## TransactWriteItems

A transactional write can include operations such as:

- Put
- Update
- Delete
- Condition Check

The key idea:

**Atomic multi-item write operation**

---

## TransactGetItems

DynamoDB also supports transactional reads across:

**Multiple items**

This provides:

**A consistent transactional view**

of those items.

---

# Conditional Writes

A:

**Conditional Write**

changes an item only if:

**A specified condition is true**

Example:

Update order only if:

`Status = PENDING`

This helps prevent:

- Race conditions
- Duplicate updates
- Invalid state transitions

---

## Optimistic Locking

Optimistic locking uses a:

**Version number**

Example:

Read:

Version = 3

Update:

Only if Version = 3

Then:

Set Version = 4

If another process already changed it:

**The condition fails**

### Killer Exam Clue

> **Prevent concurrent writers from silently overwriting each other's DynamoDB changes**
>
> → **Conditional Write / Optimistic Locking**

---

# Atomic Counters

DynamoDB can perform:

**Atomic counter updates**

Example:

PageViews = PageViews + 1

without requiring:

Read  
↓  
Modify Locally  
↓  
Write Full Value

This helps safely handle:

**Concurrent counter updates**

---

# Point-in-Time Recovery

**Point-in-Time Recovery — PITR**

provides:

**Continuous backup capability**

for DynamoDB tables.

It allows restoration to:

**A previous point in time**

within the supported recovery window.

### Killer Exam Clue

> **Recover a DynamoDB table to an earlier point in time**
>
> → **PITR**

---

## PITR Use Cases

Use PITR for:

- Accidental deletes
- Bad application updates
- Data corruption
- Recovery from unwanted changes

### Memory Trick

**PITR = Undo the table clock**

---

# On-Demand Backups

DynamoDB also supports:

**On-Demand Backups**

These create:

**A backup when requested**

Use for:

- Compliance snapshots
- Pre-change backups
- Long-term backup workflows

---

## PITR vs On-Demand Backup

### PITR

Think:

**Continuous recovery timeline**

### On-Demand Backup

Think:

**Manual snapshot**

### Memory Trick

**PITR = Timeline**

**On-Demand = Snapshot**

---

# Backup Impact

DynamoDB backups do not require you to:

**Stop the table**

The table can remain:

**Available**

while backup operations occur.

This supports:

**Highly available production workloads**

---

# Restore Behavior

Restoring a DynamoDB backup or PITR typically creates:

**A new table**

rather than overwriting:

**The existing table in place**

### Exam Trap

> Recovery does not usually mean "rewind the same live table in place."

Think:

**Restore to a new table**

---

# DynamoDB Encryption

DynamoDB data is encrypted:

**At rest**

and integrates with:

[[06-Security/KMS]]

Possible key types include:

- AWS-owned key
- AWS-managed key
- Customer managed key

---

## Customer Managed KMS Key

Choose a customer managed key when you need:

- Greater key control
- Key-policy management
- Audit requirements
- Rotation/control requirements

### Killer Exam Clue

> **Need customer control over DynamoDB encryption keys**
>
> → **Customer Managed KMS Key**

---

# Fine-Grained Access Control

DynamoDB can use:

**IAM condition keys**

to restrict access to:

**Specific partition-key values**

Example:

User A can access only:

`UserId = A`

User B can access only:

`UserId = B`

This is useful for:

**Multi-user applications**

---

## LeadingKeys

A commonly associated DynamoDB IAM condition is:

**LeadingKeys**

This can restrict operations based on:

**Partition key values**

### Exam Pattern

> **Users should access only their own DynamoDB records**
>
> → **Fine-Grained IAM using partition-key conditions**

---

# DynamoDB + Cognito

Architecture:

User  
↓  
[[Cognito]]  
↓  
Temporary Credentials  
↓  
DynamoDB

This can allow authenticated users to:

**Access only permitted table items**

with appropriately designed:

**IAM policies**

---

# DynamoDB Export to S3

DynamoDB can export table data to:

[[S3]]

This is useful for:

- Analytics
- Archival
- Data lake workflows
- Offline processing

Architecture:

DynamoDB  
↓  
Export  
↓  
S3  
↓  
Analytics

---

## Why Export to S3?

S3 integrates well with:

- Athena
- Glue
- EMR
- Redshift
- Data lake architectures

This allows analytical workloads to avoid:

**Scanning the production DynamoDB table repeatedly**

---

# DynamoDB Import from S3

DynamoDB can also support:

**Importing data from S3**

This helps with:

- Bulk data loading
- Migration
- Data ingestion

---

# DynamoDB PartiQL

DynamoDB supports:

**PartiQL**

which provides:

**SQL-compatible query syntax**

for DynamoDB data.

Important:

PartiQL does NOT turn DynamoDB into:

**A relational database**

The underlying data model remains:

**NoSQL**

### Exam Trap

> SQL-like syntax does not mean relational behavior.

---

# Contributor Insights

DynamoDB can integrate with:

**CloudWatch Contributor Insights**

to help identify:

- Frequently accessed keys
- Traffic patterns
- Potential hot keys

### Killer Exam Clue

> **Identify the most frequently accessed DynamoDB partition keys**
>
> → **Contributor Insights**

---

# Hot Partition Troubleshooting

Symptoms:

- Throttling
- Uneven traffic
- One key receiving most requests

Possible cause:

**Poor partition-key design**

Possible solution:

- Increase key cardinality
- Distribute writes
- Redesign access pattern

Do NOT assume:

**Simply increasing table capacity always fixes bad key distribution**

---

# Write Sharding

For extremely hot write keys:

You can introduce:

**Write sharding**

Example:

Instead of:

`PartitionKey = 2026-08-26`

use:

`2026-08-26#1`

`2026-08-26#2`

`2026-08-26#3`

This distributes:

**Writes across multiple partition-key values**

### Exam Concept

> **Artificially increase partition-key distribution to avoid hot partitions**

---

# Sparse Indexes

A secondary index only contains items that have:

**The index key attributes**

This can create a:

**Sparse Index**

Example:

Only orders with:

`Escalated = true`

contain the indexed attribute.

The GSI then naturally contains:

**Only escalated orders**

### Killer Exam Pattern

> **Efficiently query a small subset of items based on an attribute that exists only on those items**
>
> → **Sparse GSI pattern**

---

# GSI Overloading

A GSI can sometimes support:

**Multiple access patterns**

by storing different item types using:

**Shared index attributes**

This is an advanced single-table design technique.

For SAA, the main concept is:

> **Indexes can be designed around application access patterns**

---

# DynamoDB Standard vs Standard-IA

DynamoDB offers table classes optimized for:

**Different storage/access patterns**

### Standard

Best for:

**Frequently accessed data**

### Standard-IA

Best for:

**Infrequently accessed data where storage cost matters more**

### Killer Exam Clue

> **Large DynamoDB table with infrequently accessed items and storage cost concern**
>
> → **Standard-IA table class**

---

# Architecture Thinking

## Scenario 1 — Microsecond Reads

Read-heavy application repeatedly accesses the same DynamoDB items.

Need:

**Microsecond latency**

Choose:

[[DAX]]

---

## Scenario 2 — Session Expiration

Session items should disappear automatically after:

30 minutes.

Choose:

**TTL**

---

## Scenario 3 — React to Item Changes

When order status changes:

Run business logic.

Choose:

DynamoDB Streams  
↓  
Lambda

---

## Scenario 4 — Global Shopping App

Users worldwide need:

**Local reads and writes**

Choose:

**Global Tables**

---

## Scenario 5 — Money Transfer

Two items must update:

**Atomically**

Choose:

**Transactions**

---

## Scenario 6 — Concurrent Writers

Two users may update:

**The same item**

Need to prevent overwrites.

Choose:

**Conditional Writes / Optimistic Locking**

---

## Scenario 7 — Accidental Delete

Administrator accidentally deletes important data.

Need recovery to:

**Yesterday at 3:15 PM**

Choose:

**PITR**

---

## Scenario 8 — Compliance Backup

Need:

**A backup before a major release**

Choose:

**On-Demand Backup**

---

## Scenario 9 — User-Specific Access

Each user should read:

**Only their own items**

Choose:

**Fine-Grained IAM with partition-key conditions**

---

## Scenario 10 — Analytics

Analysts need to run large queries without impacting:

**Production DynamoDB traffic**

Choose:

DynamoDB Export  
↓  
S3  
↓  
Analytics Services

---

## Scenario 11 — Hot Key

One partition key receives:

**Most table writes**

and throttling occurs.

Think:

**Partition-key redesign / write sharding**

---

## Scenario 12 — Find Hot Keys

Operations team needs to identify:

**Which partition keys generate the most traffic**

Choose:

**Contributor Insights**

---

# Scenario Recognition

Immediately think:

**DAX**

when you see:

- Microsecond DynamoDB reads
- DynamoDB cache
- Read-heavy workload

---

## Immediately Think TTL When You See

- Expiration
- Sessions
- Temporary records
- Automatic deletion

---

## Immediately Think Streams When You See

- Item changes
- Trigger downstream processing
- Lambda on INSERT/MODIFY/REMOVE

---

## Immediately Think Global Tables When You See

- Multi-Region
- Active-active
- Global low latency
- Local writes

---

## Immediately Think Transactions When You See

- Atomic
- All-or-nothing
- Multiple item operations

---

## Immediately Think PITR When You See

- Recover earlier table state
- Accidental deletion
- Continuous backup

---

# Exam Traps

## Trap 1 — DAX Improves Write Throughput

❌

DAX primarily improves:

**Read latency**

---

## Trap 2 — TTL Deletes Items at the Exact Expiration Time

❌

Deletion is:

**Asynchronous**

---

## Trap 3 — Global Tables Are Read Replicas

❌

They provide:

**Active-active reads and writes**

---

## Trap 4 — DynamoDB Streams Are Long-Term Event Storage

❌

Streams are:

**Change-data capture with limited retention**

---

## Trap 5 — PITR Overwrites the Existing Table

❌

Recovery generally creates:

**A new table**

---

## Trap 6 — PartiQL Makes DynamoDB Relational

❌

It remains:

**NoSQL**

---

## Trap 7 — Increasing Capacity Always Solves Hot Keys

❌

Poor partition-key design may still create:

**Uneven workload concentration**

---

## Trap 8 — DAX Is General-Purpose Redis

❌

DAX is:

**DynamoDB-specific**

---

## Trap 9 — On-Demand Backup and PITR Are Identical

❌

PITR:

**Continuous timeline**

On-Demand:

**Point snapshot**

---

## Trap 10 — Global Tables Require You to Build Cross-Region Replication Logic

❌

DynamoDB manages:

**Multi-Region replication**

---

# Quick Cheat Sheet

| Exam Clue | Feature |
|---|---|
| Microsecond DynamoDB Reads | DAX |
| Automatic Item Expiration | TTL |
| React to Item Changes | DynamoDB Streams |
| Multi-Region Active-Active | Global Tables |
| Atomic Multi-Item Operations | Transactions |
| Prevent Concurrent Overwrite | Conditional Write |
| Restore Earlier Table State | PITR |
| Manual Backup Point | On-Demand Backup |
| User-Specific Item Access | Fine-Grained IAM |
| Export for Analytics | Export to S3 |
| Identify Hot Keys | Contributor Insights |
| Distribute Hot Writes | Write Sharding |
| Infrequently Accessed Table | Standard-IA |

---

# DAX vs ElastiCache

| Requirement | DAX | ElastiCache |
|---|---:|---:|
| DynamoDB-Specific | ✅ | ❌ |
| General Cache | ❌ | ✅ |
| Microsecond DynamoDB Reads | ✅ | Possible but Custom |
| Transparent DynamoDB Cache Pattern | ✅ | ❌ |

---

# Backup Decision

Need:

**Continuous recovery timeline**

→ PITR

Need:

**Specific manual backup**

→ On-Demand Backup

---

# Global Database Decision

Need:

**Global NoSQL active-active**

→ DynamoDB Global Tables

Need:

**Global relational SQL**

→ Aurora Global Database

---

# Event Decision

Need:

**React to DynamoDB item changes**

→ DynamoDB Streams

Need:

**Keep events long term**

→ Consider Kinesis / EventBridge Archive / S3 depending on architecture

---

# Final Exam Rapid-Fire

> **MICROSECOND READS**
> → DAX
>
> **AUTO EXPIRE**
> → TTL
>
> **ITEM CHANGE EVENT**
> → DYNAMODB STREAMS
>
> **MULTI-REGION ACTIVE-ACTIVE**
> → GLOBAL TABLES
>
> **ALL OR NOTHING**
> → TRANSACTIONS
>
> **CONCURRENT UPDATE PROTECTION**
> → CONDITIONAL WRITE
>
> **RECOVER TO EARLIER TIME**
> → PITR
>
> **MANUAL BACKUP**
> → ON-DEMAND BACKUP
>
> **USER ONLY SEES OWN ITEMS**
> → FINE-GRAINED IAM
>
> **ANALYTICS OFFLOAD**
> → EXPORT TO S3
>
> **FIND HOT KEYS**
> → CONTRIBUTOR INSIGHTS
>
> **HOT WRITE KEY**
> → WRITE SHARDING
>
> **INFREQUENT ACCESS**
> → STANDARD-IA

---

## Master Memory Trick

> [!tip] DynamoDB Advanced Features Master Memory Trick
> Imagine DynamoDB as a giant global warehouse.
>
> Customers keep asking for the same box:
>
> **DAX**
> → Put a super-fast cache at the front desk
>
> Old boxes need to disappear:
>
> **TTL**
> → Put expiration dates on them
>
> Someone changes a box:
>
> **STREAMS**
> → Ring an event bell
>
> Warehouses around the world all need to accept updates:
>
> **GLOBAL TABLES**
> → Active-active warehouses
>
> Several box changes must happen together:
>
> **TRANSACTIONS**
> → All or nothing
>
> Someone damaged yesterday's inventory:
>
> **PITR**
> → Turn back the warehouse clock

So remember:

> **DAX**
> → CACHE
>
> **TTL**
> → EXPIRE
>
> **STREAMS**
> → REACT
>
> **GLOBAL TABLES**
> → GLOBAL ACTIVE-ACTIVE
>
> **TRANSACTIONS**
> → ATOMIC
>
> **PITR**
> → RECOVER
>
> **CONTRIBUTOR INSIGHTS**
> → FIND HOT KEYS

And the killer SAA question:

> **"What problem is the DynamoDB feature solving: latency, expiration, events, global replication, atomicity, or recovery?"**
>
> Identify that first, and the feature usually becomes obvious.

---

## Related Notes

- [[DynamoDB]]
- [[DAX]]
- [[Lambda]]
- [[Lambda Event Source Mapping]]
- [[20-SAA/10-Messaging/Kinesis Data Streams]]
- [[20-SAA/10-Messaging/EventBridge]]
- [[S3]]
- [[Aurora Global Database]]
- [[IAM]]
- [[06-Security/KMS]]
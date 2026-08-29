## What Problem Does It Solve?

[[Neptune Streams]] provides a **real-time ordered sequence of every change made to graph data in [[Neptune]]**.

It solves the problem of:

> **"How can another application know what changed inside my Neptune graph?"**

Instead of repeatedly querying Neptune to determine what changed, an application can consume the stream of changes.

Think of Neptune Streams as:

**Change Data Capture (CDC) for [[Neptune]].**

---

## How Neptune Streams Works

When data changes inside [[Neptune]], the changes are recorded in [[Neptune Streams]].

Basic architecture:

Application  
↓ writes data  
[[Neptune]] Cluster  
↓  
[[Neptune Streams]]  
↓  
Streams Reader Application  
↓  
Other Systems

Possible downstream destinations include:

- [[S3]]
- [[20-SAA/05-Databases/OpenSearch]]
- [[ElastiCache]]
- Another Neptune deployment
- Custom applications

### Architecture Thinking

Think:

**Neptune = stores the graph**

**Neptune Streams = tells you what changed in the graph**

Example:

A user creates a new relationship:

User A → FOLLOWS → User B

The application writes the relationship to [[Neptune]].

That change becomes available through [[Neptune Streams]], allowing another application to react to it.

---

## Core Neptune Streams Characteristics

### Real-Time Changes

Changes become available **immediately after they are written** to Neptune.

This makes Neptune Streams useful for applications that need to react quickly when graph data changes.

---

### Ordered Changes

Neptune Streams maintains a:

**Strictly ordered sequence of changes**

This matters when downstream applications need to process graph updates in the same order they occurred.

---

### No Duplicates

Neptune Streams does **not create duplicate change records**.

For the exam, associate Neptune Streams with:

**Real-time + Ordered + No Duplicates**

> [!tip] Memory Trick
> **RON**
>
> **R** = Real-time  
> **O** = Ordered  
> **N** = No duplicates

---

## Accessing Neptune Streams

Neptune Streams data can be accessed through an:

**HTTP REST API**

Architecture:

[[Neptune]]  
↓  
[[Neptune Streams]]  
↓  
HTTP GET Request  
↓  
Streams Reader Application

The reader application retrieves changes from the stream and can then process or forward those changes elsewhere.

---

## Neptune Streams Use Cases

### 1. Send Notifications When Data Changes

Suppose a social networking application stores relationships in [[Neptune]].

A user follows another user:

User A → FOLLOWS → User B

[[Neptune Streams]] records the change.

A downstream application can detect it and trigger:

**"User A started following you."**

Architecture:

User Action  
↓  
[[Neptune]]  
↓  
[[Neptune Streams]]  
↓  
Notification Application  
↓  
Notification

---

### 2. Synchronize Neptune with Another Data Store

One of the most important Neptune Streams use cases is keeping graph data synchronized with another datastore.

Example:

[[Neptune]]  
↓  
[[Neptune Streams]]  
↓  
Streams Reader  
↓  
[[20-SAA/05-Databases/OpenSearch]]

Now changes to graph data can also be reflected in [[20-SAA/05-Databases/OpenSearch]].

The SAA slides specifically show Neptune Streams synchronizing data with:

- [[S3]]
- [[20-SAA/05-Databases/OpenSearch]]
- [[ElastiCache]]

---

### 3. Replicate Neptune Data Across Regions

Neptune Streams can also help replicate graph changes across AWS Regions.

Architecture:

Region A  
[[Neptune]]  
↓  
[[Neptune Streams]]  
↓  
Replication Application  
↓  
Region B  
[[Neptune]]

This can be useful when an architecture requires Neptune graph data to be maintained in another Region.

---

## Architecture Thinking

### Scenario 1 — Synchronize Neptune and OpenSearch

A company stores relationship data in [[Neptune]] but wants changes to automatically become available to a search application using [[20-SAA/05-Databases/OpenSearch]].

**Choose → [[Neptune Streams]]**

Why?

The requirement is to capture changes made to the Neptune graph and synchronize them with another datastore.

---

### Scenario 2 — React to Graph Changes

A social networking application needs to trigger notifications whenever certain relationships are added to its Neptune graph.

Example:

User → FOLLOWS → User

The application needs to detect the change shortly after it occurs.

**Choose → [[Neptune Streams]]**

---

### Scenario 3 — Maintain Another Copy of Graph Data

A company needs changes from its Neptune database to be replicated into Neptune in another AWS Region.

**Choose → [[Neptune Streams]]**

The stream provides the sequence of graph changes that a replication application can process.

---

### Scenario 4 — Query Relationships

A company needs to determine how millions of users, devices, transactions, and IP addresses are connected.

**Choose → [[Neptune]]**

Not [[Neptune Streams]].

Why?

The requirement is to **query relationships**, not capture changes.

---

## Neptune vs Neptune Streams

This distinction is important.

| Requirement | Solution |
|---|---|
| Store graph data | [[Neptune]] |
| Query relationships | [[Neptune]] |
| Fraud relationship analysis | [[Neptune]] |
| Recommendation graph | [[Neptune]] |
| Capture graph changes | [[Neptune Streams]] |
| Ordered sequence of changes | [[Neptune Streams]] |
| React when graph data changes | [[Neptune Streams]] |
| Synchronize graph changes elsewhere | [[Neptune Streams]] |

### Memory Trick

**Neptune = Current graph**

**Neptune Streams = What changed**

---

## Neptune Streams vs Kinesis Data Streams

Don't automatically choose [[20-SAA/10-Messaging/Kinesis Data Streams]] just because a question contains the word **stream**.

### [[Neptune Streams]]

Designed specifically to capture:

**Changes occurring inside a Neptune graph**

### [[20-SAA/10-Messaging/Kinesis Data Streams]]

Designed for general-purpose streaming data ingestion and processing.

Examples:

- Application events
- Clickstreams
- IoT events
- Logs
- Real-time data feeds

### Exam Decision

If the scenario says:

> "Capture every change made to graph data in Neptune"

**Choose → [[Neptune Streams]]**

If the scenario says:

> "Ingest a massive stream of real-time application events"

Think → [[20-SAA/10-Messaging/Kinesis Data Streams]]

---

## Scenario Recognition

### Exam Keywords

Immediately think **[[Neptune Streams]]** when you see:

- Neptune graph changes
- Capture changes to graph data
- Real-time sequence of graph changes
- Ordered graph changes
- No duplicate change records
- React to Neptune changes
- Synchronize Neptune data
- Neptune change notifications
- Replicate Neptune changes across Regions
- HTTP REST API for Neptune changes

### Key Pattern

> **Neptune already exists + something needs to react to changes = Neptune Streams**

---

## Exam Traps

### Trap 1 — Neptune vs Neptune Streams

If the question asks about:

**Relationships themselves → [[Neptune]]**

If the question asks about:

**Changes to those relationships → [[Neptune Streams]]**

---

### Trap 2 — Neptune Streams vs Kinesis Data Streams

The word **stream** does not automatically mean [[20-SAA/10-Messaging/Kinesis Data Streams]].

Look at the source of the data.

**Changes inside Neptune → [[Neptune Streams]]**

**General streaming workload → [[20-SAA/10-Messaging/Kinesis Data Streams]]**

---

### Trap 3 — Forgetting Strict Ordering

Neptune Streams provides a **strictly ordered sequence** of changes.

If ordering of Neptune graph changes is important, this is a strong Neptune Streams clue.

---

### Trap 4 — Assuming Duplicate Records

The SAA slides specifically emphasize:

**No duplicates**

Remember:

**Real-time + Strict Order + No Duplicates**

---

### Trap 5 — Thinking Streams Is Another Database

[[Neptune Streams]] is not a separate graph database.

[[Neptune]] stores and queries the graph.

[[Neptune Streams]] exposes the **changes made to that graph**.

---

## Quick Cheat Sheet

| Feature | Neptune Streams |
|---|---|
| Purpose | Capture Neptune graph changes |
| Change Availability | Immediately after writing |
| Ordering | Strict order |
| Duplicates | No duplicates |
| Access | HTTP REST API |
| Notifications | ✅ |
| Synchronize Datastores | ✅ |
| Cross-Region Replication | ✅ |
| Works with S3 | ✅ |
| Works with OpenSearch | ✅ |
| Works with ElastiCache | ✅ |

---

## Master Memory Trick

> [!tip] Master Memory Trick
> **Neptune Streams = Graph Change Log**
>
> [[Neptune]] tells you:
>
> **"What relationships exist?"**
>
> [[Neptune Streams]] tells you:
>
> **"What relationships changed?"**

Remember:

**Neptune = Relationships**

**Neptune Streams = Relationship Changes**

And for the stream itself:

### RON

**R = Real-time**

**O = Ordered**

**N = No duplicates**

---

## Related Notes

- [[Neptune]]
- [[20-SAA/05-Databases/OpenSearch]]
- [[ElastiCache]]
- [[S3]]
- [[20-SAA/10-Messaging/Kinesis Data Streams]]
- [[Availability Zones]]
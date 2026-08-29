## What Problem Does It Solve?

[[Neptune]] is a **fully managed graph database** designed for data where the **relationships between objects are just as important as the objects themselves**.

Instead of primarily thinking in rows, columns, or key-value pairs, think:

**Entity → Relationship → Entity**

Example:

User A ──FRIENDS_WITH──> User B  
   │  
   └──LIKES──> Post 1 ──HAS_COMMENT──> Comment 1

This makes Neptune well suited for **highly connected datasets** where relationship queries would become complex in a traditional relational database.

> [!tip] Memory Trick
> **Neptune = Network of relationships**
>
> If the exam emphasizes **connections, relationships, graphs, friends, fraud patterns, or recommendations → think Neptune.**

---

## Neptune Core Architecture

Neptune is a:

- **Fully managed graph database**
- Designed for **highly connected datasets**
- Optimized for complex relationship queries
- Capable of storing **billions of relationships**
- Designed for **millisecond query latency**
- Highly available across multiple [[Availability Zones]]
- Supports **up to 15 read replicas**

### Architecture Thinking

Think of Neptune as:

Application  
↓  
Neptune Cluster  
├── Writer Instance  
├── Read Replica  
├── Read Replica  
└── Read Replica  

Deployed across multiple [[Availability Zones]] for high availability.

The key SAA concept isn't memorizing every internal component.

The important architectural question is:

> **Does the application need to efficiently traverse large numbers of relationships?**

If yes, [[Neptune]] should immediately be on your radar.

---

## Why a Graph Database?

Imagine building a social network.

You need to answer questions such as:

- Who are this user's friends?
- Which friends liked this post?
- Which users share common friends?
- What content do similar users like?
- How are multiple suspicious accounts connected?

A relational database could model these relationships using tables and joins.

But as the number and depth of relationships increase:

User  
↓  
Friends  
↓  
Friends of Friends  
↓  
Posts  
↓  
Comments  
↓  
Likes  

Queries can become increasingly complex.

[[Neptune]] is specifically optimized for querying these **connected relationships**.

A classic graph dataset is a social network:

- Users have friends
- Posts have comments
- Comments receive likes
- Users share posts
- Users like posts

---

## Common Neptune Use Cases

### Social Networks

Example relationships:

User → Friend → User  
User → Likes → Post  
User → Follows → User  

The relationships themselves are a major part of the data model.

**Choose → [[Neptune]]**

---

### Fraud Detection

A financial company may need to uncover relationships between:

Account  
↓  
Credit Card  
↓  
Transaction  
↓  
IP Address  
↓  
Device  
↓  
Another Account  

The individual records may appear normal.

The suspicious behavior may only become visible when analyzing **how the entities are connected**.

**Choose → [[Neptune]]**

---

### Recommendation Engines

Example:

User A → likes → Product X  
User B → likes → Product X  
User B → likes → Product Y  

The application may infer:

**User A may also like Product Y.**

Recommendation systems based heavily on relationships can be a strong use case for [[Neptune]].

---

### Knowledge Graphs

Knowledge graphs represent relationships between pieces of information.

Example:

Detroit → located in → Michigan  
Michigan → located in → United States  
Detroit → has team → Lions  
Lions → plays sport → Football  

**Choose → [[Neptune]]**

---

## Neptune Streams

[[Neptune Streams]] provides a **real-time ordered sequence of changes made to graph data**.

Think:

> **Change Data Capture for Neptune**

Architecture:

Application  
↓ write  
[[Neptune]]  
↓  
[[Neptune Streams]]  
↓  
Streams Reader Application  
↓  
Other Services

Possible destinations include:

- [[S3]]
- [[20-SAA/05-Databases/OpenSearch]]
- [[ElastiCache]]

### Neptune Streams Characteristics

- Records changes to graph data
- Changes are available immediately after writing
- Maintains strict ordering
- No duplicate records
- Stream data is accessible using an HTTP REST API

### Neptune Streams Use Cases

Use [[Neptune Streams]] when you need to:

- Send notifications when graph data changes
- Synchronize Neptune data with another datastore
- Synchronize data with [[S3]]
- Synchronize data with [[20-SAA/05-Databases/OpenSearch]]
- Synchronize data with [[ElastiCache]]
- Replicate Neptune data across Regions

> [!tip] Memory Trick
> **Neptune = relationships**
>
> **Neptune Streams = relationship changes**

---

## Architecture Thinking

### Scenario 1 — Social Network

A company needs to model millions of users and efficiently determine:

- Friends
- Followers
- Mutual connections
- Likes
- Shares

**Choose → [[Neptune]]**

Why?

The workload revolves around **relationships between entities**.

---

### Scenario 2 — Fraud Detection

A financial company needs to identify connections between:

- Customer accounts
- Transactions
- IP addresses
- Devices
- Payment methods

**Choose → [[Neptune]]**

Why?

The company needs to traverse complex relationships to uncover fraud patterns.

---

### Scenario 3 — Product Recommendations

An e-commerce application needs to determine products users may like based on relationships between:

Users → Products → Purchases → Reviews → Similar Users

**Choose → [[Neptune]]**

---

### Scenario 4 — Full-Text Search

A company needs full-text search across millions of documents.

**Choose → [[20-SAA/05-Databases/OpenSearch]]**

Not [[Neptune]].

The problem is **search**, not graph relationships.

---

### Scenario 5 — Massive Key-Value Workload

An application needs extremely fast lookups using a partition key at massive scale.

**Choose → [[04-Databases/DynamoDB]]**

Not [[Neptune]].

The problem is scalable **key-value/document access**, not graph traversal.

---

## Neptune vs Other Databases

| Requirement | Best Choice |
|---|---|
| Relational / SQL data | [[RDS]] / [[Aurora]] |
| Key-value / document NoSQL | [[04-Databases/DynamoDB]] |
| MongoDB-compatible document database | [[DocumentDB]] |
| In-memory caching | [[ElastiCache]] |
| Full-text search | [[20-SAA/05-Databases/OpenSearch]] |
| Graph relationships | **[[Neptune]]** |
| Data warehouse / OLAP | [[04-Databases/Redshift]] |

### Database Memory Map

SQL → [[RDS]] / [[Aurora]]  
Key-Value NoSQL → [[04-Databases/DynamoDB]]  
MongoDB → [[DocumentDB]]  
Cache → [[ElastiCache]]  
Search → [[20-SAA/05-Databases/OpenSearch]]  
Relationships → [[Neptune]]  
Analytics Warehouse → [[04-Databases/Redshift]]

---

## Scenario Recognition

### Exam Keywords

Immediately think **[[Neptune]]** when you see:

- Graph database
- Highly connected data
- Complex relationships
- Billions of relationships
- Social networking
- Friends / followers
- Knowledge graph
- Recommendation engine
- Fraud detection
- Relationship traversal

### Neptune Streams Keywords

Think **[[Neptune Streams]]** when you see:

- Changes to graph data
- Ordered sequence of changes
- No duplicates
- Synchronize Neptune with another datastore
- Notify an application when graph data changes
- Replicate Neptune changes across Regions

---

## Exam Traps

### Trap 1 — Neptune vs DynamoDB

Both are managed database services, but they solve very different problems.

**[[04-Databases/DynamoDB]]**
- Key-value/document database
- Massive scale
- Low-latency lookups

**[[Neptune]]**
- Graph database
- Highly connected data
- Relationship traversal

> **Key-value → DynamoDB**
>
> **Relationships → Neptune**

---

### Trap 2 — Neptune vs RDS/Aurora

Don't automatically choose a relational database just because the data contains entities with relationships.

Ask:

> Are complex relationships and traversing those relationships the **core workload**?

If yes:

**Choose → [[Neptune]]**

If the workload is traditional relational SQL transactions:

**Choose → [[RDS]] / [[Aurora]]**

---

### Trap 3 — Neptune vs OpenSearch

This is an easy exam trap.

**Search through text, documents, or logs → [[20-SAA/05-Databases/OpenSearch]]**

**Traverse connections and relationships → [[Neptune]]**

---

### Trap 4 — Recommendation Engine Does Not Automatically Mean Machine Learning

A recommendation scenario does **not automatically mean [[SageMaker]]**.

If the recommendation problem focuses on relationships between:

Users ↔ Products ↔ Purchases ↔ Interests

Then [[Neptune]] may be the intended solution.

Focus on **how the data is modeled**, not just the word "recommendation."

---

### Trap 5 — Forgetting Neptune Streams

If Neptune is already being used and the question asks how to capture an:

- Ordered sequence of graph changes
- Immediate record of graph updates
- Change stream without duplicates

Think:

**[[Neptune Streams]]**

Do not automatically choose [[20-SAA/10-Messaging/Kinesis Data Streams]].

---

## Quick Cheat Sheet

| Feature | Neptune |
|---|---|
| Database Type | Graph |
| Managed | Yes |
| Best For | Highly connected data |
| Scale | Billions of relationships |
| Query Performance | Millisecond latency |
| High Availability | Multiple AZs |
| Read Replicas | Up to 15 |
| Social Networks | ✅ |
| Fraud Detection | ✅ |
| Recommendation Engines | ✅ |
| Knowledge Graphs | ✅ |
| Change Tracking | [[Neptune Streams]] |

---

## Master Memory Trick

> [!tip] Master Memory Trick
> **Neptune = Navigate the Network**
>
> Neptune answers:
>
> **"How is everything connected?"**

Remember:

**[[RDS]] = Rows**

**[[04-Databases/DynamoDB]] = Keys**

**[[20-SAA/05-Databases/OpenSearch]] = Search**

**[[Neptune]] = Relationships**

**[[Neptune Streams]] = Relationship Changes**

---

## Related Notes

- [[RDS]]
- [[Aurora]]
- [[04-Databases/DynamoDB]]
- [[DocumentDB]]
- [[ElastiCache]]
- [[20-SAA/05-Databases/OpenSearch]]
- [[Neptune Streams]]
- [[04-Databases/Redshift]]
- [[Availability Zones]]
- [[S3]]
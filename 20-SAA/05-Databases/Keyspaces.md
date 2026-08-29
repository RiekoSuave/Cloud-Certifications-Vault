## What Problem Does It Solve?

[[Keyspaces]] is a **fully managed, serverless, Apache Cassandra-compatible NoSQL database service**.

It solves the problem of:

> **"How can I run Cassandra workloads without managing Cassandra clusters myself?"**

Instead of provisioning and maintaining your own Apache Cassandra infrastructure, [[Keyspaces]] manages the underlying database infrastructure for you.

Think:

**Apache Cassandra + AWS managed + Serverless = Keyspaces**

---

## What Is Apache Cassandra?

Apache Cassandra is an **open-source distributed NoSQL database** designed for highly scalable workloads.

[[Keyspaces]] provides an AWS-managed database that is **compatible with Apache Cassandra**.

This means applications designed around Cassandra can use familiar Cassandra concepts without requiring you to operate Cassandra clusters yourself.

> [!tip] Memory Trick
> **Keyspaces = Cassandra without managing Cassandra**
>
> If the exam says:
>
> **Apache Cassandra-compatible + managed/serverless**
>
> Think → [[Keyspaces]]

---

## Keyspaces Core Architecture

[[Keyspaces]] is:

- **Serverless**
- **Scalable**
- **Highly available**
- **Fully managed**
- Apache Cassandra-compatible
- Automatically scales based on application traffic

You don't manage the underlying database servers.

Conceptually:

Application  
↓  
Cassandra Query Language  
↓  
[[Keyspaces]]  
↓  
AWS-managed infrastructure

### Architecture Thinking

Your application focuses on:

**Tables + Queries + Data**

AWS handles the underlying infrastructure.

Think:

> **"I need Cassandra, but I don't want to operate Cassandra."**

**Choose → [[Keyspaces]]**

---

## Cassandra Query Language — CQL

[[Keyspaces]] uses:

**Cassandra Query Language (CQL)**

CQL is the query language used by Apache Cassandra.

### Exam Recognition

If a scenario specifically mentions:

- Apache Cassandra
- Cassandra-compatible database
- CQL
- Cassandra Query Language

[[Keyspaces]] should immediately be on your radar.

> [!tip] Memory Trick
> **CQL → Cassandra → Keyspaces**

---

## Automatic Scaling

[[Keyspaces]] can automatically scale tables **up or down based on application traffic**.

That means:

More Traffic  
↓  
Keyspaces scales capacity UP

Less Traffic  
↓  
Keyspaces scales capacity DOWN

This makes Keyspaces suitable for workloads where traffic can change over time without requiring you to manually manage database servers.

---

## High Availability

Keyspaces tables are replicated:

**3 times across multiple [[Availability Zones]]**

Conceptually:

Keyspaces Table  
↓  
├── Replica → AZ A  
├── Replica → AZ B  
└── Replica → AZ C  

This provides built-in high availability.

### Architecture Thinking

You do **not** need to manually build Cassandra replication across EC2 instances and Availability Zones.

Keyspaces manages the underlying replication.

---

## Performance

[[Keyspaces]] provides:

**Single-digit millisecond latency at any scale**

It can support:

**Thousands of requests per second**

This makes it suitable for applications requiring highly scalable, low-latency NoSQL access.

### Exam Keywords

Look for combinations such as:

- Cassandra
- Massive scale
- Low latency
- Single-digit milliseconds
- Thousands of requests per second

---

## Capacity Modes

[[Keyspaces]] supports two capacity approaches:

### On-Demand Mode

Use when traffic is:

- Unpredictable
- Variable
- Difficult to forecast

Think:

**Traffic unknown → On-Demand**

---

### Provisioned Mode

Use when workload requirements are more predictable.

Provisioned capacity can be combined with:

**Auto Scaling**

Think:

**Traffic predictable → Provisioned + Auto Scaling**

---

## Data Protection

[[Keyspaces]] supports:

- Encryption
- Backups
- [[Point-in-Time Recovery]]
- PITR for up to **35 days**

### Memory Trick

**Keyspaces protects Cassandra data with PITR up to 35 days.**

---

## Common Use Cases

The SAA slides specifically highlight:

### IoT Device Information

Example:

Millions of IoT devices continuously generate information.

IoT Devices  
↓  
Application  
↓  
[[Keyspaces]]

Keyspaces can scale as the number of devices and requests increases.

---

### Time-Series Data

Keyspaces can also store large amounts of:

**Time-series data**

Examples:

- Device readings
- Measurements
- Sensor information
- Events over time

However, be careful:

AWS also has a database specifically designed for time-series workloads:

[[04-Databases/Timestream]]

This creates an important exam distinction.

---

## Architecture Thinking

### Scenario 1 — Migrating Cassandra to AWS

A company currently operates an Apache Cassandra database.

They want to migrate to AWS while:

- Maintaining Cassandra compatibility
- Using CQL
- Eliminating database infrastructure management

**Choose → [[Keyspaces]]**

Why?

Keyspaces is specifically designed as a **managed Apache Cassandra-compatible database service**.

---

### Scenario 2 — Cassandra Without Servers

A development team wants to build an application using Cassandra APIs but doesn't want to:

- Provision servers
- Manage database nodes
- Scale Cassandra clusters manually

**Choose → [[Keyspaces]]**

Why?

Keyspaces is **serverless and fully managed**.

---

### Scenario 3 — Unpredictable Cassandra Traffic

A Cassandra-compatible application receives unpredictable traffic.

The company doesn't want to manually provision database capacity.

**Choose → [[Keyspaces]] with On-Demand capacity**

---

### Scenario 4 — Predictable Cassandra Workload

A Cassandra-compatible workload has relatively predictable traffic but needs the ability to scale when demand increases.

**Choose → [[Keyspaces]] with Provisioned capacity + Auto Scaling**

---

## Keyspaces vs DynamoDB

This is an important SAA distinction.

Both are scalable managed NoSQL databases.

### [[04-Databases/DynamoDB]]

AWS-native:

- Key-value/document NoSQL database
- Serverless
- Massive scale
- Single-digit millisecond performance

### [[Keyspaces]]

Designed specifically for:

- Apache Cassandra compatibility
- Cassandra workloads
- CQL

### Exam Decision

If the question says:

> **Apache Cassandra-compatible**

**Choose → [[Keyspaces]]**

If Cassandra compatibility isn't required and the application needs an AWS-native serverless NoSQL database:

Think → [[04-Databases/DynamoDB]]

> [!tip] Memory Trick
> **DynamoDB = AWS-native NoSQL**
>
> **Keyspaces = Cassandra NoSQL**

---

## Keyspaces vs Timestream

Both may appear in scenarios involving time-based data.

### [[Keyspaces]]

Can be used for:

- Cassandra workloads
- IoT device information
- Time-series data

### [[04-Databases/Timestream]]

Purpose-built specifically for:

**Time-series data**

### Exam Decision

If the scenario emphasizes:

**Apache Cassandra / CQL → [[Keyspaces]]**

If the scenario emphasizes:

**Purpose-built time-series database → [[04-Databases/Timestream]]**

---

## Scenario Recognition

### Exam Keywords

Immediately think **[[Keyspaces]]** when you see:

- Apache Cassandra
- Cassandra-compatible
- Cassandra migration
- CQL
- Cassandra Query Language
- Managed Cassandra
- Serverless Cassandra
- Cassandra without managing servers
- Automatically scaling Cassandra tables

### Strongest Keyword

The biggest clue is:

> **Cassandra**

On the SAA exam:

**Cassandra → Keyspaces**

---

## Exam Traps

### Trap 1 — Keyspaces vs DynamoDB

Both are scalable NoSQL databases.

Don't choose based only on:

**"NoSQL + massive scale."**

Look for Cassandra.

**Cassandra compatibility → [[Keyspaces]]**

**AWS-native key-value/document database → [[04-Databases/DynamoDB]]**

---

### Trap 2 — Keyspaces vs Self-Managed Cassandra on EC2

You could technically operate Cassandra yourself on [[EC2]].

But if the question emphasizes:

- Fully managed
- Serverless
- Minimal operational overhead
- Cassandra compatibility

**Choose → [[Keyspaces]]**

---

### Trap 3 — CQL vs SQL

CQL stands for:

**Cassandra Query Language**

Do not confuse it with traditional relational SQL databases such as [[RDS]] or [[Aurora]].

**CQL → Cassandra → Keyspaces**

---

### Trap 4 — Time-Series Automatically Means Timestream

The SAA slides specifically mention **time-series data** as a possible Keyspaces use case.

So don't choose based only on the phrase:

**time-series**

Look at the broader requirements.

**Cassandra / CQL + time-series → [[Keyspaces]]**

**Purpose-built time-series database → [[04-Databases/Timestream]]**

---

### Trap 5 — Manually Configuring Multi-AZ Replication

Keyspaces automatically replicates tables:

**3 times across multiple Availability Zones**

You don't need to manually build Cassandra replicas across AZs.

---

## Quick Cheat Sheet

| Feature | Keyspaces |
|---|---|
| Database Type | NoSQL |
| Compatibility | Apache Cassandra |
| Query Language | CQL |
| Infrastructure | Serverless |
| Management | Fully Managed |
| Scaling | Automatic |
| Availability | Multi-AZ |
| Replication | 3 replicas across multiple AZs |
| Latency | Single-digit milliseconds |
| Capacity | On-Demand or Provisioned |
| Auto Scaling | Supported |
| Encryption | Supported |
| Backups | Supported |
| PITR | Up to 35 days |
| IoT Data | ✅ |
| Time-Series Data | ✅ |

---

## Master Memory Trick

> [!tip] Master Memory Trick
> **Keyspaces = Cassandra's Space in AWS**
>
> Whenever you see:
>
> **Cassandra**
>
> Think:
>
> **[[Keyspaces]]**

Remember the database map:

**SQL → [[RDS]] / [[Aurora]]**

**Key-Value NoSQL → [[04-Databases/DynamoDB]]**

**MongoDB → [[DocumentDB]]**

**Graph → [[Neptune]]**

**Search → [[20-SAA/05-Databases/OpenSearch]]**

**Cassandra → [[Keyspaces]]**

**Time-Series → [[04-Databases/Timestream]]**

---

## Related Notes

- [[04-Databases/DynamoDB]]
- [[DocumentDB]]
- [[Neptune]]
- [[Neptune Streams]]
- [[04-Databases/Timestream]]
- [[RDS]]
- [[Aurora]]
- [[EC2]]
- [[Availability Zones]]
- [[Point-in-Time Recovery]]
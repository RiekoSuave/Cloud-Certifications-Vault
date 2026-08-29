## What Problem Does It Solve?

[[MSK]] is AWS's fully managed service for:

**Apache Kafka**

It is designed for applications that need:

- High-throughput event streaming
- Kafka-compatible producers and consumers
- Durable event pipelines
- Existing Kafka applications migrated to AWS
- Multiple independent consumers
- Ordered event streams

Architecture:

Producers  
↓  
MSK  
↓  
Kafka Topics  
↓  
Consumers

> [!tip] Memory Trick
> **MSK = Managed Kafka**

---

## Core Concept

With MSK, AWS manages much of the Kafka infrastructure, including:

- Broker provisioning
- Broker replacement
- Patching
- Cluster monitoring
- Availability

You still work with familiar Kafka concepts such as:

- Brokers
- Topics
- Partitions
- Producers
- Consumers

### Killer Exam Clue

> **Need Apache Kafka on AWS without managing the Kafka cluster yourself**
>
> → **MSK**

---

# Kafka Topics

A:

**Topic**

is a named stream of records.

Example:

`orders`

`payments`

`clickstream`

Architecture:

Producer  
↓  
Topic  
↓  
Consumers

Think:

**Topic = Category of Events**

---

# Partitions

Kafka topics are divided into:

**Partitions**

Partitions provide:

- Parallelism
- Scalability
- Ordering within a partition

### Memory Trick

**Partition = Scale + Order**

---

# Ordering

Kafka preserves ordering:

**Within a partition**

It does not guarantee one global order across:

**All partitions**

### Killer Exam Clue

> **Need ordered Kafka processing for related records**
>
> → Route related records to the same partition.

---

# Producers

Kafka:

**Producers**

send records into:

**Topics**

Architecture:

Producer  
↓  
Kafka Topic

---

# Consumers

Kafka:

**Consumers**

read records from:

**Topics**

Multiple consumers can process:

**The same topic**

depending on consumer-group design.

---

# Consumer Groups

A:

**Consumer Group**

lets multiple consumers share:

**The work of processing topic partitions**

Example:

Topic  
↓  
Consumer Group A  
├── Consumer 1
└── Consumer 2

Each partition is assigned to:

**One consumer within the group at a time**

### Memory Trick

**Same Group = Share the Work**

---

# Multiple Consumer Groups

Different consumer groups can independently read:

**The same topic**

Example:

Orders Topic  
↓  
├── Fraud Consumer Group
├── Analytics Consumer Group
└── Shipping Consumer Group

Each group receives:

**Its own logical view of the stream**

### Killer Exam Clue

> **Multiple independent applications need to consume the same Kafka data**
>
> → **Separate Consumer Groups**

---

# Brokers

Kafka runs on:

**Brokers**

A broker stores and serves:

**Topic partitions**

MSK manages the broker infrastructure for you.

### Memory Trick

**Broker = Kafka Server**

---

# High Availability

MSK can distribute brokers across:

**Multiple Availability Zones**

This improves:

- Availability
- Fault tolerance
- Resilience

### Killer Exam Clue

> **Need highly available managed Kafka on AWS**
>
> → **MSK across multiple AZs**

---

# Replication

Kafka partitions can have:

**Replicas**

This protects against:

**Broker failure**

### Memory Trick

**Replica = Copy of Partition Data**

---

# MSK Provisioned

With:

**MSK Provisioned**

you choose and manage more of:

- Broker sizing
- Broker count
- Storage
- Cluster capacity

Think:

**More control**

---

# MSK Serverless

MSK also provides:

**MSK Serverless**

This lets you run Kafka workloads with less cluster-capacity management.

AWS handles more of:

- Capacity
- Scaling
- Infrastructure

### Killer Exam Clue

> **Need Kafka compatibility without managing broker capacity**
>
> → **MSK Serverless**

---

# Provisioned vs Serverless

| Requirement | MSK Provisioned | MSK Serverless |
|---|---:|---:|
| Kafka Compatibility | ✅ | ✅ |
| Broker Sizing Control | ✅ | Less |
| Capacity Management | More | Less |
| Minimal Ops | ❌ | ✅ |
| Predictable Dedicated Design | ✅ | ✅ |

### Memory Trick

**Provisioned = Control**

**Serverless = Simplicity**

---

# MSK Connect

**MSK Connect**

helps run:

**Kafka Connect connectors**

for moving data between Kafka and:

**Other systems**

Examples can include:

- S3
- Databases
- Search systems

### Killer Exam Clue

> **Need managed Kafka Connect on AWS**
>
> → **MSK Connect**

---

# MSK + S3

A common pattern:

Kafka Producers  
↓  
MSK  
↓  
Connector / Consumer  
↓  
[[S3]]

Use for:

- Long-term archival
- Data lakes
- Analytics

---

# MSK + Lambda

[[Lambda]] can consume from:

**MSK**

through an event-source integration.

Architecture:

MSK  
↓  
Lambda Event Source Mapping  
↓  
Lambda

### Killer Exam Clue

> **Need serverless processing of Kafka records**
>
> → **MSK + Lambda**

---

# MSK + Glue

Kafka data can be processed through analytics and ETL architectures that include:

[[Glue]]

Use Glue when the requirement is:

**ETL / transformation**

rather than Kafka ingestion itself.

---

# MSK + OpenSearch

A common pattern:

MSK  
↓  
Connector / Consumer  
↓  
[[OpenSearch]]

Use when Kafka events need to become:

**Searchable / analyzable**

---

# MSK + Redshift

Kafka event streams can eventually feed:

[[Redshift]]

for:

**Warehouse analytics**

MSK handles:

**Streaming transport**

Redshift handles:

**OLAP**

---

# MSK vs Kinesis Data Streams

This is the biggest exam comparison.

## [[Kinesis Data Streams]]

Think:

- AWS-native streaming
- Shards
- Partition keys
- Managed service
- AWS integrations
- Replay

## MSK

Think:

- Apache Kafka
- Topics
- Partitions
- Consumer groups
- Kafka ecosystem
- Kafka compatibility

### Killer Shortcut

**Need Kafka compatibility**
→ MSK

**Need AWS-native streaming**
→ Kinesis Data Streams

---

# Migration Scenario

A company currently runs:

**Apache Kafka on EC2**

and wants to:

- Reduce operational overhead
- Keep existing Kafka producers/consumers
- Avoid rewriting applications

Choose:

**MSK**

### Killer Exam Clue

> **Migrate existing Kafka workload to AWS with minimal application change**
>
> → **MSK**

---

# MSK vs SQS

## [[SQS]]

Think:

- Work queue
- Decoupling
- Worker backlog
- Simpler messaging

## MSK

Think:

- Event streaming
- Replay
- Multiple independent consumer groups
- Kafka ecosystem

### Killer Shortcut

**Worker queue**
→ SQS

**Kafka event stream**
→ MSK

---

# MSK vs SNS

## [[SNS]]

Think:

**Push fan-out**

## MSK

Think:

**Durable Kafka stream**

Use SNS when:

**Simple pub/sub delivery**

is enough.

Use MSK when:

**Kafka semantics and streaming architecture**

are required.

---

# MSK vs EventBridge

## [[20-SAA/10-Messaging/EventBridge]]

Think:

- Business event routing
- Rules
- AWS/SaaS integration

## MSK

Think:

- High-throughput Kafka streaming
- Topic/partition model
- Kafka consumers

### Memory Trick

**EventBridge = Route**

**MSK = Stream**

---

# MSK vs Firehose

## [[Kinesis Data Firehose]]

Think:

**Managed delivery to destinations**

## MSK

Think:

**Kafka streaming platform**

Firehose is not a replacement for:

**A Kafka cluster**

---

# MSK vs Self-Managed Kafka

## Self-Managed Kafka

You manage:

- Brokers
- Patching
- Failures
- Scaling
- Monitoring

## MSK

AWS manages much of:

**The Kafka infrastructure**

### Killer Exam Clue

> **Reduce Kafka operational burden**
>
> → **MSK**

---

# Security

MSK supports security mechanisms involving:

- IAM-based access where supported
- TLS
- Encryption at rest
- VPC networking
- Authentication options

For SAA, remember:

> **MSK clusters are commonly deployed privately inside a VPC**

---

# Encryption in Transit

Kafka client connections can use:

**TLS**

to encrypt:

**Data in transit**

---

# Encryption at Rest

MSK supports encryption at rest using:

**KMS-backed encryption**

This protects:

**Stored Kafka data**

---

# VPC Networking

MSK clusters operate inside:

**A VPC**

Applications typically connect through:

**Private networking**

### Killer Exam Clue

> **Need private managed Kafka inside AWS networking**
>
> → **MSK**

---

# IAM and Client Access

Client applications require appropriate:

**Authentication and authorization**

to connect and interact with:

**Kafka topics**

Use:

**Least privilege**

---

# Monitoring

MSK integrates with:

[[07-Monitoring/CloudWatch]]

for monitoring items such as:

- Broker health
- Throughput
- Storage
- Consumer lag
- Cluster metrics

---

# Consumer Lag

A major operational metric is:

**Consumer Lag**

It indicates:

**How far consumers are behind producers**

### Killer Exam Clue

> **Kafka consumers cannot keep up with incoming records**
>
> → Check **Consumer Lag**

---

# Architecture Thinking

## Scenario 1 — Existing Kafka Platform

Company already uses:

- Kafka producers
- Kafka consumers
- Kafka libraries

Wants managed AWS infrastructure.

Choose:

**MSK**

---

## Scenario 2 — AWS-Native New Stream

New application has no Kafka requirement.

Needs:

- Real-time streaming
- AWS-native integration
- Replay

Think:

**Kinesis Data Streams**

---

## Scenario 3 — Kafka Without Broker Management

Team wants Kafka API compatibility but does not want to manage:

**Broker sizing**

Choose:

**MSK Serverless**

---

## Scenario 4 — Kafka Connector

Need to move Kafka records into:

S3

using Kafka Connect.

Choose:

**MSK Connect**

---

## Scenario 5 — Lambda Consumer

Kafka topic needs:

**Serverless event processing**

Choose:

MSK  
↓  
Lambda

---

## Scenario 6 — Independent Consumers

Fraud, analytics, and billing all need:

**The same Kafka events**

Create:

**Separate consumer groups**

---

## Scenario 7 — Consumer Falling Behind

Producer traffic grows.

Consumers process too slowly.

Monitor:

**Consumer Lag**

and scale:

**Consumer processing capacity**

---

# Scenario Recognition

Immediately think:

**MSK**

when you see:

- Apache Kafka
- Kafka topics
- Kafka partitions
- Kafka consumer groups
- Existing Kafka workload
- Kafka migration
- Managed Kafka

---

## Think MSK Connect When You See

- Kafka Connect
- Managed connector
- Move Kafka data into external systems

---

## Think MSK Serverless When You See

- Kafka without broker management
- Variable Kafka workload
- Minimal infrastructure administration

---

## Think Kinesis Data Streams When You See

- AWS-native streaming
- Shards
- Partition keys
- No Kafka requirement

---

# Exam Traps

## Trap 1 — MSK Is Just Another Name for Kinesis Data Streams

❌

MSK:

**Apache Kafka**

Kinesis:

**AWS-native streaming**

---

## Trap 2 — MSK Uses Shards as Its Main Kafka Concept

❌

Kafka uses:

**Topics + Partitions**

---

## Trap 3 — Multiple Consumers Must Always Share the Same Work

❌

Separate consumer groups can independently consume:

**The same topic**

---

## Trap 4 — MSK Is a Work Queue Like SQS

❌

It is:

**A streaming platform**

---

## Trap 5 — MSK Connect Is the Kafka Broker

❌

MSK Connect runs:

**Kafka Connect connectors**

---

## Trap 6 — Existing Kafka Applications Must Be Rewritten for Kinesis

Not if you choose:

**MSK**

when Kafka compatibility is the requirement.

---

# Quick Cheat Sheet

| Exam Clue | Answer |
|---|---|
| Managed Apache Kafka | MSK |
| Kafka Topic | Event Stream |
| Kafka Parallelism | Partitions |
| Independent Kafka Consumers | Consumer Groups |
| Kafka Without Broker Management | MSK Serverless |
| Managed Kafka Connect | MSK Connect |
| Kafka → Lambda | MSK + Lambda |
| Existing Kafka Migration | MSK |
| AWS-Native Streaming | Kinesis Data Streams |
| Worker Queue | SQS |
| Kafka Consumer Falling Behind | Consumer Lag |

---

# MSK vs Kinesis

| Requirement | MSK | Kinesis Data Streams |
|---|---:|---:|
| Apache Kafka Compatibility | ✅ | ❌ |
| Topics / Partitions | ✅ | ❌ |
| Consumer Groups | ✅ | Different Model |
| AWS-Native Shards | ❌ | ✅ |
| Replay | ✅ | ✅ |
| Multiple Consumers | ✅ | ✅ |
| Existing Kafka Apps | ✅ Best | Rewrite Usually Needed |

---

# Messaging Decision

Need:

**Kafka compatibility**

→ MSK

Need:

**AWS-native real-time stream**

→ Kinesis Data Streams

Need:

**Worker queue**

→ SQS

Need:

**Simple fan-out**

→ SNS

Need:

**Business event routing**

→ EventBridge

---

# Final Exam Rapid-Fire

> **APACHE KAFKA**
> → MSK
>
> **KAFKA TOPIC**
> → EVENT STREAM
>
> **KAFKA PARTITION**
> → SCALE + ORDER
>
> **INDEPENDENT CONSUMERS**
> → CONSUMER GROUPS
>
> **MANAGED KAFKA CONNECT**
> → MSK CONNECT
>
> **NO BROKER CAPACITY MANAGEMENT**
> → MSK SERVERLESS
>
> **KAFKA → LAMBDA**
> → MSK EVENT SOURCE
>
> **EXISTING KAFKA MIGRATION**
> → MSK
>
> **AWS-NATIVE STREAM**
> → KINESIS DATA STREAMS
>
> **WORK QUEUE**
> → SQS
>
> **CONSUMER BEHIND**
> → CONSUMER LAG

---

## Master Memory Trick

> [!tip] MSK Master Memory Trick
> Imagine a company already runs:
>
> **A huge Kafka railway system**
>
> Events travel through:
>
> **TOPICS**
>
> The railway splits into:
>
> **PARTITIONS**
>
> Producers load events onto trains:
>
> **PRODUCERS**
>
> Consumers unload them:
>
> **CONSUMERS**
>
> Multiple departments want the same trains:
>
> **CONSUMER GROUPS**
>
> The company says:
>
> **"We want to keep Kafka, but we don't want to maintain all the railway infrastructure."**
>
> That's:
>
> **MSK**

So remember:

> **MSK**
> → MANAGED KAFKA
>
> **TOPIC**
> → EVENT STREAM
>
> **PARTITION**
> → SCALE + ORDER
>
> **CONSUMER GROUP**
> → INDEPENDENT PROCESSING GROUP
>
> **MSK CONNECT**
> → CONNECT KAFKA TO OTHER SYSTEMS
>
> **MSK SERVERLESS**
> → LESS BROKER MANAGEMENT
>
> **KINESIS**
> → AWS-NATIVE STREAMING

And the killer SAA question:

> **"Does the company specifically need Apache Kafka compatibility?"**
>
> YES
>
> → **MSK**

---

## Related Notes

- [[Kinesis Data Streams]]
- [[Kinesis Data Firehose]]
- [[Lambda]]
- [[S3]]
- [[OpenSearch]]
- [[Redshift]]
- [[07-Monitoring/CloudWatch]]
- [[06-Security/KMS]]
- [[SQS]]
- [[SNS]]
- [[20-SAA/10-Messaging/EventBridge]]
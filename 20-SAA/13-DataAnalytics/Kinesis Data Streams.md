## What Problem Does It Solve?

[[Kinesis Data Streams]] is AWS's:

**Real-time data streaming service**

It is designed for continuously ingesting and processing:

- Application events
- Clickstreams
- IoT telemetry
- Logs
- Financial transactions
- Metrics
- Real-time records

Architecture:

Producers  
↓  
Kinesis Data Streams  
↓  
Consumers

> [!tip] Memory Trick
> **Kinesis Data Streams = Real-time event pipe**
>
> Think:
>
> **PRODUCERS → STREAM → CONSUMERS**

---

## Core Concept

Kinesis Data Streams lets applications send:

**Streaming records**

into a durable stream that can be consumed by:

**Multiple applications**

Example:

Website Events  
↓  
Kinesis Data Streams  
↓  
├── Lambda
├── Analytics Consumer
└── Storage Pipeline

### Killer Exam Clue

> **Need to ingest high-volume streaming data in real time**
>
> → **Kinesis Data Streams**

---

# Producers

A:

**Producer**

writes records into:

**Kinesis Data Streams**

Examples:

- Applications
- Servers
- IoT devices
- SDK-based producers
- Kinesis Producer Library

Architecture:

Producer  
↓  
PutRecord / PutRecords  
↓  
Kinesis

---

# Consumers

A:

**Consumer**

reads records from the stream.

Examples:

- [[Lambda]]
- Applications using Kinesis Client Library
- Managed analytics services
- Firehose-style downstream delivery architectures

### Memory Trick

**Producer = Writes**

**Consumer = Reads**

---

# Shards

A Kinesis Data Stream is divided into:

**Shards**

A shard is the basic:

**Throughput and capacity unit**

Architecture:

Stream  
↓  
├── Shard 1
├── Shard 2
└── Shard 3

### Killer Exam Concept

> **More shards = more stream throughput**

---

## Shard Capacity

Each shard has its own:

**Read and write throughput limits**

For SAA, the exact numbers are less important than understanding:

> **Shard count controls stream capacity**

---

# Partition Key

Each record includes a:

**Partition Key**

Kinesis hashes the partition key to determine:

**Which shard receives the record**

Architecture:

Record + Partition Key  
↓  
Hash  
↓  
Shard

### Memory Trick

**Partition Key = Which shard?**

---

# Ordering

Kinesis preserves record ordering:

**Within a shard**

More specifically, records with the same partition key are routed consistently and can preserve:

**Order within that shard path**

### Killer Exam Clue

> **Need ordered processing for related streaming records**
>
> → Use a consistent **partition key**

---

# Good Partition Key Design

A good partition key distributes traffic:

**Evenly across shards**

Examples:

- UserId
- DeviceId
- CustomerId

Poor choice:

`Country = USA`

if nearly all traffic is:

**USA**

This can create:

**Hot shards**

---

# Hot Shard

A:

**Hot Shard**

occurs when too much traffic is directed toward:

**One shard**

because partition-key distribution is uneven.

Symptoms:

- Throttling
- Uneven throughput
- Some shards overloaded
- Other shards underused

### Memory Trick

**Bad Partition Key = Hot Shard**

---

# Stream Retention

Kinesis Data Streams retains records for:

**A configurable retention period**

This allows consumers to:

- Read later
- Replay data
- Recover from temporary consumer failure

### Killer Exam Clue

> **Need to replay recent streaming data**
>
> → **Kinesis Data Streams**

---

# Replay

Because records remain in the stream during retention:

Consumers can:

**Re-read records**

This is very different from:

**A simple one-time notification**

### Memory Trick

**Kinesis = Stream + Replay**

---

# Multiple Consumers

Multiple consumers can read from:

**The same stream**

Architecture:

Kinesis Stream  
↓  
├── Fraud Detection
├── Analytics
├── Monitoring
└── Data Lake Pipeline

Each consumer can process:

**The same events independently**

---

# Real-Time Processing

Kinesis is designed for:

**Near-real-time streaming**

Example:

Financial Transaction  
↓  
Kinesis  
↓  
Fraud Detection Consumer  
↓  
Alert

The consumer can respond:

**Seconds after the event occurs**

---

# Kinesis + Lambda

A very important architecture:

Producer  
↓  
Kinesis Data Streams  
↓  
Lambda Event Source Mapping  
↓  
Lambda

Lambda:

**Polls Kinesis shards**

and receives:

**Batches of records**

### Killer Exam Clue

> **Process Kinesis records with serverless compute**
>
> → **Kinesis + Lambda**

---

# Event Source Mapping

Kinesis does NOT simply push each record directly into Lambda.

Instead:

Lambda uses:

**Event Source Mapping**

Architecture:

Kinesis Shard  
↓  
Lambda Polling  
↓  
Batch  
↓  
Lambda Function

### Memory Trick

**Kinesis → Lambda = Poll + Batch**

---

# Ordered Lambda Processing

Because Kinesis preserves ordering within a shard:

Lambda processing must respect:

**Shard ordering**

A failed record can delay:

**Later records in the same shard**

### Killer Exam Concept

> **Poison record in an ordered stream can block records behind it**

---

# Bisect Batch on Function Error

For Lambda processing Kinesis:

You can use:

**Bisect Batch on Function Error**

A failed batch can be:

**Split into smaller batches**

until the problematic records are easier to isolate.

### Memory Trick

**BISECT = Split the failed batch**

---

# Maximum Record Age

Lambda event source mapping can limit:

**How old a stream record may become**

before processing is abandoned.

Use when:

**Old poison records should stop blocking processing**

---

# Maximum Retry Attempts

You can also control:

**How many times failed stream records are retried**

This helps avoid:

**Infinite retry behavior**

---

# Parallelization Factor

Lambda can process multiple batches from:

**The same shard**

in parallel using:

**Parallelization Factor**

This increases:

**Consumer throughput**

while maintaining ordering where required for:

**Partition-key groups**

### Killer Exam Clue

> **Need more Lambda processing parallelism per Kinesis shard**
>
> → **Parallelization Factor**

---

# Standard Consumers

Traditional Kinesis consumers share:

**Shard read throughput**

among consumers.

As more consumers are added:

They compete for:

**Available shard read capacity**

---

# Enhanced Fan-Out

**Enhanced Fan-Out**

gives each registered consumer:

**Dedicated read throughput per shard**

Architecture:

Kinesis Shard  
↓  
├── Consumer A Dedicated Throughput
├── Consumer B Dedicated Throughput
└── Consumer C Dedicated Throughput

### Killer Exam Clue

> **Multiple Kinesis consumers need dedicated low-latency read throughput**
>
> → **Enhanced Fan-Out**

---

# Standard vs Enhanced Fan-Out

## Standard Consumer

Consumers share:

**Shard read throughput**

## Enhanced Fan-Out

Each registered consumer gets:

**Dedicated throughput**

### Memory Trick

**STANDARD = SHARE**

**ENHANCED = DEDICATED**

---

# Kinesis Client Library

The:

**Kinesis Client Library — KCL**

helps applications:

**Consume records from Kinesis streams**

It handles concerns such as:

- Shard discovery
- Load balancing
- Checkpointing
- Worker coordination

### Exam Concept

> **Build a custom scalable Kinesis consumer**
>
> → **KCL**

---

# Checkpointing

Consumers need to remember:

**Which records have already been processed**

KCL uses:

**Checkpointing**

to track progress through:

**Shards**

### Memory Trick

**Checkpoint = Where consumer stopped**

---

# Kinesis Producer Library

The:

**Kinesis Producer Library — KPL**

helps producers efficiently send:

**Large volumes of records**

It can improve:

- Throughput
- Batching
- Aggregation

### Memory Trick

**KPL = Write efficiently**

**KCL = Read efficiently**

---

# Record Aggregation

KPL can combine multiple logical records into:

**Larger Kinesis records**

This helps improve:

**Write efficiency**

and reduce:

**API overhead**

---

# Provisioned Mode

Kinesis Data Streams can use:

**Provisioned capacity**

where you choose:

**The number of shards**

Use when:

- Traffic is predictable
- Capacity needs are understood
- You want direct shard control

---

# On-Demand Mode

Kinesis Data Streams can also use:

**On-Demand capacity mode**

AWS automatically manages stream capacity based on:

**Traffic**

### Killer Exam Clue

> **Streaming workload is unpredictable and team does not want to manage shard capacity**
>
> → **Kinesis On-Demand**

---

# Provisioned vs On-Demand

| Requirement | Provisioned | On-Demand |
|---|---:|---:|
| Manage Shard Capacity | ✅ | ❌ |
| Predictable Workload | ✅ | ✅ |
| Unpredictable Workload | Possible | ✅ |
| Minimal Capacity Planning | ❌ | ✅ |
| Direct Shard Control | ✅ | Less |

### Memory Trick

**Provisioned = Plan Shards**

**On-Demand = AWS Handles Capacity**

---

# Resharding

In provisioned mode, stream capacity can be adjusted by:

**Changing shard count**

Conceptually:

More Demand  
↓  
More Shards

Less Demand  
↓  
Fewer Shards

This is commonly called:

**Resharding**

---

# Split and Merge

Traditional shard scaling concepts include:

- Splitting shards
- Merging shards

For SAA, remember:

> **Shard count can be adjusted to change throughput capacity**

---

# Kinesis Data Streams vs SQS

This is a major exam comparison.

## Kinesis Data Streams

Think:

- Streaming
- Ordered within shard
- Multiple consumers
- Replay
- Retention
- Real-time analytics

## [[SQS]]

Think:

- Queue
- Decoupling
- Work distribution
- Message backlog
- Consumer processing

### Killer Shortcut

**Stream of events + replay**
→ Kinesis

**Queue of work**
→ SQS

---

# Kinesis vs SNS

## [[SNS]]

Think:

**Push notifications / fan-out**

## Kinesis

Think:

**Durable event stream**

Kinesis retains records for:

**Replay**

SNS is primarily designed for:

**Delivery to subscribers**

### Memory Trick

**SNS = Send**

**Kinesis = Stream**

---

# Kinesis vs EventBridge

## [[20-SAA/10-Messaging/EventBridge]]

Think:

- Event bus
- Rule-based routing
- AWS/SaaS events

## Kinesis

Think:

- High-volume streaming
- Ordered shards
- Replay
- Continuous ingestion

### Killer Shortcut

**Route business events**
→ EventBridge

**Process huge continuous event stream**
→ Kinesis Data Streams

---

# Kinesis vs Firehose

Do not confuse:

**Streaming platform**

with:

**Delivery service**

## Kinesis Data Streams

Provides:

- Stream
- Shards
- Consumers
- Replay
- Custom processing

## Kinesis Data Firehose

Focuses on:

**Delivering streaming data to destinations**

with less custom consumer management.

### Memory Trick

**Data Streams = Process the Stream**

**Firehose = Deliver the Stream**

---

# Kinesis + S3

One common architecture:

Producers  
↓  
Kinesis Data Streams  
↓  
Consumer / Delivery Pipeline  
↓  
[[S3]]

This can create:

**A streaming data lake ingestion pipeline**

---

# Kinesis + Redshift

Streaming data can eventually be delivered or ingested into:

[[Redshift]]

for:

**Analytics**

Architecture:

Events  
↓  
Kinesis  
↓  
Analytics Pipeline  
↓  
Redshift

---

# Kinesis + OpenSearch

Streaming records can be used to populate:

**OpenSearch**

for near-real-time:

- Search
- Log analytics
- Dashboards

---

# Kinesis + Analytics Processing

A stream can feed:

**Real-time analytics applications**

Examples:

- Fraud detection
- Clickstream analysis
- IoT monitoring
- Operational dashboards

---

# Data Streams vs Batch

Kinesis is best for:

**Continuous event flow**

Not:

**Occasional static batch files**

For batch files in S3:

Think:

- Athena
- Glue
- EMR

depending on processing requirements.

---

# Kinesis Durability

Records are retained across:

**Multiple Availability Zones**

within a Region.

This provides:

**Highly available stream storage**

for the configured retention period.

---

# Encryption

Kinesis Data Streams supports:

**Encryption at rest**

using:

[[06-Security/KMS]]

This helps protect:

**Stream records**

---

# Encryption in Transit

Applications interact with Kinesis using:

**HTTPS**

providing:

**Encryption in transit**

---

# IAM

Kinesis uses:

**IAM**

for access control.

Examples:

Producer Role  
→ PutRecord

Consumer Role  
→ GetRecords

### SAA Principle

> **Use least privilege for producers and consumers**

---

# Kinesis VPC Endpoints

Applications in a VPC can access Kinesis through:

**VPC endpoints**

to avoid requiring traffic to traverse:

**Public Internet paths**

### Killer Exam Clue

> **Privately access Kinesis from a VPC**
>
> → **VPC Endpoint**

---

# Monitoring

Kinesis integrates with:

[[07-Monitoring/CloudWatch]]

for metrics such as:

- Incoming records
- Incoming bytes
- Read throughput
- Write throughput
- Throttling
- Iterator age

---

# Iterator Age

A key consumer-health metric is:

**Iterator Age**

It indicates how far:

**A consumer is falling behind**

Conceptually:

Newest Record  
↓  
Consumer is processing much older record  
↓  
Iterator Age increases

### Killer Exam Clue

> **Kinesis consumer is falling behind the stream**
>
> → Check **Iterator Age**

---

# Consumer Lag

If incoming data arrives faster than a consumer processes it:

Consumer falls:

**Behind**

Possible fixes:

- Increase consumer capacity
- Increase shard capacity
- Increase Lambda parallelization
- Optimize processing
- Use Enhanced Fan-Out where appropriate

---

# Architecture Thinking

## Scenario 1 — Clickstream

Website produces:

Millions of click events

Need:

- Real-time ingestion
- Multiple consumers
- Replay

Choose:

**Kinesis Data Streams**

---

## Scenario 2 — Ordered Device Events

Events from each IoT device must be processed:

**In order**

Use:

`DeviceId`

as:

**Partition Key**

---

## Scenario 3 — Multiple Consumers

Fraud detection, analytics, and archival all read:

**The same stream**

and each needs dedicated throughput.

Choose:

**Enhanced Fan-Out**

---

## Scenario 4 — Unpredictable Traffic

Streaming traffic varies dramatically.

Team does not want to manage:

**Shard count**

Choose:

**On-Demand Mode**

---

## Scenario 5 — Predictable High Volume

Company knows its expected throughput and wants:

**Explicit shard control**

Choose:

**Provisioned Mode**

---

## Scenario 6 — Lambda Processing

Need serverless processing of:

Kinesis records.

Choose:

Kinesis  
↓  
Lambda Event Source Mapping

---

## Scenario 7 — Poison Record

One record repeatedly causes Lambda failure and blocks:

**Later records in shard**

Consider:

- Bisect Batch
- Maximum Retry Attempts
- Maximum Record Age

---

## Scenario 8 — Consumer Falling Behind

CloudWatch shows:

**High Iterator Age**

Meaning:

Consumer cannot keep up.

Increase:

**Consumer processing capacity**

or optimize:

**Shard/consumer architecture**

---

## Scenario 9 — Need Work Queue

Messages should be processed by workers and removed after success.

No need for replay or multiple stream consumers.

Choose:

**SQS**

rather than Kinesis.

---

## Scenario 10 — Need Simple Delivery to S3

No custom stream processing is required.

Need managed delivery to:

**S3**

Think:

**Kinesis Data Firehose**

rather than Data Streams.

---

# Scenario Recognition

Immediately think:

**Kinesis Data Streams**

when you see:

- Real-time streaming
- Continuous event ingestion
- Shards
- Partition keys
- Ordered records
- Multiple consumers
- Replay
- Streaming logs
- Clickstreams
- IoT telemetry

---

## Think Enhanced Fan-Out When You See

- Multiple consumers
- Dedicated read throughput
- Low-latency consumer access

---

## Think On-Demand When You See

- Unpredictable stream traffic
- No shard management
- Variable throughput

---

## Think SQS When You See

- Queue
- Worker backlog
- Decoupling
- Remove after processing

---

## Think Firehose When You See

- Managed delivery
- S3 destination
- Redshift destination
- OpenSearch destination
- Minimal consumer management

---

# Exam Traps

## Trap 1 — Kinesis Data Streams Is Just a Queue

❌

It is a:

**Durable streaming platform**

with:

- Replay
- Multiple consumers
- Shards

---

## Trap 2 — Ordering Is Guaranteed Across the Entire Stream

❌

Ordering is preserved:

**Within a shard**

---

## Trap 3 — Partition Key Has Nothing to Do With Shard Selection

❌

Partition key determines:

**Shard placement**

through hashing.

---

## Trap 4 — More Consumers Always Get More Read Throughput Automatically

❌

Standard consumers share:

**Shard read throughput**

Use:

**Enhanced Fan-Out**

for dedicated throughput.

---

## Trap 5 — Kinesis Pushes Records Directly to Lambda One by One

❌

Lambda uses:

**Event Source Mapping**

and processes:

**Batches**

---

## Trap 6 — Kinesis Records Disappear Immediately After One Consumer Reads Them

❌

Records remain for:

**The retention period**

and can be replayed.

---

## Trap 7 — On-Demand Still Requires Manual Shard Planning

❌

AWS manages:

**Capacity**

---

## Trap 8 — Kinesis Data Streams Is Best for Simple Managed S3 Delivery

❌

Think:

**Data Firehose**

if the main requirement is:

**Delivery**

---

# Quick Cheat Sheet

| Exam Clue | Answer |
|---|---|
| Real-Time Data Stream | Kinesis Data Streams |
| Stream Capacity Unit | Shard |
| Determine Shard | Partition Key |
| Ordering | Within Shard |
| Replay Events | Kinesis Data Streams |
| Serverless Stream Consumer | Lambda |
| Lambda Integration | Event Source Mapping |
| Dedicated Consumer Throughput | Enhanced Fan-Out |
| Consumer Falling Behind | Iterator Age |
| Unpredictable Throughput | On-Demand |
| Manual Capacity Control | Provisioned |
| Queue Work | SQS |
| Managed Destination Delivery | Firehose |

---

# Producer / Consumer Cheat Sheet

| Component | Think |
|---|---|
| Producer | WRITE |
| Stream | HOLD / ORDER / RETAIN |
| Consumer | READ |
| KPL | PRODUCE EFFICIENTLY |
| KCL | CONSUME EFFICIENTLY |
| Partition Key | CHOOSE SHARD |
| Shard | CAPACITY |

---

# Streaming Decision

Need:

**Replay + multiple consumers + ordered shards**

→ Kinesis Data Streams

Need:

**Simple queue**

→ SQS

Need:

**Broadcast notification**

→ SNS

Need:

**Rule-based event routing**

→ EventBridge

Need:

**Managed streaming delivery to destination**

→ Firehose

---

# Final Exam Rapid-Fire

> **REAL-TIME STREAM**
> → KINESIS DATA STREAMS
>
> **CAPACITY UNIT**
> → SHARD
>
> **SHARD SELECTION**
> → PARTITION KEY
>
> **ORDERING**
> → WITHIN SHARD
>
> **REPLAY**
> → KINESIS
>
> **LAMBDA CONSUMER**
> → EVENT SOURCE MAPPING
>
> **DEDICATED CONSUMER THROUGHPUT**
> → ENHANCED FAN-OUT
>
> **CONSUMER LAG**
> → ITERATOR AGE
>
> **UNPREDICTABLE STREAM**
> → ON-DEMAND
>
> **EXPLICIT SHARD CONTROL**
> → PROVISIONED
>
> **QUEUE**
> → SQS
>
> **DELIVERY SERVICE**
> → FIREHOSE

---

## Master Memory Trick

> [!tip] Kinesis Data Streams Master Memory Trick
> Imagine a river.
>
> Producers pour water into:
>
> **THE STREAM**
>
> The river is divided into:
>
> **SHARDS**
>
> A record's:
>
> **PARTITION KEY**
>
> decides which channel it enters.
>
> Water in each channel flows:
>
> **IN ORDER**
>
> Multiple teams can stand downstream and read:
>
> **THE SAME STREAM**
>
> And because the water is retained for a while:
>
> they can:
>
> **REPLAY RECENT EVENTS**
>
> If each team needs its own dedicated pipe:
>
> **ENHANCED FAN-OUT**

So remember:

> **KINESIS**
> → STREAM
>
> **SHARD**
> → CAPACITY
>
> **PARTITION KEY**
> → ROUTE TO SHARD
>
> **ORDER**
> → WITHIN SHARD
>
> **RETENTION**
> → REPLAY
>
> **ENHANCED FAN-OUT**
> → DEDICATED CONSUMER THROUGHPUT
>
> **ITERATOR AGE**
> → CONSUMER LAG

And the killer SAA question:

> **"Does the application need a durable real-time stream with ordered records, multiple consumers, and replay?"**
>
> YES
>
> → **Kinesis Data Streams**

---

## Related Notes

- [[Lambda]]
- [[Lambda Event Source Mapping]]
- [[SQS]]
- [[SNS]]
- [[20-SAA/10-Messaging/EventBridge]]
- [[20-SAA/10-Messaging/Kinesis Data Firehose]]
- [[S3]]
- [[Redshift]]
- [[EMR]]
- [[07-Monitoring/CloudWatch]]
- [[06-Security/KMS]]
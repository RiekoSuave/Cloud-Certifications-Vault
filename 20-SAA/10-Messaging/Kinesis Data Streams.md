## What Problem Does It Solve?

[[20-SAA/10-Messaging/Kinesis Data Streams]] is designed for:

**Collecting and processing streaming data in real time**

It solves the problem:

> **"How can I continuously ingest large amounts of real-time data and let multiple consumers process that stream?"**

Think:

Producers  
↓  
Kinesis Data Streams  
↓  
Real-Time Consumers

Common producers include:

- Applications
- Clickstreams
- IoT devices
- Metrics
- Logs

Common consumers include:

- [[02-Compute/Lambda]]
- Applications
- Kinesis Data Firehose
- Managed Service for Apache Flink

> [!tip] Memory Trick
> **Kinesis = Data moving like a river**
>
> Continuous data flows in.
>
> Consumers process it in real time.

---

## Streaming Model

Kinesis Data Streams uses a:

**Streaming model**

Unlike [[SQS]], records are not simply removed after one consumer processes them.

Instead:

Producer  
↓  
Kinesis Stream  
↓  
Stored Records  
↓  
Multiple Consumers

Consumers can independently:

**Read the same stream**

This makes Kinesis useful when:

**Multiple systems need to analyze the same real-time data**

---

## Core Architecture

Architecture:

Applications  
↓  
Kinesis Data Streams  
↓  
├── Consumer A
├── Consumer B
├── Lambda
└── Firehose

Data enters continuously through:

**Producers**

and is read continuously by:

**Consumers**

---

## Producers

Producers send records into:

[[20-SAA/10-Messaging/Kinesis Data Streams]]

Examples:

- Web applications
- Mobile applications
- IoT devices
- Servers
- Logging systems
- Monitoring agents

### Typical Data

Think:

- Click events
- Transactions
- Metrics
- Logs
- Sensor readings
- Application events

---

## Consumers

Consumers read records from the stream.

Examples include:

- Custom applications
- [[02-Compute/Lambda]]
- Kinesis Data Firehose
- Managed Service for Apache Flink

A consumer might:

- Analyze
- Transform
- Aggregate
- Store
- Trigger downstream processing

---

## Real-Time Processing

One of the strongest Kinesis clues is:

**Real-Time**

Example:

Website Clicks  
↓  
Kinesis  
↓  
Real-Time Analytics

or:

IoT Sensors  
↓  
Kinesis  
↓  
Anomaly Detection

or:

Application Logs  
↓  
Kinesis  
↓  
Security Monitoring

### Exam Pattern

> **Continuous high-volume data + real-time processing**
>
> → **Kinesis Data Streams**

---

## Data Retention

Kinesis Data Streams keeps records for:

**A configurable retention period**

The Maarek slides highlight retention of:

**Up to 365 days**

This is fundamentally different from SQS.

Records remain available during:

**The retention window**

even after a consumer reads them.

---

## Why Retention Matters

Because records remain in the stream:

Consumers can:

- Process later
- Recover after failure
- Re-read old records
- Replay data

This is one of Kinesis's biggest advantages.

> [!tip] Memory Trick
> **SQS = Process and delete**
>
> **Kinesis = Read and replay**

---

## Replay

Kinesis consumers can:

**Reprocess previously stored records**

during the retention period.

Architecture:

Kinesis Records  
↓  
Consumer Processes  
↓  
Bug Found  
↓  
Fix Consumer  
↓  
Replay Old Records

### Killer Exam Clue

> **Need to replay previously processed streaming data**
>
> → **Kinesis Data Streams**

---

## Records Are Not Deleted by Consumers

A consumer reading a Kinesis record does NOT:

**Delete that record**

The record remains until:

**Its retention period expires**

This allows:

**Multiple consumers**

to independently process the same data.

---

## Kinesis vs SQS Deletion Model

### [[SQS]]

Message  
↓  
Consumer Processes  
↓  
DeleteMessage  
↓  
Message Gone

---

### Kinesis

Record  
↓  
Consumer Reads  
↓  
Record Remains  
↓  
Other Consumers Can Read  
↓  
Expires After Retention Period

### Memory Trick

**SQS = Take the ticket**

**Kinesis = Read the newspaper**

Many people can read:

**The same edition**

---

## Record Size

The Maarek slides highlight records up to:

**10 MiB**

with Kinesis typically being used for:

**Large numbers of relatively small real-time records**

Examples:

- Click events
- Log entries
- Metrics
- Sensor readings

---

## Partition Key

Kinesis uses a:

**Partition Key**

to determine where records are placed.

The partition key is crucial for:

- Distribution
- Ordering
- Scaling

Conceptually:

Record  
↓  
Partition Key  
↓  
Kinesis Partition / Shard

---

## Ordering

Kinesis provides:

**Ordering for records with the same partition key**

Example:

Partition Key:

`Customer-100`

Records:

Event 1  
↓  
Event 2  
↓  
Event 3

Kinesis preserves their order for:

**That partition key**

> [!tip] Memory Trick
> **Same Partition Key = Same Ordered Lane**

---

## Ordering Is Not Global

Do NOT assume all records across the entire stream are:

**Globally ordered**

Ordering is associated with:

**The same partition key**

Different partition keys may be processed independently.

---

## Example — Customer Events

Suppose:

Customer A  
→ Partition Key A

Customer B  
→ Partition Key B

Customer A events stay ordered relative to:

**Customer A**

Customer B events stay ordered relative to:

**Customer B**

But there is no requirement for:

A1  
B1  
A2  
B2

to maintain a single global order.

---

## Shards

Kinesis Data Streams historically scales using:

**Shards**

A shard provides capacity for:

- Writes
- Reads

Partition keys determine:

**Which shard receives a record**

Conceptually:

Producer  
↓  
Partition Key  
↓  
Shard  
↓  
Consumer

---

## Why Shards Matter

More shards can provide:

**More throughput**

Think:

1 Shard  
→ Lower capacity

Multiple Shards  
→ Higher capacity

For SAA, the important architectural concept is:

> **Shards are units of stream capacity.**

---

## Hot Partition / Hot Shard

If producers use:

**The same partition key too often**

too much traffic may be directed toward:

**The same shard**

This can create:

**A hot shard**

### Example

Bad:

Partition Key = `ALL-USERS`

for every event

Result:

Everything routed toward:

**The same partition path**

Better:

Use partition keys with:

**Good distribution**

such as:

- User ID
- Device ID
- Customer ID

depending on ordering requirements.

---

## Partition Key Tradeoff

The partition key determines both:

**Ordering**

and:

**Distribution**

This creates an architectural tradeoff.

Need all events globally ordered?

→ Less parallelism

Need high scalability?

→ Distribute records across multiple keys

### SAA Principle

> **Choose a partition key that preserves the ordering you need while distributing traffic effectively.**

---

## Kinesis Producer Library

The Maarek slides highlight:

**Kinesis Producer Library — KPL**

KPL helps developers build:

**Optimized producer applications**

Think:

Producer Application  
↓  
KPL  
↓  
Kinesis Data Streams

### Memory Trick

**KPL = Producer**

---

## Kinesis Client Library

The Maarek slides also highlight:

**Kinesis Client Library — KCL**

KCL helps developers build:

**Optimized consumer applications**

Think:

Kinesis Data Streams  
↓  
KCL  
↓  
Consumer Application

### Memory Trick

**KCL = Consumer**

---

## KPL vs KCL

| Library | Purpose |
|---|---|
| KPL | Optimized Producer |
| KCL | Optimized Consumer |

> [!tip] Memory Trick
> **P = Producer**
>
> **C = Consumer**

---

## Encryption in Transit

Kinesis supports:

**HTTPS**

for encryption:

**In transit**

This protects data while being sent:

To / From the stream.

---

## Encryption at Rest

Kinesis supports:

[[06-Security/KMS]]

for:

**Encryption at rest**

### Exam Pattern

> **Encrypt streaming records stored in Kinesis**
>
> → **KMS**

---

## Kinesis + Lambda

[[02-Compute/Lambda]] can consume:

Kinesis Data Streams

Architecture:

Producer  
↓  
Kinesis  
↓  
Lambda

This creates:

**Serverless real-time stream processing**

### Example

IoT Device  
↓  
Kinesis  
↓  
Lambda  
↓  
Detect Anomaly

---

## Lambda and Ordered Processing

When Lambda consumes Kinesis records:

Ordering is maintained according to:

**The stream's partitioning model**

This makes Kinesis useful for:

**Ordered per-key event processing**

---

## Kinesis + Firehose

Kinesis Data Streams can feed:

**Kinesis Data Firehose**

Architecture:

Producers  
↓  
Kinesis Data Streams  
↓  
Firehose  
↓  
Destination

This lets Kinesis act as the:

**Real-time ingestion layer**

while Firehose provides:

**Managed delivery**

---

## Kinesis + S3

A common architecture:

Applications  
↓  
Kinesis Data Streams  
↓  
Firehose  
↓  
[[S3]]

Use when you want:

- Real-time ingestion
- Stream consumers
- Long-term storage in S3

---

## Kinesis + Apache Flink

Managed Service for Apache Flink can process:

**Kinesis streaming data**

for:

- Real-time analytics
- Stateful stream processing
- Aggregations
- Transformations

Conceptually:

Kinesis  
↓  
Flink  
↓  
Real-Time Analytics

---

## Kinesis vs SQS

This is one of the most important exam comparisons.

### [[SQS]]

Think:

- Queue
- Decoupling
- Work distribution
- Consumers compete
- Message deleted after processing
- Limited replay behavior

---

### Kinesis

Think:

- Stream
- Real-time data
- Multiple consumers
- Records retained
- Replay
- Ordered by partition key

### Memory Trick

**SQS = WORK QUEUE**

**Kinesis = DATA STREAM**

---

## Consumer Behavior: SQS vs Kinesis

### SQS

Multiple consumers:

**Compete for work**

One message typically goes to:

**One consumer**

---

### Kinesis

Multiple consumers can:

**Read the same records independently**

This allows:

- Analytics
- Monitoring
- Archival
- Fraud detection

to all process:

**The same stream**

---

## Kinesis vs SNS

### [[SNS]]

Think:

- Pub/Sub
- Push
- Fan-Out
- Notifications
- No stream replay model

---

### Kinesis

Think:

- Streaming
- Retention
- Replay
- Ordered records
- Real-time analytics

### Exam Shortcut

**Broadcast event now**
→ SNS

**Continuously process/replay event stream**
→ Kinesis

---

## Kinesis vs SNS + SQS

SNS + SQS provides:

**Durable fan-out**

Kinesis provides:

**A retained stream**

### SNS + SQS

Best for:

- Independent queues
- Message retries
- Work processing
- Fan-out

### Kinesis

Best for:

- Continuous streaming
- Replay
- Ordered data
- Real-time analytics

---

## Kinesis vs SQS FIFO

Both can maintain:

**Ordering**

but they solve different problems.

### [[SQS FIFO]]

Think:

- Ordered work queue
- Deduplication
- Process and delete
- One logical consumer path per message

---

### Kinesis

Think:

- Ordered stream
- Replay
- Multiple consumers
- Retention

### Exam Shortcut

**Ordered tasks**
→ SQS FIFO

**Ordered replayable stream**
→ Kinesis

---

## Kinesis vs EventBridge

### Kinesis

Think:

**High-volume real-time data stream**

---

### [[20-SAA/10-Messaging/EventBridge]]

Think:

**Event routing**

based on:

- Rules
- Event sources
- Event patterns
- Targets

### Exam Shortcut

**Process continuous telemetry**
→ Kinesis

**Route business events**
→ EventBridge

---

## Kinesis vs Firehose

These are often confused.

### Kinesis Data Streams

Think:

- Stream storage
- Multiple consumers
- Custom consumers
- Replay
- Ordering
- Real-time processing

---

### Kinesis Data Firehose

Think:

**Managed delivery**

to destinations such as:

- S3
- Redshift
- OpenSearch
- Other supported destinations

### Memory Trick

**Streams = PROCESS**

**Firehose = DELIVER**

---

## Architecture Thinking

### Scenario 1 — Clickstream Analytics

A website produces millions of:

**Click events**

The business needs:

**Real-time analytics**

**Choose → Kinesis Data Streams**

---

### Scenario 2 — IoT Sensors

Thousands of devices continuously send:

**Sensor readings**

Multiple applications must analyze the data.

**Choose → Kinesis Data Streams**

---

### Scenario 3 — Replay After Consumer Bug

A consumer processed records incorrectly.

The team fixes the code and wants to:

**Reprocess old records**

**Choose → Kinesis Data Streams**

because retained records can be:

**Replayed**

---

### Scenario 4 — One Job Per Worker

A batch-processing system needs each job processed by:

**One worker**

Replay is unnecessary.

Think:

[[SQS]]

instead of Kinesis.

---

### Scenario 5 — Strict Ordered Work Queue

Financial operations must be:

- Strictly ordered
- Deduplicated
- Processed as tasks

Think:

[[SQS FIFO]]

rather than Kinesis if the requirement is fundamentally:

**A work queue**

---

### Scenario 6 — Multiple Real-Time Consumers

The same streaming data must be consumed by:

- Fraud Detection
- Analytics
- Monitoring

and each needs independent access.

**Choose → Kinesis Data Streams**

---

### Scenario 7 — Stream to S3

Real-time records need:

- Stream processing
- Long-term storage

Architecture:

Kinesis Data Streams  
↓  
Firehose  
↓  
S3

---

### Scenario 8 — Route AWS Events

A company needs to route:

- EC2 state changes
- SaaS events
- CloudTrail events

based on:

**Rules**

Think:

[[20-SAA/10-Messaging/EventBridge]]

not Kinesis.

---

## Scenario Recognition

Immediately think:

[[20-SAA/10-Messaging/Kinesis Data Streams]]

when you see:

- Real-time
- Streaming
- Clickstream
- IoT
- Metrics
- Logs
- Telemetry
- Multiple consumers
- Replay
- Retention
- Partition key
- Ordered records
- Shards

### Strongest Exam Pattern

> **"Continuously ingest high-volume real-time data that multiple consumers must process independently, with the ability to replay records."**
>
> → **Kinesis Data Streams**

---

## Exam Traps

### Trap 1 — Kinesis Is Just Another Work Queue

False.

Kinesis is:

**A retained data stream**

For normal work distribution:

[[SQS]]

---

### Trap 2 — Reading a Record Deletes It

False.

Records remain until:

**Retention expires**

---

### Trap 3 — Only One Consumer Can Read a Record

False.

Multiple consumers can independently read:

**The same stream**

---

### Trap 4 — Kinesis Guarantees Global Ordering

False.

Ordering is tied to:

**The same partition key**

---

### Trap 5 — Partition Key Only Controls Scaling

False.

It affects:

- Distribution
- Ordering

---

### Trap 6 — One Partition Key Is Always Best

False.

Using one key can create:

**A hot partition / shard**

and limit parallelism.

---

### Trap 7 — Kinesis Data Streams and Firehose Are the Same

False.

Streams:

**Retain + process + replay**

Firehose:

**Managed delivery**

---

### Trap 8 — Kinesis Is Better Than SNS for Simple Notifications

Not usually.

Simple one-to-many notifications:

→ [[SNS]]

Real-time retained streaming:

→ Kinesis

---

### Trap 9 — SQS FIFO and Kinesis Are Interchangeable

False.

SQS FIFO:

**Ordered work queue**

Kinesis:

**Ordered replayable stream**

---

## Quick Cheat Sheet

| Exam Clue | Answer |
|---|---|
| Real-Time Streaming | Kinesis Data Streams |
| Clickstream | Kinesis |
| IoT Data | Kinesis |
| Metrics / Logs | Kinesis |
| Multiple Independent Consumers | Kinesis |
| Replay Records | Kinesis |
| Retained Stream | Kinesis |
| Ordered by Key | Partition Key |
| Stream Capacity Unit | Shard |
| Optimized Producer Library | KPL |
| Optimized Consumer Library | KCL |
| Encryption at Rest | KMS |
| Work Queue | SQS |
| Ordered Work Queue | SQS FIFO |
| Pub/Sub Broadcast | SNS |
| Managed Destination Delivery | Firehose |
| Advanced Event Routing | EventBridge |

---

## Messaging Comparison

| Requirement | Best Choice |
|---|---|
| Decouple Workers | SQS |
| Ordered Work Queue | SQS FIFO |
| Broadcast / Fan-Out | SNS |
| Ordered Fan-Out | SNS FIFO |
| Real-Time Stream | Kinesis Data Streams |
| Replay Events | Kinesis |
| Deliver Stream to Destination | Firehose |
| Advanced Event Routing | EventBridge |

---

## Master Memory Trick

> [!tip] Kinesis Master Memory Trick
> Imagine a river.
>
> Producers throw records into:
>
> **THE RIVER**
>
> ↓
>
> Kinesis keeps them flowing for:
>
> **A RETENTION PERIOD**
>
> ↓
>
> Multiple consumers stand downstream and:
>
> **READ THE SAME WATER**
>
> One consumer does analytics.
>
> One checks fraud.
>
> One stores results.
>
> If one consumer breaks:
>
> **GO BACK UPSTREAM AND REPLAY**

So remember:

> **KINESIS = STREAM**
>
> **RETENTION = REPLAY**
>
> **PARTITION KEY = ORDER + DISTRIBUTION**
>
> **SHARDS = CAPACITY**
>
> **KPL = PRODUCER**
>
> **KCL = CONSUMER**

And the killer comparison:

> **SQS**
> → Work Queue
>
> **SNS**
> → Broadcast
>
> **Kinesis**
> → Real-Time Replayable Stream
>
> **EventBridge**
> → Event Router

---

## Related Notes

- [[SQS]]
- [[SQS FIFO]]
- [[SNS]]
- [[SNS FIFO]]
- [[20-SAA/10-Messaging/Kinesis Data Firehose]]
- [[20-SAA/10-Messaging/EventBridge]]
- [[02-Compute/Lambda]]
- [[S3]]
- [[06-Security/KMS]]
## Why This Comparison Matters

AWS SAA questions often place several messaging services in the same answer set:

- [[SQS]]
- [[SQS FIFO]]
- [[SNS]]
- [[SNS FIFO]]
- [[20-SAA/10-Messaging/Kinesis Data Streams]]
- [[20-SAA/10-Messaging/Kinesis Data Firehose]]
- [[20-SAA/10-Messaging/EventBridge]]

The exam is usually testing:

> **"Is this a queue, broadcast, stream, delivery pipeline, or event router?"**

> [!tip] Master Decision
> **WAIT → SQS**
>
> **ORDERED WAIT → SQS FIFO**
>
> **BROADCAST → SNS**
>
> **ORDERED BROADCAST → SNS FIFO**
>
> **STREAM → Kinesis Data Streams**
>
> **DELIVER STREAM → Kinesis Data Firehose**
>
> **ROUTE EVENTS → EventBridge**

---

## Start With the Communication Pattern

Ask:

1. Does work need to wait in a queue?
2. Does one message need to reach many receivers?
3. Is this continuous real-time streaming data?
4. Does streaming data simply need to land somewhere?
5. Do events need rule-based routing?

Those five questions eliminate most wrong answers quickly.

---

# SQS

[[SQS]] is a:

**Managed message queue**

Primary purpose:

**Decouple producers and consumers**

Architecture:

Producer  
↓  
SQS Queue  
↓  
Consumer

Think:

- Queue
- Buffer
- Async processing
- Traffic spikes
- Backpressure
- Worker fleet
- Consumer polling

### Killer Exam Clue

> **Work must wait safely until a consumer is ready**
>
> → **SQS**

### Memory Trick

**SQS = WAIT**

---

## SQS Standard

Think:

- Very high throughput
- At-least-once delivery
- Best-effort ordering
- Duplicate messages possible

Best for:

**Independent work items where strict ordering is unnecessary**

---

# SQS FIFO

[[SQS FIFO]]

adds:

- Strict ordering within a message group
- Deduplication
- MessageGroupId
- MessageDeduplicationId

Think:

**Ordered work queue**

### Killer Exam Clue

> **Tasks must be processed in order and duplicates must be prevented**
>
> → **SQS FIFO**

### Memory Trick

**SQS FIFO = ORDERED WAIT**

---

# SQS Standard vs FIFO

| Requirement | Standard | FIFO |
|---|---:|---:|
| Queue | ✅ | ✅ |
| Very High Throughput | ✅ | More Controlled |
| Strict Ordering | ❌ | ✅ |
| Deduplication | ❌ | ✅ |
| Message Groups | ❌ | ✅ |
| Independent Jobs | ✅ | ✅ |
| Sequence-Sensitive Jobs | ❌ | ✅ |

---

# SNS

[[SNS]] is a:

**Publish / Subscribe service**

Primary purpose:

**One message → many subscribers**

Architecture:

Publisher  
↓  
SNS Topic  
↓  
├── Subscriber A
├── Subscriber B
└── Subscriber C

Think:

- Pub/Sub
- Push
- Fan-Out
- Notifications
- Broadcast

### Killer Exam Clue

> **One event must be delivered to many receivers**
>
> → **SNS**

### Memory Trick

**SNS = BROADCAST**

---

# SNS + SQS Fan-Out

This is one of the most important architectures in the section.

Producer  
↓  
SNS  
↓  
├── SQS Queue A
├── SQS Queue B
└── SQS Queue C

SNS provides:

**Copies**

SQS provides:

**Durability + buffering**

### Memory Trick

**SNS COPIES**

**SQS HOLDS**

Use when:

> **Multiple independent systems must reliably process the same event**

---

# SNS FIFO

[[SNS FIFO]]

adds:

- Ordering
- Deduplication
- MessageGroupId
- FIFO fan-out

Think:

**Ordered Pub/Sub**

### Killer Exam Clue

> **Multiple subscribers need the same events in order**
>
> → **SNS FIFO**

For durable ordered fan-out:

SNS FIFO  
↓  
Multiple SQS FIFO Queues

### Memory Trick

**SNS FIFO = ORDERED BROADCAST**

---

# SNS Message Filtering

[[SNS Message Filtering]]

lets each subscription receive:

**Only matching messages**

Example:

SNS Topic  
↓  
├── Placed Orders Queue
├── Cancelled Orders Queue
└── Declined Orders Queue

Each subscription can have:

**Its own filter policy**

### Killer Exam Clue

> **Same SNS topic, but different subscribers need different subsets**
>
> → **SNS Filter Policy**

### Important Rule

**No filter policy**
→ Receive all messages

---

# SQS vs SNS

This is the single most important messaging comparison.

## SQS

Question:

> **Where should the work wait?**

Think:

**Queue**

Consumers:

**Poll / Pull**

---

## SNS

Question:

> **Who should receive this event?**

Think:

**Broadcast**

Subscribers:

**Receive pushed notifications**

---

## SQS vs SNS Quick Comparison

| Requirement | SQS | SNS |
|---|---:|---:|
| Queue | ✅ | ❌ |
| Pub/Sub | ❌ | ✅ |
| Consumer Pulls | ✅ | ❌ |
| Push to Subscribers | ❌ | ✅ |
| Buffer Work | ✅ | ❌ |
| One → Many | Not Alone | ✅ |
| Backpressure | ✅ | ❌ |
| Fan-Out | ❌ | ✅ |

### Memory Trick

**SQS = LINE**

**SNS = LOUDSPEAKER**

---

# Kinesis Data Streams

[[20-SAA/10-Messaging/Kinesis Data Streams]] is for:

**Real-time streaming data**

Think:

- Clickstreams
- IoT
- Logs
- Metrics
- Telemetry
- Multiple consumers
- Retention
- Replay
- Ordered records by partition key

Architecture:

Producers  
↓  
Kinesis Data Streams  
↓  
Multiple Consumers

### Killer Exam Clue

> **Continuous real-time data that multiple consumers must process and potentially replay**
>
> → **Kinesis Data Streams**

### Memory Trick

**Kinesis = STREAM**

---

# Kinesis Data Streams Retention

Unlike SQS:

Consumers do NOT delete records after reading them.

Records remain available during:

**The retention period**

This allows:

- Multiple consumers
- Replay
- Reprocessing

### Memory Trick

**SQS = Consume + Delete**

**Kinesis = Read + Retain**

---

# Kinesis Ordering

Ordering is guaranteed for records using:

**The same partition key**

Think:

Customer A  
→ Partition A  
→ Ordered

Customer B  
→ Partition B  
→ Ordered

Do NOT assume:

**Global ordering across the entire stream**

---

# Kinesis Data Firehose

[[20-SAA/10-Messaging/Kinesis Data Firehose]] is for:

**Managed delivery of streaming data**

Think:

Stream  
↓  
Firehose  
↓  
Destination

Common destinations include:

- [[S3]]
- Redshift
- OpenSearch
- Supported external destinations

### Killer Exam Clue

> **Continuously deliver streaming data to S3 with minimal management**
>
> → **Kinesis Data Firehose**

### Memory Trick

**Firehose = DELIVER**

---

# Data Streams vs Firehose

This is a major exam distinction.

## Kinesis Data Streams

Think:

- Process
- Retain
- Replay
- Multiple consumers
- Custom consumers
- Ordered stream

---

## Firehose

Think:

- Deliver
- Buffer
- Batch
- Transform
- Land data in destination

### Memory Trick

**Streams = PROCESS**

**Firehose = DELIVER**

---

# Data Streams vs Firehose Quick Comparison

| Requirement | Data Streams | Firehose |
|---|---:|---:|
| Real-Time Stream | ✅ | Near Real-Time Delivery |
| Multiple Consumers | ✅ | Not Primary Purpose |
| Retention | ✅ | No Stream-Retention Model |
| Replay | ✅ | ❌ |
| Custom Consumers | ✅ | ❌ |
| Destination Delivery | Integration Needed | ✅ |
| Buffer / Batch | Not Primary Purpose | ✅ |
| Transform Before Delivery | Consumer Logic | Lambda Integration |
| Shards / Stream Capacity | Relevant | Managed |

---

# EventBridge

[[20-SAA/10-Messaging/EventBridge]] is a:

**Serverless event bus**

Primary purpose:

**Route events based on rules**

Architecture:

Event Source  
↓  
Event Bus  
↓  
Rule  
↓  
Target

Think:

- Event patterns
- AWS service events
- Custom application events
- SaaS events
- Rules
- Targets
- Archive
- Replay
- Schema Registry

### Killer Exam Clue

> **Route events to different targets based on event content**
>
> → **EventBridge**

### Memory Trick

**EventBridge = ROUTE**

---

# EventBridge Buses

| Event Bus | Source |
|---|---|
| Default | AWS Services |
| Partner | SaaS Partners |
| Custom | Your Applications |

### Memory Trick

**AWS → DEFAULT**

**SaaS → PARTNER**

**YOUR APP → CUSTOM**

---

# EventBridge + SQS

A very common combined architecture:

Event  
↓  
EventBridge  
↓  
Rule  
↓  
SQS  
↓  
Consumer

EventBridge:

**Routes**

SQS:

**Buffers**

### Memory Trick

**ROUTE → HOLD**

---

# EventBridge + SNS

Architecture:

Event  
↓  
EventBridge  
↓  
SNS  
↓  
Subscribers

EventBridge:

**Selects the event**

SNS:

**Broadcasts it**

### Memory Trick

**ROUTE → BROADCAST**

---

# SNS vs EventBridge

Both can distribute events.

The difference is:

## SNS

Think:

**Simple Pub/Sub**

One topic  
↓  
Subscribers

Best for:

- Fan-Out
- Notifications
- Push messaging

---

## EventBridge

Think:

**Event Routing**

Event bus  
↓  
Rules  
↓  
Targets

Best for:

- AWS events
- SaaS events
- Custom app events
- Complex routing
- Archive
- Replay

### Exam Shortcut

**Simple broadcast**
→ SNS

**Rule-based event routing**
→ EventBridge

---

# SNS Filtering vs EventBridge

Both can:

**Filter**

but they do it in different architectures.

## SNS Filtering

Question:

> Which subscribers should receive this topic message?

---

## EventBridge

Question:

> Where should this event be routed?

### Memory Trick

**SNS Filter = Select subscribers**

**EventBridge = Route events**

---

# Kinesis vs EventBridge

## Kinesis

Think:

**Continuous data**

Examples:

- Telemetry
- Clickstreams
- IoT
- Logs

---

## EventBridge

Think:

**Discrete business / operational events**

Examples:

- EC2 stopped
- Order created
- Build failed
- API call occurred

### Exam Shortcut

**Continuous stream**
→ Kinesis

**Something happened**
→ EventBridge

---

# SQS vs Kinesis

## SQS

Think:

**Work distribution**

Message normally processed by:

**One consumer path**

---

## Kinesis

Think:

**Shared retained stream**

Multiple consumers can read:

**The same records**

### Exam Shortcut

**Jobs**
→ SQS

**Telemetry**
→ Kinesis

---

# SQS FIFO vs Kinesis

Both can preserve ordering.

## SQS FIFO

Think:

- Ordered tasks
- Deduplication
- Queue semantics
- Process and delete

---

## Kinesis

Think:

- Ordered streaming data
- Retention
- Replay
- Multiple consumers

### Memory Trick

**Ordered WORK**
→ SQS FIFO

**Ordered STREAM**
→ Kinesis

---

# SNS FIFO vs Kinesis

Both can deliver ordered information.

## SNS FIFO

Think:

**Ordered fan-out**

---

## Kinesis

Think:

**Ordered retained stream**

### Exam Shortcut

**Ordered broadcast**
→ SNS FIFO

**Ordered replayable stream**
→ Kinesis

---

# Firehose vs SQS

## SQS

Purpose:

**Queue work**

---

## Firehose

Purpose:

**Deliver streaming data to a destination**

### Exam Shortcut

Worker backlog  
→ SQS

Logs continuously landing in S3  
→ Firehose

---

# Firehose vs EventBridge

## Firehose

Question:

> **Where should this stream land?**

## EventBridge

Question:

> **Where should this event go?**

### Memory Trick

**Firehose = DESTINATION**

**EventBridge = ROUTING**

---

# Architecture Thinking

## Scenario 1 — Web Tier Decoupling

A front-end receives requests faster than the backend can process them.

Need:

- Buffer
- Async work
- Backpressure protection

**Choose → SQS**

---

## Scenario 2 — Financial Queue

Transactions must be:

- Ordered
- Deduplicated

**Choose → SQS FIFO**

---

## Scenario 3 — Order Fan-Out

One order event must reach:

- Shipping
- Billing
- Fraud

**Choose → SNS**

For durable independent processing:

**SNS + multiple SQS queues**

---

## Scenario 4 — Ordered Fan-Out

Fraud and accounting both require:

**The same ordered financial events**

**Choose → SNS FIFO + SQS FIFO**

---

## Scenario 5 — Selective Fan-Out

One SNS topic contains:

- Placed
- Cancelled
- Declined

Each queue only needs one state.

**Choose → SNS Subscription Filter Policies**

---

## Scenario 6 — IoT Streaming

Millions of sensors continuously send readings.

Multiple consumers need:

- Real-time processing
- Independent consumption
- Replay

**Choose → Kinesis Data Streams**

---

## Scenario 7 — Logs to S3

Application logs continuously arrive and should automatically land in:

[[S3]]

with minimal administration.

**Choose → Kinesis Data Firehose**

---

## Scenario 8 — EC2 State Automation

When an EC2 instance enters:

**Stopped**

a Lambda function should run.

**Choose → EventBridge + Lambda**

---

## Scenario 9 — API Security Event

Security needs an alert whenever:

`DeleteTable`

is called.

Choose:

CloudTrail  
↓  
EventBridge  
↓  
SNS

---

## Scenario 10 — Consumer Backlog

Workers are offline temporarily.

Messages must remain available until they return.

**Choose → SQS**

---

## Scenario 11 — Replay Streaming Data

A bug requires yesterday's telemetry records to be:

**Reprocessed**

**Choose → Kinesis Data Streams**

---

## Scenario 12 — Replay Business Events

Archived business events need to be rerun through routing rules.

**Choose → EventBridge Archive + Replay**

---

# Scenario Recognition

Immediately think:

## [[SQS]]

when you see:

- Queue
- Buffer
- Backpressure
- Poll
- Worker
- Decouple
- Traffic spike

---

## [[SQS FIFO]]

when you see:

- Queue + strict ordering
- Deduplication
- Sequence-sensitive work

---

## [[SNS]]

when you see:

- Pub/Sub
- Broadcast
- Fan-Out
- Push
- One-to-many

---

## [[SNS FIFO]]

when you see:

- Ordered fan-out
- Fan-Out + deduplication

---

## [[20-SAA/10-Messaging/Kinesis Data Streams]]

when you see:

- Real-time streaming
- Replay
- Retention
- Multiple stream consumers
- Partition key
- Clickstream
- IoT

---

## [[20-SAA/10-Messaging/Kinesis Data Firehose]]

when you see:

- Deliver stream
- S3 destination
- Redshift
- OpenSearch
- Managed delivery
- Buffering

---

## [[20-SAA/10-Messaging/EventBridge]]

when you see:

- Event bus
- Rule
- Event pattern
- AWS events
- SaaS events
- Custom events
- Archive / replay
- Event routing

---

# Biggest Exam Traps

## Trap 1 — SNS and SQS Are Interchangeable

False.

SNS:

**Broadcast**

SQS:

**Queue**

---

## Trap 2 — One SQS Queue Gives Every Application a Copy

False.

Consumers:

**Compete**

Need every app to receive a copy?

→ SNS + multiple SQS queues

---

## Trap 3 — SQS Is for Streaming Analytics

False.

Think:

[[20-SAA/10-Messaging/Kinesis Data Streams]]

---

## Trap 4 — Kinesis Deletes Records After Processing

False.

Records remain until:

**Retention expires**

---

## Trap 5 — Firehose Is Replayable Like Data Streams

False.

Need replay?

→ Data Streams

---

## Trap 6 — EventBridge Is a Queue

False.

EventBridge:

**Routes**

SQS:

**Queues**

---

## Trap 7 — SNS Filtering and EventBridge Are Identical

False.

SNS filtering:

**Selective pub/sub**

EventBridge:

**Broader event-bus routing**

---

## Trap 8 — FIFO Is Always Better

False.

Use FIFO when:

**Ordering / deduplication are required**

Otherwise Standard services may offer:

**Greater flexibility / throughput**

---

## Trap 9 — Kinesis and SQS FIFO Are the Same Because Both Have Ordering

False.

SQS FIFO:

**Ordered tasks**

Kinesis:

**Ordered retained stream**

---

## Trap 10 — Firehose Is a Consumer Queue

False.

Firehose is primarily:

**Managed destination delivery**

---

# Ultra-Fast Messaging Decision Tree

Need asynchronous messaging?  
↓

Need work to WAIT?  
→ [[SQS]]

Need work to WAIT IN ORDER?  
→ [[SQS FIFO]]

Need ONE event sent to MANY?  
→ [[SNS]]

Need ONE ORDERED event sent to MANY?  
→ [[SNS FIFO]]

Need continuous REAL-TIME DATA?  
→ [[20-SAA/10-Messaging/Kinesis Data Streams]]

Need streaming data to LAND somewhere?  
→ [[20-SAA/10-Messaging/Kinesis Data Firehose]]

Need rules to decide WHERE an event goes?  
→ [[20-SAA/10-Messaging/EventBridge]]

---

# Quick Comparison Table

| Service | Main Model | Best Exam Clue |
|---|---|---|
| [[SQS]] | Queue | Buffer / Worker |
| [[SQS FIFO]] | Ordered Queue | Order + Dedup |
| [[SNS]] | Pub/Sub | Fan-Out |
| [[SNS FIFO]] | Ordered Pub/Sub | Ordered Fan-Out |
| [[20-SAA/10-Messaging/Kinesis Data Streams]] | Stream | Real-Time + Replay |
| [[20-SAA/10-Messaging/Kinesis Data Firehose]] | Delivery | Stream → Destination |
| [[20-SAA/10-Messaging/EventBridge]] | Event Bus | Rules + Routing |

---

# Pull vs Push vs Stream vs Route

| Service | Behavior |
|---|---|
| SQS | Consumers Pull |
| SNS | Push to Subscribers |
| Kinesis Data Streams | Consumers Read Stream |
| Firehose | Pushes/Batches to Destination |
| EventBridge | Routes Matching Events |

---

# Retention / Replay Thinking

| Service | Main Replay / Retention Model |
|---|---|
| SQS | Temporary queue retention |
| SNS | No queue-like replay model |
| Kinesis Data Streams | Retained stream + replay |
| Firehose | Delivery-focused |
| EventBridge | Archive + Replay |

---

# Final Exam Rapid-Fire

> **DECOUPLE WORKERS**
> → SQS
>
> **STRICTLY ORDER WORK**
> → SQS FIFO
>
> **ONE → MANY**
> → SNS
>
> **ORDERED ONE → MANY**
> → SNS FIFO
>
> **SELECTIVE SNS DELIVERY**
> → SNS FILTER POLICY
>
> **REAL-TIME DATA + REPLAY**
> → KINESIS DATA STREAMS
>
> **STREAM → S3 / REDSHIFT / OPENSEARCH**
> → FIREHOSE
>
> **EVENT RULES + TARGETS**
> → EVENTBRIDGE
>
> **AWS API CALL → AUTOMATION**
> → CLOUDTRAIL + EVENTBRIDGE

---

## Master Memory Trick

> [!tip] Messaging Master Memory Trick
> Imagine a company office:
>
> **SQS**
>
> → Inbox
>
> Work waits until someone picks it up.
>
> **SQS FIFO**
>
> → Numbered inbox
>
> Work must be handled in sequence.
>
> **SNS**
>
> → Office loudspeaker
>
> Everyone subscribed hears the announcement.
>
> **SNS FIFO**
>
> → Numbered announcements
>
> Everyone hears them in order.
>
> **Kinesis Data Streams**
>
> → Security camera feed
>
> Continuous stream that multiple people can watch and replay.
>
> **Firehose**
>
> → Delivery truck
>
> Takes the stream and drops it at a destination.
>
> **EventBridge**
>
> → Dispatcher
>
> Looks at each event and decides where it belongs.

So memorize:

> **SQS = WAIT**
>
> **SQS FIFO = ORDERED WAIT**
>
> **SNS = BROADCAST**
>
> **SNS FIFO = ORDERED BROADCAST**
>
> **KINESIS = STREAM**
>
> **FIREHOSE = DELIVER**
>
> **EVENTBRIDGE = ROUTE**

And the best exam question:

> **"What does the application need to DO with the message?"**

The answer usually tells you:

**Which service wins.**

---

## Related Notes

- [[SQS]]
- [[SQS FIFO]]
- [[SNS]]
- [[SNS FIFO]]
- [[SNS Message Filtering]]
- [[20-SAA/10-Messaging/Kinesis Data Streams]]
- [[20-SAA/10-Messaging/Kinesis Data Firehose]]
- [[20-SAA/10-Messaging/EventBridge]]
- [[02-Compute/Lambda]]
- [[06-Security/CloudTrail]]
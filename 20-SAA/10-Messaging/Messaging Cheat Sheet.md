## Messaging Exam Strategy

For SAA messaging questions, start by asking:

> **What should happen to the message?**

Use this fast decision map:

| Requirement | Immediately Think |
|---|---|
| Queue / Buffer Work | [[SQS]] |
| Queue + Strict Ordering | [[SQS FIFO]] |
| One Message → Many Receivers | [[SNS]] |
| Ordered Fan-Out | [[SNS FIFO]] |
| Selective SNS Delivery | [[SNS Message Filtering]] |
| Real-Time Streaming + Replay | [[20-SAA/10-Messaging/Kinesis Data Streams]] |
| Deliver Stream to Destination | [[20-SAA/10-Messaging/Kinesis Data Firehose]] |
| Event Rules / Routing | [[20-SAA/10-Messaging/EventBridge]] |

> [!tip] Master Messaging Rule
> **WAIT → SQS**
>
> **ORDERED WAIT → SQS FIFO**
>
> **BROADCAST → SNS**
>
> **ORDERED BROADCAST → SNS FIFO**
>
> **STREAM → Kinesis**
>
> **DELIVER → Firehose**
>
> **ROUTE → EventBridge**

---

## SQS

[[SQS]] provides:

**Managed Message Queues**

Think:

Producer  
↓  
Queue  
↓  
Consumer

Best for:

- Decoupling
- Async processing
- Traffic spikes
- Backpressure
- Worker fleets
- Buffering

### Killer Exam Clue

> **Work must wait until a consumer is ready**
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
- Duplicates possible
- Consumer should be idempotent

### Exam Shortcut

**Maximum throughput + no strict order**
→ SQS Standard

---

## SQS FIFO

[[SQS FIFO]]

Think:

- Strict ordering
- Deduplication
- MessageGroupId
- MessageDeduplicationId
- Sequence-sensitive work

### Killer Exam Clue

> **Order matters and duplicate messages must be prevented**
>
> → **SQS FIFO**

### Memory Trick

**GROUP = ORDER**

**DEDUP = DUPLICATES**

---

## SQS Visibility Timeout

When a consumer receives a message:

**It becomes temporarily invisible**

If processing succeeds:

**Delete it**

If processing fails:

Visibility timeout expires  
↓  
Message becomes visible again

### Killer Exam Clue

> **Same message is being processed by multiple consumers because processing takes too long**
>
> → **Increase Visibility Timeout**

---

## SQS Long Polling

Long polling:

- Reduces empty responses
- Reduces API calls
- Reduces cost

Maximum wait:

**20 seconds**

### Killer Exam Clue

> **Too many empty ReceiveMessage responses**
>
> → **Enable Long Polling**

---

## Dead-Letter Queue

A DLQ stores:

**Messages that repeatedly fail processing**

Architecture:

Main Queue  
↓  
Retries  
↓  
maxReceiveCount  
↓  
DLQ

### Killer Exam Clue

> **Poison message keeps failing**
>
> → **DLQ**

---

## SNS

[[SNS]] provides:

**Publish / Subscribe**

Think:

Publisher  
↓  
SNS Topic  
↓  
Many Subscribers

Best for:

- Fan-Out
- Notifications
- Push delivery
- One-to-many messaging

### Killer Exam Clue

> **One event must reach multiple receivers**
>
> → **SNS**

### Memory Trick

**SNS = BROADCAST**

---

## SNS + SQS Fan-Out

Architecture:

Producer  
↓  
SNS  
↓  
├── SQS Queue A
├── SQS Queue B
└── SQS Queue C

SNS:

**Copies**

SQS:

**Stores / Buffers**

### Killer Exam Clue

> **Multiple independent systems need their own durable copy**
>
> → **SNS + Multiple SQS Queues**

### Memory Trick

**SNS COPIES**

**SQS HOLDS**

---

## SNS FIFO

[[SNS FIFO]]

Think:

- Ordered Pub/Sub
- Fan-Out
- Deduplication
- MessageGroupId

### Killer Exam Clue

> **Multiple consumers need the same ordered events**
>
> → **SNS FIFO + SQS FIFO**

### Memory Trick

**SNS FIFO = ORDERED BROADCAST**

---

## SNS Message Filtering

[[SNS Message Filtering]]

lets each subscription receive:

**Only messages that match its filter policy**

### Important Rule

**No Filter**
→ Receive All

### Killer Exam Clue

> **One SNS topic, but subscribers need different message categories**
>
> → **SNS Subscription Filter Policies**

### Memory Trick

**FILTER = WHICH**

**FIFO = ORDER**

---

## Kinesis Data Streams

[[20-SAA/10-Messaging/Kinesis Data Streams]]

provides:

**Real-Time Streaming Data**

Think:

- Clickstreams
- IoT
- Logs
- Metrics
- Telemetry
- Multiple consumers
- Retention
- Replay
- Partition keys

### Killer Exam Clue

> **Continuous real-time data + multiple consumers + replay**
>
> → **Kinesis Data Streams**

### Memory Trick

**Kinesis = STREAM**

---

## Kinesis Retention

Consumers reading a record do NOT:

**Delete it**

Records remain available for:

**The retention period**

This allows:

- Multiple consumers
- Replay
- Reprocessing

### Memory Trick

**SQS = Consume + Delete**

**Kinesis = Read + Retain**

---

## Kinesis Ordering

Ordering is preserved for:

**Records with the same partition key**

### Killer Exam Clue

> **Need ordered streaming events per customer/device**
>
> → **Use the same partition key for that logical entity**

### Memory Trick

**PARTITION KEY = ORDER + DISTRIBUTION**

---

## Kinesis Shards

Shards represent:

**Stream capacity**

More shards:

→ More throughput

Poor partition-key distribution:

→ Hot shard risk

### Exam Trap

One partition key for everything:

**Bad for scaling**

---

## KPL vs KCL

| Library | Purpose |
|---|---|
| KPL | Producer |
| KCL | Consumer |

### Memory Trick

**P = Producer**

**C = Consumer**

---

## Kinesis Data Firehose

[[20-SAA/10-Messaging/Kinesis Data Firehose]]

provides:

**Managed streaming delivery**

Think:

Stream  
↓  
Firehose  
↓  
Destination

Common destinations:

- [[S3]]
- Redshift
- OpenSearch
- Supported external endpoints

### Killer Exam Clue

> **Continuously deliver streaming data to S3 with minimal management**
>
> → **Firehose**

### Memory Trick

**Firehose = DELIVER**

---

## Firehose Behavior

Think:

- Fully managed
- Automatic scaling
- Buffering
- Batching
- Near real-time
- Lambda transformation

### Exam Trap

Firehose is NOT primarily for:

- Replay
- Multiple custom consumers
- Worker queues

---

## Data Streams vs Firehose

| Requirement | Data Streams | Firehose |
|---|---:|---:|
| Stream Processing | ✅ | Delivery Focus |
| Replay | ✅ | ❌ |
| Retention | ✅ | ❌ Stream Model |
| Multiple Consumers | ✅ | ❌ Primary Use |
| Buffer / Batch Delivery | ❌ Primary Use | ✅ |
| Deliver to S3 | Via Integration | ✅ |
| Managed Delivery | ❌ | ✅ |

### Memory Trick

**Streams = PROCESS**

**Firehose = DELIVER**

---

## EventBridge

[[20-SAA/10-Messaging/EventBridge]]

provides:

**Rule-Based Event Routing**

Think:

Event Source  
↓  
Event Bus  
↓  
Rule  
↓  
Target

Best for:

- AWS events
- SaaS events
- Custom events
- Event patterns
- Automation
- Archive
- Replay

### Killer Exam Clue

> **Route events to targets based on event content**
>
> → **EventBridge**

### Memory Trick

**EventBridge = ROUTE**

---

## EventBridge Buses

| Bus | Main Source |
|---|---|
| Default | AWS Services |
| Partner | SaaS |
| Custom | Your Applications |

### Memory Trick

**AWS → DEFAULT**

**SAAS → PARTNER**

**YOUR APP → CUSTOM**

---

## EventBridge Rules

Think:

IF:

Event matches pattern

THEN:

Send to target

### Killer Exam Clue

> **React automatically when an EC2 instance changes state**
>
> → **EventBridge Rule**

---

## CloudTrail + EventBridge

[[06-Security/CloudTrail]] records:

**AWS API activity**

EventBridge reacts to:

**That activity**

Architecture:

API Call  
↓  
CloudTrail  
↓  
EventBridge  
↓  
Target

### Killer Exam Clue

> **Alert when a specific AWS API call occurs**
>
> → **CloudTrail + EventBridge**

---

## EventBridge Archive + Replay

Archive:

**Save events**

Replay:

**Run saved events through the event bus again**

### Killer Exam Clue

> **Need to reprocess historical business events**
>
> → **EventBridge Archive + Replay**

---

## EventBridge Schema Registry

Think:

- Discover event structure
- Understand JSON schemas
- Version schemas
- Generate code bindings

### Killer Exam Clue

> **Automatically discover the structure of events**
>
> → **Schema Registry**

---

## SQS vs SNS

| Requirement | SQS | SNS |
|---|---:|---:|
| Queue | ✅ | ❌ |
| Pub/Sub | ❌ | ✅ |
| Consumer Pull | ✅ | ❌ |
| Push to Subscribers | ❌ | ✅ |
| Buffer Work | ✅ | ❌ |
| Fan-Out | ❌ | ✅ |

### Memory Trick

**SQS = LINE**

**SNS = LOUDSPEAKER**

---

## SNS vs EventBridge

### SNS

Think:

**Simple Fan-Out**

### EventBridge

Think:

**Advanced Event Routing**

### Exam Shortcut

**Broadcast**
→ SNS

**Route based on event pattern**
→ EventBridge

---

## SQS vs Kinesis

### SQS

Think:

**Jobs**

Consumers compete for:

**Work**

### Kinesis

Think:

**Streaming data**

Consumers independently read:

**The same stream**

### Exam Shortcut

**Work items**
→ SQS

**Telemetry**
→ Kinesis

---

## SQS FIFO vs Kinesis

### SQS FIFO

Think:

**Ordered tasks**

### Kinesis

Think:

**Ordered replayable stream**

### Exam Shortcut

**Ordered WORK**
→ SQS FIFO

**Ordered STREAM**
→ Kinesis

---

## SNS FIFO vs Kinesis

### SNS FIFO

Think:

**Ordered Fan-Out**

### Kinesis

Think:

**Ordered Retained Stream**

---

## Firehose vs EventBridge

### Firehose

Question:

> **Where should this streaming data land?**

### EventBridge

Question:

> **Where should this event go?**

### Memory Trick

**Firehose = DESTINATION**

**EventBridge = ROUTING**

---

## Architecture Thinking

### Scenario 1 — Web Tier Buffer

Front-end traffic arrives faster than the backend can process it.

**Choose → [[SQS]]**

---

### Scenario 2 — Financial Work Queue

Transactions must be processed:

- In order
- Without duplicates

**Choose → [[SQS FIFO]]**

---

### Scenario 3 — One Order to Many Systems

Shipping, fraud, and analytics each need:

**The same order event**

**Choose → [[SNS]]**

For durable processing:

**SNS + SQS**

---

### Scenario 4 — Ordered Fan-Out

Multiple systems need:

**The same ordered transactions**

**Choose → SNS FIFO + SQS FIFO**

---

### Scenario 5 — Subscriber Filtering

Different SQS queues only need:

- Placed
- Cancelled
- Declined

events from one SNS topic.

**Choose → SNS Filter Policies**

---

### Scenario 6 — IoT Streaming

Millions of devices continuously send:

**Sensor readings**

with multiple consumers and replay.

**Choose → [[20-SAA/10-Messaging/Kinesis Data Streams]]**

---

### Scenario 7 — Logs to S3

Streaming logs must land in S3 automatically.

**Choose → [[20-SAA/10-Messaging/Kinesis Data Firehose]]**

---

### Scenario 8 — EC2 Automation

When an EC2 instance stops:

**Run Lambda**

**Choose → EventBridge + Lambda**

---

### Scenario 9 — API Security Alert

Alert security when:

`DeleteTable`

occurs.

Choose:

CloudTrail  
↓  
EventBridge  
↓  
SNS

---

### Scenario 10 — Replay Stream

Yesterday's telemetry must be:

**Reprocessed**

**Choose → Kinesis Data Streams**

---

### Scenario 11 — Replay Business Events

Previously archived order events must be:

**Routed again**

**Choose → EventBridge Archive + Replay**

---

## Biggest Messaging Exam Traps

### Trap 1 — One SQS Queue Gives Every Consumer a Copy

False.

Consumers:

**Compete**

Need copies?

→ SNS + multiple SQS queues

---

### Trap 2 — SNS Buffers Messages Like SQS

False.

Need durable buffering?

→ SNS + SQS

---

### Trap 3 — Standard SQS Guarantees Ordering

False.

Need strict ordering?

→ SQS FIFO

---

### Trap 4 — Kinesis Is Just a Queue

False.

Kinesis:

**Retained stream**

SQS:

**Work queue**

---

### Trap 5 — Reading Kinesis Deletes the Record

False.

Record remains until:

**Retention expires**

---

### Trap 6 — Firehose Supports Replay Like Data Streams

False.

Replay:

→ Kinesis Data Streams

---

### Trap 7 — EventBridge Is a Queue

False.

EventBridge:

**Routes**

SQS:

**Queues**

---

### Trap 8 — SNS Filtering and EventBridge Are Identical

False.

SNS Filtering:

**Selective Pub/Sub**

EventBridge:

**Broader event routing**

---

### Trap 9 — FIFO Is Always Better

False.

Use FIFO only when:

**Ordering / deduplication are required**

---

### Trap 10 — EventBridge and CloudTrail Do the Same Thing

False.

CloudTrail:

**Records API activity**

EventBridge:

**Reacts to events**

---

## Ultra-Fast Decision Tree

Need asynchronous messaging?  
↓

Need work to wait?  
→ [[SQS]]

Need strict order too?  
→ [[SQS FIFO]]

Need one event sent to many?  
→ [[SNS]]

Need ordered one-to-many?  
→ [[SNS FIFO]]

Need different SNS subscribers to receive different messages?  
→ [[SNS Message Filtering]]

Need continuous real-time records?  
→ [[20-SAA/10-Messaging/Kinesis Data Streams]]

Need streaming data delivered to storage / analytics?  
→ [[20-SAA/10-Messaging/Kinesis Data Firehose]]

Need rules deciding where events go?  
→ [[20-SAA/10-Messaging/EventBridge]]

---

## Quick Cheat Sheet

| Exam Clue | Answer |
|---|---|
| Queue | SQS |
| Buffer | SQS |
| Backpressure | SQS |
| Strict Queue Ordering | SQS FIFO |
| Deduplication | SQS FIFO |
| Fan-Out | SNS |
| One → Many | SNS |
| Ordered Fan-Out | SNS FIFO |
| Selective SNS Delivery | SNS Filter Policy |
| Real-Time Stream | Kinesis Data Streams |
| Replay Streaming Records | Kinesis Data Streams |
| Partition Key Ordering | Kinesis Data Streams |
| Stream → S3 | Firehose |
| Managed Stream Delivery | Firehose |
| Event Rules | EventBridge |
| AWS/SaaS/Custom Event Routing | EventBridge |
| Historical Business Event Replay | EventBridge Archive |
| API Activity Automation | CloudTrail + EventBridge |

---

## Final Exam Rapid-Fire

> **QUEUE**
> → SQS
>
> **QUEUE + ORDER**
> → SQS FIFO
>
> **ONE → MANY**
> → SNS
>
> **ONE → MANY + ORDER**
> → SNS FIFO
>
> **WHO GETS WHICH SNS MESSAGE?**
> → SNS FILTER POLICY
>
> **REAL-TIME + RETENTION + REPLAY**
> → KINESIS DATA STREAMS
>
> **STREAM → DESTINATION**
> → FIREHOSE
>
> **RULE → TARGET**
> → EVENTBRIDGE
>
> **AWS API CALL → EVENT**
> → CLOUDTRAIL + EVENTBRIDGE

---

## Master Memory Trick

> [!tip] Messaging Master Memory Trick
> Picture seven different tools:
>
> **SQS**
> → Waiting line
>
> **SQS FIFO**
> → Numbered waiting line
>
> **SNS**
> → Loudspeaker
>
> **SNS FIFO**
> → Numbered announcements
>
> **Kinesis Data Streams**
> → River
>
> **Firehose**
> → Delivery hose
>
> **EventBridge**
> → Traffic controller

Then memorize:

> **WAIT**
> → SQS
>
> **ORDERED WAIT**
> → SQS FIFO
>
> **BROADCAST**
> → SNS
>
> **ORDERED BROADCAST**
> → SNS FIFO
>
> **STREAM**
> → Kinesis
>
> **DELIVER**
> → Firehose
>
> **ROUTE**
> → EventBridge

And the single best exam question:

> **"What should happen to the message?"**

That usually tells you:

**Which AWS messaging service wins.**

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
- [[Messaging Services Comparison]]
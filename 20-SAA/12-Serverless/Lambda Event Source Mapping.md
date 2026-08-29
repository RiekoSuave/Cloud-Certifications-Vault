## What Problem Does It Solve?

A:

**Lambda Event Source Mapping**

connects [[Lambda]] to event sources that Lambda must:

**Poll for records**

instead of receiving direct push-style invocations.

Important event sources include:

- [[SQS]]
- [[20-SAA/10-Messaging/Kinesis Data Streams]]
- DynamoDB Streams

Architecture:

Event Source  
↓  
Lambda Event Source Mapping  
↓  
Lambda Polls  
↓  
Function Invoked

> [!tip] Memory Trick
> **Event Source Mapping = Lambda goes and gets the work**
>
> Think:
>
> **POLL → BATCH → INVOKE**

---

## Why This Is Different

Some services invoke Lambda by:

**Pushing events**

Examples:

- [[S3]]
- [[SNS]]
- [[20-SAA/10-Messaging/EventBridge]]

Other services are consumed through:

**Event Source Mapping**

Examples:

- [[SQS]]
- [[20-SAA/10-Messaging/Kinesis Data Streams]]
- DynamoDB Streams

### Master Distinction

> **S3 / SNS / EventBridge**
> → Push toward Lambda
>
> **SQS / Kinesis / DynamoDB Streams**
> → Lambda polls through Event Source Mapping

---

## Core Architecture

Think:

SQS / Stream  
↓  
Event Source Mapping  
↓  
Poll Records  
↓  
Create Batch  
↓  
Invoke Lambda  
↓  
Process Records

The event source mapping handles:

- Polling
- Batch retrieval
- Lambda invocation
- Scaling behavior
- Record tracking

---

## Polling

Lambda automatically:

**Polls the configured event source**

You do NOT need to write application code that continuously says:

> "Are there any new messages?"

The event source mapping handles:

**Polling infrastructure**

---

## Batch Processing

Event source mappings generally deliver:

**A batch of records**

to Lambda.

Architecture:

Source Records  
↓  
Event Source Mapping  
↓  
Batch  
↓  
Lambda Invocation

One invocation can therefore process:

**Multiple messages or records**

### Memory Trick

**Event Source Mapping = Batch Collector**

---

## Why Batching Matters

Without batching:

100 records  
→ 100 Lambda invocations

With batching:

100 records  
↓  
Groups of Records  
↓  
Fewer Lambda invocations

This can improve:

- Efficiency
- Throughput
- Cost

depending on the workload.

---

# Batch Size

The:

**Batch Size**

controls how many records the event source mapping attempts to send to:

**One Lambda invocation**

The exact supported limits vary by event source.

For SAA, the important concept is:

> **Larger batches can improve efficiency, while smaller batches can reduce per-invocation work and failure scope.**

---

# Batching Window

Some event source mappings support:

**A batching window**

which allows Lambda to wait briefly to collect:

**More records**

before invoking the function.

Conceptually:

Records Arrive  
↓  
Wait Briefly  
↓  
Build Larger Batch  
↓  
Invoke Lambda

Tradeoff:

**Throughput efficiency vs latency**

---

# SQS + Lambda Event Source Mapping

One of the most important architectures:

Producer  
↓  
[[SQS]]  
↓  
Event Source Mapping  
↓  
Lambda  
↓  
Process Messages

Lambda:

**Polls SQS**

on your behalf.

### Killer Exam Clue

> **Serverless processing of messages stored in SQS**
>
> → **SQS + Lambda Event Source Mapping**

---

## SQS Polling

Lambda's integration with SQS handles:

**Polling**

and invokes your Lambda function with:

**A batch of messages**

The function processes:

**The batch**

---

## SQS Visibility Timeout

When Lambda receives SQS messages:

Those messages become:

**Invisible**

for the queue's:

**Visibility Timeout**

This must be long enough for:

**Lambda processing**

### Exam Trap

If Lambda takes longer than the visibility timeout:

Messages can become:

**Visible again**

before processing finishes.

Potential result:

**Duplicate processing**

### Killer Fix

> **Set visibility timeout appropriately relative to Lambda processing time**

---

## Successful SQS Processing

Conceptually:

SQS Message  
↓  
Lambda Processes Successfully  
↓  
Message Removed from Queue

If processing fails:

Message can become available again according to:

**SQS retry / visibility behavior**

---

## SQS Failure Handling

Repeatedly failing messages can eventually be moved to:

**An SQS Dead-Letter Queue**

using:

**The queue's redrive policy**

Architecture:

SQS  
↓  
Lambda  
↓  
Failure  
↓  
Retry  
↓  
maxReceiveCount  
↓  
DLQ

### Important Distinction

For SQS-triggered Lambda:

Think primarily about:

**SQS DLQ / Redrive Policy**

rather than:

**Lambda asynchronous DLQ**

because SQS is using:

**Event Source Mapping**

not direct asynchronous invocation.

---

# Partial Batch Response

When Lambda processes an SQS batch:

One message can fail while others succeed.

Without careful handling:

**The entire batch may be retried**

depending on configuration and failure behavior.

Lambda supports:

**Partial Batch Response**

so the function can report:

**Only the failed messages**

for retry.

### Killer Exam Clue

> **Avoid reprocessing successful SQS messages when only some messages in a Lambda batch fail**
>
> → **Partial Batch Response**

---

## Why Partial Batch Response Matters

Example batch:

Message A ✅  
Message B ✅  
Message C ❌  
Message D ✅

Without partial failure reporting:

Potential retry:

A  
B  
C  
D

With partial batch response:

Retry:

**C only**

This reduces:

- Duplicate work
- Waste
- Unnecessary processing

---

# SQS Standard vs FIFO with Lambda

Lambda can consume:

- Standard SQS
- FIFO SQS

For FIFO queues:

Ordering must be respected according to:

**MessageGroupId**

### Exam Pattern

> **Serverless ordered queue processing**
>
> → **SQS FIFO + Lambda**

---

# SQS FIFO + Lambda

Architecture:

Producer  
↓  
SQS FIFO  
↓  
Event Source Mapping  
↓  
Lambda

Within each:

**Message Group**

processing preserves:

**Ordering semantics**

Different message groups can allow:

**Parallel processing**

### Memory Trick

**Same Group = Ordered**

**Different Groups = Parallel**

---

# Kinesis + Lambda Event Source Mapping

Architecture:

Producer  
↓  
[[20-SAA/10-Messaging/Kinesis Data Streams]]  
↓  
Shard  
↓  
Event Source Mapping  
↓  
Lambda

Lambda polls:

**Kinesis shards**

and delivers:

**Batches of records**

to the function.

---

## Kinesis Ordering

Kinesis preserves ordering:

**Within a shard / partition-key ordering path**

Lambda must process records in a way that respects:

**That ordered stream**

### Killer Exam Clue

> **Process ordered real-time stream records with serverless compute**
>
> → **Kinesis + Lambda Event Source Mapping**

---

## Kinesis Checkpoints

Consumers need to know:

**How far they have processed**

through a stream.

The integration tracks:

**Progress through the stream**

so processing can continue from:

**The appropriate record position**

after successful processing.

---

## Kinesis Failure Behavior

A failed record in an ordered stream can:

**Block progress**

for later records in that shard.

Why?

Because ordering must be preserved.

### Exam Concept

> **A poison record in a Kinesis shard can delay records behind it**

---

## Stream Retry Behavior

Because stream records remain available for:

**The retention period**

Lambda can retry:

**Failed batches / records**

according to stream event-source configuration.

This differs from:

**SQS message visibility**

---

# Bisect Batch on Function Error

For stream sources such as Kinesis, Lambda can support:

**Bisect Batch on Function Error**

This means:

Large Failed Batch  
↓  
Split Into Smaller Batches  
↓  
Retry

This helps isolate:

**The problematic record**

### Memory Trick

**BISECT = Split the bad batch in half**

---

## Example

Batch:

A  
B  
C  
D  
E  
F  
G  
H

Fails.

Bisect:

A B C D  
and  
E F G H

Continue splitting until:

**The problematic subset / record is isolated**

---

# Maximum Record Age

For stream event source mappings, you can control:

**How long Lambda should keep retrying old records**

Think:

Old Record  
↓  
Too Old  
↓  
Stop Retrying / Handle Failure

This helps prevent:

**Very old poison records**

from blocking processing indefinitely.

---

# Maximum Retry Attempts

You can also configure:

**Maximum Retry Attempts**

for certain stream event source mappings.

This limits:

**How many times Lambda retries failed records**

---

# Parallelization Factor

For Kinesis, Lambda can increase:

**Parallel processing per shard**

using:

**Parallelization Factor**

This allows multiple batches from the same shard to be processed:

**Concurrently**

while maintaining ordering where required for partition-key groups.

### Exam Concept

Use when:

**Stream processing needs more throughput**

without necessarily increasing shard count immediately.

---

# DynamoDB Streams + Lambda

Architecture:

DynamoDB Table  
↓  
DynamoDB Stream  
↓  
Event Source Mapping  
↓  
Lambda

Lambda polls:

**DynamoDB Streams**

for table changes.

Examples:

- INSERT
- MODIFY
- REMOVE

### Killer Exam Clue

> **Run code automatically when DynamoDB items change**
>
> → **DynamoDB Streams + Lambda Event Source Mapping**

---

# DynamoDB Streams Use Cases

Examples:

DynamoDB Change  
↓  
Lambda  
↓  
Update Search Index

or:

DynamoDB Change  
↓  
Lambda  
↓  
Send Notification

or:

DynamoDB Change  
↓  
Lambda  
↓  
Replicate / Transform Data

---

# Ordered Stream Processing

Both:

- Kinesis Data Streams
- DynamoDB Streams

are:

**Ordered stream sources**

This creates different failure behavior from:

**SQS Standard**

A bad record can delay:

**Later records in the same ordered path**

---

# Event Source Mapping vs Direct Async Invocation

This distinction is essential.

## Direct Async

Examples:

S3  
SNS  
EventBridge

Architecture:

Source  
↓  
Push Event  
↓  
Lambda Internal Async Queue  
↓  
Lambda

Failure handling:

**Lambda async retry model**

---

## Event Source Mapping

Examples:

SQS  
Kinesis  
DynamoDB Streams

Architecture:

Source  
↓  
Lambda Polling  
↓  
Batch  
↓  
Lambda

Failure handling:

**Depends heavily on source semantics**

### Memory Trick

**PUSH SOURCE**
→ Async Invocation

**POLL SOURCE**
→ Event Source Mapping

---

# Event Source Mapping and Concurrency

Event source mappings can drive:

**Lambda concurrency**

based on:

- Queue backlog
- Stream shards
- Batch processing
- Source-specific scaling behavior

This makes source design important for:

**Application scaling**

---

# SQS Scaling Behavior

With SQS:

Backlog ↑  
↓  
Lambda Polling Increases  
↓  
More Concurrent Lambda Executions

This allows Lambda to process:

**Growing queue depth**

automatically.

### Exam Risk

Downstream systems may not scale as quickly.

Possible protections:

- Reserved Concurrency
- RDS Proxy
- Queue-based architecture
- Controlled batch/concurrency configuration

---

# Kinesis Scaling Behavior

With Kinesis:

Concurrency is closely related to:

**Shard count and processing configuration**

Think:

More Shards  
↓  
More Parallel Stream Capacity

This is different from:

**SQS backlog-driven scaling**

---

# Source Semantics Matter

Do NOT treat:

SQS  
Kinesis  
DynamoDB Streams

as identical just because they all use:

**Event Source Mapping**

Each source has different:

- Retention
- Ordering
- Retry behavior
- Scaling
- Failure semantics

---

# SQS Semantics

Think:

- Queue
- Visibility timeout
- Messages removed after successful processing
- DLQ
- Worker distribution

---

# Kinesis Semantics

Think:

- Retained stream
- Shards
- Replay
- Ordered records
- Multiple consumers

---

# DynamoDB Streams Semantics

Think:

- DynamoDB item changes
- Ordered change records
- Event-driven table processing

---

# Event Source Mapping + Reserved Concurrency

If a source could invoke too many Lambda executions:

**Reserved Concurrency**

can control:

**Maximum function concurrency**

Example:

SQS Backlog  
↓  
Lambda Scaling  
↓  
Reserved Concurrency = 50  
↓  
Maximum ~50 concurrent function executions

This can protect:

**Downstream resources**

---

# Event Source Mapping + Idempotency

Because retries and duplicate processing can occur:

Functions should often be:

**Idempotent**

Example:

Message ID already processed?

Yes  
→ Do not duplicate business action

### SAA Principle

> **Queue and stream consumers should be designed for safe retries**

---

# Event Source Mapping + DLQ Thinking

Failure handling differs by source.

### SQS

Think:

**SQS DLQ**

### Kinesis / DynamoDB Streams

Think:

- Retry configuration
- Maximum record age
- Maximum retries
- Failure destination where supported
- Batch splitting

### Exam Rule

> **Always identify the event source before choosing failure handling**

---

# Architecture Thinking

## Scenario 1 — SQS Worker

Messages are stored in SQS.

Need serverless workers.

Choose:

SQS  
↓  
Event Source Mapping  
↓  
Lambda

---

## Scenario 2 — Duplicate Processing

Lambda processing takes:

2 minutes

SQS visibility timeout:

30 seconds

Messages reappear.

Fix:

**Increase SQS Visibility Timeout**

---

## Scenario 3 — Partial Batch Failure

Batch contains:

10 SQS messages

Only:

1 fails

Need to avoid reprocessing:

The other 9.

Choose:

**Partial Batch Response**

---

## Scenario 4 — Real-Time Stream

Application sends:

Clickstream records

to Kinesis.

Need serverless processing.

Choose:

Kinesis  
↓  
Event Source Mapping  
↓  
Lambda

---

## Scenario 5 — Poison Kinesis Record

One record repeatedly fails and blocks later records.

Consider:

- Bisect Batch on Function Error
- Maximum Retry Attempts
- Maximum Record Age
- Failure destination

depending on requirements.

---

## Scenario 6 — DynamoDB Change

When a customer record changes:

Run business logic.

Choose:

DynamoDB Streams  
↓  
Event Source Mapping  
↓  
Lambda

---

## Scenario 7 — S3 Upload

An object upload should trigger Lambda.

Do NOT think:

Event Source Mapping.

S3 uses:

**Asynchronous invocation**

---

## Scenario 8 — SNS Message

SNS should invoke Lambda.

Think:

**Asynchronous invocation**

not:

Event Source Mapping.

---

## Scenario 9 — EventBridge Event

EventBridge triggers Lambda.

Think:

**Asynchronous invocation**

not:

Polling.

---

# Scenario Recognition

Immediately think:

**Event Source Mapping**

when you see:

- Lambda polls source
- Batch records
- SQS + Lambda
- Kinesis + Lambda
- DynamoDB Streams + Lambda
- Batch size
- Batching window
- Partial batch response
- Bisect batch
- Stream retry behavior

---

# Exam Traps

## Trap 1 — SQS Pushes Directly to Lambda

❌

Lambda polls SQS through:

**Event Source Mapping**

---

## Trap 2 — Kinesis Pushes Each Record Directly to Lambda

❌

Lambda polls:

**Kinesis shards**

through Event Source Mapping.

---

## Trap 3 — S3 Uses Event Source Mapping

❌

S3 typically invokes Lambda:

**Asynchronously**

---

## Trap 4 — SNS Uses Event Source Mapping

❌

SNS invokes Lambda:

**Asynchronously**

---

## Trap 5 — EventBridge Uses Event Source Mapping

❌

EventBridge invokes Lambda:

**Asynchronously**

---

## Trap 6 — SQS Failures Use Lambda Async Retry Semantics

Not primarily.

Think:

**SQS visibility, redrive, and DLQ semantics**

---

## Trap 7 — Entire Batch Must Always Be Retried

❌

For supported SQS processing:

**Partial Batch Response**

can isolate failed messages.

---

## Trap 8 — Stream Failure Never Blocks Later Records

❌

Ordered stream processing means:

**Failed records can delay later records**

---

## Trap 9 — Bisect Batch Is Mainly an SQS Feature

❌

Think:

**Ordered stream sources such as Kinesis**

---

## Trap 10 — Event Source Mapping Removes Need for Idempotency

❌

Retries and duplicates can still occur.

---

# Quick Cheat Sheet

| Exam Clue | Answer |
|---|---|
| SQS → Lambda | Event Source Mapping |
| Kinesis → Lambda | Event Source Mapping |
| DynamoDB Streams → Lambda | Event Source Mapping |
| S3 → Lambda | Async Invocation |
| SNS → Lambda | Async Invocation |
| EventBridge → Lambda | Async Invocation |
| Batch Records | Event Source Mapping |
| SQS Message Reappears Too Soon | Increase Visibility Timeout |
| One SQS Record Fails in Batch | Partial Batch Response |
| Split Failed Stream Batch | Bisect Batch |
| Old Poison Stream Record | Maximum Record Age |
| Limit Stream Retries | Maximum Retry Attempts |
| Protect Downstream System | Reserved Concurrency |
| Safe Duplicate Processing | Idempotency |

---

# Push vs Poll Cheat Sheet

| Source | Lambda Model |
|---|---|
| S3 | Push / Async |
| SNS | Push / Async |
| EventBridge | Push / Async |
| SQS | Poll / Event Source Mapping |
| Kinesis | Poll / Event Source Mapping |
| DynamoDB Streams | Poll / Event Source Mapping |

---

# Queue vs Stream Failure Thinking

| Source | Primary Failure Concept |
|---|---|
| SQS | Visibility + Retry + DLQ |
| Kinesis | Ordered Retry + Record Age + Batch Handling |
| DynamoDB Streams | Ordered Retry + Batch Handling |

---

# Final Exam Rapid-Fire

> **SQS → LAMBDA**
> → EVENT SOURCE MAPPING
>
> **KINESIS → LAMBDA**
> → EVENT SOURCE MAPPING
>
> **DYNAMODB STREAMS → LAMBDA**
> → EVENT SOURCE MAPPING
>
> **S3 / SNS / EVENTBRIDGE**
> → ASYNC PUSH
>
> **LAMBDA POLLS**
> → EVENT SOURCE MAPPING
>
> **MULTIPLE RECORDS PER INVOCATION**
> → BATCHING
>
> **SQS MESSAGE RETURNS TOO EARLY**
> → VISIBILITY TIMEOUT
>
> **ONE MESSAGE IN BATCH FAILS**
> → PARTIAL BATCH RESPONSE
>
> **STREAM BATCH FAILS**
> → BISECT BATCH
>
> **OLD POISON RECORD**
> → MAX RECORD AGE
>
> **TOO MANY LAMBDA EXECUTIONS**
> → RESERVED CONCURRENCY
>
> **DUPLICATE-SAFE PROCESSING**
> → IDEMPOTENCY

---

## Master Memory Trick

> [!tip] Lambda Event Source Mapping Master Memory Trick
> Imagine Lambda is a worker who sometimes waits for someone to hand it work and sometimes goes to pick work up.
>
> **S3 / SNS / EVENTBRIDGE**
>
> walk over and hand Lambda the job.
>
> That's:
>
> **PUSH / ASYNC**
>
> But:
>
> **SQS / KINESIS / DYNAMODB STREAMS**
>
> keep the work in their own systems.
>
> Lambda has to:
>
> **GO GET IT**
>
> That's:
>
> **EVENT SOURCE MAPPING**

Then remember:

> **POLL**
> → Event Source Mapping
>
> **BATCH**
> → Multiple records per invocation
>
> **SQS**
> → Visibility + DLQ
>
> **KINESIS**
> → Shards + ordered stream
>
> **DYNAMODB STREAMS**
> → Table changes
>
> **PARTIAL BATCH**
> → Retry only failed SQS items
>
> **BISECT**
> → Split failed stream batch

And the killer SAA question:

> **"Who initiates delivery?"**
>
> Source pushes to Lambda?
> → Async Invocation
>
> Lambda polls the source?
> → **Event Source Mapping**

---

## Related Notes

- [[Lambda]]
- [[Lambda Synchronous Invocations]]
- [[Lambda Asynchronous Invocations]]
- [[SQS]]
- [[SQS FIFO]]
- [[20-SAA/10-Messaging/Kinesis Data Streams]]
- [[04-Databases/DynamoDB]]
- [[S3]]
- [[SNS]]
- [[20-SAA/10-Messaging/EventBridge]]
- [[RDS Proxy]]
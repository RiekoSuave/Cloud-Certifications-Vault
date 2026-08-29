## What Is an Asynchronous Invocation?

An:

**Asynchronous Invocation**

means the caller sends an event to [[Lambda]] and:

**Does not wait for the function to finish**

Architecture:

Event Source  
↓  
Lambda  
↓  
Caller Continues Immediately

Lambda then processes the event:

**In the background**

> [!tip] Memory Trick
> **ASYNC = SEND → MOVE ON**
>
> Caller says:
>
> **"Do this when you can."**

---

## Core Concept

With asynchronous invocation:

1. Event is sent to Lambda
2. Lambda accepts the event
3. Caller receives acknowledgement
4. Caller continues
5. Lambda processes the event separately

This is ideal when:

**The caller does not need an immediate response**

---

## Common Asynchronous Sources

Common asynchronous event sources include:

- [[S3]]
- [[SNS]]
- [[20-SAA/10-Messaging/EventBridge]]
- Some direct Lambda invocations configured as asynchronous

Think:

S3 Event  
↓  
Lambda

SNS Message  
↓  
Lambda

EventBridge Event  
↓  
Lambda

### Killer Exam Clue

> **Caller should not wait for Lambda to finish**
>
> → **Asynchronous Invocation**

---

# S3 + Lambda

Classic architecture:

User  
↓  
Upload Object  
↓  
[[S3]]  
↓  
Lambda  
↓  
Process File

Examples:

- Resize image
- Generate thumbnail
- Validate file
- Extract metadata
- Process uploaded document

The user does NOT need to wait for:

**The Lambda result**

### Memory Trick

**S3 EVENT = ASYNC**

---

# SNS + Lambda

[[SNS]] can invoke Lambda asynchronously.

Architecture:

Publisher  
↓  
SNS Topic  
↓  
Lambda

This is useful for:

- Fan-out
- Notifications
- Event-driven processing

If multiple Lambda functions subscribe:

SNS  
↓  
├── Lambda A
├── Lambda B
└── Lambda C

each can process:

**Its own copy**

---

# EventBridge + Lambda

[[20-SAA/10-Messaging/EventBridge]] commonly invokes Lambda asynchronously.

Architecture:

AWS Event  
↓  
EventBridge Rule  
↓  
Lambda

Examples:

- EC2 state change
- CodeBuild failure
- Custom application event
- Scheduled event

### Killer Exam Pattern

> **React to an AWS event without blocking the source**
>
> → **EventBridge + Lambda**

---

# Asynchronous Retry Behavior

This is one of the most important concepts.

For asynchronous invocation:

**Lambda itself manages retry behavior**

If the function returns an error:

Lambda can retry the event automatically.

### Memory Trick

**SYNC = Caller Retries**

**ASYNC = Lambda Retries**

---

## Why This Matters

Suppose:

S3  
↓  
Lambda  
↓  
Error

With async invocation:

S3 does not need to:

**Wait and retry the function itself**

Lambda handles:

**The asynchronous event-processing retry behavior**

---

# Asynchronous Event Queue

Conceptually, asynchronous events are placed into:

**An internal Lambda event queue**

Architecture:

Event Source  
↓  
Lambda Async Queue  
↓  
Lambda Function

This decouples:

**Event acceptance**

from:

**Function execution**

---

## Burst Handling

If many events arrive:

Events  
↓  
Internal Queue  
↓  
Lambda Scales  
↓  
Processes Events

This helps Lambda absorb:

**Bursty event traffic**

but concurrency and service limits still matter.

---

# Retry Attempts

If an asynchronous invocation fails:

Lambda retries according to:

**Its asynchronous retry behavior**

The exact behavior can depend on configuration and service behavior.

For SAA, the key idea is:

> **Lambda manages retries for async invocation**

not:

**The original caller**

---

# Event Age

Asynchronous event processing can also be constrained by:

**Maximum Event Age**

This limits how long Lambda should continue attempting to process:

**An old event**

### Exam Thinking

If an event becomes too old:

It can be discarded or routed according to:

**Failure-handling configuration**

---

# Maximum Retry Attempts

You can configure:

**Maximum Retry Attempts**

for asynchronous Lambda invocations.

This allows control over:

**How many times a failed asynchronous event is retried**

### Memory Trick

**RETRY COUNT = How persistent should Lambda be?**

---

# Dead-Letter Queue

Failed asynchronous events can be sent to a:

**Dead-Letter Queue**

after retries are exhausted.

Possible destinations include services such as:

- [[SQS]]
- [[SNS]]

Architecture:

Event  
↓  
Lambda  
↓  
Retry  
↓  
Retry  
↓  
Still Fails  
↓  
DLQ

### Killer Exam Clue

> **Preserve failed asynchronous Lambda events for investigation**
>
> → **Dead-Letter Queue**

---

## Why Use a DLQ?

Without a DLQ:

Repeatedly failing events may eventually be:

**Lost from the normal processing path**

With a DLQ:

Failed Event  
↓  
Stored Separately  
↓  
Investigate / Reprocess Later

### Memory Trick

**DLQ = Failed Event Parking Lot**

---

# Lambda Destinations

Lambda Destinations provide a more flexible way to route:

**Asynchronous invocation results**

You can configure destinations for:

- Success
- Failure

Architecture:

Lambda Async Invocation  
↓  
Success  
→ Destination A

Failure  
→ Destination B

---

## Destination Use Cases

On success:

Lambda  
↓  
Send result to another service

On failure:

Lambda  
↓  
Send failure details to:

- SQS
- SNS
- EventBridge
- Another Lambda

depending on supported architecture

### Memory Trick

**DESTINATIONS = What happens AFTER async execution?**

---

# DLQ vs Destinations

This distinction can appear on the exam.

## DLQ

Think:

**Capture failed events**

Primary focus:

**Failure preservation**

---

## Lambda Destinations

Think:

**Route invocation results**

Can handle:

- Success
- Failure

with more context.

### Exam Shortcut

**Just preserve failures**
→ DLQ

**Route success/failure outcomes**
→ Lambda Destinations

---

# Asynchronous Invocation Is Not SQS

Lambda's internal asynchronous queue does NOT make it equivalent to:

[[SQS]]

SQS provides:

- Explicit queue
- Message visibility
- Retention configuration
- Polling consumers
- Backpressure architecture
- Multiple queue-specific controls

Lambda async queue is primarily:

**An internal invocation mechanism**

### Exam Rule

> If the architecture explicitly needs a queue:
>
> **Use SQS**

---

# SQS + Lambda Is Different

[[SQS]] is NOT an asynchronous push source in the same way as S3/SNS/EventBridge.

Lambda uses:

**Event Source Mapping**

to poll SQS.

Architecture:

Producer  
↓  
SQS  
↓  
Lambda Event Source Mapping  
↓  
Lambda

### Killer Distinction

**S3 / SNS / EventBridge**
→ Async invocation

**SQS**
→ Event Source Mapping

---

# Kinesis + Lambda

[[20-SAA/10-Messaging/Kinesis Data Streams]] also uses:

**Event Source Mapping**

Lambda polls stream shards and processes:

**Batches of records**

This is not the same model as:

**Direct asynchronous Lambda invocation**

---

# DynamoDB Streams + Lambda

DynamoDB Streams also uses:

**Event Source Mapping**

Architecture:

DynamoDB  
↓  
Stream  
↓  
Lambda Polling  
↓  
Lambda

Again:

Not direct async push.

---

# Async vs Event Source Mapping

| Source | Invocation Model |
|---|---|
| S3 | Asynchronous |
| SNS | Asynchronous |
| EventBridge | Asynchronous |
| Direct Event Invocation | Asynchronous |
| SQS | Event Source Mapping |
| Kinesis | Event Source Mapping |
| DynamoDB Streams | Event Source Mapping |

---

# Asynchronous Error Flow

Example:

S3 Event  
↓  
Lambda  
↓  
Failure  
↓  
Retry  
↓  
Failure  
↓  
Retry / Age Limit  
↓  
DLQ or Destination

This provides:

**Built-in failure management**

---

# Idempotency

Asynchronous systems can process:

**Duplicate events**

Therefore Lambda code should often be:

**Idempotent**

Meaning:

Processing the same event more than once should not create:

**Incorrect duplicate effects**

Example:

Order ID 123  
↓  
Lambda  
↓  
Writes Transaction

If repeated:

Check Order ID  
↓  
Avoid Duplicate Transaction

### SAA Principle

> **Assume event-driven systems can deliver duplicates**

---

# Duplicate Events

Possible causes include:

- Retry behavior
- Upstream delivery semantics
- Network uncertainty
- Application failures

Do NOT assume:

**Exactly one invocation means exactly one business operation**

Design for:

**Safe retries**

---

# Async + Concurrency

Asynchronous events can cause Lambda to:

**Scale rapidly**

This can overwhelm downstream systems.

Example:

10,000 S3 Events  
↓  
Lambda Scales  
↓  
RDS

Potential problem:

**Too many DB connections**

Possible controls:

- Reserved Concurrency
- RDS Proxy
- SQS buffering

---

# When to Put SQS Before Lambda

Direct async:

S3  
↓  
Lambda

Can be fine for many workloads.

But if you need stronger buffering:

S3 / Producer  
↓  
SQS  
↓  
Lambda

SQS provides:

- Explicit backlog
- Visibility timeout
- DLQ
- Backpressure
- Message retention
- Controlled consumption

### Exam Pattern

> **Need durable buffering before Lambda**
>
> → **SQS + Lambda**

---

# SNS + SQS + Lambda

For durable fan-out:

Publisher  
↓  
SNS  
↓  
Multiple SQS Queues  
↓  
Multiple Lambda Consumers

SNS:

**Copies**

SQS:

**Buffers**

Lambda:

**Processes**

### Memory Trick

**SNS = COPY**

**SQS = HOLD**

**Lambda = DO**

---

# Async + EventBridge

EventBridge can route events before Lambda executes.

Architecture:

Event  
↓  
EventBridge Rule  
↓  
Lambda

This is useful when:

**Only matching events should trigger the function**

---

# Async + S3 Filtering

S3 Event Notifications can be configured using event criteria such as:

- Object creation
- Prefix
- Suffix

Example:

Only `.jpg` uploads  
↓  
Lambda Image Processor

This reduces:

**Unnecessary invocations**

---

# Asynchronous Invocation and User Experience

Async is a good fit when the user does NOT need:

**Immediate completion**

Example:

User uploads video  
↓  
Application returns:

"Upload received"

Processing continues:

**In background**

This provides:

**Better responsiveness**

for long-ish background work.

---

# Job Status Pattern

A common asynchronous architecture:

Client  
↓  
Submit Job  
↓  
Return Job ID

Background Processing  
↓  
Lambda / Queue / Workflow

Client later checks:

**Job Status**

This avoids keeping:

**A synchronous request open**

---

# Long-Running Work

Even asynchronous Lambda still has:

**15-minute maximum execution time**

Async does NOT remove:

**Lambda's runtime limit**

### Exam Trap

> **Async Lambda can run longer than 15 minutes**

❌ False.

If work requires longer:

Think:

- [[Fargate]]
- ECS
- AWS Batch
- Step Functions coordinating smaller jobs

---

# Async + Step Functions

If background processing requires:

**Multiple coordinated steps**

consider:

[[Step Functions]]

Architecture:

Event  
↓  
Step Functions  
↓  
Lambda A  
↓  
Lambda B  
↓  
Lambda C

Use Step Functions for:

- Orchestration
- Retries
- Branching
- State management
- Long-running workflows

---

# Architecture Thinking

## Scenario 1 — S3 Image Upload

User uploads image.

Need:

**Thumbnail generation**

User should not wait.

Choose:

S3  
↓  
Lambda

Invocation:

**Asynchronous**

---

## Scenario 2 — SNS Fan-Out

SNS publishes an order event.

Three Lambda functions should react independently.

Choose:

SNS  
↓  
Multiple Lambda Subscribers

Invocation:

**Asynchronous**

---

## Scenario 3 — EC2 State Event

When EC2 stops:

Run automated remediation.

Choose:

EventBridge  
↓  
Lambda

Invocation:

**Asynchronous**

---

## Scenario 4 — Failed Event Preservation

Async Lambda repeatedly fails.

Need:

**Store the failed event**

Choose:

**DLQ**

---

## Scenario 5 — Route Success and Failure

Need:

Successful invocation  
→ EventBridge

Failed invocation  
→ SQS

Choose:

**Lambda Destinations**

---

## Scenario 6 — Heavy Burst

Thousands of events arrive and downstream database cannot handle rapid Lambda scaling.

Consider:

- Reserved Concurrency
- RDS Proxy
- SQS buffer

depending on requirements.

---

## Scenario 7 — Explicit Backlog Needed

Need to:

- See queue depth
- Retain messages
- Control consumption
- Retry visibly

Choose:

**SQS + Lambda**

instead of relying only on:

**Direct async invocation**

---

## Scenario 8 — 30-Minute Background Job

Caller does not need response.

But processing takes:

30 minutes.

Do NOT choose Lambda just because:

**It is asynchronous**

Lambda still has:

**15-minute limit**

Think:

Fargate / ECS / Batch

---

# Scenario Recognition

Immediately think:

**Asynchronous Lambda Invocation**

when you see:

- Caller does not wait
- Background event processing
- S3 events
- SNS events
- EventBridge events
- Lambda-managed retries
- Async DLQ
- Lambda Destinations

---

# Think SQS + Lambda Instead When You See

- Explicit message queue
- Backpressure
- Queue depth
- Visibility timeout
- Long message retention
- Controlled consumer scaling
- Durable workload backlog

---

# Exam Traps

## Trap 1 — Caller Handles Async Retry

❌

Lambda manages:

**Asynchronous retry behavior**

---

## Trap 2 — SQS Directly Pushes Asynchronously into Lambda

❌

Lambda polls SQS through:

**Event Source Mapping**

---

## Trap 3 — Async Lambda Has No Runtime Limit

❌

Maximum execution is still:

**15 minutes**

---

## Trap 4 — DLQ Handles Successful Invocations

❌

DLQ focuses on:

**Failed events**

---

## Trap 5 — Lambda Destinations Only Work for Failures

❌

They can route:

**Success and failure**

for supported asynchronous invocation patterns.

---

## Trap 6 — Async Means Exactly-Once Processing

❌

Design for:

**Idempotency**

---

## Trap 7 — Lambda Internal Async Queue Replaces SQS

❌

Use SQS when explicit queue semantics are required.

---

## Trap 8 — Async Automatically Protects RDS

❌

Lambda can still scale rapidly.

Think:

- Reserved Concurrency
- RDS Proxy
- SQS buffering

---

# Quick Cheat Sheet

| Exam Clue | Answer |
|---|---|
| Caller Does Not Wait | Asynchronous |
| S3 → Lambda | Async |
| SNS → Lambda | Async |
| EventBridge → Lambda | Async |
| Async Retry Owner | Lambda |
| Preserve Failed Async Event | DLQ |
| Route Success / Failure | Lambda Destinations |
| Need Explicit Queue | SQS |
| SQS → Lambda | Event Source Mapping |
| Kinesis → Lambda | Event Source Mapping |
| DynamoDB Streams → Lambda | Event Source Mapping |
| Prevent Duplicate Effects | Idempotency |
| Long Job >15 Minutes | Not Lambda |

---

# Sync vs Async

| Feature | Synchronous | Asynchronous |
|---|---|---|
| Caller Waits | ✅ | ❌ |
| Immediate Result | ✅ | ❌ |
| Caller Handles Retry | ✅ | ❌ |
| Lambda Handles Retry | ❌ | ✅ |
| Good for APIs | ✅ | Usually Not Primary |
| Good for Background Events | ❌ | ✅ |
| S3 Events | ❌ | ✅ |
| SNS Events | ❌ | ✅ |
| EventBridge Events | ❌ | ✅ |

---

# Async vs Event Source Mapping

| Model | Example |
|---|---|
| Async Push | S3 → Lambda |
| Async Push | SNS → Lambda |
| Async Push | EventBridge → Lambda |
| Event Source Mapping | SQS → Lambda |
| Event Source Mapping | Kinesis → Lambda |
| Event Source Mapping | DynamoDB Streams → Lambda |

---

# Failure Decision Shortcut

Async Lambda fails?  
↓

Need to preserve failed event?

→ **DLQ**

Need to route success and failure differently?

→ **Lambda Destinations**

Need explicit backlog and retry control?

→ **SQS**

---

# Final Exam Rapid-Fire

> **CALLER DOES NOT WAIT**
> → ASYNC
>
> **S3 EVENT**
> → ASYNC LAMBDA
>
> **SNS EVENT**
> → ASYNC LAMBDA
>
> **EVENTBRIDGE EVENT**
> → ASYNC LAMBDA
>
> **WHO RETRIES?**
> → LAMBDA
>
> **FAILED EVENT PARKING**
> → DLQ
>
> **SUCCESS/FAILURE ROUTING**
> → DESTINATIONS
>
> **EXPLICIT BUFFER**
> → SQS
>
> **QUEUE → LAMBDA**
> → EVENT SOURCE MAPPING
>
> **STREAM → LAMBDA**
> → EVENT SOURCE MAPPING
>
> **DUPLICATE SAFETY**
> → IDEMPOTENCY
>
> **MORE THAN 15 MINUTES**
> → NOT LAMBDA

---

## Master Memory Trick

> [!tip] Asynchronous Invocation Master Memory Trick
> Imagine dropping clothes off at a dry cleaner.
>
> You:
>
> **DROP THEM OFF**
>
> then:
>
> **LEAVE**
>
> You do NOT stand there waiting for:
>
> **The cleaning to finish**
>
> That's:
>
> **ASYNCHRONOUS**

If something goes wrong:

> The cleaner:
>
> **TRIES AGAIN**
>
> That's:
>
> **LAMBDA RETRY**

If it still fails:

> Put it in:
>
> **THE PROBLEM BIN**
>
> That's:
>
> **DLQ**

If you want different actions for:

**Success vs Failure**

that's:

**Lambda Destinations**

So remember:

> **ASYNC**
> → SEND + MOVE ON
>
> **RETRY**
> → LAMBDA
>
> **FAILED EVENT**
> → DLQ
>
> **OUTCOME ROUTING**
> → DESTINATIONS
>
> **NEED REAL QUEUE**
> → SQS
>
> **SQS / KINESIS / DYNAMODB STREAMS**
> → EVENT SOURCE MAPPING

And the killer SAA question:

> **"Does the caller need to wait for the function result?"**
>
> NO
>
> → **Asynchronous Invocation**

---

## Related Notes

- [[Lambda]]
- [[Lambda Synchronous Invocations]]
- [[S3]]
- [[SNS]]
- [[20-SAA/10-Messaging/EventBridge]]
- [[SQS]]
- [[20-SAA/10-Messaging/Kinesis Data Streams]]
- [[04-Databases/DynamoDB]]
- [[Step Functions]]
- [[Fargate]]
- [[RDS Proxy]]
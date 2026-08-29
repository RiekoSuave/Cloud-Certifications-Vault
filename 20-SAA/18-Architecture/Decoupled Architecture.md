## Core Concept

Decoupled architecture means:

**Components do not depend directly on each other being available at the same time**

Instead of:

Producer  
↓  
Direct Call  
↓  
Consumer

use an intermediary such as:

- [[SQS]]
- [[SNS]]
- [[EventBridge]]

Architecture:

Producer  
↓  
Messaging Layer  
↓  
Consumer

> [!tip] Memory Trick
> **Decoupling = Put Something Between the Components**

---

# Why Decouple?

Tightly coupled systems can fail when:

**One component becomes slow or unavailable**

Example:

Web Tier  
↓  
Processing Service

If the processing service becomes:

**Overloaded**

the web tier may:

- Wait
- Time out
- Fail requests
- Become overloaded itself

Decoupling breaks:

**That dependency chain**

### Killer Exam Clue

> **A backend component cannot keep up with incoming requests**
>
> → **Decouple with SQS**

---

# Tightly Coupled Architecture

Example:

Application Server  
↓  
Synchronous Request  
↓  
Worker

The application waits for:

**The worker to finish**

If the worker fails:

**The application request may fail**

### Problems

- Failure propagation
- Scaling dependencies
- Traffic spikes
- Timeouts
- Reduced resilience

### Memory Trick

**Tight Coupling = If You Fail, I Fail**

---

# Decoupled Architecture

Example:

Application  
↓  
[[SQS]]  
↓  
Workers

The producer:

**Places work into the queue**

and continues.

Workers process:

**Messages independently**

### Benefits

- Independent scaling
- Better fault tolerance
- Traffic buffering
- Improved resilience
- Asynchronous processing

### Memory Trick

**Queue = Separation**

---

# Asynchronous Processing

A common decoupled pattern is:

**Asynchronous processing**

The producer does NOT need to wait for:

**The task to finish**

Example:

User Uploads Video  
↓  
Application Stores Request  
↓  
SQS  
↓  
Video Processing Workers

The user does not wait for:

**The entire video-processing job**

### Killer Exam Clue

> **Long-running work should occur independently of the user request**
>
> → **Asynchronous architecture**

---

# Synchronous vs Asynchronous

## Synchronous

Producer:

**Waits for response**

Architecture:

A  
↓  
B  
↓  
Response  
↓  
A continues

## Asynchronous

Producer:

**Submits work and continues**

Architecture:

A  
↓  
Queue/Event  
↓  
B processes later

### Killer Shortcut

**Must respond immediately**
→ Synchronous may be appropriate

**Can process later**
→ Asynchronous

---

# SQS

[[SQS]] is one of the most important decoupling services.

Use it to:

**Buffer work between producers and consumers**

Architecture:

Producer  
↓  
SQS  
↓  
Consumers

### Killer Exam Clue

> **Traffic arrives faster than workers can process it**
>
> → **SQS**

---

# Queue as a Buffer

Suppose:

Producer rate:

**10,000 messages/minute**

Consumer capacity:

**4,000 messages/minute**

Without a queue:

**Requests may fail**

With SQS:

Messages accumulate temporarily  
↓  
Consumers process backlog  
↓  
System catches up

### Memory Trick

**SQS = Shock Absorber**

---

# Independent Scaling

With SQS:

Producer tier can scale based on:

**Request volume**

Consumer tier can scale based on:

**Queue depth**

These layers no longer need to:

**Scale together**

### Killer Exam Principle

> **Decoupling allows each component to scale independently**

---

# Auto Scaling Consumers

A common architecture:

SQS  
↓  
CloudWatch Metric  
↓  
[[Auto Scaling]]  
↓  
Worker Fleet

Example:

Queue Depth Increases  
↓  
Scale Out Workers

Queue Depth Decreases  
↓  
Scale In Workers

### Killer Exam Clue

> **Scale worker EC2 instances based on queue backlog**
>
> → **SQS + Auto Scaling**

---

# Queue Depth

One important metric is:

**Approximate number of messages waiting**

A growing queue may indicate:

**Consumers are falling behind**

### Exam Principle

> **Queue depth can drive consumer scaling decisions**

---

# Message Durability

SQS stores messages:

**Durably**

across AWS infrastructure.

This helps prevent work from being lost simply because:

**A consumer is temporarily unavailable**

### Memory Trick

**Consumer Down ≠ Message Gone**

---

# Visibility Timeout

When a consumer receives an SQS message:

The message becomes temporarily:

**Invisible to other consumers**

This period is the:

**Visibility Timeout**

Architecture:

Consumer Receives Message  
↓  
Message Hidden  
↓  
Consumer Processes  
↓  
Deletes Message

### Killer Exam Clue

> **Same message is being processed by multiple workers because processing takes longer than visibility timeout**
>
> → **Increase Visibility Timeout**

---

# Visibility Timeout Failure

Suppose:

Visibility Timeout:

30 seconds

Processing Time:

2 minutes

After 30 seconds:

The message becomes:

**Visible again**

Another consumer may receive:

**The same message**

### Memory Trick

**Processing Time Must Fit Inside Visibility Timeout**

---

# Message Deletion

After successful processing:

The consumer must:

**Delete the message**

Otherwise the message can:

**Become visible again**

and be processed:

**Again**

### Exam Principle

> **Receive does not permanently remove an SQS message**

---

# At-Least-Once Delivery

SQS Standard queues provide:

**At-least-once delivery**

This means:

A message can occasionally be delivered:

**More than once**

Therefore consumers should ideally be:

**Idempotent**

---

# Idempotency

An:

**Idempotent operation**

can safely execute multiple times without creating:

**Incorrect duplicate effects**

Example:

Bad:

Charge credit card every time message is received

Better:

Use transaction/order ID to ensure:

**The same order is charged once**

### Killer Exam Principle

> **SQS consumers should tolerate duplicate message delivery**

---

# Standard Queue

SQS Standard provides:

- Very high throughput
- At-least-once delivery
- Best-effort ordering

### Think Standard When You See

- Maximum throughput
- Ordering not strict
- Duplicate tolerance

---

# FIFO Queue

SQS FIFO provides:

**First-In-First-Out processing**

with features designed for:

- Strict ordering
- Deduplication

### Killer Exam Clue

> **Messages must be processed in exact order**
>
> → **SQS FIFO**

### Memory Trick

**FIFO = Order Matters**

---

# Standard vs FIFO

| Requirement | Standard | FIFO |
|---|---:|---:|
| Very High Throughput | ✅ | More Controlled |
| Strict Ordering | ❌ | ✅ |
| Possible Duplicate Delivery | ✅ | Deduplication Features |
| Simple Decoupling | ✅ | ✅ |
| Order-Critical Workflows | ❌ | ✅ |

---

# Dead-Letter Queue

A:

**Dead-Letter Queue — DLQ**

stores messages that:

**Repeatedly fail processing**

Architecture:

Main Queue  
↓  
Processing Failure  
↓  
Retry  
↓  
Retry  
↓  
DLQ

### Killer Exam Clue

> **Need to isolate messages that repeatedly fail processing**
>
> → **Dead-Letter Queue**

### Memory Trick

**DLQ = Parking Lot for Bad Messages**

---

# Redrive Policy

A:

**Redrive Policy**

determines when a message should move from:

**The source queue**

to:

**The DLQ**

after repeated receives.

### Exam Principle

> **Do not let permanently failing messages block normal processing**

---

# SQS Long Polling

Long polling allows consumers to:

**Wait for messages**

instead of repeatedly making empty requests.

Benefits:

- Fewer empty responses
- Lower API usage
- More efficient consumers

### Killer Exam Clue

> **Reduce unnecessary empty SQS receive calls**
>
> → **Long Polling**

---

# Short Polling

Short polling returns:

**Immediately**

even if:

**No messages are available**

This can create:

**More empty receives**

---

# SQS Delay Queue

A:

**Delay Queue**

makes newly sent messages:

**Invisible for a configured period**

before they become available to consumers.

### Killer Exam Clue

> **Message should not be processed immediately after being sent**
>
> → **Delay Queue**

---

# SNS

[[SNS]] solves a different messaging problem.

SNS provides:

**Publish/Subscribe fan-out**

Architecture:

Publisher  
↓  
SNS Topic  
↓  
├── Subscriber A
├── Subscriber B
└── Subscriber C

### Killer Exam Clue

> **One event must be delivered to multiple independent consumers**
>
> → **SNS**

---

# SNS Fan-Out

A classic architecture:

Application  
↓  
SNS Topic  
↓  
├── SQS Orders
├── SQS Analytics
└── Lambda Notifications

Each consumer receives:

**Its own copy of the event**

### Memory Trick

**SNS = One-to-Many**

---

# SNS + SQS

This is one of the most important architecture combinations.

Architecture:

Producer  
↓  
SNS  
↓  
├── SQS Queue A
├── SQS Queue B
└── SQS Queue C

SNS provides:

**Fan-out**

SQS provides:

**Buffering and durability**

### Killer Exam Clue

> **Multiple applications must independently process the same event without losing messages when consumers are down**
>
> → **SNS + SQS**

---

# Why SNS + SQS?

Suppose one order should trigger:

- Billing
- Shipping
- Analytics

Direct architecture:

Order Service  
↓  
Billing  
↓  
Shipping  
↓  
Analytics

This creates:

**Tight coupling**

Better:

Order Service  
↓  
SNS  
↓  
Separate SQS Queues  
↓  
Independent Consumers

### Memory Trick

**SNS Copies**

**SQS Holds**

---

# EventBridge

[[EventBridge]] provides:

**Event routing based on rules**

Architecture:

Event Producer  
↓  
EventBridge Event Bus  
↓  
Rules  
↓  
Targets

Think:

- AWS service events
- SaaS events
- Application events
- Content-based routing

### Killer Exam Clue

> **Route different events to different targets based on event content**
>
> → **EventBridge**

---

# EventBridge Rules

Rules examine:

**Event patterns**

and determine:

**Which targets receive each event**

Example:

EC2 State Change  
↓  
EventBridge Rule  
↓  
Lambda

### Memory Trick

**EventBridge = If Event Looks Like This, Send It There**

---

# EventBridge vs SNS

## SNS

Think:

**Publish to subscribers**

## EventBridge

Think:

**Route events using rules**

### Killer Shortcut

Simple fan-out  
→ SNS

Content-based event routing  
→ EventBridge

---

# EventBridge vs SQS

## SQS

Think:

**Store work until consumer processes it**

## EventBridge

Think:

**Route events**

### Memory Trick

**SQS = Wait**

**EventBridge = Route**

---

# Messaging Decision Map

Need:

**Buffer work**

→ SQS

Need:

**One message to many subscribers**

→ SNS

Need:

**Route events based on content**

→ EventBridge

Need:

**Fan-out + buffering**

→ SNS + SQS

---

# Decoupling Failure Domains

In tightly coupled systems:

Service A failure  
↓  
Service B waits  
↓  
Service C fails  
↓  
Whole workflow fails

In decoupled systems:

Service A  
↓  
Queue  
↓  
Service B unavailable

Messages remain:

**In the queue**

When B recovers:

**Processing continues**

### Killer Exam Principle

> **Queues prevent temporary downstream failure from immediately becoming upstream failure**

---

# Backpressure

Backpressure occurs when:

**Consumers cannot process work as quickly as producers generate it**

Queues absorb:

**Temporary backpressure**

### Killer Exam Clue

> **Backend processing capacity varies and request spikes must not be lost**
>
> → **Queue-based buffering**

---

# Decoupling and Availability

Decoupled systems can continue accepting:

**Work**

even when downstream systems are:

**Temporarily unavailable**

This improves:

**Overall resilience**

---

# Decoupling and Scalability

Each component can scale using:

**Its own workload signal**

Example:

Web Tier  
→ Scale on requests

Worker Tier  
→ Scale on queue depth

Database  
→ Scale independently

### Memory Trick

**Decouple First, Scale Separately**

---

# Decoupling and Microservices

Microservices architectures benefit from:

**Loose coupling**

Services communicate through:

- Queues
- Events
- APIs

rather than maintaining unnecessary:

**Hard dependencies**

### Exam Principle

> **Loose coupling helps services deploy and scale independently**

---

# Lambda + SQS

[[Lambda]] can consume:

**SQS messages**

Architecture:

Producer  
↓  
SQS  
↓  
Lambda

This provides:

**Serverless asynchronous processing**

### Killer Exam Clue

> **Need serverless processing of queued work**
>
> → **SQS + Lambda**

---

# Lambda + SNS

SNS can invoke:

**Lambda**

when events are published.

Architecture:

Publisher  
↓  
SNS  
↓  
Lambda

Use when:

**A Lambda function should react to published events**

---

# Lambda + EventBridge

EventBridge can invoke:

**Lambda**

based on:

**Event rules**

Example:

AWS Event  
↓  
EventBridge  
↓  
Lambda

This is common in:

**Event-driven automation**

---

# Decoupling Long-Running Work

Do not keep:

**A synchronous web request open**

for long-running processing if the user does not need:

**Immediate completion**

Better:

Request  
↓  
Queue Job  
↓  
Return Job ID  
↓  
Process Asynchronously

### Killer Exam Principle

> **Long-running tasks often belong behind a queue**

---

# Status Tracking

Asynchronous applications may return:

**A job ID**

and allow clients to check:

**Processing status**

This avoids:

**Long synchronous timeouts**

---

# Database Decoupling

Applications may use messaging to avoid:

**Large synchronized write spikes**

Example:

Incoming Events  
↓  
SQS  
↓  
Workers  
↓  
Database

The workers write at:

**A manageable rate**

### Killer Exam Clue

> **Database is overwhelmed by sudden bursts of write requests**
>
> → **Buffer writes with SQS**

---

# Batch Processing

SQS works well for:

**Distributed batch workloads**

Example:

Jobs  
↓  
Queue  
↓  
Worker Fleet

Workers can process:

**Independent jobs in parallel**

---

# Image Processing Architecture

Example:

User  
↓  
Upload Image to S3  
↓  
Event  
↓  
Queue  
↓  
Lambda / Worker  
↓  
Process Image

This separates:

**Upload**

from:

**Processing**

### Killer Exam Pattern

> **User upload should succeed even if image processing is delayed**
>
> → **Decouple processing**

---

# Order Processing Architecture

Order Created  
↓  
SNS  
↓  
├── Billing Queue
├── Shipping Queue
└── Analytics Queue

Each subsystem:

**Processes independently**

### Memory Trick

**One Order, Many Reactions = SNS + SQS**

---

# Decoupling vs Load Balancing

These solve different problems.

## Load Balancer

Distributes:

**Synchronous network requests**

## Queue

Buffers:

**Asynchronous work**

### Killer Shortcut

Need requests spread across web servers  
→ Load Balancer

Need work stored until workers are ready  
→ SQS

---

# Decoupling vs Auto Scaling

Auto Scaling changes:

**Capacity**

Decoupling changes:

**Dependency structure**

They work well:

**Together**

Example:

SQS backlog  
↓  
Auto Scaling  
↓  
More Workers

---

# Architecture Thinking

## Scenario 1 — Traffic Spike

Website suddenly generates:

100,000 image-processing jobs.

Workers can only process:

10,000 immediately.

Choose:

**SQS**

---

## Scenario 2 — Three Consumers

Order event must go to:

- Shipping
- Billing
- Analytics

Choose:

**SNS fan-out**

For durable independent processing:

**SNS + SQS**

---

## Scenario 3 — Failed Messages

Some jobs repeatedly fail due to:

**Bad input**

Choose:

**Dead-Letter Queue**

---

## Scenario 4 — Duplicate Processing

SQS Standard occasionally delivers:

**Same message twice**

Application must not charge customer twice.

Design consumer to be:

**Idempotent**

---

## Scenario 5 — Strict Order

Banking workflow requires:

Messages processed in:

**Exact order**

Choose:

**SQS FIFO**

---

## Scenario 6 — Long Processing

Worker takes:

5 minutes

but SQS Visibility Timeout is:

30 seconds.

Messages are duplicated.

Increase:

**Visibility Timeout**

---

## Scenario 7 — Empty Polling

Workers frequently call SQS and receive:

**No messages**

Use:

**Long Polling**

---

## Scenario 8 — Event Routing

Security events of different types must go to:

**Different automated targets**

Choose:

**EventBridge**

---

# Scenario Recognition

Immediately think:

**SQS**

when you see:

- Buffer
- Decouple
- Backlog
- Traffic spike
- Worker processing
- Asynchronous jobs
- Consumer temporarily unavailable

---

## Think SNS When You See

- Fan-out
- Broadcast
- Multiple subscribers
- One event to many consumers

---

## Think EventBridge When You See

- Event rules
- Event bus
- Content-based routing
- AWS/SaaS events

---

## Think DLQ When You See

- Repeated failures
- Poison message
- Troubleshoot failed processing

---

# Exam Traps

## Trap 1 — SNS Stores Messages Until Consumers Recover

❌

For durable buffering:

Think:

**SQS**

A common solution:

**SNS + SQS**

---

## Trap 2 — SQS Is Primarily a Broadcast Service

❌

Think:

**SNS**

SQS is:

**Queue-based messaging**

---

## Trap 3 — Receive Deletes an SQS Message

❌

Consumer must:

**Delete after successful processing**

---

## Trap 4 — SQS Standard Guarantees Exact Ordering

❌

Think:

**FIFO**

---

## Trap 5 — A Message Can Never Be Delivered Twice

❌

Standard queues provide:

**At-least-once delivery**

Design:

**Idempotent consumers**

---

## Trap 6 — Visibility Timeout Controls Message Retention

❌

Visibility Timeout controls:

**How long a received message is hidden from other consumers**

---

## Trap 7 — EventBridge and SQS Solve the Same Problem

❌

SQS:

**Buffers**

EventBridge:

**Routes**

---

# Quick Cheat Sheet

| Exam Clue | Answer |
|---|---|
| Decouple Components | SQS |
| Buffer Traffic Spike | SQS |
| Async Processing | SQS |
| One-to-Many | SNS |
| Fan-Out + Durability | SNS + SQS |
| Event-Based Routing | EventBridge |
| Strict Ordering | SQS FIFO |
| Duplicate-Tolerant Consumer | Idempotency |
| Failed Messages | DLQ |
| Long Processing | Increase Visibility Timeout |
| Reduce Empty Receives | Long Polling |
| Scale Workers | Queue Depth + Auto Scaling |

---

# Messaging Decision Tree

Need:

**Store work until processed?**

→ SQS

Need:

**Send one event to many consumers?**

→ SNS

Need:

**Both fan-out and buffering?**

→ SNS + SQS

Need:

**Route different event types to different targets?**

→ EventBridge

Need:

**Exact processing order?**

→ SQS FIFO

Need:

**Handle repeatedly failing messages?**

→ DLQ

---

# Final Exam Rapid-Fire

> **DECOUPLE**
> → SQS
>
> **BUFFER**
> → SQS
>
> **TRAFFIC SPIKE**
> → SQS
>
> **ASYNC JOB**
> → SQS
>
> **FAN-OUT**
> → SNS
>
> **FAN-OUT + BUFFER**
> → SNS + SQS
>
> **EVENT ROUTING**
> → EVENTBRIDGE
>
> **STRICT ORDER**
> → FIFO
>
> **DUPLICATE SAFETY**
> → IDEMPOTENCY
>
> **FAILED MESSAGE**
> → DLQ
>
> **MESSAGE HIDDEN DURING PROCESSING**
> → VISIBILITY TIMEOUT
>
> **FEWER EMPTY RECEIVES**
> → LONG POLLING
>
> **WORKER SCALING**
> → QUEUE DEPTH

---

## Master Memory Trick

> [!tip] Decoupled Architecture Master Memory Trick
> Imagine a busy restaurant.
>
> Customers give orders directly to:
>
> **THE COOK**
>
> The cook becomes overwhelmed.
>
> Customers cannot place new orders until:
>
> **THE COOK CATCHES UP**
>
> That's:
>
> **TIGHT COUPLING**
>
> Now put:
>
> **AN ORDER TICKET RACK**
>
> between the cashier and cooks.
>
> The cashier can keep accepting orders.
>
> Cooks pull tickets when:
>
> **THEY'RE READY**
>
> That ticket rack is:
>
> **SQS**
>
> Now one order also needs to notify:
>
> **BILLING**
>
> **SHIPPING**
>
> **ANALYTICS**
>
> That's:
>
> **SNS FAN-OUT**

So remember:

> **SQS**
> → HOLD THE WORK
>
> **SNS**
> → COPY THE EVENT
>
> **EVENTBRIDGE**
> → ROUTE THE EVENT
>
> **DLQ**
> → HOLD FAILED WORK
>
> **FIFO**
> → KEEP ORDER
>
> **IDEMPOTENT**
> → DUPLICATES DON'T HURT
>
> **DECOUPLING**
> → COMPONENTS FAIL AND SCALE INDEPENDENTLY

And the killer SAA question:

> **"Can these components continue operating independently if one side becomes slow, overloaded, or temporarily unavailable?"**
>
> NO
>
> → **Decouple them**

---

## Related Notes

- [[Architecture Principles]]
- [[SQS]]
- [[SNS]]
- [[EventBridge]]
- [[Auto Scaling]]
- [[Lambda]]
- [[Application Load Balancer]]
- [[CloudWatch]]
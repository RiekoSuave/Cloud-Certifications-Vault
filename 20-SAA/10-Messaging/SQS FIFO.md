## What Problem Does It Solve?

[[SQS FIFO]] is an Amazon SQS queue type designed for workloads that require:

- **Strict message ordering**
- **Message deduplication**
- **Exactly-once processing semantics**

FIFO means:

**First-In-First-Out**

It solves the problem:

> **"How do I decouple applications with SQS when the order of operations matters and duplicate messages must be prevented?"**

Architecture:

Producer  
↓  
Message 1  
↓  
Message 2  
↓  
Message 3  
↓  
SQS FIFO  
↓  
Consumer  
↓  
1 → 2 → 3

> [!tip] Memory Trick
> **FIFO = FIRST IN, FIRST OUT**
>
> Think:
>
> **ORDER + DEDUPLICATION**

---

## When Do You Need FIFO?

Use FIFO when:

**Sequence matters**

Examples:

- Banking transactions
- Order processing
- Inventory updates
- Commands
- Workflow steps
- Financial operations
- State changes

Example:

Account Balance = 1,000

Messages:

1. Deposit 500
2. Withdraw 1,200

Correct order:

1,000  
↓  
+500  
↓  
1,500  
↓  
-1,200  
↓  
300

If processed out of order:

1,000  
↓  
-1,200  
↓  
Potential Failure

The sequence can change:

**The outcome**

---

## FIFO Queue Naming

FIFO queue names must end with:

`.fifo`

Example:

`orders.fifo`

`payments.fifo`

`inventory.fifo`

### Exam Clue

If you see:

`.fifo`

immediately think:

**SQS FIFO Queue**

---

## FIFO vs Standard

[[SQS]] provides two primary queue types:

- Standard
- FIFO

### Standard

Optimized for:

**Very high throughput**

Provides:

- At-least-once delivery
- Best-effort ordering

### FIFO

Optimized for:

**Ordering + deduplication**

Provides:

- Strict ordering within message groups
- Deduplication
- Exactly-once processing semantics

---

## Standard vs FIFO Quick Comparison

| Feature | Standard | FIFO |
|---|---|---|
| Ordering | Best Effort | Strict Within Message Group |
| Delivery Model | At Least Once | Exactly-Once Processing Semantics |
| Duplicate Messages | Possible | Deduplication |
| Message Groups | ❌ | ✅ |
| `.fifo` Suffix | ❌ | ✅ |
| Throughput Focus | Maximum Scale | Ordered Processing |
| Best For | Independent Work | Sequence-Sensitive Work |

> [!tip] Exam Shortcut
> **Maximum scale + no ordering requirement**
> → Standard
>
> **Strict order + deduplication**
> → FIFO

---

## Message Groups

One of the most important FIFO concepts is:

**MessageGroupId**

Every message sent to a FIFO queue must belong to:

**A message group**

Messages with the same:

`MessageGroupId`

are processed:

**In strict order**

Example:

MessageGroupId = `Customer-A`

A1  
↓  
A2  
↓  
A3

Processing order:

A1  
↓  
A2  
↓  
A3

---

## Why Message Groups Matter

Without multiple message groups:

A FIFO workload can become highly:

**Sequential**

But different message groups can be processed:

**In parallel**

Example:

FIFO Queue

Customer A:

A1  
↓  
A2  
↓  
A3

Customer B:

B1  
↓  
B2  
↓  
B3

Customer C:

C1  
↓  
C2  
↓  
C3

Ordering is maintained:

**Within each customer**

while different customers can be processed:

**Concurrently**

---

## Message Group Architecture

Think:

Producer  
↓  
FIFO Queue  
↓

Group A  
→ A1 → A2 → A3

Group B  
→ B1 → B2 → B3

Group C  
→ C1 → C2 → C3

Different groups:

**Parallel**

Same group:

**Sequential**

> [!tip] Memory Trick
> **Same Group = Same Line**
>
> **Different Groups = Different Lines**

---

## FIFO Throughput and Message Groups

A common mistake is thinking:

> **FIFO means everything must be processed one message at a time.**

Not necessarily.

Using multiple:

**MessageGroupId values**

allows:

**Parallel processing**

while preserving ordering inside each group.

### SAA Architecture Principle

> If you need FIFO ordering AND scalability:
>
> **Use multiple message groups where the workload permits it.**

---

## Deduplication

FIFO queues help prevent:

**Duplicate message processing**

using:

**Deduplication IDs**

A message can include:

`MessageDeduplicationId`

SQS uses this value to determine whether a message:

**Has already been accepted recently**

---

## Deduplication Interval

FIFO deduplication operates over a:

**5-minute deduplication interval**

If SQS receives another message with the same:

`MessageDeduplicationId`

during that interval:

The duplicate is:

**Accepted successfully but not delivered again**

### Memory Trick

**FIFO Dedup Window = 5 Minutes**

---

## MessageDeduplicationId

Example:

Producer sends:

Order ID:

`ORDER-12345`

MessageDeduplicationId:

`ORDER-12345`

If the producer accidentally retries:

`ORDER-12345`

within the deduplication interval:

SQS recognizes:

**The duplicate**

and avoids introducing another copy for delivery.

---

## Content-Based Deduplication

FIFO queues can use:

**Content-Based Deduplication**

When enabled:

SQS generates the deduplication ID using a hash based on the:

**Message body**

This reduces the need for the producer to manually supply:

`MessageDeduplicationId`

### Important Detail

Content-based deduplication is based on:

**The message body**

not message attributes.

---

## Explicit Deduplication ID

Instead of content-based deduplication:

The producer can explicitly provide:

`MessageDeduplicationId`

This is useful when the application already has a unique identifier such as:

- Transaction ID
- Order ID
- Request ID
- Operation ID

### Exam Pattern

> **Application already has a unique transaction identifier**
>
> → Use it as the deduplication ID.

---

## MessageGroupId vs MessageDeduplicationId

These two are easy to confuse.

### MessageGroupId

Controls:

**Ordering**

Question:

> Which ordered sequence does this message belong to?

### MessageDeduplicationId

Controls:

**Deduplication**

Question:

> Have I already received this logical message?

### Memory Trick

**GROUP = ORDER**

**DEDUP = DUPLICATES**

---

## Example

Suppose:

Customer:

`Customer-100`

places:

`Order-555`

You might use:

MessageGroupId:

`Customer-100`

MessageDeduplicationId:

`Order-555`

Meaning:

> Keep this customer's messages ordered.

and:

> Don't accept the same logical order twice during the deduplication interval.

---

## Exactly-Once Processing Semantics

FIFO queues provide:

**Exactly-once processing semantics**

through:

**Deduplication**

This prevents duplicate messages from being introduced into the queue during the deduplication interval.

> [!warning] Architecture Reminder
> Do not interpret this as:
>
> **"My application can never perform a business operation twice under any possible failure condition."**
>
> Consumers should still be designed carefully, and idempotency remains a strong distributed-system practice.

---

## FIFO Consumers

Consumers still:

**Poll**

the queue.

Architecture:

Producer  
↓  
FIFO Queue  
↑  
Consumer Polls

Just like Standard SQS:

Messages are not normally pushed directly to traditional consumers.

---

## Visibility Timeout Still Applies

FIFO queues still use:

**Visibility Timeout**

Consumer receives message  
↓  
Message becomes invisible  
↓  
Consumer processes  
↓  
Consumer deletes message

If processing fails:

Visibility Timeout Expires  
↓  
Message becomes visible again

---

## FIFO Ordering + Visibility Timeout

Suppose a message group contains:

A1  
↓  
A2  
↓  
A3

Consumer receives:

A1

While A1 is:

**In flight**

SQS will not deliver:

A2

from the same message group until A1 is:

- Deleted
- Or becomes visible again after the visibility timeout

This preserves:

**Ordering**

---

## Head-of-Line Blocking

This can create:

**Head-of-line blocking**

Example:

A1  
↓  
A2  
↓  
A3

If A1 takes:

10 minutes

A2 and A3 must wait.

### Solution

Where architecturally possible:

Use:

**Multiple Message Groups**

instead of placing unrelated messages into:

**One group**

---

## FIFO + Dead-Letter Queue

FIFO queues can use:

**Dead-Letter Queues**

If a message repeatedly fails:

FIFO Queue  
↓  
Retry  
↓  
Retry  
↓  
maxReceiveCount  
↓  
FIFO DLQ

### Important

FIFO source queue:

→ FIFO DLQ

Standard source queue:

→ Standard DLQ

---

## FIFO + Lambda

[[02-Compute/Lambda]] can process:

**SQS FIFO queues**

Architecture:

Producer  
↓  
SQS FIFO  
↓  
Lambda

Lambda preserves:

**Message ordering within each message group**

Different message groups can allow:

**Concurrent processing**

### Exam Pattern

> **Serverless processing + strict order per customer**
>
> → SQS FIFO + Lambda + MessageGroupId

---

## FIFO Fan-Out

If multiple independent applications each need:

**Their own ordered copy**

of an event stream:

A common pattern is:

[[SNS FIFO]]  
↓  
├── SQS FIFO Queue A
├── SQS FIFO Queue B
└── SQS FIFO Queue C

Each application gets:

**Its own FIFO queue**

while preserving:

**Ordered fan-out**

---

## Standard Fan-Out vs FIFO Fan-Out

### Standard

[[SNS]]  
↓  
Multiple Standard SQS Queues

Think:

**Massive fan-out**

### FIFO

[[SNS FIFO]]  
↓  
Multiple SQS FIFO Queues

Think:

**Ordered fan-out**

---

## FIFO vs Kinesis

Both can involve:

**Ordered data**

but they solve different problems.

### SQS FIFO

Think:

- Message queue
- Work distribution
- Message processed and deleted
- Ordering
- Deduplication
- Decoupling

### [[Kinesis]]

Think:

- Data stream
- Real-time analytics
- Replay
- Multiple consumers
- Records retained
- Ordered within shards

### Exam Shortcut

**Ordered work queue**
→ SQS FIFO

**Ordered real-time stream**
→ Kinesis

---

## FIFO vs EventBridge

### FIFO

Think:

**Ordered queued work**

### [[20-SAA/10-Messaging/EventBridge]]

Think:

**Event routing**

using:

- Rules
- Event patterns
- Targets

### Exam Shortcut

**Must wait in strict order**
→ FIFO

**Route events based on event content**
→ EventBridge

---

## Architecture Thinking

### Scenario 1 — Financial Transactions

A banking application must process account transactions:

**In order**

and prevent duplicate messages.

**Choose → SQS FIFO**

---

### Scenario 2 — Order State Changes

Messages arrive:

1. Order Created
2. Payment Confirmed
3. Order Shipped
4. Order Delivered

These must remain:

**Sequential**

**Choose → SQS FIFO**

---

### Scenario 3 — Multiple Customers

Each customer's operations must be ordered, but different customers should process concurrently.

Use:

**Customer ID as MessageGroupId**

Example:

Customer A  
→ Group A

Customer B  
→ Group B

Customer C  
→ Group C

---

### Scenario 4 — Duplicate Producer Retries

A producer retries a transaction because it did not receive the response.

Use:

**MessageDeduplicationId**

to help prevent duplicate messages.

---

### Scenario 5 — Maximum Throughput, No Ordering

A workload has millions of unrelated jobs and ordering does not matter.

Do NOT choose FIFO simply because:

**FIFO sounds safer**

Choose:

**SQS Standard**

---

### Scenario 6 — Real-Time Analytics Stream

Millions of clickstream records must:

- Remain available for multiple consumers
- Support streaming analytics
- Be replayable

Do NOT choose SQS FIFO.

Think:

[[Kinesis]]

---

### Scenario 7 — Ordered Serverless Processing

Messages must be processed in order by serverless functions.

**Choose → SQS FIFO + Lambda**

---

### Scenario 8 — Ordered Fan-Out

Multiple applications each need their own copy of ordered events.

**Choose → SNS FIFO + multiple SQS FIFO queues**

---

## Scenario Recognition

Immediately think:

[[SQS FIFO]]

when you see:

- Strict ordering
- First-in-first-out
- Deduplication
- Duplicate prevention
- Sequence matters
- `.fifo`
- MessageGroupId
- MessageDeduplicationId
- Financial transactions
- Ordered commands

---

## Exam Traps

### Trap 1 — Standard SQS Guarantees Strict Ordering

False.

Standard provides:

**Best-effort ordering**

Need strict ordering?

→ FIFO

---

### Trap 2 — FIFO Means No Parallel Processing

False.

Different:

**Message Groups**

can be processed concurrently.

---

### Trap 3 — MessageGroupId Prevents Duplicates

False.

MessageGroupId:

**Controls ordering**

MessageDeduplicationId:

**Controls deduplication**

---

### Trap 4 — MessageDeduplicationId Controls Ordering

False.

Deduplication ID:

**Identifies duplicate messages**

Group ID:

**Identifies ordered sequences**

---

### Trap 5 — Content-Based Deduplication Uses Message Attributes

False.

It is based on:

**Message body content**

---

### Trap 6 — FIFO Removes the Need for Visibility Timeout

False.

FIFO still uses:

**Visibility Timeout**

---

### Trap 7 — One Message Group Maximizes FIFO Throughput

False.

One group forces:

**Sequential processing**

Multiple groups can increase:

**Parallelism**

---

### Trap 8 — FIFO Is Always Better Than Standard

False.

FIFO should be chosen when you actually need:

- Ordering
- Deduplication

If messages are independent and maximum scale matters:

**Standard may be better**

---

## FIFO Quick Cheat Sheet

| Exam Clue | Answer |
|---|---|
| Strict Ordering | FIFO |
| Duplicate Prevention | FIFO |
| Queue Name | `.fifo` |
| Ordering Identifier | MessageGroupId |
| Deduplication Identifier | MessageDeduplicationId |
| Dedup Window | 5 Minutes |
| Automatic Body-Based Dedup | Content-Based Deduplication |
| Parallel Ordered Workloads | Multiple Message Groups |
| Ordered Serverless Processing | FIFO + Lambda |
| Ordered Fan-Out | SNS FIFO + SQS FIFO |
| Maximum Unordered Throughput | Standard |
| Real-Time Replayable Stream | Kinesis |

---

## Standard vs FIFO Final Review

| Requirement | Standard | FIFO |
|---|---:|---:|
| Best-Effort Ordering | ✅ | — |
| Strict Ordering | ❌ | ✅ |
| At-Least-Once Delivery | ✅ | — |
| Deduplication | ❌ | ✅ |
| MessageGroupId | ❌ | ✅ |
| MessageDeduplicationId | ❌ | ✅ |
| `.fifo` Name | ❌ | ✅ |
| Massive Independent Workloads | ✅ | Possible |
| Sequence-Sensitive Workloads | ❌ | ✅ |

---

## Master Memory Trick

> [!tip] SQS FIFO Master Memory Trick
> Imagine a bank with multiple teller lines.
>
> Each customer has transactions that must happen:
>
> **IN ORDER**
>
> That's:
>
> **MessageGroupId**
>
> Customer A:
>
> A1 → A2 → A3
>
> Customer B:
>
> B1 → B2 → B3
>
> Customer A and Customer B can process:
>
> **IN PARALLEL**
>
> but each customer's own operations stay:
>
> **IN ORDER**
>
> Then imagine the same transaction accidentally gets submitted twice.
>
> That's where:
>
> **MessageDeduplicationId**
>
> helps identify:
>
> **THE DUPLICATE**

Remember:

> **GROUP = ORDER**
>
> **DEDUP = DUPLICATES**

And the big exam choice:

> **DON'T CARE ABOUT ORDER?**
> → SQS Standard
>
> **ORDER MATTERS?**
> → SQS FIFO
>
> **ORDERED STREAM + REPLAY?**
> → Kinesis

---

## Related Notes

- [[SQS]]
- [[SNS]]
- [[SNS FIFO]]
- [[Kinesis]]
- [[02-Compute/Lambda]]
- [[Dead-Letter Queue]]
- [[Visibility Timeout]]
- [[Long Polling]]
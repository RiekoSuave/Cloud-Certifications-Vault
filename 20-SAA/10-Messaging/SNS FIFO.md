## What Problem Does It Solve?

[[SNS FIFO]] is an Amazon SNS topic type designed for:

- **Ordered message delivery**
- **Message deduplication**
- **Publish/subscribe fan-out**

It solves the problem of:

> **"How can I publish one event to multiple subscribers while preserving message order and preventing duplicates?"**

Architecture:

Producer  
↓  
SNS FIFO Topic  
↓  
├── SQS FIFO Queue A
├── SQS FIFO Queue B
└── SQS FIFO Queue C

Each subscriber receives:

**Its own ordered copy**

> [!tip] Memory Trick
> **SNS FIFO = Ordered Broadcast**

---

## FIFO Means First-In-First-Out

FIFO stands for:

**First-In-First-Out**

If messages are published:

1  
↓  
2  
↓  
3  
↓  
4

SNS FIFO preserves their ordering:

**Within the same message group**

This makes SNS FIFO useful when:

**Event sequence matters**

---

## Why SNS FIFO Exists

Standard SNS is excellent for:

**Fan-Out**

but does not provide the same strict FIFO behavior required by:

**Sequence-sensitive applications**

SNS FIFO combines:

**SNS Pub/Sub**

with:

**FIFO ordering and deduplication**

Think:

SNS Standard  
→ Broadcast

SNS FIFO  
→ Ordered Broadcast

---

## SNS FIFO Core Features

The Maarek slides highlight features similar to:

[[SQS FIFO]]

including:

- Ordering using Message Group ID
- Deduplication using Deduplication ID
- Content-based deduplication
- FIFO-aware fan-out

> [!tip] Memory Trick
> **SNS FIFO borrows the FIFO brain from SQS FIFO**

---

## MessageGroupId

SNS FIFO uses:

**MessageGroupId**

to control:

**Message ordering**

Messages within the same group are delivered:

**In order**

Example:

MessageGroupId:

`Customer-A`

Messages:

A1  
↓  
A2  
↓  
A3

Delivery:

A1  
↓  
A2  
↓  
A3

### Memory Trick

**GROUP = ORDER**

---

## Multiple Message Groups

Different message groups can represent:

**Independent ordered sequences**

Example:

Customer A:

A1  
→ A2  
→ A3

Customer B:

B1  
→ B2  
→ B3

Customer C:

C1  
→ C2  
→ C3

Ordering is maintained:

**Within each group**

while unrelated groups can provide:

**Parallelism**

---

## Why Message Groups Matter

Suppose all messages use:

**One MessageGroupId**

Then all messages belong to:

**One ordered stream**

If instead your application can divide messages by:

- Customer
- Account
- Order
- Device

you can create:

**Multiple independent ordered sequences**

### SAA Architecture Principle

> **Use a logical entity as MessageGroupId when ordering is required per entity rather than globally.**

---

## Deduplication

SNS FIFO also supports:

**Message deduplication**

This helps prevent the same logical message from being distributed repeatedly.

Two important approaches:

- Deduplication ID
- Content-Based Deduplication

---

## MessageDeduplicationId

A producer can provide:

**MessageDeduplicationId**

Example:

Transaction:

`TX-10045`

Deduplication ID:

`TX-10045`

If the same logical event is retried within the deduplication interval:

SNS can recognize:

**The duplicate**

and avoid publishing another duplicate into the FIFO workflow.

### Memory Trick

**DEDUP ID = Have I already seen this event?**

---

## Content-Based Deduplication

SNS FIFO can also use:

**Content-Based Deduplication**

Instead of explicitly providing a deduplication ID:

SNS generates one based on:

**Message content**

This is useful when duplicate messages have:

**Identical bodies**

---

## Group ID vs Deduplication ID

These two concepts solve completely different problems.

### MessageGroupId

Controls:

**Ordering**

Question:

> **Which ordered stream does this message belong to?**

### MessageDeduplicationId

Controls:

**Duplicate detection**

Question:

> **Have I already accepted this logical event?**

> [!tip] Memory Trick
> **GROUP = ORDER**
>
> **DEDUP = DUPLICATES**

---

# SNS FIFO Subscribers

The Maarek slides highlight that SNS FIFO topics can have:

- SQS Standard queues
- SQS FIFO queues

as subscribers. :contentReference[oaicite:0]{index=0}

However, the classic architecture when you specifically need:

**Ordering + Deduplication end-to-end**

is:

[[SNS FIFO]]  
↓  
Multiple [[SQS FIFO]] Queues

---

# SNS FIFO + SQS FIFO Fan-Out

This is the most important SNS FIFO architecture.

Use it when:

> **One ordered event must be reliably processed by multiple independent applications.**

Architecture:

Producer  
↓  
SNS FIFO  
↓  
├── Fraud SQS FIFO
├── Shipping SQS FIFO
└── Accounting SQS FIFO

Each downstream application gets:

**Its own copy**

while maintaining:

**FIFO semantics**

The Maarek deck explicitly describes this as the solution for **fan-out + ordering + deduplication**. :contentReference[oaicite:1]{index=1}

---

## Example — Financial Transaction

A banking system publishes:

1. Account Opened
2. Deposit
3. Withdrawal
4. Account Closed

Several systems need the same events:

- Fraud detection
- Auditing
- Reporting

Architecture:

Banking Service  
↓  
SNS FIFO  
↓  
├── Fraud FIFO Queue
├── Audit FIFO Queue
└── Reporting FIFO Queue

Each receives:

1  
↓  
2  
↓  
3  
↓  
4

### Killer Exam Pattern

> **Multiple applications need the same events in strict order**
>
> → **SNS FIFO + SQS FIFO**

---

# SNS Standard vs SNS FIFO

## SNS Standard

Think:

- Pub/Sub
- Broadcast
- Fan-Out
- Very high scalability
- Ordering not guaranteed

---

## SNS FIFO

Think:

- Pub/Sub
- Ordered fan-out
- Message groups
- Deduplication

### Memory Trick

**SNS Standard = Broadcast**

**SNS FIFO = Ordered Broadcast**

---

# SNS Standard vs FIFO Comparison

| Feature | SNS Standard | SNS FIFO |
|---|---:|---:|
| Publish / Subscribe | ✅ | ✅ |
| Fan-Out | ✅ | ✅ |
| Strict Ordering | ❌ | ✅ Within Message Group |
| MessageGroupId | ❌ | ✅ |
| Deduplication | ❌ | ✅ |
| Content-Based Deduplication | ❌ | ✅ |
| Best For | General Notifications | Ordered Events |

---

# SNS FIFO vs SQS FIFO

Both support:

- MessageGroupId
- Deduplication
- FIFO semantics

But their roles are different.

## SNS FIFO

Purpose:

**One → Many**

Model:

**Pub/Sub**

---

## [[SQS FIFO]]

Purpose:

**Queue work**

Model:

**Producer → Queue → Consumer**

### Memory Trick

**SNS FIFO = Ordered COPY**

**SQS FIFO = Ordered HOLD**

---

# Ordered Fan-Out

Suppose:

One producer creates:

**Order events**

Three services must receive:

**Every event**

in the correct order.

Using:

One SQS FIFO queue

would not work for fan-out because the consumers would:

**Compete for messages**

Instead:

Producer  
↓  
SNS FIFO  
↓  
├── Queue A
├── Queue B
└── Queue C

Now each application receives:

**A separate ordered copy**

---

# SNS FIFO + SQS Standard

The Maarek slides note that an SNS FIFO topic can also have:

**SQS Standard queues**

as subscribers. :contentReference[oaicite:2]{index=2}

However:

If the downstream application requires:

**Strict end-to-end ordering**

choose:

**SQS FIFO**

as the subscriber.

### Exam Thinking

SNS FIFO gives ordering at the topic level.

But your:

**Subscriber choice**

must also fit the downstream ordering requirement.

---

# SNS FIFO Throughput

The Maarek slides describe SNS FIFO as having:

**Limited throughput**

similar to:

[[SQS FIFO]]

relative to Standard SNS. :contentReference[oaicite:3]{index=3}

The exam takeaway is:

> **Choose FIFO because you need ordering and deduplication—not because you want maximum throughput.**

---

# SNS FIFO + Filtering

SNS supports:

**Subscription Filter Policies**

which determine which messages a subscription receives.

That means an ordered pub/sub architecture can also incorporate:

**Selective delivery**

when appropriate.

Conceptually:

SNS FIFO  
↓  
Order Events  
↓  
├── Payment Subscriber
├── Shipping Subscriber
└── Fraud Subscriber

Each subscription can be designed around:

**Its own event requirements**

---

# FIFO vs Message Filtering

Do not confuse these concepts.

## FIFO

Controls:

- Ordering
- Deduplication

---

## Filter Policy

Controls:

**Which messages a subscriber receives**

### Memory Trick

**FIFO = HOW messages arrive**

**FILTER = WHICH messages arrive**

---

# SNS FIFO vs Kinesis

Both can preserve:

**Order**

but they solve different problems.

## SNS FIFO

Think:

- Pub/Sub
- Fan-Out
- Push delivery
- Deduplication
- Ordered events

---

## [[Kinesis]]

Think:

- Real-time streaming
- Record retention
- Replay
- Multiple stream consumers
- Ordered records within partition/shard

### Exam Shortcut

**Ordered notification / fan-out**
→ SNS FIFO

**Replayable real-time stream**
→ Kinesis

---

# SNS FIFO vs EventBridge

## SNS FIFO

Think:

**Ordered pub/sub**

---

## [[20-SAA/10-Messaging/EventBridge]]

Think:

- Event routing
- Rules
- Event patterns
- Multiple event sources
- Archive / replay capabilities

### Exam Shortcut

**Ordered fan-out**
→ SNS FIFO

**Complex event routing**
→ EventBridge

---

# SNS FIFO vs Standard SNS + SQS FIFO

This can be a tricky architecture distinction.

If:

**The publishing layer itself must preserve FIFO ordering and deduplication**

think:

[[SNS FIFO]]

If ordering is only needed inside a specific downstream queue:

The architecture requirements determine whether:

**Standard SNS + specific queue behavior**

is enough.

### SAA Rule

When the question explicitly says:

> **Fan-Out + Ordering + Deduplication**

the strongest answer is:

**SNS FIFO + SQS FIFO**

---

# Architecture Thinking

## Scenario 1 — Ordered Financial Fan-Out

A financial service publishes transactions.

Fraud, accounting, and audit systems each require:

- Every transaction
- Correct order
- Duplicate prevention

**Choose:**

SNS FIFO  
↓  
Multiple SQS FIFO Queues

---

## Scenario 2 — Ordinary Notifications

A company sends application notifications to:

- Email
- Lambda
- HTTP endpoint

Ordering is irrelevant.

Do NOT choose FIFO unnecessarily.

Choose:

[[SNS]]

Standard.

---

## Scenario 3 — Ordered Events for One Consumer

Only one processing system needs:

**An ordered work queue**

Fan-out is unnecessary.

Choose:

[[SQS FIFO]]

rather than adding SNS FIFO.

---

## Scenario 4 — Ordered Events for Many Consumers

Several applications independently require:

**Every ordered event**

Choose:

**SNS FIFO + SQS FIFO**

---

## Scenario 5 — Real-Time Replay

A company needs:

- Ordered data
- Multiple consumers
- Ability to replay hours-old records

SNS FIFO is not the strongest fit.

Think:

[[Kinesis]]

---

## Scenario 6 — Different Customers

Transactions must remain ordered:

**Per customer**

but different customers can process concurrently.

Use:

Customer ID  
→ MessageGroupId

Example:

Customer A  
→ Group A

Customer B  
→ Group B

Customer C  
→ Group C

---

## Scenario 7 — Producer Retries

A producer retries an event because it is unsure whether the original request succeeded.

Use:

**Deduplication**

to help prevent duplicate publication.

---

# Scenario Recognition

Immediately think:

[[SNS FIFO]]

when you see:

- Ordered fan-out
- Pub/Sub + ordering
- Multiple ordered subscribers
- Deduplication
- MessageGroupId
- MessageDeduplicationId
- Content-based deduplication
- Fan-Out + FIFO

### Strongest Exam Pattern

> **"Multiple independent consumers need the same messages in order with deduplication."**
>
> → **SNS FIFO + SQS FIFO**

---

# Exam Traps

## Trap 1 — Standard SNS Guarantees Ordering

False.

Need strict ordering?

→ SNS FIFO

---

## Trap 2 — SNS FIFO Is Just SQS FIFO with a Different Name

False.

SNS FIFO:

**Pub/Sub**

SQS FIFO:

**Queue**

---

## Trap 3 — One SQS FIFO Queue Provides Fan-Out

False.

Consumers of one queue:

**Compete**

Need separate copies?

→ SNS FIFO + multiple SQS FIFO queues

---

## Trap 4 — MessageGroupId Performs Deduplication

False.

MessageGroupId:

**Ordering**

Deduplication ID:

**Duplicate prevention**

---

## Trap 5 — Deduplication ID Controls Message Sequence

False.

Use:

**MessageGroupId**

for ordering.

---

## Trap 6 — FIFO Is Always Better Than Standard SNS

False.

FIFO introduces:

**Ordering constraints and lower throughput characteristics**

Use it only when:

**Ordering / deduplication are required**

---

## Trap 7 — SNS FIFO Gives You Stream Replay

False.

If replayable retained streaming data is required:

Think:

[[Kinesis]]

---

## Trap 8 — FIFO Filtering and FIFO Ordering Are the Same Feature

False.

Filtering:

**Determines which subscriber receives a message**

FIFO:

**Determines message ordering and deduplication**

---

# Quick Cheat Sheet

| Exam Clue | Answer |
|---|---|
| Ordered Pub/Sub | SNS FIFO |
| Ordered Fan-Out | SNS FIFO |
| Fan-Out + Deduplication | SNS FIFO |
| Ordering Identifier | MessageGroupId |
| Duplicate Identifier | MessageDeduplicationId |
| Automatic Dedup | Content-Based Deduplication |
| Ordered Fan-Out to Queues | SNS FIFO + SQS FIFO |
| One Ordered Work Queue | SQS FIFO |
| General Fan-Out | SNS Standard |
| Replayable Ordered Stream | Kinesis |
| Advanced Event Routing | EventBridge |

---

# Standard SNS vs SNS FIFO vs SQS FIFO

| Requirement | SNS Standard | SNS FIFO | SQS FIFO |
|---|---:|---:|---:|
| Pub/Sub | ✅ | ✅ | ❌ |
| Queue | ❌ | ❌ | ✅ |
| One → Many | ✅ | ✅ | ❌ |
| Strict Ordering | ❌ | ✅ | ✅ |
| Deduplication | ❌ | ✅ | ✅ |
| Message Groups | ❌ | ✅ | ✅ |
| Fan-Out | ✅ | ✅ | ❌ |
| Work Buffer | ❌ | ❌ | ✅ |

---

## Master Memory Trick

> [!tip] SNS FIFO Master Memory Trick
> Imagine a company sends numbered memos:
>
> **Memo 1**
>
> **Memo 2**
>
> **Memo 3**
>
> Every department needs:
>
> **ALL THREE**
>
> and they must arrive:
>
> **IN ORDER**

That's:

> **SNS FIFO**
>
> → Makes ordered copies
>
> **SQS FIFO**
>
> → Gives each department its own ordered inbox

So remember:

> **SNS = COPY**
>
> **FIFO = ORDER**
>
> **SQS = HOLD**

Put them together:

> **SNS FIFO + SQS FIFO**
>
> =
>
> **COPY + ORDER + HOLD**

And the killer clue:

> **FAN-OUT + ORDERING + DEDUPLICATION**
>
> → **SNS FIFO + SQS FIFO**

---

## Related Notes

- [[SNS]]
- [[SQS]]
- [[SQS FIFO]]
- [[Kinesis]]
- [[20-SAA/10-Messaging/EventBridge]]
- [[02-Compute/Lambda]]
- [[SNS Message Filtering]]
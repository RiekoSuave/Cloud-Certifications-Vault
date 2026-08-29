## What Problem Does It Solve?

[[SQS]] — Amazon Simple Queue Service — is a:

**Fully managed message queue**

used to:

**Decouple applications and process work asynchronously**

Instead of one application component directly depending on another:

Producer  
↓  
Consumer

you place a queue between them:

Producer  
↓  
SQS Queue  
↓  
Consumer

This means the producer and consumer:

**Do not need to operate at the same speed or even be available at the same time.**

> [!tip] Memory Trick
> **SQS = WAITING LINE**
>
> Producer puts work in line.
>
> Consumer processes the line.

---

## Core SQS Architecture

SQS uses:

**Producers**

and:

**Consumers**

Architecture:

Producer  
↓  
SendMessage  
↓  
SQS Queue  
↓  
ReceiveMessage  
↓  
Consumer  
↓  
Process Message  
↓  
DeleteMessage

### Producer

Creates and sends:

**Messages**

to the queue.

### Consumer

Retrieves and processes:

**Messages**

from the queue.

---

## Why Decoupling Matters

Without SQS:

Application A  
↓  
Application B

If Application B becomes unavailable:

Application A may:

- Fail
- Wait
- Time out
- Become overloaded

With SQS:

Application A  
↓  
SQS  
↓  
Application B

If Application B becomes unavailable:

**Messages remain in the queue**

until consumers can process them.

### SAA Architecture Principle

> **Decouple application components whenever they do not need synchronous communication.**

SQS is one of the most important AWS services for:

**Loose coupling**

---

## Example Architecture

Imagine an online store.

Customer  
↓  
Places Order  
↓  
Web Application  
↓  
SQS Queue  
↓  
Order Processing Workers

Without SQS:

The customer may have to wait while the backend:

- Processes payment
- Updates inventory
- Generates documents
- Starts fulfillment

With SQS:

The web application can:

1. Accept the request
2. Place work into SQS
3. Respond quickly
4. Let workers process the work asynchronously

---

## SQS Is Pull-Based

Consumers:

**Poll SQS**

for messages.

Architecture:

Consumer  
↓  
"Any messages?"  
↓  
SQS

SQS does not normally push messages directly to traditional consumers.

> [!tip] Memory Trick
> **SQS = Consumers PULL**
>
> **SNS = Subscribers get PUSHED notifications**

This distinction becomes extremely important when comparing:

[[SQS]]

and:

[[SNS]]

---

## SQS Message Size

Maximum SQS message size:

**256 KB**

If the payload is larger:

A common architecture is:

Large Object  
↓  
[[S3]]

and place:

**A reference / pointer to the object**

inside the SQS message.

Conceptually:

Producer  
↓  
Store Large File in S3  
↓  
Send S3 Object Reference to SQS  
↓  
Consumer Retrieves Message  
↓  
Consumer Reads File from S3

### Exam Trap

> **Large file ≠ put entire file in SQS**

Think:

**S3 for data**

+

**SQS for notification / work instruction**

---

## Message Retention

SQS messages can be retained for:

**1 minute to 14 days**

Default retention:

**4 days**

### Memory Trick

> **Default = 4 Days**
>
> **Maximum = 14 Days**

---

## Consumers

Consumers can include:

- [[EC2]]
- [[02-Compute/Lambda]]
- Containers
- Custom applications

Example:

Producer  
↓  
SQS  
↓  
EC2 Consumer Fleet

or:

Producer  
↓  
SQS  
↓  
Lambda

---

## SQS + Auto Scaling

One powerful architecture is:

Producer  
↓  
SQS Queue  
↓  
EC2 Auto Scaling Group

As the queue grows:

**Add more consumers**

As the queue shrinks:

**Remove consumers**

A useful scaling metric is:

**ApproximateNumberOfMessagesVisible**

Conceptually:

Queue Depth ↑  
↓  
Scale EC2 Consumers Out

Queue Depth ↓  
↓  
Scale EC2 Consumers In

### SAA Pattern

> **Large SQS backlog + EC2 consumers**
>
> → Scale consumers based on queue depth.

---

## SQS Standard Queue

The default SQS queue type is:

**Standard Queue**

Standard queues provide:

- Nearly unlimited throughput
- At-least-once delivery
- Best-effort ordering

### Memory Trick

**STANDARD = SPEED**

---

## At-Least-Once Delivery

With a Standard Queue:

A message may occasionally be delivered:

**More than once**

Therefore consumers should ideally be:

**Idempotent**

---

## Idempotency

An idempotent consumer can process the same request multiple times without causing:

**Incorrect duplicate effects**

Example:

Message:

> Charge customer $100

If processed twice:

Customer might be charged:

**$200**

Bad.

An idempotent design could track:

**Transaction ID**

and determine:

> "This transaction was already processed."

### SAA Principle

> **Standard SQS + duplicate possibility**
>
> → Design consumers to be idempotent.

---

## Best-Effort Ordering

Standard SQS does NOT guarantee:

**Strict message ordering**

Messages:

1  
2  
3

could potentially be processed:

2  
1  
3

If strict ordering matters:

Think:

[[SQS FIFO]]

---

## SQS FIFO Queue

FIFO means:

**First-In-First-Out**

FIFO queues are designed for:

- Strict ordering
- Duplicate prevention / deduplication
- Workflows where sequence matters

Queue names must end in:

`.fifo`

Example:

`payments.fifo`

### Memory Trick

**FIFO = ORDER**

---

## FIFO Ordering

Messages are processed in:

**Order**

within a message group.

Example:

Message 1  
↓  
Message 2  
↓  
Message 3

Processing:

1  
↓  
2  
↓  
3

This is useful for:

- Financial transactions
- Order updates
- Inventory operations
- Commands that must occur sequentially

---

## FIFO Deduplication

FIFO queues provide mechanisms to prevent:

**Duplicate messages**

within the deduplication interval.

Deduplication can use:

- Content-based deduplication
- Explicit message deduplication ID

### Exam Clue

> **Strict ordering + duplicate prevention**
>
> → **SQS FIFO**

---

## Standard vs FIFO

| Feature | Standard | FIFO |
|---|---|---|
| Throughput | Very High | More Controlled |
| Ordering | Best Effort | Strict within Message Group |
| Delivery | At Least Once | Exactly-Once Processing Semantics |
| Duplicate Possibility | Yes | Deduplication |
| Queue Suffix | None | `.fifo` |
| Best For | Massive Scale | Ordering / Deduplication |

### Exam Shortcut

**Need maximum throughput**
→ Standard

**Need strict order**
→ FIFO

---

## Message Groups

FIFO queues use:

**MessageGroupId**

Messages within the same group are:

**Strictly ordered**

Example:

Customer A:

A1  
A2  
A3

Customer B:

B1  
B2  
B3

Each group maintains its own:

**Ordering**

while different groups can be processed:

**In parallel**

### SAA Insight

Message groups allow you to combine:

**Ordering**

with:

**Parallelism**

---

## Visibility Timeout

This is one of the most important SQS concepts.

When a consumer receives a message:

The message becomes:

**Temporarily invisible**

to other consumers.

This period is called:

**Visibility Timeout**

Architecture:

Message Available  
↓  
Consumer Receives Message  
↓  
Message Becomes Invisible  
↓  
Consumer Processes Message

If successful:

Consumer deletes message.

If unsuccessful:

Visibility timeout expires.

Message becomes:

**Visible again**

---

## Why Visibility Timeout Exists

Imagine:

Consumer A receives:

Message #10

Consumer A is processing it.

Without visibility timeout:

Consumer B could immediately receive:

Message #10

and process it too.

Visibility timeout prevents:

**Multiple consumers from processing the same message simultaneously under normal operation.**

---

## Visibility Timeout Failure Scenario

Consumer receives message  
↓  
Message becomes invisible  
↓  
Consumer crashes  
↓  
Message is NOT deleted  
↓  
Visibility timeout expires  
↓  
Message becomes visible  
↓  
Another consumer processes it

This provides:

**Fault tolerance**

---

## Visibility Timeout Exam Trap

Suppose processing takes:

**5 minutes**

but visibility timeout is:

**30 seconds**

Then:

Consumer A is still processing  
↓  
30 seconds passes  
↓  
Message becomes visible again  
↓  
Consumer B receives same message

Result:

**Duplicate processing**

### Solution

Increase:

**Visibility Timeout**

---

## ChangeMessageVisibility

If processing takes longer than expected:

A consumer can use:

**ChangeMessageVisibility**

to extend the visibility timeout.

### Exam Pattern

> **Consumer needs more time to process a message**
>
> → Increase / extend visibility timeout.

---

## Long Polling

Consumers can poll SQS using:

- Short polling
- Long polling

Long polling allows the request to wait for messages to arrive.

Maximum long-poll wait time:

**20 seconds**

### Benefits

Long polling:

- Reduces empty responses
- Reduces unnecessary API calls
- Reduces cost
- Improves efficiency

### Exam Preference

When given a choice:

> **Prefer Long Polling**

---

## Short Polling

Short polling returns:

**Immediately**

even if:

No message is available.

This can cause:

- More empty responses
- More API requests
- Higher cost

### Memory Trick

**Long Polling = WAIT instead of constantly asking**

---

## Delay Queue

A Delay Queue postpones delivery of:

**New messages**

for a configured amount of time.

Maximum delay:

**15 minutes**

Example:

Producer  
↓  
SQS  
↓  
Wait 10 Minutes  
↓  
Consumer Can Receive Message

### Use Cases

- Delayed processing
- Retry later
- Deferred workflows

---

## Message Timers

Individual messages can also be delayed.

This allows:

**Per-message delay**

rather than applying the delay to the entire queue.

> [!tip] Difference
> **Delay Queue**
> → Delay applies to queue messages generally
>
> **Message Timer**
> → Delay applies to a specific message

---

## Dead-Letter Queue

A:

**Dead-Letter Queue — DLQ**

stores messages that repeatedly fail processing.

Architecture:

Main SQS Queue  
↓  
Consumer Attempts Processing  
↓  
Failure  
↓  
Retry  
↓  
Failure  
↓  
Maximum Receive Count Reached  
↓  
DLQ

### Purpose

Instead of endlessly retrying a poison message:

**Move it aside for investigation**

---

## maxReceiveCount

The:

**Redrive Policy**

determines when a message moves to the DLQ.

A key setting is:

**maxReceiveCount**

Example:

`maxReceiveCount = 5`

After repeated unsuccessful receives:

Message  
↓  
DLQ

---

## DLQ Retention

A useful exam principle:

> **Set DLQ retention longer than the source queue retention when appropriate.**

This gives administrators more time to:

- Inspect
- Troubleshoot
- Recover

failed messages.

---

## DLQ Requirements

For SQS:

The DLQ should use a compatible queue type.

Standard Queue  
→ Standard DLQ

FIFO Queue  
→ FIFO DLQ

---

## Redrive to Source

After fixing the underlying issue:

Messages in a DLQ can be:

**Redriven**

back to the source queue for:

**Reprocessing**

Conceptually:

DLQ  
↓  
Fix Problem  
↓  
Redrive  
↓  
Original Queue  
↓  
Consumer

---

## SQS Encryption

SQS supports encryption:

**At rest**

using:

[[06-Security/KMS]]

It also supports encryption:

**In transit**

using:

HTTPS

### Exam Pattern

> **Encrypt messages stored in SQS**
>
> → Server-side encryption / KMS

---

## SQS Access Control

SQS security can use:

- IAM policies
- SQS queue policies

### IAM Policy

Controls:

**What an IAM principal can do**

Example:

Can application role:

`SendMessage`?

---

### Queue Policy

Resource-based policy attached to:

**The SQS Queue**

Useful when allowing:

- Cross-account access
- Other AWS services to send messages

### Memory Trick

**IAM Policy = Who can act**

**Queue Policy = Who can access this queue**

---

## SQS + Lambda

[[02-Compute/Lambda]] integrates directly with SQS.

Architecture:

Producer  
↓  
SQS  
↓  
Lambda

Lambda polls the queue through its:

**Event source mapping**

and invokes functions to process messages.

### Strong Exam Pattern

> **Serverless asynchronous message processing**
>
> → **SQS + Lambda**

---

## SQS Buffering

SQS is excellent for:

**Absorbing traffic spikes**

Imagine:

Normal:

100 requests/sec

Sudden spike:

10,000 requests/sec

Instead of overwhelming the backend:

Requests  
↓  
SQS Queue  
↓  
Consumers Process at Sustainable Rate

The queue acts as a:

**Buffer**

### SAA Architecture Principle

> **Use SQS to smooth traffic spikes and protect downstream systems.**

---

## SQS Backpressure

Suppose producers generate work faster than consumers can process it.

Without a queue:

Backend crashes.

With SQS:

Messages accumulate:

Producer Rate  
>  
Consumer Rate

↓  

Queue Depth Increases

Consumers continue processing at:

**Their sustainable rate**

This is one of the strongest architectural reasons for:

[[SQS]]

---

## SQS Temporary Storage

SQS should NOT be treated as:

**Permanent data storage**

Remember:

Maximum message retention:

**14 days**

If data must remain permanently:

Think:

- [[S3]]
- Database
- Another durable storage service

---

## SQS vs SNS

This comparison is extremely important.

### SQS

Model:

**Queue**

Consumer:

**Pulls**

Each message is normally processed by:

**A consumer**

Think:

**Work queue**

---

### [[SNS]]

Model:

**Publish / Subscribe**

SNS pushes messages to:

**Multiple subscribers**

Think:

**Broadcast**

### Memory Trick

**SQS = QUEUE**

**SNS = ANNOUNCEMENT**

---

## SQS vs Kinesis

### SQS

Think:

- Message queue
- Decoupling
- Work distribution
- Message removed after successful processing

---

### [[Kinesis]]

Think:

- Streaming
- Ordered records
- Real-time analytics
- Multiple consumers can process the stream
- Records retained for a period

### Exam Shortcut

**Work Queue**
→ SQS

**Real-Time Stream**
→ Kinesis

---

## SQS vs EventBridge

### SQS

Think:

**Buffer work for consumers**

---

### [[20-SAA/10-Messaging/EventBridge]]

Think:

**Event routing**

based on:

- Event patterns
- Sources
- Rules
- Targets

### Exam Shortcut

**Store work until consumer is ready**
→ SQS

**Route events based on rules**
→ EventBridge

---

## Fan-Out Architecture

Sometimes one event must trigger:

**Multiple independent processing systems**

Sending one message to one SQS queue does not automatically create a copy for every consumer.

Instead, a common architecture is:

Producer  
↓  
[[SNS]]  
↓  
├── SQS Queue A  
├── SQS Queue B  
└── SQS Queue C

Each queue receives:

**Its own copy**

This is:

**SNS + SQS Fan-Out**

### Example

Order Created  
↓  
SNS  
↓  
├── Billing Queue
├── Shipping Queue
└── Analytics Queue

Each system processes independently.

### Killer Exam Clue

> **Same message must be reliably processed by multiple independent applications**
>
> → **SNS + multiple SQS queues**

---

## Why SNS + SQS?

SNS provides:

**Fan-Out**

SQS provides:

**Durability + Buffering**

Together:

SNS  
↓  
Multiple SQS Queues  
↓  
Independent Consumers

### Memory Trick

**SNS COPIES**

**SQS HOLDS**

---

## Architecture Thinking

### Scenario 1 — Decouple Web and Worker Tier

A web application receives requests faster than workers can process them.

**Choose → SQS**

---

### Scenario 2 — Traffic Spike

A backend database cannot handle sudden bursts of work.

Place:

**SQS between the producer and workers**

to buffer requests.

---

### Scenario 3 — Strict Ordering

Financial transactions must be processed:

**In order**

with duplicate prevention.

**Choose → SQS FIFO**

---

### Scenario 4 — Maximum Throughput

Millions of independent messages must be processed and strict ordering is unnecessary.

**Choose → SQS Standard**

---

### Scenario 5 — Consumer Takes Too Long

Processing requires 5 minutes but messages become visible after 30 seconds.

**Increase → Visibility Timeout**

---

### Scenario 6 — Empty Polling Costs

Consumers repeatedly poll an empty queue.

**Enable → Long Polling**

---

### Scenario 7 — Poison Message

A malformed message repeatedly fails processing.

**Use → Dead-Letter Queue**

---

### Scenario 8 — Multiple Applications Need Same Event

Billing, shipping, and analytics each need:

**Their own copy**

of an order event.

**Choose → SNS + SQS Fan-Out**

---

### Scenario 9 — Serverless Worker

Messages should automatically trigger serverless processing.

**Choose → SQS + Lambda**

---

### Scenario 10 — Large Payload

An application needs to process:

**A file larger than the SQS message limit**

**Store file → S3**

**Send reference → SQS**

---

## Scenario Recognition

Immediately think:

[[SQS]]

when you see:

- Decouple
- Queue
- Asynchronous
- Buffer
- Traffic spike
- Producer / consumer
- Worker fleet
- Backpressure
- Pull messages
- Queue depth
- Visibility timeout
- Dead-letter queue
- Long polling

Immediately think:

[[SQS FIFO]]

when you see:

- Strict ordering
- FIFO
- Sequence matters
- Deduplication

---

## Exam Traps

### Trap 1 — SQS Pushes Messages to Traditional Consumers

Not normally.

Consumers:

**Poll / pull from SQS**

---

### Trap 2 — Standard SQS Guarantees Ordering

False.

Standard:

**Best-effort ordering**

Need strict ordering?

→ FIFO

---

### Trap 3 — Standard SQS Guarantees No Duplicates

False.

Standard queues use:

**At-least-once delivery**

Design consumers to be:

**Idempotent**

---

### Trap 4 — Receiving a Message Deletes It

False.

Receiving makes the message:

**Invisible temporarily**

The consumer must:

**Delete it after successful processing**

---

### Trap 5 — Visibility Timeout Is Message Retention

False.

**Visibility Timeout**
→ How long received message is hidden

**Retention Period**
→ How long SQS keeps an unconsumed message

---

### Trap 6 — Delay Queue and Visibility Timeout Are the Same

False.

**Delay**
→ Before message becomes initially available

**Visibility Timeout**
→ After consumer receives it

---

### Trap 7 — SQS Is Permanent Storage

False.

Maximum retention:

**14 days**

---

### Trap 8 — One Queue Gives Every Consumer a Copy

False.

Consumers of the same queue generally:

**Compete for messages**

Need every application to receive its own copy?

→ SNS + multiple SQS queues

---

## Standard vs FIFO Quick Comparison

| Requirement | Standard | FIFO |
|---|---:|---:|
| Massive Throughput | ✅ | More Controlled |
| Strict Ordering | ❌ | ✅ |
| At-Least-Once Delivery | ✅ | — |
| Deduplication | ❌ | ✅ |
| Message Groups | ❌ | ✅ |
| `.fifo` Suffix | ❌ | ✅ |
| General Decoupling | ✅ | ✅ |

---

## SQS Timing Cheat Sheet

| Setting | Value |
|---|---|
| Message Retention Default | 4 Days |
| Message Retention Maximum | 14 Days |
| Message Retention Minimum | 1 Minute |
| Long Polling Maximum | 20 Seconds |
| Delay Maximum | 15 Minutes |
| Message Size Maximum | 256 KB |

---

## SQS Quick Cheat Sheet

| Exam Clue | Answer |
|---|---|
| Decouple Applications | SQS |
| Buffer Traffic | SQS |
| Producer / Consumer | SQS |
| Maximum Throughput | Standard |
| Strict Ordering | FIFO |
| Deduplication | FIFO |
| Duplicate Processing Risk | Idempotent Consumer |
| Message Reappears Too Soon | Increase Visibility Timeout |
| Reduce Empty Polls | Long Polling |
| Repeated Failure | DLQ |
| Serverless Queue Consumer | SQS + Lambda |
| Scale Workers | Queue Depth |
| Multiple Independent Copies | SNS + SQS |
| Large Payload | S3 + SQS Reference |

---

## Master Memory Trick

> [!tip] SQS Master Memory Trick
> Imagine a restaurant kitchen.
>
> Customers place orders:
>
> **PRODUCERS**
>
> ↓
>
> Tickets go onto the rail:
>
> **SQS QUEUE**
>
> ↓
>
> Cooks grab tickets:
>
> **CONSUMERS**
>
> The cashier does NOT wait for the cook to finish.
>
> That's:
>
> **DECOUPLING**

If the kitchen gets slammed:

> Tickets pile up safely.
>
> **SQS = BUFFER**

If a cook grabs a ticket:

> Other cooks temporarily cannot see it.
>
> **VISIBILITY TIMEOUT**

If the cook finishes:

> Throw away the ticket.
>
> **DELETE MESSAGE**

If the cook disappears:

> Ticket eventually becomes visible again.
>
> **RETRY**

If the ticket keeps failing:

> Move it to the problem pile.
>
> **DLQ**

If order matters:

> **FIFO**

If order doesn't matter and you want huge scale:

> **STANDARD**

If several departments need their own ticket:

> **SNS + MULTIPLE SQS QUEUES**

Finally:

> **SQS = DECOUPLE + BUFFER + ASYNC**

---

## Related Notes

- [[SNS]]
- [[SQS FIFO]]
- [[Kinesis]]
- [[20-SAA/10-Messaging/EventBridge]]
- [[02-Compute/Lambda]]
- [[EC2]]
- [[Auto Scaling]]
- [[S3]]
- [[06-Security/KMS]]
- [[Dead-Letter Queue]]
- [[Long Polling]]
- [[Visibility Timeout]]


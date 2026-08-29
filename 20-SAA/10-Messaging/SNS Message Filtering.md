## What Problem Does It Solve?

[[SNS Message Filtering]] allows each SNS subscription to receive:

**Only the messages it cares about**

instead of receiving:

**Every message published to the topic**

It solves the problem:

> **"How can multiple subscribers share one SNS topic but receive different subsets of messages?"**

Architecture:

Publisher  
↓  
SNS Topic  
↓  
├── Subscriber A → Only Matching Messages  
├── Subscriber B → Only Matching Messages  
└── Subscriber C → All Messages

> [!tip] Memory Trick
> **SNS Filtering = Same topic, different interests**

---

## Default SNS Behavior

Without subscription filtering:

A publisher sends a message to:

[[SNS]]

and subscriptions normally receive:

**Every message published to the topic**

Architecture:

Producer  
↓  
SNS Topic  
↓  
├── Subscriber A ✅  
├── Subscriber B ✅  
└── Subscriber C ✅

This is classic:

**Pub/Sub Fan-Out**

But sometimes different subscribers only need:

**Specific events**

That is where:

**Subscription Filter Policies**

are used.

---

## Subscription Filter Policy

An SNS subscription can have a:

**Filter Policy**

A filter policy is:

**A JSON policy**

that determines which messages are delivered to:

**That specific subscription**

Conceptually:

Message  
↓  
SNS Topic  
↓  
Subscription Filter Policy  
↓  
Does It Match?  
↓  
Yes → Deliver  
No → Do Not Deliver

> [!tip] Memory Trick
> **Filter Policy = Subscriber's shopping list**
>
> "Only send me the events I care about."

---

## Filtering Happens Per Subscription

The filter policy belongs to:

**The subscription**

not globally to:

**The SNS topic**

This is extremely important.

One SNS Topic  
↓  
Multiple Subscriptions  
↓  
Different Filter Policies

Example:

SNS Topic  
↓  
Order Events

Subscription A:

`State = Placed`

Subscription B:

`State = Cancelled`

Subscription C:

`State = Declined`

Subscription D:

No Filter

Result:

Each filtered subscription receives:

**Only matching messages**

while the subscription without a filter receives:

**Everything**

---

## No Filter Policy

This is one of the most important exam rules.

If a subscription has:

**No Filter Policy**

then it receives:

**Every message published to the topic**

> [!tip] Exam Rule
> **NO FILTER = RECEIVE ALL**

Do NOT confuse:

**No Filter**

with:

**Receive Nothing**

It means the exact opposite:

**Receive Everything**

---

## Maarek Order-State Example

A classic example is an SNS topic receiving:

**Order events**

with different states.

Possible states:

- Placed
- Cancelled
- Declined

Architecture:

Buying Service  
↓  
SNS Topic  
↓  
Order Events  
↓  
├── Placed Queue
├── Cancelled Queue
├── Declined Queue
└── All Messages Queue

Each subscription can use:

**Its own filter policy**

---

## Example — Placed Order

Suppose an event represents:

Order:

`1036`

Product:

`Pencil`

Quantity:

`4`

State:

`Placed`

Architecture:

SNS Topic  
↓  
State = Placed

Placed Queue  
Filter:

`State = Placed`

→ Receives Message ✅

Cancelled Queue  
Filter:

`State = Cancelled`

→ Does NOT Receive ❌

Declined Queue  
Filter:

`State = Declined`

→ Does NOT Receive ❌

All Messages Queue  
No Filter

→ Receives Message ✅

---

## Filter Policy Matching

SNS evaluates the message against:

**The subscription's filter policy**

Conceptually:

Message  
↓  
Filter Policy  
↓  
Match?

If:

**YES**

→ Deliver to Subscriber

If:

**NO**

→ Do Not Deliver to Subscriber

### Memory Trick

**MATCH = SEND**

**NO MATCH = SKIP**

---

## Message Attributes Filtering

SNS filter policies can evaluate:

**Message attributes**

Example:

Message Attributes:

`state = Placed`

`priority = High`

`region = us-east-1`

A subscription might only want:

`state = Placed`

SNS evaluates the attributes before deciding:

**Whether to deliver the message**

---

## Message Body Filtering

SNS can also support filtering based on:

**Message body properties**

when the message body contains:

**Valid JSON**

Conceptually:

JSON Message Body  
↓  
SNS Filter Policy  
↓  
Inspect Relevant Properties  
↓  
Match?  
↓  
Deliver / Do Not Deliver

### Exam Takeaway

You do NOT need to memorize complex JSON syntax for SAA.

Remember:

> **SNS can selectively deliver messages based on message attributes or message body properties.**

---

## Filter Policy Scope

SNS filtering can therefore operate against:

- Message attributes
- Message body

The architecture question matters more than:

**The exact JSON syntax**

### Exam Pattern

> **Subscribers need different subsets of messages from the same SNS topic**
>
> → **SNS Subscription Filter Policies**

---

## Why Filtering Improves Architecture

Without filtering:

SNS  
↓  
Subscriber  
↓  
Receive Everything  
↓  
Application Inspects Message  
↓  
Application Discards Irrelevant Messages

This can create unnecessary:

- Processing
- Queue traffic
- Lambda invocations
- Application logic
- Network activity

With filtering:

SNS  
↓  
Filter Policy  
↓  
Only Relevant Messages  
↓  
Subscriber

This creates a:

**Cleaner event-driven architecture**

---

## Filtering vs Application-Side Filtering

### Application-Side Filtering

SNS  
↓  
Everything Delivered  
↓  
Consumer  
↓  
Inspect Message  
↓  
Discard Unwanted Messages

---

### SNS Filtering

SNS  
↓  
Filter Policy  
↓  
Only Matching Messages Delivered

### SAA Preference

If SNS can determine whether a subscriber needs the event:

**Filter before delivery**

rather than sending unnecessary messages downstream.

---

## Filtered Fan-Out

SNS filtering works especially well with:

**Fan-Out**

Architecture:

Order Service  
↓  
SNS Topic  
↓  
├── Payment Queue
├── Shipping Queue
├── Cancellation Queue
└── Analytics Queue

Each queue can receive:

**Different messages**

from the:

**Same topic**

This allows independent microservices to subscribe to:

**Only relevant events**

---

## SNS Filtering + SQS

This is a strong SAA architecture.

Producer  
↓  
SNS Topic  
↓  
Subscription Filter  
↓  
[[SQS]]  
↓  
Consumer

Each SQS queue can receive:

**Only the event category required by its application**

Example:

Order Service  
↓  
SNS  
↓  
├── Placed Filter → Fulfillment SQS
├── Cancelled Filter → Cancellation SQS
├── Declined Filter → Fraud SQS
└── No Filter → Analytics SQS

This combines:

**SNS selective fan-out**

with:

**SQS durability and buffering**

---

## SNS Filtering + Lambda

SNS can also use filtering before invoking:

[[02-Compute/Lambda]]

Architecture:

Publisher  
↓  
SNS  
↓  
Filter Policy  
↓  
Lambda

Example:

SNS receives:

- Low Priority
- Medium Priority
- High Priority

Lambda only needs:

**High Priority**

Filter:

`priority = High`

Result:

Only matching messages trigger:

**Lambda**

### Benefit

This reduces:

**Unnecessary Lambda invocations**

---

## SNS Filtering + Multiple Applications

Imagine one topic publishes:

**Customer Events**

Possible events:

- CustomerCreated
- CustomerUpdated
- CustomerDeleted

Three applications subscribe.

CRM:

`CustomerCreated`

Marketing:

`CustomerCreated`

Audit:

No Filter

Result:

CRM receives:

**Created**

Marketing receives:

**Created**

Audit receives:

**Everything**

One topic can therefore support:

**Different downstream requirements**

---

## Filtering vs Multiple SNS Topics

Without filtering, you might create:

- Orders-Placed Topic
- Orders-Cancelled Topic
- Orders-Declined Topic

Then the producer must determine:

**Which topic receives each message**

With filtering:

Producer  
↓  
One SNS Topic  
↓  
Subscribers Filter What They Need

This can reduce:

- Topic sprawl
- Publisher complexity
- Point-to-point logic

### Architecture Principle

> **Keep publishers simple and let subscriptions express subscriber interests when appropriate.**

---

## Filtering Is Not Message Transformation

SNS filtering determines:

**Whether a message is delivered**

It does NOT primarily:

**Rewrite or transform the message**

Think:

Message  
↓  
Filter  
↓  
Deliver?

not:

Message  
↓  
Transform Into Something Else

### Exam Trap

**Select matching messages**
→ SNS Filter Policy

**Complex transformation / advanced event processing**
→ Look at the broader event architecture

---

## Filtering Is Not a Queue

A filter policy does NOT:

- Store messages
- Buffer messages
- Retry work like SQS
- Create a durable work queue

It only determines:

**Which subscriber receives which message**

Need buffering?

→ [[SQS]]

Need filtering?

→ SNS Filter Policy

Need both?

→ **SNS Filter → SQS**

---

## Filtering vs FIFO

These solve:

**Different problems**

### SNS Filtering

Controls:

**WHICH messages are delivered**

### [[SNS FIFO]]

Controls:

- Ordering
- Deduplication

### [[SQS FIFO]]

Controls:

- Ordered queue processing
- Deduplication

> [!tip] Memory Trick
> **FILTER = WHICH**
>
> **FIFO = ORDER**

---

## Filtering + FIFO

A workload may require:

**Both**

Example:

A subscriber only wants:

**Payment events**

and those events must remain:

**Ordered**

Conceptually:

SNS FIFO  
↓  
Filter  
↓  
SQS FIFO

The filter determines:

**Which events**

FIFO determines:

**Their order**

---

## SNS Filtering vs EventBridge

This is an important SAA comparison.

### SNS Message Filtering

Think:

- Pub/Sub
- One SNS topic
- Subscription-level filtering
- Fan-Out
- Selective delivery

---

### [[20-SAA/10-Messaging/EventBridge]]

Think:

- Event bus
- Event patterns
- Advanced event routing
- Many AWS service sources
- SaaS integrations
- Multiple targets
- Archive
- Replay

### Exam Shortcut

**SNS topic + subscribers need different subsets**
→ SNS Filter Policy

**Advanced event routing architecture**
→ EventBridge

---

## SNS Filtering vs SQS

### SNS Filtering

Question:

> **Who should receive this message?**

---

### [[SQS]]

Question:

> **Where should this work wait until a consumer is ready?**

### Memory Trick

**SNS Filter = ROUTE**

**SQS = HOLD**

---

## SNS Filtering vs Kinesis

### SNS Filtering

Think:

**Selective Pub/Sub delivery**

### [[Kinesis]]

Think:

- Streaming data
- Retention
- Replay
- Real-time processing
- Ordered records

If the requirement is:

> **Only certain SNS subscribers should receive certain events**

Think:

**SNS Filtering**

not Kinesis.

---

## Architecture Thinking

### Scenario 1 — Different Order States

One SNS topic receives:

- Placed
- Cancelled
- Declined

Different SQS queues only need:

**One state each**

**Choose → SNS Subscription Filter Policies**

---

### Scenario 2 — Analytics Needs Everything

Operational queues use filters.

Analytics needs:

**Every event**

Give the Analytics subscription:

**No Filter Policy**

Result:

**Receive All**

---

### Scenario 3 — Reduce Lambda Invocations

A Lambda function only needs:

**Critical alerts**

SNS receives:

- Informational
- Warning
- Critical

Use:

**Subscription Filter Policy**

so Lambda receives:

**Critical only**

---

### Scenario 4 — Durable Selective Processing

Different microservices need:

- Different events
- Durable queues
- Independent retries

Choose:

SNS  
↓  
Filter Policies  
↓  
Multiple SQS Queues

---

### Scenario 5 — Advanced Routing

Events come from:

- AWS services
- Custom applications
- SaaS applications

The system requires:

- Advanced event patterns
- Routing rules
- Archive
- Replay

Think:

[[20-SAA/10-Messaging/EventBridge]]

rather than SNS filtering alone.

---

### Scenario 6 — Strict Ordering

Subscribers need:

**Ordered events**

Filtering alone does NOT solve this.

Think:

[[SNS FIFO]]

and/or:

[[SQS FIFO]]

depending on the architecture.

---

### Scenario 7 — One Subscriber Wants Everything

One queue needs every event while other queues only need specific categories.

Use:

Filtered subscriptions  
+

One subscription with:

**No Filter Policy**

---

## Scenario Recognition

Immediately think:

[[SNS Message Filtering]]

when you see:

- Subscription Filter Policy
- JSON filter policy
- Same SNS topic
- Different subscribers
- Different message categories
- Selective fan-out
- Only matching messages
- Reduce unnecessary downstream processing
- Filter before SQS
- Filter before Lambda

### Killer Exam Pattern

> **One SNS topic has multiple subscribers, but each subscriber should receive only certain messages.**
>
> → **SNS Subscription Filter Policies**

---

## Exam Traps

### Trap 1 — No Filter Means No Messages

False.

**No Filter = Receive All**

---

### Trap 2 — Filter Policy Is Attached to the SNS Topic

False.

Filtering is configured:

**Per subscription**

This allows different subscriptions to have:

**Different filters**

---

### Trap 3 — Every Subscriber Must Use the Same Filter

False.

Each subscription can define:

**Its own filter policy**

---

### Trap 4 — Filtering Requires Multiple SNS Topics

False.

A major advantage is:

**One Topic + Multiple Filtered Subscriptions**

---

### Trap 5 — Filtering Guarantees Ordering

False.

Filtering controls:

**Which messages**

FIFO controls:

**Ordering**

---

### Trap 6 — SNS Filtering Stores Messages

False.

Need durable message storage / buffering?

→ [[SQS]]

---

### Trap 7 — SNS Filtering Is Message Transformation

False.

It decides:

**Deliver or Don't Deliver**

---

### Trap 8 — Consumers Should Always Filter Messages Themselves

Not necessarily.

If SNS can filter before delivery:

**Subscription filtering can reduce unnecessary downstream work**

---

### Trap 9 — SNS Filtering and EventBridge Are Identical

False.

SNS filtering is:

**Selective delivery within SNS Pub/Sub**

EventBridge is:

**A broader event-routing service**

---

## Quick Cheat Sheet

| Exam Clue | Answer |
|---|---|
| Different Subscribers Need Different Messages | SNS Filter Policy |
| JSON Subscription Filter | SNS Filtering |
| No Filter Policy | Receive All |
| Filter by Message Attributes | SNS Filtering |
| Filter by JSON Message Body | SNS Filtering |
| One Topic + Selective Fan-Out | SNS Filtering |
| Reduce Irrelevant SQS Messages | SNS Filtering |
| Reduce Unnecessary Lambda Invocations | SNS Filtering |
| Durable Selective Processing | SNS Filter + SQS |
| Strict Ordering | FIFO |
| Advanced Event Routing | EventBridge |

---

## Filtering Decision Table

| Requirement | Best Choice |
|---|---|
| Everyone receives everything | SNS without filters |
| Subscriber receives subset | SNS Filter Policy |
| Different queues receive different categories | SNS + Filter Policies |
| Filter before durable processing | SNS Filter + SQS |
| Filter before serverless processing | SNS Filter + Lambda |
| Strict ordered Pub/Sub | SNS FIFO |
| Ordered queue processing | SQS FIFO |
| Advanced event routing | EventBridge |
| Replayable data stream | Kinesis |

---

## Final Exam Rapid-Fire

> **ONE TOPIC + EVERYONE GETS EVERYTHING**
> → SNS
>
> **ONE TOPIC + DIFFERENT SUBSCRIBERS WANT DIFFERENT EVENTS**
> → SNS FILTER POLICY
>
> **NO FILTER**
> → RECEIVE ALL
>
> **FILTER**
> → WHICH MESSAGE
>
> **FIFO**
> → WHAT ORDER
>
> **SQS**
> → HOLD THE MESSAGE
>
> **EVENTBRIDGE**
> → ADVANCED EVENT ROUTING

---

## Master Memory Trick

> [!tip] SNS Filtering Master Memory Trick
> Imagine SNS is a giant mailroom.
>
> Every order event enters:
>
> **ONE MAILROOM**
>
> But each department leaves instructions.
>
> Shipping:
>
> **"Only give me PLACED orders."**
>
> Cancellation:
>
> **"Only give me CANCELLED orders."**
>
> Fraud:
>
> **"Only give me DECLINED orders."**
>
> Analytics:
>
> **"Give me EVERYTHING."**
>
> Those instructions are:
>
> **SUBSCRIPTION FILTER POLICIES**

Remember:

> **SNS = BROADCAST**
>
> **FILTER = SELECT**
>
> **NO FILTER = ALL**
>
> **SQS = HOLD**
>
> **FIFO = ORDER**
>
> **EVENTBRIDGE = ADVANCED ROUTING**

And the killer exam question:

> **"Who should receive this SNS message?"**
>
> → **FILTER POLICY**

---

## Related Notes

- [[SNS]]
- [[SNS FIFO]]
- [[SQS]]
- [[SQS FIFO]]
- [[20-SAA/10-Messaging/EventBridge]]
- [[Kinesis]]
- [[02-Compute/Lambda]]
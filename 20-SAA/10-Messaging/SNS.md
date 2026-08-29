## What Problem Does It Solve?

[[SNS]] — Simple Notification Service — is a:

**Fully managed publish/subscribe messaging service**

used when:

> **One message must be delivered to multiple receivers.**

Without SNS:

Producer  
↓  
Send to Service A  
↓  
Send to Service B  
↓  
Send to Service C

The producer must integrate directly with:

**Every receiver**

With SNS:

Producer  
↓  
SNS Topic  
↓  
├── Subscriber A
├── Subscriber B
└── Subscriber C

The producer publishes:

**Once**

and SNS distributes the message to:

**Many subscribers**

> [!tip] Memory Trick
> **SNS = ANNOUNCEMENT SYSTEM**
>
> Publish once.
>
> Everyone subscribed hears it.

---

## Pub/Sub Model

SNS uses a:

**Publish / Subscribe**

or:

**Pub/Sub**

model.

There are two main roles:

### Publisher

Sends messages to:

**An SNS Topic**

### Subscriber

Receives messages from:

**The SNS Topic**

Architecture:

Publisher  
↓  
SNS Topic  
↓  
Subscribers

> [!tip] Memory Trick
> **Publisher talks to the TOPIC**
>
> **Subscribers listen to the TOPIC**

---

## SNS Topic

An SNS Topic acts as:

**The communication channel**

Publishers do not need to know:

- How many subscribers exist
- Where subscribers are running
- What each subscriber does

They simply publish to:

**The Topic**

This provides:

**Loose coupling**

---

## Why SNS Helps Decouple Applications

Without SNS:

Buying Service  
↓  
Email Service

Buying Service  
↓  
Fraud Service

Buying Service  
↓  
Shipping Service

The Buying Service must understand:

**Every downstream integration**

With SNS:

Buying Service  
↓  
SNS Topic  
↓  
├── Email
├── Fraud
└── Shipping

Now the producer only knows:

**The SNS Topic**

This reduces:

**Point-to-point coupling**

---

## One Message to Many Receivers

This is the strongest SNS exam clue.

> **One event**
>
> needs to reach:
>
> **Many independent receivers**

Think:

[[SNS]]

Example:

Order Placed  
↓  
SNS  
↓  
├── Billing
├── Shipping
├── Fraud Detection
└── Email Notification

Each subscriber receives:

**Its own notification**

---

## SNS Is Push-Based

SNS generally:

**Pushes messages to subscribers**

This differs from:

[[SQS]]

where consumers:

**Poll / pull**

messages from the queue.

### Memory Trick

**SNS = PUSH**

**SQS = PULL**

---

## SNS Subscribers

SNS supports many subscriber types.

Important examples from the Maarek slides include:

- [[SQS]]
- [[02-Compute/Lambda]]
- Kinesis Data Firehose
- HTTP / HTTPS endpoints
- Email
- SMS
- Mobile push notifications

Architecture:

SNS Topic  
↓  
├── SQS
├── Lambda
├── HTTP/S
├── Email
├── SMS
└── Firehose

### Exam Thinking

SNS is not only:

**Email notifications**

It is a general:

**Pub/Sub messaging service**

---

## SQS Subscriber

One of the most important architectures:

SNS Topic  
↓  
SQS Queue

SNS:

**Pushes a copy**

to the queue.

SQS then:

**Stores the message**

until a consumer processes it.

This combines:

**SNS Fan-Out**

with:

**SQS durability and buffering**

---

## Lambda Subscriber

SNS can invoke:

[[02-Compute/Lambda]]

when a message is published.

Architecture:

Producer  
↓  
SNS  
↓  
Lambda

This is useful for:

**Serverless event-driven processing**

### Exam Pattern

> **Publish event and immediately trigger serverless processing**
>
> → **SNS + Lambda**

---

## HTTP / HTTPS Subscriber

SNS can push notifications to:

**HTTP or HTTPS endpoints**

Architecture:

SNS  
↓  
HTTPS  
↓  
External / Internal Application Endpoint

This allows SNS to notify:

**Web applications or APIs**

---

## Email Subscriber

SNS can send:

**Email notifications**

This is useful for:

- Operational alerts
- Simple notifications
- Human-readable alerts

Example:

[[07-Monitoring/CloudWatch]] Alarm  
↓  
SNS  
↓  
Email

### Strong Exam Pattern

> **CloudWatch alarm must email an administrator**
>
> → **SNS**

---

## SMS Subscriber

SNS can send:

**SMS messages**

to mobile phones.

Think:

Event  
↓  
SNS  
↓  
SMS Notification

Useful for:

- Alerts
- Notifications
- User messaging

---

## Mobile Push Notifications

SNS can integrate with mobile push-notification platforms.

Think:

Application Event  
↓  
SNS  
↓  
Mobile Push Service  
↓  
User Device

---

## AWS Services Can Publish to SNS

Many AWS services can send notifications directly to SNS.

Examples in the Maarek slides include:

- [[07-Monitoring/CloudWatch]] Alarms
- [[S3]] Events
- Auto Scaling notifications
- CloudFormation state changes
- AWS Budgets
- [[02-Compute/Lambda]]
- DMS
- DynamoDB
- [[RDS]] Events

### Architecture Pattern

AWS Service  
↓  
SNS Topic  
↓  
Subscribers

---

## CloudWatch + SNS

Classic monitoring architecture:

CloudWatch Alarm  
↓  
SNS Topic  
↓  
Email / SMS / Lambda

Example:

EC2 CPU > Threshold  
↓  
CloudWatch Alarm  
↓  
SNS  
↓  
Operations Team

### Memory Trick

**CloudWatch detects**

**SNS tells someone**

---

## S3 + SNS

[[S3 Event Notifications]] can publish events to SNS.

Example:

Object Uploaded  
↓  
S3  
↓  
SNS  
↓  
Subscribers

This can be useful when:

**Multiple systems need to react to the same S3 event**

---

# SNS + SQS Fan-Out

This is one of the most important SAA messaging architectures.

Architecture:

Producer  
↓  
SNS Topic  
↓  
├── SQS Queue A
├── SQS Queue B
└── SQS Queue C

Each queue receives:

**Its own copy of the message**

Then each queue can have:

**Independent consumers**

---

## Why Fan-Out?

Suppose an order is created.

Three systems must process it:

1. Fraud Detection
2. Shipping
3. Analytics

If all consumers share:

**One SQS Queue**

they compete for messages.

That means:

One consumer receives the message

rather than:

Every system receiving a copy.

Instead:

Order Service  
↓  
SNS  
↓  
├── Fraud Queue
├── Shipping Queue
└── Analytics Queue

Now:

**Every application gets its own copy**

> [!tip] Memory Trick
> **SNS COPIES**
>
> **SQS HOLDS**

---

## Fan-Out Benefits

SNS + SQS provides:

- Loose coupling
- Message persistence
- Independent processing
- Independent retries
- Delayed processing
- Horizontal scaling
- Ability to add subscribers later

The Maarek slides emphasize:

> **Push once to SNS, receive in all subscribed SQS queues.**

---

## Fan-Out Durability

SNS itself is focused on:

**Message distribution**

SQS adds:

**Persistence**

If a consumer is unavailable:

SNS  
↓  
SQS Queue  
↓  
Message Waits

Consumer returns later:

SQS  
↓  
Consumer

This prevents the subscriber from needing to be continuously available.

---

## Queue Policy for SNS

When SNS publishes to SQS:

The SQS queue must allow:

**SNS to send messages**

through its:

**Queue Access Policy**

Architecture:

SNS Topic  
↓  
SQS Queue Policy  
↓  
Allow  
↓  
Message Stored

> [!warning] Exam Trap
> Creating the SNS subscription alone is not enough if the SQS resource policy does not allow the SNS topic to write.

---

## Cross-Region SNS to SQS

The Maarek slides highlight that SNS fan-out can support:

**Cross-Region delivery**

to SQS queues in other Regions.

Conceptually:

SNS Topic  
Region A  
↓  
SQS Queue  
Region B

This can help build:

**Multi-Region messaging architectures**

---

# S3 Event Fan-Out

Suppose the same S3 object-created event must reach:

- Thumbnail Processor
- Metadata Processor
- Audit Processor

Architecture:

[[S3]]  
↓  
SNS Topic  
↓  
├── SQS Queue A
├── SQS Queue B
└── Lambda

This provides:

**Fan-Out**

from one S3 event.

### Exam Pattern

> **Same S3 event must be processed independently by multiple systems**
>
> → **SNS Fan-Out**

---

# SNS to S3 Through Firehose

SNS can send messages through:

**Kinesis Data Firehose**

which can then deliver data into supported destinations such as:

[[S3]]

Architecture:

Publisher  
↓  
SNS  
↓  
Kinesis Data Firehose  
↓  
S3

### Exam Thinking

SNS does not directly act like:

**Permanent object storage**

If SNS data must land in S3:

A delivery architecture such as:

**Firehose**

may be appropriate.

---

# SNS Security

SNS supports:

**Encryption + Access Control**

Important security features include:

- HTTPS in transit
- KMS encryption at rest
- Client-side encryption
- IAM policies
- SNS Access Policies

---

## Encryption in Transit

SNS supports:

**HTTPS APIs**

for encrypting messages:

**In transit**

---

## Encryption at Rest

SNS can use:

[[06-Security/KMS]]

for:

**Server-side encryption at rest**

### Exam Pattern

> **SNS messages must be encrypted at rest**
>
> → **KMS**

---

## Client-Side Encryption

Applications can also encrypt messages:

**Before publishing**

and decrypt them:

**After receiving**

when the application requires control over:

**Encryption and decryption**

---

# SNS Access Control

Two major policy concepts are:

## IAM Policies

Control:

**Who can call SNS APIs**

Example:

Can this application:

`Publish`

to the topic?

---

## SNS Access Policies

These are:

**Resource-based policies**

attached to SNS topics.

They are useful for:

- Cross-account access
- Allowing AWS services to publish to SNS

### Memory Trick

**IAM = What can this identity do?**

**SNS Policy = Who can access this topic?**

---

# Cross-Account SNS

SNS Access Policies can allow:

**Another AWS account**

to access or publish to an SNS topic.

Architecture:

Account A  
↓  
SNS Access Policy  
↓  
SNS Topic in Account B

### Exam Pattern

> **Cross-account access to SNS Topic**
>
> → **SNS Access Policy**

---

# Allow AWS Services to Publish

SNS Access Policies can also authorize services such as:

[[S3]]

to publish notifications to:

**The SNS Topic**

Architecture:

S3  
↓  
SNS Resource Policy  
↓  
SNS Topic

---

# SNS FIFO Topics

[[SNS FIFO]] adds:

**Ordering + Deduplication**

to the pub/sub model.

FIFO means:

**First-In-First-Out**

Think:

SNS Standard  
→ Fan-Out

SNS FIFO  
→ Fan-Out + Ordering + Deduplication

---

## SNS FIFO Ordering

SNS FIFO uses:

**MessageGroupId**

just like:

[[SQS FIFO]]

Messages in the same group remain:

**Ordered**

### Memory Trick

**Group = Order**

---

## SNS FIFO Deduplication

SNS FIFO supports:

- Deduplication ID
- Content-based deduplication

This helps prevent:

**Duplicate message delivery into the FIFO workflow**

### Memory Trick

**Dedup = Duplicate Protection**

---

## SNS FIFO Subscribers

The Maarek slides highlight SNS FIFO support for:

- SQS Standard queues
- SQS FIFO queues

For the classic ordered fan-out architecture:

Think:

SNS FIFO  
↓  
Multiple SQS FIFO Queues

---

# SNS FIFO + SQS FIFO Fan-Out

This is a major architecture pattern.

Use it when you need:

**Fan-Out + Ordering + Deduplication**

Architecture:

Producer  
↓  
SNS FIFO Topic  
↓  
├── SQS FIFO Queue A
└── SQS FIFO Queue B

Each application receives:

**Its own ordered message stream**

### Killer Exam Clue

> **One ordered event stream must be processed independently by multiple applications**
>
> → **SNS FIFO + SQS FIFO**

---

# Standard Fan-Out vs FIFO Fan-Out

## Standard

[[SNS]]  
↓  
Multiple Standard SQS Queues

Best when:

**Ordering does not matter**

---

## FIFO

[[SNS FIFO]]  
↓  
Multiple [[SQS FIFO]] Queues

Best when:

**Order + deduplication matter**

### Memory Trick

**Standard = Broadcast**

**FIFO = Ordered Broadcast**

---

# SNS Message Filtering

By default:

A subscriber receives:

**Every message published to the topic**

But SNS supports:

**Subscription Filter Policies**

These are:

**JSON policies**

that determine which messages a subscription should receive.

---

## Why Message Filtering Matters

Suppose the topic receives:

Order Events

with states such as:

- Placed
- Cancelled
- Declined

Different subscribers care about:

**Different states**

Without filtering:

SNS  
↓  
Every Subscriber Gets Everything

With filtering:

SNS  
↓  
├── Placed Queue → Placed Messages
├── Cancelled Queue → Cancelled Messages
└── Declined Queue → Declined Messages

---

## Filter Policy

A subscription can have a:

**Filter Policy**

Example concept:

State = Placed

Only matching messages are delivered to:

**That subscription**

### Memory Trick

**SNS Filter = Subscriber chooses what it cares about**

---

## No Filter Policy

If a subscription does NOT have:

**A filter policy**

it receives:

**Every message**

published to the SNS topic.

> [!tip] Exam Rule
> **No filter = Receive all**

---

## Message Filtering Architecture

Buying Service  
↓  
SNS Topic  
↓  
Order Event

Message:

Order 1036  
State: Placed

Subscribers:

Placed Queue  
Filter: State = Placed  
→ Receives ✅

Cancelled Queue  
Filter: State = Cancelled  
→ Does Not Receive ❌

Declined Queue  
Filter: State = Declined  
→ Does Not Receive ❌

All-Messages Queue  
No Filter  
→ Receives ✅

---

# SNS vs SQS

This is the biggest messaging distinction.

## SNS

Model:

**Pub/Sub**

Messages:

**Pushed**

Purpose:

**One → Many**

Think:

Broadcast / Fan-Out

---

## [[SQS]]

Model:

**Queue**

Messages:

**Pulled**

Purpose:

**Producer → Work Queue → Consumers**

Think:

Buffer / Decouple

### Memory Trick

**SNS = ANNOUNCE**

**SQS = WAIT IN LINE**

---

# SNS vs EventBridge

Both can distribute events, but they have different strengths.

## SNS

Think:

- Pub/Sub
- Direct fan-out
- Simple distribution
- Push to subscribers

---

## [[20-SAA/10-Messaging/EventBridge]]

Think:

- Event bus
- Advanced routing
- Event patterns
- Many AWS / SaaS sources
- Archive
- Replay
- Schema Registry

### Exam Shortcut

**Simple broadcast / fan-out**
→ SNS

**Advanced event routing**
→ EventBridge

---

# SNS vs Kinesis

## SNS

Think:

**Push notifications / Pub-Sub**

Messages are distributed to subscribers.

---

## [[Kinesis]]

Think:

**Real-time data stream**

Supports:

- Retention
- Replay
- Ordered streaming
- Multiple stream consumers

### Exam Shortcut

**Broadcast event**
→ SNS

**Streaming analytics**
→ Kinesis

---

# SNS vs SES

This can be a sneaky exam distinction.

## SNS

Can send:

**Notifications via email**

Best for:

- Alerts
- Notifications
- Operational messaging

---

## SES

Designed for:

**Email sending at application scale**

Think:

- Marketing email
- Transactional email
- Rich email workflows

### Memory Trick

**SNS = Notify**

**SES = Email Service**

---

# Architecture Thinking

## Scenario 1 — One Order, Many Systems

An order-created event must go to:

- Fraud
- Shipping
- Analytics

Each needs:

**Its own copy**

**Choose → SNS**

For reliable independent processing:

**SNS + multiple SQS queues**

---

## Scenario 2 — Email an Administrator

A CloudWatch Alarm enters:

**ALARM**

An administrator must receive:

**Email**

**Choose → CloudWatch + SNS**

---

## Scenario 3 — Multiple Durable Consumers

Three applications need the same event.

Each application may temporarily go offline.

**Choose:**

SNS  
↓  
Three SQS Queues

Why?

SNS:

**Fan-Out**

SQS:

**Durability + Retries**

---

## Scenario 4 — One Work Item, One Worker

A job should be processed by:

**One consumer**

not every consumer.

Do NOT choose SNS alone.

Choose:

[[SQS]]

---

## Scenario 5 — Filter Subscriber Messages

One topic contains:

- Placed orders
- Cancelled orders
- Declined orders

Each subscriber only wants:

**One category**

**Choose → SNS Subscription Filter Policies**

---

## Scenario 6 — Ordered Fan-Out

A financial workflow needs:

- One event to many applications
- Strict ordering
- Deduplication

**Choose:**

[[SNS FIFO]]  
+  
Multiple [[SQS FIFO]] Queues

---

## Scenario 7 — Event Replay

Applications need to:

**Replay old events**

SNS is not the strongest choice.

Think:

[[Kinesis]]

or:

[[20-SAA/10-Messaging/EventBridge]]

depending on the architecture.

---

## Scenario 8 — S3 Event to Multiple Queues

A single S3 event must be delivered to:

**Multiple independent SQS queues**

Architecture:

S3  
↓  
SNS  
↓  
Multiple SQS Queues

**Choose → SNS Fan-Out**

---

# Scenario Recognition

Immediately think:

[[SNS]]

when you see:

- Pub/Sub
- Publish / Subscribe
- One-to-many
- Fan-Out
- Broadcast
- Multiple receivers
- Push notifications
- Email notification
- SMS
- SQS subscribers
- Lambda subscribers

Immediately think:

[[SNS FIFO]]

when you see:

- Ordered fan-out
- Deduplication
- MessageGroupId
- FIFO subscribers
- Multiple ordered consumers

Immediately think:

**Message Filtering**

when you see:

- Same topic
- Different subscribers
- Each subscriber wants different message categories

---

# Exam Traps

## Trap 1 — SNS Is a Work Queue

False.

SNS is:

**Pub/Sub**

For a durable work queue:

[[SQS]]

---

## Trap 2 — SNS Consumers Poll the Topic

False.

SNS generally:

**Pushes**

notifications to subscriptions.

SQS consumers:

**Poll**

---

## Trap 3 — One SQS Queue Gives Every Application Its Own Copy

False.

Consumers of the same queue:

**Compete for messages**

Need each application to get a copy?

→ SNS + multiple SQS queues

---

## Trap 4 — SNS + SQS Fan-Out Loses SQS Benefits

False.

Each SQS queue still provides:

- Persistence
- Delayed processing
- Retries
- Independent consumers

---

## Trap 5 — Every SNS Subscription Must Receive Every Message

False.

Use:

**Subscription Filter Policies**

---

## Trap 6 — No Filter Policy Means No Messages

False.

No filter policy means:

**Receive every message**

---

## Trap 7 — SNS Standard Guarantees Strict Ordering

False.

Need ordered pub/sub?

Think:

[[SNS FIFO]]

---

## Trap 8 — SNS FIFO Means SQS Is No Longer Needed for Durable Fan-Out

Not necessarily.

For durable independent ordered consumers:

SNS FIFO  
+  
SQS FIFO

is a powerful architecture.

---

## Trap 9 — SNS Stores Messages Like a Queue Until Consumers Return

Do not treat SNS as a replacement for:

**SQS persistence**

If a subscriber needs durable buffering:

Use:

**SNS + SQS**

---

## Trap 10 — SNS Email and SES Solve the Same Problem

False.

SNS:

**Notification**

SES:

**Application email service**

---

# SNS Quick Cheat Sheet

| Exam Clue | Answer |
|---|---|
| Pub/Sub | SNS |
| One → Many | SNS |
| Broadcast | SNS |
| Push Messages | SNS |
| Fan-Out | SNS |
| Durable Fan-Out | SNS + SQS |
| Email Alert | SNS |
| SMS | SNS |
| Lambda Subscriber | SNS |
| HTTP/S Subscriber | SNS |
| SQS Subscriber | SNS |
| Cross-Account Topic Access | SNS Access Policy |
| Encryption at Rest | KMS |
| Ordered Fan-Out | SNS FIFO |
| Deduplication + Fan-Out | SNS FIFO |
| Different Messages per Subscriber | Filter Policy |
| No Filter Policy | Receive All |
| One Work Item for One Consumer | SQS |
| Replayable Streaming Data | Kinesis |
| Advanced Event Routing | EventBridge |

---

## SNS vs SQS Quick Comparison

| Requirement | SNS | SQS |
|---|---:|---:|
| Pub/Sub | ✅ | ❌ |
| Queue | ❌ | ✅ |
| Push | ✅ | ❌ |
| Pull / Poll | ❌ | ✅ |
| One → Many | ✅ | Not by itself |
| Buffer Work | ❌ | ✅ |
| Fan-Out | ✅ | ❌ |
| Message Persistence for Consumers | Use SQS Subscriber | ✅ |
| Multiple Independent Copies | ✅ | ❌ |
| Worker Queue | ❌ | ✅ |

---

## Master Memory Trick

> [!tip] SNS Master Memory Trick
> Imagine a store manager grabs the PA microphone.
>
> Manager:
>
> **PUBLISHER**
>
> ↓
>
> PA System:
>
> **SNS TOPIC**
>
> ↓
>
> Everyone listening:
>
> **SUBSCRIBERS**
>
> The manager makes:
>
> **ONE ANNOUNCEMENT**
>
> and:
>
> **MANY PEOPLE HEAR IT**

Now add SQS:

> **SNS**
> → Copies the announcement
>
> **SQS**
> → Gives each department its own inbox

So remember:

> **SNS = PUSH + PUB/SUB + FAN-OUT**
>
> **SQS = PULL + QUEUE + BUFFER**

If everyone needs:

**The same event**

→ SNS

If everyone needs:

**Their own durable copy**

→ SNS + SQS

If order matters too:

→ SNS FIFO + SQS FIFO

If subscribers only want certain events:

→ SNS Filter Policy

---

## Related Notes

- [[SQS]]
- [[SQS FIFO]]
- [[SNS FIFO]]
- [[Kinesis]]
- [[20-SAA/10-Messaging/EventBridge]]
- [[02-Compute/Lambda]]
- [[S3]]
- [[S3 Event Notifications]]
- [[07-Monitoring/CloudWatch]]
- [[06-Security/KMS]]
- [[SES]]
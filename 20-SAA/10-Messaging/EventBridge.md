## What Problem Does It Solve?

[[20-SAA/10-Messaging/EventBridge]] is a:

**Serverless event bus service**

used to:

**Receive events, match them against rules, and route them to targets**

It solves the problem:

> **"How can I react to events from AWS services, custom applications, or SaaS providers and automatically route those events to the right downstream services?"**

Architecture:

Event Source  
↓  
EventBridge Event Bus  
↓  
Rule / Event Pattern  
↓  
Target

> [!tip] Memory Trick
> **EventBridge = Event Traffic Controller**
>
> Event comes in.
>
> Rule decides where it goes.

---

## EventBridge Overview

Amazon EventBridge is the evolution of:

**CloudWatch Events**

For SAA, think of EventBridge as:

**Event routing**

rather than:

- A work queue
- A pub/sub topic
- A retained streaming platform

Its major role is:

> **React to events based on rules and route matching events to targets.**

---

## Event-Driven Architecture

EventBridge is a core building block for:

**Event-driven architectures**

Instead of one application constantly asking:

> **"Did something happen?"**

an event is generated when:

**Something happens**

Example:

EC2 Instance  
↓  
Changes State  
↓  
EventBridge Event  
↓  
Rule Matches  
↓  
Lambda Runs

This reduces:

**Polling**

and improves:

**Loose coupling**

---

## Core EventBridge Architecture

Think:

Source  
↓  
Event Bus  
↓  
Rule  
↓  
Target

### Source

Produces the event.

### Event Bus

Receives events.

### Rule

Matches events based on:

- Event patterns
- Scheduling

### Target

Receives the matching event.

---

## Events

An EventBridge event is structured as:

**JSON**

Example:

~~~json
{
  "source": "aws.ec2",
  "detail-type": "EC2 Instance State-change Notification",
  "detail": {
    "state": "stopped"
  }
}
~~~

The exam takeaway:

> **EventBridge events contain structured fields that rules can inspect.**

---

## Event Sources

EventBridge can receive events from:

- AWS services
- Custom applications
- SaaS partners

Examples include:

- [[EC2]]
- CodeBuild
- [[S3]]
- Trusted Advisor
- [[06-Security/CloudTrail]]
- Custom applications
- SaaS integrations

---

## AWS Service Events

AWS services can generate events when:

**Something changes**

Examples:

EC2  
↓  
Instance State Change

CodeBuild  
↓  
Build Failed

S3  
↓  
Object Event

Trusted Advisor  
↓  
New Finding

EventBridge can detect these events and route them to:

**Targets**

---

## CloudTrail + EventBridge

[[06-Security/CloudTrail]] records:

**AWS API activity**

EventBridge can react to:

**That API activity**

Architecture:

User / Application  
↓  
AWS API Call  
↓  
CloudTrail  
↓  
EventBridge  
↓  
Rule  
↓  
Target

Example:

`DeleteTable` API Call  
↓  
CloudTrail  
↓  
EventBridge  
↓  
[[SNS]]  
↓  
Security Alert

> [!tip] Exam Pattern
> **React to a specific AWS API call**
>
> → **CloudTrail + EventBridge**

---

## Event Patterns

An EventBridge rule can use an:

**Event Pattern**

to determine whether an event matches.

Conceptually:

Incoming Event  
↓  
Event Pattern  
↓  
Match?

Yes  
→ Send to Target

No  
→ Ignore for that rule

---

## Event Pattern Example

Suppose you only care about:

**EC2 instances entering the stopped state**

Rule checks:

Source:

`aws.ec2`

Detail Type:

`EC2 Instance State-change Notification`

State:

`stopped`

Architecture:

All EC2 State Events  
↓  
EventBridge  
↓  
Rule Filters  
↓  
Stopped Events Only  
↓  
Target

---

## EventBridge Rules

Rules define:

**Which events trigger which targets**

Think:

IF:

Event matches pattern

THEN:

Send event to target

> [!tip] Memory Trick
> **RULE = IF EVENT → THEN TARGET**

---

## Example Event Sources

Common exam-style EventBridge sources include:

- EC2 state changes
- CodeBuild failures
- S3 events
- Trusted Advisor findings
- CloudTrail API activity
- Scheduled events

The broader concept:

> **EventBridge reacts to operational and business events across AWS.**

---

## EventBridge Targets

EventBridge supports many target types.

Examples include:

- [[02-Compute/Lambda]]
- AWS Batch
- ECS Tasks
- [[SQS]]
- [[SNS]]
- [[20-SAA/10-Messaging/Kinesis Data Streams]]
- [[Step Functions]]
- CodePipeline
- CodeBuild
- Systems Manager
- EC2 Actions

Architecture:

EventBridge  
↓  
Rule  
↓  
Target

---

## EventBridge + Lambda

A classic serverless pattern:

Event  
↓  
EventBridge  
↓  
Rule  
↓  
[[02-Compute/Lambda]]

Example:

EC2 Stops  
↓  
EventBridge  
↓  
Lambda  
↓  
Automated Remediation

### Killer Exam Pattern

> **Automatically run code when a specific AWS event occurs**
>
> → **EventBridge + Lambda**

---

## EventBridge + SQS

EventBridge can route matching events into:

[[SQS]]

Architecture:

Event Source  
↓  
EventBridge  
↓  
Rule  
↓  
SQS  
↓  
Consumer

EventBridge provides:

**Routing**

SQS provides:

- Buffering
- Durability
- Async processing

### Memory Trick

**EventBridge ROUTES**

**SQS HOLDS**

---

## EventBridge + SNS

EventBridge can route matching events to:

[[SNS]]

Architecture:

AWS Event  
↓  
EventBridge  
↓  
SNS  
↓  
Subscribers

Use this when:

**A matching event should trigger notifications or fan-out**

---

## EventBridge + Step Functions

EventBridge can start:

[[Step Functions]]

Architecture:

Business Event  
↓  
EventBridge  
↓  
Step Functions  
↓  
Workflow

Use this when an event should launch:

**A multi-step workflow**

---

## EventBridge + ECS

EventBridge can trigger:

**ECS Tasks**

Architecture:

Event  
↓  
EventBridge  
↓  
ECS Task

This is useful for:

**Containerized event-driven workloads**

---

## Event Buses

EventBridge supports different:

**Event buses**

Important SAA types:

1. Default Event Bus
2. Partner Event Bus
3. Custom Event Bus

---

## Default Event Bus

The:

**Default Event Bus**

primarily receives events from:

**AWS services**

Architecture:

AWS Services  
↓  
Default Event Bus  
↓  
Rules  
↓  
Targets

> [!tip] Memory Trick
> **AWS Services → Default Bus**

---

## Partner Event Bus

Partner Event Buses are used with:

**Supported SaaS providers**

Architecture:

SaaS Partner  
↓  
Partner Event Bus  
↓  
Rules  
↓  
Targets

Think:

**External SaaS events entering AWS**

---

## Custom Event Bus

A:

**Custom Event Bus**

can receive events from:

**Your own applications**

Architecture:

Custom Application  
↓  
PutEvents  
↓  
Custom Event Bus  
↓  
Rules  
↓  
Targets

> [!tip] Memory Trick
> **Your App → Custom Bus**

---

## Event Bus Comparison

| Event Bus | Main Source |
|---|---|
| Default | AWS Services |
| Partner | SaaS Partners |
| Custom | Your Applications |

> [!tip] Master Memory Trick
> **AWS → DEFAULT**
>
> **SaaS → PARTNER**
>
> **Your App → CUSTOM**

---

## Cross-Account EventBridge

Event buses can use:

**Resource-Based Policies**

to allow events from:

**Other AWS accounts**

Architecture:

Account A  
↓  
PutEvents  
↓  
Event Bus in Account B

This enables:

**Centralized multi-account event architectures**

---

## Centralized Multi-Account Events

Example:

Account A  
↓  

Account B  
↓  

Account C  
↓  

Central Event Bus  
↓  
Security / Operations

Use this when:

**Multiple AWS accounts should send events to one central account**

### Exam Pattern

> **Aggregate events from multiple AWS accounts into one central account**
>
> → **EventBridge + Resource-Based Policy**

---

## Resource-Based Policies

An EventBridge bus can have:

**A Resource-Based Policy**

This controls:

**Who can send events to the bus**

Example:

Allow another AWS account to call:

`PutEvents`

on:

`central-event-bus`

### Memory Trick

**Event Bus Policy = Who can PUT events here?**

---

## Event Archive

EventBridge can:

**Archive events**

sent to an event bus.

You can archive:

- All events
- Filtered events

Conceptually:

Event  
↓  
Event Bus  
↓  
Archive

This gives you:

**Historical event retention**

---

## Event Replay

Archived events can later be:

**Replayed**

Architecture:

Archived Events  
↓  
Replay  
↓  
Event Bus  
↓  
Rules  
↓  
Targets

Useful when:

- A consumer had a bug
- Processing logic changed
- A workflow needs to be rerun
- Testing requires historical events

> [!tip] Killer Exam Clue
> **Need to reprocess previously archived business events**
>
> → **EventBridge Archive + Replay**

---

## Archive vs Replay

### Archive

**Save events**

### Replay

**Send saved events back through the event bus**

### Memory Trick

**ARCHIVE = SAVE**

**REPLAY = RUN AGAIN**

---

## Schema Registry

EventBridge provides a:

**Schema Registry**

It helps applications understand:

**The structure of event data**

---

## Schema Discovery

EventBridge can:

**Analyze events**

and infer:

**Their schemas**

Architecture:

Events  
↓  
EventBridge  
↓  
Schema Discovery  
↓  
Schema Registry

---

## Why Schemas Matter

Applications need to understand:

- What fields exist
- What those fields are called
- How the JSON is structured

The Schema Registry helps developers work with:

**Known event structures**

---

## Code Generation

The Schema Registry can help generate:

**Code bindings**

for supported application development workflows.

This helps applications understand:

**The expected event structure**

### Exam Pattern

> **Automatically discover event structure and generate usable application bindings**
>
> → **EventBridge Schema Registry**

---

## Schema Versioning

Schemas can be:

**Versioned**

This matters when:

**Event formats evolve**

Example:

Version 1:

- Customer ID
- Order ID

Version 2:

- Customer ID
- Order ID
- Region

---

## Scheduling

Classic EventBridge capabilities include:

**Scheduled rules**

using:

- Rate expressions
- Cron expressions

Example:

Every Hour  
↓  
EventBridge  
↓  
Lambda

or:

Every 4 Hours  
↓  
EventBridge  
↓  
Target

> [!tip] Memory Trick
> **EventBridge reacts to an EVENT or a CLOCK**

---

## Scheduled Tasks

Use EventBridge scheduling for:

- Recurring Lambda invocations
- Periodic scripts
- Maintenance jobs
- Scheduled workflows

### Exam Pattern

> **Run a serverless task on a recurring schedule**
>
> → **EventBridge scheduled rule / scheduler-style architecture**

---

## EventBridge vs SNS

This is an important comparison.

### [[SNS]]

Think:

- Pub/Sub
- Fan-Out
- Push notifications
- Simple one-to-many messaging

### EventBridge

Think:

- Event bus
- Rules
- Event patterns
- Content-based routing
- AWS / SaaS / custom events
- Archive / replay

### Memory Trick

**SNS = BROADCAST**

**EventBridge = ROUTE**

---

## EventBridge vs SNS Filtering

SNS can also:

**Filter subscriptions**

So distinguish them carefully.

### SNS Filtering

Think:

**Selective Pub/Sub**

One SNS Topic  
↓  
Filtered Subscribers

### EventBridge

Think:

**Event bus routing**

Events  
↓  
Event Bus  
↓  
Rules  
↓  
Targets

### Exam Shortcut

**Simple fan-out with filtering**
→ SNS

**Broader event-routing architecture**
→ EventBridge

---

## EventBridge vs SQS

### [[SQS]]

Think:

- Queue
- Buffer
- Backpressure
- Worker decoupling
- Work waits for consumers

### EventBridge

Think:

- Routing
- Rules
- Event patterns
- Triggering targets

### Memory Trick

**EventBridge = Where should this event GO?**

**SQS = Where should this work WAIT?**

---

## EventBridge + SQS

These services frequently work together.

Architecture:

Event  
↓  
EventBridge  
↓  
Rule  
↓  
SQS  
↓  
Worker

EventBridge:

**Selects + routes**

SQS:

**Buffers + persists**

---

## EventBridge vs Kinesis

### [[20-SAA/10-Messaging/Kinesis Data Streams]]

Think:

- Continuous streaming
- High-volume records
- Retention
- Replay
- Partition keys
- Streaming analytics

### EventBridge

Think:

- Discrete events
- Business events
- Operational events
- Rule-based routing
- Event buses

### Exam Shortcut

**Continuous telemetry**
→ Kinesis

**EC2 stopped / order created / build failed**
→ EventBridge

---

## EventBridge Replay vs Kinesis Replay

Both support replay-like behavior, but the model differs.

### EventBridge

Replays:

**Archived discrete events**

Think:

Business / operational event history

### Kinesis

Replays:

**Retained stream records**

Think:

Continuous streaming history

### Memory Trick

**EventBridge = EVENT history**

**Kinesis = STREAM history**

---

## EventBridge vs CloudTrail

These services are complementary.

### [[06-Security/CloudTrail]]

Records:

**AWS API activity**

Question:

> **Who called what API?**

### EventBridge

Reacts to:

**Events**

Question:

> **What should happen now?**

Architecture:

API Call  
↓  
CloudTrail  
↓  
EventBridge  
↓  
Target

---

## EventBridge vs Lambda

EventBridge does NOT replace:

[[02-Compute/Lambda]]

EventBridge:

**Detects and routes**

Lambda:

**Runs code**

Architecture:

Event  
↓  
EventBridge  
↓  
Lambda  
↓  
Action

### Memory Trick

**EventBridge decides WHEN**

**Lambda decides WHAT TO DO**

---

## EventBridge vs Step Functions

### EventBridge

Think:

**Event routing**

### [[Step Functions]]

Think:

**Workflow orchestration**

Together:

Event  
↓  
EventBridge  
↓  
Step Functions  
↓  
Multi-Step Workflow

---

## Architecture Thinking

### Scenario 1 — EC2 State Change

A Lambda function should run whenever:

**An EC2 instance enters the stopped state**

Choose:

EC2  
↓  
EventBridge  
↓  
Lambda

---

### Scenario 2 — Failed Build

Developers need an alert whenever:

**CodeBuild fails**

Choose:

CodeBuild  
↓  
EventBridge  
↓  
SNS  
↓  
Developers

---

### Scenario 3 — API Security Alert

Security wants an alert whenever someone calls:

**DeleteTable**

Choose:

API Call  
↓  
CloudTrail  
↓  
EventBridge  
↓  
SNS  
↓  
Security Team

---

### Scenario 4 — Central Multi-Account Events

Security events from multiple AWS accounts should be sent to:

**One central account**

Choose:

EventBridge  
+  
Resource-Based Policy  
+  
Central Event Bus

---

### Scenario 5 — Replay Events

A consumer processed order events incorrectly.

The events were archived.

After fixing the logic:

**Replay the archive**

through EventBridge.

---

### Scenario 6 — SaaS Events

A supported SaaS provider generates events that must trigger AWS workflows.

Think:

**Partner Event Bus**

---

### Scenario 7 — Custom Application Events

Your application publishes:

`OrderCreated`

events.

Think:

**Custom Event Bus**

---

### Scenario 8 — Scheduled Lambda

A Lambda function must run:

**Every four hours**

Think:

**EventBridge scheduling**

---

### Scenario 9 — Worker Backlog

Jobs must wait safely while consumers catch up.

Do NOT use EventBridge alone as the queue.

Choose:

[[SQS]]

or:

EventBridge → SQS

---

### Scenario 10 — Clickstream Data

Millions of click events require:

- Streaming analytics
- Retention
- Replay

Think:

[[20-SAA/10-Messaging/Kinesis Data Streams]]

not EventBridge.

---

### Scenario 11 — Simple Broadcast

One event needs to be sent to multiple subscribers with simple pub/sub behavior.

Think:

[[SNS]]

---

## Scenario Recognition

Immediately think:

[[20-SAA/10-Messaging/EventBridge]]

when you see:

- Event bus
- Event rule
- Event pattern
- React to AWS events
- EC2 state change
- CodeBuild failure
- Trusted Advisor finding
- CloudTrail API event
- SaaS events
- Custom application events
- Cross-account events
- Archive
- Replay
- Schema Registry
- Scheduled events

### Strongest Exam Pattern

> **"Route AWS, SaaS, or custom application events to different targets based on event content."**
>
> → **EventBridge**

---

## Exam Traps

### Trap 1 — EventBridge Is a Queue

False.

EventBridge:

**Routes events**

SQS:

**Queues work**

---

### Trap 2 — EventBridge Is Just SNS

False.

SNS:

**Pub/Sub fan-out**

EventBridge:

**Event bus + rules + patterns**

---

### Trap 3 — EventBridge Is a Streaming Data Store

False.

For retained high-volume streaming:

[[20-SAA/10-Messaging/Kinesis Data Streams]]

---

### Trap 4 — CloudTrail Performs Remediation

False.

CloudTrail:

**Records**

EventBridge:

**Reacts**

Lambda / SSM / other targets:

**Perform actions**

---

### Trap 5 — Custom Apps Must Use the Default Bus

False.

Use:

**Custom Event Bus**

---

### Trap 6 — SaaS Events Belong on the Default Bus

Think:

**Partner Event Bus**

---

### Trap 7 — EventBridge Cannot Replay Events

False.

It supports:

**Archive + Replay**

---

### Trap 8 — Archive and DLQ Are the Same

False.

Archive:

**Stores events for later replay**

DLQ:

**Captures failed deliveries**

---

### Trap 9 — Schema Registry Routes Events

False.

Schema Registry:

**Describes event structure**

Rules:

**Route events**

---

### Trap 10 — EventBridge Must Trigger Lambda

False.

Lambda is only one target.

Other targets include:

- SQS
- SNS
- Kinesis
- Step Functions
- ECS
- Batch
- CodePipeline
- CodeBuild
- Systems Manager

---

## Quick Cheat Sheet

| Exam Clue | Answer |
|---|---|
| Event Bus | EventBridge |
| Event Pattern | EventBridge Rule |
| Route Events | EventBridge |
| AWS Service Events | Default Bus |
| SaaS Partner Events | Partner Bus |
| Custom Application Events | Custom Bus |
| Cross-Account Event Bus | Resource-Based Policy |
| Central Multi-Account Events | EventBridge |
| Save Events | Archive |
| Reprocess Saved Events | Replay |
| Discover Event Structure | Schema Registry |
| EC2 State Change Automation | EventBridge |
| React to API Calls | CloudTrail + EventBridge |
| Scheduled Task | EventBridge |
| Buffer Work | SQS |
| Pub/Sub Fan-Out | SNS |
| Real-Time Streaming | Kinesis |

---

## Event Bus Quick Comparison

| Bus | Main Source |
|---|---|
| Default Event Bus | AWS Services |
| Partner Event Bus | SaaS Partners |
| Custom Event Bus | Custom Applications |

---

## Messaging Decision Table

| Requirement | Best Choice |
|---|---|
| Worker Queue | SQS |
| Ordered Worker Queue | SQS FIFO |
| Pub/Sub Fan-Out | SNS |
| Ordered Fan-Out | SNS FIFO |
| Real-Time Data Stream | Kinesis Data Streams |
| Managed Stream Delivery | Kinesis Data Firehose |
| Event Routing | EventBridge |
| Event Archive / Replay | EventBridge |

---

## Master Memory Trick

> [!tip] EventBridge Master Memory Trick
> Imagine an airport.
>
> Events arrive like:
>
> **AIRPLANES**
>
> The airport is:
>
> **EVENT BUS**
>
> The routing logic is:
>
> **RULE**
>
> The destination gate is:
>
> **TARGET**

So remember:

> **EVENT BUS**
> → Receives
>
> **RULE**
> → Decides
>
> **TARGET**
> → Acts

Then remember:

> **AWS SERVICES**
> → DEFAULT BUS
>
> **SAAS**
> → PARTNER BUS
>
> **YOUR APPS**
> → CUSTOM BUS

And the messaging shortcut:

> **SQS**
> → WAIT
>
> **SNS**
> → BROADCAST
>
> **KINESIS**
> → STREAM
>
> **FIREHOSE**
> → DELIVER
>
> **EVENTBRIDGE**
> → ROUTE

Finally:

> **ARCHIVE**
> → SAVE
>
> **REPLAY**
> → RUN AGAIN
>
> **SCHEMA REGISTRY**
> → UNDERSTAND EVENT STRUCTURE

---

## Related Notes

- [[SQS]]
- [[SQS FIFO]]
- [[SNS]]
- [[SNS FIFO]]
- [[SNS Message Filtering]]
- [[20-SAA/10-Messaging/Kinesis Data Streams]]
- [[20-SAA/10-Messaging/Kinesis Data Firehose]]
- [[02-Compute/Lambda]]
- [[Step Functions]]
- [[06-Security/CloudTrail]]
- [[S3]]
- [[EC2]]
- [[07-Monitoring/CloudWatch]]
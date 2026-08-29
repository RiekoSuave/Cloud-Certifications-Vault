## What Problem Does It Solve?

[[Lambda Destinations]] lets you route the result of an:

**Asynchronous Lambda invocation**

to another AWS service after the function finishes.

You can configure separate destinations for:

- Success
- Failure

Architecture:

Async Event  
↓  
Lambda  
↓  
Invocation Result  
↓  
├── Success Destination
└── Failure Destination

> [!tip] Memory Trick
> **Destinations = Where does the result go AFTER Lambda finishes?**

---

## Core Concept

With asynchronous invocation:

Source  
↓  
Lambda  
↓  
Function Executes  
↓  
Result Produced

Lambda Destinations can then route:

**The invocation result**

to another target.

This is different from:

**What triggered Lambda**

Destinations focus on:

> **What happens after Lambda finishes**

---

## Supported Invocation Type

Lambda Destinations are associated primarily with:

**Asynchronous invocations**

Examples include events from:

- [[S3]]
- [[SNS]]
- [[20-SAA/10-Messaging/EventBridge]]
- Direct asynchronous Lambda invocation

### Killer Exam Clue

> **Route the result of an asynchronous Lambda invocation**
>
> → **Lambda Destinations**

---

## Success Destination

A success destination receives information after:

**The asynchronous Lambda invocation succeeds**

Architecture:

Event  
↓  
Lambda  
↓  
Success  
↓  
Destination

This can be used to:

- Trigger another workflow
- Notify another system
- Send event to an event bus
- Continue asynchronous processing

---

## Failure Destination

A failure destination receives information after:

**The asynchronous invocation ultimately fails**

Architecture:

Event  
↓  
Lambda  
↓  
Retries  
↓  
Failure  
↓  
Failure Destination

This helps with:

- Troubleshooting
- Recovery
- Alerting
- Reprocessing
- Workflow branching

---

## Supported Destination Types

Lambda Destinations can route supported asynchronous results to services such as:

- [[SQS]]
- [[SNS]]
- [[20-SAA/10-Messaging/EventBridge]]
- Another [[Lambda]] function

Think:

Lambda  
↓  
Result  
↓  
AWS Messaging / Compute Service

---

## Destination to SQS

Architecture:

Async Lambda  
↓  
Success / Failure  
↓  
[[SQS]]

Use when the result should:

**Wait durably for downstream processing**

### Memory Trick

**Destination → SQS = Hold the result**

---

## Destination to SNS

Architecture:

Lambda  
↓  
Success / Failure  
↓  
[[SNS]]  
↓  
Subscribers

Use when the result needs:

**Fan-out or notifications**

### Memory Trick

**Destination → SNS = Broadcast the result**

---

## Destination to EventBridge

Architecture:

Lambda  
↓  
Result  
↓  
[[20-SAA/10-Messaging/EventBridge]]  
↓  
Rules  
↓  
Targets

Use when the result should enter:

**A broader event-routing architecture**

### Memory Trick

**Destination → EventBridge = Route the result**

---

## Destination to Another Lambda

Architecture:

Lambda A  
↓  
Result  
↓  
Lambda B

This can continue:

**Event-driven processing**

However, if the workflow becomes complex:

Think:

[[Step Functions]]

instead of creating:

**Large chains of directly connected functions**

---

# Destination Payload

Lambda Destinations can provide more information than:

**The original event alone**

The destination record can include context about:

- Original request
- Function response
- Invocation status
- Error details
- Metadata

This makes destinations useful for:

**Observability and downstream processing**

---

# Why Destinations Are Useful

Imagine:

S3  
↓  
Lambda Image Processor

If processing succeeds:

→ Send event to EventBridge

If processing fails:

→ Send message to SQS

Architecture:

S3 Event  
↓  
Lambda  
↓  
├── Success → EventBridge
└── Failure → SQS

This allows:

**Different workflows for different outcomes**

---

# Lambda Destinations vs DLQ

This is the biggest exam comparison for this note.

## Dead-Letter Queue

A DLQ primarily captures:

**Failed asynchronous events**

Think:

Failure only

---

## Lambda Destinations

Can route:

- Successful invocation results
- Failed invocation results

Think:

**Outcome routing**

### Memory Trick

**DLQ = FAILED EVENT**

**DESTINATION = SUCCESS OR FAILURE RESULT**

---

# DLQ vs Destinations Comparison

| Feature | DLQ | Lambda Destinations |
|---|---:|---:|
| Failure Handling | ✅ | ✅ |
| Success Handling | ❌ | ✅ |
| Original Event Preservation | ✅ | ✅ |
| Invocation Result Context | Limited | More Context |
| Route Success Separately | ❌ | ✅ |
| Route Failure Separately | ✅ | ✅ |

### Killer Exam Shortcut

> **Need only failed async events**
>
> → DLQ
>
> **Need success AND failure routing**
>
> → Lambda Destinations

---

# Destination vs Event Source

Do not confuse:

**Where Lambda gets an event from**

with:

**Where Lambda sends the result**

Example:

S3  
↓  
Lambda  
↓  
EventBridge

Here:

S3 = Event Source

EventBridge = Destination

### Memory Trick

**SOURCE = BEFORE**

**DESTINATION = AFTER**

---

# Destination vs Event Source Mapping

These are completely different.

## Event Source Mapping

Controls:

**How Lambda receives records**

Examples:

- SQS
- Kinesis
- DynamoDB Streams

---

## Destinations

Control:

**Where asynchronous invocation outcomes go**

Examples:

- SQS
- SNS
- EventBridge
- Lambda

### Memory Trick

**EVENT SOURCE MAPPING = IN**

**DESTINATION = OUT**

---

# Asynchronous Retry Flow

Typical async invocation:

Event  
↓  
Lambda  
↓  
Failure  
↓  
Automatic Retry  
↓  
Failure Again  
↓  
Retry Policy Exhausted  
↓  
Failure Destination

The destination is used after:

**Invocation processing concludes**

---

# Success Destination Example

Suppose:

User uploads:

`video.mp4`

Architecture:

S3  
↓  
Lambda Transcoder Metadata Processor  
↓  
Success  
↓  
EventBridge  
↓  
Workflow Continues

The successful invocation creates:

**A new event for downstream processing**

---

# Failure Destination Example

Suppose:

S3  
↓  
Lambda  
↓  
Fails Repeatedly  
↓  
SQS Failure Queue

Operations can later:

- Inspect
- Repair issue
- Reprocess

This provides:

**Durable failure handling**

---

# Destination + Step Functions

If a successful Lambda invocation should launch:

**A multi-step workflow**

a useful pattern is:

Lambda  
↓  
EventBridge / Other Integration  
↓  
[[Step Functions]]

However, if orchestration is central to the application:

It may be cleaner to let Step Functions:

**Coordinate Lambda directly**

---

# Destination + SNS Notifications

Example:

Order Processing Lambda  
↓  
Failure  
↓  
SNS  
↓  
Operations Team

Use when:

**Humans or multiple subscribers need notification**

---

# Destination + SQS Recovery

Example:

Lambda  
↓  
Failure  
↓  
SQS Recovery Queue  
↓  
Later Reprocessing

Use when you need:

**Durable downstream retry or manual recovery**

---

# Destination + EventBridge

EventBridge is powerful when successful or failed Lambda outcomes should be:

**Routed based on rules**

Architecture:

Lambda  
↓  
EventBridge  
↓  
├── Analytics
├── Notifications
└── Workflow

---

# Lambda Destinations and Idempotency

Even with destinations:

Distributed systems can still:

**Retry or duplicate processing**

Downstream consumers should often remain:

**Idempotent**

Example:

Same success event arrives twice  
↓  
Consumer recognizes same transaction ID  
↓  
Avoid duplicate business operation

---

# Permissions

Lambda needs permission to send records to:

**The configured destination**

Depending on the destination, permissions may involve:

- Lambda execution role
- Resource-based policies
- Target permissions

The exam principle:

> **Destination configuration still requires proper IAM authorization**

---

# Architecture Thinking

## Scenario 1 — Success and Failure Paths

An async Lambda function needs:

Success  
→ EventBridge

Failure  
→ SQS

Choose:

**Lambda Destinations**

---

## Scenario 2 — Only Failed Events Matter

A Lambda function should preserve:

**Only failed asynchronous events**

Choose:

**DLQ**

---

## Scenario 3 — Notify Operations on Failure

Async Lambda fails permanently.

Need:

**Email notification**

Architecture:

Failure Destination  
↓  
SNS  
↓  
Email

Choose:

**Lambda Destination to SNS**

---

## Scenario 4 — Durable Recovery

Failed async invocation must be:

**Stored for later reprocessing**

Choose:

Failure Destination  
↓  
SQS

---

## Scenario 5 — Continue Event Workflow

Successful function output should be:

**Routed to multiple downstream systems**

Choose:

Success Destination  
↓  
EventBridge

or:

SNS

depending on routing requirements.

---

## Scenario 6 — Complex Workflow

Lambda A should call B, then C, retry conditionally, branch, and wait.

Do NOT build this primarily with:

**Destinations**

Think:

[[Step Functions]]

---

## Scenario 7 — SQS Trigger Failure

Lambda is triggered by SQS through:

**Event Source Mapping**

Do NOT automatically assume:

Lambda async Destinations

Use:

**SQS failure-handling semantics**

such as:

- Visibility Timeout
- Redrive Policy
- DLQ
- Partial Batch Response

---

# Scenario Recognition

Immediately think:

**Lambda Destinations**

when you see:

- Async Lambda outcome
- Success destination
- Failure destination
- Route invocation result
- Send result to SQS
- Send result to SNS
- Send result to EventBridge
- Continue async processing after function completion

---

# Exam Traps

## Trap 1 — Lambda Destinations Are for Every Invocation Type

❌

Their main association is:

**Asynchronous Lambda invocations**

---

## Trap 2 — Destinations and DLQs Are Identical

❌

DLQ:

**Failures**

Destinations:

**Success + Failure**

---

## Trap 3 — Destination Is the Service That Triggered Lambda

❌

Source:

**Before Lambda**

Destination:

**After Lambda**

---

## Trap 4 — Event Source Mapping Is a Destination Feature

❌

Event Source Mapping:

**Gets records INTO Lambda**

Destination:

**Sends outcomes OUT**

---

## Trap 5 — A Success Destination Only Gets the Original Event

Not necessarily.

Destinations can include:

**Invocation metadata and response information**

---

## Trap 6 — Destinations Replace Step Functions

❌

For complex orchestration:

**Step Functions**

is usually the stronger design.

---

## Trap 7 — SQS-Triggered Lambda Uses the Same Failure Model as Direct Async Lambda

❌

SQS uses:

**Event Source Mapping**

and queue-specific failure handling.

---

# Quick Cheat Sheet

| Exam Clue | Answer |
|---|---|
| Route Async Success Result | Lambda Destination |
| Route Async Failure Result | Lambda Destination |
| Preserve Only Failed Async Event | DLQ |
| Success → EventBridge | Destination |
| Failure → SQS | Destination |
| Failure → SNS | Destination |
| Continue Complex Workflow | Step Functions |
| SQS Trigger Failure | SQS DLQ / Redrive |
| Incoming SQS/Kinesis Records | Event Source Mapping |

---

# DLQ vs Destination

| Requirement | Best Choice |
|---|---|
| Store Failed Async Event | DLQ |
| Route Failed Outcome | Destination |
| Route Successful Outcome | Destination |
| Separate Success and Failure Paths | Destinations |
| Capture SQS Poison Message | SQS DLQ |

---

# IN vs OUT Memory Map

> **INTO LAMBDA**
>
> S3 / SNS / EventBridge
> → Async Invocation
>
> SQS / Kinesis / DynamoDB Streams
> → Event Source Mapping
>
> **OUT OF LAMBDA**
>
> Success / Failure Result
> → Lambda Destinations

---

# Final Exam Rapid-Fire

> **ASYNC SUCCESS → TARGET**
> → DESTINATION
>
> **ASYNC FAILURE → TARGET**
> → DESTINATION
>
> **FAILED EVENT ONLY**
> → DLQ
>
> **SUCCESS + FAILURE ROUTING**
> → DESTINATIONS
>
> **RESULT → SQS**
> → DESTINATION
>
> **RESULT → SNS**
> → DESTINATION
>
> **RESULT → EVENTBRIDGE**
> → DESTINATION
>
> **COMPLEX ORCHESTRATION**
> → STEP FUNCTIONS
>
> **SQS SOURCE FAILURE**
> → SQS DLQ / REDRIVE
>
> **GET RECORDS INTO LAMBDA**
> → EVENT SOURCE MAPPING

---

## Master Memory Trick

> [!tip] Lambda Destinations Master Memory Trick
> Imagine Lambda is a package-processing station.
>
> A package arrives:
>
> **SOURCE**
>
> Lambda processes it:
>
> **FUNCTION**
>
> Then the station asks:
>
> **"Where should the result go?"**
>
> If successful:
>
> → Success Destination
>
> If failed:
>
> → Failure Destination

So remember:

> **BEFORE LAMBDA**
> → SOURCE
>
> **AFTER LAMBDA**
> → DESTINATION
>
> **FAILURE ONLY**
> → DLQ
>
> **SUCCESS + FAILURE**
> → DESTINATIONS
>
> **COMPLEX MULTI-STEP LOGIC**
> → STEP FUNCTIONS

And the killer SAA clue:

> **"Route asynchronous Lambda invocation results differently depending on whether the function succeeds or fails."**
>
> → **Lambda Destinations**

---

## Related Notes

- [[Lambda]]
- [[Lambda Asynchronous Invocations]]
- [[Lambda Event Source Mapping]]
- [[SQS]]
- [[SNS]]
- [[20-SAA/10-Messaging/EventBridge]]
- [[Step Functions]]
- [[S3]]
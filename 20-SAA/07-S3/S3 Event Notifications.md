## What Problem Does It Solve?

[[S3 Event Notifications]] let S3 automatically react when something happens to an object.

They solve the problem of:

> **"How can I trigger another AWS service when an S3 event occurs?"**

Examples:

Object Uploaded  
↓  
Trigger [[02-Compute/Lambda]]

Object Deleted  
↓  
Send Message to [[SQS]]

Object Restored  
↓  
Publish to [[SNS]]

Think:

S3 Event  
↓  
Notification  
↓  
Downstream Action

> [!tip] Memory Trick
> **S3 Event Notifications = Something happened in S3 → React**

---

## Common S3 Events

The Maarek slides highlight events such as:

- `s3:ObjectCreated`
- `s3:ObjectRemoved`
- `s3:ObjectRestore`
- S3 Replication events

These events can trigger downstream processing.

### Example

New Image Uploaded  
↓  
`s3:ObjectCreated`  
↓  
[[02-Compute/Lambda]]  
↓  
Generate Thumbnail

This is one of the most classic S3 event-driven architectures.

---

# Event Destinations

Traditional S3 Event Notifications can send events to:

- [[02-Compute/Lambda]]
- [[SQS]]
- [[SNS]]

Architecture:

[[S3]]  
↓ Event  
├── [[02-Compute/Lambda]]
├── [[SQS]]
└── [[SNS]]

Each destination fits a different architecture pattern.

---

# S3 → Lambda

Use:

[[02-Compute/Lambda]]

when an event should trigger:

**Immediate serverless processing**

Example:

Image Uploaded  
↓  
S3 Event Notification  
↓  
Lambda  
↓  
Generate Thumbnail

Other examples:

- Validate file
- Extract metadata
- Process document
- Transform image
- Start application logic

> [!tip] Memory Trick
> **S3 event needs CODE → Lambda**

---

# S3 → SQS

Use:

[[SQS]]

when you want to:

**Queue events for asynchronous processing**

Architecture:

S3  
↓  
Event  
↓  
SQS Queue  
↓  
Worker Application

This helps decouple:

S3

from:

Downstream processing

### Architecture Thinking

If the consumer may be slow or temporarily unavailable:

**Queue the work**

instead of requiring immediate processing.

> [!tip] Memory Trick
> **S3 event needs BUFFER → SQS**

---

# S3 → SNS

Use:

[[SNS]]

when you want:

**Publish/subscribe notifications**

Architecture:

S3  
↓  
SNS Topic  
↓  
Multiple Subscribers

Potential subscribers:

- SQS
- Lambda
- Email
- Other supported endpoints

### Architecture Thinking

If one S3 event must notify:

**Multiple consumers**

think:

[[SNS]]

> [!tip] Memory Trick
> **S3 event needs FAN-OUT → SNS**

---

# Object Name Filtering

S3 Event Notifications support:

**Object name filtering**

Example:

Only trigger Lambda for:

`*.jpg`

Architecture:

Upload:

photo.jpg  
↓  
Matches Filter  
↓  
Lambda Triggered

Upload:

report.pdf  
↓  
Does Not Match  
↓  
No Trigger

This can help avoid unnecessary downstream processing.

---

## Prefix and Suffix Thinking

A common architecture pattern is filtering based on object names.

Examples:

Prefix:

`images/`

Suffix:

`.jpg`

Conceptually:

S3 Object Created  
↓  
Does Key Match Required Pattern?  
├── Yes → Send Event
└── No → Ignore

### Scenario Recognition

If the exam says:

> **"Only process uploaded JPG images"**

Think:

**S3 Event Notification filtering**

---

# Multiple S3 Event Notifications

You can configure:

**Multiple event notifications**

on a bucket.

Example:

Image Upload  
↓  
Lambda

Log Upload  
↓  
SQS

Object Removal  
↓  
SNS

One S3 bucket can therefore participate in several event-driven workflows.

---

# Delivery Timing

S3 Event Notifications are generally delivered:

**Within seconds**

but delivery can sometimes take:

**A minute or longer**

This means the architecture is:

**Event-driven and asynchronous**

not:

**Synchronous request processing**

### Exam Thinking

Do not assume:

Object Upload  
↓  
Notification  
↓  
Downstream action

happens at exactly the same instant.

---

# Permissions Are Required

S3 must be allowed to invoke or publish to the destination service.

The permission model depends on the destination.

---

## S3 → Lambda Permissions

For S3 to invoke:

[[02-Compute/Lambda]]

the Lambda function needs a:

**Lambda Resource-Based Policy**

that permits S3 to invoke it.

Architecture:

S3  
↓  
Lambda Resource Policy  
↓  
Lambda Function

> [!tip] Memory Trick
> **S3 invokes Lambda → Lambda Resource Policy**

---

## S3 → SNS Permissions

For S3 to publish to:

[[SNS]]

the SNS topic needs a:

**Resource Policy**

that permits S3 to publish.

Architecture:

S3  
↓  
SNS Topic Policy  
↓  
SNS Topic

---

## S3 → SQS Permissions

For S3 to send messages to:

[[SQS]]

the SQS queue needs a:

**Resource Policy**

allowing S3.

Architecture:

S3  
↓  
SQS Queue Policy  
↓  
SQS Queue

---

# Permission Comparison

| Destination | Permission Needed |
|---|---|
| [[02-Compute/Lambda]] | Lambda Resource Policy |
| [[SNS]] | SNS Topic Resource Policy |
| [[SQS]] | SQS Queue Resource Policy |

### Memory Trick

> **S3 must be trusted by the destination**

---

# S3 Event Notifications with EventBridge

S3 can also send events to:

[[20-SAA/10-Messaging/EventBridge]]

This is a much more flexible event-routing architecture.

Architecture:

[[S3]]  
↓  
All Events  
↓  
[[20-SAA/10-Messaging/EventBridge]]  
↓  
Rules  
↓  
Many Possible Targets

---

# Why Use EventBridge?

The Maarek slides highlight several advantages.

## Advanced Filtering

EventBridge can filter using:

**JSON event rules**

Examples include:

- Object name
- Object size
- Metadata
- Other event attributes

This is more flexible than basic S3 object-name filtering.

---

## Multiple Destinations

EventBridge can route S3 events to many different services.

Examples from the Maarek slides include:

- [[Step Functions]]
- [[20-SAA/10-Messaging/Kinesis Data Streams]]
- [[20-SAA/10-Messaging/Kinesis Data Firehose]]

and many other AWS services.

### Architecture Thinking

If the event routing requirements are:

**Complex**

think:

[[20-SAA/10-Messaging/EventBridge]]

---

## Archive Events

EventBridge can:

**Archive events**

This lets you retain events for later use.

---

## Replay Events

Archived events can be:

**Replayed**

This is useful when:

- Fixing downstream processing
- Retesting workflows
- Recovering from application failures

---

## Reliable Delivery

The Maarek slides also emphasize:

**Reliable delivery**

as an EventBridge capability.

---

# Traditional Notifications vs EventBridge

## Traditional S3 Event Notifications

Destinations:

- Lambda
- SQS
- SNS

Filtering:

Relatively simple

Use when:

The event path is straightforward.

---

## S3 + EventBridge

Provides:

- Advanced filtering
- Many more destinations
- Event archive
- Event replay
- More complex event routing

### Memory Trick

**Simple reaction → S3 Event Notification**

**Advanced event routing → EventBridge**

---

# Architecture Thinking

## Scenario 1 — Generate Thumbnail

Users upload JPG files to S3.

Every new JPG must trigger code that generates a thumbnail.

**Choose:**

S3 Event Notification  
↓  
[[02-Compute/Lambda]]

Use object-name filtering for:

`.jpg`

---

## Scenario 2 — Queue File Processing

A large number of files arrive in S3.

A backend fleet should process them gradually without becoming overwhelmed.

**Choose:**

S3 Event Notification  
↓  
[[SQS]]  
↓  
Workers

Why?

SQS provides:

**Decoupling + buffering**

---

## Scenario 3 — Notify Multiple Systems

Every object upload must notify several downstream consumers.

**Choose:**

S3  
↓  
[[SNS]]  
↓  
Multiple Subscribers

---

## Scenario 4 — Complex Filtering

A company wants to trigger different workflows based on:

- Object size
- Object metadata
- Object name

**Choose → S3 + [[20-SAA/10-Messaging/EventBridge]]**

Why?

EventBridge supports:

**Advanced JSON filtering**

---

## Scenario 5 — Need Event Replay

A downstream workflow occasionally fails.

The company wants to archive S3 events and replay them later.

**Choose → EventBridge**

Traditional S3 Event Notifications do not provide EventBridge-style event archive/replay.

---

## Scenario 6 — XML Upload Starts ETL

An S3 bucket receives new files.

Each PUT must automatically start an ETL workflow.

Possible architecture:

S3 PUT  
↓  
Event Notification  
↓  
[[02-Compute/Lambda]]  
↓  
Start ETL Job

or:

S3  
↓  
[[20-SAA/10-Messaging/EventBridge]]  
↓  
ETL Workflow

depending on the event-routing complexity.

---

# S3 Event Notification vs S3 Object Lambda

These are easy to confuse.

## [[S3 Event Notifications]]

Runs because:

**Something happened to an object**

Examples:

- Created
- Removed
- Restored

---

## [[S3 Object Lambda]]

Runs because:

**Someone retrieves an object**

Purpose:

Transform the response.

### Memory Trick

**Event Notification = EVENT happened**

**Object Lambda = GET happened**

---

# S3 Event Notifications vs Lifecycle Rules

## [[S3 Lifecycle Rules]]

React to:

**Object age**

Example:

After 90 days → Glacier

---

## S3 Event Notifications

React to:

**Object events**

Example:

Object Created → Lambda

### Exam Decision

**After X days → Lifecycle**

**When object uploaded → Event Notification**

---

# S3 Event Notifications vs EventBridge

| Requirement | Best Fit |
|---|---|
| Trigger Lambda on upload | S3 Event Notification |
| Send message to SQS | S3 Event Notification |
| Publish to SNS | S3 Event Notification |
| Advanced JSON filtering | EventBridge |
| Many destination types | EventBridge |
| Archive event | EventBridge |
| Replay event | EventBridge |
| Complex event routing | EventBridge |

---

# Scenario Recognition

## Immediately Think S3 Event Notifications When You See

- Object uploaded
- Object created
- Object deleted
- Object restored
- Trigger Lambda
- Send SQS message
- Publish SNS notification
- Generate thumbnail
- Process object after upload
- Event-driven S3 workflow

## Immediately Think EventBridge When You See

- Advanced filtering
- Event archive
- Replay
- Step Functions target
- Kinesis target
- Many destination types
- Complex event routing

### Strongest Exam Pattern

> **"When a file is uploaded to S3..."**
>
> → **S3 Event Notification**

---

# Exam Traps

## Trap 1 — Event Notifications Are Synchronous

False.

They are:

**Asynchronous**

Events usually arrive within seconds but may take longer.

---

## Trap 2 — S3 Event Notification Can Only Trigger Lambda

False.

Traditional destinations include:

- Lambda
- SQS
- SNS

---

## Trap 3 — No Filtering Is Possible

False.

Object-name filtering is supported.

Example:

`.jpg`

---

## Trap 4 — Lambda Needs an IAM Role Allowing S3 to Invoke It

The key permission for invocation is:

**Lambda Resource-Based Policy**

allowing S3 to invoke the function.

The Lambda execution role controls what the function itself can do after invocation.

---

## Trap 5 — S3 Can Publish to SNS Without Topic Permission

False.

The destination resource must allow S3.

Same principle for:

- SNS
- SQS
- Lambda

---

## Trap 6 — EventBridge and S3 Event Notifications Are Identical

False.

EventBridge provides:

- Advanced filtering
- More destinations
- Archive
- Replay
- More flexible routing

---

## Trap 7 — Object Lambda Is Used for Object Upload Events

False.

Object Lambda transforms:

**Objects during retrieval**

Use Event Notifications for:

**Object event automation**

---

# Quick Cheat Sheet

| Feature | S3 Event Notifications |
|---|---|
| ObjectCreated | ✅ |
| ObjectRemoved | ✅ |
| ObjectRestore | ✅ |
| Replication Events | ✅ |
| Object Name Filtering | ✅ |
| Lambda Target | ✅ |
| SQS Target | ✅ |
| SNS Target | ✅ |
| Asynchronous | ✅ |
| Typical Delivery | Seconds |
| Can Sometimes Take Longer | ✅ |
| Lambda Resource Policy Needed | ✅ |
| SNS Resource Policy Needed | ✅ |
| SQS Resource Policy Needed | ✅ |
| Advanced JSON Filtering | Use EventBridge |
| Archive / Replay | Use EventBridge |

---

## Master Memory Trick

> [!tip] Master Memory Trick
> **S3 Event Notifications = IF THIS happens, DO THAT**
>
> **Upload**
>
> → Lambda
>
> **Need buffering**
>
> → SQS
>
> **Need fan-out**
>
> → SNS
>
> **Need advanced routing**
>
> → EventBridge

And remember the killer distinction:

> **Object CREATED → Event Notification**
>
> **Object REQUESTED → Object Lambda**
>
> **Object AGES → Lifecycle Rule**

---

## Related Notes

- [[S3]]
- [[S3 Object Lambda]]
- [[S3 Lifecycle Rules]]
- [[02-Compute/Lambda]]
- [[SQS]]
- [[SNS]]
- [[20-SAA/10-Messaging/EventBridge]]
- [[Step Functions]]
- [[20-SAA/10-Messaging/Kinesis Data Streams]]
- [[20-SAA/10-Messaging/Kinesis Data Firehose]]
- [[IAM]]
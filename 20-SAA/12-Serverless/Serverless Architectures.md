## What Problem Does It Solve?

Serverless architectures combine managed AWS services to build applications with:

**Little or no server management**

Common building blocks include:

- [[API Gateway]]
- [[Lambda]]
- [[DynamoDB]]
- [[S3]]
- [[SQS]]
- [[SNS]]
- [[20-SAA/10-Messaging/EventBridge]]
- [[Step Functions]]
- [[Cognito]]
- [[CloudFront]]

The core idea is:

> **Use managed services for compute, storage, messaging, APIs, and workflows so the application can scale without managing fleets of servers.**

> [!tip] Master Memory Trick
> **API = API Gateway**
>
> **CODE = Lambda**
>
> **DATA = DynamoDB / S3**
>
> **QUEUE = SQS**
>
> **EVENTS = EventBridge**
>
> **WORKFLOW = Step Functions**
>
> **USERS = Cognito**

---

## Core Serverless Pattern

A classic architecture:

User  
↓  
[[CloudFront]]  
↓  
[[API Gateway]]  
↓  
[[Lambda]]  
↓  
[[DynamoDB]]

This architecture provides:

- Global delivery
- Managed API layer
- Serverless compute
- Serverless NoSQL database
- Automatic scaling

---

## What "Serverless" Really Means

Serverless does NOT mean:

**No servers exist**

It means:

**You do not provision or manage the underlying servers**

AWS manages:

- Infrastructure
- Scaling
- Availability
- Patching
- Capacity

You manage:

- Application code
- Permissions
- Configuration
- Architecture

---

# Architecture 1 — Serverless Web API

Classic pattern:

Client  
↓  
[[API Gateway]]  
↓  
[[Lambda]]  
↓  
[[DynamoDB]]

Use for:

- REST APIs
- Mobile backends
- Web application APIs
- CRUD applications

### Killer Exam Clue

> **Build a scalable API with no server management**
>
> → **API Gateway + Lambda + DynamoDB**

---

# Architecture 2 — Static Website + Serverless Backend

Architecture:

User  
↓  
[[CloudFront]]  
↓  
[[S3]] Static Website Assets

Dynamic Requests  
↓  
API Gateway  
↓  
Lambda  
↓  
DynamoDB

This separates:

**Static content**

from:

**Dynamic application logic**

### Memory Trick

**STATIC = S3 + CloudFront**

**DYNAMIC = API Gateway + Lambda**

---

# Why Put CloudFront in Front?

[[CloudFront]] can provide:

- Global caching
- Lower latency
- HTTPS
- Edge delivery
- Reduced origin load

### Killer Exam Clue

> **Globally distribute static application assets with low latency**
>
> → **CloudFront + S3**

---

# Architecture 3 — User Authentication

Add:

[[Cognito]]

Architecture:

User  
↓  
Cognito  
↓  
Token  
↓  
API Gateway  
↓  
Lambda  
↓  
DynamoDB

Use when the application needs:

- Sign-up
- Sign-in
- JWT authentication
- MFA
- Social login

### Killer Exam Clue

> **Serverless application needs managed end-user authentication**
>
> → **Cognito**

---

# Architecture 4 — Direct S3 Uploads

Sometimes users should upload files directly to:

[[S3]]

instead of sending them through:

Lambda.

Architecture:

User  
↓  
Cognito  
↓  
Identity Pool  
↓  
Temporary AWS Credentials  
↓  
S3

This avoids:

**Proxying large files through API Gateway/Lambda**

### SAA Principle

> **Do not send large object uploads through compute when users can securely upload directly to S3.**

---

# Presigned URL Pattern

Another common pattern:

Client  
↓  
API Gateway  
↓  
Lambda  
↓  
Generate S3 Presigned URL  
↓  
Client Uploads Directly to S3

This gives the client:

**Temporary permission for a specific S3 operation**

### Killer Exam Clue

> **Allow client to upload directly to S3 without exposing AWS credentials**
>
> → **S3 Presigned URL**

---

# Architecture 5 — S3 Event Processing

Architecture:

User Upload  
↓  
[[S3]]  
↓  
[[Lambda]]  
↓  
Process File  
↓  
S3 / DynamoDB

Use cases:

- Thumbnail creation
- File validation
- Metadata extraction
- Document processing

### Killer Exam Clue

> **Automatically process an object after upload**
>
> → **S3 + Lambda**

---

# Architecture 6 — Asynchronous Processing

When work does not need an immediate response:

Producer  
↓  
[[SQS]]  
↓  
Lambda  
↓  
Backend

SQS provides:

- Buffering
- Decoupling
- Backpressure
- Retry durability

Lambda provides:

**Serverless processing**

### Memory Trick

**SQS = WAIT**

**Lambda = WORK**

---

# Why Add SQS?

Without SQS:

Traffic Spike  
↓  
Lambda / Backend

Potential issue:

**Downstream overload**

With SQS:

Traffic Spike  
↓  
SQS  
↓  
Controlled Processing  
↓  
Lambda

This makes the architecture:

**More resilient to bursts**

---

# Architecture 7 — Fan-Out

One event needs to reach:

**Multiple independent consumers**

Architecture:

Publisher  
↓  
[[SNS]]  
↓  
├── SQS Queue A
├── SQS Queue B
└── Lambda C

Use this for:

**Fan-out**

### Killer Exam Clue

> **One event must be delivered to multiple independent systems**
>
> → **SNS**

---

# SNS + SQS Fan-Out

A more durable pattern:

Publisher  
↓  
SNS  
↓  
├── SQS Queue A
├── SQS Queue B
└── SQS Queue C

Each consumer receives:

**Its own durable copy**

### Memory Trick

**SNS = COPY**

**SQS = HOLD**

---

# Architecture 8 — Event Routing

When different events should go to:

**Different targets**

use:

[[20-SAA/10-Messaging/EventBridge]]

Architecture:

Event Sources  
↓  
EventBridge  
↓  
Rules  
↓  
Targets

Targets can include:

- Lambda
- Step Functions
- SNS
- SQS
- ECS

### Killer Exam Clue

> **Route events to different targets based on event content**
>
> → **EventBridge**

---

# SNS vs EventBridge

### SNS

Think:

**Broadcast**

### EventBridge

Think:

**Rule-based routing**

### Memory Trick

**SNS = WHO GETS A COPY**

**EVENTBRIDGE = WHERE DOES THIS EVENT GO**

---

# Architecture 9 — Workflow Orchestration

For multi-step workflows:

Event  
↓  
[[Step Functions]]  
↓  
Lambda A  
↓  
Choice  
↓  
Lambda B / Lambda C  
↓  
Finish

Use Step Functions when you need:

- Branching
- Retry
- Catch
- Wait
- Parallel execution
- Workflow state

### Killer Exam Clue

> **Coordinate multiple serverless steps with retries and branching**
>
> → **Step Functions**

---

# Step Functions vs SQS

### SQS

Question:

> **Where should work wait?**

### Step Functions

Question:

> **What step happens next?**

---

# Architecture 10 — Long-Running Step

Lambda has a maximum runtime of:

**15 minutes**

If one workflow step takes longer:

Step Functions  
↓  
[[ECS]] / [[Fargate]]  
↓  
Long-Running Task  
↓  
Step Functions Continues

### Killer Exam Pattern

> **Serverless workflow has one container job that takes 45 minutes**
>
> → **Step Functions + Fargate**

---

# Architecture 11 — DynamoDB Change Processing

Architecture:

DynamoDB  
↓  
DynamoDB Streams  
↓  
Lambda Event Source Mapping  
↓  
Lambda

Use when:

**Application logic should react to table changes**

Examples:

- Notifications
- Derived data
- Search updates
- Audit processing

---

# Architecture 12 — Global Serverless Application

Architecture:

Global Users  
↓  
CloudFront  
↓  
API Gateway  
↓  
Lambda  
↓  
DynamoDB Global Tables

This can provide:

- Global edge delivery
- Regional API execution
- Multi-Region data

### Killer Exam Clue

> **Serverless global application needs active-active NoSQL data**
>
> → **DynamoDB Global Tables**

---

# Multi-Region API Thinking

A highly available global architecture may deploy:

**Regional APIs and Lambda functions**

in multiple Regions.

Then use services such as:

- Route 53
- CloudFront
- Global data stores

to route:

**Users appropriately**

---

# Architecture 13 — Serverless Image Processing

Architecture:

User  
↓  
S3 Upload  
↓  
Lambda  
↓  
Resize Image  
↓  
S3  
↓  
CloudFront

This provides:

**Automatic media processing and global delivery**

---

# Architecture 14 — Serverless Notification System

Architecture:

Application Event  
↓  
SNS  
↓  
Subscribers

Possible subscribers:

- Email
- SQS
- Lambda

Use for:

**One-to-many notifications**

---

# Architecture 15 — Scheduled Automation

Architecture:

Schedule  
↓  
[[20-SAA/10-Messaging/EventBridge]]  
↓  
Lambda

Use for:

- Nightly cleanup
- Reports
- Scheduled automation
- Periodic maintenance

### Killer Exam Clue

> **Run serverless code every night**
>
> → **EventBridge + Lambda**

---

# Architecture 16 — Scheduled Workflow

If scheduled work has:

**Multiple steps**

Architecture:

EventBridge  
↓  
Step Functions  
↓  
Workflow

Instead of:

EventBridge  
↓  
Lambda A  
↓  
Lambda B  
↓  
Lambda C

### Exam Principle

> **Use EventBridge to trigger; use Step Functions to orchestrate**

---

# Architecture 17 — Protecting RDS

Serverless does not mean every backend must be:

**DynamoDB**

Lambda can connect to:

[[RDS]]

Architecture:

API Gateway  
↓  
Lambda  
↓  
[[RDS Proxy]]  
↓  
RDS

RDS Proxy helps manage:

**Database connections**

### Killer Exam Clue

> **Lambda concurrency causes too many RDS connections**
>
> → **RDS Proxy**

---

# Architecture 18 — Protecting Downstream Systems

Lambda can scale rapidly.

Possible architecture:

SQS  
↓  
Lambda  
↓  
Slow Backend

Then use:

**Reserved Concurrency**

to limit:

**Lambda parallelism**

### Memory Trick

**SQS = Hold Excess Work**

**Reserved Concurrency = Control Workers**

---

# Architecture 19 — Low-Latency Lambda

For customer-facing applications:

API Gateway  
↓  
Lambda

If cold starts cause unacceptable latency:

Think:

- Provisioned Concurrency
- SnapStart when appropriate for supported runtimes

### Killer Distinction

**Pre-warmed environments**
→ Provisioned Concurrency

**Snapshot restore**
→ SnapStart

---

# Architecture 20 — API Security

Architecture:

User  
↓  
Cognito  
↓  
API Gateway  
↓  
Lambda

Additional protection:

Internet  
↓  
[[06-Security/WAF]]  
↓  
API Gateway

Possible security layers:

- Cognito
- IAM
- Lambda Authorizer
- API Gateway Resource Policy
- WAF

---

# Architecture 21 — Private API

For internal applications:

Private Client  
↓  
VPC Endpoint  
↓  
Private API Gateway  
↓  
Backend

Use when:

**The API should not be publicly accessible**

---

# Architecture 22 — API Gateway to Private Backend

Public or managed API Gateway  
↓  
VPC Link  
↓  
Private Backend

Use when:

**API Gateway must access private VPC services**

### Memory Trick

**Private API**
→ Client reaches API privately

**VPC Link**
→ API reaches backend privately

---

# Architecture 23 — Caching

Different layers can cache different things.

### CloudFront

Caches:

**Content near users**

### API Gateway Cache

Caches:

**API responses**

### DAX

Caches:

**DynamoDB reads**

### ElastiCache

Caches:

**General application data**

### Memory Trick

**CLOUDFRONT = EDGE**

**API CACHE = RESPONSE**

**DAX = DYNAMODB**

**ELASTICACHE = GENERAL**

---

# Serverless Storage Choices

## S3

Think:

- Objects
- Files
- Images
- Static content

## DynamoDB

Think:

- Key-value/document data
- Millisecond latency
- Massive NoSQL scale

## EFS

Think:

- Shared file system
- Lambda filesystem needs

### Killer Storage Question

> **What kind of data is this?**
>
> Object?
> → S3
>
> NoSQL record?
> → DynamoDB
>
> Shared filesystem?
> → EFS

---

# Serverless Messaging Choices

## SQS

Think:

**Queue / Buffer**

## SNS

Think:

**Fan-Out**

## EventBridge

Think:

**Routing**

## Step Functions

Think:

**Workflow**

### Master Messaging Trick

> **WAIT**
> → SQS
>
> **BROADCAST**
> → SNS
>
> **ROUTE**
> → EventBridge
>
> **ORCHESTRATE**
> → Step Functions

---

# Synchronous vs Asynchronous

## Synchronous

Caller waits.

Example:

Client  
↓  
API Gateway  
↓  
Lambda  
↓  
Response

Use when:

**Immediate result is required**

---

## Asynchronous

Caller does not wait.

Example:

S3  
↓  
Lambda

Use when:

**Background processing is acceptable**

---

# Serverless Failure Handling

A resilient architecture needs:

**Failure paths**

Potential mechanisms include:

- SQS DLQ
- Lambda Destinations
- Lambda async DLQ
- Step Functions Retry/Catch
- EventBridge DLQ
- Idempotency

### SAA Principle

> **Design failure handling into the architecture instead of treating it as an afterthought**

---

# Idempotency

Serverless event-driven systems may process:

**Duplicate events**

Functions should often be:

**Idempotent**

Example:

Same Payment Event  
↓  
Lambda Invoked Twice  
↓  
Only One Charge Created

### Killer Exam Concept

> **Retries should not create duplicate business effects**

---

# Stateless Design

Serverless compute such as Lambda should generally be:

**Stateless**

Persistent state should live in:

- DynamoDB
- S3
- RDS
- EFS
- ElastiCache

depending on requirements.

### Memory Trick

**COMPUTE = TEMPORARY**

**STATE = EXTERNAL**

---

# Decoupling

One of the strongest serverless architecture principles is:

**Decouple components**

Bad:

Producer  
↓  
Consumer  
↓  
Consumer 2  
↓  
Consumer 3

Better:

Producer  
↓  
SQS / SNS / EventBridge  
↓  
Independent Consumers

Benefits:

- Resilience
- Scalability
- Independent failure domains
- Easier evolution

---

# Loose Coupling

A loosely coupled serverless architecture allows:

**One component to fail without immediately breaking everything else**

Example:

Producer  
↓  
SQS  
↓  
Consumer

Consumer offline?

Messages remain:

**In the queue**

---

# Backpressure

If producers are faster than consumers:

Use:

[[SQS]]

Architecture:

Fast Producer  
↓  
SQS  
↓  
Slower Consumer

This prevents:

**Immediate overload**

---

# Event-Driven Design

Serverless applications often use:

**Events**

instead of tightly coupled service calls.

Example:

Order Created  
↓  
EventBridge  
↓  
├── Billing
├── Shipping
└── Analytics

Each service reacts:

**Independently**

---

# Architecture Thinking

## Scenario 1 — Serverless E-Commerce API

Need:

- User login
- REST API
- Business logic
- NoSQL database

Choose:

Cognito  
↓  
API Gateway  
↓  
Lambda  
↓  
DynamoDB

---

## Scenario 2 — Static SPA

Need:

- HTML
- JavaScript
- CSS
- Global delivery

Choose:

S3  
↓  
CloudFront

---

## Scenario 3 — SPA + API

Architecture:

CloudFront  
↓  
├── S3 Static Frontend
└── API Gateway  
    ↓  
    Lambda  
    ↓  
    DynamoDB

---

## Scenario 4 — File Upload

Users upload:

**Large videos**

Do NOT send through:

API Gateway → Lambda

Prefer:

**Direct S3 upload**

using:

- Presigned URLs
- Cognito temporary credentials

---

## Scenario 5 — Background Order Processing

API should immediately return:

**Order accepted**

while backend processing occurs later.

Choose:

API Gateway  
↓  
Lambda  
↓  
SQS  
↓  
Worker

---

## Scenario 6 — One Event, Many Systems

Order must notify:

- Shipping
- Fraud
- Analytics

Choose:

**SNS fan-out**

or:

**EventBridge**

depending on whether the requirement emphasizes:

Broadcast vs rule-based routing.

---

## Scenario 7 — Complex Order Workflow

Need:

- Charge payment
- Retry
- Wait
- Branch
- Compensating action

Choose:

**Step Functions**

---

## Scenario 8 — Global Active-Active App

Need:

- Users worldwide
- Local DynamoDB reads/writes

Choose:

**DynamoDB Global Tables**

---

## Scenario 9 — Database Connection Storm

Lambda overwhelms RDS.

Choose:

**RDS Proxy**

---

## Scenario 10 — Spiky Workload

10,000 jobs arrive suddenly.

Backend can process only:

100 at a time.

Choose:

SQS  
↓  
Lambda with controlled concurrency

---

## Scenario 11 — API Cold Starts

Interactive API requires:

**Predictable low latency**

Choose:

**Provisioned Concurrency**

---

## Scenario 12 — Scheduled Business Workflow

Every night:

- Generate report
- Store report
- Notify management

Choose:

EventBridge  
↓  
Step Functions  
↓  
Workflow

---

# Scenario Recognition

Immediately think:

**Serverless Architecture**

when you see:

- Minimal operational overhead
- No server management
- Event-driven
- Automatic scaling
- API Gateway
- Lambda
- DynamoDB
- S3
- Managed messaging
- Managed workflows

---

# Exam Traps

## Trap 1 — Serverless Means Everything Must Use Lambda

❌

Serverless architectures can use:

- DynamoDB
- S3
- API Gateway
- EventBridge
- Step Functions
- SQS
- SNS
- Fargate

---

## Trap 2 — Large File Uploads Should Always Pass Through Lambda

❌

Prefer:

**Direct S3 uploads**

when appropriate.

---

## Trap 3 — Step Functions Is a Queue

❌

Step Functions:

**Orchestrates**

SQS:

**Queues**

---

## Trap 4 — EventBridge and SNS Are Identical

❌

SNS:

**Fan-out**

EventBridge:

**Rule-based routing**

---

## Trap 5 — Lambda Scaling Automatically Protects RDS

❌

Think:

- RDS Proxy
- Reserved Concurrency
- SQS buffering

---

## Trap 6 — Serverless Means Stateful Lambda Functions

❌

Keep persistent state:

**External**

---

## Trap 7 — API Gateway Is Required for Every Lambda

❌

Lambda can be invoked by:

- S3
- SNS
- EventBridge
- SQS
- Streams
- Function URLs
- ALB
- Other AWS services

---

## Trap 8 — Cognito User Pool Gives Users AWS Credentials

❌

Identity Pool provides:

**Temporary AWS credentials**

---

## Trap 9 — Asynchronous Architecture Removes Lambda's 15-Minute Limit

❌

Lambda runtime limit still applies.

---

## Trap 10 — More Services Always Means Better Architecture

❌

Choose:

**The simplest architecture that satisfies requirements**

---

# Quick Cheat Sheet

| Requirement | Architecture |
|---|---|
| Serverless API | API Gateway + Lambda |
| Serverless NoSQL | DynamoDB |
| Static Website | S3 + CloudFront |
| User Authentication | Cognito |
| Direct File Upload | S3 Presigned URL / Cognito |
| Async Buffer | SQS |
| Fan-Out | SNS |
| Event Routing | EventBridge |
| Workflow | Step Functions |
| File Event Processing | S3 + Lambda |
| DynamoDB Change Processing | Streams + Lambda |
| Global NoSQL | Global Tables |
| Too Many RDS Connections | RDS Proxy |
| Low Lambda Startup Latency | Provisioned Concurrency / SnapStart |
| Shared Lambda Files | EFS |
| Long Container Job | Fargate |

---

# Service Decision Map

Need:

**API**
→ API Gateway

Need:

**Compute**
→ Lambda

Need:

**NoSQL**
→ DynamoDB

Need:

**Objects**
→ S3

Need:

**Queue**
→ SQS

Need:

**Broadcast**
→ SNS

Need:

**Event Routing**
→ EventBridge

Need:

**Workflow**
→ Step Functions

Need:

**User Login**
→ Cognito

Need:

**Global Delivery**
→ CloudFront

---

# Final Exam Rapid-Fire

> **STATIC CONTENT**
> → S3 + CLOUDFRONT
>
> **SERVERLESS API**
> → API GATEWAY + LAMBDA
>
> **SERVERLESS NOSQL**
> → DYNAMODB
>
> **USER AUTH**
> → COGNITO
>
> **DIRECT FILE UPLOAD**
> → PRESIGNED URL / COGNITO
>
> **QUEUE**
> → SQS
>
> **FAN-OUT**
> → SNS
>
> **EVENT ROUTING**
> → EVENTBRIDGE
>
> **WORKFLOW**
> → STEP FUNCTIONS
>
> **FILE EVENT**
> → S3 + LAMBDA
>
> **TABLE CHANGE**
> → DYNAMODB STREAMS + LAMBDA
>
> **GLOBAL ACTIVE-ACTIVE NOSQL**
> → GLOBAL TABLES
>
> **RDS CONNECTION STORM**
> → RDS PROXY
>
> **COLD START**
> → PROVISIONED CONCURRENCY / SNAPSTART
>
> **MORE THAN 15 MINUTES**
> → FARGATE / ECS
>
> **EXCESS WORK**
> → SQS
>
> **DUPLICATE-SAFE**
> → IDEMPOTENCY

---

## Master Memory Trick

> [!tip] Serverless Architecture Master Memory Trick
> Imagine building an online store without owning a building.
>
> Customers enter through:
>
> **API GATEWAY**
> → Front Door
>
> They log in through:
>
> **COGNITO**
> → Identity Desk
>
> Workers perform tasks:
>
> **LAMBDA**
> → On-Demand Workers
>
> Product/order records live in:
>
> **DYNAMODB**
> → Database
>
> Files live in:
>
> **S3**
> → Warehouse
>
> Jobs wait in:
>
> **SQS**
> → Waiting Line
>
> Announcements go through:
>
> **SNS**
> → Loudspeaker
>
> Events are directed by:
>
> **EVENTBRIDGE**
> → Dispatcher
>
> Complex processes are coordinated by:
>
> **STEP FUNCTIONS**
> → Manager
>
> Global content is delivered by:
>
> **CLOUDFRONT**
> → Global Delivery Network

So remember:

> **FRONT DOOR**
> → API Gateway
>
> **WORKER**
> → Lambda
>
> **DATABASE**
> → DynamoDB
>
> **FILES**
> → S3
>
> **WAIT**
> → SQS
>
> **BROADCAST**
> → SNS
>
> **ROUTE**
> → EventBridge
>
> **ORCHESTRATE**
> → Step Functions
>
> **IDENTITY**
> → Cognito
>
> **GLOBAL DELIVERY**
> → CloudFront

And the killer SAA question:

> **"Can this application be decomposed into managed event-driven services instead of running continuously on servers?"**
>
> If yes:
>
> **Think serverless architecture.**

---

## Related Notes

- [[Lambda]]
- [[API Gateway]]
- [[API Gateway Security]]
- [[DynamoDB]]
- [[DynamoDB Advanced Features]]
- [[S3]]
- [[SQS]]
- [[SNS]]
- [[20-SAA/10-Messaging/EventBridge]]
- [[Step Functions]]
- [[Cognito]]
- [[CloudFront]]
- [[RDS Proxy]]
- [[Fargate]]
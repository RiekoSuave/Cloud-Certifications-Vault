## Core Concept

Serverless architecture means building applications where:

**AWS manages most of the underlying infrastructure**

You focus primarily on:

- Code
- Data
- Permissions
- Application logic
- Event flow

Common serverless services include:

- [[Lambda]]
- [[API Gateway]]
- [[DynamoDB]]
- [[S3]]
- [[SQS]]
- [[SNS]]
- [[EventBridge]]
- Step Functions

> [!tip] Memory Trick
> **Serverless = Focus on the Application, Not the Servers**

---

# What Serverless Does NOT Mean

Serverless does NOT mean:

**There are literally no servers**

It means:

**You do not manage the servers**

AWS handles much of:

- Provisioning
- Scaling
- Patching
- Infrastructure maintenance
- Availability

### Memory Trick

**Servers Still Exist**

**You Just Don't Manage Them**

---

# Why Use Serverless?

Serverless can be useful when you want:

- Minimal operational overhead
- Automatic scaling
- Pay-per-use pricing
- Event-driven processing
- Rapid development
- No EC2 server management

### Killer Exam Clue

> **Need a highly scalable application with minimal infrastructure administration**
>
> → **Serverless Architecture**

---

# Classic Serverless Web Architecture

A common pattern:

Users  
↓  
[[API Gateway]]  
↓  
[[Lambda]]  
↓  
[[DynamoDB]]

Optional additions:

- Cognito
- S3
- CloudFront
- SQS
- EventBridge

### Killer Memory Trick

> **API Gateway = Front Door**
>
> **Lambda = Compute**
>
> **DynamoDB = Database**

---

# API Gateway

[[API Gateway]] provides:

**Managed API endpoints**

It can expose:

- REST APIs
- HTTP APIs
- WebSocket APIs

### Killer Exam Clue

> **Need a managed API front end without running web servers**
>
> → **API Gateway**

---

# API Gateway + Lambda

Architecture:

Client  
↓  
API Gateway  
↓  
Lambda  
↓  
Backend Services

This is one of the most common:

**Serverless application patterns**

### Benefits

- No EC2 web servers
- Automatic scaling
- Pay-per-request style architecture
- Managed API layer

---

# Lambda

[[Lambda]] provides:

**Event-driven serverless compute**

Lambda runs code when:

**Triggered by an event**

Examples:

- API request
- S3 upload
- SQS message
- EventBridge event
- SNS notification

### Killer Exam Clue

> **Run code in response to events without managing servers**
>
> → **Lambda**

---

# Event-Driven Compute

Lambda works especially well when processing is:

**Triggered**

rather than:

**Continuously running**

Architecture:

Event  
↓  
Lambda  
↓  
Action

### Memory Trick

**Event Happens → Lambda Runs**

---

# Lambda Scaling

Lambda can automatically scale by increasing:

**Concurrent executions**

as demand increases.

### Exam Principle

> **Serverless reduces capacity planning, but service quotas still exist**

---

# Lambda Statelessness

Lambda should be treated as:

**Stateless compute**

Do NOT rely on:

- Local memory
- Local temporary files
- Same execution environment

being permanently available between:

**Invocations**

### Killer Exam Principle

> **Persistent state belongs outside Lambda**

---

# Persistent State for Lambda

Use external services such as:

- [[DynamoDB]]
- [[S3]]
- [[RDS]]
- [[Aurora]]
- EFS where appropriate

### Memory Trick

**Lambda Computes**

**Other Services Remember**

---

# Lambda Temporary Storage

Lambda can use temporary local storage during:

**Function execution**

But important persistent data should not depend on:

**That local storage surviving**

---

# Lambda Execution Role

Lambda accesses AWS services using:

**An IAM execution role**

Example:

Lambda  
↓  
IAM Role  
↓  
S3

### Killer Exam Clue

> **Lambda must write to S3 without hardcoded credentials**
>
> → **Lambda Execution Role**

---

# Lambda Timeout

Lambda has:

**Execution-duration limits**

This makes it better suited for:

**Shorter event-driven tasks**

than indefinitely running processes.

### Killer Exam Trap

> **Long-running continuous application**
>
> → Lambda may not be the best fit.

---

# Lambda Concurrency

Concurrency means:

**How many Lambda executions run simultaneously**

Higher event volume:

↓  
More concurrent invocations

### Exam Principle

> **Concurrency limits can become an architecture consideration**

---

# Reserved Concurrency

Reserved concurrency can help:

- Guarantee capacity for a function
- Limit how much concurrency it consumes

### Killer Exam Clue

> **Prevent one Lambda function from consuming all available account concurrency**
>
> → **Reserved Concurrency**

---

# Provisioned Concurrency

Provisioned Concurrency keeps:

**Pre-initialized Lambda environments**

ready to respond.

This helps reduce:

**Cold-start latency**

### Killer Exam Clue

> **Need predictable low latency for Lambda requests**
>
> → **Provisioned Concurrency**

---

# Cold Starts

A:

**Cold Start**

can occur when Lambda needs to initialize:

**A new execution environment**

This may add:

**Startup latency**

### Memory Trick

**Cold = Needs to Wake Up**

---

# Lambda + S3

A classic pattern:

User Uploads Object  
↓  
[[S3]]  
↓  
Event Notification  
↓  
Lambda  
↓  
Process Object

Use cases:

- Image resizing
- File validation
- Metadata extraction

### Killer Exam Clue

> **Automatically process a file when uploaded to S3**
>
> → **S3 Event + Lambda**

---

# Lambda + SQS

Architecture:

Producer  
↓  
[[SQS]]  
↓  
Lambda  
↓  
Process Messages

This provides:

**Serverless asynchronous processing**

### Killer Exam Clue

> **Need queued work processed automatically without managing worker servers**
>
> → **SQS + Lambda**

---

# Lambda + SNS

Architecture:

Publisher  
↓  
[[SNS]]  
↓  
Lambda

Use when:

**Lambda should react to published notifications**

---

# Lambda + EventBridge

Architecture:

AWS / App Event  
↓  
[[EventBridge]]  
↓  
Rule  
↓  
Lambda

Use for:

**Event-driven automation**

### Killer Exam Clue

> **Run Lambda when a specific AWS event occurs**
>
> → **EventBridge + Lambda**

---

# DynamoDB

[[DynamoDB]] provides:

**Serverless NoSQL storage**

Think:

- Key-value
- Document
- Millisecond latency
- Automatic scaling
- High availability

### Killer Exam Clue

> **Need highly scalable serverless key-value database**
>
> → **DynamoDB**

---

# DynamoDB On-Demand

On-Demand mode works well for:

**Unpredictable traffic**

because capacity adjusts without requiring:

**Manual provisioning**

### Killer Shortcut

Unpredictable DynamoDB  
→ On-Demand

Predictable DynamoDB  
→ Provisioned may be appropriate

---

# DynamoDB Streams

DynamoDB Streams capture:

**Item-level changes**

Examples:

- Insert
- Update
- Delete

Architecture:

DynamoDB  
↓  
Stream  
↓  
Lambda

### Killer Exam Clue

> **Trigger processing whenever DynamoDB records change**
>
> → **DynamoDB Streams + Lambda**

---

# S3

[[S3]] is a natural serverless storage service.

Use for:

- Static website assets
- User uploads
- Documents
- Media
- Data lakes

### Killer Exam Principle

> **Do not run EC2 just to serve scalable object storage**

---

# S3 + CloudFront

A common serverless static website architecture:

Users  
↓  
[[CloudFront]]  
↓  
S3

Benefits:

- Global caching
- No web servers
- High scalability
- Reduced origin load

### Killer Exam Clue

> **Globally distribute static website content without EC2**
>
> → **S3 + CloudFront**

---

# Cognito

[[Cognito]] can provide:

**User authentication and authorization**

for serverless applications.

Architecture:

User  
↓  
Cognito  
↓  
API Gateway  
↓  
Lambda

### Killer Exam Clue

> **Need managed sign-up/sign-in for application users**
>
> → **Cognito**

---

# Step Functions

Step Functions coordinates:

**Multi-step workflows**

Architecture:

Task A  
↓  
Decision  
↓  
Task B  
↓  
Task C

Possible tasks include:

- Lambda
- AWS service integrations
- Human approval patterns
- Parallel steps

### Killer Exam Clue

> **Need to orchestrate multiple serverless tasks with retries and workflow state**
>
> → **Step Functions**

---

# Step Functions vs SQS

## Step Functions

Think:

**Workflow orchestration**

## SQS

Think:

**Work queue**

### Killer Shortcut

Ordered multi-step workflow  
→ Step Functions

Independent asynchronous jobs  
→ SQS

---

# Step Functions vs EventBridge

## Step Functions

Controls:

**The sequence of work**

## EventBridge

Routes:

**Events to targets**

### Memory Trick

**EventBridge = Route**

**Step Functions = Orchestrate**

---

# EventBridge

[[EventBridge]] provides:

**Serverless event routing**

Use for:

- AWS events
- Application events
- SaaS events
- Event-driven architectures

### Killer Exam Clue

> **Route different event types to different targets using rules**
>
> → **EventBridge**

---

# Serverless Decoupling

Serverless systems often use:

[[SQS]]

to decouple:

**Producers and consumers**

Architecture:

API Gateway  
↓  
Lambda  
↓  
SQS  
↓  
Lambda Workers

### Killer Exam Principle

> **Serverless does not eliminate the need for decoupling**

---

# Serverless Fan-Out

Use:

[[SNS]]

when one event needs to reach:

**Multiple consumers**

Architecture:

Event  
↓  
SNS  
↓  
├── Lambda
├── SQS
└── Other Subscriber

---

# Serverless Workflow Example

Order Submitted  
↓  
API Gateway  
↓  
Lambda  
↓  
Step Functions  
↓  
Payment  
↓  
Inventory  
↓  
Shipping

This provides:

**Managed workflow orchestration**

without running:

**Dedicated orchestration servers**

---

# Serverless Image Processing

Architecture:

User  
↓  
S3 Upload  
↓  
Lambda  
↓  
Process Image  
↓  
Store Result in S3

This is a classic:

**Event-driven serverless pattern**

---

# Serverless API Architecture

Users  
↓  
CloudFront  
↓  
API Gateway  
↓  
Lambda  
↓  
DynamoDB

Possible additions:

Cognito  
→ Authentication

WAF  
→ Web protection

### Killer Exam Pattern

> **Highly variable public API with minimal infrastructure administration**
>
> → **API Gateway + Lambda + DynamoDB**

---

# Serverless and Auto Scaling

Traditional:

EC2  
↓  
Auto Scaling Group

Serverless:

Service itself often handles much of:

**Scaling automatically**

### Memory Trick

**EC2 = You Configure Scaling**

**Serverless = Service Handles More Scaling**

---

# Serverless and High Availability

Managed serverless services are typically designed with:

**Built-in AWS-managed availability**

This reduces the need to manually build:

**Multi-AZ server fleets**

### Exam Principle

> **Managed/serverless does not mean no architecture decisions, but AWS handles more infrastructure resilience**

---

# Serverless and Cost

Serverless pricing often aligns with:

**Actual usage**

This can be attractive for:

- Sporadic workloads
- Variable workloads
- Event-driven workloads

### Killer Exam Clue

> **Application is idle most of the day and should avoid paying for always-on servers**
>
> → **Serverless**

---

# Serverless Is Not Always Cheapest

If workload is:

**Constant and extremely high-volume**

always-on infrastructure may sometimes be more:

**Cost-efficient**

### Exam Principle

> **Choose serverless because it fits the workload, not because it is automatically cheapest**

---

# Serverless and Operational Overhead

One of the strongest exam clues is:

**Minimal operational overhead**

Serverless removes tasks such as:

- Server patching
- OS management
- Instance replacement
- Capacity provisioning

### Killer Exam Shortcut

> **Least management**
>
> → Strongly consider **serverless/managed services**

---

# Serverless Security

Serverless still requires:

- IAM
- Encryption
- Secrets management
- Logging
- Input validation
- Network design where applicable

### Exam Trap

> **No servers to manage does NOT mean no security responsibilities**

---

# IAM Least Privilege

Each Lambda function should have:

**Only the permissions it requires**

Example:

Image Processor Lambda  
→ Read from Upload Bucket  
→ Write to Processed Bucket

Not:

**AdministratorAccess**

---

# Secrets

Do not put:

**Database passwords or API keys**

directly into:

- Lambda code
- Environment configuration without proper protection

Use:

[[Secrets Manager]]

or another appropriate secure configuration mechanism.

---

# Monitoring

Use:

[[CloudWatch]]

for:

- Lambda metrics
- Logs
- Alarms
- Operational monitoring

### Killer Exam Clue

> **Need to monitor Lambda errors and duration**
>
> → **CloudWatch**

---

# Dead-Letter Handling

Asynchronous serverless architectures should account for:

**Failed events**

Possible patterns include:

- SQS DLQ
- Service-specific failure destinations
- Retry policies

### Killer Exam Principle

> **Failed asynchronous work should not disappear silently**

---

# Retries and Idempotency

Serverless event-driven systems may:

**Retry failed operations**

Therefore application logic should often be:

**Idempotent**

### Memory Trick

**Retry Safe = Idempotent**

---

# API Gateway Throttling

API Gateway can help protect backends through:

**Throttling**

This prevents clients from overwhelming:

**Backend integrations**

### Killer Exam Clue

> **Need to limit API request rates**
>
> → **API Gateway Throttling**

---

# API Gateway Caching

API Gateway can cache:

**API responses**

to reduce:

- Backend calls
- Lambda invocations
- Latency

### Killer Exam Clue

> **Same API responses are repeatedly requested**
>
> → **API Gateway Cache**

---

# Serverless vs Containers

## Serverless

Think:

- Minimal infrastructure
- Event-driven
- Function/service model

## Containers

Think:

- More control
- Long-running processes
- Custom runtimes
- Portability

### Killer Shortcut

Short event-driven function  
→ Lambda

Long-running custom service  
→ ECS / EKS may be more appropriate

---

# Serverless vs EC2

## EC2

Choose when you need:

- OS control
- Long-running processes
- Custom agents
- Specialized software

## Serverless

Choose when you need:

- Minimal administration
- Event-driven execution
- Automatic scaling
- Variable traffic

### Memory Trick

**Need the Server?**
→ EC2

**Need the Function?**
→ Lambda

---

# Serverless vs RDS

Traditional serverless architecture often uses:

**DynamoDB**

but relational requirements may still require:

**RDS / Aurora**

### Exam Principle

> **Do not choose NoSQL simply because the architecture is serverless**

The:

**Data model**

still determines:

**The right database**

---

# Aurora Serverless

Aurora Serverless can provide:

**Automatically adjusting relational database capacity**

for compatible workloads.

### Killer Exam Clue

> **Need relational database with highly variable capacity requirements**
>
> → **Aurora Serverless**

---

# Architecture Thinking

## Scenario 1 — Sporadic API

API receives:

Very little traffic overnight

and:

Large unpredictable daytime bursts.

Operations team wants:

**No server management**

Choose:

API Gateway  
+  
Lambda  
+  
DynamoDB

---

## Scenario 2 — Image Upload

Every uploaded S3 image must:

**Automatically create a thumbnail**

Choose:

S3 Event  
+  
Lambda

---

## Scenario 3 — Async Orders

API should immediately accept:

**Order**

but processing can happen later.

Choose:

API Gateway  
↓  
Lambda  
↓  
SQS  
↓  
Lambda Worker

---

## Scenario 4 — Multi-Step Order

Order processing requires:

1. Charge payment
2. Reserve inventory
3. Schedule shipment
4. Handle retries

Choose:

**Step Functions**

---

## Scenario 5 — DynamoDB Change

When a DynamoDB record changes:

Lambda must automatically process it.

Choose:

**DynamoDB Streams + Lambda**

---

## Scenario 6 — Global Static Site

Website consists mostly of:

HTML, CSS, JavaScript, images.

Choose:

**S3 + CloudFront**

---

## Scenario 7 — Authentication

Serverless app needs:

**User registration and login**

Choose:

**Cognito**

---

## Scenario 8 — Long-Running Process

Application must run:

**Continuously for many hours**

with custom OS-level dependencies.

Do not automatically choose:

Lambda.

Consider:

**ECS / EKS / EC2**

depending on requirements.

---

# Scenario Recognition

Immediately think:

**Lambda**

when you see:

- Event-driven code
- No server management
- Short-lived processing
- Automatic compute scaling

Think:

**API Gateway**

when you see:

- Managed API
- REST
- HTTP API
- WebSocket API

Think:

**DynamoDB**

when you see:

- Serverless NoSQL
- Key-value
- Massive scale

Think:

**Step Functions**

when you see:

- Workflow
- Multiple steps
- Orchestration
- Retry logic

---

# Exam Traps

## Trap 1 — Serverless Means No Servers Exist

❌

AWS manages:

**The servers**

---

## Trap 2 — Lambda Is Good for Every Workload

❌

Long-running or highly specialized workloads may fit:

**Containers or EC2**

better.

---

## Trap 3 — Lambda Local State Is Durable

❌

Persistent state belongs in:

**External storage**

---

## Trap 4 — Serverless Means Unlimited Scaling

❌

Services have:

**Quotas and scaling characteristics**

---

## Trap 5 — DynamoDB Is Required for Every Serverless App

❌

Choose the database based on:

**Data requirements**

---

## Trap 6 — Serverless Means No IAM Needed

❌

IAM remains:

**Critical**

---

## Trap 7 — Serverless Is Always Cheapest

❌

Usage patterns determine:

**Cost efficiency**

---

# Quick Cheat Sheet

| Exam Clue | Answer |
|---|---|
| Event-Driven Compute | Lambda |
| Managed API | API Gateway |
| Serverless NoSQL | DynamoDB |
| Static Object Storage | S3 |
| Global Static Delivery | CloudFront |
| User Authentication | Cognito |
| Async Buffer | SQS |
| Fan-Out | SNS |
| Event Routing | EventBridge |
| Workflow Orchestration | Step Functions |
| DynamoDB Change Processing | Streams + Lambda |
| Monitor Lambda | CloudWatch |
| Fast Lambda Startup | Provisioned Concurrency |

---

# Serverless Decision Map

Need:

**Run code on event**

→ Lambda

Need:

**Expose API**

→ API Gateway

Need:

**NoSQL database**

→ DynamoDB

Need:

**Static files**

→ S3

Need:

**Global static delivery**

→ CloudFront

Need:

**User sign-in**

→ Cognito

Need:

**Queue**

→ SQS

Need:

**Broadcast**

→ SNS

Need:

**Route events**

→ EventBridge

Need:

**Orchestrate steps**

→ Step Functions

---

# Classic Serverless Stack

> **USER**
> ↓
> CLOUDFRONT
> ↓
> API GATEWAY
> ↓
> LAMBDA
> ↓
> DYNAMODB
>
> Optional:
>
> COGNITO
> → AUTH
>
> SQS
> → BUFFER
>
> SNS
> → FAN-OUT
>
> EVENTBRIDGE
> → EVENTS
>
> STEP FUNCTIONS
> → WORKFLOW

---

# Final Exam Rapid-Fire

> **NO SERVER MANAGEMENT**
> → SERVERLESS
>
> **EVENT COMPUTE**
> → LAMBDA
>
> **API FRONT DOOR**
> → API GATEWAY
>
> **SERVERLESS NOSQL**
> → DYNAMODB
>
> **STATIC STORAGE**
> → S3
>
> **GLOBAL STATIC**
> → CLOUDFRONT
>
> **AUTHENTICATION**
> → COGNITO
>
> **BUFFER**
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
> **DYNAMODB CHANGES**
> → STREAMS
>
> **LOWER COLD START**
> → PROVISIONED CONCURRENCY

---

## Master Memory Trick

> [!tip] Serverless Architecture Master Memory Trick
> Imagine you're opening:
>
> **A restaurant**
>
> Traditional EC2 means:
>
> You own the building.
>
> You maintain the kitchen.
>
> You repair equipment.
>
> You hire someone to watch the building all night.
>
> Serverless means:
>
> AWS manages:
>
> **THE BUILDING**
>
> You focus on:
>
> **THE FOOD**
>
> A customer places an order:
>
> **API GATEWAY**
>
> The cook prepares it:
>
> **LAMBDA**
>
> The order information is stored:
>
> **DYNAMODB**
>
> A job must wait?
>
> **SQS**
>
> Everyone needs to hear the announcement?
>
> **SNS**
>
> Different events need different destinations?
>
> **EVENTBRIDGE**
>
> The recipe has multiple ordered steps?
>
> **STEP FUNCTIONS**

So remember:

> **API GATEWAY**
> → FRONT DOOR
>
> **LAMBDA**
> → COMPUTE
>
> **DYNAMODB**
> → DATA
>
> **S3**
> → OBJECTS
>
> **SQS**
> → WAIT
>
> **SNS**
> → BROADCAST
>
> **EVENTBRIDGE**
> → ROUTE
>
> **STEP FUNCTIONS**
> → ORCHESTRATE
>
> **COGNITO**
> → USERS

And the killer SAA question:

> **"Can this workload use managed event-driven services instead of maintaining always-on infrastructure?"**
>
> YES
>
> → **Strongly consider a serverless architecture**

---

## Related Notes

- [[Architecture Principles]]
- [[Stateless vs Stateful Architecture]]
- [[Decoupled Architecture]]
- [[Scalable Architecture]]
- [[Cost-Optimized Architecture]]
- [[Lambda]]
- [[API Gateway]]
- [[DynamoDB]]
- [[S3]]
- [[SQS]]
- [[SNS]]
- [[EventBridge]]
- [[CloudFront]]
- [[Cognito]]
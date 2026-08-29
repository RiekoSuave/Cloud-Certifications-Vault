## Core Serverless Services

| Service | Main Purpose | Killer Exam Clue |
|---|---|---|
| [[Lambda]] | Serverless compute | Run code without servers |
| [[API Gateway]] | Managed API front door | REST/HTTP/WebSocket API |
| [[DynamoDB]] | Serverless NoSQL database | Massive scale + low latency |
| [[S3]] | Object storage | Files / objects / static content |
| [[SQS]] | Queue | Buffer / decouple |
| [[SNS]] | Pub/Sub fan-out | One message → many subscribers |
| [[20-SAA/10-Messaging/EventBridge]] | Event routing | Rules + targets |
| [[Step Functions]] | Workflow orchestration | Multi-step stateful workflows |
| [[Cognito]] | App-user identity | Sign-up/sign-in / temporary AWS credentials |
| [[CloudFront]] | Global content delivery | Edge caching / CDN |
| [[Fargate]] | Serverless container compute | Containers without EC2 management |

> [!tip] Master Serverless Memory Trick
> **API = API Gateway**
>
> **CODE = Lambda**
>
> **DATA = DynamoDB**
>
> **FILES = S3**
>
> **WAIT = SQS**
>
> **BROADCAST = SNS**
>
> **ROUTE = EventBridge**
>
> **WORKFLOW = Step Functions**
>
> **USERS = Cognito**

---

# Lambda

[[Lambda]] provides:

**Serverless event-driven compute**

Think:

Event  
↓  
Lambda  
↓  
Action

### Killer Exam Clue

> **Run short-lived code without managing servers**
>
> → **Lambda**

---

## Lambda Maximum Runtime

Maximum execution time:

**15 minutes**

### Killer Shortcut

**More than 15 minutes**
→ Consider ECS / Fargate / Batch / EC2

---

## Lambda Invocation Types

### Synchronous

Caller:

**Waits for response**

Examples:

- API Gateway
- ALB
- Function URL
- SDK direct invocation

Memory:

**SYNC = CALL → WAIT → RESPONSE**

---

### Asynchronous

Caller:

**Does not wait**

Examples:

- S3
- SNS
- EventBridge

Memory:

**ASYNC = SEND → MOVE ON**

---

### Event Source Mapping

Lambda:

**Polls source**

Examples:

- SQS
- Kinesis
- DynamoDB Streams

Memory:

**POLL → BATCH → INVOKE**

---

# Invocation Cheat Sheet

| Source | Model |
|---|---|
| API Gateway | Synchronous |
| ALB | Synchronous |
| Function URL | Synchronous |
| S3 | Asynchronous |
| SNS | Asynchronous |
| EventBridge | Asynchronous |
| SQS | Event Source Mapping |
| Kinesis | Event Source Mapping |
| DynamoDB Streams | Event Source Mapping |

---

# Lambda Retry Ownership

## Synchronous

**Caller handles retry**

## Asynchronous

**Lambda handles retry**

## SQS / Streams

Failure behavior depends on:

**Event source semantics**

### Memory Trick

**SYNC = CALLER RETRIES**

**ASYNC = LAMBDA RETRIES**

---

# Lambda Execution Role

Controls:

**What Lambda can access**

Direction:

Lambda  
→ AWS Service

Examples:

Lambda  
→ S3

Lambda  
→ DynamoDB

Lambda  
→ Secrets Manager

### Memory Trick

**Execution Role = Lambda goes OUT**

---

# Lambda Resource-Based Policy

Controls:

**Who can invoke Lambda**

Direction:

AWS Service / Principal  
→ Lambda

### Memory Trick

**Resource Policy = Caller comes IN**

---

# Lambda IAM Shortcut

> **LAMBDA → AWS**
> → Execution Role
>
> **AWS → LAMBDA**
> → Resource-Based Policy

---

# Lambda Environment Variables

Use for:

**Configuration**

Examples:

- Table name
- Bucket name
- Environment
- Feature flag

Do NOT treat them as:

**IAM permissions**

### Memory Trick

**ENV VAR = CONFIG**

---

# Secrets

Sensitive values such as:

- Passwords
- API keys
- Tokens

should generally use:

[[Secrets Manager]]

### Memory Trick

**CONFIG = Environment Variable**

**SECRET = Secrets Manager**

---

# Lambda Layers

Use:

**Lambda Layers**

for:

- Shared libraries
- Dependencies
- Utilities
- Custom runtimes

### Memory Trick

**LAYER = SHARED CODE**

---

# Lambda Concurrency

Concurrency means:

**Simultaneous Lambda executions**

---

## Reserved Concurrency

Use for:

- Reserve capacity
- Limit maximum function concurrency
- Protect downstream resources
- Prevent one function consuming all capacity

### Memory Trick

**RESERVED = RESERVE + RESTRICT**

---

## Provisioned Concurrency

Use for:

**Pre-initialized environments**

Goal:

**Reduce cold-start latency**

### Memory Trick

**PROVISIONED = PRE-WARM**

---

## SnapStart

Use for:

**Snapshot-based startup optimization**

Concept:

Initialize  
↓  
Snapshot  
↓  
Restore Faster

### Memory Trick

**SNAPSTART = SNAPSHOT + RESTORE**

---

# Concurrency Comparison

| Requirement | Feature |
|---|---|
| Limit Lambda Scale | Reserved Concurrency |
| Guarantee Function Capacity | Reserved Concurrency |
| Protect Downstream Resource | Reserved Concurrency |
| Reduce Cold Starts | Provisioned Concurrency |
| Keep Environments Ready | Provisioned Concurrency |
| Snapshot-Based Startup | SnapStart |

---

# Lambda + RDS

Problem:

Lambda scales rapidly  
↓  
Too Many DB Connections

Solution:

[[RDS Proxy]]

Architecture:

Lambda  
↓  
RDS Proxy  
↓  
RDS

### Killer Exam Clue

> **Lambda overwhelms RDS with connections**
>
> → **RDS Proxy**

---

# Lambda@Edge

[[Lambda@Edge]] runs:

**Advanced Lambda logic at CloudFront edge locations**

Use for:

- Viewer request logic
- Origin request logic
- Origin response logic
- Viewer response logic

### Killer Exam Clue

> **Advanced CloudFront edge processing**
>
> → **Lambda@Edge**

---

## Lambda@Edge Key Facts

- Created in `us-east-1`
- Uses published Lambda version
- Integrated with CloudFront
- Supports origin events
- No VPC access
- No Lambda Layers
- No Provisioned Concurrency

---

# CloudFront Functions vs Lambda@Edge

### CloudFront Functions

Think:

**Light + Fast**

Use for:

- Simple redirects
- URI rewrites
- Header manipulation

### Lambda@Edge

Think:

**Advanced + Origin Events**

### Shortcut

**Simple viewer logic**
→ CloudFront Functions

**Origin request/response**
→ Lambda@Edge

---

# DynamoDB

[[DynamoDB]] is:

**Serverless NoSQL**

Think:

- Key-value/document
- Millisecond latency
- Massive scale
- No server management

### Killer Exam Clue

> **Serverless NoSQL at massive scale**
>
> → **DynamoDB**

---

# DynamoDB Keys

## Partition Key

Determines:

**Data distribution**

## Sort Key

Orders related items within:

**Same partition key**

### Memory Trick

**Partition = Group**

**Sort = Order Within Group**

---

# DynamoDB Capacity Modes

## On-Demand

Use for:

- Unpredictable
- Spiky
- New workloads

### Memory

**On-Demand = Surprise Me**

---

## Provisioned

Use for:

- Predictable traffic
- Cost optimization
- Capacity planning

### Memory

**Provisioned = Predict**

---

# DynamoDB Consistency

## Eventually Consistent

- Lower cost
- May be briefly stale

## Strongly Consistent

- Latest committed value
- Higher read-capacity cost

### Shortcut

**Latest value required**
→ Strongly Consistent

---

# DynamoDB Indexes

## GSI

**Different partition key**

Can be created after table creation.

### Memory

**GSI = Global Key Change**

---

## LSI

**Same partition key + different sort key**

Must be created:

**With the table**

### Memory

**LSI = Local Sort Change**

---

# GSI vs LSI

| Feature | GSI | LSI |
|---|---:|---:|
| Different Partition Key | ✅ | ❌ |
| Different Sort Key | ✅ | ✅ |
| Same Partition Key Required | ❌ | ✅ |
| Add Later | ✅ | ❌ |
| Strongly Consistent Reads | ❌ | ✅ |

---

# Query vs Scan

## Query

Efficient when you know:

**Partition key**

## Scan

Reads:

**Every item**

### Memory Trick

**QUERY = TARGET**

**SCAN = EVERYTHING**

---

# DynamoDB Advanced Features

## DAX

**Microsecond DynamoDB reads**

### Memory

**DAX = CACHE**

---

## TTL

**Automatically expires items**

### Memory

**TTL = EXPIRE**

---

## DynamoDB Streams

**React to item changes**

Common architecture:

DynamoDB Streams  
↓  
Lambda

### Memory

**STREAMS = REACT**

---

## Global Tables

**Multi-Region active-active DynamoDB**

### Memory

**GLOBAL TABLES = GLOBAL WRITES**

---

## Transactions

**All-or-nothing multi-item operations**

### Memory

**TRANSACTION = ATOMIC**

---

## PITR

**Point-in-Time Recovery**

### Memory

**PITR = TURN BACK THE CLOCK**

---

# DynamoDB Advanced Shortcut

> **MICROSECOND**
> → DAX
>
> **EXPIRE**
> → TTL
>
> **CHANGE EVENT**
> → STREAMS
>
> **GLOBAL ACTIVE-ACTIVE**
> → GLOBAL TABLES
>
> **ALL OR NOTHING**
> → TRANSACTIONS
>
> **RECOVER EARLIER**
> → PITR

---

# API Gateway

[[API Gateway]] is:

**Managed API front door**

Supports:

- REST API
- HTTP API
- WebSocket API

### Killer Exam Clue

> **Managed API with routing, security, throttling, and backend integration**
>
> → **API Gateway**

---

# REST vs HTTP vs WebSocket

## REST API

Think:

**Advanced features**

Examples:

- Usage plans
- API keys
- Caching
- Mapping templates

---

## HTTP API

Think:

**Simple + Lower Cost + Lower Latency**

---

## WebSocket API

Think:

**Persistent bidirectional communication**

Examples:

- Chat
- Live updates

---

# API Type Shortcut

**Advanced API management**
→ REST API

**Simple HTTP API**
→ HTTP API

**Real-time two-way**
→ WebSocket

---

# API Gateway Endpoint Types

## Edge-Optimized

Think:

**Global public clients**

## Regional

Think:

**Regional public clients**

## Private

Think:

**VPC-only clients**

---

# Private API vs VPC Link

## Private API

Controls:

**How clients reach API Gateway**

## VPC Link

Controls:

**How API Gateway reaches private backend**

### Memory Trick

**Private API = Private Front Door**

**VPC Link = Private Back Door**

---

# API Gateway Security

Important mechanisms:

- IAM
- Cognito
- Lambda Authorizer
- Resource Policies
- WAF
- API Keys
- Usage Plans

---

## IAM Authorization

Think:

**AWS identities**

---

## Cognito

Think:

**Application users**

---

## Lambda Authorizer

Think:

**Custom auth logic**

---

## Resource Policy

Think:

**Access boundary**

Examples:

- AWS account
- Source IP
- VPC endpoint

---

## WAF

Think:

**Web attack protection**

Examples:

- SQL injection
- XSS
- Malicious IPs

---

## API Keys

Think:

**Usage identification**

NOT:

**Strong authentication**

---

## Usage Plans

Think:

**Quotas + throttling**

---

# API Gateway Security Shortcut

> **AWS IDENTITY**
> → IAM
>
> **APP USER**
> → COGNITO
>
> **CUSTOM AUTH**
> → LAMBDA AUTHORIZER
>
> **NETWORK / ACCOUNT RESTRICTION**
> → RESOURCE POLICY
>
> **WEB ATTACK**
> → WAF
>
> **USAGE METER**
> → API KEY
>
> **QUOTA**
> → USAGE PLAN

---

# Step Functions

[[Step Functions]] provides:

**Serverless workflow orchestration**

Use for:

- Branching
- Retry
- Catch
- Wait
- Parallel execution
- State tracking

### Killer Exam Clue

> **Coordinate multiple serverless steps**
>
> → **Step Functions**

---

# State Types

| State | Think |
|---|---|
| Task | DO |
| Choice | IF / ELSE |
| Wait | PAUSE |
| Parallel | TOGETHER |
| Map | FOR EACH |
| Pass | MOVE DATA |
| Succeed | DONE ✅ |
| Fail | DONE ❌ |

---

# Retry vs Catch

## Retry

**Try again**

## Catch

**Handle failure path**

---

# Standard vs Express Workflows

## Standard

Think:

- Long-running
- Durable
- Auditable
- Business workflows

## Express

Think:

- Short
- High-volume
- High-throughput

### Shortcut

**Long + durable**
→ Standard

**Fast + huge volume**
→ Express

---

# Step Functions Integration Patterns

## Request/Response

Call service and wait for:

**Immediate response**

## Run a Job

Start job and wait until:

**Job completes**

## Callback / Task Token

Wait until:

**External process signals completion**

### Killer Clue

**Human approval**
→ Callback / Task Token

---

# Cognito

[[Cognito]] handles:

**Application user identity**

Two major pieces:

- User Pools
- Identity Pools

---

# User Pool

Think:

**Authentication**

Provides:

- Sign-up
- Sign-in
- MFA
- JWT tokens
- Social login
- Federation

### Memory

**USER POOL = WHO ARE YOU?**

---

# Identity Pool

Think:

**Temporary AWS credentials**

Provides:

- IAM role mapping
- Direct S3 access
- Direct DynamoDB access
- Guest access

### Memory

**IDENTITY POOL = HERE ARE AWS CREDENTIALS**

---

# User Pool vs Identity Pool

| Requirement | User Pool | Identity Pool |
|---|---:|---:|
| Sign-Up | ✅ | ❌ |
| Sign-In | ✅ | ❌ |
| JWT Tokens | ✅ | ❌ Primary |
| Temporary AWS Credentials | ❌ | ✅ |
| IAM Role Mapping | ❌ | ✅ |
| Direct AWS Service Access | ❌ | ✅ |

---

# Cognito Token Shortcut

> **ID TOKEN**
> → WHO YOU ARE
>
> **ACCESS TOKEN**
> → WHAT YOU CAN ACCESS
>
> **REFRESH TOKEN**
> → GET NEW TOKENS

---

# Serverless Messaging

## SQS

Think:

**Queue / Buffer / Decouple**

### Killer Clue

**Work must wait**
→ SQS

---

## SNS

Think:

**Fan-Out**

### Killer Clue

**One message → many consumers**
→ SNS

---

## EventBridge

Think:

**Rule-Based Event Routing**

### Killer Clue

**Route different events to different targets**
→ EventBridge

---

## Step Functions

Think:

**Workflow orchestration**

### Killer Clue

**Coordinate steps**
→ Step Functions

---

# Messaging Master Shortcut

> **WAIT**
> → SQS
>
> **BROADCAST**
> → SNS
>
> **ROUTE**
> → EVENTBRIDGE
>
> **ORCHESTRATE**
> → STEP FUNCTIONS

---

# Serverless Storage

## S3

Think:

**Objects / files**

## DynamoDB

Think:

**NoSQL records**

## EFS

Think:

**Shared filesystem**

### Shortcut

**OBJECT**
→ S3

**NOSQL**
→ DynamoDB

**SHARED FILESYSTEM**
→ EFS

---

# Direct S3 Upload Pattern

Avoid:

Client  
↓  
API Gateway  
↓  
Lambda  
↓  
S3

for large file uploads when unnecessary.

Better:

Client  
↓  
Presigned URL  
↓  
S3

or:

Client  
↓  
Cognito Identity Pool  
↓  
Temporary Credentials  
↓  
S3

### Killer Exam Clue

> **Large client upload with minimum compute overhead**
>
> → **Direct S3 upload**

---

# Serverless Caching

| Requirement | Service |
|---|---|
| Edge Content Cache | CloudFront |
| API Response Cache | API Gateway Cache |
| DynamoDB Cache | DAX |
| General Application Cache | ElastiCache |

---

# Event-Driven Architecture

Common pattern:

Event  
↓  
Messaging / Routing  
↓  
Compute  
↓  
Storage

Example:

Order Created  
↓  
EventBridge  
↓  
Lambda  
↓  
DynamoDB

---

# Decoupling Pattern

Bad:

Producer  
↓  
Consumer

Better:

Producer  
↓  
SQS  
↓  
Consumer

Benefits:

- Buffering
- Resilience
- Independent scaling
- Backpressure

---

# Fan-Out Pattern

Producer  
↓  
SNS  
↓  
├── SQS A
├── SQS B
└── Lambda C

Think:

**One event → multiple independent consumers**

---

# Workflow Pattern

EventBridge  
↓  
Step Functions  
↓  
├── Lambda
├── Fargate
└── AWS Service

Think:

**Route event → orchestrate workflow**

---

# Global Serverless App

CloudFront  
↓  
API Gateway  
↓  
Lambda  
↓  
DynamoDB Global Tables

Optional:

Cognito  
→ Authentication

WAF  
→ Protection

---

# Classic Serverless Web App

User  
↓  
CloudFront  
↓  
S3 Static Frontend

Dynamic Request  
↓  
API Gateway  
↓  
Lambda  
↓  
DynamoDB

Authentication:

Cognito

---

# Failure Handling

## Async Lambda Failure

Think:

- Lambda Destinations
- Lambda DLQ

## SQS Consumer Failure

Think:

- Visibility Timeout
- Redrive Policy
- SQS DLQ
- Partial Batch Response

## Step Functions Failure

Think:

- Retry
- Catch

### Master Failure Trick

**ASYNC RESULT**
→ Destinations

**BAD QUEUE MESSAGE**
→ SQS DLQ

**WORKFLOW ERROR**
→ Retry / Catch

---

# Idempotency

Serverless event-driven applications should often be:

**Idempotent**

Meaning:

> **Processing the same event multiple times should not create duplicate business effects.**

### Killer Exam Clue

**Possible duplicate event delivery**
→ Design idempotently

---

# Stateless Design

Serverless compute should generally remain:

**Stateless**

State belongs in:

- DynamoDB
- S3
- RDS
- EFS
- ElastiCache

### Memory Trick

**COMPUTE = TEMPORARY**

**STATE = EXTERNAL**

---

# Lambda vs Fargate

## Lambda

Think:

- Event-driven function
- Maximum 15 minutes
- Fine-grained serverless compute

## [[Fargate]]

Think:

- Containers
- Longer-running workloads
- More runtime control
- No EC2 management

### Shortcut

**Function**
→ Lambda

**Long-running container**
→ Fargate

---

# API Gateway vs ALB

## API Gateway

Think:

- API management
- Auth
- Throttling
- Usage plans
- Stages

## [[Application Load Balancer]]

Think:

- Web load balancing
- Host/path routing
- ECS/EC2/Lambda targets

### Shortcut

**API PLATFORM**
→ API Gateway

**LOAD BALANCER**
→ ALB

---

# Step Functions vs SQS vs EventBridge

| Need | Service |
|---|---|
| Hold Work | SQS |
| Route Event | EventBridge |
| Coordinate Steps | Step Functions |

---

# DynamoDB vs RDS

## DynamoDB

- NoSQL
- Serverless
- Key-value/document
- Massive scale

## [[RDS]]

- SQL
- Relational
- Joins
- Structured relationships

### Shortcut

**NOSQL**
→ DynamoDB

**SQL**
→ RDS

---

# Killer Exam Traps

## Trap 1 — Serverless Means No Servers Exist

❌

AWS manages:

**The servers**

---

## Trap 2 — Every Serverless Application Must Use Lambda

❌

Serverless includes many managed services.

---

## Trap 3 — Lambda Can Run Longer Than 15 Minutes Asynchronously

❌

Still:

**15-minute maximum**

---

## Trap 4 — API Key Authenticates Users

❌

Think:

**Usage metering**

---

## Trap 5 — User Pool Gives AWS Credentials

❌

Think:

**Identity Pool**

---

## Trap 6 — Reserved Concurrency Fixes Cold Starts

❌

Think:

**Provisioned Concurrency / SnapStart**

---

## Trap 7 — DAX Improves DynamoDB Writes

❌

Think:

**Read cache**

---

## Trap 8 — GSI Supports Strongly Consistent Reads

❌

GSI:

**Eventually consistent**

---

## Trap 9 — SQS Pushes Directly to Lambda

❌

Lambda polls via:

**Event Source Mapping**

---

## Trap 10 — Step Functions Is a Queue

❌

It is:

**Workflow orchestration**

---

## Trap 11 — EventBridge and SNS Are the Same

❌

SNS:

**Broadcast**

EventBridge:

**Route**

---

## Trap 12 — Private API and VPC Link Are the Same

❌

Private API:

**Client → API**

VPC Link:

**API → Backend**

---

# Master Architecture Decision Table

| Requirement | Best Choice |
|---|---|
| Serverless Compute | Lambda |
| Serverless API | API Gateway |
| Serverless NoSQL | DynamoDB |
| Object Storage | S3 |
| Queue | SQS |
| Fan-Out | SNS |
| Rule-Based Event Routing | EventBridge |
| Workflow | Step Functions |
| App User Login | Cognito User Pool |
| Temporary AWS Credentials | Cognito Identity Pool |
| Global Content Delivery | CloudFront |
| Long Serverless Container Job | Fargate |
| DynamoDB Microsecond Reads | DAX |
| Multi-Region NoSQL | DynamoDB Global Tables |
| Lambda DB Connection Pool | RDS Proxy |
| Protect API from Web Attacks | WAF |
| Private API Access | Private API |
| API to Private Backend | VPC Link |

---

# Ultimate Serverless Decision Tree

Need compute?

→ **Lambda**

Need compute longer than 15 minutes?

→ **Fargate / ECS / Batch**

Need API?

→ **API Gateway**

Need NoSQL?

→ **DynamoDB**

Need object/file storage?

→ **S3**

Need queue?

→ **SQS**

Need one-to-many fan-out?

→ **SNS**

Need event routing?

→ **EventBridge**

Need workflow orchestration?

→ **Step Functions**

Need app-user authentication?

→ **Cognito User Pool**

Need temporary AWS credentials?

→ **Cognito Identity Pool**

---

# Final Exam Rapid-Fire

> **SERVERLESS CODE**
> → LAMBDA
>
> **MAX LAMBDA RUNTIME**
> → 15 MINUTES
>
> **SERVERLESS API**
> → API GATEWAY
>
> **SERVERLESS NOSQL**
> → DYNAMODB
>
> **FILE STORAGE**
> → S3
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
> **USER LOGIN**
> → COGNITO USER POOL
>
> **TEMP AWS CREDENTIALS**
> → COGNITO IDENTITY POOL
>
> **MICROSECOND DYNAMODB**
> → DAX
>
> **GLOBAL ACTIVE-ACTIVE NOSQL**
> → GLOBAL TABLES
>
> **AUTO EXPIRE DYNAMODB ITEM**
> → TTL
>
> **DYNAMODB CHANGE**
> → STREAMS
>
> **LAMBDA COLD START**
> → PROVISIONED CONCURRENCY / SNAPSTART
>
> **LIMIT LAMBDA SCALE**
> → RESERVED CONCURRENCY
>
> **TOO MANY RDS CONNECTIONS**
> → RDS PROXY
>
> **CUSTOM API AUTH**
> → LAMBDA AUTHORIZER
>
> **WEB ATTACK**
> → WAF
>
> **LONG CONTAINER JOB**
> → FARGATE
>
> **GLOBAL STATIC DELIVERY**
> → CLOUDFRONT + S3

---

## Master Memory Trick

> [!tip] Serverless Master Memory Trick
> Imagine AWS gives you an entire company without making you manage the building.
>
> **API Gateway**
> → Reception desk
>
> **Cognito**
> → Identity desk
>
> **Lambda**
> → On-demand workers
>
> **DynamoDB**
> → Record system
>
> **S3**
> → File warehouse
>
> **SQS**
> → Waiting line
>
> **SNS**
> → Loudspeaker
>
> **EventBridge**
> → Dispatcher
>
> **Step Functions**
> → Project manager
>
> **CloudFront**
> → Global delivery network
>
> **Fargate**
> → Serverless container workforce

So remember:

> **CALL**
> → API Gateway
>
> **AUTHENTICATE**
> → Cognito
>
> **COMPUTE**
> → Lambda
>
> **STORE RECORD**
> → DynamoDB
>
> **STORE FILE**
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
> **DELIVER GLOBALLY**
> → CloudFront

And when the exam gives you a serverless architecture question, ask:

> **1. Does someone need an immediate response?**
>
> YES → Synchronous API pattern
>
> NO → Queue / event-driven pattern
>
> **2. Does work need to wait?**
>
> YES → SQS
>
> **3. Does one event need many consumers?**
>
> YES → SNS
>
> **4. Does the event need intelligent routing?**
>
> YES → EventBridge
>
> **5. Do multiple steps need coordination?**
>
> YES → Step Functions
>
> **6. Where should state live?**
>
> Outside the compute layer.

---

## Related Notes

- [[Lambda]]
- [[Lambda Synchronous Invocations]]
- [[Lambda Asynchronous Invocations]]
- [[Lambda Event Source Mapping]]
- [[Lambda Destinations]]
- [[Lambda Execution Roles]]
- [[Lambda Environment Variables]]
- [[Lambda Layers]]
- [[Lambda Concurrency]]
- [[Lambda SnapStart]]
- [[Lambda@Edge]]
- [[DynamoDB]]
- [[DynamoDB Advanced Features]]
- [[API Gateway]]
- [[API Gateway Security]]
- [[Step Functions]]
- [[Cognito]]
- [[Serverless Architectures]]
- [[S3]]
- [[SQS]]
- [[SNS]]
- [[20-SAA/10-Messaging/EventBridge]]
- [[CloudFront]]
- [[Fargate]]
- [[RDS Proxy]]
- [[06-Security/WAF]]
## What Problem Does It Solve?

[[Lambda]] is AWS's:

**Serverless compute service**

Lambda allows you to run code:

**Without provisioning or managing servers**

You upload your code, configure when it should run, and AWS manages the underlying infrastructure.

Architecture:

Event  
↓  
Lambda Function  
↓  
Code Executes  
↓  
Result

> [!tip] Memory Trick
> **Lambda = Run Code When Something Happens**
>
> Think:
>
> **EVENT → FUNCTION → ACTION**

---

## Core Lambda Idea

Traditional compute:

Application  
↓  
EC2 Instance  
↓  
You Manage Server

Lambda:

Event  
↓  
Lambda Function  
↓  
AWS Provides Compute

You do NOT manage:

- EC2 instances
- Operating systems
- Server patching
- Server capacity
- Infrastructure provisioning

### Killer Exam Clue

> **Run code without provisioning or managing servers**
>
> → **Lambda**

---

## Serverless Does Not Mean No Servers

Servers still exist.

The difference is:

**AWS manages them**

You focus on:

- Code
- Configuration
- Permissions
- Events
- Application logic

AWS manages:

- Compute infrastructure
- Operating system
- Capacity
- Scaling
- Availability

---

## Event-Driven Compute

Lambda is especially powerful for:

**Event-driven architectures**

Something happens:

↓  

Lambda runs:

↓  

Lambda performs an action

Examples:

S3 Object Uploaded  
↓  
Lambda  
↓  
Process Image

API Request  
↓  
Lambda  
↓  
Application Logic

EventBridge Event  
↓  
Lambda  
↓  
Automation

SQS Message  
↓  
Lambda  
↓  
Process Message

---

## Lambda Functions

A:

**Lambda Function**

contains:

**Code that performs a specific task**

Examples:

- Resize image
- Process order
- Validate request
- Transform data
- Send notification
- Process queue message

Lambda functions should generally be:

**Focused and stateless**

---

## Supported Runtimes

Lambda supports multiple programming languages through:

**Managed runtimes**

Common examples include:

- Python
- Node.js
- Java
- .NET
- Ruby

Lambda can also support:

**Custom runtimes**

and:

**Container images**

### SAA Takeaway

The exam usually cares more about:

**The serverless execution model**

than memorizing every runtime.

---

# Lambda Pricing

Lambda follows:

**Pay-per-use**

pricing.

You are generally charged based on:

- Number of requests
- Execution duration
- Memory allocated

You are NOT paying for:

**An idle EC2 server**

### Memory Trick

**No Execution = No Compute Running for Your Function**

---

## Lambda Execution Duration

A Lambda invocation has a:

**Maximum execution duration of 15 minutes**

This is a major SAA exam fact.

> [!warning] Killer Exam Fact
> **Lambda Maximum Execution Time = 15 Minutes**

If a workload needs:

**Longer than 15 minutes**

Lambda may not be appropriate.

Consider alternatives such as:

- [[ECS]]
- [[Fargate]]
- AWS Batch
- EC2

depending on the workload.

---

## Lambda Memory

You configure:

**Memory**

for the Lambda function.

AWS allocates CPU and other resources:

**In proportion to configured memory**

More memory can therefore provide:

**More compute performance**

### Exam Concept

Sometimes increasing Lambda memory can:

**Reduce execution time**

even though more memory is allocated.

---

## Lambda Temporary Storage

Lambda provides temporary local storage in:

`/tmp`

This storage is intended for:

- Temporary files
- Intermediate processing
- Caching
- Scratch data

Do NOT treat `/tmp` as:

**Durable application storage**

### Memory Trick

**/tmp = Temporary**

Persistent data should live in services such as:

- [[S3]]
- DynamoDB
- [[EFS]]
- RDS

depending on requirements.

---

# Lambda Scaling

Lambda automatically scales by:

**Running additional execution environments as requests increase**

Architecture:

1 Request  
↓  
Lambda Execution

100 Requests  
↓  
Multiple Concurrent Executions

You do NOT manually create:

**An Auto Scaling Group**

### Killer Exam Clue

> **Automatically scale event-driven code without managing servers**
>
> → **Lambda**

---

# Lambda Concurrency

Concurrency means:

**The number of Lambda executions running at the same time**

Example:

10 requests simultaneously  
↓  
Approximately 10 concurrent executions

Concurrency is important because it affects:

- Scaling
- Downstream systems
- Account/function limits
- Performance

---

## Reserved Concurrency

**Reserved Concurrency** reserves concurrency capacity for:

**A specific function**

and also limits how much concurrency that function can consume.

This provides:

- Guaranteed capacity from the account concurrency pool
- Maximum concurrency control

### Example

Function A:

Reserved Concurrency = 100

This means Function A can use up to:

**100 concurrent executions**

from its reserved allocation.

### Killer Exam Clue

> **Prevent one Lambda function from consuming all available concurrency**
>
> → **Reserved Concurrency**

---

## Why Limit Concurrency?

Suppose:

Lambda  
↓  
RDS

Traffic suddenly increases.

Lambda could scale rapidly and create:

**Too many database connections**

A concurrency limit can help protect:

**The downstream database**

### SAA Principle

> Lambda can scale faster than downstream systems can handle.

---

# Provisioned Concurrency

**Provisioned Concurrency**

keeps Lambda execution environments:

**Initialized and ready**

This reduces:

**Cold-start latency**

### Killer Exam Clue

> **Lambda requires predictable low latency and cold starts are unacceptable**
>
> → **Provisioned Concurrency**

---

## Reserved vs Provisioned Concurrency

This distinction is heavily testable.

### Reserved Concurrency

Think:

**CAPACITY CONTROL**

Used to:

- Reserve concurrency
- Limit maximum concurrency
- Protect other functions
- Protect downstream resources

### Provisioned Concurrency

Think:

**LATENCY**

Used to:

- Pre-initialize environments
- Reduce cold starts
- Provide predictable startup performance

### Memory Trick

**RESERVED = RESERVE / RESTRICT**

**PROVISIONED = PRE-WARM**

---

# Cold Starts

A:

**Cold Start**

can occur when Lambda must initialize:

**A new execution environment**

Before running your code, AWS may need to:

- Initialize runtime
- Load application code
- Initialize dependencies

This adds:

**Startup latency**

---

## Warm Execution

After an execution environment exists:

AWS may reuse it for:

**Later invocations**

This can avoid:

**Full initialization overhead**

Think:

First Invocation  
→ Cold

Later Reuse  
→ Warm

---

## Reducing Cold Start Impact

Possible strategies include:

- Provisioned Concurrency
- Efficient initialization
- Smaller deployment packages
- Appropriate runtime choices

For SAA:

> **Predictable low latency**
>
> → **Provisioned Concurrency**

---

# Lambda Execution Role

A Lambda function needs permissions to:

**Access AWS services**

These permissions come from:

**Lambda Execution Role**

Architecture:

Lambda Function  
↓  
Execution Role  
↓  
AWS Service

Examples:

Lambda  
→ S3

Lambda  
→ DynamoDB

Lambda  
→ SQS

Lambda  
→ Secrets Manager

### Killer Exam Clue

> **Lambda function needs permission to access another AWS service**
>
> → **Lambda Execution Role**

---

## Least Privilege

The execution role should contain:

**Only required permissions**

Example:

Image Processor Lambda  
↓  
Needs only:

`s3:GetObject`

and:

`s3:PutObject`

Do NOT give:

**AdministratorAccess**

just because the function needs S3.

### SAA Principle

> **Use least-privilege IAM roles for Lambda functions**

---

# Resource-Based Policies

Lambda also supports:

**Resource-based policies**

These control:

**Who or what can invoke the function**

This creates an important distinction.

### Execution Role

Controls:

**What Lambda can access**

### Resource-Based Policy

Controls:

**Who can invoke Lambda**

### Memory Trick

**ROLE = Lambda → AWS**

**RESOURCE POLICY = AWS → Lambda**

---

# Lambda + S3

One of the classic serverless architectures:

User  
↓  
Upload Image  
↓  
[[S3]]  
↓  
Lambda  
↓  
Process Image  
↓  
S3

Example use cases:

- Image resizing
- Thumbnail generation
- Metadata extraction
- File validation

### Killer Exam Pattern

> **Automatically process a file when it is uploaded to S3**
>
> → **S3 Event Notification + Lambda**

---

# Lambda + API Gateway

Classic serverless API:

Client  
↓  
[[API Gateway]]  
↓  
Lambda  
↓  
DynamoDB

This provides:

**Serverless application backend**

### Killer Exam Pattern

> **Build a serverless REST API**
>
> → **API Gateway + Lambda**

---

# Lambda + DynamoDB

Lambda integrates naturally with:

DynamoDB

Architecture:

API Gateway  
↓  
Lambda  
↓  
DynamoDB

This creates an architecture with:

**No servers to manage**

### Memory Trick

**API Gateway = Front Door**

**Lambda = Logic**

**DynamoDB = Data**

---

# DynamoDB Streams + Lambda

Changes to DynamoDB can be captured in:

**DynamoDB Streams**

Architecture:

DynamoDB  
↓  
Stream  
↓  
Lambda  
↓  
Process Change

Examples:

- React to new records
- Update another system
- Send notifications
- Perform downstream processing

### Killer Exam Clue

> **Run code automatically when DynamoDB records change**
>
> → **DynamoDB Streams + Lambda**

---

# Lambda + SQS

Lambda can process messages from:

[[SQS]]

Architecture:

Producer  
↓  
SQS  
↓  
Lambda  
↓  
Process Messages

SQS provides:

**Buffering and decoupling**

Lambda provides:

**Serverless processing**

### Killer Exam Pattern

> **Serverless asynchronous message processing**
>
> → **SQS + Lambda**

---

## Why Put SQS Before Lambda?

Without buffering:

Producer  
↓  
Lambda

With SQS:

Producer  
↓  
SQS  
↓  
Lambda

SQS helps:

- Absorb traffic spikes
- Decouple producers and consumers
- Provide retry durability
- Smooth processing demand

### Memory Trick

**SQS = Buffer**

**Lambda = Processor**

---

# Lambda + SNS

[[SNS]] can invoke Lambda subscribers.

Architecture:

Publisher  
↓  
SNS Topic  
↓  
├── Lambda A
├── Lambda B
└── Other Subscribers

Use this for:

**Fanout architectures**

---

# Lambda + EventBridge

[[20-SAA/10-Messaging/EventBridge]] can trigger Lambda based on:

- Events
- Rules
- Schedules

Architecture:

Event Source  
↓  
EventBridge  
↓  
Lambda

Examples:

- Scheduled automation
- AWS service events
- Application events

### Killer Exam Clue

> **Run Lambda on a schedule**
>
> → **EventBridge Scheduler / EventBridge Rule**

---

# Lambda + CloudWatch

Lambda integrates with:

[[07-Monitoring/CloudWatch]]

for:

- Metrics
- Logs
- Alarms
- Monitoring

Lambda function output can be sent to:

**CloudWatch Logs**

Useful metrics include:

- Invocations
- Errors
- Duration
- Throttles
- Concurrent executions

---

# Lambda Environment Variables

Lambda supports:

**Environment variables**

for configuration.

Examples:

- Table name
- Bucket name
- Environment
- Application setting

Do NOT store sensitive credentials in:

**Plaintext configuration**

when secure secret-management services are more appropriate.

---

# Lambda + Secrets Manager

For secrets such as:

- Database passwords
- API credentials
- Tokens

use:

[[Secrets Manager]]

Architecture:

Lambda  
↓  
Execution Role  
↓  
Secrets Manager  
↓  
Secret

This avoids:

**Hardcoding credentials**

inside application code.

---

# Lambda Layers

**Lambda Layers**

allow you to package:

**Shared code and dependencies**

separately from the function deployment package.

Examples:

- Shared libraries
- SDKs
- Runtime dependencies
- Common utilities

### Memory Trick

**Layer = Shared Dependency Package**

---

# Lambda Container Images

Lambda functions can also be packaged as:

**Container images**

This can simplify:

- Dependency packaging
- Existing container workflows
- Large application dependencies

Images can be stored in:

[[ECR]]

Architecture:

Container Image  
↓  
ECR  
↓  
Lambda

### Exam Trap

Lambda supporting container images does NOT turn it into:

**ECS**

The Lambda execution model still applies.

---

# Lambda Versions

Lambda supports:

**Versions**

A published version is:

**Immutable**

Example:

`$LATEST`

↓ Publish

Version 1

↓ Update

Version 2

This allows controlled:

**Application releases**

---

# Lambda Aliases

An:

**Alias**

is a pointer to:

**A Lambda version**

Examples:

`dev`

`test`

`prod`

Architecture:

`prod`  
↓  
Version 7

### Memory Trick

**VERSION = Immutable Code**

**ALIAS = Friendly Pointer**

---

## Weighted Aliases

Aliases can distribute traffic between:

**Lambda versions**

Example:

Version 7  
→ 90%

Version 8  
→ 10%

This supports:

- Canary deployments
- Gradual releases
- Testing new versions

### Killer Exam Clue

> **Gradually shift Lambda traffic to a new version**
>
> → **Weighted Alias**

---

# Lambda Function URLs

Lambda can expose:

**HTTPS endpoints**

using:

**Lambda Function URLs**

This provides a direct way to invoke:

**A Lambda function over HTTP**

For more advanced API features, consider:

[[API Gateway]]

---

# Function URL vs API Gateway

### Function URL

Think:

**Simple direct HTTPS endpoint**

### API Gateway

Think:

- Full API management
- Authentication options
- Throttling
- API stages
- Request transformations
- More advanced API functionality

### Exam Shortcut

**Simple Lambda HTTPS endpoint**
→ Function URL

**Full managed API**
→ API Gateway

---

# Lambda VPC Access

Lambda can connect to resources inside:

**A VPC**

Examples:

- Private RDS
- ElastiCache
- Internal services

Architecture:

Lambda  
↓  
VPC Networking  
↓  
Private Resource

### Killer Exam Clue

> **Lambda needs access to a private RDS database**
>
> → **Configure Lambda VPC access**

---

# Lambda + RDS

Architecture:

Lambda  
↓  
RDS

Potential issue:

Lambda can scale rapidly.

RDS may receive:

**Too many database connections**

A common solution is:

**RDS Proxy**

Architecture:

Lambda  
↓  
RDS Proxy  
↓  
RDS

---

# RDS Proxy

[[RDS Proxy]]:

**Pools and manages database connections**

This is especially useful with:

**Lambda**

because Lambda can create:

**Large bursts of concurrent connections**

### Killer Exam Clue

> **Lambda causes too many connections to an RDS database**
>
> → **RDS Proxy**

---

# Lambda Destinations

For asynchronous Lambda invocations, destinations can route:

**Invocation results**

to other services.

You can route:

- Successful results
- Failed results

to supported destinations.

### SAA Concept

Think:

**Post-processing after asynchronous Lambda execution**

---

# Dead-Letter Queues

For certain asynchronous invocation patterns, failed events can be sent to:

**A Dead-Letter Queue**

This helps preserve:

**Failed events for later investigation**

### Memory Trick

**DLQ = Failed Event Parking Lot**

---

# Synchronous Invocation

With:

**Synchronous invocation**

the caller waits for:

**The Lambda response**

Example:

Client  
↓  
API Gateway  
↓  
Lambda  
↓  
Response

Think:

**Request / Response**

---

# Asynchronous Invocation

With:

**Asynchronous invocation**

the caller sends the event and:

**Does not wait for function completion**

Example event sources can include:

- S3
- SNS
- EventBridge

Lambda manages:

**Asynchronous event processing and retries**

### Memory Trick

**SYNC = WAIT**

**ASYNC = SEND AND MOVE ON**

---

# Event Source Mapping

Some services are processed by Lambda through:

**Event Source Mappings**

Important examples:

- SQS
- DynamoDB Streams
- Kinesis

Conceptually:

Lambda polls source  
↓  
Receives records  
↓  
Invokes function

### Killer Exam Distinction

S3 / SNS:

**Push events toward Lambda**

SQS / Streams:

**Lambda polls through event source mapping**

---

# Lambda Retry Behavior

Retry behavior depends on:

**Invocation type and event source**

Do NOT assume:

**Every Lambda failure retries the same way**

For the exam, first identify:

- Synchronous
- Asynchronous
- Stream
- Queue

before determining:

**Failure behavior**

---

# Lambda Idempotency

Because distributed systems can sometimes deliver or process events:

**More than once**

Lambda functions should often be designed to be:

**Idempotent**

Meaning:

Running the same operation multiple times does not create:

**Incorrect duplicate effects**

Example:

Order ID 123 processed twice  
↓  
Application detects same ID  
↓  
Only one payment created

### SAA Principle

> **Design event-driven functions to tolerate duplicate events**

---

# Lambda Stateless Design

Lambda functions should generally be:

**Stateless**

Persistent state belongs in:

- DynamoDB
- S3
- RDS
- EFS
- ElastiCache

depending on requirements.

### Memory Trick

**Lambda = Compute**

**External Service = State**

---

# Lambda + EFS

Lambda can integrate with:

[[EFS]]

when functions need:

**Persistent shared file storage**

Architecture:

Lambda  
↓  
EFS

Useful when:

- Shared files are required
- Large dependencies/files are needed
- Persistent filesystem semantics are needed

---

# Lambda vs EC2

### Lambda

Think:

- Serverless
- Event-driven
- Automatic scaling
- Maximum 15-minute execution
- Pay per execution

### [[EC2]]

Think:

- Virtual machine
- Long-running workloads
- Full OS control
- No 15-minute execution limit
- Server management

---

# Lambda vs Fargate

### Lambda

Think:

- Functions
- Event-driven execution
- 15-minute maximum
- Fine-grained serverless execution

### [[Fargate]]

Think:

- Containers
- Longer-running workloads
- More runtime flexibility
- Serverless container compute

### Killer Shortcut

**Short event-driven function**
→ Lambda

**Long-running container**
→ Fargate

---

# Lambda vs App Runner

### Lambda

Think:

**Event-driven functions**

### [[App Runner]]

Think:

**Continuously available web applications/APIs**

---

# Lambda vs Step Functions

### Lambda

Performs:

**Individual compute tasks**

### Step Functions

Coordinates:

**Multiple workflow steps**

Example:

Step Functions  
↓  
Lambda A  
↓  
Lambda B  
↓  
Lambda C

### Memory Trick

**Lambda = Worker**

**Step Functions = Workflow Manager**

---

# Architecture Thinking

## Scenario 1 — Image Processing

Image uploaded to S3.

Need automatic thumbnail creation.

Choose:

S3  
↓  
Lambda

---

## Scenario 2 — Serverless API

Need:

- REST API
- No servers
- Serverless database

Choose:

API Gateway  
↓  
Lambda  
↓  
DynamoDB

---

## Scenario 3 — Queue Processing

Messages arrive unpredictably.

Need serverless processing.

Choose:

SQS  
↓  
Lambda

---

## Scenario 4 — Database Connections

Thousands of Lambda executions connect to:

RDS

Database becomes overwhelmed.

Choose:

**RDS Proxy**

---

## Scenario 5 — Low-Latency Function

Application requires:

**Predictable startup latency**

Choose:

**Provisioned Concurrency**

---

## Scenario 6 — Protect Database

Lambda should never exceed:

**100 simultaneous database operations**

Choose:

**Reserved Concurrency**

---

## Scenario 7 — Long Job

Job requires:

**45 minutes**

Do NOT choose Lambda.

Think:

- Fargate
- ECS
- AWS Batch
- EC2

depending on requirements.

---

## Scenario 8 — DynamoDB Changes

Need code to execute when:

**Records change**

Choose:

DynamoDB Streams  
↓  
Lambda

---

## Scenario 9 — Scheduled Function

Need code to run:

**Every night**

Choose:

EventBridge  
↓  
Lambda

---

## Scenario 10 — Shared Files

Multiple Lambda executions require:

**Persistent filesystem access**

Think:

[[EFS]]

---

## Scenario 11 — Canary Deployment

Need:

**10% of traffic to new Lambda version**

Choose:

**Weighted Alias**

---

## Scenario 12 — Private Database

Lambda must connect to:

**Private RDS**

Choose:

**Lambda VPC access**

---

# Scenario Recognition

Immediately think:

**Lambda**

when you see:

- Serverless function
- Event-driven code
- No server management
- S3 processing
- API Gateway backend
- SQS processing
- DynamoDB Streams
- EventBridge automation
- Short-lived compute

---

# Exam Traps

## Trap 1 — Lambda Can Run Indefinitely

❌

Maximum execution:

**15 minutes**

---

## Trap 2 — Lambda Requires EC2 Provisioning

❌

Lambda is:

**Serverless**

---

## Trap 3 — Reserved Concurrency Eliminates Cold Starts

❌

Think:

**Provisioned Concurrency**

---

## Trap 4 — Provisioned Concurrency Is Mainly for Limiting Scale

❌

Its primary exam association is:

**Reducing cold starts**

---

## Trap 5 — Lambda Local Storage Is Durable Application Storage

❌

`/tmp` is:

**Temporary**

---

## Trap 6 — Lambda Should Store Persistent State Inside the Function

❌

Use:

**External persistent services**

---

## Trap 7 — Lambda Scaling Cannot Hurt RDS

❌

Rapid Lambda scaling can create:

**Too many database connections**

Think:

**RDS Proxy**

---

## Trap 8 — Lambda Execution Role Controls Who Invokes Lambda

❌

Execution Role:

**What Lambda can access**

Resource-Based Policy:

**Who can invoke Lambda**

---

## Trap 9 — Every Lambda Invocation Is Asynchronous

❌

Lambda supports:

- Synchronous
- Asynchronous
- Event source mappings

---

## Trap 10 — SQS Pushes Messages Directly into Lambda

For exam architecture thinking:

Lambda uses:

**Event source mapping to poll SQS**

---

## Trap 11 — Lambda Is Always Better Than Fargate

❌

Long-running container workloads may fit:

**Fargate**

better.

---

# Quick Cheat Sheet

| Exam Clue | Answer |
|---|---|
| Serverless Code | Lambda |
| Event-Driven Compute | Lambda |
| Max Runtime | 15 Minutes |
| S3 File Processing | S3 + Lambda |
| Serverless API | API Gateway + Lambda |
| Queue Processing | SQS + Lambda |
| DynamoDB Changes | Streams + Lambda |
| Scheduled Code | EventBridge + Lambda |
| Lambda AWS Permissions | Execution Role |
| Reduce Cold Starts | Provisioned Concurrency |
| Limit / Reserve Concurrency | Reserved Concurrency |
| Too Many RDS Connections | RDS Proxy |
| Persistent Shared Files | EFS |
| Direct Simple HTTPS Endpoint | Function URL |
| Full API Management | API Gateway |
| Canary Deployment | Weighted Alias |
| Container Image for Lambda | ECR |
| Shared Dependencies | Lambda Layers |

---

# Concurrency Cheat Sheet

| Requirement | Feature |
|---|---|
| Reduce Cold Starts | Provisioned Concurrency |
| Pre-Initialize Environments | Provisioned Concurrency |
| Reserve Function Capacity | Reserved Concurrency |
| Limit Maximum Concurrency | Reserved Concurrency |
| Protect Downstream System | Reserved Concurrency |

---

# Invocation Cheat Sheet

| Pattern | Think |
|---|---|
| API Gateway → Lambda | Synchronous |
| S3 → Lambda | Asynchronous |
| SNS → Lambda | Asynchronous |
| EventBridge → Lambda | Asynchronous |
| SQS → Lambda | Event Source Mapping |
| DynamoDB Streams → Lambda | Event Source Mapping |
| Kinesis → Lambda | Event Source Mapping |

---

# Final Exam Rapid-Fire

> **SERVERLESS COMPUTE**
> → LAMBDA
>
> **MAX EXECUTION**
> → 15 MINUTES
>
> **S3 EVENT PROCESSING**
> → LAMBDA
>
> **SERVERLESS API**
> → API GATEWAY + LAMBDA
>
> **QUEUE PROCESSOR**
> → SQS + LAMBDA
>
> **DATABASE CHANGE EVENT**
> → DYNAMODB STREAMS + LAMBDA
>
> **SCHEDULED FUNCTION**
> → EVENTBRIDGE + LAMBDA
>
> **REDUCE COLD STARTS**
> → PROVISIONED CONCURRENCY
>
> **LIMIT CONCURRENCY**
> → RESERVED CONCURRENCY
>
> **TOO MANY RDS CONNECTIONS**
> → RDS PROXY
>
> **LAMBDA → AWS SERVICE**
> → EXECUTION ROLE
>
> **WHO CAN INVOKE LAMBDA**
> → RESOURCE-BASED POLICY
>
> **PERSISTENT SHARED FILES**
> → EFS
>
> **CANARY DEPLOYMENT**
> → WEIGHTED ALIAS
>
> **LONG-RUNNING CONTAINER**
> → FARGATE

---

## Master Memory Trick

> [!tip] Lambda Master Memory Trick
> Think of Lambda as:
>
> **An on-call worker**
>
> The worker does not sit around waiting on a server you manage.
>
> Something happens:
>
> **EVENT**
>
> The worker appears:
>
> **LAMBDA**
>
> Does the job:
>
> **FUNCTION**
>
> Then disappears.

Remember:

> **EVENT**
> → LAMBDA
>
> **API**
> → API GATEWAY + LAMBDA
>
> **FILE**
> → S3 + LAMBDA
>
> **QUEUE**
> → SQS + LAMBDA
>
> **DATABASE CHANGE**
> → DYNAMODB STREAMS + LAMBDA
>
> **CLOCK**
> → EVENTBRIDGE + LAMBDA
>
> **COLD START**
> → PROVISIONED CONCURRENCY
>
> **CONTROL SCALE**
> → RESERVED CONCURRENCY
>
> **RDS CONNECTION EXPLOSION**
> → RDS PROXY
>
> **MORE THAN 15 MINUTES**
> → NOT LAMBDA

And the killer SAA question:

> **"Can this workload be triggered by an event, finish within 15 minutes, and run without server management?"**
>
> If yes:
>
> **Lambda should immediately be on your shortlist.**

---

## Related Notes

- [[API Gateway]]
- [[04-Databases/DynamoDB]]
- [[S3]]
- [[SQS]]
- [[SNS]]
- [[20-SAA/10-Messaging/EventBridge]]
- [[07-Monitoring/CloudWatch]]
- [[EFS]]
- [[RDS]]
- [[RDS Proxy]]
- [[IAM]]
- [[ECR]]
- [[Fargate]]
- [[App Runner]]
- [[Step Functions]]
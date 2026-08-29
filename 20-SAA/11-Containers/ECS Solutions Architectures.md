## Why This Note Matters

AWS SAA questions often test ECS through:

**Architecture scenarios**

rather than simple definitions.

The exam may describe:

- A web application
- Background workers
- Scheduled tasks
- Event-driven containers
- SQS processing
- Load balancing
- Auto Scaling
- Shared storage
- IAM permissions

and ask:

> **"Which ECS architecture best satisfies the requirements?"**

> [!tip] Master ECS Architecture Rule
> Think in layers:
>
> **TRAFFIC**
> → ALB / NLB
>
> **CONTAINERS**
> → ECS Service / Tasks
>
> **COMPUTE**
> → EC2 or Fargate
>
> **SCALING**
> → ECS Service Auto Scaling
>
> **STATE**
> → External storage / database
>
> **PERMISSIONS**
> → Task Role

---

## Architecture 1 — ECS Web Application

A classic ECS web architecture:

Users  
↓  
[[Application Load Balancer]]  
↓  
ECS Service  
↓  
├── Task A
├── Task B
└── Task C

The ECS Service maintains:

**Multiple healthy tasks**

The ALB distributes:

**HTTP / HTTPS traffic**

across those tasks.

---

## Why Use an ALB?

ALB is a strong fit for ECS web applications because it supports:

- HTTP
- HTTPS
- Host-based routing
- Path-based routing
- Target groups
- Dynamic port mapping

### Killer Exam Pattern

> **Containerized web application with multiple ECS tasks behind HTTP/HTTPS**
>
> → **ALB + ECS Service**

---

## High Availability

For production workloads:

Run ECS tasks across:

**Multiple Availability Zones**

Architecture:

ALB  
↓  
├── AZ-A → ECS Tasks
└── AZ-B → ECS Tasks

This protects against:

**Single-AZ failure**

### Exam Rule

> **Highly available ECS service**
>
> → Multiple tasks across multiple AZs behind a load balancer

---

## Architecture 2 — ECS + Fargate Web Application

If the company wants:

**Minimum operational overhead**

Architecture:

Users  
↓  
ALB  
↓  
ECS Service  
↓  
Fargate Tasks

AWS manages:

**Underlying servers**

The customer manages:

- Task definitions
- Services
- Application configuration
- Scaling policies

### Killer Exam Clue

> **Highly available containerized web application with no EC2 management**
>
> → **ECS + Fargate + ALB**

---

## Architecture 3 — ECS on EC2

If the company requires:

- Specific EC2 instance types
- Host-level control
- Custom AMIs
- Specialized hardware
- Existing EC2 capacity

Architecture:

ALB  
↓  
ECS Service  
↓  
Tasks  
↓  
EC2 Auto Scaling Group

### Killer Exam Clue

> **Container orchestration with control over underlying hosts**
>
> → **ECS on EC2**

---

## Architecture 4 — SQS Worker Pattern

One of the strongest ECS architectures for the SAA exam is:

**SQS + ECS Workers**

Architecture:

Producer  
↓  
[[SQS]]  
↓  
ECS Worker Service  
↓  
Tasks Process Messages

This provides:

- Decoupling
- Buffering
- Backpressure protection
- Horizontal scaling

---

## Why SQS Works Well with ECS

Suppose incoming work arrives faster than containers can process it.

Without SQS:

Producer  
↓  
ECS Workers

Traffic spike  
↓  
Workers overwhelmed

With SQS:

Producer  
↓  
SQS Queue  
↓  
ECS Workers

Traffic spike  
↓  
Messages accumulate safely  
↓  
Workers process at sustainable rate

### Memory Trick

**SQS = Buffer**

**ECS = Workers**

---

## Scale ECS Workers from Queue Depth

A common architecture:

SQS Queue  
↓  
CloudWatch Metric  
↓  
ECS Service Auto Scaling  
↓  
More Worker Tasks

Useful metric concept:

**Queue depth**

or:

**Messages waiting**

### Killer Exam Pattern

> **Scale ECS workers based on SQS backlog**
>
> → **ECS Service Auto Scaling using queue-related CloudWatch metrics**

---

## Worker Architecture Example

Normal workload:

100 Messages  
↓  
2 ECS Tasks

Traffic spike:

10,000 Messages  
↓  
Queue Depth Rises  
↓  
Scale to 20 Tasks

Backlog clears:

Queue Depth Falls  
↓  
Scale back to 2 Tasks

This provides:

**Elastic asynchronous processing**

---

## SQS Visibility Timeout

When ECS workers consume SQS:

Remember:

**Visibility Timeout must be long enough for task processing**

Example:

Processing time:

5 minutes

Visibility timeout:

30 seconds

Problem:

Message becomes visible again while still processing.

Potential result:

**Duplicate processing**

### Exam Fix

Increase:

**Visibility Timeout**

---

## Dead-Letter Queue

If an ECS worker repeatedly fails to process a message:

Main Queue  
↓  
Retries  
↓  
[[Dead-Letter Queue]]

This prevents:

**Poison messages**

from endlessly cycling.

### Architecture Pattern

SQS  
↓  
ECS Workers  
↓  
Repeated Failure  
↓  
DLQ  
↓  
Investigation

---

## Architecture 5 — EventBridge + ECS

[[20-SAA/10-Messaging/EventBridge]] can trigger:

**ECS tasks**

Architecture:

Event Source  
↓  
EventBridge  
↓  
Rule  
↓  
ECS Task

Use this for:

**Event-driven container workloads**

---

## Event-Driven ECS Example

An application emits:

`ReportRequested`

EventBridge matches:

**ReportRequested**

and starts:

**An ECS task**

The task:

- Generates report
- Stores output
- Stops

### Killer Exam Clue

> **Run a container only when a specific event occurs**
>
> → **EventBridge + ECS Task**

---

## ECS Service vs One-Off Task

This distinction matters.

### ECS Service

Use for:

**Long-running applications**

Examples:

- Web servers
- APIs
- Worker pools

The service maintains:

**Desired task count**

---

### One-Off ECS Task

Use for:

**Finite jobs**

Examples:

- Batch job
- Report generation
- Maintenance
- Data processing

Task runs:

**Until work finishes**

then stops.

### Memory Trick

**SERVICE = KEEP RUNNING**

**TASK = RUN AND FINISH**

---

## Architecture 6 — Scheduled ECS Tasks

Scheduled workloads can use:

[[20-SAA/10-Messaging/EventBridge]]

Architecture:

Schedule  
↓  
EventBridge  
↓  
ECS Task

Examples:

- Nightly report
- Daily data cleanup
- Hourly batch processing
- Weekly maintenance

### Killer Exam Pattern

> **Run a containerized job every night**
>
> → **EventBridge Schedule + ECS Task**

---

## Scheduled Task vs Long-Running Service

If requirement says:

**Always available**

→ ECS Service

If requirement says:

**Run every night**

→ Scheduled ECS Task

---

## Architecture 7 — ECS + EFS

Containers should generally be treated as:

**Ephemeral**

If multiple tasks need:

**Shared persistent files**

use:

[[EFS]]

Architecture:

ECS Task A  
↓  

ECS Task B  
↓  

ECS Task C  
↓  

EFS

### Killer Exam Clue

> **Multiple ECS tasks need shared persistent file storage**
>
> → **ECS + EFS**

---

## Why Local Container Storage Is Not Enough

If a task is replaced:

Local container data may disappear.

For scalable systems:

State should live outside:

**Individual tasks**

Potential external state:

- [[EFS]]
- [[S3]]
- RDS
- DynamoDB
- ElastiCache

### SAA Principle

> **Stateless containers scale better**

---

## Architecture 8 — ECS + RDS

A common three-tier architecture:

Users  
↓  
ALB  
↓  
ECS Service  
↓  
[[RDS]]

ECS tasks run:

**Application logic**

RDS stores:

**Persistent relational data**

This keeps tasks:

**Stateless**

---

## ECS Task Role + Database Access

If application containers need AWS service permissions:

Use:

**Task Role**

Example:

ECS Task  
↓  
Task Role  
↓  
Secrets Manager

or:

ECS Task  
↓  
Task Role  
↓  
DynamoDB

### Killer Exam Clue

> **Container application needs AWS API permissions**
>
> → **Task Role**

---

## Architecture 9 — ECS + Secrets Manager

Do NOT store database passwords in:

- Docker image
- Source code
- Environment file committed to Git

Better:

ECS Task  
↓  
[[Secrets Manager]]  
↓  
Database Credentials

Task Role allows:

**Retrieve secret**

### Exam Pattern

> **Securely provide database credentials to ECS tasks**
>
> → **Secrets Manager + ECS Task Role**

---

## Architecture 10 — ECS + ECR

Deployment flow:

Developer  
↓  
Build Image  
↓  
[[02-Compute/ECR]]  
↓  
ECS  
↓  
Tasks

ECR stores:

**Container images**

ECS runs:

**Containers**

### Memory Trick

**ECR = STORE**

**ECS = RUN**

---

## Private ECR Images

If ECS needs permission to pull:

**Private ECR images**

think:

**Task Execution Role**

### Exam Shortcut

Application needs S3?

→ Task Role

ECS needs ECR image?

→ Task Execution Role

---

## Architecture 11 — ECS + ALB Path Routing

A microservices architecture can use:

**Path-based routing**

Architecture:

Users  
↓  
ALB  
↓

`/orders`  
→ Orders ECS Service

`/payments`  
→ Payments ECS Service

`/users`  
→ Users ECS Service

This reduces the need for:

**Separate load balancers for every service**

---

## Host-Based Routing

ALB can also route by:

**Hostname**

Example:

`orders.example.com`  
→ Orders Service

`payments.example.com`  
→ Payments Service

`admin.example.com`  
→ Admin Service

### Killer Exam Pattern

> **Multiple ECS microservices behind one load balancer**
>
> → **ALB host/path-based routing**

---

## Architecture 12 — ECS + Auto Scaling

Typical scalable web architecture:

Users  
↓  
ALB  
↓  
ECS Service  
↓  
Auto Scaling Tasks

Scaling metric examples:

- CPU
- Memory
- ALB requests per target

Architecture:

Demand ↑  
↓  
Metric ↑  
↓  
ECS Service Auto Scaling  
↓  
More Tasks

---

## ECS on EC2 Double Scaling

For ECS on EC2:

Traffic ↑  
↓  
More Tasks Needed  
↓  
Service Auto Scaling  
↓  
Not Enough EC2 Capacity  
↓  
Capacity Provider / ASG  
↓  
More EC2 Instances

Remember:

> **Tasks and servers are separate scaling layers**

---

## Architecture 13 — ECS + Fargate Spot

For fault-tolerant workloads:

ECS  
↓  
Capacity Provider Strategy  
↓  
Fargate + Fargate Spot

Use Fargate Spot for:

- Batch workers
- Queue processors
- Interruptible jobs

Avoid it for:

**Critical tasks that cannot tolerate interruption**

---

## Base + Weight Strategy

Capacity provider strategy can distribute tasks.

Example:

Base:

2 Tasks on Fargate

Additional Tasks:

1 part Fargate  
3 parts Fargate Spot

This can provide:

**Baseline reliability + lower-cost burst capacity**

---

## Architecture 14 — ECS Blue/Green Deployments

Containerized applications may need:

**Safer deployments**

A blue/green pattern uses:

Blue Environment  
→ Current Version

Green Environment  
→ New Version

Traffic shifts after:

**Validation**

AWS deployment tooling can integrate with ECS for:

**Controlled deployment strategies**

### Exam Concept

> **Reduce deployment risk by keeping old and new task sets separately available**

Think:

**Blue/Green deployment**

---

## Architecture 15 — Microservices

ECS is well suited to:

**Microservices**

Architecture:

ALB  
↓  
├── Service A
├── Service B
├── Service C
└── Service D

Each service can have:

- Separate task definition
- Separate scaling policy
- Separate IAM role
- Separate deployment lifecycle

This provides:

**Independent scaling and deployment**

---

## Service-to-Service Permissions

Different ECS services should use:

**Different Task Roles**

Example:

Orders Service  
→ DynamoDB Orders Table

Payments Service  
→ Payment Resources

Reporting Service  
→ S3 Reports Bucket

This supports:

**Least privilege**

---

## Architecture 16 — ECS + CloudWatch

ECS integrates with:

[[07-Monitoring/CloudWatch]]

for:

- Metrics
- Logs
- Alarms
- Auto Scaling

Architecture:

ECS Tasks  
↓  
CloudWatch Logs

ECS Metrics  
↓  
CloudWatch  
↓  
Alarm / Scaling

### Exam Pattern

> **Centralize ECS container logs**
>
> → **CloudWatch Logs**

---

## Architecture 17 — ECS Queue-Based Batch Processing

Suppose users upload jobs.

Architecture:

Users  
↓  
Application  
↓  
SQS  
↓  
ECS Workers  
↓  
S3 / Database

Each task:

1. Polls SQS
2. Receives work
3. Processes data
4. Stores output
5. Deletes message

This is a classic:

**Asynchronous batch-processing architecture**

---

## When Fargate Is Strong for Queue Workers

Fargate works well when:

- Workload is bursty
- You don't want EC2 management
- Workers can scale horizontally
- Containers are stateless

Architecture:

SQS  
↓  
ECS Service on Fargate  
↓  
Worker Tasks

---

## When EC2 May Be Better for Workers

ECS on EC2 may be better when:

- Jobs run continuously
- Instance utilization is high
- Specialized EC2 hardware is required
- Host-level control matters

The exam usually gives:

**Operational or technical clues**

to decide.

---

## Architecture Thinking

### Scenario 1 — Public Web App

A company needs:

- Containerized HTTP application
- High availability
- Automatic scaling
- No server management

Choose:

ALB  
↓  
ECS Service  
↓  
Fargate Tasks  
↓  
Multi-AZ

---

### Scenario 2 — Queue Workers

Messages arrive unpredictably.

Workers should process them asynchronously.

Choose:

SQS  
↓  
ECS Service  
↓  
Worker Tasks

Scale based on:

**Queue depth**

---

### Scenario 3 — Nightly Container Job

A container should run:

**Every night at midnight**

Choose:

EventBridge  
↓  
Scheduled ECS Task

Do NOT maintain:

**A 24/7 ECS Service**

just for a once-daily job.

---

### Scenario 4 — Shared Files

Multiple ECS tasks need:

**The same files**

Choose:

[[EFS]]

---

### Scenario 5 — Microservices

Three containerized APIs require different URLs:

- `/orders`
- `/payments`
- `/users`

Choose:

ALB  
+  
Path-Based Routing  
+  
Separate ECS Services

---

### Scenario 6 — Container Needs DynamoDB

A container application requires:

`dynamodb:GetItem`

Choose:

**ECS Task Role**

---

### Scenario 7 — Pull Private Image

ECS must pull a private image from:

[[02-Compute/ECR]]

Choose:

**Task Execution Role**

---

### Scenario 8 — Long-Running API

Application must:

**Always remain available**

Choose:

**ECS Service**

rather than a standalone task.

---

### Scenario 9 — One-Time Report

An event requests report generation.

Container runs, creates report, then exits.

Choose:

**One-Off ECS Task**

possibly triggered by:

[[20-SAA/10-Messaging/EventBridge]]

---

### Scenario 10 — No EC2 Capacity

ECS Service wants more tasks but tasks remain:

**PENDING**

Cluster EC2 instances are full.

Choose:

**Capacity Provider / Cluster Auto Scaling**

---

### Scenario 11 — Fault-Tolerant Workers

Background processing can tolerate interruption.

Need lower cost.

Choose:

**Fargate Spot**

---

## Scenario Recognition

Immediately think:

**ALB + ECS**

when you see:

- Containerized web application
- HTTP/HTTPS
- Multiple tasks
- Microservices
- Path routing

Immediately think:

**SQS + ECS**

when you see:

- Background workers
- Queue
- Async jobs
- Backpressure
- Queue-depth scaling

Immediately think:

**EventBridge + ECS**

when you see:

- Scheduled container job
- Event-triggered container
- One-off task

Immediately think:

**EFS + ECS**

when you see:

- Shared persistent files
- Multiple tasks
- File system access

---

## Exam Traps

### Trap 1 — Every Container Workload Should Be an ECS Service

False.

Use a service for:

**Long-running workloads**

Use standalone tasks for:

**Finite jobs**

---

### Trap 2 — ECS Workers Should Receive Requests Directly During Traffic Spikes

Not always.

If work can be asynchronous:

Use:

**SQS as a buffer**

---

### Trap 3 — Shared Files Should Live Inside One Container

Bad architecture for scalable tasks.

Use:

**External persistent storage**

such as:

[[EFS]]

---

### Trap 4 — ALB and ECS Auto Scaling Are the Same Thing

False.

ALB:

**Distributes traffic**

Auto Scaling:

**Changes task capacity**

---

### Trap 5 — Task Role and Execution Role Are Interchangeable

False.

Task Role:

**App permissions**

Execution Role:

**ECS startup permissions**

---

### Trap 6 — Fargate Spot Is Best for Critical Stateful Workloads

False.

It is designed for:

**Interruptible fault-tolerant workloads**

---

### Trap 7 — Scaling Tasks Automatically Gives ECS on EC2 More Hosts

False.

Underlying EC2 capacity may need:

**Cluster scaling**

---

### Trap 8 — Scheduled Jobs Need a Permanently Running Service

False.

Use:

**EventBridge + standalone ECS Task**

---

### Trap 9 — Microservices Need Separate ALBs

Not necessarily.

One ALB can use:

- Host-based routing
- Path-based routing

to multiple ECS services.

---

### Trap 10 — Local Container State Is Safe for Replacement Tasks

False.

Tasks are designed to be:

**Replaceable**

Persist important state externally.

---

## Architecture Decision Table

| Requirement | Best Architecture |
|---|---|
| Public HTTP Containers | ALB + ECS Service |
| No Server Management | ECS + Fargate |
| Control Hosts | ECS on EC2 |
| Async Worker Processing | SQS + ECS |
| Scale Queue Workers | SQS Metric + ECS Auto Scaling |
| Event-Triggered Container | EventBridge + ECS Task |
| Scheduled Container | EventBridge + ECS Task |
| Shared Persistent Files | ECS + EFS |
| Store Images | ECR |
| App AWS Permissions | Task Role |
| Startup / Image Pull Permissions | Task Execution Role |
| Microservice Routing | ALB Host/Path Routing |
| Fault-Tolerant Cheap Tasks | Fargate Spot |

---

## Long-Running vs One-Off

| Requirement | ECS Service | Standalone ECS Task |
|---|---:|---:|
| Web Server | ✅ | ❌ |
| API | ✅ | ❌ |
| Continuous Worker Pool | ✅ | ❌ |
| Nightly Job | ❌ | ✅ |
| Report Generation | ❌ | ✅ |
| One-Time Processing | ❌ | ✅ |
| Desired Count Maintained | ✅ | ❌ |

---

## Final Exam Rapid-Fire

> **WEB CONTAINERS**
> → ALB + ECS SERVICE
>
> **NO SERVER MANAGEMENT**
> → FARGATE
>
> **ASYNC CONTAINER WORKERS**
> → SQS + ECS
>
> **SCALE WORKERS BY BACKLOG**
> → SQS METRIC + ECS AUTO SCALING
>
> **EVENT-DRIVEN CONTAINER**
> → EVENTBRIDGE + ECS TASK
>
> **SCHEDULED CONTAINER**
> → EVENTBRIDGE + ECS TASK
>
> **LONG-RUNNING CONTAINERS**
> → ECS SERVICE
>
> **ONE-TIME CONTAINER JOB**
> → ECS TASK
>
> **SHARED FILES**
> → EFS
>
> **STORE CONTAINER IMAGES**
> → ECR
>
> **APP NEEDS AWS ACCESS**
> → TASK ROLE
>
> **ECS NEEDS TO PULL IMAGE**
> → EXECUTION ROLE
>
> **MICROSERVICE ROUTING**
> → ALB PATH / HOST ROUTING

---

## Master Memory Trick

> [!tip] ECS Architecture Master Memory Trick
> Think of ECS as a workforce.
>
> **ALB**
> → Sends customers to workers
>
> **ECS Service**
> → Keeps enough workers on duty
>
> **SQS**
> → Holds the job tickets
>
> **Auto Scaling**
> → Adds or removes workers
>
> **EventBridge**
> → Calls a worker when a special event or schedule occurs
>
> **EFS**
> → Shared filing cabinet
>
> **ECR**
> → Storage room containing worker blueprints
>
> **Task Role**
> → What workers are allowed to access
>
> **Execution Role**
> → What ECS needs to get workers started

Then remember:

> **ALWAYS RUNNING**
> → ECS SERVICE
>
> **RUN AND FINISH**
> → ECS TASK
>
> **WAITING WORK**
> → SQS
>
> **EVENT / CLOCK**
> → EventBridge
>
> **SHARED STATE**
> → External Storage
>
> **SCALE**
> → Add Tasks
>
> **STATELESS**
> → Easier to Scale

The killer SAA architecture question:

> **"Does this container need to stay running, wait for queued work, or run only when triggered?"**

That usually tells you:

**Which ECS architecture wins.**

---

## Related Notes

- [[ECS]]
- [[ECS Auto Scaling]]
- [[02-Compute/Fargate]]
- [[02-Compute/ECR]]
- [[Application Load Balancer]]
- [[SQS]]
- [[20-SAA/10-Messaging/EventBridge]]
- [[EFS]]
- [[S3]]
- [[RDS]]
- [[04-Databases/DynamoDB]]
- [[Secrets Manager]]
- [[07-Monitoring/CloudWatch]]
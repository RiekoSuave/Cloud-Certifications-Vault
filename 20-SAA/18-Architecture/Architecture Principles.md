## Core Concept

AWS architecture questions are rarely asking:

**"Which service do you remember?"**

They are usually asking:

**"Which design best satisfies the business and technical requirements?"**

The correct answer often depends on balancing:

- Availability
- Scalability
- Performance
- Security
- Cost
- Operational effort
- Reliability
- Disaster recovery

> [!tip] Memory Trick
> **SAA Architecture = Requirements First, Services Second**

---

# Start With the Requirement

Before choosing any AWS service, identify:

**What the question is actually optimizing for**

Common priorities include:

- Lowest cost
- Highest availability
- Lowest operational overhead
- Fastest performance
- Global users
- Security
- Disaster recovery
- Scalability

### Killer Exam Principle

> **Do not choose the most powerful architecture**
>
> Choose:
>
> **The simplest architecture that satisfies the stated requirements**

---

# Requirement Keywords

Certain words dramatically change:

**The correct architecture**

Examples:

**Most cost-effective**
→ Reduce unnecessary infrastructure

**Least operational overhead**
→ Prefer managed/serverless services

**Highly available**
→ Multi-AZ

**Disaster recovery**
→ RPO + RTO

**Global users**
→ Edge / Multi-Region architectures

**Millions of requests**
→ Scalable managed services

**Decouple**
→ Messaging

### Memory Trick

**Read the adjective before choosing the service**

---

# Design for Failure

One of the most important AWS architecture principles is:

**Assume components will eventually fail**

Instead of trying to prevent:

**Every possible failure**

design systems that:

**Continue operating or recover automatically**

### Examples

Single EC2 instance  
❌

Auto Scaling Group across multiple AZs  
✅

Single database server  
❌

Managed Multi-AZ database  
✅

### Killer Exam Clue

> **Avoid single points of failure**

---

# Single Points of Failure

A:

**Single Point of Failure — SPOF**

is a component whose failure causes:

**The entire system to fail**

Examples:

- One EC2 instance
- One NAT instance
- One Availability Zone
- One manually managed database
- One application server

### SAA Goal

> **Eliminate single points of failure whenever availability requirements justify it**

---

# Multi-AZ Architecture

For high availability within a Region:

Use:

**Multiple Availability Zones**

Example:

Users  
↓  
[[Application Load Balancer]]  
↓  
EC2 — AZ A  
EC2 — AZ B

### Killer Exam Clue

> **Application must survive an Availability Zone failure**
>
> → **Multi-AZ architecture**

---

# Multi-AZ Does Not Mean Multi-Region

Multi-AZ protects primarily against:

**Availability Zone failure**

Multi-Region can protect against:

**Regional failure**

### Memory Trick

> **AZ Failure**
> → Multi-AZ
>
> **Region Failure**
> → Multi-Region

---

# Horizontal Scaling

Horizontal scaling means:

**Add more instances**

Example:

2 EC2 instances  
↓  
Traffic increases  
↓  
6 EC2 instances

This is commonly implemented with:

[[Auto Scaling]]

### Memory Trick

**Horizontal = More Machines**

---

# Vertical Scaling

Vertical scaling means:

**Make one machine larger**

Example:

`t3.medium`

→

`m7i.2xlarge`

### Limitation

Vertical scaling eventually reaches:

**Instance-size limits**

and can still leave:

**A single point of failure**

### Killer Shortcut

**Elastic cloud architecture**
→ Prefer horizontal scaling where appropriate.

---

# Stateless Application Tier

Stateless applications do not store critical:

**User session state locally**

This makes instances easier to:

- Add
- Remove
- Replace
- Scale
- Fail over

### Architecture

Users  
↓  
Load Balancer  
↓  
Stateless EC2 Fleet  
↓  
Shared Data Store

### Killer Exam Principle

> **Stateless compute scales more easily**

---

# Externalize State

Instead of storing session data on:

**One EC2 instance**

store it in a shared system such as:

- DynamoDB
- ElastiCache
- Database
- S3 depending on workload

### Memory Trick

**Compute Can Die**

**State Must Survive**

---

# Load Balancing

A load balancer distributes traffic across:

**Multiple healthy targets**

Benefits include:

- High availability
- Horizontal scaling
- Health checks
- Traffic distribution

### Killer Exam Clue

> **Multiple application servers must receive traffic evenly**
>
> → **Elastic Load Balancing**

---

# Auto Scaling

[[Auto Scaling]] adjusts compute capacity based on:

**Demand**

Benefits:

- Scale out under load
- Scale in when demand falls
- Replace unhealthy instances
- Improve cost efficiency

### Memory Trick

**Load Balancer Distributes**

**Auto Scaling Adds/Removes**

---

# Elastic Architecture

An elastic architecture:

**Adjusts resources to actual demand**

Example:

Traffic Increases  
↓  
Scale Out

Traffic Decreases  
↓  
Scale In

### Exam Principle

> **Elasticity reduces the need to permanently provision for peak load**

---

# Decoupling

Decoupling means reducing:

**Direct dependencies between components**

Bad:

Web Server  
↓  
Directly calls Worker  
↓  
Worker overloaded  
↓  
Web application fails

Better:

Web Tier  
↓  
Queue  
↓  
Worker Tier

### Killer Exam Clue

> **Components must operate independently and absorb traffic spikes**
>
> → **Decouple with messaging**

---

# SQS for Decoupling

[[SQS]] is one of the most important architecture tools for:

**Decoupling**

Architecture:

Producer  
↓  
SQS Queue  
↓  
Consumers

Benefits:

- Buffer requests
- Handle spikes
- Independent scaling
- Improve resilience

### Killer Exam Clue

> **Traffic arrives faster than backend workers can process**
>
> → **SQS**

---

# Buffering

A queue acts as:

**A buffer**

Suppose:

Producer sends:

10,000 requests/minute

Workers process:

5,000/minute

Without a buffer:

**Requests may fail**

With SQS:

**Messages wait until consumers catch up**

### Memory Trick

**SQS = Shock Absorber**

---

# SNS for Fan-Out

[[SNS]] is useful when:

**One event must notify multiple consumers**

Architecture:

Publisher  
↓  
SNS Topic  
↓  
├── SQS A
├── SQS B
└── Lambda

### Killer Exam Clue

> **One message must be delivered to multiple independent subscribers**
>
> → **SNS Fan-Out**

---

# EventBridge for Event-Driven Architecture

[[EventBridge]] is useful when:

**Applications react to events**

Architecture:

Event Producer  
↓  
EventBridge  
↓  
Rules  
↓  
Multiple Targets

Think:

- Event routing
- SaaS events
- AWS service events
- Loosely coupled applications

### Memory Trick

**SQS = Queue**

**SNS = Broadcast**

**EventBridge = Route Events**

---

# Serverless Architecture

Serverless architectures reduce:

**Infrastructure management**

Common services:

- [[Lambda]]
- [[API Gateway]]
- [[DynamoDB]]
- S3
- EventBridge
- SQS

### Killer Exam Clue

> **Need minimal operational overhead and automatic scaling**
>
> → Consider **serverless**

---

# Managed Services

Prefer managed services when the question emphasizes:

**Least operational effort**

Examples:

Self-managed MySQL on EC2  
vs  
[[RDS]]

Self-managed Kafka  
vs  
MSK

Custom queue  
vs  
[[SQS]]

### Memory Trick

**Managed = AWS Operates More**

---

# Managed vs Self-Managed

## Managed Service

Advantages:

- Less administration
- Built-in scalability
- Built-in resilience
- Automated maintenance

## Self-Managed

Advantages:

- More control
- Custom software/configuration

But requires:

**More operational effort**

### Killer Exam Clue

> **Reduce administrative overhead**
>
> → Prefer managed services when requirements allow.

---

# Caching

Caching improves:

**Performance**

and reduces load on:

**Backend systems**

Possible caching layers include:

- [[CloudFront]]
- [[ElastiCache]]
- API Gateway caching
- Application caching

### Memory Trick

**Cache = Don't Recompute or Re-fetch**

---

# CloudFront

[[CloudFront]] caches content closer to:

**Users**

Use for:

- Static content
- Global users
- Reduced origin load
- Lower latency

### Killer Exam Clue

> **Global users need faster access to cacheable content**
>
> → **CloudFront**

---

# ElastiCache

[[ElastiCache]] provides:

**In-memory caching**

for applications.

Useful for:

- Database query caching
- Session storage
- Frequently requested application data

### Killer Exam Clue

> **Database receives repeated read queries and needs reduced latency/load**
>
> → **ElastiCache**

---

# Read Scaling

If a database workload is:

**Read-heavy**

consider:

- Read replicas
- Caching
- DynamoDB
- Aurora replicas depending on requirements

### Killer Exam Principle

> **Do not scale the primary database vertically if reads can be offloaded**

---

# Write Scaling

Write-heavy workloads require different strategies.

Possible patterns:

- DynamoDB partition scaling
- Queue buffering
- Sharding where appropriate
- Purpose-built databases

### Exam Principle

> **Read scaling and write scaling are not the same problem**

---

# Storage Selection

Choose storage based on:

**How the data is accessed**

### S3

Think:

**Object storage**

### EBS

Think:

**Block storage for EC2**

### EFS

Think:

**Shared Linux file system**

### FSx

Think:

**Specialized managed file systems**

### Killer Shortcut

> **Object**
> → S3
>
> **Block**
> → EBS
>
> **Shared File**
> → EFS / FSx

---

# Database Selection

Choose the database based on:

**Data model and access pattern**

### RDS / Aurora

Think:

**Relational + SQL**

### DynamoDB

Think:

**Key-value / document + massive scale**

### ElastiCache

Think:

**In-memory cache**

### Redshift

Think:

**Analytics warehouse**

### Memory Trick

**Workload First, Database Second**

---

# Relational vs NoSQL

Use relational databases when you need:

- SQL
- Joins
- Transactions
- Relational schema

Think:

[[RDS]] / [[Aurora]]

Use DynamoDB when you need:

- Massive scale
- Predictable low latency
- Key-value/document model
- Serverless operation

---

# Security by Design

Security should be built into:

**Every architecture layer**

Think:

- IAM least privilege
- Encryption at rest
- Encryption in transit
- Private subnets
- Security Groups
- Secrets Manager
- Logging

### Killer Exam Principle

> **Do not bolt security on afterward**

---

# Least Privilege

[[IAM]] permissions should grant:

**Only what is required**

Bad:

`AdministratorAccess`

for application workload

Better:

Specific API permissions for:

**Only required resources**

---

# Use IAM Roles

Applications running on AWS should normally use:

**IAM Roles**

instead of:

**Hardcoded access keys**

### Killer Exam Clue

> **EC2/Lambda needs access to S3**
>
> → **IAM Role**

---

# Encrypt Data at Rest

Common encryption options use:

[[KMS]]

Examples:

- S3
- EBS
- RDS
- DynamoDB

### Killer Shortcut

> **Customer-controlled encryption key**
>
> → **KMS Customer Managed Key**

---

# Encrypt Data in Transit

Think:

- TLS
- HTTPS
- [[ACM]]

### Killer Exam Clue

> **Need managed TLS certificate**
>
> → **ACM**

---

# Private Subnets

Sensitive backend resources such as:

- Databases
- Internal application servers

should generally avoid:

**Direct Internet exposure**

Architecture:

Internet  
↓  
Public ALB  
↓  
Private Application Tier  
↓  
Private Database Tier

---

# VPC Endpoints

[[VPC Endpoints]] allow private access to:

**Supported AWS services**

without using:

- NAT Gateway
- Internet Gateway path
- Public IP

### Killer Exam Clue

> **Private EC2 needs S3 without NAT**
>
> → **Gateway Endpoint**

---

# Cost Optimization

Cost-effective architecture often means:

**Match capacity and service choice to demand**

Common techniques:

- Auto Scaling
- Serverless
- S3 lifecycle policies
- Spot Instances
- Savings Plans
- Reserved capacity
- VPC Endpoints
- Caching

### Exam Principle

> **Cost optimization is not simply choosing the cheapest individual service**

---

# Spot Instances

Spot is appropriate for:

**Fault-tolerant and interruptible workloads**

Examples:

- Batch processing
- Stateless workers
- Flexible jobs

### Killer Exam Trap

Do NOT choose Spot for:

**Critical non-interruptible workloads**

unless architecture can tolerate interruptions.

---

# Reserved Capacity / Savings Plans

For:

**Predictable steady workloads**

committed pricing can reduce:

**Compute cost**

### Killer Shortcut

Steady workload  
→ Commitment discount

Interruptible workload  
→ Spot

Variable workload  
→ On-Demand / Auto Scaling

---

# Data Transfer Cost

Architecture should consider:

**Where traffic flows**

Examples:

- Cross-AZ traffic
- Cross-Region traffic
- NAT Gateway processing
- Internet transfer

### Killer Exam Principle

> **The shortest architectural path is often not the cheapest or most resilient path**

---

# Reliability

Reliable systems:

- Recover automatically
- Replace failed components
- Replicate critical data
- Monitor health
- Avoid single points of failure

### Architecture Pattern

Health Check  
↓  
Detect Failure  
↓  
Replace / Fail Over  
↓  
Continue Service

---

# Health Checks

Health checks should measure:

**Whether the application can actually serve requests**

not merely:

**Whether a server process exists**

### Exam Principle

> **Good health checks improve automated recovery**

---

# Monitoring

Architectures should include:

[[CloudWatch]]

for:

- Metrics
- Logs
- Alarms
- Automated responses

### Killer Exam Clue

> **Automatically respond to infrastructure metrics**
>
> → **CloudWatch Alarm + Automation**

---

# Auditing

For AWS API history:

Think:

[[CloudTrail]]

### Memory Trick

**CloudWatch = How Is It Running?**

**CloudTrail = Who Did What?**

---

# Disaster Recovery

DR architecture is driven by:

- RPO
- RTO
- Cost
- Recovery strategy

Strategies:

- [[Backup and Restore]]
- [[Pilot Light]]
- [[Warm Standby]]
- [[Multi-Site]]

### Killer Shortcut

> **Backups**
> → Build
>
> **Core**
> → Start
>
> **Small**
> → Scale
>
> **Full**
> → Route

---

# Architecture Thinking

## Scenario 1 — Traffic Spikes

Application receives unpredictable:

**Traffic spikes**

Choose:

Load Balancer  
+  
Auto Scaling

---

## Scenario 2 — Backend Overwhelmed

Frontend generates requests faster than workers process.

Choose:

**SQS**

to:

**Buffer and decouple**

---

## Scenario 3 — Global Static Content

Users worldwide access:

Images and videos.

Choose:

**CloudFront + S3**

---

## Scenario 4 — Repeated Database Reads

Application repeatedly reads:

Same database records.

Choose:

**ElastiCache**

---

## Scenario 5 — Private Database

Database should not be:

Internet-accessible.

Place:

RDS  
↓  
Private Subnets

and allow only:

**Application Security Group**

---

## Scenario 6 — Minimal Operations

Need API with:

**Highly variable traffic**

and:

**Minimal infrastructure management**

Think:

API Gateway  
+  
Lambda  
+  
DynamoDB

---

## Scenario 7 — Two AZ Failure Protection

Application must survive:

**One AZ failure**

Use:

**Multi-AZ architecture**

---

## Scenario 8 — Region Failure

Application must survive:

**Complete Region outage**

Use:

**Multi-Region DR**

---

## Scenario 9 — Lowest Cost

Two answers meet all requirements.

One uses:

Many always-on servers.

The other uses:

Managed/serverless scaling.

When the question emphasizes:

**Most cost-effective**

choose the architecture with:

**Less unnecessary idle infrastructure**

---

# Scenario Recognition

Immediately think:

**High Availability**

when you see:

- AZ failure
- Multiple instances
- Load balancing
- Automatic failover

Think:

**Scalability**

when you see:

- Traffic growth
- Millions of users
- Unpredictable load

Think:

**Decoupling**

when you see:

- Components fail together
- Traffic spikes overwhelm backend
- Async processing

Think:

**Caching**

when you see:

- Repeated reads
- High latency
- Reduce backend load

Think:

**DR**

when you see:

- RPO
- RTO
- Region failure

---

# Exam Traps

## Trap 1 — Most Complex Architecture Is Best

❌

Choose:

**The simplest architecture that meets the requirements**

---

## Trap 2 — Multi-Region Is Required for Every Highly Available Application

❌

Often:

**Multi-AZ**

is sufficient.

---

## Trap 3 — Vertical Scaling Is Always Better

❌

Horizontal scaling usually provides:

**Better elasticity and resilience**

where supported.

---

## Trap 4 — Application Servers Should Store Critical Session State Locally

❌

Externalize:

**State**

so instances can be replaced.

---

## Trap 5 — Direct Synchronous Coupling Is Always Fine

❌

For asynchronous workloads and spikes:

Think:

**SQS / event-driven design**

---

## Trap 6 — Cheapest Service Means Cheapest Architecture

❌

Consider:

**Total architecture cost**

including operations and data transfer.

---

## Trap 7 — Managed Services Give Less Value Because They Cost More Per Unit

❌

Managed services may greatly reduce:

**Operational overhead**

which is often an explicit exam requirement.

---

# Quick Architecture Cheat Sheet

| Requirement | Think |
|---|---|
| Survive AZ Failure | Multi-AZ |
| Survive Region Failure | Multi-Region |
| Distribute Traffic | Load Balancer |
| Automatic Compute Scaling | Auto Scaling |
| Buffer Work | SQS |
| Fan-Out | SNS |
| Event Routing | EventBridge |
| Global Cache | CloudFront |
| Database Cache | ElastiCache |
| Minimal Ops | Managed / Serverless |
| Object Storage | S3 |
| Block Storage | EBS |
| Shared File Storage | EFS |
| Relational Database | RDS / Aurora |
| Massive NoSQL | DynamoDB |
| Least Privilege | IAM |
| Encryption Keys | KMS |
| Private AWS Access | VPC Endpoint |
| Metrics / Alarms | CloudWatch |
| API Audit | CloudTrail |

---

# Architecture Decision Process

When reading an exam question:

## Step 1

Identify:

**The workload**

---

## Step 2

Identify:

**The primary requirement**

Examples:

- Cost
- Availability
- Performance
- Security
- Scalability
- DR

---

## Step 3

Identify:

**Constraints**

Examples:

- Must remain private
- Must survive Region failure
- Cannot lose data
- Minimal administration
- No code changes

---

## Step 4

Eliminate answers that:

**Violate a requirement**

---

## Step 5

Among remaining answers choose:

**The simplest and most cost-effective design**

that satisfies:

**All stated requirements**

---

# Final Exam Rapid-Fire

> **AZ FAILURE**
> → MULTI-AZ
>
> **REGION FAILURE**
> → MULTI-REGION
>
> **TRAFFIC DISTRIBUTION**
> → LOAD BALANCER
>
> **COMPUTE ELASTICITY**
> → AUTO SCALING
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
> **GLOBAL CACHE**
> → CLOUDFRONT
>
> **DATABASE CACHE**
> → ELASTICACHE
>
> **MINIMAL OPS**
> → MANAGED / SERVERLESS
>
> **STATE**
> → EXTERNALIZE IT
>
> **PRIVATE AWS SERVICE ACCESS**
> → VPC ENDPOINT
>
> **METRICS**
> → CLOUDWATCH
>
> **API AUDIT**
> → CLOUDTRAIL
>
> **DATA LOSS**
> → RPO
>
> **DOWNTIME**
> → RTO

---

## Master Memory Trick

> [!tip] Architecture Master Memory Trick
> When you see a long SAA scenario, do NOT start by asking:
>
> **"Which AWS service is this?"**
>
> Start by asking:
>
> **"WHAT DOES THE BUSINESS NEED?"**
>
> Then identify:
>
> **AVAILABILITY**
>
> **SCALABILITY**
>
> **PERFORMANCE**
>
> **SECURITY**
>
> **COST**
>
> **OPERATIONS**
>
> **DISASTER RECOVERY**
>
> Then choose the:
>
> **Simplest AWS architecture that satisfies all of them.**

So remember:

> **REQUIREMENTS**
> → FIRST
>
> **SERVICES**
> → SECOND
>
> **MULTI-AZ**
> → AVAILABILITY
>
> **AUTO SCALING**
> → ELASTICITY
>
> **SQS**
> → DECOUPLE
>
> **CACHE**
> → PERFORMANCE
>
> **MANAGED SERVICE**
> → LOWER OPERATIONS
>
> **IAM + ENCRYPTION**
> → SECURITY
>
> **RPO + RTO**
> → DR
>
> **COST-EFFECTIVE**
> → MEET REQUIREMENT WITHOUT OVERBUILDING

And the killer SAA principle:

> **"Choose the architecture that satisfies every stated requirement with the least unnecessary complexity, cost, and operational overhead."**

---

## Related Notes

- [[Application Load Balancer]]
- [[Auto Scaling]]
- [[SQS]]
- [[SNS]]
- [[EventBridge]]
- [[CloudFront]]
- [[ElastiCache]]
- [[S3]]
- [[RDS]]
- [[Aurora]]
- [[DynamoDB]]
- [[IAM]]
- [[KMS]]
- [[VPC Endpoints]]
- [[CloudWatch]]
- [[CloudTrail]]
- [[Disaster Recovery Overview]]
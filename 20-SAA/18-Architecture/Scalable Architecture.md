## Core Concept

Scalable architecture means designing systems that can:

**Handle increasing or decreasing workload without major redesign**

Scaling can involve:

- Compute
- Databases
- Storage
- Messaging
- Networking
- Caching
- Serverless services

> [!tip] Memory Trick
> **Scalability = Handle More Work**

---

# Scalability vs Elasticity

These terms are related but different.

## Scalability

The system can:

**Handle more workload**

## Elasticity

The system can:

**Automatically adjust capacity as demand changes**

### Killer Shortcut

> **Can grow**
> → Scalable
>
> **Grows and shrinks automatically**
> → Elastic

---

# Vertical Scaling

Vertical scaling means:

**Make one resource larger**

Example:

EC2:

`t3.medium`

→

`m7i.4xlarge`

### Benefits

- Simple
- Minimal architectural change

### Limitations

- Maximum instance size
- Possible downtime during resize
- Still may be one failure point

### Memory Trick

**Vertical = Bigger Machine**

---

# Horizontal Scaling

Horizontal scaling means:

**Add more resources**

Example:

2 EC2 instances  
↓  
8 EC2 instances

### Benefits

- Better elasticity
- Better resilience
- Large-scale capacity
- Works well with load balancing

### Killer Exam Clue

> **Application must scale automatically with unpredictable traffic**
>
> → **Horizontal scaling**

### Memory Trick

**Horizontal = More Machines**

---

# Horizontal Scaling Architecture

Users  
↓  
[[Application Load Balancer]]  
↓  
[[Auto Scaling]] Group  
↓  
EC2 A  
EC2 B  
EC2 C

As traffic increases:

**Add instances**

As traffic decreases:

**Remove instances**

---

# Auto Scaling

[[Auto Scaling]] automatically adjusts:

**EC2 capacity**

based on:

- Metrics
- Schedules
- Target utilization
- Demand

### Killer Exam Clue

> **Need automatic EC2 scale-out and scale-in**
>
> → **Auto Scaling**

---

# Auto Scaling Benefits

- Handles traffic growth
- Handles traffic decline
- Replaces unhealthy instances
- Reduces idle capacity
- Supports Multi-AZ deployments

### Memory Trick

**Auto Scaling = Right Amount of Compute**

---

# Load Balancer

A load balancer distributes traffic across:

**Multiple application instances**

Without one:

Clients may not know:

**Which instance should receive traffic**

Architecture:

Users  
↓  
Load Balancer  
↓  
Scaled Compute Fleet

### Killer Exam Principle

> **Horizontal scaling often requires load balancing**

---

# Load Balancer vs Auto Scaling

## Load Balancer

Think:

**Distribute traffic**

## Auto Scaling

Think:

**Change capacity**

### Memory Trick

**ALB = Send**

**ASG = Add/Remove**

---

# Stateless Compute

Horizontal scaling works best when application servers are:

**Stateless**

Any instance should be able to:

**Handle any request**

### Killer Exam Clue

> **Application needs seamless horizontal scaling**
>
> → **Externalize state**

---

# Why Stateful Compute Is Harder to Scale

If user sessions live on:

**Specific EC2 instances**

adding or removing instances becomes:

**More complicated**

Better:

Store shared state in:

- ElastiCache
- DynamoDB
- RDS
- S3
- EFS depending on the requirement

### Memory Trick

**Stateless Compute = Easy Scale**

---

# Scaling Based on CPU

A common Auto Scaling metric is:

**CPU utilization**

Example:

CPU > 70%  
→ Scale Out

CPU < 30%  
→ Scale In

### Exam Principle

> **Choose a metric that represents actual workload**

---

# Scaling Based on Request Count

For web applications:

**Request count**

may be more meaningful than CPU.

Example:

ALB Request Count per Target increases  
↓  
Auto Scaling adds instances

### Killer Exam Clue

> **Scale web tier according to incoming request volume**
>
> → **Request-based scaling**

---

# Scaling Based on Queue Depth

For worker systems:

[[SQS]] queue depth can drive:

**Worker scaling**

Architecture:

Producer  
↓  
SQS  
↓  
Worker Auto Scaling Group

Queue grows  
→ Scale Out

Queue shrinks  
→ Scale In

### Killer Exam Clue

> **Workers must scale based on queued jobs**
>
> → **SQS Queue Depth + Auto Scaling**

---

# Target Tracking Scaling

Target Tracking keeps a metric near:

**A desired target**

Example:

Maintain average CPU around:

**50%**

Auto Scaling handles:

**Scale-out and scale-in**

### Memory Trick

**Target Tracking = Keep Metric Near This Number**

---

# Step Scaling

Step Scaling changes capacity by:

**Different amounts**

depending on:

**How far a metric exceeds a threshold**

Example:

CPU 60–70%  
→ Add 1 instance

CPU 70–90%  
→ Add 3 instances

CPU > 90%  
→ Add 5 instances

### Exam Recognition

> **Different scaling amounts for different alarm levels**
>
> → **Step Scaling**

---

# Scheduled Scaling

Scheduled Scaling changes capacity based on:

**Known time patterns**

Example:

Every weekday at 8 AM:

Scale to 20 instances

At 8 PM:

Scale down

### Killer Exam Clue

> **Traffic spike occurs predictably every weekday morning**
>
> → **Scheduled Scaling**

---

# Predictive Scaling

Predictive Scaling uses historical patterns to:

**Forecast future capacity needs**

### Killer Exam Clue

> **Automatically forecast recurring traffic patterns**
>
> → **Predictive Scaling**

---

# Reactive vs Proactive Scaling

## Reactive

Scale after:

**Demand increases**

Examples:

- Target Tracking
- Step Scaling

## Proactive

Scale before:

**Expected demand**

Examples:

- Scheduled Scaling
- Predictive Scaling

### Memory Trick

**Reactive = Respond**

**Proactive = Prepare**

---

# Scaling Cooldowns / Stabilization

Scaling systems need to avoid:

**Rapid oscillation**

where instances constantly:

- Launch
- Terminate
- Launch again

Scaling behavior should allow enough time for:

**Capacity changes to take effect**

### Exam Principle

> **Avoid unnecessary scaling churn**

---

# Database Scaling

Databases scale differently from:

**Stateless compute**

Common strategies include:

- Vertical scaling
- Read replicas
- Caching
- Sharding/partitioning
- Serverless scaling

---

# Read Scaling

If the problem is:

**Too many reads**

consider:

- Read replicas
- ElastiCache
- DAX
- DynamoDB
- Aurora replicas

### Killer Exam Principle

> **Do not solve every read problem by making the primary database larger**

---

# RDS Read Replicas

[[RDS]] Read Replicas provide:

**Additional read capacity**

Architecture:

Primary RDS  
↓  
Replication  
↓  
Read Replica A  
Read Replica B

Applications send:

**Read queries**

to replicas.

### Killer Exam Clue

> **Relational database is overwhelmed by read traffic**
>
> → **Read Replicas**

---

# Multi-AZ vs Read Replica

## Multi-AZ

Think:

**Availability**

## Read Replica

Think:

**Read scaling**

### Killer Shortcut

**Failover**
→ Multi-AZ

**More reads**
→ Read Replica

---

# Aurora Scaling

[[Aurora]] supports:

**Multiple read replicas**

and can scale relational read workloads across:

**Aurora Replicas**

### Killer Exam Clue

> **Need high-performance relational read scaling**
>
> → **Aurora Replicas**

---

# Caching Before Scaling Database

If requests repeatedly ask for:

**The same data**

cache may be more efficient than:

**Adding more database replicas**

Architecture:

Application  
↓  
[[ElastiCache]]  
↓  
Database

### Memory Trick

**Repeated Read = Cache First**

---

# DynamoDB Scaling

[[DynamoDB]] is designed for:

**Massive horizontal scale**

Capacity modes include concepts such as:

- On-demand
- Provisioned capacity

### Killer Exam Clue

> **Serverless key-value database must handle unpredictable traffic**
>
> → **DynamoDB On-Demand**

---

# DynamoDB On-Demand

On-Demand mode automatically handles:

**Variable request traffic**

without requiring:

**Capacity planning**

### Memory Trick

**Unpredictable DynamoDB = On-Demand**

---

# DynamoDB Provisioned Capacity

Provisioned capacity can work well for:

**Predictable workloads**

and supports:

**Auto Scaling**

### Killer Shortcut

Unpredictable traffic  
→ On-Demand

Predictable traffic  
→ Provisioned may be cost-effective

---

# Partitioning

Distributed databases scale through:

**Partitioning**

Data is spread across:

**Multiple partitions**

A poor key design can create:

**Hot partitions**

### Killer Exam Principle

> **Good partition-key distribution is critical for scalable DynamoDB design**

---

# Hot Partition

A hot partition occurs when:

**Too much traffic targets the same partition key**

Example:

Every request uses:

`customer_id = GLOBAL`

This concentrates load.

### Memory Trick

**Bad Key Distribution = Hot Spot**

---

# S3 Scaling

[[S3]] is designed to scale automatically for:

**Very large object workloads**

You do not manually:

**Add storage servers**

### Killer Exam Principle

> **Use managed storage instead of building custom scalable object-storage fleets**

---

# EFS Scaling

[[EFS]] provides:

**Elastic shared file storage**

that grows and shrinks with:

**Stored data**

This reduces manual filesystem capacity management.

---

# Serverless Scaling

Serverless services automatically handle much of:

**Infrastructure scaling**

Examples:

- [[Lambda]]
- [[API Gateway]]
- DynamoDB
- S3
- SQS

### Killer Exam Clue

> **Need automatic scaling with minimal infrastructure management**
>
> → **Serverless architecture**

---

# Lambda Scaling

[[Lambda]] can scale by running:

**Multiple concurrent executions**

as request/event volume increases.

### Killer Exam Clue

> **Event-driven compute must automatically scale without managing EC2**
>
> → **Lambda**

---

# Lambda Concurrency

Concurrency represents:

**How many function executions run at the same time**

High event volume:

↓  
Higher concurrent executions

### Exam Principle

> **Serverless does not mean unlimited capacity; service quotas and concurrency still matter**

---

# API Gateway Scaling

[[API Gateway]] provides managed:

**API request handling**

without deploying:

**Your own web server fleet**

This pairs well with:

**Lambda**

for elastic APIs.

---

# Decoupling for Scalability

[[SQS]] helps prevent temporary demand spikes from overwhelming:

**Backend consumers**

Producer scale and consumer scale become:

**Independent**

### Killer Exam Clue

> **Front-end scales faster than backend processing tier**
>
> → **Decouple with SQS**

---

# Queue as Load Leveler

SQS acts as:

**A load-leveling buffer**

Instead of processing every request immediately:

Requests  
↓  
Queue  
↓  
Workers process at sustainable rate

### Memory Trick

**SQS Smooths the Spike**

---

# Fan-Out Scaling

[[SNS]] can send one event to:

**Multiple independent consumers**

Each consumer can:

**Scale independently**

Example:

Order  
↓  
SNS  
↓  
Billing Queue  
Shipping Queue  
Analytics Queue

---

# Caching for Scalability

Caching reduces:

**Repeated backend work**

This can prevent:

**Backend scaling requirements**

Architecture:

Users  
↓  
Cache  
↓  
Backend

Fewer backend calls mean:

**More effective capacity**

---

# CloudFront for Global Scale

[[CloudFront]] distributes content through:

**Edge locations**

This helps origins handle:

**Large global request volume**

### Killer Exam Clue

> **Millions of global users request static content**
>
> → **CloudFront**

---

# ElastiCache for Backend Scale

[[ElastiCache]] reduces:

**Repeated database reads**

This can allow databases to handle:

**Larger application workloads**

without proportional scaling.

---

# Scaling Storage and Compute Independently

A strong architecture avoids tying:

**Storage capacity**

directly to:

**Compute capacity**

Example:

Stateless EC2  
↓  
S3 / EFS / Database

This allows:

Compute  
→ Scale independently

Storage  
→ Scale independently

### Memory Trick

**Separate Layers = Scale Separately**

---

# Microservices and Scalability

Microservices can allow each service to:

**Scale independently**

Example:

Search Service  
→ 20 instances

Billing Service  
→ 3 instances

Image Processor  
→ 50 workers

This is more efficient than scaling:

**One giant monolith**

when only one function is busy.

---

# Monolith Scaling

With a monolith:

If one feature needs more capacity:

**The entire application may need to scale**

This can waste:

**Resources**

### Exam Principle

> **Independent components can scale more efficiently**

---

# ECS and EKS Scaling

Container platforms such as:

[[ECS]]

and:

[[EKS]]

can scale:

- Tasks
- Pods
- Nodes

based on:

**Workload demand**

### Killer Exam Clue

> **Containerized application needs dynamic horizontal scaling**
>
> → Scale container tasks/pods and underlying capacity appropriately

---

# Cost and Scaling

Scaling should not mean:

**Run maximum capacity all the time**

Elastic design matches:

**Resources to actual demand**

### Killer Exam Principle

> **Overprovisioning improves capacity but hurts cost efficiency**

---

# Scale Out vs Overprovision

Bad:

Run 50 servers continuously for:

**Peak holiday traffic**

Good:

Normal:

5 servers

Peak:

Scale to 50

After peak:

Scale back to 5

### Memory Trick

**Elasticity = Don't Pay for Peak Forever**

---

# Spot for Scalable Workers

Fault-tolerant worker fleets can use:

**Spot Instances**

to reduce cost.

A good pattern:

SQS  
↓  
Auto Scaling Worker Fleet  
↓  
Spot + On-Demand Mix

### Killer Exam Clue

> **Large fault-tolerant batch workload needs low-cost scaling**
>
> → Consider **Spot Instances**

---

# Scaling and High Availability

Scalability and availability often reinforce:

**Each other**

Multiple instances provide:

- More capacity
- More redundancy

However:

**More instances in one AZ**

do not protect against:

**AZ failure**

### Exam Principle

> **Scale across failure domains**

---

# Multi-AZ Scaling

A strong web tier:

ALB  
↓  
Auto Scaling Group  
↓  
AZ A + AZ B + AZ C

This provides:

- Capacity
- Resilience
- Elasticity

---

# Global Scaling

For global users, scaling may require:

**Multiple geographic layers**

Examples:

- CloudFront
- Global Accelerator
- Multi-Region applications
- DynamoDB Global Tables
- Aurora Global Database

### Killer Exam Clue

> **Users worldwide need low latency and regional resilience**
>
> → Consider **global architecture**

---

# Architecture Thinking

## Scenario 1 — Unpredictable Website

Traffic ranges from:

1,000 requests/hour

to:

100,000 requests/hour

Choose:

**Load Balancer + Auto Scaling**

---

## Scenario 2 — Predictable Monday Spike

Traffic spikes:

Every Monday at 9 AM.

Choose:

**Scheduled Scaling**

---

## Scenario 3 — Worker Backlog

SQS messages rapidly increase.

Choose:

**Scale worker fleet based on queue depth**

---

## Scenario 4 — Database Reads

RDS CPU is high because of:

**Read-heavy reporting queries**

Choose:

**Read Replica**

---

## Scenario 5 — Repeated Reads

Application repeatedly requests:

**Same product data**

Choose:

**ElastiCache**

before simply increasing database size.

---

## Scenario 6 — Unpredictable NoSQL

Application uses DynamoDB and traffic varies:

**Wildly**

Choose:

**On-Demand capacity**

---

## Scenario 7 — Static Global Site

Millions of users request:

**Same website assets**

Choose:

**CloudFront**

---

## Scenario 8 — Async Processing

Processing tier cannot keep up with:

**Burst traffic**

Choose:

**SQS**

---

## Scenario 9 — Serverless API

API demand is:

Highly unpredictable

and operations team wants:

Minimal infrastructure management.

Think:

**API Gateway + Lambda**

---

# Scenario Recognition

Immediately think:

**Auto Scaling**

when you see:

- EC2 capacity
- Scale out/in
- Dynamic compute
- CPU/request scaling

---

## Think SQS When You See

- Worker backlog
- Burst traffic
- Processing capacity mismatch

---

## Think Read Replica When You See

- Relational read scaling
- Reporting queries

---

## Think Cache When You See

- Repeated reads
- Same data
- Reduce backend load

---

## Think Serverless When You See

- Unpredictable demand
- Minimal operations
- Automatic scaling

---

# Exam Traps

## Trap 1 — Vertical Scaling Is Unlimited

❌

Eventually you reach:

**Maximum resource sizes**

---

## Trap 2 — More EC2 Instances Automatically Means Elasticity

❌

Elasticity requires:

**Capacity to adjust with demand**

---

## Trap 3 — Multi-AZ Alone Solves Scalability

❌

Multi-AZ primarily improves:

**Availability**

Scaling requires:

**Capacity management**

---

## Trap 4 — RDS Multi-AZ Is for Read Scaling

❌

Think:

**Read Replica**

---

## Trap 5 — Cache and Read Replica Are Identical

❌

Cache:

**May avoid database query**

Read Replica:

**Processes database read**

---

## Trap 6 — SQS Processes Messages

❌

SQS:

**Stores messages**

Consumers:

**Process them**

---

## Trap 7 — Serverless Means Infinite Capacity

❌

Quotas and service-specific scaling behavior still matter.

---

## Trap 8 — Scaling Only Means Compute

❌

Also consider:

- Database
- Storage
- Messaging
- Network
- Cache

---

# Quick Cheat Sheet

| Exam Clue | Answer |
|---|---|
| Bigger Machine | Vertical Scaling |
| More Machines | Horizontal Scaling |
| Automatic EC2 Scaling | Auto Scaling |
| Distribute Requests | Load Balancer |
| Predictable Time-Based Spike | Scheduled Scaling |
| Forecast Traffic | Predictive Scaling |
| Maintain Target Metric | Target Tracking |
| Different Scale Amounts | Step Scaling |
| Worker Backlog | SQS + Auto Scaling |
| Relational Read Scaling | Read Replica |
| Repeated Reads | Cache |
| DynamoDB Unpredictable Traffic | On-Demand |
| Global Static Scale | CloudFront |
| Minimal Ops Compute | Lambda |

---

# Scaling Decision Map

Need:

**More EC2 capacity**

→ Auto Scaling

Need:

**Distribute web requests**

→ Load Balancer

Need:

**Predictable scheduled demand**

→ Scheduled Scaling

Need:

**Forecast recurring demand**

→ Predictive Scaling

Need:

**Worker scaling**

→ SQS Queue Depth + Auto Scaling

Need:

**More relational reads**

→ Read Replica

Need:

**Repeated database reads**

→ ElastiCache

Need:

**Massive unpredictable NoSQL**

→ DynamoDB On-Demand

Need:

**Serverless compute**

→ Lambda

---

# Scaling Layer Map

> **WEB TIER**
> → LOAD BALANCER + AUTO SCALING
>
> **WORKER TIER**
> → SQS + AUTO SCALING
>
> **DATABASE READS**
> → READ REPLICAS
>
> **REPEATED DATA**
> → CACHE
>
> **NOSQL**
> → DYNAMODB
>
> **STATIC CONTENT**
> → CLOUDFRONT
>
> **SERVERLESS COMPUTE**
> → LAMBDA

---

# Final Exam Rapid-Fire

> **BIGGER INSTANCE**
> → VERTICAL
>
> **MORE INSTANCES**
> → HORIZONTAL
>
> **AUTOMATIC CAPACITY**
> → AUTO SCALING
>
> **TRAFFIC DISTRIBUTION**
> → LOAD BALANCER
>
> **KNOWN TRAFFIC TIME**
> → SCHEDULED SCALING
>
> **FORECAST TRAFFIC**
> → PREDICTIVE SCALING
>
> **KEEP CPU NEAR TARGET**
> → TARGET TRACKING
>
> **QUEUE BACKLOG**
> → SCALE WORKERS
>
> **DATABASE READS**
> → READ REPLICAS
>
> **REPEATED DATABASE READS**
> → CACHE
>
> **UNPREDICTABLE DYNAMODB**
> → ON-DEMAND
>
> **GLOBAL STATIC TRAFFIC**
> → CLOUDFRONT
>
> **MINIMAL OPS COMPUTE**
> → LAMBDA

---

## Master Memory Trick

> [!tip] Scalable Architecture Master Memory Trick
> Imagine your application is:
>
> **A grocery store**
>
> One checkout lane gets overwhelmed.
>
> You could:
>
> **Make that one cashier faster**
>
> That's:
>
> **VERTICAL SCALING**
>
> Or:
>
> **Open more checkout lanes**
>
> That's:
>
> **HORIZONTAL SCALING**
>
> Then traffic changes throughout the day.
>
> Automatically open and close lanes:
>
> **AUTO SCALING**
>
> Send customers to available lanes:
>
> **LOAD BALANCER**
>
> Customers arrive faster than stockroom workers can handle requests?
>
> Put requests into:
>
> **SQS**
>
> Everyone keeps asking where the milk is?
>
> Put the answer somewhere fast:
>
> **CACHE**

So remember:

> **VERTICAL**
> → BIGGER
>
> **HORIZONTAL**
> → MORE
>
> **AUTO SCALING**
> → ADJUST
>
> **LOAD BALANCER**
> → DISTRIBUTE
>
> **SQS**
> → BUFFER
>
> **CACHE**
> → AVOID REPEATED WORK
>
> **READ REPLICA**
> → MORE READ CAPACITY
>
> **SERVERLESS**
> → AWS HANDLES SCALE

And the killer SAA question:

> **"Which layer is becoming the bottleneck, and can that layer scale independently?"**
>
> Find the bottleneck.
>
> Then choose:
>
> **The appropriate scaling mechanism for that layer.**

---

## Related Notes

- [[Architecture Principles]]
- [[Stateless vs Stateful Architecture]]
- [[Decoupled Architecture]]
- [[Caching Architecture]]
- [[High Availability Architecture]]
- [[Application Load Balancer]]
- [[Auto Scaling]]
- [[SQS]]
- [[ElastiCache]]
- [[RDS]]
- [[Aurora]]
- [[DynamoDB]]
- [[CloudFront]]
- [[Lambda]]
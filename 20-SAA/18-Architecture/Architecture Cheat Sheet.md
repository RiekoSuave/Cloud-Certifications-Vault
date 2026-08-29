## Core Architecture Mindset

The SAA exam is usually asking:

**Which architecture best satisfies the requirements?**

Start with:

1. Availability
2. Scalability
3. Performance
4. Security
5. Cost
6. Operational overhead
7. Disaster recovery

> [!tip] Master Memory Trick
> **Requirements First**
>
> **Services Second**

---

# First Question to Ask

Before choosing a service, identify:

**What is the question optimizing for?**

Common clues:

**Most cost-effective**
→ Minimize unnecessary cost

**Least operational overhead**
→ Prefer managed/serverless

**Highly available**
→ Multi-AZ

**Global users**
→ CloudFront / Global architecture

**Decouple**
→ SQS / messaging

**Survive Region failure**
→ Multi-Region

**Low latency repeated reads**
→ Cache

---

# Architecture Decision Rule

Choose:

**The simplest architecture that satisfies every stated requirement**

Do NOT automatically choose:

- Most expensive
- Most complex
- Most redundant
- Most powerful

### Killer Exam Principle

> **Meet requirements without overengineering**

---

# Stateless vs Stateful

[[Stateless vs Stateful Architecture]]

## Stateless

Any server can handle:

**Any request**

Best for:

- Auto Scaling
- Load balancing
- Multi-AZ
- Containers
- Serverless

## Stateful

Important state lives on:

**A specific server**

This makes scaling and failover:

**Harder**

### Killer Shortcut

> **Replaceable Compute**
> → Stateless
>
> **Unique Local State**
> → Stateful

---

# Externalize State

Move state into:

- ElastiCache
- DynamoDB
- RDS / Aurora
- S3
- EFS

### Memory Trick

> **Compute Can Die**
>
> **State Must Survive**

---

# Session State

Need:

**Fast shared sessions**

→ ElastiCache

Need:

**Durable serverless session/state**

→ DynamoDB

Need:

**Shared Linux files**

→ EFS

Need:

**Object uploads**

→ S3

---

# Sticky Sessions

Sticky sessions keep users attached to:

**The same backend**

This may help legacy stateful applications.

But:

**Stickiness is not true stateless architecture**

### Killer Exam Principle

> **Externalizing state is usually more scalable than relying on stickiness**

---

# Decoupled Architecture

[[Decoupled Architecture]]

Decoupling means:

**Components do not require each other to be available at the same moment**

Classic pattern:

Producer  
↓  
SQS  
↓  
Consumer

### Killer Exam Clue

> **Backend cannot keep up with incoming work**
>
> → **SQS**

---

# SQS

Think:

**Buffer**

Use for:

- Asynchronous work
- Traffic spikes
- Worker queues
- Backpressure
- Decoupling

### Memory Trick

**SQS = Shock Absorber**

---

# SNS

Think:

**Fan-Out**

One event:

↓  

Many subscribers

### Killer Exam Clue

> **One event must reach multiple independent consumers**
>
> → **SNS**

---

# SNS + SQS

Think:

**Fan-Out + Durable Buffering**

Architecture:

SNS  
↓  
├── SQS A
├── SQS B
└── SQS C

### Killer Exam Clue

> **Multiple applications must independently process the same event**
>
> → **SNS + SQS**

---

# EventBridge

Think:

**Event Routing**

Use when:

**Different events need different targets**

### Memory Trick

> **SQS = Hold**
>
> **SNS = Broadcast**
>
> **EventBridge = Route**

---

# SQS FIFO

Need:

**Strict ordering**

→ SQS FIFO

### Killer Shortcut

**Order matters**
→ FIFO

**Maximum throughput / loose ordering**
→ Standard Queue

---

# Dead-Letter Queue

Need:

**Messages that repeatedly fail processing**

→ DLQ

### Memory Trick

**DLQ = Failed Message Parking Lot**

---

# Visibility Timeout

If processing takes longer than:

**Visibility Timeout**

a message may become visible again and:

**Be processed twice**

### Killer Exam Clue

> **Duplicate processing because workers take too long**
>
> → Increase Visibility Timeout

---

# Idempotency

SQS Standard may deliver a message:

**More than once**

Consumers should ideally be:

**Idempotent**

### Memory Trick

**Duplicate Message Should Not Duplicate the Business Action**

---

# Caching Architecture

[[Caching Architecture]]

Use caching when:

**The system repeatedly retrieves the same data**

Possible caching layers:

- CloudFront
- ElastiCache
- DAX
- API Gateway Cache

---

# CloudFront

Think:

**Cache Near the User**

Use for:

- Global users
- Static content
- Edge caching
- Reduced origin load

### Killer Exam Clue

> **Global users repeatedly request the same content**
>
> → **CloudFront**

---

# ElastiCache

Think:

**Application / Database Cache**

Use for:

- Sessions
- Repeated database reads
- Frequently accessed application data

### Killer Exam Clue

> **Database receives repeated identical read queries**
>
> → **ElastiCache**

---

# DAX

Think:

**DynamoDB Cache**

### Killer Exam Clue

> **Repeated DynamoDB reads need very low latency**
>
> → **DAX**

---

# Read Replica vs Cache

## Read Replica

Provides:

**More database read capacity**

## Cache

May avoid:

**Database queries entirely**

### Killer Shortcut

Repeated same data  
→ Cache

Many different reads  
→ Read Replica

---

# High Availability

[[High Availability Architecture]]

High Availability means:

**Keep running during failure**

Think:

- Multi-AZ
- Load Balancer
- Auto Scaling
- Health checks
- Database failover

### Memory Trick

**HA = Stay Running**

---

# Single Point of Failure

A single point of failure is:

**One component whose failure breaks the application**

Examples:

- One EC2
- One AZ
- One database
- One NAT instance

### Killer Exam Principle

> **Identify what happens when each component fails**

---

# Multi-AZ

Need to survive:

**Availability Zone failure**

→ Multi-AZ

### Killer Shortcut

**AZ Failure**
→ Multi-AZ

**Region Failure**
→ Multi-Region

---

# Load Balancer

Need:

**Distribute traffic across healthy targets**

→ Load Balancer

### Memory Trick

**Load Balancer = Route Traffic**

---

# Auto Scaling

Need:

**Maintain or adjust EC2 capacity**

→ Auto Scaling

### Memory Trick

**Load Balancer = Send**

**Auto Scaling = Add / Remove**

---

# RDS Multi-AZ

Need:

**Relational database failover**

→ RDS Multi-AZ

### Killer Exam Trap

RDS Multi-AZ:

**High Availability**

RDS Read Replica:

**Read Scaling**

---

# Multi-AZ vs Read Replica

| Requirement | Answer |
|---|---|
| Automatic Failover | Multi-AZ |
| AZ Failure Protection | Multi-AZ |
| More Read Capacity | Read Replica |
| Reporting Queries | Read Replica |

---

# Multi-Region

Need to survive:

**Complete Region failure**

→ Multi-Region

### Memory Trick

> **Instance Failure**
> → Replace
>
> **AZ Failure**
> → Multi-AZ
>
> **Region Failure**
> → Multi-Region

---

# Scalability

[[Scalable Architecture]]

Scalability means:

**Handle more workload**

Elasticity means:

**Automatically grow and shrink with demand**

---

# Vertical Scaling

Think:

**Bigger machine**

Example:

Small EC2  
→ Larger EC2

### Limitation

Eventually:

**You hit a maximum size**

---

# Horizontal Scaling

Think:

**More machines**

Example:

2 EC2  
→ 10 EC2

### Killer Exam Principle

> **Cloud-native architectures generally prefer horizontal scaling where practical**

---

# Target Tracking

Need:

**Keep a metric near a target**

Example:

CPU near 50%

→ Target Tracking

---

# Step Scaling

Need:

**Different scale amounts based on alarm severity**

→ Step Scaling

---

# Scheduled Scaling

Need:

**Known recurring traffic increase**

→ Scheduled Scaling

---

# Predictive Scaling

Need:

**Forecast recurring demand**

→ Predictive Scaling

---

# Queue-Based Scaling

Need workers to scale according to:

**Backlog**

→ SQS Queue Depth + Auto Scaling

### Killer Exam Clue

> **Queue grows faster than workers process**
>
> → Scale workers

---

# Database Read Scaling

Need:

**More relational reads**

→ Read Replica

Need:

**Repeated same reads**

→ Cache

Need:

**Massive serverless NoSQL**

→ DynamoDB

---

# DynamoDB Capacity

## On-Demand

Think:

**Unpredictable traffic**

## Provisioned

Think:

**Predictable traffic**

### Killer Shortcut

Unpredictable  
→ On-Demand

Predictable  
→ Provisioned may be more cost-effective

---

# Serverless Architecture

[[Serverless Architecture]]

Think:

**Minimal infrastructure management**

Core pattern:

User  
↓  
API Gateway  
↓  
Lambda  
↓  
DynamoDB

### Killer Exam Clue

> **Highly variable workload + minimal operations**
>
> → **Serverless**

---

# Lambda

Think:

**Event-driven compute**

Use when:

- Code runs on events
- No server management
- Short-lived execution
- Automatic scaling

### Killer Exam Clue

> **Run code when an event occurs**
>
> → **Lambda**

---

# API Gateway

Think:

**Managed API front door**

### Killer Exam Clue

> **Expose REST/HTTP/WebSocket API without managing web servers**
>
> → **API Gateway**

---

# Step Functions

Think:

**Workflow Orchestration**

Use when:

- Multiple steps
- Retry logic
- Decisions
- Parallel branches

### Memory Trick

**EventBridge = Route**

**Step Functions = Orchestrate**

---

# Cognito

Think:

**Application User Authentication**

### Killer Exam Clue

> **Managed user sign-up/sign-in**
>
> → **Cognito**

---

# Secure Architecture

[[Secure Architecture]]

Security should be:

**Layered**

Think:

- IAM
- Security Groups
- NACL
- KMS
- Secrets Manager
- WAF
- Shield
- GuardDuty
- Inspector
- Macie
- Security Hub

---

# Least Privilege

Need:

**Only necessary permissions**

→ IAM Least Privilege

### Killer Exam Clue

> **EC2 needs S3 without stored credentials**
>
> → **IAM Role**

---

# Security Groups

Think:

**Stateful Resource Firewall**

---

# NACL

Think:

**Stateless Subnet Firewall**

### Killer Shortcut

Resource  
→ Security Group

Subnet + Explicit Deny  
→ NACL

---

# KMS

Think:

**Encryption Keys**

---

# Secrets Manager

Think:

**Secrets + Automatic Rotation**

---

# WAF

Think:

**Web Attacks**

Examples:

- SQL injection
- XSS

---

# Shield

Think:

**DDoS**

---

# GuardDuty

Think:

**Threat Detection**

---

# Inspector

Think:

**Vulnerabilities / CVEs**

---

# Macie

Think:

**Sensitive S3 Data**

---

# Security Hub

Think:

**Central Security Findings**

---

# CloudTrail

Think:

**Who Did What?**

Records:

**AWS API activity**

---

# VPC Flow Logs

Think:

**Who Talked to Whom?**

Records:

**Network traffic metadata**

---

# Cost-Optimized Architecture

[[Cost-Optimized Architecture]]

Cost optimization means:

**Meet requirements without unnecessary spend**

### Killer Exam Principle

> **Do not reduce cost by violating stated availability, performance, or security requirements**

---

# Right-Sizing

Underutilized resource?

→ Right-size

### Killer Exam Clue

> **EC2 consistently uses very little CPU**
>
> → **Choose smaller instance**

---

# EC2 Pricing Decision

## On-Demand

Think:

**Unpredictable**

## Savings Plans / Reserved Pricing

Think:

**Steady**

## Spot

Think:

**Interruptible**

### Memory Trick

> **Unpredictable**
> → On-Demand
>
> **Steady**
> → Commit
>
> **Interruptible**
> → Spot

---

# S3 Cost Optimization

Need:

**Automatic storage transitions**

→ Lifecycle Policy

Need:

**Unknown access pattern**

→ Intelligent-Tiering

Need:

**Archive**

→ Glacier class

### Killer Exam Principle

> **Retrieval time must still satisfy the requirement**

---

# NAT Gateway Cost

Private resources sending heavy traffic to:

**S3 or DynamoDB**

through NAT?

Consider:

**Gateway VPC Endpoint**

### Killer Exam Clue

> **Reduce NAT cost for heavy S3 traffic**
>
> → **S3 Gateway Endpoint**

---

# Disaster Recovery

DR strategy depends on:

**RPO + RTO**

### RPO

Think:

**Data Loss**

### RTO

Think:

**Downtime**

---

# Four DR Strategies

| Strategy | Think |
|---|---|
| Backup & Restore | Rebuild |
| Pilot Light | Start |
| Warm Standby | Scale |
| Multi-Site | Route |

### Killer Memory Trick

> **BACKUP**
> → BUILD
>
> **PILOT**
> → START
>
> **WARM**
> → SCALE
>
> **MULTI-SITE**
> → ROUTE

---

# Storage Architecture

Need:

**Object storage**

→ S3

Need:

**Block storage**

→ EBS

Need:

**Shared Linux filesystem**

→ EFS

Need:

**Specialized managed filesystem**

→ FSx

### Memory Trick

> **Object**
> → S3
>
> **Block**
> → EBS
>
> **File**
> → EFS / FSx

---

# Database Architecture

Need:

**Relational SQL**

→ RDS / Aurora

Need:

**Massive NoSQL key-value**

→ DynamoDB

Need:

**In-memory cache**

→ ElastiCache

Need:

**Analytics warehouse**

→ Redshift

### Memory Trick

**Data Model First**

**Database Second**

---

# Networking Architecture

Need:

**Public Internet access**

→ Internet Gateway

Need:

**Private IPv4 outbound Internet**

→ NAT Gateway

Need:

**Private S3 / DynamoDB**

→ Gateway Endpoint

Need:

**Private supported AWS service**

→ Interface Endpoint

Need:

**Two VPCs**

→ VPC Peering

Need:

**Many VPCs**

→ Transit Gateway

Need:

**One private service**

→ PrivateLink

---

# Hybrid Connectivity

Need:

**Quick encrypted on-prem connectivity**

→ Site-to-Site VPN

Need:

**Dedicated predictable connectivity**

→ Direct Connect

Need:

**Remote user access**

→ Client VPN

Need:

**Hybrid DNS**

→ Route 53 Resolver

---

# Performance Decision Map

Need:

**Global static acceleration**

→ CloudFront

Need:

**Application/database cache**

→ ElastiCache

Need:

**DynamoDB cache**

→ DAX

Need:

**More relational reads**

→ Read Replica

Need:

**Global static IP acceleration**

→ Global Accelerator

---

# Architecture Scenario 1 — Web Application

Requirement:

- Highly available
- Variable traffic
- Relational database

Think:

Users  
↓  
ALB  
↓  
Auto Scaling Across Multiple AZs  
↓  
RDS Multi-AZ

---

# Architecture Scenario 2 — Static Website

Requirement:

- Global users
- Static assets
- Low operations

Think:

CloudFront  
↓  
S3

---

# Architecture Scenario 3 — Serverless API

Requirement:

- Unpredictable traffic
- Minimal operations
- NoSQL

Think:

API Gateway  
↓  
Lambda  
↓  
DynamoDB

---

# Architecture Scenario 4 — Async Processing

Requirement:

- Traffic spikes
- Backend workers
- No message loss during temporary worker failure

Think:

Producer  
↓  
SQS  
↓  
Workers

---

# Architecture Scenario 5 — Fan-Out

Requirement:

One event must trigger:

- Billing
- Shipping
- Analytics

Think:

SNS  
↓  
Separate SQS Queues

---

# Architecture Scenario 6 — Global Application

Requirement:

- Global users
- Low latency
- Multi-Region database

Possible pattern:

Route 53 / Global Accelerator  
↓  
Regional Application Stacks  
↓  
Aurora Global Database or DynamoDB Global Tables

depending on:

**Data model**

---

# Architecture Scenario 7 — Private Three-Tier App

Internet  
↓  
Public ALB  
↓  
Private Application Subnets  
↓  
Private Database Subnets

### Security Pattern

ALB SG  
↓  
App SG  
↓  
DB SG

---

# Architecture Scenario 8 — Read-Heavy Database

Application repeatedly requests:

**The same records**

Think:

ElastiCache

If reads are:

**Varied but numerous**

Think:

Read Replica

---

# Architecture Scenario 9 — Region Failure

Application must survive:

**Complete Region outage**

Think:

**Multi-Region architecture**

Then determine DR strategy from:

**RPO / RTO**

---

# Architecture Scenario 10 — Lowest Operational Overhead

Question emphasizes:

**Minimal management**

Prefer:

- Managed services
- Serverless
- Automatic scaling
- Managed databases

over:

**Custom EC2 fleets**

when requirements allow.

---

# Major Exam Traps

## Trap 1 — Most Complex Answer Is Best

❌

Choose:

**Simplest answer meeting every requirement**

---

## Trap 2 — Multi-Region Is Always Needed for HA

❌

Often:

**Multi-AZ**

is sufficient.

---

## Trap 3 — RDS Multi-AZ Scales Reads

❌

Use:

**Read Replica**

---

## Trap 4 — Sticky Sessions Make App Stateless

❌

Externalize:

**State**

---

## Trap 5 — SNS Is a Queue

❌

SNS:

**Fan-Out**

SQS:

**Queue**

---

## Trap 6 — SQS Processes Messages

❌

Consumers:

**Process**

SQS:

**Stores**

---

## Trap 7 — Cache Replaces Database

❌

Database normally remains:

**System of Record**

---

## Trap 8 — Serverless Is Always Cheapest

❌

Usage pattern matters.

---

## Trap 9 — Spot Is Safe for Critical Non-Interruptible Work

❌

Spot can be:

**Interrupted**

---

## Trap 10 — Cheapest DR Strategy Is Always Correct

❌

Must satisfy:

**RPO + RTO**

---

# Ultimate Architecture Cheat Sheet

| Requirement | Think |
|---|---|
| AZ Failure | Multi-AZ |
| Region Failure | Multi-Region |
| Distribute Traffic | Load Balancer |
| Dynamic Compute | Auto Scaling |
| Stateless Scaling | Externalize State |
| Async Buffer | SQS |
| Fan-Out | SNS |
| Event Routing | EventBridge |
| Workflow | Step Functions |
| Global Cache | CloudFront |
| App/DB Cache | ElastiCache |
| DynamoDB Cache | DAX |
| Relational DB | RDS / Aurora |
| NoSQL | DynamoDB |
| Read Scaling | Read Replica |
| Minimal Ops | Serverless / Managed |
| Event Compute | Lambda |
| API Front Door | API Gateway |
| User Authentication | Cognito |
| Least Privilege | IAM |
| Encryption Keys | KMS |
| Secrets | Secrets Manager |
| Web Attacks | WAF |
| DDoS | Shield |
| Threat Detection | GuardDuty |
| Vulnerabilities | Inspector |
| PII in S3 | Macie |
| API Audit | CloudTrail |
| Network Metadata | VPC Flow Logs |
| Private S3 | Gateway Endpoint |
| Two VPCs | VPC Peering |
| Many VPCs | Transit Gateway |
| One Private Service | PrivateLink |
| Quick Hybrid Link | Site-to-Site VPN |
| Dedicated Hybrid Link | Direct Connect |
| RPO | Data Loss |
| RTO | Downtime |

---

# Master Architecture Decision Tree

> **WHAT IS THE PRIMARY REQUIREMENT?**
>
> ---
>
> **AVAILABILITY?**
>
> Instance failure
> → Auto Scaling
>
> AZ failure
> → Multi-AZ
>
> Region failure
> → Multi-Region
>
> ---
>
> **SCALABILITY?**
>
> Web compute
> → Load Balancer + Auto Scaling
>
> Worker backlog
> → SQS + Auto Scaling
>
> Database reads
> → Read Replica / Cache
>
> Serverless scale
> → Lambda / DynamoDB
>
> ---
>
> **DECOUPLING?**
>
> Buffer
> → SQS
>
> Fan-Out
> → SNS
>
> Event Routing
> → EventBridge
>
> Workflow
> → Step Functions
>
> ---
>
> **PERFORMANCE?**
>
> Global content
> → CloudFront
>
> Repeated DB reads
> → ElastiCache
>
> DynamoDB cache
> → DAX
>
> ---
>
> **SECURITY?**
>
> Identity
> → IAM
>
> Resource firewall
> → Security Group
>
> Subnet deny
> → NACL
>
> Keys
> → KMS
>
> Secrets
> → Secrets Manager
>
> Web attacks
> → WAF
>
> Threats
> → GuardDuty
>
> ---
>
> **COST?**
>
> Underutilized
> → Right-size
>
> Variable
> → Auto Scale
>
> Steady
> → Commitment pricing
>
> Interruptible
> → Spot
>
> Old S3 data
> → Lifecycle
>
> ---
>
> **DR?**
>
> Data loss
> → RPO
>
> Downtime
> → RTO
>
> Backups only
> → Backup and Restore
>
> Core running
> → Pilot Light
>
> Full stack small
> → Warm Standby
>
> Full stack full
> → Multi-Site

---

## Master Memory Trick

> [!tip] Architecture Master Memory Trick
> When the SAA exam gives you:
>
> **A giant paragraph**
>
> do not panic and start matching service names.
>
> Ask:
>
> **WHAT IS BROKEN OR WHAT NEEDS TO IMPROVE?**
>
> Too much traffic?
>
> → **SCALE**
>
> Backend overwhelmed?
>
> → **DECOUPLE**
>
> Same data repeatedly requested?
>
> → **CACHE**
>
> One component can fail everything?
>
> → **ADD REDUNDANCY**
>
> Too much operational work?
>
> → **MANAGED / SERVERLESS**
>
> Too expensive?
>
> → **RIGHT-SIZE / ELASTICITY**
>
> Security problem?
>
> → **IDENTITY + NETWORK + DATA + DETECTION**
>
> Region can fail?
>
> → **MULTI-REGION / DR**

So remember:

> **STATELESS**
> → REPLACEABLE
>
> **SQS**
> → BUFFER
>
> **SNS**
> → BROADCAST
>
> **EVENTBRIDGE**
> → ROUTE
>
> **CACHE**
> → AVOID REPEATED WORK
>
> **MULTI-AZ**
> → AVAILABILITY
>
> **AUTO SCALING**
> → ELASTICITY
>
> **SERVERLESS**
> → LOWER OPERATIONS
>
> **IAM**
> → IDENTITY
>
> **KMS**
> → ENCRYPTION
>
> **RPO**
> → DATA LOSS
>
> **RTO**
> → DOWNTIME

And the ultimate SAA rule:

> **Identify the requirement, eliminate answers that violate it, then choose the simplest and most cost-effective architecture that satisfies everything.**

---

## Related Notes

- [[Architecture Principles]]
- [[Stateless vs Stateful Architecture]]
- [[Decoupled Architecture]]
- [[Caching Architecture]]
- [[High Availability Architecture]]
- [[Scalable Architecture]]
- [[Cost-Optimized Architecture]]
- [[Secure Architecture]]
- [[Serverless Architecture]]
- [[Disaster Recovery Overview]]
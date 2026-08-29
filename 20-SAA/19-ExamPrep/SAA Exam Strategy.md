## Core Concept

The SAA exam is less about:

**Memorizing isolated AWS services**

and more about:

**Recognizing architecture patterns and eliminating wrong answers**

The strongest approach is:

1. Identify the requirement
2. Spot the key exam clue
3. Eliminate answers that violate constraints
4. Compare the final choices
5. Pick the simplest correct architecture

> [!tip] Memory Trick
> **Read for the Requirement, Not the Service Name**

---

# Read the Question in Layers

A long SAA question usually contains:

- Scenario
- Existing architecture
- Problem
- Business requirement
- Technical constraint
- Optimization goal

Do not treat every sentence as equally important.

### Killer Exam Principle

> **Find the sentence that changes the architecture**

---

# Look for Trigger Words

Certain phrases should immediately narrow your options.

Examples:

**Highly available**
→ Multi-AZ

**Most cost-effective**
→ Lowest-cost solution that still meets requirements

**Least operational overhead**
→ Managed / serverless

**Decouple**
→ SQS / messaging

**Global users**
→ CloudFront / Global Accelerator / Multi-Region

**Survive Region failure**
→ Multi-Region

**Read-heavy database**
→ Read Replica / Cache

**Private access**
→ VPC Endpoint / PrivateLink depending on context

---

# Identify the Primary Requirement

Some questions include many details, but only one requirement determines:

**The best answer**

Example:

Application must:

- Be secure
- Handle traffic
- Use relational data
- Recover within 30 seconds

The standout requirement may be:

**30-second recovery**

That can eliminate:

- Backup and Restore
- Pilot Light

### Memory Trick

**The Tightest Constraint Usually Drives the Design**

---

# Requirement Types

Common requirement categories:

- Availability
- Scalability
- Performance
- Security
- Cost
- Operational overhead
- Disaster recovery
- Data durability
- Network connectivity

### Exam Principle

> **Classify the problem before choosing the service**

---

# Eliminate Impossible Answers First

Instead of trying to prove one answer correct immediately:

**Remove answers that clearly violate AWS behavior**

Examples:

VPC Peering with overlapping CIDRs  
→ Eliminate

Security Group explicit deny  
→ Eliminate

RDS Multi-AZ for read scaling  
→ Eliminate

NAT Gateway in private subnet for Internet egress  
→ Eliminate

### Memory Trick

**Wrong Answers Often Contain One Fatal Flaw**

---

# The "Most" and "Least" Words

Pay close attention to words such as:

- MOST cost-effective
- LEAST operational overhead
- MOST resilient
- LEAST complex
- MOST secure

These tell you:

**How to rank technically valid answers**

### Killer Exam Principle

> **Two answers may work, but only one best matches the optimization word**

---

# Cost-Effective

If the question says:

**Most cost-effective**

do NOT automatically choose:

**The cheapest-looking component**

Choose:

**The lowest-cost architecture that still satisfies every requirement**

### Example

Need:

- Highly available database
- Automatic failover

Single-AZ RDS is cheaper.

But it fails:

**The availability requirement**

Therefore it is:

**Wrong**

---

# Least Operational Overhead

When you see:

**Least operational overhead**

prefer:

- Managed services
- Serverless services
- Automatic scaling
- Built-in HA

over:

- Custom EC2 fleets
- Self-managed clusters
- Manual scripts

### Killer Shortcut

> **AWS Manages More**
>
> → Usually Less Operational Overhead

---

# Highly Available

If the requirement is:

**Highly available**

look for:

- Multiple AZs
- Load balancing
- Auto Scaling
- Automatic database failover
- Managed multi-AZ services

### Killer Exam Trap

One very large EC2 instance:

**Is still one instance**

---

# Fault Tolerant

Fault tolerance implies:

**The system continues operating despite failure**

This usually requires:

**More redundancy**

than a design that simply:

**Recovers quickly**

### Exam Principle

> **Fault tolerance is stronger than basic recovery**

---

# Scalability

When you see:

- Unpredictable traffic
- Millions of users
- Bursts
- Growing workload

think:

- Horizontal scaling
- Auto Scaling
- Serverless
- DynamoDB
- SQS
- Caching

depending on:

**The bottleneck**

---

# Find the Bottleneck

Do not scale everything.

Ask:

**Which layer is failing?**

Examples:

Web CPU high  
→ Scale compute

DB read load high  
→ Read Replica / Cache

Workers falling behind  
→ SQS + more workers

Static origin overloaded  
→ CloudFront

### Memory Trick

**Scale the Bottleneck**

---

# Read vs Write Problems

This distinction appears frequently.

## Read Problem

Think:

- Read Replica
- ElastiCache
- DAX
- CloudFront

## Write Problem

Think:

- Queue buffering
- DynamoDB scaling
- Partition design
- Write-capable architecture

### Killer Exam Principle

> **A read solution may not solve a write bottleneck**

---

# High Availability vs Read Scaling

A classic exam trap:

[[RDS]] Multi-AZ  
→ High Availability

Read Replica  
→ Read Scaling

### Killer Memory Trick

> **MULTI-AZ = SURVIVE**
>
> **READ REPLICA = READ**

---

# Synchronous vs Asynchronous

If the user does not need the result:

**Immediately**

think:

**Asynchronous processing**

Possible pattern:

Application  
↓  
SQS  
↓  
Workers

### Killer Exam Clue

> **Long-running processing should not block user request**
>
> → **Decouple**

---

# SQS vs SNS vs EventBridge

## SQS

Think:

**Buffer / Queue**

## SNS

Think:

**Fan-Out / Broadcast**

## EventBridge

Think:

**Event Routing**

### Master Memory Trick

> **SQS = HOLD**
>
> **SNS = SEND TO MANY**
>
> **EVENTBRIDGE = ROUTE**

---

# Standard vs FIFO

Need:

**Maximum throughput**

and strict ordering is not required:

→ SQS Standard

Need:

**Strict message order**

→ SQS FIFO

### Killer Exam Clue

> **Order must be preserved**
>
> → **FIFO**

---

# Visibility Timeout

If SQS messages are being:

**Processed twice**

and processing takes longer than:

**Visibility Timeout**

increase:

**Visibility Timeout**

### Memory Trick

**Hide Message Long Enough to Finish**

---

# DLQ

Repeatedly failing message?

→ Dead-Letter Queue

### Killer Exam Clue

> **Need to isolate poison messages**
>
> → **DLQ**

---

# Stateless vs Stateful

If the application must scale horizontally:

Prefer:

**Stateless compute**

Store state externally in:

- ElastiCache
- DynamoDB
- RDS
- S3
- EFS

### Killer Exam Principle

> **Any app instance should be disposable**

---

# Sticky Sessions Trap

Sticky sessions can help:

**Stateful applications**

but they do not make:

**The application stateless**

If the question asks for a more scalable design:

Think:

**Externalize state**

---

# Storage Recognition

Need:

**Object storage**
→ S3

Need:

**Block storage**
→ EBS

Need:

**Shared Linux file system**
→ EFS

Need:

**Specialized file system**
→ FSx

### Memory Trick

> **OBJECT**
> → S3
>
> **BLOCK**
> → EBS
>
> **FILE**
> → EFS / FSx

---

# Database Recognition

Need:

**Relational SQL**
→ RDS / Aurora

Need:

**Massive key-value**
→ DynamoDB

Need:

**In-memory**
→ ElastiCache

Need:

**Analytics warehouse**
→ Redshift

### Exam Principle

> **Choose database by access pattern, not popularity**

---

# Aurora vs RDS

Think Aurora when the question emphasizes:

- Higher relational scalability
- Aurora replicas
- Global Database
- Aurora Serverless

Think standard RDS when:

**Managed relational database**

is sufficient without Aurora-specific requirements.

---

# DynamoDB

Think DynamoDB when you see:

- Serverless NoSQL
- Key-value
- Massive scale
- Millisecond latency
- Global Tables
- Streams

### Killer Exam Clue

> **Unpredictable key-value workload with minimal administration**
>
> → **DynamoDB**

---

# Cache Recognition

Need:

**Global edge cache**
→ CloudFront

Need:

**Application/database cache**
→ ElastiCache

Need:

**DynamoDB cache**
→ DAX

Need:

**API response cache**
→ API Gateway Cache

---

# Network Recognition

Need:

**Public Internet**
→ Internet Gateway

Need:

**Private subnet outbound IPv4 Internet**
→ NAT Gateway

Need:

**Private S3/DynamoDB**
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

# VPC Peering Trap

VPC Peering is:

**Non-transitive**

A ↔ B  
B ↔ C

does NOT mean:

A ↔ C

### Killer Shortcut

**Many VPCs + Transitive**
→ Transit Gateway

---

# PrivateLink Recognition

Think PrivateLink when:

- One private service
- Many consumers
- No full network connectivity
- Overlapping CIDRs may exist

### Memory Trick

**PrivateLink = Service**

**Peering = Network**

---

# Security Group vs NACL

## Security Group

- Stateful
- Resource-level
- Allow only

## NACL

- Stateless
- Subnet-level
- Allow + deny

### Killer Shortcut

**Explicit Deny**
→ NACL

---

# IAM Recognition

Need:

**AWS API permissions**
→ IAM

Need:

**Workload access without stored credentials**
→ IAM Role

Need:

**Organization guardrail**
→ SCP

Need:

**Workforce multi-account access**
→ IAM Identity Center

---

# Encryption Recognition

Need:

**Encryption keys**
→ KMS

Need:

**Dedicated HSM**
→ CloudHSM

Need:

**Secret + rotation**
→ Secrets Manager

Need:

**TLS certificate**
→ ACM

---

# Security Services Recognition

Need:

**SQL injection**
→ WAF

Need:

**DDoS**
→ Shield

Need:

**Threat detection**
→ GuardDuty

Need:

**Known vulnerabilities**
→ Inspector

Need:

**PII in S3**
→ Macie

Need:

**Central findings**
→ Security Hub

Need:

**Configuration compliance**
→ Config

---

# Logging Recognition

Need:

**Who made the API call?**
→ CloudTrail

Need:

**Metrics / logs / alarms**
→ CloudWatch

Need:

**Network ACCEPT / REJECT**
→ VPC Flow Logs

### Memory Trick

> **CloudTrail = WHO**
>
> **CloudWatch = HOW**
>
> **Flow Logs = NETWORK**

---

# Hybrid Networking Recognition

Need:

**Quick encrypted on-prem connection**
→ Site-to-Site VPN

Need:

**Dedicated predictable on-prem connection**
→ Direct Connect

Need:

**Remote individual user**
→ Client VPN

Need:

**Hybrid DNS**
→ Route 53 Resolver

---

# Route 53 Resolver Direction

On-Prem  
→ AWS DNS

= **Inbound**

AWS  
→ On-Prem DNS

= **Outbound**

### Memory Trick

**Direction is from AWS's point of view**

---

# Disaster Recovery Recognition

Need:

**Data loss tolerance**
→ RPO

Need:

**Downtime tolerance**
→ RTO

### Memory Trick

**RPO = Data**

**RTO = Time**

---

# DR Strategy Recognition

Backups only  
→ Backup and Restore

Core running  
→ Pilot Light

Full stack running small  
→ Warm Standby

Full stack running full  
→ Multi-Site

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

# Region Failure vs AZ Failure

Need survive:

**AZ failure**

→ Multi-AZ

Need survive:

**Region failure**

→ Multi-Region

### Killer Exam Trap

> **RDS Multi-AZ does not protect against complete Region failure**

---

# Cost Recognition

Need:

**Unpredictable EC2**
→ On-Demand

Need:

**Steady compute**
→ Savings Plans / Reserved pricing

Need:

**Interruptible**
→ Spot

Need:

**Variable capacity**
→ Auto Scaling

Need:

**Aging S3 data**
→ Lifecycle Policy

Need:

**Unknown S3 access pattern**
→ Intelligent-Tiering

---

# Spot Trap

Spot is great for:

- Batch
- Stateless workers
- Flexible workloads

But not as the only option for:

**Critical non-interruptible work**

unless interruption is handled.

---

# Serverless Recognition

Need:

**Event-driven compute**
→ Lambda

Need:

**Managed API**
→ API Gateway

Need:

**NoSQL**
→ DynamoDB

Need:

**Workflow**
→ Step Functions

Need:

**User authentication**
→ Cognito

### Killer Exam Clue

> **Minimal operational overhead**
>
> → Strongly consider managed/serverless

---

# Step Functions vs EventBridge

Step Functions:

**Orchestrate sequence**

EventBridge:

**Route events**

### Memory Trick

**EventBridge = Where**

**Step Functions = What Next**

---

# Common Wrong-Answer Pattern 1

The answer provides:

**More availability than required**

but at much higher cost.

If question asks:

**Most cost-effective**

and a simpler answer satisfies:

**All requirements**

choose:

**The simpler option**

---

# Common Wrong-Answer Pattern 2

The answer solves:

**A different problem**

Example:

Requirement:

Read scaling

Answer:

RDS Multi-AZ

Multi-AZ is useful.

But it solves:

**Availability**

not:

**Read scaling**

---

# Common Wrong-Answer Pattern 3

The answer is technically possible but requires:

**More manual operations**

Question asks:

**Least operational overhead**

Prefer:

**Managed alternative**

---

# Common Wrong-Answer Pattern 4

The answer contains:

**One impossible AWS behavior**

Example:

Security Group deny rule.

Even if everything else sounds good:

**Eliminate it**

---

# Common Wrong-Answer Pattern 5

The answer ignores:

**One keyword**

Example:

Requirement says:

**Private connectivity**

Answer sends traffic through:

**Public Internet**

Likely wrong if a private AWS-native option exists.

---

# Common Wrong-Answer Pattern 6

The answer ignores:

**Scale**

Example:

Single EC2 instance

for:

**Millions of unpredictable requests**

Likely wrong.

---

# Common Wrong-Answer Pattern 7

The answer ignores:

**Failure domain**

Example:

Multiple EC2 instances

all in:

**One AZ**

Question requires:

**AZ resilience**

Still wrong.

---

# Answer Elimination Process

For each option ask:

1. Does it actually work?
2. Does it meet availability?
3. Does it meet performance?
4. Does it meet security?
5. Does it satisfy RPO/RTO?
6. Does it meet cost requirement?
7. Does it meet operational-overhead requirement?

If any critical answer is:

**NO**

eliminate it.

---

# Two-Answer Tie Breaker

If two answers both work:

Ask which one better matches:

**The optimization phrase**

Example:

Both are secure and highly available.

Question says:

**Least operational overhead**

Choose the one with:

**More managed services**

---

# Watch for Absolute Words

Words such as:

- MUST
- NEVER
- ONLY
- ALL
- NO data loss
- NO downtime

can dramatically tighten:

**Architecture requirements**

### Exam Principle

> **Absolute requirements eliminate flexible compromises**

---

# No Data Loss

If requirement says:

**No data loss**

a backup every hour:

**Does not satisfy it**

You need an architecture with:

**Much stronger replication/durability guarantees**

depending on workload.

---

# No Downtime

If requirement truly requires:

**Near-zero interruption**

Backup and Restore:

**Clearly fails**

Think:

**More active infrastructure**

such as Multi-Site depending on requirements.

---

# Exam Time Management

Do not spend too long trying to prove:

**Every option wrong**

Once you identify:

**The clear architecture pattern**

choose and move on.

### Memory Trick

**Recognize → Eliminate → Select**

---

# Flag Difficult Questions

If a question remains unclear:

1. Eliminate obvious wrong answers
2. Make the best choice
3. Flag it
4. Return later if time remains

### Exam Principle

> **Do not let one difficult question steal time from many easier questions**

---

# First-Pass Strategy

On the first pass:

Answer questions where the pattern is:

**Clear**

Flag questions that require:

**More comparison**

This helps preserve:

**Exam momentum**

---

# Read Every Answer Carefully

A wrong answer often differs from the correct one by:

**One word**

Example:

Correct:

Gateway Endpoint for S3

Wrong:

Interface Endpoint when exam specifically expects the lower-cost Gateway pattern

### Killer Exam Principle

> **Read the entire option, not just the service names**

---

# Watch for Composite Answers

Some correct answers require:

**Multiple AWS services**

Example:

Highly available scalable web app:

ALB  
+  
Auto Scaling  
+  
Multi-AZ

Do not assume the answer must be:

**One service**

---

# Architecture Layers

When stuck, break the problem into layers.

## Traffic Layer

- Route 53
- CloudFront
- Global Accelerator
- Load Balancer

## Compute Layer

- EC2
- Lambda
- ECS/EKS

## Messaging Layer

- SQS
- SNS
- EventBridge

## Data Layer

- RDS/Aurora
- DynamoDB
- S3

## Security Layer

- IAM
- SG
- WAF
- KMS

### Memory Trick

**Break the Big Architecture Into Small Decisions**

---

# Sample Scenario 1

Requirement:

- Global users
- Static assets
- Low latency
- Reduce origin load

Recognition:

Global + Static + Cache

Answer:

**CloudFront**

---

# Sample Scenario 2

Requirement:

- Web traffic unpredictable
- EC2 application
- Must survive instance failure

Recognition:

Elastic compute + HA

Answer pattern:

**ALB + Auto Scaling**

across:

**Multiple AZs**

---

# Sample Scenario 3

Requirement:

- Order request accepted immediately
- Processing takes minutes
- Backend may become overloaded

Recognition:

Asynchronous + buffer

Answer:

**SQS**

---

# Sample Scenario 4

Requirement:

- RDS primary overloaded by reporting queries
- Need more read capacity

Recognition:

Read scaling

Answer:

**Read Replica**

not:

**Multi-AZ**

---

# Sample Scenario 5

Requirement:

- Private EC2
- Needs S3
- Reduce NAT charges

Recognition:

Private S3 + cost

Answer:

**S3 Gateway Endpoint**

---

# Sample Scenario 6

Requirement:

- Remote employee
- Secure VPC access

Recognition:

Individual user

Answer:

**Client VPN**

---

# Sample Scenario 7

Requirement:

- On-premises network
- Encrypted AWS connectivity
- Needed quickly

Recognition:

Hybrid + quick + encrypted

Answer:

**Site-to-Site VPN**

---

# Sample Scenario 8

Requirement:

- On-premises
- Predictable bandwidth
- Dedicated connection

Recognition:

Dedicated hybrid

Answer:

**Direct Connect**

---

# Sample Scenario 9

Requirement:

- Survive complete Region outage
- Full environment already running small

Recognition:

Region DR + reduced-capacity full stack

Answer:

**Warm Standby**

---

# Sample Scenario 10

Requirement:

- One event
- Billing
- Shipping
- Analytics
- Each consumer processes independently

Recognition:

Fan-Out + buffering

Answer:

**SNS + SQS**

---

# Most Important Service Pairs

## Multi-AZ vs Read Replica

Availability  
vs  
Read Scaling

---

## SQS vs SNS

Queue  
vs  
Broadcast

---

## CloudFront vs Global Accelerator

Content/HTTP Edge Cache  
vs  
Network Acceleration + Static Anycast IPs

---

## Security Group vs NACL

Stateful Resource  
vs  
Stateless Subnet

---

## VPN vs Direct Connect

Quick Encrypted Internet  
vs  
Dedicated Predictable Connection

---

## VPC Peering vs Transit Gateway

Two VPCs  
vs  
Many VPCs

---

## Peering vs PrivateLink

Network Connectivity  
vs  
Service Connectivity

---

## KMS vs Secrets Manager

Encryption Keys  
vs  
Secrets

---

## GuardDuty vs Inspector

Threat Detection  
vs  
Vulnerability Detection

---

## CloudWatch vs CloudTrail

Monitoring  
vs  
API Audit

---

# Ultimate Recognition Table

| Exam Clue | Think |
|---|---|
| AZ Failure | Multi-AZ |
| Region Failure | Multi-Region |
| Read Scaling | Read Replica |
| Repeated Reads | Cache |
| Buffer | SQS |
| Fan-Out | SNS |
| Event Routing | EventBridge |
| Workflow | Step Functions |
| Global Static | CloudFront |
| Dynamic EC2 Scale | Auto Scaling |
| Stateless | Externalize State |
| Relational | RDS / Aurora |
| NoSQL | DynamoDB |
| Object Storage | S3 |
| Shared Files | EFS |
| Private S3 | Gateway Endpoint |
| Many VPCs | Transit Gateway |
| One Private Service | PrivateLink |
| Quick Hybrid | Site-to-Site VPN |
| Dedicated Hybrid | Direct Connect |
| User VPN | Client VPN |
| Threat Detection | GuardDuty |
| CVEs | Inspector |
| PII | Macie |
| API Audit | CloudTrail |
| Data Loss | RPO |
| Downtime | RTO |
| Lowest DR Cost | Backup & Restore |
| Core Running | Pilot Light |
| Full Stack Small | Warm Standby |
| Full Stack Full | Multi-Site |

---

# Final Exam Rapid-Fire

> **READ THE REQUIREMENT**
> → FIRST
>
> **ELIMINATE IMPOSSIBLE AWS BEHAVIOR**
> → SECOND
>
> **MATCH THE OPTIMIZATION WORD**
> → THIRD
>
> **AZ FAILURE**
> → MULTI-AZ
>
> **REGION FAILURE**
> → MULTI-REGION
>
> **READ SCALE**
> → READ REPLICA
>
> **REPEATED READ**
> → CACHE
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
> **PRIVATE S3**
> → GATEWAY ENDPOINT
>
> **TWO VPCs**
> → PEERING
>
> **MANY VPCs**
> → TRANSIT GATEWAY
>
> **ONE SERVICE**
> → PRIVATELINK
>
> **RPO**
> → DATA LOSS
>
> **RTO**
> → DOWNTIME

---

## Master Memory Trick

> [!tip] SAA Exam Strategy Master Memory Trick
> Imagine every question is:
>
> **A detective case**
>
> The long scenario gives you:
>
> **A lot of noise**
>
> Your job is to find:
>
> **THE CLUE THAT MATTERS**
>
> First ask:
>
> **What does the business NEED?**
>
> Then:
>
> **What is the bottleneck or failure?**
>
> Then:
>
> **Which answers violate AWS rules?**
>
> Remove them.
>
> Then:
>
> **Which remaining answer best matches the optimization word?**

So remember:

> **REQUIREMENT**
> → FIND IT
>
> **KEYWORD**
> → USE IT
>
> **IMPOSSIBLE ANSWER**
> → ELIMINATE IT
>
> **BOTTLENECK**
> → FIX IT
>
> **MOST / LEAST**
> → USE AS TIEBREAKER
>
> **SIMPLE + CORRECT**
> → USUALLY WINS

And the ultimate exam question to ask yourself:

> **"Why is this answer better than the other technically possible answer?"**

The reason is usually one of:

- Lower cost
- Higher availability
- Better scalability
- Lower latency
- Better security
- Lower operational overhead

---

## Related Notes

- [[Architecture Principles]]
- [[18-Architecture Cheat Sheet]]
- [[High Availability Architecture]]
- [[Scalable Architecture]]
- [[Cost-Optimized Architecture]]
- [[Secure Architecture]]
- [[Serverless Architecture]]
- [[Disaster Recovery Overview]]
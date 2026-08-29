## Core Concept

Cost-optimized architecture means:

**Meeting business and technical requirements without paying for unnecessary capacity, services, or data movement**

The goal is NOT:

**Always choose the cheapest service**

The goal is:

**Choose the lowest-cost architecture that still satisfies all requirements**

> [!tip] Memory Trick
> **Cost Optimization = Meet the Requirement Without Overbuilding**

---

# Start With the Requirement

Before reducing cost, ask:

- What availability is required?
- What performance is required?
- What RPO/RTO is required?
- What security is required?
- What traffic pattern exists?
- What operational effort is acceptable?

### Killer Exam Principle

> **Never sacrifice a stated requirement just to reduce cost**

---

# Cost vs Architecture

Two architectures may both work.

Example:

Option A:

20 EC2 instances running all day

Option B:

Auto Scaling from 4 to 20 as demand changes

If traffic is variable:

Option B may provide:

**Better cost efficiency**

### Memory Trick

**Don't Pay for Idle Capacity**

---

# Right-Sizing

Right-sizing means selecting:

**The appropriate resource size for the workload**

Example:

Application uses:

10% CPU

on:

`m7i.4xlarge`

A smaller instance may provide:

**Lower cost**

while still meeting:

**Performance requirements**

### Killer Exam Clue

> **EC2 instances are consistently underutilized**
>
> → **Right-size the instances**

---

# Vertical Overprovisioning

A common anti-pattern:

**Choose a huge instance "just in case"**

This creates:

- Idle capacity
- Higher cost
- Poor resource utilization

Better:

**Measure and right-size**

---

# Auto Scaling

[[Auto Scaling]] improves cost efficiency by:

**Matching compute capacity to demand**

Traffic increases:

→ Scale Out

Traffic decreases:

→ Scale In

### Killer Exam Clue

> **Workload demand changes throughout the day**
>
> → **Auto Scaling**

### Memory Trick

**Use Capacity Only When Needed**

---

# Auto Scaling vs Fixed Fleet

## Fixed Fleet

Runs:

**The same capacity all the time**

Good when:

**Demand is steady**

## Auto Scaling

Better when:

**Demand changes**

### Exam Principle

> **Elasticity can reduce idle compute cost**

---

# On-Demand Instances

On-Demand EC2 is useful for:

- Short-term workloads
- Unpredictable workloads
- No commitment
- Flexible capacity

### Killer Exam Clue

> **Workload is unpredictable and cannot commit long term**
>
> → **On-Demand**

---

# Savings Plans

Savings Plans can reduce compute cost for:

**Predictable sustained usage**

in exchange for:

**A usage commitment**

### Killer Exam Clue

> **Company has steady long-term compute usage and wants lower cost**
>
> → **Savings Plans**

---

# Reserved Instances

Reserved pricing can reduce cost for:

**Predictable long-running EC2/RDS workloads**

depending on service and purchasing model.

### Memory Trick

**Steady Workload = Commitment Discount**

---

# Spot Instances

Spot Instances provide:

**Large discounts**

in exchange for:

**Interruption risk**

Best for:

- Batch processing
- Stateless workers
- CI/CD
- Flexible jobs
- Distributed processing

### Killer Exam Clue

> **Fault-tolerant workload can handle interruptions and needs lowest EC2 cost**
>
> → **Spot Instances**

---

# Spot Exam Trap

Do NOT choose Spot as the only capacity for:

**Critical non-interruptible workload**

unless the architecture explicitly:

**Handles interruptions**

### Memory Trick

**Spot = Cheap but Interruptible**

---

# Mixed Instance Strategy

A resilient cost-optimized architecture may combine:

**On-Demand + Spot**

Example:

Auto Scaling Group  
↓  
Base On-Demand Capacity  
+  
Spot Burst Capacity

This balances:

- Reliability
- Cost

### Killer Exam Principle

> **Not every workload must use only one EC2 purchasing model**

---

# Serverless

Serverless services can reduce cost when:

**Workloads are intermittent or highly variable**

Examples:

- [[Lambda]]
- [[API Gateway]]
- [[DynamoDB]] On-Demand
- S3
- SQS

### Killer Exam Clue

> **Application receives infrequent unpredictable requests and should avoid paying for idle servers**
>
> → **Serverless**

---

# Lambda Cost Model

Lambda generally charges based on:

**Invocations and execution**

rather than:

**Running a server continuously**

This can be cost-effective for:

- Sporadic jobs
- Event-driven workloads
- Variable APIs

### Exam Principle

> **Don't run EC2 24/7 for work that happens occasionally**

---

# Serverless Is Not Always Cheapest

For:

**Constant high-volume workloads**

always-on infrastructure may sometimes be more cost-efficient.

### Killer Exam Principle

> **Match the billing model to the usage pattern**

---

# Storage Cost Optimization

Different storage classes exist because:

**Not all data needs the same access pattern**

Use the storage tier that matches:

- Access frequency
- Retrieval speed
- Durability requirements
- Retention period

---

# S3 Storage Classes

[[S3]] provides multiple storage classes.

Think broadly:

## Frequently Accessed

→ S3 Standard

## Infrequently Accessed

→ Standard-IA / One Zone-IA depending on requirements

## Archive

→ Glacier classes

### Killer Exam Clue

> **Old data is rarely accessed but must be retained**
>
> → **Move to lower-cost storage class**

---

# S3 Lifecycle Policies

Lifecycle rules automate:

**Storage-class transitions and expiration**

Architecture:

New Object  
↓  
S3 Standard

After 30 days  
↓  
Standard-IA

After 180 days  
↓  
Glacier

### Killer Exam Clue

> **Automatically reduce S3 storage cost as data ages**
>
> → **Lifecycle Policy**

---

# S3 Intelligent-Tiering

S3 Intelligent-Tiering can automatically move data between:

**Access tiers**

when:

**Access patterns are unknown or changing**

### Killer Exam Clue

> **Cannot predict which S3 objects will be frequently accessed**
>
> → **Intelligent-Tiering**

---

# Glacier Cost Tradeoff

Archive storage can be:

**Very inexpensive**

but retrieval may involve:

- Delay
- Retrieval charges

### Exam Principle

> **Do not choose archival storage if recovery/access requirements need immediate retrieval**

---

# EBS Cost Optimization

[[EBS]] cost depends on:

- Volume type
- Provisioned size
- Performance
- IOPS/throughput configuration

### Killer Exam Principle

> **Choose the EBS volume type based on performance requirements, not habit**

---

# gp3

For many general-purpose workloads:

**gp3**

can provide:

**Cost-effective SSD storage**

with independently configurable performance.

### Killer Exam Clue

> **General-purpose SSD workload needs lower cost with configurable IOPS/throughput**
>
> → **gp3**

---

# EBS Snapshot Lifecycle

Old EBS snapshots can create:

**Unnecessary storage cost**

Use:

- Snapshot retention policies
- Data Lifecycle Manager
- AWS Backup

to manage:

**Snapshot lifecycle**

---

# Database Cost Optimization

Database cost can often be reduced through:

- Right-sizing
- Reserved pricing
- Aurora Serverless
- Read scaling appropriately
- Caching
- DynamoDB capacity-mode selection

---

# Read Replicas

Do not scale the primary relational database vertically when the issue is:

**Read traffic**

Use:

**Read Replicas**

when appropriate.

### Killer Exam Principle

> **Scale the bottleneck, not everything**

---

# Caching

[[Caching Architecture]] can reduce:

**Repeated backend work**

Example:

Application  
↓  
ElastiCache  
↓  
Database

This can reduce:

- DB CPU
- Read load
- Required database size

### Killer Exam Clue

> **Same database queries are repeatedly executed**
>
> → **Cache the results**

---

# DynamoDB On-Demand

[[DynamoDB]] On-Demand works well when:

**Traffic is unpredictable**

because you do not provision:

**Fixed read/write capacity**

### Killer Shortcut

Unpredictable  
→ On-Demand

Predictable steady traffic  
→ Provisioned capacity may be more cost-effective

---

# DynamoDB Provisioned Capacity

For predictable workloads:

**Provisioned capacity**

with Auto Scaling can provide:

**Cost control**

while still adjusting within expected ranges.

---

# Data Transfer Cost

Data movement can create significant:

**Architecture cost**

Common sources include:

- Cross-AZ transfer
- Cross-Region transfer
- NAT Gateway processing
- Internet egress

### Killer Exam Principle

> **Always notice where the traffic flows**

---

# Cross-AZ Traffic

Traffic crossing:

**Availability Zones**

can incur:

**Data transfer charges**

depending on service/path.

This does NOT mean:

**Avoid Multi-AZ when HA is required**

It means:

**Avoid unnecessary cross-AZ traffic**

### Memory Trick

**Don't Sacrifice HA to Save Pennies**

---

# NAT Gateway Cost

NAT Gateway can include:

- Hourly charge
- Data processing charge

If private workloads send large amounts of traffic to:

**AWS services**

using NAT, there may be:

**A cheaper private path**

---

# VPC Endpoints for Cost Optimization

[[VPC Endpoints]] can reduce NAT Gateway usage.

Example:

Private EC2  
↓  
NAT Gateway  
↓  
S3

Better:

Private EC2  
↓  
S3 Gateway Endpoint  
↓  
S3

### Killer Exam Clue

> **Large private-subnet S3 traffic creates high NAT Gateway charges**
>
> → **S3 Gateway Endpoint**

---

# Gateway Endpoints

Gateway Endpoints are especially important for:

- S3
- DynamoDB

They can provide:

**Private service access**

without routing those requests through:

**NAT Gateway**

### Memory Trick

**S3/DynamoDB Traffic? Avoid NAT When Endpoint Fits**

---

# Interface Endpoint Cost

Interface Endpoints can reduce NAT dependency but usually have:

- Hourly cost
- Data processing cost

Therefore:

**Interface Endpoint is not automatically cheaper**

### Exam Principle

> **Compare access pattern and traffic volume**

---

# CloudFront Cost Optimization

[[CloudFront]] can reduce:

**Origin traffic**

by serving cached content from:

**Edge locations**

This can reduce:

- Origin load
- Repeated origin requests
- Certain data-transfer costs depending on architecture

### Killer Exam Clue

> **Global users repeatedly download the same content from S3 or ALB**
>
> → **CloudFront**

---

# Caching Saves Backend Capacity

Caching may allow you to run:

**Smaller backend infrastructure**

because fewer requests reach:

- Databases
- Application servers
- Origins

### Memory Trick

**Cheapest Request = One You Don't Have to Recompute**

---

# SQS and Cost Optimization

[[SQS]] can help smooth:

**Traffic spikes**

Instead of provisioning workers for:

**Maximum possible burst**

you can:

Queue work  
↓  
Process gradually  
↓  
Scale workers as needed

### Killer Exam Principle

> **Buffering can reduce the need to permanently provision for peak load**

---

# Scheduled Scaling

If demand is:

**Predictable**

Scheduled Scaling can add capacity:

**Before the peak**

and remove it:

**Afterward**

### Killer Exam Clue

> **Traffic increases every weekday at 8 AM**
>
> → **Scheduled Scaling**

---

# Predictive Scaling

Predictive Scaling can forecast:

**Recurring usage patterns**

and prepare capacity in advance.

This can improve:

- Performance
- Cost efficiency

when patterns are:

**Consistent**

---

# Reserved Capacity for Databases

Steady RDS usage may benefit from:

**Reserved DB Instances**

when long-term usage is predictable.

### Memory Trick

**Steady Database = Consider Commitment**

---

# Aurora Serverless

Aurora Serverless can be useful for:

**Variable or intermittent relational workloads**

because database capacity can:

**Adjust with demand**

### Killer Exam Clue

> **Relational workload is highly variable and should avoid permanently provisioned database capacity**
>
> → **Aurora Serverless**

---

# Shut Down Non-Production Resources

Development/test environments may not need to run:

**24/7**

Cost can be reduced through:

- Scheduling
- Automation
- Temporary environments

### Killer Exam Principle

> **Non-production does not automatically need production-level uptime**

---

# Managed Services and Cost

Managed services may appear more expensive than:

**Raw infrastructure**

but they can reduce:

- Administration
- Patching
- Backup work
- HA engineering
- Operational staffing

### Exam Principle

> **Cost includes operational burden, not only hourly resource price**

---

# Operational Overhead

If the question says:

**Most cost-effective with minimum operational overhead**

do not automatically choose:

**The cheapest self-managed EC2 solution**

A managed service may be:

**The better total-cost architecture**

---

# Multi-AZ Cost

Multi-AZ usually costs more than:

**Single-AZ**

but if the requirement says:

**Highly available**

you cannot remove redundancy merely to:

**Reduce cost**

### Killer Exam Principle

> **First satisfy availability. Then optimize cost within that constraint.**

---

# Disaster Recovery Cost

DR strategies have different ongoing costs.

From lower to higher:

Backup & Restore  
↓  
Pilot Light  
↓  
Warm Standby  
↓  
Multi-Site

### Killer Shortcut

**Cheapest acceptable RTO/RPO strategy wins**

---

# Backup and Restore

[[Backup and Restore]] is generally:

**The lowest-cost DR strategy**

but has:

**The longest recovery time**

Choose it only when:

**RTO/RPO permit it**

---

# Multi-Site

[[Multi-Site]] provides:

**Very fast recovery**

but requires:

**More continuously running infrastructure**

Therefore:

**Higher ongoing cost**

### Exam Principle

> **Do not choose Multi-Site if business requirements do not justify it**

---

# Cost Allocation

Tags can help organizations:

**Track resource ownership and spending**

Examples:

- Project
- Environment
- Department
- Cost Center

### Killer Exam Clue

> **Need to understand which team is generating AWS spend**
>
> → **Cost Allocation Tags**

---

# AWS Budgets

AWS Budgets can alert when:

**Costs or usage exceed thresholds**

### Killer Exam Clue

> **Notify team when monthly AWS spend approaches a limit**
>
> → **AWS Budgets**

---

# Cost Explorer

Cost Explorer helps:

**Analyze historical spending and usage trends**

### Killer Exam Clue

> **Need to visualize AWS spending trends**
>
> → **Cost Explorer**

---

# Compute Optimizer

AWS Compute Optimizer can provide recommendations for:

**Resource right-sizing**

based on utilization patterns.

### Killer Exam Clue

> **Need recommendations for underutilized EC2 resources**
>
> → **Compute Optimizer**

---

# Trusted Advisor

Trusted Advisor can provide recommendations related to:

- Cost optimization
- Security
- Performance
- Fault tolerance
- Service limits

### Exam Recognition

> **AWS best-practice recommendations across multiple categories**
>
> → **Trusted Advisor**

---

# Architecture Thinking

## Scenario 1 — Variable Web Traffic

Website has:

Large daytime traffic

and:

Very little overnight traffic.

Choose:

**Auto Scaling**

rather than peak capacity 24/7.

---

## Scenario 2 — Batch Processing

Batch jobs are:

Fault tolerant

and:

Can restart.

Choose:

**Spot Instances**

---

## Scenario 3 — Steady Compute

Application uses:

Consistent compute capacity

all year.

Consider:

**Savings Plans / Reserved pricing**

---

## Scenario 4 — Rare Lambda Job

Task runs:

10 minutes per day.

Do not run:

**Dedicated EC2 continuously**

Think:

**Lambda or other event-driven option**

if requirements fit.

---

## Scenario 5 — Old S3 Data

Files are rarely accessed after:

90 days.

Use:

**Lifecycle Policy**

to transition them to:

**Lower-cost storage**

---

## Scenario 6 — Unknown S3 Access Pattern

Access patterns constantly change.

Think:

**S3 Intelligent-Tiering**

---

## Scenario 7 — High NAT Bill

Private EC2 transfers:

Large volumes to S3.

Use:

**S3 Gateway Endpoint**

---

## Scenario 8 — Database Read Load

Database instance was enlarged because of:

Repeated read queries.

Better architecture may be:

**ElastiCache**

or:

**Read Replicas**

depending on access pattern.

---

## Scenario 9 — Predictable DynamoDB

DynamoDB traffic is:

Stable and predictable.

Consider:

**Provisioned Capacity**

rather than automatically assuming:

**On-Demand**

---

## Scenario 10 — DR Cost

Application can tolerate:

12 hours downtime.

Do not select:

**Multi-Site**

if:

**Backup and Restore**

meets requirements.

---

# Scenario Recognition

Immediately think:

**Auto Scaling**

when you see:

- Variable EC2 demand
- Idle capacity
- Peak traffic

---

## Think Spot When You See

- Fault tolerant
- Flexible
- Batch
- Interruptible

---

## Think Commitment Pricing When You See

- Steady workload
- Predictable long-term usage

---

## Think Lifecycle Policy When You See

- Aging S3 data
- Rarely accessed data
- Archive

---

## Think VPC Endpoint When You See

- High NAT costs
- Private AWS service traffic

---

## Think Cache When You See

- Repeated backend work
- Repeated reads
- Origin overload

---

# Exam Traps

## Trap 1 — Cheapest Service Is Always the Best Answer

❌

Choose:

**Cheapest architecture that meets all requirements**

---

## Trap 2 — Spot Is Appropriate for Every Workload

❌

Spot can be:

**Interrupted**

---

## Trap 3 — On-Demand Is Always Cheapest for EC2

❌

Steady workloads may benefit from:

**Commitment pricing**

---

## Trap 4 — Serverless Is Always Cheapest

❌

Usage pattern matters.

---

## Trap 5 — Glacier Is Always Best for Backups

❌

Retrieval requirements matter.

---

## Trap 6 — VPC Endpoint Is Always Cheaper Than NAT

❌

Interface Endpoints have:

**Their own charges**

Evaluate the architecture.

---

## Trap 7 — Removing Multi-AZ Is Good Cost Optimization

❌

Not when:

**High availability is required**

---

## Trap 8 — Larger Database Is Always the Best Scaling Fix

❌

Consider:

- Caching
- Read replicas
- Better access patterns

---

# Quick Cheat Sheet

| Exam Clue | Answer |
|---|---|
| Underutilized EC2 | Right-Size |
| Variable EC2 Demand | Auto Scaling |
| Unpredictable Compute | On-Demand |
| Steady Compute | Savings Plans / Reserved Pricing |
| Fault-Tolerant Batch | Spot |
| Sporadic Compute | Serverless |
| Aging S3 Data | Lifecycle Policy |
| Unknown S3 Pattern | Intelligent-Tiering |
| Large S3 NAT Traffic | Gateway Endpoint |
| Repeated Database Reads | Cache |
| More DB Read Capacity | Read Replica |
| Variable Relational DB | Aurora Serverless |
| Lowest-Cost DR | Backup & Restore |
| Spending Alert | AWS Budgets |
| Spending Trends | Cost Explorer |
| Right-Sizing Recommendation | Compute Optimizer |

---

# Compute Cost Decision Map

Need:

**No commitment**

→ On-Demand

Need:

**Steady long-term compute**

→ Savings Plans / Reserved pricing

Need:

**Interruptible low-cost compute**

→ Spot

Need:

**Highly variable capacity**

→ Auto Scaling

Need:

**Short event-driven execution**

→ Lambda

---

# Storage Cost Decision Map

Need:

**Frequent S3 access**

→ Standard

Need:

**Infrequent access**

→ IA class

Need:

**Long-term archive**

→ Glacier class

Need:

**Unknown access pattern**

→ Intelligent-Tiering

Need:

**Automatic transitions**

→ Lifecycle Policy

---

# Network Cost Decision Map

Need:

**General private Internet access**

→ NAT Gateway

Need:

**Private S3/DynamoDB access**

→ Gateway Endpoint

Need:

**Private supported AWS service**

→ Interface Endpoint

Need:

**Global cache**

→ CloudFront

---

# Final Exam Rapid-Fire

> **UNDERUTILIZED**
> → RIGHT-SIZE
>
> **VARIABLE CAPACITY**
> → AUTO SCALING
>
> **UNPREDICTABLE EC2**
> → ON-DEMAND
>
> **STEADY EC2**
> → SAVINGS PLAN / RESERVED
>
> **INTERRUPTIBLE**
> → SPOT
>
> **SPORADIC COMPUTE**
> → SERVERLESS
>
> **OLD S3 DATA**
> → LIFECYCLE
>
> **UNKNOWN S3 ACCESS**
> → INTELLIGENT-TIERING
>
> **HIGH S3 NAT COST**
> → GATEWAY ENDPOINT
>
> **REPEATED DB READS**
> → CACHE
>
> **MORE DB READS**
> → READ REPLICA
>
> **CHEAPEST DR**
> → BACKUP AND RESTORE
>
> **COST ALERT**
> → BUDGETS
>
> **COST ANALYSIS**
> → COST EXPLORER
>
> **RIGHT-SIZING ADVICE**
> → COMPUTE OPTIMIZER

---

## Master Memory Trick

> [!tip] Cost-Optimized Architecture Master Memory Trick
> Imagine you own:
>
> **A hotel**
>
> You do NOT keep:
>
> **500 rooms fully staffed**
>
> when only:
>
> **50 guests are staying**
>
> That's:
>
> **RIGHT-SIZING**
>
> More guests arrive?
>
> Add capacity:
>
> **AUTO SCALING**
>
> Know the hotel will stay full all year?
>
> Negotiate a commitment:
>
> **SAVINGS PLANS / RESERVED PRICING**
>
> Have flexible temporary workers?
>
> Use:
>
> **SPOT**
>
> Old records nobody reads?
>
> Move them into:
>
> **LOWER-COST STORAGE**
>
> Guests repeatedly ask the same question?
>
> Put the answer somewhere fast:
>
> **CACHE**
>
> Private workloads keep paying to reach S3 through NAT?
>
> Build:
>
> **A VPC ENDPOINT**

So remember:

> **RIGHT-SIZE**
> → DON'T OVERBUY
>
> **AUTO SCALE**
> → DON'T IDLE
>
> **COMMIT**
> → STEADY WORKLOAD
>
> **SPOT**
> → INTERRUPTIBLE WORK
>
> **SERVERLESS**
> → PAY WHEN USED
>
> **LIFECYCLE**
> → CHEAPER STORAGE OVER TIME
>
> **CACHE**
> → DO LESS BACKEND WORK
>
> **VPC ENDPOINT**
> → AVOID UNNECESSARY NAT PATHS
>
> **COST OPTIMIZATION**
> → MEET REQUIREMENTS WITHOUT OVERBUILDING

And the killer SAA question:

> **"Which solution satisfies every requirement while eliminating the most unnecessary ongoing cost?"**
>
> That is usually the:
>
> **Cost-optimized architecture**

---

## Related Notes

- [[Architecture Principles]]
- [[Scalable Architecture]]
- [[High Availability Architecture]]
- [[Caching Architecture]]
- [[Auto Scaling]]
- [[EC2]]
- [[S3]]
- [[VPC Endpoints]]
- [[ElastiCache]]
- [[RDS]]
- [[DynamoDB]]
- [[Lambda]]
- [[Backup and Restore]]
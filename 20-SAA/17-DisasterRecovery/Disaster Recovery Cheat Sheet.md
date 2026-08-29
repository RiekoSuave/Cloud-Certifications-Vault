## Core DR Concepts

Disaster Recovery focuses on:

**Recovering applications and data after a major disruption**

The two most important exam metrics are:

**RPO**

and:

**RTO**

> [!tip] Master Memory Trick
> **RPO = Data Loss**
>
> **RTO = Downtime**

---

# RPO

**Recovery Point Objective**

asks:

> **How much data can the business afford to lose?**

Example:

Company can lose:

**No more than 15 minutes of transactions**

Therefore:

**RPO = 15 minutes**

### Memory Trick

> **RPO = POINT in the past**

---

# RTO

**Recovery Time Objective**

asks:

> **How long can the application remain unavailable?**

Example:

Application must return within:

**2 hours**

Therefore:

**RTO = 2 hours**

### Memory Trick

> **RTO = TIME to recover**

---

# RPO vs RTO

| Requirement | Metric |
|---|---|
| Acceptable Data Loss | RPO |
| Acceptable Downtime | RTO |
| Backup Frequency | Primarily Affects RPO |
| Recovery Speed | Primarily Affects RTO |

### Killer Shortcut

> **"How much data?"**
> → RPO
>
> **"How long down?"**
> → RTO

---

# Cost vs Recovery

As RPO and RTO requirements become:

**More aggressive**

architectures generally require:

- More replication
- More automation
- More infrastructure
- More redundancy
- Higher cost

### Exam Principle

> **Faster recovery generally costs more**

---

# Four Major DR Strategies

The four major strategies are:

1. [[Backup and Restore]]
2. [[Pilot Light]]
3. [[Warm Standby]]
4. [[Multi-Site]]

They move from:

**Lowest cost + slowest recovery**

toward:

**Highest cost + fastest recovery**

---

# Master DR Strategy Table

| Strategy | What Exists Before Disaster | Main Recovery Action | Relative RTO | Relative Cost |
|---|---|---|---|---|
| Backup & Restore | Backups | Rebuild | Highest | Lowest |
| Pilot Light | Critical Core | Start / Provision | High | Low |
| Warm Standby | Full Stack, Small | Scale | Low | Medium |
| Multi-Site | Full Stack, Full | Redirect | Lowest | Highest |

---

# Master Strategy Memory Trick

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

This is the fastest way to distinguish the four strategies.

---

# Backup and Restore

[[Backup and Restore]] means:

**Save the data now and rebuild the environment after disaster**

Before disaster:

Backups  
Snapshots  
IaC Templates

After disaster:

Restore  
↓  
Rebuild  
↓  
Deploy  
↓  
Route Traffic

### Think Backup and Restore When You See

- Lowest cost
- Long downtime acceptable
- Snapshots
- Backups
- Rebuild after disaster
- Minimal standby infrastructure

### Killer Exam Clue

> **Cheapest solution that can tolerate hours of recovery**
>
> → **Backup and Restore**

---

# Pilot Light

[[Pilot Light]] means:

**Critical core components remain running**

while most application infrastructure is:

**Off or unprovisioned**

Classic example:

Database Replica  
→ Running

Application Servers  
→ Not Running

During disaster:

Start / Provision Application  
↓  
Scale  
↓  
Redirect Traffic

### Think Pilot Light When You See

- Core running
- Database replica running
- Compute off
- Continuous data replication
- Start infrastructure after disaster

### Killer Exam Clue

> **Database continuously replicated but application servers launch after disaster**
>
> → **Pilot Light**

---

# Warm Standby

[[Warm Standby]] means:

**The entire application stack is already running at reduced capacity**

Example:

Production:

20 EC2 Instances

DR:

2 EC2 Instances

During disaster:

2  
↓  
Auto Scaling  
↓  
20

### Think Warm Standby When You See

- Full stack running
- Reduced capacity
- Functional DR environment
- Scale after disaster

### Killer Exam Clue

> **Complete secondary environment is already functional but smaller than production**
>
> → **Warm Standby**

---

# Multi-Site

[[Multi-Site]] means:

**Multiple production-capable environments are already running**

During disaster:

**Redirect traffic**

rather than:

- Rebuild
- Start
- Scale the entire environment

### Think Multi-Site When You See

- Full secondary environment
- Active-active
- Production-capable secondary
- Near-immediate recovery
- Lowest RTO
- Highest ongoing cost

### Killer Exam Clue

> **Both Regions are production-capable and recovery mainly requires redirecting traffic**
>
> → **Multi-Site**

---

# The Four Restaurant Trick

Imagine your primary restaurant is destroyed.

## Backup and Restore

You saved:

**Recipes and blueprints**

Now:

**Rebuild the restaurant**

---

## Pilot Light

You have:

**The core kitchen flame burning**

Now:

**Start everything else**

---

## Warm Standby

You have:

**A complete small restaurant**

Now:

**Expand it**

---

## Multi-Site

You already have:

**Another full restaurant**

Now:

**Send customers there**

---

# Strategy Recognition

> **NOTHING RUNNING**
>
> → Backup and Restore
>
> **CORE RUNNING**
>
> → Pilot Light
>
> **WHOLE STACK RUNNING SMALL**
>
> → Warm Standby
>
> **WHOLE STACK RUNNING FULL**
>
> → Multi-Site

---

# Recovery Action Recognition

> **REBUILD**
>
> → Backup and Restore
>
> **START**
>
> → Pilot Light
>
> **SCALE**
>
> → Warm Standby
>
> **REDIRECT**
>
> → Multi-Site

---

# High Availability vs Disaster Recovery

## High Availability

Goal:

**Keep the application running**

Think:

- Multi-AZ
- Load Balancing
- Auto Scaling
- Automatic failover

## Disaster Recovery

Goal:

**Recover after major disruption**

Think:

- Backups
- Cross-Region replication
- Secondary environments
- Failover

### Memory Trick

> **HA = Stay Running**
>
> **DR = Get Running Again**

---

# Multi-AZ vs Multi-Region

## Multi-AZ

Primarily protects against:

**Availability Zone failure**

## Multi-Region

Can protect against:

**Region failure**

### Killer Shortcut

> **AZ Failure**
> → Multi-AZ
>
> **Region Failure**
> → Multi-Region

---

# Important Multi-AZ Trap

[[RDS]] Multi-AZ provides:

**High Availability**

within a Region.

If the question specifically requires:

**Surviving complete Region failure**

then:

**Multi-AZ alone is not sufficient**

Think:

**Cross-Region architecture**

---

# Data Replication and RPO

Lower RPO generally requires:

**More frequent replication**

Examples:

Daily backup  
→ Larger potential data loss

Hourly backup  
→ Less potential data loss

Continuous replication  
→ Much lower potential data loss

### Memory Trick

> **Replication Frequency Drives RPO**

---

# Automation and RTO

Lower RTO generally requires:

**Faster recovery operations**

Automation can help with:

- Infrastructure deployment
- Database promotion
- Auto Scaling
- DNS failover
- Application deployment

### Memory Trick

> **Automation Drives Down RTO**

---

# Infrastructure as Code

Infrastructure as Code can help recreate:

- VPCs
- Subnets
- Security Groups
- EC2
- Load Balancers
- Application infrastructure

Examples:

- CloudFormation
- Terraform

### Killer Exam Clue

> **Need repeatable rapid infrastructure reconstruction**
>
> → **Infrastructure as Code**

---

# EBS Snapshots

[[EBS Snapshots]] provide:

**Point-in-time EBS backups**

Recovery:

Snapshot  
↓  
New EBS Volume  
↓  
EC2

### Regional DR

Need snapshot available after:

**Region failure**

→ Copy snapshot to:

**Another Region**

---

# RDS Backups

[[RDS]] provides:

**Automated Backups**

for:

**Point-in-time recovery**

and:

**Manual Snapshots**

for retained recovery points.

### Killer Shortcut

> **RDS Point-in-Time Recovery**
> → Automated Backups

---

# DynamoDB Recovery

[[DynamoDB]] provides:

**Point-in-Time Recovery**

for restoring data to:

**A previous point within the supported recovery window**

### Killer Exam Clue

> **Recover DynamoDB after accidental writes/deletion**
>
> → **PITR**

---

# S3 Versioning

[[S3 Versioning]] protects against:

- Accidental overwrite
- Accidental deletion

### Killer Exam Clue

> **Recover previous version of S3 object**
>
> → **Versioning**

---

# Cross-Region Replication

Cross-Region replication can improve:

**Regional resilience**

Examples:

- S3 Cross-Region Replication
- Database replication
- Snapshot copies
- Aurora Global Database

### Exam Principle

> **If Region failure is part of the requirement, the recovery data must survive outside that Region**

---

# AWS Backup

AWS Backup provides:

**Centralized backup management**

Think:

- Backup plans
- Retention
- Backup vaults
- Cross-Region copies
- Cross-account backup
- Centralized policies

### Killer Exam Clue

> **Manage backups centrally across multiple AWS services**
>
> → **AWS Backup**

---

# Backup Vault Lock

Backup Vault Lock helps provide:

**Backup immutability**

Think:

- WORM
- Compliance
- Prevent deletion
- Ransomware protection

### Killer Exam Clue

> **Backups must not be modified or deleted**
>
> → **Backup Vault Lock**

---

# Cross-Region vs Cross-Account

## Cross-Region

Protects against:

**Regional failure**

## Cross-Account

Provides stronger:

**Administrative/account isolation**

### Memory Trick

> **Cross-Region = Location Isolation**
>
> **Cross-Account = Account Isolation**

---

# Elastic Disaster Recovery

[[Elastic Disaster Recovery]] provides:

**Continuous block-level server replication into AWS**

Architecture:

Source Servers  
↓  
Replication Agent  
↓  
Low-Cost Staging Area  
↓  
Disaster  
↓  
Recovery Instances

### Think Elastic Disaster Recovery When You See

- Entire servers
- Block-level replication
- On-premises workloads
- Low-cost staging
- Launch recovery instances
- AWS used as DR site

### Killer Exam Clue

> **Continuously replicate on-premises servers into AWS without running full standby compute**
>
> → **Elastic Disaster Recovery**

---

# Elastic Disaster Recovery vs AWS Backup

## Elastic Disaster Recovery

Think:

**Continuous server replication**

## AWS Backup

Think:

**Centralized backup management**

### Killer Shortcut

> **Replicate Servers**
> → Elastic Disaster Recovery
>
> **Manage Backups**
> → AWS Backup

---

# Elastic Disaster Recovery vs Pilot Light

## Pilot Light

Is a:

**DR architecture strategy**

## Elastic Disaster Recovery

Is an:

**AWS DR service**

It can support architectures resembling:

**Pilot Light**

but the terms are:

**Not interchangeable**

---

# Route 53 for DR

[[Route 53]] can redirect users between:

**Primary and recovery environments**

### Failover Routing

Think:

**Primary → Secondary**

based on:

**Health**

### Killer Exam Clue

> **DNS-based automatic DR failover**
>
> → **Route 53 Failover Routing**

---

# Route 53 Latency-Based Routing

For active-active Multi-Site architectures:

**Latency-Based Routing**

can direct users toward:

**The Region providing lower latency**

### Killer Exam Clue

> **Global users should use the lowest-latency healthy Region**
>
> → **Latency-Based Routing**

---

# Global Accelerator

Global Accelerator provides:

**Static anycast IP addresses**

and routes users toward:

**Healthy AWS endpoints**

### Killer Exam Clue

> **Need static global IPs and fast regional endpoint failover**
>
> → **Global Accelerator**

---

# Aurora Global Database

[[Aurora]] Global Database provides:

**Cross-Region Aurora replication**

Think:

- Low replication lag
- Cross-Region reads
- Regional DR

### Killer Exam Clue

> **Aurora requires low-lag Multi-Region DR**
>
> → **Aurora Global Database**

---

# DynamoDB Global Tables

[[DynamoDB]] Global Tables provide:

**Multi-Region active-active DynamoDB**

Think:

**Reads + writes across multiple Regions**

### Killer Exam Clue

> **DynamoDB application must accept writes in multiple Regions**
>
> → **Global Tables**

---

# DR Service Decision Map

Need:

**Traditional backups**

→ AWS Backup / Service Backups

Need:

**Server-level continuous replication**

→ Elastic Disaster Recovery

Need:

**Aurora Multi-Region**

→ Aurora Global Database

Need:

**DynamoDB Multi-Region**

→ Global Tables

Need:

**DNS failover**

→ Route 53

Need:

**Static global IP failover**

→ Global Accelerator

Need:

**Recreate infrastructure**

→ Infrastructure as Code

---

# Scenario 1 — Data Loss

Requirement:

> No more than 10 minutes of transactions can be lost.

Think:

**RPO = 10 minutes**

---

# Scenario 2 — Downtime

Requirement:

> Application must return within 30 minutes.

Think:

**RTO = 30 minutes**

---

# Scenario 3 — Lowest Cost

Business can tolerate:

**24 hours of downtime**

Think:

**Backup and Restore**

---

# Scenario 4 — Database Running

DR Region contains:

**Continuously replicated database**

but:

**Application servers are off**

Think:

**Pilot Light**

---

# Scenario 5 — Small DR Environment

DR Region contains:

**Complete application stack**

but:

**Reduced compute capacity**

Think:

**Warm Standby**

---

# Scenario 6 — Full DR Environment

Secondary Region is:

**Already production-capable**

Think:

**Multi-Site**

---

# Scenario 7 — On-Prem Servers

Company wants:

**Continuous replication of VMware servers into AWS**

Think:

**Elastic Disaster Recovery**

---

# Scenario 8 — Region Failure

Application must survive:

**Complete Region loss**

Think:

**Multi-Region**

not merely:

**Multi-AZ**

---

# Scenario 9 — Immutable Backups

Backups must survive:

**Malicious deletion**

Think:

**Backup Vault Lock**

---

# Scenario 10 — Fast Failover

Application uses:

**Static IP addresses**

and requires:

**Fast regional endpoint failover**

Think:

**Global Accelerator**

---

# Exam Traps

## Trap 1 — RPO = Downtime

❌

RPO:

**Data Loss**

RTO:

**Downtime**

---

## Trap 2 — Pilot Light = Full Stack Running Small

❌

That is:

**Warm Standby**

Pilot Light:

**Core only**

---

## Trap 3 — Warm Standby = Full Production Capacity

❌

That is:

**Multi-Site**

Warm Standby:

**Reduced capacity**

---

## Trap 4 — Backup and Restore Has Fastest Recovery

❌

It generally has:

**The slowest recovery**

---

## Trap 5 — Multi-Site Is Cheapest

❌

It generally has:

**The highest ongoing cost**

---

## Trap 6 — Multi-AZ Protects Against Complete Region Failure

❌

Think:

**Multi-Region**

---

## Trap 7 — Backup and Replication Are Identical

❌

Backup:

**Recovery point**

Replication:

**Copies changes**

---

## Trap 8 — AWS Backup = Elastic Disaster Recovery

❌

AWS Backup:

**Backup management**

Elastic Disaster Recovery:

**Continuous server replication**

---

## Trap 9 — Successful Backup Guarantees Recovery

❌

Backups must be:

**Restorable and tested**

---

## Trap 10 — Lowest Possible RTO/RPO Is Always Best

❌

Choose the architecture that:

**Meets business requirements at appropriate cost**

---

# Ultimate DR Cheat Sheet

| Exam Clue | Answer |
|---|---|
| Data Loss | RPO |
| Downtime | RTO |
| Backups Only | Backup & Restore |
| Core Running | Pilot Light |
| Full Stack Small | Warm Standby |
| Full Stack Full | Multi-Site |
| Rebuild | Backup & Restore |
| Start | Pilot Light |
| Scale | Warm Standby |
| Redirect | Multi-Site |
| Lowest Cost | Backup & Restore |
| Lowest RTO | Multi-Site |
| Central Backups | AWS Backup |
| Immutable Backups | Vault Lock |
| Server Replication | Elastic Disaster Recovery |
| Region Failure | Multi-Region |
| AZ Failure | Multi-AZ |
| DNS Failover | Route 53 |
| Static Global IP Failover | Global Accelerator |
| Aurora Multi-Region | Global Database |
| DynamoDB Multi-Region | Global Tables |

---

# Final Exam Decision Tree

> **WHAT IS THE REQUIREMENT?**
>
> ---
>
> **DATA LOSS?**
>
> → RPO
>
> **DOWNTIME?**
>
> → RTO
>
> ---
>
> **WHAT EXISTS IN DR BEFORE FAILURE?**
>
> Backups only
> → Backup and Restore
>
> Core only
> → Pilot Light
>
> Full stack small
> → Warm Standby
>
> Full stack full
> → Multi-Site
>
> ---
>
> **WHAT HAPPENS DURING RECOVERY?**
>
> Rebuild
> → Backup and Restore
>
> Start
> → Pilot Light
>
> Scale
> → Warm Standby
>
> Redirect
> → Multi-Site
>
> ---
>
> **SERVER REPLICATION?**
>
> → Elastic Disaster Recovery
>
> **CENTRAL BACKUPS?**
>
> → AWS Backup
>
> **IMMUTABLE BACKUPS?**
>
> → Backup Vault Lock
>
> ---
>
> **AZ FAILURE?**
>
> → Multi-AZ
>
> **REGION FAILURE?**
>
> → Multi-Region
>
> ---
>
> **DNS FAILOVER?**
>
> → Route 53
>
> **STATIC GLOBAL IP FAILOVER?**
>
> → Global Accelerator

---

## Master Memory Trick

> [!tip] Disaster Recovery Master Memory Trick
> First ask:
>
> **HOW MUCH DATA CAN WE LOSE?**
>
> → RPO
>
> Then:
>
> **HOW LONG CAN WE BE DOWN?**
>
> → RTO
>
> Then look at:
>
> **WHAT IS ALREADY RUNNING?**
>
> Nothing except backups?
>
> → **BACKUP AND RESTORE**
>
> Critical core?
>
> → **PILOT LIGHT**
>
> Whole application, but small?
>
> → **WARM STANDBY**
>
> Whole application at production capability?
>
> → **MULTI-SITE**

Then remember the four recovery verbs:

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

And for AWS services:

> **AWS BACKUP**
> → MANAGE BACKUPS
>
> **ELASTIC DISASTER RECOVERY**
> → REPLICATE SERVERS
>
> **ROUTE 53**
> → DNS FAILOVER
>
> **GLOBAL ACCELERATOR**
> → FAST GLOBAL ENDPOINT FAILOVER
>
> **AURORA GLOBAL DATABASE**
> → AURORA MULTI-REGION
>
> **DYNAMODB GLOBAL TABLES**
> → DYNAMODB MULTI-REGION

The killer SAA question is:

> **"What RPO and RTO does the business require, and how much infrastructure must already be running to meet those requirements?"**

That tells you:

**Which DR strategy to choose.**

---

## Related Notes

- [[Disaster Recovery Overview]]
- [[Backup and Restore]]
- [[Pilot Light]]
- [[Warm Standby]]
- [[Multi-Site]]
- [[Elastic Disaster Recovery]]
- [[EBS Snapshots]]
- [[RDS]]
- [[Aurora]]
- [[DynamoDB]]
- [[S3]]
- [[Route 53]]
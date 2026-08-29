## What Is Disaster Recovery?

Disaster Recovery — DR — is the process of:

**Preparing for and recovering from events that disrupt business operations or IT systems**

A disaster can include:

- Data center failure
- Availability Zone failure
- Regional failure
- Application failure
- Hardware failure
- Data corruption
- Accidental deletion
- Large-scale infrastructure outage

The goal is to:

**Restore applications and data within acceptable business requirements**

> [!tip] Memory Trick
> **Disaster Recovery = How Fast Can We Get Back + How Much Can We Lose?**

Those two questions lead directly to:

**RTO + RPO**

---

# High Availability vs Disaster Recovery

These concepts are related but:

**Not the same**

## High Availability

Focuses on:

**Keeping an application running during failures**

Example:

Application Load Balancer  
↓  
EC2 — AZ A  
EC2 — AZ B

If one AZ fails:

**The application continues operating**

---

## Disaster Recovery

Focuses on:

**Recovering after a major disruption**

Example:

Primary Region  
↓  
Disaster  
↓  
Recover workload in Secondary Region

### Killer Memory Trick

> **High Availability**
> → Stay Running
>
> **Disaster Recovery**
> → Get Running Again

---

# Business Continuity

Disaster Recovery is part of the larger concept of:

**Business Continuity**

Business continuity asks:

> **How does the organization continue operating when something goes wrong?**

DR focuses specifically on:

**Recovering technology systems and data**

---

# RPO

## Recovery Point Objective

RPO answers:

> **How much data can the business afford to lose?**

Think:

**TIME BETWEEN THE DISASTER AND THE LAST RECOVERABLE DATA**

Example:

Backups occur every:

**6 hours**

A disaster happens at:

**5:00 PM**

Last backup:

**12:00 PM**

Potential data loss:

**5 hours**

### Memory Trick

> **RPO = DATA LOSS**

---

# RPO Timeline

Example:

Backup  
12:00 PM  
↓  
New Data  
↓  
New Data  
↓  
Disaster  
5:00 PM

If recovery uses the:

**12:00 PM backup**

then data created after that point may be:

**Lost**

### Killer Exam Question

> **How much data can the company afford to lose?**
>
> → **RPO**

---

# Lower RPO

A lower RPO means:

**Less acceptable data loss**

Example:

RPO:

**5 minutes**

means the architecture should be capable of recovering data from roughly:

**No more than 5 minutes before the disruption**

This usually requires:

- More frequent backups
- Continuous replication
- Cross-Region replication
- Database replication

### Exam Principle

> **Lower RPO generally means more replication and higher cost**

---

# RTO

## Recovery Time Objective

RTO answers:

> **How long can the application remain unavailable?**

Think:

**TIME FROM DISASTER TO RECOVERY**

Example:

Disaster:

2:00 PM

Application restored:

3:00 PM

RTO:

**1 hour**

### Memory Trick

> **RTO = DOWNTIME**

---

# RTO Timeline

Disaster  
2:00 PM  
↓  
Recovery Process  
↓  
Infrastructure Restored  
↓  
Application Available  
3:00 PM

Downtime:

**1 hour**

### Killer Exam Question

> **How long can the business tolerate the application being unavailable?**
>
> → **RTO**

---

# RPO vs RTO

This is one of the most important DR concepts for SAA.

| Metric | Question | Think |
|---|---|---|
| RPO | How much data can we lose? | Data Loss |
| RTO | How long can we be down? | Downtime |

### Killer Memory Trick

> **RPO = POINT in the past**
>
> **RTO = TIME to recover**

---

# RPO Example

Requirement:

> Company can lose no more than **15 minutes of transaction data**

Think:

**RPO = 15 minutes**

---

# RTO Example

Requirement:

> Application must be restored within **2 hours**

Think:

**RTO = 2 hours**

---

# RPO + RTO Example

Requirement:

> The company can lose no more than 5 minutes of data and the application must return within 30 minutes.

Answer:

**RPO = 5 minutes**

**RTO = 30 minutes**

---

# Lower RPO + RTO

The closer RPO and RTO move toward:

**Zero**

the more demanding the architecture becomes.

Typically this requires:

- More infrastructure
- More replication
- More automation
- More redundancy
- Higher cost

### Master DR Principle

> **Lower RPO + Lower RTO = Higher Cost**

---

# Disaster Recovery Strategies

AWS DR architectures generally fall into four major strategies:

1. **Backup and Restore**
2. **Pilot Light**
3. **Warm Standby**
4. **Multi-Site / Hot Site**

They move from:

**Cheapest + Slowest**

to:

**Most Expensive + Fastest**

---

# DR Strategy Spectrum

> **LOW COST**
>
> Backup & Restore
> ↓
> Pilot Light
> ↓
> Warm Standby
> ↓
> Multi-Site / Hot Site
>
> **HIGH COST**

At the same time:

> **HIGH RTO**
>
> Backup & Restore
> ↓
> Pilot Light
> ↓
> Warm Standby
> ↓
> Multi-Site / Hot Site
>
> **LOW RTO**

### Killer Memory Trick

> **More Infrastructure Running Before Disaster**
>
> =
>
> **Faster Recovery + Higher Cost**

---

# Backup and Restore

Basic concept:

**Store backups and rebuild after disaster**

Before disaster:

Primary Region  
↓  
Backups

After disaster:

Backups  
↓  
Restore Infrastructure  
↓  
Restore Data  
↓  
Application

Think:

**Nothing significant is waiting fully operational**

### Characteristics

- Lowest cost
- Slowest recovery
- Higher RTO
- Appropriate when downtime is acceptable

### Killer Exam Clue

> **Cheapest DR strategy and business can tolerate hours of recovery**
>
> → **Backup and Restore**

---

# Pilot Light

Basic concept:

Keep:

**Critical core components running**

while most application infrastructure remains:

**Stopped or unprovisioned**

Example:

Secondary Region:

Database replication  
↓  
Critical core services

During disaster:

Scale/provision application infrastructure  
↓  
Start application

### Memory Trick

A pilot light on a stove is:

**A tiny flame already burning**

The core is alive.

The rest can be:

**Ignited quickly**

### Killer Exam Clue

> **Critical database/core services remain running, application servers are started after disaster**
>
> → **Pilot Light**

---

# Warm Standby

Basic concept:

Keep:

**A smaller but fully functional version of the environment running**

Secondary Region:

Small Application Tier  
↓  
Small Database Capacity

During disaster:

**Scale it up**

### Memory Trick

> **Warm = Already Running**

but:

**Smaller than production**

### Killer Exam Clue

> **Secondary environment is fully functional but running at reduced capacity**
>
> → **Warm Standby**

---

# Multi-Site / Hot Site

Basic concept:

Run:

**Full production-capable environments simultaneously**

across multiple locations or Regions.

Architecture:

Users  
↓  
DNS / Global Routing  
↓  
Region A + Region B

Both environments are:

**Active**

or ready for near-immediate production traffic.

### Characteristics

- Lowest RTO
- Potentially very low RPO
- Highest cost
- Most infrastructure already running

### Killer Exam Clue

> **Near-zero downtime and very aggressive recovery requirements**
>
> → **Multi-Site / Hot Site**

---

# DR Strategy Comparison

| Strategy | Infrastructure Running | RTO | Cost |
|---|---|---|---|
| Backup & Restore | Minimal | Highest | Lowest |
| Pilot Light | Core Only | High | Low |
| Warm Standby | Reduced Full Environment | Lower | Medium |
| Multi-Site / Hot Site | Full Environment | Lowest | Highest |

### Master Exam Order

> **BACKUP**
> → Rebuild
>
> **PILOT LIGHT**
> → Core Running
>
> **WARM STANDBY**
> → Everything Running Small
>
> **MULTI-SITE**
> → Everything Running Full

---

# Pilot Light vs Warm Standby

This is a common exam distinction.

## Pilot Light

Only:

**Critical core components**

are continuously running.

Other infrastructure must be:

**Started/provisioned**

after disaster.

## Warm Standby

A:

**Complete working environment**

already exists.

It simply operates at:

**Reduced capacity**

### Killer Shortcut

> **Core Only**
> → Pilot Light
>
> **Whole Stack but Small**
> → Warm Standby

---

# Warm Standby vs Multi-Site

## Warm Standby

Secondary environment:

**Running smaller**

During disaster:

**Scale up**

## Multi-Site

Secondary environment:

**Already production-scale or actively serving traffic**

### Killer Shortcut

> **Scale After Disaster**
> → Warm Standby
>
> **Already Full/Active**
> → Multi-Site

---

# Backup Strategy

Backups may involve services such as:

- [[S3]]
- [[S3 Glacier]]
- [[EBS Snapshots]]
- [[RDS]]
- AWS Backup

Backups should be stored so they survive:

**The disaster being planned for**

### Exam Principle

> **A backup located only inside the failed environment may not provide sufficient DR protection**

---

# Cross-Region Disaster Recovery

For protection against:

**Regional failure**

organizations may replicate:

**Data and infrastructure configuration**

to:

**Another AWS Region**

Architecture:

Primary Region  
↓  
Replication / Backup  
↓  
Secondary Region

### Killer Exam Clue

> **Must survive complete AWS Region failure**
>
> → **Cross-Region DR architecture**

---

# Multi-AZ vs Multi-Region

Do not confuse these.

## Multi-AZ

Protects primarily against:

**Availability Zone failures**

## Multi-Region

Can protect against:

**Regional failures**

### Memory Trick

> **AZ Failure**
> → Multi-AZ
>
> **Region Failure**
> → Multi-Region

---

# Multi-AZ Is Usually High Availability

Example:

[[RDS]] Multi-AZ

provides:

**High availability and automatic failover**

within a Region.

It is not automatically equivalent to:

**Cross-Region disaster recovery**

### Killer Exam Trap

> **Requirement says survive complete Region failure**
>
> Multi-AZ alone is:
>
> ❌ **Not enough**

---

# Data Replication

Lower RPO often requires:

**Frequent or continuous data replication**

Possible patterns include:

- Database replication
- S3 replication
- Snapshot copying
- Cross-Region replication
- Global databases

### Exam Principle

> **Replication frequency strongly affects RPO**

---

# Infrastructure as Code

Disaster recovery can use:

**Infrastructure as Code**

to recreate infrastructure quickly.

Examples:

- CloudFormation
- Terraform

Instead of manually rebuilding:

VPC  
EC2  
Load Balancers  
Security Groups  
Databases

the architecture can be:

**Recreated automatically**

### Killer Exam Clue

> **Need repeatable infrastructure reconstruction after disaster**
>
> → **Infrastructure as Code**

---

# Automation

Lower RTO often depends heavily on:

**Automation**

Examples:

- Automated deployment
- Automated failover
- Automated scaling
- DNS failover
- Infrastructure provisioning

### Memory Trick

> **Manual Recovery = Slow RTO**
>
> **Automated Recovery = Faster RTO**

---

# Route 53 and DR

[[Route 53]] can help redirect users when:

**Primary infrastructure becomes unhealthy**

Example:

Primary Region  
❌

Route 53 Failover  
↓

Secondary Region  
✅

### Killer Exam Clue

> **Automatically redirect DNS traffic to DR environment**
>
> → **Route 53 Failover Routing**

---

# Global Accelerator and DR

Global applications may use:

**Global Accelerator**

to redirect traffic between:

**Healthy regional endpoints**

This can support:

**Multi-Region resilience**

especially where:

**Fast endpoint failover**

is important.

---

# Aurora Global Database

For globally distributed relational database architectures:

**Aurora Global Database**

can replicate data across:

**AWS Regions**

This supports:

- Cross-Region reads
- Disaster recovery
- Low-latency global architectures

### Killer Exam Clue

> **Aurora workload requires cross-Region database DR with low replication lag**
>
> → **Aurora Global Database**

---

# Elastic Disaster Recovery

AWS provides:

**Elastic Disaster Recovery**

for recovering servers and applications into:

**AWS**

It can continuously replicate:

**Server data**

into a low-cost staging environment.

During disaster:

**Recovery instances are launched**

### Memory Trick

> **Elastic Disaster Recovery = Replicate First, Launch When Needed**

---

# Disaster Recovery Testing

A DR plan should be:

**Tested regularly**

A recovery plan that exists only on paper may fail because of:

- Missing dependencies
- Incorrect permissions
- Broken automation
- Outdated backups
- Routing problems
- DNS problems

### Exam Principle

> **DR must be tested, not merely documented**

---

# Backups Must Be Restorable

Successful backup creation does not guarantee:

**Successful recovery**

Organizations should verify:

**Backups can actually be restored**

### Memory Trick

> **Backup ≠ Recovery**
>
> **Restorable Backup = Recovery**

---

# DR and Security

Recovery environments still require:

- IAM controls
- Encryption
- Security Groups
- Network controls
- Logging
- Monitoring

### Exam Principle

> **Disaster recovery does not eliminate normal security requirements**

---

# DR and Cost

The four strategies represent a:

**Cost vs Recovery tradeoff**

### Lowest Cost

**Backup and Restore**

but:

**Longest recovery**

### Highest Cost

**Multi-Site**

but:

**Fastest recovery**

### Killer Exam Principle

> **Business requirements determine DR strategy — not simply the most resilient architecture**

---

# Architecture Thinking

## Scenario 1 — 24-Hour Recovery

Application can remain offline for:

**24 hours**

and cost must be minimized.

Think:

**Backup and Restore**

---

## Scenario 2 — Core Database Running

Secondary Region continuously maintains:

**Database replication**

but application servers are created after failure.

Think:

**Pilot Light**

---

## Scenario 3 — Small Environment Running

Secondary Region already has:

- Application servers
- Database
- Load balancer

but at:

**Reduced capacity**

Think:

**Warm Standby**

---

## Scenario 4 — Near-Zero Downtime

Both Regions operate:

**Production-capable infrastructure**

Think:

**Multi-Site / Hot Site**

---

## Scenario 5 — Five-Minute Data Loss

Business says:

> No more than 5 minutes of transactions may be lost.

Think:

**RPO = 5 minutes**

---

## Scenario 6 — Thirty-Minute Downtime

Business says:

> Application must be restored within 30 minutes.

Think:

**RTO = 30 minutes**

---

## Scenario 7 — Complete Region Failure

Application must survive:

**Entire AWS Region failure**

Think:

**Multi-Region DR**

not merely:

**Multi-AZ**

---

## Scenario 8 — Cheapest Solution

Exam asks:

> Which solution satisfies the recovery requirements at the lowest cost?

Do NOT automatically choose:

**Multi-Site**

Choose the:

**Least expensive strategy that still satisfies the required RPO/RTO**

---

# Scenario Recognition

Immediately think:

**RPO**

when you see:

- Data loss
- Backup frequency
- Recovery point
- Replication frequency

Immediately think:

**RTO**

when you see:

- Downtime
- Recovery duration
- Restore time
- How quickly service must return

---

## Think Backup and Restore When You See

- Lowest cost
- Long downtime acceptable
- Rebuild after disaster
- Restore from backups

---

## Think Pilot Light When You See

- Core components running
- Database continuously available/replicated
- Application infrastructure started later

---

## Think Warm Standby When You See

- Full environment already running
- Reduced capacity
- Scale up after disaster

---

## Think Multi-Site When You See

- Near-zero downtime
- Active environments
- Very low RTO
- Highest cost

---

# Exam Traps

## Trap 1 — RPO Means Downtime

❌

RPO:

**Data loss**

RTO:

**Downtime**

---

## Trap 2 — Lowest RPO/RTO Is Always the Best Architecture

❌

The architecture must balance:

**Business requirements + Cost**

---

## Trap 3 — Pilot Light and Warm Standby Are the Same

❌

Pilot Light:

**Core only**

Warm Standby:

**Entire environment at reduced capacity**

---

## Trap 4 — Multi-AZ Automatically Protects Against Region Failure

❌

For Region failure:

Think:

**Multi-Region**

---

## Trap 5 — Backup Means Recovery Is Guaranteed

❌

Backups must be:

**Restorable**

---

## Trap 6 — Multi-Site Is Cheapest

❌

It is generally:

**The most expensive strategy**

---

## Trap 7 — DR Is Only About Data

❌

DR includes recovering:

- Infrastructure
- Applications
- Networking
- DNS
- Security
- Data

---

# Quick Cheat Sheet

| Exam Clue | Answer |
|---|---|
| Acceptable Data Loss | RPO |
| Acceptable Downtime | RTO |
| Lowest Cost DR | Backup & Restore |
| Core Components Running | Pilot Light |
| Full Stack Running Small | Warm Standby |
| Full Production Environments | Multi-Site |
| AZ Failure | Multi-AZ |
| Region Failure | Multi-Region |
| Rebuild Infrastructure | IaC |
| DNS DR Failover | Route 53 |
| Cross-Region Aurora DR | Aurora Global Database |
| Server DR into AWS | Elastic Disaster Recovery |

---

# DR Strategy Decision Map

Need:

**Lowest cost**

→ Backup & Restore

Need:

**Core always running**

→ Pilot Light

Need:

**Complete environment running small**

→ Warm Standby

Need:

**Near-zero recovery time**

→ Multi-Site / Hot Site

Need:

**Less data loss**

→ Lower RPO

Need:

**Less downtime**

→ Lower RTO

Need:

**Regional disaster protection**

→ Multi-Region

---

# DR Cost Ladder

> **CHEAPEST**
>
> Backup & Restore
>
> ↓
>
> Pilot Light
>
> ↓
>
> Warm Standby
>
> ↓
>
> Multi-Site / Hot Site
>
> **MOST EXPENSIVE**

---

# DR Recovery Speed Ladder

> **SLOWEST**
>
> Backup & Restore
>
> ↓
>
> Pilot Light
>
> ↓
>
> Warm Standby
>
> ↓
>
> Multi-Site / Hot Site
>
> **FASTEST**

---

# Final Exam Rapid-Fire

> **DATA LOSS**
> → RPO
>
> **DOWNTIME**
> → RTO
>
> **CHEAPEST**
> → BACKUP & RESTORE
>
> **CORE RUNNING**
> → PILOT LIGHT
>
> **FULL STACK RUNNING SMALL**
> → WARM STANDBY
>
> **FULL ENVIRONMENT RUNNING**
> → MULTI-SITE
>
> **AZ FAILURE**
> → MULTI-AZ
>
> **REGION FAILURE**
> → MULTI-REGION
>
> **DNS FAILOVER**
> → ROUTE 53
>
> **REBUILD AUTOMATICALLY**
> → INFRASTRUCTURE AS CODE
>
> **SERVER RECOVERY INTO AWS**
> → ELASTIC DISASTER RECOVERY

---

## Master Memory Trick

> [!tip] Disaster Recovery Master Memory Trick
> Imagine your restaurant burns down.
>
> **RPO asks:**
>
> "How many customer orders can we afford to lose?"
>
> That's:
>
> **DATA LOSS**
>
> **RTO asks:**
>
> "How long can the restaurant remain closed?"
>
> That's:
>
> **DOWNTIME**
>
> Now choose your backup restaurant:
>
> **BACKUP & RESTORE**
>
> You have the recipes stored somewhere, but you must rebuild the restaurant.
>
> **PILOT LIGHT**
>
> The kitchen's tiny pilot flame is still burning, but you need to start everything else.
>
> **WARM STANDBY**
>
> A small backup restaurant is already open. You just need to expand it.
>
> **MULTI-SITE**
>
> You already operate a second full restaurant.

So remember:

> **RPO**
> → DATA
>
> **RTO**
> → TIME
>
> **BACKUP**
> → REBUILD
>
> **PILOT LIGHT**
> → CORE
>
> **WARM STANDBY**
> → SMALL
>
> **MULTI-SITE**
> → FULL
>
> **LOWER RPO/RTO**
> → MORE $

And the killer SAA question:

> **"What are the business's acceptable data loss and downtime?"**
>
> Those requirements determine:
>
> **The appropriate Disaster Recovery strategy**

---

## Related Notes

- [[RDS]]
- [[Aurora]]
- [[S3]]
- [[S3 Glacier]]
- [[EBS Snapshots]]
- [[Route 53]]
- [[Direct Connect]]
- [[Site-to-Site VPN]]
- [[Transit Gateway]]
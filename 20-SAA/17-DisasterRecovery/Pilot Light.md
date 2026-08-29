## Core Concept

Pilot Light is a Disaster Recovery strategy where:

**The critical core of the application is always running in the disaster recovery environment**

but:

**Most application infrastructure is stopped or not yet provisioned**

During a disaster, you:

1. Activate or provision the remaining infrastructure
2. Scale the environment
3. Redirect traffic
4. Resume production

Architecture:

Primary Region  
↓  
Continuous Data Replication  
↓  
Secondary Region  
↓  
Critical Core Running

After Disaster:

Critical Core  
↓  
Start / Provision Compute  
↓  
Scale Application  
↓  
Redirect Traffic

> [!tip] Memory Trick
> **Pilot Light = Keep the Flame Burning**

---

# Why Is It Called Pilot Light?

Think about:

**A gas stove**

Even when the stove is not fully operating:

**A tiny flame remains lit**

When needed:

**The full burner can ignite quickly**

That is exactly how this DR strategy works.

Before disaster:

**Critical core is alive**

After disaster:

**Turn on the rest**

### Killer Memory Trick

> **Core Running + Rest Off**
>
> → **Pilot Light**

---

# What Stays Running?

The most critical components usually remain:

**Continuously available**

A common example is:

**The data layer**

such as:

- Replicated databases
- Critical data stores
- Core infrastructure

Meanwhile:

Application servers may be:

- Stopped
- Scaled to zero where supported
- Not yet provisioned

### Killer Exam Clue

> **Database is continuously replicated to the DR Region, but application servers are launched only after a disaster**
>
> → **Pilot Light**

---

# Before Disaster

Example:

## Primary Region

Users  
↓  
Load Balancer  
↓  
Application Servers  
↓  
Database

## DR Region

Database Replica  
↓  
Critical Core

But:

**Full application tier is not running**

This keeps costs:

**Lower than Warm Standby**

---

# During Disaster

If the primary environment fails:

DR Database  
↓  
Promote / Activate  
↓  
Provision Application Servers  
↓  
Provision / Scale Load Balancer  
↓  
Validate Application  
↓  
Redirect Users

### Key Principle

> **Some infrastructure must still be activated before the DR environment can serve full production traffic**

---

# RTO

Pilot Light usually has:

**Lower RTO than Backup and Restore**

because:

**Critical components are already running**

However, it generally has:

**Higher RTO than Warm Standby**

because:

**The complete application environment is not yet operational**

### Recovery Speed

Backup & Restore  
↓  
**Pilot Light**  
↓  
Warm Standby  
↓  
Multi-Site

From:

**Slower**

to:

**Faster**

---

# RPO

Pilot Light can provide a:

**Low RPO**

when critical data is:

**Continuously replicated**

Example:

Primary Database  
↓  
Continuous Replication  
↓  
DR Database

If replication lag is low:

**Potential data loss can also be low**

### Killer Exam Principle

> **RPO depends heavily on how the critical data is replicated**

---

# Pilot Light vs Backup and Restore

## Backup and Restore

Before disaster:

**Primarily backups exist**

After disaster:

**Infrastructure and data must be restored**

## Pilot Light

Before disaster:

**Critical core infrastructure is already running**

After disaster:

**Activate the remaining application infrastructure**

### Killer Shortcut

> **Restore Core After Disaster**
> → Backup and Restore
>
> **Core Already Alive**
> → Pilot Light

---

# Pilot Light vs Warm Standby

This distinction is extremely important.

## Pilot Light

Secondary environment:

**Not fully functional for production**

Only:

**Critical core components**

are continuously running.

## Warm Standby

Secondary environment:

**Already fully functional**

but operating at:

**Reduced capacity**

### Killer Shortcut

> **Core Only**
> → Pilot Light
>
> **Whole Stack Running Small**
> → Warm Standby

---

# Pilot Light vs Multi-Site

## Pilot Light

Most application capacity must be:

**Started after disaster**

## Multi-Site

Production-capable infrastructure is:

**Already operating**

### Memory Trick

> **Pilot Light = Ignite**
>
> **Multi-Site = Already Burning**

---

# Cost

Pilot Light generally costs:

**More than Backup and Restore**

because:

**Some DR infrastructure remains running**

But it generally costs:

**Less than Warm Standby**

because:

**The complete application stack is not continuously operational**

### Cost Order

Backup & Restore  
↓  
**Pilot Light**  
↓  
Warm Standby  
↓  
Multi-Site

From:

**Lower cost**

to:

**Higher cost**

---

# Data Replication

Data replication is often the heart of:

**Pilot Light**

The DR environment may continuously maintain:

- Database replicas
- Object replication
- Critical storage
- Configuration

### Exam Principle

> **The data/core remains ready while disposable compute can be recreated**

---

# RDS Cross-Region Read Replica

For supported [[RDS]] engines:

A:

**Cross-Region Read Replica**

can maintain a copy of:

**Database data**

in another Region.

During disaster:

The replica may be:

**Promoted**

to support recovery.

### Killer Exam Clue

> **Relational database continuously replicated to another Region and promoted during disaster**
>
> → Think **Cross-Region Read Replica**

---

# Aurora Global Database

[[Aurora]] Global Database can replicate:

**Aurora data across Regions**

This can support architectures requiring:

- Low replication lag
- Cross-Region reads
- Faster regional database recovery

### Killer Exam Clue

> **Aurora application needs low-lag cross-Region replication for DR**
>
> → **Aurora Global Database**

---

# DynamoDB Global Tables

[[DynamoDB]] Global Tables provide:

**Multi-Region replication**

for DynamoDB.

This can support:

**Low-RPO global and DR architectures**

### Exam Recognition

> **DynamoDB data must be available across multiple Regions**
>
> → **Global Tables**

---

# S3 Cross-Region Replication

[[S3]] Cross-Region Replication can copy objects from:

**Primary Region**

to:

**DR Region**

Architecture:

S3 — Primary  
↓  
Cross-Region Replication  
↓  
S3 — DR

This can help ensure:

**Critical application objects are already available**

during recovery.

---

# Infrastructure as Code

Because the entire application environment may not be running:

**Infrastructure as Code is especially valuable**

During disaster:

CloudFormation / Terraform  
↓  
Create Infrastructure  
↓  
Deploy Application  
↓  
Scale Environment

### Killer Exam Clue

> **Need to rapidly create application servers during Pilot Light recovery**
>
> → **Infrastructure as Code + Automation**

---

# AMIs

Prebuilt:

**AMIs**

can speed up recovery by allowing EC2 instances to launch with:

**Required software already installed**

Instead of:

Installing everything after launch

you can:

**Launch preconfigured instances**

### Memory Trick

> **AMI = Ready-to-Launch Server Blueprint**

---

# Auto Scaling

[[Auto Scaling]] can help rapidly:

**Increase compute capacity**

during recovery.

Example:

Pilot Light DR  
↓  
Disaster Declared  
↓  
Increase Desired Capacity  
↓  
EC2 Instances Launch  
↓  
Application Capacity Restored

### Killer Exam Clue

> **Need to rapidly scale DR compute after failover**
>
> → **Auto Scaling**

---

# Load Balancer

A DR architecture may activate or scale:

**Elastic Load Balancing**

to distribute traffic across:

**Recovered application instances**

The exact implementation depends on:

**What infrastructure is kept running before the disaster**

---

# Route 53 Failover

[[Route 53]] can redirect users from:

**Primary Region**

to:

**Recovered DR Region**

Architecture:

Primary Region  
❌  
↓  
Route 53 Failover  
↓  
DR Region  
✅

### Important

With Pilot Light, Route 53 should redirect production traffic:

**After the DR environment is ready**

because the secondary environment is not necessarily:

**Fully operational before recovery actions occur**

---

# Recovery Automation

A Pilot Light recovery workflow can be heavily automated.

Example:

Disaster Detected  
↓  
Promote Database  
↓  
Deploy Infrastructure  
↓  
Scale Compute  
↓  
Validate Application  
↓  
Update DNS  
↓  
Serve Users

### Exam Principle

> **Automation reduces Pilot Light RTO**

---

# Pilot Light and Infrastructure Templates

A strong Pilot Light design keeps:

**Infrastructure definitions ready**

Examples:

- CloudFormation templates
- Terraform configuration
- Launch Templates
- AMIs
- Deployment scripts

This allows the environment to be:

**Expanded rapidly**

---

# Testing

Pilot Light DR should be:

**Tested regularly**

Tests should confirm:

- Database promotion works
- Infrastructure launches
- Applications deploy
- Security controls work
- DNS failover works
- Dependencies are available

### Memory Trick

> **A Pilot Light That Never Gets Tested Might Not Ignite**

---

# Failback

After the primary environment is restored, organizations may need to:

**Fail back**

from the DR Region.

This can involve:

1. Re-establish replication
2. Synchronize data
3. Restore primary infrastructure
4. Redirect traffic
5. Return to normal operations

### Exam Principle

> **DR planning includes recovery and eventual return to normal operations**

---

# Architecture Thinking

## Scenario 1 — Database Always Running

Company continuously replicates:

**Database to another Region**

but EC2 instances are:

**Created only after disaster**

Choose:

**Pilot Light**

---

## Scenario 2 — Nothing Running

Only:

- Backups
- Snapshots
- IaC templates

exist in the DR Region.

Choose:

**Backup and Restore**

not Pilot Light.

---

## Scenario 3 — Entire Stack Running Small

Secondary Region already has:

- Load balancer
- Application servers
- Database

and can:

**Immediately serve limited production traffic**

Choose:

**Warm Standby**

not Pilot Light.

---

## Scenario 4 — Full Production Capacity

Both Regions are:

**Production-capable**

Choose:

**Multi-Site**

---

## Scenario 5 — Reduce Pilot Light RTO

Company wants faster recovery without maintaining:

**A full standby stack**

Use:

- IaC
- AMIs
- Auto Scaling
- Automated database promotion
- Automated DNS changes

---

## Scenario 6 — Regional Database DR

RDS database must remain:

**Continuously replicated**

to another Region.

Think:

**Cross-Region Read Replica**

where supported.

---

## Scenario 7 — Aurora DR

Aurora database requires:

**Low-lag cross-Region replication**

Think:

**Aurora Global Database**

---

## Scenario 8 — DynamoDB DR

DynamoDB data must exist:

**Across multiple Regions**

Think:

**Global Tables**

---

# Scenario Recognition

Immediately think:

**Pilot Light**

when you see:

- Critical core running
- Database replica running
- Data continuously replicated
- Compute launched after disaster
- Application servers stopped
- Infrastructure provisioned during recovery

---

## Think Backup and Restore When You See

- Backups only
- Rebuild everything
- Long recovery time
- Lowest cost

---

## Think Warm Standby When You See

- Complete environment running
- Reduced capacity
- Can already serve traffic

---

## Think Multi-Site When You See

- Full environments
- Active production
- Near-immediate failover

---

# Exam Traps

## Trap 1 — Pilot Light Means the Entire Application Is Running Small

❌

That is:

**Warm Standby**

Pilot Light keeps:

**Critical core components running**

---

## Trap 2 — Pilot Light Means Only Backups Exist

❌

That is closer to:

**Backup and Restore**

Pilot Light has:

**Core infrastructure already running**

---

## Trap 3 — Pilot Light Has the Lowest RTO

❌

Warm Standby and Multi-Site generally provide:

**Faster recovery**

---

## Trap 4 — Pilot Light Is the Lowest-Cost DR Strategy

❌

Backup and Restore is generally:

**Lower cost**

---

## Trap 5 — Continuous Data Replication Means the Application Is Ready

❌

The application tier may still need to be:

- Provisioned
- Started
- Scaled
- Validated

---

## Trap 6 — Route 53 Should Immediately Send Traffic to an Unprepared Pilot Light

❌

The DR environment must first become:

**Production ready**

---

# Quick Cheat Sheet

| Exam Clue | Answer |
|---|---|
| Critical Core Running | Pilot Light |
| Database Running, Compute Off | Pilot Light |
| Continuous Data Replication | Common Pilot Light Pattern |
| Nothing Running | Backup & Restore |
| Full Stack Running Small | Warm Standby |
| Full Production Environment | Multi-Site |
| Faster Than Backup & Restore | Pilot Light |
| Slower Than Warm Standby | Pilot Light |
| Rapid Compute Launch | Auto Scaling |
| Recreate Infrastructure | IaC |
| Redirect After Recovery | Route 53 |
| Aurora Cross-Region DR | Aurora Global Database |
| DynamoDB Multi-Region | Global Tables |

---

# DR Strategy Decision Map

Need:

**Backups only**

→ Backup and Restore

Need:

**Core running**

→ Pilot Light

Need:

**Whole stack running small**

→ Warm Standby

Need:

**Whole stack running full**

→ Multi-Site

---

# Pilot Light Recovery Map

> **BEFORE DISASTER**
>
> Data Replication
> ↓
> Critical Core Running
>
> ---
>
> **DISASTER**
>
> ↓
>
> Promote / Activate Data Layer
> ↓
> Provision Compute
> ↓
> Scale Application
> ↓
> Validate
> ↓
> Redirect Traffic
>
> ---
>
> **RECOVERED**

---

# Final Exam Rapid-Fire

> **CORE RUNNING**
> → PILOT LIGHT
>
> **DATABASE RUNNING + COMPUTE OFF**
> → PILOT LIGHT
>
> **BACKUPS ONLY**
> → BACKUP AND RESTORE
>
> **FULL STACK RUNNING SMALL**
> → WARM STANDBY
>
> **FULL STACK RUNNING FULL**
> → MULTI-SITE
>
> **FAST PROVISIONING**
> → INFRASTRUCTURE AS CODE
>
> **FAST COMPUTE SCALE**
> → AUTO SCALING
>
> **DNS FAILOVER**
> → ROUTE 53
>
> **AURORA CROSS-REGION**
> → GLOBAL DATABASE
>
> **DYNAMODB MULTI-REGION**
> → GLOBAL TABLES

---

## Master Memory Trick

> [!tip] Pilot Light Master Memory Trick
> Imagine your main restaurant is destroyed.
>
> In another city, you already have:
>
> **THE GAS PILOT LIGHT BURNING**
>
> and:
>
> **THE CRITICAL FOOD SUPPLY READY**
>
> But you do NOT yet have:
>
> **A FULL RESTAURANT OPERATING**
>
> When disaster happens:
>
> Turn on the equipment.
>
> Bring in the staff.
>
> Open the dining room.
>
> Scale everything up.
>
> Then:
>
> **SERVE CUSTOMERS**
>
> That's:
>
> **PILOT LIGHT**

So remember:

> **BACKUP AND RESTORE**
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
> **PILOT LIGHT**
> → CORE ALIVE, REST STARTS LATER

And the killer SAA question:

> **"Are the critical core components continuously running in the DR environment while the remaining application infrastructure must be started or provisioned after the disaster?"**
>
> YES
>
> → **Pilot Light**

---

## Related Notes

- [[Disaster Recovery Overview]]
- [[Backup and Restore]]
- [[RDS]]
- [[Aurora]]
- [[DynamoDB]]
- [[S3]]
- [[Auto Scaling]]
- [[Route 53]]
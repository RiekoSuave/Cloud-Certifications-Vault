## Core Concept

Warm Standby is a Disaster Recovery strategy where:

**A complete but scaled-down version of the production environment is already running in the DR location**

Unlike Pilot Light:

**The full application stack exists and is functional**

but it operates at:

**Reduced capacity**

During a disaster, you:

1. Scale the DR environment up
2. Redirect traffic
3. Continue production

Architecture:

Primary Region  
↓  
Production Traffic

Secondary Region  
↓  
Small Functional Environment  
↓  
Ready to Scale

> [!tip] Memory Trick
> **Warm Standby = Whole Stack Running Small**

---

# What Stays Running?

In Warm Standby, the DR environment typically includes:

- Load balancer
- Application servers
- Database
- Networking
- Security controls
- Application configuration

The environment is:

**Already functional**

but:

**Not sized for full production traffic**

### Killer Exam Clue

> **Secondary Region has the full application stack running at reduced capacity**
>
> → **Warm Standby**

---

# Before Disaster

Example:

## Primary Region

Users  
↓  
Load Balancer  
↓  
Large Application Fleet  
↓  
Primary Database

## Secondary Region

Small Load Balancer Capacity  
↓  
Small Application Fleet  
↓  
Replicated Database

The secondary environment can:

**Already operate**

but may only support:

**Limited traffic**

---

# During Disaster

If the primary Region fails:

Secondary Region  
↓  
Scale Compute  
↓  
Increase Application Capacity  
↓  
Promote / Scale Database  
↓  
Redirect Traffic  
↓  
Full Production

### Key Principle

> **Warm Standby recovery is mostly about scaling up, not building from scratch**

---

# RTO

Warm Standby usually provides:

**Lower RTO than Pilot Light**

because:

**The complete environment is already running**

The main recovery actions are:

- Scale
- Promote
- Redirect

rather than:

**Provision the entire application stack**

### Recovery Speed

Backup & Restore  
↓  
Pilot Light  
↓  
**Warm Standby**  
↓  
Multi-Site

From:

**Slower**

to:

**Faster**

---

# RPO

Warm Standby can support:

**Low RPO**

when data is:

**Continuously replicated**

Example:

Primary Database  
↓  
Cross-Region Replication  
↓  
Standby Database

### Killer Exam Principle

> **Warm Standby reduces RTO through pre-running infrastructure, while replication strategy determines RPO**

---

# Warm Standby vs Pilot Light

This comparison is extremely important.

## [[Pilot Light]]

Secondary environment:

**Core components only**

Application infrastructure may need to be:

- Provisioned
- Started
- Activated

## Warm Standby

Secondary environment:

**Complete application stack is already running**

but at:

**Reduced capacity**

### Killer Shortcut

> **Core Only**
> → Pilot Light
>
> **Whole Stack Running Small**
> → Warm Standby

---

# Warm Standby vs Multi-Site

## Warm Standby

Secondary environment:

**Running below full production capacity**

During disaster:

**Scale up**

## Multi-Site

Secondary environment:

**Already production-capable**

and may already be:

**Serving production traffic**

### Killer Shortcut

> **Scale After Disaster**
> → Warm Standby
>
> **Already Full**
> → Multi-Site

---

# Warm Standby vs Backup and Restore

## Backup and Restore

DR infrastructure is largely:

**Not running**

## Warm Standby

DR environment is:

**Already operational**

### Memory Trick

**Backup = Rebuild**

**Warm = Scale**

---

# Cost

Warm Standby generally costs:

**More than Pilot Light**

because:

**The full application stack stays running**

However, it generally costs:

**Less than Multi-Site**

because:

**The DR environment is smaller than full production**

### Cost Order

Backup & Restore  
↓  
Pilot Light  
↓  
**Warm Standby**  
↓  
Multi-Site

From:

**Lower cost**

to:

**Higher cost**

---

# Reduced Capacity

The key phrase is:

**Reduced Capacity**

Examples:

Production:

20 EC2 instances

Warm Standby:

2 EC2 instances

During disaster:

2 instances  
↓  
Auto Scaling  
↓  
20 instances

### Killer Exam Clue

> **DR environment can already serve traffic but must scale before handling full production load**
>
> → **Warm Standby**

---

# Auto Scaling

[[Auto Scaling]] is especially useful in Warm Standby.

Architecture:

Secondary Region  
↓  
Small Auto Scaling Group  
↓  
Disaster  
↓  
Increase Desired Capacity  
↓  
Full Production Fleet

### Memory Trick

**Warm Standby = Running Small, Scale Fast**

---

# Load Balancer

A Warm Standby environment commonly already includes:

**A functional load balancer**

This means traffic can be redirected without first creating:

**The entire front-end architecture**

### Exam Principle

> **The secondary environment should already be functional end-to-end**

---

# Database Replication

Warm Standby typically relies on:

**Continuous or frequent database replication**

Possible patterns include:

- RDS Cross-Region Read Replica
- Aurora Global Database
- DynamoDB Global Tables
- Other supported replication models

### Killer Exam Clue

> **Secondary application stack is running and database data is continuously replicated**
>
> → Strong Warm Standby pattern

---

# RDS Cross-Region Read Replica

For supported [[RDS]] engines:

Primary RDS  
↓  
Cross-Region Replication  
↓  
Read Replica

During disaster:

Read Replica  
↓  
Promote  
↓  
DR Database

### Exam Principle

> **Database promotion may still be part of Warm Standby recovery**

---

# Aurora Global Database

[[Aurora]] Global Database is useful when:

- Aurora is used
- Cross-Region replication is required
- Low replication lag matters
- Faster regional recovery is desired

### Killer Exam Clue

> **Aurora-based Warm Standby across Regions**
>
> → **Aurora Global Database**

---

# DynamoDB Global Tables

[[DynamoDB]] Global Tables can keep:

**Multi-Region active replicas**

This can reduce database recovery work in:

**Warm Standby or Multi-Site architectures**

---

# S3 Cross-Region Replication

[[S3]] can replicate application assets and objects to:

**The secondary Region**

This helps ensure DR infrastructure can access:

**Required application data immediately**

---

# Route 53 Failover

[[Route 53]] can redirect users from:

**Primary Region**

to:

**Warm Standby Region**

Architecture:

Primary Region  
❌  
↓  
Route 53 Failover  
↓  
Secondary Region  
✅

Because the secondary environment already works:

**Failover can happen faster than Pilot Light**

---

# Health Checks

Route 53 health checks can monitor:

**Primary endpoints**

If unhealthy:

Traffic can be redirected according to:

**Failover routing**

### Killer Exam Clue

> **Automatically redirect users to warm standby Region when primary fails**
>
> → **Route 53 Failover Routing**

---

# Global Accelerator

Global applications may use:

**Global Accelerator**

to shift traffic toward:

**Healthy regional endpoints**

This can provide:

**Fast network-level failover**

for supported architectures.

---

# Infrastructure as Code

Even though the full stack already exists, IaC remains useful for:

- Keeping environments consistent
- Rebuilding failed components
- Scaling architectures
- Preventing configuration drift

### Exam Principle

> **Warm Standby still benefits from reproducible infrastructure**

---

# Configuration Consistency

The DR environment should closely match:

**Production configuration**

Otherwise failover may expose:

- Missing dependencies
- Security differences
- Version drift
- Application incompatibilities

### Memory Trick

> **Smaller Does Not Mean Different**

Warm Standby should be:

**Same architecture, less capacity**

---

# DR Environment Must Be Functional

A Warm Standby environment should be able to:

**Serve real application requests**

even before scaling.

This is the critical distinction from:

**Pilot Light**

### Killer Exam Test

Ask:

> **Can the DR environment already run the application end-to-end?**

YES, but smaller  
→ Warm Standby

NO, core only  
→ Pilot Light

---

# Testing

Warm Standby should be:

**Regularly tested**

Testing should confirm:

- Application works
- Database replication is healthy
- Scaling works
- DNS failover works
- Security controls work
- Capacity can increase

---

# Failover Workflow

Example:

Primary Region Failure  
↓  
Health Check Fails  
↓  
Promote / Confirm Database  
↓  
Scale Auto Scaling Group  
↓  
Validate Environment  
↓  
Route 53 Redirects Traffic  
↓  
DR Region Handles Production

### Memory Trick

**Promote → Scale → Route**

---

# Failback

After the primary Region is restored:

1. Re-establish data synchronization
2. Restore primary environment
3. Validate application
4. Redirect traffic
5. Return secondary to standby capacity

### Exam Principle

> **Failback must be planned just like failover**

---

# Multi-AZ Within Warm Standby

The secondary Region should still use:

**High Availability principles**

For example:

- Multiple AZs
- Load balancing
- Auto Scaling
- Multi-AZ database configuration where appropriate

### Killer Exam Principle

> **A DR Region should not become a new single point of failure**

---

# Architecture Thinking

## Scenario 1 — Full Stack Running Small

Primary Region has:

20 EC2 instances

Secondary Region has:

2 EC2 instances

plus:

- Load balancer
- Database replica
- Networking

Choose:

**Warm Standby**

---

## Scenario 2 — Database Only

Secondary Region has:

Database replication

but no active application tier.

Choose:

**Pilot Light**

---

## Scenario 3 — Backups Only

Secondary Region has:

Snapshots and IaC

but no running environment.

Choose:

**Backup and Restore**

---

## Scenario 4 — Full Capacity in Both Regions

Both Regions can immediately handle:

**Full production traffic**

Choose:

**Multi-Site**

---

## Scenario 5 — Faster Recovery Than Pilot Light

Business requires:

**Low downtime**

but cannot justify full Multi-Site cost.

Choose:

**Warm Standby**

when it satisfies RTO/RPO.

---

## Scenario 6 — Scale During Failover

Secondary environment is functional but cannot handle:

**Normal production volume**

Use:

**Auto Scaling**

during recovery.

---

## Scenario 7 — Database Promotion

Secondary RDS Read Replica exists.

During disaster:

Promote replica  
↓  
Scale applications  
↓  
Redirect traffic

This is a typical:

**Warm Standby workflow**

---

# Scenario Recognition

Immediately think:

**Warm Standby**

when you see:

- Complete DR environment
- Reduced capacity
- Already functional
- Scale up after disaster
- Lower RTO than Pilot Light
- Secondary Region running small

---

## Think Pilot Light When You See

- Database/core only
- App tier not operational
- Provision compute after disaster

---

## Think Backup and Restore When You See

- Backups only
- Infrastructure rebuilt after disaster

---

## Think Multi-Site When You See

- Both Regions full scale
- Active-active
- Near-immediate failover
- Production traffic already served

---

# Exam Traps

## Trap 1 — Warm Standby Means Only the Database Is Running

❌

That is:

**Pilot Light**

Warm Standby has:

**The full stack running**

---

## Trap 2 — Warm Standby Means Full Production Capacity

❌

That is closer to:

**Multi-Site**

Warm Standby is:

**Reduced capacity**

---

## Trap 3 — Warm Standby Requires Rebuilding the Entire Environment

❌

That is closer to:

**Backup and Restore**

---

## Trap 4 — Warm Standby Is the Cheapest DR Strategy

❌

Backup and Restore and Pilot Light generally cost:

**Less**

---

## Trap 5 — Warm Standby Has the Fastest Possible RTO

❌

Multi-Site generally provides:

**Faster recovery**

---

## Trap 6 — Same Architecture Means Same Capacity

❌

Warm Standby usually uses:

**Same functional stack**

but:

**Smaller capacity**

---

# Quick Cheat Sheet

| Exam Clue | Answer |
|---|---|
| Full DR Stack Running | Warm Standby |
| Reduced Capacity | Warm Standby |
| Scale During Disaster | Warm Standby |
| Core Only | Pilot Light |
| Backups Only | Backup & Restore |
| Full Production Capacity | Multi-Site |
| Scale Compute | Auto Scaling |
| DNS Failover | Route 53 |
| RDS Cross-Region DR | Read Replica |
| Aurora Cross-Region | Global Database |
| DynamoDB Multi-Region | Global Tables |

---

# DR Strategy Decision Map

Need:

**Rebuild after disaster**

→ Backup and Restore

Need:

**Critical core already running**

→ Pilot Light

Need:

**Complete environment already running small**

→ Warm Standby

Need:

**Complete environment already running full**

→ Multi-Site

---

# Four-Strategy Comparison

| Strategy | DR Environment Before Disaster | Recovery Action |
|---|---|---|
| Backup & Restore | Backups | Rebuild + Restore |
| Pilot Light | Core Only | Provision + Scale |
| Warm Standby | Full Stack, Small | Scale |
| Multi-Site | Full Stack, Full | Redirect |

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

# Warm Standby Recovery Map

> **BEFORE DISASTER**
>
> Full Application Stack
> ↓
> Reduced Capacity
>
> ---
>
> **DISASTER**
>
> ↓
>
> Promote / Confirm Data Layer
> ↓
> Scale Compute
> ↓
> Increase Capacity
> ↓
> Redirect Traffic
>
> ---
>
> **FULL PRODUCTION**

---

# Final Exam Rapid-Fire

> **FULL STACK RUNNING SMALL**
> → WARM STANDBY
>
> **ALREADY FUNCTIONAL**
> → WARM STANDBY
>
> **SCALE AFTER DISASTER**
> → WARM STANDBY
>
> **CORE ONLY**
> → PILOT LIGHT
>
> **BACKUPS ONLY**
> → BACKUP AND RESTORE
>
> **FULL CAPACITY**
> → MULTI-SITE
>
> **SCALE COMPUTE**
> → AUTO SCALING
>
> **REDIRECT USERS**
> → ROUTE 53
>
> **AURORA DR**
> → GLOBAL DATABASE
>
> **DYNAMODB DR**
> → GLOBAL TABLES

---

## Master Memory Trick

> [!tip] Warm Standby Master Memory Trick
> Imagine your primary restaurant closes because of:
>
> **A DISASTER**
>
> In another city, you already have:
>
> **A SECOND RESTAURANT**
>
> It has:
>
> - Kitchen
> - Staff
> - Tables
> - Food
> - Working registers
>
> Customers could already eat there.
>
> The problem?
>
> It only has:
>
> **10 TABLES**
>
> while the primary restaurant had:
>
> **100 TABLES**
>
> During disaster recovery:
>
> Add tables.
>
> Bring in more staff.
>
> Increase capacity.
>
> Then:
>
> **SEND EVERYONE THERE**
>
> That's:
>
> **WARM STANDBY**

So remember:

> **BACKUP AND RESTORE**
> → REBUILD
>
> **PILOT LIGHT**
> → CORE RUNNING
>
> **WARM STANDBY**
> → WHOLE STACK RUNNING SMALL
>
> **MULTI-SITE**
> → WHOLE STACK RUNNING FULL

And the killer SAA question:

> **"Is a complete, functional DR environment already running at reduced capacity and only needs to scale up during a disaster?"**
>
> YES
>
> → **Warm Standby**

---

## Related Notes

- [[Disaster Recovery Overview]]
- [[Backup and Restore]]
- [[Pilot Light]]
- [[RDS]]
- [[Aurora]]
- [[DynamoDB]]
- [[S3]]
- [[Auto Scaling]]
- [[Route 53]]
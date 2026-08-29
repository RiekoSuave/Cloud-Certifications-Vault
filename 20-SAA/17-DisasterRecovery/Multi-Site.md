## Core Concept

Multi-Site is the Disaster Recovery strategy where:

**Multiple environments are already running at full or near-full production capability**

These environments may operate:

- Active-active
- Active-passive with near-immediate failover
- Across multiple AWS Regions

Architecture:

Users  
↓  
Global Routing  
↓  
Region A  
+
Region B

Both environments are:

**Production ready**

> [!tip] Memory Trick
> **Multi-Site = Full Environment Already Running**

---

# Main Goal

Multi-Site is designed for workloads that require:

- Very low RTO
- Very low RPO
- Minimal downtime
- High resilience
- Fast regional failover

### Killer Exam Clue

> **Application requires near-immediate recovery and the business accepts the highest DR operating cost**
>
> → **Multi-Site**

---

# Before Disaster

Unlike other DR strategies:

**You do not wait for disaster to build the environment**

Both regions already have:

- Compute
- Load balancing
- Networking
- Security controls
- Application deployment
- Data replication
- Production-ready capacity

### Memory Trick

**Nothing Major to Build**

---

# During Disaster

If Region A fails:

Region B  
↓  
Already Running  
↓  
Traffic Redirected  
↓  
Production Continues

Recovery actions are focused on:

- Routing
- Health checks
- Database failover where needed
- Traffic redistribution

rather than:

**Building or scaling the entire environment**

---

# RTO

Multi-Site generally provides:

**The lowest RTO**

among the major DR strategies.

Why?

Because:

**The secondary environment is already operational**

### Recovery Speed

Backup & Restore  
↓  
Pilot Light  
↓  
Warm Standby  
↓  
**Multi-Site**

From:

**Slowest**

to:

**Fastest**

---

# RPO

Multi-Site can support:

**Very low RPO**

when the data layer uses:

- Continuous replication
- Multi-Region databases
- Global tables
- Cross-Region replication

### Killer Exam Principle

> **Multi-Site infrastructure lowers RTO, while replication architecture determines how low RPO can be**

---

# Cost

Multi-Site generally has:

**The highest ongoing cost**

because multiple environments remain:

**Production capable**

before any disaster occurs.

### Cost Order

Backup & Restore  
↓  
Pilot Light  
↓  
Warm Standby  
↓  
**Multi-Site**

From:

**Lowest cost**

to:

**Highest cost**

---

# Active-Active

A common Multi-Site pattern is:

**Active-Active**

Both environments:

**Serve production traffic simultaneously**

Architecture:

Users  
↓  
Global Routing  
↓  
Region A + Region B

### Benefits

- Very fast failover
- Better global performance
- More efficient use of secondary infrastructure

### Killer Exam Clue

> **Both Regions actively serve production traffic**
>
> → **Active-Active Multi-Site**

---

# Active-Passive Multi-Site

Another pattern is:

**Active-Passive**

Primary Region:

**Serves production**

Secondary Region:

**Already full-capacity and ready**

During failure:

Traffic switches to:

**Secondary Region**

### Key Difference From Warm Standby

The secondary site is already:

**Production-scale**

rather than:

**Reduced capacity**

---

# Multi-Site vs Warm Standby

## [[Warm Standby]]

Secondary environment:

**Running smaller**

During disaster:

**Scale up**

## Multi-Site

Secondary environment:

**Already full or near-full production capability**

During disaster:

**Redirect traffic**

### Killer Shortcut

> **Scale**
> → Warm Standby
>
> **Route**
> → Multi-Site

---

# Multi-Site vs Pilot Light

## [[Pilot Light]]

Only:

**Critical core components**

remain running.

## Multi-Site

The:

**Entire production stack**

already exists and operates.

### Memory Trick

**Pilot = Tiny Flame**

**Multi-Site = Full Fire**

---

# Multi-Site vs Backup and Restore

## Backup and Restore

After disaster:

**Rebuild**

## Multi-Site

After disaster:

**Redirect**

These are opposite ends of the:

**DR spectrum**

---

# Global Traffic Management

Multi-Site requires a way to direct users between:

**Healthy environments**

Possible services include:

- [[Route 53]]
- Global Accelerator
- CloudFront depending on architecture

### Exam Principle

> **A second Region is not useful if clients cannot be redirected to it**

---

# Route 53 Failover Routing

[[Route 53]] can direct traffic to:

**Primary Region**

and fail over to:

**Secondary Region**

Architecture:

Users  
↓  
Route 53  
↓  
Primary Region

If unhealthy:

Route 53  
↓  
Secondary Region

### Killer Exam Clue

> **DNS-based active-passive regional failover**
>
> → **Route 53 Failover Routing**

---

# Route 53 Latency-Based Routing

For active-active architectures:

Route 53 can use:

**Latency-Based Routing**

to send users toward:

**The Region providing the best latency**

### Killer Exam Clue

> **Global users should connect to the Region with the lowest latency**
>
> → **Latency-Based Routing**

---

# Route 53 Weighted Routing

Weighted routing can distribute:

**Specified percentages of traffic**

between:

**Multiple environments**

Example:

Region A  
→ 70%

Region B  
→ 30%

This can support:

- Controlled traffic distribution
- Migration
- Testing
- Active-active architectures

---

# Global Accelerator

Global Accelerator provides:

**Static anycast IP addresses**

and directs traffic through:

**The AWS global network**

toward healthy endpoints.

### Killer Exam Clue

> **Need fast global failover using static IP addresses**
>
> → **Global Accelerator**

---

# Route 53 vs Global Accelerator

## Route 53

Think:

**DNS-based routing**

## Global Accelerator

Think:

**Network-level traffic routing with static anycast IPs**

### Killer Shortcut

DNS failover  
→ Route 53

Static global IP + fast endpoint failover  
→ Global Accelerator

---

# Aurora Global Database

[[Aurora]] Global Database is especially useful for:

**Multi-Region Aurora applications**

Architecture:

Primary Aurora Region  
↓  
Cross-Region Replication  
↓  
Secondary Aurora Region

### Benefits

- Low-lag replication
- Cross-Region reads
- Faster regional recovery

### Killer Exam Clue

> **Aurora must support low-RPO cross-Region DR**
>
> → **Aurora Global Database**

---

# DynamoDB Global Tables

[[DynamoDB]] Global Tables provide:

**Multi-Region active-active replication**

This is especially useful for:

**True active-active application architectures**

### Killer Exam Clue

> **DynamoDB writes must be accepted in multiple Regions**
>
> → **Global Tables**

### Memory Trick

**Global Tables = Multi-Region DynamoDB Active-Active**

---

# S3 Cross-Region Replication

[[S3]] can use:

**Cross-Region Replication**

to keep objects available across:

**Multiple Regions**

This may support:

- Static assets
- Application content
- DR copies
- Global workloads

---

# Database Conflict Considerations

Active-active systems can introduce:

**Data consistency challenges**

especially when writes occur in:

**Multiple locations**

Applications must consider:

- Conflict resolution
- Replication behavior
- Consistency model
- Data ownership

### Exam Principle

> **Active-active is powerful but more complex than active-passive**

---

# Stateless Applications

Multi-Site works especially well when application servers are:

**Stateless**

State should be stored in:

- Shared data stores
- Replicated databases
- Distributed caches
- Externalized session stores

### Killer Exam Principle

> **Stateless application tiers are easier to fail over across Regions**

---

# Session State

Do not store critical session state only in:

**One EC2 instance**

Better:

Store session state in a:

**Distributed or replicated data store**

so users can fail over between:

**Regions**

---

# Infrastructure Consistency

Both environments should remain:

**Consistent**

Use:

- CloudFormation
- Terraform
- CI/CD
- Automated deployments

to prevent:

**Configuration drift**

### Memory Trick

**Multi-Site Must Be Multi-Same**

---

# Deployment Strategy

Applications may need to deploy:

**The same software version**

to both Regions.

Otherwise:

Failover can send users to:

**An incompatible environment**

### Exam Principle

> **DR environments should not become stale**

---

# Multi-AZ Inside Each Region

Each Region should still follow:

**High Availability best practices**

Example:

Region A:

- Multiple AZs
- Load Balancer
- Auto Scaling

Region B:

- Multiple AZs
- Load Balancer
- Auto Scaling

### Killer Exam Principle

> **Multi-Region does not replace Multi-AZ**

---

# Failure Domains

A robust architecture may protect against:

## Instance Failure

→ Auto Scaling / Load Balancing

## AZ Failure

→ Multi-AZ

## Region Failure

→ Multi-Region / Multi-Site

### Memory Trick

> **Instance**
> → Replace
>
> **AZ**
> → Multi-AZ
>
> **Region**
> → Multi-Region

---

# Health Checks

Traffic-routing systems need:

**Reliable health checks**

to determine:

**Which environment can receive traffic**

Bad health checks can cause:

- False failovers
- Failed failovers
- Traffic sent to unhealthy systems

### Exam Principle

> **Health checks are a critical part of automated DR**

---

# Failover Testing

Multi-Site architectures should be:

**Tested regularly**

A common strategy is to intentionally route traffic toward:

**The secondary Region**

to verify:

- Application health
- Capacity
- DNS
- Database behavior
- Security
- Replication

---

# Failback

After the failed Region returns:

Organizations must decide whether to:

- Continue using secondary
- Restore active-active balance
- Return primary role
- Synchronize data

### Exam Principle

> **Failback can be just as important as failover**

---

# Architecture Thinking

## Scenario 1 — Near-Zero Downtime

Financial application requires:

**Almost no downtime**

Choose:

**Multi-Site**

when cost is acceptable.

---

## Scenario 2 — Full Capacity Secondary

Primary Region serves traffic.

Secondary Region is:

**Already capable of handling full production load**

Choose:

**Multi-Site Active-Passive**

---

## Scenario 3 — Both Regions Serve Users

Users are routed to:

**Both Regions simultaneously**

Choose:

**Active-Active Multi-Site**

---

## Scenario 4 — Secondary Running Small

Secondary Region is functional but has:

**Only 10% of production compute**

Choose:

**Warm Standby**

not Multi-Site.

---

## Scenario 5 — Core Only

Secondary Region contains:

Database replica

but application servers are not running.

Choose:

**Pilot Light**

---

## Scenario 6 — Global DynamoDB

Application needs:

**Multi-Region writes**

Choose:

**DynamoDB Global Tables**

---

## Scenario 7 — Aurora DR

Application uses Aurora and requires:

**Very low cross-Region replication lag**

Choose:

**Aurora Global Database**

---

## Scenario 8 — Fast Static-IP Failover

Clients need:

**Static global IP addresses**

and fast endpoint failover.

Choose:

**Global Accelerator**

---

## Scenario 9 — Lowest Latency

Users should access:

**The nearest/lowest-latency Region**

Choose:

**Route 53 Latency-Based Routing**

---

# Scenario Recognition

Immediately think:

**Multi-Site**

when you see:

- Full secondary environment
- Production-capable secondary
- Active-active
- Near-zero downtime
- Very low RTO
- Multi-Region production
- Highest DR availability

---

## Think Warm Standby When You See

- Full stack
- Reduced capacity
- Scale after disaster

---

## Think Pilot Light When You See

- Core only
- Compute off
- Database replication

---

## Think Backup and Restore When You See

- Backups only
- Rebuild after failure

---

# Exam Traps

## Trap 1 — Multi-Site Means Secondary Is Running Small

❌

That is:

**Warm Standby**

---

## Trap 2 — Multi-Site Is the Lowest-Cost DR Strategy

❌

It generally has:

**The highest ongoing cost**

---

## Trap 3 — Multi-Site Automatically Means Zero RPO

❌

RPO still depends on:

**Data replication architecture**

---

## Trap 4 — Multi-Region Means Multi-AZ Is Unnecessary

❌

Each Region should still use:

**High Availability design**

---

## Trap 5 — Active-Active Is Simpler Than Active-Passive

❌

Active-active generally introduces:

**More data and routing complexity**

---

## Trap 6 — Second Region Alone Guarantees Failover

❌

You also need:

- Routing
- Health checks
- Replication
- Capacity
- Security
- Testing

---

# Quick Cheat Sheet

| Exam Clue | Answer |
|---|---|
| Lowest RTO | Multi-Site |
| Highest DR Cost | Multi-Site |
| Full Secondary Environment | Multi-Site |
| Both Regions Serving Traffic | Active-Active |
| Full Secondary Waiting | Active-Passive Multi-Site |
| Small Secondary | Warm Standby |
| Core Only | Pilot Light |
| Backups Only | Backup & Restore |
| DNS Failover | Route 53 |
| Static Global IP Failover | Global Accelerator |
| Aurora Multi-Region | Global Database |
| DynamoDB Active-Active | Global Tables |

---

# DR Strategy Decision Map

Need:

**Rebuild after disaster**

→ Backup and Restore

Need:

**Core already running**

→ Pilot Light

Need:

**Full stack running small**

→ Warm Standby

Need:

**Full stack already production-capable**

→ Multi-Site

---

# Four Strategy Recovery Actions

| Strategy | Main Recovery Action |
|---|---|
| Backup & Restore | Rebuild |
| Pilot Light | Provision / Start |
| Warm Standby | Scale |
| Multi-Site | Redirect |

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

# Multi-Site Architecture Map

> **USERS**
> ↓
> GLOBAL TRAFFIC MANAGEMENT
> ↓
> REGION A + REGION B
>
> Each Region:
>
> Load Balancer
> ↓
> Auto Scaling
> ↓
> Application
> ↓
> Replicated Data Layer

---

# Final Exam Rapid-Fire

> **NEAR-ZERO DOWNTIME**
> → MULTI-SITE
>
> **LOWEST RTO**
> → MULTI-SITE
>
> **FULL SECONDARY**
> → MULTI-SITE
>
> **BOTH REGIONS ACTIVE**
> → ACTIVE-ACTIVE
>
> **FULL SECONDARY WAITING**
> → ACTIVE-PASSIVE
>
> **SMALL SECONDARY**
> → WARM STANDBY
>
> **CORE ONLY**
> → PILOT LIGHT
>
> **BACKUPS ONLY**
> → BACKUP AND RESTORE
>
> **DNS FAILOVER**
> → ROUTE 53
>
> **STATIC GLOBAL IP**
> → GLOBAL ACCELERATOR
>
> **AURORA MULTI-REGION**
> → GLOBAL DATABASE
>
> **DYNAMODB MULTI-REGION WRITES**
> → GLOBAL TABLES

---

## Master Memory Trick

> [!tip] Multi-Site Master Memory Trick
> Imagine you own:
>
> **TWO FULL RESTAURANTS**
>
> Both have:
>
> - Full kitchens
> - Full staff
> - Full inventory
> - Full seating capacity
>
> If one restaurant suddenly closes:
>
> you do NOT need to:
>
> **BUILD**
>
> **START**
>
> or:
>
> **SCALE**
>
> the second restaurant.
>
> You simply:
>
> **SEND THE CUSTOMERS THERE**
>
> That's:
>
> **MULTI-SITE**

So remember:

> **BACKUP AND RESTORE**
> → BUILD
>
> **PILOT LIGHT**
> → START
>
> **WARM STANDBY**
> → SCALE
>
> **MULTI-SITE**
> → ROUTE
>
> **MULTI-SITE**
> → FASTEST RECOVERY
>
> **MULTI-SITE**
> → HIGHEST COST

And the killer SAA question:

> **"Is a complete production-capable environment already running in another location so recovery mainly requires redirecting traffic?"**
>
> YES
>
> → **Multi-Site**

---

## Related Notes

- [[Disaster Recovery Overview]]
- [[Backup and Restore]]
- [[Pilot Light]]
- [[Warm Standby]]
- [[Route 53]]
- [[Aurora]]
- [[DynamoDB]]
- [[S3]]
- [[Auto Scaling]]
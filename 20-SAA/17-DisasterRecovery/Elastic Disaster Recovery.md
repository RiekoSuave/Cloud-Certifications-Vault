## Core Concept

Elastic Disaster Recovery provides:

**Continuous block-level replication of servers into AWS for disaster recovery**

It is designed to help recover:

- Physical servers
- Virtual machines
- On-premises workloads
- Cloud-based servers
- Supported application servers

Architecture:

Source Servers  
↓  
Continuous Block-Level Replication  
↓  
Low-Cost Staging Area in AWS  
↓  
Disaster  
↓  
Launch Recovery Instances

> [!tip] Memory Trick
> **Elastic Disaster Recovery = Replicate First, Launch Later**

---

# What Problem Does It Solve?

Without a DR service, recovering servers may require:

- Restoring backups
- Rebuilding operating systems
- Reinstalling applications
- Reconfiguring networking
- Restoring large amounts of data

Elastic Disaster Recovery continuously replicates:

**Server disks**

into AWS so recovery can happen:

**Much faster**

### Killer Exam Clue

> **Need continuous server replication into AWS with low-cost standby infrastructure**
>
> → **Elastic Disaster Recovery**

---

# Continuous Replication

Elastic Disaster Recovery continuously replicates:

**Block-level changes**

from source servers into:

**AWS**

This helps maintain a recent copy of:

**Server data**

### Memory Trick

**Changed Disk Blocks → Replicated to AWS**

---

# Block-Level Replication

Block-level replication operates below:

**The file/application level**

It replicates changes to:

**Storage blocks**

rather than requiring applications to manually:

**Copy individual files**

### Killer Exam Clue

> **Need server-level disaster recovery using continuous block replication**
>
> → **Elastic Disaster Recovery**

---

# Source Servers

Source workloads can include supported:

- Physical servers
- Virtual machines
- On-premises servers
- EC2 instances
- Other cloud-hosted servers

This makes Elastic Disaster Recovery useful for:

**Migration-style DR and hybrid environments**

---

# Replication Agent

A source server uses:

**A replication agent**

to send disk changes toward:

**The AWS staging environment**

Architecture:

Source Server  
↓  
Replication Agent  
↓  
AWS  
↓  
Staging Area

### Memory Trick

**Agent = Sends Changed Blocks**

---

# Staging Area

One of the most important concepts is:

**Low-cost staging infrastructure**

Instead of running:

**Full production-sized recovery servers continuously**

Elastic Disaster Recovery maintains:

**Replication resources**

until recovery is required.

### Killer Exam Clue

> **Need fast server recovery without paying for full standby compute all the time**
>
> → **Elastic Disaster Recovery**

---

# Low-Cost Architecture

Before disaster:

Source Servers  
↓  
Replication  
↓  
Low-Cost AWS Staging Resources

You do NOT necessarily keep:

**Full-size production recovery instances running**

### Memory Trick

**Store the Replica Cheaply**

**Launch the Big Servers When Needed**

---

# Recovery Instances

During a disaster:

Replicated Data  
↓  
Launch Recovery Instances  
↓  
Configure Networking  
↓  
Validate Workload  
↓  
Serve Production

Recovery instances are created using:

**The replicated server state**

### Killer Exam Principle

> **Production-capable recovery infrastructure is launched when needed**

---

# Recovery Point Objective

Continuous replication helps provide:

**Low RPO**

because changes are:

**Regularly replicated**

rather than waiting for:

**Infrequent traditional backups**

### Killer Shortcut

Frequent continuous replication  
→ Lower RPO

Daily backup  
→ Potentially higher RPO

---

# Recovery Time Objective

Elastic Disaster Recovery can provide:

**Lower RTO than traditional Backup and Restore**

because:

**The latest server data is already replicated into AWS**

You still need to:

- Launch recovery instances
- Validate them
- Redirect traffic

### Exam Principle

> **Replication reduces recovery work, but failover still requires launching production recovery resources**

---

# Elastic Disaster Recovery vs Backup and Restore

## [[Backup and Restore]]

Think:

- Backups
- Rebuild
- Restore
- Longer recovery

## Elastic Disaster Recovery

Think:

- Continuous replication
- Low-cost staging area
- Launch recovery servers when needed

### Killer Shortcut

**Restore backups**
→ Backup and Restore

**Continuously replicate whole servers**
→ Elastic Disaster Recovery

---

# Elastic Disaster Recovery vs Pilot Light

These can sound similar.

## [[Pilot Light]]

Architectural DR strategy:

**Critical core components stay running**

## Elastic Disaster Recovery

Service that continuously:

**Replicates server workloads**

into a staging environment.

### Important

Elastic Disaster Recovery can help implement:

**A DR architecture resembling Pilot Light concepts**

because:

- Data is ready
- Full production compute launches later

But:

**The service and the DR strategy are not exactly the same thing**

### Memory Trick

**Pilot Light = Strategy**

**Elastic Disaster Recovery = Service**

---

# Elastic Disaster Recovery vs Warm Standby

## [[Warm Standby]]

Full application environment:

**Already running at reduced capacity**

## Elastic Disaster Recovery

Production recovery instances:

**Usually launched when recovery is needed**

### Killer Shortcut

**Whole stack already running**
→ Warm Standby

**Replica stored, servers launch later**
→ Elastic Disaster Recovery

---

# Elastic Disaster Recovery vs Multi-Site

## [[Multi-Site]]

Multiple production-capable environments:

**Already running**

## Elastic Disaster Recovery

Recovery infrastructure is:

**Activated when needed**

Therefore Multi-Site usually provides:

**Faster failover**

but:

**Higher ongoing cost**

---

# Recovery Drills

A strong DR strategy should include:

**Regular recovery testing**

Elastic Disaster Recovery supports workflows where organizations can test:

**Recovery instances**

without permanently switching:

**Production traffic**

### Killer Exam Principle

> **Test DR before a real disaster occurs**

---

# Testing Recovery

Example:

Source Servers  
↓  
Replication Continues  
↓  
Launch Test Instances  
↓  
Validate Application  
↓  
Terminate Test

Production remains:

**Unaffected**

### Memory Trick

**Test the Lifeboat Before the Ship Sinks**

---

# Point-in-Time Recovery

Elastic Disaster Recovery can maintain recovery points based on:

**Replicated server data**

This can help recover from:

- Infrastructure failure
- Data corruption
- Operational incidents

### Exam Principle

> **Choose a recovery point that predates the problem when necessary**

---

# Failover

During disaster:

1. Select recovery point
2. Launch recovery instances
3. Validate application
4. Update routing/DNS
5. Resume operations

### Memory Trick

**Select → Launch → Validate → Route**

---

# Route 53 Integration

[[Route 53]] can redirect users toward:

**Recovered instances**

after the environment becomes:

**Ready**

Architecture:

Primary Environment  
❌  
↓  
Elastic Disaster Recovery  
↓  
Recovery Environment  
✅  
↓  
Route 53 Redirects Users

---

# Networking

Recovery instances still require:

**Normal AWS networking**

such as:

- [[VPC]]
- Subnets
- [[Security Groups]]
- Route tables
- Load balancers
- DNS

### Exam Trap

> **Elastic Disaster Recovery does not eliminate the need for correct VPC architecture**

---

# Target Network Configuration

Recovery servers may need to launch into:

**Predefined subnets and networking environments**

Planning should include:

- IP connectivity
- Security Groups
- Routes
- DNS
- Internet/private access
- Load balancer integration

---

# Security Groups

Recovered instances need:

**Appropriate Security Groups**

Example:

Application Recovery Instance  
↓  
Security Group  
↓  
Allow Only Required Traffic

### Killer Exam Principle

> **DR environments require the same security discipline as production**

---

# IAM

Elastic Disaster Recovery workflows require appropriate:

**IAM permissions**

to perform operations such as:

- Replication
- Launching infrastructure
- Managing recovery resources

Follow:

**Least privilege**

---

# Cross-Region DR

Elastic Disaster Recovery can support architectures where:

**Source workloads and recovery infrastructure exist in different Regions**

This helps protect against:

**Regional disasters**

### Killer Exam Clue

> **Need server recovery into another AWS Region**
>
> → **Elastic Disaster Recovery**

---

# On-Premises to AWS DR

A classic use case:

On-Premises Servers  
↓  
Continuous Replication  
↓  
AWS Staging Area

If the data center fails:

AWS  
↓  
Launch Recovery Instances  
↓  
Run Production

### Killer Exam Clue

> **Use AWS as the DR site for on-premises servers**
>
> → **Elastic Disaster Recovery**

---

# Cloud-to-AWS DR

The source does not necessarily have to be:

**On-premises**

Elastic Disaster Recovery can also support recovery from:

**Other cloud environments or AWS workloads**

depending on supported configurations.

### Exam Principle

> **Think server-level DR, not only data-center DR**

---

# Cost Efficiency

The service reduces standby cost because:

**Full production recovery servers do not need to run continuously**

Instead:

Replication resources  
→ Running

Full recovery resources  
→ Launched during test/disaster

### Memory Trick

**Pay for Replication Before Disaster**

**Pay for Production Compute During Recovery**

---

# Recovery Scaling

Once recovery instances launch, you may still need to:

**Scale application capacity**

using services such as:

[[Auto Scaling]]

depending on architecture.

---

# Load Balancing

Recovered applications may sit behind:

**Elastic Load Balancing**

Architecture:

Users  
↓  
Load Balancer  
↓  
Recovery Instances

This helps provide:

- Distribution
- Health checks
- Multi-AZ availability

---

# High Availability Inside DR Region

After failover, the recovered environment should not become:

**A new single point of failure**

Use appropriate:

- Multi-AZ design
- Load balancing
- Auto Scaling
- Database resilience

### Killer Exam Principle

> **DR gets you into another environment; HA keeps that recovered environment running**

---

# Failback

After the original environment becomes available again:

Organizations may need to:

**Fail back**

Typical steps include:

1. Synchronize data
2. Prepare original environment
3. Validate
4. Redirect traffic
5. Return to normal operations

### Exam Principle

> **DR planning includes both failover and failback**

---

# Elastic Disaster Recovery vs AWS Backup

## AWS Backup

Think:

**Centralized backup management**

Examples:

- Snapshots
- Recovery points
- Retention
- Backup vaults

## Elastic Disaster Recovery

Think:

**Continuous server replication and rapid recovery**

### Killer Shortcut

**Manage backups**
→ AWS Backup

**Replicate entire servers continuously**
→ Elastic Disaster Recovery

---

# Elastic Disaster Recovery vs Migration Tools

Elastic Disaster Recovery is focused on:

**Business continuity and recovery**

Migration services focus on:

**Moving workloads permanently**

The technologies may look similar because both can involve:

**Replication**

but the goal differs.

### Memory Trick

**Migration = Move**

**DR = Recover**

---

# Architecture Thinking

## Scenario 1 — On-Prem DR

Company runs:

100 VMware servers

and wants AWS to serve as:

**Its disaster recovery environment**

with continuous replication.

Choose:

**Elastic Disaster Recovery**

---

## Scenario 2 — Traditional Snapshots

Company only needs:

Daily EC2 backups

and can tolerate:

Long recovery times.

Think:

**Backup and Restore**

rather than continuous DR replication.

---

## Scenario 3 — Full Secondary Stack

Company already runs:

**Complete application stack in another Region**

at reduced capacity.

Think:

**Warm Standby**

not Elastic Disaster Recovery as the strategy description.

---

## Scenario 4 — Recovery Testing

Company wants to test:

**Recovered servers**

without impacting:

**Production replication**

Think:

**Elastic Disaster Recovery recovery drill/testing**

---

## Scenario 5 — Low Standby Cost

Company needs:

Faster recovery than traditional backups

but cannot afford:

**Full duplicate compute continuously**

Choose:

**Elastic Disaster Recovery**

---

## Scenario 6 — Regional Failure

Primary Region may fail.

Need server replicas available in:

**Another Region**

Choose:

**Cross-Region Elastic Disaster Recovery architecture**

---

## Scenario 7 — DR Environment Launched

Recovery instances are running.

Need users redirected.

Think:

**Route 53**

---

# Scenario Recognition

Immediately think:

**Elastic Disaster Recovery**

when you see:

- Continuous server replication
- Block-level replication
- Low-cost staging area
- On-premises server DR
- Launch recovery instances
- AWS as DR site
- Rapid server recovery
- Replication agent

---

## Think AWS Backup When You See

- Backup schedules
- Retention
- Backup vaults
- Centralized backup policies

---

## Think Backup and Restore When You See

- Snapshots only
- Long RTO
- Rebuild after disaster

---

## Think Warm Standby When You See

- Complete stack already running
- Reduced capacity

---

# Exam Traps

## Trap 1 — Elastic Disaster Recovery Keeps Full Production Servers Running Continuously

❌

The normal value proposition includes:

**Low-cost staging infrastructure**

and launching production recovery instances:

**When needed**

---

## Trap 2 — Elastic Disaster Recovery Is Just AWS Backup

❌

AWS Backup:

**Backup management**

Elastic Disaster Recovery:

**Continuous server replication**

---

## Trap 3 — Elastic Disaster Recovery Removes the Need for Networking

❌

Recovered servers still need:

- VPC
- Subnets
- Security Groups
- Routes
- DNS

---

## Trap 4 — Continuous Replication Automatically Means Zero RPO

❌

Replication can provide:

**Low RPO**

but actual RPO depends on:

**Replication state and recovery architecture**

---

## Trap 5 — Recovery Instances Never Need Testing

❌

Regular:

**Recovery drills**

are important.

---

## Trap 6 — Elastic Disaster Recovery Is the Same as Multi-Site

❌

Multi-Site:

**Production environment already running**

Elastic Disaster Recovery:

**Recovery instances typically launch when needed**

---

# Quick Cheat Sheet

| Exam Clue | Answer |
|---|---|
| Continuous Server Replication | Elastic Disaster Recovery |
| Block-Level Replication | Elastic Disaster Recovery |
| AWS as On-Prem DR Site | Elastic Disaster Recovery |
| Low-Cost Staging | Elastic Disaster Recovery |
| Launch Servers During Recovery | Elastic Disaster Recovery |
| Central Backup Policies | AWS Backup |
| Snapshots + Rebuild | Backup and Restore |
| Full Stack Running Small | Warm Standby |
| Redirect Recovered Users | Route 53 |
| Recovery Environment Networking | VPC |
| DR Testing | Recovery Drill |

---

# DR Service Decision Map

Need:

**Continuous server replication**

→ Elastic Disaster Recovery

Need:

**Centralized backups**

→ AWS Backup

Need:

**Traditional snapshot restore**

→ Backup and Restore

Need:

**Full standby stack running**

→ Warm Standby

Need:

**Full production secondary**

→ Multi-Site

---

# Recovery Flow

> **BEFORE DISASTER**
>
> Source Server
> ↓
> Replication Agent
> ↓
> Continuous Block Replication
> ↓
> Low-Cost AWS Staging Area
>
> ---
>
> **DISASTER**
>
> ↓
>
> Select Recovery Point
> ↓
> Launch Recovery Instances
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

> **SERVER-LEVEL DR**
> → ELASTIC DISASTER RECOVERY
>
> **BLOCK REPLICATION**
> → ELASTIC DISASTER RECOVERY
>
> **LOW-COST STAGING**
> → ELASTIC DISASTER RECOVERY
>
> **ON-PREM → AWS DR**
> → ELASTIC DISASTER RECOVERY
>
> **LAUNCH RECOVERY SERVERS**
> → ELASTIC DISASTER RECOVERY
>
> **CENTRAL BACKUPS**
> → AWS BACKUP
>
> **BACKUPS + REBUILD**
> → BACKUP AND RESTORE
>
> **FULL STACK SMALL**
> → WARM STANDBY
>
> **FULL STACK FULL**
> → MULTI-SITE
>
> **REDIRECT TRAFFIC**
> → ROUTE 53

---

## Master Memory Trick

> [!tip] Elastic Disaster Recovery Master Memory Trick
> Imagine your data center contains:
>
> **100 physical servers**
>
> Building a second full data center would be:
>
> **Expensive**
>
> Instead, AWS keeps:
>
> **A continuously updated copy of each server's disk**
>
> in:
>
> **A low-cost staging area**
>
> The full replacement servers do NOT need to run:
>
> **All day, every day**
>
> Then disaster strikes.
>
> AWS takes the replicated data and:
>
> **LAUNCHES RECOVERY INSTANCES**
>
> Your servers come back inside:
>
> **AWS**

So remember:

> **ELASTIC DISASTER RECOVERY**
> → CONTINUOUS SERVER REPLICATION
>
> **BLOCK LEVEL**
> → DISK CHANGES
>
> **STAGING AREA**
> → LOW-COST BEFORE DISASTER
>
> **RECOVERY INSTANCE**
> → LAUNCH WHEN NEEDED
>
> **AWS BACKUP**
> → BACKUPS
>
> **ROUTE 53**
> → REDIRECT USERS
>
> **VPC**
> → RECOVERY NETWORK

And the killer SAA question:

> **"Does the company need to continuously replicate entire servers into AWS so recovery instances can be launched quickly after a disaster without maintaining full standby compute?"**
>
> YES
>
> → **Elastic Disaster Recovery**

---

## Related Notes

- [[Disaster Recovery Overview]]
- [[Backup and Restore]]
- [[Pilot Light]]
- [[Warm Standby]]
- [[Multi-Site]]
- [[VPC]]
- [[Route 53]]
- [[Auto Scaling]]
## Core Concept

Backup and Restore is the:

**Simplest and lowest-cost Disaster Recovery strategy**

Instead of keeping a complete secondary environment running, you:

1. Back up critical data
2. Store the backups safely
3. Recreate infrastructure after a disaster
4. Restore the data
5. Restart the application

Architecture:

Production Environment  
↓  
Backups / Snapshots  
↓  
Durable Storage

After Disaster:

Backups  
↓  
Restore Data  
↓  
Recreate Infrastructure  
↓  
Launch Application

> [!tip] Memory Trick
> **Backup and Restore = Save Now, Rebuild Later**

---

# When Should You Use It?

Backup and Restore is appropriate when:

- Cost must be minimized
- Longer downtime is acceptable
- Recovery does not need to be immediate
- Infrastructure can be recreated
- Backups satisfy the required RPO

### Killer Exam Clue

> **Company wants the lowest-cost DR solution and can tolerate several hours of downtime**
>
> → **Backup and Restore**

---

# Infrastructure Before Disaster

Before a disaster, the secondary environment may contain:

**Little or no continuously running application infrastructure**

Instead, you maintain:

- Backups
- Snapshots
- Infrastructure templates
- Configuration
- Application artifacts

### Key Principle

> **You are paying primarily to preserve what is needed for recovery, not to run a duplicate application environment**

---

# Recovery Process

After a disaster:

Backups  
↓  
Restore Databases / Storage  
↓  
Provision Networking  
↓  
Provision Compute  
↓  
Deploy Application  
↓  
Restore Configuration  
↓  
Redirect Traffic

Because much of this happens:

**After the disaster**

Backup and Restore generally has:

**The highest RTO of the major DR strategies**

---

# RTO

[[Disaster Recovery Overview|RTO]] measures:

**Acceptable downtime**

Backup and Restore usually has a relatively:

**High RTO**

because infrastructure may need to be:

- Created
- Configured
- Restored
- Tested
- Started

### Memory Trick

> **Nothing Running = More Time Recovering**

---

# RPO

[[Disaster Recovery Overview|RPO]] measures:

**Acceptable data loss**

RPO depends heavily on:

**How frequently backups are created**

Example:

Backup every:

**24 hours**

Potential data loss:

**Up to roughly 24 hours**

Backup every:

**1 hour**

Potential data loss:

**Up to roughly 1 hour**

### Killer Exam Principle

> **Backup frequency strongly affects RPO**

---

# Backup Frequency

More frequent backups generally provide:

**Lower RPO**

Example:

Daily Backup  
→ Higher potential data loss

Hourly Backup  
→ Lower potential data loss

Continuous Replication  
→ Much lower potential data loss

### Memory Trick

> **More Frequent Backup = Less Data at Risk**

---

# S3

[[S3]] is commonly used to store:

- Backup files
- Application artifacts
- Configuration files
- Database exports

S3 provides:

**Highly durable object storage**

making it useful for:

**Disaster Recovery data**

---

# S3 Storage Classes

Backup data can potentially move into:

**Lower-cost storage classes**

depending on:

- Recovery requirements
- Retrieval speed
- Access frequency

Examples include:

- S3 Standard-IA
- S3 Glacier Instant Retrieval
- S3 Glacier Flexible Retrieval
- S3 Glacier Deep Archive

### Exam Principle

> **Storage class must match the required recovery time**

---

# Glacier and RTO

Be careful when choosing:

[[S3 Glacier]]

for disaster recovery.

Some archival storage classes may require:

**Retrieval time**

before the data can be restored.

If the business has a very low:

**RTO**

a slow archival retrieval tier may not satisfy:

**Recovery requirements**

### Killer Exam Trap

> **Cheapest storage is not automatically the correct DR storage**

---

# EBS Snapshots

[[EBS Snapshots]] provide:

**Point-in-time backups of EBS volumes**

Architecture:

EBS Volume  
↓  
Snapshot  
↓  
Restore New EBS Volume

After disaster:

Snapshot  
↓  
New EBS Volume  
↓  
EC2

### Killer Exam Clue

> **Need to restore an EC2 data volume after failure**
>
> → **EBS Snapshot**

---

# EBS Snapshot Cross-Region Copy

Snapshots can be copied to:

**Another AWS Region**

This can protect against:

**Regional failure**

Architecture:

Region A  
EBS Snapshot  
↓  
Copy  
↓  
Region B

### Killer Exam Clue

> **Need EBS backup available if the primary Region fails**
>
> → **Cross-Region Snapshot Copy**

---

# AMIs

An:

**AMI**

can preserve information needed to launch:

**EC2 instances**

A DR strategy may maintain:

- AMIs
- EBS snapshots
- Launch configurations/templates
- Application deployment artifacts

This allows EC2 infrastructure to be:

**Recreated after disaster**

---

# RDS Backups

[[RDS]] supports:

- Automated backups
- Manual snapshots

These can be used to:

**Restore databases**

after data loss or infrastructure failure.

### Killer Exam Clue

> **Need point-in-time recovery for an RDS database**
>
> → **RDS Automated Backups**

---

# RDS Snapshots

Manual RDS snapshots remain available until:

**You explicitly delete them**

They can be useful for:

**Longer-term recovery points**

---

# RDS Cross-Region Snapshots

Database snapshots can be copied to:

**Another Region**

to support:

**Cross-Region DR**

### Exam Principle

> **If Region failure is in scope, ensure recovery data exists outside the primary Region**

---

# DynamoDB Backups

[[DynamoDB]] supports:

**Point-in-Time Recovery — PITR**

and:

**On-Demand Backups**

PITR provides continuous backups that allow restoration to:

**A point within the supported recovery window**

### Killer Exam Clue

> **Need to recover DynamoDB from accidental writes or deletion**
>
> → **Point-in-Time Recovery**

---

# S3 Versioning

[[S3 Versioning]] protects against:

- Accidental deletion
- Accidental overwrite

Instead of permanently replacing an object:

**Previous versions remain available**

### Killer Exam Clue

> **Need to recover an accidentally overwritten S3 object**
>
> → **S3 Versioning**

---

# S3 Cross-Region Replication

For regional resilience:

S3 objects can be replicated to:

**Another Region**

using:

**Cross-Region Replication**

Architecture:

S3 — Region A  
↓  
Replication  
↓  
S3 — Region B

### Important Distinction

Replication and backup are related but:

**Not identical**

Replication can quickly copy changes—including potentially unwanted changes depending on configuration—whereas backup strategies preserve:

**Recovery points**

### Memory Trick

> **Replication = Copy Changes**
>
> **Backup = Preserve Recovery Point**

---

# AWS Backup

AWS Backup provides:

**Centralized backup management**

across supported AWS services.

It can help manage:

- Backup schedules
- Retention
- Backup policies
- Backup vaults
- Cross-Region copies
- Cross-account backup strategies

### Killer Exam Clue

> **Need centralized backup management across multiple AWS services**
>
> → **AWS Backup**

---

# Backup Plans

AWS Backup uses:

**Backup Plans**

to define:

- Backup frequency
- Backup windows
- Lifecycle
- Retention

### Memory Trick

**Backup Plan = When + How Long**

---

# Backup Vault

A:

**Backup Vault**

stores and organizes:

**Recovery points**

Vaults can also help apply:

**Access controls**

to backup data.

---

# Backup Vault Lock

AWS Backup Vault Lock can help protect backups from:

**Deletion or modification**

using:

**Write Once, Read Many — WORM-style controls**

This can be important for:

- Compliance
- Ransomware protection
- Backup immutability

### Killer Exam Clue

> **Backups must be protected from deletion or tampering**
>
> → **AWS Backup Vault Lock**

---

# Cross-Account Backup

A stronger DR strategy may store backups in:

**Another AWS account**

This reduces the risk that:

**A compromise of the production account also compromises the backups**

### Killer Exam Principle

> **Separate backup account = stronger isolation**

---

# Cross-Region Backup

Backups can also be stored in:

**Another Region**

This protects against:

**Regional disasters**

### Memory Trick

> **Cross-Account = Account Isolation**
>
> **Cross-Region = Region Isolation**

---

# Infrastructure as Code

Backup and Restore is much more effective when infrastructure can be rebuilt using:

**Infrastructure as Code**

Examples:

- CloudFormation
- Terraform

Instead of manually rebuilding:

- VPC
- Subnets
- Security Groups
- EC2
- Load Balancers

you can:

**Redeploy the architecture from templates**

### Killer Exam Clue

> **Need repeatable and faster infrastructure reconstruction**
>
> → **Infrastructure as Code**

---

# Infrastructure Configuration Is Part of DR

Backing up data alone may not be enough.

You may also need to preserve:

- IaC templates
- Application code
- Configuration
- AMIs
- Deployment scripts
- Security configuration
- DNS configuration

### Exam Principle

> **Recover the entire workload, not merely its data**

---

# Route 53 During Recovery

[[Route 53]] can redirect users toward:

**The recovered environment**

Example:

Primary Region  
❌  
↓  
Restore Secondary Region  
↓  
Route 53  
↓  
Recovered Application

Because Backup and Restore may require substantial recovery time:

Traffic is usually redirected:

**After the secondary environment becomes operational**

---

# Restore Testing

Backups should be:

**Regularly tested**

A successful backup job does not prove that:

**The workload can actually be restored**

Testing can verify:

- Backup integrity
- Recovery procedures
- Permissions
- Infrastructure templates
- Application dependencies

### Memory Trick

> **Backup Successful ≠ Recovery Successful**

---

# Recovery Automation

Automation can reduce:

**RTO**

even when using Backup and Restore.

Possible automation:

Disaster Declared  
↓  
Deploy CloudFormation / Terraform  
↓  
Restore Snapshots  
↓  
Deploy Application  
↓  
Validate  
↓  
Update DNS

### Killer Exam Principle

> **Automation can improve RTO without keeping an entire standby environment running**

---

# Backup and Restore vs Pilot Light

## Backup and Restore

Before disaster:

**Backups primarily exist**

After disaster:

**Infrastructure is rebuilt**

## Pilot Light

Before disaster:

**Critical core infrastructure is already running**

### Killer Shortcut

> **Rebuild Everything**
> → Backup and Restore
>
> **Core Already Running**
> → Pilot Light

---

# Backup and Restore vs Warm Standby

## Backup and Restore

Secondary application environment:

**Not continuously operational**

## Warm Standby

Secondary environment:

**Fully functional at reduced capacity**

### Killer Shortcut

> **Nothing/Minimal Running**
> → Backup and Restore
>
> **Whole Stack Running Small**
> → Warm Standby

---

# Backup and Restore vs Multi-Site

## Backup and Restore

Think:

**Lowest cost + slowest recovery**

## Multi-Site

Think:

**Highest cost + fastest recovery**

These sit at:

**Opposite ends of the DR spectrum**

---

# Architecture Thinking

## Scenario 1 — Lowest Cost

Company can tolerate:

**24 hours of downtime**

and wants:

**Minimum DR cost**

Choose:

**Backup and Restore**

---

## Scenario 2 — Restore EC2 Storage

Critical EC2 data must be recoverable.

Use:

**EBS Snapshots**

---

## Scenario 3 — Region Failure

EBS snapshots must survive:

**Complete Region failure**

Use:

**Cross-Region Snapshot Copies**

---

## Scenario 4 — RDS Recovery

Database must support:

**Point-in-time restoration**

Use:

**RDS Automated Backups**

---

## Scenario 5 — Accidental S3 Overwrite

User overwrites:

**Critical S3 object**

Use:

**S3 Versioning**

to recover:

**Previous version**

---

## Scenario 6 — Central Backup Management

Company has:

Many AWS services and accounts.

Need:

**Centralized backup policies**

Choose:

**AWS Backup**

---

## Scenario 7 — Ransomware Protection

Backups must not be:

**Deleted or modified**

Think:

**Backup Vault Lock**

---

## Scenario 8 — Regional Disaster

Company's backups exist only in:

**Primary Region**

Requirement:

Survive Region failure.

Improve architecture with:

**Cross-Region Backup Copies**

---

## Scenario 9 — Account Compromise

Administrators in production account should not be able to destroy:

**Every backup**

Think:

**Cross-Account Backup**

---

## Scenario 10 — Faster Rebuild

Company uses Backup and Restore but wants to reduce:

**Manual recovery time**

Use:

**Infrastructure as Code + Automation**

---

# Scenario Recognition

Immediately think:

**Backup and Restore**

when you see:

- Lowest-cost DR
- Long RTO acceptable
- Restore after disaster
- Snapshots
- Rebuild infrastructure
- Minimal standby infrastructure

---

## Think AWS Backup When You See

- Centralized backups
- Multiple AWS services
- Backup policies
- Backup vaults
- Cross-account backups

---

## Think Vault Lock When You See

- Immutable backups
- WORM
- Ransomware
- Prevent backup deletion
- Compliance retention

---

## Think Cross-Region When You See

- Region failure
- Geographic DR
- Secondary Region

---

# Exam Traps

## Trap 1 — Backup and Restore Has the Lowest RTO

❌

It generally has:

**The highest RTO**

among the four major DR strategies.

---

## Trap 2 — Backup Frequency Primarily Determines RTO

❌

Backup frequency primarily affects:

**RPO**

---

## Trap 3 — Cheapest Archive Tier Is Always Best

❌

Retrieval time must satisfy:

**RTO**

---

## Trap 4 — Backup in the Same Region Always Protects Against Regional Failure

❌

For Region-level DR:

Consider:

**Cross-Region copies**

---

## Trap 5 — Replication and Backup Are Identical

❌

Replication:

**Copies changes**

Backup:

**Preserves recovery points**

---

## Trap 6 — Data Backup Alone Is a Complete DR Strategy

❌

You must also recover:

- Infrastructure
- Applications
- Configuration
- Networking
- Security

---

## Trap 7 — Successful Backup Means Recovery Is Guaranteed

❌

Backups should be:

**Tested for restoration**

---

# Quick Cheat Sheet

| Exam Clue | Answer |
|---|---|
| Lowest-Cost DR | Backup and Restore |
| Recovery Speed | Slowest Major DR Strategy |
| Backup Frequency | Affects RPO |
| Restore Speed | Affects RTO |
| EC2 Volume Backup | EBS Snapshot |
| RDS Point-in-Time Recovery | Automated Backup |
| DynamoDB Recovery | PITR |
| S3 Accidental Overwrite | Versioning |
| Centralized Backup Management | AWS Backup |
| Immutable Backup | Backup Vault Lock |
| Region Failure Protection | Cross-Region Backup |
| Account Isolation | Cross-Account Backup |
| Faster Infrastructure Rebuild | IaC + Automation |

---

# Recovery Decision Map

Need:

**Lowest-cost DR**

→ Backup and Restore

Need:

**EC2 storage recovery**

→ EBS Snapshot

Need:

**Database recovery point**

→ Database backup / snapshot

Need:

**Central backup policies**

→ AWS Backup

Need:

**Immutable backups**

→ Backup Vault Lock

Need:

**Regional protection**

→ Cross-Region Copies

Need:

**Account isolation**

→ Cross-Account Backup

Need:

**Faster rebuild**

→ Infrastructure as Code

---

# Final Exam Rapid-Fire

> **LOWEST COST DR**
> → BACKUP AND RESTORE
>
> **HIGHEST RTO**
> → BACKUP AND RESTORE
>
> **BACKUP FREQUENCY**
> → RPO
>
> **RESTORE TIME**
> → RTO
>
> **EBS**
> → SNAPSHOT
>
> **RDS POINT-IN-TIME**
> → AUTOMATED BACKUP
>
> **DYNAMODB**
> → PITR
>
> **S3 OVERWRITE**
> → VERSIONING
>
> **CENTRAL BACKUPS**
> → AWS BACKUP
>
> **IMMUTABLE BACKUPS**
> → VAULT LOCK
>
> **REGION FAILURE**
> → CROSS-REGION COPY
>
> **ACCOUNT ISOLATION**
> → CROSS-ACCOUNT BACKUP
>
> **FAST REBUILD**
> → INFRASTRUCTURE AS CODE

---

## Master Memory Trick

> [!tip] Backup and Restore Master Memory Trick
> Imagine your restaurant is destroyed.
>
> You do NOT have:
>
> **A second restaurant waiting**
>
> But you safely stored:
>
> **The recipes**
>
> **The equipment list**
>
> **The floor plan**
>
> **The customer records**
>
> After the disaster, you:
>
> **BUILD A NEW RESTAURANT**
>
> then restore everything from:
>
> **YOUR BACKUPS**
>
> This is inexpensive before the disaster because:
>
> **Very little standby infrastructure is running**
>
> But recovery takes longer because:
>
> **You must rebuild**

So remember:

> **BACKUP AND RESTORE**
> → SAVE NOW, REBUILD LATER
>
> **LOWEST COST**
> → BACKUP AND RESTORE
>
> **LONGEST RECOVERY**
> → BACKUP AND RESTORE
>
> **BACKUP FREQUENCY**
> → RPO
>
> **RESTORE SPEED**
> → RTO
>
> **CROSS-REGION**
> → REGION PROTECTION
>
> **CROSS-ACCOUNT**
> → ACCOUNT ISOLATION
>
> **VAULT LOCK**
> → IMMUTABILITY
>
> **IaC**
> → FASTER REBUILD

And the killer SAA question:

> **"Can the business tolerate a relatively long recovery time and wants to minimize the cost of maintaining a disaster recovery environment?"**
>
> YES
>
> → **Backup and Restore**

---

## Related Notes

- [[Disaster Recovery Overview]]
- [[S3]]
- [[S3 Glacier]]
- [[EBS Snapshots]]
- [[RDS]]
- [[DynamoDB]]
- [[Route 53]]
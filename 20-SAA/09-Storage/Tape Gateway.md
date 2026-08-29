## What Problem Does It Solve?

[[Tape Gateway]] allows organizations to replace:

**Physical backup tapes**

with:

**Virtual tapes stored in AWS**

without requiring them to completely redesign their existing tape-based backup workflows.

It solves the problem of:

> **"How can we stop buying, managing, transporting, and storing physical backup tapes while continuing to use our existing tape-based backup software?"**

Architecture:

Existing Backup Software  
↓  
iSCSI  
↓  
Tape Gateway  
↓  
Virtual Tapes  
↓  
AWS

> [!tip] Memory Trick
> **Tape Gateway = Physical tapes without the physical tapes**

---

## What Is Tape Gateway?

Tape Gateway is part of:

[[Storage Gateway]]

It provides a:

**Cloud-backed Virtual Tape Library**

or:

**VTL**

Existing backup applications interact with the gateway as though they were using:

**Traditional physical tape infrastructure**

But the tapes are actually:

**Virtual tapes backed by AWS storage**

---

# Virtual Tape Library

VTL means:

**Virtual Tape Library**

Architecture:

Backup Application  
↓  
Virtual Tape Drive  
↓  
Virtual Tape Library  
↓  
AWS

The backup software does not need to know that the underlying tapes are:

**Virtual**

### Memory Trick

**VTL = Tape library without the tape room**

---

# Why Tape Gateway Exists

Traditional tape environments require organizations to manage:

- Physical tapes
- Tape drives
- Tape libraries
- Tape rotation
- Off-site storage
- Tape transportation
- Tape replacement

Tape Gateway replaces much of that physical infrastructure with:

**AWS cloud storage**

---

# Existing Backup Applications

One of the biggest benefits is compatibility with:

**Existing backup applications**

The organization does not necessarily need to redesign its entire backup process.

Conceptually:

Existing Backup Software  
↓  
Still Thinks It Uses Tapes  
↓  
Tape Gateway  
↓  
AWS

> [!tip] Exam Pattern
> **Existing tape backup software + eliminate physical tapes**
>
> → **Tape Gateway**

---

# iSCSI

Tape Gateway uses:

**iSCSI**

to expose its virtual tape infrastructure to:

**Backup applications**

Architecture:

Backup Server  
↓  
iSCSI  
↓  
Tape Gateway

This is similar to Volume Gateway in that both use:

**iSCSI**

but they expose different storage concepts.

---

# Volume Gateway vs Tape Gateway

Both can use:

**iSCSI**

Do not choose based on iSCSI alone.

## [[Volume Gateway]]

Exposes:

**Block Storage Volumes**

Think:

Virtual Disks

---

## Tape Gateway

Exposes:

**Virtual Tape Infrastructure**

Think:

Backup Tapes

### Memory Trick

**iSCSI + DISK**
→ Volume Gateway

**iSCSI + TAPE**
→ Tape Gateway

---

# Virtual Tapes

Backup applications write data to:

**Virtual Tapes**

just as they would write to physical tapes.

Architecture:

Backup Job  
↓  
Virtual Tape  
↓  
Tape Gateway  
↓  
AWS

This allows organizations to preserve:

**Traditional tape backup workflows**

while using:

**Cloud storage**

---

# Active Virtual Tapes

Virtual tapes that are actively being used by backup applications are available through:

**The Virtual Tape Library**

Think:

Backup Software  
↕  
VTL  
↕  
Active Virtual Tapes

These tapes behave like:

**Normal tapes inserted into a tape library**

---

# Archive Virtual Tapes

When a tape no longer needs to remain actively available:

It can be:

**Archived**

This allows organizations to use AWS for:

**Long-term backup retention**

Architecture:

Active Virtual Tape  
↓  
Archive  
↓  
Long-Term AWS Storage

---

# Tape Gateway Storage Architecture

Conceptually:

On-Premises Backup Software  
↓  
Tape Gateway  
↓  
Virtual Tape Library  
↓  
AWS Storage  
↓  
Archive

This provides:

**Cloud-backed tape lifecycle management**

---

# Physical Tape Replacement

This is the strongest Tape Gateway use case.

Old Architecture:

Backup Server  
↓  
Physical Tape Drive  
↓  
Physical Tape  
↓  
Employee Removes Tape  
↓  
Transport to Off-Site Facility

Tape Gateway:

Backup Server  
↓  
Tape Gateway  
↓  
Virtual Tape  
↓  
AWS

### Memory Trick

**Stop shipping tapes. Start shipping bits.**

---

# Off-Site Backup

Traditional tape strategies often move physical tapes to:

**Off-site storage facilities**

for disaster recovery.

Tape Gateway allows AWS to serve as the:

**Off-site cloud backup location**

This removes the operational burden of:

- Transporting tapes
- Tracking tapes
- Maintaining physical archives

---

# Long-Term Retention

Tape Gateway is useful for:

**Long-term backup retention**

especially when organizations already have:

**Tape-oriented backup policies**

Think:

Daily / Weekly Backup  
↓  
Virtual Tape  
↓  
Archive  
↓  
Long-Term Retention

---

# Tape Gateway vs S3 File Gateway

## [[S3 File Gateway]]

Provides:

**File access**

Protocols:

- NFS
- SMB

Backend:

S3 Objects

---

## Tape Gateway

Provides:

**Virtual tape access**

Used by:

Backup software

### Exam Decision

Application needs files  
→ S3 File Gateway

Backup application expects tapes  
→ Tape Gateway

---

# Tape Gateway vs Volume Gateway

## [[Volume Gateway]]

Best for:

**Hybrid block storage**

Use when applications need:

**Volumes**

---

## Tape Gateway

Best for:

**Backup and archival**

Use when backup applications need:

**Tapes**

### Memory Trick

**Volume = Working Disk**

**Tape = Backup Archive**

---

# Tape Gateway vs S3

A company could build a new backup system that directly writes to:

[[S3]]

But legacy backup software may expect:

**Tape infrastructure**

Tape Gateway provides the:

**Compatibility layer**

Architecture:

Legacy Backup Software  
↓  
Tape Interface  
↓  
Tape Gateway  
↓  
AWS Storage

### Exam Pattern

If the backup software already supports S3 directly:

Tape Gateway may not be necessary.

If it expects:

**Tape drives / tape libraries**

think:

Tape Gateway.

---

# Tape Gateway vs Snowball

## [[Snowball]]

Best for:

**Large-scale offline data migration**

Physical device is shipped.

---

## Tape Gateway

Best for:

**Ongoing backup workflows**

over a network connection.

### Memory Trick

**Snowball = Move huge datasets**

**Tape Gateway = Keep doing backups**

---

# Tape Gateway vs DataSync

## [[DataSync]]

Best for:

**Automated data movement**

between storage systems and AWS.

---

## Tape Gateway

Best for:

**Tape-compatible backup**

### Exam Decision

Move NFS data to AWS  
→ DataSync

Existing backup software requires tapes  
→ Tape Gateway

---

# Tape Gateway vs Glacier

This distinction matters.

Glacier storage classes provide:

**Low-cost archival storage**

Tape Gateway provides:

**A tape-compatible interface and workflow**

Think:

Tape Gateway  
= How legacy backup software interacts with cloud tape

Glacier  
= Archival storage tier

### Memory Trick

**Tape Gateway = Tape Interface**

**Glacier = Archive Storage**

---

# Architecture Thinking

## Scenario 1 — Replace Physical Tapes

A company currently backs up data to physical tapes.

It wants to eliminate:

- Tape libraries
- Tape transportation
- Off-site tape storage

but keep its existing backup application.

**Choose → Tape Gateway**

---

## Scenario 2 — Existing Backup Software

A company's backup software is designed to write to:

**Tape drives**

The company wants to move backups to AWS with minimal application changes.

**Choose → Tape Gateway**

---

## Scenario 3 — Long-Term Tape Archive

An organization must retain backups for:

**Several years**

Its existing workflow is tape-based.

**Choose → Tape Gateway**

with archived virtual tapes.

---

## Scenario 4 — Application Needs Block Storage

An application needs:

**iSCSI volumes**

for active application data.

Do NOT choose Tape Gateway simply because it uses iSCSI.

Choose:

[[Volume Gateway]]

---

## Scenario 5 — Linux Application Needs NFS

A Linux application needs file access to data stored in S3.

Do NOT choose Tape Gateway.

Choose:

[[S3 File Gateway]]

---

## Scenario 6 — Massive One-Time Migration

A company needs to migrate:

500 TB

to AWS with limited network bandwidth.

Tape Gateway is not the primary migration solution.

Think:

[[Snowball]]

---

# Scenario Recognition

Immediately think:

[[Tape Gateway]]

when you see:

- Physical tapes
- Virtual tapes
- Virtual Tape Library
- VTL
- Tape backup
- Existing backup software
- Replace tape infrastructure
- Off-site tape storage
- Long-term backup retention
- Legacy backup system

### Strongest Exam Pattern

> **"Replace physical tape backups with AWS while keeping the existing backup application."**
>
> → **Tape Gateway**

---

# Exam Traps

## Trap 1 — Tape Gateway Requires Physical Tapes

False.

It provides:

**Virtual tapes**

---

## Trap 2 — Tape Gateway Is General-Purpose File Storage

False.

For file storage interfaces:

Think:

[[S3 File Gateway]]

or:

[[FSx File Gateway]]

---

## Trap 3 — iSCSI Automatically Means Volume Gateway

False.

Both:

- Volume Gateway
- Tape Gateway

use iSCSI.

Look at what the application expects.

**Disk / Volume**
→ Volume Gateway

**Tape**
→ Tape Gateway

---

## Trap 4 — Tape Gateway Is Mainly for HPC

False.

HPC:

→ [[FSx for Lustre]]

Tape Gateway:

→ Backup / Archive

---

## Trap 5 — Tape Gateway and Glacier Are the Same Service

False.

Tape Gateway:

**Tape-compatible backup interface**

Glacier:

**Archive storage class**

---

## Trap 6 — Tape Gateway Is for One-Time Petabyte Migration

False.

Think:

[[Snowball]]

for massive offline migration.

---

## Trap 7 — Existing Backup Software Must Be Rewritten for S3 APIs

Not necessarily.

That is exactly the type of problem Tape Gateway helps avoid.

---

# Storage Gateway Family Comparison

| Gateway | Interface | Primary Purpose |
|---|---|---|
| [[S3 File Gateway]] | NFS / SMB | Files → S3 |
| [[FSx File Gateway]] | SMB | On-Prem → FSx Windows |
| [[Volume Gateway]] | iSCSI | Hybrid Block Storage |
| [[Tape Gateway]] | iSCSI / VTL | Virtual Tape Backup |

---

# Quick Cheat Sheet

| Requirement | Answer |
|---|---|
| Replace Physical Tapes | Tape Gateway |
| Virtual Tape Library | Tape Gateway |
| VTL | Tape Gateway |
| Existing Tape Backup Software | Tape Gateway |
| Virtual Tapes | Tape Gateway |
| Long-Term Backup Retention | Tape Gateway |
| Tape Workflow | Tape Gateway |
| Hybrid Block Storage | Volume Gateway |
| NFS / SMB → S3 | S3 File Gateway |
| SMB → FSx Windows | FSx File Gateway |
| Massive Offline Migration | Snowball |

---

## Master Memory Trick

> [!tip] Master Memory Trick
> Imagine an old-school company basement filled with backup tapes.
>
> Every night:
>
> **Backup software**
> → Writes to tape
>
> **Employee**
> → Removes tape
>
> **Truck**
> → Takes tape off-site
>
> Tape Gateway replaces that whole mess with:
>
> **Backup Software**
> ↓
> **Virtual Tape**
> ↓
> **AWS**

So memorize:

> **PHYSICAL TAPE**
>
> → Replace it
>
> **VIRTUAL TAPE**
>
> → Tape Gateway
>
> **VTL**
>
> → Tape Gateway
>
> **LEGACY BACKUP SOFTWARE**
>
> → Tape Gateway

And for the whole Storage Gateway family:

> **FILES → File Gateway**
>
> **BLOCKS → Volume Gateway**
>
> **TAPES → Tape Gateway**

---

## Related Notes

- [[Storage Gateway]]
- [[S3 File Gateway]]
- [[FSx File Gateway]]
- [[Volume Gateway]]
- [[S3]]
- [[S3 Glacier Flexible Retrieval]]
- [[S3 Glacier Deep Archive]]
- [[DataSync]]
- [[Snowball]]
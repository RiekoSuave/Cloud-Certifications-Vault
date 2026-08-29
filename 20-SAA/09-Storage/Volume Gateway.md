## What Problem Does It Solve?

[[Volume Gateway]] provides on-premises applications with:

**Block storage**

backed by AWS cloud storage.

It solves the problem of:

> **"How can my on-premises servers continue using block storage while AWS provides cloud-backed storage and snapshots?"**

Architecture:

On-Premises Application  
↓  
iSCSI  
↓  
Volume Gateway  
↓  
AWS

> [!tip] Memory Trick
> **Volume Gateway = Hybrid Block Storage**

---

## What Is Volume Gateway?

Volume Gateway is part of:

[[Storage Gateway]]

It presents storage to on-premises applications using:

**iSCSI**

Applications see:

**Block storage volumes**

rather than:

- Files
- S3 objects
- Virtual tapes

### Master Distinction

**File Gateway**
→ Files

**Volume Gateway**
→ Blocks

**Tape Gateway**
→ Tapes

---

# iSCSI

Volume Gateway uses:

**iSCSI**

to expose block-storage volumes to:

**On-Premises Servers**

Architecture:

Server  
↓  
iSCSI  
↓  
Volume Gateway  
↓  
AWS Storage

> [!tip] Memory Trick
> **iSCSI = Block Storage clue**

If the exam says:

**iSCSI**

your brain should immediately consider:

[[Volume Gateway]]

---

# Volume Gateway Modes

There are two important Volume Gateway modes:

1. **Cached Volumes**
2. **Stored Volumes**

The biggest difference is:

> **Where is the primary copy of the data?**

---

# Cached Volumes

With:

**Cached Volumes**

the primary data is stored in:

**AWS**

while frequently accessed data is cached:

**On-Premises**

Architecture:

On-Premises Application  
↓  
iSCSI  
↓  
Volume Gateway  
├── Frequently Accessed Data → Local Cache
└── Primary Data → AWS

> [!tip] Memory Trick
> **Cached = CLOUD holds the main copy**

---

## Why Cached Volumes?

Cached Volumes allow you to:

**Minimize on-premises storage requirements**

because the full dataset does not need to remain locally stored.

Instead:

AWS  
→ Primary Dataset

On-Premises  
→ Frequently Accessed Blocks

This combines:

**Cloud-scale storage**

with:

**Low-latency access to frequently used data**

---

# Cached Volume Architecture

Imagine an organization has:

100 TB Dataset

but only:

5 TB

is frequently accessed.

Instead of keeping all 100 TB locally:

AWS  
↓  
Stores Full Dataset

On-Premises Cache  
↓  
Stores Frequently Used Blocks

Application  
↓  
Accesses through iSCSI

This reduces:

**Local storage capacity requirements**

---

# Cached Volume Exam Pattern

> **"A company wants to minimize its on-premises storage infrastructure while maintaining low-latency access to frequently used blocks."**
>
> → **Cached Volume Gateway**

### Strong Clues

- Primary data in AWS
- Local cache
- Minimize local storage
- Frequently accessed blocks
- iSCSI

---

# Stored Volumes

With:

**Stored Volumes**

the primary data is stored:

**On-Premises**

AWS maintains:

**Cloud backups**

Architecture:

Application  
↓  
iSCSI  
↓  
Volume Gateway  
↓  
Full Dataset Stored Locally  
↓  
Asynchronous Backup to AWS

> [!tip] Memory Trick
> **Stored = SITE holds the main copy**

---

# Why Stored Volumes?

Stored Volumes are designed for workloads requiring:

**Low-latency access to the entire dataset**

because the full dataset remains:

**On-Premises**

AWS provides:

**Off-site backup**

---

# Stored Volume Architecture

Imagine an application requires:

100 TB Dataset

and all 100 TB must be available locally with:

**Low latency**

Architecture:

Application  
↓  
Local 100 TB Dataset  
↓  
Volume Gateway  
↓  
AWS Backup

The local environment remains the:

**Primary storage location**

---

# Stored Volume Exam Pattern

> **"The entire dataset must remain on-premises for low-latency access, but the company wants asynchronous cloud backups."**
>
> → **Stored Volume Gateway**

### Strong Clues

- Primary data on-premises
- Entire dataset local
- Low latency
- Cloud backup
- iSCSI

---

# Cached vs Stored Volumes

This is the most important Volume Gateway exam comparison.

| Feature | Cached Volumes | Stored Volumes |
|---|---|---|
| Primary Data | AWS | On-Premises |
| Frequently Used Data Local | ✅ | Entire Dataset Local |
| Full Dataset Local | ❌ | ✅ |
| Minimize Local Storage | ✅ | ❌ |
| Low-Latency Hot Data | ✅ | ✅ |
| Low-Latency Entire Dataset | ❌ | ✅ |
| Cloud Backup | ✅ | ✅ |
| Protocol | iSCSI | iSCSI |

---

## Master Memory Trick

> **CACHED**
>
> → Main copy in **CLOUD**
>
> **STORED**
>
> → Main copy at your **SITE**

Both begin with the same letter pair:

**C → C**
→ Cached = Cloud

**S → S**
→ Stored = Site

---

# EBS Snapshots

Volume Gateway can create:

[[EBS Snapshots]]

from its volumes.

Architecture:

Volume Gateway  
↓  
Snapshot  
↓  
AWS

These snapshots provide:

**Point-in-time backups**

of the block-storage volumes.

---

# Why EBS Snapshots Matter

Snapshots can be useful for:

- Backup
- Disaster recovery
- Migration
- Restoring volumes

Example:

On-Premises Volume  
↓  
Volume Gateway  
↓  
EBS Snapshot  
↓  
AWS Recovery

---

# Incremental Snapshots

Like normal:

[[EBS Snapshots]]

subsequent snapshots are:

**Incremental**

Only changed blocks need to be stored after the initial snapshot.

This helps reduce:

- Storage usage
- Backup transfer
- Backup cost

---

# Restore into EBS

Because Volume Gateway backups can exist as:

EBS Snapshots

they can be useful when migrating or recovering workloads into:

[[EC2]]

Conceptually:

On-Premises Volume  
↓  
Volume Gateway  
↓  
EBS Snapshot  
↓  
EBS Volume  
↓  
EC2

This creates a useful bridge between:

**On-Premises Block Storage**

and:

**AWS Compute**

---

# Volume Gateway vs S3 File Gateway

## [[S3 File Gateway]]

Storage interface:

**File**

Protocols:

- NFS
- SMB

Backend:

S3

---

## Volume Gateway

Storage interface:

**Block**

Protocol:

**iSCSI**

### Memory Trick

**NFS / SMB**
→ File Gateway

**iSCSI**
→ Volume Gateway

---

# Volume Gateway vs FSx File Gateway

## [[FSx File Gateway]]

Provides:

**Windows file access**

Protocol:

SMB

Backend:

FSx Windows

---

## Volume Gateway

Provides:

**Block storage**

Protocol:

iSCSI

### Exam Decision

Windows file share  
→ FSx File Gateway

Application disk / block volume  
→ Volume Gateway

---

# Volume Gateway vs Tape Gateway

## Volume Gateway

Think:

**Virtual disks**

Protocol:

iSCSI

---

## [[Tape Gateway]]

Think:

**Virtual tapes**

Used by:

Backup software

### Memory Trick

**Volume = Disk**

**Tape = Backup Tape**

---

# Volume Gateway vs EBS

## [[EBS]]

Provides block storage for:

**EC2**

---

## Volume Gateway

Provides hybrid block storage for:

**On-Premises applications**

using:

iSCSI

### Exam Decision

EC2 needs a disk  
→ EBS

On-premises server needs AWS-backed block storage  
→ Volume Gateway

---

# Volume Gateway vs DataSync

## Volume Gateway

Provides:

**Ongoing hybrid block storage**

Applications actively use the volume.

---

## [[DataSync]]

Provides:

**Data transfer**

It is primarily about:

**Moving datasets**

### Memory Trick

**Gateway = USE**

**DataSync = MOVE**

---

# Volume Gateway vs Snowball

## [[Snowball]]

Provides:

**Offline physical migration**

---

## Volume Gateway

Provides:

**Ongoing network-based hybrid block storage**

### Exam Decision

Massive one-time migration  
→ Snowball

Ongoing iSCSI block access  
→ Volume Gateway

---

# Architecture Thinking

## Scenario 1 — Minimize On-Prem Storage

A company has a large dataset.

It wants:

- Primary storage in AWS
- Only frequently accessed blocks locally
- Reduced on-premises storage requirements

**Choose → Cached Volume Gateway**

---

## Scenario 2 — Entire Dataset Must Remain Local

An application requires:

**Low-latency access to every block**

The company also wants cloud backups.

**Choose → Stored Volume Gateway**

---

## Scenario 3 — iSCSI Requirement

A legacy on-premises application requires:

**iSCSI block storage**

and AWS-backed storage.

**Choose → Volume Gateway**

---

## Scenario 4 — Point-in-Time Block Backup

A company needs snapshots of its hybrid block-storage volumes.

**Choose:**

Volume Gateway  
↓  
[[EBS Snapshots]]

---

## Scenario 5 — NFS Application

An application requires:

**NFS**

and files must be stored in S3.

Do NOT choose Volume Gateway.

Choose:

[[S3 File Gateway]]

---

## Scenario 6 — Physical Tape Replacement

A company's existing backup application expects:

**Tape drives**

Do NOT choose Volume Gateway.

Choose:

[[Tape Gateway]]

---

# Scenario Recognition

Immediately think:

[[Volume Gateway]]

when you see:

- Block storage
- iSCSI
- Hybrid block storage
- Cached volume
- Stored volume
- EBS snapshot
- On-premises application disks
- Cloud-backed volumes

---

## Immediately Think Cached When You See

- Primary data in AWS
- Minimize local storage
- Local cache
- Frequently accessed blocks

---

## Immediately Think Stored When You See

- Primary data on-premises
- Entire dataset local
- Lowest latency for full dataset
- AWS backup

---

# Exam Traps

## Trap 1 — Volume Gateway Provides NFS

False.

Think:

**iSCSI**

---

## Trap 2 — Volume Gateway Is File Storage

False.

It provides:

**Block storage**

---

## Trap 3 — Cached Volumes Keep the Primary Dataset On-Premises

False.

Cached:

**Primary data in AWS**

---

## Trap 4 — Stored Volumes Keep the Primary Dataset in AWS

False.

Stored:

**Primary data on-premises**

---

## Trap 5 — Cached Means Nothing Is Stored Locally

False.

Frequently accessed blocks are:

**Cached locally**

---

## Trap 6 — Stored Volumes Do Not Use AWS

False.

AWS provides:

**Cloud backup**

for the locally stored dataset.

---

## Trap 7 — Volume Gateway Backups Are File-Level S3 Objects

Think instead:

**EBS Snapshots**

---

## Trap 8 — EBS and Volume Gateway Solve the Same Problem

False.

EBS:

**Block storage for EC2**

Volume Gateway:

**Hybrid block storage for on-premises applications**

---

# Quick Cheat Sheet

| Requirement | Answer |
|---|---|
| Hybrid Block Storage | Volume Gateway |
| Protocol | iSCSI |
| Primary Data in AWS | Cached Volume |
| Local Hot Data | Cached Volume |
| Minimize Local Storage | Cached Volume |
| Primary Data On-Premises | Stored Volume |
| Entire Dataset Local | Stored Volume |
| Low Latency for Entire Dataset | Stored Volume |
| Point-in-Time Backup | EBS Snapshot |
| NFS / SMB | File Gateway |
| Virtual Tape | Tape Gateway |
| EC2 Block Storage | EBS |

---

## Master Memory Trick

> [!tip] Master Memory Trick
> Picture Volume Gateway as an extension cord connecting an on-premises disk to AWS.
>
> **VOLUME**
> → Block storage
>
> **iSCSI**
> → Connection
>
> Then ask one question:
>
> **WHERE IS THE MAIN COPY?**

If:

> **CLOUD**
>
> → **CACHED**

If:

> **SITE**
>
> → **STORED**

So memorize:

> **CACHED = CLOUD**
>
> **STORED = SITE**

And:

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
- [[Tape Gateway]]
- [[EBS]]
- [[EBS Snapshots]]
- [[DataSync]]
- [[Snowball]]
## What Problem Does It Solve?

[[Storage Gateway]] connects:

**On-Premises Infrastructure**

with:

**AWS Cloud Storage**

It solves the problem of:

> **"How can my on-premises applications continue using familiar storage protocols while storing or backing up data in AWS?"**

Architecture:

On-Premises Applications  
↓  
Storage Gateway  
↓  
AWS Cloud Storage

Storage Gateway is a:

**Hybrid Cloud Storage Service**

> [!tip] Memory Trick
> **Storage Gateway = Bridge between your data center and AWS storage**

---

## Why Storage Gateway Exists

Many companies cannot move everything to AWS immediately.

They may still have:

- On-premises applications
- Existing file servers
- Local storage requirements
- Backup software
- Low-latency local access requirements

But they also want AWS for:

- Cloud storage
- Backups
- Disaster recovery
- Archival
- Storage expansion

Storage Gateway connects these two environments.

---

# Hybrid Cloud Architecture

Architecture:

On-Premises  
↓  
Storage Gateway  
↓  
AWS

This creates:

**Hybrid Storage**

where applications can continue running locally while AWS provides cloud-based storage capabilities.

---

# Storage Gateway Types

The major Storage Gateway types for SAA are:

1. **S3 File Gateway**
2. **FSx File Gateway**
3. **Volume Gateway**
4. **Tape Gateway**

Each solves a different hybrid-storage problem.

> [!tip] Master Decision
> **FILES → File Gateway**
>
> **BLOCKS → Volume Gateway**
>
> **TAPES → Tape Gateway**

---

# S3 File Gateway

[[S3 File Gateway]] provides on-premises applications with:

**File-based access to S3**

Supported protocols:

- NFS
- SMB

Architecture:

On-Premises Application  
↓  
NFS / SMB  
↓  
S3 File Gateway  
↓  
[[S3]]

Applications see:

**Files**

while AWS stores them as:

**S3 objects**

---

# File-to-Object Mapping

This is an important architecture concept.

On-Premises:

`report.pdf`

↓  
NFS / SMB  
↓  
S3 File Gateway  
↓  

S3:

`report.pdf` object

The application uses:

**File protocols**

while the backend uses:

**Object storage**

### Memory Trick

**File Gateway = Files in front, S3 objects in back**

---

# S3 File Gateway Local Cache

S3 File Gateway maintains a:

**Local Cache**

for frequently accessed data.

Architecture:

Application  
↓  
File Gateway  
├── Local Cache
└── S3

Frequently accessed data can remain:

**Locally available**

while the durable data resides in AWS.

This improves:

**Local access performance**

---

# S3 Storage Classes

Data stored through S3 File Gateway can take advantage of:

**S3 storage capabilities**

including lifecycle transitions.

Architecture:

File Gateway  
↓  
S3  
↓  
[[S3 Lifecycle Rules]]  
↓  
Lower-Cost Storage Class

This can help reduce long-term storage cost.

---

# S3 File Gateway Authentication

For SMB environments, S3 File Gateway can integrate with:

**Active Directory**

This is useful for enterprise Windows file-sharing environments.

### Scenario Recognition

> **On-premises users need SMB access to files stored as S3 objects**
>
> → **S3 File Gateway**

---

# FSx File Gateway

[[FSx File Gateway]] provides on-premises access to:

[[FSx for Windows File Server]]

Architecture:

On-Premises Windows Users  
↓  
SMB  
↓  
FSx File Gateway  
↓  
FSx for Windows File Server

This is useful when organizations want:

**Hybrid access to Windows file shares hosted in AWS**

---

# FSx File Gateway Local Cache

FSx File Gateway maintains:

**Local cached copies**

of frequently accessed data.

Architecture:

On-Premises User  
↓  
FSx File Gateway  
├── Local Cache
└── FSx Windows in AWS

This provides:

**Low-latency local access**

while the primary file system exists in AWS.

---

# S3 File Gateway vs FSx File Gateway

These are easy to confuse.

## S3 File Gateway

Backend:

[[S3]]

Front-end protocols:

- NFS
- SMB

Data stored as:

**S3 objects**

---

## FSx File Gateway

Backend:

[[FSx for Windows File Server]]

Front-end:

**SMB**

Designed for:

**Windows file shares**

### Memory Trick

**S3 File Gateway**
→ File interface to S3

**FSx File Gateway**
→ Local access to Windows FSx

---

# Volume Gateway

[[Volume Gateway]] provides:

**Block storage**

to on-premises applications using:

**iSCSI**

Architecture:

On-Premises Server  
↓  
iSCSI  
↓  
Volume Gateway  
↓  
AWS

Think:

**Hybrid block storage**

> [!tip] Memory Trick
> **Volume = Block**

---

# Volume Gateway Backups

Volume Gateway volumes can be backed up as:

**EBS Snapshots**

Architecture:

On-Premises Volume  
↓  
Volume Gateway  
↓  
Snapshot  
↓  
[[EBS Snapshots]]

These snapshots can help with:

- Backup
- Disaster recovery
- Migration

---

# Volume Gateway Modes

Volume Gateway has two important modes:

1. **Cached Volumes**
2. **Stored Volumes**

This is a major exam distinction.

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
Volume Gateway  
├── Frequently Used Data → Local Cache
└── Primary Data → AWS

### Memory Trick

**Cached = Cloud holds the main copy**

---

# Why Cached Volumes?

Cached Volumes reduce the amount of:

**On-premises storage capacity**

required.

The full dataset can live in AWS while local cache provides:

**Low-latency access to frequently used data**

### Exam Pattern

> **Minimize local storage while keeping frequently accessed blocks local**
>
> → **Cached Volume Gateway**

---

# Stored Volumes

With:

**Stored Volumes**

the complete primary dataset remains:

**On-Premises**

while data is asynchronously backed up to:

**AWS**

Architecture:

Application  
↓  
Local Primary Storage  
↓  
Volume Gateway  
↓  
AWS Backup

### Memory Trick

**Stored = Store the main copy locally**

---

# Why Stored Volumes?

Stored Volumes are useful when:

**Low-latency access to the entire dataset**

is required locally.

The on-premises environment retains:

**The full dataset**

while AWS provides:

**Off-site backup**

---

# Cached vs Stored Volumes

| Requirement | Cached | Stored |
|---|---:|---:|
| Primary Data in AWS | ✅ | ❌ |
| Primary Data On-Premises | ❌ | ✅ |
| Local Cache | ✅ | Full Dataset Local |
| Minimize Local Storage | ✅ | ❌ |
| Full Dataset Low-Latency Local Access | ❌ | ✅ |
| Cloud Backup | ✅ | ✅ |

### Memory Trick

**CACHED**
→ Cloud main copy

**STORED**
→ Site main copy

---

# Tape Gateway

[[Tape Gateway]] provides a:

**Virtual Tape Library**

or:

**VTL**

for organizations using traditional:

**Tape-based backup systems**

Architecture:

Backup Software  
↓  
iSCSI  
↓  
Tape Gateway  
↓  
Virtual Tapes  
↓  
AWS

> [!tip] Memory Trick
> **Tape Gateway = Replace physical tapes with virtual AWS tapes**

---

# Why Tape Gateway?

Many enterprises still use backup software designed for:

**Tape libraries**

Instead of completely redesigning the backup environment:

Existing Backup Software  
↓  
Tape Gateway  
↓  
AWS

The backup application behaves as if it is writing to:

**Physical tapes**

but the tapes are:

**Virtual**

---

# Tape Storage

Virtual tapes can be stored using AWS storage services for:

- Backup
- Long-term retention
- Archival

This makes Tape Gateway useful for:

**Replacing physical tape infrastructure**

---

# Tape Gateway Use Cases

Think:

- Legacy backup software
- Tape replacement
- Virtual Tape Library
- Long-term archive
- Existing tape workflows

### Strong Exam Pattern

> **"Company wants to stop managing physical backup tapes without changing its tape-based backup software."**
>
> → **Tape Gateway**

---

# Storage Gateway Deployment

Storage Gateway can be deployed:

**On-Premises**

as a virtual appliance.

Conceptually:

VMware / Hypervisor  
↓  
Storage Gateway Appliance  
↓  
AWS

It can also be deployed using:

**Hardware appliance options**

depending on the environment.

---

# Local Cache

Local caching is a recurring Storage Gateway concept.

Why?

On-Premises Application  
↓  
Local Gateway Cache  
↓  
Fast Access

while:

AWS  
↓  
Provides Durable Cloud Storage

This gives hybrid architectures:

**Local performance + Cloud scale**

---

# Storage Gateway vs DataSync

These services are easy to confuse.

## [[Storage Gateway]]

Provides:

**Ongoing hybrid storage access**

Think:

On-Premises Application  
↕  
AWS Storage

---

## [[DataSync]]

Provides:

**Data transfer / migration**

Think:

Source Storage  
↓  
Transfer Data  
↓  
AWS Storage

### Memory Trick

**Storage Gateway = USE cloud storage from on-prem**

**DataSync = MOVE data to/from AWS**

---

# Storage Gateway vs Snowball

## [[Snowball]]

Best for:

**Offline massive data transfer**

Physical device:

Data  
↓  
Snowball  
↓  
Ship to AWS

---

## Storage Gateway

Best for:

**Ongoing hybrid storage**

Network connection:

On-Premises  
↕  
AWS

### Memory Trick

**Snowball = Ship**

**Storage Gateway = Bridge**

---

# Storage Gateway vs Direct Connect

[[05-Networking/Direct Connect]] provides:

**Dedicated network connectivity**

Storage Gateway provides:

**Storage integration**

They can work together.

Architecture:

On-Premises Application  
↓  
Storage Gateway  
↓  
Direct Connect  
↓  
AWS Storage

### Exam Trap

Direct Connect does not itself provide:

**File, block, or tape storage interfaces**

---

# Storage Gateway vs S3

S3 is:

**Object Storage**

Storage Gateway can provide familiar:

**File / Block / Tape interfaces**

to AWS storage.

Example:

Legacy Application  
↓  
NFS  
↓  
S3 File Gateway  
↓  
S3

The application does not need to directly use:

**S3 APIs**

---

# Architecture Thinking

## Scenario 1 — NFS to S3

An on-premises Linux application uses:

**NFS**

The company wants files stored as objects in S3.

**Choose → S3 File Gateway**

---

## Scenario 2 — SMB to S3

Windows users require:

**SMB**

but the company wants backend storage in S3.

**Choose → S3 File Gateway**

---

## Scenario 3 — Hybrid Windows FSx

On-premises Windows users need low-latency access to:

**FSx for Windows File Server**

running in AWS.

**Choose → FSx File Gateway**

---

## Scenario 4 — Minimize Local Block Storage

A company wants the primary block dataset stored in AWS.

Only frequently accessed blocks should remain locally cached.

**Choose → Cached Volume Gateway**

---

## Scenario 5 — Entire Dataset Must Stay Local

A company requires:

**Low-latency local access to its complete block dataset**

but wants cloud backups.

**Choose → Stored Volume Gateway**

---

## Scenario 6 — Replace Physical Tapes

A company uses traditional tape-based backup software.

It wants to eliminate physical tapes without redesigning its backup system.

**Choose → Tape Gateway**

---

## Scenario 7 — Migrate 800 TB Once

A company must perform a one-time migration of:

800 TB

with limited network bandwidth.

**Do NOT choose Storage Gateway as the primary migration solution**

Think:

[[Snowball]]

---

## Scenario 8 — Recurring File Transfers

A company needs automated scheduled transfers between its on-premises NFS server and AWS.

Think:

[[DataSync]]

rather than using Storage Gateway purely as a migration tool.

---

# Scenario Recognition

## Immediately Think Storage Gateway When You See

- Hybrid storage
- On-premises + AWS
- Local cache
- Existing applications
- NFS
- SMB
- iSCSI
- Virtual tapes
- Cloud-backed storage
- Hybrid backup

---

## Immediately Think S3 File Gateway When You See

- NFS → S3
- SMB → S3
- Files stored as S3 objects
- Local file cache

---

## Immediately Think FSx File Gateway When You See

- On-premises Windows
- SMB
- FSx Windows
- Local cache of FSx files

---

## Immediately Think Volume Gateway When You See

- iSCSI
- Block storage
- EBS snapshots
- Cached volumes
- Stored volumes

---

## Immediately Think Tape Gateway When You See

- Tape
- Virtual Tape Library
- VTL
- Legacy backup software
- Replace physical tapes

---

# Exam Traps

## Trap 1 — Storage Gateway Is Only for Migration

False.

Its major purpose is:

**Hybrid storage integration**

---

## Trap 2 — S3 File Gateway Exposes S3 APIs to Applications

Not the key architecture.

Applications use:

- NFS
- SMB

while the backend data is stored as:

**S3 objects**

---

## Trap 3 — Volume Gateway Provides File Storage

False.

Volume Gateway provides:

**Block storage through iSCSI**

---

## Trap 4 — Cached Volume Keeps Primary Data On-Premises

False.

Cached:

**Primary data in AWS**

---

## Trap 5 — Stored Volume Keeps Primary Data in AWS

False.

Stored:

**Primary data on-premises**

---

## Trap 6 — Tape Gateway Requires Physical Tapes

False.

It provides:

**Virtual tapes**

---

## Trap 7 — Storage Gateway and Snowball Solve the Same Problem

False.

Snowball:

**Offline physical transfer**

Storage Gateway:

**Ongoing hybrid storage**

---

## Trap 8 — Storage Gateway and DataSync Are Identical

False.

Storage Gateway:

**Storage interface**

DataSync:

**Data movement**

---

# Quick Cheat Sheet

| Requirement | Best Choice |
|---|---|
| Hybrid AWS Storage | Storage Gateway |
| NFS → S3 | S3 File Gateway |
| SMB → S3 | S3 File Gateway |
| Files Stored as S3 Objects | S3 File Gateway |
| On-Prem → FSx Windows | FSx File Gateway |
| Block Storage | Volume Gateway |
| Block Protocol | iSCSI |
| Primary Data in AWS | Cached Volume |
| Primary Data On-Prem | Stored Volume |
| EBS Snapshot Backup | Volume Gateway |
| Replace Physical Tapes | Tape Gateway |
| Virtual Tape Library | Tape Gateway |
| One-Time Massive Offline Transfer | Snowball |
| Automated Data Transfer | DataSync |

---

## Master Memory Trick

> [!tip] Master Memory Trick
> **Storage Gateway = Door from your data center into AWS storage**
>
> **FILE GATEWAY**
>
> → Files go through the door
>
> **VOLUME GATEWAY**
>
> → Blocks go through the door
>
> **TAPE GATEWAY**
>
> → Virtual tapes go through the door

Then:

> **S3 FILE**
> → NFS / SMB → S3
>
> **FSx FILE**
> → SMB → FSx Windows
>
> **CACHED VOLUME**
> → Main copy in CLOUD
>
> **STORED VOLUME**
> → Main copy at your SITE
>
> **TAPE**
> → Replace physical tapes

And the killer exam distinction:

> **Storage Gateway = HYBRID ACCESS**
>
> **DataSync = DATA MOVEMENT**
>
> **Snowball = OFFLINE MIGRATION**

---

## Related Notes

- [[S3 File Gateway]]
- [[FSx File Gateway]]
- [[Volume Gateway]]
- [[Tape Gateway]]
- [[S3]]
- [[FSx for Windows File Server]]
- [[EBS Snapshots]]
- [[DataSync]]
- [[Snowball]]
- [[05-Networking/Direct Connect]]
- [[05-Networking/Site-to-Site VPN]]
- [[S3 Lifecycle Rules]]
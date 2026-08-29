## Storage Cheat Sheet

## Storage Exam Strategy

For SAA questions, start by asking:

> **What type of storage is needed, where is the workload running, and is the goal ACCESS or MOVE?**

Use this fast decision map:

| Requirement | Immediately Think |
|---|---|
| Object storage | [[S3]] |
| EC2 block storage | [[EBS]] |
| Shared Linux file storage | [[EFS]] |
| Windows SMB file share | [[FSx for Windows File Server]] |
| HPC / ML parallel file system | [[FSx for Lustre]] |
| NetApp workloads | [[FSx for NetApp ONTAP]] |
| ZFS workloads | [[FSx for OpenZFS]] |
| Hybrid file access to S3 | [[S3 File Gateway]] |
| Hybrid block storage | [[Volume Gateway]] |
| Virtual tape backup | [[Tape Gateway]] |
| Move / sync data online | [[DataSync]] |
| SFTP / FTPS / FTP | [[AWS Transfer Family]] |
| Huge offline migration | [[Snow Family]] |
| Small portable edge device | [[Snowcone]] |
| Large storage-focused Snow device | [[Snowball Edge Storage Optimized]] |
| Heavy edge compute | [[Snowball Edge Compute Optimized]] |

> [!tip] Master Storage Question
> Ask:
>
> **OBJECT?**
>
> **BLOCK?**
>
> **FILE?**
>
> **HYBRID?**
>
> **TRANSFER?**
>
> **EDGE?**

---

## S3

[[S3]] provides:

**Object Storage**

Think:

- Buckets
- Objects
- Keys
- Data lakes
- Backups
- Static content
- Media
- Logs
- Archives

### Killer Exam Clue

> **Massively scalable object storage**
>
> → **S3**

### Memory Trick

**S3 = STORE OBJECTS**

---

## EBS

[[EBS]] provides:

**Persistent Block Storage**

primarily for:

[[EC2]]

Think:

EC2  
↓  
EBS Volume

Best for:

- Boot volumes
- Databases on EC2
- Application disks
- High IOPS
- Persistent block storage

### Killer Exam Clue

> **EC2 needs a persistent disk**
>
> → **EBS**

### Memory Trick

**EBS = EC2 Hard Drive**

---

## EFS

[[EFS]] provides:

**Managed shared NFS file storage**

Think:

- Linux
- NFS
- Shared files
- Multiple EC2 instances
- Elastic file system

Architecture:

EC2 #1  
↘  
EFS

EC2 #2  
→  
EFS

EC2 #3  
↗  
EFS

### Killer Exam Clue

> **Multiple Linux instances need the same shared file system**
>
> → **EFS**

### Memory Trick

**EFS = Elastic Linux File Share**

---

## FSx

[[FSx]] provides:

**Fully managed specialized file systems**

Main variants:

- [[FSx for Windows File Server]]
- [[FSx for Lustre]]
- [[FSx for NetApp ONTAP]]
- [[FSx for OpenZFS]]

### Memory Trick

**FSx = Specialized File Systems**

---

## FSx for Windows File Server

[[FSx for Windows File Server]]

Think:

- Windows
- SMB
- NTFS
- Active Directory
- ACLs
- User quotas
- Multi-AZ

### Killer Exam Clue

> **Windows + SMB + Active Directory**
>
> → **FSx for Windows File Server**

---

## FSx for Lustre

[[FSx for Lustre]]

Think:

- HPC
- Machine Learning
- Parallel file system
- Massive throughput
- Millions of IOPS
- S3 integration

### Killer Exam Clue

> **HPC / ML + shared high-performance storage**
>
> → **FSx for Lustre**

### Memory Trick

**Lustre = Linux + Cluster**

---

## Lustre Scratch vs Persistent

### Scratch

Think:

- Temporary
- Not replicated
- High burst
- Short-term processing
- Re-creatable data

### Persistent

Think:

- Long-term
- Replicated within same AZ
- Important data
- Sensitive data

### Memory Trick

**Scratch = Disposable**

**Persistent = Keep It**

---

## FSx for NetApp ONTAP

[[FSx for NetApp ONTAP]]

Think:

- NetApp
- ONTAP
- NFS
- SMB
- iSCSI
- Compression
- Deduplication
- Snapshots
- Instant cloning

### Killer Exam Clue

> **Existing NetApp environment**
>
> → **FSx for NetApp ONTAP**

### Memory Trick

**NetApp = ONTAP**

---

## FSx for OpenZFS

[[FSx for OpenZFS]]

Think:

- ZFS
- NFS
- High IOPS
- Low latency
- Snapshots
- Compression
- Instant cloning

### Killer Exam Clue

> **Existing ZFS workload moving to AWS**
>
> → **FSx for OpenZFS**

### Memory Trick

**ZFS = OpenZFS**

---

## FSx Family Rapid-Fire

| Exam Clue | Answer |
|---|---|
| Windows / SMB | FSx Windows |
| HPC / ML | FSx Lustre |
| NetApp | FSx ONTAP |
| ZFS | FSx OpenZFS |
| Generic Linux NFS | EFS |

---

## Storage Gateway

[[Storage Gateway]] provides:

**Hybrid storage access**

between:

On-Premises  
and  
AWS

### Master Memory Trick

**Storage Gateway = ACCESS**

---

## S3 File Gateway

[[S3 File Gateway]]

Front-end:

- NFS
- SMB

Backend:

[[S3]]

Files become:

**S3 objects**

Architecture:

On-Premises Application  
↓  
NFS / SMB  
↓  
S3 File Gateway  
↓  
S3

### Killer Exam Clue

> **On-premises NFS/SMB access to S3**
>
> → **S3 File Gateway**

### Memory Trick

**FILES IN FRONT, OBJECTS IN BACK**

---

## FSx File Gateway

[[FSx File Gateway]]

Classic course concept:

- SMB
- On-premises Windows users
- Local cache
- Backend = FSx Windows

### Memory Trick

**Local doorway to FSx Windows**

> [!warning] Current Context
> Recognize this when it appears in older course material or practice questions, but always prioritize the architecture described in the current exam question.

---

## Volume Gateway

[[Volume Gateway]]

Provides:

**Hybrid Block Storage**

Protocol:

**iSCSI**

Two modes:

- Cached
- Stored

---

## Cached Volumes

Primary data:

**AWS**

Frequently accessed blocks:

**Local cache**

### Memory Trick

**CACHED = CLOUD**

---

## Stored Volumes

Primary data:

**On-Premises**

Cloud provides:

**Backup**

### Memory Trick

**STORED = SITE**

---

## Cached vs Stored

| Requirement | Cached | Stored |
|---|---:|---:|
| Primary Data in AWS | ✅ | ❌ |
| Primary Data On-Prem | ❌ | ✅ |
| Minimize Local Storage | ✅ | ❌ |
| Entire Dataset Local | ❌ | ✅ |
| iSCSI | ✅ | ✅ |

---

## Tape Gateway

[[Tape Gateway]]

Provides:

**Virtual Tape Library**

or:

**VTL**

Think:

- Existing backup software
- Virtual tapes
- Replace physical tapes
- Long-term backup

### Killer Exam Clue

> **Keep tape-based backup software but eliminate physical tapes**
>
> → **Tape Gateway**

### Memory Trick

**Tape Gateway = Virtual Tape Room**

---

## DataSync

[[DataSync]]

Provides:

**Managed online data movement and synchronization**

Think:

Source  
↓  
DataSync  
↓  
Destination

Common clues:

- NFS migration
- SMB migration
- Scheduled transfer
- Recurring sync
- Changed files
- S3 / EFS / FSx

### Killer Exam Clue

> **Move or synchronize large datasets over the network**
>
> → **DataSync**

### Memory Trick

**DataSync = MOVE / SYNC**

---

## Storage Gateway vs DataSync

This is one of the biggest exam distinctions.

**Need ongoing ACCESS**
→ [[Storage Gateway]]

**Need to MOVE / SYNC**
→ [[DataSync]]

> [!tip] Killer Question
> **ACCESS or MOVE?**

---

## AWS Transfer Family

[[AWS Transfer Family]]

Provides managed:

- SFTP
- FTPS
- FTP

with backends such as:

- [[S3]]
- [[EFS]]

### Killer Exam Clue

> **Business partner uploads through SFTP into S3**
>
> → **AWS Transfer Family**

---

## Transfer Protocol Memory

**SFTP**
→ SSH

**FTPS**
→ TLS

**FTP**
→ Plain / traditional

### Memory Trick

**FTP-style protocol = Transfer Family**

---

## Transfer Family vs DataSync

**SFTP / FTPS / FTP**
→ Transfer Family

**NFS / SMB migration or synchronization**
→ DataSync

---

## Snow Family

[[Snow Family]] provides:

**Physical data transfer + edge computing**

Think:

- Huge datasets
- Poor bandwidth
- Offline migration
- Remote locations
- Edge compute

### Master Memory Trick

**Snow = MOVE PHYSICALLY**

---

## Snowcone

[[Snowcone]]

Think:

- Smallest
- Portable
- Rugged
- Remote
- Edge computing
- Smaller datasets

### Killer Exam Clue

> **Small portable AWS edge device**
>
> → **Snowcone**

---

## Snowball Edge Storage Optimized

[[Snowball Edge Storage Optimized]]

Think:

- Large migration
- Storage capacity
- Poor bandwidth
- Hundreds of TB
- Storage-heavy edge workload

### Killer Exam Clue

> **Huge dataset + network cannot meet deadline**
>
> → **Snowball Edge Storage Optimized**

### Memory Trick

**DATA problem = Storage Optimized**

---

## Snowball Edge Compute Optimized

[[Snowball Edge Compute Optimized]]

Think:

- Heavy edge processing
- ML inference
- Video analytics
- Remote sensors
- Poor connectivity

### Killer Exam Clue

> **Substantial compute in a disconnected environment**
>
> → **Snowball Edge Compute Optimized**

### Memory Trick

**PROCESSING problem = Compute Optimized**

---

## Snowmobile

[[Snowmobile]]

Classic / legacy concept:

- Truck-scale migration
- Tens of petabytes
- Historically around 100 PB
- Entire data center

> [!warning] Current Context
> Snowmobile is primarily legacy exam/course knowledge.
>
> AWS stopped accepting new Snowmobile customers in 2024.

### Memory Trick

**Cone → Small**

**Ball → Large**

**Mobile → Massive**

---

## Snow vs DataSync

**Good enough network**
→ DataSync

**Network impractical**
→ Snow

### Memory Trick

**DataSync = Send it**

**Snow = Ship it**

---

## Snow vs Storage Gateway

**Offline migration / edge**
→ Snow

**Ongoing hybrid storage access**
→ Storage Gateway

---

## Data Migration Decision Table

| Requirement | Best Choice |
|---|---|
| Online NFS/SMB migration | DataSync |
| Scheduled synchronization | DataSync |
| SFTP partner upload | Transfer Family |
| Ongoing hybrid storage | Storage Gateway |
| Huge offline migration | Snowball Edge |
| Small portable edge workload | Snowcone |
| Heavy edge processing | Compute Optimized |

---

## Protocol Decision Table

| Clue | Best Association |
|---|---|
| S3 API | S3 |
| EC2 Block | EBS |
| NFS + Shared Linux | EFS |
| SMB + Windows | FSx Windows |
| NFS/SMB → S3 | S3 File Gateway |
| iSCSI + Hybrid Volume | Volume Gateway |
| VTL | Tape Gateway |
| SFTP / FTPS / FTP | Transfer Family |
| NFS/SMB + Move | DataSync |
| NetApp + NFS/SMB/iSCSI | FSx ONTAP |
| ZFS + NFS | FSx OpenZFS |

> [!warning] Exam Trap
> Protocol narrows the answer.
>
> **The architecture requirement chooses the answer.**

---

## Architecture Thinking

### Scenario 1 — Linux Shared Files

Several Linux EC2 instances need the same shared files.

**Choose → [[EFS]]**

---

### Scenario 2 — EC2 Disk

An EC2-hosted database needs persistent low-latency block storage.

**Choose → [[EBS]]**

---

### Scenario 3 — Object Storage

A company stores millions of images, logs, and backups.

**Choose → [[S3]]**

---

### Scenario 4 — Windows Share

A Windows application needs:

- SMB
- NTFS
- Active Directory

**Choose → [[FSx for Windows File Server]]**

---

### Scenario 5 — HPC

A compute cluster needs extreme shared-file throughput.

**Choose → [[FSx for Lustre]]**

---

### Scenario 6 — NetApp

A company wants to migrate NetApp ONTAP workloads.

**Choose → [[FSx for NetApp ONTAP]]**

---

### Scenario 7 — ZFS

A company wants to migrate an existing ZFS workload.

**Choose → [[FSx for OpenZFS]]**

---

### Scenario 8 — NFS to S3 Access

An on-premises app must keep using NFS while files live in S3.

**Choose → [[S3 File Gateway]]**

---

### Scenario 9 — Hybrid Block

An on-premises application requires iSCSI volumes backed by AWS.

**Choose → [[Volume Gateway]]**

---

### Scenario 10 — Tape Replacement

Legacy backup software expects a tape library.

**Choose → [[Tape Gateway]]**

---

### Scenario 11 — Nightly Sync

Changed files from an on-premises NFS share must sync to S3 nightly.

**Choose → [[DataSync]]**

---

### Scenario 12 — SFTP Partner

A partner must upload files using SFTP into S3.

**Choose → [[AWS Transfer Family]]**

---

### Scenario 13 — Huge Migration

Hundreds of TB must move to AWS, but the network cannot meet the deadline.

**Choose → [[Snowball Edge Storage Optimized]]**

---

### Scenario 14 — Remote Compute

A remote factory needs local video analytics with unreliable connectivity.

**Choose → [[Snowball Edge Compute Optimized]]**

---

## Biggest Storage Exam Traps

### Trap 1 — NFS Always Means EFS

False.

NFS could mean:

- EFS
- S3 File Gateway
- DataSync
- FSx Lustre
- FSx ONTAP
- FSx OpenZFS

Ask:

**What is the workload doing?**

---

### Trap 2 — SMB Always Means FSx Windows

False.

SMB could appear with:

- FSx Windows
- S3 File Gateway
- DataSync
- FSx ONTAP

Again:

**Requirement > Protocol**

---

### Trap 3 — iSCSI Always Means Volume Gateway

False.

iSCSI also appears with:

[[FSx for NetApp ONTAP]]

---

### Trap 4 — Large Dataset Always Means Snowball

False.

Ask:

- How much bandwidth?
- How much time?
- Is this recurring?

If the network can meet the requirement:

**DataSync may be better**

---

### Trap 5 — SFTP Means S3 File Gateway

False.

SFTP:

→ [[AWS Transfer Family]]

S3 File Gateway:

→ NFS / SMB

---

### Trap 6 — Storage Gateway Is Mainly for Migration

False.

Storage Gateway:

**ACCESS**

DataSync:

**MOVE**

---

### Trap 7 — File Storage Automatically Means EFS

False.

Linux  
→ EFS

Windows  
→ FSx Windows

HPC  
→ FSx Lustre

NetApp  
→ FSx ONTAP

ZFS  
→ FSx OpenZFS

---

### Trap 8 — Snowball Edge Is Only for Data Migration

False.

It can also perform:

**Edge computing**

---

## Quick Cheat Sheet

| Exam Clue | Answer |
|---|---|
| Objects | S3 |
| EC2 Disk | EBS |
| Linux Shared NFS | EFS |
| Windows SMB | FSx Windows |
| HPC / ML | FSx Lustre |
| NetApp | FSx ONTAP |
| ZFS | FSx OpenZFS |
| NFS/SMB → S3 | S3 File Gateway |
| iSCSI Hybrid Block | Volume Gateway |
| VTL / Virtual Tape | Tape Gateway |
| Move / Sync | DataSync |
| SFTP / FTPS / FTP | Transfer Family |
| Large Offline Migration | Snowball Edge |
| Small Portable Edge | Snowcone |
| Heavy Edge Processing | Snowball Edge Compute Optimized |

---

## Final Exam Rapid-Fire

> **OBJECTS → S3**
>
> **EC2 DISK → EBS**
>
> **LINUX SHARED FILES → EFS**
>
> **WINDOWS + SMB → FSx Windows**
>
> **HPC / ML → FSx Lustre**
>
> **NETAPP → FSx ONTAP**
>
> **ZFS → FSx OpenZFS**
>
> **NFS/SMB TO S3 → S3 File Gateway**
>
> **ISCSI BLOCKS → Volume Gateway**
>
> **VIRTUAL TAPES → Tape Gateway**
>
> **MOVE / SYNC → DataSync**
>
> **SFTP / FTPS / FTP → Transfer Family**
>
> **HUGE DATA + BAD NETWORK → Snowball Edge**
>
> **PORTABLE EDGE → Snowcone**
>
> **HEAVY EDGE COMPUTE → Compute Optimized**

---

## Master Memory Trick

> [!tip] Storage Master Memory Trick
> Break the entire storage section into five jobs:
>
> **STORE OBJECTS**
> → S3
>
> **ATTACH BLOCK STORAGE**
> → EBS
>
> **SHARE FILES**
> → EFS / FSx
>
> **CONNECT ON-PREM STORAGE**
> → Storage Gateway
>
> **MOVE DATA**
> → DataSync / Transfer Family / Snow

Then:

> **Storage Gateway**
> → ACCESS
>
> **DataSync**
> → MOVE / SYNC
>
> **Transfer Family**
> → FTP-style protocols
>
> **Snow**
> → Physical migration / Edge

And the single best storage exam rule:

> **PROTOCOL narrows the answer**
>
> **REQUIREMENT chooses the answer**

---

## Related Notes

- [[S3]]
- [[EBS]]
- [[EFS]]
- [[FSx]]
- [[FSx for Windows File Server]]
- [[FSx for Lustre]]
- [[FSx for NetApp ONTAP]]
- [[FSx for OpenZFS]]
- [[Storage Gateway]]
- [[S3 File Gateway]]
- [[FSx File Gateway]]
- [[Volume Gateway]]
- [[Tape Gateway]]
- [[DataSync]]
- [[AWS Transfer Family]]
- [[Snow Family]]
- [[Snowcone]]
- [[Snowball Edge]]
- [[Snowball Edge Storage Optimized]]
- [[Snowball Edge Compute Optimized]]
- [[Snowmobile]]
- [[Storage Services Comparison]]

## Storage Services Comparison

## Why This Comparison Matters

AWS SAA questions often give you several storage services that seem capable of solving the same problem.

The exam is really testing:

> **What type of storage is required, where is it accessed from, what protocol is needed, and is the goal ongoing access or data movement?**

The major services to distinguish are:

- [[S3]]
- [[EBS]]
- [[EFS]]
- [[FSx]]
- [[Storage Gateway]]
- [[DataSync]]
- [[AWS Transfer Family]]
- [[Snow Family]]

> [!tip] Master Decision
> **OBJECTS → S3**
>
> **EC2 BLOCK STORAGE → EBS**
>
> **SHARED LINUX FILES → EFS**
>
> **SPECIALIZED MANAGED FILE SYSTEM → FSx**
>
> **HYBRID STORAGE ACCESS → Storage Gateway**
>
> **MOVE / SYNC DATA → DataSync**
>
> **SFTP / FTPS / FTP → Transfer Family**
>
> **HUGE DATA + NETWORK IMPRACTICAL → Snow Family**

---

## Start With the Storage Type

The fastest way to eliminate wrong answers is to determine whether the workload needs:

1. Object Storage
2. Block Storage
3. File Storage
4. Hybrid Storage
5. Data Transfer

---

# Object Storage

If the question describes:

- Objects
- Buckets
- Object keys
- Massive scalability
- Static assets
- Data lakes
- Backups
- Archival

think:

[[S3]]

Architecture:

Application  
↓  
S3 API  
↓  
S3 Bucket  
↓  
Objects

> [!tip] Memory Trick
> **S3 = Objects**

---

# Block Storage

If the question describes:

- EC2 disk
- Boot volume
- Database disk
- Low-latency block storage
- IOPS
- Provisioned throughput

think:

[[EBS]]

Architecture:

EC2  
↓  
EBS Volume

> [!tip] Memory Trick
> **EBS = Persistent block storage for EC2**

---

# File Storage

If applications require:

- File system
- Directories
- File paths
- NFS
- SMB
- Shared file access

think about:

- [[EFS]]
- [[FSx]]
- File Gateway

Then determine:

> **Which file system, protocol, operating system, and location?**

---

# S3

[[S3]] is:

**Object Storage**

Best for:

- Static content
- Backups
- Data lakes
- Logs
- Media
- Objects
- Massive durability
- Massive scalability

Access primarily through:

**S3 APIs / HTTP**

### Strong Exam Clues

- Bucket
- Object
- Object key
- Lifecycle
- Storage class
- Versioning
- Static website
- Data lake

---

# EBS

[[EBS]] is:

**Block Storage**

primarily associated with:

[[EC2]]

Architecture:

EC2 Instance  
↓  
EBS Volume

Best for:

- Boot volumes
- Databases running on EC2
- Persistent application disks
- Workloads requiring predictable IOPS / throughput

### Strong Exam Clues

- Block
- Volume
- IOPS
- EC2 disk
- gp3
- io2
- Snapshot

---

# EFS

[[EFS]] is:

**Managed shared file storage**

using:

**NFS**

It is designed primarily for:

**Linux workloads**

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

Multiple compute resources can access:

**The same file system**

### Strong Exam Clues

- Linux
- NFS
- Shared files
- Multiple EC2 instances
- Regional / Multi-AZ availability
- Automatically scales

> [!tip] Memory Trick
> **EFS = Elastic shared NFS file system**

---

# FSx

[[FSx]] provides:

**Fully managed specialized file systems**

Important SAA variants include:

- [[FSx for Windows File Server]]
- [[FSx for Lustre]]
- [[FSx for NetApp ONTAP]]
- [[FSx for OpenZFS]]

> [!tip] Memory Trick
> **FSx = Specialized managed file systems**

---

# FSx for Windows File Server

[[FSx for Windows File Server]]

Think:

- Windows
- SMB
- Microsoft Active Directory integration
- Windows file shares
- NTFS

### Strong Exam Pattern

> **Managed Windows shared file system using SMB**
>
> → **FSx for Windows File Server**

---

# FSx for Lustre

[[FSx for Lustre]]

Think:

- HPC
- Machine learning
- High-performance computing
- Parallel processing
- Very high throughput
- S3 integration

### Strong Exam Pattern

> **High-performance parallel file system for HPC / ML**
>
> → **FSx for Lustre**

---

# FSx for NetApp ONTAP

[[FSx for NetApp ONTAP]]

Think:

- NetApp ONTAP
- Enterprise NAS
- Multi-protocol access
- NFS
- SMB
- iSCSI
- Snapshots
- Cloning
- Storage efficiencies

### Strong Exam Pattern

> **Existing NetApp / ONTAP workloads need an AWS-managed equivalent**
>
> → **FSx for NetApp ONTAP**

---

# FSx for OpenZFS

[[FSx for OpenZFS]]

Think:

- ZFS
- Linux
- NFS
- Snapshots
- Cloning
- Migrating ZFS workloads

### Strong Exam Pattern

> **Existing ZFS workload needs managed AWS storage**
>
> → **FSx for OpenZFS**

---

# Storage Gateway

[[Storage Gateway]] provides:

**Hybrid cloud storage**

It connects:

**On-Premises Environments**

with:

**AWS Storage**

Its major SAA purpose is:

> **Ongoing hybrid storage access**

Conceptually:

On-Premises Application  
↕  
Storage Gateway  
↕  
AWS Storage

### Strong Exam Clue

> **Hybrid storage**

---

# S3 File Gateway

[[S3 File Gateway]]

Provides on-premises applications with:

- NFS
- SMB

while storing files as:

**Objects in S3**

Architecture:

On-Premises Application  
↓  
NFS / SMB  
↓  
S3 File Gateway  
↓  
[[S3]]

### Strong Exam Pattern

> **On-premises applications need NFS/SMB access while the data is stored as S3 objects**
>
> → **S3 File Gateway**

---

# FSx File Gateway

[[FSx File Gateway]] is mainly important as:

**Older / legacy Storage Gateway course material**

It provided:

**Low-latency on-premises SMB access**

to:

[[FSx for Windows File Server]]

using:

**Local caching**

> [!warning] Current AWS Context
> Recognize FSx File Gateway if it appears in older course material or practice questions.
>
> Always prioritize the actual architecture requirements and current service choices presented in the exam question.

---

# Volume Gateway

[[Volume Gateway]]

provides:

**iSCSI block storage**

for hybrid environments.

The classic two configurations are:

- Cached Volumes
- Stored Volumes

---

## Cached Volumes

Primary data is stored in:

**AWS**

while frequently accessed blocks are cached:

**On-Premises**

Architecture:

On-Premises Application  
↓  
iSCSI  
↓  
Volume Gateway  
├── Local Cache
└── Primary Data in AWS

> [!tip] Memory Trick
> **CACHED = CLOUD is primary**

---

## Stored Volumes

Primary data remains:

**On-Premises**

while asynchronous snapshots / backups are stored in:

**AWS**

Architecture:

Application  
↓  
Local Primary Dataset  
↓  
Volume Gateway  
↓  
AWS Backup

> [!tip] Memory Trick
> **STORED = SITE is primary**

---

# Cached vs Stored Volumes

| Feature | Cached Volumes | Stored Volumes |
|---|---|---|
| Primary Data | AWS | On-Premises |
| Local Data | Frequently Accessed Blocks | Entire Dataset |
| Minimize Local Storage | ✅ | ❌ |
| Full Dataset Local | ❌ | ✅ |
| Hybrid Block Storage | ✅ | ✅ |
| Protocol | iSCSI | iSCSI |

---

# Tape Gateway

[[Tape Gateway]]

provides a:

**Virtual Tape Library**

or:

**VTL**

for existing backup applications.

Think:

Existing Backup Software  
↓  
Tape Gateway  
↓  
Virtual Tapes  
↓  
AWS

### Strong Exam Clues

- VTL
- Virtual tape
- Existing tape backup software
- Replace physical tapes
- Long-term backup / archival workflow

### Strong Exam Pattern

> **Keep existing tape-oriented backup software but eliminate physical tape infrastructure**
>
> → **Tape Gateway**

---

# DataSync

[[DataSync]] is for:

**Moving and synchronizing data**

Think:

Source Storage  
↓  
DataSync  
↓  
Destination Storage

Common sources and destinations can include:

- NFS
- SMB
- HDFS
- [[S3]]
- [[EFS]]
- Various [[FSx]] file systems

### Strong Exam Clues

- Migrate
- Move
- Sync
- Scheduled transfer
- Recurring transfer
- Changed files
- Online migration

> [!tip] Memory Trick
> **DataSync = MOVE / SYNC**

---

# Storage Gateway vs DataSync

This is one of the most important distinctions.

## Storage Gateway

Primary idea:

**ACCESS**

An on-premises environment continues interacting with:

**AWS-backed storage**

---

## DataSync

Primary idea:

**MOVE / SYNC**

Data is transferred:

Source  
↓  
Destination

### Killer Exam Question

Ask:

> **Does the application need ongoing hybrid ACCESS, or does the dataset need to MOVE?**

**Ongoing Access**
→ Storage Gateway

**Move / Synchronize**
→ DataSync

---

# AWS Transfer Family

[[AWS Transfer Family]]

provides managed file-transfer endpoints using protocols such as:

- SFTP
- FTPS
- FTP

with storage backends including:

- [[S3]]
- [[EFS]]

### Strong Exam Pattern

> **External business partners upload files through SFTP and the files must land in S3**
>
> → **AWS Transfer Family**

> [!tip] Memory Trick
> **FTP-style protocols → Transfer Family**

---

# Transfer Family Protocols

## SFTP

Uses:

**SSH**

Think:

Secure SSH-based file transfer.

---

## FTPS

Uses:

**TLS**

Think:

FTP secured using SSL/TLS.

---

## FTP

Traditional:

**Unencrypted file transfer**

### Memory Trick

**SFTP = SSH**

**FTPS = TLS**

**FTP = Plain**

---

# DataSync vs Transfer Family

## DataSync

Think:

**Storage-to-storage data movement**

Example:

On-Premises NFS  
↓  
DataSync  
↓  
S3

---

## Transfer Family

Think:

**Users / applications connecting through familiar FTP-style protocols**

Example:

Business Partner  
↓  
SFTP  
↓  
Transfer Family  
↓  
S3

### Exam Decision

**Migrate NFS/SMB storage**
→ DataSync

**Client or partner uses SFTP/FTPS/FTP**
→ Transfer Family

---

# Snow Family

[[Snow Family]] is associated with:

**Physical data-transfer devices and edge computing**

Think:

- Huge dataset
- Insufficient bandwidth
- Offline migration
- Remote / disconnected edge workloads

---

# Snowcone

[[Snowcone]]

Think:

- Small
- Portable
- Rugged
- Remote
- Edge computing
- Smaller datasets

### Strong Clue

> **Smallest / most portable Snow device**
>
> → **Snowcone**

---

# Snowball Edge Storage Optimized

[[Snowball Edge Storage Optimized]]

Think:

- Large offline migration
- Large storage capacity
- Poor bandwidth
- Storage-heavy edge workloads

### Strong Clue

> **Large dataset + network cannot meet migration deadline**
>
> → **Snowball Edge Storage Optimized**

---

# Snowball Edge Compute Optimized

[[Snowball Edge Compute Optimized]]

Think:

- Edge computing
- Video analytics
- ML inference
- Remote processing
- Limited connectivity

### Strong Clue

> **Substantial local compute in a disconnected / remote environment**
>
> → **Snowball Edge Compute Optimized**

---

# Snowmobile

[[Snowmobile]] is:

**Legacy / classic AWS exam knowledge**

Historically it represented:

- Truck-scale migration
- Tens of petabytes
- Approximately 100 PB per Snowmobile
- Entire data-center migrations

> [!warning] Current AWS Context
> AWS stopped accepting new Snowmobile customers in 2024.
>
> Recognize it when reviewing older course material, but treat it as a legacy concept rather than a normal new architecture choice.

---

# DataSync vs Snow Family

## DataSync

Transfer method:

**Network**

Best when:

**Available bandwidth can meet the migration requirement**

---

## Snow Family

Transfer method:

**Physical device**

Best when:

**Network transfer is impractical**

### Exam Decision

Good enough network  
→ DataSync

Huge dataset + network cannot meet deadline  
→ Snow Family

---

# Core Storage Comparison

| Service | Type / Purpose | Strongest Exam Clue |
|---|---|---|
| [[S3]] | Object | Buckets / Objects |
| [[EBS]] | Block | EC2 Persistent Disk |
| [[EFS]] | File | Linux / NFS / Shared |
| [[FSx for Windows File Server]] | File | Windows / SMB |
| [[FSx for Lustre]] | File | HPC / ML |
| [[FSx for NetApp ONTAP]] | File / Block | NetApp / Multi-Protocol |
| [[FSx for OpenZFS]] | File | ZFS / NFS |
| [[S3 File Gateway]] | Hybrid File | NFS/SMB → S3 |
| [[Volume Gateway]] | Hybrid Block | iSCSI Volumes |
| [[Tape Gateway]] | Hybrid Backup | VTL / Virtual Tapes |
| [[DataSync]] | Data Movement | Move / Sync |
| [[AWS Transfer Family]] | Managed Transfer | SFTP / FTPS / FTP |
| [[Snowcone]] | Edge / Transfer | Small / Portable |
| [[Snowball Edge Storage Optimized]] | Offline Transfer / Edge | Large Data |
| [[Snowball Edge Compute Optimized]] | Edge Compute | Heavy Local Processing |

---

# Protocol Decision Table

Protocol alone does NOT always identify the correct service.

Use:

**Protocol + Requirement**

| Protocol / Interface + Requirement | Think |
|---|---|
| S3 API + Objects | S3 |
| Block Storage + EC2 | EBS |
| NFS + Shared Linux File System | EFS |
| SMB + Managed Windows File System | FSx Windows |
| NFS/SMB + S3 Backend | S3 File Gateway |
| iSCSI + Hybrid Volumes | Volume Gateway |
| Virtual Tape / VTL | Tape Gateway |
| SFTP / FTPS / FTP + Managed Endpoint | Transfer Family |
| NFS/SMB + Migrate / Sync | DataSync |
| HPC / Parallel File Processing | FSx for Lustre |
| NFS/SMB/iSCSI + NetApp | FSx for NetApp ONTAP |
| ZFS + NFS | FSx for OpenZFS |

> [!warning] Exam Trap
> **Never choose solely from the protocol.**
>
> Example:
>
> **NFS** could point toward:
>
> - EFS
> - S3 File Gateway
> - DataSync
> - FSx for Lustre
> - FSx for NetApp ONTAP
> - FSx for OpenZFS
>
> The **requirement** chooses the answer.

---

# Location Decision

Another powerful exam technique is asking:

> **Where is the workload?**

---

## Workload Running in AWS

Needs EC2 block storage?

→ [[EBS]]

Needs shared Linux files?

→ [[EFS]]

Needs managed Windows file shares?

→ [[FSx for Windows File Server]]

Needs HPC / ML parallel file storage?

→ [[FSx for Lustre]]

Needs object storage?

→ [[S3]]

Needs NetApp-compatible storage?

→ [[FSx for NetApp ONTAP]]

Needs ZFS-compatible storage?

→ [[FSx for OpenZFS]]

---

## On-Premises Workload

Needs ongoing NFS/SMB access backed by S3?

→ [[S3 File Gateway]]

Needs hybrid iSCSI block storage?

→ [[Volume Gateway]]

Needs virtual tapes?

→ [[Tape Gateway]]

Needs to migrate or synchronize data?

→ [[DataSync]]

---

## External Business Partner

Uses:

- SFTP
- FTPS
- FTP

→ [[AWS Transfer Family]]

---

## Huge Offline Migration

Network cannot meet the migration deadline?

→ [[Snow Family]]

---

# Architecture Thinking

## Scenario 1 — Shared Linux Website Files

Several Linux EC2 instances behind an ALB need access to:

**The same shared files**

**Choose → EFS**

---

## Scenario 2 — EC2 Database Disk

A database running directly on EC2 needs:

**Low-latency persistent block storage**

**Choose → EBS**

---

## Scenario 3 — Static Images

Millions of images require:

- Massive scalability
- High durability
- Object-based access

**Choose → S3**

---

## Scenario 4 — Windows Shared Drive

Windows applications need:

- SMB
- Microsoft Active Directory integration
- Managed Windows file storage

**Choose → FSx for Windows File Server**

---

## Scenario 5 — HPC

Thousands of compute cores need:

**High-performance parallel file access**

**Choose → FSx for Lustre**

---

## Scenario 6 — NetApp Migration

A company uses:

**NetApp ONTAP**

on-premises and wants an AWS-managed equivalent supporting:

- NFS
- SMB
- iSCSI

**Choose → FSx for NetApp ONTAP**

---

## Scenario 7 — ZFS Migration

A company has existing:

**ZFS-based workloads**

that need a managed AWS file system.

**Choose → FSx for OpenZFS**

---

## Scenario 8 — On-Premises NFS to S3

An on-premises application must continue accessing files through:

**NFS**

while the files are stored as:

**S3 objects**

**Choose → S3 File Gateway**

---

## Scenario 9 — Hybrid Block Storage

An on-premises application requires:

**iSCSI block volumes**

integrated with AWS.

**Choose → Volume Gateway**

---

## Scenario 10 — Physical Tape Replacement

Existing backup software expects:

**Tape drives / VTL**

The company wants to eliminate physical tapes.

**Choose → Tape Gateway**

---

## Scenario 11 — Nightly NFS Synchronization

An on-premises NFS server must synchronize changed files into S3:

**Every night**

**Choose → DataSync**

---

## Scenario 12 — Partner SFTP Upload

A business partner uploads files through:

**SFTP**

The files must land in:

[[S3]]

**Choose → AWS Transfer Family**

---

## Scenario 13 — Large Migration + Poor Bandwidth

A company must migrate:

**Hundreds of TB**

but available network bandwidth cannot meet the migration deadline.

**Choose → Snowball Edge Storage Optimized**

---

## Scenario 14 — Remote Video Analytics

A remote site requires:

- Significant local compute
- Video analytics
- Operation with unreliable connectivity

**Choose → Snowball Edge Compute Optimized**

---

## Scenario 15 — Small Remote Edge Device

A remote field team needs:

- Maximum portability
- Rugged hardware
- Local data collection
- Limited connectivity

**Choose → Snowcone**

---

# Common Exam Traps

## Trap 1 — NFS Always Means EFS

False.

Ask what the workload is doing.

**NFS + Shared Linux AWS File System**
→ EFS

**NFS + S3 Backend for On-Premises Application**
→ S3 File Gateway

**NFS + Migrate / Synchronize**
→ DataSync

**HPC + Parallel File System**
→ FSx for Lustre

**NetApp**
→ FSx for NetApp ONTAP

**ZFS**
→ FSx for OpenZFS

---

## Trap 2 — SMB Always Means FSx Windows

False.

**SMB + Managed Windows File System**
→ FSx for Windows File Server

**SMB + S3 Backend**
→ S3 File Gateway

**SMB + Migration / Synchronization**
→ DataSync

**NetApp + SMB**
→ FSx for NetApp ONTAP

---

## Trap 3 — iSCSI Automatically Means Volume Gateway

False.

iSCSI also appears with:

[[FSx for NetApp ONTAP]]

Always identify the:

**Architecture + storage requirement**

Hybrid on-prem block volumes  
→ Volume Gateway

NetApp multi-protocol storage  
→ FSx ONTAP

---

## Trap 4 — Large Dataset Automatically Means Snowball

False.

Ask:

- How much data?
- How much bandwidth?
- What is the deadline?

If the network can satisfy the requirement:

[[DataSync]]

may be better.

If it cannot:

Think:

[[Snow Family]]

---

## Trap 5 — SFTP Means S3 File Gateway

False.

**SFTP**
→ [[AWS Transfer Family]]

S3 File Gateway uses:

**NFS / SMB**

---

## Trap 6 — Storage Gateway Is Primarily a Migration Service

False.

Its major role is:

**Ongoing hybrid storage access**

For migration / synchronization:

→ [[DataSync]]

---

## Trap 7 — File Storage Automatically Means EFS

False.

Ask what type of file storage is required.

Linux / NFS shared storage  
→ EFS

Windows / SMB  
→ FSx Windows

HPC / ML  
→ FSx Lustre

NetApp  
→ FSx ONTAP

ZFS  
→ FSx OpenZFS

---

## Trap 8 — DataSync and Transfer Family Are the Same

False.

DataSync:

**Storage migration / synchronization**

Transfer Family:

**SFTP / FTPS / FTP endpoints**

---

## Trap 9 — Snow Family Is for Ongoing Hybrid Access

False.

Snow:

**Physical migration / edge computing**

Storage Gateway:

**Ongoing hybrid storage**

---

# Five-Question Exam Method

When you see a storage question, ask:

## 1. What Storage Type?

**Object**
→ S3

**Block**
→ EBS / Volume Gateway / FSx ONTAP depending on architecture

**File**
→ EFS / FSx / File Gateway

**Tape**
→ Tape Gateway

---

## 2. Where Is the Workload?

**AWS**

or:

**On-Premises**

On-premises requirements often point toward:

- Storage Gateway
- DataSync
- Transfer Family
- Snow Family

depending on what the workload is doing.

---

## 3. What Protocol or Interface?

Look for:

- NFS
- SMB
- iSCSI
- SFTP
- FTPS
- FTP
- S3 API

Use the protocol to:

**Narrow the choices**

not automatically select the answer.

---

## 4. ACCESS or MOVE?

Need:

**Ongoing storage access?**

→ Storage service / Storage Gateway

Need:

**Migration or synchronization?**

→ DataSync / Snow Family

Need:

**FTP-style file exchange?**

→ Transfer Family

---

## 5. Is the Network Practical?

If:

**Yes**

→ Online transfer may be appropriate

If:

**No**

→ Snow Family may be appropriate

---

# Ultra-Fast Exam Decision Tree

Need storage?  
↓  

Objects?  
→ [[S3]]

EC2 Block Storage?  
→ [[EBS]]

Shared / Specialized Files?  
↓

Linux / NFS  
→ [[EFS]]

Windows / SMB  
→ [[FSx for Windows File Server]]

HPC / ML  
→ [[FSx for Lustre]]

NetApp  
→ [[FSx for NetApp ONTAP]]

ZFS  
→ [[FSx for OpenZFS]]

Hybrid On-Premises Storage?  
↓

NFS / SMB → S3  
→ [[S3 File Gateway]]

iSCSI Volumes  
→ [[Volume Gateway]]

Virtual Tapes  
→ [[Tape Gateway]]

Moving / Exchanging Data?  
↓

SFTP / FTPS / FTP  
→ [[AWS Transfer Family]]

Online Migration / Sync  
→ [[DataSync]]

Huge Dataset + Network Impractical  
→ [[Snow Family]]

---

# Quick Cheat Sheet

| Exam Clue | Answer |
|---|---|
| Objects / Buckets | S3 |
| EC2 Persistent Disk | EBS |
| Linux + Shared NFS | EFS |
| Windows + SMB | FSx Windows |
| HPC / ML File System | FSx Lustre |
| NetApp / ONTAP | FSx ONTAP |
| ZFS | FSx OpenZFS |
| NFS/SMB → S3 | S3 File Gateway |
| Hybrid iSCSI Volumes | Volume Gateway |
| Virtual Tape / VTL | Tape Gateway |
| Move / Sync Data | DataSync |
| SFTP / FTPS / FTP | Transfer Family |
| Huge Data + Network Impractical | Snowball Edge |
| Small Portable Edge Device | Snowcone |
| Heavy Edge Compute | Snowball Edge Compute Optimized |

---

## Master Memory Trick

> [!tip] Master Memory Trick
> Don't memorize AWS storage as one giant list.
>
> Break it into **five jobs**:
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
> **MOVE / EXCHANGE DATA**
> → DataSync / Transfer Family / Snow Family

Then remember:

> **Storage Gateway**
> → ACCESS
>
> **DataSync**
> → MOVE / SYNC
>
> **Transfer Family**
> → SFTP / FTPS / FTP
>
> **Snow Family**
> → PHYSICAL TRANSFER / EDGE

And finally:

> **Protocol narrows the answer.**
>
> **The requirement chooses the answer.**

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

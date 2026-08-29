## What Problem Does It Solve?

[[FSx]] provides fully managed, high-performance file systems on AWS for workloads that need specialized file-system technologies.

It solves the problem of:

> **"How can I use enterprise or high-performance file systems in AWS without managing the underlying file servers myself?"**

The FSx family includes:

- [[FSx for Windows File Server]]
- [[FSx for Lustre]]
- [[FSx for NetApp ONTAP]]
- [[FSx for OpenZFS]]

> [!tip] Memory Trick
> **FSx = Specialized File Systems, Fully Managed**

---

## FSx Overview

The Maarek slides describe FSx as a:

**Fully managed service for third-party high-performance file systems**

Think:

Application Requirement  
↓  
Specific File-System Technology  
↓  
Choose Correct FSx Family

The exam usually gives you a strong clue such as:

- Windows / SMB
- HPC / Lustre
- NetApp / ONTAP
- ZFS / OpenZFS

---

## FSx Family Decision

| Requirement | Best Choice |
|---|---|
| Windows shared file system | [[FSx for Windows File Server]] |
| SMB + NTFS | [[FSx for Windows File Server]] |
| HPC / Machine Learning | [[FSx for Lustre]] |
| Extremely high file-system performance | [[FSx for Lustre]] |
| NetApp migration | [[FSx for NetApp ONTAP]] |
| NFS + SMB + iSCSI | [[FSx for NetApp ONTAP]] |
| Existing ZFS workload | [[FSx for OpenZFS]] |
| NFS-based OpenZFS | [[FSx for OpenZFS]] |

---

## FSx for Windows File Server

[[FSx for Windows File Server]] provides a:

**Fully managed Windows file-system shared drive**

It supports:

- SMB
- Windows NTFS
- Microsoft Active Directory
- ACLs
- User quotas

Architecture:

Windows Applications  
↓  
SMB  
↓  
FSx for Windows File Server

> [!tip] Memory Trick
> **Windows + SMB + NTFS = FSx Windows**

---

## Active Directory Integration

FSx for Windows integrates with:

**Microsoft Active Directory**

This allows familiar Windows authentication and authorization.

Think:

Corporate Users  
↓  
Active Directory  
↓  
SMB Share  
↓  
FSx Windows

### Scenario Recognition

If you see:

- Windows file share
- Active Directory
- SMB
- NTFS

Think:

[[FSx for Windows File Server]]

---

## Linux Can Mount FSx Windows

Important exam detail:

FSx for Windows can also be mounted from:

**Linux EC2 instances**

So do not assume that only Windows EC2 instances can access it.

The key clue is the:

**Windows / SMB file system requirement**

---

## Distributed File System Namespaces

FSx for Windows supports:

**Microsoft Distributed File System Namespaces**

or:

**DFS Namespaces**

This can group files across:

**Multiple file systems**

under a unified namespace.

---

## FSx Windows Performance

The Maarek slides emphasize that FSx Windows can scale to:

- Tens of GB/s
- Millions of IOPS
- Hundreds of PB of data

The important exam takeaway is:

**Enterprise-scale Windows file storage**

---

## FSx Windows Storage Options

Two main storage options:

### SSD

Use for:

**Latency-sensitive workloads**

Examples:

- Databases
- Media processing
- Data analytics

---

### HDD

Use for:

**Broad general-purpose workloads**

Examples:

- Home directories
- Content management systems

### Memory Trick

**SSD = Latency Sensitive**

**HDD = General / Cost-Oriented**

---

## On-Premises Access to FSx Windows

FSx for Windows can be accessed from on-premises through:

- [[05-Networking/Site-to-Site VPN]]
- [[05-Networking/Direct Connect]]

Architecture:

On-Premises  
↓  
VPN / Direct Connect  
↓  
FSx Windows

This makes it useful for:

**Hybrid Windows storage**

---

## FSx Windows High Availability

FSx for Windows can be configured as:

**Multi-AZ**

This provides:

**High availability**

### Exam Pattern

> **Managed Windows file share + Multi-AZ**
>
> → **FSx for Windows File Server**

---

## FSx Windows Backups

FSx for Windows data is:

**Backed up daily to S3**

This is a managed backup capability.

---

# FSx for Lustre

[[FSx for Lustre]] is a:

**Parallel distributed file system**

designed for:

**Large-scale computing**

The name Lustre comes from:

**Linux + Cluster**

> [!tip] Memory Trick
> **Lustre = Linux + Cluster = HPC**

---

## Lustre Use Cases

The Maarek slides explicitly highlight:

- Machine Learning
- High Performance Computing
- Video Processing
- Financial Modeling
- Electronic Design Automation

Whenever the workload requires:

**Extreme parallel file-system performance**

think:

[[FSx for Lustre]]

---

## Lustre Performance

FSx for Lustre can scale to:

- Hundreds of GB/s
- Millions of IOPS
- Sub-millisecond latency

### Memory Trick

**Lustre = Massive Speed**

---

## Lustre Storage Options

FSx for Lustre supports:

### SSD

Use for:

- Low-latency workloads
- IOPS-intensive workloads
- Small file operations
- Random file operations

---

### HDD

Use for:

- Throughput-intensive workloads
- Large file operations
- Sequential file operations

### Memory Trick

**SSD = Small + Random + IOPS**

**HDD = Large + Sequential + Throughput**

---

## Lustre + S3 Integration

One of the biggest Lustre exam features is:

**Seamless integration with S3**

Architecture:

[[S3]]  
↕  
[[FSx for Lustre]]  
↕  
Compute Fleet

FSx for Lustre can:

- Read S3 data through a file-system interface
- Write computation output back to S3

---

## Read S3 as a File System

This is a very strong exam clue.

Dataset Stored in S3  
↓  
FSx for Lustre  
↓  
Application Sees File System  
↓  
HPC / ML Processing

Think:

> **"S3 data needs high-performance file-system access."**

→ **FSx for Lustre**

---

## Write Results Back to S3

Architecture:

S3 Input Dataset  
↓  
Lustre  
↓  
Compute  
↓  
Lustre  
↓  
S3 Output

This makes Lustre a strong companion for:

**Large S3 analytical or HPC datasets**

---

## On-Premises Access to Lustre

FSx for Lustre can also be used from on-premises servers through:

- [[05-Networking/Site-to-Site VPN]]
- [[05-Networking/Direct Connect]]

---

# Lustre Deployment Options

This is a very important section that was missing from the earlier note.

FSx for Lustre has two key deployment models:

1. **Scratch**
2. **Persistent**

---

## Scratch File System

Scratch is designed for:

**Temporary storage**

Characteristics:

- Data is NOT replicated
- Data may be lost if a file server fails
- Very high burst performance
- Lower-cost option
- Designed for short-term processing

The Maarek slides highlight:

**6x higher burst performance**

and approximately:

**200 MB/s per TiB**

### Best Use Cases

- Temporary calculations
- Short-lived HPC jobs
- Data that exists elsewhere
- Cost optimization

> [!tip] Memory Trick
> **Scratch = Fast but Disposable**

---

## Persistent File System

Persistent deployment is designed for:

**Long-term storage and processing**

Characteristics:

- Data is replicated within the same AZ
- Failed file servers are replaced
- Designed for sensitive data
- Better durability than Scratch

### Best Use Cases

- Long-running workloads
- Long-term processing
- Important datasets
- Sensitive data

> [!tip] Memory Trick
> **Persistent = Keep It**

---

## Scratch vs Persistent

| Feature | Scratch | Persistent |
|---|---|---|
| Temporary Storage | ✅ | ❌ |
| Long-Term Storage | ❌ | ✅ |
| Data Replicated | ❌ | ✅ |
| Data Can Be Lost After Failure | ✅ | Much Lower Risk |
| High Burst Performance | ✅ | Not Main Advantage |
| Short-Term Processing | ✅ | ❌ |
| Sensitive / Important Data | ❌ | ✅ |
| Optimize Cost | ✅ | Less Focus |

### Exam Decision

**Temporary HPC data**
→ Scratch

**Important long-term HPC data**
→ Persistent

---

# FSx for NetApp ONTAP

[[FSx for NetApp ONTAP]] provides:

**Managed NetApp ONTAP on AWS**

Use it when migrating or extending:

**NetApp / NAS workloads**

into AWS.

> [!tip] Memory Trick
> **NetApp in the question = ONTAP**

---

## ONTAP Protocols

FSx for NetApp ONTAP supports:

- NFS
- SMB
- iSCSI

This makes it highly flexible for:

**Multi-protocol environments**

Architecture:

Linux  
↓ NFS

Windows  
↓ SMB

Block Storage Workload  
↓ iSCSI

All connect to:

FSx for NetApp ONTAP

---

## ONTAP Platform Support

The Maarek slides highlight compatibility with:

- Linux
- Windows
- macOS
- VMware Cloud on AWS
- WorkSpaces
- AppStream 2.0
- EC2
- ECS
- EKS

This makes ONTAP a strong:

**Enterprise hybrid-storage platform**

---

## ONTAP Auto Scaling

Storage can:

**Shrink or grow automatically**

This is a notable ONTAP characteristic.

---

## ONTAP Storage Features

Important features include:

- Snapshots
- Replication
- Compression
- Data deduplication
- Low-cost storage
- Point-in-time instantaneous cloning

---

## ONTAP Instant Cloning

ONTAP supports:

**Point-in-time instantaneous cloning**

This is particularly useful for:

**Testing new workloads**

Example:

Production Dataset  
↓  
Instant Clone  
↓  
Test Environment

without requiring a slow full data copy.

### Exam Pattern

> **NetApp + Instant Clone + Testing**
>
> → **FSx for NetApp ONTAP**

---

# FSx for OpenZFS

[[FSx for OpenZFS]] provides:

**Managed OpenZFS on AWS**

Use it when moving workloads that currently use:

**ZFS**

into AWS.

> [!tip] Memory Trick
> **ZFS in the question = OpenZFS**

---

## OpenZFS Protocol Support

FSx for OpenZFS supports:

**NFS**

including:

- NFS v3
- NFS v4
- NFS v4.1
- NFS v4.2

This is an important difference from ONTAP's broader protocol support.

---

## OpenZFS Platform Support

The Maarek slides highlight compatibility with:

- Linux
- Windows
- macOS
- VMware Cloud on AWS
- WorkSpaces
- AppStream 2.0
- EC2
- ECS
- EKS

---

## OpenZFS Performance

FSx for OpenZFS can provide:

**Up to 1,000,000 IOPS**

with:

**Less than 0.5 ms latency**

Think:

**Very high-performance NFS / ZFS storage**

---

## OpenZFS Features

Important features include:

- Snapshots
- Compression
- Low-cost storage
- Point-in-time instantaneous cloning

Instant cloning can again be useful for:

**Testing workloads**

---

# ONTAP vs OpenZFS

These can look similar on the exam.

## ONTAP

Strong clue:

**NetApp**

Protocols:

- NFS
- SMB
- iSCSI

---

## OpenZFS

Strong clue:

**ZFS**

Protocol:

**NFS**

### Memory Trick

**NetApp → ONTAP**

**ZFS → OpenZFS**

---

# FSx vs EFS

[[EFS]] and FSx are both managed file-storage services.

## EFS

Think:

**AWS-native shared NFS**

Best for:

- Linux
- Shared file storage
- Elastic capacity
- General workloads

---

## FSx

Think:

**Specialized file-system technology**

Best when the requirement explicitly calls for:

- Windows
- Lustre
- NetApp
- ZFS

### Exam Decision

**Generic Linux NFS**
→ EFS

**Specific file-system requirement**
→ FSx

---

# Architecture Thinking

## Scenario 1 — Windows File Share

A company needs:

- Windows shared storage
- SMB
- NTFS
- Active Directory
- Multi-AZ

**Choose → FSx for Windows File Server**

---

## Scenario 2 — Windows Hybrid Storage

On-premises Windows servers need to access a managed AWS SMB file system through Direct Connect.

**Choose → FSx for Windows File Server**

---

## Scenario 3 — Machine Learning

A machine-learning cluster needs:

- Massive throughput
- Millions of IOPS
- S3 dataset integration

**Choose → FSx for Lustre**

---

## Scenario 4 — Temporary HPC Job

An HPC workload processes temporary data.

The source data already exists in S3.

Maximum burst performance and lower cost matter more than durability.

**Choose → Lustre Scratch**

---

## Scenario 5 — Important HPC Dataset

A long-running HPC workload requires Lustre performance but cannot tolerate losing its working dataset after a file-server failure.

**Choose → Lustre Persistent**

---

## Scenario 6 — NetApp Migration

An enterprise uses NetApp ONTAP on-premises.

It needs:

- NFS
- SMB
- iSCSI
- Snapshots
- Deduplication

**Choose → FSx for NetApp ONTAP**

---

## Scenario 7 — Testing with Instant Clone

A company needs rapid clones of its NetApp production dataset for testing.

**Choose → FSx for NetApp ONTAP**

---

## Scenario 8 — ZFS Migration

A company wants to move an existing ZFS workload into AWS.

**Choose → FSx for OpenZFS**

---

## Scenario 9 — High-Performance NFS

A ZFS application requires:

- NFS
- Extremely high IOPS
- Sub-millisecond latency

**Choose → FSx for OpenZFS**

---

# Scenario Recognition

## Immediately Think FSx Windows When You See

- Windows
- SMB
- NTFS
- Active Directory
- ACLs
- User quotas
- DFS Namespace
- Windows share drive

---

## Immediately Think Lustre When You See

- HPC
- Machine learning
- Linux + cluster
- S3 integration
- Parallel file system
- Hundreds of GB/s
- Millions of IOPS
- Video processing
- Financial modeling

---

## Immediately Think Lustre Scratch When You See

- Temporary data
- Short-term processing
- Maximum burst
- Cost optimization
- Data already exists elsewhere

---

## Immediately Think Lustre Persistent When You See

- Long-term processing
- Important data
- Sensitive data
- Replication required

---

## Immediately Think ONTAP When You See

- NetApp
- ONTAP
- NAS
- NFS + SMB + iSCSI
- Deduplication
- Instant cloning
- Enterprise storage

---

## Immediately Think OpenZFS When You See

- ZFS
- OpenZFS
- NFS
- High IOPS
- Instant cloning
- ZFS migration

---

# Exam Traps

## Trap 1 — FSx Is One File System

False.

FSx is a:

**Family of managed file systems**

---

## Trap 2 — FSx Windows Is SMB Only From Windows Clients

False.

It can also be mounted from:

**Linux EC2 instances**

---

## Trap 3 — FSx Windows Has No HA Option

False.

It can be configured:

**Multi-AZ**

---

## Trap 4 — Lustre Is Best for Ordinary Shared Linux Storage

Usually not.

For general-purpose Linux NFS:

Think:

[[EFS]]

For:

**HPC / extreme performance**

think:

[[FSx for Lustre]]

---

## Trap 5 — Lustre Scratch Replicates Data

False.

Scratch:

**Does not replicate the data**

and is designed for temporary workloads.

---

## Trap 6 — Lustre Persistent Is Multi-AZ Replication

Be careful.

The Maarek slides specify:

**Replication within the same AZ**

for the persistent deployment.

---

## Trap 7 — Lustre Cannot Use S3

False.

S3 integration is one of Lustre's biggest features.

---

## Trap 8 — ONTAP Uses Only NFS

False.

ONTAP supports:

- NFS
- SMB
- iSCSI

---

## Trap 9 — OpenZFS Supports SMB and iSCSI Like ONTAP

Not according to the key Maarek distinction.

OpenZFS is highlighted around:

**NFS**

while ONTAP provides:

**NFS + SMB + iSCSI**

---

## Trap 10 — ONTAP and OpenZFS Are the Same

False.

**NetApp workload**
→ ONTAP

**ZFS workload**
→ OpenZFS

---

# Quick Cheat Sheet

| Exam Clue | Best Choice |
|---|---|
| Windows Share | FSx Windows |
| SMB | FSx Windows |
| NTFS | FSx Windows |
| Active Directory | FSx Windows |
| DFS Namespace | FSx Windows |
| Multi-AZ Windows Storage | FSx Windows |
| HPC | FSx Lustre |
| Machine Learning | FSx Lustre |
| S3 as File System | FSx Lustre |
| Temporary HPC | Lustre Scratch |
| Long-Term HPC | Lustre Persistent |
| NetApp | FSx ONTAP |
| NFS + SMB + iSCSI | FSx ONTAP |
| Deduplication | FSx ONTAP |
| NetApp Instant Clone | FSx ONTAP |
| ZFS | FSx OpenZFS |
| High-Performance NFS | FSx OpenZFS |
| Generic Linux NFS | EFS |

---

## Master Memory Trick

> [!tip] Master Memory Trick
> **FSx = Listen for the file-system keyword**
>
> **WINDOWS**
>
> → SMB + NTFS + AD
>
> → FSx Windows
>
> **LUSTRE**
>
> → Linux + Cluster
>
> → HPC / ML
>
> **NETAPP**
>
> → NFS + SMB + iSCSI
>
> → ONTAP
>
> **ZFS**
>
> → NFS
>
> → OpenZFS

Then for Lustre:

> **SCRATCH**
>
> → Temporary + Fast + Disposable
>
> **PERSISTENT**
>
> → Long-Term + Replicated

And the killer exam clues:

**Windows + SMB**
→ FSx Windows

**HPC + S3**
→ FSx Lustre

**NetApp**
→ FSx ONTAP

**ZFS**
→ FSx OpenZFS

---

## Related Notes

- [[FSx for Windows File Server]]
- [[FSx for Lustre]]
- [[FSx for NetApp ONTAP]]
- [[FSx for OpenZFS]]
- [[EFS]]
- [[S3]]
- [[EC2]]
- [[02-Compute/ECS]]
- [[02-Compute/EKS]]
- [[05-Networking/Direct Connect]]
- [[05-Networking/Site-to-Site VPN]]
- [[Active Directory]]
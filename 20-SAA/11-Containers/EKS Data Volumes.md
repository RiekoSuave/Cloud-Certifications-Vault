## Why This Matters

Containers and Kubernetes pods should generally be treated as:

**Ephemeral**

If a pod is:

- Restarted
- Rescheduled
- Replaced
- Moved to another node

data stored only inside that pod may be:

**Lost**

For persistent application data, EKS integrates with AWS storage services such as:

- [[EBS]]
- [[EFS]]
- [[FSx]]

> [!tip] Master Memory Trick
> **POD = Temporary**
>
> **PERSISTENT DATA = External Storage**

---

## Kubernetes Storage Model

Kubernetes separates:

**Application lifecycle**

from:

**Storage lifecycle**

Think:

Pod  
↓  
Persistent Volume Claim  
↓  
Persistent Volume  
↓  
AWS Storage

Important Kubernetes concepts:

- PersistentVolume
- PersistentVolumeClaim
- StorageClass
- CSI Driver

For SAA, you do not need every Kubernetes detail.

You mainly need to recognize:

> **Which AWS storage service best fits the workload?**

---

## PersistentVolume

A:

**PersistentVolume**

represents:

**Persistent storage available to the Kubernetes cluster**

It exists independently of:

**An individual pod**

This lets data survive:

**Pod replacement**

---

## PersistentVolumeClaim

A:

**PersistentVolumeClaim — PVC**

is a pod's request for:

**Persistent storage**

Think:

Pod  
↓  
PVC  
↓  
Persistent Volume  
↓  
AWS Storage

### Memory Trick

**PV = Storage**

**PVC = Request for Storage**

---

## StorageClass

A:

**StorageClass**

defines:

**How storage should be dynamically provisioned**

Conceptually:

PVC  
↓  
StorageClass  
↓  
AWS Storage Created

This allows Kubernetes to create storage:

**On demand**

instead of administrators manually creating every volume.

---

## CSI Drivers

Kubernetes uses:

**Container Storage Interface — CSI**

drivers to integrate with external storage systems.

Important AWS examples include:

- Amazon EBS CSI Driver
- Amazon EFS CSI Driver

Think:

Kubernetes  
↓  
CSI Driver  
↓  
AWS Storage Service

### Memory Trick

**CSI = Kubernetes storage connector**

---

# EBS with EKS

[[EBS]] provides:

**Persistent block storage**

for Kubernetes workloads.

Architecture:

Pod  
↓  
PVC  
↓  
EBS Persistent Volume  
↓  
EBS Volume

Use EBS when the workload needs:

- Block storage
- Low-latency storage
- Database-style storage
- Persistent disk attached to a workload

### Killer Exam Clue

> **Kubernetes workload requires persistent block storage**
>
> → **EBS**

---

## EBS Is Availability-Zone Scoped

This is extremely important.

An EBS volume exists in:

**One Availability Zone**

Example:

EBS Volume  
→ us-east-1a

A pod using that volume generally needs compute in:

**The same AZ**

### Exam Trap

> **EBS is NOT a Regional shared file system**

That role is more closely associated with:

[[EFS]]

---

## EBS + Pod Scheduling

Suppose:

EBS Volume  
↓  
AZ-A

Pod needs that volume.

The scheduler must place the workload where:

**The volume can be attached**

If the pod moves to:

**Another AZ**

the same EBS volume cannot simply attach across AZs.

### Memory Trick

**EBS = One AZ**

---

## EBS Use Cases

Think EBS for:

- Stateful application
- Database pod
- Persistent single-workload disk
- Low-latency block storage
- Filesystem mounted by one workload

---

## EBS Access Pattern

EBS behaves like:

**A disk**

rather than:

**A shared network file system**

This is why it is best associated with:

**Block storage requirements**

---

# EFS with EKS

[[EFS]] provides:

**Shared NFS file storage**

for EKS.

Architecture:

Pod A  
↓  

Pod B  
↓  

Pod C  
↓  

EFS

Multiple pods can access:

**The same file system**

### Killer Exam Clue

> **Multiple Kubernetes pods need shared persistent files**
>
> → **EFS**

---

## EFS Is Regional

Unlike EBS:

EFS can provide a:

**Regional shared file system**

across:

**Multiple Availability Zones**

Architecture:

AZ-A Pods  
↓  

EFS

AZ-B Pods  
↑  

This makes EFS particularly useful for:

**Multi-AZ shared storage**

---

## EFS Use Cases

Think EFS for:

- Shared files
- NFS
- Multiple pods
- Multi-AZ access
- Content repositories
- Shared application assets
- Shared configuration files

### Memory Trick

**EFS = Everyone Files Share**

---

## EBS vs EFS

This is the biggest storage distinction.

### EBS

Think:

**Block Disk**

- One AZ
- Low latency
- Persistent disk
- Stateful workload

### EFS

Think:

**Shared File System**

- NFS
- Multi-AZ
- Multiple pods
- Shared files

---

## EBS vs EFS Quick Comparison

| Requirement | EBS | EFS |
|---|---:|---:|
| Block Storage | ✅ | ❌ |
| Shared File System | ❌ | ✅ |
| NFS | ❌ | ✅ |
| Single-AZ Scope | ✅ | ❌ |
| Regional Multi-AZ | ❌ | ✅ |
| Database Disk | ✅ | Possible but not typical |
| Multiple Pods Share Files | Limited | ✅ |
| Low-Latency Block Device | ✅ | ❌ |

### Memory Trick

**EBS = BLOCK**

**EFS = SHARE**

---

# EKS + FSx

[[FSx]] can also be relevant when Kubernetes workloads need:

**Specialized file systems**

Examples include:

- [[FSx for Lustre]]
- [[FSx for NetApp ONTAP]]
- [[FSx for OpenZFS]]

Think:

EKS  
↓  
Specialized Storage Requirement  
↓  
FSx

---

## FSx for Lustre

[[FSx for Lustre]]

Think:

- HPC
- Machine learning
- High throughput
- Parallel file system

### Killer Exam Clue

> **Kubernetes-based HPC workload needs high-performance parallel storage**
>
> → **FSx for Lustre**

---

## FSx for NetApp ONTAP

[[FSx for NetApp ONTAP]]

Think:

- NetApp
- Enterprise NAS
- NFS
- SMB
- iSCSI
- Multi-protocol access

### Killer Exam Clue

> **EKS workload requires NetApp-compatible storage**
>
> → **FSx for NetApp ONTAP**

---

## FSx for OpenZFS

[[FSx for OpenZFS]]

Think:

- ZFS
- NFS
- Existing ZFS workloads
- Snapshots / clones

---

# Ephemeral Storage

Pods also have:

**Ephemeral local storage**

This is useful for:

- Temporary files
- Cache
- Scratch space
- Intermediate processing

Do NOT use ephemeral storage for:

**Critical persistent data**

### Memory Trick

**Ephemeral = Okay to lose**

---

## Pod Replacement

Suppose:

Pod A  
↓  
Writes Important Data Locally  
↓  
Pod Fails  
↓  
Replacement Pod B Starts

If the data only existed inside:

**Pod A**

it may be:

**Gone**

Better:

Pod  
↓  
Persistent External Storage

---

# Stateful vs Stateless

Scalable Kubernetes applications generally work best when:

**Pods are stateless**

State should live in:

- EBS
- EFS
- FSx
- S3
- RDS
- DynamoDB
- ElastiCache

depending on the application.

### SAA Principle

> **Keep compute replaceable and state external**

---

# EKS + S3

[[S3]] is:

**Object storage**

not:

**A mounted block disk**

or:

**Traditional shared NFS filesystem**

Use S3 when the application needs:

- Objects
- Data lake storage
- Static content
- Backups
- Large-scale durable object storage

### Exam Trap

Do not choose S3 simply because:

**The application needs persistent storage**

First identify:

**Object vs Block vs File**

---

# EKS + RDS

For relational application state:

Use:

[[RDS]]

rather than storing the entire database inside a pod unless the architecture specifically requires Kubernetes-managed stateful databases.

Typical architecture:

Pods  
↓  
RDS

This keeps:

**Database persistence outside the container platform**

---

# EKS + DynamoDB

For serverless NoSQL state:

Pods  
↓  
DynamoDB

This allows Kubernetes compute to remain:

**Stateless**

while DynamoDB handles:

**Durable application data**

---

# Storage and Availability Zones

This is a major SAA exam concept.

## EBS

Scoped to:

**One AZ**

## EFS

Designed for:

**Regional shared access across AZs**

### Killer Exam Decision

Need:

**One persistent disk**
→ EBS

Need:

**Multiple pods across AZs sharing files**
→ EFS

---

# Storage and Fargate

EKS workloads running on:

[[Fargate]]

do not have customer-managed worker-node disks.

For persistent shared storage:

Think:

**EFS**

depending on the workload.

Fargate is particularly aligned with:

**Externalized persistent storage**

because pods should remain:

**Disposable**

---

# Dynamic Provisioning

Kubernetes can dynamically provision storage.

Conceptually:

Pod Needs Storage  
↓  
PVC  
↓  
StorageClass  
↓  
CSI Driver  
↓  
AWS Creates Storage

This reduces:

**Manual storage administration**

---

# Volume Expansion

Persistent storage may sometimes need:

**More capacity**

Depending on the storage class and driver configuration, Kubernetes can support:

**Volume expansion**

For SAA, the broader concept matters more:

> **Persistent volumes can be managed independently of pod lifecycle**

---

# Snapshots and Backups

Persistent storage should still have:

**Backup and recovery plans**

Examples:

EBS  
→ EBS Snapshots

EFS  
→ AWS Backup

FSx  
→ Service-specific backup features

### SAA Principle

> **Persistent does not automatically mean protected from deletion or corruption**

---

# EBS Snapshot Architecture

EBS Volume  
↓  
Snapshot  
↓  
Recovery / New Volume

Useful for:

- Backup
- Recovery
- Cloning
- Migration

---

# Storage Performance

Storage selection should consider:

- Latency
- Throughput
- IOPS
- Sharing requirements
- AZ scope
- Protocol

Do NOT select storage based only on:

**Persistence**

---

# Architecture Thinking

## Scenario 1 — Database Pod

A Kubernetes database workload needs:

**Low-latency persistent block storage**

Choose:

[[EBS]]

---

## Scenario 2 — Shared Web Content

Multiple pods across multiple AZs need:

**The same shared files**

Choose:

[[EFS]]

---

## Scenario 3 — HPC Kubernetes Workload

EKS-based machine learning workload requires:

**High-performance parallel file access**

Choose:

[[FSx for Lustre]]

---

## Scenario 4 — Pod Replaced

Application stores uploads only inside:

**Local pod storage**

Pod gets replaced and uploads disappear.

Fix:

Use:

**Persistent external storage**

such as EFS, EBS, or S3 depending on access pattern.

---

## Scenario 5 — Multi-AZ Shared Storage

Pods in AZ-A and AZ-B must access:

**The same filesystem**

Do NOT choose:

EBS

Choose:

**EFS**

---

## Scenario 6 — Single-AZ Stateful Workload

One stateful workload needs:

**Dedicated persistent block storage**

Choose:

**EBS**

---

## Scenario 7 — Object Storage

Application stores:

- Images
- Backups
- Large immutable files

Choose:

[[S3]]

rather than EBS/EFS if object semantics are appropriate.

---

## Scenario 8 — Existing NetApp Workload

Kubernetes application requires:

- NFS
- SMB
- iSCSI
- NetApp semantics

Choose:

[[FSx for NetApp ONTAP]]

---

# Scenario Recognition

Immediately think:

**EBS**

when you see:

- Block storage
- Database disk
- PersistentVolume
- One-AZ storage
- Low-latency disk

Immediately think:

**EFS**

when you see:

- Shared files
- NFS
- Multiple pods
- Multi-AZ
- Regional file system

Immediately think:

**FSx**

when you see:

- HPC
- NetApp
- ZFS
- Specialized file system

---

# Exam Traps

## Trap 1 — Pod Local Storage Is Persistent

False.

Pods are:

**Replaceable**

Critical data should live externally.

---

## Trap 2 — EBS Can Be Mounted Across Multiple AZs

False.

EBS is:

**AZ-scoped**

---

## Trap 3 — EFS Is Block Storage

False.

EFS is:

**Shared NFS file storage**

---

## Trap 4 — EBS and EFS Are Interchangeable

False.

EBS:

**Block**

EFS:

**Shared File**

---

## Trap 5 — PersistentVolume Means the Data Is Automatically Backed Up

False.

Persistence and:

**Backup**

are separate concerns.

---

## Trap 6 — Every Persistent Kubernetes Workload Should Use EBS

False.

Ask whether the workload needs:

- Block
- Shared File
- Object
- Specialized File System

---

## Trap 7 — S3 Is a Drop-In Replacement for EBS

False.

S3 is:

**Object storage**

not:

**Block storage**

---

## Trap 8 — Multi-AZ Shared Files Point to EBS

False.

Think:

**EFS**

---

# Quick Cheat Sheet

| Exam Clue | Best Choice |
|---|---|
| Persistent Block Storage | EBS |
| Single-AZ Persistent Disk | EBS |
| Database Pod Disk | EBS |
| Shared NFS Files | EFS |
| Multiple Pods Share Files | EFS |
| Multi-AZ Shared File System | EFS |
| HPC Parallel File System | FSx for Lustre |
| NetApp Workload | FSx ONTAP |
| ZFS Workload | FSx OpenZFS |
| Object Storage | S3 |
| Temporary Scratch Storage | Ephemeral Storage |
| Dynamic Storage Provisioning | StorageClass + CSI |
| Pod Storage Request | PVC |

---

# Storage Decision Table

| Requirement | Answer |
|---|---|
| Block | EBS |
| Shared File | EFS |
| Object | S3 |
| HPC | FSx Lustre |
| NetApp | FSx ONTAP |
| ZFS | FSx OpenZFS |

---

# Kubernetes Storage Shortcut

> **POD ASKS**
> → PVC
>
> **CLUSTER PROVIDES**
> → PV
>
> **HOW TO CREATE STORAGE**
> → StorageClass
>
> **AWS CONNECTION**
> → CSI Driver
>
> **BLOCK**
> → EBS
>
> **SHARED FILE**
> → EFS

---

# Final Exam Rapid-Fire

> **PERSISTENT BLOCK**
> → EBS
>
> **SHARED NFS**
> → EFS
>
> **MULTI-AZ SHARED FILES**
> → EFS
>
> **ONE-AZ DISK**
> → EBS
>
> **HPC**
> → FSx LUSTRE
>
> **NETAPP**
> → FSx ONTAP
>
> **OBJECTS**
> → S3
>
> **TEMPORARY POD DATA**
> → EPHEMERAL STORAGE
>
> **POD REQUESTS STORAGE**
> → PVC
>
> **DYNAMIC PROVISIONING**
> → STORAGECLASS + CSI

---

## Master Memory Trick

> [!tip] EKS Data Volumes Master Memory Trick
> Imagine pods are hotel guests.
>
> The pod's local disk is:
>
> **The hotel room desk**
>
> When the guest leaves:
>
> **Don't expect anything left on the desk to survive.**
>
> For important data, use external storage.
>
> **EBS**
> → Private storage locker in one building
>
> **EFS**
> → Shared filing room accessible across buildings
>
> **S3**
> → Massive object warehouse
>
> **FSx**
> → Specialized storage facility

So remember:

> **EBS = BLOCK + ONE AZ**
>
> **EFS = FILE + SHARED + MULTI-AZ**
>
> **S3 = OBJECT**
>
> **FSx = SPECIALIZED**
>
> **POD LOCAL STORAGE = TEMPORARY**

And the killer SAA question:

> **"Does this Kubernetes workload need a private disk or a shared filesystem?"**

Private block disk  
→ **EBS**

Shared filesystem  
→ **EFS**

---

## Related Notes

- [[EKS]]
- [[EKS Node Types]]
- [[EBS]]
- [[EFS]]
- [[FSx]]
- [[FSx for Lustre]]
- [[FSx for NetApp ONTAP]]
- [[FSx for OpenZFS]]
- [[S3]]
- [[Fargate]]
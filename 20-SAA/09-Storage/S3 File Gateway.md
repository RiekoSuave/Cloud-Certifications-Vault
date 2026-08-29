## What Problem Does It Solve?

[[S3 File Gateway]] allows on-premises applications to access:

**Amazon S3**

using familiar file-system protocols.

It solves the problem of:

> **"My applications use normal file shares, but I want the underlying data stored as objects in S3."**

Architecture:

On-Premises Application  
↓  
NFS / SMB  
↓  
S3 File Gateway  
↓  
[[S3]]

> [!tip] Memory Trick
> **S3 File Gateway = File interface in front, S3 objects in back**

---

## What Is S3 File Gateway?

S3 File Gateway provides a bridge between:

**Traditional File Storage**

and:

**S3 Object Storage**

Applications interact with:

**Files and directories**

using:

- NFS
- SMB

The gateway stores those files as:

**Objects in S3**

---

# Supported Protocols

S3 File Gateway supports:

- NFS
- SMB

### NFS

Typically associated with:

- Linux
- Unix
- On-premises applications

Architecture:

Linux Application  
↓  
NFS  
↓  
S3 File Gateway  
↓  
S3

---

### SMB

Typically associated with:

**Windows file-sharing environments**

Architecture:

Windows Application  
↓  
SMB  
↓  
S3 File Gateway  
↓  
S3

### Memory Trick

**NFS / SMB in front**

**S3 behind**

---

# Files Become S3 Objects

One of the most important concepts:

Files written through the gateway become:

**S3 Objects**

Example:

On-Premises:

`reports/august.pdf`

↓  
S3 File Gateway  
↓

S3:

`reports/august.pdf`

The application can continue working with:

**Files**

without being redesigned to directly use:

**S3 APIs**

---

# S3 Object Mapping

Conceptually:

File Path  
↓  
Object Key

File Data  
↓  
Object Data

File Metadata  
↓  
Object Metadata

This allows traditional applications to interact with S3 through:

**File protocols**

---

# S3 Storage Classes

S3 File Gateway supports storage in:

- S3 Standard
- S3 Standard-IA
- S3 One Zone-IA
- S3 Intelligent-Tiering

> [!tip] Exam Detail
> Think:
>
> **S3 File Gateway → S3 storage classes**

This allows organizations to choose storage based on:

- Access frequency
- Resilience requirements
- Cost

---

# Glacier Through Lifecycle Policies

S3 File Gateway does not directly use:

**S3 Glacier storage classes**

for active file access.

Instead, use:

[[S3 Lifecycle Rules]]

Architecture:

S3 File Gateway  
↓  
S3 Object  
↓  
Lifecycle Policy  
↓  
Glacier Storage Class

### Memory Trick

**Gateway → S3 → Lifecycle → Glacier**

---

# Local Cache

S3 File Gateway maintains a:

**Local Cache**

for recently used data.

Architecture:

Application  
↓  
Gateway  
├── Local Cache
└── S3

The cache provides:

**Low-latency access to recently used files**

while the durable data resides in:

**S3**

---

# Why Local Cache Matters

Without caching:

Application  
↓  
Network  
↓  
AWS  
↓  
Retrieve Every File

With caching:

Application  
↓  
Gateway  
↓  
Recently Used File Found Locally

This reduces:

- Latency
- Repeated network retrieval
- Dependence on WAN performance for frequently accessed data

> [!tip] Memory Trick
> **Hot files stay close**

---

# S3 Is the Backend

An important architecture point:

The gateway itself is not the durable cloud storage destination.

The durable backend is:

[[S3]]

Think:

Gateway  
= Bridge + Cache

S3  
= Cloud Storage

---

# SMB Authentication

For SMB access, S3 File Gateway can integrate with:

**Microsoft Active Directory**

This allows Windows environments to use:

**Enterprise authentication**

Architecture:

Windows User  
↓  
Active Directory  
↓  
SMB  
↓  
S3 File Gateway  
↓  
S3

---

# Guest Access

S3 File Gateway can also support:

**Guest access**

for SMB environments.

The exact architecture depends on:

**Authentication requirements**

### Exam Thinking

Enterprise Windows authentication  
→ Active Directory

Simpler SMB access requirement  
→ Guest access may be relevant

---

# IAM Roles

S3 File Gateway uses:

**IAM Roles**

to access:

[[S3]]

Architecture:

Application  
↓  
Gateway  
↓  
IAM Role  
↓  
S3 Bucket

The IAM role determines:

**What S3 resources the gateway can access**

---

# S3 File Gateway Architecture

A typical architecture:

On-Premises Users  
↓  
NFS / SMB  
↓  
S3 File Gateway  
├── Local Cache
↓
IAM Role  
↓  
S3 Bucket

This combines:

**Local file access**

with:

**AWS object storage**

---

# Why Use S3 File Gateway?

Use it when an application:

**Cannot or should not be rewritten to use S3 APIs**

but the organization still wants:

- S3 durability
- S3 scalability
- S3 storage classes
- Cloud-based storage
- Hybrid architecture

The application keeps using:

**NFS / SMB**

---

# Hybrid Cloud Use Case

Example:

Legacy File Application  
↓  
NFS  
↓  
S3 File Gateway  
↓  
S3

The legacy application continues behaving as if it is accessing:

**A traditional file share**

while AWS stores the data as:

**Objects**

---

# S3 File Gateway vs Direct S3 Access

## Direct S3

Application uses:

- S3 API
- AWS SDK
- HTTP

Best for:

**Cloud-native applications**

---

## S3 File Gateway

Application uses:

- NFS
- SMB

Best for:

**Traditional file-based applications**

### Memory Trick

**Cloud-native → S3 API**

**Legacy file app → File Gateway**

---

# S3 File Gateway vs EFS

These both involve file access but solve different problems.

## [[EFS]]

Provides:

**Native managed NFS file storage**

The backend itself is:

**A file system**

---

## S3 File Gateway

Provides:

**File interface to S3**

The backend is:

**Object storage**

### Exam Decision

Need an AWS-native shared NFS file system  
→ EFS

Need on-premises NFS/SMB access to S3 objects  
→ S3 File Gateway

---

# S3 File Gateway vs FSx File Gateway

## S3 File Gateway

Backend:

[[S3]]

Protocols:

- NFS
- SMB

Data becomes:

**S3 Objects**

---

## [[FSx File Gateway]]

Backend:

[[FSx for Windows File Server]]

Protocol:

**SMB**

Best for:

**Hybrid Windows file shares**

### Memory Trick

**S3 File Gateway → S3**

**FSx File Gateway → FSx Windows**

---

# S3 File Gateway vs Volume Gateway

## S3 File Gateway

Provides:

**File storage interface**

Protocols:

- NFS
- SMB

Backend:

S3

---

## [[Volume Gateway]]

Provides:

**Block storage interface**

Protocol:

**iSCSI**

### Exam Decision

**Files**
→ S3 File Gateway

**Blocks**
→ Volume Gateway

---

# S3 File Gateway vs DataSync

## S3 File Gateway

Provides:

**Ongoing access**

Architecture:

Application  
↕  
Gateway  
↕  
S3

---

## [[DataSync]]

Provides:

**Data movement**

Architecture:

Source  
↓  
Transfer  
↓  
Destination

### Memory Trick

**Gateway = ACCESS**

**DataSync = MOVE**

---

# S3 File Gateway vs Snowball

## [[Snowball]]

Best for:

**Massive offline migration**

---

## S3 File Gateway

Best for:

**Ongoing hybrid file access**

### Exam Decision

500 TB one-time migration over terrible network  
→ Snowball

On-prem application continuously needs NFS access to S3  
→ S3 File Gateway

---

# Architecture Thinking

## Scenario 1 — Linux Application to S3

An on-premises Linux application requires:

**NFS**

but the company wants the files stored in:

**S3**

**Choose → S3 File Gateway**

---

## Scenario 2 — Windows File Share to S3

Windows users need:

**SMB**

The backend must be:

**S3**

**Choose → S3 File Gateway**

---

## Scenario 3 — Existing Application Cannot Use S3 API

A legacy application only understands:

**NFS**

The company wants S3 storage without modifying the application.

**Choose → S3 File Gateway**

---

## Scenario 4 — Frequently Accessed Files Need Low Latency

An on-premises application stores files in S3 but frequently accesses the same files.

**Choose → S3 File Gateway**

because it provides:

**Local caching**

---

## Scenario 5 — Windows Authentication

Corporate Windows users access the gateway through SMB.

Authentication should use the organization's existing directory.

**Choose:**

S3 File Gateway  
+  
Microsoft Active Directory

---

## Scenario 6 — Archive Old Gateway Files

Files written through S3 File Gateway eventually need cheap archival storage.

Architecture:

S3 File Gateway  
↓  
S3  
↓  
[[S3 Lifecycle Rules]]  
↓  
Glacier

---

## Scenario 7 — Cloud-Native Application

A new application can directly use:

**S3 APIs**

There is no file-protocol requirement.

Do NOT add S3 File Gateway unnecessarily.

Use:

[[S3]]

directly.

---

# Scenario Recognition

Immediately think:

[[S3 File Gateway]]

when you see:

- On-premises
- Hybrid storage
- NFS
- SMB
- S3 backend
- Files become S3 objects
- Local cache
- Legacy file application
- Active Directory + SMB + S3

### Strongest Exam Pattern

> **"On-premises applications need NFS or SMB access while the files are stored as objects in S3."**
>
> → **S3 File Gateway**

---

# Exam Traps

## Trap 1 — S3 File Gateway Is a Native File System in S3

False.

S3 remains:

**Object storage**

The gateway provides:

**A file interface**

---

## Trap 2 — Applications Must Use the S3 API

False.

They use:

- NFS
- SMB

---

## Trap 3 — S3 File Gateway Stores the Only Copy in Its Local Cache

False.

The cache is for:

**Low-latency access**

The cloud backend is:

**S3**

---

## Trap 4 — S3 File Gateway Is Block Storage

False.

For block storage:

[[Volume Gateway]]

---

## Trap 5 — S3 File Gateway Backend Is FSx Windows

False.

That describes:

[[FSx File Gateway]]

S3 File Gateway backend:

**S3**

---

## Trap 6 — S3 File Gateway Is Best for a One-Time Petabyte Migration

Not usually.

Think:

[[Snowball]]

for massive offline migration.

---

## Trap 7 — Glacier Should Be Used as the Active Gateway Storage Class

Think instead:

S3 File Gateway  
↓  
S3  
↓  
Lifecycle  
↓  
Glacier

---

# Quick Cheat Sheet

| Requirement | S3 File Gateway |
|---|---|
| Hybrid File Storage | ✅ |
| NFS | ✅ |
| SMB | ✅ |
| Backend = S3 | ✅ |
| Files Become S3 Objects | ✅ |
| Local Cache | ✅ |
| Active Directory for SMB | ✅ |
| IAM Role to Access S3 | ✅ |
| S3 Standard | ✅ |
| Standard-IA | ✅ |
| One Zone-IA | ✅ |
| Intelligent-Tiering | ✅ |
| Archive via Lifecycle | ✅ |
| Block Storage | ❌ |
| iSCSI | ❌ |
| Backend = FSx Windows | ❌ |

---

## Master Memory Trick

> [!tip] Master Memory Trick
> Imagine a translator standing between your old application and S3.
>
> Application says:
>
> **"Give me NFS or SMB."**
>
> Gateway says:
>
> **"Sure."**
>
> Then Gateway turns around to AWS and stores:
>
> **S3 Objects**

So remember:

> **FRONT**
>
> → NFS / SMB
>
> **MIDDLE**
>
> → S3 File Gateway + Local Cache
>
> **BACK**
>
> → S3 Objects

And the killer exam clue:

> **NFS / SMB + ON-PREMISES + S3**
>
> → **S3 File Gateway**

---

## Related Notes

- [[Storage Gateway]]
- [[FSx File Gateway]]
- [[Volume Gateway]]
- [[Tape Gateway]]
- [[S3]]
- [[S3 Lifecycle Rules]]
- [[EFS]]
- [[DataSync]]
- [[Snowball]]
- [[IAM]]
## What Problem Does It Solve?

[[FSx File Gateway]] provides on-premises users and applications with access to:

[[FSx for Windows File Server]]

while maintaining a:

**Local cache**

for frequently accessed files.

It solves the problem of:

> **"How can my on-premises Windows users access an FSx for Windows file system in AWS with low-latency access to frequently used files?"**

Architecture:

On-Premises Windows Users  
↓  
SMB  
↓  
FSx File Gateway  
↓  
Local Cache  
↓  
[[FSx for Windows File Server]]

> [!tip] Memory Trick
> **FSx File Gateway = Local doorway to FSx Windows**

---

## What Is FSx File Gateway?

FSx File Gateway provides:

**Native access to Amazon FSx for Windows File Server**

from:

**On-Premises Environments**

It is designed for:

**Hybrid Windows file-storage architectures**

Think:

On-Premises  
↕  
FSx File Gateway  
↕  
FSx Windows in AWS

---

# SMB Protocol

FSx File Gateway provides access through:

**SMB**

or:

**Server Message Block**

Architecture:

Windows Client  
↓  
SMB  
↓  
FSx File Gateway  
↓  
FSx Windows

This allows existing Windows applications and users to continue using:

**Familiar Windows file-sharing protocols**

---

# Backend Storage

The backend for FSx File Gateway is:

[[FSx for Windows File Server]]

This is the most important distinction from:

[[S3 File Gateway]]

### Memory Trick

**FSx Gateway → FSx Windows**

**S3 Gateway → S3**

---

# Local Cache

FSx File Gateway maintains a:

**Local cache**

of frequently accessed files.

Architecture:

On-Premises User  
↓  
FSx File Gateway  
├── Frequently Accessed File → Local Cache
└── Other Files → FSx Windows

This provides:

**Low-latency access**

to frequently used data.

> [!tip] Memory Trick
> **Hot Windows files stay local**

---

# Why Local Cache Matters

Without a local cache:

On-Premises User  
↓  
Network  
↓  
AWS  
↓  
FSx Windows

Every file access may depend more heavily on:

**Network latency**

With FSx File Gateway:

Frequently Used File  
↓  
Local Cache  
↓  
Fast Access

while the primary file system remains:

**FSx for Windows File Server**

---

# Primary File System Remains in AWS

An important architecture concept:

FSx File Gateway is not the:

**Primary file system**

The primary Windows file system is:

[[FSx for Windows File Server]]

The gateway provides:

- Local access
- SMB connectivity
- Local caching

Think:

FSx Windows  
= Primary File System

FSx File Gateway  
= Local Access Layer

---

# Hybrid Windows Architecture

A common architecture:

Corporate Office  
↓  
Windows Users  
↓  
SMB  
↓  
FSx File Gateway  
↓  
Network Connection  
↓  
FSx for Windows File Server

This lets organizations:

**Centralize Windows file storage in AWS**

while maintaining:

**Fast local access**

for on-premises users.

---

# Active Directory Integration

Because the architecture is based around Windows file sharing, it can integrate with:

**Microsoft Active Directory**

This allows users to continue using familiar:

- Windows identities
- Groups
- File permissions

Architecture:

Windows User  
↓  
Active Directory  
↓  
SMB  
↓  
FSx File Gateway  
↓  
FSx Windows

### Exam Pattern

> **On-premises Windows users + Active Directory + FSx Windows**
>
> → **FSx File Gateway**

---

# Why Use FSx File Gateway?

Use FSx File Gateway when:

- FSx Windows is the centralized file system
- Users remain on-premises
- SMB is required
- Frequently accessed files need low latency
- Local caching is beneficial

The architecture combines:

**AWS centralized storage**

with:

**On-premises performance**

---

# Branch Office Use Case

Imagine a company with:

**Multiple branch offices**

and one centralized:

[[FSx for Windows File Server]]

Each branch can use:

FSx File Gateway  
↓  
Local Cache  
↓  
FSx Windows

Frequently used files remain close to:

**Local users**

while the main file system remains centralized in:

**AWS**

---

# Centralized File Storage

Without centralized storage:

Branch A  
→ Local File Server

Branch B  
→ Local File Server

Branch C  
→ Local File Server

This can create:

- Duplicate infrastructure
- Separate backups
- Management overhead

With FSx File Gateway:

Branch A  
↓  
Gateway

Branch B  
↓  
Gateway

Branch C  
↓  
Gateway

All connect to:

FSx Windows

This creates:

**Centralized cloud file storage**

with:

**Distributed local caching**

---

# FSx File Gateway vs S3 File Gateway

This is the most important comparison.

## [[S3 File Gateway]]

Backend:

[[S3]]

Protocols:

- NFS
- SMB

Files become:

**S3 Objects**

Best when:

**Applications need file access to S3**

---

## FSx File Gateway

Backend:

[[FSx for Windows File Server]]

Protocol:

**SMB**

Best when:

**On-premises Windows users need access to FSx Windows**

### Memory Trick

**Need S3 objects?**
→ S3 File Gateway

**Need Windows file system?**
→ FSx File Gateway

---

# FSx File Gateway vs Direct FSx Windows Access

On-premises systems can access FSx Windows through network connectivity.

So why use the gateway?

The key additional benefit is:

**Local caching**

---

## Direct Access

On-Premises User  
↓  
Network  
↓  
FSx Windows

Every access depends on:

**Network connectivity and latency**

---

## Gateway Access

On-Premises User  
↓  
FSx File Gateway  
↓  
Local Cache  
↓  
FSx Windows

Frequently accessed files can be served:

**Locally**

### Exam Decision

Need basic network access  
→ Direct connectivity may work

Need:

**Local cache + low-latency access**

→ FSx File Gateway

---

# FSx File Gateway vs EFS

## [[EFS]]

Provides:

**Managed NFS storage**

primarily associated with Linux workloads.

---

## FSx File Gateway

Provides:

**Hybrid SMB access**

to:

FSx for Windows File Server

### Exam Decision

**Linux + NFS**
→ EFS

**On-prem Windows + SMB + FSx**
→ FSx File Gateway

---

# FSx File Gateway vs Volume Gateway

## FSx File Gateway

Storage type:

**File**

Protocol:

**SMB**

Backend:

FSx Windows

---

## [[Volume Gateway]]

Storage type:

**Block**

Protocol:

**iSCSI**

### Memory Trick

**Windows Files**
→ FSx File Gateway

**Blocks**
→ Volume Gateway

---

# FSx File Gateway vs DataSync

## FSx File Gateway

Provides:

**Ongoing hybrid file access**

Users continue working with files through the gateway.

---

## [[DataSync]]

Provides:

**Data movement**

Best for:

- Migration
- Replication
- Scheduled transfers

### Memory Trick

**Gateway = ACCESS**

**DataSync = MOVE**

---

# FSx File Gateway vs Snowball

## [[Snowball]]

Provides:

**Offline physical data migration**

---

## FSx File Gateway

Provides:

**Ongoing network-based hybrid access**

### Exam Decision

One-time massive migration  
→ Snowball

Continuous Windows file access  
→ FSx File Gateway

---

# Architecture Thinking

## Scenario 1 — Branch Office

A company has a branch office with Windows users.

The central file system is:

FSx for Windows File Server

Frequently accessed files need:

**Low-latency local access**

**Choose → FSx File Gateway**

---

## Scenario 2 — Multiple Offices

A company wants one centralized Windows file system in AWS.

Multiple branch offices need:

- SMB
- Local caching
- Shared centralized files

**Choose:**

FSx File Gateway  
+  
FSx for Windows File Server

---

## Scenario 3 — Files Must Become S3 Objects

An on-premises application needs SMB access, but files must be stored as:

**S3 Objects**

Do NOT choose FSx File Gateway.

Choose:

[[S3 File Gateway]]

---

## Scenario 4 — Block Storage

An on-premises application requires:

**iSCSI**

Do NOT choose FSx File Gateway.

Choose:

[[Volume Gateway]]

---

## Scenario 5 — Windows Share Without Local Cache Requirement

An on-premises environment already has reliable low-latency connectivity to AWS.

Users simply need direct access to:

FSx for Windows File Server.

FSx File Gateway may not be necessary.

The gateway becomes especially valuable when:

**Local caching is required**

---

# Scenario Recognition

Immediately think:

[[FSx File Gateway]]

when you see:

- On-premises Windows users
- SMB
- FSx for Windows File Server
- Local cache
- Branch office
- Hybrid Windows storage
- Centralized Windows file share
- Low-latency access to frequently used files

### Strongest Exam Pattern

> **"On-premises Windows users need low-latency access to frequently used files stored in FSx for Windows File Server."**
>
> → **FSx File Gateway**

---

# Exam Traps

## Trap 1 — FSx File Gateway Stores Files in S3

False.

Its backend is:

[[FSx for Windows File Server]]

---

## Trap 2 — FSx File Gateway and S3 File Gateway Are the Same

False.

S3 File Gateway:

**NFS / SMB → S3**

FSx File Gateway:

**SMB → FSx Windows**

---

## Trap 3 — FSx File Gateway Is Block Storage

False.

It provides:

**File access**

For block storage:

[[Volume Gateway]]

---

## Trap 4 — The Gateway Is the Primary Windows File System

False.

The primary file system remains:

**FSx for Windows File Server**

The gateway provides:

**Local access + caching**

---

## Trap 5 — Local Cache Contains the Only Copy

False.

The centralized file system remains:

**FSx Windows in AWS**

---

## Trap 6 — FSx File Gateway Is Primarily a Migration Service

False.

Its primary purpose is:

**Ongoing hybrid file access**

For migration:

Think [[DataSync]] or [[Snowball]] depending on the requirement.

---

# Quick Cheat Sheet

| Requirement | FSx File Gateway |
|---|---|
| Hybrid Windows Storage | ✅ |
| On-Premises Users | ✅ |
| SMB | ✅ |
| Backend = FSx Windows | ✅ |
| Local Cache | ✅ |
| Low-Latency Frequent Files | ✅ |
| Branch Offices | ✅ |
| Centralized Windows Files | ✅ |
| Active Directory Environment | ✅ |
| Backend = S3 | ❌ |
| NFS Primary Protocol | ❌ |
| Block Storage | ❌ |
| iSCSI | ❌ |

---

## Master Memory Trick

> [!tip] Master Memory Trick
> Imagine the company's main Windows file server moved to AWS.
>
> **FSx Windows**
>
> → Central corporate file cabinet
>
> But employees are still sitting in the branch office.
>
> **FSx File Gateway**
>
> → Small local cabinet containing copies of the files they use most often

So:

> **MAIN FILE SYSTEM**
>
> → FSx Windows
>
> **LOCAL DOORWAY**
>
> → FSx File Gateway
>
> **HOT FILES**
>
> → Local Cache
>
> **PROTOCOL**
>
> → SMB

And the killer exam clue:

> **ON-PREM + WINDOWS + FSx + LOCAL CACHE**
>
> → **FSx File Gateway**

---

## Related Notes

- [[Storage Gateway]]
- [[S3 File Gateway]]
- [[FSx for Windows File Server]]
- [[Volume Gateway]]
- [[Tape Gateway]]
- [[EFS]]
- [[DataSync]]
- [[Snowball]]
- [[05-Networking/Direct Connect]]
- [[05-Networking/Site-to-Site VPN]]
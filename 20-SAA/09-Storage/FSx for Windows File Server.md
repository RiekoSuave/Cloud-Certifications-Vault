## What Problem Does It Solve?

[[FSx for Windows File Server]] provides a fully managed Windows shared file system on AWS.

It solves the problem of:

> **"How can I run a Windows file share in AWS without managing the underlying Windows file servers myself?"**

Think:

Windows Applications  
↓  
SMB  
↓  
FSx for Windows File Server  
↓  
Shared Files

> [!tip] Memory Trick
> **Windows + SMB + NTFS = FSx for Windows**

---

## Core Characteristics

FSx for Windows File Server is:

**A fully managed Windows file-system shared drive**

It supports:

- SMB
- Windows NTFS
- Microsoft Active Directory
- ACLs
- User quotas

This makes it a strong fit for:

**Enterprise Windows file-sharing workloads**

---

## SMB Protocol

FSx for Windows uses:

**SMB**

or:

**Server Message Block**

SMB is commonly used by:

**Windows file-sharing environments**

Architecture:

Windows Client  
↓  
SMB  
↓  
FSx for Windows File Server

### Memory Trick

**SMB = Windows File Share**

---

## NTFS

FSx for Windows supports:

**Windows NTFS**

This gives applications a familiar Windows file-system environment.

Think:

Windows Application  
↓  
NTFS File System  
↓  
FSx for Windows

---

## Active Directory Integration

FSx for Windows integrates with:

**Microsoft Active Directory**

This is important for:

- User authentication
- Group-based access
- Enterprise identity
- Windows permissions

Architecture:

User  
↓  
Active Directory  
↓  
FSx Windows  
↓  
Shared Files

> [!tip] Exam Pattern
> **SMB + Active Directory**
>
> → **FSx for Windows File Server**

---

## ACLs

FSx for Windows supports:

**Access Control Lists**

or:

**ACLs**

These allow Windows-style file and folder permissions.

Think:

User / Group  
↓  
ACL  
↓  
Allowed / Denied  
↓  
File or Folder

---

## User Quotas

FSx for Windows supports:

**User quotas**

This lets administrators limit how much storage individual users can consume.

Example:

User A  
↓  
Maximum Allowed Storage

User B  
↓  
Different Maximum

Useful for:

- Home directories
- Department shares
- Enterprise file storage

---

## Linux EC2 Can Mount FSx Windows

An important exam detail:

FSx for Windows can also be mounted from:

**Linux EC2 instances**

Do not assume:

> **"Windows file system means only Windows EC2 can connect."**

The stronger clue is:

**SMB / Windows file-system requirement**

---

## Distributed File System Namespaces

FSx for Windows supports:

**Microsoft Distributed File System Namespaces**

or:

**DFS Namespaces**

DFS Namespaces can group files across:

**Multiple file systems**

under a unified namespace.

Conceptually:

Users  
↓  
DFS Namespace  
↓  
├── File System A
├── File System B
└── File System C

### Architecture Thinking

Users can interact with:

**One logical file namespace**

while the underlying files may live across multiple file systems.

---

## Performance and Scale

The Maarek slides highlight that FSx for Windows can scale to:

- Tens of GB/s
- Millions of IOPS
- Hundreds of PB of data

The main exam takeaway is:

> **FSx Windows is designed for very large enterprise Windows workloads.**

---

## Storage Options

FSx for Windows supports:

- SSD
- HDD

The correct choice depends on:

**Performance requirements**

---

## SSD Storage

Choose:

**SSD**

for:

**Latency-sensitive workloads**

Examples from the Maarek slides include:

- Databases
- Media processing
- Data analytics

### Memory Trick

**SSD = Speed-sensitive**

---

## HDD Storage

Choose:

**HDD**

for broader workloads where extreme latency performance is not required.

Examples include:

- Home directories
- Content management systems

### Memory Trick

**HDD = General file storage**

---

## SSD vs HDD

| Requirement | Best Choice |
|---|---|
| Latency-sensitive application | SSD |
| Database workload | SSD |
| Media processing | SSD |
| Data analytics | SSD |
| Home directory | HDD |
| Content management system | HDD |
| General shared file storage | HDD may fit |

---

## On-Premises Access

FSx for Windows can be accessed from:

**On-premises infrastructure**

using:

- [[05-Networking/Site-to-Site VPN]]
- [[05-Networking/Direct Connect]]

Architecture:

On-Premises Windows Servers  
↓  
VPN / Direct Connect  
↓  
AWS  
↓  
FSx for Windows File Server

This makes FSx Windows useful in:

**Hybrid Cloud architectures**

---

## Hybrid Windows File Storage

Example:

Corporate Data Center  
↓  
Existing Windows Users  
↓  
[[05-Networking/Direct Connect]]  
↓  
FSx Windows

Users can continue accessing centralized file storage while infrastructure gradually moves into AWS.

### Exam Pattern

> **On-premises Windows systems need managed SMB storage in AWS**
>
> → **FSx Windows + VPN / Direct Connect**

---

## Multi-AZ

FSx for Windows can be configured as:

**Multi-AZ**

This provides:

**High Availability**

Architecture:

Availability Zone A  
↕  
FSx Windows  
↕  
Availability Zone B

The important exam clue:

> **Windows shared file system + HA**
>
> → **Multi-AZ FSx Windows**

---

## Why Multi-AZ Matters

If one Availability Zone experiences a failure:

The file system architecture can maintain:

**Higher availability**

than a single-AZ deployment.

Think:

Windows File Share  
+  
Production Critical  
+  
AZ Failure Protection

→ Multi-AZ

---

## Daily Backups

The Maarek slides state that FSx for Windows data is:

**Backed up daily to S3**

This helps provide:

- Backup protection
- Recovery capability
- Managed data protection

### Memory Trick

**FSx Windows = Daily S3 Backup**

---

## Architecture Thinking

### Scenario 1 — Corporate Windows Share

A company is moving its Windows file server into AWS.

Requirements:

- SMB
- NTFS
- Active Directory
- Shared file access

**Choose → FSx for Windows File Server**

---

### Scenario 2 — Highly Available Windows Share

A business-critical Windows application requires:

- Shared file storage
- Active Directory
- Protection from AZ failure

**Choose → Multi-AZ FSx for Windows File Server**

---

### Scenario 3 — Home Directories

A company needs centralized Windows home directories.

The workload does not require very low latency.

**Choose:**

FSx for Windows  
+  
HDD Storage

---

### Scenario 4 — Latency-Sensitive Workload

A Windows application performs:

- Database operations
- Media processing
- Analytics

and requires low storage latency.

**Choose:**

FSx for Windows  
+  
SSD Storage

---

### Scenario 5 — Hybrid Migration

An enterprise still has Windows servers on-premises.

Those servers must access a managed AWS file share.

**Choose:**

FSx for Windows  
+  
[[05-Networking/Direct Connect]]

or:

[[05-Networking/Site-to-Site VPN]]

---

### Scenario 6 — Linux Client Needs SMB Share

A Linux EC2 instance must access an existing Windows-compatible SMB file share.

Can FSx Windows work?

**Yes.**

The Maarek slides explicitly note that it can be mounted on:

**Linux EC2 instances**

---

### Scenario 7 — Multiple File Systems Under One Namespace

An enterprise has multiple Windows file systems but wants users to see one logical file structure.

**Choose → DFS Namespaces**

with:

FSx for Windows

---

## FSx Windows vs EFS

These are commonly confused.

### FSx Windows

Think:

- Windows
- SMB
- NTFS
- Active Directory

---

### [[EFS]]

Think:

- Linux
- NFS
- Elastic shared file system

### Exam Decision

**Windows + SMB**
→ FSx Windows

**Linux + NFS**
→ EFS

---

## FSx Windows vs FSx for Lustre

### FSx Windows

Optimized for:

**Enterprise Windows file sharing**

---

### [[FSx for Lustre]]

Optimized for:

**High-performance parallel computing**

### Exam Decision

**SMB / Windows**
→ FSx Windows

**HPC / ML**
→ Lustre

---

## FSx Windows vs S3

### [[S3]]

Is:

**Object Storage**

Objects are accessed using:

APIs / HTTP

---

### FSx Windows

Is:

**File Storage**

Applications access:

Files and directories

through:

**SMB**

### Memory Trick

**S3 = Objects**

**FSx Windows = Windows Files**

---

## Scenario Recognition

Immediately think:

[[FSx for Windows File Server]]

when you see:

- SMB
- NTFS
- Windows file share
- Active Directory
- ACL
- User quotas
- DFS Namespace
- Windows home directories
- Hybrid Windows file storage
- Multi-AZ Windows file system

### Strongest Exam Pattern

> **"Managed shared Windows file system using SMB and Active Directory."**
>
> → **FSx for Windows File Server**

---

## Exam Traps

### Trap 1 — FSx Windows Uses NFS

False.

Its key protocol is:

**SMB**

---

### Trap 2 — Only Windows Instances Can Mount It

False.

The Maarek slides explicitly state:

**Linux EC2 instances can mount it**

---

### Trap 3 — FSx Windows Cannot Integrate with Active Directory

False.

Active Directory integration is one of its main enterprise features.

---

### Trap 4 — FSx Windows Is Single-AZ Only

False.

It can be configured:

**Multi-AZ**

---

### Trap 5 — FSx Windows Only Supports SSD

False.

It supports:

- SSD
- HDD

---

### Trap 6 — HDD Is Better for Latency-Sensitive Databases

False.

Use:

**SSD**

for latency-sensitive workloads.

---

### Trap 7 — On-Premises Systems Cannot Access FSx Windows

False.

They can connect through:

- [[05-Networking/Site-to-Site VPN]]
- [[05-Networking/Direct Connect]]

---

### Trap 8 — FSx Windows Is Object Storage

False.

It provides:

**Managed file storage**

---

## Quick Cheat Sheet

| Requirement | FSx Windows |
|---|---|
| Managed Windows File Share | ✅ |
| SMB | ✅ |
| NTFS | ✅ |
| Active Directory | ✅ |
| ACLs | ✅ |
| User Quotas | ✅ |
| Linux EC2 Can Mount | ✅ |
| DFS Namespaces | ✅ |
| SSD | ✅ |
| HDD | ✅ |
| Multi-AZ | ✅ |
| On-Premises Access | ✅ |
| VPN | ✅ |
| Direct Connect | ✅ |
| Daily Backup to S3 | ✅ |
| NFS Primary Protocol | ❌ |
| HPC Specialty | ❌ |

---

## Master Memory Trick

> [!tip] Master Memory Trick
> **FSx Windows = Corporate Windows Shared Drive in AWS**
>
> **SMB**
> → File sharing
>
> **NTFS**
> → Windows file system
>
> **Active Directory**
> → Users and groups
>
> **ACLs**
> → Permissions
>
> **Quotas**
> → Storage limits
>
> **Multi-AZ**
> → High availability
>
> **VPN / Direct Connect**
> → Hybrid access

Then remember storage:

> **SSD = Latency-sensitive**
>
> **HDD = General file sharing**

And the killer exam clue:

> **Windows + SMB + Active Directory**
>
> → **FSx for Windows File Server**

---

## Related Notes

- [[FSx]]
- [[FSx for Lustre]]
- [[FSx for NetApp ONTAP]]
- [[FSx for OpenZFS]]
- [[EFS]]
- [[S3]]
- [[EC2]]
- [[Active Directory]]
- [[05-Networking/Direct Connect]]
- [[05-Networking/Site-to-Site VPN]]
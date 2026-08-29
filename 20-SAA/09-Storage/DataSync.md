## What Problem Does It Solve?

[[DataSync]] is a managed AWS service for:

**Moving large amounts of data between storage systems**

It solves the problem of:

> **"How can I efficiently move or synchronize large datasets between on-premises storage and AWS, or between AWS storage services?"**

Think:

Source Storage  
↓  
DataSync  
↓  
Destination Storage

> [!tip] Memory Trick
> **DataSync = MOVE the data**
>
> [[Storage Gateway]] = USE hybrid storage  
> [[DataSync]] = MOVE / SYNC storage

---

## What Is DataSync?

DataSync is designed for:

**Online data transfer**

It can automate and accelerate moving data:

- From on-premises to AWS
- From AWS to on-premises
- Between AWS storage services

Common use cases include:

- Data migration
- Data replication
- Archival
- Disaster recovery
- Data processing workflows

---

# On-Premises to AWS

A common architecture:

On-Premises Storage  
↓  
DataSync Agent  
↓  
Network  
↓  
DataSync  
↓  
AWS Storage

This allows organizations to migrate or synchronize data without manually building:

**Custom transfer scripts**

---

# Supported On-Premises Storage

DataSync can work with storage using protocols such as:

- NFS
- SMB

It can also work with:

**HDFS**

for certain data-transfer scenarios.

### Memory Trick

**NFS / SMB + MOVE**
→ DataSync

**NFS / SMB + CONTINUOUS FILE ACCESS TO S3**
→ S3 File Gateway

---

# DataSync Agent

When transferring data between:

**On-Premises Storage**

and:

**AWS**

you generally deploy a:

**DataSync Agent**

in the on-premises environment.

Architecture:

NFS / SMB Server  
↓  
DataSync Agent  
↓  
AWS DataSync  
↓  
AWS Storage

The agent helps connect:

**Local storage**

to:

**AWS DataSync**

---

# DataSync Agent Deployment

The agent can run in the customer's environment as a:

**Virtual Machine**

Conceptually:

On-Premises Hypervisor  
↓  
DataSync Agent  
↓  
AWS

The key exam point:

> **On-premises DataSync transfers normally involve a DataSync agent.**

---

# AWS-to-AWS Transfers

DataSync can also transfer data:

**Between AWS storage services**

In these cases, an on-premises agent is not required.

Architecture:

AWS Storage A  
↓  
DataSync  
↓  
AWS Storage B

### Exam Pattern

> **Move data between supported AWS storage services**
>
> → **DataSync**

---

# Supported AWS Storage

Important DataSync destinations and sources include:

- [[S3]]
- [[EFS]]
- [[FSx for Windows File Server]]
- [[FSx for Lustre]]
- [[FSx for OpenZFS]]
- [[FSx for NetApp ONTAP]]

The exact supported direction can depend on the storage service, but for SAA the major concept is:

> **DataSync moves data into, out of, and between AWS file/object storage services.**

---

# DataSync + S3

A very common architecture:

On-Premises NFS Server  
↓  
DataSync Agent  
↓  
DataSync  
↓  
[[S3]]

Use this when:

**Large amounts of file data need to be transferred into S3 over the network**

---

# DataSync + EFS

Example:

On-Premises NFS  
↓  
DataSync  
↓  
[[EFS]]

This is useful when migrating:

**Linux shared-file workloads**

to AWS.

---

# DataSync + FSx

DataSync can be useful for moving datasets into or between:

**Amazon FSx file systems**

Example:

On-Premises SMB  
↓  
DataSync  
↓  
[[FSx for Windows File Server]]

### Exam Pattern

> **Migrate an on-premises SMB file share into FSx Windows**
>
> → **DataSync**

---

# Scheduled Transfers

DataSync transfers can be:

**Scheduled**

This makes it useful for:

- Recurring synchronization
- Periodic replication
- Regular archival
- Hybrid workflows

Architecture:

On-Premises Storage  
↓  
Every Day / Week  
↓  
DataSync  
↓  
AWS

> [!tip] Memory Trick
> **Need recurring copies? DataSync can schedule them.**

---

# Incremental Transfers

After an initial transfer:

DataSync can copy:

**Only changed data**

during subsequent executions.

Conceptually:

Initial Run  
↓  
Transfer Dataset

Later Run  
↓  
Detect Changes  
↓  
Transfer Changed Data

This makes recurring synchronization more efficient.

---

# Data Integrity

DataSync includes mechanisms for:

**Data integrity verification**

during transfers.

The service can verify that transferred data:

**Arrived correctly**

This is important for:

- Migration
- Backup
- Replication

---

# Metadata Preservation

DataSync can preserve relevant:

**File metadata**

depending on the source and destination.

Examples may include:

- Timestamps
- Permissions
- Ownership-related metadata

This is particularly important when migrating:

**File systems**

rather than simply copying object contents.

---

# Encryption

DataSync protects data:

**In transit**

between storage environments and AWS.

This helps provide secure network-based:

**Data movement**

---

# Network Connectivity

DataSync transfers occur:

**Over the network**

Possible connectivity can include:

- Internet
- [[05-Networking/Site-to-Site VPN]]
- [[05-Networking/Direct Connect]]

depending on the architecture.

### Important Distinction

If network bandwidth is insufficient for the required migration window:

Think:

[[Snowball]]

instead.

---

# DataSync vs Storage Gateway

This is one of the most important exam comparisons.

## [[Storage Gateway]]

Purpose:

**Ongoing hybrid storage access**

Architecture:

Application  
↕  
Storage Gateway  
↕  
AWS Storage

---

## DataSync

Purpose:

**Move or synchronize data**

Architecture:

Source  
↓  
DataSync  
↓  
Destination

### Master Memory Trick

**Storage Gateway = USE**

**DataSync = MOVE**

---

# DataSync vs S3 File Gateway

## [[S3 File Gateway]]

Use when:

An on-premises application needs:

**Ongoing NFS / SMB access**

while data is stored in S3.

---

## DataSync

Use when:

You need to:

**Transfer or synchronize**

the dataset.

### Exam Decision

> Application continuously works with S3 through NFS
>
> → S3 File Gateway

> Copy NFS dataset into S3 every night
>
> → DataSync

---

# DataSync vs AWS Transfer Family

## [[AWS Transfer Family]]

Best when users or partners use:

- SFTP
- FTPS
- FTP

---

## DataSync

Best when transferring data between:

**Storage systems**

such as:

- NFS
- SMB
- S3
- EFS
- FSx

### Memory Trick

**SFTP client**
→ Transfer Family

**Storage migration**
→ DataSync

---

# DataSync vs Snowball

## DataSync

Best for:

**Online transfers**

Uses:

Network connectivity

---

## [[Snowball]]

Best for:

**Offline transfers**

Uses:

Physical AWS devices

### Exam Decision

Good network + large migration  
→ DataSync

Terrible network + enormous migration  
→ Snowball

---

# DataSync vs Direct Connect

[[05-Networking/Direct Connect]] provides:

**Network connectivity**

DataSync provides:

**Data-transfer functionality**

They can work together.

Architecture:

On-Premises Storage  
↓  
DataSync Agent  
↓  
Direct Connect  
↓  
AWS DataSync  
↓  
AWS Storage

### Memory Trick

**Direct Connect = Road**

**DataSync = Moving Truck**

---

# DataSync vs S3 Transfer Acceleration

## [[S3 Transfer Acceleration]]

Accelerates:

**S3 uploads and downloads**

over long geographic distances using AWS edge locations.

---

## DataSync

Provides:

**Managed storage-to-storage transfer and synchronization**

including:

- Scheduling
- Verification
- Metadata handling

### Exam Decision

Application uploads objects globally to S3  
→ Transfer Acceleration

Migrate an NFS file server to AWS  
→ DataSync

---

# Architecture Thinking

## Scenario 1 — NFS to S3 Migration

A company has:

100 TB

on an on-premises NFS server.

It has sufficient network bandwidth and wants a managed online migration.

**Choose:**

DataSync Agent  
↓  
DataSync  
↓  
[[S3]]

---

## Scenario 2 — SMB to FSx Windows

A company is migrating its on-premises:

**Windows SMB file server**

to:

[[FSx for Windows File Server]]

**Choose → DataSync**

---

## Scenario 3 — NFS to EFS

A company wants to migrate a Linux NFS workload into:

[[EFS]]

with metadata preserved.

**Choose → DataSync**

---

## Scenario 4 — Nightly Synchronization

A company needs to copy changed files from:

On-Premises NFS

to:

S3

every night.

**Choose → DataSync**

using:

**Scheduled transfers**

---

## Scenario 5 — Continuous NFS Access to S3

An application must continue using NFS against files whose backend is S3.

Do NOT choose DataSync just because NFS and S3 appear in the question.

Choose:

[[S3 File Gateway]]

because the requirement is:

**Access**

not:

**Transfer**

---

## Scenario 6 — SFTP Partners

External partners upload files using:

**SFTP**

Do NOT choose DataSync.

Choose:

[[AWS Transfer Family]]

---

## Scenario 7 — Petabyte Migration with Weak Network

A company needs to migrate:

2 PB

but its available network connection would take months.

Do NOT choose DataSync.

Choose:

[[Snowball]]

---

## Scenario 8 — AWS-to-AWS Migration

A company needs to move large amounts of data between supported AWS storage services.

**Choose → DataSync**

No on-premises DataSync agent is needed for a purely:

**AWS-to-AWS transfer**

---

# Scenario Recognition

Immediately think:

[[DataSync]]

when you see:

- Move data
- Synchronize data
- Migrate file server
- NFS migration
- SMB migration
- Scheduled transfer
- Recurring replication
- Changed files
- Metadata preservation
- Data verification
- Online storage migration
- S3 / EFS / FSx transfer

### Strongest Exam Pattern

> **"Automate and accelerate moving large datasets between on-premises storage and AWS over the network."**
>
> → **AWS DataSync**

---

# Exam Traps

## Trap 1 — DataSync Provides a File System for Applications

False.

DataSync:

**Moves data**

It does not provide the ongoing hybrid file interface that:

[[Storage Gateway]]

provides.

---

## Trap 2 — NFS Automatically Means S3 File Gateway

False.

Ask:

**ACCESS or MOVE?**

NFS + Access S3 continuously  
→ S3 File Gateway

NFS + Migrate / Sync  
→ DataSync

---

## Trap 3 — SFTP Means DataSync

False.

Think:

[[AWS Transfer Family]]

---

## Trap 4 — DataSync Requires an Agent for Every Transfer

False.

The agent is important for:

**On-premises storage transfers**

AWS-to-AWS transfers do not require an on-premises agent.

---

## Trap 5 — DataSync Is an Offline Migration Service

False.

DataSync transfers data:

**Over the network**

For offline physical migration:

[[Snowball]]

---

## Trap 6 — Direct Connect Replaces DataSync

False.

Direct Connect provides:

**Connectivity**

DataSync provides:

**Transfer logic**

They can work together.

---

## Trap 7 — DataSync Always Retransfers the Entire Dataset

False.

Recurring transfers can copy:

**Changed data**

rather than unnecessarily retransferring everything.

---

# Migration Decision Table

| Requirement | Best Choice |
|---|---|
| NFS/SMB → AWS Migration | DataSync |
| Scheduled Storage Sync | DataSync |
| AWS Storage → AWS Storage | DataSync |
| Ongoing NFS/SMB → S3 Access | S3 File Gateway |
| SFTP/FTPS/FTP | Transfer Family |
| Massive Offline Migration | Snowball |
| Hybrid Block Storage | Volume Gateway |
| Virtual Tape Backup | Tape Gateway |

---

# Quick Cheat Sheet

| Feature | DataSync |
|---|---|
| Managed Data Transfer | ✅ |
| Online Transfer | ✅ |
| On-Prem → AWS | ✅ |
| AWS → On-Prem | ✅ |
| AWS → AWS | ✅ |
| NFS | ✅ |
| SMB | ✅ |
| S3 | ✅ |
| EFS | ✅ |
| FSx | ✅ |
| Scheduled Transfers | ✅ |
| Incremental Transfers | ✅ |
| Data Verification | ✅ |
| Metadata Preservation | ✅ |
| On-Prem Agent | Usually Required |
| Ongoing File Interface | ❌ |
| FTP/SFTP Service | ❌ |
| Offline Physical Transfer | ❌ |

---

## Master Memory Trick

> [!tip] Master Memory Trick
> Imagine you're moving houses.
>
> **Storage Gateway**
>
> → Builds a doorway between the two houses so you can keep using both.
>
> **DataSync**
>
> → Hires movers to carry your stuff from one house to the other.
>
> **Snowball**
>
> → Loads everything into a giant truck because the road/network is terrible.
>
> **Transfer Family**
>
> → Lets outside people deliver packages using the protocol they already know.

For DataSync, remember:

> **NFS / SMB**
>
> +
>
> **MOVE / MIGRATE / SYNC**
>
> =
>
> **DATASYNC**

And always ask:

> **ACCESS or MOVE?**
>
> **ACCESS**
> → Storage Gateway
>
> **MOVE**
> → DataSync

---

## Related Notes

- [[Storage Gateway]]
- [[S3 File Gateway]]
- [[AWS Transfer Family]]
- [[Snowball]]
- [[S3]]
- [[EFS]]
- [[FSx for Windows File Server]]
- [[FSx for Lustre]]
- [[FSx for NetApp ONTAP]]
- [[FSx for OpenZFS]]
- [[05-Networking/Direct Connect]]
- [[05-Networking/Site-to-Site VPN]]
- [[S3 Transfer Acceleration]]
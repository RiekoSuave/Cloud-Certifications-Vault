## What Problem Does It Solve?

[[Snowball Edge Storage Optimized]] is designed for:

**Large-scale data migration and storage-heavy edge workloads**

when transferring the data over the network would be:

- Too slow
- Impractical
- Limited by bandwidth
- Unable to meet the migration deadline

It solves the problem of:

> **"How can I move a very large amount of data to AWS when storage capacity matters more than edge compute power?"**

Architecture:

On-Premises Data  
↓  
Snowball Edge Storage Optimized  
↓  
Physical Shipment  
↓  
AWS  
↓  
[[S3]]

> [!tip] Memory Trick
> **Storage Optimized = Pick it when DATA SIZE is the problem**

---

# What Is Snowball Edge Storage Optimized?

Snowball Edge Storage Optimized is a:

**Rugged physical Snow Family device**

optimized primarily for:

- Data migration
- Large-capacity storage
- Local data collection
- Storage-heavy edge workloads

It belongs to:

[[Snowball Edge]]

within the:

[[Snow Family]]

---

# Primary Exam Purpose

For SAA, the strongest association should be:

> **Large dataset + insufficient network bandwidth**
>
> → **Snowball Edge Storage Optimized**

Think:

Large Data  
+
Poor Network  
+
Migration Deadline  
=
Snowball Edge Storage Optimized

---

# Storage Capacity

The Maarek course traditionally highlights approximately:

**80 TB of usable storage**

for data-transfer workloads on Snowball Edge Storage Optimized.

The exact hardware specifications can evolve.

For exam reasoning, focus on:

> **Snowball Edge Storage Optimized provides substantially more storage capacity than Snowcone and is intended for large migration jobs.**

---

# Large-Scale Data Migration

Example:

Company Data Center  
↓  
200 TB Dataset  
↓  
Multiple Snowball Edge Devices  
↓  
Ship to AWS  
↓  
Import into S3

Instead of transferring the dataset across a slow WAN connection:

**The data physically travels to AWS.**

---

# Multiple Devices

If the dataset is larger than the capacity of one device:

Use:

**Multiple Snowball Edge devices**

Example:

240 TB Dataset  
↓  
Snowball Edge #1  
Snowball Edge #2  
Snowball Edge #3  
↓  
AWS

### Exam Thinking

Do not reject Snowball Edge simply because:

**The dataset exceeds one device's capacity.**

Multiple devices can be used.

---

# Migration Workflow

A typical migration looks like:

1. Order Snowball Edge Storage Optimized
2. AWS ships the device
3. Connect it to the local network
4. Copy data onto the device
5. Ship it back to AWS
6. AWS imports the data
7. Device data is securely erased

Architecture:

Customer Data  
↓  
Load Device  
↓  
Ship  
↓  
AWS  
↓  
Import  
↓  
Secure Erase

---

# Import into S3

A major destination for migrated data is:

[[S3]]

Architecture:

On-Premises Storage  
↓  
Snowball Edge Storage Optimized  
↓  
AWS  
↓  
S3 Bucket

### Exam Pattern

> **Hundreds of TB must be migrated into S3, but available bandwidth is inadequate.**
>
> → **Snowball Edge Storage Optimized**

---

# Local Storage at the Edge

Storage Optimized is not limited to:

**One-time migration**

It can also provide:

**Large local storage capacity at edge locations**

Example:

Remote Site  
↓  
Generates Large Dataset  
↓  
Snowball Edge Storage Optimized  
↓  
Store Locally  
↓  
Transfer Later

---

# Edge Data Collection

Imagine a remote scientific operation generates:

**Large amounts of raw data**

but cannot continuously send that data to AWS.

Architecture:

Sensors  
↓  
Snowball Edge Storage Optimized  
↓  
Store Data Locally  
↓  
Ship / Transfer Later

This makes Storage Optimized useful when:

**Data volume is larger than available connectivity**

---

# Limited Edge Compute

Snowball Edge Storage Optimized can provide edge capabilities, but its main design emphasis is:

**Storage**

If the scenario emphasizes:

- Heavy processing
- CPU requirements
- Video analytics
- ML inference

think more strongly about:

[[Snowball Edge Compute Optimized]]

---

# Storage Optimized vs Compute Optimized

This is the key distinction.

## Snowball Edge Storage Optimized

Priority:

**Storage Capacity**

Think:

- Migration
- Large datasets
- Data collection
- Storage-heavy edge

---

## [[Snowball Edge Compute Optimized]]

Priority:

**Compute Power**

Think:

- Edge analytics
- Video processing
- Machine learning inference
- Compute-intensive workloads

### Memory Trick

**Lots of DATA**
→ Storage Optimized

**Lots of PROCESSING**
→ Compute Optimized

---

# Storage Optimized vs Snowcone

## [[Snowcone]]

Think:

- Small
- Portable
- Limited space
- Smaller datasets
- Lightweight edge

---

## Storage Optimized

Think:

- Larger
- Much more storage
- Large migration
- Storage-heavy workloads

### Exam Decision

Small portable field device  
→ Snowcone

Large physical migration device  
→ Snowball Edge Storage Optimized

---

# Storage Optimized vs DataSync

## [[DataSync]]

Transfers data:

**Over the network**

Best when:

**Network bandwidth is sufficient**

---

## Snowball Edge Storage Optimized

Transfers data:

**Physically**

Best when:

**Network bandwidth is insufficient**

### Memory Trick

**Good pipe → DataSync**

**Bad pipe → Snowball**

---

# Storage Optimized vs Direct Connect

## [[05-Networking/Direct Connect]]

Provides:

**Dedicated network connectivity**

Useful for:

**Ongoing connectivity**

---

## Snowball Edge Storage Optimized

Provides:

**Offline physical data migration**

Useful for:

**Large one-time migrations**

### Exam Decision

Long-term hybrid network requirement  
→ Direct Connect

Large one-time migration with poor bandwidth  
→ Snowball Edge Storage Optimized

---

# Storage Optimized vs Storage Gateway

## [[Storage Gateway]]

Provides:

**Ongoing hybrid storage access**

---

## Snowball Edge Storage Optimized

Provides:

**Physical data migration + edge storage**

### Memory Trick

**Gateway = ACCESS**

**Snowball = MIGRATE**

---

# Storage Optimized vs S3 Transfer Acceleration

## [[S3 Transfer Acceleration]]

Accelerates:

**Network-based S3 transfers**

using AWS edge locations.

---

## Snowball Edge Storage Optimized

Avoids the network bottleneck by:

**Physically transporting the data**

### Exam Decision

Long-distance uploads with adequate bandwidth  
→ S3 Transfer Acceleration may help

Huge migration where bandwidth itself is inadequate  
→ Snowball Edge

---

# Migration Time Reasoning

Suppose:

Dataset:

**300 TB**

Available bandwidth:

**100 Mbps**

Even under ideal conditions, network transfer could take:

**Many months**

If the business requires completion in:

**Two weeks**

the network does not meet the requirement.

Think:

**Multiple Snowball Edge Storage Optimized devices**

---

# One-Time vs Recurring

This distinction matters.

## One-Time Huge Migration

Think:

**Snowball Edge Storage Optimized**

---

## Recurring Online Synchronization

Think:

[[DataSync]]

---

## Continuous Hybrid Access

Think:

[[Storage Gateway]]

### Master Decision

**MOVE ONCE OFFLINE**
→ Snowball

**SYNC REPEATEDLY ONLINE**
→ DataSync

**ACCESS CONTINUOUSLY**
→ Storage Gateway

---

# Architecture Thinking

## Scenario 1 — 300 TB to S3

A company needs to migrate:

300 TB

to S3.

Its internet connection cannot complete the migration within the required timeframe.

**Choose → Multiple Snowball Edge Storage Optimized devices**

---

## Scenario 2 — Remote Data Collection

A remote site generates large datasets but has:

**Intermittent network connectivity**

The primary requirement is:

**Large local storage capacity**

**Choose → Snowball Edge Storage Optimized**

---

## Scenario 3 — Video Analytics

A remote site needs to perform:

**Compute-intensive video analytics**

The major requirement is compute, not storage capacity.

Choose:

[[Snowball Edge Compute Optimized]]

---

## Scenario 4 — Small Portable Device

A field team needs:

**Maximum portability**

and only a relatively small amount of storage.

Choose:

[[Snowcone]]

---

## Scenario 5 — Nightly Transfer

A company wants to synchronize:

5 TB of changed data

to AWS every night over a fast network.

Do NOT choose Snowball Edge.

Choose:

[[DataSync]]

---

## Scenario 6 — Ongoing NFS Access

An application requires:

**Continuous NFS access**

to cloud-backed storage.

Do NOT choose Snowball Edge.

Think:

[[Storage Gateway]]

---

# Scenario Recognition

Immediately think:

[[Snowball Edge Storage Optimized]]

when you see:

- Large offline migration
- Hundreds of TB
- Poor bandwidth
- Storage capacity
- Physical AWS device
- Large local data collection
- Storage-heavy edge workload
- Migration deadline
- S3 migration

### Strongest Exam Pattern

> **"Hundreds of TB must be migrated to AWS, available bandwidth cannot meet the deadline, and storage capacity is the main requirement."**
>
> → **Snowball Edge Storage Optimized**

---

# Exam Traps

## Trap 1 — Storage Optimized Means It Cannot Perform Any Edge Computing

False.

It has edge capabilities.

The distinction is:

**Its primary emphasis is storage.**

---

## Trap 2 — Storage Optimized Is the Best Snowball for Heavy ML Inference

Not usually.

Think:

[[Snowball Edge Compute Optimized]]

---

## Trap 3 — A Dataset Larger Than One Device Means Snowball Cannot Be Used

False.

Use:

**Multiple devices**

---

## Trap 4 — Snowball Edge Is Best for Recurring Daily Synchronization

False.

Think:

[[DataSync]]

---

## Trap 5 — Snowball Edge Provides Continuous Hybrid Storage Access

False.

Think:

[[Storage Gateway]]

---

## Trap 6 — Snowball Edge Requires Good Network Connectivity

False.

It specifically helps when:

**Network transfer is impractical**

---

## Trap 7 — Snowcone Has More Storage Than Storage Optimized

False.

[[Snowcone]] is the:

**Smaller portable option**

---

# Quick Cheat Sheet

| Requirement | Best Choice |
|---|---|
| Large Offline Migration | Snowball Edge Storage Optimized |
| Hundreds of TB | Snowball Edge Storage Optimized |
| Storage Is Main Requirement | Storage Optimized |
| Poor Bandwidth | Storage Optimized |
| Large Edge Data Collection | Storage Optimized |
| Heavy Edge Processing | Compute Optimized |
| Small Portable Device | Snowcone |
| Recurring Online Transfer | DataSync |
| Continuous Hybrid Access | Storage Gateway |
| Dedicated Network Connection | Direct Connect |

---

## Master Memory Trick

> [!tip] Master Memory Trick
> Imagine you have a warehouse full of data.
>
> Your internet connection is a garden hose.
>
> You could spend months trying to squeeze the warehouse through the hose...
>
> or AWS can send you:
>
> **SNOWBALL EDGE STORAGE OPTIMIZED**

Load it:

> **DATA**
> ↓
> **SNOWBALL**
> ↓
> **TRUCK**
> ↓
> **AWS**
> ↓
> **S3**

Then ask:

> **WHAT'S THE BOTTLENECK?**

If:

> **STORAGE / DATA SIZE**
>
> → **Storage Optimized**

If:

> **COMPUTE / PROCESSING**
>
> → [[Snowball Edge Compute Optimized]]

And remember the migration trio:

> **MOVE ONCE + BAD NETWORK**
> → Snowball Edge
>
> **MOVE REPEATEDLY + GOOD NETWORK**
> → [[DataSync]]
>
> **KEEP ACCESSING CLOUD STORAGE**
> → [[Storage Gateway]]

---

## Related Notes

- [[Snow Family]]
- [[Snowball Edge]]
- [[Snowball Edge Compute Optimized]]
- [[Snowcone]]
- [[Snowmobile]]
- [[DataSync]]
- [[Storage Gateway]]
- [[S3]]
- [[S3 Transfer Acceleration]]
- [[05-Networking/Direct Connect]]
- [[06-Security/KMS]]
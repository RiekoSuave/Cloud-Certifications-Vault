## What Problem Does It Solve?

[[Snowball Edge]] is a physical AWS device designed for:

- Large-scale offline data migration
- Edge storage
- Edge computing

It solves the problem of:

> **"How can I move a very large dataset or run AWS-style compute at a location where network connectivity is limited or unavailable?"**

Think:

On-Premises / Edge Location  
↓  
Snowball Edge  
↓  
Store + Process Data  
↓  
Ship / Transfer  
↓  
AWS

> [!tip] Memory Trick
> **Snowball Edge = Big Snow device for MOVE + COMPUTE**

---

# What Is Snowball Edge?

Snowball Edge is part of:

[[Snow Family]]

It is a:

**Rugged physical device**

that provides:

- Storage
- Data transfer
- Edge computing

It is larger and more capable than:

[[Snowcone]]

---

# Major Snowball Edge Uses

Think of two major categories:

## Data Migration

Move large datasets:

On-Premises  
↓  
Snowball Edge  
↓  
Ship Device  
↓  
AWS

---

## Edge Computing

Run workloads:

**Locally**

without requiring continuous access to an AWS Region.

Architecture:

Sensors / Applications  
↓  
Snowball Edge  
↓  
Local Processing  
↓  
AWS Later

> [!tip] Memory Trick
> **Snowball Edge = MOVE DATA or PROCESS AT THE EDGE**

---

# Snowball Edge Device Types

For the SAA exam, distinguish between:

1. **Snowball Edge Storage Optimized**
2. **Snowball Edge Compute Optimized**

The names are your biggest clue.

---

# Snowball Edge Storage Optimized

[[Snowball Edge Storage Optimized]] emphasizes:

**Storage capacity**

It is designed primarily for:

- Large-scale data migration
- Local storage
- Data collection
- Storage-heavy edge workloads

### Memory Trick

**Storage Optimized = More DATA**

---

# Storage Optimized Capacity

The Maarek course traditionally highlights roughly:

**80 TB of usable storage**

for Snowball Edge Storage Optimized data-transfer workloads.

For the exam, the stronger concept is:

> **Storage Optimized is the Snowball Edge choice when storage capacity and large data transfer are the priority.**

---

# Storage Optimized Use Cases

Think:

- Hundreds of TB to migrate
- Large file collections
- Data-center migration
- Storage-heavy remote workload
- Physical offline transfer

### Exam Pattern

> **"A company needs to transfer a very large dataset to AWS and network bandwidth is insufficient."**
>
> → **Snowball Edge Storage Optimized**

---

# Snowball Edge Compute Optimized

[[Snowball Edge Compute Optimized]] emphasizes:

**Compute resources**

It is designed for:

- Edge processing
- Machine learning inference
- Data analysis
- Video processing
- Remote compute workloads

### Memory Trick

**Compute Optimized = More CPU**

---

# Compute Optimized Use Cases

Imagine:

Remote Industrial Site  
↓  
Cameras / Sensors  
↓  
Snowball Edge Compute Optimized  
↓  
Local Processing  
↓  
Results Sent to AWS Later

This allows workloads to continue even when:

**Connectivity is intermittent**

---

# Storage Optimized vs Compute Optimized

| Requirement | Storage Optimized | Compute Optimized |
|---|---:|---:|
| Large Data Migration | ✅ | Possible |
| Maximum Storage Focus | ✅ | ❌ |
| Edge Compute Focus | Limited / Secondary | ✅ |
| Data Collection | ✅ | ✅ |
| Heavy Local Processing | ❌ | ✅ |
| Video Processing | Less Ideal | ✅ |
| ML Inference | Less Ideal | ✅ |

### Memory Trick

**Need space?**
→ Storage Optimized

**Need horsepower?**
→ Compute Optimized

---

# Offline Data Transfer

Snowball Edge is particularly useful when:

**Network transfer would take too long**

Architecture:

Data Center  
↓  
Copy Data onto Snowball Edge  
↓  
Ship Device  
↓  
AWS  
↓  
Import Data

This avoids trying to push an enormous dataset through:

**A limited network connection**

---

# Migration Process

A typical Snowball Edge migration looks like:

1. Order Snowball Edge
2. AWS ships the device
3. Connect it to the local network
4. Copy data onto the device
5. Ship the device back
6. AWS imports the data
7. Device data is securely erased

---

# Import into S3

For migration workloads, data can ultimately be imported into:

[[S3]]

Architecture:

On-Premises Data  
↓  
Snowball Edge  
↓  
Physical Shipment  
↓  
AWS  
↓  
S3

### Exam Pattern

> **Large offline migration → S3**
>
> → **Snowball Edge**

---

# Edge Computing

Snowball Edge can run:

**Compute workloads locally**

at the edge.

This is valuable when:

- Connectivity is poor
- Latency to an AWS Region is too high
- Data must be processed locally
- Sending all raw data to AWS is impractical

---

# EC2-Compatible Compute

Snowball Edge supports:

**EC2-compatible compute instances**

at the edge.

Conceptually:

Application  
↓  
EC2-Compatible Instance  
↓  
Snowball Edge Hardware

This gives developers an AWS-like compute environment:

**Outside an AWS Region**

---

# Local Processing

Instead of sending:

100% of raw data

to AWS:

Raw Data  
↓  
Snowball Edge  
↓  
Process Locally  
↓  
Keep Important Results  
↓  
Transfer to AWS

This can dramatically reduce:

**Network requirements**

---

# Edge Video Processing

Example:

Remote Site Cameras  
↓  
Generate Massive Video Streams  
↓  
Snowball Edge Compute Optimized  
↓  
Analyze Video Locally  
↓  
Send Relevant Results to AWS

### Exam Pattern

> **Remote video analytics + unreliable connectivity + substantial local compute**
>
> → **Snowball Edge Compute Optimized**

---

# Machine Learning at the Edge

Snowball Edge can also support workloads such as:

**Machine learning inference**

Architecture:

Model  
↓  
Snowball Edge  
↓  
Local Input Data  
↓  
Inference  
↓  
Result

This avoids requiring every inference request to travel to:

**An AWS Region**

---

# Disconnected Operation

Snowball Edge is designed for locations that may have:

- No internet
- Intermittent internet
- Very limited bandwidth

This makes it useful in:

- Remote industrial sites
- Ships
- Field operations
- Research locations
- Disaster-response environments

---

# Rugged Design

Snowball Edge is designed as:

**Rugged physical hardware**

It can operate outside a traditional:

**Data-center environment**

This distinguishes it from many standard AWS services that require continuous network access.

---

# Clustering

Multiple Snowball Edge devices can be:

**Clustered**

for edge workloads.

Conceptually:

Snowball Edge  
+
Snowball Edge  
+
Snowball Edge  
↓  
Edge Cluster

This can provide greater:

- Storage
- Compute
- Availability

---

# Security

Snowball Edge includes strong security features.

Important concepts include:

- Encryption
- Tamper-resistant design
- Secure data handling
- Device tracking
- Secure erasure

Data stored on the device is:

**Encrypted**

---

# KMS

Encryption can integrate with:

[[06-Security/KMS]]

for:

**Encryption key management**

### Exam Trap

Do not think:

> Physical device = unprotected hard drive.

Snowball Edge is designed for:

**Secure enterprise data migration**

---

# Snowball Edge vs Snowcone

## [[Snowcone]]

Think:

- Small
- Portable
- Lightweight
- Smaller datasets
- Smaller edge workloads

---

## Snowball Edge

Think:

- Larger
- More storage
- More compute
- Larger migrations
- More substantial edge workloads

### Memory Trick

**Snowcone = Backpack**

**Snowball Edge = Rugged server box**

---

# Snowball Edge vs DataSync

## [[DataSync]]

Uses:

**Network connectivity**

Best when bandwidth is:

**Sufficient**

---

## Snowball Edge

Uses:

**Physical shipment**

Best when network bandwidth is:

**Insufficient**

### Exam Decision

100 TB + fast network + enough time  
→ DataSync

100 TB + slow network + tight deadline  
→ Snowball Edge

---

# Snowball Edge vs Storage Gateway

## [[Storage Gateway]]

Provides:

**Ongoing hybrid storage access**

---

## Snowball Edge

Provides:

- Offline migration
- Edge storage
- Edge compute

### Memory Trick

**Gateway = Bridge**

**Snowball = Box**

---

# Snowball Edge vs AWS Transfer Family

## [[AWS Transfer Family]]

Uses:

- SFTP
- FTPS
- FTP

over:

**Network connections**

---

## Snowball Edge

Moves data through:

**Physical transportation**

### Exam Decision

Daily SFTP uploads  
→ Transfer Family

Huge one-time offline migration  
→ Snowball Edge

---

# Snowball Edge vs Direct Connect

## [[05-Networking/Direct Connect]]

Provides:

**Dedicated network connectivity**

Best for:

**Ongoing connectivity requirements**

---

## Snowball Edge

Provides:

**Physical offline transfer**

Best for:

**Large migration where network transfer is impractical**

### Exam Thinking

If the company needs:

**Long-term hybrid connectivity**

→ Direct Connect

If the company needs:

**One-time huge migration**

→ Snowball Edge may be better.

---

# Snowball Edge vs Snowmobile

## Snowball Edge

Think:

**Large physical device**

for:

Large migrations

---

## [[Snowmobile]]

Classic course material:

**Truck/container-scale migration**

for:

Extremely massive datasets

### Memory Trick

**SnowBALL = Big**

**SnowMOBILE = Massive**

---

# Migration Time Reasoning

Always compare:

**Dataset Size**

against:

**Available Network Bandwidth**

Example:

200 TB Dataset  
↓  
100 Mbps Network

This could take:

**Months**

under idealized conditions.

If the migration deadline is:

**Two weeks**

network transfer is not practical.

Think:

**Snowball Edge**

---

# Architecture Thinking

## Scenario 1 — 200 TB Migration

A company must move:

200 TB

to AWS.

Its network connection is slow and the migration must finish quickly.

**Choose → Snowball Edge Storage Optimized**

---

## Scenario 2 — Remote Factory

A factory has:

- Poor connectivity
- Cameras
- Sensor data
- Local analytics requirements

It needs substantial compute power.

**Choose → Snowball Edge Compute Optimized**

---

## Scenario 3 — Remote Data Collection

A remote location generates large amounts of data.

The data must be stored locally until the device can be physically returned.

**Choose → Snowball Edge**

---

## Scenario 4 — Small Portable Requirement

A field worker needs the smallest possible rugged AWS edge device.

Do NOT choose Snowball Edge.

Choose:

[[Snowcone]]

---

## Scenario 5 — Nightly Synchronization

A company needs to transfer changed files to S3 every night.

It has good network connectivity.

Do NOT choose Snowball Edge.

Choose:

[[DataSync]]

---

## Scenario 6 — Ongoing Hybrid Storage

An on-premises application needs continuous access to AWS-backed storage.

Do NOT choose Snowball Edge.

Choose:

[[Storage Gateway]]

---

# Scenario Recognition

Immediately think:

[[Snowball Edge]]

when you see:

- Large offline migration
- Physical AWS device
- Poor bandwidth
- Hundreds of TB
- Edge computing
- Remote processing
- Disconnected location
- Storage Optimized
- Compute Optimized
- Rugged hardware

---

## Immediately Think Storage Optimized When You See

- Data migration
- Large dataset
- Maximum storage
- Storage-heavy workload

---

## Immediately Think Compute Optimized When You See

- Local compute
- Video processing
- ML inference
- Edge analytics
- CPU-intensive workload

---

# Exam Traps

## Trap 1 — Snowball Edge Requires Continuous Internet

False.

It is designed for:

**Disconnected or limited-connectivity environments**

---

## Trap 2 — Snowball Edge Is Only for Data Migration

False.

It can also perform:

**Edge computing**

---

## Trap 3 — Storage Optimized Is the Best Choice for Compute-Intensive Edge Processing

Not usually.

Think:

**Compute Optimized**

---

## Trap 4 — Compute Optimized Is Primarily Chosen for Maximum Storage Capacity

False.

Think:

**Compute power**

---

## Trap 5 — Snowball Edge Is Best for Recurring Nightly Transfers

False.

Think:

[[DataSync]]

---

## Trap 6 — Snowball Edge Provides Continuous Hybrid Storage Access

False.

Think:

[[Storage Gateway]]

---

## Trap 7 — Snowball Edge Is the Smallest Snow Device

False.

That is:

[[Snowcone]]

---

# Quick Cheat Sheet

| Requirement | Best Choice |
|---|---|
| Large Offline Migration | Snowball Edge |
| Hundreds of TB | Snowball Edge |
| Storage-Focused Migration | Storage Optimized |
| Heavy Edge Compute | Compute Optimized |
| ML Inference at Edge | Compute Optimized |
| Video Analytics at Edge | Compute Optimized |
| Poor Connectivity | Snowball Edge |
| Disconnected Operation | Snowball Edge |
| Smallest Portable Device | Snowcone |
| Online Scheduled Transfer | DataSync |
| Ongoing Hybrid Storage | Storage Gateway |

---

## Master Memory Trick

> [!tip] Master Memory Trick
> Imagine AWS gives you a rugged server in a shipping box.
>
> You can:
>
> **LOAD DATA ON IT**
> → Ship it to AWS
>
> or:
>
> **RUN COMPUTE ON IT**
> → Process data at the edge

Then ask:

> **WHAT MATTERS MORE?**

If:

> **DATA CAPACITY**
>
> → **STORAGE OPTIMIZED**

If:

> **COMPUTE POWER**
>
> → **COMPUTE OPTIMIZED**

And remember:

> **Snowcone**
> → Small + Portable
>
> **Snowball Edge**
> → Large + Powerful
>
> **Snowmobile**
> → Massive

Finally:

> **GOOD NETWORK**
> → [[DataSync]]
>
> **BAD NETWORK + HUGE DATA**
> → **Snowball Edge**
>
> **ONGOING HYBRID ACCESS**
> → [[Storage Gateway]]

---

## Related Notes

- [[Snow Family]]
- [[Snowcone]]
- [[Snowball Edge Storage Optimized]]
- [[Snowball Edge Compute Optimized]]
- [[Snowmobile]]
- [[DataSync]]
- [[Storage Gateway]]
- [[S3]]
- [[06-Security/KMS]]
- [[05-Networking/Direct Connect]]
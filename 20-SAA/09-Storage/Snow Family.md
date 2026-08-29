## What Problem Does It Solve?

[[Snow Family]] helps move very large amounts of data into or out of AWS when transferring everything over the network would be:

- Too slow
- Too expensive
- Unreliable
- Limited by available bandwidth

It can also provide:

**Edge computing capabilities**

in locations with limited or no connectivity.

It solves the problem of:

> **"How do I move huge datasets when the network isn't practical?"**

Think:

On-Premises Data  
↓  
AWS Snow Device  
↓  
Physical Shipment  
↓  
AWS  
↓  
Data Imported into AWS

> [!tip] Memory Trick
> **Snow = Ship the data instead of sending it over the network**

---

# What Is the Snow Family?

The AWS Snow Family consists of:

**Highly secure portable devices**

used for:

- Data migration
- Edge computing

For SAA, the major Snow devices are:

- [[Snowcone]]
- [[Snowball Edge]]

Historically, you may also encounter:

**Snowmobile**

in course material and exam-prep comparisons.

---

# Two Major Snow Family Uses

## Data Migration

Use Snow devices to:

**Physically transport data**

between:

On-Premises  
and  
AWS

---

## Edge Computing

Snow devices can also run:

**Compute workloads at the edge**

where normal AWS Region connectivity may be:

- Limited
- Intermittent
- Unavailable

Examples:

- Factories
- Ships
- Remote research sites
- Mining operations
- Disaster zones

### Memory Trick

**Snow = MOVE + EDGE**

---

# Why Physical Data Transfer?

Suppose a company needs to transfer:

**500 TB**

to AWS.

Using the network could take:

- Weeks
- Months
- Longer

depending on bandwidth.

Instead:

Data  
↓  
Snow Device  
↓  
Ship Device  
↓  
AWS  
↓  
Import Data

Sometimes the fastest network is:

**A delivery truck.**

---

# Bandwidth Problem

A key exam calculation is:

> **How long would the transfer take over the available network?**

If the answer is:

**Too long for the business requirement**

consider:

[[Snow Family]]

---

# Snowcone

[[Snowcone]] is the:

**Smallest Snow Family device**

It is designed to be:

- Small
- Portable
- Rugged
- Suitable for edge computing
- Suitable for smaller data-transfer jobs

> [!tip] Memory Trick
> **SnowCONE = Small cone, small Snow device**

---

# Snowcone Storage

The Maarek course commonly highlights Snowcone as having roughly:

**8 TB usable HDD storage**

with SSD-based variants also associated with the Snowcone family.

For exam reasoning, the more important concept is:

> **Snowcone = smallest and most portable Snow option**

---

# Snowcone Use Cases

Think:

- Smaller migrations
- Remote locations
- Portable edge computing
- Limited physical space
- Harsh environments

Example:

Remote Research Site  
↓  
Snowcone  
↓  
Collect / Process Data  
↓  
Ship or Transfer Data to AWS

---

# Snowcone + DataSync

Snowcone can work with:

[[DataSync]]

to transfer data back to AWS over the network when connectivity is available.

Architecture:

Edge Data  
↓  
Snowcone  
↓  
DataSync  
↓  
AWS

This provides flexibility:

**Ship the device**

or:

**Transfer over the network**

depending on circumstances.

---

# Snowball Edge

[[Snowball Edge]] is a larger Snow Family device designed for:

- Large-scale data migration
- Edge storage
- Edge computing

Think:

**More storage and compute than Snowcone**

---

# Snowball Edge Device Types

The Maarek course distinguishes between:

- Snowball Edge Storage Optimized
- Snowball Edge Compute Optimized

The names tell you what each emphasizes.

---

# Snowball Edge Storage Optimized

Designed primarily for:

**Large-scale data transfer and storage**

Think:

Large Dataset  
↓  
Snowball Edge Storage Optimized  
↓  
Ship to AWS

### Memory Trick

**Storage Optimized = Move lots of data**

---

# Snowball Edge Compute Optimized

Designed for:

**Edge computing workloads**

It provides stronger compute capabilities for workloads that need processing:

**Away from an AWS Region**

### Memory Trick

**Compute Optimized = Run more compute at the edge**

---

# Edge Computing

Edge computing means processing data:

**Close to where the data is generated**

instead of always sending it to an AWS Region first.

Architecture:

Sensors / Cameras / Machines  
↓  
Snow Device  
↓  
Local Processing  
↓  
Results / Data  
↓  
AWS Later

---

# Why Edge Computing Matters

Imagine an oil platform with:

**Poor internet connectivity**

Sensors continuously generate data.

Instead of:

Sensor  
↓  
Slow Internet  
↓  
AWS Region  
↓  
Process

Use:

Sensor  
↓  
Snowball Edge  
↓  
Process Locally  
↓  
Send Results Later

This reduces dependency on:

**Continuous network connectivity**

---

# EC2 and Lambda at the Edge

Snow Family edge devices can support AWS-style compute capabilities such as:

- EC2-compatible compute
- Lambda-style local processing capabilities in applicable Snow environments

The exam takeaway is:

> **Snow devices can do more than move data — they can process data at the edge.**

---

# Snowball Edge Clustering

Multiple Snowball Edge devices can be used together for:

**Larger edge environments**

This can increase:

- Storage
- Compute
- Resilience

Think:

Snowball Edge  
+
Snowball Edge  
+
Snowball Edge  
↓  
Edge Cluster

---

# Snowmobile

[[Snowmobile]] is historically described as:

**A massive physical data-transfer solution**

implemented using a:

**Shipping container / truck-scale system**

It is intended for:

**Extremely large migrations**

Think:

**Exabyte-scale data**

> [!tip] Memory Trick
> **SnowCONE → Small**
>
> **SnowBALL → Big**
>
> **SnowMOBILE → Absolutely ridiculous amounts of data**

---

# Snowmobile Scale

Classic AWS exam material associates Snowmobile with migrations up to approximately:

**100 PB per Snowmobile**

The main exam takeaway:

> **Massive data-center migration at extreme scale**
>
> → Snowmobile

---

# Snow Family Scale Thinking

Conceptually:

Smaller / Portable  
↓  
Snowcone

Large Migration  
↓  
Snowball Edge

Extreme Data Center Migration  
↓  
Snowmobile

### Memory Trick

**Cone → Ball → Mobile**

Small → Large → Massive

---

# Snow Family Data Migration Process

A typical Snow migration follows:

1. Request the Snow device
2. AWS ships the device
3. Connect it to the local environment
4. Copy data onto the device
5. Ship the device back
6. AWS imports the data
7. Device data is securely erased

Architecture:

Customer  
↓  
Load Data  
↓  
Ship  
↓  
AWS  
↓  
Import  
↓  
Secure Erasure

---

# Security

Snow Family devices are designed with strong security controls.

Important concepts include:

- Encryption
- Tamper resistance
- AWS-managed security
- Secure erase after use

Data stored on Snow devices is:

**Encrypted**

---

# KMS

Snow Family encryption can integrate with:

[[06-Security/KMS]]

for encryption-key management.

### Exam Thinking

Physical device does NOT mean:

**Unencrypted portable hard drive**

Snow devices are designed for:

**Secure enterprise data transfer**

---

# Tracking

Because the device physically moves between:

Customer  
and  
AWS

tracking and chain-of-custody considerations are important.

AWS provides mechanisms to help track:

**Snow devices during shipment**

---

# Import and Export

Snow Family can support:

**Importing data into AWS**

and certain workflows for:

**Exporting data from AWS**

The strongest SAA pattern is usually:

**Large on-premises migration → AWS**

---

# Snow Family vs DataSync

This is one of the most important comparisons.

## [[DataSync]]

Uses:

**Network**

Best when:

- Bandwidth is sufficient
- Online transfer is practical
- Scheduled synchronization is required

---

## Snow Family

Uses:

**Physical devices**

Best when:

- Network is too slow
- Dataset is huge
- Transfer deadline cannot be met online

### Memory Trick

**DataSync = Network movers**

**Snow = Physical movers**

---

# Snow Family vs Storage Gateway

## [[Storage Gateway]]

Provides:

**Ongoing hybrid storage access**

---

## Snow Family

Provides:

**Data migration and edge computing**

### Exam Decision

Keep using AWS storage from on-premises  
→ Storage Gateway

Move enormous dataset offline  
→ Snow Family

---

# Snow Family vs AWS Transfer Family

## [[AWS Transfer Family]]

Provides:

- SFTP
- FTPS
- FTP

over:

**Network connections**

---

## Snow Family

Provides:

**Physical data transfer**

### Exam Decision

Business partners uploading files daily  
→ Transfer Family

500 TB migration with poor bandwidth  
→ Snowball Edge

---

# Snow Family vs Direct Connect

## [[05-Networking/Direct Connect]]

Provides:

**Dedicated network connectivity**

---

## Snow Family

Provides:

**Physical data transfer**

For a one-time migration, installing Direct Connect solely for the migration may not always be the fastest or most cost-effective option.

### Exam Thinking

Ask:

- One-time or ongoing?
- How much data?
- How much bandwidth?
- What is the deadline?

---

# Migration Time Calculation

You should be able to reason about whether a network transfer is practical.

Formula:

**Transfer Time = Data Size / Network Throughput**

---

# Example

Suppose:

Data:

**100 TB**

Network:

**100 Mbps**

Approximate calculation:

100 TB  
≈ 800,000,000 Mb

800,000,000 Mb  
÷  
100 Mb/s

≈ 8,000,000 seconds

≈ 92 days

And that assumes:

**Perfect utilization**

Real-world transfer could take longer.

### Exam Conclusion

If the company needs migration completed in:

**One week**

the network is clearly insufficient.

Think:

[[Snowball Edge]]

---

# When NOT to Use Snow

Do not automatically choose Snow whenever the dataset is large.

If the company has:

- High-bandwidth connectivity
- Direct Connect
- Enough transfer time
- Ongoing synchronization requirements

then:

[[DataSync]]

may be more appropriate.

---

# Architecture Thinking

## Scenario 1 — 500 TB Migration

A company needs to migrate:

500 TB

from its data center to AWS.

Its internet connection is slow and the migration must finish quickly.

**Choose → Snowball Edge**

---

## Scenario 2 — Small Remote Edge Site

A remote field location has:

- Limited space
- Poor connectivity
- Local processing requirements

**Choose → Snowcone**

---

## Scenario 3 — Edge Video Processing

A remote industrial site generates large amounts of video.

Internet connectivity is unreliable.

Video must be processed locally.

**Choose → Snowball Edge Compute Optimized**

---

## Scenario 4 — Large Storage Migration

A company needs a physical device primarily to move a very large dataset.

**Choose → Snowball Edge Storage Optimized**

---

## Scenario 5 — Massive Data Center Migration

A company historically needs to migrate an enormous multi-petabyte/exabyte-scale dataset.

Classic exam material may point toward:

**Snowmobile**

---

## Scenario 6 — Nightly Synchronization

A company needs to synchronize changed files to S3:

**Every night**

It has sufficient network bandwidth.

Do NOT choose Snow.

Choose:

[[DataSync]]

---

## Scenario 7 — Continuous Hybrid Storage

An on-premises application needs ongoing NFS access to S3.

Do NOT choose Snow.

Choose:

[[S3 File Gateway]]

---

# Scenario Recognition

Immediately think:

[[Snow Family]]

when you see:

- Offline migration
- Physical device
- Huge dataset
- Limited bandwidth
- Migration deadline
- Remote location
- Edge computing
- Disconnected environment
- Rugged device

---

## Immediately Think Snowcone When You See

- Smallest device
- Portable
- Limited space
- Smaller migration
- Remote edge location

---

## Immediately Think Snowball Edge When You See

- Hundreds of TB
- Large migration
- Edge computing
- Storage Optimized
- Compute Optimized

---

## Think Snowmobile in Classic Material When You See

- Exabyte scale
- Entire data center
- Extreme migration scale
- Truck/container-scale transfer

---

# Exam Traps

## Trap 1 — Snow Family Requires Fast Internet

False.

One of its biggest purposes is solving:

**Network bandwidth limitations**

---

## Trap 2 — Snow Devices Only Transfer Data

False.

Snow devices can also support:

**Edge computing**

---

## Trap 3 — Snowball Edge and DataSync Are the Same

False.

DataSync:

**Network transfer**

Snowball:

**Physical transfer**

---

## Trap 4 — Snowcone Is the Largest Snow Device

False.

Snowcone is:

**Small and portable**

---

## Trap 5 — Snowball Edge Compute Optimized Is Primarily About Maximum Storage

No.

Its major clue is:

**Edge compute**

---

## Trap 6 — Snowball Edge Storage Optimized Is Primarily About Compute

No.

Its major clue is:

**Storage / data migration**

---

## Trap 7 — Snow Family Provides Ongoing Hybrid File Access

False.

Think:

[[Storage Gateway]]

for ongoing hybrid storage.

---

## Trap 8 — Snowball Is Best for Nightly File Synchronization

False.

Think:

[[DataSync]]

---

# Quick Cheat Sheet

| Requirement | Best Choice |
|---|---|
| Small / Portable Snow Device | Snowcone |
| Large Offline Migration | Snowball Edge |
| Storage-Focused Snowball | Storage Optimized |
| Edge Processing | Compute Optimized |
| Extreme Classic Migration | Snowmobile |
| Limited Network | Snow Family |
| Offline Transfer | Snow Family |
| Edge Computing | Snow Family |
| Scheduled Online Transfer | DataSync |
| Ongoing Hybrid Storage | Storage Gateway |
| SFTP / FTPS / FTP | Transfer Family |

---

# Migration Decision Table

| Scenario | Best Choice |
|---|---|
| 100 TB + Good Network | DataSync |
| 100 TB + Poor Network | Snowball Edge |
| Recurring NFS → S3 | DataSync |
| Continuous NFS Access to S3 | S3 File Gateway |
| SFTP Partner Upload | Transfer Family |
| Remote Edge Compute | Snowcone / Snowball Edge |
| Massive Offline Migration | Snow Family |

---

## Master Memory Trick

> [!tip] Master Memory Trick
> Imagine your network pipe is tiny, but your dataset is enormous.
>
> Trying to push everything through the pipe would take months.
>
> AWS says:
>
> **"Don't send the data through the internet. Put it in a box."**
>
> Then:
>
> **Snowcone**
> → Small box
>
> **Snowball Edge**
> → Big box
>
> **Snowmobile**
> → Basically the whole truck

For the exam:

> **GOOD NETWORK**
>
> → [[DataSync]]
>
> **BAD NETWORK + HUGE DATA**
>
> → [[Snow Family]]
>
> **ONGOING HYBRID ACCESS**
>
> → [[Storage Gateway]]

And remember:

> **Snow = MOVE + EDGE**

---

## Related Notes

- [[Snowcone]]
- [[Snowball Edge]]
- [[Snowmobile]]
- [[DataSync]]
- [[Storage Gateway]]
- [[S3 File Gateway]]
- [[AWS Transfer Family]]
- [[S3]]
- [[06-Security/KMS]]
- [[05-Networking/Direct Connect]]
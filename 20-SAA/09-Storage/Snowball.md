## What Problem Does It Solve?

[[Snowball]] helps move very large amounts of data into or out of AWS when transferring everything over the network would be:

- Too slow
- Too expensive
- Unreliable
- Limited by bandwidth

It solves the problem of:

> **"How can I migrate terabytes or petabytes of data when the network connection is not practical?"**

Instead of:

On-Premises Data  
↓  
Internet  
↓  
Days / Months / Years  
↓  
AWS

you can use:

On-Premises Data  
↓  
Snowball Device  
↓  
Physically Ship Device  
↓  
AWS  
↓  
Import Data

> [!tip] Memory Trick
> **Snowball = Ship the data instead of sending it**

---

## What Is Snowball?

Snowball uses:

**Highly secure portable devices**

that can be used to:

- Collect data
- Process data at the edge
- Migrate data into AWS
- Migrate data out of AWS

The Maarek slides emphasize that Snowball can help migrate:

**Up to petabytes of data**

---

# Why Snowball Exists

Network transfer becomes difficult when datasets get extremely large.

Challenges include:

- Limited connectivity
- Limited bandwidth
- High network costs
- Shared bandwidth
- Connection instability

Architecture:

Large Dataset  
↓  
Limited Network  
↓  
Transfer Takes Too Long

Snowball solves this through:

**Offline physical data transfer**

---

# The One-Week Rule

This is one of the strongest Maarek exam rules.

> [!tip] Exam Rule
> **If transferring the data over the network would take more than one week, consider Snowball.**

Think:

Network Transfer  
↓  
More Than 1 Week  
↓  
[[Snowball]]

### Memory Trick

**More than a week? Ship it.**

---

# Why Large Network Transfers Can Be Impractical

The Maarek slides provide examples showing how transfer time grows quickly.

For example:

10 TB over 100 Mbps  
↓  
Approximately 12 days

100 TB over 1 Gbps  
↓  
Approximately 12 days

1 PB over 1 Gbps  
↓  
Approximately 124 days

The exact numbers matter less than the exam lesson:

> **Huge dataset + limited bandwidth = Snowball**

---

# Snowball Migration Architecture

## Direct Network Upload

Client  
↓  
Internet / Direct Connection  
↓  
[[S3]]

This may work well for manageable data volumes.

---

## Snowball Migration

Client  
↓  
Copy Data to Snowball  
↓  
Ship Snowball  
↓  
AWS  
↓  
Data Imported into S3

### Architecture Thinking

Snowball turns:

**Network transfer**

into:

**Physical transfer**

---

# Snowball Edge

The Maarek slides focus on:

**Snowball Edge**

Snowball Edge combines:

**Storage**

with:

**Compute capabilities**

This means the device can do more than simply move data.

---

# Snowball Edge Storage Optimized

[[Snowball Edge Storage Optimized]]

is designed for workloads that emphasize:

**Large storage capacity**

The Maarek slides show:

- 104 vCPUs
- 416 GB memory
- 210 TB storage

### Best Fit

Think:

- Large-scale migration
- Large storage requirements
- Edge storage
- Data collection

### Memory Trick

**Storage Optimized = More disk**

---

# Snowball Edge Compute Optimized

[[Snowball Edge Compute Optimized]]

focuses more heavily on:

**Edge computing workloads**

The Maarek slides show:

- 104 vCPUs
- 416 GB memory
- 28 TB storage

### Best Fit

Think:

- Compute at remote locations
- Data preprocessing
- Machine learning
- Media transcoding

### Memory Trick

**Compute Optimized = More focus on processing**

---

# Storage Optimized vs Compute Optimized

| Requirement | Best Choice |
|---|---|
| Maximum Snowball storage capacity | Storage Optimized |
| Large migration workload | Storage Optimized |
| Edge computing | Compute Optimized |
| Preprocess data at edge | Compute Optimized |
| Machine learning at edge | Compute Optimized |
| Media transcoding | Compute Optimized |

---

# Edge Computing

Snowball Edge is not only a migration device.

It can also perform:

**Edge Computing**

Edge Computing means:

> **Process data close to where the data is being generated.**

Examples from the Maarek slides include:

- Truck on the road
- Ship at sea
- Mining station underground

These environments may have:

- Limited internet connectivity
- No nearby compute infrastructure

---

# Edge Computing Architecture

Remote Location  
↓  
Data Generated  
↓  
Snowball Edge  
↓  
Process Data Locally  
↓  
Store Results  
↓  
Eventually Transfer to AWS

This reduces dependence on a constant internet connection.

> [!tip] Memory Trick
> **Edge Computing = Process HERE, not somewhere far away**

---

# Compute at the Edge

Snowball Edge can run compute workloads locally.

The Maarek slides highlight:

- [[EC2]] instances
- [[02-Compute/Lambda]] functions

Architecture:

Remote Sensors  
↓  
Snowball Edge  
↓  
EC2 / Lambda  
↓  
Process Data Locally

This is useful when:

**Cloud connectivity is limited or unavailable**

---

# Edge Computing Use Cases

The Maarek slides explicitly highlight:

- Data preprocessing
- Machine learning
- Media transcoding

---

## Data Preprocessing

Example:

Remote Sensors  
↓  
Generate Huge Raw Dataset  
↓  
Snowball Edge  
↓  
Filter / Clean Data  
↓  
Transfer Only Useful Data

This can reduce:

**Network transfer volume**

---

## Machine Learning

Example:

Remote Camera  
↓  
Image Data  
↓  
Snowball Edge  
↓  
Local ML Processing  
↓  
Result

Useful when sending every raw data point to AWS is impractical.

---

## Media Transcoding

Example:

Remote Production Site  
↓  
Video Files  
↓  
Snowball Edge  
↓  
Transcode Locally

This provides local compute where normal cloud connectivity may be poor.

---

# Snowball Import to S3

The standard migration architecture is:

On-Premises  
↓  
Snowball  
↓  
AWS  
↓  
[[S3]]

S3 commonly becomes the first AWS storage destination for imported data.

---

# Snowball Cannot Import Directly into Glacier

This is a classic exam trap.

Snowball cannot directly import data into:

**Glacier**

Instead:

Snowball  
↓  
[[S3]]  
↓  
[[S3 Lifecycle Rules]]  
↓  
Glacier Storage Class

> [!warning] Exam Rule
> **Snowball → S3 → Lifecycle → Glacier**

NOT:

**Snowball → Glacier directly**

---

# Glacier Migration Architecture

Correct:

Snowball  
↓  
S3 Standard  
↓  
Lifecycle Policy  
↓  
[[S3 Glacier Flexible Retrieval]]

or:

[[S3 Glacier Deep Archive]]

depending on the retention requirement.

### Memory Trick

**Snowball always stops at S3 before Glacier**

---

# Snowball vs Network Transfer

## Network Transfer

Best when:

- Dataset is manageable
- High-bandwidth connection exists
- Transfer completes reasonably quickly

---

## Snowball

Best when:

- Massive data volume
- Limited bandwidth
- Network transfer takes over a week
- Network connection is unreliable
- Network costs are excessive

---

# Snowball vs Direct Connect

[[05-Networking/Direct Connect]] provides:

**Dedicated network connectivity**

between:

On-Premises  
and  
AWS

Use Direct Connect when:

- Ongoing network connectivity is required
- Hybrid workloads continuously exchange data
- Stable dedicated bandwidth is needed

Use Snowball when:

- Migration is extremely large
- Offline transfer is faster
- Connectivity is limited

### Memory Trick

**Direct Connect = Permanent road**

**Snowball = Moving truck**

---

# Snowball vs Site-to-Site VPN

[[05-Networking/Site-to-Site VPN]] transfers data over:

**Encrypted public internet connectivity**

Good for:

- Hybrid networking
- Smaller transfers
- Ongoing communication

Snowball is better for:

**Massive offline transfer**

---

# Snowball vs S3 Transfer Acceleration

[[S3 Transfer Acceleration]] improves network transfer speed using:

**AWS Edge Locations**

But the transfer still happens:

**Over the network**

Snowball instead:

**Physically ships the data**

### Exam Decision

Large transfer but network is still practical  
→ Transfer Acceleration

Network transfer would take weeks/months  
→ Snowball

---

# Snowball vs DataSync

[[DataSync]] automates:

**Online data transfer**

between storage systems and AWS.

Think:

Network-based migration

Snowball:

**Offline physical migration**

### Memory Trick

**DataSync = Send it**

**Snowball = Ship it**

---

# Architecture Thinking

## Scenario 1 — 500 TB Migration

A company must migrate:

500 TB

from its data center to AWS.

Its available network connection would take several months.

**Choose → Snowball**

---

## Scenario 2 — Limited Remote Connectivity

A mining operation generates large amounts of data underground.

Internet connectivity is unreliable.

Data must be processed locally before later uploading to AWS.

**Choose → Snowball Edge**

---

## Scenario 3 — Media Processing on a Ship

A ship generates large video files.

The files need transcoding while at sea with poor connectivity.

**Choose → Snowball Edge Compute Optimized**

---

## Scenario 4 — Archive Data into Glacier

A company wants to migrate hundreds of TB of archival data into Glacier.

Can Snowball send directly to Glacier?

**No.**

Architecture:

Snowball  
↓  
[[S3]]  
↓  
[[S3 Lifecycle Rules]]  
↓  
Glacier

---

## Scenario 5 — Continuous Hybrid Connectivity

A company continuously transfers data between its data center and AWS.

The requirement is not a one-time massive migration.

**Do NOT choose Snowball automatically**

Consider:

[[05-Networking/Direct Connect]]

or:

[[DataSync]]

depending on the architecture.

---

# Scenario Recognition

## Immediately Think Snowball When You See

- Petabytes
- Hundreds of TB
- Offline migration
- Physical appliance
- Ship device to AWS
- Limited bandwidth
- Network transfer takes weeks
- Network transfer takes months
- More than one week
- Edge computing
- Remote site
- Poor connectivity

### Strongest Exam Pattern

> **"Network transfer would take more than one week."**
>
> → **Snowball**

---

# Exam Traps

## Trap 1 — Snowball Is Only for Data Migration

False.

Snowball Edge can also provide:

**Edge computing**

---

## Trap 2 — Snowball Requires Constant Internet Connectivity

False.

One of its major use cases is:

**Limited or unreliable connectivity**

---

## Trap 3 — Snowball Can Import Directly into Glacier

False.

Use:

Snowball  
↓  
S3  
↓  
Lifecycle  
↓  
Glacier

---

## Trap 4 — Snowball Is Best for Every Large File

False.

If network transfer is fast enough:

Use normal online transfer methods.

The strong Maarek rule is:

**More than one week → Snowball**

---

## Trap 5 — Snowball Edge Cannot Run Compute

False.

It can run:

- EC2 instances
- Lambda functions

at the edge.

---

## Trap 6 — Storage Optimized and Compute Optimized Are Identical

False.

Storage Optimized prioritizes:

**Storage capacity**

Compute Optimized focuses on:

**Edge processing**

---

## Trap 7 — Snowball Is an Ongoing Dedicated Network Connection

False.

That sounds more like:

[[05-Networking/Direct Connect]]

Snowball is:

**Physical data transfer / edge device**

---

# Quick Cheat Sheet

| Requirement | Best Choice |
|---|---|
| Massive Offline Migration | Snowball |
| Petabyte Migration | Snowball |
| Transfer Takes More Than Week | Snowball |
| Limited Bandwidth | Snowball |
| High Network Cost | Snowball |
| Connection Unstable | Snowball |
| Edge Computing | Snowball Edge |
| Maximum Device Storage | Storage Optimized |
| Edge Processing | Compute Optimized |
| Run EC2 at Edge | Snowball Edge |
| Run Lambda at Edge | Snowball Edge |
| Preprocess Data | Snowball Edge |
| Machine Learning at Edge | Snowball Edge |
| Media Transcoding | Snowball Edge |
| Import Directly into Glacier | ❌ |
| Glacier Migration | Snowball → S3 → Lifecycle |
| Continuous Dedicated Network | Direct Connect |

---

## Master Memory Trick

> [!tip] Master Memory Trick
> **Snowball = AWS Moving Truck**
>
> If sending the data through the internet is too slow:
>
> **Load the truck**
>
> → Snowball
>
> **Ship the truck**
>
> → AWS
>
> **Unload into the warehouse**
>
> → S3

For edge computing:

> **Snowball Edge = Moving truck with a computer inside**

Remember:

**More than one week**
→ Snowball

**Need lots of storage**
→ Storage Optimized

**Need local processing**
→ Compute Optimized

**Need Glacier**
→ Snowball → S3 → Lifecycle → Glacier

---

## Related Notes

- [[S3]]
- [[S3 Lifecycle Rules]]
- [[S3 Glacier Flexible Retrieval]]
- [[S3 Glacier Deep Archive]]
- [[S3 Transfer Acceleration]]
- [[DataSync]]
- [[05-Networking/Direct Connect]]
- [[05-Networking/Site-to-Site VPN]]
- [[EC2]]
- [[02-Compute/Lambda]]
- [[Snowball Edge Storage Optimized]]
- [[Snowball Edge Compute Optimized]]
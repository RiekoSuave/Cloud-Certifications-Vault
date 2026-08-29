## What Problem Does It Solve?

[[FSx for Lustre]] provides a fully managed, high-performance parallel file system for workloads that need extremely fast shared storage.

It solves the problem of:

> **"How can I give large-scale compute workloads very high throughput and low-latency access to shared files?"**

Think:

Compute Fleet  
↓  
Parallel File Access  
↓  
FSx for Lustre

Best for:

- Machine Learning
- High Performance Computing
- Video Processing
- Financial Modeling
- Electronic Design Automation

> [!tip] Memory Trick
> **Lustre = Linux + Cluster = Extreme Parallel Performance**

---

## What Is Lustre?

Lustre is a:

**Parallel distributed file system**

designed for:

**Large-scale computing**

The name comes from:

**Linux + Cluster**

Architecture:

Many Compute Nodes  
↓ ↓ ↓ ↓ ↓  
FSx for Lustre  
↓  
Shared High-Performance File System

---

## Why Lustre Is Different

[[EFS]] provides general-purpose shared Linux storage.

Lustre is designed for workloads that need:

- Massive throughput
- Millions of IOPS
- Very low latency
- Parallel access from many compute nodes

The Maarek slides highlight performance scaling to:

- Hundreds of GB/s
- Millions of IOPS
- Sub-millisecond latency

### Memory Trick

**Normal Linux sharing → EFS**

**Extreme Linux performance → Lustre**

---

## Core Use Cases

The Maarek slides specifically highlight:

- Machine Learning
- High Performance Computing
- Video Processing
- Financial Modeling
- Electronic Design Automation

### Scenario Recognition

If the question says:

> **"Hundreds of compute instances must process a shared dataset at extremely high speed."**

Think:

[[FSx for Lustre]]

---

## Machine Learning

Example:

Large Dataset  
↓  
FSx for Lustre  
↓  
Many ML Training Instances  
↓  
Parallel Reads

Lustre helps provide the throughput needed to feed compute-intensive training workloads.

---

## High Performance Computing

HPC workloads often divide a computation across:

**Many compute instances**

Those instances may need simultaneous access to:

**The same large dataset**

Architecture:

EC2 Compute Cluster  
↓  
Parallel File Access  
↓  
FSx for Lustre

> [!tip] Exam Pattern
> **HPC + Shared High-Performance Storage**
>
> → **FSx for Lustre**

---

## Lustre Storage Options

FSx for Lustre supports:

- SSD
- HDD

The workload determines which option fits best.

---

## SSD Storage

Choose:

**SSD**

for:

- Low-latency workloads
- IOPS-intensive workloads
- Small file operations
- Random file operations

### Memory Trick

**SSD = Small + Random + IOPS**

---

## HDD Storage

Choose:

**HDD**

for:

- Throughput-intensive workloads
- Large file operations
- Sequential file operations

### Memory Trick

**HDD = Large + Sequential + Throughput**

---

## SSD vs HDD

| Requirement | Best Choice |
|---|---|
| Low latency | SSD |
| High IOPS | SSD |
| Small files | SSD |
| Random file access | SSD |
| Large files | HDD |
| Sequential access | HDD |
| Throughput-heavy workload | HDD |

---

## Lustre + S3 Integration

One of the most important SAA features of FSx for Lustre is its:

**Seamless integration with [[S3]]**

Architecture:

S3 Bucket  
↕  
FSx for Lustre  
↕  
Compute Fleet

Lustre can expose S3 data through a:

**File-system interface**

---

## Read S3 as a File System

Applications can effectively:

**Read S3 data through FSx for Lustre**

Architecture:

S3 Dataset  
↓  
FSx for Lustre  
↓  
Application Sees Files  
↓  
HPC / ML Processing

This is useful because applications written to expect:

**File-system access**

can process datasets stored in:

[[S3]]

---

## Write Computation Results Back to S3

FSx for Lustre can also write output back to:

[[S3]]

Architecture:

S3 Input  
↓  
FSx for Lustre  
↓  
Compute Processing  
↓  
FSx for Lustre  
↓  
S3 Output

### Memory Trick

**S3 stores it**

**Lustre processes it fast**

---

## Strong S3 + Lustre Pattern

A classic exam architecture:

Huge Dataset in S3  
↓  
Need HPC Processing  
↓  
FSx for Lustre  
↓  
EC2 Compute Fleet

If the workload says:

> **"Data already exists in S3, but compute nodes need high-performance file access."**

Think:

[[FSx for Lustre]]

---

## On-Premises Access

FSx for Lustre can also be accessed from on-premises servers through:

- [[05-Networking/Site-to-Site VPN]]
- [[05-Networking/Direct Connect]]

Architecture:

On-Premises Compute  
↓  
VPN / Direct Connect  
↓  
FSx for Lustre

This supports hybrid HPC or data-processing architectures.

---

# Lustre Deployment Options

There are two important FSx for Lustre deployment types:

1. **Scratch**
2. **Persistent**

This is a major exam distinction.

---

## Scratch File System

Scratch is designed for:

**Temporary storage**

Characteristics:

- Data is NOT replicated
- Data does not persist if the file server fails
- Very high burst performance
- Lower-cost use case
- Intended for short-term processing

The Maarek slides highlight approximately:

**6x higher burst performance**

and:

**200 MB/s per TiB**

### Best Use Cases

- Temporary processing
- Short-lived HPC jobs
- Data that already exists elsewhere
- Cost optimization
- Intermediate computation data

> [!tip] Memory Trick
> **Scratch = Fast + Temporary + Disposable**

---

## Scratch Architecture

S3 Source Data  
↓  
Lustre Scratch  
↓  
Temporary Compute Job  
↓  
Output  
↓  
S3

If Lustre fails:

The working data may be lost.

But if the original data exists in S3:

It can be recreated.

### Architecture Thinking

Scratch is attractive when:

**Speed matters more than durability**

---

## Persistent File System

Persistent Lustre is designed for:

**Long-term storage and processing**

Characteristics:

- Data is replicated within the same AZ
- Failed file servers are replaced
- Better suited for important data
- Intended for long-running workloads

### Best Use Cases

- Long-term processing
- Sensitive data
- Important working datasets
- Workloads that cannot easily recreate data

> [!tip] Memory Trick
> **Persistent = Keep the working data**

---

## Persistent Architecture

Compute Instances  
↓  
FSx for Lustre Persistent  
↓  
Replicated Storage within AZ  
↓  
Long-Term Processing

If a file server fails:

AWS replaces it within:

**Minutes**

according to the Maarek slides.

---

## Scratch vs Persistent

| Feature | Scratch | Persistent |
|---|---:|---:|
| Temporary Storage | ✅ | ❌ |
| Long-Term Storage | ❌ | ✅ |
| Data Replicated | ❌ | ✅ |
| Data Loss on File Server Failure | Possible | Much Lower Risk |
| High Burst Performance | ✅ | Not Main Focus |
| Short-Term Processing | ✅ | ❌ |
| Sensitive Data | Poor Fit | ✅ |
| Cost Optimization | ✅ | Less Focus |

### Fast Exam Rule

**Temporary + Re-creatable data**
→ Scratch

**Important + Long-term data**
→ Persistent

---

## Scratch + S3

Scratch works especially well when S3 is the:

**Durable source of truth**

Architecture:

[[S3]]  
↓  
Scratch Lustre  
↓  
HPC Processing  
↓  
Results  
↓  
S3

If Scratch data disappears:

Recreate from:

**S3**

### Memory Trick

**S3 = Durable**

**Scratch = Fast workspace**

---

## Persistent + S3

Persistent Lustre can still integrate with S3.

But the working Lustre dataset itself is intended to be:

**Longer lived**

and more resilient than Scratch.

---

## Lustre vs EFS

These are easy to confuse because both support Linux workloads.

### [[EFS]]

Best for:

- General-purpose Linux file sharing
- NFS
- Elastic storage
- Web servers
- Application shared directories

---

### FSx for Lustre

Best for:

- HPC
- Machine learning
- Extreme throughput
- Parallel workloads
- Very low latency

### Exam Decision

**Linux shared files**
→ EFS

**Linux cluster doing extreme parallel processing**
→ Lustre

---

## Lustre vs S3

### [[S3]]

Is:

**Object Storage**

Best for:

- Durable data storage
- Data lakes
- Massive datasets
- Long-term storage

---

### Lustre

Is:

**High-performance File Storage**

Best for:

**Compute processing**

They are often:

**Used together**

### Memory Trick

**S3 = Data Lake**

**Lustre = High-Speed Workbench**

---

## Lustre vs EBS

### [[EBS]]

Provides:

**Block Storage**

typically attached to EC2 instances.

---

### Lustre

Provides:

**Shared parallel file storage**

for many compute nodes.

### Exam Pattern

> **Large compute cluster needs one shared high-performance file system**
>
> → Lustre

Not:

Individual EBS volumes

---

## Architecture Thinking

### Scenario 1 — Machine Learning Training

A company stores a multi-terabyte training dataset in S3.

Hundreds of EC2 instances need high-speed parallel access.

**Choose:**

[[S3]]  
↓  
[[FSx for Lustre]]  
↓  
ML Compute Fleet

---

### Scenario 2 — Temporary HPC Simulation

A scientific simulation runs for several hours.

The data is temporary and can be recreated from S3.

Maximum performance and lower cost matter.

**Choose → Lustre Scratch**

---

### Scenario 3 — Long-Running HPC

A research workload runs continuously.

Its working dataset is important and should survive file-server failures.

**Choose → Lustre Persistent**

---

### Scenario 4 — Random Small Files

A workload performs a huge number of:

- Small file reads
- Random operations
- IOPS-heavy access

**Choose:**

FSx for Lustre  
+  
SSD

---

### Scenario 5 — Huge Sequential Files

A workload processes:

Very large files

using:

Sequential reads

and requires:

High throughput

**Choose:**

FSx for Lustre  
+  
HDD

---

### Scenario 6 — Hybrid HPC

An on-premises HPC environment needs high-performance access to FSx for Lustre in AWS.

**Choose:**

FSx for Lustre  
+  
[[05-Networking/Direct Connect]]

or:

[[05-Networking/Site-to-Site VPN]]

---

## Scenario Recognition

Immediately think:

[[FSx for Lustre]]

when you see:

- Lustre
- Linux + cluster
- HPC
- Machine learning
- Extreme throughput
- Parallel file system
- Millions of IOPS
- Sub-millisecond latency
- S3 dataset processing
- Video processing
- Financial modeling
- Electronic design automation

---

## Immediately Think Scratch When You See

- Temporary data
- Short-term processing
- Cost optimization
- High burst
- Data can be recreated
- Source data already in S3

---

## Immediately Think Persistent When You See

- Important working data
- Long-running processing
- Sensitive data
- Replication
- File-server failure protection

---

## Exam Traps

### Trap 1 — Lustre Is a General-Purpose Object Store

False.

It is a:

**Parallel distributed file system**

---

### Trap 2 — Lustre Replaces S3

False.

They commonly work:

**Together**

S3:

**Durable object storage**

Lustre:

**High-performance file processing**

---

### Trap 3 — Scratch Replicates Data

False.

Scratch data is:

**Not replicated**

---

### Trap 4 — Scratch Is Best for Sensitive Long-Term Data

False.

Choose:

**Persistent**

---

### Trap 5 — Persistent Means Multi-AZ Replication

Be careful.

The Maarek slides specify:

**Replication within the same AZ**

---

### Trap 6 — HDD Is Best for Random Small-File IOPS

False.

Use:

**SSD**

---

### Trap 7 — SSD Is Always Required for Lustre

False.

HDD can be appropriate for:

**Large sequential throughput workloads**

---

### Trap 8 — Lustre Cannot Be Accessed from On-Premises

False.

It can be accessed through:

- VPN
- Direct Connect

---

## Quick Cheat Sheet

| Requirement | Best Choice |
|---|---|
| HPC | FSx for Lustre |
| Machine Learning | FSx for Lustre |
| Parallel File System | FSx for Lustre |
| S3 + HPC | FSx for Lustre |
| Temporary HPC | Scratch |
| Re-creatable Data | Scratch |
| High Burst Performance | Scratch |
| Long-Term HPC | Persistent |
| Sensitive Data | Persistent |
| Small Random Files | SSD |
| High IOPS | SSD |
| Large Sequential Files | HDD |
| Throughput Intensive | HDD |
| On-Premises Access | VPN / Direct Connect |

---

## Master Memory Trick

> [!tip] Master Memory Trick
> **Lustre = High-Speed Workbench for S3 Data**
>
> **S3**
> → Stores the dataset
>
> **Lustre**
> → Lets compute tear through it at high speed
>
> **SCRATCH**
> → Disposable workbench
>
> **PERSISTENT**
> → Keep the workbench and the working data

Remember:

**Linux + Cluster**
→ Lustre

**HPC + S3**
→ Lustre

**Temporary + Re-creatable**
→ Scratch

**Important + Long-Term**
→ Persistent

And:

> **SSD = Random + IOPS**
>
> **HDD = Sequential + Throughput**

---

## Related Notes

- [[FSx]]
- [[FSx for Windows File Server]]
- [[FSx for NetApp ONTAP]]
- [[FSx for OpenZFS]]
- [[EFS]]
- [[S3]]
- [[EC2]]
- [[EBS]]
- [[05-Networking/Direct Connect]]
- [[05-Networking/Site-to-Site VPN]]
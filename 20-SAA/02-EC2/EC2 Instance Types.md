## What Problem Does It Solve?

EC2 Instance Types let you choose a virtual server optimized for a specific:

WORKLOAD

Different applications need different amounts of:

- Compute
- Memory
- Networking
- Storage

### Memory Trick

Instance Type = PICK THE RIGHT SERVER FOR THE JOB

---

## EC2 Instance Naming Convention

Your course uses:

m5.2xlarge

Break it down:

m

→ INSTANCE CLASS

5

→ GENERATION

2xlarge

→ SIZE WITHIN THE INSTANCE CLASS

### Memory Trick

m5.2xlarge

=

CLASS + GENERATION + SIZE

---

## Instance Class

The first part identifies the:

INSTANCE CLASS

Example:

m5.2xlarge

↓

m = INSTANCE CLASS

---

## Generation

The number represents the:

GENERATION

Example:

m5.2xlarge

↓

5 = GENERATION

AWS improves instance generations over time.

---

## Size

The final part represents the:

SIZE

within the instance class.

Example:

m5.2xlarge

↓

2xlarge = SIZE

---

# GENERAL PURPOSE

## What Is General Purpose?

General Purpose instances provide a balance between:

COMPUTE

+

MEMORY

+

NETWORKING

They are useful for a diversity of workloads.

### Course Examples

- Web servers
- Code repositories

The course uses:

t2.micro

as an example of a General Purpose EC2 instance.

### Memory Trick

GENERAL PURPOSE = BALANCED

---

## General Purpose Scenario

Need an EC2 instance without an extreme CPU, memory, or storage requirement?

Think:

BALANCED WORKLOAD

↓

GENERAL PURPOSE

---

# COMPUTE OPTIMIZED

## What Is Compute Optimized?

Compute Optimized instances are designed for:

COMPUTE-INTENSIVE TASKS

that require:

HIGH-PERFORMANCE PROCESSORS

### Course Use Cases

- Batch processing workloads
- Media transcoding
- High-performance web servers
- High-performance computing (HPC)
- Scientific modeling
- Machine learning
- Dedicated gaming servers

### Memory Trick

COMPUTE OPTIMIZED = CPU

---

## Compute Optimized Scenario

Need powerful processors for:

SCIENTIFIC MODELING?

→ Compute Optimized

Need:

MEDIA TRANSCODING?

→ Compute Optimized

Need:

HIGH-PERFORMANCE COMPUTING?

→ Compute Optimized

### Exam Keyword

CPU / PROCESSOR INTENSIVE

→ COMPUTE OPTIMIZED

---

# MEMORY OPTIMIZED

## What Is Memory Optimized?

Memory Optimized instances provide fast performance for workloads that process:

LARGE DATA SETS

in:

MEMORY

### Course Use Cases

- High-performance relational databases
- High-performance non-relational databases
- Distributed web-scale cache stores
- In-memory databases optimized for BI
- Real-time processing of large unstructured data

### Memory Trick

MEMORY OPTIMIZED = RAM

---

## Memory Optimized Scenario

Need to process a very large dataset:

IN MEMORY?

→ Memory Optimized

Need an:

IN-MEMORY DATABASE?

→ Memory Optimized

Need a:

HIGH-PERFORMANCE DATABASE

with heavy memory requirements?

→ Memory Optimized

### Exam Keyword

RAM / IN-MEMORY

→ MEMORY OPTIMIZED

---

# STORAGE OPTIMIZED

## What Is Storage Optimized?

Storage Optimized instances are designed for:

STORAGE-INTENSIVE TASKS

requiring:

HIGH SEQUENTIAL READ

+

HIGH SEQUENTIAL WRITE

access to:

LARGE DATA SETS

on:

LOCAL STORAGE

### Memory Trick

STORAGE OPTIMIZED = FAST LOCAL STORAGE

---

## Storage Optimized Use Cases

Your course lists:

- High-frequency OLTP systems
- Relational databases
- NoSQL databases
- Cache for in-memory databases such as Redis
- Data warehousing applications
- Distributed file systems

---

## Storage Optimized Scenario

Need:

HIGH SEQUENTIAL READ / WRITE

on large datasets stored locally?

→ Storage Optimized

Need a:

DATA WAREHOUSE

with storage-intensive processing?

→ Storage Optimized

Need:

DISTRIBUTED FILE SYSTEM

with heavy local storage activity?

→ Storage Optimized

### Exam Keyword

HIGH LOCAL STORAGE I/O

→ STORAGE OPTIMIZED

---

# THE BIG COMPARISON

| Instance Category | Optimized For | Think |
| --- | --- | --- |
| General Purpose | Balanced workloads | BALANCE |
| Compute Optimized | Processor-intensive workloads | CPU |
| Memory Optimized | Large datasets in memory | RAM |
| Storage Optimized | High local storage read/write | STORAGE |

---

## Fast Scenario Recognition

Web server or code repository with balanced needs?

→ GENERAL PURPOSE

---

Batch processing?

→ COMPUTE OPTIMIZED

---

Media transcoding?

→ COMPUTE OPTIMIZED

---

HPC?

→ COMPUTE OPTIMIZED

---

Scientific modeling / machine learning?

→ COMPUTE OPTIMIZED

---

In-memory database?

→ MEMORY OPTIMIZED

---

Large dataset processed in RAM?

→ MEMORY OPTIMIZED

---

Distributed cache?

→ MEMORY OPTIMIZED

---

High sequential read/write on local storage?

→ STORAGE OPTIMIZED

---

OLTP with storage-intensive requirements?

→ STORAGE OPTIMIZED

---

Data warehousing with heavy local storage?

→ STORAGE OPTIMIZED

---

## Instance Type Example

Your course compares example instances using characteristics such as:

- vCPU
- Memory
- Storage
- Network Performance
- EBS Bandwidth

This reinforces the idea that:

INSTANCE TYPES

↓

HAVE DIFFERENT RESOURCE COMBINATIONS

↓

CHOOSE BASED ON WORKLOAD

---

## Exam Traps

GENERAL PURPOSE

≠ BEST AT EVERYTHING

It means:

BALANCED

---

COMPUTE OPTIMIZED

= CPU / PROCESSOR

---

MEMORY OPTIMIZED

= RAM / IN-MEMORY DATA

---

STORAGE OPTIMIZED

= HIGH LOCAL STORAGE READ/WRITE

---

Don't choose based only on the amount of data.

Ask:

WHAT RESOURCE DOES THE WORKLOAD NEED MOST?

CPU?

RAM?

STORAGE?

BALANCE?

---

## Quick Cheat Sheet

GENERAL PURPOSE

= BALANCED

COMPUTE OPTIMIZED

= CPU

MEMORY OPTIMIZED

= RAM

STORAGE OPTIMIZED

= LOCAL STORAGE I/O

---

## Master Memory Trick

BALANCED?

→ GENERAL PURPOSE

CPU?

→ COMPUTE OPTIMIZED

RAM?

→ MEMORY OPTIMIZED

STORAGE?

→ STORAGE OPTIMIZED

---

## Naming Trick

m5.2xlarge

m

= CLASS

5

= GENERATION

2xlarge

= SIZE

---

## Related Notes

- [[EC2]]
- [[EC2 User Data]]
- [[02-Compute/EC2 Purchasing Options]]
- [[EC2 Spot Instances]]
- [[03-Storage/EC2 Instance Store]]
- [[EBS Volumes]]
- [[EC2 Comparison]]
- [[SAA EC2 Cheat Sheet]]
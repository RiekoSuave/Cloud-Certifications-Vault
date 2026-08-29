## What Problem Does It Solve?

Different workloads need different combinations of:

- CPU
- Memory
- Storage
- Networking

EC2 instance families are optimized for different workload types.

---

## General Purpose

Balanced resources.

Designed for workloads that need a mix of:

- CPU
- Memory
- Networking

### Common Uses

- Web servers
- Small databases
- Applications

### Examples

- t2
- t3
- t4g
- m5
- m6i

### Memory Trick

General Purpose = Balanced

---

## Compute Optimized

Designed for workloads that need high-performance processors.

### Common Uses

- Batch processing
- Media transcoding
- High-performance web servers
- High Performance Computing (HPC)
- Scientific modeling
- Machine learning
- Dedicated gaming servers

### Examples

- C5
- C6i

### Memory Trick

C = Compute

---

## Memory Optimized

Designed for workloads that need large amounts of RAM.

### Common Uses

- Databases
- In-memory analytics
- Caching

### Examples

- R5
- R6i
- X1

### Memory Trick

R = RAM

---

## Storage Optimized

Designed for workloads that need high sequential read/write performance on local storage.

### Common Uses

- High-frequency OLTP systems
- Relational databases
- NoSQL databases
- Distributed file systems
- Storage-intensive applications

### Examples

- I3
- D3

### Memory Trick

Storage Optimized = Fast disks

---

## Instance Family Comparison

| Family | Optimized For | Typical Workload |
|---|---|---|
| General Purpose | Balance | Web apps |
| Compute Optimized | CPU | HPC, batch jobs |
| Memory Optimized | RAM | Databases, caching |
| Storage Optimized | Local disk performance | OLTP, large datasets |

---

## Exam Scenarios

Application needs lots of CPU power.

→ Compute Optimized

---

Application needs lots of RAM.

→ Memory Optimized

---

Application needs balanced resources.

→ General Purpose

---

Application needs very high local disk performance.

→ Storage Optimized

---

## Exam Keywords

General Purpose

Compute Optimized

Memory Optimized

Storage Optimized

HPC

OLTP

---

## Quick Cheat Sheet

General Purpose = Balanced

Compute Optimized = CPU

Memory Optimized = RAM

Storage Optimized = Disk
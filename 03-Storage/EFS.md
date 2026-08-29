See also: [[EBS]]

See also: [[03-Storage/EC2 Instance Store]]

See also: [[02-Compute/EC2]]

See also: [[03-Storage/FSx]]

## What Problem Does It Solve?

Provides shared file storage that multiple EC2 instances can access simultaneously.

EFS solves the need for a scalable shared filesystem for Linux workloads.

---

## Type

Managed File Storage

Managed NFS

---

## What Is EFS?

EFS stands for:

Elastic File System

It is a managed NFS (Network File System) that can be mounted by hundreds of EC2 instances.

### Memory Trick

EFS = Shared Drive for Linux

---

## Shared Storage

Unlike EBS, EFS can be accessed by many EC2 instances.

Example:

EC2 Instance

↘

EC2 Instance → EFS

↗

EC2 Instance

All of the instances can access the same shared filesystem.

---

## Linux Workloads

EFS works with:

Linux EC2 instances

It uses:

NFS

### Memory Trick

EFS = Linux + NFS

---

## Multi-AZ

EFS can work with Linux EC2 instances across multiple Availability Zones.

This makes EFS useful when applications need shared file storage across an environment spanning multiple AZs.

---

## Automatic Scaling

EFS automatically scales as files are added or removed.

You do not need to provision a fixed storage capacity in advance.

### Memory Trick

EFS = No Capacity Planning

---

## Pay Per Use

EFS uses a pay-per-use model.

You pay for the storage you actually use rather than provisioning a fixed disk size beforehand.

---

## High Availability

Your course describes EFS as:

- Highly available
- Scalable
- Multi-AZ

This makes it suitable for applications where multiple EC2 instances need access to the same files.

---

## EFS Infrequent Access

EFS includes a cost-optimized storage class for files that are not accessed frequently:

EFS-IA

IA stands for:

Infrequent Access

### Best For

Files that:

- Need to remain available
- Are accessed infrequently

### Memory Trick

IA = Infrequent Access

---

## Common Use Cases

- Shared web server files
- Shared application storage
- Linux workloads
- Multiple EC2 instances accessing the same files

---

## EFS vs EBS

### EBS

Primarily provides block storage for an EC2 instance.

### EFS

Provides a shared filesystem that many EC2 instances can access.

| EBS | EFS |
|---|---|
| Block storage | File storage |
| Network disk | Network filesystem |
| AZ-bound | Multi-AZ |
| Provision capacity | Automatically scales |
| EC2 disk | Shared EC2 filesystem |

### Memory Trick

EBS = One Server's Disk

EFS = Shared Files

---

## EFS vs Instance Store

### EFS

- Shared
- Network filesystem
- Persistent
- Multi-instance

### Instance Store

- Local hardware disk
- Temporary
- High performance
- Tied to EC2 host

---

## EFS vs FSx

EFS → Shared Linux filesystem

FSx → Specialized managed filesystems

See:

[[03-Storage/FSx]]

---

## Exam Scenarios

Hundreds of Linux EC2 instances need access to the same filesystem.

→ EFS

---

Linux EC2 instances across multiple Availability Zones need shared file storage.

→ EFS

---

A company does not want to provision storage capacity ahead of time.

→ EFS

---

Files are accessed infrequently and the company wants a cost-optimized EFS storage option.

→ EFS-IA

---

A single EC2 workload needs persistent block storage.

→ EBS

---

## Exam Keywords

NFS

Linux

Shared filesystem

Multiple EC2 instances

Multi-AZ

Automatic scaling

EFS-IA

---

## Memory Tricks

EFS = Shared Drive for Linux

EFS = NFS

EFS = Multi-Instance

EFS = Multi-AZ

EFS-IA = Infrequent Files

EBS = EC2 Disk
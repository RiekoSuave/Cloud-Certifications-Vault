See also: [[03-Storage/EFS]]

See also: [[EBS]]

See also: [[S3]]

## What Problem Does It Solve?

Provides fully managed, specialized file systems for workloads that need capabilities beyond a general-purpose shared filesystem.

---

## Type

Managed File Storage

---

## What Is FSx?

FSx provides managed file systems designed for specific workloads.

Your course focuses on:

- FSx for Windows File Server
- FSx for Lustre

### Memory Trick

FSx = Specialized File Systems

---

## FSx for Windows File Server

Provides a managed network file system for Windows servers.

### Best For

Windows-based applications and workloads that need shared file storage.

### Memory Trick

FSx for Windows = Windows Files

---

## FSx for Lustre

Provides a high-performance file system designed for Linux workloads.

Lustre is commonly associated with:

High Performance Computing (HPC)

### Best For

Workloads requiring very high file-system performance.

### Memory Trick

Lustre = Linux + High Performance

---

## FSx for Windows vs FSx for Lustre

| Service | Best For |
|---|---|
| FSx for Windows File Server | Windows workloads |
| FSx for Lustre | High-performance Linux/HPC workloads |

---

## FSx vs EFS

### EFS

Managed shared filesystem primarily associated with Linux EC2 workloads.

### FSx

Managed specialized filesystems.

| EFS | FSx |
|---|---|
| Linux shared filesystem | Specialized filesystems |
| NFS | Depends on FSx type |
| General shared Linux storage | Specialized workload requirements |

---

## Storage Relationship

Need EC2 block storage?

→ EBS

---

Need shared Linux file storage?

→ EFS

---

Need Windows shared file storage?

→ FSx for Windows File Server

---

Need a high-performance Linux filesystem for HPC?

→ FSx for Lustre

---

## Common Use Cases

### FSx for Windows

- Windows servers
- Windows applications
- Shared Windows files

### FSx for Lustre

- High Performance Computing
- Performance-intensive Linux workloads

---

## Exam Scenarios

A company needs a managed network filesystem for Windows servers.

→ FSx for Windows File Server

---

A company needs a high-performance Linux filesystem for an HPC workload.

→ FSx for Lustre

---

Hundreds of Linux EC2 instances need a general shared NFS filesystem.

→ EFS

---

An EC2 instance needs persistent block storage.

→ EBS

---

## Exam Keywords

Windows

Lustre

Linux

HPC

Managed filesystem

File storage

---

## Memory Tricks

FSx = Specialized Filesystems

FSx Windows = Windows Files

FSx Lustre = Linux + HPC

EFS = Shared Linux Drive

EBS = EC2 Hard Drive
See also: [[S3]]

See also: [[EBS]]

See also: [[03-Storage/EFS]]

See also: [[03-Storage/FSx]]

See also: [[S3 Glacier]]

See also: [[S3 Glacier Deep Archive]]

See also: [[03-Storage/Storage Gateway]]

## What Problem Does This Solve?

Helps identify which AWS storage service should be used for a particular workload.

For the exam, focus on the problem being described and match it to the correct storage service.

---

## Storage Comparison

| Service | Storage Type | Best For |
|---|---|---|
| S3 | Object | Files, backups, images, objects |
| EBS | Block | EC2 disks |
| EFS | File | Shared Linux files |
| FSx | File | Windows / Lustre workloads |
| S3 Glacier | Archive | Long-term storage |
| S3 Glacier Deep Archive | Archive | Lowest-cost long-term retention |
| Storage Gateway | Hybrid | On-premises + AWS storage |

---

## S3

### Storage Type

Object Storage

### Best For

- Files
- Images
- Videos
- Backups
- Static website content
- Data lakes

### Exam Clue

Need scalable object storage?

→ S3

### Memory Trick

S3 = Objects

---

## EBS

### Storage Type

Block Storage

### Best For

EC2 instance disks.

Think of EBS as a virtual hard drive attached to EC2.

### Exam Clue

EC2 needs persistent block storage?

→ EBS

### Memory Trick

EBS = EC2 Hard Drive

---

## EFS

### Storage Type

File Storage

### Best For

Multiple Linux EC2 instances that need access to the same filesystem.

### Exam Clue

Multiple Linux servers need shared storage?

→ EFS

### Memory Trick

EFS = Shared Linux Drive

---

## FSx

### Storage Type

Specialized File Storage

### Best For

Specialized filesystem requirements.

Your course focuses on:

- Windows File Server
- Lustre

### Exam Clues

Need Windows shared file storage?

→ FSx for Windows File Server

Need a high-performance Linux filesystem for HPC?

→ FSx for Lustre

### Memory Trick

FSx = Specialized File Systems

---

## S3 Glacier

### Storage Type

Archive Storage

### Best For

Long-term archival data.

Retrieval does not need to occur as frequently as normal S3 data.

### Exam Clue

Need low-cost cold storage?

→ Glacier

### Memory Trick

Glacier = Cold Storage

---

## S3 Glacier Deep Archive

### Storage Type

Deep Archive Storage

### Best For

Extremely long-term data retention that is almost never accessed.

### Exam Clue

Need the lowest-cost long-term archive?

→ Glacier Deep Archive

### Memory Trick

Deep Archive = Cheapest Storage

---

## Storage Gateway

### Storage Type

Hybrid Cloud Storage

### Best For

Connecting:

On-Premises Storage

↕

AWS Cloud Storage

### Exam Clue

Need hybrid storage between on-premises and AWS?

→ Storage Gateway

### Memory Trick

Storage Gateway = Bridge to AWS

---

## Storage Scenario Questions

### Scenario 1

A company needs storage for website images.

**Answer:**

S3

**Why?**

Object storage for files.

---

### Scenario 2

An EC2 instance needs a persistent hard drive.

**Answer:**

EBS

**Why?**

Block storage attached to EC2.

---

### Scenario 3

Multiple Linux EC2 instances need shared storage.

**Answer:**

EFS

**Why?**

Shared filesystem.

---

### Scenario 4

A company needs Windows shared file storage.

**Answer:**

FSx for Windows File Server

**Why?**

Managed Windows filesystem.

---

### Scenario 5

A company needs a high-performance filesystem for a Linux HPC workload.

**Answer:**

FSx for Lustre

**Why?**

High-performance specialized filesystem.

---

### Scenario 6

A company must store legal documents for 10 years and rarely access them.

**Answer:**

S3 Glacier Deep Archive

**Why?**

Lowest-cost long-term archival storage.

---

### Scenario 7

A company needs to connect its on-premises storage environment with AWS.

**Answer:**

Storage Gateway

**Why?**

Hybrid storage.

---

## Don't Confuse These

### S3 vs EBS

S3 = Objects

EBS = EC2 disk

---

### EBS vs EFS

EBS = Block storage

EFS = Shared filesystem

---

### EFS vs FSx

EFS = Shared Linux filesystem

FSx = Specialized filesystems

---

### Glacier vs Deep Archive

Glacier = Cold archive

Deep Archive = Lowest-cost long-term archive

---

### S3 vs Storage Gateway

S3 = AWS object storage

Storage Gateway = Connect on-premises storage to AWS

---

## Storage Decision Tree

Need object storage?

→ S3

Need an EC2 hard drive?

→ EBS

Need shared Linux storage?

→ EFS

Need Windows file storage?

→ FSx for Windows

Need high-performance Linux/HPC filesystem?

→ FSx for Lustre

Need cold archival storage?

→ S3 Glacier

Need lowest-cost long-term archival storage?

→ S3 Glacier Deep Archive

Need hybrid on-premises + AWS storage?

→ Storage Gateway

---

## Storage Cheat Code

S3 = Objects

EBS = EC2 Hard Drive

EFS = Shared Linux Drive

FSx = Specialized File Systems

Glacier = Cold Storage

Deep Archive = Cheapest Storage

Storage Gateway = Hybrid Storage

---

## Exam Strategy

When you see a storage question:

**1. Identify the storage type**

Object?

Block?

File?

Archive?

Hybrid?

**2. Look for the workload**

EC2?

Linux?

Windows?

HPC?

Long-term archive?

On-premises?

**3. Match the keyword to the service**

This usually eliminates the wrong answers quickly.
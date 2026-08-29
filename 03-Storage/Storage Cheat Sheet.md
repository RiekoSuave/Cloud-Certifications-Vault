See also: [[Storage Comparison]]

## Core Storage Services

S3 = Object Storage

EBS = EC2 Hard Drive

EFS = Shared Linux Drive

FSx = Specialized File Systems

EC2 Instance Store = Fast Temporary Storage

Storage Gateway = Hybrid Storage

---

## S3 Cheat Code

S3 Standard = Frequently Accessed

Standard-IA = Infrequent + Multi-AZ

One Zone-IA = Infrequent + One AZ

Intelligent-Tiering = AWS Automatically Optimizes

Glacier Instant = Archive + Fast Retrieval

Glacier Flexible = Cold Storage

Glacier Deep Archive = Cheapest Long-Term Archive

Express One Zone = High Performance + One AZ

---

## Quick Storage Decisions

Need scalable object storage?

→ S3

Need an EC2 hard drive?

→ EBS

Need very fast temporary EC2 storage?

→ EC2 Instance Store

Need shared Linux storage?

→ EFS

Need Windows file storage?

→ FSx for Windows File Server

Need high-performance Linux/HPC storage?

→ FSx for Lustre

Need hybrid on-premises + AWS storage?

→ Storage Gateway

Need cold archival storage?

→ S3 Glacier

Need the cheapest long-term archive?

→ S3 Glacier Deep Archive

---

## S3 Quick Decisions

Frequently accessed objects?

→ S3 Standard

Infrequently accessed but need fast retrieval?

→ Standard-IA

Infrequent and re-creatable data?

→ One Zone-IA

Unknown access pattern?

→ Intelligent-Tiering

Archive but need immediate retrieval?

→ Glacier Instant Retrieval

Cold archive where retrieval can wait?

→ Glacier Flexible Retrieval

Long-term archive that is almost never accessed?

→ Glacier Deep Archive

Need extremely high-performance S3 in one AZ?

→ S3 Express One Zone

---

## Don't Confuse These

EBS = Block Storage

EFS = File Storage

S3 = Object Storage

---

EBS = Persistent Network Drive

Instance Store = Fast Temporary Local Drive

---

EFS = Shared Linux Files

FSx = Specialized File Systems

---

Standard-IA = Multi-AZ

One Zone-IA = One AZ

---

Glacier Instant = Fast Archive Retrieval

Glacier Flexible = Cold Archive

Deep Archive = Cheapest Long-Term Archive

---

Lifecycle = You Define When Data Moves

Intelligent-Tiering = AWS Automatically Optimizes Based on Access

---

## S3 Data Protection

Versioning = Keep Old Versions

Replication = Copy Objects to Another Bucket

CRR = Cross-Region Replication

SRR = Same-Region Replication

Replication Requires Versioning

---

## S3 Security

IAM Policy = Identity Permissions

Bucket Policy = Bucket Permissions

EC2 → S3 = IAM Role

Cross-Account Access = Bucket Policy

Block Public Access = Prevent Accidental Public Exposure

Explicit Deny = Always Wins

---

## 30-Second Storage Review

S3 → Objects

EBS → EC2 Disk

EFS → Shared Linux

FSx → Specialized Filesystems

Instance Store → Fast + Temporary

Storage Gateway → Hybrid Storage

Standard → Frequent

IA → Infrequent

Intelligent-Tiering → Automatic

Glacier → Archive

Deep Archive → Cheapest Archive
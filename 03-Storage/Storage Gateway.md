See also: [[S3]]

See also: [[03-Storage/EFS]]

## What Problem Does It Solve?

Connects on-premises storage environments with AWS cloud storage.

Storage Gateway allows organizations to use AWS storage while still maintaining part of their infrastructure on-premises.

---

## Type

Hybrid Cloud Storage

---

## What Is Storage Gateway?

Storage Gateway is a hybrid storage service.

It acts as a bridge between:

On-Premises Storage

↓

Storage Gateway

↓

AWS Cloud Storage / S3

### Memory Trick

Storage Gateway = Bridge On-Premises Storage to AWS

---

## What Is Hybrid Cloud?

Hybrid cloud means part of an organization's infrastructure remains:

On-Premises

while another part runs in:

AWS

Your course identifies several reasons organizations may use hybrid environments:

- Long cloud migrations
- Security requirements
- Compliance requirements
- IT strategy

---

## Why Storage Gateway?

Your course points out an important difference:

S3 uses AWS's object-storage technology.

Traditional on-premises environments may use familiar file or storage protocols instead.

Storage Gateway helps connect those environments.

---

## Key Purpose

Storage Gateway allows on-premises environments to seamlessly use AWS cloud storage.

It can provide access between:

On-Premises Data

↕

Storage Gateway

↕

AWS Cloud Storage

---

## Common Use Cases

Your course identifies:

- Disaster recovery
- Backup and restore
- Tiered storage

---

## Storage Gateway Types

Your course mentions three types:

- File Gateway
- Volume Gateway
- Tape Gateway

### Important Course Note

Your CCP course specifically says you do NOT need to know the individual gateway types for the exam.

For now, focus on:

Storage Gateway = Hybrid Storage

We'll go deeper if your SAA material requires it.

---

## File Gateway

High-level awareness:

File-based gateway.

---

## Volume Gateway

High-level awareness:

Volume-based gateway.

---

## Tape Gateway

High-level awareness:

Tape-based gateway.

---

## Storage Gateway vs S3

### S3

AWS object storage.

### Storage Gateway

Connects on-premises storage environments with AWS storage.

| S3 | Storage Gateway |
|---|---|
| Cloud object storage | Hybrid storage |
| AWS-native storage | Connects on-premises + AWS |
| Stores objects | Bridges storage environments |

---

## Storage Gateway vs EFS

### EFS

Managed shared filesystem for Linux workloads in AWS.

### Storage Gateway

Hybrid storage connection between on-premises environments and AWS.

---

## Exam Scenarios

A company wants to keep some storage on-premises while extending its storage into AWS.

→ Storage Gateway

---

A company needs a hybrid-cloud storage solution.

→ Storage Gateway

---

A company needs cloud storage for backup and restore while maintaining an on-premises environment.

→ Storage Gateway

---

A company needs massively scalable object storage entirely in AWS.

→ S3

---

## Exam Keywords

Hybrid cloud

On-premises

Storage

S3

Backup

Disaster recovery

Gateway

---

## Memory Tricks

Storage Gateway = Hybrid Storage

Storage Gateway = On-Premises ↔ AWS

S3 = Cloud Object Storage

Gateway = Bridge
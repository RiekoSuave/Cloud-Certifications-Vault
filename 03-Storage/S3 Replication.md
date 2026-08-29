See also: [[S3]]

See also: [[03-Storage/S3 Versioning]]

See also: [[IAM]]

## What Problem Does It Solve?

Automatically copies S3 objects from one bucket to another.

Replication can be used to maintain copies of data in:

- Another AWS Region
- The same AWS Region
- Another AWS account

---

## Type

Data Replication

---

## What Is S3 Replication?

S3 Replication automatically copies objects between S3 buckets.

There are two main types:

- Cross-Region Replication (CRR)
- Same-Region Replication (SRR)

### Memory Trick

CRR = Different Regions

SRR = Same Region

---

## Versioning Requirement

Versioning must be enabled on:

- Source bucket
- Destination bucket

before S3 Replication can be used.

See:

[[03-Storage/S3 Versioning]]

### Memory Trick

Replication Requires Versioning

---

## Cross-Region Replication (CRR)

CRR replicates objects between buckets located in different AWS Regions.

Basic Flow:

Source Bucket

↓

Different AWS Region

↓

Destination Bucket

---

## CRR Use Cases

Your course identifies:

- Compliance
- Lower-latency access
- Replication across AWS accounts

### Memory Trick

CRR = Cross Regions

---

## Same-Region Replication (SRR)

SRR replicates objects between buckets located within the same AWS Region.

Basic Flow:

Source Bucket

↓

Same AWS Region

↓

Destination Bucket

---

## SRR Use Cases

Your course identifies:

- Log aggregation
- Live replication between production and test accounts

### Memory Trick

SRR = Same Region

---

## CRR vs SRR

| CRR | SRR |
|---|---|
| Different Regions | Same Region |
| Compliance | Log aggregation |
| Lower-latency access | Production/test replication |
| Can replicate across accounts | Can replicate across accounts |

---

## Cross-Account Replication

Source and destination buckets can exist in:

Different AWS accounts

This makes S3 Replication useful when organizations need data copied between accounts.

---

## IAM Permissions

S3 must be given the proper:

IAM permissions

to perform replication.

Without the required permissions, S3 cannot replicate the objects.

See:

[[IAM]]

---

## Replication Is Asynchronous

S3 replication occurs:

Asynchronously

This means the copy does not necessarily appear in the destination bucket immediately when the source object is created.

### Memory Trick

Replication = Automatic but Asynchronous

---

## Basic Replication Flow

Source Bucket

↓

Versioning Enabled

↓

S3 Replication

↓

Destination Bucket

↓

Versioning Enabled

---

## Common Use Cases

### CRR

- Compliance
- Geographic copies
- Lower-latency access
- Cross-account replication

### SRR

- Log aggregation
- Production/test replication
- Same-Region copies

---

## Replication vs Versioning

### Versioning

Maintains multiple versions of objects.

### Replication

Copies objects to another bucket.

Versioning is required before replication can be configured.

| Versioning | Replication |
|---|---|
| Object history | Object copies |
| Same bucket | Different bucket |
| Protects previous versions | Copies data elsewhere |
| Required for replication | Requires versioning |

---

## Exam Scenarios

A company needs S3 objects automatically copied to a bucket in another AWS Region.

→ Cross-Region Replication (CRR)

---

A company needs S3 replication for compliance across Regions.

→ CRR

---

A company wants to aggregate logs into another bucket in the same Region.

→ Same-Region Replication (SRR)

---

Production S3 data needs to be replicated to a test account in the same Region.

→ SRR

---

A company wants to configure S3 Replication.

What must be enabled first?

→ Versioning on the source and destination buckets

---

A company expects replicated objects to appear instantaneously.

What should they remember?

→ S3 Replication is asynchronous

---

## Exam Keywords

CRR

SRR

Replication

Versioning

Asynchronous

Cross-account

Compliance

Log aggregation

IAM permissions

---

## Memory Tricks

CRR = Cross Region

SRR = Same Region

Replication = Copy Objects

Replication Requires Versioning

Replication = Asynchronous
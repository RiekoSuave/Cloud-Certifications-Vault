## What Problem Does It Solve?

[[S3 Replication]] automatically copies objects from one S3 bucket to another.

It solves problems such as:

> **"How can I keep another copy of my objects in a different Region, account, or bucket?"**

There are two main replication types:

- [[S3 Cross-Region Replication]]
- [[S3 Same-Region Replication]]

Think:

Source Bucket  
↓ asynchronous copy  
Destination Bucket

> [!tip] Memory Trick
> **Replication = Another Bucket**
>
> **CRR = Cross Region**
>
> **SRR = Same Region**

---

## Replication Prerequisite — Versioning

This is the first thing to remember.

S3 Replication requires:

**Versioning enabled on both the source and destination buckets**

Architecture:

Source Bucket  
Versioning ✅  
↓  
Replication  
↓  
Destination Bucket  
Versioning ✅

If Versioning is missing on either side:

**Replication cannot be configured correctly.**

> [!warning] Exam Rule
> **Replication → Versioning on BOTH buckets**

---

## Replication Is Asynchronous

S3 Replication performs copies:

**Asynchronously**

That means:

Object Uploaded  
↓  
Stored in Source Bucket  
↓  
Replication Happens Later  
↓  
Object Appears in Destination

The application does not have to wait for the destination copy before the source upload completes.

### Memory Trick

**Replication = Eventually copied, not synchronous write**

---

## IAM Permissions Are Required

S3 needs permission to:

- Read from the source
- Replicate objects
- Write to the destination

Therefore:

**Proper IAM permissions must be granted to S3**

Architecture:

Source Bucket  
↓  
IAM Role / Permissions  
↓  
S3 Replication  
↓  
Destination Bucket

### Exam Trap

If:

- Versioning is enabled
- Replication rule exists
- Objects are not replicating

also check:

**IAM permissions**

---

# Cross-Region Replication — CRR

[[S3 Cross-Region Replication]] copies objects between buckets in:

**Different AWS Regions**

Example:

Source:

eu-west-1

Destination:

us-east-2

Architecture:

S3 Bucket  
eu-west-1  
↓ asynchronous  
S3 Bucket  
us-east-2

---

## Common CRR Use Cases

The Maarek slides highlight:

- Compliance
- Lower-latency access
- Replication across AWS accounts

### Compliance

A company may be required to maintain a copy of data in another Region.

Choose:

**CRR**

---

### Lower-Latency Access

Users in another Region need access to a closer copy of the data.

Choose:

**CRR**

---

### Cross-Account Replication

The destination bucket may exist in another:

**AWS Account**

This can improve separation between:

- Production
- Backup
- Security
- Compliance environments

> [!tip] Memory Trick
> **CRR = Geography / Compliance / Cross-Account**

---

# Same-Region Replication — SRR

[[S3 Same-Region Replication]] copies objects between buckets in the:

**Same AWS Region**

Example:

Bucket A  
us-east-1  
↓  
Bucket B  
us-east-1

---

## Common SRR Use Cases

The Maarek slides highlight:

- Log aggregation
- Live replication between production and test accounts

### Log Aggregation

Multiple S3 buckets can replicate logs into:

**One central bucket**

Architecture:

Application Bucket A  
↓  
Application Bucket B  
↓  
Application Bucket C  
↓  
[[S3 Same-Region Replication]]  
↓  
Central Logging Bucket

---

### Production → Test

A production bucket can replicate objects into a test account.

Example:

Production Account  
↓  
SRR  
↓  
Test Account

This provides a live copy of application data for testing or analytics.

> [!tip] Memory Trick
> **SRR = Same Region, Separate Purpose**

---

# CRR vs SRR

| Requirement | Replication Type |
|---|---|
| Different Regions | CRR |
| Same Region | SRR |
| Compliance copy in another Region | CRR |
| Lower latency in another Region | CRR |
| Cross-account copy | CRR or SRR |
| Central log aggregation | SRR |
| Production → Test | SRR |

### Master Difference

**CRR = Region changes**

**SRR = Region stays**

---

# Cross-Account Replication

Source and destination buckets can belong to:

**Different AWS accounts**

Example:

Production Account  
↓  
S3 Replication  
↓  
Backup Account

This can improve security because the replicated copy exists outside the production account.

### Architecture Thinking

If an attacker compromises:

Production Account

a separately controlled destination account may provide stronger isolation than storing every copy under the same account.

---

# What Gets Replicated After You Enable Replication?

This is an important exam rule.

After replication is enabled:

**New objects are replicated automatically**

Existing objects are not automatically copied by the normal replication rule.

Example:

Before Replication:

Object A  
Object B  
Object C

Enable replication.

Then upload:

Object D

Normal result:

Object D → Replicated

Existing A/B/C:

Not automatically replicated by the new rule.

> [!warning] Exam Rule
> **Enable replication today → New objects replicate**

---

# Replicating Existing Objects

For objects that already existed before the replication rule:

Use:

[[S3 Batch Replication]]

S3 Batch Replication can replicate:

- Existing objects
- Objects that previously failed replication

Architecture:

Existing Objects  
↓  
[[S3 Batch Replication]]  
↓  
Destination Bucket

### Memory Trick

**New Objects = Replication Rule**

**Old Objects = Batch Replication**

---

# Delete Marker Replication

Delete behavior requires careful exam reading.

When Versioning is enabled:

Deleting an object normally creates a:

**Delete Marker**

S3 Replication can optionally replicate:

**Delete Markers**

Example:

Source Bucket  
↓ delete object  
Delete Marker  
↓ optional replication  
Destination Bucket  
↓ Delete Marker

This behavior must be configured.

---

# Permanent Version Deletes Are Not Replicated

Suppose you explicitly delete:

A specific Version ID

That permanent deletion is:

**Not replicated**

Why?

AWS avoids propagating malicious or accidental permanent deletes across replicated copies.

### Architecture Thinking

Source:

Version 1  
Version 2  
Version 3

Administrator permanently deletes:

Version 2

That permanent deletion does not automatically propagate to the destination.

> [!tip] Memory Trick
> **Delete Marker can replicate**
>
> **Permanent Version Delete does NOT**

---

# Replication Chaining Does Not Work

This is a very important exam trap.

Suppose:

Bucket A  
↓ replication  
Bucket B  
↓ replication  
Bucket C

You upload an object directly to:

Bucket A

Result:

Bucket A  
↓  
Bucket B ✅

But:

Bucket C ❌

The object replicated from A to B is not automatically replicated again from B to C.

This is called:

**No Replication Chaining**

> [!warning] Exam Trap
> **A → B → C does NOT mean A's objects reach C**

---

## If You Need A to Replicate to B and C

Configure replication directly from the source as required.

Conceptually:

Bucket A  
├── Replicate → Bucket B
└── Replicate → Bucket C

Do not rely on:

A → B → C

---

# Replication and Encryption

Encryption introduces additional replication considerations.

---

## Unencrypted Objects

Unencrypted objects can be replicated normally.

---

## SSE-S3

Objects encrypted using:

[[S3 SSE-S3]]

are replicated by default.

Think:

S3-managed encryption  
↓  
Replication works normally

---

## SSE-C

Objects encrypted using:

[[S3 SSE-C]]

can also be replicated.

---

## SSE-KMS

[[S3 SSE-KMS]] requires additional configuration.

For KMS-encrypted objects:

You must explicitly enable replication for those objects.

You also specify:

**Which KMS key encrypts the replicated object in the destination bucket**

Architecture:

Source Object  
↓  
Source KMS Key  
↓ decrypt  
Replication  
↓ encrypt  
Destination KMS Key  
↓  
Destination Object

---

# KMS Permissions for Replication

The S3 replication IAM role needs permission for:

Source Key:

**kms:Decrypt**

Destination Key:

**kms:Encrypt**

Conceptually:

Source KMS Key  
↓ Decrypt Permission  
Replication Role  
↓ Encrypt Permission  
Destination KMS Key

The destination KMS key policy must also permit the required operations.

> [!tip] Memory Trick
> **Replication with KMS: Decrypt HERE → Encrypt THERE**

---

## KMS Throttling

Heavy SSE-KMS replication can increase KMS API activity.

This can cause:

**KMS throttling**

If the architecture hits KMS quotas:

You may need a:

**Service Quotas increase**

### Exam Recognition

Large replication workload  
+  
SSE-KMS  
+  
Throttling

Think:

**KMS request limits**

---

# Multi-Region KMS Keys

S3 can use:

[[KMS Multi-Region Keys]]

However, for S3 replication they are treated as:

**Independent keys**

The object is still:

1. Decrypted using the source key
2. Replicated
3. Re-encrypted using the destination key

Do not assume a Multi-Region Key allows S3 to simply copy the encrypted ciphertext unchanged.

---

# Architecture Thinking

## Scenario 1 — Compliance Copy in Another Region

A company must maintain an object copy in another AWS Region.

**Choose → [[S3 Cross-Region Replication]]**

Requirements:

- Versioning on both buckets
- IAM permissions
- Replication rule

---

## Scenario 2 — Central Logging Bucket

Multiple application buckets in the same Region need their objects copied to a central logging bucket.

**Choose → [[S3 Same-Region Replication]]**

---

## Scenario 3 — Separate Backup Account

Production objects must automatically copy into a security-controlled AWS account.

The destination can be:

**Another AWS account**

Use:

[[S3 Replication]]

with the appropriate cross-account permissions.

---

## Scenario 4 — Existing Objects Need Replication

A company enables CRR today.

The bucket already contains millions of objects.

They need those old objects copied too.

**Choose → [[S3 Batch Replication]]**

Normal replication automatically handles new objects.

Batch Replication handles existing objects.

---

## Scenario 5 — Replication Chain

A company configures:

Bucket A → Bucket B

and:

Bucket B → Bucket C

Objects uploaded to Bucket A must eventually reach Bucket C.

Will this automatically happen?

**No.**

S3 does not chain replication.

Configure the required replication directly.

---

## Scenario 6 — KMS-Encrypted Objects

A source bucket uses [[S3 SSE-KMS]].

The company enables replication, but KMS-encrypted objects are not copying.

Check:

- SSE-KMS replication option enabled
- Source KMS decrypt permission
- Destination KMS encrypt permission
- Destination KMS key policy

---

# Replication vs Versioning

## [[S3 Versioning]]

Creates:

**History inside the same bucket**

Think:

Version 1  
Version 2  
Version 3

---

## S3 Replication

Creates:

**Another copy in another bucket**

Think:

Bucket A  
↓  
Bucket B

### Memory Trick

**Versioning = Time**

**Replication = Space**

Versioning protects across:

**Time / object history**

Replication protects across:

**Buckets / Regions / Accounts**

---

# Replication vs Lifecycle

## [[S3 Lifecycle Rules]]

Purpose:

- Transition
- Archive
- Delete

Question:

> What happens as the object ages?

---

## S3 Replication

Purpose:

**Create another copy**

Question:

> Where else should this object exist?

### Memory Trick

**Lifecycle = AGE**

**Replication = COPY**

---

# Scenario Recognition

## Immediately Think CRR When You See

- Different AWS Region
- Compliance
- Geographic copy
- Lower latency in another Region
- Cross-Region backup

---

## Immediately Think SRR When You See

- Same Region
- Log aggregation
- Production to test
- Another account in same Region

---

## Immediately Think Batch Replication When You See

- Existing objects
- Objects created before replication enabled
- Previously failed replication

---

## Immediately Think KMS Configuration When You See

- Replication fails only for SSE-KMS objects
- kms:Decrypt
- kms:Encrypt
- Destination KMS key
- KMS throttling

---

# Exam Traps

## Trap 1 — Versioning Needed Only on Source

False.

Versioning must be enabled on:

**Source + Destination**

---

## Trap 2 — Replication Is Synchronous

False.

Replication is:

**Asynchronous**

---

## Trap 3 — Existing Objects Automatically Replicate

Not through a newly enabled normal replication rule.

Use:

[[S3 Batch Replication]]

for existing objects.

---

## Trap 4 — Every Delete Is Replicated

False.

Delete markers:

**Optional replication**

Permanent deletion of a specific Version ID:

**Not replicated**

---

## Trap 5 — Replication Chaining Works

False.

A → B → C

does not cause objects created in A to automatically reach C through B.

---

## Trap 6 — CRR Is Only for Backups

False.

Other CRR use cases include:

- Compliance
- Lower-latency access
- Cross-account replication

---

## Trap 7 — SSE-KMS Objects Replicate Automatically with No Extra Configuration

False.

SSE-KMS requires:

- Replication enabled for KMS objects
- Destination KMS key
- KMS key-policy permissions
- Decrypt source / Encrypt destination permissions

---

# Quick Cheat Sheet

| Feature | S3 Replication |
|---|---|
| Versioning Required on Source | ✅ |
| Versioning Required on Destination | ✅ |
| Asynchronous | ✅ |
| Different Accounts | ✅ |
| Different Regions | CRR |
| Same Region | SRR |
| Existing Objects Automatically Replicated | ❌ |
| Existing Objects via Batch Replication | ✅ |
| Failed Objects via Batch Replication | ✅ |
| Delete Marker Replication | Optional |
| Specific Version Delete Replicated | ❌ |
| Replication Chaining | ❌ |
| SSE-S3 Replication | Default |
| SSE-C Replication | ✅ |
| SSE-KMS Extra Configuration | ✅ |

---

## Master Memory Trick

> [!tip] Master Memory Trick
> **S3 Replication = V-A-N-D-K**
>
> **V = Versioning on BOTH**
>
> **A = Asynchronous**
>
> **N = New objects by default**
>
> **D = Delete markers optional**
>
> **K = KMS needs extra permissions**

Then:

**Different Region → CRR**

**Same Region → SRR**

**Old Objects → Batch Replication**

And never forget:

> **Replication does NOT chain**
>
> A → B → C
>
> does not mean A automatically reaches C.

---

## Related Notes

- [[S3]]
- [[S3 Versioning]]
- [[S3 Cross-Region Replication]]
- [[S3 Same-Region Replication]]
- [[S3 Batch Replication]]
- [[S3 Lifecycle Rules]]
- [[S3 SSE-S3]]
- [[S3 SSE-KMS]]
- [[S3 SSE-C]]
- [[06-Security/KMS]]
- [[IAM]]
- [[AWS Accounts]]
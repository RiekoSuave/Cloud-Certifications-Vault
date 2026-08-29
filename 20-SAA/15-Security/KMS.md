## What Problem Does It Solve?

[[KMS]] helps you:

**Create, manage, and control encryption keys used to protect data**

It integrates with many AWS services to provide:

- Encryption at rest
- Key management
- Key policies
- Key rotation
- Auditability
- Centralized cryptographic control

Architecture:

Application / AWS Service  
↓  
KMS Key  
↓  
Encrypt / Decrypt Data

> [!tip] Memory Trick
> **KMS = Manage Encryption Keys**

---

## Core Concept

KMS does NOT usually store:

**Your application data**

Instead, it manages:

**The cryptographic keys used to encrypt data**

Example:

S3 Object  
↓  
Encrypted with Data Key  
↓  
Data Key Protected by KMS Key

### Killer Exam Clue

> **Need centralized management and control of encryption keys**
>
> → **KMS**

---

# Encryption at Rest

KMS is commonly used for:

**Encryption at rest**

with AWS services such as:

- [[S3]]
- [[EBS]]
- [[RDS]]
- [[DynamoDB]]
- [[Lambda]]
- [[Secrets Manager]]
- [[CloudWatch]]

### Memory Trick

**Data Stored**
→ Encryption at Rest

---

# Encryption in Transit

KMS is not the primary service for:

**Network encryption in transit**

For encryption in transit, think:

- HTTPS
- TLS
- Certificates
- [[AWS Certificate Manager]]

### Killer Exam Distinction

**Stored Data**
→ KMS

**Network Connection**
→ TLS / ACM

---

# KMS Keys

The central object in KMS is a:

**KMS Key**

A KMS key is used to protect:

**Cryptographic material**

and control:

**Encryption/decryption permissions**

---

# Symmetric Keys

Most AWS-integrated KMS use cases rely on:

**Symmetric encryption keys**

The same key is conceptually used for:

- Encryption
- Decryption

AWS services commonly use:

**Symmetric KMS keys**

### Killer Exam Clue

> **AWS service encryption using KMS**
>
> → Usually **symmetric KMS key**

---

# Asymmetric Keys

KMS also supports:

**Asymmetric key pairs**

These contain:

- Public key
- Private key

They can be used for supported:

- Encryption/decryption
- Signing/verification

### Memory Trick

**Symmetric = One Secret Key**

**Asymmetric = Public + Private**

---

# AWS-Owned Keys

An:

**AWS-Owned Key**

is owned and managed entirely by:

**AWS**

You generally:

- Do not see the key
- Do not manage its policy
- Do not control rotation

### Memory Trick

**AWS-Owned = AWS Controls Everything**

---

# AWS-Managed Keys

An:

**AWS-Managed Key**

is created and managed by AWS for use with:

**A specific AWS service**

They are commonly recognizable by aliases such as:

`aws/s3`

`aws/ebs`

### Key Characteristics

AWS manages:

- Creation
- Rotation
- Key policy structure

You have:

**Less control**

than with a customer managed key.

### Memory Trick

**AWS-Managed = Visible, But AWS Runs It**

---

# Customer Managed Keys

A:

**Customer Managed Key**

is created and controlled by:

**You**

You control:

- Key policy
- IAM access
- Enable/disable state
- Rotation configuration
- Grants
- Aliases
- Deletion scheduling

### Killer Exam Clue

> **Need full control over encryption key permissions**
>
> → **Customer Managed KMS Key**

---

# Key Type Comparison

| Key Type | Managed By | Customer Control |
|---|---|---|
| AWS-Owned | AWS | Minimal |
| AWS-Managed | AWS | Limited |
| Customer Managed | Customer | Highest |

### Memory Trick

**OWNED**
→ AWS Everything

**MANAGED**
→ AWS Manages

**CUSTOMER MANAGED**
→ You Control

---

# Envelope Encryption

One of the most important KMS concepts is:

**Envelope Encryption**

Instead of using the KMS key directly to encrypt:

**Large amounts of data**

KMS uses a:

**Data Key**

Architecture:

KMS Key  
↓  
Generate Data Key  
↓  
Data Key Encrypts Application Data  
↓  
Encrypted Data Key Stored with Ciphertext

### Killer Exam Clue

> **Encrypt large data efficiently using KMS**
>
> → **Envelope Encryption**

---

# Why Envelope Encryption?

KMS keys are designed to protect:

**Smaller cryptographic keys**

rather than directly encrypting huge files.

So:

Large File  
↓  
Encrypted with Data Key

Data Key  
↓  
Encrypted with KMS Key

### Memory Trick

**KMS Key encrypts the key**

**Data Key encrypts the data**

---

# Data Keys

A:

**Data Key**

is generated for:

**Encrypting application data**

KMS can return:

- Plaintext data key
- Encrypted data key

The application uses:

**Plaintext key**

to encrypt data

then discards it.

It stores:

**Encrypted data key**

with the encrypted data.

---

# Decryption Flow

Encrypted Data  
+  
Encrypted Data Key  
↓  
KMS Decrypts Data Key  
↓  
Plaintext Data Key  
↓  
Decrypt Application Data

### Memory Trick

**Unlock the small key first**

**Then unlock the data**

---

# KMS Key Policies

A:

**Key Policy**

is a resource-based policy attached directly to:

**A KMS key**

It controls:

**Who can use and administer the key**

### Killer Exam Clue

> **User has IAM permission but still cannot use a KMS key**
>
> → Check the **KMS Key Policy**

---

# Key Policy Importance

KMS access commonly depends on:

- Key policy
- IAM policy
- Grants

The key policy is especially important because:

**KMS keys have their own authorization boundary**

### Memory Trick

**KMS Permission Problem? Check Key Policy**

---

# IAM Policies

IAM policies can grant permissions such as:

- `kms:Encrypt`
- `kms:Decrypt`
- `kms:GenerateDataKey`

But effective access must still align with:

**The key policy**

---

# KMS Grants

A:

**Grant**

allows permissions on a KMS key to be delegated to:

**Another principal**

Grants are often used by:

**AWS services**

to use keys on your behalf.

### Exam Concept

> **KMS grants provide delegated key permissions without constantly modifying the key policy**

---

# Key Administrators vs Key Users

These are different responsibilities.

## Key Administrator

Can perform management tasks such as:

- Modify key
- Configure rotation
- Disable key
- Schedule deletion

## Key User

Can perform cryptographic operations such as:

- Encrypt
- Decrypt
- Generate data keys

### Memory Trick

**Admin = Manage the Key**

**User = Use the Key**

---

# Key Rotation

KMS supports:

**Key rotation**

for supported key types.

Rotation changes:

**Underlying cryptographic material**

without requiring applications to change:

**The logical KMS key identifier**

### Killer Exam Clue

> **Need periodic cryptographic key rotation without changing application references**
>
> → **KMS Key Rotation**

---

# Automatic Rotation

Customer managed symmetric KMS keys can support:

**Automatic rotation**

according to supported configuration.

AWS-managed keys also use:

**AWS-managed rotation behavior**

### Exam Principle

> **Rotation does not normally require re-encrypting every existing object immediately**

---

# Old Ciphertext After Rotation

When a KMS key rotates:

Previously encrypted data can still be:

**Decrypted**

KMS retains the required:

**Older key material**

### Exam Trap

> Rotation does NOT make old encrypted data unreadable.

---

# Manual Rotation

Manual rotation can be achieved by:

**Creating a new KMS key**

and updating:

**Aliases/applications**

to use it.

This gives more explicit:

**Key lifecycle control**

---

# Key Aliases

A:

**Key Alias**

provides a friendly name for:

**A KMS key**

Example:

`alias/app-production`

This makes applications easier to manage than using:

**Raw key IDs**

### Memory Trick

**Alias = Friendly Pointer**

---

# Multi-Region Keys

KMS supports:

**Multi-Region keys**

These are related KMS keys in:

**Different AWS Regions**

with the same:

**Key material**

### Killer Exam Clue

> **Need compatible KMS keys in multiple Regions for a multi-Region application**
>
> → **Multi-Region KMS Keys**

---

# Multi-Region Key Architecture

Region A  
↓  
Primary Multi-Region Key

Replicated To  
↓

Region B  
↓  
Replica Multi-Region Key

This can help applications that need:

**Cross-Region cryptographic compatibility**

---

# Regional Nature of KMS

Standard KMS keys are:

**Regional resources**

A KMS key created in:

`us-east-1`

does not automatically exist in:

`us-west-2`

unless using:

**Multi-Region key capabilities**

### Killer Exam Trap

> **KMS key is normally Region-specific**

---

# KMS + S3

[[S3]] can use:

**SSE-KMS**

Architecture:

S3 Object  
↓  
Data Key  
↓  
KMS Key

Benefits include:

- Centralized key control
- Auditability
- Customer-managed key option

### Killer Exam Clue

> **Need S3 server-side encryption with customer-controlled KMS permissions**
>
> → **SSE-KMS with Customer Managed Key**

---

# SSE-S3 vs SSE-KMS

## SSE-S3

AWS manages:

**Encryption keys for S3**

Minimal customer key management.

## SSE-KMS

Uses:

**KMS**

Provides:

- Key policies
- Auditability
- More access control

### Killer Shortcut

**Simplest S3 encryption**
→ SSE-S3

**Need key control/auditing**
→ SSE-KMS

---

# KMS + EBS

[[EBS]] encryption commonly uses:

**KMS**

Encryption can protect:

- EBS volumes
- Snapshots
- Data moving between EC2 and encrypted EBS

### Exam Pattern

> **Need customer-controlled encryption for EBS volumes**
>
> → **Customer Managed KMS Key**

---

# KMS + RDS

[[RDS]] can use:

**KMS encryption at rest**

This protects resources such as:

- Database storage
- Automated backups
- Snapshots
- Read replicas where supported/configured

---

# KMS + DynamoDB

[[DynamoDB]] supports encryption at rest with:

**KMS-integrated key options**

Choose customer managed keys when you need:

**More direct key control**

---

# KMS + Secrets Manager

[[Secrets Manager]] encrypts stored secrets using:

**KMS**

Architecture:

Secret  
↓  
KMS Encryption  
↓  
Secrets Manager

### SAA Principle

> **Secrets Manager stores the secret**
>
> **KMS protects the encryption key**

---

# KMS + Lambda

Lambda environment variables can be protected using:

**KMS-backed encryption**

For actual secrets:

Prefer:

**Secrets Manager**

rather than treating environment variables as:

**A secret-management system**

---

# KMS + CloudTrail

KMS API activity is logged through:

[[CloudTrail]]

This provides visibility into operations such as:

- Encrypt
- Decrypt
- Key management operations

### Killer Exam Clue

> **Need to audit KMS key usage**
>
> → **CloudTrail**

---

# Auditing Key Usage

Suppose security needs to know:

> Who used this customer managed key?

Architecture:

KMS API Activity  
↓  
CloudTrail  
↓  
Audit

### Memory Trick

**KMS Protects**

**CloudTrail Records**

---

# Key Deletion

Customer managed keys can be:

**Scheduled for deletion**

KMS requires a:

**Waiting period**

before permanent deletion.

### Killer Exam Warning

Deleting a KMS key can make encrypted data:

**Permanently unrecoverable**

---

# Disable vs Delete

## Disable Key

Key remains:

**Present**

but cannot currently perform:

**Cryptographic operations**

This is reversible.

## Delete Key

After the waiting period:

**Key material is permanently removed**

This can make ciphertext:

**Unrecoverable**

### Memory Trick

**Disable = Pause**

**Delete = Destroy**

---

# Key Deletion Exam Trap

If data is encrypted using:

**A KMS key**

and that key is permanently deleted:

The encrypted data may become:

**Impossible to decrypt**

### Killer Exam Principle

> **Protect the lifecycle of encryption keys as carefully as the encrypted data**

---

# Imported Key Material

KMS supports scenarios where customers can:

**Import their own key material**

into supported KMS keys.

Use when compliance requires:

**Customer-supplied cryptographic material**

---

# External Key Store

KMS can integrate with:

**External key-management architectures**

for organizations requiring even greater control over:

**Cryptographic key material**

For SAA, the main concept is:

> **Some compliance requirements may require customer-controlled or externally managed key material**

---

# KMS vs CloudHSM

This is a major security comparison.

## KMS

Think:

- Managed key service
- Deep AWS integration
- Key policies
- Encryption across AWS services
- Minimal infrastructure management

## [[06-Security/CloudHSM]]

Think:

- Dedicated hardware security modules
- Customer-controlled HSM cluster
- Greater control
- Specialized cryptographic requirements

### Killer Shortcut

**Managed encryption keys**
→ KMS

**Dedicated customer-controlled HSM**
→ CloudHSM

---

# KMS vs Secrets Manager

## KMS

Manages:

**Encryption keys**

## [[Secrets Manager]]

Manages:

**Passwords, API keys, database credentials**

### Memory Trick

**KMS = KEY**

**Secrets Manager = SECRET**

---

# KMS vs ACM

## KMS

Think:

**Encryption keys for data**

## [[AWS Certificate Manager]]

Think:

**TLS certificates**

### Killer Shortcut

**Encrypt stored data**
→ KMS

**HTTPS certificate**
→ ACM

---

# KMS vs SSM Parameter Store

Parameter Store can hold:

**Configuration values and secure parameters**

KMS can be used to encrypt:

**SecureString values**

Think:

Parameter Store  
→ Stores configuration

KMS  
→ Encrypts protected values

---

# Client-Side Encryption

With:

**Client-side encryption**

the application encrypts data:

**Before sending it to AWS**

KMS can help generate/manage:

**Encryption keys**

---

# Server-Side Encryption

With:

**Server-side encryption**

AWS encrypts the data:

**After receiving it**

Examples:

- S3 SSE-KMS
- EBS encryption
- RDS encryption

### Memory Trick

**Client-Side = Encrypt Before Upload**

**Server-Side = AWS Encrypts After Receipt**

---

# Throttling

KMS APIs have:

**Request quotas**

A highly scaled application making excessive direct KMS calls can encounter:

**Throttling**

Envelope encryption helps because applications can:

**Use data keys locally**

instead of sending every byte through:

**KMS**

---

# Architecture Thinking

## Scenario 1 — Customer-Controlled S3 Encryption

Company requires:

- S3 encryption
- Customer-controlled key permissions
- Audit trail of key usage

Choose:

**SSE-KMS + Customer Managed Key**

---

## Scenario 2 — HTTPS Website

Need:

**TLS certificate**

Do NOT choose KMS.

Choose:

**ACM**

---

## Scenario 3 — Database Password

Need to securely store and rotate:

**RDS credentials**

Do NOT store the password in KMS.

Choose:

**Secrets Manager**

KMS can protect:

**The encryption key**

---

## Scenario 4 — Dedicated HSM

Compliance requires:

**Dedicated hardware security modules under customer control**

Choose:

**CloudHSM**

---

## Scenario 5 — Cross-Region Encryption

Application needs compatible key material in:

Two Regions.

Choose:

**Multi-Region KMS Keys**

---

## Scenario 6 — User Cannot Decrypt

IAM policy contains:

`kms:Decrypt`

but access still fails.

Check:

**KMS Key Policy**

---

## Scenario 7 — Key Rotation

Security requires periodic:

**Cryptographic key rotation**

without changing application references.

Choose:

**KMS Automatic Rotation**

---

## Scenario 8 — Large File

Application needs to encrypt:

10 GB file.

Do NOT send the entire file to KMS for encryption.

Use:

**Envelope Encryption**

---

## Scenario 9 — Audit Decrypt Usage

Need to determine:

**Who called KMS Decrypt**

Choose:

**CloudTrail**

---

## Scenario 10 — Temporary Key Shutdown

Security incident requires stopping:

**All key usage**

without permanently destroying it.

Choose:

**Disable the KMS key**

---

# Scenario Recognition

Immediately think:

**KMS**

when you see:

- Encryption key
- Encrypt at rest
- Customer managed key
- Key policy
- Envelope encryption
- Key rotation
- KMS key
- SSE-KMS
- Audit encryption-key usage

---

## Think Customer Managed Key When You See

- Full key-policy control
- Customer-controlled permissions
- Disable key
- Schedule deletion
- Custom rotation requirements

---

## Think Envelope Encryption When You See

- Large data
- Data keys
- Encrypt key with another key
- GenerateDataKey

---

## Think CloudHSM When You See

- Dedicated HSM
- Customer-controlled hardware
- Specialized compliance

---

# Exam Traps

## Trap 1 — KMS Stores Database Passwords

❌

Think:

**Secrets Manager**

KMS manages:

**Encryption keys**

---

## Trap 2 — KMS Is Mainly for TLS Certificates

❌

Think:

**ACM**

---

## Trap 3 — AWS-Managed and Customer Managed Keys Provide the Same Control

❌

Customer managed keys provide:

**More customer control**

---

## Trap 4 — KMS Keys Are Global by Default

❌

They are normally:

**Regional**

---

## Trap 5 — Rotate Key = Old Data Cannot Be Decrypted

❌

KMS retains required:

**Old key material**

---

## Trap 6 — Deleting KMS Key Is Harmless

❌

Ciphertext encrypted under it may become:

**Permanently unrecoverable**

---

## Trap 7 — IAM Permission Alone Always Grants KMS Access

❌

Check:

**Key Policy**

---

## Trap 8 — KMS Directly Encrypts Huge Files as the Normal Pattern

❌

Use:

**Envelope Encryption**

---

# Quick Cheat Sheet

| Exam Clue | Answer |
|---|---|
| Encryption Key Management | KMS |
| Full Customer Key Control | Customer Managed Key |
| AWS Controls Key Completely | AWS-Owned Key |
| AWS Service-Managed Key | AWS-Managed Key |
| Encrypt Large Data | Envelope Encryption |
| Encrypt Data | Data Key |
| Encrypt Data Key | KMS Key |
| Control KMS Access | Key Policy |
| Friendly Key Name | Alias |
| Periodic Key Material Change | Rotation |
| Cross-Region Compatible Keys | Multi-Region Keys |
| S3 Customer-Controlled Encryption | SSE-KMS |
| Audit Key Usage | CloudTrail |
| Dedicated Hardware HSM | CloudHSM |
| Store Passwords/Secrets | Secrets Manager |
| TLS Certificate | ACM |

---

# Encryption Decision Map

Need:

**Encryption key management**

→ KMS

Need:

**Dedicated customer-controlled HSM**

→ CloudHSM

Need:

**Secret storage/rotation**

→ Secrets Manager

Need:

**TLS certificate**

→ ACM

Need:

**Encrypt large application data**

→ Envelope Encryption

Need:

**Audit encryption key use**

→ CloudTrail

---

# KMS Key Decision

Need:

**Simplest AWS-managed encryption**

→ AWS-Owned / AWS-Managed depending service

Need:

**Control key policy**

→ Customer Managed Key

Need:

**Disable/delete/alias/grants**

→ Customer Managed Key

Need:

**Cross-Region key compatibility**

→ Multi-Region Key

---

# Final Exam Rapid-Fire

> **ENCRYPTION KEYS**
> → KMS
>
> **CUSTOMER KEY CONTROL**
> → CUSTOMER MANAGED KEY
>
> **AWS SERVICE KEY**
> → AWS-MANAGED KEY
>
> **LARGE DATA**
> → ENVELOPE ENCRYPTION
>
> **DATA ENCRYPTION**
> → DATA KEY
>
> **PROTECT DATA KEY**
> → KMS KEY
>
> **KMS PERMISSIONS**
> → KEY POLICY
>
> **FRIENDLY KEY NAME**
> → ALIAS
>
> **KEY ROTATION**
> → KMS ROTATION
>
> **MULTI-REGION KEY**
> → KMS MULTI-REGION
>
> **S3 + KEY CONTROL**
> → SSE-KMS
>
> **AUDIT KMS**
> → CLOUDTRAIL
>
> **DEDICATED HSM**
> → CLOUDHSM
>
> **PASSWORD / API KEY**
> → SECRETS MANAGER
>
> **HTTPS CERTIFICATE**
> → ACM

---

## Master Memory Trick

> [!tip] KMS Master Memory Trick
> Imagine a giant bank vault.
>
> Your actual data is stored in:
>
> **LOCKED BOXES**
>
> Each box has its own small key:
>
> **DATA KEY**
>
> But you don't want those keys lying around.
>
> So the small keys are locked inside:
>
> **ANOTHER SECURE BOX**
>
> protected by:
>
> **THE KMS KEY**
>
> That's:
>
> **ENVELOPE ENCRYPTION**
>
> The KMS key does NOT need to encrypt the entire warehouse.
>
> It protects:
>
> **THE KEYS THAT PROTECT THE DATA**

So remember:

> **KMS**
> → MANAGE KEYS
>
> **DATA KEY**
> → ENCRYPT DATA
>
> **KMS KEY**
> → PROTECT DATA KEY
>
> **KEY POLICY**
> → WHO CAN USE KEY?
>
> **ROTATION**
> → CHANGE CRYPTOGRAPHIC MATERIAL
>
> **CLOUDTRAIL**
> → WHO USED KEY?
>
> **SECRETS MANAGER**
> → STORE SECRET
>
> **CLOUDHSM**
> → DEDICATED HARDWARE

And the killer SAA question:

> **"Does the requirement involve controlling, auditing, or managing encryption keys used by AWS services?"**
>
> YES
>
> → **KMS**

---

## Related Notes

- [[06-Security/CloudHSM]]
- [[Secrets Manager]]
- [[AWS Certificate Manager]]
- [[S3]]
- [[EBS]]
- [[RDS]]
- [[DynamoDB]]
- [[Lambda]]
- [[CloudTrail]]
- [[IAM]]
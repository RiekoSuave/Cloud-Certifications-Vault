## What Problem Does It Solve?

Manages encryption keys used to protect data in AWS.

AWS Key Management Service (KMS) helps remove the complexity of creating and managing encryption keys.

### Memory Trick

KMS = Key Management

---

## Type

Encryption Service

---

## What Is AWS KMS?

KMS stands for:

Key Management Service

AWS KMS manages encryption keys used to protect data.

Your course gives a very useful shortcut:

When you hear:

Encryption + AWS Service

Think:

KMS

### Memory Trick

Encryption in AWS?

→ Think KMS

---

## KMS and AWS Services

KMS integrates with many AWS services to provide encryption.

Your course gives several examples.

### Encryption Can Be Enabled

Examples include:

- EBS volumes
- S3 objects using SSE-KMS
- Amazon Redshift databases
- Amazon RDS databases
- Amazon EFS

### Memory Trick

KMS = Encryption Across AWS Services

---

## Encryption Automatically Enabled

Your course also identifies services where encryption is automatically enabled.

Examples include:

- CloudTrail Logs
- S3 Glacier
- Storage Gateway

The main exam idea is:

Some AWS services require you to choose or configure encryption options, while other services automatically provide encryption.

---

## Types of KMS Keys

Your course identifies three important categories:

1. Customer Managed Keys
2. AWS Managed Keys
3. AWS Owned Keys

---

## Customer Managed Key

A Customer Managed Key is created and managed by:

You — the customer.

You have more control over this type of key.

Your course identifies capabilities such as:

- Create the key
- Manage the key
- Enable or disable the key
- Configure key rotation
- Bring your own key

### Memory Trick

Customer Managed = YOU Control It

---

## Key Rotation

Customer Managed Keys can have a:

Rotation Policy

Your course describes rotation as periodically generating new key material while preserving the old key material so previously encrypted data remains usable.

### Memory Trick

Rotation = Refresh Encryption Key Material

---

## Bring Your Own Key

Customer Managed Keys can support:

Bring Your Own Key

This allows organizations to bring their own key material into AWS.

### Memory Trick

BYOK = Bring Your Own Key

---

## AWS Managed Key

AWS Managed Keys are:

Created and managed by AWS on the customer's behalf.

They are used by AWS services.

Examples from your course include:

- aws/s3
- aws/ebs
- aws/redshift

### Memory Trick

AWS Managed Key = AWS Manages It for Your Service

---

## AWS Owned Key

AWS Owned Keys are owned and managed by:

AWS

AWS services can use these keys to protect resources in your account.

Your course emphasizes that:

You cannot view these keys.

### Memory Trick

AWS Owned = AWS Controls It

---

## KMS Key Comparison

| Key Type | Who Manages It? | Customer Control |
|---|---|---|
| Customer Managed Key | Customer | Highest |
| AWS Managed Key | AWS on customer's behalf | Less |
| AWS Owned Key | AWS | Not visible to customer |

### Memory Trick

Customer Managed = YOU

AWS Managed = AWS for YOUR service

AWS Owned = AWS

---

## Encryption at Rest

KMS is commonly associated with protecting:

Data at Rest

Think:

Stored Data

↓

Encryption

↓

KMS Key

Examples from your course include:

- EBS
- S3
- RDS
- Redshift
- EFS

### Memory Trick

Stored Data + Encryption

→ KMS

---

## Common Use Cases

- Managing encryption keys
- Encrypting stored data
- Protecting sensitive information
- Controlling encryption keys
- Integrating encryption with AWS services

---

## Scenario Questions

A company needs to manage encryption keys in AWS.

→ AWS KMS

---

A company wants to encrypt an EBS volume.

→ Encryption + KMS

---

A company wants to use KMS encryption for objects stored in S3.

→ SSE-KMS

---

A company wants full control over creating and managing its KMS key.

→ Customer Managed Key

---

A company wants to enable or disable its own KMS key.

→ Customer Managed Key

---

A company wants to configure rotation for a key it manages.

→ Customer Managed Key

---

A company wants AWS to create and manage a key on its behalf for an AWS service.

→ AWS Managed Key

---

An AWS service uses encryption keys that the customer cannot view.

→ AWS Owned Key

---

## Don't Confuse These

Customer Managed Key = Customer Controls Key

AWS Managed Key = AWS Manages Key for Customer

AWS Owned Key = AWS Owns and Manages Key

KMS = Encryption Key Management

---

## Exam Keywords

AWS KMS

Key Management Service

Encryption

Encryption Keys

Customer Managed Key

AWS Managed Key

AWS Owned Key

Key Rotation

Bring Your Own Key

SSE-KMS

Encryption at Rest

---

## Quick Cheat Sheet

KMS = Key Management

Encryption + AWS = Think KMS

Customer Managed = YOU Control It

AWS Managed = AWS Manages It for Your Service

AWS Owned = AWS Controls It

Customer Managed Key = Rotation Possible

Customer Managed Key = Bring Your Own Key

EBS + Encryption = KMS

S3 + SSE-KMS = KMS

RDS + Encryption = KMS

Redshift + Encryption = KMS

EFS + Encryption = KMS
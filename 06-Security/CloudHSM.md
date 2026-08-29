See also: [KMS](06-Security/KMS.md)

## What Problem Does It Solve?

Provides hardware-based encryption and gives the customer control over encryption keys.

AWS CloudHSM is used when an organization needs dedicated hardware security modules and wants to manage its own encryption keys.

### Memory Trick

CloudHSM = Hardware Encryption

---

## Type

Hardware Security Module

---

## What Is CloudHSM?

CloudHSM stands for:

Cloud Hardware Security Module

It provides:

Hardware Encryption

The important distinction in your course is that with CloudHSM:

You manage your own encryption keys.

### Memory Trick

CloudHSM = YOU Manage the Keys

---

## Hardware Security Module (HSM)

CloudHSM uses:

Hardware Security Modules

These are dedicated hardware devices used for cryptographic operations and protecting encryption keys.

For your course, focus on:

CloudHSM = Hardware Encryption

---

## Customer Key Management

The major concept to remember is:

Customer manages the encryption keys.

This gives the customer more direct control over key management.

Think:

CloudHSM

↓

Hardware Encryption

↓

Customer Manages Keys

---

## CloudHSM vs KMS

This is the most important comparison for this note.

### AWS KMS

AWS manages the encryption-key service for you.

Think:

Managed Encryption Key Service

### AWS CloudHSM

Provides hardware encryption where:

You manage your encryption keys.

Think:

Customer-Controlled Hardware Encryption

| KMS | CloudHSM |
|---|---|
| Managed encryption key service | Hardware encryption |
| AWS-managed service | Dedicated HSM concept |
| AWS manages the service | Customer manages encryption keys |
| Easier key management | More customer control |

### Memory Trick

KMS = AWS Managed

CloudHSM = YOU Manage

See:

[KMS](06-Security/KMS.md)

---

## Common Use Cases

- Hardware-based encryption
- Managing your own encryption keys
- Workloads requiring greater control over encryption keys

---

## Scenario Questions

A company wants AWS to provide a managed service for encryption keys.

→ AWS KMS

---

A company requires hardware-based encryption and wants to manage its own encryption keys.

→ AWS CloudHSM

---

A company wants more direct control over encryption keys using hardware security modules.

→ AWS CloudHSM

---

## Don't Confuse These

KMS = Managed Encryption Keys

CloudHSM = Hardware Encryption

KMS = AWS Managed

CloudHSM = Customer Manages Keys

---

## Exam Keywords

AWS CloudHSM

HSM

Hardware Security Module

Hardware Encryption

Encryption Keys

Customer Managed

KMS

---

## Quick Cheat Sheet

CloudHSM = Hardware Encryption

HSM = Hardware Security Module

CloudHSM = YOU Manage the Keys

KMS = Managed Encryption Key Service

KMS → AWS Managed

CloudHSM → Customer Managed
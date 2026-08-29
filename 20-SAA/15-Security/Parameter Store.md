## What Problem Does It Solve?

[[Parameter Store]] provides:

**Secure, hierarchical storage for application configuration and parameters**

It is part of:

**Systems Manager**

Common examples:

- Database connection strings
- Application settings
- Environment variables
- AMI IDs
- License keys
- Passwords
- Configuration values

Architecture:

Application  
↓  
IAM Role  
↓  
Parameter Store  
↓  
Retrieve Configuration

> [!tip] Memory Trick
> **Parameter Store = Application Configuration Store**

---

## Core Concept

Instead of hardcoding configuration:

`database_host = prod-db.example.com`

store it centrally:

Parameter Store  
↓  
`/prod/database/host`

Applications retrieve the value:

**At runtime**

### Killer Exam Clue

> **Need centralized hierarchical storage for application configuration**
>
> → **Parameter Store**

---

# Parameter Hierarchy

Parameters can use:

**Hierarchical names**

Example:

`/dev/database/host`

`/dev/database/password`

`/prod/database/host`

`/prod/database/password`

This makes it easy to organize configuration by:

- Environment
- Application
- Team
- Service

### Memory Trick

**Parameter Store = Folders for Configuration**

---

# Parameter Types

Parameter Store supports three important parameter types:

## String

Stores:

**Plaintext string data**

Example:

`/prod/app/region = us-east-1`

---

## StringList

Stores:

**Comma-separated values**

Example:

`us-east-1a,us-east-1b,us-east-1c`

---

## SecureString

Stores sensitive values:

**Encrypted using [[KMS]]**

Example:

`/prod/database/password`

Architecture:

SecureString  
↓  
KMS Encryption  
↓  
Parameter Store

### Killer Exam Clue

> **Need an encrypted configuration parameter**
>
> → **SecureString + KMS**

---

# SecureString

SecureString is important because Parameter Store can store:

**Sensitive configuration**

without keeping it:

**In plaintext**

Examples:

- Passwords
- Tokens
- License keys
- Sensitive configuration

### Memory Trick

**String = Plain**

**SecureString = KMS**

---

# Parameter Store + KMS

[[KMS]] protects:

**SecureString parameters**

Parameter Store stores:

**The parameter**

KMS handles:

**Encryption**

### Killer Shortcut

**Store encrypted parameter**
→ Parameter Store

**Manage encryption key**
→ KMS

---

# IAM Access

Applications retrieve parameters using:

**IAM permissions**

Architecture:

EC2 / Lambda / ECS  
↓  
IAM Role  
↓  
Parameter Store

This avoids:

**Hardcoded AWS credentials**

### SAA Principle

> **Use IAM roles to give applications access to only the parameters they need**

---

# Example IAM Design

Application needs:

`/prod/app/*`

Grant access to:

**Only that parameter hierarchy**

instead of:

**Every parameter in the account**

### Memory Trick

**Hierarchy + IAM = Organized Least Privilege**

---

# Parameter Store + EC2

Applications running on:

[[EC2]]

can retrieve configuration using:

**Instance Roles**

Architecture:

EC2 Application  
↓  
Instance Role  
↓  
Parameter Store

Example:

EC2 retrieves:

- Database endpoint
- Application mode
- API URL

---

# Parameter Store + Lambda

[[Lambda]] can retrieve parameters using:

**Its execution role**

Architecture:

Lambda  
↓  
Execution Role  
↓  
Parameter Store

Useful for:

**Centralized serverless configuration**

---

# Parameter Store + ECS

Applications running in:

[[ECS]]

can use Parameter Store for:

**Container configuration and sensitive values**

This avoids embedding configuration directly inside:

**Container images**

---

# Parameter Store + CloudFormation

Parameter Store can help separate:

**Configuration**

from:

**Infrastructure templates**

Instead of hardcoding:

AMI IDs

inside every template, you can reference:

**Parameters**

### Killer Exam Clue

> **Need centrally maintained configuration that infrastructure deployments can reference**
>
> → **Parameter Store**

---

# Public Parameters

Parameter Store also provides:

**AWS-managed public parameters**

These can expose useful AWS-maintained values.

A notable example is:

**Latest AMI information**

### Killer Exam Clue

> **Need to dynamically reference the latest AWS-provided AMI instead of hardcoding an AMI ID**
>
> → **Parameter Store Public Parameters**

---

# Standard Parameters

Parameter Store provides:

**Standard parameters**

for common configuration-storage requirements.

Think:

- Simpler use cases
- Lower limits
- Lower cost

---

# Advanced Parameters

**Advanced parameters**

provide additional capabilities and higher limits.

Think:

- Larger parameter values
- More parameters
- Parameter policies
- More advanced requirements

### Memory Trick

**Standard = Simple**

**Advanced = More Features**

---

# Parameter Policies

Advanced parameters can use:

**Parameter Policies**

to help manage:

**Parameter lifecycle**

Examples include policies involving:

- Expiration
- Expiration notification
- No-change notification

### Killer Exam Clue

> **Need notification when a parameter has not changed for a defined period**
>
> → **Parameter Policy**

---

# Parameter Versioning

When a parameter changes:

Parameter Store maintains:

**Versions**

Example:

Version 1  
→ Old Database Host

Version 2  
→ New Database Host

This helps applications and administrators track:

**Parameter updates**

---

# Parameter Labels

Labels can provide:

**Friendly references to parameter versions**

Example concept:

Version 5  
→ `CURRENT`

Version 4  
→ `PREVIOUS`

This can simplify:

**Configuration deployment workflows**

---

# Parameter Store vs Secrets Manager

This is the most important comparison.

## Parameter Store

Think:

- Configuration
- Hierarchical parameters
- SecureString
- KMS encryption
- Lower-cost/simple storage
- No built-in automatic credential rotation like Secrets Manager

## [[Secrets Manager]]

Think:

- Secrets
- Database credentials
- API keys
- Automatic rotation
- Secret lifecycle management

### Killer Shortcut

**Application configuration**
→ Parameter Store

**Secret requiring automatic rotation**
→ Secrets Manager

---

# Configuration vs Secret

Example:

Database endpoint:

`prod-db.example.com`

→ Parameter Store

Database password:

`SuperSecretPassword`

Could technically be:

**SecureString**

but if the requirement includes:

**Automatic credential rotation**

choose:

**Secrets Manager**

### Memory Trick

**Parameter Store = CONFIG**

**Secrets Manager = SECRET + ROTATE**

---

# Parameter Store vs KMS

## [[KMS]]

Manages:

**Encryption keys**

## Parameter Store

Stores:

**Configuration values**

KMS can encrypt:

**SecureString**

### Killer Shortcut

**Value**
→ Parameter Store

**Encryption key**
→ KMS

---

# Parameter Store vs AppConfig

Parameter Store:

**Stores configuration values**

AppConfig:

**Deploys and manages application configuration changes**

For SAA, think:

**Parameter Store = Store**

**AppConfig = Deploy Configuration**

---

# Parameter Store vs S3

You could store configuration files in:

[[S3]]

but Parameter Store provides features designed specifically for:

- Parameters
- Hierarchies
- IAM access
- SecureString
- Versioning

### Exam Principle

> **For centralized application parameters, Parameter Store is usually more purpose-built than an arbitrary S3 object**

---

# Secrets Manager Rotation Difference

Parameter Store does NOT provide the same purpose-built:

**Automatic database credential rotation**

as:

[[Secrets Manager]]

### Killer Exam Trap

Question says:

> Rotate RDS password automatically every 30 days.

Choose:

**Secrets Manager**

not Parameter Store.

---

# Parameter Store and Secrets Manager Integration

Parameter Store can reference:

**Secrets Manager secrets**

This allows Systems Manager workflows to access:

**Secrets managed by Secrets Manager**

For the exam, remember:

> They are complementary services, not necessarily mutually exclusive.

---

# Auditing

Parameter Store API activity can be audited using:

[[CloudTrail]]

This can help determine:

- Who retrieved parameters
- Who changed parameters
- Who deleted parameters

### Memory Trick

**Parameter Store stores**

**CloudTrail audits**

---

# Monitoring

Operational monitoring can integrate with:

[[CloudWatch]]

while:

[[CloudTrail]]

focuses on:

**API activity**

---

# Architecture Thinking

## Scenario 1 — Environment Configuration

Application needs:

- `/prod/database/host`
- `/prod/app/region`
- `/prod/api/url`

Choose:

**Parameter Store**

---

## Scenario 2 — Encrypted Configuration

Application needs:

**Sensitive license key**

but no automatic rotation requirement.

Choose:

**SecureString**

with:

**KMS**

---

## Scenario 3 — RDS Password Rotation

Application needs:

**Automatic database password rotation**

Choose:

**Secrets Manager**

---

## Scenario 4 — Latest AMI

CloudFormation needs:

**Latest supported AMI ID**

without manually updating:

**The template**

Choose:

**Parameter Store Public Parameter**

---

## Scenario 5 — Encryption Key

Need:

**Customer-controlled encryption key**

Choose:

**KMS**

not Parameter Store.

---

## Scenario 6 — EC2 Application Configuration

EC2 instances need:

**Production application settings**

without hardcoding them into:

**The AMI**

Choose:

EC2  
↓  
IAM Role  
↓  
Parameter Store

---

## Scenario 7 — Container Configuration

ECS application needs:

**Environment-specific configuration**

without baking it into:

**Container image**

Choose:

**Parameter Store**

---

# Scenario Recognition

Immediately think:

**Parameter Store**

when you see:

- Application configuration
- Hierarchical parameters
- SecureString
- Configuration values
- Central parameter storage
- Latest AMI parameter
- Systems Manager parameters

---

## Think SecureString When You See

- Encrypted parameter
- Sensitive configuration
- KMS-backed value

---

## Think Secrets Manager When You See

- Automatic rotation
- Database credentials
- Secret lifecycle
- API key rotation

---

## Think KMS When You See

- Encryption key
- Key policy
- Customer managed key
- Envelope encryption

---

# Exam Traps

## Trap 1 — Parameter Store Is Only for Plaintext Values

❌

Use:

**SecureString**

for encrypted values.

---

## Trap 2 — SecureString Replaces KMS

❌

SecureString uses:

**KMS**

for encryption.

---

## Trap 3 — Parameter Store and Secrets Manager Are Identical

❌

Parameter Store:

**Configuration-focused**

Secrets Manager:

**Secret lifecycle + rotation**

---

## Trap 4 — Parameter Store Automatically Rotates RDS Passwords

❌

Think:

**Secrets Manager**

---

## Trap 5 — Applications Need Hardcoded AWS Credentials to Retrieve Parameters

❌

Use:

**IAM Roles**

---

## Trap 6 — AMI IDs Must Always Be Hardcoded

❌

AWS-managed public parameters can help retrieve:

**Current AMI information**

---

# Quick Cheat Sheet

| Exam Clue | Answer |
|---|---|
| Application Configuration | Parameter Store |
| Hierarchical Configuration | Parameter Store |
| Plaintext Parameter | String |
| Comma-Separated Values | StringList |
| Encrypted Parameter | SecureString |
| SecureString Encryption | KMS |
| Automatic Secret Rotation | Secrets Manager |
| Latest AWS AMI Parameter | Public Parameter |
| Application Access | IAM Role |
| Audit Parameter API Calls | CloudTrail |
| Parameter Lifecycle Controls | Parameter Policies |

---

# Parameter Decision Map

Need:

**Application configuration**

→ Parameter Store

Need:

**Encrypted configuration**

→ SecureString + KMS

Need:

**Database password with rotation**

→ Secrets Manager

Need:

**Encryption key**

→ KMS

Need:

**Latest AWS-managed AMI value**

→ Parameter Store Public Parameter

Need:

**Audit parameter changes**

→ CloudTrail

---

# Parameter Store vs Secrets Manager

| Requirement | Parameter Store | Secrets Manager |
|---|---:|---:|
| Configuration | ✅ | Possible |
| Hierarchical Parameters | ✅ | ❌ Primary Use |
| Encrypted Values | ✅ | ✅ |
| KMS Integration | ✅ | ✅ |
| Automatic Secret Rotation | ❌ | ✅ |
| Database Credential Management | Basic Storage | ✅ Best Fit |
| API Keys | Possible | ✅ Best Fit |
| Public AWS Parameters | ✅ | ❌ |

---

# Final Exam Rapid-Fire

> **APP CONFIG**
> → PARAMETER STORE
>
> **HIERARCHICAL CONFIG**
> → PARAMETER STORE
>
> **PLAIN VALUE**
> → STRING
>
> **ENCRYPTED VALUE**
> → SECURESTRING
>
> **SECURESTRING ENCRYPTION**
> → KMS
>
> **SECRET + ROTATION**
> → SECRETS MANAGER
>
> **LATEST AMI**
> → PUBLIC PARAMETER
>
> **APP ACCESS**
> → IAM ROLE
>
> **AUDIT PARAMETER ACCESS**
> → CLOUDTRAIL

---

## Master Memory Trick

> [!tip] Parameter Store Master Memory Trick
> Imagine your application has:
>
> **A giant configuration filing cabinet**
>
> The drawers are organized:
>
> `/dev/`
>
> `/test/`
>
> `/prod/`
>
> Inside are values such as:
>
> **DATABASE HOST**
>
> **API URL**
>
> **REGION**
>
> **AMI ID**
>
> That's:
>
> **PARAMETER STORE**
>
> Some drawer contents are sensitive.
>
> Put them inside:
>
> **SECURESTRING**
>
> and lock them using:
>
> **KMS**
>
> But then someone says:
>
> **"This is our production database password, and it must automatically rotate."**
>
> Move that one to:
>
> **SECRETS MANAGER**

So remember:

> **PARAMETER STORE**
> → CONFIGURATION
>
> **HIERARCHY**
> → ORGANIZE
>
> **SECURESTRING**
> → ENCRYPTED PARAMETER
>
> **KMS**
> → ENCRYPT
>
> **SECRETS MANAGER**
> → SECRET + ROTATE
>
> **IAM ROLE**
> → APPLICATION ACCESS
>
> **CLOUDTRAIL**
> → AUDIT

And the killer SAA question:

> **"Does the application need centralized, hierarchical configuration storage without a requirement for automatic secret rotation?"**
>
> YES
>
> → **Parameter Store**

---

## Related Notes

- [[Secrets Manager]]
- [[KMS]]
- [[Systems Manager]]
- [[CloudTrail]]
- [[CloudWatch]]
- [[Lambda]]
- [[EC2]]
- [[ECS]]
- [[S3]]
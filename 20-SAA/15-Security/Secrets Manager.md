## What Problem Does It Solve?

[[Secrets Manager]] securely stores and manages:

**Application secrets**

Examples include:

- Database passwords
- API keys
- OAuth tokens
- Service credentials
- Application secrets

It helps applications avoid:

**Hardcoding sensitive values in code**

Architecture:

Application  
↓  
Secrets Manager  
↓  
Retrieve Secret  
↓  
Authenticate to Service

> [!tip] Memory Trick
> **Secrets Manager = Store + Rotate Secrets**

---

## Core Concept

Secrets Manager solves a different problem from:

[[KMS]]

### Secrets Manager

Stores:

**The secret itself**

Examples:

- Password
- API token
- Database credential

### KMS

Protects:

**Encryption keys**

### Killer Exam Shortcut

**Need to store a password**
→ Secrets Manager

**Need to manage encryption keys**
→ KMS

---

# What Is a Secret?

A:

**Secret**

is sensitive information that an application should not expose.

Examples:

- `DatabasePassword`
- `API_KEY`
- `OAuthToken`
- `PrivateCredential`

Instead of:

Application Code  
↓  
Hardcoded Password

use:

Application  
↓  
Secrets Manager  
↓  
Retrieve Secret at Runtime

### SAA Principle

> **Do not hardcode credentials in application code**

---

# Secret Values

A secret can contain:

**Key-value data**

Example concept:

`username = appuser`

`password = SuperSecretPassword`

Secrets can also contain:

**Other sensitive application information**

---

# Encryption at Rest

Secrets Manager encrypts secrets at rest using:

[[KMS]]

Architecture:

Secret  
↓  
KMS Encryption  
↓  
Stored Secret

### Memory Trick

**Secrets Manager stores**

**KMS encrypts**

---

# Encryption in Transit

Applications communicate with Secrets Manager using:

**HTTPS**

This protects secrets:

**In transit**

---

# Automatic Secret Rotation

One of the most important Secrets Manager features is:

**Automatic Rotation**

Secrets Manager can periodically change:

**Credentials**

without requiring administrators to manually update:

**Every application**

### Killer Exam Clue

> **Automatically rotate database credentials**
>
> → **Secrets Manager**

---

# Rotation Architecture

Secrets Manager  
↓  
Rotation Schedule  
↓  
[[Lambda]] Rotation Function  
↓  
Update Credential  
↓  
Update Stored Secret

### Memory Trick

**Secrets Manager + Lambda = Rotate**

---

# Rotation Function

Automatic rotation commonly uses:

**Lambda**

to perform steps such as:

- Create new credential
- Update target service
- Test new credential
- Finish rotation

### Exam Principle

> **Rotation changes both the stored secret and the credential at the target system**

---

# RDS Credential Rotation

Secrets Manager has strong integration with:

[[RDS]]

and related database services.

Architecture:

Application  
↓  
Secrets Manager  
↓  
Database Credential  
↓  
RDS

Rotation:

Secrets Manager  
↓  
Lambda  
↓  
Change RDS Password  
↓  
Store New Secret

### Killer Exam Clue

> **Need automatic rotation of RDS database credentials**
>
> → **Secrets Manager**

---

# Aurora Credential Rotation

The same concept applies to:

**Aurora**

Use Secrets Manager when you want:

- Centralized credentials
- Secure storage
- Automatic rotation

---

# Application Retrieval

An application can retrieve a secret using:

**AWS APIs / SDKs**

Architecture:

Application  
↓  
IAM Role  
↓  
Secrets Manager  
↓  
Secret Value

The application should use:

**Temporary IAM credentials**

to authenticate to Secrets Manager.

---

# IAM Permissions

Applications need appropriate permissions such as:

**Permission to retrieve the required secret**

Follow:

**Least privilege**

Example concept:

Application Role  
↓  
Can Read  
↓  
Only `ProductionDatabaseSecret`

### Killer Exam Principle

> **Grant applications access only to the secrets they actually need**

---

# Secret Resource Policies

Secrets Manager supports:

**Resource-based policies**

for controlling access to:

**Secrets**

This can help with:

- Cross-account access
- Centralized secret management
- Additional access controls

---

# Cross-Account Access

A secret can be shared with:

**Another AWS account**

using appropriate:

- Resource policy
- IAM permissions
- KMS permissions

### Killer Exam Clue

> **Application in Account B must retrieve a secret stored in Account A**
>
> → **Secrets Manager resource policy + appropriate IAM/KMS access**

---

# KMS Permissions

Because Secrets Manager uses KMS encryption:

Access may require:

- Secrets Manager permission
- KMS permission

depending on:

**The KMS key configuration**

### Exam Trap

If the application can call Secrets Manager but receives:

**AccessDenied while decrypting**

check:

**KMS permissions**

---

# Customer Managed KMS Key

Secrets can use:

**Customer Managed KMS Keys**

when you need:

- More key control
- Custom key policies
- Audit requirements
- Cross-account key design

---

# Versioning

Secrets Manager maintains:

**Versions of secrets**

This helps support:

**Rotation**

and controlled transitions between:

**Old and new credentials**

---

# Version Stages

Secret versions can have labels such as:

**AWSCURRENT**

and:

**AWSPREVIOUS**

For SAA, the important concept is:

> **Secrets Manager can keep track of current and previous secret versions during rotation**

---

# Secret Rotation Workflow

Conceptually:

Current Secret  
↓  
Generate New Secret  
↓  
Update Database  
↓  
Test New Secret  
↓  
Mark New Secret Current  
↓  
Old Secret Becomes Previous

### Memory Trick

**Rotate → Test → Promote**

---

# Secret Caching

Applications that retrieve secrets frequently can use:

**Caching**

to reduce:

- API calls
- Latency
- Cost

### SAA Principle

> **Do not retrieve the same unchanged secret on every single request when caching is appropriate**

---

# Secrets Manager + Lambda

[[Lambda]] commonly retrieves secrets such as:

- Database credentials
- API keys
- Third-party tokens

Architecture:

Lambda  
↓  
Execution Role  
↓  
Secrets Manager  
↓  
Secret

### Killer Exam Clue

> **Lambda needs database credentials without hardcoding them**
>
> → **Secrets Manager**

---

# Secrets Manager + ECS

Containerized applications in:

[[ECS]]

can retrieve:

**Secrets**

at runtime using appropriate:

**Task roles / integrations**

This avoids putting credentials directly into:

**Container images**

---

# Secrets Manager + EC2

Applications running on:

[[EC2]]

can retrieve secrets using:

**Instance roles**

Architecture:

EC2 Application  
↓  
IAM Role  
↓  
Secrets Manager

Do NOT store:

**Long-term AWS credentials**

on the instance just to access secrets.

---

# Secrets Manager + CloudFormation

Infrastructure deployments can reference:

**Secrets**

without embedding their plaintext values directly into:

**Templates**

The broader exam principle is:

> **Keep secrets separate from infrastructure-as-code files**

---

# Secrets Manager + CloudTrail

Secrets Manager API activity can be audited using:

[[CloudTrail]]

This helps answer:

- Who retrieved a secret?
- Who modified rotation?
- Who changed secret configuration?

### Memory Trick

**Secrets Manager protects**

**CloudTrail audits**

---

# Secrets Manager vs Parameter Store

This is a major SAA comparison.

## Secrets Manager

Think:

- Secrets
- Automatic rotation
- Database credentials
- API keys
- Purpose-built secret management

## Systems Manager Parameter Store

Think:

- Application configuration
- Parameters
- SecureString
- Hierarchical configuration
- Lower-cost/simple secret storage use cases

### Killer Shortcut

**Need automatic rotation**
→ Secrets Manager

**Need configuration parameter**
→ Parameter Store

---

# SecureString

Parameter Store can store encrypted values using:

**SecureString**

with:

[[KMS]]

This means Parameter Store can hold:

**Sensitive values**

but Secrets Manager is more purpose-built for:

**Secret lifecycle and rotation**

### Memory Trick

**Parameter Store = Config**

**Secrets Manager = Credentials**

---

# Secrets Manager vs KMS

## [[KMS]]

Stores/manages:

**Encryption keys**

## Secrets Manager

Stores/manages:

**Secrets**

### Killer Shortcut

Encryption key  
→ KMS

Password / API key  
→ Secrets Manager

---

# Secrets Manager vs CloudHSM

## [[CloudHSM]]

Think:

**Dedicated cryptographic hardware**

## Secrets Manager

Think:

**Application credentials**

### Example

Private signing key requiring dedicated HSM  
→ CloudHSM

Database password  
→ Secrets Manager

---

# Secrets Manager vs IAM

## [[IAM]]

Controls:

**Who can access AWS resources**

## Secrets Manager

Stores:

**The credential or secret value**

These solve:

**Different security problems**

---

# Secrets Manager vs Cognito

## [[Cognito]]

Handles:

**Application user identity**

## Secrets Manager

Handles:

**Backend application secrets**

Example:

Customer login  
→ Cognito

Database password used by backend  
→ Secrets Manager

---

# Secrets Manager vs Environment Variables

Environment variables are convenient for:

**Configuration**

but sensitive credentials should usually be managed using:

**A secret-management service**

### Killer Exam Pattern

> **Remove database password from Lambda environment variable and centralize rotation**
>
> → **Secrets Manager**

---

# Hardcoding Secrets

Bad architecture:

Application Source Code  
↓  
`password = "SuperSecret123"`

Problems:

- Secret stored in Git
- Difficult rotation
- Broad developer exposure
- Security risk

Better:

Application  
↓  
IAM Role  
↓  
Secrets Manager  
↓  
Secret

---

# Secret Rotation Benefits

Automatic rotation reduces:

- Long-lived credentials
- Manual administrative work
- Credential exposure duration
- Operational errors

### SAA Principle

> **Prefer short-lived or regularly rotated credentials when possible**

---

# High Availability

Secrets Manager is:

**A managed regional service**

AWS manages:

- Infrastructure
- Availability
- Service scaling

Applications should still consider:

**Regional architecture requirements**

---

# Multi-Region Secrets

Secrets Manager supports:

**Multi-Region secret replication**

This lets a secret be replicated to:

**Other Regions**

Architecture:

Primary Secret  
↓  
Replication  
↓  
Replica Secret in Another Region

### Killer Exam Clue

> **Multi-Region application needs locally available copies of the same secret**
>
> → **Secrets Manager Multi-Region Replication**

---

# Disaster Recovery

Secret replication can help:

**Multi-Region disaster recovery**

because applications can access:

**Regional secret replicas**

rather than depending entirely on:

**One Region**

---

# Regional Nature

Secrets are normally:

**Regional resources**

If your workload runs in multiple Regions:

Think about:

**Secret replication**

---

# Monitoring and Auditing

Use:

[[CloudTrail]]

to audit:

**Secrets Manager API actions**

Use:

[[CloudWatch]]

for relevant:

**Operational monitoring**

---

# Secret Deletion

Secrets Manager supports:

**Secret deletion workflows**

with recovery protections.

Be careful because deleting a secret can break:

**Applications that depend on it**

### SAA Principle

> **Treat secret lifecycle as part of application availability**

---

# Architecture Thinking

## Scenario 1 — RDS Password

Application needs:

**Database username/password**

and security requires:

**Automatic rotation**

Choose:

**Secrets Manager**

---

## Scenario 2 — Encryption Key

Need to control:

**The encryption key used by S3**

Choose:

**KMS**

not Secrets Manager.

---

## Scenario 3 — Application Configuration

Need to store:

`Environment = Production`

This is not really a secret.

Think:

**Parameter Store**

---

## Scenario 4 — Lambda Credential

Lambda needs an:

**External API key**

Do NOT hardcode it.

Choose:

**Secrets Manager**

---

## Scenario 5 — Dedicated HSM

Application requires:

**Private cryptographic key in dedicated hardware**

Choose:

**CloudHSM**

---

## Scenario 6 — Cross-Account Secret

Central security account stores:

**Database credentials**

Application in another account must access them.

Choose:

**Secrets Manager cross-account resource policy**

with required:

- IAM
- KMS permissions

---

## Scenario 7 — Multi-Region App

Application runs in:

Two Regions

and needs the same secret available locally.

Choose:

**Multi-Region Secret Replication**

---

## Scenario 8 — Git Credential Leak Prevention

Developers currently store:

**API keys inside source code**

Move them to:

**Secrets Manager**

and grant runtime access through:

**IAM roles**

---

## Scenario 9 — Audit Secret Access

Security team asks:

**Who retrieved this production secret?**

Choose:

**CloudTrail**

---

# Scenario Recognition

Immediately think:

**Secrets Manager**

when you see:

- Database password
- API key
- Application credential
- Automatic secret rotation
- Secret lifecycle
- Retrieve secret at runtime
- Cross-account secret
- Multi-Region secret

---

## Think Automatic Rotation When You See

- Regular password changes
- Database credentials
- Reduce long-lived credential risk

---

## Think Parameter Store When You See

- Application configuration
- Hierarchical parameters
- SecureString
- No advanced rotation requirement

---

## Think KMS When You See

- Encryption key
- Key policy
- Envelope encryption
- Customer managed key

---

# Exam Traps

## Trap 1 — Secrets Manager Is an Encryption-Key Management Service

❌

Think:

**KMS**

Secrets Manager stores:

**Secrets**

---

## Trap 2 — KMS Stores Database Passwords

❌

Think:

**Secrets Manager**

---

## Trap 3 — Secrets Manager Is the Same as Parameter Store

❌

They overlap somewhat, but:

Secrets Manager is more focused on:

**Secrets + Rotation**

Parameter Store is broader for:

**Configuration/parameters**

---

## Trap 4 — Secrets Should Be Hardcoded and Encrypted in Source Code

❌

Retrieve them:

**At runtime**

from Secrets Manager.

---

## Trap 5 — IAM Role Stores the Secret

❌

IAM controls:

**Access**

Secrets Manager stores:

**The secret**

---

## Trap 6 — Secret Rotation Only Updates the Stored Value

❌

Proper rotation also updates:

**The target credential**

such as the database password.

---

## Trap 7 — Secrets Are Global by Default

❌

Secrets are normally:

**Regional**

Use:

**Multi-Region replication**

when needed.

---

# Quick Cheat Sheet

| Exam Clue | Answer |
|---|---|
| Store Database Password | Secrets Manager |
| Store API Key | Secrets Manager |
| Automatic Secret Rotation | Secrets Manager |
| Rotation Logic | Lambda |
| Protect Secret at Rest | KMS |
| Audit Secret Access | CloudTrail |
| Multi-Region Secret | Secret Replication |
| Cross-Account Secret | Resource Policy |
| Encryption Key | KMS |
| Dedicated HSM | CloudHSM |
| Configuration Parameter | Parameter Store |
| Secure Parameter | Parameter Store SecureString |

---

# Secrets Decision Map

Need:

**Password / API key**

→ Secrets Manager

Need:

**Automatic rotation**

→ Secrets Manager

Need:

**Configuration value**

→ Parameter Store

Need:

**Encryption key**

→ KMS

Need:

**Dedicated hardware crypto key**

→ CloudHSM

Need:

**Audit secret access**

→ CloudTrail

---

# Secrets Manager vs Parameter Store

| Requirement | Secrets Manager | Parameter Store |
|---|---:|---:|
| Secret Storage | ✅ | ✅ SecureString |
| Configuration Storage | Possible | ✅ |
| Automatic Rotation | ✅ | ❌ Native Equivalent |
| Database Credential Rotation | ✅ | ❌ |
| Hierarchical Parameters | Less Focus | ✅ |
| Purpose-Built Secrets | ✅ | Less Specialized |

---

# Security Memory Map

> **PASSWORD**
> → SECRETS MANAGER
>
> **ENCRYPTION KEY**
> → KMS
>
> **DEDICATED HSM**
> → CLOUDHSM
>
> **CONFIGURATION**
> → PARAMETER STORE
>
> **USER IDENTITY**
> → COGNITO / IAM
>
> **AUDIT**
> → CLOUDTRAIL

---

# Final Exam Rapid-Fire

> **DATABASE PASSWORD**
> → SECRETS MANAGER
>
> **API KEY**
> → SECRETS MANAGER
>
> **AUTO ROTATION**
> → SECRETS MANAGER
>
> **ROTATION FUNCTION**
> → LAMBDA
>
> **SECRET ENCRYPTION**
> → KMS
>
> **AUDIT SECRET ACCESS**
> → CLOUDTRAIL
>
> **MULTI-REGION SECRET**
> → SECRET REPLICATION
>
> **CROSS-ACCOUNT SECRET**
> → RESOURCE POLICY
>
> **ENCRYPTION KEY**
> → KMS
>
> **DEDICATED CRYPTO HARDWARE**
> → CLOUDHSM
>
> **APP CONFIGURATION**
> → PARAMETER STORE

---

## Master Memory Trick

> [!tip] Secrets Manager Master Memory Trick
> Imagine your application needs to enter:
>
> **A locked database room**
>
> It needs:
>
> **A PASSWORD**
>
> You could write the password:
>
> **On the wall**
>
> That's:
>
> **HARDCODING**
>
> Bad idea.
>
> Instead, keep the password inside:
>
> **SECRETS MANAGER**
>
> The application arrives with:
>
> **AN IAM ROLE**
>
> Secrets Manager checks:
>
> **"Are you allowed to retrieve this password?"**
>
> If yes:
>
> It gives the application:
>
> **THE SECRET**
>
> Then periodically:
>
> **SECRETS MANAGER ROTATES THE PASSWORD**
>
> so the same credential does not live forever.

So remember:

> **SECRETS MANAGER**
> → STORE SECRET
>
> **KMS**
> → PROTECT ENCRYPTION KEY
>
> **IAM**
> → WHO MAY ACCESS SECRET
>
> **LAMBDA**
> → ROTATE SECRET
>
> **CLOUDTRAIL**
> → WHO ACCESSED SECRET
>
> **PARAMETER STORE**
> → CONFIGURATION

And the killer SAA question:

> **"Does the application need to securely store and automatically rotate passwords, API keys, or database credentials?"**
>
> YES
>
> → **Secrets Manager**

---

## Related Notes

- [[KMS]]
- [[CloudHSM]]
- [[Lambda]]
- [[RDS]]
- [[IAM]]
- [[CloudTrail]]
- [[CloudWatch]]
- [[Systems Manager]]
- [[Cognito]]
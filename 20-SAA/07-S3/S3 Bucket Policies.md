## What Problem Does It Solve?

[[S3 Bucket Policies]] control **who can access an S3 bucket and what actions they can perform**.

They solve questions such as:

> **"How can I grant or deny access to this bucket at the resource level?"**

Bucket Policies are:

**Resource-Based Policies**

They are attached directly to:

**S3 Buckets**

> [!tip] Memory Trick
> **IAM Policy = What can THIS user do?**
>
> **Bucket Policy = Who can access THIS bucket?**

---

# S3 Security Models

S3 access can be controlled through two major policy models:

1. **User-Based Policies**
2. **Resource-Based Policies**

---

## User-Based Security

User-based permissions are typically defined using:

[[IAM Policies]]

An IAM Policy answers:

> **"Which API actions can this IAM principal perform?"**

Example:

IAM User  
↓  
IAM Policy  
↓  
Allow `s3:GetObject`

Think:

**Policy attached to identity**

---

## Resource-Based Security

Resource-based permissions are attached directly to the S3 resource.

Examples include:

- [[S3 Bucket Policies]]
- Object ACLs
- Bucket ACLs

Bucket Policies are the most important resource-based control for SAA.

Think:

**Policy attached to bucket**

---

# IAM Policy vs Bucket Policy

## IAM Policy

Attached to:

- User
- Group
- Role

Controls:

**What that identity can do**

Example:

User  
↓  
IAM Policy  
↓  
Access Bucket

---

## Bucket Policy

Attached to:

**S3 Bucket**

Controls:

**Who can access the bucket and under what conditions**

Example:

User / Account / Service  
↓  
Bucket Policy  
↓  
S3 Bucket

---

## Architecture Thinking

Think of the difference this way:

**IAM Policy follows the user**

**Bucket Policy stays with the bucket**

---

# How S3 Determines Access

An IAM principal can access an S3 object when:

**IAM permissions allow it**

OR:

**The resource policy allows it**

AND:

> **There is no explicit DENY**

This follows one of the most important IAM rules in AWS:

**Explicit Deny wins**

---

## Permission Logic

Conceptually:

IAM Allow  
OR  
Bucket Policy Allow  
↓  
Access Potentially Allowed

But:

Explicit Deny  
↓  
Access Denied

### Memory Trick

> **Allow opens the door**
>
> **Explicit Deny locks it shut**

---

# Bucket Policy Structure

Bucket Policies are written in:

**JSON**

Important components include:

- Effect
- Principal
- Action
- Resource
- Condition

---

## Effect

Defines whether the statement:

**Allows or Denies**

Example:

`"Effect": "Allow"`

or:

`"Effect": "Deny"`

---

## Principal

Defines:

> **Who does this policy apply to?**

Possible principals include:

- AWS account
- IAM user
- IAM role
- AWS service
- Public users

Example concept:

Principal  
↓  
Account B

---

## Action

Defines:

> **Which S3 API operations are allowed or denied?**

Examples:

- `s3:GetObject`
- `s3:PutObject`
- `s3:DeleteObject`
- `s3:ListBucket`

---

## Resource

Defines:

> **Which bucket or objects does the statement apply to?**

Important distinction:

Bucket ARN:

`arn:aws:s3:::example-bucket`

Object ARN:

`arn:aws:s3:::example-bucket/*`

These target different resource levels.

---

# Bucket vs Object Resource

This is a common exam and troubleshooting issue.

## Bucket-Level Actions

Actions such as:

`s3:ListBucket`

apply to the:

**Bucket**

Resource:

`arn:aws:s3:::example-bucket`

---

## Object-Level Actions

Actions such as:

`s3:GetObject`

apply to:

**Objects**

Resource:

`arn:aws:s3:::example-bucket/*`

> [!tip] Memory Trick
> **No `/*` = Bucket**
>
> **With `/*` = Objects inside bucket**

---

# Common Bucket Policy Use Cases

The Maarek slides highlight three especially important uses:

1. Grant public access
2. Force encryption during upload
3. Grant cross-account access

---

# Public Access

A Bucket Policy can grant:

**Public access**

Example architecture:

Anonymous Website Visitor  
↓  
[[S3 Bucket Policies|Bucket Policy]]  
↓  
S3 Objects

Historically, this is commonly associated with:

[[03-Storage/S3 Static Website Hosting]]

---

## Public Principal

A public Bucket Policy may use:

Principal:

`*`

Meaning:

**Everyone**

This should be used very carefully.

### Architecture Thinking

Public read access may be appropriate for:

- Public website assets
- Public downloadable files

It is not appropriate for:

- Private application data
- Logs
- Backups
- Sensitive records

---

# S3 Block Public Access

Even if a Bucket Policy allows public access:

**S3 Block Public Access settings can prevent that access.**

This is a major S3 security concept.

Think:

Public Bucket Policy  
↓  
Block Public Access  
↓  
Public Access Blocked

> [!warning] Exam Rule
> **Public Bucket Policy alone may not be enough if Block Public Access is enabled.**

---

## Block Public Access Levels

Block Public Access settings can be configured at:

- Account level
- Bucket level

These controls are designed to prevent accidental exposure of S3 data.

### Architecture Thinking

If an exam question says:

> "The company wants to ensure no S3 bucket can accidentally become public."

Think:

**S3 Block Public Access at the account level**

---

# Cross-Account Access

One of the strongest use cases for Bucket Policies is:

**Cross-account access**

Example:

Account A  
↓  
IAM User

needs access to:

Account B  
↓  
S3 Bucket

You can attach a Bucket Policy to the bucket in Account B granting access to the principal from Account A.

Architecture:

IAM Principal  
Account A  
↓  
Bucket Policy  
Account B  
↓  
S3 Bucket

> [!tip] Memory Trick
> **Another account needs my bucket → Bucket Policy**

---

# Bucket Policy vs AssumeRole for Cross-Account Access

Cross-account access can often be implemented using either:

1. Resource-based policy
2. IAM Role

---

## Resource-Based Policy

Example:

Account A User  
↓  
S3 Bucket Policy in Account B  
↓  
S3 Bucket

One advantage:

The principal keeps its original permissions.

---

## AssumeRole

User  
↓  
Assume Role in Account B  
↓  
Use Role Permissions

When assuming a role:

The principal operates with the permissions assigned to that role.

---

## Architecture Thinking

Suppose a user in Account A needs to:

1. Read from DynamoDB in Account A
2. Write results into S3 in Account B

A resource-based Bucket Policy can be attractive because the user can retain its original Account A permissions while gaining S3 access in Account B.

> [!tip] Exam Distinction
> **Resource Policy → Principal keeps original permissions**
>
> **AssumeRole → Operates with assumed-role permissions**

---

# Enforcing Encryption with Bucket Policies

Bucket Policies can enforce encryption requirements.

Example requirement:

> **"Reject any object upload that does not use SSE-KMS."**

Architecture:

PUT Object  
↓  
Bucket Policy Checks Encryption Header  
├── SSE-KMS → Allow
└── Missing/Wrong Encryption → Deny

This is stronger than simply relying on:

**Default Encryption**

---

# Default Encryption vs Policy Enforcement

Default encryption says:

> **"If accepted, S3 will encrypt the object."**

Bucket Policy says:

> **"I may reject the request unless the caller explicitly meets my requirement."**

Important:

**Bucket Policies are evaluated before Default Encryption**

So if the policy requires SSE-KMS:

PUT Object without SSE-KMS header  
↓  
Bucket Policy  
↓  
DENY

Default SSE-S3 encryption does not rescue the request.

---

# Enforcing HTTPS

Bucket Policies can also enforce:

**Encryption in transit**

Use the condition:

`aws:SecureTransport`

Architecture:

HTTPS Request  
↓  
Allowed

HTTP Request  
↓  
Bucket Policy Explicit Deny  
↓  
Blocked

### Exam Pattern

If the question says:

> **"Ensure all S3 requests use HTTPS."**

Choose:

**Bucket Policy with `aws:SecureTransport`**

---

# Bucket Policy Conditions

Conditions let you apply permissions only under certain circumstances.

Examples:

- Require HTTPS
- Require a specific encryption method
- Restrict source IP
- Restrict VPC endpoint
- Restrict organization/account
- Require specific headers

Conceptually:

Request  
↓  
Principal + Action + Resource  
↓  
Condition  
↓  
Allow / Deny

---

# Explicit Deny

Explicit Deny deserves special emphasis.

Suppose:

IAM Policy:

**Allow s3:GetObject**

Bucket Policy:

**Deny s3:GetObject**

Result:

**DENIED**

Why?

Explicit Deny overrides Allow.

### Memory Trick

**DENY beats everything**

---

# Bucket Policy and AWS Services

Bucket Policies can also allow AWS services to interact with the bucket.

Example patterns include:

- [[05-Networking/CloudFront]] accessing private S3 content
- Logging services writing objects
- Other AWS services writing into S3

Architecture:

AWS Service  
↓  
Bucket Policy  
↓  
S3 Bucket

The Bucket Policy defines the service principal and allowed actions.

---

# CloudFront + Private S3

A common architecture is:

Users  
↓  
[[05-Networking/CloudFront]]  
↓  
Private S3 Bucket

Instead of making the bucket publicly accessible:

Use:

[[CloudFront Origin Access Control]]  
+  
S3 Bucket Policy

Architecture:

Internet User  
↓  
CloudFront  
↓  
Origin Access Control  
↓  
Bucket Policy  
↓  
Private S3 Bucket

### Architecture Thinking

If CloudFront should be the only public entry point:

> **Keep S3 private and allow CloudFront through the Bucket Policy**

---

# Bucket Policy vs ACL

S3 also supports ACLs:

- Object ACL
- Bucket ACL

But ACLs are:

- Older access-control mechanisms
- Less commonly preferred for modern architectures
- Often disabled

Bucket Policies and IAM Policies are generally more important for SAA scenarios.

### Memory Trick

**Modern S3 access → IAM + Bucket Policies**

---

# Architecture Thinking

## Scenario 1 — Cross-Account Read Access

An application in Account A must read objects from a bucket owned by Account B.

The company wants direct resource-based access.

**Choose → S3 Bucket Policy in Account B**

Grant the Account A principal:

`s3:GetObject`

---

## Scenario 2 — Public Static Website

A bucket hosts a public website and users need public read access.

Possible requirement:

**Bucket Policy allowing public `GetObject`**

Also verify:

**Block Public Access settings**

---

## Scenario 3 — Prevent Public Exposure

A company wants to guarantee that developers cannot accidentally expose S3 buckets publicly.

**Choose → S3 Block Public Access**

Prefer account-level enforcement when the requirement applies to all buckets.

---

## Scenario 4 — Force HTTPS

Security policy requires:

**No unencrypted HTTP requests to S3**

**Choose → Bucket Policy using `aws:SecureTransport`**

Explicitly deny insecure transport.

---

## Scenario 5 — Require SSE-KMS

All uploaded objects must explicitly use:

[[S3 SSE-KMS]]

**Choose → Bucket Policy**

Deny PUT requests without the expected encryption header.

---

## Scenario 6 — IAM Allows but Bucket Explicitly Denies

IAM Policy:

Allow GetObject

Bucket Policy:

Explicit Deny GetObject

Result:

**Access Denied**

---

## Scenario 7 — CloudFront Must Access Private S3

Users should not access S3 directly.

Only [[05-Networking/CloudFront]] should access the bucket.

**Choose:**

Private S3 Bucket  
+  
[[CloudFront Origin Access Control]]  
+  
Bucket Policy

---

# IAM Policy vs Bucket Policy

| Feature | IAM Policy | Bucket Policy |
|---|---|---|
| Attached To | Identity | S3 Bucket |
| Policy Type | Identity-Based | Resource-Based |
| Controls | What identity can do | Who can access resource |
| Cross-Account Access | Usually via role/policies | ✅ Strong use case |
| Public Access | ❌ | ✅ |
| Explicit Deny | ✅ | ✅ |
| JSON Policy | ✅ | ✅ |

---

# Bucket Policy Anatomy

| Element | Question |
|---|---|
| Effect | Allow or Deny? |
| Principal | Who? |
| Action | What can they do? |
| Resource | Which bucket/object? |
| Condition | Under what circumstances? |

### Memory Trick

> **WHO + WHAT + WHERE + WHEN → ALLOW/DENY**

---

# Scenario Recognition

## Immediately Think Bucket Policy When You See

- Resource-based policy
- Bucket-wide permissions
- Cross-account access
- Public S3 access
- Anonymous user
- Force encryption
- Require SSE-KMS
- Force HTTPS
- `aws:SecureTransport`
- Explicit Deny
- CloudFront access to private bucket
- Service principal accessing S3

### Strongest Exam Patterns

> **Cross-account S3 → Bucket Policy**
>
> **Force HTTPS → Bucket Policy**
>
> **Require encryption → Bucket Policy**
>
> **Public access → Bucket Policy + check Block Public Access**

---

# Exam Traps

## Trap 1 — IAM Policy Is the Only Way to Grant S3 Access

False.

A Bucket Policy can independently allow access.

Remember:

IAM Allow  
OR  
Resource Policy Allow

provided there is:

**No explicit Deny**

---

## Trap 2 — Allow Overrides Explicit Deny

False.

**Explicit Deny always wins**

---

## Trap 3 — Public Bucket Policy Guarantees Public Access

False.

[[S3 Block Public Access]] may still block it.

---

## Trap 4 — Bucket and Object ARNs Are the Same

False.

Bucket:

`arn:aws:s3:::bucket-name`

Objects:

`arn:aws:s3:::bucket-name/*`

Use the correct resource for the API action.

---

## Trap 5 — Default Encryption Enforces SSE-KMS

Not automatically.

Default SSE-S3 encryption may encrypt an accepted object, but if the requirement is:

> **Every upload MUST explicitly use SSE-KMS**

use:

**Bucket Policy enforcement**

---

## Trap 6 — Bucket Policies Are Only for Public Access

False.

They are also heavily used for:

- Cross-account access
- Encryption enforcement
- HTTPS enforcement
- AWS service access

---

## Trap 7 — ACLs Are Always Required

False.

ACLs can be disabled.

Modern S3 architectures commonly rely on:

**IAM + Bucket Policies**

---

# Quick Cheat Sheet

| Requirement | Best Answer |
|---|---|
| Identity permissions | IAM Policy |
| Bucket-wide access | Bucket Policy |
| Resource-based S3 policy | Bucket Policy |
| Cross-account S3 access | Bucket Policy |
| Public bucket access | Bucket Policy |
| Prevent accidental public access | Block Public Access |
| Force HTTPS | `aws:SecureTransport` |
| Force SSE-KMS | Bucket Policy |
| Explicit Deny present | Access Denied |
| Bucket ARN | `arn:aws:s3:::bucket` |
| Object ARN | `arn:aws:s3:::bucket/*` |
| CloudFront → Private S3 | OAC + Bucket Policy |

---

## Master Memory Trick

> [!tip] Master Memory Trick
> **Bucket Policy = Security Guard standing at the bucket**
>
> Every request arrives and the guard asks:
>
> **WHO are you?**
>
> → Principal
>
> **WHAT are you trying to do?**
>
> → Action
>
> **WHERE are you trying to do it?**
>
> → Resource
>
> **ARE the conditions satisfied?**
>
> → Condition
>
> Then:
>
> **ALLOW or DENY**

Remember the killer exam rules:

**IAM Policy = Identity-Based**

**Bucket Policy = Resource-Based**

**Cross-Account = Bucket Policy**

**Force HTTPS = `aws:SecureTransport`**

**Explicit Deny = Game Over**

And:

> **Public Policy + Block Public Access = Still Private**

---

## Related Notes

- [[S3]]
- [[S3 Encryption]]
- [[S3 SSE-S3]]
- [[S3 SSE-KMS]]
- [[S3 Block Public Access]]
- [[03-Storage/S3 Static Website Hosting]]
- [[S3 Versioning]]
- [[IAM]]
- [[IAM Policies]]
- [[05-Networking/CloudFront]]
- [[CloudFront Origin Access Control]]
- [[06-Security/CloudTrail]]
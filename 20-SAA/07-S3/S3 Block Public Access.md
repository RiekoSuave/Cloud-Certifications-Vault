## What Problem Does It Solve?

[[S3 Block Public Access]] helps prevent accidental exposure of S3 buckets and objects to the public internet.

It solves the problem of:

> **"How can I make sure this S3 bucket does not accidentally become public?"**

This is especially important because a Bucket Policy or ACL could otherwise grant public access.

Think:

Public Bucket Policy / ACL  
↓  
[[S3 Block Public Access]]  
↓  
Public Exposure Prevented

> [!tip] Memory Trick
> **Block Public Access = Safety Lock for S3**
>
> If the bucket should never be public:
>
> **Leave the safety lock ON.**

---

## Why Block Public Access Exists

The Maarek slides emphasize that these settings were created to help prevent:

**Company data leaks**

S3 buckets often store sensitive information such as:

- Backups
- Logs
- Customer data
- Application files
- Financial records
- Internal documents

An accidental public Bucket Policy or ACL could expose that data.

Block Public Access adds another layer of protection.

---

## Architecture Thinking

Without Block Public Access:

Bucket Policy  
↓  
Allows Public Access  
↓  
Internet User  
↓  
S3 Objects

With Block Public Access:

Bucket Policy Attempts Public Access  
↓  
[[S3 Block Public Access]]  
↓  
Public Access Blocked

### Architecture Lesson

Think of Bucket Policies and ACLs as:

**Permission mechanisms**

Block Public Access acts as:

**A guardrail against public exposure**

---

## Public Access Is Different from Normal AWS Access

Block Public Access focuses specifically on:

**Public access**

It does not mean:

> **"Nobody can access the bucket."**

Authorized AWS principals can still access the bucket through properly configured:

- [[IAM Policies]]
- [[S3 Bucket Policies]]
- IAM Roles
- AWS service permissions

The goal is to prevent access that makes the resource broadly public.

---

## Bucket-Level Block Public Access

Block Public Access settings can be configured for an:

**Individual S3 bucket**

Example:

Bucket A  
↓  
Block Public Access ON

Bucket B  
↓  
Different configuration

This allows different buckets to have different public-access requirements.

---

## Account-Level Block Public Access

Block Public Access can also be configured at the:

**AWS Account level**

This is an important architecture option.

Architecture:

AWS Account  
↓  
Block Public Access  
↓  
All S3 Buckets

Use this when the requirement is:

> **"No S3 bucket in this AWS account should ever be public."**

> [!tip] Exam Pattern
> **Prevent ALL buckets in an account from becoming public**
>
> → **Account-Level S3 Block Public Access**

---

## Bucket-Level vs Account-Level

### Bucket-Level

Protects:

**One bucket**

Use when:

Only a particular bucket must remain private.

---

### Account-Level

Protects:

**Buckets across the AWS account**

Use when:

Company policy says public S3 buckets should not exist at all.

### Memory Trick

**One bucket → Bucket-level**

**Whole account → Account-level**

---

## Block Public Access and Bucket Policies

Suppose a Bucket Policy says:

Principal:

`*`

Action:

`s3:GetObject`

Effect:

Allow

That policy is attempting to grant:

**Public read access**

But if Block Public Access prevents that type of public policy:

The bucket remains protected.

Architecture:

Public Bucket Policy  
↓  
Block Public Access  
↓  
Public User Denied

> [!warning] Exam Trap
> **Bucket Policy says public does NOT automatically mean the bucket is publicly accessible.**
>
> Always check:
>
> **Block Public Access**

---

## Block Public Access and ACLs

Public access can also historically come from:

- Bucket ACLs
- Object ACLs

[[S3 Block Public Access]] is designed to prevent or restrict public exposure through these mechanisms as well.

This is important because S3 security may involve multiple permission systems.

---

## Modern S3 Security Architecture

A strong modern design usually looks like:

Private S3 Bucket  
↓  
Block Public Access ON  
↓  
Access through:
- IAM
- Bucket Policy
- AWS Service Integration

Instead of exposing the bucket directly to the internet.

---

## CloudFront Architecture

A very common exam architecture is:

Users  
↓  
[[05-Networking/CloudFront]]  
↓  
[[CloudFront Origin Access Control]]  
↓  
Private S3 Bucket

In this design:

The S3 bucket itself remains:

**Private**

and users access the content through CloudFront.

The bucket policy allows:

**CloudFront**

rather than:

**The entire public internet**

### Architecture Thinking

If the requirement says:

> **"Users should access S3 content through CloudFront, but should not access S3 directly."**

Think:

- Block Public Access ON
- Private S3 bucket
- [[CloudFront Origin Access Control]]
- Bucket Policy allowing CloudFront

---

## Static Website Hosting Caveat

[[03-Storage/S3 Static Website Hosting]] can involve public access to the website endpoint.

This can conflict with Block Public Access.

If the architecture requires a truly public S3 website endpoint:

You must carefully configure the required public access.

However, for many production architectures:

[[05-Networking/CloudFront]]

in front of a private S3 bucket is preferable.

### Exam Thinking

If the question says:

**S3 Website Endpoint directly accessible by public users**

public access may be necessary.

If the question says:

**CloudFront serves S3 content securely**

keep S3 private.

---

## Defense in Depth

Block Public Access is an example of:

**Defense in Depth**

Even if someone accidentally creates:

- Public Bucket Policy
- Public ACL

another control can prevent exposure.

Architecture:

IAM / Bucket Policy  
↓  
Block Public Access  
↓  
Private S3 Data

### Memory Trick

**Block Public Access = Seatbelt**

You still drive carefully with policies.

But the extra safety control reduces the damage from a mistake.

---

## Architecture Thinking

### Scenario 1 — Never Public

A company stores financial reports in S3.

Security policy states:

> No S3 object in this AWS account may ever be publicly accessible.

**Choose → Account-Level S3 Block Public Access**

---

### Scenario 2 — One Sensitive Bucket

A company has several S3 buckets.

One contains confidential backups and must never be public.

**Choose → Bucket-Level S3 Block Public Access**

---

### Scenario 3 — Public Policy but Still No Access

A developer creates a Bucket Policy allowing:

Principal `*`

to perform:

`s3:GetObject`

However, users on the internet still cannot retrieve objects.

What should you check?

**S3 Block Public Access**

It may be preventing the policy from exposing the bucket.

---

### Scenario 4 — CloudFront + S3

A company wants public users to retrieve website content.

Users must access the content only through CloudFront.

Direct S3 access must remain blocked.

**Choose:**

[[05-Networking/CloudFront]]  
+  
[[CloudFront Origin Access Control]]  
+  
Private S3 Bucket  
+  
Block Public Access

---

### Scenario 5 — Company-Wide Guardrail

A security administrator wants to prevent developers from accidentally creating public S3 buckets anywhere in the AWS account.

**Choose → Account-Level Block Public Access**

This is more operationally efficient than configuring each bucket individually.

---

## Block Public Access vs Bucket Policy

These solve different problems.

### [[S3 Bucket Policies]]

Define:

**Who can access the bucket and what they can do**

---

### Block Public Access

Acts as a:

**Guardrail against public exposure**

### Memory Trick

**Bucket Policy = Permission**

**Block Public Access = Public Safety Lock**

---

## Block Public Access vs IAM

### [[IAM Policies]]

Control:

**Identity permissions**

Example:

Can this role read S3?

---

### Block Public Access

Controls:

**Whether resources can become publicly accessible**

These are separate security layers.

---

## Block Public Access vs Encryption

Do not confuse:

**Privacy of access**

with:

**Encryption**

### Block Public Access

Controls:

Who can publicly access the object.

### [[S3 Encryption]]

Protects:

Data confidentiality at rest or in transit.

You may need:

**Both**

Architecture:

Block Public Access  
+  
Encryption  
+  
IAM / Bucket Policy

---

## Scenario Recognition

### Immediately Think Block Public Access When You See

- Prevent public bucket
- Prevent accidental public exposure
- Company data leak
- No S3 bucket should be public
- Account-wide public access prevention
- Bucket Policy says public but access still fails
- Public ACL blocked
- Security guardrail
- Keep S3 private behind CloudFront

### Strongest Exam Phrase

> **"Ensure S3 can never become public"**
>
> → **S3 Block Public Access**

---

## Exam Traps

### Trap 1 — Public Bucket Policy Always Makes the Bucket Public

False.

Block Public Access may prevent the policy from taking effect.

---

### Trap 2 — Block Public Access Means No AWS Principal Can Access S3

False.

It focuses on:

**Public exposure**

Authorized identities can still access the bucket through normal permissions.

---

### Trap 3 — Block Public Access Is Only Bucket-Level

False.

It can also be configured at the:

**Account level**

---

### Trap 4 — Every S3 Website Should Keep Block Public Access On

Be careful.

A directly hosted public S3 website may require public access.

But a CloudFront architecture can keep the S3 bucket private.

Read the architecture requirement carefully.

---

### Trap 5 — Encryption Prevents Public Access

False.

An encrypted object could still be publicly accessible if permissions allow it.

Encryption and access control solve different problems.

---

### Trap 6 — IAM Policy Replaces Block Public Access

False.

IAM permissions control identities.

Block Public Access provides an additional public-access guardrail.

---

## Quick Cheat Sheet

| Requirement | Best Choice |
|---|---|
| Prevent one bucket from becoming public | Bucket-Level Block Public Access |
| Prevent all account buckets from becoming public | Account-Level Block Public Access |
| Public Bucket Policy not working | Check Block Public Access |
| Prevent accidental S3 data leak | Block Public Access |
| Users access S3 only through CloudFront | Keep Block Public Access ON |
| Control specific identity access | IAM Policy |
| Define bucket permissions | Bucket Policy |
| Protect object contents cryptographically | S3 Encryption |

---

## Master Memory Trick

> [!tip] Master Memory Trick
> **Block Public Access = S3's Master Public Safety Switch**
>
> Ask:
>
> **"Should this bucket EVER be public?"**
>
> If:
>
> **NO**
>
> → Leave Block Public Access ON
>
> If:
>
> **NO bucket in the entire account should ever be public**
>
> → Configure it at the ACCOUNT level

And remember:

> **Bucket Policy = Permission**
>
> **Block Public Access = Guardrail**
>
> **Encryption = Protect the data**
>
> **IAM = Protect the identity**

---

## Related Notes

- [[S3]]
- [[S3 Bucket Policies]]
- [[S3 Encryption]]
- [[IAM]]
- [[IAM Policies]]
- [[05-Networking/CloudFront]]
- [[CloudFront Origin Access Control]]
- [[03-Storage/S3 Static Website Hosting]]
- [[S3 Versioning]]
- [[Security]]
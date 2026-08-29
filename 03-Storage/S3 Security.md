See also: [[S3]]

See also: [[IAM]]

See also: [[06-Security/KMS]]

## What Problem Does It Solve?

Controls who can access S3 buckets and objects and what actions they are allowed to perform.

S3 security uses both identity-based and resource-based permissions.

---

## Main S3 Security Methods

S3 access can be controlled using:

- IAM Policies
- Bucket Policies
- Object ACLs
- Bucket ACLs
- Block Public Access
- Encryption

---

## IAM Policies

IAM Policies are:

User-based permissions.

They define which S3 API actions an IAM identity is allowed to perform.

Examples:

- Read objects
- Upload objects
- Delete objects
- List buckets

### Memory Trick

IAM Policy = What can this identity do?

---

## Bucket Policies

Bucket Policies are:

Resource-based policies.

They apply permissions directly to an S3 bucket.

They are written using JSON.

Bucket Policies can define:

- Resource
- Effect
- Action
- Principal

---

## Bucket Policy Components

### Resource

Which bucket or objects the policy applies to.

### Effect

Can be:

- Allow
- Deny

### Action

Which S3 actions are allowed or denied.

### Principal

Who the policy applies to.

---

## Common Bucket Policy Uses

Your course notes identify uses such as:

- Granting public access
- Requiring encryption during uploads
- Granting another AWS account access
- Controlling bucket-wide permissions

### Memory Trick

Bucket Policy = Rules attached to the bucket

---

## IAM Policy vs Bucket Policy

### IAM Policy

Attached to:

IAM identity

Examples:

- User
- Group
- Role

### Bucket Policy

Attached to:

S3 bucket

| IAM Policy | Bucket Policy |
|---|---|
| Identity-based | Resource-based |
| Attached to IAM identity | Attached to bucket |
| Controls identity permissions | Controls bucket access |
| Useful for user access | Useful for cross-account/public access |

---

## How Access Is Evaluated

Your course states that an IAM principal can access an S3 object when:

IAM permissions allow access

OR

the resource policy allows access

AND

there is no explicit deny.

### Important Exam Rule

Explicit Deny wins.

### Memory Trick

Allow + No Deny = Access

Explicit Deny = Blocked

---

## Access Control Lists

S3 also supports:

### Object ACL

Provides finer-grained permissions on individual objects.

### Bucket ACL

Provides permissions at the bucket level.

Your course notes say ACLs are less commonly used and can be disabled.

---

## Block Public Access

S3 provides:

Block Public Access

settings.

These settings help prevent buckets or objects from accidentally becoming publicly accessible.

### Memory Trick

Block Public Access = Safety switch

---

## Public Website Access

If an S3 bucket hosts a public static website, the bucket permissions must allow the appropriate public reads.

If you receive:

403 Forbidden

your course notes recommend checking the bucket policy.

See:

[[03-Storage/S3 Static Website Hosting]]

---

## EC2 Access to S3

When an EC2 instance needs access to S3:

Use an IAM Role.

Avoid storing long-term AWS credentials directly on the EC2 instance.

Basic Flow:

EC2

↓

IAM Role

↓

S3

### Memory Trick

EC2 → IAM Role → S3

---

## Cross-Account Access

Bucket Policies can provide access to another AWS account.

### Example

Account A owns S3 bucket

↓

Bucket Policy grants access

↓

Account B can access bucket

### Memory Trick

Cross Account = Bucket Policy

---

## Encryption

Your course includes encryption as part of S3 security.

Encryption can protect data:

- At rest
- In transit

See also:

[[06-Security/KMS]]

---

## IAM Access Analyzer for S3

IAM Access Analyzer helps determine whether S3 resources are accessible by unintended users or accounts.

It evaluates:

- Bucket Policies
- ACLs
- Access Point Policies

It can identify situations such as:

- Publicly accessible buckets
- Buckets shared with another AWS account

### Memory Trick

Access Analyzer = Who can access my bucket?

---

## Shared Responsibility for S3 Security

### AWS Is Responsible For

- Underlying infrastructure
- Global security
- Availability
- Durability
- Compliance validation

### Customer Is Responsible For

- Bucket Policies
- Versioning
- Replication
- Logging
- Monitoring
- Storage class configuration
- Encryption

---

## Exam Scenarios

A user needs permission to access S3.

→ IAM Policy

---

A bucket needs to grant access to another AWS account.

→ Bucket Policy

---

An EC2 instance needs to access S3 securely.

→ IAM Role

---

A company wants to prevent accidental public exposure of S3 buckets.

→ Block Public Access

---

A security team wants to identify buckets accessible by external accounts.

→ IAM Access Analyzer

---

A policy contains an Allow and another policy contains an explicit Deny.

→ Explicit Deny wins

---

## Exam Keywords

IAM Policy

Bucket Policy

Resource Policy

ACL

Block Public Access

Cross-account access

IAM Role

Encryption

Access Analyzer

Explicit Deny

---

## Memory Tricks

IAM Policy = Identity Permissions

Bucket Policy = Bucket Permissions

EC2 Access = IAM Role

Cross Account = Bucket Policy

Public Protection = Block Public Access

Access Analyzer = Find External Access

Explicit Deny = Always Wins
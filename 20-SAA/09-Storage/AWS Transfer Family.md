## What Problem Does It Solve?

[[AWS Transfer Family]] provides fully managed file-transfer endpoints for moving files into and out of:

- [[S3]]
- [[EFS]]

using familiar file-transfer protocols.

It solves the problem of:

> **"Our users, customers, or business partners already use FTP-style protocols. How can we let them transfer files into AWS without managing our own FTP servers?"**

Architecture:

Users / Partners  
↓  
SFTP / FTPS / FTP  
↓  
AWS Transfer Family  
↓  
S3 / EFS

> [!tip] Memory Trick
> **Transfer Family = Managed FTP-style doorway into S3 or EFS**

---

## What Is AWS Transfer Family?

AWS Transfer Family is a:

**Fully managed service**

for file transfers into and out of AWS storage.

The key protocols are:

- SFTP
- FTPS
- FTP

The backend storage can be:

- [[S3]]
- [[EFS]]

---

# Supported Protocols

## SFTP

SFTP means:

**SSH File Transfer Protocol**

It provides:

**Secure file transfer over SSH**

### Port

Typically:

**22**

### Exam Pattern

> **Secure file transfer using SSH**
>
> → **SFTP**

---

## FTPS

FTPS means:

**FTP over SSL/TLS**

It provides:

**Encrypted FTP communication using TLS**

### Memory Trick

**FTPS = FTP + TLS**

---

## FTP

FTP means:

**File Transfer Protocol**

Traditional FTP is:

**Unencrypted**

This makes it less suitable when secure internet-based transfer is required.

> [!warning] Exam Thinking
> If security is emphasized, expect:
>
> **SFTP or FTPS**
>
> rather than plain FTP.

---

# Protocol Comparison

| Protocol | Security | Main Clue |
|---|---|---|
| SFTP | SSH | Secure transfer over SSH |
| FTPS | SSL/TLS | Secure FTP using TLS |
| FTP | None by default | Traditional FTP |

### Memory Trick

**SFTP → SSH**

**FTPS → TLS**

**FTP → Plain**

---

# Backend Storage

AWS Transfer Family can store transferred files in:

- [[S3]]
- [[EFS]]

Architecture:

External User  
↓  
Transfer Family  
↓  
S3

or:

External User  
↓  
Transfer Family  
↓  
EFS

---

# Transfer Family + S3

One of the most common architectures:

Business Partner  
↓  
SFTP  
↓  
AWS Transfer Family  
↓  
[[S3]]

This allows a partner to continue using:

**SFTP**

while AWS stores the files in:

**S3**

### Strong Exam Pattern

> **"Business partners upload files through SFTP and the company wants the files stored in S3."**
>
> → **AWS Transfer Family**

---

# Transfer Family + EFS

Transfer Family can also use:

[[EFS]]

as the backend.

Architecture:

User  
↓  
SFTP / FTPS / FTP  
↓  
Transfer Family  
↓  
EFS

This can be useful when the destination needs to be:

**A shared file system**

rather than object storage.

---

# Fully Managed

Without Transfer Family, a company might need to manage:

EC2  
↓  
FTP Server Software  
↓  
Patching  
↓  
Scaling  
↓  
Availability  
↓  
Security

With Transfer Family:

AWS manages the:

**File-transfer service infrastructure**

### Exam Thinking

If the question asks for:

**Least operational overhead**

avoid building FTP servers on EC2 when:

AWS Transfer Family

meets the requirement.

---

# High Availability and Scaling

Because Transfer Family is:

**Fully managed**

AWS handles much of the infrastructure associated with:

- Availability
- Scaling
- Server management

The architecture removes the need to manually operate:

**FTP/SFTP server fleets**

---

# External Business Partners

Transfer Family is especially useful for:

**B2B file exchange**

Example:

Supplier  
↓  
SFTP  
↓  
Transfer Family  
↓  
S3

Another Partner  
↓  
FTPS  
↓  
Transfer Family  
↓  
S3

This allows existing external workflows to continue while the company modernizes its backend storage.

---

# Migration from Existing FTP Servers

Imagine an organization currently runs:

On-Premises SFTP Server  
↓  
Local Storage

It wants to migrate to AWS while preserving:

**Existing client transfer workflows**

New Architecture:

Client  
↓  
SFTP  
↓  
AWS Transfer Family  
↓  
S3

This can eliminate the need to maintain:

**Traditional file-transfer servers**

---

# Authentication

AWS Transfer Family supports different methods for authenticating users.

The key exam concept is:

> Users must be authenticated before they can access the underlying S3 or EFS resources.

Depending on the architecture, authentication can integrate with:

- Service-managed users
- Existing identity systems
- Custom identity providers

---

# IAM Integration

When using:

[[S3]]

AWS permissions help determine what transferred users can access.

Conceptually:

Transfer User  
↓  
Authentication  
↓  
IAM Permissions  
↓  
Allowed S3 Resources

This helps enforce:

**Least privilege**

---

# Route 53 Integration

A company can use:

[[Route 53]]

to provide a friendly DNS name for its file-transfer endpoint.

Example:

`sftp.example.com`

↓  
Transfer Family Endpoint

This allows customers or partners to connect using a:

**Familiar domain name**

instead of changing their workflow around an AWS-generated endpoint.

---

# Public vs VPC Access

Transfer Family endpoints can be designed around different networking requirements.

For example:

External Partner  
↓  
Internet  
↓  
Transfer Family

or:

Private Environment  
↓  
VPC-Based Access  
↓  
Transfer Family

### Exam Thinking

Pay attention to whether the question requires:

- Internet-accessible transfers
- Private access
- Existing network controls

---

# Transfer Family vs S3 File Gateway

These services can look similar because both can ultimately involve S3.

## [[S3 File Gateway]]

Protocols:

- NFS
- SMB

Purpose:

**Hybrid file-system access**

---

## AWS Transfer Family

Protocols:

- SFTP
- FTPS
- FTP

Purpose:

**File transfer**

### Memory Trick

**NFS / SMB**
→ S3 File Gateway

**SFTP / FTPS / FTP**
→ Transfer Family

---

# Transfer Family vs DataSync

## [[DataSync]]

Best for:

**Automated high-speed data movement**

between storage systems.

Examples:

- NFS → S3
- SMB → S3
- AWS storage → AWS storage

---

## AWS Transfer Family

Best for:

**Users and applications using FTP-style protocols**

### Exam Decision

Existing SFTP clients  
→ Transfer Family

Automated migration of millions of files  
→ DataSync

---

# Transfer Family vs Storage Gateway

## [[Storage Gateway]]

Provides:

**Ongoing hybrid storage interfaces**

such as:

- NFS
- SMB
- iSCSI
- Virtual tapes

---

## Transfer Family

Provides:

**Managed file-transfer endpoints**

using:

- SFTP
- FTPS
- FTP

### Memory Trick

**Gateway = Storage Access**

**Transfer Family = File Transfer**

---

# Transfer Family vs Snowball

## [[Snowball]]

Best for:

**Massive offline data transfer**

---

## Transfer Family

Best for:

**Network-based file transfers**

### Exam Decision

Petabytes + poor network  
→ Snowball

Partners continuously upload via SFTP  
→ Transfer Family

---

# Transfer Family vs EC2 FTP Server

You could deploy:

EC2  
↓  
SFTP Server

But then you manage:

- Operating system
- Patching
- Availability
- Scaling
- Server software
- Security

Transfer Family provides:

**Managed file-transfer infrastructure**

### Exam Rule

If both solutions meet the requirements and the question asks for:

**Least operational overhead**

prefer:

**AWS Transfer Family**

---

# Architecture Thinking

## Scenario 1 — Partner Uploads to S3

A financial company receives daily files from external partners.

Partners already use:

**SFTP**

Files must land in:

[[S3]]

**Choose:**

AWS Transfer Family  
+  
SFTP  
+  
S3

---

## Scenario 2 — Existing FTPS Workflow

Customers currently upload files through:

**FTPS**

The company wants to move the backend to AWS without requiring customers to change protocols.

**Choose → AWS Transfer Family**

---

## Scenario 3 — Traditional FTP

A legacy internal system requires:

**FTP**

The company wants a managed AWS service instead of maintaining FTP servers.

**Choose → AWS Transfer Family**

---

## Scenario 4 — Shared File-System Backend

Users transfer files using SFTP.

The files need to land on a shared:

**NFS file system**

**Choose:**

AWS Transfer Family  
+  
[[EFS]]

---

## Scenario 5 — On-Premises Application Uses NFS

An on-premises application needs continuous:

**NFS access**

to files stored as S3 objects.

Do NOT choose Transfer Family.

Choose:

[[S3 File Gateway]]

---

## Scenario 6 — Massive Automated Migration

A company needs to transfer millions of files from an on-premises NFS server to S3.

The transfer should be:

- Automated
- Scheduled
- Optimized

Think:

[[DataSync]]

rather than Transfer Family.

---

## Scenario 7 — Petabyte Migration with Poor Bandwidth

A company must migrate petabytes of data but has inadequate network bandwidth.

Do NOT choose Transfer Family.

Think:

[[Snowball]]

---

# Scenario Recognition

Immediately think:

[[AWS Transfer Family]]

when you see:

- SFTP
- FTPS
- FTP
- Managed FTP server
- Business partners
- File exchange
- External uploads
- SFTP → S3
- SFTP → EFS
- Replace existing FTP server
- Minimize server management

### Strongest Exam Pattern

> **"External partners need to continue using SFTP to upload files directly into S3."**
>
> → **AWS Transfer Family**

---

# Exam Traps

## Trap 1 — SFTP and FTPS Are the Same

False.

SFTP:

**SSH**

FTPS:

**SSL/TLS**

---

## Trap 2 — Transfer Family Uses NFS and SMB as Client Transfer Protocols

False.

Think:

- SFTP
- FTPS
- FTP

NFS / SMB point more toward:

Storage Gateway or DataSync depending on the requirement.

---

## Trap 3 — Transfer Family Requires You to Manage EC2 FTP Servers

False.

It is:

**Fully managed**

---

## Trap 4 — Transfer Family Backend Must Be S3

False.

It can also use:

[[EFS]]

---

## Trap 5 — Transfer Family Is the Best Tool for Massive Offline Migration

False.

Think:

[[Snowball]]

---

## Trap 6 — Transfer Family Is the Same as DataSync

False.

Transfer Family:

**FTP-style client transfers**

DataSync:

**Automated data movement**

---

## Trap 7 — Plain FTP Provides Encryption

False.

Plain FTP is:

**Unencrypted**

For secure transfer:

Think SFTP or FTPS.

---

# Quick Cheat Sheet

| Requirement | Answer |
|---|---|
| Managed SFTP | Transfer Family |
| Managed FTPS | Transfer Family |
| Managed FTP | Transfer Family |
| SFTP → S3 | Transfer Family |
| SFTP → EFS | Transfer Family |
| Business Partner File Exchange | Transfer Family |
| Replace Self-Managed FTP Server | Transfer Family |
| SSH-Based Transfer | SFTP |
| TLS-Based FTP | FTPS |
| NFS / SMB → S3 | S3 File Gateway |
| Automated Storage Migration | DataSync |
| Offline Massive Migration | Snowball |

---

## Master Memory Trick

> [!tip] Master Memory Trick
> Picture a business partner who refuses to change how they send files.
>
> They say:
>
> **"I've been using SFTP for 15 years. I'm not changing."**
>
> AWS says:
>
> **"Fine."**
>
> Partner
> ↓
> **SFTP**
> ↓
> **Transfer Family**
> ↓
> **S3 / EFS**

So memorize:

> **SFTP**
> → SSH
>
> **FTPS**
> → TLS
>
> **FTP**
> → Plain
>
> **BACKEND**
> → S3 / EFS

And the killer exam clue:

> **SFTP / FTPS / FTP + MANAGED AWS SERVICE**
>
> → **AWS Transfer Family**

---

## Related Notes

- [[S3]]
- [[EFS]]
- [[S3 File Gateway]]
- [[Storage Gateway]]
- [[DataSync]]
- [[Snowball]]
- [[Route 53]]
- [[IAM]]
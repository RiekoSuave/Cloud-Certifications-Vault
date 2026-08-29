## What Problem Does It Solve?

[[ACM]] provides:

**Provisioning, management, and deployment of SSL/TLS certificates**

These certificates are used to secure:

**Network connections using HTTPS/TLS**

Common integrations include:

- [[Application Load Balancer]]
- [[CloudFront]]
- [[API Gateway]]

Architecture:

Client  
↓  
HTTPS  
↓  
TLS Certificate from ACM  
↓  
AWS Service

> [!tip] Memory Trick
> **ACM = Certificates for HTTPS**

---

## Core Concept

ACM helps remove much of the operational work involved in:

**Managing SSL/TLS certificates**

Instead of manually:

- Purchasing certificates
- Installing certificates
- Tracking expiration
- Renewing certificates

ACM can manage much of this lifecycle for:

**Supported AWS services**

### Killer Exam Clue

> **Need an SSL/TLS certificate for an AWS-managed service**
>
> → **ACM**

---

# SSL/TLS Certificates

Certificates are used to:

- Authenticate identities
- Enable encrypted connections
- Protect data in transit

Example:

Browser  
↓  
HTTPS  
↓  
TLS Certificate  
↓  
Application Load Balancer

### Memory Trick

**Certificate = Secure Connection**

---

# Encryption in Transit

ACM primarily helps protect:

**Data in transit**

This differs from:

[[KMS]]

which commonly protects:

**Data at rest**

### Killer Shortcut

**HTTPS / TLS**
→ ACM

**Encryption at rest**
→ KMS

---

# Public Certificates

ACM can issue:

**Publicly trusted certificates**

for public domain names.

Example:

`www.example.com`

These certificates can be used with supported AWS services to provide:

**HTTPS**

### Killer Exam Clue

> **Need a publicly trusted TLS certificate for an ALB**
>
> → **ACM Public Certificate**

---

# Private Certificates

ACM can also work with:

**Private certificates**

through:

**ACM Private CA**

These are useful for:

- Internal applications
- Private services
- Internal TLS
- Enterprise PKI

### Memory Trick

**Public Certificate = Internet Trust**

**Private Certificate = Internal Trust**

---

# Domain Validation

Before ACM issues a public certificate, you must prove:

**You control the domain**

ACM supports validation mechanisms such as:

- DNS validation
- Email validation

---

# DNS Validation

With:

**DNS validation**

ACM provides a DNS record that must be added to:

**The domain's DNS configuration**

Architecture:

ACM  
↓  
Validation Record  
↓  
DNS  
↓  
Domain Ownership Verified  
↓  
Certificate Issued

### Killer Exam Clue

> **Need easy automated renewal of an ACM certificate**
>
> → Prefer **DNS Validation**

---

# Route 53 Integration

When DNS is hosted in:

[[Route 53]]

ACM validation records can be conveniently added to:

**Route 53**

Architecture:

ACM  
↓  
DNS Validation Record  
↓  
Route 53  
↓  
Certificate Validation

### Memory Trick

**ACM + Route 53 = Easy DNS Validation**

---

# Email Validation

ACM can also validate domain ownership through:

**Email**

Validation messages are sent to:

**Domain-related addresses**

### Exam Principle

DNS validation is generally preferable when possible because it supports:

**Easier ongoing automated renewal**

---

# Certificate Renewal

ACM can automatically renew:

**Eligible ACM-issued certificates**

when they remain:

**Properly configured and in use**

This reduces:

**Certificate expiration risk**

### Killer Exam Clue

> **Need AWS to manage TLS certificate renewal automatically**
>
> → **ACM**

---

# Imported Certificates

You can import:

**Third-party certificates**

into ACM.

However:

**ACM does not automatically renew imported certificates**

You are responsible for:

- Obtaining replacement certificate
- Renewing it
- Reimporting it

### Killer Exam Trap

> **Imported certificate**
>
> → **Customer manages renewal**

---

# ACM-Issued vs Imported

| Feature | ACM-Issued | Imported |
|---|---:|---:|
| Store Certificate | ✅ | ✅ |
| Deploy to Supported Services | ✅ | ✅ |
| ACM-Managed Renewal | ✅ Eligible Certificates | ❌ |
| Customer Obtains Certificate | ❌ | ✅ |

### Memory Trick

**ACM Issues It**
→ ACM Can Renew It

**You Import It**
→ You Renew It

---

# ACM + Application Load Balancer

[[Application Load Balancer]] supports:

**HTTPS listeners**

The ALB can use:

**ACM certificates**

Architecture:

Client  
↓  
HTTPS  
↓  
ALB + ACM Certificate  
↓  
Target Group  
↓  
EC2

### Killer Exam Clue

> **Need HTTPS for an Application Load Balancer**
>
> → **ACM Certificate on ALB HTTPS Listener**

---

# TLS Termination

An ALB can perform:

**TLS termination**

Architecture:

Client  
↓  
HTTPS  
↓  
ALB  
↓  
HTTP or HTTPS  
↓  
Backend

The certificate is installed on:

**The Load Balancer**

not individually on:

**Every EC2 instance**

### Memory Trick

**Terminate TLS at the Load Balancer**

---

# Multiple Certificates on ALB

An ALB HTTPS listener can support:

**Multiple TLS certificates**

using:

**Server Name Indication — SNI**

This allows one load balancer to serve:

**Multiple HTTPS domains**

### Killer Exam Clue

> **Multiple HTTPS websites behind one ALB**
>
> → **SNI + Multiple Certificates**

---

# SNI

**Server Name Indication**

allows the client to tell the server:

**Which hostname it is trying to reach**

during the TLS handshake.

Example:

`app.example.com`

and:

`shop.example.com`

can use:

**Different certificates**

on:

**The same ALB**

### Memory Trick

**SNI = Select the Right Certificate**

---

# ACM + Network Load Balancer

[[Network Load Balancer]] can support:

**TLS listeners**

and use:

**ACM certificates**

Architecture:

Client  
↓  
TLS  
↓  
NLB  
↓  
Targets

### Exam Principle

> **ALB commonly terminates HTTPS**
>
> **NLB can terminate TLS**

---

# ACM + CloudFront

[[CloudFront]] can use:

**ACM certificates**

to provide HTTPS for:

**Custom domain names**

Example:

`www.example.com`

↓  

CloudFront Distribution

### Killer Exam Clue

> **Need HTTPS for a custom CloudFront domain**
>
> → **ACM Certificate**

---

# CloudFront Region Requirement

This is a major exam detail.

ACM certificates used with:

**CloudFront**

must be requested or imported in:

**us-east-1**

### Killer Exam Trap

> **CloudFront + ACM**
>
> → **Certificate must be in us-east-1**

### Memory Trick

**CloudFront Certificate Lives in Virginia**

`us-east-1`

---

# Regional ACM Certificates

ACM certificates used by regional services such as:

**Application Load Balancers**

must exist in:

**The same Region as the resource**

Example:

ALB:

`us-west-2`

ACM Certificate:

`us-west-2`

### Killer Shortcut

**ALB**
→ Same Region

**CloudFront**
→ us-east-1

---

# ACM + API Gateway

[[API Gateway]] can use ACM certificates for:

**Custom domain names**

This allows APIs to be exposed through:

**HTTPS custom domains**

Example:

`api.example.com`

---

# ACM + Route 53

A common architecture:

Route 53  
↓  
Domain Name  
↓  
ALB / CloudFront  
↓  
ACM Certificate

Important distinction:

[[Route 53]] handles:

**DNS**

ACM handles:

**TLS certificates**

### Memory Trick

**Route 53 = Find It**

**ACM = Secure It**

---

# ACM vs KMS

## [[KMS]]

Think:

**Encryption keys**

Commonly:

**Data at rest**

## ACM

Think:

**SSL/TLS certificates**

Commonly:

**Data in transit**

### Killer Shortcut

**S3 encryption key**
→ KMS

**HTTPS website certificate**
→ ACM

---

# ACM vs CloudHSM

## [[CloudHSM]]

Think:

**Dedicated cryptographic hardware**

## ACM

Think:

**Managed certificates**

### Exam Shortcut

Need standard HTTPS certificate?

→ ACM

Need dedicated HSM for specialized private-key operations?

→ CloudHSM

---

# ACM vs Secrets Manager

## [[Secrets Manager]]

Stores:

- Passwords
- API keys
- Credentials

## ACM

Manages:

**Certificates**

### Memory Trick

**Password**
→ Secrets Manager

**Certificate**
→ ACM

---

# ACM Private CA

**ACM Private CA**

allows organizations to create:

**Private certificate authorities**

for internal certificate issuance.

Use cases include:

- Internal applications
- Private APIs
- Internal servers
- Enterprise PKI
- Private service authentication

### Killer Exam Clue

> **Need an AWS-managed private certificate authority**
>
> → **ACM Private CA**

---

# Public vs Private Certificate

## Public ACM Certificate

Use when:

**Public clients need to trust the certificate**

Example:

Public website

## Private Certificate

Use when:

**Internal systems need private organizational trust**

Example:

Internal corporate service

### Killer Shortcut

**Internet Website**
→ Public Certificate

**Internal PKI**
→ Private CA

---

# Certificate Monitoring

Certificate expiration is a critical operational concern.

For ACM-managed certificates:

**Renewal can be automated**

For imported certificates:

**You must manage expiration and replacement**

### Exam Principle

> **Managed certificates reduce operational overhead**

---

# Architecture Thinking

## Scenario 1 — Public ALB

Company has:

`www.example.com`

behind an:

Application Load Balancer.

Need:

**HTTPS**

Choose:

ACM Public Certificate  
↓  
ALB HTTPS Listener

---

## Scenario 2 — Automatic Renewal

Company wants:

**Minimal operational overhead**

for certificate renewal.

Choose:

**ACM-issued certificate + DNS validation**

---

## Scenario 3 — Imported Certificate

Company imports a certificate from:

**Third-party CA**

Who renews it?

**The customer**

---

## Scenario 4 — CloudFront

CloudFront distribution needs:

**Custom HTTPS domain**

Certificate must be located in:

**us-east-1**

---

## Scenario 5 — Regional ALB

ALB runs in:

`eu-west-1`

Certificate should be in:

**eu-west-1**

---

## Scenario 6 — Multiple Domains

ALB serves:

`shop.example.com`

and:

`api.example.com`

with separate certificates.

Choose:

**SNI**

---

## Scenario 7 — Internal Corporate PKI

Company needs:

**Private certificates for internal services**

Choose:

**ACM Private CA**

---

## Scenario 8 — S3 Encryption

Need encryption key for:

**Stored S3 objects**

Do NOT choose ACM.

Choose:

**KMS**

---

# Scenario Recognition

Immediately think:

**ACM**

when you see:

- SSL certificate
- TLS certificate
- HTTPS
- Certificate renewal
- ALB certificate
- CloudFront custom HTTPS domain
- API Gateway custom domain
- Public certificate
- Private certificate authority

---

## Think DNS Validation When You See

- Automated certificate renewal
- Route 53
- Domain ownership verification
- Minimal certificate administration

---

## Think us-east-1 When You See

**CloudFront + ACM**

---

## Think Same Region When You See

**Regional AWS service + ACM**

---

# Exam Traps

## Trap 1 — ACM Encrypts S3 Objects

❌

Think:

**KMS**

---

## Trap 2 — Imported Certificates Automatically Renew

❌

Customer must:

**Renew and reimport them**

---

## Trap 3 — CloudFront Can Use an ACM Certificate from Any Region

❌

CloudFront ACM certificate:

**us-east-1**

---

## Trap 4 — ALB Can Use an ACM Certificate from Any Region

❌

Certificate must be:

**In the ALB's Region**

---

## Trap 5 — Route 53 Provides TLS Certificates

❌

Route 53:

**DNS**

ACM:

**Certificates**

---

## Trap 6 — Every EC2 Instance Needs the Public Certificate When TLS Terminates at ALB

❌

The certificate can be attached to:

**The ALB**

---

## Trap 7 — Multiple HTTPS Domains Require Multiple Load Balancers

❌

Use:

**SNI + Multiple Certificates**

---

# Quick Cheat Sheet

| Exam Clue | Answer |
|---|---|
| SSL/TLS Certificate | ACM |
| HTTPS | ACM |
| Public Certificate | ACM |
| Internal Certificate Authority | ACM Private CA |
| Domain Validation | DNS / Email |
| Preferred Validation for Automation | DNS |
| ALB HTTPS | ACM |
| Multiple ALB Certificates | SNI |
| CloudFront Certificate Region | us-east-1 |
| Regional Service Certificate | Same Region |
| ACM-Issued Renewal | ACM Managed |
| Imported Certificate Renewal | Customer |
| Encryption at Rest | KMS |
| DNS | Route 53 |

---

# Certificate Decision Map

Need:

**Public HTTPS certificate**

→ ACM Public Certificate

Need:

**Automatic certificate renewal**

→ ACM-issued + DNS Validation

Need:

**ALB HTTPS**

→ ACM Certificate

Need:

**Multiple HTTPS domains on ALB**

→ SNI

Need:

**CloudFront HTTPS**

→ ACM in us-east-1

Need:

**Internal private certificates**

→ ACM Private CA

Need:

**Encryption at rest**

→ KMS

---

# Final Exam Rapid-Fire

> **HTTPS CERTIFICATE**
> → ACM
>
> **PUBLIC TLS CERT**
> → ACM
>
> **AUTOMATIC RENEWAL**
> → ACM-ISSUED CERTIFICATE
>
> **BEST VALIDATION FOR AUTOMATION**
> → DNS
>
> **ALB HTTPS**
> → ACM
>
> **MULTIPLE CERTIFICATES**
> → SNI
>
> **CLOUDFRONT CERTIFICATE**
> → US-EAST-1
>
> **REGIONAL SERVICE**
> → SAME REGION
>
> **IMPORTED CERTIFICATE**
> → CUSTOMER RENEWS
>
> **INTERNAL PKI**
> → ACM PRIVATE CA
>
> **DATA AT REST**
> → KMS

---

## Master Memory Trick

> [!tip] ACM Master Memory Trick
> Imagine AWS has a:
>
> **CERTIFICATE OFFICE**
>
> Your website walks in and says:
>
> **"I need HTTPS."**
>
> ACM asks:
>
> **"Can you prove you own the domain?"**
>
> You answer with:
>
> **DNS VALIDATION**
>
> ACM gives you:
>
> **THE CERTIFICATE**
>
> You attach it to:
>
> **ALB / CLOUDFRONT / API GATEWAY**
>
> and ACM can handle:
>
> **RENEWAL**
>
> But if you walk into the office carrying:
>
> **YOUR OWN IMPORTED CERTIFICATE**
>
> ACM says:
>
> **"I'll hold it, but YOU renew it."**

So remember:

> **ACM**
> → CERTIFICATE
>
> **DNS VALIDATION**
> → PROVE DOMAIN
>
> **SNI**
> → MULTIPLE CERTIFICATES
>
> **ALB**
> → SAME REGION
>
> **CLOUDFRONT**
> → US-EAST-1
>
> **PRIVATE CA**
> → INTERNAL CERTIFICATES
>
> **KMS**
> → ENCRYPTION KEYS

And the killer SAA question:

> **"Does the requirement involve SSL/TLS certificates for HTTPS on an AWS-managed service?"**
>
> YES
>
> → **ACM**

---

## Related Notes

- [[Application Load Balancer]]
- [[Network Load Balancer]]
- [[CloudFront]]
- [[API Gateway]]
- [[Route 53]]
- [[KMS]]
- [[CloudHSM]]
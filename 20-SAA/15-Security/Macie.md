## What Problem Does It Solve?

[[Macie]] is AWS's:

**Managed data security and privacy service for S3**

It uses machine learning and pattern matching to discover:

- Personally identifiable information — PII
- Financial data
- Credentials
- Sensitive business data
- Other sensitive information

Architecture:

[[S3]]  
↓  
Macie  
↓  
Sensitive Data Discovery  
↓  
Security Findings

> [!tip] Memory Trick
> **Macie = Find Sensitive Data in S3**

---

## Core Concept

Macie helps answer:

> **"What sensitive data is stored in my S3 buckets?"**

It can inspect S3 objects and identify:

**Sensitive information**

### Killer Exam Clue

> **Need to automatically discover PII or sensitive data stored in S3**
>
> → **Macie**

---

# S3 Focus

Macie is primarily associated with:

**Amazon S3**

It evaluates:

- Buckets
- Objects
- Sensitive data patterns
- Access/security posture

### Memory Trick

**Macie = S3 Data Detective**

---

# Sensitive Data Discovery

Macie can identify data such as:

- Names
- Addresses
- Email addresses
- Phone numbers
- Credit card numbers
- Social Security numbers
- Credentials
- Financial information

### Killer Exam Clue

> **Find credit card numbers stored in S3 objects**
>
> → **Macie**

---

# Machine Learning + Pattern Matching

Macie uses:

- Machine learning
- Pattern matching
- Managed data identifiers

to detect:

**Sensitive content**

This reduces the need to manually inspect:

**Every S3 object**

---

# Managed Data Identifiers

Macie provides:

**Managed Data Identifiers**

for common sensitive-data types.

Examples include patterns for:

- PII
- Financial information
- Credentials

### Memory Trick

**Managed Identifier = AWS Knows the Pattern**

---

# Custom Data Identifiers

You can create:

**Custom Data Identifiers**

when you need to detect:

**Organization-specific sensitive data**

Example:

Internal Employee ID format

or:

Custom account-number pattern

### Killer Exam Clue

> **Need to discover a company-specific sensitive-data pattern in S3**
>
> → **Macie Custom Data Identifier**

---

# Discovery Jobs

Macie uses:

**Sensitive Data Discovery Jobs**

to inspect selected:

**S3 objects**

Architecture:

S3 Buckets  
↓  
Macie Discovery Job  
↓  
Object Inspection  
↓  
Sensitive Data Findings

### Memory Trick

**Discovery Job = Scan the Data**

---

# Scheduled Discovery

Discovery jobs can be:

- One-time
- Scheduled

Use scheduled jobs when:

**Sensitive data continues to arrive**

### Killer Exam Clue

> **Continuously inspect new S3 data for sensitive information**
>
> → **Scheduled Macie Discovery**

---

# Automated Sensitive Data Discovery

Macie can also provide:

**Automated sensitive data discovery**

to continuously evaluate S3 data with less manual job configuration.

For SAA, the key concept is:

> **Macie can continuously help identify sensitive data across S3**

---

# Macie Findings

When Macie identifies a security issue or sensitive data, it creates:

**Findings**

Findings can include:

- Affected bucket/object
- Type of sensitive data
- Severity
- Security context

### Memory Trick

**Macie Finds → Finding Appears**

---

# Sensitive Data Findings

A finding may indicate that an S3 object contains:

**Sensitive information**

Example:

`s3://company-bucket/customer-data.csv`

contains:

**Credit card numbers**

---

# Policy Findings

Macie can also generate findings related to:

**S3 security posture**

Examples can include:

- Publicly accessible buckets
- Unencrypted or overly exposed data
- Risky S3 configurations

### Exam Principle

> **Macie combines sensitive-data discovery with S3 security awareness**

---

# Macie vs GuardDuty

This is a key distinction.

## Macie

Think:

**What sensitive data exists in S3?**

## [[GuardDuty]]

Think:

**Is suspicious or malicious activity happening?**

### Killer Shortcut

PII in S3  
→ Macie

Compromised credentials  
→ GuardDuty

---

# Macie vs Inspector

## Macie

Think:

**Sensitive data**

## [[Inspector]]

Think:

**Vulnerabilities**

### Memory Trick

**Macie = DATA**

**Inspector = SOFTWARE**

---

# Macie vs Security Hub

## Macie

Generates:

**Sensitive-data and S3 security findings**

## [[06-Security/Security Hub]]

Aggregates:

**Security findings from multiple services**

### Killer Shortcut

Need to discover sensitive data  
→ Macie

Need one place for all findings  
→ Security Hub

---

# Macie vs Config

## [[Config]]

Think:

**Resource configuration compliance**

## Macie

Think:

**Sensitive S3 data discovery**

Example:

S3 bucket became public  
→ Config can detect configuration state

S3 object contains PII  
→ Macie

---

# Macie vs GuardDuty S3 Protection

These can sound similar.

## GuardDuty S3 Protection

Think:

**Suspicious S3 activity**

Example:

Unusual object access

## Macie

Think:

**Sensitive data inside S3**

Example:

Object contains credit card numbers

### Memory Trick

**GuardDuty = Suspicious Access**

**Macie = Sensitive Content**

---

# Macie vs Athena

## [[Athena]]

Think:

**Query S3 data**

## Macie

Think:

**Classify sensitive data**

Athena can search data with SQL.

Macie is purpose-built for:

**Sensitive data discovery**

---

# Macie vs Glue

## [[Glue]]

Think:

- ETL
- Crawlers
- Metadata
- Data Catalog

## Macie

Think:

**Security classification**

### Killer Shortcut

Discover schema  
→ Glue

Discover PII  
→ Macie

---

# Macie + Security Hub

Architecture:

Macie  
↓  
Sensitive Data Finding  
↓  
Security Hub  
↓  
Central Security View

### Killer Exam Clue

> **Centralize Macie findings with other AWS security findings**
>
> → **Security Hub**

---

# Macie + EventBridge

Macie findings can be routed through:

[[EventBridge]]

Architecture:

Macie Finding  
↓  
EventBridge  
↓  
Lambda / SNS / Automation

### Killer Exam Clue

> **Automatically respond when Macie finds sensitive data**
>
> → **Macie + EventBridge**

---

# Macie + SNS

For notification:

Macie  
↓  
EventBridge  
↓  
[[SNS]]  
↓  
Security Team

Use when:

**Security personnel need immediate awareness**

---

# Automated Remediation

Example:

Macie detects:

Sensitive data in public S3 bucket  
↓  
EventBridge  
↓  
Lambda / Systems Manager  
↓  
Restrict Access

### Memory Trick

**Macie Detects**

**EventBridge Routes**

**Automation Fixes**

---

# Multi-Account Macie

Macie supports:

**Centralized management across AWS accounts**

This is useful with:

**AWS Organizations**

Architecture:

AWS Organizations  
↓  
Security Account  
↓  
Macie  
↓  
Member Accounts

### Killer Exam Clue

> **Centrally manage sensitive-data discovery across multiple AWS accounts**
>
> → **Macie multi-account management**

---

# Delegated Administrator

An organization can configure a:

**Delegated administrator**

to centrally manage Macie.

This supports:

**Enterprise-wide S3 data security**

---

# S3 Inventory Awareness

Macie evaluates:

**S3 bucket information**

to help organizations understand:

- Where sensitive data may exist
- Which buckets may be risky
- Which data needs investigation

---

# Cost Thinking

Macie sensitive-data discovery can incur cost based on:

**Amount of data analyzed**

For large S3 environments:

Use thoughtful scoping and automation.

### SAA Principle

> **Scan the right data, not blindly everything when requirements are narrower**

---

# Architecture Thinking

## Scenario 1 — Find PII

Company stores:

Millions of S3 objects

and needs to identify:

**Personally identifiable information**

Choose:

**Macie**

---

## Scenario 2 — Credit Card Numbers

Security team wants to find:

**PCI-related data**

inside S3.

Choose:

**Macie**

---

## Scenario 3 — Custom Employee IDs

Company has a proprietary employee identifier format.

Need to discover it in S3.

Choose:

**Custom Data Identifier**

---

## Scenario 4 — Compromised IAM Credentials

Need to detect:

**Suspicious credential use**

Choose:

**GuardDuty**

not Macie.

---

## Scenario 5 — Vulnerable EC2 Package

Need to detect:

**Known CVE**

Choose:

**Inspector**

---

## Scenario 6 — Public S3 Bucket Compliance

Need to continuously evaluate:

**Whether S3 bucket configuration is public**

Think:

**Config**

rather than Macie as the primary compliance service.

---

## Scenario 7 — Sensitive Data + Automation

Macie detects sensitive data in:

**Unexpected S3 location**

Need automatic alert.

Choose:

Macie  
↓  
EventBridge  
↓  
SNS

---

## Scenario 8 — Central Security Dashboard

Need findings from:

- Macie
- Inspector
- GuardDuty

Choose:

**Security Hub**

---

# Scenario Recognition

Immediately think:

**Macie**

when you see:

- Sensitive data
- PII
- Credit card numbers
- S3 classification
- Data privacy
- Data discovery
- Sensitive S3 objects
- Custom data identifiers

---

## Think GuardDuty When You See

- Suspicious activity
- Compromised credentials
- Malicious IP
- Threat detection

---

## Think Inspector When You See

- CVE
- Vulnerability
- Vulnerable package

---

## Think Config When You See

- Configuration compliance
- Public bucket configuration
- Encryption setting
- Required configuration

---

# Exam Traps

## Trap 1 — Macie Scans EC2 for CVEs

❌

Think:

**Inspector**

---

## Trap 2 — Macie Detects Compromised IAM Credentials

❌

Think:

**GuardDuty**

---

## Trap 3 — Macie Is a DDoS Protection Service

❌

Think:

**Shield**

---

## Trap 4 — Macie Blocks SQL Injection

❌

Think:

**WAF**

---

## Trap 5 — Macie Is Mainly a General S3 Query Tool

❌

Think:

**Athena**

Macie focuses on:

**Sensitive-data discovery**

---

## Trap 6 — Macie Is the Central Security Findings Dashboard

❌

Think:

**Security Hub**

---

# Quick Cheat Sheet

| Exam Clue | Answer |
|---|---|
| Sensitive Data in S3 | Macie |
| PII Discovery | Macie |
| Credit Card Discovery | Macie |
| Custom Sensitive Pattern | Custom Data Identifier |
| Scheduled S3 Scan | Discovery Job |
| Suspicious AWS Activity | GuardDuty |
| Software Vulnerability | Inspector |
| Resource Compliance | Config |
| Central Security Findings | Security Hub |
| SQL on S3 | Athena |

---

# Security Decision Map

Need:

**Find sensitive data in S3**

→ Macie

Need:

**Detect active threats**

→ GuardDuty

Need:

**Find software vulnerabilities**

→ Inspector

Need:

**Check configuration compliance**

→ Config

Need:

**Aggregate security findings**

→ Security Hub

Need:

**Query S3 data**

→ Athena

---

# Macie vs GuardDuty vs Inspector

| Question | Service |
|---|---|
| What sensitive data is in S3? | Macie |
| Is malicious activity happening? | GuardDuty |
| What software is vulnerable? | Inspector |

### Memory Trick

> **MACIE**
> → DATA
>
> **GUARDDUTY**
> → THREAT
>
> **INSPECTOR**
> → VULNERABILITY

---

# Final Exam Rapid-Fire

> **PII IN S3**
> → MACIE
>
> **CREDIT CARD DATA**
> → MACIE
>
> **SENSITIVE DATA DISCOVERY**
> → MACIE
>
> **CUSTOM SENSITIVE PATTERN**
> → CUSTOM DATA IDENTIFIER
>
> **SCHEDULED S3 CLASSIFICATION**
> → DISCOVERY JOB
>
> **ACTIVE THREAT**
> → GUARDDUTY
>
> **CVE**
> → INSPECTOR
>
> **CONFIGURATION COMPLIANCE**
> → CONFIG
>
> **CENTRAL FINDINGS**
> → SECURITY HUB
>
> **SQL ON S3**
> → ATHENA

---

## Master Memory Trick

> [!tip] Macie Master Memory Trick
> Imagine your company has:
>
> **A giant S3 warehouse**
>
> containing millions of files.
>
> Somewhere inside are:
>
> **SOCIAL SECURITY NUMBERS**
>
> **CREDIT CARD NUMBERS**
>
> **EMAIL ADDRESSES**
>
> **CONFIDENTIAL DATA**
>
> Nobody knows exactly where.
>
> Macie walks through the warehouse with:
>
> **A SENSITIVE-DATA SCANNER**
>
> and says:
>
> **"This file contains PII."**
>
> **"This object contains financial data."**
>
> **"This bucket contains sensitive information."**

So remember:

> **MACIE**
> → SENSITIVE DATA
>
> **S3**
> → PRIMARY DATA SOURCE
>
> **PII**
> → MACIE
>
> **CUSTOM IDENTIFIER**
> → COMPANY-SPECIFIC PATTERN
>
> **GUARDDUTY**
> → THREAT
>
> **INSPECTOR**
> → VULNERABILITY
>
> **SECURITY HUB**
> → CENTRAL FINDINGS

And the killer SAA question:

> **"Does the requirement involve automatically discovering, classifying, or protecting sensitive information stored in S3?"**
>
> YES
>
> → **Macie**

---

## Related Notes

- [[S3]]
- [[GuardDuty]]
- [[Inspector]]
- [[06-Security/Security Hub]]
- [[Config]]
- [[Athena]]
- [[EventBridge]]
- [[SNS]]
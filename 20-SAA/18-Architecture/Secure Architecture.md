## Core Concept

Secure architecture means designing systems so security is:

**Built into every layer**

rather than added afterward.

A strong AWS security architecture considers:

- Identity
- Network access
- Encryption
- Secrets
- Monitoring
- Logging
- Threat detection
- Vulnerability management
- Data protection

> [!tip] Memory Trick
> **Secure Architecture = Identity + Network + Data + Detection**

---

# Least Privilege

[[IAM]] should grant:

**Only the permissions required**

Bad:

Application Role  
→ AdministratorAccess

Better:

Application Role  
→ Only required S3 / DynamoDB / API permissions

### Killer Exam Clue

> **Application needs access to one specific AWS resource**
>
> → Use **least-privilege IAM policy**

---

# IAM Roles

AWS workloads should normally use:

**IAM Roles**

rather than:

**Hardcoded access keys**

Examples:

EC2  
→ IAM Role

Lambda  
→ Execution Role

ECS Task  
→ Task Role

### Killer Exam Clue

> **EC2 needs access to S3 without storing credentials**
>
> → **IAM Role**

---

# Avoid Long-Lived Credentials

Long-lived access keys create:

**Security risk**

Better options include:

- IAM Roles
- Temporary credentials
- Federation
- STS

### Memory Trick

**Temporary Credentials > Hardcoded Keys**

---

# MFA

MFA adds:

**Additional authentication protection**

Especially important for:

- Root user
- Privileged IAM users
- Sensitive administrative access

### Killer Exam Principle

> **Root account should be protected with MFA**

---

# Root User

The AWS account root user should be used:

**As little as possible**

Best practices include:

- Enable MFA
- Avoid routine use
- Do not create root access keys
- Use IAM identities for normal administration

### Memory Trick

**Root = Emergency Use**

---

# Identity Federation

Federation allows users to access AWS using:

**Existing identity systems**

rather than creating:

**Separate long-lived IAM users**

### Killer Exam Clue

> **Employees should access AWS using corporate credentials**
>
> → **Federation / IAM Identity Center**

---

# IAM Identity Center

IAM Identity Center provides:

**Centralized workforce access**

across:

- Multiple AWS accounts
- Applications

### Killer Exam Clue

> **Centrally manage employee access across an AWS Organization**
>
> → **IAM Identity Center**

---

# AWS Organizations

AWS Organizations provides:

**Centralized multi-account governance**

It helps organizations separate:

- Production
- Development
- Security
- Networking
- Logging

into:

**Different AWS accounts**

### Memory Trick

**Accounts = Security Boundaries**

---

# Service Control Policies

SCPs define:

**Maximum available permissions**

for accounts or OUs.

They do NOT directly grant:

**IAM permissions**

### Killer Exam Trap

> **SCP allows an action**
>
> does NOT mean:
>
> **The user automatically has permission**

### Memory Trick

**SCP = Guardrail**

---

# Multi-Account Architecture

A strong security design may separate:

- Production account
- Development account
- Security account
- Logging account
- Networking account

### Benefits

- Blast-radius reduction
- Administrative separation
- Central governance
- Better isolation

### Killer Exam Principle

> **Separate critical workloads into accounts when strong isolation is required**

---

# Defense in Depth

Defense in depth means using:

**Multiple layers of security**

Example:

Internet  
↓  
[[WAF]]  
↓  
ALB Security Group  
↓  
Application Security Group  
↓  
Database Security Group  
↓  
IAM + Encryption

If one control fails:

**Other controls still exist**

### Memory Trick

**Never Rely on One Lock**

---

# Security Groups

[[Security Groups]] provide:

**Stateful resource-level network control**

Think:

- Allow rules only
- Instance/ENI level
- Security Group references

### Killer Exam Clue

> **Only ALB should reach application EC2**
>
> → Reference **ALB Security Group**

---

# NACL

[[NACL]] provides:

**Stateless subnet-level filtering**

Think:

- Allow
- Deny
- Rule numbers
- Subnet boundary

### Killer Exam Clue

> **Explicitly block a malicious CIDR at subnet level**
>
> → **NACL**

---

# Security Group vs NACL

| Requirement | Answer |
|---|---|
| Resource-Level Stateful | Security Group |
| Subnet-Level Stateless | NACL |
| Explicit Deny | NACL |
| SG Reference | Security Group |

---

# Private Subnets

Sensitive workloads should generally avoid:

**Direct Internet exposure**

Example:

Internet  
↓  
Public ALB  
↓  
Private Application Tier  
↓  
Private Database Tier

### Killer Exam Principle

> **Public entry point does not require public backend servers**

---

# Bastion Host vs Session Manager

Traditional:

Administrator  
↓  
Bastion Host  
↓  
Private EC2

More managed approach:

Administrator  
↓  
[[Systems Manager]] Session Manager  
↓  
Private EC2

### Killer Exam Clue

> **Need administrative EC2 access without opening SSH or using public IPs**
>
> → **Session Manager**

---

# VPC Endpoints

[[VPC Endpoints]] allow:

**Private connectivity to supported AWS services**

without requiring:

- Public IP
- NAT path
- Internet Gateway path

### Killer Exam Clue

> **Private workload needs AWS service access without Internet**
>
> → **VPC Endpoint**

---

# Endpoint Policies

Endpoint Policies can restrict:

**What may be accessed through a VPC endpoint**

Example:

S3 Endpoint  
→ Only approved bucket

### Exam Principle

> **Endpoint Policy adds another access-control layer**

---

# Encryption at Rest

Data at rest should be encrypted when required.

Common services integrate with:

[[KMS]]

Examples:

- S3
- EBS
- RDS
- DynamoDB

### Killer Exam Clue

> **Need customer control over encryption keys**
>
> → **KMS Customer Managed Key**

---

# KMS

[[KMS]] provides:

**Managed encryption key control**

Think:

- Key policies
- Encryption integration
- Key rotation
- Auditability

### Memory Trick

**KMS = KEY**

---

# CloudHSM

[[CloudHSM]] provides:

**Dedicated HSM hardware**

Think:

- Dedicated cryptographic hardware
- Specialized compliance
- Customer-controlled HSM

### Killer Shortcut

Managed AWS key service  
→ KMS

Dedicated cryptographic hardware  
→ CloudHSM

---

# Encryption in Transit

Use:

**TLS / HTTPS**

to protect traffic in transit.

[[ACM]] can provide:

**Managed TLS certificates**

for supported services.

### Killer Exam Clue

> **Need managed HTTPS certificate for ALB**
>
> → **ACM**

---

# Secrets Manager

[[Secrets Manager]] stores:

**Application secrets**

such as:

- Database passwords
- API keys
- Tokens

It can also support:

**Automatic rotation**

### Killer Exam Clue

> **Need automatic rotation of RDS credentials**
>
> → **Secrets Manager**

---

# Parameter Store

[[Parameter Store]] is useful for:

**Application configuration**

including:

**SecureString**

when appropriate.

### Killer Shortcut

Secret + automatic rotation  
→ Secrets Manager

Configuration parameter  
→ Parameter Store

---

# Never Store Secrets in Code

Bad:

`db_password = "mypassword123"`

Better:

Application  
↓  
IAM Role  
↓  
Secrets Manager  
↓  
Retrieve Secret

### Memory Trick

**Code Is Not a Vault**

---

# S3 Security

Strong [[S3]] security can involve:

- Block Public Access
- Bucket Policies
- IAM
- Encryption
- Versioning
- Logging
- VPC endpoints

### Killer Exam Clue

> **S3 bucket must never become public**
>
> → **Block Public Access**

---

# S3 Bucket Policy

Bucket policies provide:

**Resource-based access control**

They can enforce conditions such as:

- Required encryption
- Specific principals
- VPC endpoint access
- HTTPS-only access

### Killer Exam Principle

> **Resource policy can enforce conditions at the bucket boundary**

---

# HTTPS-Only S3 Access

A bucket policy can deny requests that do not use:

**Secure transport**

This enforces:

**TLS**

### Exam Recognition

> **S3 access must use HTTPS**
>
> → Bucket policy condition requiring secure transport

---

# WAF

[[WAF]] protects:

**Web applications from malicious HTTP(S) requests**

Think:

- SQL injection
- XSS
- Bad IPs
- Rate rules
- Bots

### Killer Exam Clue

> **Block SQL injection**
>
> → **WAF**

---

# Shield

[[Shield]] protects against:

**DDoS attacks**

### Killer Shortcut

Bad web request  
→ WAF

Too much malicious traffic  
→ Shield

---

# Network Firewall

[[Network Firewall]] provides:

**Advanced VPC network inspection**

Think:

- Stateful inspection
- Stateless inspection
- Suricata
- Intrusion prevention

### Killer Exam Clue

> **Need managed stateful inspection of VPC traffic**
>
> → **Network Firewall**

---

# Firewall Manager

[[Firewall Manager]] provides:

**Centralized firewall/security policy enforcement**

across:

**Multiple AWS accounts**

### Killer Exam Clue

> **Apply the same WAF/Network Firewall policies across an AWS Organization**
>
> → **Firewall Manager**

---

# GuardDuty

[[GuardDuty]] provides:

**Threat detection**

Think:

- Suspicious IAM activity
- Malicious IPs
- Credential compromise
- Command-and-control

### Killer Exam Clue

> **Detect suspicious activity in AWS**
>
> → **GuardDuty**

---

# Inspector

[[Inspector]] provides:

**Vulnerability management**

Think:

- CVEs
- Vulnerable packages
- EC2
- ECR images
- Lambda

### Killer Exam Clue

> **Continuously scan workloads for known vulnerabilities**
>
> → **Inspector**

---

# Macie

[[Macie]] provides:

**Sensitive data discovery in S3**

Think:

- PII
- Credit cards
- Sensitive information

### Killer Exam Clue

> **Discover PII in S3**
>
> → **Macie**

---

# Security Hub

[[Security Hub]] provides:

**Centralized security findings and posture**

It can aggregate findings from:

- GuardDuty
- Inspector
- Macie
- Other supported sources

### Killer Exam Clue

> **Need one central dashboard for AWS security findings**
>
> → **Security Hub**

---

# Config

[[Config]] tracks:

**Resource configuration and compliance**

Think:

- Configuration history
- Compliance rules
- Resource changes

### Killer Exam Clue

> **Determine whether AWS resources remain compliant with required configuration**
>
> → **Config**

---

# CloudTrail

[[CloudTrail]] records:

**AWS API activity**

Think:

- Who did it?
- Which API?
- When?
- From where?

### Killer Exam Clue

> **Who changed the Security Group?**
>
> → **CloudTrail**

---

# CloudWatch

[[CloudWatch]] provides:

**Monitoring**

Think:

- Metrics
- Logs
- Alarms
- Dashboards

### Memory Trick

**CloudWatch = What Is Happening**

**CloudTrail = Who Did It**

---

# VPC Flow Logs

[[VPC Flow Logs]] record:

**Network traffic metadata**

Think:

- Source IP
- Destination IP
- Port
- ACCEPT
- REJECT

### Killer Exam Clue

> **Determine whether network traffic was rejected**
>
> → **VPC Flow Logs**

---

# Security Logging Decision Map

Need:

**AWS API activity**

→ CloudTrail

Need:

**Metrics and application/system logs**

→ CloudWatch

Need:

**Network connection metadata**

→ VPC Flow Logs

Need:

**DNS query records**

→ Route 53 Resolver Query Logging

Need:

**Central security findings**

→ Security Hub

---

# Detection vs Prevention

## Preventive / Protective

Think:

- IAM
- Security Groups
- NACL
- WAF
- Shield
- Network Firewall

## Detective

Think:

- GuardDuty
- Inspector
- Macie
- Config
- CloudTrail

### Memory Trick

**Prevent = Stop**

**Detect = Find**

---

# Shared Responsibility Model

AWS security is based on:

**Shared Responsibility**

AWS is responsible for:

**Security OF the cloud**

Customer is responsible for:

**Security IN the cloud**

### AWS Examples

- Physical facilities
- Hardware
- Core infrastructure

### Customer Examples

- IAM permissions
- Data encryption choices
- Security Groups
- Application security
- OS patching on EC2

### Killer Exam Principle

> **Responsibility changes depending on how managed the service is**

---

# EC2 Responsibility

With EC2, customer manages more:

- Guest OS
- Patching
- Applications
- Security Groups
- IAM
- Data

### Memory Trick

**EC2 = More Customer Responsibility**

---

# Managed Service Responsibility

With managed/serverless services:

AWS handles more underlying infrastructure.

Example:

[[Lambda]]

Customer focuses more on:

- Code
- IAM
- Data
- Configuration

### Killer Exam Principle

> **More managed service = less infrastructure security administration**

---

# Patching

For EC2:

Customer is generally responsible for:

**Guest OS patching**

[[Systems Manager]] Patch Manager can help automate:

**Patching**

### Killer Exam Clue

> **Centrally patch managed EC2 instances**
>
> → **Systems Manager Patch Manager**

---

# Vulnerability vs Patching

## Inspector

Finds:

**Vulnerabilities**

## Patch Manager

Applies:

**Patches**

### Killer Shortcut

Find CVE  
→ Inspector

Install patch  
→ Patch Manager

---

# Backup Security

Backups should also be protected through:

- Encryption
- Access control
- Cross-account isolation
- Backup Vault Lock
- Cross-Region copies

### Exam Principle

> **A backup that an attacker can delete is weaker DR protection**

---

# Multi-Account Security

A mature organization may centralize:

**Security tooling**

in a dedicated:

**Security account**

Examples:

- Security Hub
- GuardDuty administration
- Firewall Manager
- Logging

### Memory Trick

**Central Security Account = Security Headquarters**

---

# Centralized Logging

Critical logs may be sent to:

**A separate logging account**

This reduces risk that:

**An attacker in the workload account can alter evidence**

### Killer Exam Principle

> **Separate logs from the workloads they monitor when strong isolation is required**

---

# Immutable Logs

Some security/compliance requirements may require logs and backups to be:

**Protected from modification or deletion**

Use appropriate:

- Access controls
- Object Lock
- Backup Vault Lock
- Separate accounts

depending on:

**The requirement**

---

# S3 Object Lock

S3 Object Lock can provide:

**WORM-style object retention**

### Killer Exam Clue

> **S3 objects must not be deleted or overwritten during retention period**
>
> → **S3 Object Lock**

---

# Security Architecture Thinking

## Scenario 1 — EC2 to S3

EC2 needs to read:

One S3 bucket

without storing credentials.

Choose:

**IAM Role + least-privilege policy**

---

## Scenario 2 — Private Database

RDS should only accept connections from:

Application EC2.

Choose:

**Database Security Group referencing Application SG**

---

## Scenario 3 — Secrets

Application currently stores:

Database password in source code.

Choose:

**Secrets Manager**

---

## Scenario 4 — SQL Injection

Public web application needs protection from:

**SQL injection**

Choose:

**WAF**

---

## Scenario 5 — DDoS

Application faces:

**Large volumetric attacks**

Choose:

**Shield**

---

## Scenario 6 — Suspicious API Activity

Need to detect:

**Potentially compromised IAM credentials**

Choose:

**GuardDuty**

---

## Scenario 7 — Vulnerable EC2 Package

Need to detect:

**Known CVE**

Choose:

**Inspector**

---

## Scenario 8 — PII in S3

Need to discover:

**Sensitive customer data**

Choose:

**Macie**

---

## Scenario 9 — Central Findings

Need one place for:

GuardDuty + Inspector + Macie

Choose:

**Security Hub**

---

## Scenario 10 — Who Changed Resource?

Need to identify:

**Who modified a route table**

Choose:

**CloudTrail**

---

## Scenario 11 — Block One CIDR

Need:

**Explicit deny at subnet boundary**

Choose:

**NACL**

---

## Scenario 12 — Advanced VPC Inspection

Need:

**Stateful inspection and intrusion prevention**

Choose:

**Network Firewall**

---

# Scenario Recognition

Immediately think:

**IAM**

when you see:

- Permissions
- Identity
- Least privilege
- AWS API access

Think:

**KMS**

when you see:

- Encryption keys
- Customer-controlled encryption

Think:

**Secrets Manager**

when you see:

- Password
- Secret
- Rotation

Think:

**WAF**

when you see:

- SQL injection
- XSS

Think:

**GuardDuty**

when you see:

- Suspicious activity

Think:

**Inspector**

when you see:

- CVE

Think:

**Macie**

when you see:

- PII in S3

---

# Exam Traps

## Trap 1 — Hardcoded Access Keys Are Fine Inside Private EC2

❌

Use:

**IAM Roles**

---

## Trap 2 — Security Group Can Explicitly Deny

❌

Think:

**NACL**

---

## Trap 3 — Private Subnet Means No Security Controls Needed

❌

Still use:

- Security Groups
- IAM
- Encryption
- Monitoring

---

## Trap 4 — KMS Stores Database Passwords

❌

Think:

**Secrets Manager**

---

## Trap 5 — WAF Is Main DDoS Service

❌

Think:

**Shield**

---

## Trap 6 — GuardDuty Blocks All Threats

❌

GuardDuty primarily:

**Detects**

---

## Trap 7 — Security Hub Performs All Detection

❌

It primarily:

**Aggregates findings**

---

## Trap 8 — CloudTrail Records Network Packets

❌

Think:

**VPC Flow Logs**

CloudTrail records:

**API calls**

---

## Trap 9 — Inspector Installs Patches

❌

Inspector:

**Finds vulnerabilities**

Patch Manager:

**Patches**

---

## Trap 10 — Encryption Alone Makes Architecture Secure

❌

Security requires:

**Multiple layers**

---

# Quick Cheat Sheet

| Exam Clue | Answer |
|---|---|
| Least Privilege | IAM |
| Workload AWS Access | IAM Role |
| Workforce Access | IAM Identity Center |
| Org Permission Guardrail | SCP |
| Resource Firewall | Security Group |
| Explicit Subnet Deny | NACL |
| Private AWS Access | VPC Endpoint |
| Encryption Keys | KMS |
| Dedicated HSM | CloudHSM |
| Secrets + Rotation | Secrets Manager |
| TLS Certificate | ACM |
| SQL Injection | WAF |
| DDoS | Shield |
| VPC Inspection | Network Firewall |
| Central Firewall Policies | Firewall Manager |
| Threat Detection | GuardDuty |
| Vulnerability Scanning | Inspector |
| PII Discovery | Macie |
| Central Security Findings | Security Hub |
| Configuration Compliance | Config |
| API Audit | CloudTrail |
| Network Metadata | VPC Flow Logs |

---

# Security Decision Map

Need:

**Who can access AWS API?**

→ IAM

Need:

**Who can reach resource over network?**

→ Security Group

Need:

**Explicit subnet deny?**

→ NACL

Need:

**Encrypt data?**

→ KMS

Need:

**Store secret?**

→ Secrets Manager

Need:

**Block web attack?**

→ WAF

Need:

**Block advanced VPC traffic?**

→ Network Firewall

Need:

**Detect threat?**

→ GuardDuty

Need:

**Find vulnerability?**

→ Inspector

Need:

**Find sensitive S3 data?**

→ Macie

Need:

**See findings together?**

→ Security Hub

---

# Final Exam Rapid-Fire

> **LEAST PRIVILEGE**
> → IAM
>
> **NO HARDCODED KEYS**
> → IAM ROLE
>
> **MULTI-ACCOUNT WORKFORCE ACCESS**
> → IAM IDENTITY CENTER
>
> **ORG GUARDRAIL**
> → SCP
>
> **RESOURCE FIREWALL**
> → SECURITY GROUP
>
> **SUBNET DENY**
> → NACL
>
> **PRIVATE AWS SERVICE**
> → VPC ENDPOINT
>
> **ENCRYPTION KEY**
> → KMS
>
> **SECRET ROTATION**
> → SECRETS MANAGER
>
> **TLS CERTIFICATE**
> → ACM
>
> **SQL INJECTION**
> → WAF
>
> **DDoS**
> → SHIELD
>
> **THREAT**
> → GUARDDUTY
>
> **CVE**
> → INSPECTOR
>
> **PII**
> → MACIE
>
> **CENTRAL FINDINGS**
> → SECURITY HUB
>
> **API HISTORY**
> → CLOUDTRAIL
>
> **NETWORK FLOW**
> → VPC FLOW LOGS

---

## Master Memory Trick

> [!tip] Secure Architecture Master Memory Trick
> Imagine your AWS environment is:
>
> **A secure office building**
>
> [[IAM]] decides:
>
> **WHO GETS A BADGE**
>
> Security Groups decide:
>
> **WHICH DOORS THEY CAN ENTER**
>
> NACLs guard:
>
> **THE NEIGHBORHOOD GATE**
>
> [[KMS]] protects:
>
> **THE LOCKED DATA VAULT**
>
> [[Secrets Manager]] stores:
>
> **THE PASSWORDS**
>
> [[WAF]] guards:
>
> **THE WEB FRONT DOOR**
>
> [[Shield]] protects against:
>
> **A CROWD TRYING TO OVERWHELM THE BUILDING**
>
> [[GuardDuty]] watches for:
>
> **SUSPICIOUS PEOPLE**
>
> [[Inspector]] finds:
>
> **BROKEN LOCKS**
>
> [[Macie]] finds:
>
> **SENSITIVE DOCUMENTS**
>
> [[Security Hub]] is:
>
> **SECURITY HEADQUARTERS**
>
> [[CloudTrail]] records:
>
> **WHO DID WHAT**

So remember:

> **IDENTITY**
> → IAM
>
> **NETWORK**
> → SG / NACL / FIREWALL
>
> **DATA**
> → KMS / SECRETS
>
> **WEB**
> → WAF / SHIELD
>
> **DETECTION**
> → GUARDDUTY / INSPECTOR / MACIE
>
> **CENTRAL VIEW**
> → SECURITY HUB
>
> **AUDIT**
> → CLOUDTRAIL

And the killer SAA question:

> **"What happens if one security control fails?"**
>
> If the answer is:
>
> **"The resource is exposed"**
>
> then the architecture may need:
>
> **More defense in depth**

---

## Related Notes

- [[Architecture Principles]]
- [[High Availability Architecture]]
- [[Cost-Optimized Architecture]]
- [[IAM]]
- [[KMS]]
- [[Secrets Manager]]
- [[Security Groups]]
- [[NACL]]
- [[VPC Endpoints]]
- [[WAF]]
- [[Shield]]
- [[GuardDuty]]
- [[Inspector]]
- [[Macie]]
- [[Security Hub]]
- [[CloudTrail]]
- [[VPC Flow Logs]]
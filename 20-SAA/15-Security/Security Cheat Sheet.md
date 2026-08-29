## Core Exam Map

> [!tip] Master Shortcut
> **Encryption keys** → [[KMS]]
>
> **Dedicated cryptographic hardware** → [[CloudHSM]]
>
> **Passwords / API keys / credentials** → [[Secrets Manager]]
>
> **Application configuration** → [[Parameter Store]]
>
> **TLS certificates** → [[ACM]]
>
> **Web attack filtering** → [[WAF]]
>
> **DDoS protection** → [[Shield]]
>
> **Threat detection** → [[GuardDuty]]
>
> **Vulnerability scanning** → [[Inspector]]
>
> **Sensitive S3 data discovery** → [[Macie]]
>
> **Central security findings** → [[Security Hub]]
>
> **VPC traffic inspection** → [[20-SAA/15-Security/Network Firewall]]
>
> **Central firewall policy management** → [[Firewall Manager]]

---

# KMS

Think:

**Encryption Key Management**

Use for:

- Customer managed keys
- Key policies
- Encryption at rest
- Envelope encryption
- Key rotation
- SSE-KMS

### Killer Exam Clues

- Encryption key
- Key policy
- Customer-controlled key
- Key rotation
- Data key
- SSE-KMS

### Memory Trick

**KMS = KEY**

---

# CloudHSM

Think:

**Dedicated customer-controlled HSM hardware**

Use when requirements explicitly mention:

- Dedicated HSM
- Single-tenant cryptographic hardware
- PKCS#11
- Specialized cryptography
- Strict compliance

### Killer Shortcut

**Managed AWS key service**
→ KMS

**Dedicated hardware HSM**
→ CloudHSM

### Memory Trick

**CloudHSM = HARDWARE**

---

# Secrets Manager

Think:

**Store + rotate secrets**

Examples:

- Database passwords
- API keys
- Application credentials
- Tokens

### Killer Exam Clue

> **Automatically rotate RDS credentials**
>
> → **Secrets Manager**

### Memory Trick

**Secrets Manager = SECRET + ROTATE**

---

# Parameter Store

Think:

**Application configuration**

Use for:

- Hierarchical parameters
- Environment configuration
- SecureString
- AMI parameters
- Centralized application settings

### Killer Shortcut

**Configuration**
→ Parameter Store

**Secret needing automatic rotation**
→ Secrets Manager

### Memory Trick

**Parameter Store = CONFIG**

---

# ACM

Think:

**SSL/TLS Certificates**

Use for:

- ALB HTTPS
- CloudFront HTTPS
- API Gateway custom domains
- Public certificates
- Private certificates

### Killer Exam Clues

**CloudFront certificate**
→ ACM in `us-east-1`

**Regional service**
→ ACM certificate in same Region

### Memory Trick

**ACM = HTTPS CERTIFICATE**

---

# WAF

Think:

**Layer 7 web request filtering**

Protects against:

- SQL injection
- XSS
- Malicious IPs
- Bad HTTP requests
- Bots
- Excessive request rates

### Killer Exam Clue

> **SQL injection / XSS**
>
> → **WAF**

### Memory Trick

**WAF = BAD WEB REQUEST**

---

# Shield

Think:

**DDoS Protection**

## Shield Standard

- Baseline protection
- Automatically included

## Shield Advanced

- Enhanced DDoS protection
- Specialized support
- DDoS cost protection
- Greater visibility

### Killer Shortcut

**Basic DDoS**
→ Shield Standard

**Mission-critical DDoS**
→ Shield Advanced

### Memory Trick

**Shield = TOO MUCH TRAFFIC**

---

# GuardDuty

Think:

**Threat Detection**

Detects patterns such as:

- Compromised credentials
- Suspicious API activity
- Malicious IP communication
- Suspicious DNS behavior
- Command-and-control activity

### Killer Exam Clue

> **Detect suspicious behavior in AWS**
>
> → **GuardDuty**

### Memory Trick

**GuardDuty = THREAT**

---

# Inspector

Think:

**Vulnerability Management**

Use for:

- EC2 CVEs
- ECR image vulnerabilities
- Lambda vulnerabilities
- Network exposure

### Killer Exam Clue

> **Find vulnerable packages or CVEs**
>
> → **Inspector**

### Memory Trick

**Inspector = WEAKNESS**

---

# Macie

Think:

**Sensitive Data Discovery in S3**

Finds:

- PII
- Credit card numbers
- Credentials
- Sensitive data patterns

### Killer Exam Clue

> **Discover PII stored in S3**
>
> → **Macie**

### Memory Trick

**Macie = SENSITIVE DATA**

---

# Security Hub

Think:

**Central Security Findings**

It aggregates findings from services such as:

- GuardDuty
- Inspector
- Macie
- Other supported sources

It also helps evaluate:

**Security posture**

### Killer Exam Clue

> **Need one place to view security findings from multiple services**
>
> → **Security Hub**

### Memory Trick

**Security Hub = HEADQUARTERS**

---

# Network Firewall

Think:

**Advanced VPC network inspection**

Provides:

- Stateful inspection
- Stateless inspection
- Domain filtering
- Intrusion prevention
- Suricata-compatible rules

### Killer Exam Clue

> **Need centralized stateful inspection of VPC traffic**
>
> → **Network Firewall**

### Memory Trick

**Network Firewall = VPC TRAFFIC**

---

# Firewall Manager

Think:

**Manage security policies across many accounts**

Works especially well with:

**AWS Organizations**

Can centrally manage supported policies for:

- WAF
- Shield Advanced
- Security groups
- Network Firewall
- DNS Firewall

### Killer Exam Clue

> **Apply consistent firewall policies across multiple AWS accounts**
>
> → **Firewall Manager**

### Memory Trick

**Firewall Manager = MANAGE AT SCALE**

---

# Encryption Decision Map

Need:

**Encryption key management**

→ KMS

Need:

**Dedicated HSM**

→ CloudHSM

Need:

**Store password/API key**

→ Secrets Manager

Need:

**Application configuration**

→ Parameter Store

Need:

**HTTPS certificate**

→ ACM

---

# KMS vs CloudHSM

| Requirement | KMS | CloudHSM |
|---|---:|---:|
| Managed Key Service | ✅ | ❌ |
| Dedicated Hardware | ❌ Standard | ✅ |
| Deep AWS Integration | ✅ | More Specialized |
| Customer-Controlled HSM | ❌ | ✅ |
| PKCS#11 | ❌ Primary | ✅ |
| Lower Operational Burden | ✅ | ❌ |

### Killer Shortcut

**Normal AWS encryption**
→ KMS

**Dedicated hardware requirement**
→ CloudHSM

---

# Secrets Manager vs Parameter Store

| Requirement | Secrets Manager | Parameter Store |
|---|---:|---:|
| Password Storage | ✅ | SecureString Possible |
| Automatic Rotation | ✅ | ❌ Native Equivalent |
| API Keys | ✅ | Possible |
| Hierarchical Config | ❌ Primary | ✅ |
| SecureString | ❌ | ✅ |
| Application Config | Possible | ✅ Best Fit |

### Killer Shortcut

**SECRET + ROTATE**
→ Secrets Manager

**CONFIG**
→ Parameter Store

---

# WAF vs Shield

| Requirement | WAF | Shield |
|---|---:|---:|
| SQL Injection | ✅ | ❌ |
| XSS | ✅ | ❌ |
| HTTP Filtering | ✅ | ❌ Primary |
| Bad IP Rules | ✅ | Different Purpose |
| DDoS | Supporting Role | ✅ |
| Volumetric Attack | ❌ Primary | ✅ |

### Memory Trick

**WAF = BAD REQUEST**

**Shield = TOO MUCH TRAFFIC**

---

# GuardDuty vs Inspector vs Macie

| Question | Service |
|---|---|
| Is malicious activity happening? | GuardDuty |
| What software is vulnerable? | Inspector |
| What sensitive data is in S3? | Macie |

### Master Memory Trick

> **GUARDDUTY**
> → THREAT
>
> **INSPECTOR**
> → VULNERABILITY
>
> **MACIE**
> → DATA

---

# Security Hub vs Specialized Services

## GuardDuty

**Detects threats**

## Inspector

**Finds vulnerabilities**

## Macie

**Finds sensitive data**

## Security Hub

**Centralizes the findings**

### Killer Shortcut

**Find the problem**
→ Specialized service

**See everything together**
→ Security Hub

---

# Network Security Layers

## Security Group

Think:

**Resource-level access**

Examples:

- Port 443
- Source security group
- EC2 access

---

## NACL

Think:

**Subnet-level stateless filtering**

Examples:

- Allow/deny CIDR
- Port ranges

---

## WAF

Think:

**HTTP(S) request inspection**

Examples:

- SQL injection
- XSS

---

## Network Firewall

Think:

**Advanced VPC traffic inspection**

Examples:

- Stateful inspection
- Suricata
- Domain filtering

---

## Shield

Think:

**DDoS protection**

### Memory Map

> **SECURITY GROUP**
> → RESOURCE
>
> **NACL**
> → SUBNET
>
> **WAF**
> → WEB
>
> **NETWORK FIREWALL**
> → VPC TRAFFIC
>
> **SHIELD**
> → DDoS

---

# Firewall Manager vs Security Hub

## Firewall Manager

Think:

**Central security policy enforcement**

## Security Hub

Think:

**Central security findings**

### Killer Shortcut

**Push security policy**
→ Firewall Manager

**Collect security findings**
→ Security Hub

---

# Detective vs Preventive Security

## Detective

Think:

**Find something that happened or exists**

Examples:

- GuardDuty
- Inspector
- Macie
- Config
- CloudTrail

---

## Preventive / Protective

Think:

**Stop or restrict activity**

Examples:

- IAM
- Security Groups
- WAF
- Shield
- Network Firewall

### Memory Trick

**Detective = FIND**

**Preventive = STOP**

---

# Security Architecture Scenario 1 — Encrypt S3

Requirement:

Customer wants:

- S3 encryption
- Customer-controlled permissions
- Auditability

Choose:

**SSE-KMS + Customer Managed Key**

---

# Security Architecture Scenario 2 — RDS Password

Requirement:

Securely store and automatically rotate:

**Database credentials**

Choose:

**Secrets Manager**

---

# Security Architecture Scenario 3 — App Configuration

Requirement:

Store:

- Environment
- API URL
- AMI ID

Choose:

**Parameter Store**

---

# Security Architecture Scenario 4 — HTTPS

Requirement:

Public ALB needs:

**TLS certificate**

Choose:

**ACM**

---

# Security Architecture Scenario 5 — SQL Injection

Requirement:

Block:

**SQL injection**

Choose:

**WAF**

---

# Security Architecture Scenario 6 — DDoS

Requirement:

Protect against:

**Large-scale volumetric attack**

Choose:

**Shield**

---

# Security Architecture Scenario 7 — Suspicious Credentials

Requirement:

Detect IAM credentials being used:

**From a suspicious location**

Choose:

**GuardDuty**

---

# Security Architecture Scenario 8 — CVE

Requirement:

Find:

**Known vulnerabilities in EC2 packages**

Choose:

**Inspector**

---

# Security Architecture Scenario 9 — PII

Requirement:

Find:

**Social Security numbers in S3**

Choose:

**Macie**

---

# Security Architecture Scenario 10 — Security Dashboard

Requirement:

Centralize:

- GuardDuty
- Inspector
- Macie

findings.

Choose:

**Security Hub**

---

# Security Architecture Scenario 11 — VPC Inspection

Requirement:

Inspect outbound VPC traffic for:

**Malicious destinations and intrusion signatures**

Choose:

**Network Firewall**

---

# Security Architecture Scenario 12 — 100 Accounts

Requirement:

Apply the same:

**WAF policy**

to web applications across:

100 AWS accounts.

Choose:

**Firewall Manager**

---

# Scenario Recognition

## Encryption Key

→ **KMS**

## Dedicated HSM

→ **CloudHSM**

## Database Password

→ **Secrets Manager**

## App Configuration

→ **Parameter Store**

## HTTPS Certificate

→ **ACM**

## SQL Injection / XSS

→ **WAF**

## DDoS

→ **Shield**

## Suspicious AWS Activity

→ **GuardDuty**

## CVE

→ **Inspector**

## PII in S3

→ **Macie**

## Central Security Findings

→ **Security Hub**

## Advanced VPC Inspection

→ **Network Firewall**

## Multi-Account Firewall Policies

→ **Firewall Manager**

---

# Common Exam Traps

## Trap 1 — KMS Stores Passwords

❌

Think:

**Secrets Manager**

---

## Trap 2 — Secrets Manager Manages Encryption Keys

❌

Think:

**KMS**

---

## Trap 3 — Parameter Store Automatically Rotates RDS Passwords

❌

Think:

**Secrets Manager**

---

## Trap 4 — ACM Encrypts Stored Data

❌

Think:

**KMS**

---

## Trap 5 — WAF Is the Main DDoS Protection Service

❌

Think:

**Shield**

---

## Trap 6 — GuardDuty Blocks Traffic

❌

GuardDuty primarily:

**Detects**

---

## Trap 7 — Inspector Detects Compromised Credentials

❌

Think:

**GuardDuty**

---

## Trap 8 — Macie Scans EC2 for CVEs

❌

Think:

**Inspector**

---

## Trap 9 — Security Hub Discovers PII

❌

Think:

**Macie**

Security Hub:

**Aggregates findings**

---

## Trap 10 — Network Firewall and WAF Are the Same

❌

WAF:

**HTTP**

Network Firewall:

**VPC traffic**

---

## Trap 11 — Firewall Manager Performs All Packet Inspection

❌

It:

**Manages policies**

Other services perform:

**The actual protection/inspection**

---

# Quick Cheat Sheet

| Exam Clue | Answer |
|---|---|
| Encryption Keys | KMS |
| Dedicated HSM | CloudHSM |
| Password / API Key | Secrets Manager |
| Application Config | Parameter Store |
| TLS Certificate | ACM |
| SQL Injection / XSS | WAF |
| DDoS | Shield |
| Threat Detection | GuardDuty |
| CVE / Vulnerability | Inspector |
| PII in S3 | Macie |
| Central Security Findings | Security Hub |
| VPC Network Inspection | Network Firewall |
| Multi-Account Firewall Policy | Firewall Manager |

---

# One-Word Memory Map

| Service | Remember |
|---|---|
| KMS | KEY |
| CloudHSM | HARDWARE |
| Secrets Manager | SECRET |
| Parameter Store | CONFIG |
| ACM | CERTIFICATE |
| WAF | WEB |
| Shield | DDoS |
| GuardDuty | THREAT |
| Inspector | VULNERABILITY |
| Macie | DATA |
| Security Hub | CENTRALIZE |
| Network Firewall | INSPECT |
| Firewall Manager | MANAGE |

---

# Final Exam Rapid-Fire

> **ENCRYPTION KEY**
> → KMS
>
> **DEDICATED HSM**
> → CLOUDHSM
>
> **DATABASE PASSWORD**
> → SECRETS MANAGER
>
> **AUTO ROTATE SECRET**
> → SECRETS MANAGER
>
> **APP CONFIG**
> → PARAMETER STORE
>
> **TLS CERTIFICATE**
> → ACM
>
> **SQL INJECTION**
> → WAF
>
> **XSS**
> → WAF
>
> **DDoS**
> → SHIELD
>
> **SUSPICIOUS AWS ACTIVITY**
> → GUARDDUTY
>
> **CVE**
> → INSPECTOR
>
> **PII IN S3**
> → MACIE
>
> **CENTRAL FINDINGS**
> → SECURITY HUB
>
> **STATEFUL VPC INSPECTION**
> → NETWORK FIREWALL
>
> **MULTI-ACCOUNT SECURITY POLICY**
> → FIREWALL MANAGER

---

## Master Memory Trick

> [!tip] Security Master Memory Trick
> Imagine AWS security as:
>
> **A giant secure building**
>
> The encryption-key vault is:
>
> **KMS**
>
> The dedicated hardware vault is:
>
> **CLOUDHSM**
>
> The password safe is:
>
> **SECRETS MANAGER**
>
> The configuration filing cabinet is:
>
> **PARAMETER STORE**
>
> The HTTPS certificate office is:
>
> **ACM**
>
> The web-door security guard is:
>
> **WAF**
>
> The giant anti-DDoS wall is:
>
> **SHIELD**
>
> The suspicious-activity detective is:
>
> **GUARDDUTY**
>
> The vulnerability inspector is:
>
> **INSPECTOR**
>
> The sensitive-data scanner is:
>
> **MACIE**
>
> Security headquarters is:
>
> **SECURITY HUB**
>
> The highway inspection station is:
>
> **NETWORK FIREWALL**
>
> And the person making sure every building follows the same firewall rules is:
>
> **FIREWALL MANAGER**

So memorize:

> **KMS**
> → KEY
>
> **CLOUDHSM**
> → HARDWARE
>
> **SECRETS MANAGER**
> → SECRET
>
> **PARAMETER STORE**
> → CONFIG
>
> **ACM**
> → CERTIFICATE
>
> **WAF**
> → WEB ATTACK
>
> **SHIELD**
> → DDoS
>
> **GUARDDUTY**
> → THREAT
>
> **INSPECTOR**
> → VULNERABILITY
>
> **MACIE**
> → SENSITIVE DATA
>
> **SECURITY HUB**
> → CENTRALIZE
>
> **NETWORK FIREWALL**
> → INSPECT NETWORK
>
> **FIREWALL MANAGER**
> → MANAGE POLICIES

And the master SAA shortcut:

> **WHAT ARE YOU TRYING TO PROTECT OR FIND?**
>
> Key?
> → KMS
>
> Secret?
> → Secrets Manager
>
> Web attack?
> → WAF
>
> DDoS?
> → Shield
>
> Threat?
> → GuardDuty
>
> Vulnerability?
> → Inspector
>
> Sensitive data?
> → Macie
>
> All findings?
> → Security Hub
>
> VPC traffic?
> → Network Firewall
>
> Policies across accounts?
> → Firewall Manager

---

## Related Notes

- [[KMS]]
- [[CloudHSM]]
- [[Secrets Manager]]
- [[Parameter Store]]
- [[ACM]]
- [[WAF]]
- [[Shield]]
- [[GuardDuty]]
- [[Inspector]]
- [[Macie]]
- [[Security Hub]]
- [[20-SAA/15-Security/Network Firewall]]
- [[Firewall Manager]]
- [[CloudTrail]]
- [[Config]]
- [[IAM]]
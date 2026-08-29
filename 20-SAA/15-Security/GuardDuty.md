## What Problem Does It Solve?

[[GuardDuty]] is AWS's:

**Managed threat detection service**

It continuously analyzes AWS activity to detect:

- Suspicious behavior
- Compromised credentials
- Unusual API activity
- Malicious network activity
- Potentially compromised EC2 instances
- Potentially compromised containers
- Suspicious access patterns

Architecture:

AWS Activity  
↓  
GuardDuty  
↓  
Threat Analysis  
↓  
Security Finding

> [!tip] Memory Trick
> **GuardDuty = Detect Bad Behavior**

---

## Core Concept

GuardDuty does not primarily:

**Block traffic**

Instead, it:

**Detects suspicious activity and generates findings**

### Killer Exam Clue

> **Need intelligent threat detection across AWS accounts and workloads**
>
> → **GuardDuty**

---

# Data Sources

GuardDuty analyzes multiple AWS data sources.

Important examples include:

- [[CloudTrail]] activity
- VPC Flow Logs
- DNS activity
- EKS audit activity
- Supported workload/runtime telemetry

### Memory Trick

**GuardDuty Watches the Evidence**

---

# CloudTrail Analysis

GuardDuty analyzes AWS API activity to identify:

**Suspicious account behavior**

Examples:

- Unusual API calls
- Credential misuse
- Activity from unexpected locations
- Reconnaissance behavior

### Killer Exam Clue

> **Detect suspicious IAM or API activity**
>
> → **GuardDuty**

---

# VPC Flow Log Analysis

GuardDuty can analyze:

**Network traffic metadata**

to identify patterns such as:

- Connections to known malicious IPs
- Reconnaissance
- Unusual outbound traffic
- Potential command-and-control communication

### Memory Trick

**Flow Logs Tell GuardDuty Who Talked to Whom**

---

# DNS Analysis

GuardDuty can inspect:

**DNS query activity**

to detect suspicious domains.

Example:

Compromised Instance  
↓  
DNS Query  
↓  
Known Malicious Domain  
↓  
GuardDuty Finding

### Killer Exam Clue

> **EC2 instance is communicating with a suspicious domain**
>
> → **GuardDuty**

---

# Threat Intelligence

GuardDuty uses:

**AWS and third-party threat intelligence**

to identify known malicious:

- IP addresses
- Domains
- Attack infrastructure

This helps detect:

**Known threats automatically**

---

# Machine Learning

GuardDuty also uses:

**Behavioral and machine-learning techniques**

to identify:

**Unusual activity**

even if the source is not already on:

**A known threat list**

### Exam Principle

> **GuardDuty combines threat intelligence with anomaly detection**

---

# GuardDuty Findings

When GuardDuty detects suspicious activity, it creates a:

**Finding**

A finding contains information such as:

- Resource involved
- Threat type
- Severity
- Activity details
- Recommended context for investigation

### Memory Trick

**GuardDuty Detects → Finding Appears**

---

# Finding Severity

GuardDuty findings include:

**Severity levels**

to help prioritize:

**Security response**

For SAA, focus on the principle:

> **Higher-severity findings should receive faster investigation**

---

# GuardDuty Is Detective

GuardDuty is primarily:

**Detective**

It identifies:

**Potential threats**

It does not automatically behave like:

- Security Group
- WAF
- Network Firewall

### Killer Exam Trap

> **GuardDuty detects**
>
> It does not inherently:
>
> **Block**

---

# Automated Remediation

You can build automatic response workflows around:

**GuardDuty findings**

Architecture:

GuardDuty Finding  
↓  
[[EventBridge]]  
↓  
[[Lambda]] / [[Systems Manager]]  
↓  
Remediation

### Killer Exam Clue

> **Automatically isolate an EC2 instance after a GuardDuty finding**
>
> → **GuardDuty + EventBridge + Automation**

---

# Example — Compromised EC2

GuardDuty detects:

EC2 communicating with malicious IP  
↓  
Finding  
↓  
EventBridge  
↓  
Lambda  
↓  
Modify Security Group / Isolate Instance

### Memory Trick

**GuardDuty Detects**

**EventBridge Routes**

**Lambda Fixes**

---

# GuardDuty + SNS

A simpler notification architecture:

GuardDuty  
↓  
EventBridge  
↓  
[[SNS]]  
↓  
Security Team

### Killer Exam Clue

> **Notify security team when GuardDuty generates a high-severity finding**
>
> → **GuardDuty + EventBridge + SNS**

---

# Multi-Account GuardDuty

GuardDuty can be centrally managed across:

**Multiple AWS accounts**

This is useful in:

**AWS Organizations**

Architecture:

AWS Organizations  
↓  
Member Accounts  
↓  
GuardDuty  
↓  
Delegated Security Account

### Killer Exam Clue

> **Centrally manage threat detection across many AWS accounts**
>
> → **GuardDuty multi-account management**

---

# Delegated Administrator

In an Organizations environment, a:

**Delegated Administrator**

can centrally manage GuardDuty for:

**Member accounts**

This supports:

**Centralized security operations**

---

# GuardDuty + Organizations

A scalable architecture:

Management Account  
↓  
Delegated Security Account  
↓  
GuardDuty  
↓  
Member Accounts

This helps enforce:

**Consistent threat detection**

---

# S3 Protection

GuardDuty can provide protection for:

**S3-related activity**

to identify suspicious access patterns.

Examples:

- Suspicious object access
- Unusual bucket activity
- Potential credential compromise involving S3

### Killer Exam Clue

> **Need intelligent threat detection for suspicious S3 access**
>
> → **GuardDuty S3 Protection**

---

# EKS Protection

GuardDuty can analyze supported:

**EKS activity**

for suspicious Kubernetes behavior.

This can include analysis related to:

**Kubernetes audit activity**

### Killer Exam Clue

> **Need managed threat detection for EKS workloads**
>
> → **GuardDuty EKS Protection**

---

# Runtime Monitoring

GuardDuty can provide supported:

**Runtime monitoring**

for workloads such as:

- EC2
- EKS
- ECS/Fargate

depending on supported configurations.

This helps detect suspicious activity:

**Inside running workloads**

---

# Malware Protection

GuardDuty can provide supported:

**Malware protection capabilities**

for certain workloads.

This helps identify:

**Potentially malicious files or compromised resources**

### Exam Principle

> **GuardDuty can extend beyond account/network signals into workload threat detection**

---

# GuardDuty vs Inspector

This is a very important distinction.

## GuardDuty

Think:

**Is someone attacking or compromising my environment?**

Focus:

- Threat detection
- Suspicious behavior
- Credential compromise
- Malicious activity

## [[06-Security/Inspector]]

Think:

**Does my workload have vulnerabilities?**

Focus:

- Software vulnerabilities
- CVEs
- Exposure analysis
- Package vulnerabilities

### Memory Trick

**GuardDuty = ATTACK DETECTION**

**Inspector = VULNERABILITY DETECTION**

---

# GuardDuty vs WAF

## [[WAF]]

Think:

**Block malicious web requests**

## GuardDuty

Think:

**Detect suspicious AWS activity**

### Killer Shortcut

SQL injection request  
→ WAF

Compromised IAM credentials  
→ GuardDuty

---

# GuardDuty vs Shield

## [[Shield]]

Think:

**DDoS protection**

## GuardDuty

Think:

**Threat detection**

### Example

Massive DDoS  
→ Shield

EC2 contacts malware command server  
→ GuardDuty

---

# GuardDuty vs Macie

## GuardDuty

Think:

**Threats**

## [[06-Security/Macie]]

Think:

**Sensitive data in S3**

### Killer Shortcut

Suspicious activity  
→ GuardDuty

Find PII in S3  
→ Macie

---

# GuardDuty vs Security Hub

## GuardDuty

Generates:

**Security findings**

## [[06-Security/Security Hub]]

Aggregates and manages:

**Security findings from multiple services**

### Memory Trick

**GuardDuty = Detect**

**Security Hub = Centralize**

---

# GuardDuty vs CloudTrail

## [[CloudTrail]]

Records:

**AWS API history**

## GuardDuty

Analyzes activity to identify:

**Threats**

CloudTrail may tell you:

> User called API from unusual IP.

GuardDuty may tell you:

> This behavior looks suspicious.

### Memory Trick

**CloudTrail = Evidence**

**GuardDuty = Detective**

---

# GuardDuty vs Config

## [[Config]]

Think:

**Configuration compliance**

## GuardDuty

Think:

**Threat detection**

Example:

Security group allows `0.0.0.0/0`

→ Config can identify configuration issue

EC2 begins communicating with known malicious host

→ GuardDuty

---

# GuardDuty vs Security Groups

Security Groups are:

**Preventive network controls**

GuardDuty is:

**Detective security**

### Memory Trick

**Security Group = Prevent**

**GuardDuty = Detect**

---

# GuardDuty vs Network Firewall

Network Firewall:

**Inspects and blocks network traffic**

GuardDuty:

**Analyzes activity and raises findings**

### Killer Shortcut

Need to block VPC traffic  
→ Network Firewall

Need to detect suspicious activity  
→ GuardDuty

---

# Architecture Thinking

## Scenario 1 — Compromised IAM Credentials

AWS account begins making:

**Unusual API calls from an unexpected location**

Choose:

**GuardDuty**

---

## Scenario 2 — EC2 Contacts Malicious IP

Instance begins outbound communication to:

**Known command-and-control infrastructure**

Choose:

**GuardDuty**

---

## Scenario 3 — SQL Injection

Public application receives:

**SQL injection requests**

Choose:

**WAF**

not GuardDuty as primary defense.

---

## Scenario 4 — Vulnerable Package

EC2 application contains:

**Known CVE**

Choose:

**Inspector**

---

## Scenario 5 — Sensitive S3 Data

Need to identify:

**PII stored in S3**

Choose:

**Macie**

---

## Scenario 6 — Central Security Findings

Need one place to collect:

- GuardDuty
- Inspector
- Macie
- Other security findings

Choose:

**Security Hub**

---

## Scenario 7 — Automated Isolation

GuardDuty identifies:

**Potentially compromised EC2**

Need automatic response.

Choose:

GuardDuty  
↓  
EventBridge  
↓  
Lambda / Systems Manager  
↓  
Isolation

---

## Scenario 8 — DDoS

Public endpoint experiences:

**Distributed denial-of-service attack**

Choose:

**Shield**

---

# Scenario Recognition

Immediately think:

**GuardDuty**

when you see:

- Threat detection
- Compromised credentials
- Suspicious API activity
- Malicious IP
- Command-and-control
- Unusual DNS activity
- Suspicious network behavior
- Security finding
- Threat intelligence

---

## Think Inspector When You See

- Vulnerability
- CVE
- Software package weakness
- Workload vulnerability scanning

---

## Think Macie When You See

- PII
- Sensitive data
- S3 data discovery

---

## Think Security Hub When You See

- Central security dashboard
- Aggregate findings
- Security posture

---

# Exam Traps

## Trap 1 — GuardDuty Blocks Malicious Traffic

❌

GuardDuty primarily:

**Detects**

Use other controls to:

**Block or remediate**

---

## Trap 2 — GuardDuty Scans EC2 Packages for CVEs

❌

Think:

**Inspector**

---

## Trap 3 — GuardDuty Finds PII in S3 Objects

❌

Think:

**Macie**

---

## Trap 4 — GuardDuty Replaces CloudTrail

❌

CloudTrail:

**Records API events**

GuardDuty:

**Analyzes activity for threats**

---

## Trap 5 — GuardDuty Is a DDoS Protection Service

❌

Think:

**Shield**

---

## Trap 6 — GuardDuty Is a Web Application Firewall

❌

Think:

**WAF**

---

# Quick Cheat Sheet

| Exam Clue | Answer |
|---|---|
| Managed Threat Detection | GuardDuty |
| Suspicious IAM Activity | GuardDuty |
| Compromised Credentials | GuardDuty |
| Malicious IP Communication | GuardDuty |
| Suspicious DNS Activity | GuardDuty |
| Security Finding | GuardDuty |
| Automatic Response | EventBridge + Lambda/Systems Manager |
| Vulnerability Scanning | Inspector |
| Sensitive S3 Data | Macie |
| Central Security Findings | Security Hub |
| SQL Injection | WAF |
| DDoS | Shield |
| API Audit History | CloudTrail |

---

# Security Decision Map

Need:

**Detect suspicious AWS activity**

→ GuardDuty

Need:

**Find software vulnerabilities**

→ Inspector

Need:

**Discover sensitive S3 data**

→ Macie

Need:

**Aggregate security findings**

→ Security Hub

Need:

**Block malicious HTTP requests**

→ WAF

Need:

**DDoS protection**

→ Shield

Need:

**Audit API calls**

→ CloudTrail

---

# Detective vs Preventive

## Detective

- GuardDuty
- CloudTrail
- Config
- Inspector
- Macie

## Preventive / Protective

- IAM
- Security Groups
- WAF
- Shield
- Network Firewall

### Memory Trick

**GuardDuty = Alarm System**

Not:

**The Locked Door**

---

# Final Exam Rapid-Fire

> **THREAT DETECTION**
> → GUARDDUTY
>
> **COMPROMISED IAM**
> → GUARDDUTY
>
> **MALICIOUS IP**
> → GUARDDUTY
>
> **SUSPICIOUS DNS**
> → GUARDDUTY
>
> **SECURITY FINDING**
> → GUARDDUTY
>
> **AUTO RESPONSE**
> → EVENTBRIDGE + LAMBDA
>
> **VULNERABILITY**
> → INSPECTOR
>
> **PII IN S3**
> → MACIE
>
> **CENTRAL FINDINGS**
> → SECURITY HUB
>
> **SQL INJECTION**
> → WAF
>
> **DDoS**
> → SHIELD
>
> **API HISTORY**
> → CLOUDTRAIL

---

## Master Memory Trick

> [!tip] GuardDuty Master Memory Trick
> Imagine your AWS environment is:
>
> **A neighborhood at night**
>
> CloudTrail is:
>
> **The security camera**
>
> It records what happened.
>
> GuardDuty is:
>
> **THE DETECTIVE WATCHING THE CAMERAS**
>
> It notices:
>
> **"That login looks strange."**
>
> **"That EC2 instance is calling a known malicious server."**
>
> **"Those DNS requests look suspicious."**
>
> Then it creates:
>
> **A FINDING**
>
> But the detective does not personally:
>
> **Lock every door**
>
> To respond automatically:
>
> **EventBridge + Lambda / Systems Manager**

So remember:

> **CLOUDTRAIL**
> → RECORD
>
> **GUARDDUTY**
> → DETECT THREAT
>
> **INSPECTOR**
> → FIND VULNERABILITY
>
> **MACIE**
> → FIND SENSITIVE DATA
>
> **SECURITY HUB**
> → CENTRALIZE FINDINGS
>
> **WAF**
> → BLOCK WEB ATTACK
>
> **SHIELD**
> → STOP DDoS

And the killer SAA question:

> **"Does the requirement involve continuously detecting suspicious behavior, credential compromise, or malicious activity in AWS?"**
>
> YES
>
> → **GuardDuty**

---

## Related Notes

- [[CloudTrail]]
- [[WAF]]
- [[Shield]]
- [[06-Security/Inspector]]
- [[06-Security/Macie]]
- [[06-Security/Security Hub]]
- [[EventBridge]]
- [[Lambda]]
- [[Systems Manager]]
- [[CloudWatch]]
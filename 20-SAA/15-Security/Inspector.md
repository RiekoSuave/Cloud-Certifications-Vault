## What Problem Does It Solve?

[[Inspector]] is AWS's:

**Automated vulnerability management service**

It continuously scans supported workloads for:

- Software vulnerabilities
- Known CVEs
- Unintended network exposure
- Vulnerable software packages

Commonly protected workloads include:

- [[EC2]]
- Container images in ECR
- [[Lambda]] functions

Architecture:

AWS Workload  
↓  
Inspector  
↓  
Vulnerability Assessment  
↓  
Security Finding

> [!tip] Memory Trick
> **Inspector = Inspect Workloads for Vulnerabilities**

---

## Core Concept

Inspector answers:

> **"Does my workload contain known security vulnerabilities?"**

It automatically discovers supported workloads and evaluates them for:

**Security weaknesses**

### Killer Exam Clue

> **Continuously scan EC2 instances, container images, or Lambda functions for known software vulnerabilities**
>
> → **Inspector**

---

# Continuous Vulnerability Management

Inspector provides:

**Continuous vulnerability scanning**

Instead of performing only:

**One-time assessments**

it continuously evaluates supported resources as:

- New vulnerabilities are discovered
- Software changes
- Packages are updated
- Resources are created

### Memory Trick

**Inspector Keeps Rechecking**

---

# Common Vulnerabilities and Exposures

A:

**CVE — Common Vulnerabilities and Exposures**

identifies:

**Publicly known security vulnerabilities**

Example:

Application Package  
↓  
Known CVE  
↓  
Inspector Detects  
↓  
Finding

### Killer Exam Clue

> **Find EC2 packages affected by known CVEs**
>
> → **Inspector**

---

# EC2 Scanning

Inspector can scan:

**EC2 instances**

for software vulnerabilities.

It evaluates installed software packages against:

**Known vulnerability information**

### Example

EC2  
↓  
Installed Package  
↓  
Known CVE  
↓  
Inspector Finding

---

# EC2 Requirements

Inspector integrates with:

**Systems Manager**

for supported EC2 scanning workflows.

This means EC2 instances generally need appropriate:

**Systems Manager connectivity and configuration**

### SAA Principle

> **Inspector EC2 vulnerability scanning integrates with Systems Manager**

---

# Agentless Scanning

Inspector can also support:

**Agentless scanning**

for eligible EC2 environments.

This can analyze:

**EBS snapshots**

without requiring the workload to be scanned through a running agent.

### Exam Principle

> **Inspector can provide vulnerability visibility without always requiring direct agent-based scanning of the running instance**

---

# ECR Container Image Scanning

Inspector integrates with:

**Amazon ECR**

to scan container images for:

**Software vulnerabilities**

Architecture:

Container Image  
↓  
ECR  
↓  
Inspector  
↓  
CVE Finding

### Killer Exam Clue

> **Scan container images for known software vulnerabilities**
>
> → **Inspector + ECR**

---

# Container Vulnerability Example

Developer builds:

Container Image  
↓  
Pushes to ECR  
↓  
Inspector Scans Packages  
↓  
Detects Vulnerable Library  
↓  
Finding

### Memory Trick

**ECR Image + CVE = Inspector**

---

# Lambda Scanning

Inspector can scan:

[[Lambda]]

for supported:

**Software vulnerabilities**

This includes vulnerabilities found in:

**Function dependencies and packages**

### Killer Exam Clue

> **Continuously identify vulnerable packages in Lambda functions**
>
> → **Inspector**

---

# Lambda Code Scanning

Inspector can also provide supported:

**Code vulnerability scanning**

for Lambda functions.

This can help identify certain:

**Application-code security weaknesses**

### Exam Principle

> **Inspector extends beyond traditional EC2 vulnerability scanning**

---

# Network Reachability

Inspector can evaluate:

**Network exposure**

to help identify workloads that may be:

**Unintentionally reachable**

Example:

EC2  
↓  
Security Configuration  
↓  
Unexpected Internet Reachability  
↓  
Inspector Finding

### Killer Exam Clue

> **Identify EC2 instances with unintended network exposure**
>
> → **Inspector**

---

# Inspector Findings

When Inspector identifies a vulnerability, it generates:

**A finding**

A finding can include:

- Vulnerability
- Affected resource
- Severity
- CVE information
- Remediation context
- Network exposure

### Memory Trick

**Inspector Scans → Finding Appears**

---

# Risk Score

Inspector helps prioritize findings using:

**Risk information**

The risk of a vulnerability can depend on factors such as:

- CVE severity
- Exploitability
- Network exposure
- Resource context

### SAA Principle

> **Not every vulnerability presents the same practical risk**

---

# Prioritization

Suppose two EC2 instances contain:

**The same CVE**

Instance A:

Private subnet  
No Internet exposure

Instance B:

Publicly reachable

Inspector can provide context that helps prioritize:

**Instance B**

### Killer Exam Concept

> **Combine vulnerability severity with resource exposure when prioritizing remediation**

---

# Automated Discovery

Inspector can automatically discover supported:

**AWS workloads**

after being enabled.

This reduces the need to:

**Manually register every individual resource**

### Memory Trick

**Enable Inspector → Discover → Scan**

---

# Inspector + EventBridge

Inspector findings can trigger:

[[EventBridge]]

rules.

Architecture:

Inspector Finding  
↓  
EventBridge  
↓  
Lambda / SNS / Systems Manager  
↓  
Response

### Killer Exam Clue

> **Automatically respond when Inspector finds a critical vulnerability**
>
> → **Inspector + EventBridge**

---

# Inspector + SNS

For notification:

Inspector  
↓  
EventBridge  
↓  
[[SNS]]  
↓  
Security Team

Use this when:

**Administrators need alerts for important vulnerabilities**

---

# Automated Remediation

A remediation workflow might be:

Inspector  
↓  
Critical Finding  
↓  
EventBridge  
↓  
Systems Manager Automation  
↓  
Patch / Isolate / Investigate

### Memory Trick

**Inspector Finds**

**EventBridge Routes**

**Automation Responds**

---

# Inspector + Security Hub

Inspector findings can integrate with:

[[06-Security/Security Hub]]

Architecture:

Inspector  
↓  
Security Hub  
↓  
Central Security View

### Killer Exam Clue

> **Centrally aggregate Inspector findings with other AWS security findings**
>
> → **Security Hub**

---

# Inspector + Organizations

Inspector can support:

**Multi-account environments**

using:

**AWS Organizations**

This allows security teams to manage vulnerability scanning across:

**Many AWS accounts**

---

# Delegated Administrator

Organizations can designate:

**A delegated administrator**

for centralized Inspector management.

Architecture:

AWS Organizations  
↓  
Security Account  
↓  
Inspector  
↓  
Member Accounts

### Killer Exam Clue

> **Centrally manage vulnerability scanning across an AWS Organization**
>
> → **Inspector delegated administrator**

---

# Inspector vs GuardDuty

This is the most important comparison.

## Inspector

Think:

**What vulnerabilities exist?**

Examples:

- CVE
- Vulnerable package
- Container vulnerability
- Lambda dependency vulnerability
- Network exposure

## [[GuardDuty]]

Think:

**Is suspicious or malicious activity occurring?**

Examples:

- Compromised credentials
- Malicious IP
- Command-and-control
- Suspicious API calls

### Memory Trick

**Inspector = WEAKNESS**

**GuardDuty = THREAT**

---

# Vulnerability vs Threat

A:

**Vulnerability**

is a weakness that:

**Could be exploited**

A:

**Threat**

is malicious activity that:

**May be exploiting or targeting your environment**

Example:

Outdated package with CVE  
→ Inspector

EC2 contacts malware server  
→ GuardDuty

---

# Inspector vs WAF

## [[WAF]]

Protects applications from:

**Malicious HTTP requests**

## Inspector

Finds:

**Vulnerabilities inside workloads**

### Killer Shortcut

SQL injection request  
→ WAF

Vulnerable web-server package  
→ Inspector

---

# Inspector vs Shield

## [[Shield]]

Protects against:

**DDoS attacks**

## Inspector

Finds:

**Software vulnerabilities**

### Killer Shortcut

DDoS  
→ Shield

CVE  
→ Inspector

---

# Inspector vs Macie

## Inspector

Think:

**Vulnerable workload**

## [[06-Security/Macie]]

Think:

**Sensitive data in S3**

### Memory Trick

**Inspector = Software**

**Macie = Data**

---

# Inspector vs Security Hub

## Inspector

Generates:

**Vulnerability findings**

## [[06-Security/Security Hub]]

Aggregates:

**Security findings**

from multiple security services.

### Memory Trick

**Inspector = Find**

**Security Hub = Collect**

---

# Inspector vs Systems Manager Patch Manager

This distinction matters.

## Inspector

Identifies:

**Vulnerabilities**

## Systems Manager Patch Manager

Helps:

**Patch managed nodes**

### Killer Shortcut

**Find missing security fixes**
→ Inspector

**Install patches**
→ Patch Manager

---

# Inspector vs Config

## [[Config]]

Checks:

**Resource configuration and compliance**

## Inspector

Checks:

**Workload vulnerabilities**

Example:

S3 bucket configuration violates policy  
→ Config

EC2 package has CVE  
→ Inspector

---

# Inspector vs Trusted Advisor

Trusted Advisor can identify:

**AWS best-practice recommendations**

Inspector provides:

**Dedicated vulnerability management**

### Exam Principle

> **Known software vulnerability/CVE = Inspector**

---

# Architecture Thinking

## Scenario 1 — EC2 CVEs

Security team needs to continuously identify:

**Known vulnerabilities in EC2 software packages**

Choose:

**Inspector**

---

## Scenario 2 — Container Images

Company stores Docker images in:

**ECR**

Need vulnerability scanning.

Choose:

**Inspector**

---

## Scenario 3 — Lambda Dependencies

Security team needs to detect:

**Vulnerable Lambda packages**

Choose:

**Inspector**

---

## Scenario 4 — Compromised Credentials

IAM credentials are being used:

**From a suspicious location**

Choose:

**GuardDuty**

not Inspector.

---

## Scenario 5 — SQL Injection Attack

Public application receives:

**SQL injection requests**

Choose:

**WAF**

---

## Scenario 6 — Sensitive S3 Data

Need to discover:

**PII inside S3**

Choose:

**Macie**

---

## Scenario 7 — Vulnerability Dashboard

Need centralized findings from:

- Inspector
- GuardDuty
- Macie

Choose:

**Security Hub**

---

## Scenario 8 — Critical CVE Response

Inspector finds:

**Critical vulnerability**

Need automatic notification.

Choose:

Inspector  
↓  
EventBridge  
↓  
SNS

---

## Scenario 9 — Patch Vulnerable Servers

Inspector identifies:

**Missing security patches**

Need to deploy fixes.

Choose:

Inspector  
↓  
Systems Manager Patch Manager

---

# Scenario Recognition

Immediately think:

**Inspector**

when you see:

- CVE
- Vulnerability scanning
- Vulnerable software package
- EC2 vulnerability
- ECR image vulnerability
- Lambda vulnerability
- Network exposure
- Continuous vulnerability management

---

## Think GuardDuty When You See

- Suspicious activity
- Compromised credentials
- Malicious IP
- Command-and-control

---

## Think Macie When You See

- PII
- Sensitive data
- S3 discovery

---

## Think Patch Manager When You See

- Install patches
- Patch EC2
- Patch compliance

---

# Exam Traps

## Trap 1 — Inspector Detects Compromised IAM Credentials

❌

Think:

**GuardDuty**

---

## Trap 2 — Inspector Blocks SQL Injection

❌

Think:

**WAF**

---

## Trap 3 — Inspector Discovers PII in S3

❌

Think:

**Macie**

---

## Trap 4 — Inspector Is a DDoS Protection Service

❌

Think:

**Shield**

---

## Trap 5 — Inspector Automatically Patches Every Vulnerability

❌

Inspector:

**Identifies vulnerabilities**

Use remediation tools such as:

**Systems Manager**

to apply fixes.

---

## Trap 6 — Inspector Only Scans EC2

❌

Remember:

- EC2
- ECR container images
- Lambda

---

## Trap 7 — Security Hub Performs the Vulnerability Scan

❌

Inspector:

**Scans**

Security Hub:

**Aggregates findings**

---

# Quick Cheat Sheet

| Exam Clue | Answer |
|---|---|
| Vulnerability Management | Inspector |
| CVE | Inspector |
| EC2 Vulnerability | Inspector |
| ECR Image Vulnerability | Inspector |
| Lambda Vulnerability | Inspector |
| Network Exposure | Inspector |
| Suspicious AWS Activity | GuardDuty |
| Sensitive S3 Data | Macie |
| SQL Injection | WAF |
| DDoS | Shield |
| Central Security Findings | Security Hub |
| Install Patches | Systems Manager Patch Manager |

---

# Security Decision Map

Need:

**Find software vulnerabilities**

→ Inspector

Need:

**Detect active threats**

→ GuardDuty

Need:

**Discover sensitive S3 data**

→ Macie

Need:

**Block malicious web requests**

→ WAF

Need:

**DDoS protection**

→ Shield

Need:

**Aggregate security findings**

→ Security Hub

Need:

**Apply patches**

→ Systems Manager Patch Manager

---

# Inspector vs GuardDuty

| Requirement | Inspector | GuardDuty |
|---|---:|---:|
| CVE Detection | ✅ | ❌ |
| Package Vulnerability | ✅ | ❌ |
| ECR Image Scanning | ✅ | ❌ Primary |
| Lambda Vulnerability | ✅ | ❌ Primary |
| Network Exposure | ✅ | Different Purpose |
| Suspicious API Activity | ❌ | ✅ |
| Compromised Credentials | ❌ | ✅ |
| Malicious IP Communication | ❌ | ✅ |

---

# Final Exam Rapid-Fire

> **CVE**
> → INSPECTOR
>
> **EC2 VULNERABILITY**
> → INSPECTOR
>
> **ECR IMAGE VULNERABILITY**
> → INSPECTOR
>
> **LAMBDA VULNERABILITY**
> → INSPECTOR
>
> **NETWORK EXPOSURE**
> → INSPECTOR
>
> **ACTIVE THREAT**
> → GUARDDUTY
>
> **COMPROMISED CREDENTIAL**
> → GUARDDUTY
>
> **PII IN S3**
> → MACIE
>
> **SQL INJECTION**
> → WAF
>
> **DDoS**
> → SHIELD
>
> **CENTRAL FINDINGS**
> → SECURITY HUB
>
> **INSTALL PATCH**
> → PATCH MANAGER

---

## Master Memory Trick

> [!tip] Inspector Master Memory Trick
> Imagine your EC2 instance is:
>
> **A house**
>
> Inspector walks around with:
>
> **A CLIPBOARD**
>
> It checks:
>
> **"Is that window broken?"**
>
> → Vulnerability
>
> **"Is that lock outdated?"**
>
> → CVE
>
> **"Is that back door exposed to the street?"**
>
> → Network Exposure
>
> Inspector reports:
>
> **THE WEAKNESSES**
>
> Then [[GuardDuty]] comes running over and says:
>
> **"Someone suspicious is actually trying the door!"**
>
> That's the difference:
>
> **Inspector finds the weakness**
>
> **GuardDuty detects the threat**

So remember:

> **INSPECTOR**
> → VULNERABILITY
>
> **CVE**
> → INSPECTOR
>
> **EC2 / ECR / LAMBDA**
> → INSPECTOR
>
> **GUARDDUTY**
> → THREAT
>
> **MACIE**
> → SENSITIVE DATA
>
> **SECURITY HUB**
> → CENTRAL FINDINGS
>
> **PATCH MANAGER**
> → FIX/PATCH

And the killer SAA question:

> **"Does the requirement involve continuously identifying known software vulnerabilities or CVEs in AWS workloads?"**
>
> YES
>
> → **Inspector**

---

## Related Notes

- [[GuardDuty]]
- [[06-Security/Macie]]
- [[06-Security/Security Hub]]
- [[EC2]]
- [[Lambda]]
- [[ECR]]
- [[Systems Manager]]
- [[EventBridge]]
- [[WAF]]
- [[Shield]]
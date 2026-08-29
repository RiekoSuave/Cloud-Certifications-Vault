## What Problem Does It Solve?

Automatically scans supported AWS workloads for software vulnerabilities and unintended network exposure.

Amazon Inspector helps identify security weaknesses before they can be exploited.

### Memory Trick

Inspector = AWS Vulnerability Scanner

---

## Type

Vulnerability Management Service

---

## What Is Amazon Inspector?

Amazon Inspector is an automated security assessment service.

It performs continuous vulnerability management for supported AWS workloads.

Think:

AWS Workload

↓

Amazon Inspector

↓

Vulnerability Scan

↓

Security Findings

### Memory Trick

Inspector = Inspect Workloads for Vulnerabilities

---

## What Does Inspector Scan?

Your course focuses on three major workload types:

- Amazon EC2 instances
- Container images in Amazon ECR
- AWS Lambda functions

### Memory Trick

Inspector Scans:

EC2 + ECR + Lambda

---

## EC2 Instances

Inspector can assess EC2 instances for vulnerabilities.

It can analyze:

- Operating system packages
- Software packages

for known vulnerabilities.

### Memory Trick

EC2 Software Vulnerabilities

→ Inspector

---

## Amazon ECR Container Images

Inspector can scan container images stored in:

Amazon Elastic Container Registry (ECR)

This helps identify software vulnerabilities inside container images.

### Memory Trick

ECR Image Vulnerability

→ Inspector

---

## AWS Lambda Functions

Inspector can also assess:

AWS Lambda Functions

for software vulnerabilities.

### Memory Trick

Lambda Vulnerability

→ Inspector

---

## Continuous Scanning

Inspector provides automated and continuous vulnerability management.

Instead of relying only on manual security assessments, Inspector continually evaluates supported workloads.

### Memory Trick

Inspector = Automatic Vulnerability Scanning

---

## Network Reachability

Your course also associates Inspector with analyzing:

Unintended Network Exposure

This helps identify workloads that may be reachable in ways that create security risks.

### Memory Trick

Inspector = Vulnerabilities + Network Exposure

---

## Inspector Findings

When Inspector identifies a security issue, it generates:

Findings

These findings represent vulnerabilities or security issues that may require investigation.

Basic Idea:

Inspector Scan

↓

Vulnerability Detected

↓

Finding

---

## Inspector vs GuardDuty

This is an important distinction.

### Amazon Inspector

Looks for:

Vulnerabilities in workloads

Think:

Is My Software Vulnerable?

### Amazon GuardDuty

Looks for:

Threats and suspicious activity

Think:

Is Something Malicious Happening?

| Inspector | GuardDuty |
|---|---|
| Vulnerability management | Threat detection |
| Scans workloads | Analyzes activity |
| Finds software weaknesses | Finds suspicious behavior |
| EC2 / ECR / Lambda | CloudTrail / Flow Logs / DNS |

### Memory Trick

Inspector = Vulnerabilities

GuardDuty = Threats

---

## Common Use Cases

- Vulnerability management
- Security assessments
- Scanning EC2 workloads
- Scanning container images
- Scanning Lambda functions
- Identifying unintended network exposure

---

## Scenario Questions

A company wants to automatically scan EC2 instances for software vulnerabilities.

→ Amazon Inspector

---

A company wants to scan container images in Amazon ECR for vulnerabilities.

→ Amazon Inspector

---

A company wants to scan Lambda functions for software vulnerabilities.

→ Amazon Inspector

---

A company wants continuous vulnerability management for supported AWS workloads.

→ Amazon Inspector

---

A company wants to detect suspicious API calls and malicious network activity.

→ GuardDuty

NOT Inspector

---

## Don't Confuse These

Inspector = Vulnerability Management

GuardDuty = Threat Detection

Security Hub = Central Security View

Inspector = Is My Workload Vulnerable?

GuardDuty = Is Something Malicious Happening?

---

## Exam Keywords

Amazon Inspector

Vulnerability

Vulnerability Management

Security Assessment

EC2

ECR

Container Images

Lambda

Network Exposure

Continuous Scanning

Findings

---

## Quick Cheat Sheet

Inspector = Security Scanner

Inspector = Vulnerability Management

Inspector Scans EC2

Inspector Scans ECR Container Images

Inspector Scans Lambda

Inspector = Software Vulnerabilities

Inspector = Network Exposure

GuardDuty = Threat Detection
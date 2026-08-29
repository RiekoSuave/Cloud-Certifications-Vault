See also: [GuardDuty](06-Security/GuardDuty.md)

See also: [Inspector](06-Security/Inspector.md)

See also: [Config](06-Security/Config.md)

## What Problem Does It Solve?

Provides a centralized place to manage security findings across AWS.

AWS Security Hub solves the problem of having security alerts and findings spread across multiple AWS services and AWS accounts.

### Memory Trick

Security Hub = Central Security Dashboard

---

## Type

Security Aggregation

---

## What Is AWS Security Hub?

AWS Security Hub is a central security tool that helps manage security across multiple AWS accounts.

It provides integrated dashboards showing:

- Current security status
- Compliance status
- Security findings

This helps security teams quickly identify issues and take action.

Think:

Multiple Security Services

↓

Security Findings

↓

AWS Security Hub

↓

Central Security Dashboard

### Memory Trick

Security Hub = One Place for Security Findings

---

## Security Findings Aggregation

One of the most important Security Hub concepts is:

Aggregation

Security Hub automatically gathers security alerts and findings from multiple sources.

Instead of checking every security service separately:

GuardDuty

Inspector

Macie

Config

Other Security Tools

↓

Security Hub

↓

Central View

### Memory Trick

Security Hub = Gather the Findings

---

## AWS Services That Integrate with Security Hub

Your course identifies several sources Security Hub can integrate with:

- AWS Config
- Amazon GuardDuty
- Amazon Inspector
- Amazon Macie
- IAM Access Analyzer
- AWS Systems Manager
- AWS Firewall Manager
- AWS Health

It can also receive findings from:

AWS Partner Network Solutions

### Memory Trick

Other Services Find Problems

Security Hub Collects Them

---

## Security and Compliance Dashboard

Security Hub provides integrated dashboards showing:

Security Status

+

Compliance Status

This provides a centralized view that helps teams quickly take action.

### Memory Trick

Security Hub = Security + Compliance Dashboard

---

## Multiple AWS Accounts

Security Hub can help manage security across:

Several AWS Accounts

This is useful when an organization has a multi-account AWS environment.

Basic Idea:

AWS Account A

AWS Account B

AWS Account C

↓

Security Hub

↓

Central Security View

---

## AWS Config Requirement

Your course specifically notes:

AWS Config must first be enabled.

Keep this association in mind when studying Security Hub.

### Memory Trick

Security Hub?

Remember AWS Config

---

## Security Hub vs GuardDuty

These services have different jobs.

### GuardDuty

Detects:

Threats and suspicious activity

### Security Hub

Aggregates:

Security findings from multiple services

| GuardDuty | Security Hub |
|---|---|
| Threat detection | Security aggregation |
| Detects suspicious activity | Collects security findings |
| Generates findings | Centralizes findings |
| Security detector | Security dashboard |

### Memory Trick

GuardDuty = Detect

Security Hub = Collect

See:

[GuardDuty](06-Security/GuardDuty.md)

---

## Security Hub vs Inspector

### Inspector

Finds:

Software vulnerabilities and network exposure

### Security Hub

Collects:

Security findings from Inspector and other security services

### Memory Trick

Inspector = Scan

Security Hub = Aggregate

See:

[Inspector](06-Security/Inspector.md)

---

## Security Hub vs Config

### AWS Config

Tracks:

Resource configurations and compliance

### Security Hub

Provides:

Centralized security and compliance visibility

Security Hub integrates with AWS Config.

### Memory Trick

Config = Track Configuration

Security Hub = Central Security View

See:

[Config](06-Security/Config.md)

---

## Common Use Cases

- Centralizing security findings
- Security operations
- Multi-account security visibility
- Monitoring security status
- Monitoring compliance status
- Aggregating findings from AWS security services

---

## Scenario Questions

A company wants one centralized dashboard for security findings from multiple AWS services.

→ AWS Security Hub

---

A company wants to aggregate security findings across several AWS accounts.

→ AWS Security Hub

---

A company wants a centralized view of security and compliance status.

→ AWS Security Hub

---

A company wants to detect malicious activity using CloudTrail, VPC Flow Logs, and DNS logs.

→ GuardDuty

NOT Security Hub

---

A company wants to scan EC2, ECR container images, and Lambda functions for vulnerabilities.

→ Inspector

NOT Security Hub

---

A company wants to track resource configuration changes and compliance.

→ AWS Config

NOT Security Hub

---

## Don't Confuse These

Security Hub = Aggregate Security Findings

GuardDuty = Threat Detection

Inspector = Vulnerability Detection

Config = Configuration & Compliance Tracking

Macie = Sensitive Data Detection in S3

### Memory Trick

GuardDuty = Detect Threats

Inspector = Find Vulnerabilities

Macie = Find Sensitive Data

Security Hub = Bring Findings Together

---

## Exam Keywords

AWS Security Hub

Security Findings

Security Aggregation

Centralized Security

Security Dashboard

Compliance

Multiple AWS Accounts

GuardDuty

Inspector

Macie

AWS Config

---

## Quick Cheat Sheet

Security Hub = Central Security Dashboard

Security Hub = Aggregate Findings

Security Hub = Multi-Account Security View

Security Hub = Security + Compliance Status

GuardDuty = Threat Detection

Inspector = Vulnerability Scanning

Macie = Sensitive Data in S3

Config = Configuration & Compliance

Other Services Find → Security Hub Collects
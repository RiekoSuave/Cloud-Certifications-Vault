## Identity & Account Management

IAM = Who can do what

Organizations = Manage multiple AWS accounts

Control Tower = Automated multi-account governance

IAM Access Analyzer = Find resources shared externally

---

## Logging, Auditing & Compliance

CloudTrail = Who did what / API activity

Config = Resource configuration & compliance

Artifact = Compliance documents & reports

AWS Abuse = Report abusive or illegal AWS resource usage

---

## Threat Detection & Security

GuardDuty = Detect threats / suspicious activity

Inspector = Find software vulnerabilities

Macie = Find sensitive data / PII in S3

Detective = Investigate root cause

Security Hub = Gather security findings

### Memory Trick

GuardDuty = THREATS

Inspector = VULNERABILITIES

Macie = DATA

Detective = INVESTIGATE

Security Hub = GATHER

---

## Network & Application Security

Security Group = Instance / ENI firewall

NACL = Subnet firewall

AWS Network Firewall = Protect VPC from network attacks

WAF = Filter malicious web requests

Shield = DDoS protection

Firewall Manager = Manage security rules across an Organization

### Memory Trick

Security Group = INSTANCE

NACL = SUBNET

Network Firewall = VPC

WAF = WEB

Shield = DDoS

---

## Encryption & Certificates

KMS = Encryption key management

CloudHSM = Hardware encryption / You manage keys

ACM = SSL/TLS certificates

### Memory Trick

KMS = KEYS

CloudHSM = HARDWARE KEYS

ACM = CERTIFICATES

---

## Shared Responsibility Model

AWS = Security OF the Cloud

Customer = Security IN the Cloud

Physical Hardware = AWS

EC2 Guest OS Patching = Customer

Security Groups = Customer

IAM Permissions = Customer

Customer Data = Customer

### Memory Trick

AWS = Infrastructure

Customer = Configuration + Data + Access

---

## Highest-Value Exam Triggers

"Who can do what?" → IAM

"Multiple AWS accounts" → Organizations

"Automated account governance" → Control Tower

"Shared externally" → IAM Access Analyzer

"Who did what?" → CloudTrail

"Configuration changes" → Config

"Threat / suspicious activity" → GuardDuty

"Software vulnerabilities" → Inspector

"PII in S3" → Macie

"Root cause" → Detective

"Central security findings" → Security Hub

"DDoS" → Shield

"Malicious web requests" → WAF

"Protect VPC from network attacks" → AWS Network Firewall

"Security rules across accounts" → Firewall Manager

"Encryption keys" → KMS

"Hardware encryption / manage own keys" → CloudHSM

"SSL/TLS certificates" → ACM

"Compliance reports" → Artifact

"Report abusive AWS resources" → AWS Abuse

---

## Must-Know Comparisons

CloudTrail = API Activity

Config = Resource Configuration

GuardDuty = Threat Detection

Inspector = Vulnerability Detection

Macie = Sensitive Data

Detective = Investigation

Security Hub = Aggregation

Shield = DDoS

WAF = Web Filtering

KMS = Keys

CloudHSM = Hardware Keys

ACM = Certificates

IAM = Users & Permissions

Organizations = Accounts

Control Tower = Governance

---

## 10-Second Security Review

IAM → Permissions

CloudTrail → Activity

Config → Changes

GuardDuty → Threats

Inspector → Vulnerabilities

Macie → Sensitive Data

Detective → Root Cause

Security Hub → Findings

Shield → DDoS

WAF → Web

KMS → Keys

CloudHSM → Hardware Keys

ACM → Certificates
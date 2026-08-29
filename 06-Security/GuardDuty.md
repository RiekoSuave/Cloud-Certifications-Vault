See also: [CloudTrail](06-Security/CloudTrail.md)

See also: [VPC Flow Logs](<05-Networking/VPC Flow Logs.md>)

## What Problem Does It Solve?

Detects threats and suspicious activity within your AWS environment.

Amazon GuardDuty provides intelligent threat detection by continuously analyzing activity for potentially malicious or unauthorized behavior.

### Memory Trick

GuardDuty = AWS Security Guard

---

## Type

Threat Detection Service

---

## What Is Amazon GuardDuty?

GuardDuty is an intelligent threat detection service designed to protect your AWS account.

It uses:

- Machine Learning
- Anomaly Detection
- Third-Party Data

to identify suspicious activity.

Think:

AWS Activity

↓

GuardDuty

↓

Machine Learning + Anomaly Detection

↓

Security Findings

### Memory Trick

GuardDuty = Detect Suspicious Activity

---

## Easy to Enable

GuardDuty can be enabled without installing software.

Your course emphasizes:

One Click to Enable

No Software Installation Required

### Memory Trick

GuardDuty = Turn It On and Monitor

---

## GuardDuty Data Sources

One of the most important things to recognize is the information GuardDuty analyzes.

Your course identifies:

- CloudTrail Event Logs
- VPC Flow Logs
- DNS Logs

### Memory Trick

GuardDuty Watches:

API Activity + Network Traffic + DNS

---

## CloudTrail Event Logs

GuardDuty analyzes CloudTrail activity for suspicious behavior.

Examples include:

- Unusual API calls
- Unauthorized deployments

Your course also identifies:

### CloudTrail Management Events

Examples:

- Create VPC subnet
- Create trail

### CloudTrail S3 Data Events

Examples:

- Get object
- List objects
- Delete object

### Memory Trick

CloudTrail Records Activity

GuardDuty Analyzes It for Threats

See:

[CloudTrail](06-Security/CloudTrail.md)

---

## VPC Flow Logs

GuardDuty analyzes VPC Flow Logs for suspicious network activity.

Examples include:

- Unusual internal traffic
- Unusual IP addresses

### Memory Trick

Flow Logs = Network Traffic

GuardDuty = Look for Suspicious Traffic

See:

[VPC Flow Logs](<05-Networking/VPC Flow Logs.md>)

---

## DNS Logs

GuardDuty can analyze DNS activity.

Your course gives an example of:

Compromised EC2 instances sending encoded data through DNS queries.

This could indicate suspicious or malicious behavior.

### Memory Trick

Strange DNS Activity?

→ GuardDuty

---

## Optional Features

Your course also identifies optional GuardDuty features involving:

- EKS Audit Logs
- RDS & Aurora
- EBS
- Lambda
- S3 Data Events

For the current course, recognize that GuardDuty can extend threat detection beyond its core data sources.

---

## GuardDuty Findings

When GuardDuty detects suspicious activity, it generates:

Findings

A finding represents a potential security issue detected by GuardDuty.

### Memory Trick

GuardDuty Detects Threat

↓

Creates Finding

---

## EventBridge Integration

GuardDuty findings can be used with:

Amazon EventBridge

EventBridge rules can respond to GuardDuty findings.

Targets mentioned in your course include:

- AWS Lambda
- Amazon SNS

Basic Idea:

GuardDuty

↓

Security Finding

↓

EventBridge

↓

Lambda or SNS

### Memory Trick

GuardDuty Finds It

EventBridge Responds to It

---

## Cryptocurrency Attacks

Your course specifically notes that GuardDuty can help detect:

Cryptocurrency-related attacks

GuardDuty has a dedicated finding for this type of suspicious activity.

---

## GuardDuty vs CloudTrail

These services work together but solve different problems.

### CloudTrail

Records:

AWS API Activity

Think:

Who Did What?

### GuardDuty

Analyzes activity for:

Threats and Suspicious Behavior

Think:

Is Something Malicious Happening?

| CloudTrail | GuardDuty |
|---|---|
| Records activity | Detects threats |
| API activity | Suspicious activity |
| Auditing | Threat detection |
| Who did what? | Is this malicious? |

### Memory Trick

CloudTrail = Record

GuardDuty = Detect

---

## Common Use Cases

- Threat detection
- Security monitoring
- Detecting unusual API activity
- Detecting suspicious network traffic
- Detecting suspicious DNS activity
- Identifying potentially compromised resources

---

## Scenario Questions

A company wants intelligent threat detection across its AWS environment.

→ GuardDuty

---

A company wants to detect unusual API calls.

→ GuardDuty

---

A company wants to detect unusual network traffic using VPC Flow Logs.

→ GuardDuty

---

A company wants to detect suspicious DNS activity from compromised EC2 instances.

→ GuardDuty

---

A company wants security findings to trigger an automated response.

→ GuardDuty + EventBridge

---

A company wants to determine who deleted an AWS resource.

→ CloudTrail

NOT GuardDuty

---

A company wants to track how a resource configuration changed over time.

→ AWS Config

NOT GuardDuty

---

## Don't Confuse These

GuardDuty = Threat Detection

CloudTrail = API Activity / Audit Trail

Config = Resource Configuration History

VPC Flow Logs = Network Traffic Records

EventBridge = Respond to Events

---

## Exam Keywords

Amazon GuardDuty

Threat Detection

Machine Learning

Anomaly Detection

Threat Intelligence

CloudTrail

VPC Flow Logs

DNS Logs

Security Findings

EventBridge

Suspicious Activity

---

## Quick Cheat Sheet

GuardDuty = AWS Security Guard

GuardDuty = Threat Detection

GuardDuty = Machine Learning + Anomaly Detection

GuardDuty Watches CloudTrail + VPC Flow Logs + DNS

GuardDuty Detects → Finding

Finding → EventBridge → Lambda / SNS

CloudTrail = Record Activity

GuardDuty = Detect Threats
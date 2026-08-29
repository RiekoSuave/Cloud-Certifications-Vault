## What Problem Does It Solve?

[[CloudTrail]] records:

**AWS API activity and account actions**

It helps answer questions such as:

- Who changed this resource?
- Who deleted this bucket?
- Which API call was made?
- When did the change happen?
- From which IP address was the call made?
- Which IAM identity performed the action?

Architecture:

User / Role / AWS Service  
↓  
AWS API Call  
↓  
CloudTrail  
↓  
Event History / S3 / CloudWatch Logs

> [!tip] Memory Trick
> **CloudTrail = WHO DID WHAT IN AWS**

---

## Core Concept

CloudTrail focuses on:

**Governance, auditing, compliance, and investigation**

It records events related to:

**AWS API activity**

Examples:

- CreateBucket
- TerminateInstances
- PutBucketPolicy
- CreateUser
- DeleteSecurityGroup
- UpdateFunctionConfiguration

### Killer Exam Clue

> **Need to determine who made an AWS configuration change**
>
> → **CloudTrail**

---

# Management Events

**Management Events**

record operations performed on:

**AWS resources**

Examples:

- Create EC2 instance
- Modify security group
- Delete S3 bucket
- Create IAM role
- Change route table
- Stop RDS instance

These are sometimes called:

**Control plane operations**

### Memory Trick

**Management Event = Change AWS Configuration**

---

# Read vs Write Management Events

Management events can include:

## Read Events

Examples:

- DescribeInstances
- GetBucketPolicy
- ListRoles

Think:

**Look at configuration**

---

## Write Events

Examples:

- RunInstances
- TerminateInstances
- CreateRole
- DeleteBucket

Think:

**Change configuration**

### Killer Exam Shortcut

**Who changed something?**
→ Write Management Event

---

# Data Events

**Data Events**

record operations performed on:

**Data inside supported AWS resources**

Examples include:

- S3 object-level activity
- Lambda function invocation
- DynamoDB item-level API activity in supported configurations

### Killer Exam Clue

> **Need to audit S3 object-level access**
>
> → **CloudTrail Data Events**

---

# Management Events vs Data Events

## Management Event

Example:

Create S3 bucket

## Data Event

Example:

Get S3 object

### Memory Trick

**Management = Resource**

**Data = Inside the Resource**

---

# S3 Data Events

Standard management events can show:

**Bucket configuration changes**

But if you need to know:

**Who accessed a specific S3 object**

enable:

**S3 Data Events**

### Killer Exam Clue

> **Find who downloaded `secret.pdf` from S3**
>
> → **CloudTrail S3 Data Events**

---

# Lambda Data Events

CloudTrail can record:

**Lambda invocation activity**

as:

**Data Events**

This can help audit:

**Who or what invoked a Lambda function**

---

# Event History

CloudTrail provides:

**Event History**

for recent management events.

This lets you search recent API activity without first building:

**A custom trail**

### Exam Principle

> **For quick recent investigation, start with CloudTrail Event History**

---

# Trails

A:

**Trail**

delivers CloudTrail events to:

**S3**

and optionally integrates with:

**CloudWatch Logs**

Architecture:

AWS Activity  
↓  
CloudTrail Trail  
↓  
S3

Optional:

CloudTrail  
↓  
CloudWatch Logs

### Killer Exam Clue

> **Need long-term retention of AWS API audit logs**
>
> → **Create a CloudTrail Trail to S3**

---

# Why Use S3?

S3 provides:

- Durable storage
- Long-term retention
- Lifecycle policies
- Archival
- Centralized audit storage

### Memory Trick

**CloudTrail records**

**S3 keeps**

---

# Multi-Region Trail

A trail can capture activity across:

**Multiple AWS Regions**

This is usually preferred for:

**Centralized account auditing**

### Killer Exam Clue

> **Audit API activity across all Regions**
>
> → **Multi-Region Trail**

---

# Global Service Events

Some AWS services are:

**Global**

Examples include:

- IAM
- Route 53

CloudTrail can capture:

**Global service events**

as part of appropriately configured trails.

---

# Organization Trails

In AWS Organizations, you can create:

**Organization Trails**

to capture activity across:

**Multiple AWS accounts**

Architecture:

AWS Organizations  
↓  
Member Accounts  
↓  
Organization Trail  
↓  
Central S3 Bucket

### Killer Exam Clue

> **Centralize API auditing across all AWS accounts in an organization**
>
> → **CloudTrail Organization Trail**

---

# CloudTrail + CloudWatch Logs

CloudTrail events can be sent to:

[[CloudWatch]] Logs

This enables:

- Metric filters
- Alarms
- Near-real-time alerting

Architecture:

CloudTrail  
↓  
CloudWatch Logs  
↓  
Metric Filter  
↓  
Alarm  
↓  
SNS

### Killer Exam Pattern

> **Alert when someone changes a critical AWS configuration**
>
> → **CloudTrail + CloudWatch Logs + Metric Filter + Alarm**

---

# Example — Root User Activity

Architecture:

Root User API Call  
↓  
CloudTrail  
↓  
CloudWatch Logs  
↓  
Metric Filter  
↓  
Alarm  
↓  
SNS

### Killer Exam Clue

> **Alert whenever the root account is used**
>
> → **CloudTrail + CloudWatch alarm pattern**

---

# Example — Security Group Change

CloudTrail records:

SecurityGroupChange  
↓  
CloudWatch Logs  
↓  
Metric Filter  
↓  
Alarm  
↓  
Security Team

This provides:

**Automated audit alerting**

---

# CloudTrail + EventBridge

CloudTrail API activity can also participate in:

**Event-driven automation**

through integrations with:

[[20-SAA/10-Messaging/EventBridge]]

Example:

Sensitive API Event  
↓  
EventBridge  
↓  
Lambda  
↓  
Remediation

### Exam Pattern

> **Automatically react to specific AWS API activity**
>
> → **CloudTrail/EventBridge-based automation**

---

# CloudTrail Lake

**CloudTrail Lake**

provides:

**Queryable event storage**

for CloudTrail activity.

It is useful for:

- Auditing
- Investigations
- SQL-like querying
- Long-term event analysis

### Killer Exam Clue

> **Need to query large amounts of CloudTrail activity without manually analyzing raw log files**
>
> → **CloudTrail Lake**

---

# CloudTrail Lake vs Athena

Both can help analyze:

**CloudTrail data**

## CloudTrail Lake

Think:

**Purpose-built CloudTrail event querying**

## [[Athena]]

Think:

**SQL queries against CloudTrail logs stored in S3**

### Killer Shortcut

CloudTrail events already in CloudTrail Lake  
→ CloudTrail Lake

CloudTrail log files in S3  
→ Athena

---

# Log File Integrity Validation

CloudTrail supports:

**Log File Integrity Validation**

This helps detect whether:

**CloudTrail log files were modified or deleted after delivery**

### Killer Exam Clue

> **Need evidence that CloudTrail audit logs were not tampered with**
>
> → **Log File Integrity Validation**

### Memory Trick

**Integrity Validation = Prove the logs weren't changed**

---

# Encryption

CloudTrail log files stored in S3 can be encrypted.

For stronger key control:

Use:

[[06-Security/KMS]]

with appropriate:

**Key permissions**

---

# S3 Bucket Security

CloudTrail logs often contain:

**Sensitive audit information**

The S3 bucket should be protected with:

- Least privilege
- Encryption
- Bucket policies
- Versioning where appropriate
- Lifecycle controls

---

# Centralized Logging Account

A strong multi-account architecture:

Member Accounts  
↓  
CloudTrail Organization Trail  
↓  
Central Logging Account  
↓  
Dedicated S3 Bucket

Benefits:

- Separation of duties
- Reduced tampering risk
- Central auditing
- Easier compliance

### SAA Principle

> **Centralize audit logs in a dedicated security/logging account where appropriate**

---

# CloudTrail vs CloudWatch

This distinction is one of the most important monitoring topics.

## [[CloudWatch]]

Answers:

> **How is the system performing?**

Examples:

- CPU
- Latency
- Errors
- Logs
- Alarms

## CloudTrail

Answers:

> **Who did what in AWS?**

Examples:

- Who deleted EC2?
- Who changed IAM policy?
- Who modified security group?

### Memory Trick

**CloudWatch = PERFORMANCE**

**CloudTrail = ACTIVITY HISTORY**

---

# CloudTrail vs AWS Config

## CloudTrail

Records:

**The API action**

Example:

`PutBucketPolicy`

## [[AWS Config]]

Tracks:

**Resource configuration state**

Example:

S3 bucket became:

**Public**

### Killer Shortcut

**Who changed it?**
→ CloudTrail

**What configuration does it have?**
→ Config

---

# CloudTrail vs Access Logs

Different services can produce:

**Access logs**

Examples:

- ALB access logs
- CloudFront logs
- S3 server access logs

These record:

**Service-specific traffic**

CloudTrail records:

**AWS API activity**

### Exam Principle

> **Do not confuse application/request access logs with AWS API audit logs**

---

# CloudTrail vs VPC Flow Logs

## CloudTrail

Think:

**AWS API calls**

## VPC Flow Logs

Think:

**Network traffic metadata**

### Memory Trick

**CloudTrail = API**

**Flow Logs = Network**

---

# CloudTrail vs S3 Access Logs

Need:

**Who called `PutBucketPolicy`?**

→ CloudTrail

Need:

**HTTP requests made to S3 bucket objects**

→ S3 access logging or CloudTrail Data Events depending on exact auditing requirement

For SAA, if the question emphasizes:

**AWS API identity and object API activity**

think:

**CloudTrail Data Events**

---

# User Identity Information

CloudTrail events can include details such as:

- IAM identity
- Role
- Account
- Source IP
- Timestamp
- API action
- AWS Region
- Request parameters

This makes CloudTrail extremely valuable for:

**Incident investigation**

---

# Source IP

CloudTrail can record:

**Source IP address**

associated with API calls.

### Killer Exam Clue

> **Determine where a suspicious AWS API request originated**
>
> → **CloudTrail event details**

---

# Failed API Calls

CloudTrail can also record:

**Failed API requests**

This can help investigate:

- AccessDenied
- Unauthorized activity
- Misconfigured automation

---

# Incident Investigation Example

Security team notices:

An EC2 instance disappeared.

Investigation:

CloudTrail  
↓  
Search `TerminateInstances`  
↓  
Find:

- User/role
- Timestamp
- Source IP
- Region

### Memory Trick

**Resource vanished? → Check CloudTrail**

---

# IAM Investigation

Question:

> Who attached AdministratorAccess to this role?

CloudTrail can show:

**The API operation and principal**

---

# CloudTrail and Root User

Root account activity is especially sensitive.

Best practice:

- Avoid routine root use
- Monitor root activity
- Alert on root API calls

CloudTrail provides:

**The audit record**

---

# Architecture Thinking

## Scenario 1 — Who Deleted S3 Bucket?

Need to identify:

- Identity
- Time
- API call

Choose:

**CloudTrail**

---

## Scenario 2 — Who Downloaded Object?

Need object-level audit of:

`s3://bucket/payroll.csv`

Choose:

**CloudTrail S3 Data Events**

---

## Scenario 3 — Long-Term Audit

Compliance requires:

**7 years of API activity records**

Choose:

CloudTrail Trail  
↓  
S3  
↓  
Lifecycle / Archive

---

## Scenario 4 — All AWS Accounts

Security team needs central auditing across:

50 AWS accounts.

Choose:

**Organization Trail**

---

## Scenario 5 — Alert on IAM Change

Need immediate alert when:

**IAM policies change**

Choose:

CloudTrail  
↓  
CloudWatch Logs / EventBridge  
↓  
Alert / Automation

---

## Scenario 6 — CPU Too High

Need alert when:

EC2 CPU > 90%.

Do NOT choose CloudTrail.

Choose:

**CloudWatch**

---

## Scenario 7 — Resource Noncompliant

Need detect when:

**S3 bucket becomes public**

Think:

**AWS Config**

rather than CloudTrail alone.

---

## Scenario 8 — Query S3 Audit Files

CloudTrail logs are stored in:

S3.

Need SQL investigation.

Choose:

**Athena**

---

## Scenario 9 — Query CloudTrail Events Directly

Need purpose-built querying over:

**CloudTrail events**

Choose:

**CloudTrail Lake**

---

## Scenario 10 — Tamper Detection

Compliance team needs to verify:

**Audit files were not modified**

Choose:

**Log File Integrity Validation**

---

# Scenario Recognition

Immediately think:

**CloudTrail**

when you see:

- API history
- Audit
- Who changed
- Who deleted
- Source IP
- IAM activity
- Root user activity
- Governance
- Forensics
- AWS account activity

---

## Think Data Events When You See

- S3 object access
- Lambda invocation auditing
- Resource data-plane activity

---

## Think Organization Trail When You See

- Multiple AWS accounts
- Centralized audit logs
- AWS Organizations

---

## Think CloudTrail Lake When You See

- Query CloudTrail events
- Long-term event analytics
- Audit investigation

---

# Exam Traps

## Trap 1 — CloudTrail Monitors EC2 CPU

❌

Think:

**CloudWatch**

---

## Trap 2 — CloudTrail Shows Current Resource Compliance

❌

Think:

**AWS Config**

---

## Trap 3 — Standard Management Events Automatically Show Every S3 Object Read

❌

Object-level activity requires:

**Data Events**

---

## Trap 4 — CloudTrail Logs Must Stay Only in CloudTrail Console

❌

Trails can deliver logs to:

**S3**

and integrate with:

**CloudWatch Logs**

---

## Trap 5 — CloudTrail Is Just for Successful API Calls

❌

It can also help investigate:

**Failed API activity**

---

## Trap 6 — CloudTrail Lake and CloudWatch Logs Insights Are the Same

❌

CloudTrail Lake:

**CloudTrail event analytics**

Logs Insights:

**CloudWatch Logs querying**

---

## Trap 7 — CloudTrail Replaces VPC Flow Logs

❌

CloudTrail:

**API activity**

VPC Flow Logs:

**Network traffic**

---

# Quick Cheat Sheet

| Exam Clue | Answer |
|---|---|
| Who Changed AWS Resource? | CloudTrail |
| AWS API History | CloudTrail |
| Recent Management Activity | Event History |
| Long-Term Audit Logs | Trail → S3 |
| Object-Level S3 Audit | Data Events |
| Lambda Invocation Audit | Data Events |
| All Accounts Audit | Organization Trail |
| Alert on API Activity | CloudTrail + CloudWatch/EventBridge |
| Query CloudTrail Events | CloudTrail Lake |
| Query CloudTrail Logs in S3 | Athena |
| Prove Logs Untampered | Log File Integrity Validation |
| Performance Monitoring | CloudWatch |
| Resource Compliance | AWS Config |
| Network Traffic Metadata | VPC Flow Logs |

---

# Monitoring Decision Map

Need:

**How is resource performing?**

→ CloudWatch

Need:

**Who changed resource?**

→ CloudTrail

Need:

**What configuration does resource have?**

→ AWS Config

Need:

**What network traffic occurred?**

→ VPC Flow Logs

Need:

**Who accessed S3 object?**

→ CloudTrail Data Events

---

# Final Exam Rapid-Fire

> **WHO DID IT?**
> → CLOUDTRAIL
>
> **AWS API HISTORY**
> → CLOUDTRAIL
>
> **RESOURCE CONFIG CHANGE**
> → MANAGEMENT EVENT
>
> **S3 OBJECT ACCESS**
> → DATA EVENT
>
> **RECENT API HISTORY**
> → EVENT HISTORY
>
> **LONG-TERM AUDIT**
> → TRAIL → S3
>
> **MULTI-ACCOUNT AUDIT**
> → ORGANIZATION TRAIL
>
> **QUERY CLOUDTRAIL EVENTS**
> → CLOUDTRAIL LAKE
>
> **QUERY CLOUDTRAIL FILES IN S3**
> → ATHENA
>
> **LOG TAMPER DETECTION**
> → LOG FILE INTEGRITY VALIDATION
>
> **CPU / LATENCY**
> → CLOUDWATCH
>
> **RESOURCE COMPLIANCE**
> → CONFIG
>
> **NETWORK TRAFFIC**
> → VPC FLOW LOGS

---

## Master Memory Trick

> [!tip] CloudTrail Master Memory Trick
> Imagine AWS has:
>
> **A security camera pointed at the API control panel**
>
> Every time someone:
>
> - Creates something
> - Deletes something
> - Changes something
> - Calls an AWS API
>
> the camera records:
>
> **WHO**
>
> **WHAT**
>
> **WHEN**
>
> **WHERE FROM**
>
> That's:
>
> **CLOUDTRAIL**
>
> If you're asking:
>
> **"Why is CPU at 95%?"**
>
> that's:
>
> **CLOUDWATCH**
>
> If you're asking:
>
> **"Is this bucket configured correctly?"**
>
> that's:
>
> **AWS CONFIG**

So remember:

> **CLOUDWATCH**
> → HOW IS IT RUNNING?
>
> **CLOUDTRAIL**
> → WHO DID WHAT?
>
> **CONFIG**
> → WHAT IS IT CONFIGURED LIKE?
>
> **FLOW LOGS**
> → WHO TALKED TO WHOM ON THE NETWORK?

And the killer SAA question:

> **"Does the question ask who performed an AWS API action or changed a resource?"**
>
> YES
>
> → **CloudTrail**

---

## Related Notes

- [[CloudWatch]]
- [[AWS Config]]
- [[Athena]]
- [[S3]]
- [[20-SAA/10-Messaging/EventBridge]]
- [[SNS]]
- [[IAM]]
- [[05-Networking/VPC Flow Logs]]
- [[06-Security/KMS]]
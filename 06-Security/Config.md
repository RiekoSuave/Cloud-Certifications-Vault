See also: [CloudTrail](06-Security/CloudTrail.md)

## What Problem Does It Solve?

Tracks AWS resource configurations, changes, and compliance over time.

AWS Config helps answer questions such as:

- Is this resource compliant?
- How was this resource configured?
- How has this resource changed over time?

### Memory Trick

Config = Resource Configuration History

---

## Type

Compliance Monitoring

---

## What Is AWS Config?

AWS Config helps with:

- Auditing AWS resources
- Recording resource configurations
- Tracking configuration changes
- Evaluating compliance

Think:

AWS Resource

↓

Configuration Changes

↓

AWS Config

↓

Configuration & Compliance History

### Memory Trick

Config = What Changed?

---

## Configuration History

AWS Config records resource configurations and changes over time.

This allows you to investigate questions such as:

How has my Application Load Balancer configuration changed?

What configuration did a resource previously have?

### Memory Trick

Config = Resource History

---

## Compliance Monitoring

AWS Config can help determine whether resources comply with desired configurations.

Examples from your course include:

Is there unrestricted SSH access to my Security Groups?

Are my S3 buckets publicly accessible?

These types of questions involve evaluating the configuration of AWS resources.

### Memory Trick

Config = Is My Resource Compliant?

---

## Configuration Data and S3

AWS Config configuration data can be stored in:

Amazon S3

That data can then be analyzed using services such as:

Amazon Athena

Basic Idea:

AWS Resources

↓

AWS Config

↓

Amazon S3

↓

Amazon Athena

---

## Notifications

AWS Config can send notifications about changes using:

Amazon SNS

### Memory Trick

Config Change → SNS Notification

---

## Regional Service

AWS Config is a:

Per-Region Service

However, configuration and compliance information can be aggregated across:

- Multiple AWS Regions
- Multiple AWS Accounts

### Memory Trick

Config = Regional, But Can Aggregate

---

## Resource Compliance Over Time

AWS Config allows you to view the compliance status of a resource over time.

Think:

Resource

↓

Configuration

↓

Compliance History

This is useful for:

- Auditing
- Compliance reviews
- Investigating configuration changes

---

## Resource Configuration Over Time

AWS Config can also show how the configuration of a resource has changed over time.

Example:

ALB Configuration

Yesterday

↓

Configuration Change

↓

Today

AWS Config helps maintain this configuration history.

---

## Config and CloudTrail

AWS Config can show related CloudTrail API calls when CloudTrail is enabled.

This helps connect:

Configuration Change

with

API Activity

---

## Config vs CloudTrail

This is one of the most important distinctions.

### AWS Config

Tracks:

Resource configurations and changes

Think:

What changed?

### CloudTrail

Tracks:

API activity and account actions

Think:

Who did it?

| AWS Config | CloudTrail |
|---|---|
| Resource configuration | API activity |
| Configuration history | Activity history |
| Compliance | Auditing actions |
| What changed? | Who did it? |

### Memory Trick

Config = WHAT Changed?

CloudTrail = WHO Did It?

See:

[CloudTrail](06-Security/CloudTrail.md)

---

## Scenario Questions

A company wants to know how an ALB configuration changed over time.

→ AWS Config

---

A company wants to determine whether its S3 buckets have public access.

→ AWS Config

---

A company wants to determine whether Security Groups allow unrestricted SSH access.

→ AWS Config

---

A company wants to track resource compliance over time.

→ AWS Config

---

A company wants notifications when resource configurations change.

→ AWS Config + SNS

---

A company wants to determine who deleted an AWS resource.

→ CloudTrail

NOT Config

---

## Don't Confuse These

Config = Resource Configuration

CloudTrail = API Activity

CloudWatch = Monitoring

Config = What Changed?

CloudTrail = Who Did It?

---

## Common Use Cases

- Compliance audits
- Resource configuration tracking
- Configuration history
- Compliance monitoring
- Change management
- Investigating resource configurations

---

## Exam Keywords

AWS Config

Configuration

Configuration History

Compliance

Resource Compliance

Resource Changes

Audit

S3

SNS

Regional Service

---

## Quick Cheat Sheet

Config = Resource Configuration History

Config = What Changed?

Config = Compliance

Config = Per-Region Service

Config Data → S3

Config Changes → SNS

CloudTrail = Who Did It?

Config = What Changed?
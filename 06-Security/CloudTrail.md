See also: [Config](06-Security/Config.md)

See also: [GuardDuty](06-Security/GuardDuty.md)

## What Problem Does It Solve?

Tracks AWS API activity and actions performed within your AWS account.

CloudTrail helps answer:

Who did what?

It provides an audit trail of activity within AWS.

### Memory Trick

CloudTrail = Who Did What?

---

## Type

Audit Logging

---

## What Is CloudTrail?

CloudTrail records activity involving AWS APIs.

Think:

User / Service

↓

AWS API Action

↓

CloudTrail

↓

Activity Record

This provides visibility into actions performed within your AWS environment.

---

## What Does CloudTrail Track?

The key concept from your course is:

API Activity

CloudTrail helps identify actions performed against AWS resources.

This makes it useful for:

- Auditing activity
- Security investigations
- Troubleshooting events

### Memory Trick

CloudTrail = AWS Activity History

---

## Security Auditing

CloudTrail can help investigate activity inside an AWS account.

Example questions:

Who performed an action?

What action was performed?

What happened to a resource?

### Memory Trick

Security Investigation?

→ Check CloudTrail

---

## Troubleshooting

One especially important scenario from your course:

A resource was unexpectedly deleted.

What should you investigate first?

→ CloudTrail

CloudTrail can help determine what action occurred.

### Exam Scenario

An EC2 instance, S3 bucket, or another AWS resource was deleted and the company wants to determine what happened.

→ CloudTrail

---

## CloudTrail and GuardDuty

GuardDuty can use CloudTrail event information as one of its data sources.

Your course gives examples such as:

- Unusual API calls
- Unauthorized deployments
- Management activity
- S3 data activity

### Memory Trick

CloudTrail = Records Activity

GuardDuty = Detects Suspicious Activity

See:

[GuardDuty](06-Security/GuardDuty.md)

---

## CloudTrail vs CloudWatch

These are commonly confused.

### CloudTrail

Think:

Actions

API Activity

Who Did What?

### CloudWatch

Think:

Metrics

Logs

Alarms

Resource Monitoring

### Memory Trick

CloudTrail = Activity

CloudWatch = Performance / Monitoring

---

## CloudTrail vs Config

### CloudTrail

Tracks:

API activity and actions

Think:

Who changed something?

### Config

Tracks:

Resource configurations and changes over time

Think:

What changed?

| CloudTrail | Config |
|---|---|
| API activity | Resource configuration |
| User/service actions | Configuration history |
| Who did what? | What changed? |
| Auditing activity | Compliance/configuration tracking |

### Memory Trick

CloudTrail = WHO

Config = WHAT

See:

[Config](06-Security/Config.md)

---

## Common Use Cases

- Security audits
- Account auditing
- Incident investigations
- Troubleshooting AWS events
- Investigating resource deletion
- Reviewing API activity

---

## Scenario Questions

A company wants to know who deleted an AWS resource.

→ CloudTrail

---

A security team needs to investigate AWS API activity.

→ CloudTrail

---

An administrator wants an audit trail of actions within an AWS account.

→ CloudTrail

---

A company wants to monitor CPU utilization.

→ CloudWatch

NOT CloudTrail

---

A company wants to track how the configuration of a resource changed over time.

→ AWS Config

NOT CloudTrail

---

A company wants intelligent threat detection using activity such as unusual API calls.

→ GuardDuty

GuardDuty can use CloudTrail information as an input.

---

## Don't Confuse These

CloudTrail = API Activity

CloudWatch = Metrics / Logs / Alarms

Config = Resource Configuration History

GuardDuty = Threat Detection

---

## Exam Keywords

CloudTrail

API Activity

API Calls

Audit

Auditing

User Activity

Account Activity

Security Investigation

Resource Deletion

Who Did What

---

## Quick Cheat Sheet

CloudTrail = Who Did What?

CloudTrail = API Activity

CloudTrail = Audit Trail

Deleted Resource? = Check CloudTrail

CloudWatch = Monitor Resources

Config = Track Configuration

GuardDuty = Detect Threats
## Core Services

CloudWatch = Metrics, Logs & Alarms

CloudTrail = API Activity

Config = Resource Configuration History

CloudFormation = Infrastructure as Code

Systems Manager = Operations & Automation

Trusted Advisor = Recommendations

---

## Ultimate Memory Pattern

CloudWatch = WATCH

CloudTrail = WHO DID IT

Config = WHAT CHANGED

CloudFormation = BUILD

Systems Manager = MANAGE

Trusted Advisor = ADVISE

---

## CloudWatch

Think:

Metrics

Logs

Alarms

Dashboards

### Key Exam Facts

EC2 Default Monitoring = 5 Minutes

EC2 Detailed Monitoring = 1 Minute

EC2 Logs → CloudWatch Agent

Alarm → SNS Notification

Alarm → Auto Scaling

Alarm → EC2 Action

### Memory Trick

CloudWatch = What's Happening?

---

## CloudTrail

Think:

API Calls

Account Activity

Auditing

### Key Exam Facts

Who made an API call?

→ CloudTrail

Who deleted a resource?

→ CloudTrail

Investigate AWS account activity?

→ CloudTrail

### Memory Trick

CloudTrail = Who Did It?

---

## Config

Think:

Configuration

Resource History

Compliance

### Key Exam Facts

How did a resource change?

→ Config

Is a resource compliant?

→ Config

Track configuration over time?

→ Config

### Memory Trick

Config = What Changed?

---

## CloudFormation

Think:

Infrastructure as Code

Templates

Repeatable Infrastructure

### Key Exam Facts

Deploy infrastructure using code?

→ CloudFormation

Create AWS resources automatically from a template?

→ CloudFormation

Repeat infrastructure across Regions or accounts?

→ CloudFormation

### Memory Trick

CloudFormation = BUILD

---

## Systems Manager

Think:

Operations

Automation

Patching

Run Commands

### Key Exam Facts

Patch thousands of servers?

→ Systems Manager

Manage EC2 + On-Premises?

→ Systems Manager

Secure server access without SSH?

→ Session Manager

Configuration + Secrets?

→ Parameter Store

### Memory Trick

Systems Manager = MANAGE

---

## Trusted Advisor

Think:

AWS Best-Practice Recommendations

### Six Categories

Cost Optimization

Performance

Security

Fault Tolerance

Service Limits

Operational Excellence

### Key Exam Fact

AWS recommends ways to improve your environment?

→ Trusted Advisor

### Memory Trick

Trusted Advisor = AWS Consultant

---

## Most Important Comparisons

| Question | Service |
| --- | --- |
| What's happening? | CloudWatch |
| Who did it? | CloudTrail |
| What changed? | Config |
| Build infrastructure? | CloudFormation |
| Manage systems? | Systems Manager |
| How can I improve? | Trusted Advisor |

---

## Scenario Speed Round

CPU utilization?

→ CloudWatch

Metrics and alarms?

→ CloudWatch

API activity?

→ CloudTrail

Who deleted a resource?

→ CloudTrail

Configuration history?

→ Config

Compliance tracking?

→ Config

Infrastructure as Code?

→ CloudFormation

Templates?

→ CloudFormation

Patch servers?

→ Systems Manager

Run commands across servers?

→ Systems Manager

Best-practice recommendations?

→ Trusted Advisor

Cost + Performance + Security recommendations?

→ Trusted Advisor

---

## Final Exam Memory

WATCH = CloudWatch

WHO = CloudTrail

CHANGE = Config

BUILD = CloudFormation

MANAGE = Systems Manager

ADVISE = Trusted Advisor
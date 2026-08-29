## Monitoring Services Comparison

| Service | Primary Purpose | Memory Shortcut |
| --- | --- | --- |
| CloudWatch | Monitor resources | Metrics & alarms |
| CloudTrail | API activity | Who did what |
| Config | Resource configuration history | What changed |
| CloudFormation | Infrastructure as Code | Build with templates |
| Systems Manager | Operations management | Manage systems |
| Trusted Advisor | Best-practice recommendations | AWS consultant |

---

## Key Differences

### CloudWatch

Monitors AWS resources and applications.

Think:

Metrics

Logs

Alarms

→ CloudWatch

### Memory Trick

CloudWatch = WATCH

---

### CloudTrail

Records AWS API activity and account actions.

Think:

Who performed an action?

What API call occurred?

→ CloudTrail

### Memory Trick

CloudTrail = WHO DID WHAT?

---

### Config

Tracks resource configurations and changes over time.

Think:

What changed?

Is the resource compliant?

→ Config

### Memory Trick

Config = CONFIGURATION HISTORY

---

### CloudFormation

Defines and deploys AWS infrastructure using code and templates.

Think:

Infrastructure as Code

Templates

Automated deployment

→ CloudFormation

### Memory Trick

CloudFormation = BUILD

---

### Systems Manager

Manages systems and operational tasks at scale.

Think:

Patching

Run commands

Manage servers

→ Systems Manager

### Memory Trick

Systems Manager = MANAGE

---

### Trusted Advisor

Analyzes your AWS account and provides best-practice recommendations.

Think:

Cost

Performance

Security

Fault Tolerance

Service Limits

Operational Excellence

→ Trusted Advisor

### Memory Trick

Trusted Advisor = ADVISE

---

## Common Exam Confusion

| If the Question Says... | Think... |
| --- | --- |
| Metrics | CloudWatch |
| Alarms | CloudWatch |
| Monitor CPU utilization | CloudWatch |
| API calls | CloudTrail |
| Who deleted a resource? | CloudTrail |
| Who performed an action? | CloudTrail |
| Configuration history | Config |
| Compliance | Config |
| How did a resource change? | Config |
| Infrastructure as Code | CloudFormation |
| Templates | CloudFormation |
| Deploy infrastructure | CloudFormation |
| Patch servers | Systems Manager |
| Run commands across servers | Systems Manager |
| Manage systems at scale | Systems Manager |
| Best-practice recommendations | Trusted Advisor |
| Optimize AWS environment | Trusted Advisor |
| AWS account assessment | Trusted Advisor |

---

## The Big Six

CloudWatch = WATCH

CloudTrail = WHO DID IT

Config = WHAT CHANGED

CloudFormation = BUILD

Systems Manager = MANAGE

Trusted Advisor = ADVISE

---

## Scenario Practice

Need to monitor EC2 CPU utilization?

→ CloudWatch

Need to determine who deleted an AWS resource?

→ CloudTrail

Need to see how a resource's configuration changed over time?

→ Config

Need to deploy infrastructure using templates?

→ CloudFormation

Need to patch thousands of servers?

→ Systems Manager

Need AWS recommendations for improving cost, security, or performance?

→ Trusted Advisor

---

## Ultimate Memory Pattern

WATCH → CloudWatch

WHO → CloudTrail

CHANGE → Config

BUILD → CloudFormation

MANAGE → Systems Manager

ADVISE → Trusted Advisor
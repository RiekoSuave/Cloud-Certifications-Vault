## What Problem Does It Solve?

[[Config]] helps you:

**Track, evaluate, and audit the configuration of AWS resources over time**

It helps answer questions such as:

- What does this resource look like now?
- What did its configuration look like yesterday?
- When did its configuration change?
- Is the resource compliant with our rules?
- Which resources violate our required configuration?

Architecture:

AWS Resources  
↓  
Config  
↓  
Configuration History  
↓  
Config Rules  
↓  
Compliant / Noncompliant

> [!tip] Memory Trick
> **Config = WHAT is it configured like?**

---

## Core Concept

Config continuously records:

**Resource configuration changes**

and can evaluate those resources against:

**Desired configuration rules**

Think:

Resource  
↓  
Configuration Recorded  
↓  
Rule Evaluation  
↓  
Compliant / Noncompliant

### Killer Exam Clue

> **Need to track resource configuration and evaluate compliance over time**
>
> → **Config**

---

# Configuration Items

A:

**Configuration Item**

represents a point-in-time view of:

**A supported AWS resource's configuration**

It can include information about:

- Resource attributes
- Relationships
- Configuration
- Changes

### Memory Trick

**Configuration Item = Resource Snapshot**

---

# Configuration History

Config maintains:

**Configuration history**

so you can see:

**How a resource changed over time**

Example:

Monday  
↓  
S3 Bucket = Private

Tuesday  
↓  
Bucket Policy Changed

Wednesday  
↓  
S3 Bucket = Public

Config provides visibility into:

**That configuration timeline**

### Killer Exam Clue

> **Determine how a resource's configuration changed over time**
>
> → **Config**

---

# Configuration Timeline

The:

**Configuration Timeline**

provides a historical view of:

- Resource configuration changes
- Relationships
- Compliance changes

This is useful for:

**Auditing and troubleshooting**

---

# Resource Relationships

Config can track relationships between:

**AWS resources**

Example:

EC2 Instance  
↓  
Security Group  
↓  
VPC

This helps understand:

**How infrastructure components are connected**

---

# Config Rules

**Config Rules**

evaluate resource configurations against:

**Desired conditions**

Example:

Requirement:

S3 buckets must not be publicly accessible.

Config Rule  
↓  
Evaluate Bucket  
↓  
COMPLIANT / NONCOMPLIANT

### Killer Exam Clue

> **Continuously check whether AWS resources meet configuration requirements**
>
> → **Config Rules**

---

# Managed Rules

AWS provides:

**Managed Config Rules**

for common compliance checks.

Examples conceptually include:

- S3 buckets should not be public
- EBS volumes should be encrypted
- Required tags should exist
- Security groups should meet requirements

### Memory Trick

**Managed Rule = AWS Already Built the Check**

---

# Custom Rules

If a managed rule does not meet the requirement, you can create:

**Custom Config Rules**

Custom evaluation logic can use:

[[Lambda]]

### Killer Exam Clue

> **Need organization-specific configuration compliance logic**
>
> → **Custom Config Rule**

---

# Compliance States

Resources evaluated by Config rules can be classified as:

- COMPLIANT
- NON_COMPLIANT
- NOT_APPLICABLE
- INSUFFICIENT_DATA

For SAA, focus primarily on:

**COMPLIANT vs NON_COMPLIANT**

---

# Config Is Not Preventive

This is a major exam concept.

Config primarily:

**Detects and evaluates configuration**

It does NOT inherently prevent:

**The configuration change from occurring**

Example:

User makes S3 bucket public  
↓  
Config detects change  
↓  
Rule evaluates bucket  
↓  
NON_COMPLIANT

### Exam Trap

> **Config detects noncompliance after/when configuration is evaluated.**
>
> It is not itself an IAM-style preventive access-control mechanism.

---

# Config Remediation

Config rules can be associated with:

**Remediation actions**

to correct:

**Noncompliant resources**

A common mechanism is:

[[Systems Manager]] Automation

Architecture:

Resource Changes  
↓  
Config Rule  
↓  
NON_COMPLIANT  
↓  
Systems Manager Automation  
↓  
Remediation

### Killer Exam Clue

> **Automatically correct a resource after Config detects noncompliance**
>
> → **Config Rule + Automatic Remediation**

---

# Manual Remediation

Remediation can also require:

**Manual execution**

when automatic changes would be inappropriate.

Use when:

- Human approval is desired
- Change risk is high
- Investigation should occur first

---

# Example — Public S3 Bucket

Requirement:

**S3 buckets must remain private**

Architecture:

Bucket Policy Changed  
↓  
Config  
↓  
Rule Evaluation  
↓  
NON_COMPLIANT  
↓  
Remediation  
↓  
Remove Public Access

### Memory Trick

**Config Detects → Remediation Corrects**

---

# Example — Unencrypted EBS

Requirement:

**EBS volumes must be encrypted**

Config Rule  
↓  
Evaluate EBS  
↓  
Encrypted?

YES  
→ COMPLIANT

NO  
→ NON_COMPLIANT

---

# Example — Required Tags

Organization requires:

`Environment`

and:

`Owner`

tags.

Config can evaluate whether resources meet:

**Required tagging policies**

### Killer Exam Clue

> **Continuously identify resources missing required tags**
>
> → **Config Rule**

---

# Conformance Packs

A:

**Conformance Pack**

is a collection of:

**Config rules and remediation actions**

that can be deployed together.

Useful for:

- Compliance frameworks
- Organizational standards
- Repeated governance requirements

### Memory Trick

**Conformance Pack = Compliance Rules Pack**

---

# Multi-Account Governance

Config can be used across:

**Multiple AWS accounts**

to centralize:

**Compliance visibility**

This is especially useful with:

**AWS Organizations**

---

# Aggregators

A:

**Configuration Aggregator**

collects Config information from:

- Multiple accounts
- Multiple Regions

into:

**A centralized view**

### Killer Exam Clue

> **Security team needs centralized Config compliance visibility across accounts and Regions**
>
> → **Configuration Aggregator**

### Memory Trick

**Aggregator = Bring Config Results Together**

---

# Multi-Region Monitoring

AWS resources can exist across:

**Multiple Regions**

Config can aggregate configuration and compliance information to provide:

**Centralized governance**

---

# Config + Organizations

In a multi-account environment:

AWS Organizations  
↓  
Member Accounts  
↓  
Config  
↓  
Configuration Aggregator  
↓  
Central Security / Governance Account

This helps organizations:

**Monitor compliance at scale**

---

# Config + SNS

Config can integrate with:

[[SNS]]

to send notifications about:

**Configuration changes**

Architecture:

Resource Change  
↓  
Config  
↓  
SNS  
↓  
Subscriber

---

# Config + S3

Configuration history and snapshots can be delivered to:

[[S3]]

for:

- Long-term storage
- Auditing
- Compliance
- Historical analysis

### Memory Trick

**Config Tracks**

**S3 Retains**

---

# Config + CloudTrail

[[CloudTrail]] and Config answer:

**Different questions**

Example:

An S3 bucket becomes public.

Config answers:

> **What changed about the bucket configuration?**

CloudTrail answers:

> **Who made the API call that changed it?**

### Killer Architecture

Config  
→ Detect configuration change

CloudTrail  
→ Identify responsible API activity

Together:

**WHAT changed + WHO changed it**

---

# Config + CloudWatch

[[CloudWatch]] focuses on:

**Operational performance**

Config focuses on:

**Resource configuration**

Example:

EC2 CPU = 95%

→ CloudWatch

EC2 security group allows `0.0.0.0/0`

→ Config

---

# Config + Systems Manager

A powerful governance architecture:

Config  
↓  
Detect Noncompliance  
↓  
[[Systems Manager]] Automation  
↓  
Remediate Resource

### Killer Exam Clue

> **Automatically remediate noncompliant AWS resources**
>
> → **Config + Systems Manager Automation**

---

# Config vs CloudWatch

## [[CloudWatch]]

Answers:

> **How is it running?**

Think:

- CPU
- Latency
- Errors
- Metrics
- Alarms

## Config

Answers:

> **How is it configured?**

Think:

- Security group rules
- Encryption settings
- Public access
- Required tags
- Configuration history

### Memory Trick

**CloudWatch = PERFORMANCE**

**Config = CONFIGURATION**

---

# Config vs CloudTrail

## [[CloudTrail]]

Answers:

> **Who did what?**

## Config

Answers:

> **What changed?**

Example:

Security group changed.

CloudTrail:

**Who called the API?**

Config:

**What does the security group configuration look like now and historically?**

### Killer Shortcut

**WHO**
→ CloudTrail

**WHAT CONFIGURATION**
→ Config

---

# Config vs IAM

## [[IAM]]

Think:

**Permissions**

IAM can prevent:

**Unauthorized API actions**

## Config

Think:

**Configuration compliance**

Config can identify:

**Resources that violate configuration requirements**

### Exam Trap

Need to:

**Prevent a user from disabling encryption**

→ IAM / SCP / appropriate preventive control

Need to:

**Detect resources without encryption**

→ Config

---

# Config vs Service Control Policies

SCPs can:

**Restrict what actions accounts can perform**

Config:

**Evaluates resource configuration**

### Memory Trick

**SCP = Prevent**

**Config = Detect**

---

# Config vs Security Hub

Config provides:

**Resource configuration evaluation**

Security Hub provides:

**Centralized security findings and security posture management**

Config rules can contribute to:

**Broader security/compliance architectures**

---

# Config vs Trusted Advisor

Config:

**Continuously evaluates resource configuration against rules**

Trusted Advisor:

**Provides AWS best-practice recommendations**

Think:

Config  
→ Configuration compliance

Trusted Advisor  
→ Best-practice guidance

---

# Configuration Recorder

Config uses a:

**Configuration Recorder**

to detect and record:

**Supported resource configurations**

It determines which supported resource types are:

**Recorded**

### Exam Principle

> **Config must record the relevant resource type for its configuration changes to be tracked**

---

# Delivery Channel

Config can use a:

**Delivery Channel**

to deliver configuration information to:

**S3**

and notifications through:

**SNS**

Think:

Recorder  
→ Records

Delivery Channel  
→ Delivers

### Memory Trick

**Recorder = Watch**

**Delivery Channel = Send**

---

# Periodic vs Change-Triggered Rules

Config rules can evaluate resources:

**When configuration changes**

or:

**Periodically**

depending on the rule.

### Change-Triggered

Resource changes  
↓  
Evaluate

### Periodic

Schedule  
↓  
Evaluate

### Killer Exam Clue

> **Check compliance on a recurring schedule even without a resource change**
>
> → **Periodic Config Rule**

---

# Architecture Thinking

## Scenario 1 — Public S3 Bucket

Security team needs to identify:

**Any S3 bucket that becomes public**

Choose:

**Config Rule**

---

## Scenario 2 — Who Made Bucket Public?

Need identity responsible for:

**Changing the bucket policy**

Choose:

**CloudTrail**

not Config alone.

---

## Scenario 3 — Bucket Configuration History

Need to determine:

**What the bucket policy looked like three days ago**

Choose:

**Config**

---

## Scenario 4 — EC2 CPU

Need alert when:

**CPU > 90%**

Choose:

**CloudWatch**

not Config.

---

## Scenario 5 — Missing Encryption

Need continuously identify:

**Unencrypted EBS volumes**

Choose:

**Config Rule**

---

## Scenario 6 — Automatic Correction

Need to automatically remediate:

**A noncompliant resource**

Choose:

Config Rule  
↓  
Systems Manager Automation

---

## Scenario 7 — Custom Company Policy

Company requires:

**A unique internal resource configuration standard**

No managed rule exists.

Choose:

**Custom Config Rule**

---

## Scenario 8 — Multi-Account Compliance

Security team manages:

50 AWS accounts across multiple Regions.

Need one centralized compliance view.

Choose:

**Configuration Aggregator**

---

## Scenario 9 — Prevent API Action

Need to prevent member accounts from:

**Disabling a required security service**

Config alone is not enough.

Think:

**SCP / IAM preventive control**

---

## Scenario 10 — Compliance Package

Company needs to deploy:

**A standardized collection of compliance rules**

across environments.

Choose:

**Conformance Pack**

---

# Scenario Recognition

Immediately think:

**Config**

when you see:

- Configuration history
- Resource compliance
- Configuration changes
- Compliance rules
- Required tags
- Encryption compliance
- Public resource detection
- Resource relationships
- Configuration timeline

---

## Think Config Rules When You See

- Compliant
- Noncompliant
- Evaluate configuration
- Required configuration

---

## Think Remediation When You See

- Automatically fix
- Correct noncompliant resource
- Systems Manager Automation

---

## Think Configuration Aggregator When You See

- Multiple accounts
- Multiple Regions
- Centralized compliance view

---

## Think Conformance Packs When You See

- Group of compliance rules
- Compliance framework
- Standardized governance package

---

# Exam Traps

## Trap 1 — Config Shows EC2 CPU Utilization

❌

Think:

**CloudWatch**

---

## Trap 2 — Config Tells You Who Changed the Security Group

❌

Think:

**CloudTrail**

Config tells you:

**How the configuration changed**

---

## Trap 3 — Config Automatically Prevents Every Noncompliant Change

❌

Config primarily:

**Detects and evaluates**

Use:

**Remediation**

to correct detected noncompliance.

---

## Trap 4 — Config Is the Same as IAM

❌

IAM:

**Permissions**

Config:

**Configuration compliance**

---

## Trap 5 — Config Only Works in One Account

❌

Configuration Aggregators can provide:

**Multi-account / multi-Region visibility**

---

## Trap 6 — Config Rules Must Always Be AWS Managed

❌

You can create:

**Custom Rules**

---

## Trap 7 — Conformance Pack Is One Config Rule

❌

It is a:

**Collection of rules and remediation actions**

---

# Quick Cheat Sheet

| Exam Clue | Answer |
|---|---|
| Resource Configuration History | Config |
| Configuration Compliance | Config |
| Evaluate Resource | Config Rule |
| AWS-Built Compliance Check | Managed Rule |
| Custom Compliance Logic | Custom Rule |
| Automatically Fix Noncompliance | Remediation |
| Remediation Workflow | Systems Manager Automation |
| Compliance Rule Collection | Conformance Pack |
| Multi-Account/Region Compliance View | Configuration Aggregator |
| Who Changed Resource? | CloudTrail |
| Resource Performance | CloudWatch |
| Prevent Unauthorized Action | IAM / SCP |
| Store Configuration History | S3 |
| Configuration Notifications | SNS |

---

# Monitoring Decision Map

Need:

**CPU / latency / metrics**

→ CloudWatch

Need:

**Who performed API action**

→ CloudTrail

Need:

**Resource configuration history**

→ Config

Need:

**Configuration compliance**

→ Config Rule

Need:

**Automatically fix noncompliance**

→ Config + Systems Manager

Need:

**Prevent action before it happens**

→ IAM / SCP

---

# The Big Three

| Question | Service |
|---|---|
| How is it running? | [[CloudWatch]] |
| Who did it? | [[CloudTrail]] |
| How is it configured? | Config |

### Killer Memory Trick

> **WATCH**
> → PERFORMANCE
>
> **TRAIL**
> → HISTORY / WHO
>
> **CONFIG**
> → CONFIGURATION

---

# Final Exam Rapid-Fire

> **RESOURCE CONFIGURATION**
> → CONFIG
>
> **CONFIGURATION HISTORY**
> → CONFIG
>
> **COMPLIANT / NONCOMPLIANT**
> → CONFIG RULE
>
> **AWS-BUILT RULE**
> → MANAGED RULE
>
> **CUSTOM COMPLIANCE LOGIC**
> → CUSTOM RULE
>
> **AUTO-FIX**
> → REMEDIATION
>
> **REMEDIATION ENGINE**
> → SYSTEMS MANAGER AUTOMATION
>
> **GROUP OF RULES**
> → CONFORMANCE PACK
>
> **MULTI-ACCOUNT COMPLIANCE**
> → CONFIGURATION AGGREGATOR
>
> **WHO CHANGED IT**
> → CLOUDTRAIL
>
> **CPU / LATENCY**
> → CLOUDWATCH
>
> **PREVENT ACTION**
> → IAM / SCP

---

## Master Memory Trick

> [!tip] Config Master Memory Trick
> Imagine AWS infrastructure has:
>
> **A building inspector**
>
> The inspector walks around checking:
>
> **Is this S3 bucket private?**
>
> **Is this EBS volume encrypted?**
>
> **Does this resource have the required tags?**
>
> **Is this security group configured correctly?**
>
> The inspector is:
>
> **CONFIG**
>
> The inspector compares everything against:
>
> **CONFIG RULES**
>
> If something fails:
>
> **NONCOMPLIANT**
>
> If it passes:
>
> **COMPLIANT**
>
> If you want the inspector to call someone to fix the problem:
>
> **REMEDIATION**
>
> But if you ask:
>
> **"WHO made this bucket public?"**
>
> go to:
>
> **CLOUDTRAIL**
>
> If you ask:
>
> **"Why is this server running slowly?"**
>
> go to:
>
> **CLOUDWATCH**

So remember:

> **CLOUDWATCH**
> → HOW IS IT RUNNING?
>
> **CLOUDTRAIL**
> → WHO DID IT?
>
> **CONFIG**
> → HOW IS IT CONFIGURED?
>
> **CONFIG RULE**
> → IS IT COMPLIANT?
>
> **REMEDIATION**
> → FIX IT
>
> **AGGREGATOR**
> → SEE EVERYTHING TOGETHER

And the killer SAA question:

> **"Does the question ask whether AWS resources have the correct configuration or whether their configuration changed over time?"**
>
> YES
>
> → **Config**

---

## Related Notes

- [[CloudWatch]]
- [[CloudTrail]]
- [[Systems Manager]]
- [[Lambda]]
- [[SNS]]
- [[S3]]
- [[IAM]]
- [[06-Security/Security Hub]]
## Core Exam Map

> [!tip] Master Shortcut
> **Metrics / Logs / Alarms** → [[CloudWatch]]
>
> **Who performed an AWS API action?** → [[CloudTrail]]
>
> **Resource configuration / compliance** → [[Config]]
>
> **Distributed application tracing** → [[X-Ray]]
>
> **Network traffic metadata** → [[05-Networking/VPC Flow Logs]]
>
> **Event routing / automation** → [[EventBridge]]

---

# CloudWatch

Think:

**Operational monitoring**

Use it for:

- Metrics
- Logs
- Alarms
- Dashboards
- Application monitoring
- Resource performance

### Killer Exam Clues

- CPU utilization
- Metrics
- Threshold alarm
- Application logs
- Operational dashboard
- Resource performance

### Exam Shortcut

> **"How is my AWS resource performing?"**
>
> → **CloudWatch**

### Memory Trick

**CloudWatch = HOW IS IT RUNNING?**

---

# CloudWatch Metrics

Think:

**Numbers over time**

Examples:

- CPUUtilization
- RequestCount
- Errors
- Invocations
- DatabaseConnections

### Killer Shortcut

**Numeric measurement**
→ CloudWatch Metric

---

# EC2 Monitoring

## Basic Monitoring

Common EC2 metric interval:

**5 minutes**

## Detailed Monitoring

Common EC2 metric interval:

**1 minute**

### Memory Trick

**Basic = 5**

**Detailed = 1**

---

# CloudWatch Agent

Use the:

**CloudWatch Agent**

when you need operating-system-level information such as:

- EC2 memory utilization
- Disk utilization
- System logs
- Application logs

### Killer Exam Clue

> **Need EC2 RAM utilization**
>
> → **CloudWatch Agent**

### Memory Trick

**OS Data = Agent**

---

# Custom Metrics

Use:

**Custom Metrics**

for application-specific measurements.

Examples:

- OrdersProcessed
- FailedPayments
- ActiveUsers

### Killer Shortcut

**AWS doesn't provide the metric?**
→ Publish Custom Metric

---

# CloudWatch Alarms

Think:

**Metric crosses condition → Take action**

Architecture:

Metric  
↓  
Alarm  
↓  
Action

Possible actions include:

- SNS notification
- Auto Scaling
- EC2 action

### Killer Exam Clue

> **Notify operations when CPU exceeds 80%**
>
> → **CloudWatch Alarm + SNS**

---

# Composite Alarms

Combine:

**Multiple alarms**

into:

**One higher-level alarm**

Useful for:

**Reducing alarm noise**

### Killer Shortcut

**Alert only when multiple alarm conditions are met**
→ Composite Alarm

---

# CloudWatch Logs

Think:

**Application and system log storage**

Examples:

- Lambda logs
- Application logs
- System logs

### Structure

CloudWatch Logs  
↓  
Log Group  
↓  
Log Stream  
↓  
Log Events

### Memory Trick

**Group = Collection**

**Stream = Source**

---

# Metric Filters

Convert:

**Log patterns**

into:

**Metrics**

Architecture:

CloudWatch Logs  
↓  
Metric Filter  
↓  
Metric  
↓  
Alarm

### Killer Exam Clue

> **Alarm when `ERROR` appears repeatedly in application logs**
>
> → **Metric Filter + Alarm**

### Memory Trick

**LOG → FILTER → METRIC → ALARM**

---

# CloudWatch Logs Insights

Use:

**Logs Insights**

to interactively:

**Search and analyze CloudWatch Logs**

### Killer Shortcut

**Query logs in CloudWatch**
→ Logs Insights

**Query logs/files in S3**
→ [[Athena]]

---

# CloudWatch Dashboards

Think:

**Visual operational monitoring**

Use dashboards to display:

- Metrics
- Alarms
- Application health
- Resource performance

---

# Anomaly Detection

CloudWatch:

**Anomaly Detection**

learns expected metric behavior and identifies:

**Unusual patterns**

### Killer Shortcut

Fixed threshold  
→ CloudWatch Alarm

Dynamic unusual behavior  
→ Anomaly Detection

### Memory Trick

**Threshold = Fixed**

**Anomaly = Weird**

---

# Contributor Insights

Use:

**Contributor Insights**

to identify:

**Top contributors**

Example:

Which DynamoDB partition key generates:

**The most traffic?**

### Killer Exam Clue

> **Identify hot DynamoDB keys**
>
> → **Contributor Insights**

---

# CloudWatch Synthetics

Uses:

**Canaries**

to simulate:

**User interactions**

Examples:

- Check website availability
- Test API
- Test login
- Test checkout

### Memory Trick

**Synthetics = Fake User**

---

# CloudWatch RUM

**Real User Monitoring**

observes:

**Actual users**

Use for:

- Browser performance
- Page load experience
- Client-side errors
- User experience

### Memory Trick

**RUM = Real User**

---

# Synthetics vs RUM

| Requirement | Answer |
|---|---|
| Simulated User | Synthetics |
| Canary | Synthetics |
| Real User | RUM |
| Browser/User Experience | RUM |

---

# CloudTrail

Think:

**AWS API audit history**

CloudTrail answers:

> **WHO DID WHAT?**

Records information such as:

- API call
- IAM identity
- Timestamp
- Source IP
- Region

### Killer Exam Clues

- Who deleted resource?
- Who changed security group?
- Who modified IAM?
- API history
- Audit
- Root activity

### Memory Trick

**CloudTrail = WHO DID IT?**

---

# CloudTrail Management Events

Think:

**Operations on AWS resources**

Examples:

- Create resource
- Delete resource
- Modify configuration

### Memory Trick

**Management = Resource Control**

---

# CloudTrail Data Events

Think:

**Operations on data inside resources**

Important examples:

- S3 object-level activity
- Lambda invocation activity

### Killer Exam Clue

> **Who accessed a specific S3 object?**
>
> → **CloudTrail Data Events**

### Memory Trick

**Management = Resource**

**Data = Inside Resource**

---

# CloudTrail Event History

Use:

**Event History**

for:

**Recent management event investigation**

### Killer Shortcut

**Quick recent API investigation**
→ Event History

---

# CloudTrail Trail

Use a:

**Trail**

for:

**Long-term API audit logging**

Architecture:

AWS API Activity  
↓  
CloudTrail  
↓  
S3

### Killer Shortcut

**Long-term audit retention**
→ Trail → S3

---

# Organization Trail

Think:

**Centralized CloudTrail auditing across AWS accounts**

Architecture:

AWS Organizations  
↓  
Accounts  
↓  
Organization Trail  
↓  
Central S3

### Killer Exam Clue

> **Audit API activity across every AWS account**
>
> → **Organization Trail**

---

# CloudTrail Lake

Think:

**Query CloudTrail events**

Use for:

- Audit investigation
- Event analysis
- Long-term CloudTrail querying

### Killer Shortcut

CloudTrail event analytics  
→ CloudTrail Lake

CloudTrail files in S3  
→ Athena

---

# Log File Integrity Validation

Use:

**Log File Integrity Validation**

when you need to verify:

**CloudTrail logs were not altered**

### Memory Trick

**Integrity = Prove the Evidence Wasn't Changed**

---

# Config

Think:

**Resource configuration + compliance**

Config answers:

> **HOW IS IT CONFIGURED?**

Use for:

- Configuration history
- Compliance evaluation
- Resource relationships
- Configuration changes

### Killer Exam Clues

- S3 bucket public?
- EBS encrypted?
- Required tags?
- Configuration history?
- Compliant or noncompliant?

### Memory Trick

**Config = CONFIGURATION**

---

# Config Rules

Evaluate:

**Resource configuration**

against:

**Desired requirements**

Result:

COMPLIANT

or:

NONCOMPLIANT

### Killer Shortcut

**Continuously evaluate resource configuration**
→ Config Rule

---

# Managed vs Custom Rules

## Managed Rule

AWS provides:

**The compliance logic**

## Custom Rule

You define:

**Organization-specific logic**

Custom logic can use:

[[Lambda]]

### Memory Trick

**Managed = AWS Built**

**Custom = You Build**

---

# Config Remediation

Architecture:

Config Rule  
↓  
NONCOMPLIANT  
↓  
Remediation  
↓  
[[Systems Manager]] Automation  
↓  
Correct Resource

### Killer Exam Clue

> **Automatically fix a noncompliant resource**
>
> → **Config Remediation**

### Memory Trick

**Config Detects**

**Remediation Fixes**

---

# Configuration Aggregator

Collects Config information from:

- Multiple accounts
- Multiple Regions

into:

**One centralized view**

### Killer Exam Clue

> **Central compliance visibility across accounts and Regions**
>
> → **Configuration Aggregator**

---

# Conformance Packs

Think:

**Collection of Config rules and remediation actions**

Useful for:

- Compliance frameworks
- Organizational standards
- Repeatable governance

### Memory Trick

**Conformance Pack = Compliance Pack**

---

# X-Ray

Think:

**Distributed tracing**

X-Ray answers:

> **WHERE DID THE REQUEST GO?**

Use for:

- Microservices
- Request tracing
- Latency analysis
- Dependency visualization
- Distributed applications

### Killer Exam Clues

- Trace request
- Microservices latency
- Service dependencies
- Service map
- Segment
- Subsegment

### Memory Trick

**X-Ray = See Inside the Request**

---

# X-Ray Trace

A:

**Trace**

represents:

**The entire request journey**

Trace  
↓  
Segments  
↓  
Subsegments

### Memory Trick

**Trace = Whole Journey**

**Segment = One Service**

**Subsegment = Work Inside Service**

---

# X-Ray Service Map

Provides:

**Visual application dependencies**

Example:

API Gateway  
↓  
Lambda  
↓  
DynamoDB

### Killer Exam Clue

> **Visualize microservice dependencies**
>
> → **X-Ray Service Map**

---

# X-Ray Annotations

Annotations are:

**Indexed**

and can be used to:

**Search/filter traces**

### Memory Trick

**Annotation = Searchable**

---

# X-Ray Metadata

Metadata stores:

**Additional trace information**

but is:

**Not indexed**

### Memory Trick

**Metadata = Extra Detail**

---

# X-Ray Sampling

Use:

**Sampling**

to control:

**How many requests are traced**

This reduces:

- Trace volume
- Overhead
- Cost

### Killer Exam Clue

> **Trace only a representative subset of requests**
>
> → **Sampling**

---

# CloudWatch vs CloudTrail vs Config vs X-Ray

| Question | Service |
|---|---|
| How is it running? | [[CloudWatch]] |
| Who did it? | [[CloudTrail]] |
| How is it configured? | [[Config]] |
| Where did the request go? | [[X-Ray]] |

### Master Memory Trick

> **WATCH**
> → PERFORMANCE
>
> **TRAIL**
> → ACTIVITY
>
> **CONFIG**
> → CONFIGURATION
>
> **X-RAY**
> → REQUEST

---

# Metrics vs Logs vs Traces

| Data | Think |
|---|---|
| Metric | Number |
| Log | Message |
| Trace | Request Journey |

### AWS Mapping

**Metrics**
→ CloudWatch

**Logs**
→ CloudWatch Logs

**Traces**
→ X-Ray

---

# CloudTrail vs Config

This comparison is extremely important.

Scenario:

An S3 bucket becomes public.

## Config

Answers:

> **The bucket became public.**

## CloudTrail

Answers:

> **This IAM user/role called the API that changed it.**

### Killer Shortcut

**WHAT changed?**
→ Config

**WHO changed it?**
→ CloudTrail

---

# CloudWatch vs X-Ray

Scenario:

Checkout requests take:

**8 seconds**

CloudWatch tells you:

**Latency is high**

X-Ray tells you:

**Which service consumed the 8 seconds**

### Killer Shortcut

**Something is slow**
→ CloudWatch

**Where is it slow?**
→ X-Ray

---

# Config vs Preventive Controls

Config is primarily:

**Detective**

It evaluates:

**Configuration compliance**

If the requirement is:

**Prevent the action before it happens**

think about preventive controls such as:

- [[IAM]]
- SCPs

### Memory Trick

**IAM / SCP = Prevent**

**Config = Detect**

**Remediation = Correct**

---

# EventBridge

[[EventBridge]] is already covered in its dedicated note.

For monitoring scenarios, remember only:

**EventBridge = Event Routing**

Example:

AWS Event  
↓  
EventBridge  
↓  
Lambda

### Killer Shortcut

**React to AWS event**
→ EventBridge

**React to metric threshold**
→ CloudWatch Alarm

---

# VPC Flow Logs

[[05-Networking/VPC Flow Logs]] will be covered in the VPC section.

For monitoring questions, remember:

**VPC Flow Logs = Network Traffic Metadata**

Use them to analyze:

- Accepted traffic
- Rejected traffic
- Source/destination IP
- Ports
- Network communication

### Killer Shortcut

**AWS API activity**
→ CloudTrail

**Network traffic**
→ VPC Flow Logs

---

# Architecture Scenario 1 — High CPU

Requirement:

Notify administrator when:

EC2 CPU > 80%

Choose:

CloudWatch Metric  
↓  
Alarm  
↓  
SNS

---

# Architecture Scenario 2 — EC2 Memory

Requirement:

Monitor:

**RAM utilization**

Choose:

CloudWatch Agent  
↓  
CloudWatch

---

# Architecture Scenario 3 — Application Errors

Requirement:

Alert when logs contain:

`ERROR`

Choose:

CloudWatch Logs  
↓  
Metric Filter  
↓  
Metric  
↓  
Alarm

---

# Architecture Scenario 4 — Who Deleted EC2?

Requirement:

Identify:

- IAM principal
- API call
- Timestamp
- Source IP

Choose:

**CloudTrail**

---

# Architecture Scenario 5 — Who Downloaded S3 Object?

Requirement:

Audit:

**Object-level S3 activity**

Choose:

**CloudTrail Data Events**

---

# Architecture Scenario 6 — Public Bucket

Requirement:

Continuously determine whether:

**S3 bucket is public**

Choose:

**Config Rule**

---

# Architecture Scenario 7 — Auto-Fix Public Bucket

Requirement:

Detect and automatically correct:

**Public S3 bucket**

Choose:

Config Rule  
↓  
Remediation  
↓  
Systems Manager Automation

---

# Architecture Scenario 8 — Slow Microservice

Requirement:

Find which service causes:

**Application latency**

Choose:

**X-Ray**

---

# Architecture Scenario 9 — Website Health

Requirement:

AWS should simulate:

**A customer visiting the website**

Choose:

**CloudWatch Synthetics**

---

# Architecture Scenario 10 — Real Customer Performance

Requirement:

Collect browser performance from:

**Actual users**

Choose:

**CloudWatch RUM**

---

# Architecture Scenario 11 — Multi-Account Audit

Requirement:

Centralize API activity from:

**All AWS accounts**

Choose:

**CloudTrail Organization Trail**

---

# Architecture Scenario 12 — Multi-Account Compliance

Requirement:

Centralize configuration compliance from:

**Multiple accounts and Regions**

Choose:

**Config Configuration Aggregator**

---

# Exam Scenario Recognition

## CPU / Latency / Metric

→ **CloudWatch**

## EC2 RAM

→ **CloudWatch Agent**

## Threshold Alert

→ **CloudWatch Alarm**

## Log Pattern Alert

→ **Metric Filter + Alarm**

## Query CloudWatch Logs

→ **Logs Insights**

## Simulated User

→ **Synthetics**

## Real User

→ **RUM**

## Who Changed Resource?

→ **CloudTrail**

## S3 Object-Level Audit

→ **CloudTrail Data Events**

## Long-Term API Audit

→ **CloudTrail Trail → S3**

## Resource Configuration History

→ **Config**

## Compliance Evaluation

→ **Config Rule**

## Automatic Compliance Fix

→ **Config Remediation**

## Distributed Tracing

→ **X-Ray**

## Microservice Dependencies

→ **X-Ray Service Map**

## Network Traffic

→ **VPC Flow Logs**

---

# Common Exam Traps

## Trap 1 — CloudWatch Shows Who Deleted a Resource

❌

Think:

**CloudTrail**

---

## Trap 2 — CloudTrail Monitors CPU

❌

Think:

**CloudWatch**

---

## Trap 3 — Config Identifies the IAM User Who Made a Change

❌

Think:

**CloudTrail**

Config focuses on:

**The configuration**

---

## Trap 4 — X-Ray Is Used for Infrastructure CPU Monitoring

❌

Think:

**CloudWatch**

---

## Trap 5 — EC2 Memory Is Automatically Available

❌

Use:

**CloudWatch Agent**

---

## Trap 6 — Logs Insights Queries S3

❌

CloudWatch logs:

**Logs Insights**

S3:

**Athena**

---

## Trap 7 — Synthetics Observes Actual Users

❌

Synthetics:

**Fake user**

RUM:

**Real user**

---

## Trap 8 — Config Automatically Prevents Every Bad Change

❌

Config:

**Detect**

Remediation:

**Correct**

IAM/SCP:

**Prevent**

---

## Trap 9 — CloudTrail Management Events Show All S3 Object Reads

❌

Think:

**Data Events**

---

## Trap 10 — X-Ray Metadata Is Searchable

❌

Annotations:

**Indexed**

Metadata:

**Not indexed**

---

# Quick Cheat Sheet

| Exam Clue | Answer |
|---|---|
| Metrics | CloudWatch |
| Logs | CloudWatch Logs |
| Alarm | CloudWatch |
| EC2 Memory | CloudWatch Agent |
| Log → Metric | Metric Filter |
| Query CloudWatch Logs | Logs Insights |
| Unusual Metric Behavior | Anomaly Detection |
| Simulated User | Synthetics |
| Real User | RUM |
| AWS API Audit | CloudTrail |
| Object-Level S3 Audit | CloudTrail Data Events |
| Multi-Account API Audit | Organization Trail |
| Resource Configuration | Config |
| Compliance | Config Rules |
| Automatic Compliance Fix | Remediation |
| Multi-Account Compliance | Configuration Aggregator |
| Distributed Tracing | X-Ray |
| Request Dependencies | Service Map |
| Searchable Trace Attribute | Annotation |
| Network Traffic | VPC Flow Logs |
| Event Routing | EventBridge |

---

# Four-Question Exam Strategy

When you see a monitoring question, ask:

> **1. Is this about PERFORMANCE?**
>
> → CloudWatch
>
> **2. Is this about WHO performed an API action?**
>
> → CloudTrail
>
> **3. Is this about RESOURCE CONFIGURATION?**
>
> → Config
>
> **4. Is this about a REQUEST moving through an application?**
>
> → X-Ray

This resolves a huge percentage of:

**SAA monitoring questions**

---

# Final Exam Rapid-Fire

> **CPU**
> → CLOUDWATCH
>
> **RAM**
> → CLOUDWATCH AGENT
>
> **THRESHOLD**
> → CLOUDWATCH ALARM
>
> **LOG PATTERN**
> → METRIC FILTER
>
> **QUERY CLOUDWATCH LOGS**
> → LOGS INSIGHTS
>
> **UNUSUAL METRIC**
> → ANOMALY DETECTION
>
> **FAKE USER**
> → SYNTHETICS
>
> **REAL USER**
> → RUM
>
> **WHO DID IT**
> → CLOUDTRAIL
>
> **OBJECT-LEVEL S3 AUDIT**
> → CLOUDTRAIL DATA EVENTS
>
> **LONG-TERM API LOG**
> → TRAIL → S3
>
> **MULTI-ACCOUNT AUDIT**
> → ORGANIZATION TRAIL
>
> **RESOURCE CONFIG**
> → CONFIG
>
> **COMPLIANCE**
> → CONFIG RULE
>
> **AUTO-FIX**
> → REMEDIATION
>
> **MULTI-ACCOUNT COMPLIANCE**
> → CONFIGURATION AGGREGATOR
>
> **DISTRIBUTED TRACE**
> → X-RAY
>
> **DEPENDENCY MAP**
> → X-RAY SERVICE MAP
>
> **NETWORK TRAFFIC**
> → VPC FLOW LOGS
>
> **EVENT ROUTING**
> → EVENTBRIDGE

---

## Master Memory Trick

> [!tip] Monitoring Master Memory Trick
> Imagine you're investigating an AWS application.
>
> First you ask:
>
> **"Is the server healthy?"**
>
> Look at:
>
> **CLOUDWATCH**
>
> Then you discover:
>
> **Someone changed something.**
>
> Ask:
>
> **"WHO DID IT?"**
>
> Look at:
>
> **CLOUDTRAIL**
>
> Then you ask:
>
> **"WHAT DOES THE RESOURCE LOOK LIKE NOW?"**
>
> Look at:
>
> **CONFIG**
>
> Finally, customers say:
>
> **"The application is slow."**
>
> You need to follow their request through every microservice.
>
> Put on:
>
> **X-RAY**

So memorize:

> **CLOUDWATCH**
> → PERFORMANCE
>
> **CLOUDTRAIL**
> → ACTIVITY
>
> **CONFIG**
> → CONFIGURATION
>
> **X-RAY**
> → TRACE
>
> **VPC FLOW LOGS**
> → NETWORK
>
> **EVENTBRIDGE**
> → ROUTE EVENTS

And the master SAA shortcut:

> **HOW IS IT RUNNING?**
> → CLOUDWATCH
>
> **WHO DID IT?**
> → CLOUDTRAIL
>
> **HOW IS IT CONFIGURED?**
> → CONFIG
>
> **WHERE DID THE REQUEST GO?**
> → X-RAY

---

## Related Notes

- [[CloudWatch]]
- [[CloudTrail]]
- [[Config]]
- [[X-Ray]]
- [[05-Networking/VPC Flow Logs]]
- [[EventBridge]]
- [[SNS]]
- [[Systems Manager]]
- [[Lambda]]
- [[Athena]]
- [[IAM]]
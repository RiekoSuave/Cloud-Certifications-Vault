## What Problem Does It Solve?

[[CloudWatch]] is AWS's:

**Monitoring and observability service**

It helps monitor:

- AWS resources
- Applications
- Metrics
- Logs
- Alarms
- Events
- Dashboards

Architecture:

AWS Resources / Applications  
↓  
CloudWatch  
↓  
Metrics + Logs + Alarms  
↓  
Operations / Automation

> [!tip] Memory Trick
> **CloudWatch = What is happening RIGHT NOW?**

---

## Core Concept

CloudWatch helps answer questions such as:

- Is CPU usage too high?
- Is an application producing errors?
- Is Lambda failing?
- Is an EC2 instance unhealthy?
- Is an SQS queue backing up?
- Did a metric cross a threshold?

### Killer Exam Clue

> **Monitor AWS resources and trigger actions based on metrics**
>
> → **CloudWatch**

---

# CloudWatch Metrics

A:

**Metric**

is a time-ordered set of:

**Data points**

Examples:

- EC2 CPUUtilization
- Lambda Invocations
- Lambda Errors
- SQS ApproximateNumberOfMessagesVisible
- ALB RequestCount
- RDS DatabaseConnections

### Memory Trick

**Metric = Number over Time**

---

# Metric Example

EC2 Instance  
↓  
CPUUtilization  
↓  
CloudWatch

Example:

10:00 AM → 20%

10:05 AM → 45%

10:10 AM → 92%

CloudWatch records these values as:

**Metric data points**

---

# Namespaces

CloudWatch metrics are organized into:

**Namespaces**

A namespace groups metrics for:

**A service or application**

Examples conceptually include:

- AWS/EC2
- AWS/Lambda
- AWS/RDS

### Memory Trick

**Namespace = Metric Folder**

---

# Dimensions

A:

**Dimension**

identifies a metric using:

**Name/value pairs**

Example:

Metric:

CPUUtilization

Dimension:

InstanceId = `i-123456`

This lets CloudWatch distinguish:

**The same metric across different resources**

---

# Statistics

CloudWatch can calculate statistics such as:

- Average
- Minimum
- Maximum
- Sum
- SampleCount
- Percentiles

### Exam Example

Need to know:

**Highest CPU utilization**

→ Maximum

Need:

**Average CPU utilization**

→ Average

Need:

**Total request count**

→ Sum

---

# Standard Monitoring

EC2 provides:

**Basic monitoring**

with metrics published at a standard interval.

For many EC2 metrics:

Basic monitoring commonly provides:

**5-minute granularity**

### Killer Exam Clue

> **EC2 metrics every 5 minutes**
>
> → **Basic Monitoring**

---

# Detailed Monitoring

EC2:

**Detailed Monitoring**

provides metrics at:

**1-minute granularity**

### Killer Exam Clue

> **Need EC2 metrics every minute**
>
> → **Detailed Monitoring**

### Memory Trick

**Basic = 5**

**Detailed = 1**

---

# EC2 Memory Metrics

This is an important exam trap.

CloudWatch does NOT automatically receive:

**Operating-system memory utilization**

from a standard EC2 instance.

Why?

The EC2 hypervisor can observe:

- CPU
- Network
- Disk-level infrastructure metrics

but it does not automatically know:

**Guest OS memory usage**

### Killer Exam Clue

> **Need EC2 RAM utilization in CloudWatch**
>
> → **Install/configure the CloudWatch Agent**

---

# CloudWatch Agent

The:

**CloudWatch Agent**

can collect additional metrics and logs from:

- EC2
- On-premises servers

Examples:

- Memory usage
- Disk utilization
- Application logs
- System logs

### Memory Trick

**Need OS-Level Data? → Agent**

---

# CloudWatch Agent + EC2

Architecture:

EC2 Operating System  
↓  
CloudWatch Agent  
↓  
CloudWatch

Possible custom metrics:

- Memory %
- Disk %
- Swap usage

---

# Custom Metrics

Applications can publish:

**Custom Metrics**

to CloudWatch.

Examples:

- OrdersProcessed
- FailedPayments
- ActiveUsers
- QueueProcessingTime

### Killer Exam Clue

> **Monitor an application-specific value that AWS does not publish automatically**
>
> → **CloudWatch Custom Metric**

---

# High-Resolution Metrics

Custom metrics can support:

**High-resolution monitoring**

for measurements at intervals below:

**One minute**

This is useful for:

**Very granular monitoring requirements**

### Exam Principle

> **High-resolution custom metrics provide finer-grained monitoring but can increase cost**

---

# CloudWatch Alarms

A:

**CloudWatch Alarm**

watches a metric and reacts when:

**A threshold or condition is met**

Architecture:

Metric  
↓  
Alarm  
↓  
Action

Possible actions include:

- SNS notification
- Auto Scaling action
- EC2 action
- Automation workflow

### Killer Exam Clue

> **Take action when a metric crosses a threshold**
>
> → **CloudWatch Alarm**

---

# Alarm Example

EC2 CPUUtilization  
↓  
Greater than 80%  
↓  
For configured evaluation period  
↓  
CloudWatch Alarm  
↓  
SNS Notification

---

# Alarm States

CloudWatch alarms can have states such as:

- OK
- ALARM
- INSUFFICIENT_DATA

### Memory Trick

**OK = Fine**

**ALARM = Threshold Breached**

**INSUFFICIENT_DATA = Not Enough Information**

---

# Evaluation Period

An alarm evaluates:

**Metric data over configured periods**

Example:

CPU > 80%

for:

3 consecutive 5-minute periods

This helps avoid triggering on:

**A single brief spike**

---

# Datapoints to Alarm

CloudWatch can require:

**A certain number of breaching datapoints**

within:

**An evaluation window**

This provides flexibility such as:

3 out of 5 periods

instead of requiring:

**Every datapoint to breach**

---

# Composite Alarms

A:

**Composite Alarm**

combines the states of:

**Multiple alarms**

Example:

High CPU Alarm  
AND  
High Request Count Alarm  
↓  
Composite Alarm

This helps reduce:

**Alarm noise**

### Killer Exam Clue

> **Only alert when multiple CloudWatch alarm conditions are true**
>
> → **Composite Alarm**

---

# CloudWatch + SNS

A common architecture:

CloudWatch Metric  
↓  
Alarm  
↓  
[[SNS]]  
↓  
Email / SMS / Subscriber

### Killer Exam Clue

> **Notify operations when a metric exceeds a threshold**
>
> → **CloudWatch Alarm + SNS**

---

# CloudWatch + Auto Scaling

Architecture:

EC2 CPU  
↓  
CloudWatch Alarm  
↓  
Auto Scaling  
↓  
Add / Remove Instances

CloudWatch metrics can help drive:

**Scaling decisions**

---

# CloudWatch Logs

**CloudWatch Logs**

stores and monitors:

**Log data**

Examples:

- Application logs
- Lambda logs
- EC2 system logs
- API logs
- Custom application output

### Memory Trick

**Metrics = Numbers**

**Logs = Text / Events**

---

# Log Groups

Logs are organized into:

**Log Groups**

A log group commonly represents:

**An application or service**

Example:

`/aws/lambda/order-function`

---

# Log Streams

Within a log group are:

**Log Streams**

A stream represents:

**A sequence of log events from a particular source**

Architecture:

Log Group  
↓  
├── Log Stream A
├── Log Stream B
└── Log Stream C

### Memory Trick

**Group = Collection**

**Stream = One Source's Sequence**

---

# Lambda Logs

[[Lambda]] integrates directly with:

**CloudWatch Logs**

Architecture:

Lambda  
↓  
Execution Role  
↓  
CloudWatch Logs

The Lambda execution role requires:

**Appropriate logging permissions**

---

# EC2 Logs

EC2 application or operating-system logs are NOT automatically all sent to:

**CloudWatch Logs**

Use:

**CloudWatch Agent**

to send them.

### Killer Exam Trap

> **Need `/var/log/messages` from EC2 in CloudWatch**
>
> → **CloudWatch Agent**

---

# Log Retention

CloudWatch Logs can use:

**Retention policies**

to automatically delete logs after:

**A configured period**

This can help control:

- Storage
- Cost
- Compliance retention

---

# Log Encryption

CloudWatch Logs are encrypted at rest.

For additional control, you can use:

**KMS integration**

where supported.

---

# Metric Filters

A:

**Metric Filter**

extracts information from:

**CloudWatch Logs**

and converts matching log events into:

**CloudWatch Metrics**

Architecture:

Application Logs  
↓  
CloudWatch Logs  
↓  
Metric Filter  
↓  
Metric  
↓  
Alarm

### Killer Exam Clue

> **Create an alarm when the word `ERROR` appears repeatedly in logs**
>
> → **Metric Filter + CloudWatch Alarm**

---

# Metric Filter Example

Logs contain:

`ERROR Payment Failed`

Metric Filter detects:

`ERROR`

↓  

Custom Metric:

ErrorCount

↓  

Alarm:

ErrorCount > 10

↓  

SNS

### Memory Trick

**LOG → FILTER → METRIC → ALARM**

---

# CloudWatch Logs Insights

**CloudWatch Logs Insights**

lets you:

**Interactively query and analyze log data**

Use it to:

- Search logs
- Filter logs
- Aggregate logs
- Troubleshoot applications

### Killer Exam Clue

> **Run interactive queries against CloudWatch log data**
>
> → **CloudWatch Logs Insights**

---

# Logs Insights vs Athena

## CloudWatch Logs Insights

Think:

**Query logs already stored in CloudWatch Logs**

## [[Athena]]

Think:

**SQL query data/logs stored in S3**

### Killer Shortcut

**Logs in CloudWatch**
→ Logs Insights

**Logs in S3**
→ Athena

---

# CloudWatch Dashboards

A:

**CloudWatch Dashboard**

provides:

**Visual monitoring panels**

for:

- Metrics
- Alarms
- Operational health

Example:

Operations Dashboard  
↓  
├── EC2 CPU
├── ALB Requests
├── Lambda Errors
└── RDS Connections

---

# Cross-Region Dashboards

CloudWatch dashboards can provide visibility into:

**Metrics from multiple Regions**

This can help monitor:

**Distributed applications**

---

# Cross-Account Observability

CloudWatch supports architectures for:

**Centralized observability across AWS accounts**

This is useful in:

**AWS Organizations / multi-account environments**

### Killer Exam Clue

> **Central operations team needs visibility into monitoring data across multiple AWS accounts**
>
> → **CloudWatch cross-account observability**

---

# CloudWatch Anomaly Detection

CloudWatch can use:

**Anomaly Detection**

to establish an expected:

**Metric behavior band**

and identify unusual behavior.

Architecture:

Historical Metric Behavior  
↓  
Expected Range  
↓  
Current Metric  
↓  
Anomaly?

### Killer Exam Clue

> **Alert when a metric behaves abnormally rather than crossing a fixed threshold**
>
> → **CloudWatch Anomaly Detection**

---

# Fixed Threshold vs Anomaly Detection

## Fixed Alarm

CPU > 80%

## Anomaly Detection

Traffic is:

**Unusual compared with normal behavior**

### Memory Trick

**Threshold = Fixed Number**

**Anomaly = Unusual Pattern**

---

# CloudWatch Contributor Insights

**Contributor Insights**

helps identify:

**Top contributors to operational patterns**

Examples:

- Which IP generates most requests?
- Which key causes most traffic?
- Which resource contributes most errors?

This can be useful for:

**Finding hot spots**

---

# Contributor Insights + DynamoDB

A notable use case is identifying:

**Frequently accessed DynamoDB partition keys**

### Killer Exam Clue

> **Identify hot DynamoDB keys**
>
> → **CloudWatch Contributor Insights**

---

# CloudWatch Synthetics

**CloudWatch Synthetics**

uses:

**Canaries**

to simulate:

**User requests or application interactions**

Architecture:

Synthetic Canary  
↓  
Website / API  
↓  
Availability + Latency Check

### Killer Exam Clue

> **Continuously simulate user access to verify an endpoint works**
>
> → **CloudWatch Synthetics Canary**

---

# Canary Use Cases

Examples:

- Check login page
- Test REST API
- Verify checkout workflow
- Monitor public website availability

### Memory Trick

**Canary = Fake User Checking the App**

---

# CloudWatch RUM

**CloudWatch RUM — Real User Monitoring**

collects performance information from:

**Actual application users**

This can help analyze:

- Page load performance
- Browser behavior
- Client-side errors
- User experience

### Memory Trick

**Synthetics = Fake Users**

**RUM = Real Users**

---

# Synthetics vs RUM

| Requirement | Feature |
|---|---|
| Simulated User Testing | Synthetics |
| Real User Experience | RUM |
| Canary | Synthetics |
| Browser/User Telemetry | RUM |

---

# CloudWatch ServiceLens

CloudWatch observability features can provide:

**Application-level views**

combining:

- Metrics
- Logs
- Traces

This helps troubleshoot:

**Distributed applications**

---

# CloudWatch + X-Ray

[[X-Ray]] provides:

**Distributed tracing**

CloudWatch provides:

- Metrics
- Logs
- Alarms

Together they improve:

**Application observability**

### Memory Trick

**CloudWatch = Metrics + Logs**

**X-Ray = Trace the Request**

---

# CloudWatch vs CloudTrail

This distinction is critical.

## CloudWatch

Answers:

> **How is the system behaving?**

Examples:

- CPU
- Errors
- Logs
- Latency
- Alarms

## [[06-Security/CloudTrail]]

Answers:

> **Who did what in AWS?**

Examples:

- Who deleted bucket?
- Who changed security group?
- Who called API?

### Killer Memory Trick

**CloudWatch = PERFORMANCE**

**CloudTrail = API HISTORY**

---

# CloudWatch vs Config

## CloudWatch

Think:

**Operational monitoring**

## AWS Config

Think:

**Resource configuration and compliance**

Example:

CPU > 80%

→ CloudWatch

S3 bucket became public

→ Config

---

# CloudWatch vs EventBridge

CloudWatch:

**Observes metrics/logs**

[[20-SAA/10-Messaging/EventBridge]]:

**Routes events**

Example:

EC2 state-change event  
↓  
EventBridge  
↓  
Lambda

For metric thresholds:

Think:

**CloudWatch Alarm**

---

# CloudWatch vs Trusted Advisor

CloudWatch:

**Continuous operational monitoring**

Trusted Advisor:

**Best-practice recommendations**

Examples:

- Cost optimization
- Security
- Fault tolerance
- Performance

---

# Architecture Thinking

## Scenario 1 — High CPU

Operations wants notification if:

EC2 CPU > 80%

Choose:

CloudWatch Metric  
↓  
Alarm  
↓  
SNS

---

## Scenario 2 — EC2 RAM

Need:

**Memory utilization**

from EC2.

Choose:

**CloudWatch Agent**

---

## Scenario 3 — Application Error Logs

Need EC2 application's logs in:

CloudWatch.

Choose:

**CloudWatch Agent**

---

## Scenario 4 — Alert on ERROR

Application logs contain:

`ERROR`

Need alarm when more than:

10 errors occur.

Choose:

CloudWatch Logs  
↓  
Metric Filter  
↓  
CloudWatch Metric  
↓  
Alarm

---

## Scenario 5 — Search CloudWatch Logs

Need to investigate:

**Recent Lambda errors**

stored in CloudWatch Logs.

Choose:

**CloudWatch Logs Insights**

---

## Scenario 6 — Logs in S3

Need SQL analysis of:

CloudTrail logs stored in S3.

Do NOT choose Logs Insights.

Choose:

**Athena**

---

## Scenario 7 — Strange Traffic Pattern

Request count normally follows:

A predictable daily pattern.

Need alert when behavior becomes:

**Unusual**

Choose:

**CloudWatch Anomaly Detection**

---

## Scenario 8 — Website Availability

Need AWS to continuously simulate:

**A user visiting the website**

Choose:

**CloudWatch Synthetics**

---

## Scenario 9 — Real User Experience

Need actual browser performance data from:

**Real customers**

Choose:

**CloudWatch RUM**

---

## Scenario 10 — Who Deleted Resource?

Need to know:

**Who deleted an EC2 security group**

Do NOT choose CloudWatch.

Choose:

**CloudTrail**

---

# Scenario Recognition

Immediately think:

**CloudWatch**

when you see:

- Metrics
- Monitoring
- Alarm
- CPU
- Application logs
- Operational dashboard
- Threshold
- Resource performance
- Error monitoring

---

## Think CloudWatch Agent When You See

- EC2 memory
- Disk utilization
- OS logs
- Custom host metrics

---

## Think Metric Filter When You See

- Log text
- Convert log pattern to metric
- Alarm based on log occurrence

---

## Think Logs Insights When You See

- Search CloudWatch Logs
- Interactive log query
- Troubleshooting stored logs

---

## Think Synthetics When You See

- Canary
- Simulated user
- Endpoint availability test

---

## Think RUM When You See

- Actual users
- Browser performance
- Client-side experience

---

# Exam Traps

## Trap 1 — EC2 Memory Utilization Is Automatically Available

❌

Use:

**CloudWatch Agent**

---

## Trap 2 — CloudWatch Tells You Who Changed an IAM Policy

❌

Think:

**CloudTrail**

---

## Trap 3 — Logs Insights Queries S3

❌

Logs Insights queries:

**CloudWatch Logs**

Athena queries:

**S3**

---

## Trap 4 — Metric Filters Store Application Logs

❌

CloudWatch Logs stores:

**Logs**

Metric Filter creates:

**Metrics from matching logs**

---

## Trap 5 — CloudWatch Alarm Requires a Human to Watch the Dashboard

❌

Alarms can:

**Automatically trigger actions**

---

## Trap 6 — Synthetics Monitors Only Real Users

❌

Synthetics uses:

**Simulated users**

RUM observes:

**Real users**

---

## Trap 7 — Detailed EC2 Monitoring Means Every Metric Is Collected

❌

It changes the frequency of supported EC2 metrics.

OS-level metrics such as:

**Memory**

still require the agent.

---

# Quick Cheat Sheet

| Exam Clue | Answer |
|---|---|
| AWS Operational Monitoring | CloudWatch |
| Numeric Measurement | Metric |
| Threshold Alert | Alarm |
| EC2 5-Minute Metrics | Basic Monitoring |
| EC2 1-Minute Metrics | Detailed Monitoring |
| EC2 Memory | CloudWatch Agent |
| EC2 OS Logs | CloudWatch Agent |
| Application-Specific Measurement | Custom Metric |
| Logs | CloudWatch Logs |
| Log Pattern → Metric | Metric Filter |
| Query CloudWatch Logs | Logs Insights |
| Visual Monitoring | Dashboard |
| Dynamic Behavioral Threshold | Anomaly Detection |
| Find Top Contributors | Contributor Insights |
| Synthetic Endpoint Test | Synthetics |
| Real User Experience | RUM |
| AWS API History | CloudTrail |
| Configuration Compliance | Config |

---

# Monitoring Decision Map

Need:

**Metric**

→ CloudWatch Metrics

Need:

**Threshold**

→ CloudWatch Alarm

Need:

**Log storage**

→ CloudWatch Logs

Need:

**Search CloudWatch logs**

→ Logs Insights

Need:

**Convert log text into metric**

→ Metric Filter

Need:

**EC2 OS-level metric**

→ CloudWatch Agent

Need:

**Fake user monitoring**

→ Synthetics

Need:

**Real user monitoring**

→ RUM

Need:

**Who changed AWS resource**

→ CloudTrail

Need:

**Resource compliance**

→ Config

---

# Final Exam Rapid-Fire

> **MONITOR RESOURCE**
> → CLOUDWATCH
>
> **CPU**
> → CLOUDWATCH METRIC
>
> **THRESHOLD**
> → CLOUDWATCH ALARM
>
> **EC2 5-MINUTE**
> → BASIC MONITORING
>
> **EC2 1-MINUTE**
> → DETAILED MONITORING
>
> **EC2 MEMORY**
> → CLOUDWATCH AGENT
>
> **OS LOGS**
> → CLOUDWATCH AGENT
>
> **LOG TEXT → METRIC**
> → METRIC FILTER
>
> **QUERY CLOUDWATCH LOGS**
> → LOGS INSIGHTS
>
> **UNUSUAL METRIC PATTERN**
> → ANOMALY DETECTION
>
> **TOP CONTRIBUTOR**
> → CONTRIBUTOR INSIGHTS
>
> **FAKE USER**
> → SYNTHETICS
>
> **REAL USER**
> → RUM
>
> **WHO DID WHAT**
> → CLOUDTRAIL
>
> **CONFIGURATION COMPLIANCE**
> → CONFIG

---

## Master Memory Trick

> [!tip] CloudWatch Master Memory Trick
> Imagine an AWS control room.
>
> The giant screens display:
>
> **NUMBERS**
> → Metrics
>
> The screens turn red when:
>
> **A LIMIT IS CROSSED**
> → Alarms
>
> Engineers read:
>
> **APPLICATION MESSAGES**
> → Logs
>
> A special agent inside the server reports:
>
> **MEMORY + DISK + OS LOGS**
> → CloudWatch Agent
>
> A robot pretends to be a customer:
>
> **SYNTHETICS**
>
> Actual customers report their experience:
>
> **RUM**
>
> But if someone asks:
>
> **"WHO changed the security group?"**
>
> leave the CloudWatch room and go to:
>
> **CLOUDTRAIL**

So remember:

> **CLOUDWATCH**
> → HOW IS IT RUNNING?
>
> **METRIC**
> → NUMBER
>
> **LOG**
> → MESSAGE
>
> **ALARM**
> → REACT
>
> **AGENT**
> → OS DATA
>
> **SYNTHETICS**
> → FAKE USER
>
> **RUM**
> → REAL USER
>
> **CLOUDTRAIL**
> → WHO DID IT?

And the killer SAA question:

> **"Is the question asking about operational performance, logs, metrics, or threshold-based alerting?"**
>
> YES
>
> → **CloudWatch**

---

## Related Notes

- [[06-Security/CloudTrail]]
- [[AWS Config]]
- [[X-Ray]]
- [[20-SAA/10-Messaging/EventBridge]]
- [[SNS]]
- [[Lambda]]
- [[EC2]]
- [[Auto Scaling Groups]]
- [[Athena]]
- [[DynamoDB]]
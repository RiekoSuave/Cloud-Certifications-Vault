See also: [CloudTrail](<CloudTrail Monitoring Reference>)

See also: [Config](<Config Monitoring Reference>)

## What Problem Does It Solve?

Monitors AWS resources and applications.

CloudWatch solves the need for visibility into your AWS environment.

It helps you:

- Monitor metrics
- Collect logs
- Create dashboards
- Trigger alarms
- Respond when something goes wrong

### Memory Trick

CloudWatch = Watch AWS Resources

---

## Type

Monitoring Service

---

## What Is CloudWatch?

Amazon CloudWatch is AWS's monitoring service.

Think:

AWS Resources

↓

Metrics + Logs

↓

CloudWatch

↓

Dashboards + Alarms

### Memory Trick

CloudWatch = Monitor What Is Happening

---

## CloudWatch Metrics

CloudWatch provides metrics for AWS services.

A metric is:

A Variable You Monitor

Examples:

CPUUtilization

Network

Disk Reads/Writes

Number of Objects

Metrics include timestamps so CloudWatch can track values over time.

### Memory Trick

Metric = Number Being Watched

---

## Important Metrics

Your course gives several examples.

### EC2

CloudWatch can monitor:

- CPU Utilization
- Status Checks
- Network

Important:

RAM is NOT included by default.

### EBS

CloudWatch can monitor:

- Disk Reads
- Disk Writes

### S3

Examples include:

- BucketSizeBytes
- NumberOfObjects
- AllRequests

### Billing

CloudWatch can monitor:

Total Estimated Charge

Your course notes that the billing metric is available in:

us-east-1

### Memory Trick

CloudWatch = Numbers About AWS Resources

---

## EC2 Monitoring

Your course makes an important distinction between:

Default Monitoring

and

Detailed Monitoring

### Default Monitoring

Metrics every:

5 Minutes

### Detailed Monitoring

Metrics every:

1 Minute

Detailed Monitoring costs extra.

| EC2 Monitoring | Frequency |
| --- | --- |
| Default | 5 minutes |
| Detailed | 1 minute |

### Memory Trick

Default = 5

Detailed = 1

---

## CloudWatch Dashboards

CloudWatch dashboards allow you to display metrics visually.

Think:

Multiple AWS Metrics

↓

CloudWatch Dashboard

↓

One Monitoring View

### Common Use Case

A company wants a dashboard showing the performance of AWS resources.

→ CloudWatch Dashboard

---

## CloudWatch Alarms

CloudWatch Alarms watch metrics and trigger actions when defined conditions are met.

Think:

Metric

↓

Threshold Reached

↓

CloudWatch Alarm

↓

Action

### Memory Trick

Alarm = Metric Triggers Action

---

## CloudWatch Alarm Actions

Your course identifies several actions CloudWatch Alarms can trigger.

### Auto Scaling

An alarm can cause Auto Scaling to:

Increase

or

Decrease

the desired number of EC2 instances.

### EC2 Actions

An alarm can trigger actions such as:

- Stop
- Terminate
- Reboot
- Recover

an EC2 instance.

### SNS Notifications

An alarm can send a notification to:

Amazon SNS

Think:

CPU Too High

↓

CloudWatch Alarm

↓

SNS

↓

Notification

### Memory Trick

CloudWatch Sees It

Alarm Triggers It

SNS Tells You

---

## CloudWatch Alarm States

Your course identifies three alarm states:

OK

INSUFFICIENT_DATA

ALARM

### OK

The metric is within the defined threshold.

### INSUFFICIENT_DATA

CloudWatch does not currently have enough data to determine the alarm state.

### ALARM

The metric has reached the condition defined by the alarm.

### Memory Trick

OK = Good

INSUFFICIENT_DATA = Don't Know Yet

ALARM = Threshold Triggered

---

## Billing Alarm

Your course gives billing as an example of a CloudWatch Alarm.

Think:

Billing Metric

↓

CloudWatch Alarm

↓

Billing Threshold Reached

↓

Notification

### Scenario

A company wants to receive an alert when its estimated AWS charges reach a specified amount.

→ CloudWatch Billing Alarm

---

## CloudWatch Logs

CloudWatch Logs collects and monitors log data.

Your course gives examples from:

- Elastic Beanstalk
- ECS
- Lambda
- CloudTrail
- EC2
- On-premises servers
- Route 53

CloudWatch Logs enables:

Real-Time Monitoring of Logs

Log retention can also be adjusted.

### Memory Trick

Metrics = Numbers

Logs = Records

---

## CloudWatch Logs and EC2

This is an important course distinction.

By default:

EC2 Logs Do NOT Automatically Go to CloudWatch

To send EC2 log files to CloudWatch:

Install / Run CloudWatch Agent

↓

Configure IAM Permissions

↓

Push Logs to CloudWatch Logs

The CloudWatch Agent can also be used with:

On-Premises Servers

### Memory Trick

EC2 Logs?

Think CloudWatch Agent

---

## CloudWatch vs CloudTrail

These are frequently confused.

### CloudWatch

Monitors:

Performance and Resources

Think:

Metrics

Logs

Alarms

### CloudTrail

Tracks:

AWS API Activity

Think:

Who Did What?

| CloudWatch | CloudTrail |
| --- | --- |
| Monitoring | Auditing |
| Metrics | API activity |
| Logs | Account actions |
| Alarms | Who did what |

### Memory Trick

CloudWatch = WHAT IS HAPPENING?

CloudTrail = WHO DID IT?

See:

[CloudTrail](<CloudTrail Monitoring Reference>)

---

## CloudWatch vs Config

### CloudWatch

Monitors:

Resource Performance

### Config

Tracks:

Resource Configuration and Changes

| CloudWatch | Config |
| --- | --- |
| Performance monitoring | Configuration tracking |
| Metrics | Resource history |
| Alarms | Compliance |
| Logs | Configuration changes |

### Memory Trick

CloudWatch = PERFORMANCE

Config = CONFIGURATION

See:

[Config](<Config Monitoring Reference>)

---

## CloudWatch vs CloudTrail vs Config

This is one of the most important monitoring comparisons.

| Service | Think |
| --- | --- |
| CloudWatch | Metrics, Logs, Alarms |
| CloudTrail | API Activity |
| Config | Resource Configuration |

### Memory Trick

CloudWatch = WATCH

CloudTrail = TRACK ACTIONS

Config = TRACK CHANGES

---

## Common Use Cases

- Performance monitoring
- Resource monitoring
- Application monitoring
- Alerting
- Log analysis
- Dashboards
- Billing alarms
- Auto Scaling triggers

---

## Scenario Questions

A company wants to monitor CPU utilization on EC2 instances.

→ CloudWatch

---

A company wants an alert when CPU utilization becomes too high.

→ CloudWatch Alarm

---

A company wants to automatically scale EC2 instances based on a metric.

→ CloudWatch Alarm + Auto Scaling

---

A company wants to send a notification when a metric crosses a threshold.

→ CloudWatch Alarm + SNS

---

A company wants a dashboard displaying AWS resource metrics.

→ CloudWatch Dashboard

---

A company wants to collect application logs from Lambda.

→ CloudWatch Logs

---

A company wants to send EC2 operating system logs to CloudWatch.

→ CloudWatch Agent

---

A company wants metrics from an EC2 instance every minute.

→ Detailed Monitoring

---

A company wants to know which user made an AWS API call.

→ CloudTrail

NOT CloudWatch

---

A company wants to track how the configuration of a resource changed.

→ AWS Config

NOT CloudWatch

---

## Don't Confuse These

CloudWatch = Monitoring

CloudTrail = API Activity

Config = Configuration History

CloudWatch Metrics = Numbers

CloudWatch Logs = Log Records

CloudWatch Alarms = Trigger Actions

CloudWatch Dashboard = Visualize Metrics

CloudWatch Agent = Send EC2 Logs

---

## Exam Keywords

CloudWatch

Monitoring

Metrics

Logs

Alarms

Dashboards

CPU Utilization

Performance

SNS Notification

Auto Scaling

Billing Alarm

CloudWatch Agent

Detailed Monitoring

---

## Memory Tricks

CloudWatch = Watch AWS

Metric = NUMBER

Logs = RECORDS

Alarm = ACTION

Dashboard = VISUALIZE

Agent = SEND EC2 LOGS

Default EC2 Monitoring = 5 MINUTES

Detailed EC2 Monitoring = 1 MINUTE

---

## Quick Cheat Sheet

CloudWatch = Metrics + Logs + Alarms

Metrics = Numbers Being Monitored

Logs = Log Data

Alarms = Trigger Actions

Dashboards = Visualize Metrics

EC2 Default Monitoring = 5 Minutes

EC2 Detailed Monitoring = 1 Minute

EC2 Logs → CloudWatch Agent

Alarm → SNS Notification

Alarm → Auto Scaling

Alarm → EC2 Action

CloudWatch = Monitoring

CloudTrail = Who Did What

Config = What Changed
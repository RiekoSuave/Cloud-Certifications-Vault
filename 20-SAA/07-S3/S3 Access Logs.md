## What Problem Does It Solve?

[[S3 Access Logs]] record requests made to an S3 bucket for:

**Auditing and analysis**

They solve the problem of:

> **"How can I see who accessed my S3 bucket, what they requested, and whether the request succeeded or failed?"**

Think:

User / Application  
↓  
Request to S3  
↓  
S3 Access Logging  
↓  
Separate Logging Bucket  
↓  
Analyze Logs

> [!tip] Memory Trick
> **Access Logs = Who touched my S3 bucket?**

---

## What Gets Logged?

S3 Access Logs can record requests made to the monitored bucket.

The Maarek slides emphasize:

**Any request made to S3**

including requests from:

- Your AWS account
- Another AWS account
- Authorized users
- Unauthorized users

This means both:

**Successful and denied requests**

can be logged.

### Architecture Thinking

Request  
↓  
Allowed ✅

or:

Request  
↓  
Denied ❌

Both can appear in:

[[S3 Access Logs]]

---

## Why Log Denied Requests?

Denied requests can be especially useful for:

- Security investigations
- Troubleshooting permissions
- Detecting suspicious access attempts
- Finding misconfigured applications

Example:

Application  
↓  
`s3:GetObject`  
↓  
403 Access Denied  
↓  
Access Log

This can help answer:

> **"Who tried to access this object and what happened?"**

---

# Core Architecture

You typically have:

### Source Bucket

The bucket being monitored.

Example:

`application-data`

### Target Logging Bucket

The bucket receiving the access logs.

Architecture:

Users / Applications  
↓  
Requests  
↓  
Source S3 Bucket  
↓  
S3 Access Logging  
↓  
Target Logging Bucket

> [!tip] Memory Trick
> **Source Bucket = Watched**
>
> **Logging Bucket = Records what happened**

---

# Logs Go to Another S3 Bucket

The Maarek slides explicitly emphasize:

Access logs are written to:

**Another S3 bucket**

Do not use the monitored bucket itself as the logging destination.

Why?

Because every log object written to the bucket would itself generate another log entry.

That creates:

**A logging loop**

---

# The Logging Loop

This is the biggest S3 Access Logs exam trap.

Bad architecture:

Application Bucket  
↓  
Access Request  
↓  
Log Written to Same Bucket  
↓  
That PUT Generates Another Log  
↓  
Another Log Written  
↓  
Another PUT  
↓  
More Logs  
↓  
More PUTs...

Result:

**Exponential bucket growth**

> [!warning] Exam Rule
> **NEVER send S3 access logs back into the same bucket being monitored.**

---

## Logging Loop Memory Trick

> **Bucket logs itself → Infinite mirror**

Think of two mirrors facing each other:

Log  
↓  
Creates Log  
↓  
Creates Log  
↓  
Creates Log

Bad idea.

---

# Same-Region Requirement

The target logging bucket must be in the:

**Same AWS Region**

as the monitored bucket.

Architecture:

Source Bucket  
us-east-1  
↓  
Access Logs  
↓  
Logging Bucket  
us-east-1 ✅

Not:

Source Bucket  
us-east-1  
↓  
Logging Bucket  
eu-west-1 ❌

> [!tip] Exam Detail
> **Access Logs destination → Same Region**

---

# Centralized Logging Pattern

A useful architecture is:

Application Bucket A  
↓  
Application Bucket B  
↓  
Application Bucket C  
↓  
Central Logging Bucket

This can make security and auditing easier.

However, the target logging architecture still needs to respect the required S3 logging configuration.

### Architecture Thinking

If several buckets need auditing:

Think:

**Centralized log storage**

instead of trying to inspect each application bucket separately.

---

# Analyzing Access Logs

The Maarek slides note that access-log data can be analyzed using:

**Data analysis tools**

A common architecture could be:

S3 Access Logs  
↓  
Logging Bucket  
↓  
[[09-Analytics/Athena]]  
↓  
SQL Queries  
↓  
Audit / Security Analysis

Examples of questions:

- Which IP addresses accessed the bucket?
- Which objects generated Access Denied?
- Which requester downloaded a file?
- Which requests occurred during a security incident?

---

# Access Logs + Athena

Because the logs live in S3:

[[09-Analytics/Athena]]

is a natural analysis option.

Architecture:

S3 Bucket  
↓  
Access Logs  
↓  
Logging Bucket  
↓  
[[09-Analytics/Athena]]  
↓  
Query Logs

### Memory Trick

**Logs in S3 + SQL question → Athena**

---

# Lifecycle Management for Logs

Access logs themselves consume storage.

A common architecture is:

Access Logs  
↓  
Logging Bucket  
↓  
[[S3 Lifecycle Rules]]  
↓  
Transition / Archive / Delete

Example:

Logs  
↓ 30 days  
Standard-IA  
↓ 180 days  
Glacier  
↓ 365 days  
Expire

### Architecture Thinking

Logging provides visibility.

Lifecycle Rules control:

**The cost of retaining that visibility**

---

# Access Logs vs CloudTrail

This is an important distinction.

## S3 Access Logs

Focus on:

**Requests to an S3 bucket**

Think:

> **Who accessed my S3 objects/bucket?**

---

## [[06-Security/CloudTrail]]

Focuses broadly on:

**AWS API activity**

Think:

> **Who made this AWS API call?**

CloudTrail spans many AWS services, not just S3.

### Memory Trick

**Access Logs = S3 request detail**

**CloudTrail = AWS API audit trail**

---

# Access Logs vs CloudWatch

## S3 Access Logs

Provide:

**Request logs**

for auditing and later analysis.

---

## [[07-Monitoring/CloudWatch]]

Provides:

**Metrics, logs, alarms, and monitoring**

If the requirement says:

> **"Record detailed S3 requests for audit purposes"**

think:

S3 Access Logs

If it says:

> **"Alert when a metric crosses a threshold"**

think:

CloudWatch

---

# Access Logs vs S3 Event Notifications

These solve very different problems.

## [[S3 Event Notifications]]

React when:

**Something happens to an object**

Example:

Object Created  
↓  
Lambda

---

## S3 Access Logs

Record:

**Requests made to the bucket**

Example:

GetObject  
↓  
Logged for auditing

### Memory Trick

**Event Notification = DO something**

**Access Logs = RECORD something**

---

# Access Logs vs S3 Inventory

## [[S3 Inventory]]

Answers:

> **What objects exist?**

---

## S3 Access Logs

Answers:

> **Who requested them?**

### Memory Trick

**Inventory = What's there**

**Access Logs = Who touched it**

---

# Architecture Thinking

## Scenario 1 — Audit S3 Access

A security team needs to record all requests made to a sensitive S3 bucket.

They need information about:

- Successful requests
- Failed requests
- Requests from other accounts

**Choose → S3 Access Logs**

---

## Scenario 2 — Analyze 403 Errors

A company sees unexpected:

**403 Access Denied**

responses from an S3 application.

They want to investigate who made the requests.

**Choose → S3 Access Logs**

Then analyze the logs with:

[[09-Analytics/Athena]]

---

## Scenario 3 — Logging Destination

A company configures the monitored S3 bucket as its own logging destination.

Storage usage begins increasing rapidly.

What happened?

**Logging Loop**

Fix:

Use:

**A separate S3 logging bucket**

---

## Scenario 4 — Destination in Another Region

A source bucket is in:

us-east-1

The company configures its logging bucket in:

eu-west-1

This violates the expected access-log architecture.

Use:

**A target bucket in the same Region**

---

## Scenario 5 — Need AWS-Wide API Audit

A company needs to audit API actions across:

- EC2
- IAM
- S3
- RDS

**Do NOT choose → S3 Access Logs**

Choose:

[[06-Security/CloudTrail]]

---

# Scenario Recognition

## Immediately Think S3 Access Logs When You See

- Audit S3 access
- Log bucket requests
- Authorized and denied requests
- Who accessed S3
- Analyze S3 requests
- Logging bucket
- Same Region
- Access log analysis
- Logging loop

### Strongest Exam Pattern

> **"Audit all access requests to an S3 bucket"**
>
> → **S3 Access Logs**

---

# Exam Traps

## Trap 1 — Only Successful Requests Are Logged

False.

The Maarek slides emphasize that:

**Authorized and denied requests**

can be logged.

---

## Trap 2 — Logging Bucket Can Be the Same Bucket

Do NOT do this.

It creates:

**A logging loop**

and can cause exponential storage growth.

---

## Trap 3 — Logging Bucket Can Be in Any Region

False.

The target logging bucket must be in the:

**Same AWS Region**

---

## Trap 4 — Access Logs Automatically Analyze Themselves

False.

They provide:

**Raw log data**

You can use tools such as:

[[09-Analytics/Athena]]

to analyze the logs.

---

## Trap 5 — Access Logs and Event Notifications Are the Same

False.

Event Notifications:

**Trigger actions**

Access Logs:

**Record requests**

---

## Trap 6 — Access Logs Replace CloudTrail

False.

S3 Access Logs focus specifically on S3 requests.

CloudTrail provides broader AWS API auditing.

---

# Quick Cheat Sheet

| Requirement | S3 Access Logs |
|---|---|
| Audit S3 requests | ✅ |
| Log successful requests | ✅ |
| Log denied requests | ✅ |
| Requests from other accounts | ✅ |
| Destination is S3 bucket | ✅ |
| Target bucket same Region | ✅ |
| Same bucket as source | ❌ |
| Analyze with Athena | ✅ |
| Logging Loop Risk | ✅ |
| AWS-wide API auditing | Use CloudTrail |
| Trigger processing on upload | Use Event Notifications |

---

## Master Memory Trick

> [!tip] Master Memory Trick
> **S3 Access Logs = Security Camera for the Bucket**
>
> The camera records:
>
> **Who came?**
>
> **What did they request?**
>
> **Was access allowed or denied?**

Then remember the architecture:

**App Bucket**
↓
**Access Requests**
↓
**Separate Logging Bucket**

And the killer exam rule:

> **Never point the camera at itself**
>
> Same source + logging bucket
>
> → **Logging Loop**

Finally:

**Access Logs = RECORD**

**Event Notifications = REACT**

**Inventory = LIST**

**CloudTrail = AWS-WIDE AUDIT**

---

## Related Notes

- [[S3]]
- [[S3 Bucket Policies]]
- [[S3 Event Notifications]]
- [[S3 Inventory]]
- [[S3 Lifecycle Rules]]
- [[S3 Storage Lens]]
- [[09-Analytics/Athena]]
- [[06-Security/CloudTrail]]
- [[07-Monitoring/CloudWatch]]
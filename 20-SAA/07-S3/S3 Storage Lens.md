## What Problem Does It Solve?

[[S3 Storage Lens]] gives you organization-wide visibility into how S3 storage is being used.

It solves the problem of:

> **"How can I understand, analyze, and optimize S3 usage across many accounts, Regions, buckets, and prefixes?"**

Think:

Entire AWS Organization  
↓  
[[S3 Storage Lens]]  
↓  
Aggregate Metrics  
↓  
Dashboards + Insights  
↓  
Optimize Cost / Security / Usage

> [!tip] Memory Trick
> **Storage Lens = Binoculars for your whole S3 environment**

---

## What Storage Lens Can Analyze

Storage Lens can aggregate S3 information across:

- AWS Organization
- Specific AWS accounts
- Regions
- Buckets
- Prefixes

This makes it useful when S3 usage is spread across:

**Many different parts of an AWS environment**

---

## Core Goals

Storage Lens helps you:

- Understand storage usage
- Analyze trends
- Discover anomalies
- Identify cost efficiencies
- Improve data-protection practices
- Optimize S3 environments at scale

### Architecture Thinking

If the requirement says:

> **"Give me centralized S3 visibility across many accounts and Regions."**

Think:

[[S3 Storage Lens]]

---

# Storage Lens Dashboard

Storage Lens provides a:

**Dashboard**

that summarizes storage insights and trends.

Architecture:

Organization  
↓  
Accounts  
↓  
Regions  
↓  
Buckets  
↓  
Storage Lens Dashboard

The dashboard helps identify:

- Growing storage
- Unused storage
- Cost inefficiencies
- Missing data-protection controls
- Request activity

---

# Default Dashboard

S3 provides a:

**Default Storage Lens Dashboard**

The Maarek slides emphasize that it:

- Is preconfigured by S3
- Shows Multi-Region data
- Shows Multi-Account data
- Displays summarized insights and trends
- Includes both free and advanced metrics

Important:

The default dashboard:

**Cannot be deleted**

but:

**Can be disabled**

> [!tip] Exam Detail
> **Default Storage Lens Dashboard → Cannot delete, can disable**

---

# Custom Dashboards

You can also create:

**Custom Storage Lens Dashboards**

These can focus on different parts of your environment.

Example:

Organization  
↓  
Finance Account  
↓  
us-east-1  
↓  
Specific Buckets

This lets teams focus on their own relevant metrics.

---

# Export Metrics to S3

Storage Lens metrics can be exported:

**Daily**

to an S3 bucket.

Supported formats include:

- CSV
- Parquet

Architecture:

Storage Lens  
↓  
Daily Export  
↓  
S3 Bucket  
↓  
CSV / Parquet

This is useful for:

- Long-term analytics
- Custom dashboards
- External reporting
- Querying data with analytics tools

---

# Storage Lens Metrics Categories

The Maarek slides group Storage Lens metrics into several categories.

Important categories include:

- Summary Metrics
- Cost-Optimization Metrics
- Data-Protection Metrics
- Access-Management Metrics
- Event Metrics
- Performance Metrics
- Activity Metrics
- Detailed Status Code Metrics

---

# Summary Metrics

Summary Metrics provide:

**General insight into S3 storage**

Examples:

- StorageBytes
- ObjectCount

Use cases:

- Find fastest-growing buckets
- Find unused buckets
- Find growing prefixes

### Architecture Thinking

If the question asks:

> **"Which bucket is growing fastest?"**

Think:

**Storage Lens Summary Metrics**

---

# Cost-Optimization Metrics

Cost-Optimization Metrics help identify:

**Ways to reduce S3 storage cost**

Examples from the Maarek slides include:

- NonCurrentVersionStorageBytes
- IncompleteMultipartUploadStorageBytes

Use cases:

- Find old noncurrent object versions
- Find incomplete multipart uploads
- Identify data that could move to cheaper storage

Architecture:

Storage Lens  
↓  
Find Cost Waste  
↓  
[[S3 Lifecycle Rules]]  
↓  
Optimize Storage

> [!tip] Memory Trick
> **Storage Lens finds the waste**
>
> **Lifecycle Rules remove or transition it**

---

# Incomplete Multipart Uploads

Storage Lens can help identify buckets containing:

**Incomplete Multipart Uploads older than 7 days**

These can consume unnecessary storage.

Possible remediation:

[[S3 Lifecycle Rules]]

↓  

Abort Incomplete Multipart Uploads

---

# Storage Class Optimization

Storage Lens can help identify objects that may be candidates for:

**Lower-cost storage classes**

Example:

Frequently Stored  
↓  
Rarely Accessed  
↓  
Storage Lens Insight  
↓  
Lifecycle Rule  
↓  
[[S3 Standard-IA]] / Glacier

---

# Data-Protection Metrics

Data-Protection Metrics help identify whether S3 buckets follow:

**Data-protection best practices**

Examples include:

- VersioningEnabledBucketCount
- MFADeleteEnabledBucketCount
- SSEKMSEnabledBucketCount
- CrossRegionReplicationRuleCount

These can reveal buckets missing important controls.

---

## Data-Protection Architecture

Storage Lens  
↓  
Detect Missing Protection  
↓  
Examples:
- Versioning disabled
- MFA Delete absent
- SSE-KMS absent
- CRR not configured

↓  

Security Team Remediates

### Exam Pattern

If the requirement says:

> **"Find buckets that are not following S3 data-protection best practices."**

Think:

**Storage Lens Data-Protection Metrics**

---

# Access-Management Metrics

Access-Management Metrics provide visibility into:

**S3 Object Ownership**

Example metric:

ObjectOwnershipBucketOwnerEnforcedBucketCount

Use case:

Identify which buckets use specific:

[[S3 Object Ownership]]

settings.

---

# Event Metrics

Event Metrics provide visibility into:

[[S3 Event Notifications]]

Example:

EventNotificationEnabledBucketCount

Use case:

Identify which buckets have:

**S3 Event Notifications configured**

---

# Performance Metrics

Performance Metrics provide insight into:

[[S3 Transfer Acceleration]]

Example:

TransferAccelerationEnabledBucketCount

Use case:

Determine which buckets have:

**Transfer Acceleration enabled**

---

# Activity Metrics

Activity Metrics show:

**How S3 storage is being requested**

Examples:

- AllRequests
- GetRequests
- PutRequests
- ListRequests
- BytesDownloaded

This helps answer:

> **"How is this storage actually being used?"**

---

# Detailed Status Code Metrics

Storage Lens can provide insight into:

**HTTP status codes**

Examples:

- 200OKStatusCount
- 403ForbiddenErrorCount
- 404NotFoundErrorCount

These are useful for:

- Troubleshooting
- Access analysis
- Request-failure trends

### Architecture Thinking

Many 403 responses  
↓  
Storage Lens Status Metrics  
↓  
Investigate:
- Bucket Policies
- IAM
- Block Public Access

---

# Free Metrics

Storage Lens provides:

**Free Metrics**

These are automatically available.

The Maarek slides highlight:

- Around 28 usage metrics
- Data available for queries for 14 days

These provide a baseline level of S3 visibility.

---

# Advanced Metrics and Recommendations

Advanced Storage Lens capabilities are:

**Paid**

They provide additional metrics and features.

Examples include:

- Activity metrics
- Advanced cost optimization
- Advanced data protection
- Status code metrics

Additional capabilities include:

- CloudWatch publishing
- Prefix aggregation
- Longer metric retention

---

# Advanced Retention

Advanced metrics can remain queryable for:

**15 months**

Compared with free metrics:

**14 days**

### Memory Trick

**Free = 14 days**

**Advanced = 15 months**

---

# CloudWatch Publishing

Advanced Storage Lens metrics can be published to:

[[07-Monitoring/CloudWatch]]

This lets you access Storage Lens metrics through CloudWatch.

Architecture:

S3 Storage Lens  
↓  
[[07-Monitoring/CloudWatch]]  
↓  
Monitoring / Dashboards / Alarms

---

# Prefix Aggregation

Advanced Storage Lens supports:

**Prefix-level metric aggregation**

This can provide deeper visibility into how different logical sections of a bucket are being used.

Example:

Bucket  
├── finance/
├── sales/
└── analytics/

Storage Lens can help analyze:

**Usage by prefix**

---

# Storage Lens vs S3 Inventory

These are easy to confuse.

## [[S3 Inventory]]

Provides:

**Object-level listings**

Question:

> Which exact objects exist?

---

## Storage Lens

Provides:

**Aggregated metrics and insights**

Question:

> How is my S3 environment behaving overall?

### Memory Trick

**Inventory = LIST**

**Storage Lens = METRICS**

---

# Storage Lens vs S3 Analytics

## [[S3 Analytics]]

Primarily helps analyze:

**Storage-class access patterns**

especially for transition decisions.

---

## Storage Lens

Provides broader insights across:

- Cost
- Data protection
- Requests
- Access management
- Performance
- Status codes
- Organizations

### Exam Decision

**Storage class transition analysis → S3 Analytics**

**Organization-wide S3 visibility → Storage Lens**

---

# Storage Lens vs CloudWatch

## [[07-Monitoring/CloudWatch]]

Provides general AWS monitoring.

---

## Storage Lens

Provides:

**S3-specific organization-wide insights**

Advanced Storage Lens metrics can also be:

**Published into CloudWatch**

Think:

Storage Lens  
↓  
S3-specialized insights

CloudWatch  
↓  
General AWS monitoring platform

---

# Architecture Thinking

## Scenario 1 — Organization-Wide S3 Visibility

A company has:

- 50 AWS accounts
- Hundreds of buckets
- Several Regions

Security wants a centralized dashboard showing:

- Storage growth
- Cost optimization
- Data protection

**Choose → [[S3 Storage Lens]]**

---

## Scenario 2 — Find Storage Waste

A company wants to identify:

- Old noncurrent versions
- Incomplete multipart uploads
- Data that could use cheaper storage

**Choose → Storage Lens Cost-Optimization Metrics**

---

## Scenario 3 — Find Buckets Without Versioning

Security needs a report showing which S3 buckets are not following data-protection best practices.

**Choose → Storage Lens Data-Protection Metrics**

---

## Scenario 4 — Need Exact Object List

A company needs a report containing every object key and version ID.

**Do NOT choose → Storage Lens**

Choose:

[[S3 Inventory]]

---

## Scenario 5 — Find 403 Errors

Administrators want centralized insight into S3 HTTP access failures.

**Choose → Storage Lens Detailed Status Code Metrics**

---

## Scenario 6 — Long-Term S3 Metrics

A company needs Storage Lens metrics retained for many months.

**Choose → Advanced Metrics**

Remember:

**Advanced → 15 months**

---

# Scenario Recognition

## Immediately Think Storage Lens When You See

- Entire AWS Organization
- Multi-account S3 analytics
- Multi-Region S3 metrics
- S3 dashboards
- Storage usage trends
- Find fastest-growing bucket
- Cost optimization
- Data protection best practices
- S3 anomalies
- Status code metrics
- Organization-wide S3 visibility

### Strongest Exam Pattern

> **"Analyze and optimize S3 across the entire AWS Organization"**
>
> → **S3 Storage Lens**

---

# Exam Traps

## Trap 1 — Storage Lens Lists Every Individual Object

Not primarily.

That is:

[[S3 Inventory]]

Storage Lens focuses on:

**Aggregated metrics and insights**

---

## Trap 2 — Storage Lens Is Only for Cost Optimization

False.

It also provides:

- Data-protection metrics
- Access-management metrics
- Event metrics
- Performance metrics
- Activity metrics
- Status-code metrics

---

## Trap 3 — Default Dashboard Can Be Deleted

False.

It:

**Cannot be deleted**

but:

**Can be disabled**

---

## Trap 4 — Storage Lens Is Single-Bucket Only

False.

It can aggregate across:

- Organization
- Accounts
- Regions
- Buckets
- Prefixes

---

## Trap 5 — Free Metrics Are Retained for 15 Months

False.

Free:

**14 days**

Advanced:

**15 months**

---

## Trap 6 — Storage Lens Automatically Fixes Problems

False.

Storage Lens provides:

**Visibility + Insights**

You still use other services to remediate issues.

Examples:

[[S3 Lifecycle Rules]]

[[S3 Versioning]]

[[S3 Encryption]]

---

# Quick Cheat Sheet

| Requirement | Storage Lens |
|---|---|
| Organization-Wide S3 Visibility | ✅ |
| Multi-Account | ✅ |
| Multi-Region | ✅ |
| Bucket-Level Metrics | ✅ |
| Prefix-Level Metrics | ✅ |
| Summary Metrics | ✅ |
| Cost Optimization | ✅ |
| Data Protection Insights | ✅ |
| Access Management Insights | ✅ |
| Event Metrics | ✅ |
| Performance Metrics | ✅ |
| Activity Metrics | ✅ |
| HTTP Status Metrics | ✅ |
| Exact Object Listing | ❌ |
| Daily Export to S3 | ✅ |
| CSV / Parquet Export | ✅ |
| Default Dashboard Deletable | ❌ |
| Default Dashboard Disableable | ✅ |

---

## Master Memory Trick

> [!tip] Master Memory Trick
> **Storage Lens = S3 Executive Dashboard**
>
> It answers:
>
> **How much storage?**
>
> → Summary
>
> **Where am I wasting money?**
>
> → Cost Optimization
>
> **Am I protecting my data?**
>
> → Data Protection
>
> **How is S3 being accessed?**
>
> → Activity
>
> **Are requests failing?**
>
> → Status Codes

Remember the big distinction:

> **Inventory = Individual Objects**
>
> **Storage Lens = Aggregated Insights**

And:

**Free → 14 days**

**Advanced → 15 months**

---

## Related Notes

- [[S3]]
- [[S3 Inventory]]
- [[S3 Analytics]]
- [[S3 Lifecycle Rules]]
- [[S3 Versioning]]
- [[S3 MFA Delete]]
- [[S3 SSE-KMS]]
- [[S3 Replication]]
- [[S3 Event Notifications]]
- [[S3 Transfer Acceleration]]
- [[S3 Object Ownership]]
- [[07-Monitoring/CloudWatch]]
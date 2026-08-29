## What Problem Does It Solve?

[[QuickSight]] is AWS's:

**Business intelligence and data visualization service**

It is used to create:

- Interactive dashboards
- Reports
- Charts
- Data visualizations
- Embedded analytics

Architecture:

Data Sources  
↓  
QuickSight  
↓  
Dashboards / Visualizations  
↓  
Users

> [!tip] Memory Trick
> **QuickSight = See the data**
>
> Think:
>
> **ANALYTICS → DASHBOARD**

---

## Core Concept

QuickSight sits on top of:

**Data sources**

and turns analytical data into:

**Visual business insights**

Example:

S3  
↓  
Athena  
↓  
QuickSight  
↓  
Executive Dashboard

### Killer Exam Clue

> **Need managed BI dashboards and visualizations on AWS**
>
> → **QuickSight**

---

# Common Use Cases

QuickSight is useful for:

- Executive dashboards
- Business intelligence
- Sales reporting
- Operational metrics
- Financial reporting
- Embedded analytics
- Ad hoc visual analysis

---

# Supported Data Sources

QuickSight can connect to many AWS and external data sources.

Important AWS examples include:

- [[Athena]]
- [[Redshift]]
- [[RDS]]
- Aurora
- [[S3]]

It can also connect to:

**Various external databases and SaaS data sources**

depending on configuration.

---

# QuickSight + Athena

A classic data lake architecture:

[[S3]]  
↓  
[[Athena]]  
↓  
QuickSight  
↓  
Dashboard

Athena:

**Queries the S3 data**

QuickSight:

**Visualizes the results**

### Memory Trick

**Athena = Query**

**QuickSight = Visualize**

---

# QuickSight + Redshift

Architecture:

[[Redshift]]  
↓  
QuickSight  
↓  
BI Dashboard

Use this when:

**Warehouse data**

needs to be presented to:

- Analysts
- Executives
- Business teams

### Killer Exam Clue

> **Build BI dashboards from Redshift data**
>
> → **QuickSight**

---

# QuickSight + RDS

QuickSight can visualize:

**Relational database data**

from services such as:

[[RDS]]

However, be careful when pointing BI workloads at:

**Production transactional databases**

because analytical queries can add:

**Load**

---

# QuickSight + S3

QuickSight can work with data stored in:

**S3**

often through:

- Athena
- Manifest-based ingestion
- Other supported data integrations

For SAA, the common architecture is:

**S3 → Athena → QuickSight**

---

# SPICE

One of the most important QuickSight concepts is:

**SPICE**

SPICE stands for:

**Super-fast, Parallel, In-memory Calculation Engine**

It is QuickSight's:

**In-memory analytics engine**

Architecture:

Data Source  
↓  
Import into SPICE  
↓  
QuickSight Dashboard

### Killer Exam Clue

> **Improve QuickSight dashboard performance by storing data in-memory**
>
> → **SPICE**

---

# Why Use SPICE?

SPICE can provide:

- Fast dashboard response
- Reduced load on source databases
- In-memory analytical performance
- Scalable dashboard access

### Memory Trick

**SPICE = Fast In-Memory Dashboard Data**

---

# SPICE vs Direct Query

QuickSight can either:

- Query a source directly
- Use data imported into SPICE

---

## SPICE

Think:

- Faster dashboards
- Reduced source load
- Cached/in-memory dataset

---

## Direct Query

Think:

- Query source at runtime
- Fresher source data
- More load on source system

### Killer Exam Distinction

**Need fast dashboards and reduce database load**
→ SPICE

**Need most current source data**
→ Direct Query may be appropriate

---

# SPICE Refresh

Because SPICE contains:

**Imported data**

it needs to be:

**Refreshed**

to reflect newer source data.

This can be:

- Scheduled
- Triggered through supported workflows

### Exam Principle

> **SPICE improves speed, but imported data may not always be real-time**

---

# Dashboards

A:

**Dashboard**

is a published collection of:

**Interactive visuals**

Users can:

- View charts
- Filter data
- Drill into metrics
- Explore business information

---

# Analyses

An:

**Analysis**

is the workspace where authors build:

- Visuals
- Calculations
- Filters
- Sheets

An analysis can then be published as:

**A dashboard**

### Memory Trick

**Analysis = Build**

**Dashboard = Share**

---

# Visuals

QuickSight supports many visual types, such as:

- Bar charts
- Line charts
- Tables
- KPIs
- Pie charts
- Maps
- Scatter plots

The exact chart type is less important for SAA than recognizing:

**QuickSight = Visualization / BI**

---

# QuickSight Readers vs Authors

QuickSight users can have different roles.

### Authors

Create:

- Analyses
- Dashboards
- Datasets

### Readers

Consume:

**Published dashboards**

### Memory Trick

**Author = Build**

**Reader = View**

---

# QuickSight Enterprise Features

Enterprise-oriented capabilities can include:

- Advanced security
- Row-level security
- Embedded analytics
- Directory integration
- Additional governance features

For SAA, focus on:

**Secure BI sharing and access control**

---

# Row-Level Security

QuickSight can use:

**Row-Level Security — RLS**

to control:

**Which rows each user can see**

Example:

East Region Manager  
→ Sees East Region Sales

West Region Manager  
→ Sees West Region Sales

### Killer Exam Clue

> **Different users should see different rows in the same dashboard**
>
> → **QuickSight Row-Level Security**

---

# Column-Level Security

QuickSight can also restrict access to:

**Specific columns**

Example:

Analyst  
→ Can see sales totals

HR Manager  
→ Can also see salary information

### Exam Concept

> **Restrict sensitive fields in a shared BI dataset**
>
> → **Column-Level Security**

---

# Row vs Column Security

| Requirement | Feature |
|---|---|
| Restrict Records | Row-Level Security |
| Restrict Fields | Column-Level Security |

### Memory Trick

**ROW = Which records?**

**COLUMN = Which fields?**

---

# QuickSight + IAM

QuickSight integrates with:

**AWS identity and access controls**

for managing:

- Data-source permissions
- Service access
- User access

Always use:

**Least privilege**

---

# QuickSight and Data Source Permissions

QuickSight needs permission to access:

**The underlying data source**

Examples:

QuickSight  
→ Athena

QuickSight  
→ S3

QuickSight  
→ Redshift

If dashboards cannot retrieve data:

Check:

**Data-source permissions**

---

# QuickSight + KMS

If source data or intermediate data is encrypted using:

[[06-Security/KMS]]

appropriate permissions may also be required.

### Exam Principle

> **Analytics permissions can involve both the analytics service and the underlying encrypted data source**

---

# QuickSight Embedded Analytics

QuickSight dashboards can be:

**Embedded into applications**

Architecture:

Application  
↓  
Embedded QuickSight Dashboard

This allows customers to see:

**BI visualizations inside an application**

### Killer Exam Clue

> **Embed AWS-managed analytics dashboards into a web application**
>
> → **QuickSight Embedded Analytics**

---

# Anonymous Embedding

Certain QuickSight configurations can support:

**Embedded dashboard access for users who are not individually provisioned as QuickSight users**

This is useful for:

**Customer-facing applications**

depending on edition and configuration.

---

# QuickSight + Cognito

A possible architecture:

Application User  
↓  
[[Cognito]]  
↓  
Application  
↓  
Embedded QuickSight Dashboard

This combines:

**Application authentication**

with:

**Embedded BI**

---

# Natural Language Querying

QuickSight includes capabilities that can help users ask:

**Natural-language business questions**

and receive:

**Visual answers**

For SAA, the broader association is:

> **QuickSight provides managed BI and interactive analytics**

---

# Alerts and Insights

QuickSight dashboards can support features such as:

- KPI monitoring
- Alerts
- Automated insights

These help users identify:

**Important changes in business data**

---

# QuickSight vs Athena

This distinction is heavily testable.

## [[Athena]]

Think:

**Query**

## QuickSight

Think:

**Visualize**

Architecture:

S3  
↓  
Athena  
↓  
QuickSight

### Killer Shortcut

**Run SQL**
→ Athena

**Build Dashboard**
→ QuickSight

---

# QuickSight vs Redshift

## [[Redshift]]

Think:

**Data Warehouse**

## QuickSight

Think:

**BI Visualization**

Architecture:

Redshift  
↓  
QuickSight

### Memory Trick

**Redshift = Store + Analyze**

**QuickSight = Show**

---

# QuickSight vs Glue

## [[09-Analytics/Glue]]

Think:

- ETL
- Data preparation
- Catalog
- Schema discovery

## QuickSight

Think:

**Dashboard / Visualization**

---

# QuickSight vs CloudWatch Dashboards

Both can display:

**Charts**

but they solve different problems.

## [[07-Monitoring/CloudWatch]]

Think:

- AWS infrastructure metrics
- Operational monitoring
- Alarms
- Logs

## QuickSight

Think:

- Business intelligence
- Business data
- Analytical dashboards

### Killer Shortcut

**CPU / Infrastructure Metrics**
→ CloudWatch

**Sales / Business Analytics**
→ QuickSight

---

# QuickSight vs Grafana

Grafana is often associated with:

**Operational observability dashboards**

QuickSight is primarily associated with:

**Business intelligence**

### Memory Trick

**QuickSight = Business**

**Grafana = Operations**

---

# Data Preparation

QuickSight can perform:

**Dataset preparation**

such as:

- Rename fields
- Change data types
- Filter rows
- Create calculated fields

For heavy ETL:

Think:

**Glue / EMR**

rather than treating QuickSight as:

**A full ETL platform**

---

# Calculated Fields

QuickSight can create:

**Calculated fields**

for dashboard analysis.

Example:

Profit Margin  
=  
Profit / Revenue

This helps authors create:

**Business metrics**

without changing:

**The underlying source**

---

# Dashboard Sharing

Dashboards can be shared with:

**Authorized users**

depending on:

- QuickSight user access
- Permissions
- Security configuration

Do not assume a dashboard should simply be:

**Public**

when it contains sensitive data.

---

# Performance Thinking

If dashboards are slow because:

**The source database is repeatedly queried**

consider:

**SPICE**

This can:

- Cache/import data
- Reduce source load
- Improve dashboard responsiveness

---

# Real-Time Data Consideration

If the requirement says:

**Dashboard must always display the latest source data immediately**

SPICE may introduce:

**Refresh delay**

Direct query may be more appropriate depending on:

**Performance requirements**

---

# Architecture Thinking

## Scenario 1 — Executive Sales Dashboard

Company has sales data in:

Redshift.

Executives need:

**Interactive dashboards**

Choose:

**QuickSight**

---

## Scenario 2 — S3 Data Lake Dashboard

Data lives in:

S3.

Need:

- SQL analysis
- Dashboard

Choose:

S3  
↓  
Athena  
↓  
QuickSight

---

## Scenario 3 — Slow Dashboard

QuickSight repeatedly queries:

RDS

and dashboards are slow.

Need to reduce:

**Source database load**

Choose:

**SPICE**

---

## Scenario 4 — Different Regional Managers

One dashboard contains:

All company sales.

Each manager should see:

**Only their Region**

Choose:

**Row-Level Security**

---

## Scenario 5 — Sensitive Salary Column

Managers may see:

Salary

Regular analysts may not.

Choose:

**Column-Level Security**

---

## Scenario 6 — Customer-Facing Analytics

SaaS application needs to display:

**Analytics inside its web interface**

Choose:

**QuickSight Embedded Analytics**

---

## Scenario 7 — Infrastructure Monitoring

Operations team wants:

- EC2 CPU
- Lambda errors
- ALB latency

Do NOT choose QuickSight as the primary answer.

Think:

**CloudWatch**

---

## Scenario 8 — Transform 20 TB of Raw Data

Need heavy ETL before visualization.

Do NOT rely only on QuickSight.

Think:

Glue / EMR  
↓  
Prepared Data  
↓  
QuickSight

---

# Scenario Recognition

Immediately think:

**QuickSight**

when you see:

- BI
- Dashboard
- Visualization
- Business analytics
- Executive reports
- Embedded analytics
- Interactive charts

---

## Think SPICE When You See

- In-memory analytics
- Faster dashboard
- Reduce source database load
- Cached analytical dataset

---

## Think Row-Level Security When You See

- Same dashboard
- Different users
- Different records

---

## Think Column-Level Security When You See

- Hide sensitive fields
- Same dataset
- Different visible columns

---

# Exam Traps

## Trap 1 — QuickSight Is a Data Warehouse

❌

Think:

**Redshift**

QuickSight is:

**BI / Visualization**

---

## Trap 2 — QuickSight Replaces Athena

❌

Athena:

**Queries**

QuickSight:

**Visualizes**

---

## Trap 3 — SPICE Is a Durable Primary Database

❌

SPICE is:

**In-memory analytics storage**

---

## Trap 4 — SPICE Always Shows Real-Time Source Data

❌

SPICE datasets need:

**Refreshes**

---

## Trap 5 — QuickSight Is Mainly for EC2 CPU Monitoring

❌

Think:

**CloudWatch**

---

## Trap 6 — Row-Level Security Hides Columns

❌

Row-Level Security:

**Restricts records**

Column-Level Security:

**Restricts fields**

---

## Trap 7 — QuickSight Is a Full Big Data ETL Engine

❌

For large ETL:

Think:

**Glue / EMR**

---

# Quick Cheat Sheet

| Exam Clue | Answer |
|---|---|
| AWS BI Service | QuickSight |
| Business Dashboard | QuickSight |
| Data Visualization | QuickSight |
| In-Memory Analytics | SPICE |
| Reduce Dashboard Source Load | SPICE |
| S3 Dashboard | Athena + QuickSight |
| Redshift Dashboard | QuickSight |
| Different Rows per User | Row-Level Security |
| Hide Sensitive Fields | Column-Level Security |
| Embed Dashboard in App | Embedded Analytics |
| Infrastructure Metrics | CloudWatch |
| Heavy ETL | Glue / EMR |

---

# SPICE Decision

Need:

**Fast dashboard performance**

→ SPICE

Need:

**Reduce source database load**

→ SPICE

Need:

**Always-current source data**

→ Consider Direct Query

---

# Security Decision

Need:

**User sees only their records**

→ Row-Level Security

Need:

**User cannot see sensitive fields**

→ Column-Level Security

---

# Service Decision

Need:

**Query S3**

→ Athena

Need:

**Warehouse**

→ Redshift

Need:

**ETL**

→ Glue

Need:

**Big data processing**

→ EMR

Need:

**Dashboard**

→ QuickSight

---

# Final Exam Rapid-Fire

> **BUSINESS INTELLIGENCE**
> → QUICKSIGHT
>
> **DASHBOARD**
> → QUICKSIGHT
>
> **VISUALIZATION**
> → QUICKSIGHT
>
> **IN-MEMORY ENGINE**
> → SPICE
>
> **FASTER DASHBOARD**
> → SPICE
>
> **REDUCE SOURCE LOAD**
> → SPICE
>
> **S3 DATA VISUALIZATION**
> → ATHENA + QUICKSIGHT
>
> **REDSHIFT VISUALIZATION**
> → QUICKSIGHT
>
> **DIFFERENT RECORDS PER USER**
> → ROW-LEVEL SECURITY
>
> **HIDE COLUMNS**
> → COLUMN-LEVEL SECURITY
>
> **ANALYTICS INSIDE APP**
> → EMBEDDED ANALYTICS
>
> **AWS INFRASTRUCTURE METRICS**
> → CLOUDWATCH
>
> **HEAVY ETL**
> → GLUE / EMR

---

## Master Memory Trick

> [!tip] QuickSight Master Memory Trick
> Imagine your company has a giant conference room.
>
> Data comes from:
>
> **S3 / ATHENA / REDSHIFT / RDS**
>
> QuickSight puts that data onto:
>
> **THE BIG SCREEN**
>
> That's:
>
> **QUICKSIGHT**
>
> If everyone keeps asking the database for the same dashboard data:
>
> Put a fast copy in:
>
> **SPICE**
>
> If the East manager should only see East sales:
>
> **ROW-LEVEL SECURITY**
>
> If only HR should see salaries:
>
> **COLUMN-LEVEL SECURITY**

So remember:

> **ATHENA**
> → QUERY
>
> **REDSHIFT**
> → WAREHOUSE
>
> **GLUE**
> → PREPARE
>
> **EMR**
> → PROCESS
>
> **QUICKSIGHT**
> → VISUALIZE
>
> **SPICE**
> → SPEED
>
> **RLS**
> → WHICH ROWS
>
> **CLS**
> → WHICH COLUMNS

And the killer SAA clue:

> **"Business users need interactive dashboards and visualizations from AWS data sources."**
>
> → **QuickSight**

---

## Related Notes

- [[Athena]]
- [[Redshift]]
- [[EMR]]
- [[09-Analytics/Glue]]
- [[S3]]
- [[RDS]]
- [[07-Monitoring/CloudWatch]]
- [[Cognito]]
- [[06-Security/KMS]]
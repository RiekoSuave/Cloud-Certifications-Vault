## What Problem Does It Solve?

[[Lake Formation]] helps you:

**Build, secure, and govern a data lake on AWS**

It simplifies tasks such as:

- Registering data locations
- Managing data lake permissions
- Controlling access to databases and tables
- Centralizing governance
- Integrating with analytics services

Architecture:

Data Sources  
↓  
[[S3]] Data Lake  
↓  
Lake Formation  
↓  
Athena / Redshift / EMR / Glue

> [!tip] Memory Trick
> **Lake Formation = Govern the Data Lake**

---

## Core Concept

A data lake often stores large amounts of data in:

**Amazon S3**

But storing data is only part of the problem.

You also need to control:

- Who can see which data
- Which tables users can query
- Which columns are sensitive
- Which accounts can access datasets
- Which analytics services can use the data

Lake Formation provides:

**Centralized data lake governance**

### Killer Exam Clue

> **Centrally secure and govern an S3-based data lake**
>
> → **Lake Formation**

---

# Data Lake Architecture

A common architecture:

Data Sources  
↓  
S3 Data Lake  
↓  
[[Glue Data Catalog]]  
↓  
Lake Formation Permissions  
↓  
Analytics Services

Possible consumers:

- [[Athena]]
- [[Redshift]]
- [[EMR]]
- [[Glue]]

### Memory Trick

**S3 = Store**

**Glue Catalog = Describe**

**Lake Formation = Govern**

---

# Lake Formation + S3

The actual data commonly lives in:

[[S3]]

Lake Formation helps control:

**Access to that data**

through:

- Registered data locations
- Catalog permissions
- Fine-grained data access

### Exam Principle

> **Lake Formation does not replace S3**
>
> It governs data stored in the data lake.

---

# Lake Formation + Glue Data Catalog

Lake Formation uses:

[[Glue Data Catalog]]

for:

**Metadata about databases and tables**

Architecture:

S3 Data  
↓  
Glue Data Catalog  
↓  
Lake Formation Permissions  
↓  
Analytics User

### Memory Trick

**Glue Catalog knows WHAT the data is**

**Lake Formation controls WHO can use it**

---

# Data Lake Permissions

Lake Formation can grant permissions at levels such as:

- Database
- Table
- Column

This allows more precise data access than simply granting broad:

**S3 bucket permissions**

---

# Fine-Grained Access Control

A major Lake Formation feature is:

**Fine-grained data access**

Example:

Analyst A  
→ Can query Sales table

Analyst B  
→ Can query HR table

Analyst C  
→ Can query Sales table but not Salary column

### Killer Exam Clue

> **Centrally control table- or column-level access to a data lake**
>
> → **Lake Formation**

---

# Column-Level Security

Suppose a table contains:

- EmployeeId
- Name
- Department
- Salary

Most analysts should access:

- EmployeeId
- Name
- Department

but not:

**Salary**

Lake Formation can restrict:

**Sensitive columns**

### Memory Trick

**Column Security = Hide Fields**

---

# Row-Level Security

Lake Formation can also support:

**Row-level filtering**

for supported analytics patterns.

Example:

Detroit Team  
→ Detroit records only

Chicago Team  
→ Chicago records only

### Memory Trick

**Row Security = Hide Records**

---

# Cell-Level Security

More granular access can combine:

**Row and column restrictions**

to control:

**Specific portions of a dataset**

For SAA, the key concept is:

> **Lake Formation can provide fine-grained access beyond simple bucket-level permissions**

---

# IAM vs Lake Formation Permissions

This distinction is important.

## IAM

Controls:

**AWS API permissions**

Examples:

- Can principal call Athena?
- Can principal access Lake Formation APIs?
- Can role access Glue?

## Lake Formation

Controls:

**Data lake resource permissions**

Examples:

- Can user query this database?
- Can user access this table?
- Can user read these columns?

### Memory Trick

**IAM = AWS Service Access**

**Lake Formation = Data Access**

---

# Why S3 Permissions Alone May Not Be Enough

Without Lake Formation:

You may manage access using:

- IAM policies
- S3 bucket policies
- Glue permissions

Across many users and datasets this can become:

**Complex**

Lake Formation centralizes:

**Data lake permission management**

---

# Registered Data Locations

Lake Formation can register:

**S3 locations**

that belong to the:

**Data lake**

Architecture:

S3 Bucket / Prefix  
↓  
Registered with Lake Formation  
↓  
Governed Data Location

This allows Lake Formation to participate in:

**Access control**

for those datasets.

---

# Data Lake Administrator

A:

**Data Lake Administrator**

has elevated permissions to manage:

- Data lake settings
- Permissions
- Catalog resources
- Registered locations

### SAA Principle

> **Separate data lake administration from normal data consumption**

---

# Lake Formation Grants

Permissions can be granted to principals such as:

- IAM users
- IAM roles
- AWS accounts

Depending on architecture, this enables:

**Centralized sharing**

---

# Cross-Account Data Sharing

Lake Formation can help share governed data with:

**Other AWS accounts**

Architecture:

Producer Account  
↓  
Lake Formation  
↓  
Shared Catalog Resource  
↓  
Consumer Account

### Killer Exam Clue

> **Securely share data lake tables across AWS accounts**
>
> → **Lake Formation cross-account sharing**

---

# Resource Links

In cross-account scenarios, consumers can use:

**Resource Links**

to reference shared catalog resources.

Think:

Producer Table  
↓  
Shared  
↓  
Consumer Resource Link  
↓  
Athena Query

### Exam Concept

> **Resource links provide local catalog references to shared Lake Formation resources**

---

# Tag-Based Access Control

Lake Formation supports:

**LF-Tags**

These are metadata tags used for:

**Permission management**

Example tags:

`Department = Finance`

`Sensitivity = Confidential`

Then permissions can be granted based on:

**Tags**

rather than individually configuring every table.

### Killer Exam Clue

> **Manage permissions for hundreds of data lake tables based on classification**
>
> → **LF-Tag Based Access Control**

---

# LF-Tags

LF-Tags can simplify governance for:

**Large numbers of databases and tables**

Example:

All resources tagged:

`Department=Marketing`

can be granted to:

**MarketingAnalystRole**

without manually granting:

**Every table**

### Memory Trick

**LF-Tag = Permission by Category**

---

# Named Resource Permissions vs LF-Tags

## Named Resource

Grant access directly to:

**Specific database/table**

Best when:

- Few resources
- Simple permissions

## LF-Tag Based Access Control

Grant based on:

**Tags**

Best when:

- Many datasets
- Large organizations
- Scalable governance

### Killer Shortcut

**Few specific tables**
→ Named resource grants

**Many categorized tables**
→ LF-Tags

---

# Lake Formation + Athena

Architecture:

User  
↓  
[[Athena]]  
↓  
Lake Formation Permission Check  
↓  
Glue Catalog  
↓  
S3 Data

Athena can respect:

**Lake Formation permissions**

when querying governed data.

### Killer Exam Clue

> **Analysts query S3 with Athena but must only see authorized tables/columns**
>
> → **Lake Formation + Athena**

---

# Lake Formation + Redshift

[[Redshift]] can integrate with:

**Lake Formation governed data**

for data lake analytics scenarios.

This is especially relevant when Redshift interacts with:

**S3 external data**

---

# Lake Formation + EMR

[[EMR]] can participate in:

**Lake Formation-governed data lake architectures**

depending on the analytics engine and integration.

The broader SAA takeaway:

> **Lake Formation centralizes permissions across multiple analytics services**

---

# Lake Formation + Glue

[[Glue]] commonly provides:

- Crawlers
- Data Catalog
- ETL

Lake Formation adds:

**Governance and permissions**

Architecture:

S3  
↓  
Glue Crawler  
↓  
Glue Catalog  
↓  
Lake Formation  
↓  
Athena / EMR / Redshift

### Memory Trick

**Glue = Discover + Prepare**

**Lake Formation = Secure + Govern**

---

# Lake Formation vs Glue

This distinction matters.

## Glue

Think:

- ETL
- Crawlers
- Data Catalog
- Schema discovery

## Lake Formation

Think:

- Data lake governance
- Fine-grained permissions
- Cross-account sharing
- Central access control

### Killer Shortcut

**Prepare/catalog data**
→ Glue

**Govern who can access it**
→ Lake Formation

---

# Lake Formation vs IAM

## IAM

Think:

**Service/API authorization**

## Lake Formation

Think:

**Dataset authorization**

Example:

IAM allows user to call Athena.

Lake Formation decides whether user can query:

**FinanceTable**

### SAA Principle

> **A user may have Athena permission but still lack permission to the underlying governed data**

---

# Lake Formation vs S3 Bucket Policy

## S3 Bucket Policy

Controls:

**Object-level access at the bucket/resource level**

## Lake Formation

Controls:

**Logical data lake resources**

such as:

- Databases
- Tables
- Columns
- Rows

### Memory Trick

**S3 Policy = Bucket/Object**

**Lake Formation = Data Catalog/Table**

---

# Lake Formation vs QuickSight Security

## Lake Formation

Controls:

**Data lake permissions**

## [[QuickSight]]

Can apply:

- Row-level dashboard security
- Column-level dashboard security

The difference is:

**Where access is enforced**

Lake Formation:

**At data lake access layer**

QuickSight:

**At BI presentation layer**

---

# Centralized Governance

One of the strongest reasons to use Lake Formation is:

**Central governance**

Without centralized governance:

Team A manages S3 permissions  
Team B manages Athena permissions  
Team C manages Glue permissions  
Team D manages cross-account sharing

With Lake Formation:

**Data permissions are managed more centrally**

---

# Data Lake Blueprint Concept

Lake Formation can help simplify the process of:

**Creating and organizing a data lake**

Historically, this included workflows for ingesting and cataloging data.

For SAA, focus on:

> **Lake Formation simplifies building and governing data lakes**

---

# Security and Compliance

Lake Formation can help implement:

- Least privilege
- Sensitive-data segmentation
- Central auditing
- Cross-account governance

This is especially useful in:

**Enterprise analytics environments**

---

# CloudTrail Integration

Data lake administrative activity can be audited using:

[[06-Security/CloudTrail]]

Think:

> **Who changed Lake Formation permissions?**
>
> → CloudTrail

---

# Architecture Thinking

## Scenario 1 — Central Data Lake

Company stores:

- Finance data
- HR data
- Marketing data

in S3.

Different teams should only access:

**Their own datasets**

Choose:

**Lake Formation**

---

## Scenario 2 — Sensitive Column

Analysts can query employee records but must not access:

**Salary**

Choose:

**Lake Formation column-level permissions**

---

## Scenario 3 — Different Regional Records

Managers should see:

**Only records for their Region**

Think:

**Row-level data filtering**

---

## Scenario 4 — Cross-Account Analytics

Central data account owns S3 data.

Analytics accounts need access without copying:

**All datasets**

Choose:

**Lake Formation cross-account sharing**

---

## Scenario 5 — Hundreds of Tables

Company has:

500 tables

categorized by:

- Department
- Sensitivity

Need scalable permission management.

Choose:

**LF-Tag Based Access Control**

---

## Scenario 6 — Unknown S3 Schema

Need to discover:

**Table structure**

Do NOT choose Lake Formation alone.

Choose:

**Glue Crawler**

---

## Scenario 7 — Transform Raw Data

Need to convert:

CSV → Parquet

Do NOT choose Lake Formation.

Choose:

**Glue ETL**

---

## Scenario 8 — Query Governed Data

Analyst wants to query S3 with SQL.

Need both:

- Query engine
- Fine-grained permissions

Choose:

**Athena + Lake Formation**

---

## Scenario 9 — Dashboard Permissions Only

Users already have access to source data.

Need different BI users to see:

**Different dashboard rows**

Think:

QuickSight Row-Level Security

rather than automatically:

Lake Formation.

---

# Scenario Recognition

Immediately think:

**Lake Formation**

when you see:

- Data lake governance
- Centralized data permissions
- Table-level access
- Column-level access
- Row-level access
- Cross-account data lake sharing
- LF-Tags
- S3 data lake security

---

## Think Glue When You See

- Crawlers
- Schema discovery
- ETL
- Data Catalog
- Data transformation

---

## Think IAM When You See

- AWS API permissions
- Service access
- Role permissions

---

## Think S3 Policy When You See

- Bucket/object access
- Direct S3 authorization

---

# Exam Traps

## Trap 1 — Lake Formation Stores the Data

❌

The data usually lives in:

**S3**

---

## Trap 2 — Lake Formation Replaces Glue Data Catalog

❌

Lake Formation commonly uses:

**Glue Data Catalog**

for metadata.

---

## Trap 3 — Lake Formation Is Primarily an ETL Engine

❌

Think:

**Glue**

Lake Formation is primarily:

**Governance**

---

## Trap 4 — IAM and Lake Formation Permissions Are Identical

❌

IAM:

**Service access**

Lake Formation:

**Data access**

---

## Trap 5 — S3 Bucket Policy Provides the Same Fine-Grained Table Governance

❌

Lake Formation can govern:

- Tables
- Columns
- Rows

at the data lake level.

---

## Trap 6 — LF-Tags Are Normal AWS Resource Tags Only

❌

LF-Tags are specifically used for:

**Lake Formation tag-based access control**

---

## Trap 7 — Lake Formation Is a BI Dashboard Service

❌

Think:

**QuickSight**

---

## Trap 8 — Athena Alone Provides Central Data Lake Governance

❌

Athena:

**Queries**

Lake Formation:

**Governs**

---

# Quick Cheat Sheet

| Exam Clue | Answer |
|---|---|
| Govern S3 Data Lake | Lake Formation |
| Central Data Permissions | Lake Formation |
| Table-Level Access | Lake Formation |
| Column-Level Access | Lake Formation |
| Row-Level Access | Lake Formation |
| Cross-Account Data Sharing | Lake Formation |
| Permission by Classification | LF-Tags |
| Data Lake Metadata | Glue Data Catalog |
| Discover Schema | Glue Crawler |
| Transform Data | Glue ETL |
| SQL on S3 | Athena |
| Dashboard | QuickSight |

---

# Governance Decision

Need:

**Who can call AWS service?**

→ IAM

Need:

**Who can access bucket/object?**

→ S3 IAM / Bucket Policy

Need:

**Who can access database/table/column in data lake?**

→ Lake Formation

Need:

**Who can see dashboard records?**

→ QuickSight security

---

# Glue vs Lake Formation

| Requirement | Glue | Lake Formation |
|---|---:|---:|
| ETL | ✅ | ❌ |
| Crawler | ✅ | ❌ |
| Data Catalog | ✅ | Uses It |
| Schema Discovery | ✅ | ❌ |
| Fine-Grained Data Permissions | ❌ Primary | ✅ |
| Data Lake Governance | ❌ Primary | ✅ |
| LF-Tags | ❌ | ✅ |
| Cross-Account Data Sharing | Limited Different Use | ✅ |

---

# Data Lake Memory Map

> **STORE**
> → S3
>
> **DISCOVER**
> → Glue Crawler
>
> **DESCRIBE**
> → Glue Data Catalog
>
> **TRANSFORM**
> → Glue ETL
>
> **GOVERN**
> → Lake Formation
>
> **QUERY**
> → Athena
>
> **WAREHOUSE**
> → Redshift
>
> **VISUALIZE**
> → QuickSight

---

# Final Exam Rapid-Fire

> **DATA LAKE GOVERNANCE**
> → LAKE FORMATION
>
> **TABLE PERMISSIONS**
> → LAKE FORMATION
>
> **COLUMN PERMISSIONS**
> → LAKE FORMATION
>
> **ROW FILTERING**
> → LAKE FORMATION
>
> **CROSS-ACCOUNT DATA LAKE**
> → LAKE FORMATION
>
> **TAG-BASED DATA PERMISSIONS**
> → LF-TAGS
>
> **METADATA**
> → GLUE DATA CATALOG
>
> **SCHEMA DISCOVERY**
> → GLUE CRAWLER
>
> **ETL**
> → GLUE
>
> **SQL ON S3**
> → ATHENA
>
> **DASHBOARD**
> → QUICKSIGHT
>
> **SERVICE PERMISSION**
> → IAM
>
> **BUCKET/OBJECT PERMISSION**
> → S3 POLICY

---

## Master Memory Trick

> [!tip] Lake Formation Master Memory Trick
> Imagine S3 is:
>
> **A giant lake full of company data**
>
> [[Glue]] creates:
>
> **A map of the lake**
>
> [[Athena]] lets analysts:
>
> **Fish for answers**
>
> But someone needs to decide:
>
> **WHO IS ALLOWED TO FISH WHERE?**
>
> That's:
>
> **LAKE FORMATION**
>
> Finance can fish in:
>
> **Finance tables**
>
> HR can fish in:
>
> **HR tables**
>
> Junior analysts cannot see:
>
> **Sensitive columns**
>
> And LF-Tags act like:
>
> **Access labels on sections of the lake**

So remember:

> **S3**
> → DATA
>
> **GLUE CRAWLER**
> → DISCOVER
>
> **GLUE CATALOG**
> → METADATA
>
> **GLUE ETL**
> → TRANSFORM
>
> **LAKE FORMATION**
> → GOVERN
>
> **ATHENA**
> → QUERY
>
> **QUICKSIGHT**
> → VISUALIZE

And the killer SAA question:

> **"Does the company need centralized, fine-grained access control over an S3-based data lake?"**
>
> YES
>
> → **Lake Formation**

---

## Related Notes

- [[S3]]
- [[Glue]]
- [[Glue Data Catalog]]
- [[Athena]]
- [[Redshift]]
- [[EMR]]
- [[QuickSight]]
- [[IAM]]
- [[06-Security/CloudTrail]]
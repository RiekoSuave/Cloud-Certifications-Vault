See also: [[Database Fundamentals]]

See also: [[RDS]]

See also: [[04-Databases/Aurora]]

See also: [[04-Databases/DynamoDB]]

See also: [[09-Analytics/Athena]]

See also: [[09-Analytics/QuickSight]]

## What Problem Does It Solve?

Provides a data warehouse for analyzing large amounts of data.

Redshift is designed for:

- Analytics
- Reporting
- Business Intelligence
- Data warehousing
- Large analytical queries

### Memory Trick

Redshift = Analytics Warehouse

---

## Type

Data Warehouse

OLAP Database

---

## What Is Redshift?

Redshift is AWS's data warehousing service.

It is designed to analyze large datasets rather than handle normal transactional application workloads.

Your course describes Redshift as:

OLAP

OLAP stands for:

Online Analytical Processing

### Memory Trick

Redshift = OLAP = Analytics

---

## OLTP vs OLAP

This is an important distinction.

### OLTP

OLTP stands for:

Online Transaction Processing

Designed for everyday application transactions.

Examples:

- Creating an order
- Updating a customer
- Recording a payment
- Changing account information

Think:

Application Database

---

### OLAP

OLAP stands for:

Online Analytical Processing

Designed for analyzing large amounts of data.

Examples:

- Sales reports
- Business trends
- Historical analysis
- Dashboards
- Large analytical queries

Think:

Analytics Database

---

## RDS vs Redshift

### RDS

Designed primarily for relational application workloads.

Think:

OLTP

### Redshift

Designed for:

Analytics + Data Warehousing

Think:

OLAP

| RDS | Redshift |
|---|---|
| Application database | Data warehouse |
| OLTP | OLAP |
| Transactions | Analytics |
| Relational workloads | Large analytical queries |

### Memory Trick

RDS = Run the Business

Redshift = Analyze the Business

---

## PostgreSQL Connection

Your course notes state that Redshift is based on:

PostgreSQL

However:

Redshift is NOT designed for normal PostgreSQL OLTP workloads.

It is designed for:

OLAP

### Important

PostgreSQL-based does NOT mean Redshift should replace RDS PostgreSQL for transactional applications.

---

## Columnar Storage

Redshift stores data using:

Columnar Storage

rather than traditional row-based storage.

This is useful for analytical workloads that need to process large amounts of data.

### Concept

Traditional Transaction Database:

Row → Row → Row

Redshift:

Column ↓

Column ↓

Column ↓

### Memory Trick

Redshift = Columns for Analytics

---

## Massively Parallel Processing

Redshift uses:

MPP

MPP stands for:

Massively Parallel Processing

This allows large analytical queries to be processed using parallel computing.

### Memory Trick

MPP = Many Workers Processing Data

---

## Scale

Your course describes Redshift as capable of scaling to:

Petabytes of data

The important concept is:

Redshift is designed for very large analytical datasets.

---

## SQL Interface

Redshift provides:

SQL

for querying data.

This means analysts can use SQL-style queries against data stored in the warehouse.

### Memory Trick

Redshift = Analytics with SQL

---

## Business Intelligence Integration

Your course identifies integrations with BI tools such as:

- QuickSight
- Tableau

See:

[[09-Analytics/QuickSight]]

Basic Architecture:

Data

↓

Redshift

↓

SQL Analytics

↓

QuickSight / BI Tool

↓

Dashboard

---

## Redshift Pricing Concept

Your course notes describe traditional Redshift pricing as:

Pay-as-you-go based on provisioned instances.

This means the amount of data warehouse capacity provisioned affects the cost.

---

## Redshift Serverless

Redshift also provides:

Redshift Serverless

It automatically provisions and scales the underlying data warehouse capacity.

### Memory Trick

Redshift Serverless = Analytics Without Managing Warehouse Infrastructure

---

## Why Redshift Serverless?

Redshift Serverless allows you to run analytics without manually managing the underlying data warehouse infrastructure.

AWS automatically:

- Provisions capacity
- Scales capacity

Your course describes the pricing model as:

Pay only for what you use

---

## Redshift Serverless Use Cases

Your course identifies:

- Reporting
- Dashboarding applications
- Real-time analytics

---

## Redshift vs DynamoDB

### Redshift

Analytics / Data Warehouse

### DynamoDB

NoSQL application database

| Redshift | DynamoDB |
|---|---|
| Data warehouse | NoSQL database |
| Analytics | Application data |
| OLAP | Operational workloads |
| SQL interface | Key-value |

### Memory Trick

DynamoDB = Run the App

Redshift = Analyze the Data

---

## Redshift vs Athena

Both can perform analytics, but the core concepts are different.

### Redshift

Data warehouse designed for analytical workloads.

### Athena

Serverless service that queries data directly in S3 using SQL.

| Redshift | Athena |
|---|---|
| Data warehouse | Serverless query service |
| Analytics platform | Queries S3 |
| Designed for large analytical workloads | Analyze files stored in S3 |
| SQL | SQL |

See:

[[09-Analytics/Athena]]

### Memory Trick

Redshift = Data Warehouse

Athena = SQL on S3

---

## Common Use Cases

- Data warehousing
- Business Intelligence
- Reporting
- Dashboards
- Large-scale analytics
- Historical analysis

---

## Exam Scenarios

A company needs a data warehouse for large-scale analytics.

→ Redshift

---

A company needs to analyze petabytes of business data.

→ Redshift

---

A company needs OLAP rather than OLTP.

→ Redshift

---

A company needs a relational database for normal application transactions.

→ RDS or Aurora

NOT Redshift

---

A company needs columnar storage and Massively Parallel Processing for analytical queries.

→ Redshift

---

A company wants to run analytics without managing the underlying data warehouse infrastructure.

→ Redshift Serverless

---

A company wants dashboards based on data stored in Redshift.

→ QuickSight can integrate with Redshift

---

A company wants to run serverless SQL queries directly against files in S3.

→ Athena

NOT Redshift

---

## Don't Confuse These

### RDS

Relational application database

### Aurora

High-performance AWS relational database

### DynamoDB

NoSQL application database

### Redshift

Data warehouse / Analytics

### Athena

Serverless SQL queries on S3

---

## Exam Keywords

Data warehouse

Analytics

OLAP

Columnar storage

MPP

Massively Parallel Processing

Petabytes

SQL

Business Intelligence

QuickSight

Redshift Serverless

---

## Memory Tricks

Redshift = Analytics Warehouse

Redshift = OLAP

RDS = OLTP

RDS = Run the Business

Redshift = Analyze the Business

Redshift = Columnar Storage

MPP = Many Workers

Athena = SQL on S3

Redshift Serverless = No Warehouse Infrastructure Management
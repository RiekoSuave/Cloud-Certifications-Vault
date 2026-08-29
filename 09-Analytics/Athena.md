## What Problem Does It Solve?

Allows you to query data directly in Amazon S3 without managing servers or setting up a traditional database.

Athena solves the need to analyze data stored in S3 without moving the data somewhere else first.

Think:

S3 Data

↓

Athena

↓

SQL Query

↓

Results

### Memory Trick

Athena = Query S3 with SQL

---

## Type

Serverless Analytics

---

## What Is Athena?

Amazon Athena is a serverless query service used to perform analytics against objects stored in Amazon S3.

You use:

Standard SQL

to query files directly in S3.

### Key Point

No servers to manage.

No database infrastructure to provision.

### Memory Trick

S3 + SQL = Athena

---

## Serverless

Athena is:

Serverless

AWS manages the underlying infrastructure.

You focus on:

Data

+

SQL Queries

### Exam Recognition

"Analyze data in S3 without managing servers"

→ Athena

---

## Supported File Formats

Your course identifies several file formats Athena can query:

- CSV
- JSON
- ORC
- Avro
- Parquet

### Memory Trick

Athena Queries Files in S3

---

## Pricing

Your course states:

$5 per TB of data scanned

This means the amount of data Athena scans affects the cost.

### Memory Trick

Athena = Pay for Data Scanned

---

## Cost Optimization

Because Athena charges based on the amount of data scanned, your course recommends using:

Compressed Data

or

Columnar Data

to reduce the amount of data Athena needs to scan.

### Columnar Formats

Examples from your course include:

- ORC
- Parquet

Think:

Less Data Scanned

↓

Lower Athena Cost

### Memory Trick

Scan Less = Pay Less

---

## Common Use Cases

Athena can be used for:

- Business intelligence
- Analytics
- Reporting
- Ad-hoc SQL queries
- Log analysis
- Querying S3 data

Your course specifically mentions analyzing:

- VPC Flow Logs
- ELB Logs
- CloudTrail Trails

### Memory Trick

Logs in S3 + SQL = Athena

---

## Athena vs Redshift

These can both be associated with analytics, but they solve different problems.

### Athena

Think:

Serverless SQL Queries on S3

### Redshift

Think:

Dedicated Data Warehouse

| Athena | Redshift |
| --- | --- |
| Query S3 directly | Data warehouse |
| Serverless | Dedicated analytics platform |
| Pay based on data scanned | Warehouse-oriented |
| Ad-hoc queries | Large-scale data warehousing |

### Memory Trick

Athena = QUERY S3

Redshift = DATA WAREHOUSE

---

## Athena vs QuickSight

### Athena

Queries and analyzes the data.

### QuickSight

Visualizes the data.

Think:

Athena

↓

QUERY

↓

QuickSight

↓

VISUALIZE

### Memory Trick

Athena = SQL

QuickSight = DASHBOARDS

---

## Scenario Questions

A company needs to run SQL queries directly against files stored in S3.

→ Athena

---

A company wants to analyze S3 data without provisioning servers.

→ Athena

---

A company wants to analyze CloudTrail logs stored in S3 using SQL.

→ Athena

---

A company wants to analyze VPC Flow Logs using serverless SQL.

→ Athena

---

A company wants to reduce Athena query costs.

Think:

Reduce Data Scanned

Use:

Compressed / Columnar Data

---

A company needs interactive business dashboards.

→ QuickSight

NOT Athena

---

A company needs a dedicated data warehouse.

→ Redshift

NOT Athena

---

## Don't Confuse These

Athena = Query S3

QuickSight = Visualize Data

Redshift = Data Warehouse

EMR = Big Data Processing

Kinesis = Real-Time Streaming

---

## Exam Keywords

Amazon Athena

S3

SQL

Serverless

Query S3

Data Scanned

CSV

JSON

ORC

Avro

Parquet

Log Analysis

Ad-Hoc Queries

---

## Memory Tricks

Athena = Query S3 with SQL

S3 + SQL = Athena

Athena = Serverless

Athena = Pay for Data Scanned

Scan Less = Pay Less

Logs in S3 + SQL = Athena

---

## Quick Cheat Sheet

Athena = Query S3 with SQL

Athena = Serverless

Athena = $5 per TB Scanned

Compressed / Columnar Data = Lower Cost

Athena Supports CSV, JSON, ORC, Avro & Parquet

VPC Flow Logs + SQL = Athena

ELB Logs + SQL = Athena

CloudTrail Logs + SQL = Athena

Athena = QUERY

QuickSight = VISUALIZE

Redshift = DATA WAREHOUSE
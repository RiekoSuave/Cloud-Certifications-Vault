## What Problem Does It Solve?

Prepares and transforms data for analytics.

AWS Glue solves the problem of preparing raw data so it can be analyzed by other AWS analytics services.

Think:

Raw Data

↓

Glue

↓

Prepare & Transform

↓

Analytics

### Memory Trick

Glue = Prepare Data for Analytics

---

## Type

Serverless ETL Service

---

## What Is AWS Glue?

AWS Glue is a managed:

Extract

Transform

Load

service.

ETL stands for:

Extract → Get the Data

Transform → Prepare the Data

Load → Send the Data Where It Needs to Go

### Memory Trick

Glue = ETL

---

## Serverless

AWS Glue is:

Fully Serverless

You do not need to manage the underlying infrastructure.

### Exam Recognition

"Serverless ETL service"

→ Glue

---

## What Is ETL?

### Extract

Retrieve data from a source.

↓

### Transform

Prepare or change the data for analytics.

↓

### Load

Load the prepared data for use by analytics services.

### Memory Trick

ETL = Extract → Transform → Load

---

## Glue Data Catalog

AWS Glue also includes:

Glue Data Catalog

The Data Catalog provides a catalog of datasets.

Your course states that the Glue Data Catalog can be used by:

- Athena
- Redshift
- EMR

Think:

Data

↓

Glue Data Catalog

↓

Athena / Redshift / EMR

### Memory Trick

Glue Data Catalog = Catalog of Datasets

---

## Common Use Cases

- Preparing data for analytics
- Transforming data
- ETL workloads
- Cataloging datasets

---

## Glue vs Athena

### Glue

Prepares and transforms the data.

### Athena

Queries the data.

Think:

Glue

↓

PREPARE

↓

Athena

↓

QUERY

### Memory Trick

Glue = PREPARE

Athena = QUERY

---

## Glue vs EMR

### Glue

Think:

Serverless ETL

### EMR

Think:

Big Data Processing

### Memory Trick

Glue = ETL

EMR = BIG DATA

---

## Analytics Workflow

A simple way to remember how these services can work together:

Raw Data

↓

Glue

PREPARE

↓

Athena

QUERY

↓

QuickSight

VISUALIZE

---

## Scenario Questions

A company needs a managed ETL service.

→ Glue

---

A company needs a fully serverless service to prepare and transform data for analytics.

→ Glue

---

A company needs to catalog datasets for use with Athena.

→ Glue Data Catalog

---

A company needs a data catalog that can be used by Athena, Redshift, and EMR.

→ Glue Data Catalog

---

A company needs to query data in S3 using serverless SQL.

→ Athena

NOT Glue

---

A company needs Hadoop or Spark for big data processing.

→ EMR

NOT Glue

---

A company needs interactive dashboards.

→ QuickSight

NOT Glue

---

## Don't Confuse These

Glue = Prepare / Transform Data

Athena = Query S3

EMR = Big Data Processing

Kinesis = Real-Time Streaming

QuickSight = Dashboards

---

## Exam Keywords

AWS Glue

ETL

Extract

Transform

Load

Serverless

Data Preparation

Data Transformation

Glue Data Catalog

Analytics

---

## Memory Tricks

Glue = ETL

Glue = PREPARE

Glue = Prepare Data for Analytics

Glue Data Catalog = Catalog of Datasets

Athena = QUERY

EMR = PROCESS

Kinesis = STREAM

QuickSight = VISUALIZE

---

## Quick Cheat Sheet

Glue = Managed ETL

Glue = Fully Serverless

ETL = Extract + Transform + Load

Glue = Prepare & Transform Data

Glue Data Catalog = Catalog of Datasets

Glue Data Catalog → Athena

Glue Data Catalog → Redshift

Glue Data Catalog → EMR

Glue = PREPARE

Athena = QUERY

EMR = PROCESS

Kinesis = STREAM

QuickSight = VISUALIZE
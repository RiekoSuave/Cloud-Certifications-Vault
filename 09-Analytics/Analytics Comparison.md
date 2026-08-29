## Analytics Services Comparison

| Service | Best For | Memory Shortcut |
| --- | --- | --- |
| Athena | Query data in S3 | SQL on S3 |
| EMR | Big data processing | Hadoop / Spark |
| Glue | Prepare & transform data | ETL |
| Kinesis | Real-time streaming | Streaming data |
| QuickSight | Dashboards & visualization | BI |

---

## Key Differences

### Athena

Think:

SQL

S3

Serverless Queries

→ Athena

Athena allows you to query data stored directly in Amazon S3 using standard SQL.

### Memory Trick

Athena = QUERY

---

### EMR

Think:

Big Data

Hadoop

Spark

Large Clusters

→ EMR

EMR is used to process massive amounts of data using big-data frameworks.

### Memory Trick

EMR = PROCESS

---

### Glue

Think:

ETL

Prepare Data

Transform Data

Data Catalog

→ Glue

Glue is a fully serverless managed ETL service used to prepare and transform data for analytics.

### Memory Trick

Glue = PREPARE

---

### Kinesis

Think:

Real-Time

Streaming

Data As It Arrives

→ Kinesis

Kinesis collects, processes, and analyzes real-time streaming data.

### Memory Trick

Kinesis = STREAM

---

### QuickSight

Think:

Dashboards

Charts

Business Intelligence

Visualization

→ QuickSight

QuickSight is a serverless business intelligence service used to create interactive dashboards.

### Memory Trick

QuickSight = VISUALIZE

---

## Most Important Comparison

| If the Question Says... | Think... |
| --- | --- |
| Query S3 using SQL | Athena |
| Serverless SQL on S3 | Athena |
| Analyze logs stored in S3 | Athena |
| Hadoop | EMR |
| Apache Spark | EMR |
| Big data processing | EMR |
| Managed ETL | Glue |
| Extract, Transform, Load | Glue |
| Prepare data for analytics | Glue |
| Data Catalog | Glue |
| Real-time streaming | Kinesis |
| Data as it arrives | Kinesis |
| Streaming ingestion | Kinesis |
| Interactive dashboards | QuickSight |
| Business intelligence | QuickSight |
| Data visualization | QuickSight |

---

## Analytics Workflow

A useful way to visualize how some of these services can work together:

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

### Memory Trick

Glue = PREPARE

Athena = QUERY

QuickSight = VISUALIZE

---

## Glue Data Catalog

The Glue Data Catalog can be used by:

Athena

Redshift

EMR

Think:

Datasets

↓

Glue Data Catalog

↓

Athena / Redshift / EMR

### Memory Trick

Glue Data Catalog = Catalog of Datasets

---

## Athena vs Glue

### Athena

Queries data.

### Glue

Prepares and transforms data.

### Memory Trick

Athena = QUERY

Glue = PREPARE

---

## Athena vs QuickSight

### Athena

Queries data using SQL.

### QuickSight

Visualizes data using dashboards.

### Memory Trick

Athena = QUERY

QuickSight = VISUALIZE

---

## EMR vs Kinesis

### EMR

Big data processing.

### Kinesis

Real-time streaming.

### Memory Trick

EMR = PROCESS

Kinesis = STREAM

---

## Athena vs EMR

### Athena

Serverless SQL queries against S3.

### EMR

Large-scale big data processing using frameworks such as Hadoop and Spark.

### Memory Trick

Athena = QUERY

EMR = PROCESS

---

## Scenario Speed Round

Need to query files in S3 using SQL?

→ Athena

---

Need serverless SQL analytics against S3?

→ Athena

---

Need Hadoop or Spark?

→ EMR

---

Need to process massive amounts of big data?

→ EMR

---

Need a fully serverless ETL service?

→ Glue

---

Need to prepare and transform data for analytics?

→ Glue

---

Need a catalog of datasets for Athena, Redshift, or EMR?

→ Glue Data Catalog

---

Need to process streaming data in real time?

→ Kinesis

---

Need low-latency streaming ingestion?

→ Kinesis Data Streams

---

Need interactive business dashboards?

→ QuickSight

---

Need to visualize data?

→ QuickSight

---

## Don't Confuse These

Athena = Query S3

EMR = Big Data Processing

Glue = ETL / Data Preparation

Kinesis = Real-Time Streaming

QuickSight = Dashboards

---

## Ultimate Memory Pattern

QUERY = Athena

PROCESS = EMR

PREPARE = Glue

STREAM = Kinesis

VISUALIZE = QuickSight

---

## One-Line Exam Review

Athena = Query S3 with SQL

EMR = Process Big Data with Hadoop / Spark

Glue = Prepare & Transform Data with ETL

Kinesis = Stream Data in Real Time

QuickSight = Visualize Data with Dashboards
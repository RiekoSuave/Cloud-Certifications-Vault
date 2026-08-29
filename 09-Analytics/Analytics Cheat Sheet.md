## Core Services

Athena = Query S3

EMR = Big Data Processing

Glue = ETL / Prepare Data

Kinesis = Real-Time Streaming

QuickSight = Dashboards

---

## Ultimate Memory Pattern

Athena = QUERY

EMR = PROCESS

Glue = PREPARE

Kinesis = STREAM

QuickSight = VISUALIZE

---

## Athena

Think:

SQL

S3

Serverless

### Key Exam Facts

Query S3 using SQL?

→ Athena

Serverless SQL analytics?

→ Athena

Analyze logs stored in S3?

→ Athena

Pay based on data scanned?

→ Athena

### Cost Memory

Scan Less = Pay Less

Compressed / Columnar Data = Lower Cost

### Memory Trick

Athena = QUERY

---

## EMR

Think:

Big Data

Hadoop

Spark

EC2 Clusters

### Key Exam Facts

Process massive datasets?

→ EMR

Hadoop?

→ EMR

Apache Spark?

→ EMR

Large big-data clusters?

→ EMR

### Memory Trick

EMR = PROCESS

---

## Glue

Think:

ETL

Extract

Transform

Load

Prepare Data

Data Catalog

### Key Exam Facts

Managed ETL?

→ Glue

Serverless ETL?

→ Glue

Prepare and transform data for analytics?

→ Glue

Catalog datasets?

→ Glue Data Catalog

### Glue Data Catalog

Can be used by:

Athena

Redshift

EMR

### Memory Trick

Glue = PREPARE

---

## Kinesis

Think:

Real-Time

Streaming

Data As It Arrives

### Key Exam Facts

Real-time streaming?

→ Kinesis

Streaming data ingestion?

→ Kinesis

Low-latency streaming ingestion?

→ Kinesis Data Streams

Deliver streaming data to S3, Redshift, or OpenSearch?

→ Data Firehose

### Memory Trick

Kinesis = STREAM

---

## QuickSight

Think:

Business Intelligence

Dashboards

Visualization

### Key Exam Facts

Interactive dashboards?

→ QuickSight

Business intelligence?

→ QuickSight

Visualize data?

→ QuickSight

Serverless BI?

→ QuickSight

### Memory Trick

QuickSight = VISUALIZE

---

## Most Important Comparisons

| Question | Service |
| --- | --- |
| Query S3 with SQL? | Athena |
| Big data processing? | EMR |
| Hadoop / Spark? | EMR |
| ETL? | Glue |
| Prepare / transform data? | Glue |
| Data Catalog? | Glue |
| Real-time streaming? | Kinesis |
| Interactive dashboards? | QuickSight |
| Business intelligence? | QuickSight |

---

## Analytics Workflow

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

### Remember

Glue = Prepare It

Athena = Query It

QuickSight = Show It

---

## Don't Confuse These

Athena = QUERY S3

EMR = PROCESS BIG DATA

Glue = PREPARE / ETL

Kinesis = STREAM REAL-TIME DATA

QuickSight = VISUALIZE DATA

---

## Scenario Speed Round

Need SQL queries directly against S3?

→ Athena

Need Hadoop or Spark?

→ EMR

Need serverless ETL?

→ Glue

Need to prepare data for analytics?

→ Glue

Need real-time streaming?

→ Kinesis

Need interactive dashboards?

→ QuickSight

---

## Exam Keywords

Athena = SQL + S3 + Serverless

EMR = Hadoop + Spark + Big Data

Glue = ETL + Data Catalog

Kinesis = Streaming + Real-Time

QuickSight = BI + Dashboards

---

## Final Exam Memory

QUERY = Athena

PROCESS = EMR

PREPARE = Glue

STREAM = Kinesis

VISUALIZE = QuickSight

---

## One-Line Review

Athena = Query It

EMR = Process It

Glue = Prepare It

Kinesis = Stream It

QuickSight = Visualize It
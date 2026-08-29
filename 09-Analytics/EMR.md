## What Problem Does It Solve?

Processes and analyzes massive amounts of big data.

Amazon EMR solves the complexity of building and managing large big-data processing clusters.

Instead of manually configuring hundreds of servers:

Big Data

↓

EMR Cluster

↓

Process & Analyze Data

### Memory Trick

EMR = Big Data Clusters

---

## Type

Big Data Processing

---

## What Is EMR?

EMR stands for:

Elastic MapReduce

EMR helps create and manage Hadoop clusters used to analyze and process vast amounts of data.

These clusters can contain:

Hundreds of EC2 Instances

### Memory Trick

EMR = Elastic MapReduce

EMR = Big Data on EC2 Clusters

---

## Big Data Frameworks

Your course identifies several technologies supported by EMR:

- Hadoop
- Apache Spark
- HBase
- Presto
- Flink

For the CCP exam, the two strongest associations are:

Hadoop

+

Spark

→ EMR

### Memory Trick

Hadoop / Spark = EMR

---

## Managed Cluster Setup

EMR takes care of:

Provisioning

+

Configuration

of the big-data cluster.

Instead of manually configuring the underlying infrastructure, EMR helps manage the cluster setup.

### Memory Trick

EMR = Managed Big Data Clusters

---

## EC2 Integration

EMR clusters can consist of hundreds of:

EC2 Instances

Your course also states that EMR integrates with:

- Auto Scaling
- Spot Instances

### Auto Scaling

Helps adjust cluster capacity.

### Spot Instances

Can be used as part of EMR clusters.

### Memory Trick

EMR = EC2 Cluster for Big Data

---

## Common Use Cases

Your course identifies:

- Data processing
- Machine learning
- Web indexing
- Big data workloads

### Exam Recognition

"Process vast amounts of data"

→ EMR

"Create a Hadoop cluster"

→ EMR

"Apache Spark processing"

→ EMR

---

## EMR vs Kinesis

This is the most important comparison for this note.

### EMR

Think:

BIG DATA PROCESSING

### Kinesis

Think:

REAL-TIME STREAMING DATA

| EMR | Kinesis |
| --- | --- |
| Big data processing | Real-time streaming |
| Hadoop | Streaming ingestion |
| Spark | Process data as it arrives |
| EC2 clusters | Managed streaming service |

### Memory Trick

EMR = BIG DATA

Kinesis = STREAMING

---

## EMR vs Athena

### EMR

Processes massive datasets using big-data frameworks and clusters.

### Athena

Queries data directly in S3 using SQL.

### Memory Trick

EMR = PROCESS BIG DATA

Athena = QUERY S3

---

## Scenario Questions

A company needs to process massive amounts of big data using Hadoop.

→ EMR

---

A company needs an Apache Spark environment in AWS.

→ EMR

---

A company needs a cluster containing many EC2 instances to process large datasets.

→ EMR

---

A company wants AWS to handle provisioning and configuration of its Hadoop cluster.

→ EMR

---

A company needs to process real-time streaming data as it arrives.

→ Kinesis

NOT EMR

---

A company wants to run serverless SQL queries against files in S3.

→ Athena

NOT EMR

---

## Don't Confuse These

EMR = Big Data Processing

Kinesis = Real-Time Streaming

Athena = SQL Queries on S3

QuickSight = Dashboards & Visualization

---

## Exam Keywords

Amazon EMR

Elastic MapReduce

Big Data

Hadoop

Apache Spark

HBase

Presto

Flink

EC2 Clusters

Data Processing

Machine Learning

Web Indexing

Auto Scaling

Spot Instances

---

## Memory Tricks

EMR = Elastic MapReduce

EMR = Big Data Clusters

Hadoop = EMR

Spark = EMR

EMR = PROCESS

Kinesis = STREAM

Athena = QUERY

QuickSight = VISUALIZE

---

## Quick Cheat Sheet

EMR = Elastic MapReduce

EMR = Big Data Processing

EMR = Hadoop + Spark

EMR = EC2 Clusters

EMR Handles Provisioning + Configuration

EMR Supports Auto Scaling

EMR Integrates with Spot Instances

EMR = PROCESS BIG DATA

Kinesis = REAL-TIME STREAMING

Athena = QUERY S3

QuickSight = DASHBOARDS
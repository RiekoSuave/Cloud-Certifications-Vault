## What Problem Does It Solve?

Collects, processes, and analyzes streaming data in real time.

Kinesis solves the problem of handling data that is continuously being generated and needs to be processed as it arrives.

Think:

Streaming Data

↓

Kinesis

↓

Real-Time Processing

### Memory Trick

Kinesis = Streaming Data

---

## Type

Real-Time Streaming Analytics

---

## What Is Kinesis?

Amazon Kinesis is a managed service used to:

Collect

Process

Analyze

real-time streaming data at scale.

### Most Important Exam Association

Kinesis = Real-Time Big Data Streaming

---

## What Is Streaming Data?

Streaming data is data that is continuously generated.

Examples include:

- Website clickstreams
- IoT sensor data
- Application logs
- Real-time events

Instead of waiting for a large batch of data:

Data Arrives

↓

Kinesis Processes It

↓

In Real Time

### Memory Trick

Streaming = Data As It Arrives

---

## Kinesis Data Streams

Kinesis Data Streams provides:

Low-Latency Streaming

It can ingest streaming data at scale from:

Hundreds of Thousands of Sources

Think:

Many Data Sources

↓

Kinesis Data Streams

↓

Real-Time Data Stream

### Memory Trick

Data Streams = INGEST STREAMING DATA

---

## Data Firehose

Data Firehose helps load streaming data into destinations.

Your course specifically identifies:

- Amazon S3
- Amazon Redshift
- Amazon OpenSearch

Think:

Streaming Data

↓

Data Firehose

↓

S3 / Redshift / OpenSearch

### Memory Trick

Firehose = DELIVER STREAMING DATA

---

## Data Streams vs Data Firehose

Keep this high-level for CCP.

### Kinesis Data Streams

Think:

INGEST

### Data Firehose

Think:

DELIVER

| Service | Think |
| --- | --- |
| Kinesis Data Streams | Ingest streaming data |
| Data Firehose | Deliver streaming data to destinations |

### Memory Trick

Streams = INGEST

Firehose = DELIVER

---

## Common Use Cases

- Real-time streaming analytics
- IoT data
- Website clickstreams
- Application logs
- Streaming ingestion
- Real-time event processing

---

## Kinesis vs EMR

This is the most important comparison.

### Kinesis

Think:

REAL-TIME STREAMING

### EMR

Think:

BIG DATA PROCESSING

| Kinesis | EMR |
| --- | --- |
| Streaming data | Big data processing |
| Real-time | Large-scale processing |
| Data as it arrives | Hadoop / Spark |
| Streaming ingestion | Big data clusters |

### Memory Trick

Kinesis = STREAM

EMR = PROCESS

---

## Kinesis vs Athena

### Kinesis

Handles:

Real-Time Streaming Data

### Athena

Queries:

Data Stored in S3

### Memory Trick

Kinesis = STREAM

Athena = QUERY

---

## Scenario Questions

A company needs to process data as it arrives in real time.

→ Kinesis

---

A company needs to analyze real-time streaming data.

→ Kinesis

---

A company receives continuous data from thousands of IoT devices.

→ Kinesis

---

A company needs low-latency streaming ingestion at scale.

→ Kinesis Data Streams

---

A company needs to deliver streaming data into Amazon S3.

→ Data Firehose

---

A company needs to deliver streaming data into Amazon Redshift.

→ Data Firehose

---

A company needs Hadoop or Spark to process massive datasets.

→ EMR

NOT Kinesis

---

A company needs to run serverless SQL queries against data stored in S3.

→ Athena

NOT Kinesis

---

## Don't Confuse These

Kinesis = Real-Time Streaming

EMR = Big Data Processing

Athena = Query S3

QuickSight = Dashboards

---

## Exam Keywords

Amazon Kinesis

Real-Time

Streaming

Streaming Data

Data Ingestion

Low Latency

Kinesis Data Streams

Data Firehose

IoT Data

Clickstreams

---

## Memory Tricks

Kinesis = Streaming Data

Kinesis = REAL-TIME

Streaming = Data As It Arrives

Data Streams = INGEST

Firehose = DELIVER

Kinesis = STREAM

EMR = PROCESS

Athena = QUERY

QuickSight = VISUALIZE

---

## Quick Cheat Sheet

Kinesis = Real-Time Big Data Streaming

Kinesis = Data As It Arrives

Data Streams = Low-Latency Streaming Ingestion

Data Firehose = Deliver Streaming Data

Firehose → S3

Firehose → Redshift

Firehose → OpenSearch

Kinesis = STREAM

EMR = PROCESS BIG DATA

Athena = QUERY S3

QuickSight = DASHBOARDS
## What Problem Does It Solve?

[[EMR]] is AWS's managed:

**Big data processing platform**

It is designed for workloads that use frameworks such as:

- Apache Spark
- Apache Hadoop
- Apache Hive
- Apache HBase
- Apache Flink

Architecture:

Large Dataset  
↓  
EMR Cluster  
↓  
Distributed Processing  
↓  
Results

> [!tip] Memory Trick
> **EMR = Managed big data cluster**
>
> Think:
>
> **SPARK / HADOOP / BIG DATA**

---

## Core Concept

EMR helps you process:

**Very large datasets**

using:

**Distributed computing**

Instead of one server doing all the work:

Large Job  
↓  
Split Across Many Nodes  
↓  
Process in Parallel  
↓  
Combine Results

### Killer Exam Clue

> **Need managed Spark or Hadoop processing on AWS**
>
> → **EMR**

---

# Common Use Cases

EMR is useful for:

- Big data analytics
- ETL
- Machine learning preprocessing
- Log processing
- Clickstream analysis
- Genomic processing
- Large-scale transformations
- Data lake processing

---

# EMR Cluster Architecture

A traditional EMR cluster can contain:

- Primary Node
- Core Nodes
- Task Nodes

---

# Primary Node

The:

**Primary Node**

manages the cluster.

It coordinates:

- Cluster management
- Job scheduling
- Resource coordination
- Framework services

### Memory Trick

**Primary = Manager**

---

# Core Nodes

Core nodes:

- Process data
- Store data for distributed filesystems such as HDFS

Think:

**Workers + Storage**

---

# Task Nodes

Task nodes:

**Perform processing only**

They do not store:

**HDFS data**

This makes them useful for:

**Adding extra compute capacity**

### Memory Trick

**Core = Compute + Data**

**Task = Compute Only**

---

# Node Type Comparison

| Node Type | Main Role |
|---|---|
| Primary | Cluster Management |
| Core | Processing + HDFS Storage |
| Task | Processing Only |

---

# EMR and EC2

Traditional EMR clusters run on:

**EC2 instances**

You can choose:

- Instance families
- Instance counts
- On-Demand
- Spot
- Auto Scaling

This gives significant control over:

**Big data compute infrastructure**

---

# EMR Serverless

EMR also provides:

**EMR Serverless**

which lets you run supported big data frameworks without managing:

**Clusters**

AWS manages:

- Capacity
- Scaling
- Underlying infrastructure

### Killer Exam Clue

> **Run Spark/Hive jobs without managing EMR clusters**
>
> → **EMR Serverless**

---

# Traditional EMR vs EMR Serverless

| Requirement | EMR on EC2 | EMR Serverless |
|---|---:|---:|
| Choose Instances | ✅ | ❌ |
| Manage Cluster | ✅ | ❌ |
| Spark / Hive | ✅ | ✅ |
| Infrastructure Control | High | Lower |
| Minimum Ops | ❌ | ✅ |

### Memory Trick

**EMR EC2 = Control**

**EMR Serverless = Simplicity**

---

# Apache Spark

Apache Spark is designed for:

**Fast distributed data processing**

Common uses:

- ETL
- Analytics
- Machine learning
- Streaming
- Large transformations

### Killer Exam Clue

> **Need distributed Spark processing**
>
> → **EMR**

---

# Apache Hadoop

Hadoop provides:

**Distributed storage and processing**

Traditionally associated with:

- HDFS
- MapReduce

EMR makes it easier to run:

**Hadoop ecosystems**

without manually building clusters.

---

# Apache Hive

Hive provides:

**SQL-like querying**

over large datasets in big data environments.

Think:

Big Data  
↓  
Hive  
↓  
SQL-Like Queries

---

# Apache HBase

HBase is a:

**Distributed NoSQL database**

often associated with:

**Hadoop ecosystems**

It can be useful for:

- Large sparse datasets
- Low-latency access
- Distributed big data workloads

---

# EMR + S3

One of the most important architectures:

[[S3]]  
↓  
EMR  
↓  
Distributed Processing  
↓  
S3

S3 can act as:

**Durable data lake storage**

while EMR provides:

**Compute**

### Killer Exam Clue

> **Process large datasets stored in S3 using Spark**
>
> → **EMR**

---

# EMRFS

EMR can access S3 using:

**EMRFS**

This allows big data frameworks to interact with:

**S3-backed datasets**

instead of relying only on:

**HDFS**

### Memory Trick

**S3 = Durable Data**

**EMR = Processing**

---

# HDFS

HDFS is:

**Hadoop Distributed File System**

It stores data across:

**Cluster nodes**

Important distinction:

HDFS is tied more closely to:

**The cluster lifecycle**

while S3 provides:

**Durable external storage**

---

# S3 vs HDFS

## S3

Think:

- Durable
- Independent of EMR cluster
- Data lake
- Decoupled storage

## HDFS

Think:

- Cluster-local distributed storage
- Tied to cluster nodes

### Killer SAA Principle

> **Use S3 when data should survive cluster termination**

---

# Transient Clusters

A common EMR cost pattern:

Create Cluster  
↓  
Run Job  
↓  
Store Results in S3  
↓  
Terminate Cluster

This is called a:

**Transient cluster pattern**

### Killer Exam Clue

> **Run periodic big data jobs and minimize cost**
>
> → **Create EMR cluster for job, store results in S3, terminate cluster**

---

# Long-Running Clusters

Some organizations maintain:

**Persistent EMR clusters**

when workloads run:

- Continuously
- Frequently
- Interactively

Tradeoff:

**Higher ongoing cost**

but faster availability for repeated jobs.

---

# EMR + Spot Instances

EMR can use:

**EC2 Spot Instances**

to reduce compute cost.

Spot is especially useful for:

**Task nodes**

because task nodes do not store:

**HDFS data**

### Killer Exam Clue

> **Reduce EMR cost for fault-tolerant processing capacity**
>
> → **Use Spot Task Nodes**

---

# Why Spot Is Safer for Task Nodes

If a task node is interrupted:

Processing capacity decreases temporarily

but:

**HDFS data is not lost from that node**

because task nodes do not store HDFS blocks.

### Memory Trick

**Task Nodes = Best Spot Candidates**

---

# Spot on Core Nodes

Core nodes contain:

**HDFS data**

Therefore Spot interruptions can have:

**Greater impact**

than interruptions of task nodes.

For critical persistent HDFS workloads:

Be more cautious with:

**Spot core nodes**

---

# On-Demand Nodes

Use On-Demand when:

- Reliability matters
- Capacity must be stable
- Interruptions are unacceptable

A common strategy:

Primary/Core baseline  
→ On-Demand

Additional Task capacity  
→ Spot

---

# Instance Fleets

EMR:

**Instance Fleets**

can use multiple:

- Instance types
- Purchase options

to improve:

- Capacity availability
- Cost optimization

### Exam Concept

> **Use diversified instance choices to improve EMR capacity and cost efficiency**

---

# Managed Scaling

EMR can use:

**Managed Scaling**

to automatically adjust:

**Cluster capacity**

based on workload demand.

Architecture:

Workload ↑  
↓  
More EMR Capacity

Workload ↓  
↓  
Less Capacity

### Killer Exam Clue

> **Automatically resize EMR cluster based on workload**
>
> → **EMR Managed Scaling**

---

# EMR Auto Scaling

EMR can also scale resources using:

**Scaling policies**

The exam-level idea:

> **EMR capacity can dynamically adjust to workload**

---

# EMR + Glue Data Catalog

EMR can use:

[[Glue Data Catalog]]

as a shared:

**Metadata repository**

Architecture:

S3 Data  
↓  
Glue Data Catalog  
↓  
EMR / Athena / Other Analytics Services

This allows multiple analytics services to share:

**Table definitions and schemas**

---

# EMR + Athena

Both can analyze data in:

**S3**

But they solve different problems.

## [[Athena]]

Think:

- Serverless SQL
- Ad hoc queries
- Minimal setup

## EMR

Think:

- Spark
- Hadoop
- Custom distributed processing
- Complex transformations

### Killer Shortcut

**SQL on S3**
→ Athena

**Spark/Hadoop**
→ EMR

---

# EMR vs Glue

Both can perform:

**Data processing / ETL**

but their focus differs.

## [[09-Analytics/Glue]]

Think:

- Serverless ETL
- Data integration
- Crawlers
- Catalog
- Managed Spark ETL

## EMR

Think:

- Broader big data platform
- More framework control
- Spark/Hadoop ecosystem
- Cluster-level flexibility

### Memory Trick

**Glue = Managed ETL**

**EMR = Big Data Platform**

---

# EMR vs Redshift

## EMR

Think:

**Process / Transform Big Data**

## [[Redshift]]

Think:

**Store and query warehouse data**

A common architecture:

Raw Data  
↓  
EMR  
↓  
Transform  
↓  
Redshift  
↓  
BI

### Killer Shortcut

**PROCESS**
→ EMR

**WAREHOUSE**
→ Redshift

---

# EMR vs Lambda

## [[Lambda]]

Think:

- Short-lived functions
- Event-driven
- 15-minute maximum

## EMR

Think:

- Large datasets
- Distributed jobs
- Spark/Hadoop
- Long-running processing

### Killer Exam Clue

> **Job must process terabytes using distributed Spark**
>
> → **EMR, not Lambda**

---

# EMR vs AWS Batch

## EMR

Think:

- Big data frameworks
- Spark/Hadoop
- Distributed data analytics

## AWS Batch

Think:

- General batch compute jobs
- Containerized batch processing

### Shortcut

**Spark/Hadoop**
→ EMR

**General compute batch**
→ AWS Batch

---

# EMR vs Kinesis

## EMR

Think:

**Processing platform**

## [[20-SAA/10-Messaging/Kinesis Data Streams]]

Think:

**Streaming ingestion**

They can work together:

Streaming Data  
↓  
Kinesis  
↓  
Processing  
↓  
Analytics

---

# EMR + Lake Formation

EMR can participate in an S3 data lake architecture governed through:

**Lake Formation**

This can help centralize:

- Permissions
- Data lake governance
- Catalog integration

For SAA, recognize the architecture:

S3 Data Lake  
↓  
Glue Catalog / Lake Formation  
↓  
EMR / Athena / Redshift

---

# Encryption

EMR can support encryption for:

- Data at rest
- Data in transit

Depending on architecture, services such as:

[[06-Security/KMS]]

can be involved.

---

# Security Configurations

EMR:

**Security Configurations**

can centralize security settings such as:

- Encryption
- Authentication
- Data protection options

### Exam Concept

> **Use EMR security configurations to apply consistent cluster security settings**

---

# IAM Roles

EMR uses IAM roles for:

**AWS service access**

Different components may require permission to:

- Read S3
- Write S3
- Access Glue
- Call other AWS services

Follow:

**Least privilege**

---

# Networking

EMR clusters can run inside:

**A VPC**

You control:

- Subnets
- Security groups
- Routing
- Network access

Private subnets are useful when:

**Public Internet exposure is unnecessary**

---

# High Availability

A big data workload should avoid relying on:

**A single fragile processing node**

EMR manages much of the framework deployment, but architecture still matters for:

- Node failure
- Data durability
- Cluster design

Using S3 for persistent data improves:

**Resilience to cluster loss**

---

# Step Execution

EMR jobs can be submitted as:

**Steps**

A step represents:

**A unit of work**

Examples:

- Spark job
- Hive query
- Hadoop job

Architecture:

EMR Cluster  
↓  
Step 1  
↓  
Step 2  
↓  
Step 3

---

# EMR Step Functions Integration

[[Step Functions]] can orchestrate:

**EMR jobs**

Architecture:

Step Functions  
↓  
Start EMR Job  
↓  
Wait  
↓  
Next Workflow Step

### Killer Exam Clue

> **Coordinate an EMR data-processing job inside a larger workflow**
>
> → **Step Functions + EMR**

---

# Architecture Thinking

## Scenario 1 — Spark on S3

Company has:

50 TB of raw logs in S3.

Need:

**Distributed Spark transformations**

Choose:

**EMR**

---

## Scenario 2 — Simple SQL

Company only needs occasional:

**SQL queries on S3**

Do NOT create an EMR cluster.

Choose:

**Athena**

---

## Scenario 3 — ETL Warehouse Load

Raw data in S3 needs:

Complex Spark transformations

before loading into Redshift.

Choose:

S3  
↓  
EMR  
↓  
Redshift

---

## Scenario 4 — Periodic Monthly Job

Large processing job runs:

Once per month.

Need minimum ongoing cost.

Choose:

Transient EMR Cluster  
↓  
Run Job  
↓  
S3 Results  
↓  
Terminate Cluster

---

## Scenario 5 — Cost Optimization

EMR needs extra fault-tolerant compute capacity.

Choose:

**Spot Task Nodes**

---

## Scenario 6 — Persistent Data

Cluster may be terminated after processing.

Data must survive.

Store data in:

**S3**

rather than relying only on:

HDFS.

---

## Scenario 7 — Dynamic Workload

Cluster load varies dramatically throughout the day.

Choose:

**Managed Scaling**

---

## Scenario 8 — No Cluster Management

Team needs Spark but does not want to provision:

**EMR clusters**

Choose:

**EMR Serverless**

---

## Scenario 9 — General Container Batch Job

Workload is:

**Not Spark/Hadoop**

and simply needs thousands of containerized batch jobs.

Think:

**AWS Batch**

rather than EMR.

---

## Scenario 10 — Shared Metadata

Athena and EMR both need to understand:

**The same S3 tables**

Choose:

**Glue Data Catalog**

---

# Scenario Recognition

Immediately think:

**EMR**

when you see:

- Apache Spark
- Hadoop
- Hive
- HBase
- Big data cluster
- Distributed processing
- Petabyte-scale transformations
- Large ETL processing

---

## Think Athena When You See

- SQL on S3
- Ad hoc analytics
- No cluster
- Simple interactive querying

---

## Think Glue When You See

- Serverless ETL
- Crawlers
- Schema discovery
- Data Catalog

---

## Think Redshift When You See

- Data warehouse
- OLAP
- BI analytics
- Repeated analytical SQL

---

## Think Spot Task Nodes When You See

- EMR cost optimization
- Fault-tolerant extra capacity
- Interruptible workers

---

# Exam Traps

## Trap 1 — EMR Is a Data Warehouse

❌

Think:

**Redshift**

EMR is primarily:

**Big data processing**

---

## Trap 2 — EMR Is Best for Simple SQL on S3

❌

Think:

**Athena**

---

## Trap 3 — Task Nodes Store HDFS Data

❌

Task nodes:

**Compute only**

---

## Trap 4 — HDFS Data Automatically Survives Cluster Termination

❌

For durable independent storage:

**Use S3**

---

## Trap 5 — Spot Is Always Safest for Primary/Core Nodes

❌

Task nodes are generally:

**Better Spot candidates**

---

## Trap 6 — EMR Requires Permanent Clusters

❌

Transient clusters can:

**Run jobs and terminate**

---

## Trap 7 — EMR Serverless Means Spark Is No Longer Available

❌

EMR Serverless is designed to run supported:

**Big data frameworks without cluster management**

---

## Trap 8 — Lambda Is Better for Multi-Hour Spark Jobs

❌

Lambda has:

**15-minute maximum runtime**

and is not a Spark cluster.

---

# Quick Cheat Sheet

| Exam Clue | Answer |
|---|---|
| Managed Spark/Hadoop | EMR |
| Distributed Big Data Processing | EMR |
| Cluster Manager | Primary Node |
| Processing + HDFS | Core Node |
| Processing Only | Task Node |
| Best Spot Candidate | Task Node |
| Durable Data Storage | S3 |
| Cluster-Local Storage | HDFS |
| Auto Resize Cluster | Managed Scaling |
| No Cluster Management | EMR Serverless |
| SQL on S3 | Athena |
| ETL / Catalog | Glue |
| Data Warehouse | Redshift |
| General Container Batch | AWS Batch |
| Shared Metadata | Glue Data Catalog |

---

# Node Memory Map

> **PRIMARY**
> → MANAGE
>
> **CORE**
> → COMPUTE + STORE
>
> **TASK**
> → COMPUTE ONLY

---

# Service Decision

Need:

**Spark / Hadoop**

→ EMR

Need:

**Serverless Spark without cluster management**

→ EMR Serverless

Need:

**SQL directly on S3**

→ Athena

Need:

**Serverless ETL**

→ Glue

Need:

**Warehouse analytics**

→ Redshift

Need:

**General batch compute**

→ AWS Batch

---

# Final Exam Rapid-Fire

> **SPARK**
> → EMR
>
> **HADOOP**
> → EMR
>
> **BIG DATA CLUSTER**
> → EMR
>
> **CLUSTER MANAGER**
> → PRIMARY NODE
>
> **HDFS + COMPUTE**
> → CORE NODE
>
> **COMPUTE ONLY**
> → TASK NODE
>
> **SPOT COST SAVINGS**
> → TASK NODES
>
> **DURABLE DATA**
> → S3
>
> **CLUSTER-LOCAL DATA**
> → HDFS
>
> **AUTO RESIZE**
> → MANAGED SCALING
>
> **NO CLUSTER**
> → EMR SERVERLESS
>
> **SQL ON S3**
> → ATHENA
>
> **SERVERLESS ETL**
> → GLUE
>
> **DATA WAREHOUSE**
> → REDSHIFT
>
> **GENERAL BATCH**
> → AWS BATCH

---

## Master Memory Trick

> [!tip] EMR Master Memory Trick
> Imagine a huge construction project.
>
> The:
>
> **PRIMARY NODE**
> → Foreman
>
> The:
>
> **CORE NODES**
> → Workers who also store building materials
>
> The:
>
> **TASK NODES**
> → Extra temporary workers
>
> The raw materials are kept safely in:
>
> **S3**
>
> The workers use tools such as:
>
> **SPARK / HADOOP**
>
> When the project ends:
>
> **Terminate the cluster**
>
> but keep the materials and results:
>
> **In S3**

So remember:

> **EMR**
> → BIG DATA PROCESSING
>
> **SPARK / HADOOP**
> → EMR
>
> **PRIMARY**
> → MANAGE
>
> **CORE**
> → COMPUTE + HDFS
>
> **TASK**
> → COMPUTE ONLY
>
> **SPOT**
> → TASK NODES
>
> **S3**
> → DURABLE STORAGE
>
> **HDFS**
> → CLUSTER STORAGE
>
> **SERVERLESS**
> → NO CLUSTER MANAGEMENT

And the killer SAA question:

> **"Does the workload require distributed Spark/Hadoop processing rather than just SQL queries?"**
>
> YES
>
> → **EMR**

---

## Related Notes

- [[Athena]]
- [[Redshift]]
- [[09-Analytics/Glue]]
- [[Glue Data Catalog]]
- [[S3]]
- [[20-SAA/10-Messaging/Kinesis Data Streams]]
- [[Step Functions]]
- [[06-Security/KMS]]
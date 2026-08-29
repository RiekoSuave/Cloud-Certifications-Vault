## Core Exam Map

> [!tip] Master Shortcut
> **SQL on S3** → [[Athena]]
>
> **Big data processing** → [[EMR]]
>
> **ETL / Crawlers / Catalog** → [[Glue]]
>
> **Data warehouse** → [[Redshift]]
>
> **BI dashboards** → [[QuickSight]]
>
> **Data lake governance** → [[Lake Formation]]
>
> **AWS-native streaming** → [[Kinesis Data Streams]]
>
> **Managed stream delivery** → [[Kinesis Data Firehose]]
>
> **Real-time stream processing** → [[Kinesis Data Analytics]]
>
> **Full-text search / log analytics** → [[OpenSearch]]
>
> **Apache Kafka** → [[MSK]]

---

# Athena

Think:

**Serverless SQL queries directly against data in S3**

### Killer Exam Clues

- SQL on S3
- Ad hoc queries
- Serverless analytics
- Pay per data scanned
- Query logs stored in S3
- Analyze Parquet / ORC
- No infrastructure to manage

### Cost Optimization

Reduce:

**Data scanned**

using:

- Columnar formats
- Compression
- Partitioning

### Exam Shortcut

> **"Query data in S3 using SQL without loading it into a database."**
>
> → **Athena**

### Memory Trick

**Athena = SQL on S3**

---

# EMR

Think:

**Managed big data cluster**

Common frameworks include:

- Hadoop
- Spark
- Hive
- Flink

### Killer Exam Clues

- Hadoop
- Spark
- Massive distributed processing
- Big data cluster
- Petabyte-scale processing
- Custom big data frameworks

### Node Types

**Primary Node**
→ Manages cluster

**Core Node**
→ Process + Store

**Task Node**
→ Process only

### Cost Optimization

Task nodes are good candidates for:

**Spot Instances**

because losing them does not remove:

**HDFS data**

### Exam Shortcut

> **"Run Apache Spark/Hadoop processing at massive scale."**
>
> → **EMR**

### Memory Trick

**EMR = Big Data Cluster**

---

# Glue

Think:

**Serverless ETL + metadata**

Major components:

- Glue ETL
- Glue Crawlers
- Glue Data Catalog

### Glue Crawler

Discovers:

**Schema**

### Glue Data Catalog

Stores:

**Metadata**

### Glue ETL

Transforms:

**Data**

### Killer Exam Clues

- Discover schema
- Crawl S3
- ETL
- Transform datasets
- Central metadata catalog

### Exam Shortcut

> **"Automatically discover the schema of data stored in S3."**
>
> → **Glue Crawler**

### Memory Trick

**CRAWLER = DISCOVER**

**CATALOG = DESCRIBE**

**ETL = TRANSFORM**

---

# Redshift

Think:

**Petabyte-scale analytical data warehouse**

Designed for:

**OLAP**

not:

**OLTP**

### Killer Exam Clues

- Data warehouse
- Complex analytical SQL
- BI reporting
- Columnar storage
- Massive analytical datasets
- Structured analytics

### Redshift Spectrum

Queries:

**Data directly in S3**

without loading everything into:

**Redshift tables**

### Exam Shortcut

> **"Company needs a petabyte-scale SQL data warehouse for BI."**
>
> → **Redshift**

### Memory Trick

**Redshift = Warehouse**

---

# QuickSight

Think:

**Serverless Business Intelligence**

Used for:

- Dashboards
- Reports
- Visualizations
- Business analytics

### SPICE

**Super-fast, Parallel, In-memory Calculation Engine**

Provides:

**Fast in-memory analytics**

### Killer Exam Clues

- Executive dashboard
- Business intelligence
- Visualize AWS data
- Interactive reports
- Embedded dashboards

### Exam Shortcut

> **"Executives need interactive dashboards from analytical data."**
>
> → **QuickSight**

### Memory Trick

**QuickSight = See the Business**

---

# Lake Formation

Think:

**Build and govern an S3-based data lake**

Provides centralized control over:

- Databases
- Tables
- Columns
- Rows
- Cross-account data sharing

### LF-Tags

Use:

**Tag-based access control**

to scale permissions across:

**Many datasets**

### Killer Exam Clues

- Data lake governance
- Fine-grained data permissions
- Table-level security
- Column-level security
- Cross-account data lake sharing

### Exam Shortcut

> **"Centrally govern access to hundreds of data lake tables."**
>
> → **Lake Formation**

### Memory Trick

**Lake Formation = Govern the Lake**

---

# Kinesis Data Streams

Think:

**Durable real-time streaming**

Key concepts:

- Producers
- Consumers
- Shards
- Partition keys
- Replay
- Ordering within shard

### Enhanced Fan-Out

Provides:

**Dedicated consumer throughput**

### Killer Exam Clues

- Real-time stream
- Replay events
- Multiple consumers
- Ordered streaming records
- Shards
- Partition keys

### Exam Shortcut

> **"Multiple applications must independently process and replay a live event stream."**
>
> → **Kinesis Data Streams**

### Memory Trick

**Data Streams = Carry + Retain**

---

# Kinesis Data Firehose

Think:

**Managed streaming delivery**

Common destinations:

- S3
- Redshift
- OpenSearch

Can also provide:

- Buffering
- Lambda transformation
- Format conversion
- Compression

### Redshift Path

Firehose  
↓  
S3  
↓  
Redshift

### Killer Exam Clues

- Stream data to S3
- Stream data to Redshift
- Stream data to OpenSearch
- No shard management
- Convert streaming JSON to Parquet

### Exam Shortcut

> **"Continuously deliver streaming logs into S3 with minimal administration."**
>
> → **Kinesis Data Firehose**

### Memory Trick

**Firehose = Deliver**

---

# Kinesis Data Analytics

Think:

**Real-time stream processing**

Strongly associated with:

**Apache Flink**

Use for:

- Stateful processing
- Rolling calculations
- Time windows
- Streaming aggregations
- Pattern detection

### Killer Exam Clues

- Apache Flink
- Real-time analytics
- Rolling 5-minute average
- Stateful streaming
- Continuous aggregation

### Exam Shortcut

> **"Calculate rolling metrics continuously from a live stream."**
>
> → **Kinesis Data Analytics**

### Memory Trick

**Data Analytics = Think About the Stream**

---

# OpenSearch

Think:

**Search + Index + Log Analytics**

Use for:

- Full-text search
- Product search
- Search relevance
- Log analytics
- Near-real-time searching

### UltraWarm

Think:

**Older, less frequently accessed searchable data**

### Killer Exam Clues

- Full-text search
- Search engine
- Product search
- Searchable logs
- Indexed documents
- OpenSearch Dashboards

### Exam Shortcut

> **"Customers need to search product descriptions using natural text."**
>
> → **OpenSearch**

### Memory Trick

**OpenSearch = Search**

---

# MSK

Think:

**Managed Apache Kafka**

Key Kafka concepts:

- Topics
- Partitions
- Brokers
- Producers
- Consumers
- Consumer groups

### MSK Serverless

Think:

**Kafka with less broker-capacity management**

### MSK Connect

Think:

**Managed Kafka Connect**

### Killer Exam Clues

- Apache Kafka
- Existing Kafka workload
- Kafka migration
- Kafka topics
- Kafka consumer groups
- Kafka Connect

### Exam Shortcut

> **"Company wants to migrate its existing Apache Kafka applications to a managed AWS service without rewriting them."**
>
> → **MSK**

### Memory Trick

**MSK = Managed Kafka**

---

# Athena vs Redshift

| Requirement | Athena | Redshift |
|---|---:|---:|
| SQL | ✅ | ✅ |
| Query S3 Directly | ✅ Primary | Spectrum |
| Serverless | ✅ | Serverless Option Available |
| Data Warehouse | ❌ | ✅ |
| Ad Hoc S3 Queries | ✅ | Possible |
| Repeated Complex BI | Possible | ✅ |
| Infrastructure Management | Minimal | Depends on Deployment |

### Killer Shortcut

**SQL directly on S3**
→ Athena

**Dedicated analytical warehouse**
→ Redshift

---

# Athena vs OpenSearch

## Athena

Think:

**SQL**

## OpenSearch

Think:

**SEARCH**

### Example

Historical Parquet files in S3  
→ Athena

Search millions of log messages for:

`ERROR payment timeout`

→ OpenSearch

---

# Glue vs Lake Formation

## Glue

Think:

**Prepare and catalog**

## Lake Formation

Think:

**Govern**

### Killer Shortcut

**Discover schema**
→ Glue Crawler

**Transform data**
→ Glue ETL

**Store metadata**
→ Glue Data Catalog

**Control access to data lake**
→ Lake Formation

---

# EMR vs Glue

## EMR

Think:

- Cluster
- Spark
- Hadoop
- Custom big-data frameworks
- More control

## Glue

Think:

- Serverless ETL
- Less infrastructure management
- Crawlers
- Data Catalog

### Killer Shortcut

**Need Spark/Hadoop cluster control**
→ EMR

**Need managed/serverless ETL**
→ Glue

---

# Redshift vs EMR

## Redshift

Think:

**SQL data warehouse**

## EMR

Think:

**Distributed big-data processing**

### Killer Shortcut

**Warehouse analytics**
→ Redshift

**Spark/Hadoop processing**
→ EMR

---

# Redshift vs OpenSearch

## Redshift

Think:

**Structured OLAP**

## OpenSearch

Think:

**Full-text / log search**

### Killer Shortcut

**Sales warehouse**
→ Redshift

**Search application logs**
→ OpenSearch

---

# QuickSight vs OpenSearch Dashboards

## QuickSight

Think:

**Business Intelligence**

Examples:

- Revenue dashboards
- Executive reports
- Sales KPIs

## OpenSearch Dashboards

Think:

**Search and operational analytics**

Examples:

- Log dashboards
- Search analytics
- Operational events

### Memory Trick

**QuickSight = Business**

**OpenSearch Dashboards = Logs/Search**

---

# Kinesis Family

| Requirement | Service |
|---|---|
| Ingest + Retain Stream | [[Kinesis Data Streams]] |
| Analyze Live Stream | [[Kinesis Data Analytics]] |
| Deliver Stream | [[Kinesis Data Firehose]] |

### Master Shortcut

> **STREAMS**
> → CARRY
>
> **ANALYTICS**
> → THINK
>
> **FIREHOSE**
> → DELIVER

---

# Kinesis Data Streams vs MSK

## Kinesis Data Streams

Think:

**AWS-native streaming**

Keywords:

- Shards
- Partition key
- Enhanced Fan-Out

## MSK

Think:

**Apache Kafka**

Keywords:

- Topics
- Partitions
- Brokers
- Consumer groups

### Killer Shortcut

**AWS-native**
→ Kinesis Data Streams

**Kafka-compatible**
→ MSK

---

# Streaming vs Queue vs Event Routing

Need:

**Durable AWS-native stream**
→ Kinesis Data Streams

Need:

**Apache Kafka stream**
→ MSK

Need:

**Managed delivery**
→ Kinesis Data Firehose

Need:

**Work queue**
→ [[SQS]]

Need:

**Push fan-out**
→ [[SNS]]

Need:

**Rule-based event routing**
→ [[20-SAA/10-Messaging/EventBridge]]

---

# Data Analytics Architecture Map

## Data Lake

Data Sources  
↓  
S3  
↓  
Glue Crawler  
↓  
Glue Data Catalog  
↓  
Lake Formation  
↓  
Athena

Think:

> **STORE → DISCOVER → DESCRIBE → GOVERN → QUERY**

---

## Data Warehouse

Data Sources  
↓  
ETL  
↓  
Redshift  
↓  
QuickSight

Think:

> **PREPARE → WAREHOUSE → VISUALIZE**

---

## Real-Time Stream

Producer  
↓  
Kinesis Data Streams  
↓  
Kinesis Data Analytics  
↓  
Firehose  
↓  
S3 / Redshift / OpenSearch

Think:

> **INGEST → ANALYZE → DELIVER**

---

## Kafka

Producer  
↓  
MSK  
↓  
Kafka Topic  
↓  
Consumer Groups

Think:

> **PRODUCE → TOPIC → CONSUME**

---

## Search

Application Database  
↓  
Replication / Stream / Lambda  
↓  
OpenSearch  
↓  
OpenSearch Dashboards

Think:

> **STORE → INDEX → SEARCH**

---

# Scenario Recognition

## "Query S3 with SQL"

→ **Athena**

## "Run Spark/Hadoop"

→ **EMR**

## "Discover S3 schema"

→ **Glue Crawler**

## "Serverless ETL"

→ **Glue**

## "Central metadata repository"

→ **Glue Data Catalog**

## "Petabyte-scale warehouse"

→ **Redshift**

## "Executive dashboards"

→ **QuickSight**

## "Govern S3 data lake"

→ **Lake Formation**

## "Replay real-time events"

→ **Kinesis Data Streams**

## "Deliver stream to S3"

→ **Kinesis Data Firehose**

## "Rolling calculations on live stream"

→ **Kinesis Data Analytics**

## "Full-text search"

→ **OpenSearch**

## "Apache Kafka"

→ **MSK**

---

# Common Exam Traps

## Trap 1 — Athena Is a Database

❌

Athena:

**Queries data where it already lives in S3**

---

## Trap 2 — Redshift Is for OLTP

❌

Redshift:

**OLAP / analytics**

---

## Trap 3 — Glue Is Primarily a Data Lake Permission Service

❌

Think:

**ETL + Catalog**

Data lake governance:

**Lake Formation**

---

## Trap 4 — Lake Formation Stores the Data

❌

Data generally lives in:

**S3**

---

## Trap 5 — QuickSight Is a Search Engine

❌

QuickSight:

**BI**

OpenSearch:

**Search**

---

## Trap 6 — Firehose Is for Replay

❌

Replay:

**Kinesis Data Streams**

Firehose:

**Delivery**

---

## Trap 7 — Kinesis Data Streams and MSK Are the Same

❌

Kinesis:

**AWS-native**

MSK:

**Apache Kafka**

---

## Trap 8 — OpenSearch Should Automatically Replace the Primary Database

❌

OpenSearch commonly acts as:

**Search/index layer**

while RDS or DynamoDB remains:

**System of record**

---

## Trap 9 — EMR and Glue Are Always Interchangeable

❌

EMR:

**Big-data cluster/framework control**

Glue:

**Managed/serverless ETL**

---

# One-Word Memory Map

| Service | Remember |
|---|---|
| Athena | QUERY |
| EMR | PROCESS |
| Glue | ETL |
| Redshift | WAREHOUSE |
| QuickSight | VISUALIZE |
| Lake Formation | GOVERN |
| Kinesis Data Streams | STREAM |
| Kinesis Data Firehose | DELIVER |
| Kinesis Data Analytics | ANALYZE |
| OpenSearch | SEARCH |
| MSK | KAFKA |

---

# Final Exam Rapid-Fire

> **SQL ON S3**
> → ATHENA
>
> **SPARK / HADOOP**
> → EMR
>
> **ETL**
> → GLUE
>
> **CRAWLER**
> → GLUE
>
> **METADATA**
> → GLUE DATA CATALOG
>
> **WAREHOUSE**
> → REDSHIFT
>
> **BI**
> → QUICKSIGHT
>
> **SPICE**
> → QUICKSIGHT
>
> **DATA LAKE GOVERNANCE**
> → LAKE FORMATION
>
> **LF-TAGS**
> → LAKE FORMATION
>
> **AWS-NATIVE STREAM**
> → KINESIS DATA STREAMS
>
> **SHARDS**
> → KINESIS DATA STREAMS
>
> **REPLAY**
> → KINESIS DATA STREAMS
>
> **MANAGED STREAM DELIVERY**
> → FIREHOSE
>
> **STREAM → S3**
> → FIREHOSE
>
> **REAL-TIME STREAM ANALYTICS**
> → KINESIS DATA ANALYTICS
>
> **APACHE FLINK**
> → KINESIS DATA ANALYTICS
>
> **FULL-TEXT SEARCH**
> → OPENSEARCH
>
> **LOG ANALYTICS**
> → OPENSEARCH
>
> **APACHE KAFKA**
> → MSK
>
> **KAFKA CONNECT**
> → MSK CONNECT

---

## Master Memory Trick

> [!tip] Data Analytics Master Memory Trick
> Imagine AWS data moving through a factory.
>
> First, data is stored in:
>
> **S3**
>
> Need to discover what is inside?
>
> **GLUE CRAWLER**
>
> Need metadata?
>
> **GLUE DATA CATALOG**
>
> Need to transform it?
>
> **GLUE**
>
> Need to control who can access the lake?
>
> **LAKE FORMATION**
>
> Need SQL directly on the files?
>
> **ATHENA**
>
> Need a giant analytical warehouse?
>
> **REDSHIFT**
>
> Need big Spark/Hadoop processing?
>
> **EMR**
>
> Need executives to see dashboards?
>
> **QUICKSIGHT**
>
> Need real-time events flowing through AWS?
>
> **KINESIS DATA STREAMS**
>
> Need to analyze that stream while it moves?
>
> **KINESIS DATA ANALYTICS**
>
> Need to deliver that stream somewhere?
>
> **FIREHOSE**
>
> Need to search words or logs?
>
> **OPENSEARCH**
>
> Need Kafka?
>
> **MSK**

So memorize:

> **ATHENA**
> → QUERY
>
> **EMR**
> → PROCESS
>
> **GLUE**
> → TRANSFORM
>
> **REDSHIFT**
> → WAREHOUSE
>
> **QUICKSIGHT**
> → VISUALIZE
>
> **LAKE FORMATION**
> → GOVERN
>
> **KINESIS STREAMS**
> → INGEST
>
> **KINESIS ANALYTICS**
> → ANALYZE
>
> **FIREHOSE**
> → DELIVER
>
> **OPENSEARCH**
> → SEARCH
>
> **MSK**
> → KAFKA

---

## Related Notes

- [[Athena]]
- [[EMR]]
- [[Glue]]
- [[Glue Data Catalog]]
- [[Redshift]]
- [[QuickSight]]
- [[Lake Formation]]
- [[Kinesis Data Streams]]
- [[Kinesis Data Firehose]]
- [[Kinesis Data Analytics]]
- [[OpenSearch]]
- [[MSK]]
- [[S3]]
- [[SQS]]
- [[SNS]]
- [[20-SAA/10-Messaging/EventBridge]]
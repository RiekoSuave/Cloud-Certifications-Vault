## What Problem Does It Solve?

[[Timestream]] is a **fully managed, fast, scalable, serverless time-series database**.

It solves the problem of:

> **"How do I efficiently store and analyze massive amounts of data that changes over time?"**

Time-series data consists of records associated with a **timestamp**.

Examples:

- CPU utilization every minute
- Temperature readings every second
- IoT sensor measurements
- Application performance metrics
- Stock or financial measurements
- Operational telemetry

Instead of using a traditional relational database for trillions of timestamped events, [[Timestream]] is purpose-built for this type of workload.

> [!tip] Memory Trick
> **Timestream = Time + Stream of measurements**
>
> If the data is primarily:
>
> **Value + Timestamp → Think Timestream**

---

## What Is Time-Series Data?

Time-series data represents how something changes **over time**.

Example:

| Timestamp | Device | Temperature |
|---|---|---:|
| 10:00 | Sensor-A | 70°F |
| 10:01 | Sensor-A | 71°F |
| 10:02 | Sensor-A | 73°F |
| 10:03 | Sensor-A | 72°F |

The important dimension is:

**TIME**

The application may need to answer questions such as:

- What was the average temperature over the last hour?
- How has CPU utilization changed today?
- Which devices showed abnormal readings?
- What was the maximum measurement during the last 24 hours?
- What trends are occurring in near real-time?

These are classic [[Timestream]] workloads.

---

## Timestream Core Architecture

[[Timestream]] is:

- **Fully managed**
- **Serverless**
- **Fast**
- **Scalable**
- Designed specifically for time-series data
- Automatically scales capacity up and down

You do not provision or manage database servers.

Architecture thinking:

Data Producers  
↓  
[[Timestream]]  
↓  
Analytics / Applications

AWS handles the underlying database infrastructure and scaling.

> [!tip] Architecture Rule
> **Timestamped data + serverless + massive scale = Timestream**

---

## Automatic Scaling

[[Timestream]] automatically scales:

**Up → when workload demand increases**

**Down → when workload demand decreases**

This means you don't need to manually provision database capacity for changing time-series workloads.

Example:

Normal IoT Traffic  
↓  
[[Timestream]]

Traffic Spike  
↓  
[[Timestream]] automatically scales

Traffic Drops  
↓  
[[Timestream]] automatically scales down

This makes Timestream useful for workloads where the number of incoming measurements can vary significantly.

---

## Massive Time-Series Scale

[[Timestream]] is designed to store and analyze:

**Trillions of events per day**

This is important for workloads such as:

- Large IoT fleets
- Infrastructure monitoring
- Application telemetry
- Operational metrics
- Real-time analytics

The key SAA idea:

> Don't force massive timestamped datasets into a traditional relational database when AWS provides a purpose-built time-series database.

---

## Performance and Cost

The SAA slides describe Timestream as being:

- Thousands of times faster than relational databases for time-series workloads
- A fraction of the cost of relational databases for these workloads

The exact numbers are less important than the architecture lesson:

**Purpose-built database → better fit for time-series workloads than a general relational database**

---

## SQL Compatibility

[[Timestream]] supports **SQL-compatible queries**.

This allows applications and analytics tools to query time-series data using familiar SQL-style syntax.

### Important Exam Distinction

SQL compatibility does **not** mean Timestream is a traditional relational database like:

- [[RDS]]
- [[Aurora]]

It is still a:

**Purpose-built time-series database**

> [!tip] Memory Trick
> **SQL syntax doesn't automatically mean RDS.**
>
> Always identify the workload first.

---

## Scheduled Queries

[[Timestream]] supports **scheduled queries**.

Scheduled queries allow queries to run automatically on a defined schedule.

This can be useful for:

- Aggregating measurements
- Calculating statistics
- Creating summarized datasets
- Preparing time-series data for analytics

Think:

Raw Measurements  
↓  
[[Timestream]]  
↓  
Scheduled Query  
↓  
Aggregated Results

---

## Multi-Measure Records

[[Timestream]] supports **multi-measure records**.

Instead of storing only one measurement per timestamp, multiple related measurements can be associated with the same event.

Example:

Device-A  
Timestamp: 10:00

Measurements:

- Temperature: 72
- Humidity: 45
- Pressure: 1012

This is useful when a device or system generates multiple related measurements at the same time.

---

## Timestream Storage Tiering

One of the most important Timestream architecture concepts is **automatic storage tiering**.

Timestream separates data based on how recent it is.

### Recent Data

Recent data is kept in:

**Memory**

Why?

Recent measurements are often queried frequently and need fast access.

### Historical Data

Older data is moved into:

**Cost-optimized storage**

Why?

Historical data is usually queried less frequently.

Conceptually:

Incoming Time-Series Data  
↓  
[[Timestream]]  
↓  
Recent Data → Memory  
↓  
Older Data → Cost-Optimized Storage

### Architecture Thinking

Think:

**Hot recent data → Fast memory**

**Cold historical data → Cheaper storage**

AWS handles this tiering automatically.

> [!tip] Memory Trick
> **Timestream remembers NOW quickly and HISTORY cheaply.**

---

## Built-In Time-Series Analytics

[[Timestream]] includes built-in functions designed specifically for time-series analysis.

These functions help identify:

- Trends
- Patterns
- Changes over time
- Near real-time insights

Example:

IoT Sensors  
↓  
[[Timestream]]  
↓  
Analyze Measurements  
↓  
Detect Pattern / Trend

This is another reason Timestream is better suited for time-series workloads than a general-purpose database.

---

## Timestream Architecture

The SAA slides show multiple AWS services sending data into [[Timestream]].

### Data Sources

Potential producers include:

- [[AWS IoT]]
- [[20-SAA/10-Messaging/Kinesis Data Streams]]
- [[02-Compute/Lambda]]
- [[Prometheus]]
- [[MSK]]
- [[Kinesis Data Analytics]]

Conceptually:

[[AWS IoT]] ──────────────┐  
[[20-SAA/10-Messaging/Kinesis Data Streams]] ─┤  
[[02-Compute/Lambda]] ────────────────┤  
[[Prometheus]] ────────────┤  
[[MSK]] ───────────────────┤  
                          ↓  
                    [[Timestream]]

These services can generate or process data that ultimately becomes time-series records.

---

## Consuming Timestream Data

Applications and analytics services can query data stored in [[Timestream]].

The slides show integrations including:

- [[09-Analytics/QuickSight]]
- [[SageMaker]]
- JDBC-compatible applications

Architecture:

Data Sources  
↓  
[[Timestream]]  
↓  
├── [[09-Analytics/QuickSight]]  
├── [[SageMaker]]  
└── JDBC Applications

### Architecture Thinking

Think of Timestream as the specialized database sitting between:

**Real-time data producers**

and

**Analytics / visualization / machine learning consumers**

---

## Common Use Cases

### IoT Applications

IoT devices continuously generate timestamped measurements.

Example:

Sensors  
↓  
[[AWS IoT]]  
↓  
[[Timestream]]

Measurements might include:

- Temperature
- Humidity
- Pressure
- Device status
- Battery level

**Choose → [[Timestream]]**

---

### Operational Applications

Applications can store operational measurements such as:

- Request latency
- Error rates
- Transaction counts
- System health metrics

Example:

Application  
↓  
[[Timestream]]  
↓  
Operational Analytics

---

### Real-Time Analytics

Timestream can analyze incoming time-series information in near real-time.

Example:

Streaming Data  
↓  
[[20-SAA/10-Messaging/Kinesis Data Streams]]  
↓  
[[Timestream]]  
↓  
[[09-Analytics/QuickSight]]

This could support dashboards showing rapidly changing metrics.

---

## Architecture Thinking

### Scenario 1 — Millions of IoT Sensors

A company operates millions of IoT devices.

Each device sends:

- Temperature
- Humidity
- Battery level
- Timestamp

The company needs to store and analyze massive amounts of this information.

**Choose → [[Timestream]]**

Why?

The workload is fundamentally **time-series data**.

---

### Scenario 2 — Infrastructure Metrics

A company collects:

- CPU utilization
- Memory utilization
- Request latency
- Error rates

Every few seconds from thousands of systems.

They need historical trend analysis.

**Choose → [[Timestream]]**

Why?

These are timestamped measurements changing over time.

---

### Scenario 3 — Traditional Transactional Application

An application needs to store:

- Customers
- Orders
- Payments
- Products

The application requires relational transactions and SQL joins.

**Choose → [[RDS]] / [[Aurora]]**

Not [[Timestream]].

The workload is relational OLTP, not time-series analytics.

---

### Scenario 4 — Cassandra Compatibility

A company stores IoT data but specifically requires:

- Apache Cassandra compatibility
- CQL

**Choose → [[Keyspaces]]**

Not [[Timestream]].

The Cassandra requirement is the deciding factor.

---

### Scenario 5 — Real-Time IoT Analytics

Millions of devices generate measurements that must be:

1. Collected
2. Stored as time-series data
3. Analyzed
4. Displayed on dashboards

Possible architecture:

IoT Devices  
↓  
[[AWS IoT]]  
↓  
[[Timestream]]  
↓  
[[09-Analytics/QuickSight]]

---

## Timestream vs Keyspaces

This is an important exam distinction because the slides mention time-series data as a possible [[Keyspaces]] workload.

### [[Timestream]]

Purpose-built for:

- Time-series data
- Timestamped measurements
- IoT metrics
- Operational metrics
- Time-based analytics

### [[Keyspaces]]

Purpose-built for:

- Apache Cassandra-compatible workloads
- CQL applications

### Exam Decision

**Time-series is the main requirement → [[Timestream]]**

**Cassandra compatibility is required → [[Keyspaces]]**

---

## Timestream vs DynamoDB

### [[04-Databases/DynamoDB]]

Best for:

- Key-value/document data
- Massive scale
- Predictable access patterns
- Low-latency application workloads

### [[Timestream]]

Best for:

- Timestamped measurements
- Data changing over time
- Time-series analytics
- Historical trends

### Exam Decision

**Retrieve item by key → [[04-Databases/DynamoDB]]**

**Analyze measurements over time → [[Timestream]]**

---

## Timestream vs RDS/Aurora

### [[RDS]] / [[Aurora]]

Use for:

- Relational data
- OLTP
- Transactions
- SQL joins
- Traditional applications

### [[Timestream]]

Use for:

- Time-series data
- Massive timestamped event datasets
- Historical trends
- Operational analytics

### Exam Decision

Do not choose [[RDS]] simply because the question mentions SQL.

Timestream itself supports SQL-compatible querying.

Focus on:

**What kind of data is being stored?**

---

## Timestream vs CloudWatch

This can become an exam trap when monitoring metrics are involved.

### [[07-Monitoring/CloudWatch]]

Use for:

- AWS monitoring
- Metrics
- Logs
- Alarms
- Operational observability

### [[Timestream]]

Use when an application needs a **purpose-built database for storing and analyzing time-series data**.

### Exam Decision

**Monitor AWS resources / trigger alarms → [[07-Monitoring/CloudWatch]]**

**Build an application around massive time-series datasets → [[Timestream]]**

---

## Scenario Recognition

### Exam Keywords

Immediately think **[[Timestream]]** when you see:

- Time-series database
- Timestamped data
- Measurements over time
- IoT sensor data
- Operational metrics
- Trillions of events
- Historical trends
- Near real-time analytics
- Automatically tier recent and historical data
- Recent data in memory
- Historical data in cost-optimized storage
- Serverless time-series database

### Strongest Keyword

> **Time-Series Database → Timestream**

---

## Exam Traps

### Trap 1 — Time-Series vs Cassandra

If Cassandra compatibility is explicitly required:

**Choose → [[Keyspaces]]**

If the primary requirement is a purpose-built time-series database:

**Choose → [[Timestream]]**

---

### Trap 2 — SQL Means RDS

Timestream supports SQL-compatible queries.

Therefore:

**SQL mentioned + time-series workload ≠ automatically RDS**

Look at the data model.

---

### Trap 3 — IoT Automatically Means DynamoDB

[[04-Databases/DynamoDB]] can absolutely be used with IoT applications.

But if the scenario emphasizes:

- Measurements
- Timestamps
- Historical trends
- Time-based analytics

**Choose → [[Timestream]]**

---

### Trap 4 — Manually Managing Storage Tiers

Timestream automatically handles storage tiering.

Remember:

**Recent → Memory**

**Historical → Cost-Optimized Storage**

---

### Trap 5 — Timestream vs Kinesis Data Streams

[[20-SAA/10-Messaging/Kinesis Data Streams]] and [[Timestream]] solve different parts of an architecture.

**Kinesis Data Streams = Stream/transport the data**

**Timestream = Store/query time-series data**

They can work together:

Producers  
↓  
[[20-SAA/10-Messaging/Kinesis Data Streams]]  
↓  
[[Timestream]]

---

## Quick Cheat Sheet

| Feature | Timestream |
|---|---|
| Database Type | Time-Series |
| Management | Fully Managed |
| Infrastructure | Serverless |
| Scaling | Automatic |
| Scale | Trillions of events per day |
| Querying | SQL-Compatible |
| Scheduled Queries | ✅ |
| Multi-Measure Records | ✅ |
| Recent Data | Memory |
| Historical Data | Cost-Optimized Storage |
| Built-In Time-Series Analytics | ✅ |
| IoT Applications | ✅ |
| Operational Applications | ✅ |
| Real-Time Analytics | ✅ |
| Encryption in Transit | ✅ |
| Encryption at Rest | ✅ |

---

## Master Memory Trick

> [!tip] Master Memory Trick
> **Timestream = Timeline Database**
>
> Ask:
>
> **"Is the important question WHAT happened, or WHEN and how it changed?"**
>
> If the architecture revolves around measurements changing over time:
>
> **Think → [[Timestream]]**

Remember:

**[[RDS]] = Rows**

**[[04-Databases/DynamoDB]] = Keys**

**[[DocumentDB]] = Documents**

**[[Neptune]] = Relationships**

**[[20-SAA/05-Databases/OpenSearch]] = Search**

**[[Keyspaces]] = Cassandra**

**[[Timestream]] = Time**

And for Timestream storage:

**NOW = Memory**

**HISTORY = Cost-Optimized Storage**

---

## Related Notes

- [[Keyspaces]]
- [[04-Databases/DynamoDB]]
- [[RDS]]
- [[Aurora]]
- [[AWS IoT]]
- [[20-SAA/10-Messaging/Kinesis Data Streams]]
- [[Kinesis Data Analytics]]
- [[02-Compute/Lambda]]
- [[MSK]]
- [[09-Analytics/QuickSight]]
- [[SageMaker]]
- [[07-Monitoring/CloudWatch]]
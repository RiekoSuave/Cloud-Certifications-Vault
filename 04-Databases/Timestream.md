See also: [[Database Fundamentals]]

See also: [[04-Databases/DynamoDB]]

See also: [[RDS]]

See also: [[04-Databases/Redshift]]

## What Problem Does It Solve?

Provides a managed database specifically designed for storing and analyzing time-series data.

Timestream is useful when data is generated continuously over time and you need to analyze patterns in that data.

### Memory Trick

Timestream = Time-Series Data

---

## Type

Time-Series Database

Serverless Database

---

## What Is Timestream?

Timestream is a:

- Fully managed
- Fast
- Scalable
- Serverless

time-series database.

It is specifically designed for data where:

Time matters.

### Memory Trick

Timestream = Data Over Time

---

## What Is Time-Series Data?

Time-series data is data recorded over time.

Think:

Measurement

+

Timestamp

Examples conceptually include:

Temperature → Time

CPU Usage → Time

Device Reading → Time

Application Event → Time

The important concept is:

Each piece of data is associated with when it occurred.

---

## Time-Series Example

Imagine recording CPU usage:

10:00 AM → 25%

10:01 AM → 32%

10:02 AM → 48%

10:03 AM → 71%

10:04 AM → 65%

Timestream can store and analyze this type of data to help identify patterns over time.

---

## Serverless

Timestream is:

Serverless

You do not manage the underlying database servers.

AWS manages the infrastructure.

### Memory Trick

Timestream = No Servers to Manage

---

## Automatic Scaling

Your course states that Timestream:

Automatically scales up and down

to adjust capacity.

This means AWS adjusts the database capacity based on the workload.

### Memory Trick

Timestream = Automatically Scales

---

## Massive Event Scale

Your course describes Timestream as being able to:

Store and analyze trillions of events per day.

The important concept is:

Timestream is designed for very large amounts of time-series data.

---

## Built-In Analytics

Your course notes identify:

Built-in time-series analytics functions

These help identify:

Patterns in your data

in:

Near real time

### Memory Trick

Timestream = Find Patterns Over Time

---

## Performance and Cost

Your Udemy notes describe Timestream as significantly faster and less expensive than using relational databases for time-series workloads.

The key concept to remember is:

A purpose-built time-series database can be more appropriate than forcing time-series workloads into a traditional relational database.

---

## Timestream vs RDS

### RDS

General relational SQL database.

### Timestream

Purpose-built time-series database.

| RDS | Timestream |
|---|---|
| Relational database | Time-series database |
| Tables + SQL | Data over time |
| General application data | Time-based events |
| Managed | Serverless |

### Memory Trick

RDS = Relational Data

Timestream = Time Data

---

## Timestream vs DynamoDB

### DynamoDB

NoSQL key-value database designed for massive scale and low latency.

### Timestream

Database specifically designed for time-series data.

| DynamoDB | Timestream |
|---|---|
| NoSQL key-value | Time-series |
| Application data | Time-based events |
| Massive scale | Massive event scale |
| Serverless | Serverless |

### Memory Trick

DynamoDB = Key-Value

Timestream = Time-Series

---

## Timestream vs Redshift

### Timestream

Designed to store and analyze time-series events.

### Redshift

Designed for data warehousing and large analytical workloads.

| Timestream | Redshift |
|---|---|
| Time-series database | Data warehouse |
| Events over time | Business analytics |
| Near-real-time patterns | OLAP analytics |
| Serverless | Provisioned or Serverless |

### Memory Trick

Timestream = Time

Redshift = Warehouse Analytics

---

## Common Use Case Concept

Look for data that is continuously generated and associated with:

Time

or:

Timestamps

The major clue is:

Data Over Time

---

## Exam Scenarios

An application needs a purpose-built database for time-series data.

→ Timestream

---

A company needs to store and analyze extremely large quantities of events over time.

→ Timestream

---

A company wants AWS to automatically scale a serverless time-series database.

→ Timestream

---

A company wants to identify patterns in time-series data in near real time.

→ Timestream

---

An application needs a traditional relational SQL database.

→ RDS or Aurora

NOT Timestream

---

An application needs a NoSQL key-value database.

→ DynamoDB

NOT Timestream

---

A company needs an OLAP data warehouse for business analytics.

→ Redshift

NOT Timestream

---

## Don't Confuse These

RDS = Relational SQL

Aurora = High-Performance Relational

DynamoDB = NoSQL Key-Value

DocumentDB = NoSQL Documents

Neptune = Graph Relationships

Timestream = Time-Series Data

Redshift = Data Warehouse

ElastiCache = Cache

---

## Exam Keywords

Time-series

Time

Timestamp

Events

Serverless

Automatic scaling

Trillions of events

Near real time

Patterns

---

## Memory Tricks

Timestream = Time-Series

Timestream = Data Over Time

Timestream = Events + Time

Timestream = Serverless

Timestream = Automatically Scales

DynamoDB = Key-Value

DocumentDB = Documents

Neptune = Relationships

Redshift = Analytics
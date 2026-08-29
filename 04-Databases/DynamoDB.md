See also: [[Database Fundamentals]]

See also: [[RDS]]

See also: [[04-Databases/Aurora]]

See also: [[ElastiCache]]

## What Problem Does It Solve?

Provides a fully managed NoSQL database designed for massive scale and extremely fast performance.

DynamoDB solves the need for applications that require:

- Massive scalability
- Low latency
- No server management
- Fast and consistent performance

---

## Type

NoSQL Database

Serverless Database

---

## What Is DynamoDB?

DynamoDB is a:

- Fully managed
- Highly available
- NoSQL
- Serverless

database service.

Unlike RDS and Aurora, DynamoDB is:

NOT a relational database.

### Memory Trick

DynamoDB = Fast NoSQL

---

## NoSQL

DynamoDB uses a NoSQL data model rather than traditional relational tables and SQL relationships.

Your course focuses on DynamoDB as a:

Key-Value Database

### Memory Trick

RDS = SQL

DynamoDB = NoSQL

---

## Serverless

DynamoDB is considered a:

Serverless Database

You do not provision or manage database servers.

AWS manages the underlying infrastructure.

### Memory Trick

DynamoDB = No Servers to Manage

---

## Massive Scalability

Your course describes DynamoDB as being able to scale to extremely large workloads.

Examples from your notes include:

- Millions of requests per second
- Trillions of rows
- Hundreds of TB of storage

The important exam concept is:

DynamoDB = Massive Scale

---

## Performance

DynamoDB provides:

Single-digit millisecond latency

This means applications can retrieve data very quickly even at large scale.

### Memory Trick

DynamoDB = Milliseconds

---

## High Availability

Your course describes DynamoDB as highly available with replication across:

3 Availability Zones

This provides built-in resilience.

### Memory Trick

DynamoDB = Multi-AZ Built In

---

## IAM Integration

DynamoDB integrates with:

IAM

for:

- Security
- Authorization
- Administration

See also:

[[IAM]]

### Memory Trick

DynamoDB Security = IAM

---

## DynamoDB Table Classes

Your course identifies:

- Standard
- Standard-Infrequent Access (Standard-IA)

### Standard

Designed for regularly accessed DynamoDB data.

### Standard-IA

Designed for tables where data is accessed less frequently.

---

## Common Use Cases

Your notes identify use cases such as:

- Gaming applications
- Mobile applications
- Shopping carts
- Large-scale applications

DynamoDB is especially useful when applications need fast, predictable performance at massive scale.

---

## DynamoDB Accelerator (DAX)

DAX stands for:

DynamoDB Accelerator

DAX is a:

Fully managed in-memory cache for DynamoDB.

### What Problem Does DAX Solve?

DAX makes DynamoDB reads even faster.

Normal DynamoDB:

Single-digit milliseconds

DAX:

Microseconds

### Memory Trick

DAX = DynamoDB Turbo

---

## DAX Performance

Your course describes DAX as providing up to:

10x performance improvement

by reducing access times from:

Milliseconds

↓

Microseconds

---

## DAX Characteristics

Your course identifies DAX as:

- Fully managed
- Secure
- Highly scalable
- Highly available
- In-memory

---

## DAX vs ElastiCache

This distinction is important.

### DAX

Designed specifically for:

DynamoDB

### ElastiCache

Can be used as an in-memory caching solution for other database workloads.

| DAX | ElastiCache |
|---|---|
| DynamoDB specific | General database caching |
| Integrated with DynamoDB | Redis / Memcached |
| In-memory cache | In-memory cache |
| Microsecond access | Improves application/database performance |

### Memory Trick

DAX = DynamoDB Only

ElastiCache = General Cache

See:

[[ElastiCache]]

---

## DynamoDB Global Tables

DynamoDB also provides:

Global Tables

Global Tables allow DynamoDB data to be replicated across multiple AWS Regions.

This is useful for globally distributed applications.

### Basic Idea

Region A

↕

DynamoDB Global Table

↕

Region B

↕

Region C

---

## Why Global Tables?

Global Tables help applications operate across:

Multiple AWS Regions

This can improve:

- Global application availability
- Resilience
- Local access for globally distributed users

### Memory Trick

Global Tables = Multi-Region DynamoDB

---

## DynamoDB vs RDS

### DynamoDB

NoSQL database.

### RDS

Relational SQL database.

| DynamoDB | RDS |
|---|---|
| NoSQL | Relational |
| Key-value | SQL |
| Serverless | Managed database instances |
| Massive scale | Traditional relational workloads |
| Millisecond latency | Relational application database |

### Memory Trick

DynamoDB = NoSQL

RDS = SQL

---

## DynamoDB vs Aurora

### DynamoDB

NoSQL + serverless.

### Aurora

Relational + MySQL/PostgreSQL compatible.

| DynamoDB | Aurora |
|---|---|
| NoSQL | Relational |
| Key-value | SQL |
| Serverless | Managed relational |
| Massive-scale applications | High-performance relational applications |

---

## DynamoDB vs Redshift

### DynamoDB

Operational NoSQL database.

### Redshift

Analytics and data warehouse.

### Memory Trick

DynamoDB = Application Data

Redshift = Analytics

---

## Common Exam Scenarios

An application needs a fully managed NoSQL key-value database.

→ DynamoDB

---

An application needs single-digit millisecond database performance at massive scale.

→ DynamoDB

---

A company does not want to provision or manage database servers.

→ DynamoDB

---

A gaming application needs a database capable of handling massive traffic.

→ DynamoDB

---

A shopping cart needs fast NoSQL storage.

→ DynamoDB

---

A DynamoDB application needs even faster read performance measured in microseconds.

→ DAX

---

A globally distributed application needs DynamoDB data across multiple AWS Regions.

→ DynamoDB Global Tables

---

An application needs a relational SQL database.

→ RDS or Aurora

NOT DynamoDB

---

A company needs a data warehouse for analytics.

→ Redshift

NOT DynamoDB

---

## Exam Keywords

NoSQL

Key-value

Serverless database

Fully managed

Massive scale

Single-digit milliseconds

Multi-AZ

IAM

DAX

Microseconds

Global Tables

Multi-Region

---

## Memory Tricks

DynamoDB = Fast NoSQL

DynamoDB = Serverless Database

DynamoDB = Milliseconds

DAX = DynamoDB Turbo

DAX = Microseconds

Global Tables = Multi-Region DynamoDB

RDS = SQL

DynamoDB = NoSQL

Redshift = Analytics
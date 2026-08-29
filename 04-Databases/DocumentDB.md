See also: [[Database Fundamentals]]

See also: [[04-Databases/DynamoDB]]

See also: [[04-Databases/Aurora]]

See also: [[04-Databases/Neptune]]

## What Problem Does It Solve?

Provides a fully managed document database for applications that use MongoDB-compatible workloads.

DocumentDB is designed for storing, querying, and indexing document-based data such as JSON.

### Memory Trick

DocumentDB = MongoDB-Compatible Documents

---

## Type

Document Database

NoSQL Database

---

## What Is DocumentDB?

DocumentDB is AWS's managed document database service.

Your course compares it to Aurora:

Aurora

→ AWS implementation compatible with MySQL / PostgreSQL

DocumentDB

→ AWS implementation for MongoDB-compatible workloads

### Memory Trick

Aurora = MySQL/PostgreSQL Compatible

DocumentDB = MongoDB Compatible

---

## MongoDB

MongoDB is a:

NoSQL document database

Rather than focusing on traditional relational tables and rows, document databases store information as documents.

Your course specifically associates MongoDB with:

JSON data

---

## JSON Data

JSON stands for:

JavaScript Object Notation

Document databases are useful for storing data with flexible structures.

Example concept:

Customer

↓

JSON Document

↓

Name

Email

Address

Orders

Preferences

### Memory Trick

DocumentDB = JSON Documents

---

## What Can DocumentDB Do With JSON Data?

Your course identifies three important operations:

- Store
- Query
- Index

JSON data.

### Memory Trick

DocumentDB = Store + Query + Index JSON

---

## Fully Managed

DocumentDB is:

Fully managed by AWS.

This reduces the amount of database infrastructure you need to manage yourself.

### Memory Trick

DocumentDB = AWS Manages the Database

---

## High Availability

Your course describes DocumentDB as:

Highly available

with replication across:

3 Availability Zones

### Memory Trick

DocumentDB = Multi-AZ

---

## Automatic Storage Growth

Your course notes state that DocumentDB storage:

Automatically grows

in increments of:

10 GB

The main concept to remember is:

DocumentDB storage can automatically grow as the database needs more capacity.

---

## Scalability

Your course describes DocumentDB as capable of automatically scaling to workloads involving:

Millions of requests per second

The important concept is:

DocumentDB = Managed + Scalable Document Database

---

## DocumentDB vs RDS

### RDS

Relational database.

Think:

- Tables
- Rows
- SQL

### DocumentDB

Document database.

Think:

- Documents
- JSON
- MongoDB compatibility

| RDS | DocumentDB |
|---|---|
| Relational | NoSQL document |
| SQL | Document model |
| Tables + rows | JSON documents |
| Traditional relational workloads | Document workloads |

### Memory Trick

RDS = Tables

DocumentDB = Documents

---

## DocumentDB vs DynamoDB

Both are:

NoSQL databases

But they solve different problems.

### DynamoDB

Key-value NoSQL database designed for massive scale and low latency.

### DocumentDB

Document database designed for MongoDB-compatible workloads.

| DynamoDB | DocumentDB |
|---|---|
| NoSQL | NoSQL |
| Key-value | Document |
| AWS-native NoSQL | MongoDB-compatible |
| Fast key-value access | JSON document workloads |

### Memory Trick

DynamoDB = Key-Value

DocumentDB = Documents

---

## DocumentDB vs Neptune

### DocumentDB

Stores document-oriented data.

### Neptune

Stores highly connected graph data.

| DocumentDB | Neptune |
|---|---|
| Document database | Graph database |
| JSON documents | Relationships |
| MongoDB-compatible | Connected datasets |

### Memory Trick

DocumentDB = Documents

Neptune = Relationships

---

## Common Use Cases

Based on your course material, think:

- MongoDB-compatible applications
- JSON document storage
- Applications needing flexible document data
- Managed document database workloads

---

## Exam Scenarios

A company needs a fully managed AWS database for a MongoDB-compatible application.

→ DocumentDB

---

An application needs to store, query, and index JSON documents.

→ DocumentDB

---

A company wants a highly available managed document database replicated across multiple Availability Zones.

→ DocumentDB

---

An application needs a NoSQL key-value database with single-digit millisecond latency.

→ DynamoDB

NOT DocumentDB

---

An application needs to analyze complex relationships between users.

→ Neptune

NOT DocumentDB

---

An application requires traditional relational SQL tables.

→ RDS or Aurora

NOT DocumentDB

---

## Don't Confuse These

RDS = Relational SQL

Aurora = High-Performance Relational

DynamoDB = NoSQL Key-Value

DocumentDB = NoSQL Documents

Neptune = Graph Relationships

Redshift = Analytics Warehouse

ElastiCache = Cache

---

## Exam Keywords

Document database

MongoDB compatible

NoSQL

JSON

Documents

Fully managed

High availability

Multi-AZ

Automatic storage growth

---

## Memory Tricks

DocumentDB = Documents

DocumentDB = MongoDB Compatible

DocumentDB = JSON

DynamoDB = Key-Value

Neptune = Relationships

RDS = SQL
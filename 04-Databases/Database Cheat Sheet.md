See also: [[Database Comparison]]

## Core Database Services

RDS = SQL

Aurora = Faster SQL

DynamoDB = NoSQL

DocumentDB = Documents

Neptune = Relationships

Timestream = Time

Redshift = Analytics

ElastiCache = Speed

DAX = DynamoDB Turbo

---

## Quick Database Decisions

Need a managed relational SQL database?

→ RDS

Need a high-performance MySQL/PostgreSQL-compatible relational database?

→ Aurora

Need massive-scale NoSQL key-value storage?

→ DynamoDB

Need a MongoDB-compatible document database?

→ DocumentDB

Need a graph database for complex relationships?

→ Neptune

Need a time-series database?

→ Timestream

Need a data warehouse for analytics?

→ Redshift

Need Redis or Memcached caching?

→ ElastiCache

Need a cache specifically for DynamoDB?

→ DAX

---

## Relational vs NoSQL

Relational

→ Tables + SQL

→ RDS / Aurora

NoSQL

→ Flexible / Purpose-Built

→ DynamoDB / DocumentDB / Neptune / Timestream

---

## Relational Cheat Code

RDS = Managed SQL

Aurora = High-Performance SQL

### Think

RDS → Traditional managed relational database

Aurora → AWS cloud-optimized relational database

---

## RDS Deployment Cheat Code

Read Replica = Read Performance

Multi-AZ = Disaster Recovery

Point-in-Time Restore = Restore to Specific Time

No SSH = AWS manages underlying database host

---

## NoSQL Cheat Code

DynamoDB = Key-Value

DocumentDB = Documents / JSON

Neptune = Relationships

Timestream = Time-Series

---

## DynamoDB Cheat Code

DynamoDB = Serverless NoSQL

Single-Digit Milliseconds = DynamoDB

DAX = DynamoDB Cache

Global Tables = Multi-Region DynamoDB

---

## Analytics Cheat Code

Redshift = Data Warehouse

Redshift = OLAP

RDS / Aurora = OLTP

### Memory Trick

RDS = Run the Business

Redshift = Analyze the Business

---

## Cache Cheat Code

ElastiCache = Redis + Memcached

DAX = DynamoDB Only

### Memory Trick

ElastiCache = General Cache

DAX = DynamoDB Cache

---

## Data Model Clues

SQL + Tables

→ RDS / Aurora

Key-Value

→ DynamoDB

MongoDB + JSON

→ DocumentDB

Graph + Relationships

→ Neptune

Time + Events

→ Timestream

OLAP + Warehouse

→ Redshift

Redis + Memcached

→ ElastiCache

---

## 30-Second Database Review

RDS → SQL

Aurora → Faster SQL

DynamoDB → NoSQL Key-Value

DocumentDB → MongoDB / JSON

Neptune → Graph Relationships

Timestream → Time-Series

Redshift → Analytics Warehouse

ElastiCache → Cache

DAX → DynamoDB Cache
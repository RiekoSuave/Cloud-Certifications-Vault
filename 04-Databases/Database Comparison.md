See also: [[Database Fundamentals]]

See also: [[RDS]]

See also: [[04-Databases/Aurora]]

See also: [[04-Databases/DynamoDB]]

See also: [[ElastiCache]]

See also: [[04-Databases/Redshift]]

See also: [[04-Databases/Neptune]]

See also: [[DocumentDB]]

See also: [[04-Databases/Timestream]]

## Database Service Comparison

| Service | Database Type | Best For | Memory Shortcut |
|---|---|---|---|
| RDS | Relational SQL | Applications and structured data | Managed SQL |
| Aurora | Relational SQL | High-performance relational workloads | Faster SQL |
| DynamoDB | NoSQL Key-Value | Massive-scale applications | Fast NoSQL |
| DocumentDB | NoSQL Document | MongoDB-compatible document workloads | Documents |
| Neptune | Graph Database | Highly connected data | Relationships |
| Timestream | Time-Series Database | Data and events over time | Time |
| Redshift | Data Warehouse | Analytics and OLAP | Analytics |
| ElastiCache | In-Memory Cache | Improving application/database performance | Speed |

---

## RDS

### Type

Relational SQL Database

### Best For

- Applications
- Websites
- Structured data
- Traditional relational workloads

### Key Clues

- SQL
- Relational
- Managed database
- Automated backups
- Multi-AZ
- Read Replicas

### Memory Trick

RDS = Managed SQL

See:

[[RDS]]

---

## Aurora

### Type

High-Performance Relational Database

### Best For

- High-traffic applications
- Enterprise workloads
- High-performance relational applications

### Key Clues

- MySQL compatible
- PostgreSQL compatible
- AWS proprietary
- Cloud optimized
- Aurora Serverless

### Memory Trick

Aurora = Faster SQL

See:

[[04-Databases/Aurora]]

---

## DynamoDB

### Type

NoSQL Key-Value Database

### Best For

- Massive-scale applications
- Gaming applications
- Mobile applications
- Shopping carts

### Key Clues

- NoSQL
- Key-value
- Serverless
- Single-digit milliseconds
- Massive scale
- DAX
- Global Tables

### Memory Trick

DynamoDB = Fast NoSQL

See:

[[04-Databases/DynamoDB]]

---

## DocumentDB

### Type

NoSQL Document Database

### Best For

MongoDB-compatible document workloads.

### Key Clues

- MongoDB compatible
- JSON
- Documents
- NoSQL
- Fully managed

### Memory Trick

DocumentDB = Documents

See:

[[DocumentDB]]

---

## Neptune

### Type

Graph Database

### Best For

Highly connected data and complex relationships.

### Common Use Cases

- Social networks
- Knowledge graphs
- Fraud detection
- Recommendation engines

### Key Clues

- Graph
- Relationships
- Connected data

### Memory Trick

Neptune = Relationships

See:

[[04-Databases/Neptune]]

---

## Timestream

### Type

Time-Series Database

### Best For

Data and events generated over time.

### Key Clues

- Time-series
- Timestamps
- Events
- Serverless
- Automatic scaling
- Near-real-time patterns

### Memory Trick

Timestream = Time

See:

[[04-Databases/Timestream]]

---

## Redshift

### Type

Data Warehouse

OLAP

### Best For

- Analytics
- Business Intelligence
- Reporting
- Large analytical workloads

### Key Clues

- OLAP
- Data warehouse
- Columnar storage
- MPP
- Petabytes
- SQL analytics

### Memory Trick

Redshift = Analytics

See:

[[04-Databases/Redshift]]

---

## ElastiCache

### Type

In-Memory Cache

### Best For

Improving application and database performance.

### Technologies

- Redis
- Memcached

### Key Clues

- Cache
- In-memory
- Performance
- Low latency
- Reduce database load

### Memory Trick

ElastiCache = Speed

See:

[[ElastiCache]]

---

## Relational Database Comparison

| Service | Main Idea |
|---|---|
| RDS | Managed traditional relational databases |
| Aurora | AWS cloud-optimized relational database |

### Remember

RDS = Managed SQL

Aurora = Faster AWS SQL

---

## NoSQL Comparison

| Service | Data Model | Think |
|---|---|---|
| DynamoDB | Key-Value | Massive scale |
| DocumentDB | Document | JSON / MongoDB |
| Neptune | Graph | Relationships |
| Timestream | Time-Series | Data over time |

### Memory Trick

DynamoDB = Key-Value

DocumentDB = Documents

Neptune = Relationships

Timestream = Time

---

## Performance Services

Don't confuse databases with caching.

### ElastiCache

General in-memory caching using Redis or Memcached.

### DAX

In-memory accelerator specifically for DynamoDB.

### Memory Trick

ElastiCache = General Cache

DAX = DynamoDB Cache

---

## OLTP vs OLAP

### OLTP

Online Transaction Processing

Think:

Application transactions

Examples:

- Orders
- Payments
- Customer updates

RDS and Aurora are associated with transactional relational application workloads.

### OLAP

Online Analytical Processing

Think:

Large-scale analytics

Redshift is designed for OLAP.

### Memory Trick

RDS/Aurora = Run the Business

Redshift = Analyze the Business

---

## Scenario Comparison

### Need a managed relational SQL database?

→ RDS

---

### Need a high-performance MySQL/PostgreSQL-compatible AWS relational database?

→ Aurora

---

### Need massive-scale NoSQL key-value storage?

→ DynamoDB

---

### Need a MongoDB-compatible document database?

→ DocumentDB

---

### Need to analyze complex relationships?

→ Neptune

---

### Need a database specifically for time-series data?

→ Timestream

---

### Need a data warehouse for analytics?

→ Redshift

---

### Need an in-memory cache using Redis or Memcached?

→ ElastiCache

---

### Need an in-memory accelerator specifically for DynamoDB?

→ DAX

---

## Don't Confuse These

RDS = Relational SQL

Aurora = High-Performance Relational

DynamoDB = NoSQL Key-Value

DocumentDB = NoSQL Documents

Neptune = Graph Relationships

Timestream = Time-Series Data

Redshift = Data Warehouse / Analytics

ElastiCache = In-Memory Cache

DAX = DynamoDB Cache

---

## Fast Decision Tree

Need a database?

↓

Need SQL / relational?

→ RDS or Aurora

Need high-performance AWS-optimized MySQL/PostgreSQL compatibility?

→ Aurora

↓

Need NoSQL?

Key-Value?

→ DynamoDB

Documents / MongoDB?

→ DocumentDB

Relationships?

→ Neptune

Time-based events?

→ Timestream

↓

Need analytics/data warehouse?

→ Redshift

↓

Need caching rather than primary database storage?

→ ElastiCache

Using DynamoDB specifically?

→ DAX

---

## Exam Keywords

| If You See... | Think... |
|---|---|
| Relational + SQL | RDS |
| MySQL/PostgreSQL + high performance | Aurora |
| NoSQL + key-value + massive scale | DynamoDB |
| MongoDB + JSON | DocumentDB |
| Graph + relationships | Neptune |
| Time-series + events | Timestream |
| Data warehouse + OLAP | Redshift |
| Redis + Memcached | ElastiCache |
| DynamoDB + microseconds | DAX |

---

## Final Memory Map

RDS = SQL

Aurora = Faster SQL

DynamoDB = NoSQL

DocumentDB = Documents

Neptune = Relationships

Timestream = Time

Redshift = Analytics

ElastiCache = Speed

DAX = DynamoDB Turbo
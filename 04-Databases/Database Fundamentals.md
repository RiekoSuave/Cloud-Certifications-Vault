See also: [[RDS]]

See also: [[04-Databases/Aurora]]

See also: [[04-Databases/DynamoDB]]

See also: [[04-Databases/Redshift]]

See also: [[ElastiCache]]

See also: [[04-Databases/Neptune]]

## What Problem Do Databases Solve?

Storage services such as:

- EBS
- EFS
- EC2 Instance Store
- S3

can store data, but sometimes an application needs more than simply storing files or blocks.

Databases allow you to:

- Structure data
- Build indexes
- Efficiently query and search data
- Define relationships between datasets

---

## Database Fundamentals

Different database technologies are optimized for different purposes.

Each database can have different:

- Features
- Data structures
- Performance characteristics
- Constraints

### Memory Trick

Storage = Keep Data

Database = Organize + Query Data

---

## Two Major Database Categories

For AWS exams, an important distinction is:

Relational Databases

vs

NoSQL Databases

---

## Relational Databases

Relational databases organize information into structured tables.

Your course compares them to:

Excel spreadsheets with relationships between them.

Relational databases commonly use:

SQL

SQL stands for:

Structured Query Language

SQL is used to perform queries and lookups against the database.

### Memory Trick

Relational = Tables + SQL

---

## Relational Database Example

Think of:

Customers Table

↓

Orders Table

↓

Products Table

Relationships can connect the data between these tables.

---

## AWS Relational Database Services

Important services include:

[[RDS]]

and:

[[04-Databases/Aurora]]

---

## NoSQL Databases

NoSQL means:

Non-SQL / Non-Relational

NoSQL databases are purpose-built for specific data models.

They commonly provide flexible schemas for modern applications.

### Memory Trick

NoSQL = Flexible + Purpose Built

---

## Benefits of NoSQL

Your course identifies several major benefits.

### Flexibility

The data model can evolve more easily.

---

### Scalability

Designed to scale out using distributed systems or clusters.

---

### High Performance

Can be optimized for a specific type of data model.

---

### Highly Functional

Different NoSQL database types can be optimized for different purposes.

---

## NoSQL Database Types

Your course identifies examples such as:

- Key-value
- Document
- Graph
- In-memory
- Search

---

## AWS NoSQL Examples

### DynamoDB

Key-value / NoSQL database.

See:

[[04-Databases/DynamoDB]]

---

### Neptune

Graph database.

See:

[[04-Databases/Neptune]]

---

### ElastiCache

In-memory database/cache technology.

See:

[[ElastiCache]]

---

## JSON and NoSQL

JSON stands for:

JavaScript Object Notation

JSON is a common data format that fits well with NoSQL models.

JSON data can:

- Be nested
- Have fields that change over time
- Support structures such as arrays

### Memory Trick

JSON = Flexible Data Structure

---

## Relational vs NoSQL

| Relational | NoSQL |
|---|---|
| Structured tables | Flexible data models |
| Relationships between tables | Purpose-built models |
| SQL queries | Depends on database |
| Structured schema | Flexible schema |

---

## Managed AWS Databases

AWS provides managed database services.

Using a managed database means AWS can handle many infrastructure and operational responsibilities for you.

Your course identifies benefits including:

- Quick provisioning
- High Availability
- Vertical scaling
- Horizontal scaling
- Automated backup and restore
- Operations
- Upgrades
- Operating system patching
- Monitoring
- Alerting

---

## Managed Database vs Database on EC2

Many database technologies can also be installed manually on:

EC2

However, when you run your own database on EC2, you must manage much more yourself.

Examples include:

- Resiliency
- Backups
- Patching
- High Availability
- Fault tolerance

### Memory Trick

Managed Database = AWS Handles More

Database on EC2 = You Handle More

---

## Why Use a Managed Database?

Managed databases reduce the operational work required to run database infrastructure.

Instead of focusing heavily on:

Infrastructure Management

you can focus more on:

Data + Application

---

## Quick Database Decision

Need structured tables and SQL?

→ Relational Database

---

Need flexible, non-relational data?

→ NoSQL Database

---

Need AWS to manage much of the database infrastructure?

→ Managed AWS Database

---

Need complete control over the database server and operating system?

→ Database running on EC2

---

## Exam Scenarios

An application needs structured tables with relationships between datasets.

→ Relational Database

---

An application needs to perform SQL queries against relational data.

→ Relational Database

---

An application needs a flexible schema that can evolve over time.

→ NoSQL Database

---

An application needs a distributed database designed to scale horizontally.

→ NoSQL may be appropriate

---

A company wants AWS to handle database operating system patching, backups, and much of the infrastructure management.

→ Managed AWS Database

---

A company installs database software directly on EC2.

Who handles database resiliency, backups, patching, and High Availability?

→ Customer

---

## Exam Keywords

Relational

SQL

Tables

Relationships

NoSQL

Non-relational

Flexible schema

JSON

Managed database

High Availability

Backup and restore

Scaling

---

## Memory Tricks

Relational = Tables + SQL

NoSQL = Flexible + Purpose Built

JSON = Flexible Data

Managed Database = AWS Handles More

Database on EC2 = You Handle More
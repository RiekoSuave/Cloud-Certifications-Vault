See also: [[Database Fundamentals]]

See also: [[RDS]]

See also: [[04-Databases/DynamoDB]]

## What Problem Does It Solve?

Provides a high-performance managed relational database that is compatible with MySQL and PostgreSQL.

Aurora is designed for applications that need:

- Relational SQL databases
- High performance
- High availability
- Automatic scaling
- Less database management

---

## Type

Managed Relational Database

---

## What Is Aurora?

Aurora is AWS's proprietary relational database technology.

It is:

- Fully managed
- Cloud optimized
- Relational
- Compatible with MySQL and PostgreSQL

### Memory Trick

Aurora = Faster RDS

---

## Database Compatibility

Aurora supports:

- MySQL
- PostgreSQL

This means applications designed around these relational database technologies can use Aurora's compatible editions.

### Memory Trick

Aurora = MySQL + PostgreSQL

---

## Aurora Performance

Your course describes Aurora as AWS cloud optimized.

Your Udemy notes state that Aurora can provide:

- Up to 5x the performance of MySQL on RDS
- Up to 3x the performance of PostgreSQL on RDS

The important exam concept is:

Aurora = Higher-performance AWS relational database

---

## Automatic Storage Growth

Aurora storage automatically grows as needed.

Your course notes state that storage grows in:

10 GB increments

up to:

256 TB

### Memory Trick

Aurora Storage = Automatically Grows

---

## High Availability

Aurora is designed for:

High Availability

This makes it suitable for applications that require a highly available managed relational database.

---

## Aurora Cost

Your course describes Aurora as costing approximately:

20% more than standard RDS

but being more efficient.

### Exam Concept

Aurora may cost more than standard RDS engines but is designed to provide higher performance and cloud-optimized capabilities.

---

## RDS vs Aurora

Both are:

Managed relational databases

But they are not exactly the same.

### RDS

Provides managed versions of traditional relational database engines.

Examples:

- MySQL
- PostgreSQL
- MariaDB
- Oracle
- SQL Server
- Db2

### Aurora

AWS's proprietary cloud-optimized relational database technology.

Compatible with:

- MySQL
- PostgreSQL

| RDS | Aurora |
|---|---|
| Managed relational databases | AWS cloud-optimized relational database |
| Multiple database engines | MySQL/PostgreSQL compatible |
| Standard relational workloads | Higher-performance workloads |
| Managed by AWS | Managed by AWS |

### Memory Trick

RDS = Managed SQL

Aurora = Faster AWS SQL

---

## Aurora Serverless

Aurora also provides:

Aurora Serverless

This allows database capacity to automatically scale based on actual application usage.

### Memory Trick

Aurora Serverless = Database Auto Scaling

---

## Why Aurora Serverless?

Traditional database capacity requires you to estimate how much database capacity you need.

Aurora Serverless reduces this requirement.

Your course describes it as:

No capacity planning needed

AWS automatically adjusts database capacity based on demand.

---

## Aurora Serverless Compatibility

Aurora Serverless supports:

- MySQL
- PostgreSQL

---

## Aurora Serverless Pricing

Your course describes Aurora Serverless as:

Pay per second

This can make it cost-effective when database usage varies.

### Memory Trick

Serverless = Pay for Usage

---

## Aurora Serverless Use Cases

Your course specifically identifies workloads that are:

- Infrequent
- Intermittent
- Unpredictable

These workloads benefit from automatically adjusting database capacity.

---

## Provisioned vs Serverless Concept

### Provisioned Database

You provision database capacity.

### Aurora Serverless

AWS automatically adjusts database capacity according to usage.

| Provisioned | Aurora Serverless |
|---|---|
| Capacity planning | Less capacity planning |
| Provision resources | Automatically scales |
| More predictable workloads | Variable workloads |
| Provisioned capacity | Usage-based capacity |

---

## Aurora vs DynamoDB

### Aurora

Relational database.

Uses the relational/SQL model.

### DynamoDB

NoSQL database.

| Aurora | DynamoDB |
|---|---|
| Relational | NoSQL |
| SQL | Key-value |
| MySQL/PostgreSQL compatible | AWS NoSQL database |
| Managed | Fully managed/serverless |

See:

[[04-Databases/DynamoDB]]

---

## Common Use Cases

### Aurora

- High-traffic applications
- Enterprise workloads
- Applications requiring high relational database performance

### Aurora Serverless

- Infrequent workloads
- Intermittent workloads
- Unpredictable workloads
- Applications where database demand changes

---

## Exam Scenarios

A company needs a high-performance AWS-managed relational database compatible with MySQL.

→ Aurora

---

A company needs a high-performance AWS-managed relational database compatible with PostgreSQL.

→ Aurora

---

A company has unpredictable relational database usage and doesn't want to plan database capacity manually.

→ Aurora Serverless

---

A database is used only occasionally and the company wants capacity to automatically adjust based on usage.

→ Aurora Serverless

---

An application requires a NoSQL key-value database.

→ DynamoDB

NOT Aurora

---

A company specifically requires Oracle or Microsoft SQL Server.

→ RDS

NOT Aurora

---

## Exam Keywords

Relational

MySQL compatible

PostgreSQL compatible

AWS proprietary

Cloud optimized

High performance

Automatic storage growth

Aurora Serverless

Auto scaling

No capacity planning

---

## Memory Tricks

Aurora = Faster RDS

Aurora = MySQL + PostgreSQL

Aurora = AWS Cloud Optimized

Aurora Storage = Automatically Grows

Aurora Serverless = Database Auto Scaling

Serverless = No Capacity Planning

RDS = Managed SQL

DynamoDB = NoSQL
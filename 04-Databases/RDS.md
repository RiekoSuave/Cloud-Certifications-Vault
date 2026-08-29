See also: [[Database Fundamentals]]

See also: [[04-Databases/Aurora]]

See also: [[04-Databases/DynamoDB]]

See also: [[04-Databases/Redshift]]

See also: [[EBS]]

## What Problem Does It Solve?

Provides managed relational databases without requiring you to manually manage much of the underlying database infrastructure.

RDS reduces the work involved with:

- Provisioning
- Operating system patching
- Backups
- Monitoring
- Scaling
- Database maintenance

---

## Type

Managed Relational Database

---

## What Is RDS?

RDS stands for:

Relational Database Service

It is a managed database service for relational databases that use SQL.

### Memory Trick

RDS = Managed SQL Database

---

## Supported Database Engines

Your course identifies:

- PostgreSQL
- MySQL
- MariaDB
- Oracle
- Microsoft SQL Server
- IBM Db2
- Aurora

Aurora is AWS's proprietary relational database technology and deserves its own note.

See:

[[04-Databases/Aurora]]

---

## Why Use RDS Instead of Running a Database on EC2?

You could install database software yourself on:

EC2

However, that means you would be responsible for much more database administration.

RDS is managed by AWS.

---

## What AWS Manages With RDS

Your course identifies several advantages.

### Automated Provisioning

AWS helps provision the database infrastructure.

---

### OS Patching

AWS handles operating system patching.

---

### Continuous Backups

RDS supports continuous backups.

Your course also identifies:

Point-in-Time Restore

This allows the database to be restored to a specific timestamp.

### Memory Trick

RDS = AWS Handles Backups

---

### Monitoring

RDS provides monitoring dashboards.

---

### Maintenance

RDS provides maintenance windows for upgrades.

---

### Scaling

Your course identifies:

- Vertical scaling
- Horizontal scaling

as RDS scaling capabilities.

---

## Read Replicas

RDS supports:

Read Replicas

Their purpose is to:

Improve read performance

Basic Idea:

Primary Database

↓

Read Replica

↓

Read Requests

### Memory Trick

Read Replica = Read Performance

---

## Multi-AZ

RDS supports:

Multi-AZ deployments

Your course associates Multi-AZ with:

Disaster Recovery

Basic Idea:

Primary Database

↓

Another Availability Zone

↓

Standby Database

### Memory Trick

Multi-AZ = Disaster Recovery

---

## Read Replica vs Multi-AZ

This distinction is extremely important.

### Read Replica

Purpose:

Improve read performance

### Multi-AZ

Purpose:

Disaster Recovery

| Read Replica | Multi-AZ |
|---|---|
| Read performance | Disaster Recovery |
| Scaling reads | Availability/resiliency |
| Read traffic | Standby architecture |

### Memory Trick

Read Replica = Performance

Multi-AZ = DR

---

## Multi-Region

Your course also identifies:

Multi-Region

as an RDS deployment option.

We'll expand the deeper architecture implications when your SAA course material covers them.

---

## RDS Storage

Your course states that RDS storage is backed by:

EBS

See:

[[EBS]]

---

## No SSH Access

An important characteristic of RDS is that you cannot SSH into the underlying database instances.

Why?

Because RDS is:

Managed by AWS

You don't manage the underlying operating system like you would with your own database server on EC2.

### Memory Trick

RDS = Managed

Therefore:

No SSH

---

## RDS vs Database on EC2

| RDS | Database on EC2 |
|---|---|
| Managed database | Self-managed database |
| AWS handles OS patching | You patch OS |
| Automated backups | You manage backups |
| Monitoring available | You configure/manage monitoring |
| Multi-AZ options | You design HA |
| No SSH to underlying host | Full server access |

---

## RDS vs DynamoDB

### RDS

Relational database using SQL.

### DynamoDB

NoSQL database.

| RDS | DynamoDB |
|---|---|
| Relational | NoSQL |
| SQL | Key-value |
| Structured data | Flexible NoSQL data |
| Managed | Fully managed/serverless |

See:

[[04-Databases/DynamoDB]]

---

## RDS vs Redshift

### RDS

Used for relational application databases.

### Redshift

Designed for:

Analytics and Data Warehousing

### Memory Trick

RDS = Application Database

Redshift = Analytics Database

See:

[[04-Databases/Redshift]]

---

## RDS vs Aurora

Aurora is AWS's proprietary relational database technology.

It is compatible with:

- MySQL
- PostgreSQL

Your course positions Aurora as the higher-performance, AWS cloud-optimized relational database option.

See:

[[04-Databases/Aurora]]

---

## Common Use Cases

- Applications
- Websites
- Structured data
- SQL databases
- Managed relational workloads

---

## Exam Scenarios

A company needs a managed relational SQL database.

→ RDS

---

A company wants AWS to handle database OS patching and automated backups.

→ RDS

---

A database receives heavy read traffic and needs improved read performance.

→ Read Replica

---

A company needs RDS disaster recovery across Availability Zones.

→ Multi-AZ

---

A company needs to restore an RDS database to a specific timestamp.

→ Point-in-Time Restore

---

A company needs full SSH access to the underlying database server.

→ A self-managed database on EC2 may be more appropriate than RDS

---

An application requires a NoSQL key-value database.

→ DynamoDB

---

A company needs a data warehouse for analytics.

→ Redshift

---

## Exam Keywords

Relational

SQL

Managed database

Automated backups

Point-in-Time Restore

Read Replica

Multi-AZ

Disaster Recovery

Scaling

OS patching

---

## Memory Tricks

RDS = Managed SQL Database

Read Replica = Read Performance

Multi-AZ = Disaster Recovery

RDS = No SSH

RDS = Application Database

Redshift = Analytics

DynamoDB = NoSQL
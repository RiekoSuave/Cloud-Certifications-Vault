## What Problem Does It Solve?

Migrates databases to AWS with minimal downtime.

AWS Database Migration Service (DMS) solves the downtime risk of database migrations by allowing the source database to remain available during the migration.

Think:

Source Database

↓

DMS

↓

AWS Database

while the source database remains available.

### Memory Trick

DMS = Move Databases

---

## Type

Database Migration Service

---

## What Is DMS?

AWS Database Migration Service helps you quickly and securely migrate databases to AWS.

Your course describes DMS as:

- Resilient
- Self-healing
- Designed to keep the source database available during migration

### Memory Trick

DMS = Database Migration With Minimal Downtime

---

## Source Database Remains Available

This is one of the most important DMS concepts for the CCP exam.

During the migration:

Source Database

↓

Remains Available

↓

DMS Migrates Data

↓

Target Database

This reduces downtime during the migration process.

### Exam Recognition

"Database migration with minimal downtime"

→ DMS

"Source database must remain available during migration"

→ DMS

---

## Homogeneous Migrations

DMS supports:

Homogeneous Migrations

This means migrating between the same database technology.

Your course example:

Oracle

↓

DMS

↓

Oracle

### Memory Trick

Homogeneous = SAME

---

## Heterogeneous Migrations

DMS also supports:

Heterogeneous Migrations

This means migrating between different database technologies.

Your course example:

Microsoft SQL Server

↓

DMS

↓

Amazon Aurora

### Memory Trick

Heterogeneous = DIFFERENT

---

## Homogeneous vs Heterogeneous

| Migration Type | Meaning | Course Example |
| --- | --- | --- |
| Homogeneous | Same database technology | Oracle → Oracle |
| Heterogeneous | Different database technologies | SQL Server → Aurora |

### Memory Trick

Homo = SAME

Hetero = DIFFERENT

---

## Key Features

- Database migration
- Minimal downtime
- Source database remains available
- Resilient
- Self-healing
- Homogeneous migrations
- Heterogeneous migrations

---

## Common Use Cases

- Migrating databases to AWS
- Database modernization
- Moving databases with minimal downtime
- Moving between the same database technologies
- Moving between different database technologies

---

## DMS vs Migration Hub

### DMS

Actually migrates:

Databases

### Migration Hub

Helps:

Track and manage migrations

| DMS | Migration Hub |
| --- | --- |
| Database migration | Migration tracking |
| Moves database data | Central migration visibility |
| Minimal downtime | Assessment and planning |
| Database-focused | Migration management |

### Memory Trick

DMS = MOVE DATABASES

Migration Hub = TRACK MIGRATIONS

---

## Scenario Questions

A company needs to migrate a database to AWS while keeping the source database available.

→ DMS

---

A company needs to migrate Oracle to Oracle.

→ DMS

Homogeneous Migration

---

A company needs to migrate Microsoft SQL Server to Amazon Aurora.

→ DMS

Heterogeneous Migration

---

A company needs to migrate a database with minimal downtime.

→ DMS

---

A company needs a central location to track the progress of multiple migrations.

→ Migration Hub

NOT DMS

---

## Don't Confuse These

DMS = Database Migration

Migration Hub = Migration Tracking

DMS = Minimal Downtime

Homogeneous = Same Database Technology

Heterogeneous = Different Database Technologies

---

## Exam Keywords

AWS Database Migration Service

DMS

Database Migration

Minimal Downtime

Source Database Remains Available

Homogeneous Migration

Heterogeneous Migration

Replication

---

## Memory Tricks

DMS = Move Databases

Minimal Downtime = DMS

Source Stays Available = DMS

Homogeneous = SAME

Heterogeneous = DIFFERENT

Migration Hub = TRACK

---

## Quick Cheat Sheet

DMS = Database Migration

DMS = Minimal Downtime

Source Database Remains Available

Homogeneous = Same Database Technology

Heterogeneous = Different Database Technologies

Oracle → Oracle = Homogeneous

SQL Server → Aurora = Heterogeneous

DMS = MOVE DATABASES

Migration Hub = TRACK MIGRATIONS
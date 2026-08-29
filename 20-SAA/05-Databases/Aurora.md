## What Problem Does It Solve?

Traditional relational databases can become difficult to:

SCALE

↓

REPLICATE

↓

FAIL OVER

↓

MANAGE STORAGE

Aurora provides an:

AWS CLOUD-OPTIMIZED

relational database designed for:

HIGH PERFORMANCE

↓

HIGH AVAILABILITY

↓

READ SCALING

↓

AUTOMATIC STORAGE GROWTH

Think:

MYSQL / POSTGRESQL

↓

AWS CLOUD-OPTIMIZED DATABASE

↓

AURORA

### Memory Trick

AURORA

=

AWS-OPTIMIZED SQL DATABASE

---

## What Is Aurora?

Aurora is:

AWS PROPRIETARY DATABASE TECHNOLOGY

It is:

NOT OPEN SOURCE

Aurora is compatible with:

MYSQL

and:

POSTGRESQL

Think:

MYSQL APPLICATION

or:

POSTGRESQL APPLICATION

↓

AURORA-COMPATIBLE DATABASE

### Memory Trick

AURORA

=

MYSQL / POSTGRES COMPATIBLE

---

## Aurora Is Relational

Aurora is a:

RELATIONAL DATABASE

Think:

SQL

↓

TRANSACTIONS

↓

STRUCTURED DATA

↓

AURORA

It belongs to the same general database category as:

[RDS Overview](<RDS Overview>)

but Aurora's architecture is:

AWS CLOUD-OPTIMIZED

---

## Aurora Compatibility

Aurora supports compatibility with:

MYSQL

and:

POSTGRESQL

This means existing:

DATABASE DRIVERS

can work with Aurora as though they were connecting to:

MYSQL

or:

POSTGRESQL

Think:

APPLICATION

↓

MYSQL / POSTGRES DRIVER

↓

AURORA

### Memory Trick

AURORA

=

FAMILIAR SQL + AWS ARCHITECTURE

---

## Aurora Performance

Your course highlights that Aurora claims:

UP TO 5X

the performance of:

MYSQL ON RDS

and:

UP TO 3X

the performance of:

POSTGRESQL ON RDS

Think:

MYSQL RDS

↓

AURORA

↓

UP TO 5X

and:

POSTGRES RDS

↓

AURORA

↓

UP TO 3X

### Memory Trick

AURORA PERFORMANCE

=

5X MYSQL

3X POSTGRES

---

## Aurora vs Standard RDS

### Standard RDS

Supports multiple database engines such as:

MYSQL

POSTGRESQL

MARIADB

ORACLE

SQL SERVER

DB2

---

### Aurora

Supports:

MYSQL COMPATIBILITY

and:

POSTGRESQL COMPATIBILITY

with an:

AWS-OPTIMIZED ARCHITECTURE

Think:

NEED ORACLE?

↓

RDS

NEED SQL SERVER?

↓

RDS

NEED AWS-OPTIMIZED MYSQL / POSTGRES?

↓

AURORA

---

## Aurora Storage Architecture

Aurora separates:

COMPUTE

from:

STORAGE

Think:

DATABASE INSTANCES

↓

SHARED AURORA STORAGE

Multiple Aurora database instances access the same:

SHARED STORAGE VOLUME

### Memory Trick

AURORA

=

SHARED STORAGE

---

## Aurora Storage Auto Scaling

Aurora storage grows:

AUTOMATICALLY

as more data is stored.

Your course highlights growth in increments of:

10 GB

up to:

256 TB

Think:

DATABASE GROWS

↓

AURORA STORAGE GROWS

↓

NO MANUAL DISK RESIZING

### Memory Trick

AURORA STORAGE

=

AUTO GROW

---

## Aurora Storage Growth

Think:

10 GB

↓

20 GB

↓

30 GB

↓

...

↓

AUTOMATIC EXPANSION

Aurora automatically increases storage as required.

This reduces:

STORAGE CAPACITY PLANNING

compared with manually sizing database storage.

### Memory Trick

AURORA

=

STORE MORE → STORAGE GROWS

---

## Aurora High Availability

Aurora is designed to be:

HIGHLY AVAILABLE

The underlying storage maintains:

6 COPIES

of your data

across:

3 AVAILABILITY ZONES

Think:

AZ-A

↓

2 COPIES

AZ-B

↓

2 COPIES

AZ-C

↓

2 COPIES

TOTAL

=

6 COPIES

### Memory Trick

AURORA STORAGE

=

6 COPIES / 3 AZs

---

## Aurora Storage Quorum

Your course highlights:

4 COPIES OUT OF 6

are needed for:

WRITES

and:

3 COPIES OUT OF 6

are needed for:

READS

Think:

WRITE

=

4 / 6

READ

=

3 / 6

### Memory Trick

AURORA

=

WRITE 4

READ 3

OUT OF 6

---

## Aurora Self-Healing Storage

Aurora storage is:

SELF-HEALING

using:

PEER-TO-PEER REPLICATION

Think:

BAD STORAGE COPY

↓

OTHER COPIES

↓

REPAIR

Aurora's distributed storage architecture automatically helps maintain:

DATA DURABILITY

and:

AVAILABILITY

### Memory Trick

AURORA STORAGE

=

SELF-HEALING

---

## Aurora Storage Is Distributed

Aurora storage is striped across:

HUNDREDS OF VOLUMES

Think:

DATABASE DATA

↓

DISTRIBUTED STORAGE

↓

MANY STORAGE VOLUMES

This architecture contributes to Aurora's:

PERFORMANCE

↓

RESILIENCY

↓

SCALABILITY

---

## Aurora Writer Instance

An Aurora cluster has:

ONE WRITER

that handles:

WRITES

Think:

APPLICATION WRITE

↓

AURORA WRITER

↓

SHARED STORAGE

Your course refers to this as the:

MASTER

or:

WRITER INSTANCE

### Memory Trick

AURORA WRITER

=

ONE WRITE INSTANCE

---

## Aurora Read Replicas

Aurora can have:

UP TO 15

Aurora Read Replicas.

Think:

WRITER

↓

SHARED STORAGE

↓

READER #1

READER #2

READER #3

...

UP TO 15

These replicas help:

SCALE READ TRAFFIC

### Memory Trick

AURORA REPLICAS

=

SCALE READS

---

## Aurora Replica Lag

Aurora replication is designed to be:

VERY FAST

Your course highlights replica lag of:

LESS THAN 10 MILLISECONDS

Think:

WRITER

↓

FAST REPLICATION

↓

READ REPLICAS

### Memory Trick

AURORA REPLICA LAG

=

SUB-10 MS

---

## Aurora Read Scaling

A typical architecture is:

APPLICATION

↓

WRITES

↓

AURORA WRITER

and:

APPLICATION

↓

READS

↓

AURORA READ REPLICAS

Think:

ONE WRITER

↓

MANY READERS

### Memory Trick

WRITE

=

WRITER

READ

=

REPLICAS

---

## Aurora Automatic Failover

Aurora provides:

AUTOMATED FAILOVER

If the writer fails:

WRITER FAILURE

↓

AURORA REPLICA

↓

PROMOTED TO WRITER

Your SAA slides highlight failover in:

LESS THAN 30 SECONDS

### Memory Trick

AURORA

=

HA NATIVE

---

## Aurora Failover Architecture

Normal operation:

APPLICATION

↓

WRITER

↓

SHARED STORAGE

and:

READ REPLICAS

↓

SHARED STORAGE

Writer fails:

WRITER

↓

FAILS

↓

AURORA REPLICA PROMOTED

↓

NEW WRITER

Think:

REPLICA

↓

BECOMES WRITER

### Memory Trick

AURORA FAILURE

=

PROMOTE REPLICA

---

## Aurora Is High Availability Native

Your course describes Aurora as:

HIGH AVAILABILITY NATIVE

because its architecture includes:

MULTI-AZ STORAGE

↓

MULTIPLE DATA COPIES

↓

READ REPLICAS

↓

AUTOMATIC FAILOVER

Think:

AURORA

=

HA BUILT INTO ARCHITECTURE

---

## Aurora Cross-Region Replication

Aurora supports:

CROSS-REGION REPLICATION

Think:

REGION A

↓

AURORA

↓

REPLICATION

↓

REGION B

This can help support:

GLOBAL APPLICATIONS

and:

DISASTER RECOVERY

More advanced global Aurora architecture will be covered separately in:

[Aurora Global](<Aurora Global>)

---

## Aurora Cost

Your course notes that Aurora generally costs:

MORE THAN STANDARD RDS

approximately:

20% MORE

but can be:

MORE EFFICIENT

because of its performance and architecture.

Think:

HIGHER COST

↓

HIGHER PERFORMANCE / FEATURES

### Exam Thinking

Aurora is not necessarily:

THE CHEAPEST SQL DATABASE

It is optimized for:

PERFORMANCE

↓

AVAILABILITY

↓

SCALABILITY

---

## Aurora vs RDS Read Replicas

### RDS Read Replica

Separate database replica used for:

READ SCALING

Replication is:

ASYNCHRONOUS

---

### Aurora Replica

Shares Aurora's distributed storage architecture and provides:

FAST READ SCALING

with up to:

15 REPLICAS

Think:

RDS

=

TRADITIONAL READ REPLICA

AURORA

=

CLOUD-NATIVE REPLICA ARCHITECTURE

---

## Aurora vs RDS Multi-AZ

### RDS Multi-AZ

PRIMARY

↓

SYNC REPLICATION

↓

STANDBY

Purpose:

HIGH AVAILABILITY

---

### Aurora

6 STORAGE COPIES

↓

3 AZs

+

READ REPLICAS

+

AUTOMATIC FAILOVER

Think:

RDS MULTI-AZ

=

PRIMARY + STANDBY

AURORA

=

DISTRIBUTED HA ARCHITECTURE

### Memory Trick

RDS MULTI-AZ

=

STANDBY

AURORA

=

HA BUILT IN

---

## Aurora vs RDS Storage Auto Scaling

### RDS Storage Auto Scaling

RDS detects low storage and:

INCREASES ALLOCATED STORAGE

based on configured thresholds.

---

### Aurora

STORAGE AUTOMATICALLY EXPANDS

as data grows.

Think:

RDS

=

AUTO SCALE CONFIGURED STORAGE

AURORA

=

AUTO-EXPANDING SHARED STORAGE

---

## Aurora Architecture Thinking

A highly available Aurora application can look like:

USERS

↓

[Application Load Balancer](<Application Load Balancer>)

↓

[Auto Scaling Groups](<Auto Scaling Groups>)

↓

EC2 APPLICATION INSTANCES

↓

AURORA CLUSTER

Then:

WRITES

↓

WRITER INSTANCE

and:

READS

↓

AURORA REPLICAS

All database instances use:

SHARED DISTRIBUTED STORAGE

↓

6 COPIES

↓

3 AZs

Think:

APP TIER

=

HORIZONTAL SCALE

DATABASE TIER

=

AURORA HIGH AVAILABILITY + READ SCALE

---

## Aurora Failure Architecture

Imagine:

AZ-A

↓

WRITER

AZ-B

↓

READ REPLICA

AZ-C

↓

READ REPLICA

All use:

SHARED AURORA STORAGE

across:

3 AZs

If:

WRITER FAILS

↓

REPLICA PROMOTED

↓

APPLICATION CONTINUES

### Memory Trick

AURORA

=

WRITE ONCE

READ MANY

FAIL OVER FAST

---

## Why Choose Aurora?

Choose Aurora when the architecture needs:

RELATIONAL SQL

+

MYSQL / POSTGRES COMPATIBILITY

+

HIGH PERFORMANCE

+

HIGH AVAILABILITY

+

READ SCALABILITY

+

AUTOMATIC STORAGE GROWTH

Think:

HIGH-END CLOUD SQL REQUIREMENTS

↓

AURORA

---

## Scenario Recognition

Need an AWS-proprietary relational database?

→ Aurora

---

Need AWS-optimized MySQL-compatible database?

→ Aurora

---

Need AWS-optimized PostgreSQL-compatible database?

→ Aurora

---

Need up to 5x MySQL-on-RDS performance?

→ Aurora

---

Need up to 3x PostgreSQL-on-RDS performance?

→ Aurora

---

Need relational database storage that automatically grows?

→ Aurora

---

Need database data stored as 6 copies across 3 AZs?

→ Aurora

---

Question mentions:

4 OF 6 COPIES FOR WRITES?

→ Aurora

---

Question mentions:

3 OF 6 COPIES FOR READS?

→ Aurora

---

Need self-healing distributed database storage?

→ Aurora

---

Need up to 15 database Read Replicas?

→ Aurora

---

Need very low replica lag?

→ Aurora

---

Need automatic database failover?

→ Aurora

---

Need a relational database designed natively for high availability?

→ Aurora

---

Need Oracle compatibility?

→ RDS

NOT Aurora

---

Need SQL Server?

→ RDS

NOT Aurora

---

## Exam Traps

AURORA

=

RELATIONAL

---

AURORA

=

AWS PROPRIETARY

---

AURORA

≠

OPEN SOURCE

---

AURORA COMPATIBILITY

=

MYSQL + POSTGRESQL

---

AURORA

≠

ORACLE

---

AURORA

≠

SQL SERVER

---

MYSQL PERFORMANCE

=

UP TO 5X

---

POSTGRES PERFORMANCE

=

UP TO 3X

---

STORAGE

=

AUTO EXPANDING

---

STORAGE INCREMENT

=

10 GB

---

MAX STORAGE IN COURSE

=

256 TB

---

AURORA STORAGE

=

6 COPIES

---

AVAILABILITY ZONES

=

3

---

WRITE QUORUM

=

4 OF 6

---

READ QUORUM

=

3 OF 6

---

WRITER

=

ONE

---

READ REPLICAS

=

UP TO 15

---

REPLICA LAG

=

SUB-10 MS

---

AURORA

=

SELF-HEALING STORAGE

---

AURORA

=

AUTOMATED FAILOVER

---

AURORA

=

HIGH AVAILABILITY NATIVE

---

AURORA

=

GENERALLY MORE EXPENSIVE THAN STANDARD RDS

---

## Quick Cheat Sheet

AURORA

=

AWS-OPTIMIZED RELATIONAL DATABASE

COMPATIBILITY

=

MYSQL

POSTGRESQL

MYSQL PERFORMANCE

=

UP TO 5X

POSTGRES PERFORMANCE

=

UP TO 3X

STORAGE

=

AUTOMATICALLY GROWS

STORAGE INCREMENTS

=

10 GB

MAX STORAGE IN COURSE

=

256 TB

DATA COPIES

=

6

AZs

=

3

WRITES REQUIRE

=

4 / 6 COPIES

READS REQUIRE

=

3 / 6 COPIES

STORAGE

=

SELF-HEALING

WRITER

=

ONE

READ REPLICAS

=

UP TO 15

REPLICA LAG

=

LESS THAN 10 MS

FAILOVER

=

AUTOMATIC

HIGH AVAILABILITY

=

NATIVE

CROSS-REGION REPLICATION

=

SUPPORTED

COST

=

ABOUT 20% MORE THAN RDS

---

## Master Memory Trick

AURORA

=

MYSQL / POSTGRES

↓

AWS-OPTIMIZED

↓

FASTER

↓

AUTO-GROW STORAGE

↓

6 COPIES

↓

3 AZs

↓

ONE WRITER

↓

UP TO 15 READERS

↓

AUTOMATIC FAILOVER

Remember:

MYSQL

=

5X

POSTGRES

=

3X

STORAGE

=

6 COPIES / 3 AZ

WRITE

=

4 OF 6

READ

=

3 OF 6

REPLICAS

=

15

### Final Rule

QUESTION SAYS:

MANAGED SQL DATABASE?

↓

RDS

QUESTION SAYS:

HIGH-PERFORMANCE AWS-OPTIMIZED MYSQL / POSTGRES?

↓

AURORA

QUESTION SAYS:

READ SCALING ON STANDARD RDS?

↓

RDS READ REPLICA

QUESTION SAYS:

CLOUD-NATIVE HA + FAST READ SCALING?

↓

AURORA

---

## Related Notes

- [RDS Overview](<RDS Overview>)
- [RDS Storage Auto Scaling](<RDS Storage Auto Scaling>)
- [RDS Read Replicas](<RDS Read Replicas>)
- [RDS Multi-AZ](<RDS Multi-AZ>)
- [RDS Backups](<RDS Backups>)
- [Aurora Serverless](<Aurora Serverless>)
- [Aurora Global](<Aurora Global>)
- [Aurora Endpoints](<Aurora Endpoints>)
- [Aurora Auto Scaling](<Aurora Auto Scaling>)
- [Aurora Database Cloning](<Aurora Database Cloning>)
- [RDS Proxy](<RDS Proxy>)
- [SAA Databases Cheat Sheet](<SAA Databases Cheat Sheet>)
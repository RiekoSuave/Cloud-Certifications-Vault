## What Problem Does It Solve?

Running a relational database yourself requires managing:

DATABASE SOFTWARE

↓

OPERATING SYSTEM

↓

PATCHING

↓

BACKUPS

↓

HIGH AVAILABILITY

↓

SCALING

RDS provides:

MANAGED RELATIONAL DATABASES

so AWS handles much of the database infrastructure work.

Think:

MANAGE DATABASE YOURSELF

↓

MORE ADMINISTRATION

RDS

↓

AWS MANAGES DATABASE INFRASTRUCTURE

### Memory Trick

RDS

=

MANAGED SQL DATABASE

---

## What Is RDS?

RDS stands for:

RELATIONAL DATABASE SERVICE

RDS is a:

MANAGED DATABASE SERVICE

for databases that use:

SQL

Think:

APPLICATION

↓

SQL

↓

RDS

### Memory Trick

RDS

=

RELATIONAL + SQL

---

## Supported Database Engines

RDS supports several relational database engines.

Your course includes:

POSTGRESQL

↓

MYSQL

↓

MARIADB

↓

ORACLE

↓

MICROSOFT SQL SERVER

↓

IBM DB2

↓

AURORA

Think:

RDS

↓

CHOOSE SQL ENGINE

### Memory Trick

RDS

=

MULTIPLE RELATIONAL ENGINES

---

## Aurora

Aurora is:

AWS PROPRIETARY

relational database technology.

Aurora is compatible with:

MYSQL

and:

POSTGRESQL

Think:

AWS-BUILT RELATIONAL DATABASE

↓

AURORA

We'll cover Aurora separately in:

[Aurora](04-Databases/Aurora.md)

---

## RDS vs Database on EC2

You can install a database directly on:

[EC2](EC2)

But then:

YOU

must manage much more of the environment.

### Database on EC2

YOU MANAGE

↓

OS

↓

DATABASE INSTALLATION

↓

PATCHING

↓

BACKUPS

↓

HIGH AVAILABILITY

↓

SCALING

---

### RDS

AWS MANAGES

↓

DATABASE INFRASTRUCTURE

↓

PATCHING

↓

BACKUPS

↓

MONITORING

↓

FAILOVER FEATURES

Think:

EC2 DATABASE

=

MORE CONTROL + MORE MANAGEMENT

RDS

=

LESS MANAGEMENT

### Memory Trick

RDS

=

AWS DOES THE DATABASE ADMIN WORK

---

## RDS Is a Managed Service

RDS provides features such as:

AUTOMATED PROVISIONING

↓

OPERATING SYSTEM PATCHING

↓

CONTINUOUS BACKUPS

↓

MONITORING

↓

READ REPLICAS

↓

MULTI-AZ

↓

MAINTENANCE

↓

SCALING

Think:

DATABASE OPERATIONS

↓

AWS MANAGED

---

## Automated Provisioning

With RDS, AWS handles:

DATABASE INFRASTRUCTURE PROVISIONING

Think:

CREATE RDS DATABASE

↓

AWS PROVISIONS INFRASTRUCTURE

↓

DATABASE AVAILABLE

You do not need to manually install the database software on EC2.

---

## Operating System Patching

AWS manages:

UNDERLYING OS PATCHING

for normal RDS deployments.

Think:

RDS

↓

AWS MANAGES OS

This is one of the major operational advantages over:

DATABASE ON EC2

---

## RDS Backups

RDS supports:

CONTINUOUS BACKUPS

and:

POINT-IN-TIME RESTORE

Think:

DATABASE

↓

AUTOMATED BACKUP

↓

RESTORE TO SPECIFIC TIME

This allows recovery to a previous point in time.

We'll cover this further in:

[RDS Backups](<RDS Backups>)

### Memory Trick

RDS BACKUP

=

POINT-IN-TIME RECOVERY

---

## Monitoring

RDS provides:

MONITORING DASHBOARDS

Think:

RDS

↓

DATABASE METRICS

↓

MONITORING

This helps monitor database health and performance without building the monitoring infrastructure yourself.

---

## Read Replicas

RDS supports:

READ REPLICAS

for:

READ SCALABILITY

Think:

MAIN DATABASE

↓

REPLICATION

↓

READ REPLICA

Applications can send:

READ REQUESTS

to replicas.

This reduces read load on the primary database.

We'll cover this separately in:

[RDS Read Replicas](<RDS Read Replicas>)

### Memory Trick

READ REPLICA

=

SCALE READS

---

## Multi-AZ

RDS supports:

MULTI-AZ

for:

DISASTER RECOVERY

and:

HIGH AVAILABILITY

Think:

PRIMARY DB

↓

SYNCHRONOUS REPLICATION

↓

STANDBY DB

↓

DIFFERENT AZ

If the primary fails:

FAILOVER

↓

STANDBY

We'll cover this separately in:

[RDS Multi-AZ](<RDS Multi-AZ>)

### Memory Trick

MULTI-AZ

=

FAILOVER

---

## Read Replica vs Multi-AZ

This distinction is extremely important for the SAA exam.

### Read Replica

PURPOSE

=

READ SCALING

Think:

MORE READ CAPACITY

↓

READ REPLICA

---

### Multi-AZ

PURPOSE

=

HIGH AVAILABILITY / DISASTER RECOVERY

Think:

PRIMARY FAILURE

↓

FAILOVER

↓

STANDBY

### Memory Trick

READ REPLICA

=

PERFORMANCE

MULTI-AZ

=

AVAILABILITY

---

## Maintenance Windows

RDS provides:

MAINTENANCE WINDOWS

for tasks such as:

DATABASE UPGRADES

and:

SYSTEM MAINTENANCE

Think:

AWS MAINTENANCE

↓

DEFINED WINDOW

↓

DATABASE UPDATE

### Memory Trick

MAINTENANCE WINDOW

=

WHEN AWS CAN PERFORM MAINTENANCE

---

## RDS Scaling

RDS supports:

VERTICAL SCALING

and:

HORIZONTAL READ SCALING

Think:

NEED STRONGER DATABASE?

↓

BIGGER DB INSTANCE

Need more:

READ CAPACITY?

↓

READ REPLICAS

### Memory Trick

RDS SCALE UP

=

BIGGER INSTANCE

RDS SCALE READS

=

READ REPLICAS

---

## RDS Storage

RDS database storage is backed by:

EBS

Think:

RDS

↓

EBS STORAGE

You choose storage characteristics for the database.

RDS also supports:

STORAGE AUTO SCALING

which we'll cover separately.

See:

[RDS Storage Auto Scaling](<RDS Storage Auto Scaling>)

---

## RDS Storage Auto Scaling

RDS can automatically:

INCREASE DATABASE STORAGE

when free space becomes low.

Think:

DATABASE GROWS

↓

FREE STORAGE FALLS

↓

RDS AUTO SCALES STORAGE

This reduces the need to manually increase database disk capacity.

### Memory Trick

RDS STORAGE AUTO SCALING

=

AUTO GROW DATABASE DISK

---

## Maximum Storage Threshold

For Storage Auto Scaling, you define:

MAXIMUM STORAGE THRESHOLD

Think:

RDS

↓

CAN GROW

↓

UP TO MAXIMUM LIMIT

AWS does not automatically grow storage without a configured upper boundary.

---

## Storage Auto Scaling Trigger

Your course highlights that RDS can automatically increase storage when:

FREE STORAGE

is less than:

10%

of allocated storage

and:

LOW STORAGE

lasts for at least:

5 MINUTES

and:

6 HOURS

have passed since the last storage modification.

Think:

FREE SPACE < 10%

↓

FOR 5 MINUTES

↓

LAST CHANGE > 6 HOURS AGO

↓

AUTO SCALE STORAGE

### Memory Trick

RDS STORAGE AUTO SCALE

=

10% + 5 MIN + 6 HOURS

---

## Storage Auto Scaling Use Case

Storage Auto Scaling is especially useful for:

UNPREDICTABLE DATABASE GROWTH

Think:

DATABASE SIZE HARD TO PREDICT

↓

RDS STORAGE AUTO SCALING

↓

NO MANUAL RESIZE EACH TIME

Your course notes that it supports:

ALL RDS DATABASE ENGINES

---

## RDS Cannot Be SSH'd Into

A major RDS limitation is:

YOU CANNOT SSH

into the underlying RDS instance.

Think:

MANAGED SERVICE

↓

NO NORMAL OS ACCESS

This is different from:

DATABASE ON EC2

where you control the operating system.

### Memory Trick

RDS

=

MANAGED

↓

NO SSH

---

## Why No SSH?

AWS manages:

THE UNDERLYING INFRASTRUCTURE

Therefore normal RDS does not give you direct operating system access.

Think:

MORE AWS MANAGEMENT

↓

LESS LOW-LEVEL CONTROL

### Exam Thinking

Need full OS access to customize the database host?

↓

NORMAL RDS MAY NOT BE THE RIGHT DEPLOYMENT

Think about:

DATABASE ON EC2

or specialized options such as:

[RDS Custom](<RDS Custom>)

---

## RDS Architecture Thinking

A common web application architecture is:

USERS

↓

LOAD BALANCER

↓

EC2 INSTANCES

↓

RDS

Think:

WEB TIER

↓

APPLICATION TIER

↓

RELATIONAL DATABASE

The EC2 application communicates with RDS using:

SQL

---

## RDS and Auto Scaling Architecture

A scalable application might use:

USERS

↓

[Application Load Balancer](<Application Load Balancer>)

↓

[Auto Scaling Groups](<Auto Scaling Groups>)

↓

EC2 INSTANCES

↓

RDS

Think:

WEB / APP TIER

=

HORIZONTALLY SCALE

DATABASE TIER

=

RDS

---

## When Should You Think RDS?

Think RDS when the question requires:

RELATIONAL DATA

↓

SQL

↓

TRANSACTIONS

↓

STRUCTURED SCHEMA

↓

JOINS

Think:

RELATIONAL APPLICATION

↓

RDS

### Memory Trick

SQL + RELATIONAL

=

RDS

---

## RDS vs DynamoDB Preview

### RDS

RELATIONAL

↓

SQL

↓

JOINS

↓

STRUCTURED DATA

### DynamoDB

NOSQL

↓

KEY-VALUE / DOCUMENT

↓

MASSIVE SCALE

Think:

RELATIONAL SQL?

↓

RDS

NOSQL?

↓

DYNAMODB

We'll cover DynamoDB later.

---

## RDS vs Aurora Preview

### RDS

Managed relational database service supporting multiple database engines.

### Aurora

AWS cloud-optimized relational database compatible with:

MYSQL

and:

POSTGRESQL

Think:

STANDARD MANAGED SQL ENGINES

↓

RDS

AWS-OPTIMIZED MYSQL / POSTGRES

↓

AURORA

---

## Scenario Recognition

Need a managed relational database?

→ RDS

---

Need SQL database in AWS?

→ RDS

---

Need managed PostgreSQL?

→ RDS

---

Need managed MySQL?

→ RDS

---

Need managed Oracle database?

→ RDS

---

Need managed Microsoft SQL Server?

→ RDS

---

Need AWS to handle OS patching for the database?

→ RDS

---

Need point-in-time database recovery?

→ RDS Automated Backups

---

Need to scale database reads?

→ RDS Read Replicas

---

Need database failover across Availability Zones?

→ RDS Multi-AZ

---

Need database storage automatically increased?

→ RDS Storage Auto Scaling

---

Need unpredictable database storage growth handled automatically?

→ RDS Storage Auto Scaling

---

Need direct SSH access to the database server?

→ Normal RDS is not the answer

---

Need full control over database host operating system?

→ Database on EC2 / RDS Custom

---

Need relational database joins and transactions?

→ RDS

---

## Exam Traps

RDS

=

RELATIONAL DATABASE SERVICE

---

RDS

=

SQL

---

RDS

=

MANAGED SERVICE

---

RDS

=

AWS MANAGES OS PATCHING

---

RDS

=

AUTOMATED BACKUPS

---

POINT-IN-TIME RESTORE

=

RDS BACKUPS

---

READ REPLICA

=

READ SCALING

---

MULTI-AZ

=

DISASTER RECOVERY / HIGH AVAILABILITY

---

READ REPLICA

≠

MULTI-AZ

---

READ REPLICA

=

PERFORMANCE

MULTI-AZ

=

AVAILABILITY

---

RDS STORAGE

=

EBS BACKED

---

RDS STORAGE AUTO SCALING

=

INCREASE STORAGE AUTOMATICALLY

---

RDS

=

NO NORMAL SSH ACCESS

---

RDS

≠

NOSQL DATABASE

---

## Quick Cheat Sheet

RDS

=

RELATIONAL DATABASE SERVICE

TYPE

=

MANAGED SQL DATABASE

ENGINES

=

POSTGRESQL

MYSQL

MARIADB

ORACLE

SQL SERVER

DB2

AURORA

AWS MANAGES

=

PROVISIONING

OS PATCHING

BACKUPS

MONITORING

MAINTENANCE

READ REPLICA

=

READ SCALING

MULTI-AZ

=

HIGH AVAILABILITY / DR

BACKUPS

=

POINT-IN-TIME RESTORE

STORAGE

=

EBS BACKED

STORAGE AUTO SCALING

=

AUTO INCREASE STORAGE

FREE STORAGE TRIGGER

=

LESS THAN 10%

LOW STORAGE DURATION

=

5 MINUTES

TIME SINCE LAST STORAGE CHANGE

=

6 HOURS

SSH

=

NO

---

## Master Memory Trick

RDS

=

RUN DATABASE SERVICE

Think:

APPLICATION

↓

SQL

↓

RDS

AWS HANDLES:

PROVISIONING

↓

PATCHING

↓

BACKUPS

↓

MONITORING

↓

FAILOVER FEATURES

And remember:

READ REPLICA

=

SCALE READS

MULTI-AZ

=

SURVIVE FAILURE

STORAGE AUTO SCALING

=

GROW DISK

NO SSH

=

MANAGED SERVICE

---

## Related Notes

- [RDS Read Replicas](<RDS Read Replicas>)
- [RDS Multi-AZ](<RDS Multi-AZ>)
- [RDS Backups](<RDS Backups>)
- [RDS Storage Auto Scaling](<RDS Storage Auto Scaling>)
- [Aurora](04-Databases/Aurora.md)
- [ElastiCache](ElastiCache)
- [RDS Proxy](<RDS Proxy>)
- [RDS Custom](<RDS Custom>)
- [EC2](EC2)
- [EBS Volumes](<EBS Volumes>)
- [Application Load Balancer](<Application Load Balancer>)
- [Auto Scaling Groups](<Auto Scaling Groups>)
- [SAA Databases Cheat Sheet](<SAA Databases Cheat Sheet>)
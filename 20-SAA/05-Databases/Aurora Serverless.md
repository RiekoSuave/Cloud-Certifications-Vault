## What Problem Does It Solve?

Some database workloads are:

INFREQUENT

↓

INTERMITTENT

↓

UNPREDICTABLE

With a traditional provisioned database, you may have to:

ESTIMATE CAPACITY

↓

PROVISION DATABASE INSTANCES

↓

PAY EVEN WHEN USAGE IS LOW

Aurora Serverless automatically:

PROVISIONS

and:

SCALES DATABASE CAPACITY

based on actual usage.

Think:

DATABASE DEMAND CHANGES

↓

AURORA SERVERLESS

↓

CAPACITY CHANGES AUTOMATICALLY

### Memory Trick

AURORA SERVERLESS

=

DATABASE CAPACITY ON DEMAND

---

## What Is Aurora Serverless?

Aurora Serverless is an:

ON-DEMAND

AUTO-SCALING

configuration for:

AURORA

Think:

APPLICATION

↓

AURORA SERVERLESS

↓

DATABASE CAPACITY AUTOMATICALLY ADJUSTS

You do not need to manually manage:

FIXED DATABASE CAPACITY

in the same way as a provisioned Aurora deployment.

### Memory Trick

SERVERLESS

=

NO CAPACITY PLANNING

---

## Automated Database Instantiation

Aurora Serverless provides:

AUTOMATED DATABASE INSTANTIATION

Think:

DATABASE NEEDED

↓

AURORA SERVERLESS

↓

CAPACITY PROVIDED AUTOMATICALLY

This reduces the need to manually:

PROVISION DATABASE INSTANCES

for changing workloads.

### Memory Trick

AURORA SERVERLESS

=

AWS INSTANTIATES DATABASE CAPACITY

---

## Automatic Scaling

Aurora Serverless automatically:

SCALES

based on:

ACTUAL DATABASE USAGE

Think:

USAGE ↑

↓

DATABASE CAPACITY ↑

USAGE ↓

↓

DATABASE CAPACITY ↓

### Memory Trick

ACTUAL USAGE

=

ACTUAL CAPACITY

---

## No Capacity Planning

One of the biggest advantages is:

NO CAPACITY PLANNING NEEDED

With provisioned databases, you may need to ask:

HOW LARGE SHOULD MY DATABASE INSTANCE BE?

With Aurora Serverless:

DEMAND

↓

AURORA SERVERLESS

↓

CAPACITY ADJUSTS

Think:

DON'T GUESS CAPACITY

↓

LET AURORA SCALE

### Memory Trick

SERVERLESS

=

DON'T SIZE IT YOURSELF

---

## Aurora Serverless Architecture

The SAA course shows an architecture involving:

CLIENT

↓

PROXY FLEET

↓

SHARED STORAGE VOLUME

The Proxy Fleet is:

MANAGED BY AURORA

Think:

CLIENT

↓

MANAGED PROXY FLEET

↓

AUTO-SCALED DATABASE CAPACITY

↓

SHARED AURORA STORAGE

### Memory Trick

CLIENT

↓

AURORA MANAGED PROXY

↓

DATABASE

---

## Managed Proxy Fleet

Aurora Serverless uses a:

PROXY FLEET

managed by Aurora.

Think:

APPLICATION CONNECTIONS

↓

PROXY FLEET

↓

DATABASE CAPACITY

The proxy layer helps separate:

CLIENT CONNECTIONS

from:

UNDERLYING DATABASE CAPACITY

### Memory Trick

PROXY FLEET

=

MANAGED CONNECTION LAYER

---

## Shared Storage Volume

Aurora Serverless still uses:

AURORA SHARED STORAGE

Think:

DATABASE COMPUTE

↓

SHARED STORAGE VOLUME

This connects Aurora Serverless to the same general Aurora architecture discussed in:

[Aurora](Aurora)

### Memory Trick

SERVERLESS COMPUTE

+

AURORA SHARED STORAGE

---

## Supported Compatibility

Aurora Serverless supports Aurora-compatible:

MYSQL

and:

POSTGRESQL

Think:

MYSQL-COMPATIBLE

or:

POSTGRES-COMPATIBLE

↓

AURORA SERVERLESS

### Memory Trick

AURORA SERVERLESS

=

MYSQL / POSTGRES COMPATIBLE

---

## Best Use Cases

Aurora Serverless is especially good for:

INFREQUENT WORKLOADS

↓

INTERMITTENT WORKLOADS

↓

UNPREDICTABLE WORKLOADS

Think:

DATABASE IS NOT BUSY ALL THE TIME

↓

AURORA SERVERLESS

### Memory Trick

I-I-U

=

INFREQUENT

INTERMITTENT

UNPREDICTABLE

---

## Infrequent Workloads

An infrequent workload uses the database:

ONLY OCCASIONALLY

Example:

INTERNAL REPORTING APPLICATION

↓

USED A FEW TIMES PER WEEK

Running fixed database capacity continuously may be:

INEFFICIENT

Think:

LOW FREQUENCY

↓

SERVERLESS

---

## Intermittent Workloads

An intermittent workload has:

PERIODS OF ACTIVITY

and:

PERIODS OF LITTLE OR NO ACTIVITY

Think:

BUSY

↓

QUIET

↓

BUSY

↓

QUIET

Aurora Serverless can adjust capacity as usage changes.

### Memory Trick

INTERMITTENT

=

ON AND OFF USAGE

---

## Unpredictable Workloads

An unpredictable workload has demand that is:

DIFFICULT TO FORECAST

Think:

TRAFFIC MAY SPIKE

↓

YOU DON'T KNOW WHEN

↓

AURORA SERVERLESS

This avoids trying to predict:

EXACT DATABASE CAPACITY

in advance.

### Memory Trick

UNPREDICTABLE

=

LET AWS SCALE

---

## Pay Per Second

Aurora Serverless uses:

PAY-PER-SECOND

billing for database capacity.

Think:

USE CAPACITY

↓

PAY FOR CAPACITY USED

This can make Aurora Serverless:

MORE COST-EFFECTIVE

for workloads that do not require large amounts of database capacity continuously.

### Memory Trick

SERVERLESS

=

PAY FOR ACTUAL USE

---

## Cost Thinking

Imagine two workloads.

### Workload A

DATABASE BUSY:

24 / 7

Predictable load.

Provisioned Aurora may make sense.

---

### Workload B

DATABASE BUSY:

A FEW HOURS

then:

QUIET

then:

UNEXPECTED SPIKE

Aurora Serverless may be more cost-effective.

Think:

VARIABLE USAGE

↓

SERVERLESS

### Exam Thinking

Question emphasizes:

PAY ONLY WHEN CAPACITY IS NEEDED

+

UNPREDICTABLE DATABASE USAGE

↓

AURORA SERVERLESS

---

## Least Management Overhead

Aurora Serverless reduces:

DATABASE CAPACITY MANAGEMENT

Think:

NO MANUAL SIZING

↓

NO CONSTANT CAPACITY ADJUSTMENTS

↓

LESS OPERATIONAL MANAGEMENT

### Memory Trick

SERVERLESS

=

LESS DATABASE CAPACITY MANAGEMENT

---

## Aurora Serverless vs Provisioned Aurora

### Provisioned Aurora

You provision:

DATABASE INSTANCES

and choose capacity.

Think:

KNOWN WORKLOAD

↓

PROVISION CAPACITY

---

### Aurora Serverless

Capacity is:

AUTOMATICALLY ADJUSTED

based on:

ACTUAL USAGE

Think:

VARIABLE WORKLOAD

↓

SERVERLESS

### Memory Trick

PROVISIONED

=

YOU SIZE

SERVERLESS

=

AWS SIZES

---

## Aurora Serverless vs Aurora Auto Scaling

Do not confuse:

[Aurora Auto Scaling](<Aurora Auto Scaling>)

with:

AURORA SERVERLESS

### Aurora Auto Scaling

Automatically changes:

NUMBER OF READ REPLICAS

Think:

READ SCALING

---

### Aurora Serverless

Automatically adjusts:

DATABASE CAPACITY

based on actual usage.

Think:

DATABASE CAPACITY SCALING

### Memory Trick

AURORA AUTO SCALING

=

READERS

AURORA SERVERLESS

=

CAPACITY

---

## Aurora Serverless vs RDS Storage Auto Scaling

Do not confuse:

SERVERLESS DATABASE CAPACITY

with:

DATABASE STORAGE CAPACITY

### Aurora Serverless

Adjusts:

COMPUTE CAPACITY

based on usage.

### RDS Storage Auto Scaling

Adjusts:

DATABASE STORAGE

when free disk space becomes low.

Think:

COMPUTE DEMAND

↓

AURORA SERVERLESS

DISK SPACE

↓

RDS STORAGE AUTO SCALING

---

## Aurora Serverless vs DynamoDB

Both may appear in questions involving:

SERVERLESS DATABASES

But they are very different.

### Aurora Serverless

RELATIONAL

↓

SQL

↓

MYSQL / POSTGRES COMPATIBLE

### DynamoDB

NOSQL

↓

KEY-VALUE / DOCUMENT

Think:

SERVERLESS + SQL

↓

AURORA SERVERLESS

SERVERLESS + NOSQL

↓

DYNAMODB

### Memory Trick

AURORA SERVERLESS

=

SERVERLESS SQL

DYNAMODB

=

SERVERLESS NOSQL

---

## Aurora Serverless Architecture Thinking

Imagine an application used unpredictably throughout the month.

CLIENT

↓

AURORA SERVERLESS

↓

MANAGED PROXY FLEET

↓

DATABASE CAPACITY

↓

SHARED STORAGE

When traffic increases:

USAGE ↑

↓

CAPACITY ↑

When traffic decreases:

USAGE ↓

↓

CAPACITY ↓

The application does not need to manually:

RESIZE DATABASE INSTANCES

### Memory Trick

LOAD CHANGES

↓

CAPACITY FOLLOWS

---

## Development / Test Workloads

Aurora Serverless can be useful when a database is not required at:

FULL PRODUCTION CAPACITY

all the time.

Think:

DEVELOPMENT

↓

TESTING

↓

TEMPORARY APPLICATION

↓

VARIABLE DATABASE USE

The key exam clue remains:

INFREQUENT / INTERMITTENT / UNPREDICTABLE

---

## New Application Workloads

Imagine launching a new application where:

EXPECTED DATABASE TRAFFIC IS UNKNOWN

Instead of guessing:

SMALL INSTANCE?

↓

MEDIUM INSTANCE?

↓

LARGE INSTANCE?

You can use:

AURORA SERVERLESS

Think:

UNKNOWN DEMAND

↓

NO CAPACITY PLANNING

### Memory Trick

DON'T KNOW DATABASE SIZE?

↓

SERVERLESS

---

## Predictable vs Unpredictable

### Predictable Workload

KNOWN CAPACITY

↓

PROVISIONED AURORA MAY FIT

### Unpredictable Workload

UNKNOWN CAPACITY

↓

AURORA SERVERLESS

Think:

CAN PREDICT?

↓

PROVISION

CAN'T PREDICT?

↓

SERVERLESS

---

## Scenario Recognition

Need Aurora database capacity to automatically scale based on usage?

→ Aurora Serverless

---

Need a relational database with no capacity planning?

→ Aurora Serverless

---

Need MySQL-compatible serverless relational database?

→ Aurora Serverless

---

Need PostgreSQL-compatible serverless relational database?

→ Aurora Serverless

---

Database workload is infrequent?

→ Aurora Serverless

---

Database workload is intermittent?

→ Aurora Serverless

---

Database workload is unpredictable?

→ Aurora Serverless

---

Need least database capacity management overhead?

→ Aurora Serverless

---

Need pay-per-second database capacity?

→ Aurora Serverless

---

Need read replicas automatically added or removed?

→ Aurora Auto Scaling

NOT Aurora Serverless

---

Need database storage automatically increased?

→ Aurora Storage Auto Expansion / RDS Storage Auto Scaling

NOT Aurora Serverless

---

Need serverless NoSQL?

→ DynamoDB

NOT Aurora Serverless

---

Need serverless relational SQL?

→ Aurora Serverless

---

## Exam Traps

AURORA SERVERLESS

=

RELATIONAL SQL

---

AURORA SERVERLESS

=

MYSQL / POSTGRES COMPATIBLE

---

AURORA SERVERLESS

=

AUTOMATED DATABASE INSTANTIATION

---

AURORA SERVERLESS

=

AUTO SCALE BASED ON ACTUAL USAGE

---

AURORA SERVERLESS

=

NO CAPACITY PLANNING

---

AURORA SERVERLESS

=

PAY PER SECOND

---

BEST WORKLOADS

=

INFREQUENT

INTERMITTENT

UNPREDICTABLE

---

AURORA SERVERLESS

≠

DYNAMODB

---

AURORA SERVERLESS

=

SQL

DYNAMODB

=

NOSQL

---

AURORA AUTO SCALING

=

READ REPLICAS

AURORA SERVERLESS

=

DATABASE CAPACITY

---

SERVERLESS

≠

NO DATABASE

It means:

YOU DON'T MANAGE FIXED SERVER CAPACITY

in the traditional way.

---

## Quick Cheat Sheet

AURORA SERVERLESS

=

SERVERLESS RELATIONAL DATABASE

COMPATIBILITY

=

MYSQL / POSTGRESQL

SCALING

=

AUTOMATIC BASED ON ACTUAL USAGE

DATABASE INSTANTIATION

=

AUTOMATIC

CAPACITY PLANNING

=

NOT NEEDED

BILLING

=

PAY PER SECOND

MANAGEMENT OVERHEAD

=

LOW

BEST FOR

=

INFREQUENT

INTERMITTENT

UNPREDICTABLE WORKLOADS

ARCHITECTURE

=

MANAGED PROXY FLEET + SHARED STORAGE

AURORA AUTO SCALING

=

READ REPLICA SCALING

AURORA SERVERLESS

=

DATABASE CAPACITY SCALING

DYNAMODB

=

SERVERLESS NOSQL

AURORA SERVERLESS

=

SERVERLESS SQL

---

## Master Memory Trick

AURORA SERVERLESS

=

DON'T GUESS CAPACITY

Think:

DATABASE USAGE

↓

LOW

↓

HIGH

↓

LOW

↓

UNPREDICTABLE

Aurora Serverless:

↓

INSTANTIATES CAPACITY

↓

SCALES AUTOMATICALLY

↓

PAY PER SECOND

Remember:

INFREQUENT

↓

INTERMITTENT

↓

UNPREDICTABLE

=

AURORA SERVERLESS

### Final Rule

QUESTION SAYS:

MYSQL / POSTGRES

+

NO CAPACITY PLANNING

+

VARIABLE DATABASE USAGE

↓

AURORA SERVERLESS

QUESTION SAYS:

AUTO ADD READ REPLICAS

↓

AURORA AUTO SCALING

QUESTION SAYS:

SERVERLESS NOSQL

↓

DYNAMODB

---

## Related Notes

- [Aurora](Aurora)
- [Aurora Endpoints](<Aurora Endpoints>)
- [Aurora Auto Scaling](<Aurora Auto Scaling>)
- [Aurora Global](<Aurora Global>)
- [Aurora Database Cloning](<Aurora Database Cloning>)
- [RDS Overview](<RDS Overview>)
- [RDS Storage Auto Scaling](<RDS Storage Auto Scaling>)
- [DynamoDB](04-Databases/DynamoDB.md)
- [RDS Proxy](<RDS Proxy>)
- [SAA Databases Cheat Sheet](<SAA Databases Cheat Sheet>)
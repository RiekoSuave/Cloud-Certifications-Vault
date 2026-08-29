## What Problem Does It Solve?

A database can receive:

TOO MANY READ REQUESTS

If every read goes to the:

PRIMARY RDS DATABASE

the primary can become:

OVERLOADED

RDS Read Replicas allow you to:

SCALE READS

by creating additional database instances that receive replicated data from the primary.

Think:

PRIMARY DATABASE

↓

READ TRAFFIC TOO HIGH

↓

CREATE READ REPLICAS

↓

DISTRIBUTE READS

### Memory Trick

READ REPLICA

=

SCALE READS

---

## What Is an RDS Read Replica?

An RDS Read Replica is a:

READ-ONLY COPY

of an RDS database.

Think:

PRIMARY RDS

↓

REPLICATION

↓

READ REPLICA

Applications can send:

READ REQUESTS

to the Read Replica instead of sending every read to the primary.

### Memory Trick

PRIMARY

=

READ + WRITE

READ REPLICA

=

READ

---

## Why Use Read Replicas?

Read Replicas improve:

READ SCALABILITY

Think:

APPLICATION

↓

READS + WRITES

↓

PRIMARY DATABASE

As read traffic increases:

PRIMARY

↓

TOO MANY READS

Instead:

APPLICATION

↓

WRITES

↓

PRIMARY

and:

APPLICATION

↓

READS

↓

READ REPLICAS

This reduces:

READ LOAD

on the primary database.

---

## Read Replica Architecture

Imagine:

APPLICATION

↓

PRIMARY RDS

The primary handles:

READS

+

WRITES

Now create:

READ REPLICA #1

READ REPLICA #2

Architecture:

APPLICATION

↓

WRITES

↓

PRIMARY RDS

and:

APPLICATION

↓

READS

↓

READ REPLICA #1

or:

READ REPLICA #2

### Memory Trick

WRITE

=

PRIMARY

READ

=

PRIMARY OR REPLICA

---

## Replication Type

RDS Read Replicas use:

ASYNCHRONOUS REPLICATION

Think:

PRIMARY

↓

WRITE OCCURS

↓

REPLICATION HAPPENS AFTERWARD

↓

READ REPLICA

Because replication is asynchronous:

THE REPLICA MAY LAG

behind the primary.

### Memory Trick

READ REPLICA

=

ASYNC

---

## Replication Lag

Because Read Replicas use:

ASYNCHRONOUS REPLICATION

there can be:

REPLICATION LAG

Think:

PRIMARY

↓

NEW DATA WRITTEN

↓

SHORT DELAY

↓

READ REPLICA RECEIVES DATA

Therefore:

READ REPLICA

may temporarily contain:

SLIGHTLY OLDER DATA

### Exam Thinking

Need immediately consistent data after a write?

↓

READING FROM A REPLICA MAY NOT BE APPROPRIATE

because:

REPLICATION IS ASYNCHRONOUS

---

## Eventual Consistency

Read Replicas commonly involve:

EVENTUAL CONSISTENCY

Think:

WRITE TO PRIMARY

↓

REPLICA CATCHES UP

↓

EVENTUALLY SAME DATA

### Memory Trick

ASYNC REPLICATION

=

POSSIBLE LAG

---

## How Many Read Replicas?

Your course highlights that RDS can have:

UP TO 15 READ REPLICAS

depending on the database engine.

Think:

PRIMARY

↓

READ REPLICA #1

↓

READ REPLICA #2

↓

...

↓

UP TO 15

### Exam Thinking

The key concept is not just the number.

Remember:

READ REPLICAS

=

HORIZONTAL READ SCALING

---

## Read Replicas Within an AZ

A Read Replica can be created:

WITHIN THE SAME AVAILABILITY ZONE

Think:

AZ-A

↓

PRIMARY

+

READ REPLICA

This provides:

READ SCALABILITY

but does not provide the same AZ separation as a replica in another AZ.

---

## Cross-AZ Read Replicas

Read Replicas can also exist:

ACROSS AVAILABILITY ZONES

Think:

AZ-A

↓

PRIMARY

AZ-B

↓

READ REPLICA

This still primarily solves:

READ SCALABILITY

### Important

Do not automatically interpret:

DIFFERENT AZ

as:

MULTI-AZ

A Read Replica in another AZ is still:

A READ REPLICA

### Memory Trick

READ REPLICA

=

READ SCALING

EVEN ACROSS AZs

---

## Cross-Region Read Replicas

Read Replicas can also be created:

ACROSS AWS REGIONS

Think:

REGION A

↓

PRIMARY RDS

↓

CROSS-REGION REPLICATION

↓

REGION B

↓

READ REPLICA

This can help with:

READS CLOSER TO USERS

and:

DISASTER RECOVERY STRATEGIES

### Memory Trick

CROSS-REGION READ REPLICA

=

READS IN ANOTHER REGION

---

## Read Replica Use Case

Imagine a production database receives:

NORMAL APPLICATION TRAFFIC

and:

REPORTING / ANALYTICS QUERIES

Reporting queries can be:

READ-HEAVY

and may put significant load on the production database.

Instead:

PRODUCTION APPLICATION

↓

PRIMARY RDS

and:

REPORTING APPLICATION

↓

READ REPLICA

Think:

PRIMARY

=

PRODUCTION WORKLOAD

READ REPLICA

=

REPORTING / ANALYTICS READS

### Memory Trick

REPORTING

=

READ REPLICA

---

## Classic Exam Scenario

A company has:

PRODUCTION RDS DATABASE

A reporting application performs:

HEAVY READ QUERIES

The reporting workload is slowing down the production database.

Solution:

CREATE A READ REPLICA

↓

RUN REPORTING QUERIES AGAINST REPLICA

### Memory Trick

READ-HEAVY REPORTING

=

READ REPLICA

---

## Applications Must Use the Replica

Creating a Read Replica does not automatically redirect application reads.

The application must:

CONNECT TO THE READ REPLICA

Think:

READ REPLICA CREATED

↓

NEW DATABASE ENDPOINT

↓

APPLICATION USES ENDPOINT

### Exam Trap

READ REPLICA

≠

AUTOMATIC READ LOAD BALANCING

Your application must be designed to:

SEND READS TO REPLICAS

---

## Read Replica Endpoints

Each Read Replica has:

ITS OWN DATABASE ENDPOINT

Think:

PRIMARY

↓

PRIMARY ENDPOINT

READ REPLICA #1

↓

REPLICA ENDPOINT #1

READ REPLICA #2

↓

REPLICA ENDPOINT #2

The application chooses:

WHERE TO SEND READ REQUESTS

---

## Read Replicas Can Be Promoted

A Read Replica can be:

PROMOTED

into:

ITS OWN STANDALONE DATABASE

Think:

PRIMARY

↓

READ REPLICA

↓

PROMOTE

↓

INDEPENDENT DATABASE

After promotion:

REPLICATION STOPS

and the replica becomes:

READ + WRITE

### Memory Trick

PROMOTE REPLICA

=

MAKE IT ITS OWN DATABASE

---

## Promotion Use Case

Imagine:

PRIMARY RDS

↓

READ REPLICA

You want to create:

A NEW INDEPENDENT DATABASE

You can:

PROMOTE READ REPLICA

↓

STANDALONE RDS DATABASE

This can be useful in certain:

MIGRATION

or:

DISASTER RECOVERY

scenarios.

---

## Read Replica Network Cost

An important SAA cost distinction involves:

CROSS-AZ REPLICATION

For RDS Read Replicas:

CROSS-AZ REPLICATION TRAFFIC

can incur:

NETWORK COSTS

Think:

PRIMARY

↓

AZ-A

↓

DATA TRANSFER

↓

READ REPLICA

↓

AZ-B

### Memory Trick

RDS READ REPLICA CROSS-AZ

=

POSSIBLE NETWORK COST

---

## Multi-AZ Network Cost Comparison

For:

RDS MULTI-AZ

replication traffic between the primary and standby does:

NOT

incur the same cross-AZ replication charge.

Think:

READ REPLICA CROSS-AZ

↓

COST

MULTI-AZ REPLICATION

↓

NO CROSS-AZ REPLICATION CHARGE

### Exam Trap

READ REPLICA

and:

MULTI-AZ

have different:

PURPOSES

and:

COST BEHAVIOR

---

## Read Replica vs Multi-AZ

This is one of the most important RDS distinctions.

### Read Replica

PURPOSE

=

READ SCALABILITY

REPLICATION

=

ASYNCHRONOUS

CAN RECEIVE READ TRAFFIC

=

YES

APPLICATION CONNECTS TO IT

=

YES

---

### Multi-AZ

PURPOSE

=

HIGH AVAILABILITY

REPLICATION

=

SYNCHRONOUS

STANDBY USED FOR NORMAL READ TRAFFIC

=

NO

FAILOVER

=

AUTOMATIC

### Memory Trick

READ REPLICA

=

PERFORMANCE

MULTI-AZ

=

AVAILABILITY

---

## Asynchronous vs Synchronous

### Read Replica

PRIMARY

↓

ASYNCHRONOUS

↓

READ REPLICA

Think:

POSSIBLE LAG

---

### Multi-AZ

PRIMARY

↓

SYNCHRONOUS

↓

STANDBY

Think:

FAILOVER COPY

### Memory Trick

READ REPLICA

=

ASYNC

MULTI-AZ

=

SYNC

---

## Read Replica Is Not a Standby

Do not confuse:

READ REPLICA

with:

MULTI-AZ STANDBY

### Read Replica

USED FOR:

READ TRAFFIC

### Multi-AZ Standby

USED FOR:

FAILOVER

Think:

READ REPLICA

=

WORKING DATABASE FOR READS

STANDBY

=

BACKUP DATABASE WAITING FOR FAILURE

---

## Multi-AZ Is Not Read Scaling

A common exam trap is:

DATABASE NEEDS MORE READ CAPACITY

and an answer suggests:

MULTI-AZ

That is usually incorrect.

Multi-AZ primarily provides:

HIGH AVAILABILITY

not:

READ SCALING

Think:

READ BOTTLENECK

↓

READ REPLICA

PRIMARY FAILURE

↓

MULTI-AZ

---

## Read Replica Can Become Multi-AZ

A Read Replica can itself be configured as:

MULTI-AZ

Think:

PRIMARY DATABASE

↓

READ REPLICA

↓

MULTI-AZ READ REPLICA DEPLOYMENT

This can combine:

READ SCALABILITY

with:

HIGH AVAILABILITY

for the replica.

### Exam Thinking

These features are:

NOT MUTUALLY EXCLUSIVE

You can combine them when the architecture requires both.

---

## Read Scaling Architecture

Imagine:

USERS

↓

APPLICATION SERVERS

↓

WRITE REQUESTS

↓

PRIMARY RDS

and:

APPLICATION SERVERS

↓

READ REQUESTS

↓

READ REPLICA #1

READ REPLICA #2

READ REPLICA #3

Think:

ONE WRITER

↓

MULTIPLE READERS

### Memory Trick

RDS READ SCALING

=

ONE PRIMARY + MANY READERS

---

## Read Replica + Auto Scaling Application

A common scalable architecture is:

USERS

↓

[Application Load Balancer](<Application Load Balancer>)

↓

[Auto Scaling Groups](<Auto Scaling Groups>)

↓

EC2 APPLICATION INSTANCES

↓

WRITES

↓

PRIMARY RDS

and:

EC2 APPLICATION INSTANCES

↓

READS

↓

RDS READ REPLICAS

Think:

APP TIER

=

HORIZONTAL SCALE

DATABASE READ TIER

=

READ REPLICAS

---

## Scenario Recognition

Primary RDS database has too many read requests?

→ RDS Read Replica

---

Need to scale database reads?

→ RDS Read Replica

---

Need reporting queries without overloading production database?

→ RDS Read Replica

---

Need analytics queries separated from production database?

→ RDS Read Replica

---

Need a read-only database copy?

→ RDS Read Replica

---

Need asynchronous database replication?

→ RDS Read Replica

---

Question mentions replication lag?

→ RDS Read Replica

---

Need a database copy in another Region for local reads?

→ Cross-Region Read Replica

---

Need to promote a replica into an independent database?

→ Promote Read Replica

---

Need automatic failover when primary database fails?

→ RDS Multi-AZ

---

Need synchronous replication for high availability?

→ RDS Multi-AZ

---

Need more write capacity?

→ Read Replica is NOT the primary solution

---

Need immediately consistent reads after writes?

→ Be careful with Read Replicas because replication is asynchronous

---

## Exam Traps

READ REPLICA

=

READ SCALABILITY

---

READ REPLICA

=

ASYNC REPLICATION

---

ASYNC

=

POSSIBLE REPLICATION LAG

---

PRIMARY

=

READ + WRITE

READ REPLICA

=

READ

---

READ REPLICA

=

OWN ENDPOINT

---

APPLICATION

=

MUST SEND READS TO REPLICA

---

READ REPLICA

≠

AUTOMATIC LOAD BALANCING

---

READ REPLICA

=

CAN BE CROSS-AZ

---

READ REPLICA

=

CAN BE CROSS-REGION

---

READ REPLICA

=

CAN BE PROMOTED

---

PROMOTED REPLICA

=

STANDALONE DATABASE

---

READ REPLICA

≠

MULTI-AZ STANDBY

---

READ REPLICA

=

PERFORMANCE

MULTI-AZ

=

HIGH AVAILABILITY

---

READ REPLICA

=

ASYNC

MULTI-AZ

=

SYNC

---

MULTI-AZ STANDBY

=

NOT FOR NORMAL READ SCALING

---

## Quick Cheat Sheet

RDS READ REPLICA

=

READ SCALING

REPLICATION

=

ASYNCHRONOUS

REPLICATION LAG

=

POSSIBLE

PRIMARY

=

READ + WRITE

REPLICA

=

READ

READ REPLICA ENDPOINT

=

SEPARATE ENDPOINT

APPLICATION

=

MUST DIRECT READS

SAME AZ

=

SUPPORTED

CROSS-AZ

=

SUPPORTED

CROSS-REGION

=

SUPPORTED

PROMOTION

=

STANDALONE DATABASE

REPORTING

=

READ REPLICA

ANALYTICS READS

=

READ REPLICA

READ REPLICA

=

PERFORMANCE

MULTI-AZ

=

HIGH AVAILABILITY

READ REPLICA

=

ASYNC

MULTI-AZ

=

SYNC

---

## Master Memory Trick

PRIMARY RDS

↓

WRITES

↓

PRIMARY

READS

↓

READ REPLICAS

Think:

WRITE HERE

↓

PRIMARY

READ HERE

↓

REPLICA

And remember:

READ REPLICA

=

SCALE READS

↓

ASYNC

↓

POSSIBLE LAG

MULTI-AZ

=

SURVIVE FAILURE

↓

SYNC

↓

AUTOMATIC FAILOVER

### Final Rule

QUESTION SAYS:

TOO MANY READS

↓

READ REPLICA

QUESTION SAYS:

DATABASE FAILURE

↓

MULTI-AZ

---

## Related Notes

- [RDS Overview](<RDS Overview>)
- [RDS Storage Auto Scaling](<RDS Storage Auto Scaling>)
- [RDS Multi-AZ](<RDS Multi-AZ>)
- [RDS Backups](<RDS Backups>)
- [Aurora](04-Databases/Aurora.md)
- [RDS Proxy](<RDS Proxy>)
- [Application Load Balancer](<Application Load Balancer>)
- [Auto Scaling Groups](<Auto Scaling Groups>)
- [EC2](EC2)
- [SAA Databases Cheat Sheet](<SAA Databases Cheat Sheet>)
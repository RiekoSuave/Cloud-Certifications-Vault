## What Problem Does It Solve?

A single-region Aurora database can serve users well inside:

ONE AWS REGION

But global applications may need:

LOW-LATENCY READS

↓

IN MULTIPLE REGIONS

and:

DISASTER RECOVERY

↓

IF THE PRIMARY REGION FAILS

Aurora Global solves this by replicating Aurora data across:

MULTIPLE AWS REGIONS

Think:

PRIMARY REGION

↓

REPLICATION

↓

SECONDARY REGIONS

### Memory Trick

AURORA GLOBAL

=

GLOBAL READS + REGIONAL DR

---

## What Is Aurora Global?

Aurora Global allows an Aurora database to span:

MULTIPLE AWS REGIONS

Think:

REGION A

↓

PRIMARY AURORA

↓

GLOBAL REPLICATION

↓

REGION B

↓

SECONDARY AURORA

↓

REGION C

↓

SECONDARY AURORA

The primary Region handles:

READ + WRITE

Secondary Regions are:

READ-ONLY

during normal operation.

### Memory Trick

PRIMARY

=

READ + WRITE

SECONDARY

=

READ ONLY

---

## Primary Region

Aurora Global has:

ONE PRIMARY REGION

The primary Region handles:

READS

and:

WRITES

Think:

APPLICATION

↓

PRIMARY REGION

↓

WRITE REQUEST

↓

AURORA

### Memory Trick

ONE PRIMARY

=

WRITE REGION

---

## Secondary Regions

Aurora Global supports:

UP TO 10 SECONDARY REGIONS

Secondary Regions are:

READ-ONLY

during normal operation.

Think:

PRIMARY REGION

↓

REPLICATION

↓

SECONDARY REGION #1

↓

SECONDARY REGION #2

↓

SECONDARY REGION #3

...

UP TO 10

### Memory Trick

SECONDARY

=

READ REGION

---

## Global Architecture

Imagine:

US-EAST-1

↓

PRIMARY REGION

↓

READ + WRITE

Then:

EU-WEST-1

↓

SECONDARY REGION

↓

READ ONLY

and:

AP-SOUTHEAST-2

↓

SECONDARY REGION

↓

READ ONLY

Think:

ONE GLOBAL DATABASE

↓

MULTIPLE REGIONAL READ LOCATIONS

---

## Cross-Region Replication

Aurora Global replicates data from:

PRIMARY REGION

to:

SECONDARY REGIONS

Your course highlights typical cross-region replication of:

LESS THAN 1 SECOND

Think:

WRITE IN PRIMARY

↓

< 1 SECOND

↓

AVAILABLE IN SECONDARY

### Memory Trick

AURORA GLOBAL REPLICATION

=

SUB-1 SECOND

---

## Replication Lag

Aurora Global is designed for:

VERY LOW CROSS-REGION REPLICATION LAG

The slide emphasizes:

LESS THAN 1 SECOND

Think:

PRIMARY WRITE

↓

SHORT DELAY

↓

SECONDARY READ COPY

### Exam Thinking

Question says:

GLOBAL RELATIONAL DATABASE

+

CROSS-REGION REPLICATION UNDER 1 SECOND

↓

AURORA GLOBAL

---

## Global Read Latency

Secondary Regions allow applications to perform:

READS LOCALLY

Think:

EUROPEAN USER

↓

EUROPE REGION

↓

LOCAL AURORA READ

instead of:

EUROPEAN USER

↓

US REGION

↓

LONGER NETWORK LATENCY

This helps:

DECREASE READ LATENCY

for global users.

### Memory Trick

LOCAL REGION READ

=

LOWER LATENCY

---

## Read Replicas in Secondary Regions

Each secondary Region can support:

UP TO 16 READ REPLICAS

Think:

SECONDARY REGION

↓

READ REPLICA #1

READ REPLICA #2

READ REPLICA #3

...

UP TO 16

This provides significant:

REGIONAL READ SCALABILITY

### Memory Trick

SECONDARY REGION

=

UP TO 16 READERS

---

## Global Read Scaling

Imagine:

PRIMARY REGION

↓

WRITER

Then:

SECONDARY REGION A

↓

16 READ REPLICAS

SECONDARY REGION B

↓

16 READ REPLICAS

SECONDARY REGION C

↓

16 READ REPLICAS

Think:

CENTRALIZED WRITES

↓

DISTRIBUTED GLOBAL READS

### Memory Trick

WRITE CENTRAL

READ GLOBAL

---

## Disaster Recovery

Aurora Global can also support:

CROSS-REGION DISASTER RECOVERY

Think:

PRIMARY REGION FAILS

↓

PROMOTE SECONDARY REGION

↓

NEW PRIMARY REGION

This provides a recovery option when an entire AWS Region experiences problems.

### Memory Trick

REGION FAILURE

=

PROMOTE SECONDARY

---

## Regional Promotion

A secondary Region can be:

PROMOTED

to become the:

NEW PRIMARY REGION

Think:

PRIMARY REGION

↓

FAILURE

↓

SECONDARY REGION

↓

PROMOTE

↓

NEW READ / WRITE REGION

### Memory Trick

PROMOTE SECONDARY

=

NEW PRIMARY

---

## Aurora Global RTO

Your SAA course highlights a disaster recovery:

RTO

of:

LESS THAN 1 MINUTE

when promoting another Region.

Think:

REGION FAILURE

↓

PROMOTE SECONDARY

↓

< 1 MINUTE

↓

NEW PRIMARY

### Memory Trick

GLOBAL AURORA DR

=

RTO < 1 MINUTE

---

## What Is RTO?

RTO stands for:

RECOVERY TIME OBJECTIVE

RTO measures:

HOW LONG THE SYSTEM CAN BE DOWN

Think:

DISASTER

↓

DOWNTIME

↓

SYSTEM RECOVERED

That time is:

RTO

### Memory Trick

RTO

=

HOW FAST DO WE RECOVER?

---

## Global Database Architecture Thinking

Normal operation:

APPLICATIONS

↓

PRIMARY REGION

↓

READ / WRITE

Data replicates:

PRIMARY

↓

< 1 SECOND

↓

SECONDARY REGIONS

Then global users can perform:

READS

↓

NEAREST SECONDARY REGION

Think:

WRITE ONCE

↓

REPLICATE GLOBALLY

↓

READ LOCALLY

---

## Primary Region Failure

Normal:

REGION A

=

PRIMARY

REGION B

=

SECONDARY

REGION C

=

SECONDARY

Then:

REGION A FAILS

↓

PROMOTE REGION B

↓

REGION B BECOMES PRIMARY

↓

READ + WRITE

Think:

PRIMARY LOST

↓

SECONDARY PROMOTED

↓

GLOBAL DATABASE RECOVERS

---

## Aurora Global vs Cross-Region Read Replica

Your course distinguishes:

AURORA CROSS-REGION READ REPLICAS

and:

AURORA GLOBAL DATABASE

### Cross-Region Read Replica

Useful for:

DISASTER RECOVERY

and relatively:

SIMPLE TO SET UP

---

### Aurora Global

RECOMMENDED

for global Aurora architectures.

Provides:

1 PRIMARY REGION

↓

UP TO 10 SECONDARY REGIONS

↓

LOW-LATENCY GLOBAL READS

↓

FAST CROSS-REGION REPLICATION

↓

REGIONAL DR

### Memory Trick

CROSS-REGION REPLICA

=

SIMPLE

AURORA GLOBAL

=

GLOBAL ARCHITECTURE

---

## Aurora Global vs Aurora Multi-AZ

Do not confuse:

MULTI-AZ

with:

MULTI-REGION

### Aurora Multi-AZ Architecture

Protects against:

AZ FAILURE

within:

ONE REGION

Think:

AZ-A

AZ-B

AZ-C

↓

ONE REGION

---

### Aurora Global

Protects against:

REGIONAL FAILURE

and provides:

GLOBAL READS

Think:

REGION A

REGION B

REGION C

### Memory Trick

MULTI-AZ

=

REGION SURVIVES AZ FAILURE

GLOBAL

=

WORLDWIDE REGIONS

---

## Aurora Global vs RDS Multi-AZ

### RDS Multi-AZ

PRIMARY

↓

STANDBY

↓

DIFFERENT AZ

Purpose:

HIGH AVAILABILITY WITHIN REGION

---

### Aurora Global

PRIMARY REGION

↓

SECONDARY REGIONS

Purpose:

GLOBAL READS

+

REGIONAL DISASTER RECOVERY

Think:

AZ FAILURE

↓

MULTI-AZ

REGION FAILURE

↓

AURORA GLOBAL

---

## Aurora Global vs Aurora Read Replicas

### Aurora Read Replicas

Scale reads within an Aurora architecture.

Think:

MORE DATABASE READERS

---

### Aurora Global

Extends Aurora across:

MULTIPLE REGIONS

Think:

READS AROUND THE WORLD

### Memory Trick

REPLICA

=

READ SCALE

GLOBAL

=

REGIONAL READ SCALE + DR

---

## Aurora Global and Latency

Suppose users are located in:

UNITED STATES

↓

EUROPE

↓

ASIA

If all reads go to:

ONE US REGION

users in Europe and Asia may experience:

HIGHER LATENCY

With Aurora Global:

US USERS

↓

US REGION

EU USERS

↓

EU REGION

ASIA USERS

↓

ASIA REGION

Think:

READ LOCAL

↓

REDUCE LATENCY

---

## Aurora Global and Writes

A key exam distinction:

SECONDARY REGIONS

are:

READ-ONLY

during normal operation.

Think:

WRITE REQUEST

↓

PRIMARY REGION

NOT:

WRITE REQUEST

↓

SECONDARY REGION

### Memory Trick

GLOBAL AURORA

=

ONE WRITE REGION

---

## Aurora Global Is Not Multi-Writer

Do not assume:

MULTIPLE REGIONS

means:

MULTIPLE WRITE REGIONS

Aurora Global normally has:

ONE PRIMARY READ / WRITE REGION

and:

SECONDARY READ-ONLY REGIONS

Think:

GLOBAL

≠

ACTIVE-ACTIVE WRITES EVERYWHERE

### Exam Trap

WRITE IN EVERY REGION?

↓

NOT THE NORMAL AURORA GLOBAL MODEL

---

## Global Application Architecture

Imagine:

US USERS

↓

US APPLICATION

↓

PRIMARY AURORA

↓

READ + WRITE

European users:

EU USERS

↓

EU APPLICATION

↓

SECONDARY AURORA

↓

READ ONLY

Asian users:

ASIA USERS

↓

ASIA APPLICATION

↓

SECONDARY AURORA

↓

READ ONLY

All data originates from:

PRIMARY WRITES

and replicates:

GLOBALLY

---

## Global DR Architecture

Normal:

PRIMARY REGION

↓

READ / WRITE

↓

SECONDARY REGION

↓

READ ONLY

Disaster:

PRIMARY REGION FAILS

↓

PROMOTE SECONDARY

↓

NEW PRIMARY

↓

READ / WRITE

This allows the application to recover from:

REGIONAL FAILURE

### Memory Trick

GLOBAL DATABASE

=

READ NEAR USERS

+

FAIL OVER ACROSS REGIONS

---

## Scenario Recognition

Need Aurora across multiple AWS Regions?

→ Aurora Global

---

Need low-latency relational database reads for global users?

→ Aurora Global

---

Need one primary read/write Region with multiple read-only Regions?

→ Aurora Global

---

Need cross-region Aurora replication under 1 second?

→ Aurora Global

---

Need up to 10 secondary Regions?

→ Aurora Global

---

Need up to 16 Read Replicas per secondary Region?

→ Aurora Global

---

Need disaster recovery from a full Region outage?

→ Aurora Global

---

Need to promote another Region with RTO under 1 minute?

→ Aurora Global

---

Need high availability across Availability Zones inside one Region?

→ Aurora / Multi-AZ architecture

NOT necessarily Aurora Global

---

Need simple cross-region Aurora Read Replica?

→ Aurora Cross-Region Read Replica

---

Need writes in secondary Regions during normal operation?

→ Not the normal Aurora Global architecture

---

## Exam Traps

AURORA GLOBAL

=

MULTI-REGION

---

PRIMARY REGION

=

READ + WRITE

---

SECONDARY REGION

=

READ ONLY

---

PRIMARY REGIONS

=

ONE

---

SECONDARY REGIONS

=

UP TO 10

---

REPLICATION LAG

=

LESS THAN 1 SECOND

---

READ REPLICAS PER SECONDARY REGION

=

UP TO 16

---

AURORA GLOBAL

=

LOWER GLOBAL READ LATENCY

---

AURORA GLOBAL

=

REGIONAL DISASTER RECOVERY

---

PROMOTION RTO

=

LESS THAN 1 MINUTE

---

MULTI-AZ

≠

MULTI-REGION

---

MULTI-AZ

=

AZ FAILURE PROTECTION

AURORA GLOBAL

=

REGIONAL FAILURE PROTECTION + GLOBAL READS

---

SECONDARY REGIONS

≠

NORMAL WRITE REGIONS

---

AURORA GLOBAL

≠

MULTI-WRITER ACROSS ALL REGIONS

---

## Quick Cheat Sheet

AURORA GLOBAL

=

GLOBAL AURORA DATABASE

PRIMARY REGION

=

1

PRIMARY ACCESS

=

READ + WRITE

SECONDARY REGIONS

=

UP TO 10

SECONDARY ACCESS

=

READ ONLY

REPLICATION

=

CROSS-REGION

TYPICAL REPLICATION TIME

=

LESS THAN 1 SECOND

READ REPLICAS PER SECONDARY REGION

=

UP TO 16

GLOBAL BENEFIT

=

LOWER READ LATENCY

DR BENEFIT

=

REGIONAL FAILOVER

PROMOTION RTO

=

LESS THAN 1 MINUTE

MULTI-AZ

=

AZ RESILIENCY

AURORA GLOBAL

=

REGIONAL RESILIENCY

---

## Master Memory Trick

AURORA GLOBAL

=

ONE WRITE REGION

↓

MANY READ REGIONS

Think:

PRIMARY

=

READ + WRITE

SECONDARY

=

READ ONLY

Replication:

↓

< 1 SECOND

Disaster:

↓

PROMOTE SECONDARY

↓

RTO < 1 MINUTE

Remember:

1

=

PRIMARY REGION

10

=

SECONDARY REGIONS

16

=

READ REPLICAS PER SECONDARY REGION

< 1 SECOND

=

REPLICATION

< 1 MINUTE

=

DR PROMOTION RTO

### Final Rule

QUESTION SAYS:

GLOBAL SQL READS

+

LOW LATENCY

+

CROSS-REGION DR

↓

AURORA GLOBAL

QUESTION SAYS:

AZ FAILURE ONLY

↓

MULTI-AZ

QUESTION SAYS:

STANDARD READ SCALING

↓

READ REPLICAS

---

## Related Notes

- [Aurora](Aurora)
- [Aurora Endpoints](<Aurora Endpoints>)
- [Aurora Auto Scaling](<Aurora Auto Scaling>)
- [Aurora Serverless](<Aurora Serverless>)
- [Aurora Database Cloning](<Aurora Database Cloning>)
- [RDS Overview](<RDS Overview>)
- [RDS Read Replicas](<RDS Read Replicas>)
- [RDS Multi-AZ](<RDS Multi-AZ>)
- [Route 53](<05-Networking/Route 53.md>)
- [SAA Databases Cheat Sheet](<SAA Databases Cheat Sheet>)
## What Problem Does It Solve?

Read traffic on an Aurora database can:

INCREASE

and:

DECREASE

over time.

If there are too few Aurora Read Replicas:

READ TRAFFIC ↑

↓

REPLICAS OVERLOADED

↓

READ PERFORMANCE SUFFERS

If there are too many replicas:

LOW READ TRAFFIC

↓

EXTRA DATABASE CAPACITY

↓

WASTED COST

Aurora Auto Scaling can automatically:

ADD

or:

REMOVE

Aurora Read Replicas based on demand.

### Memory Trick

AURORA AUTO SCALING

=

AUTO SCALE READERS

---

## What Is Aurora Auto Scaling?

Aurora Auto Scaling dynamically adjusts:

THE NUMBER OF AURORA READ REPLICAS

Think:

READ LOAD ↑

↓

ADD REPLICAS

READ LOAD ↓

↓

REMOVE REPLICAS

This allows Aurora to:

MATCH READ CAPACITY TO DEMAND

### Memory Trick

AURORA AUTO SCALING

=

READERS GROW + SHRINK

---

## What Does Aurora Auto Scaling Scale?

Aurora Auto Scaling primarily scales:

READ REPLICAS

Think:

AURORA CLUSTER

↓

WRITER

+

READERS

Auto Scaling adjusts:

READERS

not:

THE WRITER

### Memory Trick

AURORA AUTO SCALING

=

READER SCALING

---

## Writer vs Reader Scaling

### Writer

Handles:

WRITE TRAFFIC

Think:

INSERT

UPDATE

DELETE

↓

WRITER

---

### Read Replicas

Handle:

READ TRAFFIC

Think:

SELECT

↓

READERS

Aurora Auto Scaling changes:

THE NUMBER OF READERS

### Memory Trick

WRITER

=

WRITE

AUTO SCALING

=

READERS

---

## Basic Architecture

Imagine:

AURORA CLUSTER

↓

WRITER

+

READER #1

READER #2

The application sends:

WRITES

↓

[Writer Endpoint](<Aurora Endpoints>)

and:

READS

↓

READER ENDPOINT

↓

READ REPLICAS

If read traffic increases:

READER CPU ↑

↓

AUTO SCALING

↓

ADD REPLICA

Think:

MORE READ DEMAND

↓

MORE READERS

---

## Reader Endpoint Integration

Aurora Auto Scaling works closely with the:

READER ENDPOINT

Think:

APPLICATION

↓

READER ENDPOINT

↓

READ REPLICAS

When replicas are added or removed:

APPLICATION

↓

STILL USES SAME READER ENDPOINT

The application does not need to manually track:

WHICH REPLICAS EXIST

### Memory Trick

READERS CHANGE

↓

READER ENDPOINT STAYS

---

## Reader Endpoint Connection Load Balancing

The Reader Endpoint provides:

CONNECTION LOAD BALANCING

across Aurora Read Replicas.

Think:

CLIENT

↓

READER ENDPOINT

↓

READER #1

READER #2

READER #3

When Auto Scaling adds another replica:

READER #4

the Reader Endpoint can include it in:

READ CONNECTION DISTRIBUTION

### Memory Trick

AUTO SCALING

=

ADD READERS

READER ENDPOINT

=

DISTRIBUTE CONNECTIONS

---

## High Read Demand

Imagine:

2 READ REPLICAS

Traffic increases sharply.

Think:

MANY READ REQUESTS

↓

CPU USAGE ↑

↓

READ REPLICAS BUSY

↓

AURORA AUTO SCALING

↓

ADD REPLICA

Now:

3 READ REPLICAS

↓

MORE READ CAPACITY

### Memory Trick

HIGH READ LOAD

=

SCALE OUT READERS

---

## Low Read Demand

Later:

READ TRAFFIC ↓

Think:

REPLICAS UNDERUTILIZED

↓

AURORA AUTO SCALING

↓

REMOVE UNNEEDED REPLICA

This helps reduce:

UNNECESSARY DATABASE COST

### Memory Trick

LOW READ LOAD

=

SCALE IN READERS

---

## Scaling Out

Scaling Out means:

ADD AURORA READ REPLICAS

Think:

2 READERS

↓

3 READERS

↓

4 READERS

This increases:

READ CAPACITY

### Memory Trick

SCALE OUT

=

MORE READERS

---

## Scaling In

Scaling In means:

REMOVE AURORA READ REPLICAS

Think:

4 READERS

↓

3 READERS

↓

2 READERS

This reduces:

EXCESS CAPACITY

### Memory Trick

SCALE IN

=

FEWER READERS

---

## CPU Usage and Auto Scaling

The SAA slides illustrate Auto Scaling reacting to:

CPU USAGE

on the Aurora Replicas.

Think:

READERS

↓

CPU ↑

↓

AUTO SCALING

↓

ADD REPLICA

Then:

LOAD DISTRIBUTED

↓

CPU PER READER ↓

### Memory Trick

READER CPU HIGH

=

ADD READER

---

## Many Requests

Another important clue is:

MANY READ REQUESTS

Think:

APPLICATION

↓

READER ENDPOINT

↓

MANY CONNECTIONS

↓

READ REPLICAS

As demand grows:

AURORA AUTO SCALING

↓

EXTENDS READ CAPACITY

The Reader Endpoint continues acting as:

THE READ ENTRY POINT

---

## Aurora Auto Scaling vs Aurora Storage Auto Scaling

Do not confuse:

READ REPLICA AUTO SCALING

with:

STORAGE AUTO EXPANSION

### Aurora Auto Scaling

Changes:

NUMBER OF READ REPLICAS

Think:

READ COMPUTE CAPACITY

---

### Aurora Storage Auto Expansion

Changes:

DATABASE STORAGE CAPACITY

Think:

MORE DATA STORED

↓

MORE STORAGE

### Memory Trick

AUTO SCALING

=

MORE READERS

STORAGE AUTO EXPANSION

=

MORE SPACE

---

## Aurora Auto Scaling vs EC2 Auto Scaling

Do not confuse:

[Aurora Auto Scaling](<Aurora Auto Scaling>)

with:

[Auto Scaling Groups](<Auto Scaling Groups>)

### EC2 Auto Scaling Group

Scales:

EC2 INSTANCES

Think:

APPLICATION SERVERS

---

### Aurora Auto Scaling

Scales:

AURORA READ REPLICAS

Think:

DATABASE READERS

### Memory Trick

ASG

=

APP SERVERS

AURORA AUTO SCALING

=

DB READERS

---

## Aurora Auto Scaling vs RDS Read Replicas

### Standard RDS Read Replicas

You create Read Replicas to:

SCALE READ TRAFFIC

Think:

PRIMARY RDS

↓

READ REPLICAS

---

### Aurora Auto Scaling

Aurora can automatically:

ADJUST NUMBER OF READ REPLICAS

Think:

READ DEMAND

↓

AUTO ADD / REMOVE READERS

### Memory Trick

RDS READ REPLICA

=

READ SCALING

AURORA AUTO SCALING

=

AUTOMATIC READ SCALING

---

## Aurora Auto Scaling Does Not Scale Writes

A common exam trap is assuming:

MORE AURORA REPLICAS

means:

MORE WRITE CAPACITY

But:

WRITES

still go through:

THE WRITER

Think:

READERS

=

READS

NOT:

WRITES

### Memory Trick

MORE READERS

≠

MORE WRITERS

---

## Writer Endpoint Is Separate

Application writes continue through:

WRITER ENDPOINT

Think:

APPLICATION

↓

WRITE REQUEST

↓

WRITER ENDPOINT

↓

WRITER

Aurora Auto Scaling does not change:

THE WRITE PATH

---

## Reader Endpoint Is Key

Application reads should use:

READER ENDPOINT

Think:

APPLICATION

↓

SELECT QUERY

↓

READER ENDPOINT

↓

AUTO-SCALED READ REPLICAS

This allows the backend replica count to change without requiring:

APPLICATION CONNECTION CHANGES

### Memory Trick

AUTO-SCALED READERS

↓

ONE READER ENDPOINT

---

## Architecture Thinking

Imagine an e-commerce application.

Normal traffic:

WRITER

+

2 READ REPLICAS

Then a sale begins:

READ REQUESTS ↑

↓

READER CPU ↑

↓

AURORA AUTO SCALING

↓

ADD READ REPLICAS

↓

READER ENDPOINT DISTRIBUTES CONNECTIONS

↓

READ PERFORMANCE STABILIZES

After the sale:

READ REQUESTS ↓

↓

AUTO SCALING

↓

REMOVE EXTRA READERS

Think:

DEMAND

↓

READERS

↓

CAPACITY MATCHES LOAD

---

## Aurora Auto Scaling + High Availability

Aurora already provides:

HIGH AVAILABILITY

through its distributed architecture.

Auto Scaling adds:

READ CAPACITY FLEXIBILITY

Think:

AURORA HA

=

SURVIVE FAILURES

AURORA AUTO SCALING

=

HANDLE CHANGING READ LOAD

### Memory Trick

HA

=

SURVIVE

AUTO SCALING

=

GROW / SHRINK

---

## Aurora Auto Scaling + Shared Storage

Aurora Read Replicas use:

SHARED AURORA STORAGE

Think:

WRITER

↓

SHARED STORAGE

↑

READERS

Because replicas use the same distributed storage architecture:

AUTO SCALING

can focus on adding:

DATABASE COMPUTE INSTANCES

for reads.

### Memory Trick

SHARED STORAGE

+

MORE READERS

=

AURORA READ SCALE

---

## Scenario Recognition

Need Aurora to automatically add Read Replicas?

→ Aurora Auto Scaling

---

Need Aurora to automatically remove Read Replicas when demand falls?

→ Aurora Auto Scaling

---

Need read capacity to match changing traffic?

→ Aurora Auto Scaling

---

Need to scale database reads based on high CPU usage?

→ Aurora Auto Scaling

---

Need to handle many read requests without manually creating replicas?

→ Aurora Auto Scaling

---

Need one endpoint while the number of readers changes?

→ Reader Endpoint

---

Need connection load balancing across Auto-Scaled Aurora Replicas?

→ Reader Endpoint

---

Need more Aurora write capacity?

→ Aurora Auto Scaling is NOT scaling the writer

---

Need more database storage?

→ Aurora Storage Auto Expansion

NOT Aurora Replica Auto Scaling

---

Need EC2 application servers automatically added?

→ Auto Scaling Group

NOT Aurora Auto Scaling

---

## Exam Traps

AURORA AUTO SCALING

=

READ REPLICAS

---

AURORA AUTO SCALING

≠

WRITER SCALING

---

AURORA AUTO SCALING

=

READ CAPACITY

---

READER ENDPOINT

=

CONNECTION LOAD BALANCING

---

AUTO SCALING ADDS READER

↓

READER ENDPOINT CAN USE IT

---

APPLICATION

=

KEEPS SAME READER ENDPOINT

---

HIGH READER CPU

=

POSSIBLE SCALE OUT SIGNAL

---

MANY READ REQUESTS

=

MORE READ CAPACITY NEEDED

---

AURORA AUTO SCALING

≠

STORAGE AUTO EXPANSION

---

READ REPLICA SCALING

=

COMPUTE

STORAGE EXPANSION

=

DATA CAPACITY

---

AURORA AUTO SCALING

≠

EC2 AUTO SCALING GROUP

---

MORE READ REPLICAS

≠

MORE WRITE CAPACITY

---

## Quick Cheat Sheet

AURORA AUTO SCALING

=

AUTO SCALE READ REPLICAS

SCALE OUT

=

ADD READERS

SCALE IN

=

REMOVE READERS

MAIN PURPOSE

=

READ SCALABILITY

WRITER

=

NOT AUTO-SCALED BY THIS FEATURE

READ TRAFFIC

=

READER ENDPOINT

WRITES

=

WRITER ENDPOINT

READER ENDPOINT

=

CONNECTION LOAD BALANCING

HIGH READ CPU

=

SCALE OUT CLUE

MANY READ REQUESTS

=

SCALE OUT CLUE

LOW READ DEMAND

=

SCALE IN

STORAGE AUTO EXPANSION

=

MORE STORAGE

AURORA AUTO SCALING

=

MORE / FEWER READERS

EC2 ASG

=

APPLICATION SERVER SCALING

---

## Master Memory Trick

APPLICATION

↓

READS

↓

READER ENDPOINT

↓

AURORA READERS

Then:

READ LOAD ↑

↓

CPU ↑

↓

ADD READERS

READ LOAD ↓

↓

REMOVE READERS

Think:

READER ENDPOINT

=

FRONT DOOR

AUTO SCALING

=

CHANGE NUMBER OF READERS

And remember:

WRITER

=

WRITE PATH

READERS

=

READ PATH

AUTO SCALING

=

READ PATH ONLY

### Final Rule

QUESTION SAYS:

MORE READ DEMAND?

↓

AURORA AUTO SCALING

QUESTION SAYS:

MORE DATA STORAGE?

↓

AURORA STORAGE AUTO EXPANSION

QUESTION SAYS:

MORE APPLICATION SERVERS?

↓

EC2 AUTO SCALING GROUP

---

## Related Notes

- [Aurora](Aurora)
- [Aurora Endpoints](<Aurora Endpoints>)
- [Aurora Serverless](<Aurora Serverless>)
- [Aurora Global](<Aurora Global>)
- [Aurora Database Cloning](<Aurora Database Cloning>)
- [RDS Overview](<RDS Overview>)
- [RDS Read Replicas](<RDS Read Replicas>)
- [Auto Scaling Groups](<Auto Scaling Groups>)
- [CloudWatch](07-Monitoring/CloudWatch.md)
- [SAA Databases Cheat Sheet](<SAA Databases Cheat Sheet>)
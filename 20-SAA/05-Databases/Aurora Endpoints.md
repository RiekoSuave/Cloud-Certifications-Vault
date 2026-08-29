## What Problem Does It Solve?

An Aurora cluster can contain:

ONE WRITER

and:

MULTIPLE READ REPLICAS

The application needs an easy way to know:

WHERE SHOULD WRITES GO?

and:

WHERE SHOULD READS GO?

Aurora Endpoints provide:

DIFFERENT DATABASE CONNECTION ADDRESSES

for different workloads.

Think:

APPLICATION

↓

WRITE TRAFFIC?

↓

WRITER ENDPOINT

READ TRAFFIC?

↓

READER ENDPOINT

### Memory Trick

AURORA ENDPOINTS

=

WRITE HERE / READ HERE

---

## What Is an Aurora Endpoint?

An Aurora Endpoint is:

A DATABASE CONNECTION ADDRESS

that applications use to connect to an:

AURORA CLUSTER

Instead of connecting directly to a specific database instance:

APPLICATION

↓

AURORA ENDPOINT

↓

CORRECT DATABASE INSTANCE

Think:

ENDPOINT

=

SMART DATABASE ENTRY POINT

### Memory Trick

ENDPOINT

=

HOW APP CONNECTS TO AURORA

---

## Main Aurora Endpoints

The two most important endpoints for the SAA exam are:

WRITER ENDPOINT

and:

READER ENDPOINT

Think:

WRITE

↓

WRITER ENDPOINT

READ

↓

READER ENDPOINT

### Memory Trick

WRITER

=

WRITE

READER

=

READ

---

## Writer Endpoint

The:

WRITER ENDPOINT

points to:

THE CURRENT WRITER INSTANCE

Think:

APPLICATION

↓

WRITER ENDPOINT

↓

AURORA WRITER

↓

SHARED STORAGE

The writer handles:

INSERTS

↓

UPDATES

↓

DELETES

and other:

WRITE OPERATIONS

### Memory Trick

WRITER ENDPOINT

=

POINTS TO WRITER

---

## Aurora Has One Writer

An Aurora cluster normally has:

ONE WRITER INSTANCE

Think:

AURORA CLUSTER

↓

WRITER

+

READ REPLICAS

All application writes should be directed through:

WRITER ENDPOINT

### Memory Trick

ONE WRITER

=

ONE WRITE DESTINATION

---

## Writer Endpoint Architecture

Think:

APPLICATION

↓

WRITER ENDPOINT

↓

WRITER INSTANCE

↓

SHARED AURORA STORAGE

Example:

CREATE ORDER

↓

WRITER ENDPOINT

↓

WRITER

↓

DATABASE UPDATED

### Memory Trick

CHANGING DATA?

↓

WRITER ENDPOINT

---

## Writer Endpoint and Failover

Suppose the current writer fails.

Normal:

WRITER ENDPOINT

↓

WRITER #1

Then:

WRITER #1 FAILS

↓

AURORA PROMOTES REPLICA

↓

REPLICA BECOMES WRITER #2

The:

WRITER ENDPOINT

now points to:

THE NEW WRITER

Think:

WRITER CHANGES

↓

ENDPOINT STAYS THE SAME

### Memory Trick

FAILOVER CHANGES WRITER

NOT APPLICATION ENDPOINT

---

## Why the Writer Endpoint Matters

Without the Writer Endpoint, your application would need to know:

WHICH DATABASE INSTANCE

is currently the writer.

That becomes difficult during:

FAILOVER

Instead:

APPLICATION

↓

WRITER ENDPOINT

↓

AURORA HANDLES CURRENT WRITER

### Memory Trick

APP KNOWS ENDPOINT

AURORA KNOWS WRITER

---

## Reader Endpoint

The:

READER ENDPOINT

is used for:

READ TRAFFIC

Think:

APPLICATION

↓

READER ENDPOINT

↓

AURORA READ REPLICAS

The Reader Endpoint helps:

DISTRIBUTE CONNECTIONS

across multiple Aurora Replicas.

### Memory Trick

READER ENDPOINT

=

READ LOAD BALANCER

---

## Reader Endpoint Connection Load Balancing

The SAA slides specifically describe the Reader Endpoint as providing:

CONNECTION LOAD BALANCING

Think:

APPLICATION

↓

READER ENDPOINT

↓

REPLICA #1

REPLICA #2

REPLICA #3

REPLICA #4

Instead of the application manually choosing:

WHICH REPLICA

to connect to.

### Memory Trick

READER ENDPOINT

=

BALANCE READ CONNECTIONS

---

## Reader Endpoint Architecture

Imagine:

AURORA CLUSTER

↓

WRITER

+

READER #1

READER #2

READER #3

Application reads:

APPLICATION

↓

READER ENDPOINT

↓

READ REPLICAS

Think:

SELECT QUERY

↓

READER ENDPOINT

↓

AVAILABLE READER

---

## Reader Endpoint Does Not Create Replicas

An important distinction:

READER ENDPOINT

does not:

CREATE READ REPLICAS

It only:

DISTRIBUTES CONNECTIONS

across existing replicas.

Think:

[Aurora](Aurora)

↓

CREATE REPLICAS

Then:

READER ENDPOINT

↓

DISTRIBUTE READ CONNECTIONS

### Exam Trap

READER ENDPOINT

≠

AUTO SCALING

---

## Reader Endpoint vs Writer Endpoint

### Writer Endpoint

PURPOSE

=

WRITE TRAFFIC

POINTS TO

=

CURRENT WRITER

Think:

INSERT

UPDATE

DELETE

↓

WRITER ENDPOINT

---

### Reader Endpoint

PURPOSE

=

READ TRAFFIC

POINTS TO

=

READ REPLICAS

Think:

SELECT

↓

READER ENDPOINT

### Memory Trick

WRITE

=

WRITER

READ

=

READER

---

## Endpoint Architecture

A common Aurora application looks like:

APPLICATION

↓

WRITE REQUESTS

↓

WRITER ENDPOINT

↓

WRITER

and:

APPLICATION

↓

READ REQUESTS

↓

READER ENDPOINT

↓

READ REPLICAS

All instances connect to:

SHARED AURORA STORAGE

### Memory Trick

ONE DATABASE CLUSTER

↓

TWO TRAFFIC PATHS

WRITE PATH

and:

READ PATH

---

## Reader Endpoint and Read Scaling

Aurora supports:

UP TO 15 READ REPLICAS

Think:

READER ENDPOINT

↓

REPLICA #1

REPLICA #2

REPLICA #3

...

UP TO 15

As more replicas are added:

READ CAPACITY

can increase.

The Reader Endpoint gives the application:

ONE CONNECTION ADDRESS

for those replicas.

### Memory Trick

MORE READERS

+

READER ENDPOINT

=

READ SCALING

---

## Reader Endpoint + Aurora Auto Scaling

Aurora Replicas can be:

AUTO SCALED

Think:

READ LOAD ↑

↓

ADD AURORA REPLICA

↓

READER ENDPOINT

↓

MORE READ CAPACITY

The application continues connecting to:

THE SAME READER ENDPOINT

even as the number of replicas changes.

### Memory Trick

READERS CHANGE

ENDPOINT STAYS

---

## Why Endpoints Simplify Applications

Without endpoints:

APPLICATION

↓

MUST TRACK DATABASE INSTANCES

With endpoints:

APPLICATION

↓

WRITER ENDPOINT

or:

READER ENDPOINT

↓

AURORA HANDLES INSTANCE SELECTION

Think:

DATABASE TOPOLOGY CHANGES

↓

APPLICATION CONNECTION LOGIC STAYS SIMPLE

### Memory Trick

ENDPOINTS

=

HIDE DATABASE TOPOLOGY

---

## Writer Endpoint During Failover

Imagine:

AZ-A

↓

WRITER

AZ-B

↓

READER

AZ-C

↓

READER

Application:

↓

WRITER ENDPOINT

↓

AZ-A WRITER

Then AZ-A fails:

WRITER LOST

↓

READER IN AZ-B PROMOTED

↓

WRITER ENDPOINT

↓

NOW POINTS TO AZ-B WRITER

The application continues using:

WRITER ENDPOINT

### Memory Trick

WRITER FAILS

↓

ENDPOINT FOLLOWS NEW WRITER

---

## Reader Endpoint During Scaling

Imagine:

2 READ REPLICAS

↓

READER ENDPOINT

Traffic increases:

READ LOAD ↑

↓

AURORA ADDS REPLICA

↓

3 READ REPLICAS

The application still uses:

THE SAME READER ENDPOINT

Think:

BACKEND CHANGES

↓

FRONT DOOR STAYS THE SAME

---

## Custom Endpoints

Aurora can also support:

CUSTOM ENDPOINTS

Custom Endpoints allow you to group:

SPECIFIC DATABASE INSTANCES

behind a specialized endpoint.

Think:

AURORA CLUSTER

↓

CUSTOM ENDPOINT

↓

SELECTED DATABASE INSTANCES

This can help when different workloads should use:

DIFFERENT GROUPS OF REPLICAS

### Memory Trick

CUSTOM ENDPOINT

=

CHOOSE WHICH INSTANCES

---

## Custom Endpoint Example

Imagine an Aurora cluster has:

SMALL READ REPLICAS

and:

LARGE READ REPLICAS

You may want:

NORMAL APPLICATION READS

↓

STANDARD READERS

and:

HEAVY ANALYTICS

↓

LARGE READERS

A custom endpoint can direct:

SPECIAL WORKLOAD

↓

SPECIFIC REPLICA GROUP

### Exam Thinking

Need to route a workload to:

A PARTICULAR SUBSET OF AURORA INSTANCES?

↓

CUSTOM ENDPOINT

---

## Endpoint Decision Tree

Need:

WRITE TRAFFIC?

↓

WRITER ENDPOINT

---

Need:

READ TRAFFIC ACROSS REPLICAS?

↓

READER ENDPOINT

---

Need:

CONNECTION LOAD BALANCING ACROSS READERS?

↓

READER ENDPOINT

---

Need:

CURRENT WRITER EVEN AFTER FAILOVER?

↓

WRITER ENDPOINT

---

Need:

SPECIFIC GROUP OF DATABASE INSTANCES?

↓

CUSTOM ENDPOINT

---

## Architecture Thinking

Imagine an e-commerce application.

USER PLACES ORDER

↓

APPLICATION

↓

WRITER ENDPOINT

↓

AURORA WRITER

Then:

USER VIEWS PRODUCTS

↓

APPLICATION

↓

READER ENDPOINT

↓

AURORA READ REPLICA

Think:

CHANGING DATABASE?

↓

WRITER

READING DATABASE?

↓

READER

This allows:

WRITE WORKLOAD

and:

READ WORKLOAD

to scale differently.

---

## Scenario Recognition

Need application writes sent to the current Aurora writer?

→ Writer Endpoint

---

Need one endpoint that always follows the Aurora writer after failover?

→ Writer Endpoint

---

Need reads distributed across Aurora Read Replicas?

→ Reader Endpoint

---

Need connection load balancing across Aurora replicas?

→ Reader Endpoint

---

Need a single DNS endpoint for multiple readers?

→ Reader Endpoint

---

Need to scale database reads while keeping the same application connection address?

→ Aurora Replicas + Reader Endpoint

---

Need Aurora Replica Auto Scaling without changing application connection strings?

→ Reader Endpoint

---

Need a specific subset of Aurora database instances?

→ Custom Endpoint

---

Need INSERT / UPDATE / DELETE?

→ Writer Endpoint

---

Need SELECT-heavy workload?

→ Reader Endpoint

---

## Exam Traps

WRITER ENDPOINT

=

CURRENT WRITER

---

WRITER ENDPOINT

=

WRITE TRAFFIC

---

READER ENDPOINT

=

READ TRAFFIC

---

READER ENDPOINT

=

CONNECTION LOAD BALANCING

---

READER ENDPOINT

≠

CREATE READ REPLICAS

---

READER ENDPOINT

≠

AUTO SCALING

---

AURORA REPLICAS

=

PROVIDE READ CAPACITY

READER ENDPOINT

=

DISTRIBUTES READ CONNECTIONS

---

WRITER FAILOVER

↓

WRITER ENDPOINT FOLLOWS NEW WRITER

---

APPLICATION

=

DOES NOT NEED TO TRACK CURRENT WRITER

---

CUSTOM ENDPOINT

=

SPECIFIC SUBSET OF INSTANCES

---

## Quick Cheat Sheet

WRITER ENDPOINT

=

WRITE CONNECTION

POINTS TO

=

CURRENT WRITER

WRITER FAILOVER

=

ENDPOINT FOLLOWS NEW WRITER

READER ENDPOINT

=

READ CONNECTION

READER ENDPOINT

=

CONNECTION LOAD BALANCING

READER TARGETS

=

AURORA READ REPLICAS

READ SCALING

=

ADD REPLICAS

READER ENDPOINT

=

SAME CONNECTION ADDRESS

CUSTOM ENDPOINT

=

SELECTED INSTANCE GROUP

INSERT / UPDATE / DELETE

=

WRITER

SELECT

=

READER

---

## Master Memory Trick

APPLICATION

↓

WHAT ARE YOU DOING?

CHANGING DATA?

↓

WRITER ENDPOINT

READING DATA?

↓

READER ENDPOINT

Think:

WRITER ENDPOINT

=

ONE WRITER

READER ENDPOINT

=

MANY READERS

And:

WRITER FAILS

↓

NEW WRITER

↓

SAME WRITER ENDPOINT

READERS SCALE

↓

MORE READERS

↓

SAME READER ENDPOINT

### Final Rule

WRITE

=

WRITER ENDPOINT

READ

=

READER ENDPOINT

SPECIAL REPLICA GROUP

=

CUSTOM ENDPOINT

---

## Related Notes

- [Aurora](Aurora)
- [Aurora Auto Scaling](<Aurora Auto Scaling>)
- [Aurora Serverless](<Aurora Serverless>)
- [Aurora Global](<Aurora Global>)
- [Aurora Database Cloning](<Aurora Database Cloning>)
- [RDS Overview](<RDS Overview>)
- [RDS Read Replicas](<RDS Read Replicas>)
- [RDS Multi-AZ](<RDS Multi-AZ>)
- [RDS Proxy](<RDS Proxy>)
- [SAA Databases Cheat Sheet](<SAA Databases Cheat Sheet>)
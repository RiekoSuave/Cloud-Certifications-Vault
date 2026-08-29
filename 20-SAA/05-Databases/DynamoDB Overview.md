## What Problem Does It Solve?

Traditional relational databases can become difficult to scale when an application needs:

MASSIVE TRAFFIC

↓

VERY LOW LATENCY

↓

FLEXIBLE SCHEMA

↓

SERVERLESS OPERATION

DynamoDB provides a:

FULLY MANAGED

↓

SERVERLESS

↓

NOSQL DATABASE

that can scale to extremely large workloads.

Think:

APPLICATION

↓

MILLIONS OF REQUESTS

↓

DYNAMODB

↓

LOW-LATENCY RESPONSE

### Memory Trick

DYNAMODB

=

SERVERLESS NOSQL AT MASSIVE SCALE

---

## What Is DynamoDB?

DynamoDB is an:

AWS PROPRIETARY

fully managed:

NOSQL DATABASE

Think:

RELATIONAL SQL?

↓

RDS / AURORA

NOSQL?

↓

DYNAMODB

DynamoDB is designed for:

HIGH SCALE

↓

LOW LATENCY

↓

MINIMAL MANAGEMENT

### Memory Trick

DYNAMODB

=

MANAGED NOSQL

---

## DynamoDB Is Not Relational

DynamoDB is:

NOT

a relational database.

Think:

RDS

=

RELATIONAL

↓

SQL

↓

JOINS

DYNAMODB

=

NOSQL

↓

KEY-VALUE / DOCUMENT DATA

### Memory Trick

DYNAMODB

≠

SQL DATABASE

---

## DynamoDB Is Serverless

DynamoDB is considered:

SERVERLESS

You do not manage:

DATABASE SERVERS

↓

OPERATING SYSTEMS

↓

DATABASE PATCHING

↓

DATABASE INSTANCES

Think:

APPLICATION

↓

DYNAMODB API

↓

AWS MANAGES INFRASTRUCTURE

### Memory Trick

DYNAMODB

=

NO DATABASE SERVERS TO MANAGE

---

## Fully Managed

AWS handles the underlying DynamoDB infrastructure.

You do not need to manage:

SERVERS

↓

PATCHES

↓

HARDWARE

↓

DATABASE SOFTWARE

Your course specifically highlights:

NO MAINTENANCE

and:

NO PATCHING

### Memory Trick

DYNAMODB

=

USE TABLES

AWS RUNS DATABASE

---

## Highly Available by Default

DynamoDB is:

HIGHLY AVAILABLE

with replication across:

MULTIPLE AVAILABILITY ZONES

Think:

AZ-A

↓

DATA

AZ-B

↓

DATA

AZ-C

↓

DATA

This is built into the service.

### Memory Trick

DYNAMODB

=

MULTI-AZ BY DEFAULT

---

## DynamoDB Availability Architecture

Think:

APPLICATION

↓

DYNAMODB

↓

MULTIPLE AZs

If one Availability Zone has a problem:

DYNAMODB

↓

CONTINUES OPERATING

This makes DynamoDB a strong option for:

HIGHLY AVAILABLE

serverless applications.

### Memory Trick

NO MULTI-AZ SETUP NEEDED

=

BUILT IN

---

## Massive Scale

DynamoDB is designed to scale to:

MASSIVE WORKLOADS

Your course highlights:

MILLIONS OF REQUESTS PER SECOND

↓

TRILLIONS OF ITEMS / ROWS

↓

HUNDREDS OF TB OF STORAGE

Think:

SMALL APP

↓

DYNAMODB

or:

GLOBAL MASSIVE APP

↓

DYNAMODB

### Memory Trick

DYNAMODB

=

SCALE VERY BIG

---

## Performance

DynamoDB provides:

FAST

and:

CONSISTENT PERFORMANCE

Your course highlights:

SINGLE-DIGIT MILLISECOND LATENCY

Think:

APPLICATION REQUEST

↓

DYNAMODB

↓

MILLISECONDS

### Memory Trick

DYNAMODB

=

SINGLE-DIGIT MS

---

## Performance at Scale

An important concept is that DynamoDB is designed to maintain:

CONSISTENT PERFORMANCE

even as:

DATA SIZE GROWS

and:

REQUEST VOLUME GROWS

Think:

1,000 ITEMS

↓

FAST

1 BILLION ITEMS

↓

DESIGNED TO REMAIN FAST

### Memory Trick

SCALE DATA

WITHOUT TRADITIONAL DB SLOWDOWN

---

## Tables

DynamoDB stores data inside:

TABLES

Think:

DYNAMODB

↓

TABLE

↓

ITEMS

↓

ATTRIBUTES

### Memory Trick

TABLE

=

CONTAINER FOR DYNAMODB DATA

---

## Items

An:

ITEM

is similar conceptually to a:

ROW

in a relational database.

Think:

TABLE

↓

ITEM #1

↓

ITEM #2

↓

ITEM #3

Each item represents:

ONE RECORD

### Memory Trick

DYNAMODB ITEM

=

ROW-LIKE RECORD

---

## Attributes

Each item contains:

ATTRIBUTES

Attributes are similar conceptually to:

FIELDS

or:

COLUMNS

Think:

USER ITEM

↓

UserID

↓

Name

↓

Email

↓

Age

### Memory Trick

ATTRIBUTE

=

FIELD OF AN ITEM

---

## Flexible Schema

DynamoDB provides:

FLEXIBLE SCHEMA

Different items in the same table can have:

DIFFERENT ATTRIBUTES

Think:

ITEM #1

↓

ID

NAME

EMAIL

ITEM #2

↓

ID

NAME

PHONE

ADDRESS

This allows schemas to:

EVOLVE QUICKLY

### Memory Trick

DYNAMODB

=

SCHEMA FLEXIBLE

---

## Attributes Can Be Added Over Time

Your course emphasizes that attributes:

CAN BE ADDED OVER TIME

Think:

OLD ITEM

↓

ID

NAME

New application feature:

↓

ADD EMAIL ATTRIBUTE

New items can include:

EMAIL

without redesigning a rigid relational schema.

### Memory Trick

NEW ATTRIBUTE?

↓

JUST ADD IT

---

## Primary Key

Every DynamoDB table has a:

PRIMARY KEY

The Primary Key must be decided:

WHEN THE TABLE IS CREATED

Think:

CREATE TABLE

↓

DEFINE PRIMARY KEY

↓

STORE ITEMS

The Primary Key uniquely identifies:

ITEMS

inside the table.

### Memory Trick

PRIMARY KEY

=

HOW DYNAMODB FINDS ITEMS

---

## Primary Key Is Required

Every item in a DynamoDB table must be identifiable through:

THE TABLE'S PRIMARY KEY

Think:

TABLE

↓

PRIMARY KEY

↓

FIND ITEM

This is one of the most important DynamoDB design decisions.

### Memory Trick

DESIGN ACCESS PATTERN

↓

DESIGN KEY

---

## Primary Key Types Preview

DynamoDB supports two main Primary Key designs:

PARTITION KEY

and:

PARTITION KEY + SORT KEY

Think:

SIMPLE PRIMARY KEY

↓

PARTITION KEY

COMPOSITE PRIMARY KEY

↓

PARTITION KEY + SORT KEY

We'll cover these separately in:

[DynamoDB Primary Keys](<DynamoDB Primary Keys>)

---

## Partition Key Preview

A:

PARTITION KEY

determines how DynamoDB distributes data.

Think:

ITEM

↓

PARTITION KEY

↓

DYNAMODB STORAGE PARTITION

Good partition key design is critical for:

SCALABILITY

and:

PERFORMANCE

### Memory Trick

PARTITION KEY

=

WHERE DATA GOES

---

## Sort Key Preview

A:

SORT KEY

allows multiple items to share the same:

PARTITION KEY

while remaining uniquely identifiable.

Think:

USER_ID

=

PARTITION KEY

ORDER_DATE

=

SORT KEY

This allows related items to be:

GROUPED

and:

SORTED

### Memory Trick

SORT KEY

=

ORDER ITEMS WITH SAME PARTITION KEY

---

## Maximum Item Size

Your SAA course highlights:

MAXIMUM ITEM SIZE

=

400 KB

Think:

ONE DYNAMODB ITEM

↓

MAX 400 KB

This makes DynamoDB ideal for:

SMALL RECORDS / DOCUMENTS

but not for:

LARGE FILES

### Memory Trick

DYNAMODB ITEM

=

400 KB MAX

---

## Large Object Exam Trap

Need to store:

LARGE VIDEO

↓

LARGE IMAGE

↓

MULTI-MB DOCUMENT

Do not store the entire object directly in:

DYNAMODB

Instead think:

[S3](S3)

for the large object

and:

DYNAMODB

for:

METADATA / OBJECT REFERENCE

### Memory Trick

BIG FILE

=

S3

SMALL RECORD

=

DYNAMODB

---

## DynamoDB Data Types

Your course highlights several supported data types.

### Scalar Types

STRING

↓

NUMBER

↓

BINARY

↓

BOOLEAN

↓

NULL

---

### Document Types

LIST

↓

MAP

---

### Set Types

STRING SET

↓

NUMBER SET

↓

BINARY SET

### Memory Trick

DYNAMODB

=

SCALAR + DOCUMENT + SET

---

## Document Data

DynamoDB can store:

DOCUMENT-LIKE DATA

using:

LIST

and:

MAP

Think:

JSON-LIKE STRUCTURE

↓

DYNAMODB ITEM

This makes DynamoDB useful for:

FLEXIBLE APPLICATION DATA

### Memory Trick

JSON-LIKE DATA

=

DYNAMODB

---

## DynamoDB Key-Value Model

At a high level, DynamoDB behaves like a:

KEY-VALUE

database.

Think:

KEY

↓

LOOK UP

↓

VALUE / ITEM

This makes direct key-based access:

VERY FAST

### Memory Trick

KEY KNOWN?

↓

DYNAMODB FAST

---

## Transaction Support

Although DynamoDB is NoSQL, it supports:

TRANSACTIONS

Think:

MULTIPLE OPERATIONS

↓

ALL SUCCEED

or:

ALL FAIL

This is useful when application changes need:

ATOMIC BEHAVIOR

### Memory Trick

NOSQL

DOES NOT MEAN

NO TRANSACTIONS

---

## IAM Integration

DynamoDB integrates directly with:

[IAM](IAM)

for:

SECURITY

↓

AUTHENTICATION

↓

AUTHORIZATION

Think:

APPLICATION

↓

IAM ROLE

↓

DYNAMODB

### Memory Trick

DYNAMODB SECURITY

=

IAM

---

## IAM Architecture

A serverless architecture might look like:

[Lambda](02-Compute/Lambda.md)

↓

IAM ROLE

↓

DYNAMODB

The IAM Role can allow actions such as:

READ ITEMS

↓

WRITE ITEMS

↓

UPDATE ITEMS

without hardcoding AWS credentials.

### Memory Trick

LAMBDA + DYNAMODB

=

IAM ROLE

---

## Auto Scaling

DynamoDB supports:

AUTO SCALING

for provisioned capacity.

Think:

TRAFFIC ↑

↓

CAPACITY ↑

TRAFFIC ↓

↓

CAPACITY ↓

This helps match:

DATABASE THROUGHPUT

to:

APPLICATION DEMAND

We'll cover capacity separately in:

[DynamoDB Capacity Modes](<DynamoDB Capacity Modes>)

---

## Capacity Modes Preview

DynamoDB has two major capacity modes:

PROVISIONED

and:

ON-DEMAND

Think:

PREDICTABLE TRAFFIC?

↓

PROVISIONED

UNPREDICTABLE TRAFFIC?

↓

ON-DEMAND

We'll cover the RCU / WCU details separately.

---

## Standard Table Class

DynamoDB supports:

STANDARD

table class.

Think:

FREQUENTLY ACCESSED DATA

↓

STANDARD

This is the normal general-purpose table class.

---

## Standard-IA Table Class

DynamoDB also supports:

STANDARD-INFREQUENT ACCESS

or:

STANDARD-IA

Think:

DATA STORED LONG TERM

↓

ACCESSED INFREQUENTLY

↓

STANDARD-IA

This can help optimize costs for:

LESS FREQUENTLY ACCESSED DATA

### Memory Trick

STANDARD-IA

=

DYNAMODB COLD DATA

---

## DynamoDB vs RDS

This is an important architectural distinction.

### RDS

RELATIONAL

↓

SQL

↓

JOINS

↓

STRUCTURED SCHEMA

---

### DynamoDB

NOSQL

↓

KEY-VALUE / DOCUMENT

↓

FLEXIBLE SCHEMA

↓

SERVERLESS

↓

MASSIVE SCALE

### Memory Trick

JOINS + SQL

=

RDS

SERVERLESS NOSQL

=

DYNAMODB

---

## DynamoDB vs Aurora

### Aurora

RELATIONAL

↓

MYSQL / POSTGRES COMPATIBLE

↓

SQL

---

### DynamoDB

NOSQL

↓

NO TRADITIONAL RELATIONAL JOINS

↓

SERVERLESS

Think:

RELATIONAL TRANSACTIONS / SQL?

↓

AURORA

KEY-VALUE MASSIVE SCALE?

↓

DYNAMODB

---

## DynamoDB vs ElastiCache

Both can provide:

VERY FAST KEY-VALUE ACCESS

But their roles differ.

### DynamoDB

PERSISTENT DATABASE

Think:

SOURCE OF TRUTH

---

### ElastiCache

IN-MEMORY CACHE

Think:

TEMPORARY FAST COPY

### Memory Trick

DYNAMODB

=

DATABASE

ELASTICACHE

=

CACHE

---

## DynamoDB Can Store Session Data

DynamoDB can store:

USER SESSION DATA

Think:

SESSION_ID

↓

SESSION DATA

↓

TTL

This can sometimes be an alternative to:

[ElastiCache Overview](<ElastiCache Overview>)

for distributed session storage.

### Memory Trick

PERSISTENT SERVERLESS SESSION STORE

=

DYNAMODB

---

## DynamoDB TTL Preview

DynamoDB supports:

TIME TO LIVE

or:

TTL

TTL can automatically remove items after:

AN EXPIRATION TIMESTAMP

Think:

SESSION EXPIRES

↓

DYNAMODB DELETES ITEM

We'll cover this separately in:

[DynamoDB TTL](<DynamoDB TTL>)

---

## DynamoDB Accelerator Preview

For even faster read performance, DynamoDB supports:

DAX

or:

DYNAMODB ACCELERATOR

DAX provides:

IN-MEMORY CACHING

with:

MICROSECOND READ LATENCY

Think:

DYNAMODB

↓

DAX

↓

ULTRA-FAST READS

We'll cover this separately in:

[DAX](DAX)

### Memory Trick

DYNAMODB

=

MILLISECONDS

DAX

=

MICROSECONDS

---

## DynamoDB Streams Preview

DynamoDB can capture:

ITEM-LEVEL CHANGES

using:

DYNAMODB STREAMS

Think:

CREATE

↓

UPDATE

↓

DELETE

↓

STREAM EVENT

↓

LAMBDA

This allows applications to:

REACT TO DATABASE CHANGES

We'll cover this separately in:

[DynamoDB Streams](<DynamoDB Streams>)

---

## Global Tables Preview

DynamoDB supports:

GLOBAL TABLES

for:

MULTI-REGION

ACTIVE-ACTIVE

replication.

Think:

REGION A

↔

REGION B

Users can:

READ

and:

WRITE

in multiple Regions.

We'll cover this separately in:

[DynamoDB Global Tables](<DynamoDB Global Tables>)

### Memory Trick

GLOBAL TABLE

=

MULTI-REGION ACTIVE-ACTIVE

---

## Serverless Application Architecture

A common architecture is:

CLIENT

↓

[API Gateway](<API Gateway>)

↓

[Lambda](02-Compute/Lambda.md)

↓

DYNAMODB

Think:

API GATEWAY

=

API FRONT DOOR

LAMBDA

=

COMPUTE

DYNAMODB

=

DATABASE

All three can form a:

SERVERLESS APPLICATION

### Memory Trick

API GATEWAY + LAMBDA + DYNAMODB

=

SERVERLESS STACK

---

## Why DynamoDB Fits Serverless Apps

DynamoDB does not require:

DATABASE SERVERS

or:

CONNECTION POOLS

in the traditional relational database sense.

Think:

LAMBDA

↓

DYNAMODB API

↓

READ / WRITE

This works naturally with:

EVENT-DRIVEN

↓

SERVERLESS

↓

HIGH-SCALE

architectures.

---

## Schema Evolution

Because attributes can vary between items:

APPLICATION REQUIREMENTS CHANGE

↓

ADD NEW ATTRIBUTES

↓

NO TRADITIONAL TABLE MIGRATION REQUIRED

This makes DynamoDB useful when:

SCHEMA EVOLVES QUICKLY

### Memory Trick

FAST-CHANGING SCHEMA

=

DYNAMODB

---

## Architecture Thinking

Imagine a globally growing mobile application.

MOBILE USERS

↓

API GATEWAY

↓

LAMBDA

↓

DYNAMODB

Requirements:

NO SERVER MANAGEMENT

↓

MILLIONS OF REQUESTS

↓

LOW LATENCY

↓

HIGH AVAILABILITY

↓

FLEXIBLE DATA MODEL

DynamoDB fits because it is:

SERVERLESS

↓

MULTI-AZ

↓

NOSQL

↓

HIGH SCALE

---

## When Should You Think DynamoDB?

Think DynamoDB when the question mentions:

NOSQL

↓

KEY-VALUE

↓

DOCUMENT DATA

↓

SERVERLESS DATABASE

↓

MASSIVE SCALE

↓

SINGLE-DIGIT MILLISECOND LATENCY

↓

FLEXIBLE SCHEMA

### Memory Trick

SERVERLESS + NOSQL + SCALE

=

DYNAMODB

---

## Scenario Recognition

Need a fully managed NoSQL database?

→ DynamoDB

---

Need serverless database with no servers to manage?

→ DynamoDB

---

Need a key-value database?

→ DynamoDB

---

Need document-style data?

→ DynamoDB

---

Need millions of requests per second?

→ DynamoDB

---

Need consistent single-digit millisecond database latency?

→ DynamoDB

---

Need Multi-AZ high availability by default?

→ DynamoDB

---

Need rapidly evolving schema?

→ DynamoDB

---

Need IAM-based database access?

→ DynamoDB

---

Need a maximum item size?

→ 400 KB

---

Need to store a 50 MB image?

→ S3

NOT DynamoDB

---

Need SQL joins?

→ RDS / Aurora

NOT DynamoDB

---

Need in-memory cache rather than persistent database?

→ ElastiCache

---

Need microsecond DynamoDB reads?

→ DAX

---

Need multi-Region active-active DynamoDB?

→ Global Tables

---

Need to react to item create/update/delete events?

→ DynamoDB Streams

---

## Exam Traps

DYNAMODB

=

NOSQL

---

DYNAMODB

≠

RELATIONAL DATABASE

---

DYNAMODB

=

SERVERLESS

---

DYNAMODB

=

FULLY MANAGED

---

DYNAMODB

=

MULTI-AZ BY DEFAULT

---

DYNAMODB

=

SINGLE-DIGIT MILLISECOND LATENCY

---

DYNAMODB

=

MASSIVE SCALE

---

PRIMARY KEY

=

DEFINED AT TABLE CREATION

---

ITEM

=

ROW-LIKE RECORD

---

ATTRIBUTE

=

FIELD

---

MAX ITEM SIZE

=

400 KB

---

DYNAMODB

=

FLEXIBLE SCHEMA

---

DYNAMODB SECURITY

=

IAM

---

DYNAMODB

=

TRANSACTION SUPPORT

---

DYNAMODB

≠

LARGE OBJECT STORAGE

---

LARGE FILE

=

S3

---

DAX

=

MICROSECOND CACHE

---

GLOBAL TABLES

=

ACTIVE-ACTIVE MULTI-REGION

---

## Quick Cheat Sheet

DYNAMODB

=

MANAGED SERVERLESS NOSQL

DATABASE MODEL

=

KEY-VALUE / DOCUMENT

AVAILABILITY

=

MULTI-AZ BY DEFAULT

PERFORMANCE

=

SINGLE-DIGIT MILLISECONDS

SCALE

=

MILLIONS OF REQUESTS / SECOND

MAINTENANCE

=

NONE FOR CUSTOMER

TABLE

=

CONTAINS ITEMS

ITEM

=

ROW-LIKE RECORD

ATTRIBUTE

=

FIELD

PRIMARY KEY

=

REQUIRED

PRIMARY KEY DEFINED

=

AT TABLE CREATION

MAX ITEM SIZE

=

400 KB

SCHEMA

=

FLEXIBLE

SECURITY

=

IAM

TRANSACTIONS

=

SUPPORTED

CAPACITY

=

PROVISIONED OR ON-DEMAND

TABLE CLASSES

=

STANDARD / STANDARD-IA

DAX

=

MICROSECOND READ CACHE

STREAMS

=

ITEM CHANGE EVENTS

GLOBAL TABLES

=

MULTI-REGION ACTIVE-ACTIVE

---

## Master Memory Trick

DYNAMODB

=

SERVERLESS

↓

NOSQL

↓

KEY-VALUE / DOCUMENT

↓

MULTI-AZ

↓

MILLION-SCALE

↓

MILLISECOND LATENCY

Think:

TABLE

↓

ITEM

↓

ATTRIBUTES

↓

PRIMARY KEY

And remember:

400 KB

=

MAX ITEM SIZE

IAM

=

SECURITY

DAX

=

FASTER READS

STREAMS

=

REACT TO CHANGES

GLOBAL TABLES

=

GLOBAL ACTIVE-ACTIVE

### Final Rule

QUESTION SAYS:

SERVERLESS

+

NOSQL

+

MASSIVE SCALE

+

LOW LATENCY

↓

DYNAMODB

QUESTION SAYS:

SQL + JOINS

↓

RDS / AURORA

QUESTION SAYS:

LARGE OBJECT

↓

S3

---

## Related Notes

- [DynamoDB Primary Keys](<DynamoDB Primary Keys>)
- [DynamoDB Capacity Modes](<DynamoDB Capacity Modes>)
- [DynamoDB Streams](<DynamoDB Streams.md>)
- [DAX](DAX)
- [DynamoDB Streams](<DynamoDB Streams>)
- [DynamoDB Global Tables](<DynamoDB Global Tables>)
- [DynamoDB TTL](<DynamoDB TTL>)
- [DynamoDB Backups](<DynamoDB Backups>)
- [RDS Overview](<RDS Overview>)
- [Aurora](Aurora)
- [ElastiCache Overview](<ElastiCache Overview>)
- [IAM](IAM)
- [Lambda](02-Compute/Lambda.md)
- [API Gateway](<API Gateway>)
- [S3](S3)
- [SAA Databases Cheat Sheet](<SAA Databases Cheat Sheet>)
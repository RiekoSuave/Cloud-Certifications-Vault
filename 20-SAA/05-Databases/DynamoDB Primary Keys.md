## What Problem Does It Solve?

DynamoDB needs a way to:

UNIQUELY IDENTIFY ITEMS

and:

DISTRIBUTE DATA

across its underlying infrastructure.

That job is handled by the:

PRIMARY KEY

Think:

DYNAMODB TABLE

↓

PRIMARY KEY

↓

FIND ITEM

↓

DISTRIBUTE ITEM

### Memory Trick

PRIMARY KEY

=

HOW DYNAMODB FINDS DATA

---

## What Is a DynamoDB Primary Key?

Every DynamoDB table must have:

A PRIMARY KEY

The Primary Key is defined:

WHEN THE TABLE IS CREATED

Think:

CREATE TABLE

↓

CHOOSE PRIMARY KEY

↓

STORE ITEMS

### Memory Trick

PRIMARY KEY

=

DECIDE AT CREATION

---

## Primary Key Types

DynamoDB supports two main Primary Key designs:

PARTITION KEY

and:

PARTITION KEY + SORT KEY

Think:

SIMPLE PRIMARY KEY

↓

PARTITION KEY ONLY

COMPOSITE PRIMARY KEY

↓

PARTITION KEY + SORT KEY

### Memory Trick

ONE KEY

=

PARTITION KEY

TWO-PART KEY

=

PARTITION + SORT

---

## Simple Primary Key

A Simple Primary Key contains:

ONLY A PARTITION KEY

Think:

TABLE

↓

User_ID

↓

PRIMARY KEY

Each value must uniquely identify:

ONE ITEM

Example:

User_ID

=

12345

Think:

USER 12345

↓

ONE ITEM

### Memory Trick

SIMPLE KEY

=

PARTITION KEY ONLY

---

## Partition Key

The:

PARTITION KEY

is used by DynamoDB to determine:

WHERE DATA IS STORED

Think:

ITEM

↓

PARTITION KEY VALUE

↓

HASHING

↓

STORAGE PARTITION

### Memory Trick

PARTITION KEY

=

WHERE DATA GOES

---

## Partition Key Example

Imagine a table:

USERS

Primary Key:

User_ID

Example:

User_ID = 1001

↓

USER ALICE

User_ID = 1002

↓

USER BOB

User_ID = 1003

↓

USER CHARLIE

Each Partition Key value identifies:

ONE ITEM

### Memory Trick

UNIQUE ID

=

PARTITION KEY

---

## Composite Primary Key

A Composite Primary Key contains:

PARTITION KEY

+

SORT KEY

Think:

PRIMARY KEY

=

PARTITION KEY + SORT KEY

The combination of both values must be:

UNIQUE

### Memory Trick

COMPOSITE

=

TWO-PART PRIMARY KEY

---

## Sort Key

A:

SORT KEY

allows multiple items to share:

THE SAME PARTITION KEY

Think:

SAME USER

↓

MULTIPLE ORDERS

or:

SAME GAME

↓

MULTIPLE SCORES

The Sort Key differentiates:

RELATED ITEMS

within the same Partition Key.

### Memory Trick

SORT KEY

=

DISTINGUISH RELATED ITEMS

---

## Composite Key Example

Imagine an Orders table.

Partition Key:

Customer_ID

Sort Key:

Order_ID

Think:

Customer_ID = 100

↓

Order_ID = 1

Order_ID = 2

Order_ID = 3

The full Primary Key becomes:

Customer_ID + Order_ID

### Memory Trick

ONE CUSTOMER

↓

MANY ORDERS

---

## Why Use a Sort Key?

A Sort Key is useful when you want to:

GROUP RELATED ITEMS

under the same:

PARTITION KEY

Think:

USER

↓

ORDERS

↓

SESSIONS

↓

EVENTS

↓

MESSAGES

The Partition Key groups them.

The Sort Key organizes them.

### Memory Trick

PARTITION

=

GROUP

SORT

=

ORDER / DIFFERENTIATE

---

## DynamoDB Table Example

Your SAA slides use an example with attributes such as:

User_ID

↓

Game_ID

↓

Score

↓

Result

Think:

User_ID

=

PARTITION KEY

Game_ID

=

SORT KEY

Together:

User_ID + Game_ID

↓

PRIMARY KEY

This lets one user have:

MULTIPLE GAME RECORDS

### Memory Trick

USER

=

PARTITION

GAME

=

SORT

---

## Uniqueness Rule

With a Simple Primary Key:

PARTITION KEY VALUE

must uniquely identify the item.

Think:

User_ID = 123

↓

ONE ITEM

---

With a Composite Primary Key:

PARTITION KEY

does not need to be unique by itself.

But:

PARTITION KEY + SORT KEY

must be unique.

Think:

User_ID = 123

Game_ID = 1

↓

UNIQUE

User_ID = 123

Game_ID = 2

↓

ALSO UNIQUE

### Memory Trick

COMPOSITE UNIQUENESS

=

BOTH VALUES TOGETHER

---

## Same Partition Key, Different Sort Keys

Example:

User_ID

=

777

Sort Key values:

GAME-A

↓

GAME-B

↓

GAME-C

These are allowed because:

THE FULL COMPOSITE KEY

is different.

Think:

777 + GAME-A

777 + GAME-B

777 + GAME-C

### Memory Trick

SAME PARTITION

+

DIFFERENT SORT

=

VALID

---

## Same Partition + Same Sort

This would not create two separate items.

Think:

User_ID = 777

Game_ID = GAME-A

and again:

User_ID = 777

Game_ID = GAME-A

That identifies:

THE SAME ITEM KEY

### Memory Trick

SAME FULL PRIMARY KEY

=

SAME ITEM IDENTITY

---

## Partition Key and Data Distribution

DynamoDB uses the Partition Key to:

DISTRIBUTE ITEMS

across storage partitions.

Think:

PARTITION KEY VALUE

↓

HASH FUNCTION

↓

PHYSICAL PARTITION

This allows DynamoDB to:

SCALE HORIZONTALLY

### Memory Trick

PARTITION KEY

=

DISTRIBUTION KEY

---

## Good Partition Key Design

A good Partition Key should distribute traffic:

EVENLY

Think:

MANY DIFFERENT KEY VALUES

↓

LOAD SPREAD

↓

GOOD PERFORMANCE

A poor Partition Key can concentrate too much traffic on:

ONE PARTITION

### Memory Trick

GOOD KEY

=

SPREAD THE LOAD

---

## Hot Partition

A:

HOT PARTITION

occurs when too much traffic targets:

THE SAME PARTITION KEY VALUE

Think:

MILLIONS OF REQUESTS

↓

SAME KEY

↓

SAME PARTITION

↓

BOTTLENECK

### Memory Trick

HOT KEY

=

HOT PARTITION

---

## Hot Partition Example

Suppose the Partition Key is:

Country

Most users are in:

USA

Think:

USA

↓

80% OF TRAFFIC

↓

ONE KEY VALUE GETS HEAVY LOAD

This can cause:

UNEVEN DATA / TRAFFIC DISTRIBUTION

### Exam Thinking

Poorly distributed Partition Key values can hurt:

DYNAMODB PERFORMANCE

---

## High Cardinality

A strong Partition Key usually has:

MANY POSSIBLE VALUES

This is often called:

HIGH CARDINALITY

Examples:

User_ID

↓

Order_ID

↓

Device_ID

Think:

MANY UNIQUE VALUES

↓

BETTER DISTRIBUTION

### Memory Trick

HIGH CARDINALITY

=

MORE KEY VALUES

=

BETTER SPREAD

---

## Low Cardinality

A weak Partition Key may have:

VERY FEW VALUES

Example:

Status

with values:

OPEN

CLOSED

PENDING

Think:

MILLIONS OF ITEMS

↓

ONLY 3 KEY VALUES

↓

POOR DISTRIBUTION

### Memory Trick

FEW VALUES

=

HOT PARTITION RISK

---

## Access Patterns Matter

DynamoDB table design should begin with:

HOW WILL THE APPLICATION ACCESS DATA?

Think:

WHAT WILL I QUERY BY?

↓

WHAT SHOULD MY PARTITION KEY BE?

DynamoDB does not work like a traditional SQL database where you casually query any column efficiently.

### Memory Trick

DYNAMODB DESIGN

=

ACCESS PATTERN FIRST

---

## Query Behavior

Your course later emphasizes that DynamoDB queries are performed using:

PRIMARY KEYS

or:

INDEXES

Think:

KNOW KEY?

↓

QUERY DYNAMODB

Need alternate access pattern?

↓

USE INDEX

We'll cover indexes separately in:

[DynamoDB Indexes](<DynamoDB Indexes>)

### Memory Trick

DYNAMODB QUERY

=

KEY OR INDEX

---

## Partition Key vs Sort Key

### Partition Key

PURPOSE

=

DISTRIBUTE DATA

Think:

WHERE?

---

### Sort Key

PURPOSE

=

ORGANIZE RELATED ITEMS

Think:

WHICH ONE?

### Memory Trick

PARTITION

=

WHERE

SORT

=

WHICH ITEM

---

## Simple vs Composite Key

### Simple Primary Key

PARTITION KEY ONLY

Example:

User_ID

Think:

ONE USER

↓

ONE ITEM

---

### Composite Primary Key

PARTITION KEY + SORT KEY

Example:

User_ID + Game_ID

Think:

ONE USER

↓

MANY GAMES

### Memory Trick

SIMPLE

=

ONE DIMENSION

COMPOSITE

=

GROUP + DETAIL

---

## Time-Series Example

Imagine IoT data.

Partition Key:

Device_ID

Sort Key:

Timestamp

Think:

DEVICE-001

↓

10:00

↓

10:01

↓

10:02

This allows:

ONE DEVICE

↓

MANY TIME-ORDERED EVENTS

### Memory Trick

DEVICE

=

PARTITION

TIME

=

SORT

---

## E-Commerce Example

Imagine:

Customer_ID

as:

PARTITION KEY

and:

Order_Date

as:

SORT KEY

Think:

CUSTOMER

↓

2026-08-01

↓

2026-08-12

↓

2026-08-25

This allows you to organize:

ORDERS FOR ONE CUSTOMER

by:

DATE

### Memory Trick

CUSTOMER

=

GROUP

DATE

=

ORDER

---

## Gaming Example

Using the course-style example:

User_ID

↓

PARTITION KEY

Game_ID

↓

SORT KEY

Attributes:

Score

↓

Result

Think:

USER

↓

GAME RECORDS

↓

SCORE / RESULT

### Memory Trick

PRIMARY KEY

=

WHO + WHICH GAME

---

## Architecture Thinking

Imagine:

APPLICATION

↓

DYNAMODB TABLE

↓

PARTITION KEY

↓

HASH

↓

PARTITION

Then within that partition:

SORT KEY

↓

RELATED ITEMS

Think:

PARTITION KEY

=

DISTRIBUTE

SORT KEY

=

ORGANIZE

---

## Key Design and Scaling

DynamoDB scales best when requests are:

DISTRIBUTED

across many:

PARTITION KEY VALUES

Think:

GOOD DESIGN

↓

EVEN TRAFFIC

↓

SCALABLE PERFORMANCE

Poor key design:

↓

HOT KEY

↓

HOT PARTITION

↓

THROTTLING RISK

### Memory Trick

KEY DESIGN

=

PERFORMANCE DESIGN

---

## Scenario Recognition

Need each item uniquely identified by one attribute?

→ Partition Key only

---

Need multiple related items under one entity?

→ Partition Key + Sort Key

---

Need one customer with many orders?

→ Customer_ID + Order_ID / Order_Date

---

Need one user with many game records?

→ User_ID + Game_ID

---

Need one device with many timestamped events?

→ Device_ID + Timestamp

---

Need data distributed across DynamoDB partitions?

→ Partition Key

---

Need related items ordered within the same partition key?

→ Sort Key

---

Need to avoid hot partitions?

→ Choose a well-distributed Partition Key

---

Need a good Partition Key?

→ Prefer high-cardinality values with evenly distributed access

---

Need to query using a non-primary-key attribute?

→ Consider a DynamoDB Index

---

## Exam Traps

PRIMARY KEY

=

DEFINED AT TABLE CREATION

---

PARTITION KEY

=

REQUIRED

---

SORT KEY

=

OPTIONAL

---

SIMPLE PRIMARY KEY

=

PARTITION KEY ONLY

---

COMPOSITE PRIMARY KEY

=

PARTITION KEY + SORT KEY

---

PARTITION KEY

=

DATA DISTRIBUTION

---

SORT KEY

=

GROUP / ORDER RELATED ITEMS

---

COMPOSITE KEY UNIQUENESS

=

PARTITION + SORT TOGETHER

---

SAME PARTITION KEY

=

ALLOWED WITH DIFFERENT SORT KEYS

---

HOT PARTITION

=

TOO MUCH TRAFFIC TO SAME KEY

---

HIGH CARDINALITY

=

GOOD PARTITION KEY TRAIT

---

LOW CARDINALITY

=

HOT PARTITION RISK

---

DYNAMODB QUERY

=

PRIMARY KEY OR INDEX

---

## Quick Cheat Sheet

PRIMARY KEY

=

IDENTIFIES ITEM

DEFINED

=

AT TABLE CREATION

SIMPLE PRIMARY KEY

=

PARTITION KEY

COMPOSITE PRIMARY KEY

=

PARTITION KEY + SORT KEY

PARTITION KEY

=

DISTRIBUTE DATA

SORT KEY

=

ORGANIZE RELATED ITEMS

PARTITION KEY REQUIRED

=

YES

SORT KEY REQUIRED

=

NO

GOOD PARTITION KEY

=

HIGH CARDINALITY

GOOD DISTRIBUTION

HOT PARTITION

=

TOO MUCH TRAFFIC TO ONE KEY

QUERY

=

PRIMARY KEY / INDEX

---

## Master Memory Trick

PARTITION KEY

=

WHERE DOES IT GO?

SORT KEY

=

WHICH ITEM IS IT?

Think:

USER

↓

PARTITION KEY

GAME

↓

SORT KEY

Together:

USER + GAME

↓

UNIQUE ITEM

And remember:

GOOD KEY

↓

MANY VALUES

↓

EVEN TRAFFIC

BAD KEY

↓

FEW VALUES

↓

HOT PARTITION

### Final Rule

QUESTION SAYS:

ONE UNIQUE ATTRIBUTE

↓

PARTITION KEY ONLY

QUESTION SAYS:

ONE ENTITY + MANY RELATED ITEMS

↓

PARTITION KEY + SORT KEY

QUESTION SAYS:

HOT PARTITION

↓

FIX PARTITION KEY DISTRIBUTION

---

## Related Notes

- [DynamoDB Overview](<DynamoDB Overview>)
- [DynamoDB Capacity Modes](<DynamoDB Capacity Modes>)
- [DynamoDB Streams](<DynamoDB Streams.md>)
- [DynamoDB Indexes](<DynamoDB Indexes>)
- [DAX](DAX)
- [DynamoDB Streams](<DynamoDB Streams>)
- [DynamoDB Global Tables](<DynamoDB Global Tables>)
- [DynamoDB TTL](<DynamoDB TTL>)
- [DynamoDB Backups](<DynamoDB Backups>)
- [SAA Databases Cheat Sheet](<SAA Databases Cheat Sheet>)
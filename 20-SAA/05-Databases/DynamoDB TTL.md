## What Problem Does It Solve?

DynamoDB tables can accumulate data that is only useful for:

A LIMITED PERIOD OF TIME

Examples:

WEB SESSIONS

↓

TEMPORARY DATA

↓

OLD RECORDS

↓

EXPIRED ITEMS

Without automatic expiration:

OLD DATA

↓

REMAINS IN TABLE

↓

UNNECESSARY STORAGE

DynamoDB TTL solves this by:

AUTOMATICALLY DELETING ITEMS

after they expire.

### Memory Trick

TTL

=

AUTO-DELETE EXPIRED ITEMS

---

## What Is DynamoDB TTL?

TTL stands for:

TIME TO LIVE

It allows DynamoDB to:

AUTOMATICALLY DELETE ITEMS

after an:

EXPIRATION TIMESTAMP

Think:

ITEM

↓

EXPIRATION TIME

↓

TIME REACHED

↓

ITEM DELETED

### Memory Trick

TTL

=

EXPIRATION TIMER

---

## How TTL Works

An item contains an attribute representing:

EXPIRATION TIME

Think:

DYNAMODB ITEM

↓

TTL ATTRIBUTE

↓

EXPIRATION TIMESTAMP

↓

EXPIRATION PROCESS

↓

DELETION PROCESS

The item can then be automatically removed after:

EXPIRATION

### Memory Trick

TIMESTAMP EXPIRES

↓

ITEM GOES AWAY

---

## Expiration Timestamp

The SAA slide shows the TTL value as an:

EPOCH TIMESTAMP

Think:

ExpTime

=

1631274971

This represents:

A SPECIFIC TIME

When the expiration time is reached:

ITEM BECOMES EXPIRED

### Memory Trick

TTL VALUE

=

EXPIRATION TIMESTAMP

---

## Course Table Example

The SAA slide uses:

SESSION DATA

with attributes such as:

User_ID

↓

Session_ID

↓

ExpTime (TTL)

Think:

USER SESSION

↓

EXPIRATION TIME

↓

AUTOMATIC DELETION

This is a classic TTL use case.

### Memory Trick

SESSION EXPIRES

↓

DELETE SESSION DATA

---

## Web Session Handling

One major TTL use case is:

WEB SESSION HANDLING

Imagine:

USER LOGS IN

↓

SESSION CREATED

↓

SESSION STORED IN DYNAMODB

↓

SESSION EXPIRATION TIME

↓

TTL

↓

OLD SESSION REMOVED

This prevents expired sessions from remaining indefinitely.

### Memory Trick

SESSION DATA

+

EXPIRATION

=

TTL

---

## Keep Only Current Items

Another course use case is:

KEEP ONLY CURRENT ITEMS

Think:

CURRENT DATA

↓

KEEP

OLD / EXPIRED DATA

↓

DELETE

This helps reduce:

UNNECESSARY STORED DATA

### Memory Trick

CURRENT

=

KEEP

EXPIRED

=

DELETE

---

## Reduce Stored Data

TTL can help:

REDUCE STORED DATA

by removing items that are no longer needed.

Think:

TABLE

↓

CURRENT ITEMS

+

EXPIRED ITEMS

TTL

↓

REMOVE EXPIRED ITEMS

↓

SMALLER ACTIVE DATASET

### Memory Trick

TTL

=

AUTOMATIC DATA CLEANUP

---

## Regulatory Obligations

The SAA slide also lists:

REGULATORY OBLIGATIONS

as a TTL use case.

Some data may need to exist only for:

A DEFINED PERIOD

Think:

STORE DATA

↓

RETENTION PERIOD

↓

EXPIRATION

↓

DELETE DATA

### Memory Trick

RETENTION DEADLINE

↓

TTL

---

## TTL Architecture

Think:

APPLICATION

↓

[[DynamoDB Overview]]

↓

ITEM STORED

↓

TTL ATTRIBUTE

↓

EXPIRATION TIMESTAMP

↓

EXPIRATION PROCESS

↓

DELETION PROCESS

### Memory Trick

STORE

↓

WAIT

↓

EXPIRE

↓

DELETE

---

## TTL Attribute

To use TTL, an item contains an attribute representing:

WHEN THE ITEM EXPIRES

The course example calls this:

ExpTime

Think:

ITEM DATA

+

EXPIRATION ATTRIBUTE

### Memory Trick

TTL ATTRIBUTE

=

DELETE-AFTER TIME

---

## Item Before Expiration

Before the expiration timestamp:

ITEM

↓

REMAINS IN DYNAMODB

Think:

CURRENT TIME

<

EXPIRATION TIME

↓

ITEM STILL CURRENT

### Memory Trick

NOT EXPIRED

=

KEEP ITEM

---

## Item After Expiration

Once the expiration time has passed:

CURRENT TIME

>

EXPIRATION TIME

↓

ITEM EXPIRED

↓

DELETION PROCESS

The item can then be:

AUTOMATICALLY DELETED

### Memory Trick

TIME'S UP

↓

DELETE

---

## TTL Is Automatic

A key advantage is that your application does not need to manually:

FIND OLD ITEMS

and:

DELETE THEM ONE BY ONE

Instead:

EXPIRATION TIMESTAMP

↓

DYNAMODB TTL

↓

AUTOMATIC DELETION

### Memory Trick

TTL

=

NO MANUAL CLEANUP

---

## TTL vs Manual Deletion

### Manual Deletion

APPLICATION

↓

FIND EXPIRED DATA

↓

DELETE DATA

This requires:

APPLICATION LOGIC

---

### TTL

APPLICATION

↓

STORE EXPIRATION TIMESTAMP

↓

DYNAMODB HANDLES EXPIRATION

### Memory Trick

MANUAL

=

APP DELETES

TTL

=

DYNAMODB DELETES

---

## TTL vs DynamoDB Streams

Do not confuse:

[[DynamoDB TTL]]

with:

[[DynamoDB Streams]]

### DynamoDB TTL

Purpose:

DELETE EXPIRED ITEMS

Think:

TIME EXPIRED

↓

DELETE

---

### DynamoDB Streams

Purpose:

CAPTURE ITEM-LEVEL CHANGES

Think:

CREATE

UPDATE

DELETE

↓

STREAM EVENT

### Memory Trick

TTL

=

EXPIRATION

STREAMS

=

CHANGES

---

## TTL vs Global Tables

Do not confuse:

[[DynamoDB TTL]]

with:

[[DynamoDB Global Tables]]

### TTL

Purpose:

REMOVE EXPIRED DATA

---

### Global Tables

Purpose:

MULTI-REGION DYNAMODB

Think:

TTL

=

TIME

GLOBAL TABLES

=

REGIONS

### Memory Trick

TTL

=

WHEN DATA DIES

GLOBAL TABLES

=

WHERE DATA LIVES

---

## TTL vs DAX

Do not confuse:

[[DynamoDB TTL]]

with:

[[DAX]]

### TTL

Purpose:

DELETE EXPIRED ITEMS

---

### DAX

Purpose:

CACHE DYNAMODB READS

Think:

TTL

=

DATA EXPIRATION

DAX

=

READ PERFORMANCE

### Memory Trick

TTL

=

DELETE OLD DATA

DAX

=

READ DATA FAST

---

## TTL vs DynamoDB Capacity Modes

[[DynamoDB Capacity Modes]]

determine:

HOW READ / WRITE CAPACITY IS MANAGED

TTL determines:

WHEN EXPIRED ITEMS SHOULD BE REMOVED

Think:

CAPACITY MODES

=

THROUGHPUT

TTL

=

EXPIRATION

### Memory Trick

CAPACITY

=

TRAFFIC

TTL

=

TIME

---

## Session Data Scenario

A company stores:

WEB SESSION DATA

in DynamoDB.

Each session should automatically disappear after:

SESSION EXPIRATION

Requirement:

NO MANUAL CLEANUP PROCESS

Answer:

DYNAMODB TTL

Think:

SESSION

↓

EXPIRATION TIMESTAMP

↓

TTL

↓

DELETE

### Memory Trick

EXPIRED SESSION

=

TTL

---

## Temporary Data Scenario

An application stores information that should only exist for:

A LIMITED TIME

Requirement:

AUTOMATICALLY REMOVE OLD RECORDS

Answer:

DYNAMODB TTL

### Memory Trick

TEMPORARY DYNAMODB DATA

=

TTL

---

## Current Data Scenario

A company wants its DynamoDB table to retain:

ONLY CURRENT ITEMS

Old records are no longer useful.

Think:

CURRENT

↓

KEEP

EXPIRED

↓

TTL

↓

DELETE

### Memory Trick

ONLY CURRENT DATA?

↓

TTL

---

## Retention Scenario

A company must remove records after:

A DEFINED RETENTION PERIOD

The items contain:

EXPIRATION TIMESTAMPS

Think:

RETENTION PERIOD ENDS

↓

TTL

↓

AUTOMATIC DELETION

### Memory Trick

DELETE AFTER TIME

=

TTL

---

## Architecture Thinking

Imagine:

WEB APPLICATION

↓

SESSION CREATED

↓

DYNAMODB

↓

User_ID

Session_ID

ExpTime

Then:

CURRENT TIME

↓

REACHES EXPIRATION TIME

↓

ITEM EXPIRES

↓

DELETION PROCESS

### Memory Trick

SESSION TABLE

+

EXPIRATION TIME

=

TTL

---

## When Should You Think TTL?

Look for requirements such as:

AUTOMATICALLY DELETE

↓

EXPIRED ITEMS

↓

EXPIRATION TIMESTAMP

↓

TEMPORARY DATA

↓

WEB SESSIONS

↓

KEEP ONLY CURRENT DATA

↓

RETENTION REQUIREMENTS

These strongly point toward:

DYNAMODB TTL

### Memory Trick

QUESTION MENTIONS:

EXPIRE

or:

DELETE AFTER TIME

↓

TTL

---

## Scenario Recognition

Need DynamoDB items automatically deleted after expiration?

→ DynamoDB TTL

---

Need to associate an expiration timestamp with an item?

→ DynamoDB TTL

---

Need to remove expired web sessions?

→ DynamoDB TTL

---

Need to keep only current DynamoDB items?

→ DynamoDB TTL

---

Need to reduce stored data by removing expired items?

→ DynamoDB TTL

---

Need data removed after a defined retention period?

→ DynamoDB TTL

---

Need to react to DynamoDB create/update/delete changes?

→ [[DynamoDB Streams]]

---

Need Active-Active multi-Region DynamoDB?

→ [[DynamoDB Global Tables]]

---

Need microsecond cached DynamoDB reads?

→ [[DAX]]

---

Need to manage DynamoDB read/write throughput?

→ [[DynamoDB Capacity Modes]]

---

## Exam Traps

TTL

=

TIME TO LIVE

---

TTL

=

AUTOMATIC ITEM EXPIRATION

---

TTL

=

EXPIRATION TIMESTAMP

---

TTL USE CASE

=

WEB SESSIONS

---

TTL USE CASE

=

KEEP ONLY CURRENT ITEMS

---

TTL USE CASE

=

REDUCE STORED DATA

---

TTL USE CASE

=

REGULATORY OBLIGATIONS

---

TTL

≠

DYNAMODB STREAMS

---

TTL

≠

DAX

---

TTL

≠

GLOBAL TABLES

---

TTL

≠

CAPACITY MODE

---

STREAMS

=

ITEM CHANGES

TTL

=

ITEM EXPIRATION

---

DAX

=

CACHE

TTL

=

DELETE EXPIRED DATA

---

GLOBAL TABLES

=

MULTI-REGION

TTL

=

TIME-BASED EXPIRATION

---

## Quick Cheat Sheet

TTL

=

TIME TO LIVE

PURPOSE

=

AUTOMATICALLY DELETE EXPIRED ITEMS

BASED ON

=

EXPIRATION TIMESTAMP

COURSE EXAMPLE

=

SESSION DATA

WEB SESSIONS

=

TTL USE CASE

KEEP ONLY CURRENT ITEMS

=

TTL USE CASE

REDUCE STORED DATA

=

TTL USE CASE

REGULATORY OBLIGATIONS

=

TTL USE CASE

STREAMS

=

CAPTURE CHANGES

GLOBAL TABLES

=

MULTI-REGION

DAX

=

CACHE

CAPACITY MODES

=

READ / WRITE THROUGHPUT

TTL

=

DATA EXPIRATION

---

## Master Memory Trick

TTL

=

TIME TO LIVE

Think:

ITEM CREATED

↓

EXPIRATION TIMESTAMP

↓

TIME PASSES

↓

ITEM EXPIRES

↓

AUTOMATIC DELETION

And remember:

WEB SESSION

↓

SESSION EXPIRES

↓

TTL

↓

DELETE SESSION

### Final Rule

QUESTION SAYS:

DYNAMODB

+

AUTOMATIC DELETE

+

EXPIRATION TIMESTAMP

↓

TTL

QUESTION SAYS:

WEB SESSION DATA

+

DELETE WHEN EXPIRED

↓

TTL

QUESTION SAYS:

CAPTURE TABLE CHANGES

↓

DYNAMODB STREAMS

QUESTION SAYS:

MULTI-REGION ACTIVE-ACTIVE

↓

GLOBAL TABLES

---

## Related Notes

- [[DynamoDB Overview]]
- [[DynamoDB Primary Keys]]
- [[DynamoDB Capacity Modes]]
- [[DAX]]
- [[DynamoDB Streams]]
- [[DynamoDB Global Tables]]
- [[SAA Databases Cheat Sheet]]
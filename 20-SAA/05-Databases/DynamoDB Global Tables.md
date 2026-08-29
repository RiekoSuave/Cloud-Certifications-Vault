## What Problem Does It Solve?

A DynamoDB table normally exists within:

ONE AWS REGION

But applications may have users located:

AROUND THE WORLD

If all users access a table in only one Region:

DISTANT USERS

↓

HIGHER NETWORK LATENCY

DynamoDB Global Tables solve this by making DynamoDB data available across:

MULTIPLE AWS REGIONS

Think:

US USERS

↓

US REGION

GLOBAL TABLE

↕

ASIA REGION

↓

ASIA USERS

### Memory Trick

GLOBAL TABLES

=

DYNAMODB ACROSS REGIONS

---

## What Are DynamoDB Global Tables?

DynamoDB Global Tables allow a DynamoDB table to be:

ACCESSIBLE

with:

LOW LATENCY

across:

MULTIPLE REGIONS

Think:

REGION A

↔

REGION B

Both Regions contain:

DYNAMODB TABLE REPLICAS

### Memory Trick

GLOBAL TABLE

=

MULTI-REGION DYNAMODB

---

## Multi-Region Architecture

The course architecture shows:

US-EAST-1

↓

DYNAMODB TABLE

↕

TWO-WAY REPLICATION

↕

AP-SOUTHEAST-2

↓

DYNAMODB TABLE

Together these form:

GLOBAL TABLE

### Memory Trick

MULTIPLE REGIONS

+

REPLICATED TABLE

=

GLOBAL TABLE

---

## Active-Active Replication

DynamoDB Global Tables use:

ACTIVE-ACTIVE REPLICATION

Think:

REGION A

=

ACTIVE

and:

REGION B

=

ACTIVE

Both Regions can actively serve:

APPLICATION TRAFFIC

### Memory Trick

GLOBAL TABLES

=

ACTIVE-ACTIVE

---

## What Does Active-Active Mean?

Active-Active means applications can:

READ

and:

WRITE

to the table in:

ANY PARTICIPATING REGION

Think:

REGION A

↓

READ + WRITE

↕

REPLICATION

↕

REGION B

↓

READ + WRITE

This is different from an architecture where one Region is:

READ-ONLY

### Memory Trick

ACTIVE-ACTIVE

=

WRITE ANYWHERE

---

## Reads in Multiple Regions

Applications can:

READ

from the DynamoDB table in:

ANY REGION

participating in the Global Table.

Think:

US USER

↓

US TABLE

↓

LOW LATENCY READ

ASIA USER

↓

ASIA TABLE

↓

LOW LATENCY READ

### Memory Trick

READ LOCALLY

=

LOWER LATENCY

---

## Writes in Multiple Regions

Applications can also:

WRITE

to the DynamoDB table in:

ANY PARTICIPATING REGION

Think:

US APPLICATION

↓

WRITE US REGION

ASIA APPLICATION

↓

WRITE ASIA REGION

Changes are then:

REPLICATED

between the Regions.

### Memory Trick

GLOBAL TABLE

=

READ + WRITE EVERYWHERE

---

## Two-Way Replication

The SAA slide architecture explicitly shows:

TWO-WAY REPLICATION

Think:

REGION A

↓

CHANGE

↓

REGION B

and:

REGION B

↓

CHANGE

↓

REGION A

This enables the:

ACTIVE-ACTIVE

architecture.

### Memory Trick

TWO-WAY REPLICATION

=

ACTIVE-ACTIVE

---

## Low-Latency Global Access

One major reason to use Global Tables is:

LOW LATENCY

for users located across:

MULTIPLE GEOGRAPHIC REGIONS

Think:

USER

↓

NEAREST AWS REGION

↓

DYNAMODB GLOBAL TABLE

Instead of:

USER

↓

DISTANT REGION

↓

HIGHER LATENCY

### Memory Trick

GLOBAL USERS

=

LOCAL DYNAMODB ACCESS

---

## DynamoDB Streams Requirement

This is a major exam point.

To use:

DYNAMODB GLOBAL TABLES

you must enable:

[[DynamoDB Streams]]

Think:

DYNAMODB STREAMS

↓

CHANGE INFORMATION

↓

GLOBAL TABLE REPLICATION

### Memory Trick

GLOBAL TABLES

NEED:

STREAMS

---

## Streams Are a Prerequisite

The SAA slide specifically states:

DYNAMODB STREAMS

must be enabled as a:

PREREQUISITE

Think:

NO STREAMS

↓

NO GLOBAL TABLE

for the course exam model.

### Memory Trick

STREAMS FIRST

↓

GLOBAL TABLE SECOND

---

## Why Streams Matter

Global Tables need to know when:

ITEMS CHANGE

Think:

CREATE

↓

UPDATE

↓

DELETE

[[DynamoDB Streams]]

captures:

ITEM-LEVEL MODIFICATIONS

Those changes support replication across:

MULTIPLE REGIONS

### Memory Trick

STREAMS

=

CHANGE FEED

GLOBAL TABLES

=

REPLICATE CHANGES

---

## Global Tables Architecture

Think:

APPLICATION A

↓

REGION A

↓

DYNAMODB TABLE

↕

ACTIVE-ACTIVE REPLICATION

↕

DYNAMODB TABLE

↓

REGION B

↓

APPLICATION B

Both applications can:

READ

and:

WRITE

locally.

### Memory Trick

APP A

↓

LOCAL TABLE

↕

LOCAL TABLE

↓

APP B

---

## Global Application Scenario

Imagine an application has users in:

UNITED STATES

and:

ASIA

Requirement:

LOW DATABASE LATENCY

for both locations.

Architecture:

US USERS

↓

US REGION

↓

DYNAMODB GLOBAL TABLE

↕

ASIA REGION

↓

ASIA USERS

### Memory Trick

GLOBAL USERS

+

DYNAMODB

=

GLOBAL TABLES

---

## Active-Active vs Active-Passive

### Active-Active

Both Regions:

SERVE TRAFFIC

and:

ACCEPT WRITES

Think:

REGION A

↔

REGION B

This describes:

DYNAMODB GLOBAL TABLES

---

### Active-Passive

One Region primarily handles traffic.

Another Region waits as:

STANDBY

Think:

PRIMARY

↓

SECONDARY

This is:

NOT

the Global Tables architecture highlighted in the course.

### Memory Trick

GLOBAL TABLES

=

ACTIVE-ACTIVE

NOT:

ACTIVE-PASSIVE

---

## Global Tables vs DynamoDB Streams

Do not confuse:

[[DynamoDB Global Tables]]

with:

[[DynamoDB Streams]]

### DynamoDB Streams

Purpose:

CAPTURE ITEM-LEVEL CHANGES

Think:

CREATE

UPDATE

DELETE

↓

EVENT STREAM

---

### Global Tables

Purpose:

MULTI-REGION DYNAMODB

Think:

REGION A

↔

REGION B

### Memory Trick

STREAMS

=

CHANGES

GLOBAL TABLES

=

REGIONS

---

## Global Tables Depend on Streams

The relationship is:

DYNAMODB TABLE

↓

[[DynamoDB Streams]]

↓

CHANGE INFORMATION

↓

GLOBAL TABLE REPLICATION

Think:

STREAMS

=

PREREQUISITE

GLOBAL TABLES

=

MULTI-REGION RESULT

### Memory Trick

NO STREAMS

↓

NO GLOBAL TABLES

---

## Global Tables vs DAX

Do not confuse:

[[DAX]]

with:

[[DynamoDB Global Tables]]

### DAX

Purpose:

FASTER CACHED READS

Think:

MICROSECOND CACHE

---

### Global Tables

Purpose:

LOW-LATENCY MULTI-REGION ACCESS

Think:

GLOBAL DATABASE

### Memory Trick

DAX

=

CACHE

GLOBAL TABLES

=

REGIONS

---

## Global Tables vs Read Replicas

Global Tables are:

ACTIVE-ACTIVE

Applications can:

READ + WRITE

in multiple Regions.

Traditional database read replicas generally focus on:

READ SCALING

and do not represent the same:

MULTI-REGION ACTIVE-ACTIVE

architecture.

Think:

READ REPLICA

=

READ SCALE

GLOBAL TABLE

=

READ + WRITE MULTI-REGION

### Memory Trick

GLOBAL TABLES

=

NOT JUST READ REPLICAS

---

## Global Tables and High Availability

Because the data exists across:

MULTIPLE REGIONS

Global Tables can support architectures requiring:

MULTI-REGION AVAILABILITY

Think:

REGION A

↕

REGION B

Applications can interact with table replicas across:

MULTIPLE REGIONS

### Memory Trick

MULTI-REGION

=

GLOBAL RESILIENCE

---

## Global Tables and Disaster Recovery

For SAA architecture thinking:

MULTI-REGION REPLICATION

can contribute to:

DISASTER RECOVERY

because DynamoDB data is available in:

MORE THAN ONE REGION

Think:

REGIONAL PROBLEM

↓

DATA ALSO EXISTS ELSEWHERE

However, the strongest direct exam signal for Global Tables remains:

ACTIVE-ACTIVE

+

LOW-LATENCY MULTI-REGION ACCESS

### Memory Trick

GLOBAL TABLES

=

GLOBAL ACCESS FIRST

DR BENEFIT SECOND

---

## Global Tables and Global Users

Suppose:

USERS IN NORTH AMERICA

↓

US REGION

USERS IN ASIA

↓

ASIA REGION

Requirement:

EACH USER SHOULD ACCESS DYNAMODB LOCALLY

Think:

GLOBAL TABLES

This avoids forcing all users to access:

ONE DISTANT REGION

### Memory Trick

USERS WORLDWIDE

↓

TABLES WORLDWIDE

---

## Write Architecture

Imagine:

USER A

↓

WRITE ITEM

↓

REGION A TABLE

↓

REPLICATION

↓

REGION B TABLE

At the same time:

USER B

↓

WRITE ITEM

↓

REGION B TABLE

↓

REPLICATION

↓

REGION A TABLE

This is:

ACTIVE-ACTIVE

### Memory Trick

WRITE BOTH SIDES

=

GLOBAL TABLE

---

## Read Architecture

Imagine:

USER A

↓

READ REGION A

and:

USER B

↓

READ REGION B

Each application accesses:

A NEARBY REGIONAL TABLE

This provides:

LOW-LATENCY ACCESS

### Memory Trick

READ NEAR USER

=

GLOBAL TABLES

---

## When Should You Think Global Tables?

Look for:

DYNAMODB

+

MULTIPLE REGIONS

+

LOW LATENCY

+

ACTIVE-ACTIVE

+

READ / WRITE IN ANY REGION

These requirements strongly point toward:

DYNAMODB GLOBAL TABLES

### Memory Trick

DYNAMODB + GLOBAL

=

GLOBAL TABLES

---

## Scenario Recognition

Need DynamoDB available with low latency across multiple Regions?

→ DynamoDB Global Tables

---

Need Active-Active DynamoDB replication?

→ DynamoDB Global Tables

---

Need applications to read from DynamoDB in multiple Regions?

→ DynamoDB Global Tables

---

Need applications to write to DynamoDB in multiple Regions?

→ DynamoDB Global Tables

---

Need two-way DynamoDB replication?

→ DynamoDB Global Tables

---

Need a DynamoDB database for globally distributed users?

→ DynamoDB Global Tables

---

Need a prerequisite for DynamoDB Global Tables?

→ DynamoDB Streams

---

Need to capture individual DynamoDB create/update/delete events?

→ [[DynamoDB Streams]]

---

Need microsecond cached DynamoDB reads?

→ [[DAX]]

---

Need a single-Region DynamoDB table?

→ [[DynamoDB Overview]]

NOT necessarily Global Tables

---

## Exam Traps

GLOBAL TABLES

=

MULTI-REGION

---

GLOBAL TABLES

=

LOW-LATENCY GLOBAL ACCESS

---

GLOBAL TABLES

=

ACTIVE-ACTIVE

---

ACTIVE-ACTIVE

=

READ + WRITE IN ANY REGION

---

GLOBAL TABLES

=

TWO-WAY REPLICATION

---

DYNAMODB STREAMS

=

PREREQUISITE

---

GLOBAL TABLES

≠

DAX

---

DAX

=

CACHE

GLOBAL TABLES

=

MULTI-REGION

---

GLOBAL TABLES

≠

DYNAMODB STREAMS

---

STREAMS

=

CAPTURE CHANGES

GLOBAL TABLES

=

REPLICATE ACROSS REGIONS

---

GLOBAL TABLES

≠

READ-ONLY REPLICAS

---

GLOBAL TABLES

=

WRITES IN MULTIPLE REGIONS

---

## Quick Cheat Sheet

DYNAMODB GLOBAL TABLES

=

MULTI-REGION DYNAMODB

PRIMARY PURPOSE

=

LOW-LATENCY GLOBAL ACCESS

REPLICATION

=

ACTIVE-ACTIVE

DIRECTION

=

TWO-WAY

READS

=

ANY PARTICIPATING REGION

WRITES

=

ANY PARTICIPATING REGION

PREREQUISITE

=

DYNAMODB STREAMS

GLOBAL USERS

=

LOCAL REGIONAL ACCESS

DAX

=

CACHE

STREAMS

=

CHANGE EVENTS

GLOBAL TABLES

=

MULTI-REGION DATABASE

---

## Master Memory Trick

GLOBAL TABLES

=

DYNAMODB

↓

MULTIPLE REGIONS

↓

ACTIVE-ACTIVE

↓

READ + WRITE ANYWHERE

Think:

REGION A

↔

REGION B

And remember:

DYNAMODB STREAMS

↓

REQUIRED FIRST

↓

GLOBAL TABLES

### Final Rule

QUESTION SAYS:

DYNAMODB

+

MULTIPLE REGIONS

+

LOW LATENCY

↓

GLOBAL TABLES

QUESTION SAYS:

ACTIVE-ACTIVE

+

READ AND WRITE IN ANY REGION

↓

GLOBAL TABLES

QUESTION SAYS:

GLOBAL TABLE PREREQUISITE

↓

DYNAMODB STREAMS

---

## Related Notes

- [[DynamoDB Overview]]
- [[DynamoDB Primary Keys]]
- [[DynamoDB Capacity Modes]]
- [[DAX]]
- [[DynamoDB Streams]]
- [[DynamoDB TTL]]
- [[02-Compute/Lambda]]
- [[SAA Databases Cheat Sheet]]
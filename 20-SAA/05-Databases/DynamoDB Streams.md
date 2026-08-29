## What Problem Does It Solve?

Applications sometimes need to:

REACT

when data changes inside:

DYNAMODB

Think:

ITEM CREATED

↓

ITEM UPDATED

↓

ITEM DELETED

↓

APPLICATION SHOULD DO SOMETHING

DynamoDB Streams captures those:

ITEM-LEVEL MODIFICATIONS

so downstream services can process them.

### Memory Trick

DYNAMODB STREAMS

=

REACT TO TABLE CHANGES

---

## What Is DynamoDB Streams?

DynamoDB Streams creates an:

ORDERED STREAM

of:

ITEM-LEVEL MODIFICATIONS

from a DynamoDB table.

Think:

[[DynamoDB Overview]]

↓

CREATE

UPDATE

DELETE

↓

[[DynamoDB Streams]]

↓

PROCESS CHANGE

### Memory Trick

DYNAMODB STREAM

=

CHANGE LOG

---

## What Changes Are Captured?

The SAA slides specifically highlight:

CREATE

↓

UPDATE

↓

DELETE

Think:

DYNAMODB ITEM CHANGES

↓

STREAM RECORDS

These changes can then be processed by:

DOWNSTREAM APPLICATIONS

### Memory Trick

CRUD CHANGES

↓

STREAM

---

## Ordered Stream

DynamoDB Streams provides an:

ORDERED STREAM

of modifications.

Think:

CHANGE #1

↓

CHANGE #2

↓

CHANGE #3

The stream preserves the sequence of changes for processing.

### Memory Trick

STREAM

=

ORDERED CHANGES

---

## Basic Architecture

Think:

APPLICATION

↓

DYNAMODB TABLE

↓

CREATE / UPDATE / DELETE

↓

DYNAMODB STREAM

↓

PROCESSING LAYER

The processing layer can then:

FILTER

↓

TRANSFORM

↓

NOTIFY

↓

ARCHIVE

↓

INDEX

### Memory Trick

TABLE CHANGE

↓

STREAM

↓

ACTION

---

## React to Changes in Real Time

One major use case is:

REAL-TIME REACTION

Think:

NEW USER CREATED

↓

DYNAMODB STREAM

↓

PROCESS EVENT

↓

SEND WELCOME EMAIL

This is a specific example highlighted in the course.

### Memory Trick

NEW USER

↓

STREAM

↓

WELCOME EMAIL

---

## Lambda Integration

DynamoDB Streams can invoke:

[[02-Compute/Lambda]]

when table changes occur.

Think:

DYNAMODB ITEM CHANGED

↓

DYNAMODB STREAM

↓

LAMBDA

↓

CUSTOM LOGIC

### Memory Trick

DYNAMODB CHANGE

=

LAMBDA TRIGGER

---

## Lambda Architecture

Example:

APPLICATION

↓

DYNAMODB TABLE

↓

ITEM CREATED

↓

DYNAMODB STREAM

↓

LAMBDA

↓

PROCESS EVENT

This allows you to build:

EVENT-DRIVEN APPLICATIONS

### Memory Trick

TABLE EVENT

↓

LAMBDA FUNCTION

---

## Welcome Email Scenario

Suppose:

NEW USER

is inserted into DynamoDB.

Think:

USER ITEM CREATED

↓

DYNAMODB STREAM

↓

LAMBDA

↓

SEND WELCOME EMAIL

The application does not need to continuously:

POLL THE TABLE

for new users.

### Memory Trick

CREATE USER

↓

STREAM

↓

EMAIL

---

## Real-Time Usage Analytics

Another course use case is:

REAL-TIME USAGE ANALYTICS

Think:

APPLICATION ACTIVITY

↓

DYNAMODB CHANGES

↓

STREAM

↓

ANALYTICS PROCESSING

This lets downstream systems analyze:

TABLE CHANGES

as they happen.

### Memory Trick

DYNAMODB CHANGES

=

REAL-TIME ANALYTICS INPUT

---

## Derivative Tables

DynamoDB Streams can be used to:

INSERT DATA

into:

DERIVATIVE TABLES

Think:

SOURCE TABLE

↓

STREAM

↓

PROCESSING

↓

DERIVED TABLE

This can help create:

SECONDARY DATA MODELS

based on changes to the original table.

### Memory Trick

SOURCE CHANGE

↓

BUILD DERIVED DATA

---

## Cross-Region Replication

The slides also identify:

CROSS-REGION REPLICATION

as a DynamoDB Streams use case.

Think:

REGION A

↓

DYNAMODB CHANGES

↓

STREAM

↓

REGION B

This concept connects with:

[[DynamoDB Global Tables]]

### Memory Trick

STREAM

=

CHANGE REPLICATION SOURCE

---

## DynamoDB Streams Retention

DynamoDB Streams retains records for:

24 HOURS

Think:

CHANGE HAPPENS

↓

STREAM RECORD

↓

AVAILABLE FOR 24 HOURS

### Memory Trick

DYNAMODB STREAMS

=

24 HOURS

---

## Limited Number of Consumers

The SAA slides emphasize that DynamoDB Streams supports a:

LIMITED NUMBER OF CONSUMERS

Think:

DYNAMODB STREAMS

↓

SMALLER NUMBER OF CONSUMERS

If the architecture requires:

MORE CONSUMERS

the course points toward:

KINESIS DATA STREAMS

### Memory Trick

DYNAMODB STREAM

=

LIMITED CONSUMERS

---

## Processing DynamoDB Streams

The slides highlight two primary processing options:

AWS LAMBDA TRIGGERS

or:

DYNAMODB STREAM KINESIS ADAPTER

Think:

DYNAMODB STREAM

↓

LAMBDA

or:

↓

KINESIS ADAPTER

### Memory Trick

PROCESS STREAM

=

LAMBDA OR KINESIS ADAPTER

---

## KCL Adapter

The architecture slide shows a:

DYNAMODB KCL ADAPTER

between:

DYNAMODB STREAMS

and:

PROCESSING APPLICATIONS

Think:

DYNAMODB STREAM

↓

KCL ADAPTER

↓

PROCESSING LAYER

This provides another way to consume:

STREAM RECORDS

### Memory Trick

KCL ADAPTER

=

PROCESS DYNAMODB STREAM DATA

---

## DynamoDB Streams vs Kinesis Data Streams

The course compares:

DYNAMODB STREAMS

and:

KINESIS DATA STREAMS

### DynamoDB Streams

RETENTION

=

24 HOURS

CONSUMERS

=

LIMITED

PROCESSING

=

LAMBDA TRIGGERS / KINESIS ADAPTER

---

### Kinesis Data Streams

RETENTION

=

UP TO 1 YEAR

CONSUMERS

=

HIGH NUMBER

PROCESSING OPTIONS

=

MORE EXTENSIVE

Think:

SHORTER + FEWER

↓

DYNAMODB STREAMS

LONGER + MORE

↓

KINESIS DATA STREAMS

### Memory Trick

24 HOURS

=

DYNAMODB STREAMS

1 YEAR

=

KINESIS DATA STREAMS

---

## Kinesis Data Streams Option

The SAA slides describe:

KINESIS DATA STREAMS

as the:

NEWER

streaming option for DynamoDB.

It supports:

LONGER RETENTION

↓

MORE CONSUMERS

↓

MORE PROCESSING OPTIONS

Think:

NEED MORE STREAMING SCALE?

↓

KINESIS DATA STREAMS

### Memory Trick

MORE CONSUMERS

=

KINESIS

---

## Kinesis Data Streams Processing

The slides highlight several downstream services for:

KINESIS DATA STREAMS

including:

[[02-Compute/Lambda]]

↓

KINESIS DATA ANALYTICS

↓

KINESIS DATA FIREHOSE

↓

AWS GLUE STREAMING ETL

Think:

KINESIS

=

BROADER STREAM PROCESSING

---

## SNS Integration

The architecture slide shows:

[[SNS]]

as a possible downstream destination.

Think:

DYNAMODB CHANGE

↓

STREAM

↓

PROCESSING

↓

SNS

↓

MESSAGING / NOTIFICATIONS

### Memory Trick

CHANGE

↓

STREAM

↓

NOTIFY

---

## Firehose Integration

The architecture also shows:

KINESIS DATA FIREHOSE

as a downstream processing path.

Think:

DYNAMODB STREAM

↓

PROCESSING

↓

FIREHOSE

↓

DESTINATION

This can help move streaming data into:

ANALYTICS

or:

ARCHIVAL SYSTEMS

---

## Redshift Integration

The slide architecture shows:

[[04-Databases/Redshift]]

as a possible destination for:

ANALYTICS

Think:

DYNAMODB CHANGES

↓

STREAM PROCESSING

↓

REDSHIFT

↓

ANALYTICS

### Memory Trick

STREAM DATA

↓

REDSHIFT ANALYTICS

---

## S3 Integration

The architecture slide shows:

[[S3]]

for:

ARCHIVING

Think:

DYNAMODB CHANGES

↓

STREAM

↓

PROCESSING

↓

S3

↓

ARCHIVE

### Memory Trick

STREAM

↓

S3

=

ARCHIVE

---

## OpenSearch Integration

The slide also shows:

[[20-SAA/05-Databases/OpenSearch]]

for:

INDEXING

Think:

DYNAMODB CHANGE

↓

STREAM

↓

PROCESSING

↓

OPENSEARCH

↓

SEARCH INDEX UPDATED

### Memory Trick

DYNAMODB CHANGE

↓

OPENSEARCH INDEX

---

## Filtering and Transforming

The architecture slide highlights:

FILTERING

and:

TRANSFORMING

DynamoDB stream data.

Think:

RAW TABLE CHANGE

↓

PROCESSING LAYER

↓

FILTER

↓

TRANSFORM

↓

DESTINATION

This enables downstream systems to receive:

ONLY THE DATA THEY NEED

### Memory Trick

STREAM

=

CHANGE DATA PIPELINE

---

## Event-Driven Architecture

DynamoDB Streams helps create:

EVENT-DRIVEN ARCHITECTURES

Think:

DYNAMODB CHANGE

↓

EVENT

↓

PROCESSING

↓

ACTION

Instead of:

APPLICATION CONSTANTLY CHECKING TABLE

you can:

REACT WHEN CHANGE OCCURS

### Memory Trick

POLLING?

↓

NO

EVENT?

↓

YES

---

## DynamoDB Streams vs DAX

Do not confuse:

[[DAX]]

with:

[[DynamoDB Streams]]

### DAX

Purpose:

CACHE READS

Think:

FASTER READ PERFORMANCE

---

### DynamoDB Streams

Purpose:

CAPTURE CHANGES

Think:

CREATE / UPDATE / DELETE EVENTS

### Memory Trick

DAX

=

READ FAST

STREAMS

=

REACT TO CHANGES

---

## DynamoDB Streams vs Global Tables

Do not confuse:

[[DynamoDB Streams]]

with:

[[DynamoDB Global Tables]]

### DynamoDB Streams

Purpose:

CAPTURE ITEM CHANGES

---

### Global Tables

Purpose:

MULTI-REGION ACTIVE-ACTIVE DATABASE

The Global Tables slide requires:

DYNAMODB STREAMS

as a prerequisite.

Think:

STREAMS

=

CHANGE FEED

GLOBAL TABLES

=

MULTI-REGION DATABASE

### Memory Trick

STREAMS

=

EVENTS

GLOBAL TABLES

=

REGIONS

---

## DynamoDB Streams vs Application Polling

Without Streams:

APPLICATION

↓

CHECK TABLE

↓

CHECK AGAIN

↓

CHECK AGAIN

This is:

POLLING

With Streams:

DYNAMODB CHANGE

↓

STREAM RECORD

↓

PROCESSOR

Think:

CHANGE PUSHED INTO STREAM

instead of:

CONSTANT TABLE CHECKING

### Memory Trick

STREAM

=

REACT

NOT:

POLL

---

## Architecture Thinking

Imagine:

APPLICATION

↓

DYNAMODB TABLE

↓

CREATE / UPDATE / DELETE

↓

DYNAMODB STREAMS

Then:

PROCESSING LAYER

↓

LAMBDA

↓

SNS

or:

↓

FIREHOSE

↓

S3 / REDSHIFT / OPENSEARCH

Think:

DATABASE CHANGE

↓

STREAM

↓

PROCESS

↓

DESTINATION

---

## Scenario Recognition

Need to react when a DynamoDB item is created?

→ DynamoDB Streams

---

Need to react when a DynamoDB item is updated?

→ DynamoDB Streams

---

Need to react when a DynamoDB item is deleted?

→ DynamoDB Streams

---

Need an ordered stream of item-level modifications?

→ DynamoDB Streams

---

Need to invoke Lambda after a DynamoDB change?

→ DynamoDB Streams

---

Need to send a welcome email after creating a user?

→ DynamoDB Streams + Lambda

---

Need real-time usage analytics from DynamoDB changes?

→ DynamoDB Streams

---

Need to populate derivative tables?

→ DynamoDB Streams

---

Need cross-region replication based on changes?

→ DynamoDB Streams

---

Need stream records retained for 24 hours?

→ DynamoDB Streams

---

Need a higher number of consumers?

→ Kinesis Data Streams

---

Need stream retention up to 1 year?

→ Kinesis Data Streams

---

Need to archive DynamoDB change data to S3?

→ DynamoDB Streams / Kinesis processing → S3

---

Need to update a search index when DynamoDB changes?

→ DynamoDB Streams → OpenSearch

---

Need faster DynamoDB reads?

→ [[DAX]]

NOT DynamoDB Streams

---

## Exam Traps

DYNAMODB STREAMS

=

ORDERED ITEM-LEVEL MODIFICATIONS

---

CHANGES

=

CREATE

UPDATE

DELETE

---

RETENTION

=

24 HOURS

---

DYNAMODB STREAMS

=

LIMITED CONSUMERS

---

PROCESSING

=

LAMBDA TRIGGERS

or:

KINESIS ADAPTER

---

KINESIS DATA STREAMS

=

UP TO 1 YEAR RETENTION

---

KINESIS DATA STREAMS

=

HIGH NUMBER OF CONSUMERS

---

DYNAMODB STREAMS

≠

DAX

---

DAX

=

READ CACHE

DYNAMODB STREAMS

=

CHANGE EVENTS

---

DYNAMODB STREAMS

≠

GLOBAL TABLES

---

GLOBAL TABLES

=

MULTI-REGION ACTIVE-ACTIVE

---

DYNAMODB STREAMS

=

REAL-TIME REACTION TO DATA CHANGES

---

## Quick Cheat Sheet

DYNAMODB STREAMS

=

ITEM CHANGE STREAM

ORDER

=

ORDERED

EVENT TYPES

=

CREATE

UPDATE

DELETE

RETENTION

=

24 HOURS

CONSUMERS

=

LIMITED

LAMBDA

=

SUPPORTED

KINESIS ADAPTER

=

SUPPORTED

USE CASES

=

REAL-TIME REACTIONS

ANALYTICS

DERIVATIVE TABLES

CROSS-REGION REPLICATION

LAMBDA TRIGGERS

KINESIS DATA STREAMS

=

NEWER OPTION

KINESIS RETENTION

=

UP TO 1 YEAR

KINESIS CONSUMERS

=

HIGH NUMBER

S3

=

ARCHIVING

REDSHIFT

=

ANALYTICS

OPENSEARCH

=

INDEXING

SNS

=

MESSAGING / NOTIFICATIONS

---

## Master Memory Trick

DYNAMODB TABLE

↓

CREATE / UPDATE / DELETE

↓

DYNAMODB STREAM

↓

PROCESS EVENT

Then remember:

24 HOURS

=

DYNAMODB STREAMS

UP TO 1 YEAR

=

KINESIS DATA STREAMS

And:

NEW USER

↓

STREAM

↓

LAMBDA

↓

WELCOME EMAIL

### Final Rule

QUESTION SAYS:

DYNAMODB ITEM CHANGED

+

DO SOMETHING AUTOMATICALLY

↓

DYNAMODB STREAMS

QUESTION SAYS:

NEED MORE CONSUMERS

+

LONGER STREAM RETENTION

↓

KINESIS DATA STREAMS

QUESTION SAYS:

FASTER DYNAMODB READS

↓

DAX

---

## Related Notes

- [[DynamoDB Overview]]
- [[DynamoDB Primary Keys]]
- [[DynamoDB Capacity Modes]]
- [[DAX]]
- [[DynamoDB Global Tables]]
- [[02-Compute/Lambda]]
- [[SNS]]
- [[S3]]
- [[04-Databases/Redshift]]
- [[20-SAA/05-Databases/OpenSearch]]
- [[SAA Databases Cheat Sheet]]
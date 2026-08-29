## What Problem Does It Solve?

Sometimes DynamoDB data needs to move between:

DYNAMODB

and:

S3

You may need to:

EXPORT TABLE DATA

for:

ANALYSIS

↓

BACKUP / ARCHIVAL

↓

DATA PROCESSING

Or you may need to:

IMPORT DATA

from S3 into:

A NEW DYNAMODB TABLE

Think:

DYNAMODB

↓

EXPORT

↓

S3

or:

S3

↓

IMPORT

↓

DYNAMODB

### Memory Trick

DYNAMODB + S3

=

EXPORT OR IMPORT

---

## DynamoDB Integration with S3

DynamoDB supports:

EXPORT TO S3

and:

IMPORT FROM S3

Think:

DYNAMODB

↓

[[S3]]

and:

[[S3]]

↓

DYNAMODB

These operations provide ways to move DynamoDB data without consuming normal table:

READ / WRITE CAPACITY

### Memory Trick

DYNAMODB ↔ S3

=

DATA MOVEMENT

---

## Export to S3

DynamoDB can:

EXPORT TABLE DATA

to:

[[S3]]

Think:

DYNAMODB TABLE

↓

EXPORT

↓

S3 BUCKET

This can be useful for:

ANALYTICS

↓

DATA PROCESSING

↓

ARCHIVAL

### Memory Trick

EXPORT

=

DYNAMODB → S3

---

## Export Requires PITR

This is an important exam point.

To export DynamoDB table data to S3:

POINT-IN-TIME RECOVERY

must be:

ENABLED

Think:

ENABLE PITR

↓

EXPORT TABLE

↓

S3

This connects directly with:

[[DynamoDB Backups]]

### Memory Trick

EXPORT TO S3

NEEDS:

PITR

---

## Export Any Point Within PITR Window

The SAA slide states that you can export:

ANY POINT IN TIME

within the:

PITR WINDOW

Think:

DYNAMODB TABLE HISTORY

↓

SELECT POINT IN TIME

↓

EXPORT

↓

S3

This means the export does not have to represent only:

THE CURRENT TABLE STATE

### Memory Trick

PITR HISTORY

↓

EXPORT TO S3

---

## Export Does Not Consume Read Capacity

This is a major SAA exam distinction.

Exporting DynamoDB data to S3 does:

NOT

consume:

READ CAPACITY

Think:

DYNAMODB EXPORT

↓

S3

while:

TABLE READ CAPACITY

=

UNAFFECTED

### Memory Trick

EXPORT

=

NO RCU CONSUMED

---

## Why No Read Capacity Impact Matters

Imagine a DynamoDB table serving:

PRODUCTION TRAFFIC

The company needs to export table data for:

ANALYTICS

Requirement:

DO NOT CONSUME TABLE READ CAPACITY

Answer:

DYNAMODB EXPORT TO S3

Think:

LIVE TABLE

↓

EXPORT

↓

S3

without consuming:

NORMAL READ CAPACITY

### Memory Trick

EXPORT DATA

WITHOUT:

RCU IMPACT

---

## Export Formats

The SAA slide identifies two export formats:

DYNAMODB JSON

and:

ION

Think:

DYNAMODB

↓

EXPORT

↓

DYNAMODB JSON

or:

ION

### Memory Trick

EXPORT FORMAT

=

DYNAMODB JSON OR ION

---

## DynamoDB JSON

One export format is:

DYNAMODB JSON

Think:

DYNAMODB DATA

↓

JSON REPRESENTATION

↓

S3

This format preserves DynamoDB-oriented data representation.

### Memory Trick

DYNAMODB EXPORT

↓

DYNAMODB JSON

---

## Ion Format

DynamoDB exports can also use:

ION

Think:

DYNAMODB

↓

ION FORMAT

↓

S3

For the exam, remember the slide-supported pairing:

DYNAMODB JSON

or:

ION

### Memory Trick

EXPORT

=

JSON OR ION

---

## Analyze Exported Data with Athena

After exporting DynamoDB data to:

[[S3]]

you can analyze it using:

[[09-Analytics/Athena]]

Think:

DYNAMODB

↓

EXPORT

↓

S3

↓

ATHENA

↓

SQL ANALYSIS

This is an important architecture pattern.

### Memory Trick

DYNAMODB EXPORT

↓

S3

↓

ATHENA

---

## Export Analytics Architecture

Think:

PRODUCTION APPLICATION

↓

DYNAMODB

↓

EXPORT TO S3

↓

ATHENA

↓

ANALYTICS

This separates:

OPERATIONAL DATABASE TRAFFIC

from:

ANALYTICAL QUERIES

### Memory Trick

DYNAMODB

=

OPERATIONS

S3 + ATHENA

=

ANALYTICS

---

## Export Scenario

A company stores application data in:

DYNAMODB

Analysts need to perform:

SQL QUERIES

against historical table data.

Requirement:

DO NOT CONSUME DYNAMODB READ CAPACITY

Architecture:

DYNAMODB

↓

EXPORT TO S3

↓

[[09-Analytics/Athena]]

### Memory Trick

DYNAMODB ANALYTICS

WITHOUT RCU IMPACT

=

EXPORT + ATHENA

---

## Import from S3

DynamoDB can also:

IMPORT DATA

from:

[[S3]]

Think:

S3 BUCKET

↓

IMPORT

↓

NEW DYNAMODB TABLE

### Memory Trick

IMPORT

=

S3 → DYNAMODB

---

## Import Creates a New Table

This is a major exam point.

Importing data from S3 creates:

A NEW DYNAMODB TABLE

Think:

S3 DATA

↓

IMPORT

↓

NEW TABLE

It does not simply:

APPEND DATA

to an existing DynamoDB table.

### Memory Trick

IMPORT FROM S3

=

NEW TABLE

---

## Import Does Not Consume Write Capacity

Importing data from S3 does:

NOT

consume:

WRITE CAPACITY

Think:

S3

↓

IMPORT

↓

NEW DYNAMODB TABLE

while:

TABLE WRITE CAPACITY

=

UNAFFECTED

### Memory Trick

IMPORT

=

NO WCU CONSUMED

---

## Export vs Import Capacity

This is an excellent exam pairing.

### Export to S3

Does not consume:

READ CAPACITY

Think:

EXPORT

=

NO RCU

---

### Import from S3

Does not consume:

WRITE CAPACITY

Think:

IMPORT

=

NO WCU

### Memory Trick

EXPORT

↓

NO READ CAPACITY

IMPORT

↓

NO WRITE CAPACITY

---

## Import Formats

The SAA slide identifies these import formats:

CSV

↓

DYNAMODB JSON

↓

ION

Think:

S3 FILE

↓

CSV

or:

DYNAMODB JSON

or:

ION

↓

DYNAMODB IMPORT

### Memory Trick

IMPORT

=

CSV + DYNAMODB JSON + ION

---

## Export vs Import Formats

### Export

Supports:

DYNAMODB JSON

and:

ION

---

### Import

Supports:

CSV

DYNAMODB JSON

ION

### Memory Trick

CSV

=

IMPORT OPTION

Export slide formats:

JSON + ION

---

## Import Errors

When errors occur during:

IMPORT FROM S3

the SAA slide states they are logged to:

[[CloudWatch Logs]]

Think:

S3

↓

IMPORT

↓

ERROR

↓

CLOUDWATCH LOGS

### Memory Trick

IMPORT ERROR

=

CLOUDWATCH LOGS

---

## Import Error Architecture

Think:

S3 DATA

↓

DYNAMODB IMPORT

↓

SUCCESS

↓

NEW TABLE

or:

ERROR

↓

[[CloudWatch Logs]]

This gives you a location to investigate:

IMPORT PROBLEMS

### Memory Trick

IMPORT FAILED?

↓

CHECK CLOUDWATCH LOGS

---

## Bulk Data Import Scenario

Suppose a company has a large dataset stored in:

S3

Requirement:

CREATE A DYNAMODB TABLE

from that data without consuming:

NORMAL WRITE CAPACITY

Think:

S3

↓

IMPORT

↓

NEW DYNAMODB TABLE

### Memory Trick

S3 DATA

+

NEW DYNAMODB TABLE

=

IMPORT

---

## Export vs DynamoDB Backups

Do not confuse:

EXPORT TO S3

with:

[[DynamoDB Backups]]

### DynamoDB Backups

Purpose:

RECOVERY

Think:

PITR

or:

ON-DEMAND BACKUP

---

### Export to S3

Purpose:

MOVE TABLE DATA TO S3

Think:

ANALYTICS

↓

PROCESSING

↓

ARCHIVAL

### Memory Trick

BACKUP

=

RECOVER TABLE

EXPORT

=

USE DATA IN S3

---

## PITR Relationship

PITR appears in both:

[[DynamoDB Backups]]

and:

DYNAMODB EXPORT TO S3

For backups:

PITR

=

CONTINUOUS RECOVERY

For export:

PITR

=

REQUIRED FOR EXPORT

Think:

PITR

↓

TABLE HISTORY

↓

EXPORT POINT IN TIME

### Memory Trick

EXPORT NEEDS PITR

---

## Export vs Restore

Do not confuse:

EXPORT

with:

RESTORE

### Restore

[[DynamoDB Backups]]

↓

RESTORE

↓

NEW DYNAMODB TABLE

---

### Export

DYNAMODB

↓

EXPORT

↓

S3

Think:

RESTORE

=

BACK TO DYNAMODB

EXPORT

=

OUT TO S3

### Memory Trick

RESTORE

=

NEW TABLE

EXPORT

=

S3 FILES

---

## Import vs Restore

Both can result in:

A NEW DYNAMODB TABLE

But they start from different sources.

### Restore

Source:

DYNAMODB BACKUP

↓

NEW TABLE

---

### Import

Source:

S3 DATA

↓

NEW TABLE

### Memory Trick

BACKUP SOURCE

=

RESTORE

S3 SOURCE

=

IMPORT

---

## Export vs DynamoDB Streams

Do not confuse:

DYNAMODB EXPORT

with:

[[DynamoDB Streams]]

### Export

Purpose:

MOVE TABLE DATA TO S3

---

### Streams

Purpose:

CAPTURE ITEM-LEVEL CHANGES

Think:

EXPORT

=

DATASET

STREAMS

=

CHANGE EVENTS

### Memory Trick

EXPORT

=

TABLE DATA

STREAMS

=

TABLE CHANGES

---

## Integration Architecture

Think:

DYNAMODB

↓

PITR ENABLED

↓

EXPORT

↓

S3

↓

ATHENA

For the reverse direction:

S3

↓

CSV / DYNAMODB JSON / ION

↓

IMPORT

↓

NEW DYNAMODB TABLE

If import fails:

↓

CLOUDWATCH LOGS

### Memory Trick

DYNAMODB

↓

S3

=

EXPORT

S3

↓

DYNAMODB

=

IMPORT

---

## Scenario Recognition

Need to export DynamoDB data to S3?

→ DynamoDB Export to S3

---

What must be enabled before exporting?

→ PITR

---

Need to export a previous point in time?

→ PITR + Export to S3

---

Need export without consuming DynamoDB read capacity?

→ Export to S3

---

Need to analyze exported DynamoDB data using SQL?

→ S3 + Athena

---

Need DynamoDB export format?

→ DynamoDB JSON or Ion

---

Need to import S3 data into DynamoDB?

→ DynamoDB Import from S3

---

What does S3 import create?

→ A NEW DYNAMODB TABLE

---

Need import without consuming DynamoDB write capacity?

→ Import from S3

---

Need CSV data imported into DynamoDB?

→ Import from S3

---

Need to troubleshoot DynamoDB import errors?

→ CloudWatch Logs

---

Need continuous recovery for the last 35 days?

→ [[DynamoDB Backups]]

---

Need to react to item-level table changes?

→ [[DynamoDB Streams]]

---

## Exam Traps

EXPORT TO S3

=

REQUIRES PITR

---

EXPORT

=

ANY POINT WITHIN PITR WINDOW

---

EXPORT

=

NO READ CAPACITY CONSUMED

---

EXPORT FORMATS

=

DYNAMODB JSON

+

ION

---

EXPORTED DATA

=

CAN BE ANALYZED WITH ATHENA

---

IMPORT FROM S3

=

CREATES NEW TABLE

---

IMPORT

=

NO WRITE CAPACITY CONSUMED

---

IMPORT FORMATS

=

CSV

+

DYNAMODB JSON

+

ION

---

IMPORT ERRORS

=

CLOUDWATCH LOGS

---

EXPORT

≠

BACKUP RESTORE

---

IMPORT

≠

WRITE INTO EXISTING TABLE

---

EXPORT

≠

DYNAMODB STREAMS

---

## Quick Cheat Sheet

DYNAMODB + S3

=

EXPORT + IMPORT

EXPORT DIRECTION

=

DYNAMODB → S3

EXPORT REQUIREMENT

=

PITR ENABLED

EXPORT POINT

=

ANY POINT WITHIN PITR WINDOW

EXPORT CAPACITY IMPACT

=

NO READ CAPACITY

EXPORT FORMATS

=

DYNAMODB JSON + ION

EXPORT ANALYTICS

=

ATHENA

IMPORT DIRECTION

=

S3 → DYNAMODB

IMPORT RESULT

=

NEW TABLE

IMPORT CAPACITY IMPACT

=

NO WRITE CAPACITY

IMPORT FORMATS

=

CSV + DYNAMODB JSON + ION

IMPORT ERRORS

=

CLOUDWATCH LOGS

BACKUPS

=

RECOVERY

STREAMS

=

CHANGE EVENTS

S3 INTEGRATION

=

DATA MOVEMENT

---

## Master Memory Trick

Think:

DYNAMODB

↓

S3

=

EXPORT

Then remember:

EXPORT

↓

PITR REQUIRED

↓

NO RCU

↓

ATHENA ANALYSIS

Reverse it:

S3

↓

DYNAMODB

=

IMPORT

Then remember:

IMPORT

↓

NEW TABLE

↓

NO WCU

↓

ERRORS IN CLOUDWATCH LOGS

### Final Rule

QUESTION SAYS:

DYNAMODB DATA

+

S3

+

ANALYTICS

↓

EXPORT TO S3

QUESTION SAYS:

EXPORT WITHOUT READ CAPACITY IMPACT

↓

DYNAMODB EXPORT

QUESTION SAYS:

S3 DATA

+

CREATE NEW DYNAMODB TABLE

↓

IMPORT FROM S3

QUESTION SAYS:

IMPORT WITHOUT WRITE CAPACITY IMPACT

↓

DYNAMODB IMPORT

---

## Related Notes

- [[DynamoDB Overview]]
- [[DynamoDB Capacity Modes]]
- [[DynamoDB Backups]]
- [[DynamoDB Streams]]
- [[DynamoDB Global Tables]]
- [[DynamoDB TTL]]
- [[S3]]
- [[09-Analytics/Athena]]
- [[CloudWatch Logs]]
- [[SAA Databases Cheat Sheet]]
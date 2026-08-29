## What Problem Does It Solve?

DynamoDB data may need to be recovered because of:

ACCIDENTAL DELETION

↓

APPLICATION ERRORS

↓

DATA CORRUPTION

↓

DISASTER RECOVERY EVENTS

DynamoDB provides backup capabilities that allow you to:

RESTORE DATA

from an earlier point in time.

Think:

DYNAMODB TABLE

↓

BACKUP

↓

DATA LOSS / ERROR

↓

RESTORE

### Memory Trick

DYNAMODB BACKUPS

=

RECOVER LOST DATA

---

## DynamoDB Backup Options

The SAA course highlights two main backup approaches:

CONTINUOUS BACKUPS

using:

POINT-IN-TIME RECOVERY

and:

ON-DEMAND BACKUPS

Think:

CONTINUOUS

↓

PITR

MANUAL / LONG-TERM

↓

ON-DEMAND BACKUP

### Memory Trick

DYNAMODB BACKUPS

=

PITR + ON-DEMAND

---

## Point-in-Time Recovery

PITR stands for:

POINT-IN-TIME RECOVERY

It uses:

CONTINUOUS BACKUPS

Think:

DYNAMODB TABLE

↓

CONTINUOUS BACKUP

↓

CHOOSE RECOVERY TIME

↓

RESTORE TABLE

### Memory Trick

PITR

=

GO BACK IN TIME

---

## PITR Backup Window

The SAA slides specify a PITR backup window of:

35 DAYS

Think:

TODAY

↓

GO BACK TO A POINT

within:

LAST 35 DAYS

### Memory Trick

PITR

=

35 DAYS

---

## PITR Is Optional

Point-in-Time Recovery must be:

ENABLED

for the table.

Think:

DYNAMODB TABLE

↓

ENABLE PITR

↓

CONTINUOUS BACKUPS

### Memory Trick

WANT POINT-IN-TIME RECOVERY?

↓

ENABLE PITR

---

## Recover to a Specific Time

PITR allows recovery to:

ANY POINT IN TIME

within the available:

BACKUP WINDOW

Think:

PROBLEM OCCURRED

↓

2:15 PM

Need table state from:

2:14 PM

↓

PITR

The key concept is:

RECOVER FROM A SPECIFIC POINT

rather than simply using one manually created backup.

### Memory Trick

SPECIFIC RECOVERY TIME

=

PITR

---

## PITR Restore Creates a New Table

This is a major exam point.

When you restore using:

POINT-IN-TIME RECOVERY

DynamoDB creates:

A NEW TABLE

Think:

ORIGINAL TABLE

↓

PITR RESTORE

↓

NEW TABLE

The existing table is not simply:

ROLLED BACK IN PLACE

### Memory Trick

DYNAMODB RESTORE

=

NEW TABLE

---

## On-Demand Backups

DynamoDB also supports:

ON-DEMAND BACKUPS

These are:

FULL BACKUPS

of the DynamoDB table.

Think:

DYNAMODB TABLE

↓

CREATE BACKUP

↓

FULL BACKUP

### Memory Trick

ON-DEMAND

=

FULL BACKUP NOW

---

## Long-Term Retention

On-Demand backups are useful for:

LONG-TERM RETENTION

The SAA slides state that they remain until:

EXPLICITLY DELETED

Think:

CREATE BACKUP

↓

KEEP

↓

KEEP

↓

KEEP

until:

YOU DELETE IT

### Memory Trick

ON-DEMAND BACKUP

=

KEEP UNTIL DELETED

---

## PITR vs On-Demand Backups

### PITR

Type:

CONTINUOUS BACKUPS

Recovery:

POINT IN TIME

Backup window:

35 DAYS

Best for:

RECENT RECOVERY

---

### On-Demand Backup

Type:

FULL BACKUP

Retention:

UNTIL EXPLICITLY DELETED

Best for:

LONG-TERM RETENTION

### Memory Trick

PITR

=

RECENT HISTORY

ON-DEMAND

=

LONG-TERM BACKUP

---

## On-Demand Restore Creates a New Table

Just like PITR:

RESTORING AN ON-DEMAND BACKUP

creates:

A NEW TABLE

Think:

BACKUP

↓

RESTORE

↓

NEW DYNAMODB TABLE

### Memory Trick

ANY DYNAMODB RESTORE

=

NEW TABLE

---

## Restore Behavior

For the exam, remember:

PITR RESTORE

↓

NEW TABLE

ON-DEMAND BACKUP RESTORE

↓

NEW TABLE

Think:

RESTORE

≠

OVERWRITE EXISTING TABLE

Instead:

RESTORE

=

CREATE NEW TABLE

### Memory Trick

RESTORE

=

NEW TABLE

---

## Backup Performance

DynamoDB backups do:

NOT AFFECT

table:

PERFORMANCE

or:

LATENCY

Think:

APPLICATION

↓

DYNAMODB

↓

NORMAL PERFORMANCE

while:

BACKUP OCCURS

### Memory Trick

BACKUP

=

NO PERFORMANCE HIT

---

## Why This Matters

Suppose a production DynamoDB table receives:

HEAVY APPLICATION TRAFFIC

The company needs to create a backup.

Requirement:

DO NOT DEGRADE APPLICATION PERFORMANCE

DynamoDB backups:

DO NOT AFFECT PERFORMANCE OR LATENCY

### Memory Trick

BACKUP WHILE LIVE

=

NO PERFORMANCE IMPACT

---

## AWS Backup Integration

DynamoDB backups can be:

CONFIGURED

and:

MANAGED

using:

[[AWS Backup]]

Think:

DYNAMODB

↓

AWS BACKUP

↓

CENTRALIZED BACKUP MANAGEMENT

### Memory Trick

CENTRAL BACKUP MANAGEMENT

=

AWS BACKUP

---

## Cross-Region Backup Copy

The SAA slides specifically highlight that:

AWS BACKUP

enables:

CROSS-REGION COPY

Think:

DYNAMODB BACKUP

↓

AWS BACKUP

↓

COPY

↓

ANOTHER REGION

This can support:

DISASTER RECOVERY

requirements.

### Memory Trick

CROSS-REGION BACKUP COPY

=

AWS BACKUP

---

## Disaster Recovery Scenario

A company wants to protect DynamoDB against:

DATA LOSS

Requirement:

RECOVER TABLE DATA

from a recent point in time.

Think:

ENABLE PITR

↓

CONTINUOUS BACKUPS

↓

RESTORE TO NEW TABLE

### Memory Trick

RECENT DR

=

PITR

---

## Long-Term Compliance Scenario

A company needs DynamoDB backups retained:

LONG TERM

The backups should remain until:

MANUALLY REMOVED

Think:

ON-DEMAND BACKUP

↓

KEEP UNTIL DELETED

### Memory Trick

LONG RETENTION

=

ON-DEMAND BACKUP

---

## Accidental Deletion Scenario

Imagine:

APPLICATION BUG

↓

DATA DELETED

The company discovers the problem later.

Need:

TABLE STATE BEFORE THE DELETION

Think:

PITR

↓

SELECT TIME BEFORE ERROR

↓

RESTORE

↓

NEW TABLE

### Memory Trick

OOPS

↓

PITR

---

## PITR vs TTL

Do not confuse:

POINT-IN-TIME RECOVERY

with:

[[DynamoDB TTL]]

### PITR

Purpose:

RECOVER DATA

Think:

BACKUP

↓

RESTORE

---

### TTL

Purpose:

AUTOMATICALLY DELETE EXPIRED DATA

Think:

EXPIRATION

↓

DELETE

### Memory Trick

PITR

=

BRING DATA BACK

TTL

=

REMOVE OLD DATA

---

## Backups vs DynamoDB Streams

Do not confuse:

[[DynamoDB Backups]]

with:

[[DynamoDB Streams]]

### Backups

Purpose:

DATA RECOVERY

---

### Streams

Purpose:

CAPTURE ITEM-LEVEL CHANGES

Think:

BACKUPS

=

RECOVER

STREAMS

=

REACT

### Memory Trick

BACKUP

=

RECOVERY

STREAM

=

EVENT

---

## Backups vs Global Tables

Do not confuse:

[[DynamoDB Backups]]

with:

[[DynamoDB Global Tables]]

### Backups

Purpose:

RECOVERY / RETENTION

---

### Global Tables

Purpose:

ACTIVE-ACTIVE MULTI-REGION DYNAMODB

Think:

BACKUPS

=

RECOVERY COPY

GLOBAL TABLES

=

LIVE MULTI-REGION DATABASE

### Memory Trick

BACKUP

=

RECOVER

GLOBAL TABLE

=

SERVE TRAFFIC

---

## Backups vs DAX

[[DAX]]

provides:

IN-MEMORY CACHING

for:

FASTER DYNAMODB READS

DynamoDB Backups provide:

DATA PROTECTION

and:

RECOVERY

Think:

DAX

=

PERFORMANCE

BACKUPS

=

RECOVERY

### Memory Trick

FAST READS

=

DAX

LOST DATA

=

BACKUPS

---

## Architecture Thinking

Think:

DYNAMODB TABLE

↓

ENABLE PITR

↓

CONTINUOUS BACKUPS

↓

PROBLEM OCCURS

↓

SELECT RECOVERY POINT

↓

RESTORE

↓

NEW TABLE

Or:

DYNAMODB TABLE

↓

ON-DEMAND BACKUP

↓

LONG-TERM RETENTION

↓

RESTORE

↓

NEW TABLE

### Memory Trick

BACKUP TYPE CHANGES

RESTORE RULE DOES NOT:

NEW TABLE

---

## Scenario Recognition

Need continuous DynamoDB backups?

→ PITR

---

Need point-in-time recovery?

→ PITR

---

Need recovery within the last 35 days?

→ PITR

---

Need to restore DynamoDB to a specific recent time?

→ PITR

---

Need a full DynamoDB backup?

→ On-Demand Backup

---

Need long-term backup retention?

→ On-Demand Backup

---

Need backup retained until explicitly deleted?

→ On-Demand Backup

---

Need backup without affecting table performance?

→ DynamoDB Backups

---

Need centralized DynamoDB backup management?

→ [[AWS Backup]]

---

Need cross-Region backup copy?

→ [[AWS Backup]]

---

What happens when a DynamoDB backup is restored?

→ A NEW TABLE IS CREATED

---

Need automatic deletion of expired items?

→ [[DynamoDB TTL]]

NOT Backups

---

Need multi-Region Active-Active DynamoDB?

→ [[DynamoDB Global Tables]]

NOT Backups

---

## Exam Traps

PITR

=

CONTINUOUS BACKUPS

---

PITR WINDOW

=

35 DAYS

---

PITR

=

OPTIONALLY ENABLED

---

PITR

=

RECOVER TO A POINT IN TIME

---

PITR RESTORE

=

NEW TABLE

---

ON-DEMAND BACKUP

=

FULL BACKUP

---

ON-DEMAND BACKUP

=

LONG-TERM RETENTION

---

ON-DEMAND BACKUP

=

RETAINED UNTIL EXPLICITLY DELETED

---

ON-DEMAND RESTORE

=

NEW TABLE

---

DYNAMODB BACKUPS

=

NO PERFORMANCE OR LATENCY IMPACT

---

AWS BACKUP

=

CAN MANAGE DYNAMODB BACKUPS

---

AWS BACKUP

=

ENABLES CROSS-REGION COPY

---

BACKUPS

≠

TTL

---

BACKUPS

≠

STREAMS

---

BACKUPS

≠

GLOBAL TABLES

---

## Quick Cheat Sheet

DYNAMODB BACKUPS

=

PITR + ON-DEMAND

PITR

=

CONTINUOUS BACKUP

PITR WINDOW

=

35 DAYS

PITR RECOVERY

=

ANY POINT WITHIN BACKUP WINDOW

PITR RESTORE

=

NEW TABLE

ON-DEMAND

=

FULL BACKUP

ON-DEMAND RETENTION

=

UNTIL EXPLICITLY DELETED

ON-DEMAND RESTORE

=

NEW TABLE

PERFORMANCE IMPACT

=

NONE

LATENCY IMPACT

=

NONE

AWS BACKUP

=

CENTRALIZED MANAGEMENT

CROSS-REGION COPY

=

AWS BACKUP

TTL

=

DELETE EXPIRED ITEMS

STREAMS

=

CAPTURE CHANGES

GLOBAL TABLES

=

ACTIVE-ACTIVE MULTI-REGION

---

## Master Memory Trick

DYNAMODB BACKUPS

=

TWO CHOICES

Think:

NEED RECENT HISTORY?

↓

PITR

↓

35 DAYS

Need:

LONG-TERM BACKUP?

↓

ON-DEMAND

↓

KEEP UNTIL DELETED

But regardless of backup type:

RESTORE

↓

NEW TABLE

### Final Rule

QUESTION SAYS:

CONTINUOUS BACKUP

+

SPECIFIC RECOVERY TIME

↓

PITR

QUESTION SAYS:

FULL BACKUP

+

LONG-TERM RETENTION

↓

ON-DEMAND BACKUP

QUESTION SAYS:

WHAT DOES RESTORE CREATE?

↓

NEW DYNAMODB TABLE

QUESTION SAYS:

CROSS-REGION BACKUP COPY

↓

AWS BACKUP

---

## Related Notes

- [[DynamoDB Overview]]
- [[DynamoDB Capacity Modes]]
- [[DAX]]
- [[DynamoDB Streams]]
- [[DynamoDB Global Tables]]
- [[DynamoDB TTL]]
- [[AWS Backup]]
- [[S3]]
- [[SAA Databases Cheat Sheet]]
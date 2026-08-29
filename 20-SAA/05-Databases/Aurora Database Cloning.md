## What Problem Does It Solve?

Sometimes you need a copy of a production Aurora database for:

TESTING

↓

DEVELOPMENT

↓

STAGING

↓

EXPERIMENTATION

A traditional approach might be:

TAKE SNAPSHOT

↓

RESTORE SNAPSHOT

↓

WAIT FOR NEW DATABASE COPY

That can take:

MORE TIME

and:

MORE STORAGE

Aurora Database Cloning provides a:

FASTER

and:

MORE COST-EFFECTIVE

way to create a new Aurora cluster from an existing one.

### Memory Trick

AURORA CLONE

=

FAST DATABASE COPY

---

## What Is Aurora Database Cloning?

Aurora Database Cloning creates:

A NEW AURORA DB CLUSTER

from:

AN EXISTING AURORA CLUSTER

Think:

PRODUCTION AURORA

↓

CLONE

↓

STAGING AURORA

The new cluster can be created:

QUICKLY

without immediately copying all underlying database data.

### Memory Trick

CLONE

=

NEW CLUSTER FROM EXISTING CLUSTER

---

## Why Is Cloning Fast?

Aurora Database Cloning uses:

COPY-ON-WRITE

Think:

ORIGINAL DATABASE

↓

CLONE CREATED

↓

BOTH INITIALLY SHARE SAME DATA

No full database copy is required:

AT THE BEGINNING

This makes cloning:

FAST

and:

STORAGE EFFICIENT

### Memory Trick

COPY-ON-WRITE

=

SHARE FIRST

COPY WHEN CHANGED

---

## Copy-on-Write

Copy-on-Write means:

ORIGINAL CLUSTER

and:

CLONED CLUSTER

initially reference:

THE SAME UNDERLYING DATA

Think:

PRODUCTION

↓

SHARED DATA

↑

STAGING CLONE

No separate copy of every database block is immediately created.

### Memory Trick

CLONE START

=

SHARED DATA

---

## What Happens When Data Changes?

When the cloned database modifies data:

CLONE WRITE

↓

NEW STORAGE ALLOCATED

↓

CHANGED DATA COPIED

↓

CLONE NOW HAS ITS OWN VERSION

Think:

UNCHANGED DATA

=

SHARED

CHANGED DATA

=

SEPARATED

### Memory Trick

WRITE

=

COPY ONLY WHAT CHANGES

---

## Original Database Is Not Overwritten

The cloned cluster becomes:

LOGICALLY SEPARATE

from the original.

Think:

PRODUCTION

↓

ORIGINAL DATA

STAGING

↓

CLONED DATA

Changes made in the staging database:

DO NOT CHANGE

the production database.

### Memory Trick

CLONE

=

SAFE COPY FOR CHANGES

---

## Clone Architecture

Initially:

PRODUCTION AURORA

↓

SHARED STORAGE DATA

↑

STAGING AURORA

Then:

STAGING DATA CHANGES

↓

NEW STORAGE ALLOCATED

↓

CHANGED BLOCKS STORED SEPARATELY

Meanwhile:

PRODUCTION

↓

CONTINUES USING ORIGINAL DATA

### Memory Trick

SHARE UNTIL CHANGE

---

## Faster Than Snapshot and Restore

Your SAA course explicitly compares cloning with:

SNAPSHOT + RESTORE

Aurora Database Cloning is:

FASTER

than:

TAKING A SNAPSHOT

↓

RESTORING A NEW CLUSTER

Why?

Because cloning does not initially require:

COPYING ALL DATABASE DATA

### Memory Trick

NEED FAST COPY?

↓

CLONE

---

## Clone vs Snapshot Restore

### Aurora Database Clone

CREATION

=

FAST

METHOD

=

COPY-ON-WRITE

INITIAL FULL DATA COPY

=

NO

BEST FOR

=

FAST TEST / STAGING DATABASE

---

### Snapshot Restore

CREATION

=

RESTORE FROM BACKUP

METHOD

=

CREATE DATABASE FROM SNAPSHOT

BEST FOR

=

BACKUP / RECOVERY / LONGER-TERM RESTORE NEEDS

### Memory Trick

CLONE

=

COPY FOR WORK

SNAPSHOT

=

COPY FOR RECOVERY

---

## Why Is Cloning Cost-Effective?

Because the clone initially:

SHARES EXISTING DATA

you are not immediately paying to duplicate:

THE ENTIRE DATABASE STORAGE

Think:

1 TB DATABASE

↓

CLONE CREATED

↓

NOT ANOTHER FULL 1 TB COPY IMMEDIATELY

Additional storage is primarily allocated as:

DATA CHANGES

### Memory Trick

COPY ONLY CHANGES

=

SAVE STORAGE

---

## Production to Staging

One of the strongest exam use cases is:

CREATE STAGING DATABASE

from:

PRODUCTION DATABASE

Think:

PRODUCTION AURORA

↓

CLONE

↓

STAGING AURORA

Now developers can:

TEST

↓

CHANGE DATA

↓

RUN QUERIES

without directly modifying:

PRODUCTION

### Memory Trick

PROD → CLONE → STAGING

---

## Development Use Case

Suppose developers need:

REALISTIC PRODUCTION-LIKE DATA

for testing.

Instead of:

EXPORT DATABASE

↓

IMPORT DATABASE

↓

WAIT

Use:

AURORA CLONE

Think:

PRODUCTION

↓

CLONE

↓

DEVELOPMENT DATABASE

This provides a fast environment based on:

CURRENT DATABASE DATA

---

## Testing Database Changes

Before deploying a major database change:

PRODUCTION DATABASE

↓

CLONE

↓

TEST DATABASE

Then test:

SCHEMA CHANGES

↓

APPLICATION UPDATES

↓

DATABASE QUERIES

↓

MIGRATIONS

If testing fails:

PRODUCTION REMAINS UNAFFECTED

### Memory Trick

TEST RISKY CHANGES

=

CLONE FIRST

---

## Staging Without Production Impact

Aurora cloning allows you to create:

STAGING

from:

PRODUCTION

without impacting:

PRODUCTION DATABASE OPERATIONS

Think:

PRODUCTION

↓

CONTINUES RUNNING

while:

STAGING CLONE

↓

TESTING OCCURS

### Memory Trick

CLONE

=

TEST WITHOUT TOUCHING PROD

---

## Clone Independence

After cloning:

PRODUCTION CLUSTER

and:

CLONE CLUSTER

are:

SEPARATE DATABASE CLUSTERS

Think:

CLONE WRITES

↓

ONLY CLONE CHANGES

PRODUCTION WRITES

↓

ONLY PRODUCTION CHANGES

They may initially share storage data internally, but from the application perspective:

THEY ARE INDEPENDENT DATABASES

---

## Aurora Clone vs Read Replica

Do not confuse:

DATABASE CLONE

with:

READ REPLICA

### Aurora Read Replica

Purpose:

READ SCALABILITY

Think:

MORE READ TRAFFIC

↓

READ REPLICA

---

### Aurora Clone

Purpose:

CREATE INDEPENDENT DATABASE ENVIRONMENT

Think:

TEST / STAGING

↓

CLONE

### Memory Trick

REPLICA

=

READ SCALE

CLONE

=

NEW ENVIRONMENT

---

## Aurora Clone vs Backup

Do not confuse:

CLONING

with:

BACKUP

### Backup

Purpose:

RECOVER DATA

Think:

ACCIDENTAL DELETE

↓

RESTORE BACKUP

---

### Clone

Purpose:

CREATE FAST WORKING COPY

Think:

TEST / STAGING

↓

CLONE

### Memory Trick

BACKUP

=

RECOVER

CLONE

=

EXPERIMENT

---

## Aurora Clone vs Multi-AZ

### Multi-AZ / Aurora HA

Purpose:

HIGH AVAILABILITY

Think:

DATABASE FAILURE

↓

FAILOVER

---

### Clone

Purpose:

CREATE SEPARATE DATABASE ENVIRONMENT

Think:

DEVELOPMENT

↓

TESTING

↓

STAGING

### Memory Trick

HA

=

SURVIVE FAILURE

CLONE

=

CREATE COPY

---

## Copy-on-Write Architecture

Think:

STEP 1

PRODUCTION DATA

↓

CLONE CREATED

↓

BOTH SHARE DATA

STEP 2

CLONE CHANGES ROW

↓

NEW STORAGE ALLOCATED

STEP 3

ONLY MODIFIED DATA

↓

COPIED / SEPARATED

The unchanged data can continue to be:

SHARED

This is why cloning is:

FAST

and:

COST-EFFECTIVE

---

## Architecture Thinking

Imagine:

PRODUCTION AURORA

contains:

5 TB

of data.

Developers need a staging database.

Traditional approach:

5 TB SNAPSHOT

↓

RESTORE

↓

WAIT FOR LARGE COPY

Aurora Cloning:

PRODUCTION

↓

COPY-ON-WRITE CLONE

↓

STAGING READY QUICKLY

Then:

STAGING CHANGES

↓

ONLY CHANGED DATA USES NEW STORAGE

Think:

LARGE DATABASE

+

FAST TEST COPY

↓

AURORA DATABASE CLONING

---

## When Should You Think Clone?

Question mentions:

FAST COPY OF AURORA DATABASE

↓

CLONE

---

Question mentions:

STAGING DATABASE FROM PRODUCTION

↓

CLONE

---

Question mentions:

TESTING WITHOUT IMPACTING PRODUCTION

↓

CLONE

---

Question mentions:

COPY-ON-WRITE

↓

CLONE

---

Question wants:

FASTER THAN SNAPSHOT + RESTORE

↓

CLONE

---

Question wants:

COST-EFFECTIVE DATABASE COPY

↓

CLONE

---

## Scenario Recognition

Need a staging Aurora database from production?

→ Aurora Database Cloning

---

Need a fast database copy for testing?

→ Aurora Database Cloning

---

Need developers to test using production-like data?

→ Aurora Database Cloning

---

Need production unaffected by database experimentation?

→ Aurora Database Cloning

---

Need copy-on-write?

→ Aurora Database Cloning

---

Need a copy faster than snapshot and restore?

→ Aurora Database Cloning

---

Need backup after accidental deletion?

→ RDS / Aurora Backups

NOT Database Cloning

---

Need additional read capacity?

→ Aurora Read Replicas

NOT Database Cloning

---

Need regional disaster recovery?

→ Aurora Global

NOT Database Cloning

---

## Exam Traps

AURORA DATABASE CLONING

=

NEW AURORA CLUSTER

---

SOURCE

=

EXISTING AURORA CLUSTER

---

CLONING

=

COPY-ON-WRITE

---

INITIAL FULL DATA COPY

=

NO

---

INITIAL DATA

=

SHARED

---

DATA CHANGES

↓

NEW STORAGE ALLOCATED

---

CLONE

=

FASTER THAN SNAPSHOT + RESTORE

---

CLONE

=

COST-EFFECTIVE

---

BEST USE CASE

=

PRODUCTION → STAGING

---

PRODUCTION IMPACT

=

MINIMAL / UNCHANGED BY CLONE WRITES

---

CLONE

≠

READ REPLICA

---

CLONE

≠

BACKUP

---

READ REPLICA

=

READ SCALE

BACKUP

=

RECOVERY

CLONE

=

TEST / STAGING COPY

---

## Quick Cheat Sheet

AURORA CLONING

=

CREATE NEW CLUSTER FROM EXISTING CLUSTER

TECHNOLOGY

=

COPY-ON-WRITE

INITIAL DATA COPY

=

NO FULL COPY

INITIAL STORAGE

=

SHARED

DATA CHANGES

=

NEW STORAGE ALLOCATED

SPEED

=

FASTER THAN SNAPSHOT + RESTORE

COST

=

COST-EFFECTIVE

BEST USE CASE

=

STAGING / TEST / DEVELOPMENT

PRODUCTION IMPACT

=

CLONE CHANGES DO NOT MODIFY PRODUCTION

READ REPLICA

=

READ SCALING

SNAPSHOT

=

BACKUP / RESTORE

CLONE

=

FAST WORKING COPY

---

## Master Memory Trick

PRODUCTION AURORA

↓

CLONE

↓

STAGING AURORA

At first:

PRODUCTION

↓

SHARED DATA

↑

STAGING

Then:

STAGING CHANGES DATA

↓

COPY ONLY CHANGED DATA

Think:

SHARE FIRST

↓

COPY WHEN WRITTEN

↓

COPY-ON-WRITE

Remember:

READ REPLICA

=

SCALE READS

BACKUP

=

RECOVER DATA

CLONE

=

CREATE FAST TEST COPY

### Final Rule

QUESTION SAYS:

PRODUCTION → STAGING

+

FAST

+

COST-EFFECTIVE

+

COPY-ON-WRITE

↓

AURORA DATABASE CLONING

---

## Related Notes

- [Aurora](Aurora)
- [Aurora Endpoints](<Aurora Endpoints>)
- [Aurora Auto Scaling](<Aurora Auto Scaling>)
- [Aurora Serverless](<Aurora Serverless>)
- [Aurora Global](<Aurora Global>)
- [RDS Backups](<RDS Backups>)
- [RDS Read Replicas](<RDS Read Replicas>)
- [SAA Databases Cheat Sheet](<SAA Databases Cheat Sheet>)
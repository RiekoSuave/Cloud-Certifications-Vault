## What Problem Does It Solve?

A database can lose or corrupt data because of:

ACCIDENTAL DELETION

↓

BAD APPLICATION UPDATE

↓

DATA CORRUPTION

↓

HUMAN ERROR

↓

DISASTER

High availability alone does not solve this problem.

RDS Backups allow you to:

RECOVER DATABASE DATA

from an earlier point in time.

Think:

BAD DATA CHANGE

↓

NEED OLD DATA

↓

RDS BACKUP

↓

RESTORE DATABASE

### Memory Trick

RDS BACKUPS

=

GO BACK IN TIME

---

## RDS Backup Options

RDS provides two major backup mechanisms:

AUTOMATED BACKUPS

and:

MANUAL DB SNAPSHOTS

Think:

RDS BACKUPS

↓

AUTOMATED

or:

MANUAL

### Memory Trick

AUTOMATED

=

AWS BACKS UP ON SCHEDULE

SNAPSHOT

=

YOU CREATE BACKUP

---

## Automated Backups

RDS Automated Backups automatically protect:

DATABASE DATA

without requiring you to manually create every backup.

Automated Backups include:

DAILY FULL BACKUP

and:

TRANSACTION LOG BACKUPS

Think:

DATABASE

↓

DAILY BACKUP

+

TRANSACTION LOGS

↓

POINT-IN-TIME RESTORE

### Memory Trick

AUTOMATED BACKUPS

=

DAILY + LOGS

---

## Daily Full Backup

During the:

BACKUP WINDOW

RDS performs:

FULL DAILY BACKUP

Think:

RDS DATABASE

↓

BACKUP WINDOW

↓

DAILY BACKUP

This provides the foundation for:

DATABASE RECOVERY

---

## Transaction Logs

RDS also backs up:

TRANSACTION LOGS

throughout the day.

Think:

DAILY BACKUP

↓

TRANSACTION LOGS

↓

CHANGES AFTER BACKUP

This enables:

POINT-IN-TIME RESTORE

### Memory Trick

TRANSACTION LOGS

=

RECOVER BETWEEN DAILY BACKUPS

---

## Point-in-Time Restore

Automated Backups allow:

POINT-IN-TIME RESTORE

or:

PITR

Think:

DATABASE IS GOOD

↓

BAD CHANGE HAPPENS

↓

CHOOSE TIME BEFORE BAD CHANGE

↓

RESTORE

### Example

Database is healthy at:

2:00 PM

Bad update occurs at:

2:15 PM

You can restore the database to:

2:14 PM

Think:

BAD CHANGE

↓

GO BACK TO BEFORE IT HAPPENED

### Memory Trick

PITR

=

RESTORE TO A SPECIFIC TIME

---

## Automated Backup Retention

Automated Backups have a:

RETENTION PERIOD

Your course highlights:

1 TO 35 DAYS

Think:

AUTOMATED BACKUPS

↓

KEEP FOR

↓

1–35 DAYS

### Memory Trick

AUTOMATED

=

MAX 35 DAYS

---

## Backup Window

Automated database backups occur during a:

DAILY BACKUP WINDOW

Think:

RDS

↓

BACKUP WINDOW

↓

AUTOMATED BACKUP

This is a defined period when RDS performs:

BACKUP OPERATIONS

---

## Manual DB Snapshots

You can also manually create:

DB SNAPSHOTS

Think:

ADMINISTRATOR

↓

CREATE SNAPSHOT

↓

DATABASE BACKUP

Unlike Automated Backups, manual snapshots are:

USER-INITIATED

### Memory Trick

SNAPSHOT

=

MANUAL BACKUP

---

## Manual Snapshot Retention

Manual DB Snapshots can be retained:

AS LONG AS YOU WANT

Think:

CREATE SNAPSHOT

↓

KEEP IT

↓

UNTIL YOU DELETE IT

This is different from:

AUTOMATED BACKUPS

which have a configured retention period.

### Memory Trick

MANUAL SNAPSHOT

=

KEEP UNTIL DELETE

---

## Automated Backup vs Manual Snapshot

### Automated Backup

CREATION

=

AUTOMATIC

RETENTION

=

1–35 DAYS

POINT-IN-TIME RESTORE

=

YES

Think:

CONTINUOUS RECOVERY

---

### Manual Snapshot

CREATION

=

MANUAL

RETENTION

=

UNTIL YOU DELETE IT

Think:

LONG-TERM DATABASE BACKUP

### Memory Trick

AUTOMATED

=

PITR

SNAPSHOT

=

KEEP IT

---

## Restoring an RDS Backup

An important RDS behavior:

RESTORING A BACKUP

does not restore directly over:

THE EXISTING DATABASE

Instead:

RESTORE

↓

CREATES NEW RDS DATABASE

Think:

OLD DATABASE

+

BACKUP

↓

RESTORE

↓

NEW DATABASE

### Memory Trick

RDS RESTORE

=

NEW DATABASE

---

## Why Does Restore Create a New Database?

Suppose:

PRODUCTION RDS

contains corrupted data.

You restore a backup.

Instead of overwriting production:

RDS

↓

CREATES RESTORED DATABASE

Then you can:

TEST IT

↓

VERIFY DATA

↓

CHANGE APPLICATION CONNECTION

### Exam Thinking

Question asks what happens when restoring an RDS snapshot?

↓

A NEW DB INSTANCE IS CREATED

---

## Snapshot Restore

Think:

RDS DATABASE

↓

MANUAL SNAPSHOT

↓

RESTORE

↓

NEW RDS DATABASE

The restored database receives:

A NEW ENDPOINT

Your application may need to:

CONNECT TO THE RESTORED DATABASE

---

## Point-in-Time Restore Architecture

Think:

DAILY FULL BACKUP

↓

TRANSACTION LOGS

↓

DATABASE CHANGES

↓

SELECT RESTORE TIME

↓

RDS RECONSTRUCTS DATABASE

↓

NEW RDS INSTANCE

### Memory Trick

FULL BACKUP

+

LOGS

=

POINT-IN-TIME RESTORE

---

## Multi-AZ vs Backups

Do not confuse:

HIGH AVAILABILITY

with:

DATA RECOVERY

### Multi-AZ

Protects against:

INFRASTRUCTURE FAILURE

Think:

PRIMARY FAILS

↓

STANDBY TAKES OVER

---

### Backups

Protect against:

DATA LOSS / BAD DATA CHANGES

Think:

DATA DELETED

↓

RESTORE OLDER DATABASE

### Memory Trick

MULTI-AZ

=

STAY ONLINE

BACKUP

=

GO BACK

---

## Why Multi-AZ Does Not Replace Backups

Imagine:

APPLICATION

↓

ACCIDENTALLY DELETES CUSTOMER TABLE

The deletion occurs on:

PRIMARY

With Multi-AZ:

PRIMARY

↓

SYNC REPLICATION

↓

STANDBY

The deletion can also reach:

STANDBY

Think:

BAD DATA

↓

REPLICATED

Therefore:

MULTI-AZ

cannot simply undo:

LOGICAL DATA ERRORS

You need:

BACKUPS

### Memory Trick

MULTI-AZ

=

COPY CURRENT STATE

BACKUP

=

RECOVER OLD STATE

---

## Read Replica vs Backup

Do not confuse:

READ REPLICA

with:

BACKUP

### Read Replica

Purpose:

READ SCALABILITY

Think:

MORE READS

---

### Backup

Purpose:

DATA RECOVERY

Think:

RESTORE OLD DATA

### Memory Trick

REPLICA

=

PERFORMANCE

BACKUP

=

RECOVERY

---

## Backup vs Snapshot

Think:

AUTOMATED BACKUP

=

CONTINUOUS RECOVERY SYSTEM

MANUAL SNAPSHOT

=

BACKUP TAKEN AT A SPECIFIC POINT

Both can help recover data, but their:

RETENTION

and:

MANAGEMENT

differ.

---

## Snapshot Use Case

Suppose you are about to perform:

MAJOR DATABASE CHANGE

such as:

APPLICATION UPGRADE

↓

DATABASE MIGRATION

↓

SCHEMA CHANGE

You may create:

MANUAL SNAPSHOT

before making the change.

Think:

BEFORE RISKY CHANGE

↓

TAKE SNAPSHOT

### Memory Trick

BEFORE BIG CHANGE

=

SNAPSHOT

---

## Long-Term Backup Thinking

Need a database backup retained beyond:

35 DAYS?

Think:

MANUAL SNAPSHOT

Because:

AUTOMATED BACKUPS

have a limited retention window.

### Exam Thinking

Question says:

KEEP DATABASE BACKUP INDEFINITELY

↓

MANUAL DB SNAPSHOT

---

## RDS Snapshot Copying

RDS snapshots can be:

COPIED

Think:

DB SNAPSHOT

↓

COPY

↓

ANOTHER SNAPSHOT

Snapshot copying can be useful for:

DISASTER RECOVERY

↓

MIGRATION

↓

CROSS-REGION STRATEGIES

---

## Cross-Region Snapshot Copy

A snapshot can be copied to:

ANOTHER AWS REGION

Think:

REGION A

↓

RDS SNAPSHOT

↓

COPY

↓

REGION B

This can help with:

REGIONAL DISASTER RECOVERY

### Memory Trick

CROSS-REGION SNAPSHOT

=

BACKUP IN ANOTHER REGION

---

## RDS Backup Encryption

If the source RDS database is:

ENCRYPTED

its snapshots are:

ENCRYPTED

Think:

ENCRYPTED DATABASE

↓

ENCRYPTED SNAPSHOT

Encryption concepts will connect with:

[KMS](06-Security/KMS.md)

later in the course.

---

## Sharing Snapshots

Manual RDS snapshots can be:

SHARED

with other AWS accounts.

Think:

ACCOUNT A

↓

RDS SNAPSHOT

↓

SHARE

↓

ACCOUNT B

This can help with:

DATABASE MIGRATION

or:

CROSS-ACCOUNT DATA TRANSFER

---

## Encrypted Snapshot Sharing

For encrypted snapshots, access to the:

KMS KEY

also matters.

Think:

ENCRYPTED SNAPSHOT

↓

KMS KEY

↓

AUTHORIZED ACCOUNT

This connects database security with:

[KMS](06-Security/KMS.md)

### Exam Thinking

Encrypted database data usually means:

THINK ABOUT KMS PERMISSIONS TOO

---

## RDS Backup Architecture

Imagine:

APPLICATION

↓

RDS

During normal operation:

RDS

↓

AUTOMATED BACKUPS

↓

DAILY FULL BACKUP

+

TRANSACTION LOGS

Then:

ACCIDENTAL DELETE

↓

SELECT POINT BEFORE DELETE

↓

POINT-IN-TIME RESTORE

↓

NEW RDS DATABASE

↓

VERIFY DATA

↓

APPLICATION CONNECTS TO RESTORED DB

Think:

BACKUP

↓

RESTORE

↓

NEW DATABASE

↓

RECONNECT

---

## Backup Decision Tree

Need:

AUTOMATIC CONTINUOUS RECOVERY?

↓

AUTOMATED BACKUPS

---

Need:

RESTORE TO SPECIFIC TIME?

↓

POINT-IN-TIME RESTORE

---

Need:

BACKUP KEPT INDEFINITELY?

↓

MANUAL SNAPSHOT

---

Need:

BACKUP BEFORE MAJOR DATABASE CHANGE?

↓

MANUAL SNAPSHOT

---

Need:

SURVIVE DATABASE / AZ FAILURE?

↓

MULTI-AZ

---

Need:

MORE READ PERFORMANCE?

↓

READ REPLICA

---

Need:

BACKUP IN ANOTHER REGION?

↓

CROSS-REGION SNAPSHOT COPY

---

## Scenario Recognition

Need automatic RDS backups?

→ Automated Backups

---

Need point-in-time recovery?

→ Automated Backups

---

Need to restore database to just before an accidental deletion?

→ Point-in-Time Restore

---

Need backup retained up to 35 days?

→ Automated Backups

---

Need backup retained indefinitely?

→ Manual DB Snapshot

---

Need backup before a risky database upgrade?

→ Manual DB Snapshot

---

Need to restore an RDS snapshot?

→ Creates a new RDS database

---

Need to recover from accidental data deletion?

→ RDS Backup / PITR

---

Need high availability during an AZ failure?

→ RDS Multi-AZ

---

Need more database read capacity?

→ RDS Read Replica

---

Need database backup stored in another Region?

→ Cross-Region Snapshot Copy

---

Need to share a database backup with another AWS account?

→ Manual Snapshot Sharing

---

Need to share an encrypted snapshot?

→ Consider KMS key permissions

---

## Exam Traps

AUTOMATED BACKUPS

=

POINT-IN-TIME RESTORE

---

AUTOMATED BACKUP RETENTION

=

1–35 DAYS

---

MANUAL SNAPSHOT

=

KEEP UNTIL DELETED

---

AUTOMATED BACKUP

≠

MANUAL SNAPSHOT

---

RESTORE

=

CREATES NEW DATABASE

---

RESTORE

≠

OVERWRITE EXISTING DATABASE

---

MULTI-AZ

≠

BACKUP

---

MULTI-AZ

=

HIGH AVAILABILITY

BACKUP

=

DATA RECOVERY

---

READ REPLICA

≠

BACKUP

---

READ REPLICA

=

READ PERFORMANCE

BACKUP

=

RECOVERY

---

BAD DATA CAN REPLICATE TO MULTI-AZ STANDBY

Therefore:

MULTI-AZ

DOES NOT REPLACE BACKUPS

---

MANUAL SNAPSHOT

=

GOOD FOR LONG-TERM RETENTION

---

CROSS-REGION SNAPSHOT

=

REGIONAL DR OPTION

---

ENCRYPTED SNAPSHOT

=

THINK KMS

---

## Quick Cheat Sheet

AUTOMATED BACKUPS

=

DAILY BACKUP + TRANSACTION LOGS

PITR

=

RESTORE TO SPECIFIC TIME

AUTOMATED RETENTION

=

1–35 DAYS

MANUAL SNAPSHOT

=

USER CREATED

MANUAL SNAPSHOT RETENTION

=

UNTIL DELETED

RESTORE

=

NEW RDS DATABASE

MULTI-AZ

=

HIGH AVAILABILITY

BACKUP

=

DATA RECOVERY

READ REPLICA

=

READ SCALING

SNAPSHOT COPY

=

COPY DATABASE BACKUP

CROSS-REGION COPY

=

REGIONAL DR

ENCRYPTED SNAPSHOT

=

KMS

---

## Master Memory Trick

Think:

DATABASE FAILURE?

↓

MULTI-AZ

TOO MANY READS?

↓

READ REPLICA

DATABASE STORAGE FULL?

↓

STORAGE AUTO SCALING

DATA DELETED?

↓

BACKUP

Then:

NEED RECENT TIME?

↓

PITR

NEED LONG-TERM COPY?

↓

MANUAL SNAPSHOT

And remember:

AUTOMATED

=

DAILY + LOGS

↓

1–35 DAYS

MANUAL

=

SNAPSHOT

↓

KEEP UNTIL DELETE

RESTORE

=

NEW DATABASE

### Final Rule

MULTI-AZ

=

STAY AVAILABLE

READ REPLICA

=

SCALE READS

BACKUP

=

RECOVER DATA

---

## Related Notes

- [RDS Overview](<RDS Overview>)
- [RDS Storage Auto Scaling](<RDS Storage Auto Scaling>)
- [RDS Read Replicas](<RDS Read Replicas>)
- [RDS Multi-AZ](<RDS Multi-AZ>)
- [Aurora](04-Databases/Aurora.md)
- [RDS Proxy](<RDS Proxy>)
- [KMS](06-Security/KMS.md)
- [SAA Databases Cheat Sheet](<SAA Databases Cheat Sheet>)
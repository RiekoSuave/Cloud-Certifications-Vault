## What Problem Does It Solve?

EBS Snapshots provide:

POINT-IN-TIME BACKUPS

of:

[EBS Volumes](https://chatgpt.com/c/EBS%20Volumes)

Instead of relying on a single EBS volume, you can create a snapshot that can later be used to restore the volume.

Think:

EBS VOLUME

↓

SNAPSHOT

↓

BACKUP

### Memory Trick

EBS SNAPSHOT = BACKUP OF EBS

---

## What Is an EBS Snapshot?

An EBS Snapshot is:

A POINT-IN-TIME BACKUP

of an EBS volume.

Think:

EBS VOLUME

↓

TAKE SNAPSHOT

↓

EBS SNAPSHOT

↓

RESTORE WHEN NEEDED

Snapshots allow you to protect EBS data and create new EBS volumes from previously captured data.

---

## Creating an EBS Snapshot

You do:

NOT

have to detach an EBS volume before creating a snapshot.

However, your course recommends detaching the volume first when possible.

Think:

EBS ATTACHED

↓

SNAPSHOT POSSIBLE

But:

DETACH

↓

SNAPSHOT

↓

BETTER DATA CONSISTENCY

### SAA Thinking

If an application is actively writing data while a snapshot is being created, the snapshot may capture data while changes are occurring.

For better consistency:

STOP WRITES

or

DETACH VOLUME

↓

CREATE SNAPSHOT

---

## EBS Snapshot Architecture

Think:

EC2 INSTANCE

↓

EBS VOLUME

↓

CREATE SNAPSHOT

↓

EBS SNAPSHOT

The snapshot can then be used to create another EBS volume.

Think:

EBS SNAPSHOT

↓

RESTORE

↓

NEW EBS VOLUME

---

## Moving EBS Across Availability Zones

Remember from:

[EBS Volumes](https://chatgpt.com/c/EBS%20Volumes)

EBS volumes are:

AZ LOCKED

An EBS volume cannot directly move from:

us-east-1a

to:

us-east-1b

Instead:

EBS VOLUME

↓

SNAPSHOT

↓

RESTORE SNAPSHOT

↓

NEW EBS VOLUME

↓

NEW AZ

Think:

AZ 1

↓

EBS

↓

SNAPSHOT

↓

RESTORE

↓

EBS

↓

AZ 2

### Memory Trick

MOVE EBS

=

SNAPSHOT + RESTORE

---

## Copying EBS Snapshots

EBS snapshots can be copied across:

AVAILABILITY ZONES

and

AWS REGIONS

This makes snapshots useful for:

- Moving EBS data
    
- Disaster recovery
    
- Creating storage in another location
    

Think:

EBS

↓

SNAPSHOT

↓

COPY

↓

ANOTHER LOCATION

---

## Snapshot Performance Consideration

Creating EBS backups uses:

I/O

This means snapshot operations can compete with your application for storage performance.

Think:

APPLICATION

↓

EBS I/O

and

SNAPSHOT

↓

EBS I/O

Therefore:

HIGH APPLICATION TRAFFIC

EBS BACKUP

=

POSSIBLE PERFORMANCE IMPACT

### SAA Scenario

Application is currently handling heavy traffic and requires maximum EBS performance?

→ Avoid performing heavy EBS backup activity at the same time when possible.

### Memory Trick

SNAPSHOT = USES I/O

---

## EBS Snapshot Archive

Snapshots that do not need immediate access can be moved to:

EBS SNAPSHOT ARCHIVE

This is a lower-cost storage tier for snapshots.

Your course highlights:

ARCHIVE TIER

↓

75% CHEAPER

than standard snapshot storage.

Think:

OLD SNAPSHOT

↓

RARELY NEEDED

↓

ARCHIVE

↓

LOWER COST

---

## Restoring Archived Snapshots

The tradeoff for lower cost is:

SLOW RESTORE

Restoring an archived snapshot can take:

24–72 HOURS

Think:

CHEAPER

↓

SLOWER RESTORE

### Memory Trick

ARCHIVE

=

CHEAP + SLOW

---

## EBS Snapshot Recycle Bin

AWS provides:

RECYCLE BIN

for EBS snapshots.

The Recycle Bin protects against:

ACCIDENTAL DELETION

You create retention rules that determine how long deleted snapshots are preserved.

Think:

DELETE SNAPSHOT

↓

RECYCLE BIN

↓

RECOVER SNAPSHOT

---

## Recycle Bin Retention

Your course specifies retention from:

1 DAY

to

1 YEAR

Think:

ACCIDENTALLY DELETE SNAPSHOT

↓

RECYCLE BIN

↓

RESTORE BEFORE RETENTION EXPIRES

### Memory Trick

RECYCLE BIN = UNDELETE SNAPSHOT

---

## Fast Snapshot Restore

Normally, a newly restored EBS volume may experience:

INITIALIZATION LATENCY

when blocks are accessed for the first time.

AWS provides:

FAST SNAPSHOT RESTORE

or:

FSR

FSR forces:

FULL INITIALIZATION

of the snapshot.

Think:

SNAPSHOT

↓

FAST SNAPSHOT RESTORE

↓

FULL INITIALIZATION

↓

NO FIRST-USE LATENCY

---

## Fast Snapshot Restore Tradeoff

Fast Snapshot Restore improves performance but costs:

MORE MONEY

Think:

FSR

=

FAST

EXPENSIVE

Use it when immediate storage performance is more important than minimizing cost.

### Memory Trick

FSR = FAST RESTORE $$$

---

## EBS Snapshot Architecture Thinking

Think of the full lifecycle:

EC2

↓

EBS VOLUME

↓

SNAPSHOT

Then the snapshot can be used for several purposes:

BACKUP

↓

RECOVERY

or

SNAPSHOT

↓

RESTORE

↓

NEW EBS VOLUME

or

SNAPSHOT

↓

RESTORE

↓

DIFFERENT AZ

or

SNAPSHOT

↓

COPY

↓

DIFFERENT REGION

---

## Cost Optimization Thinking

Frequently needed snapshot?

↓

STANDARD SNAPSHOT

Rarely needed long-term snapshot?

↓

SNAPSHOT ARCHIVE

Think:

ACTIVE

=

STANDARD

ARCHIVAL

=

CHEAPER

But:

ARCHIVE

=

24–72 HOUR RESTORE

---

## Protection Thinking

Need protection against accidental snapshot deletion?

↓

RECYCLE BIN

Need lower-cost long-term snapshot storage?

↓

SNAPSHOT ARCHIVE

Need immediate full performance from a restored snapshot?

↓

FAST SNAPSHOT RESTORE

---

## Scenario Recognition

Need a backup of an EBS volume?

→ EBS Snapshot

---

Need a point-in-time backup of EBS?

→ EBS Snapshot

---

Need to move an EBS volume to another Availability Zone?

→ Snapshot + Restore

---

Need to copy EBS data to another Region?

→ Copy EBS Snapshot

---

Need cheaper storage for rarely accessed snapshots?

→ EBS Snapshot Archive

---

Need to restore an archived snapshot?

→ Expect 24–72 hours

---

Need protection against accidental snapshot deletion?

→ Recycle Bin

---

Need deleted snapshots retained for a specified period?

→ Recycle Bin retention rule

---

Need a restored EBS volume with no first-use initialization latency?

→ Fast Snapshot Restore

---

Application currently requires heavy EBS I/O?

→ Avoid competing snapshot/backup activity when possible

---

## Exam Traps

EBS SNAPSHOT = POINT-IN-TIME BACKUP

SNAPSHOT ≠ EBS VOLUME

EBS does NOT need to be detached to take a snapshot

DETACHING / STOPPING WRITES = BETTER CONSISTENCY

MOVE EBS BETWEEN AZs = SNAPSHOT + RESTORE

SNAPSHOTS CAN BE COPIED ACROSS REGIONS

SNAPSHOT BACKUPS USE I/O

SNAPSHOT ARCHIVE = LOWER COST

ARCHIVE RESTORE = 24–72 HOURS

RECYCLE BIN = PROTECT DELETED SNAPSHOTS

FAST SNAPSHOT RESTORE = REMOVE FIRST-USE LATENCY

FSR = EXTRA COST

---

## Quick Cheat Sheet

EBS SNAPSHOT

=

POINT-IN-TIME BACKUP

SOURCE

=

EBS VOLUME

DETACH REQUIRED?

=

NO

DETACH RECOMMENDED?

=

YES, WHEN POSSIBLE

MOVE EBS ACROSS AZ

=

SNAPSHOT + RESTORE

COPY ACROSS REGION

=

EBS SNAPSHOT

SNAPSHOT BACKUP

=

USES EBS I/O

SNAPSHOT ARCHIVE

=

75% CHEAPER

ARCHIVE RESTORE

=

24–72 HOURS

RECYCLE BIN

=

RECOVER DELETED SNAPSHOTS

RECYCLE BIN RETENTION

=

1 DAY – 1 YEAR

FAST SNAPSHOT RESTORE

=

NO FIRST-USE LATENCY

FSR

=

EXPENSIVE

---

## Master Memory Trick

EBS

=

LIVE VOLUME

SNAPSHOT

=

BACKUP

MOVE AZ

=

SNAPSHOT + RESTORE

ARCHIVE

=

CHEAP + SLOW

RECYCLE BIN

=

UNDELETE

FSR

=

FAST + $$$

---

## Related Notes

- [EBS Volumes](https://chatgpt.com/c/EBS%20Volumes)
    
- [EBS Volume Types](https://chatgpt.com/c/EBS%20Volume%20Types)
    
- [AMI](https://chatgpt.com/c/AMI)
    
- [EC2](https://chatgpt.com/c/EC2)
    
- [EC2 Instance Store](https://chatgpt.com/c/EC2%20Instance%20Store)
    
- [EFS](https://chatgpt.com/c/EFS)
    
- [SAA EC2 Storage Cheat Sheet](https://chatgpt.com/c/SAA%20EC2%20Storage%20Cheat%20Sheet)
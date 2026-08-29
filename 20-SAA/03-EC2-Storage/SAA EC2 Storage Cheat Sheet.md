## What Problem Does It Solve?

This note helps answer:

WHICH EC2 STORAGE OPTION SHOULD I CHOOSE?

Think:

STORAGE QUESTION

↓

IDENTIFY REQUIREMENT

↓

CHOOSE SERVICE

### Memory Trick

EC2 STORAGE

=

DISK?

BACKUP?

TEMPLATE?

TEMPORARY?

SHARED?

---

## Master Storage Map

Need:

PERSISTENT EC2 DISK

↓

[EBS Volumes](https://chatgpt.com/c/EBS%20Volumes)

Need:

EBS BACKUP

↓

[EBS Snapshots](https://chatgpt.com/c/EBS%20Snapshots)

Need:

REUSABLE EC2 TEMPLATE

↓

[AMI](https://chatgpt.com/c/AMI)

Need:

VERY FAST TEMPORARY LOCAL DISK

↓

[EC2 Instance Store](https://chatgpt.com/c/EC2%20Instance%20Store)

Need:

SHARED LINUX FILESYSTEM

↓

[EFS](https://chatgpt.com/c/EFS)

Think:

EBS

=

DISK

SNAPSHOT

=

BACKUP

AMI

=

SERVER TEMPLATE

INSTANCE STORE

=

TEMPORARY SPEED

EFS

=

SHARED FILES

---

## EBS

EBS stands for:

ELASTIC BLOCK STORE

EBS provides:

PERSISTENT BLOCK STORAGE

for EC2.

Think:

EC2

↓

NETWORK

↓

EBS

### Must Remember

EBS

=

NETWORK DRIVE

EBS

=

PERSISTENT

EBS

=

AZ LOCKED

EBS

=

PROVISIONED CAPACITY

### Memory Trick

EBS = EC2 HARD DRIVE

---

## EBS Availability Zone Rule

An EBS volume exists in:

ONE AVAILABILITY ZONE

Think:

EBS IN AZ-A

↓

EC2 MUST BE IN AZ-A

Need to move EBS to another AZ?

↓

SNAPSHOT

↓

RESTORE

↓

NEW EBS VOLUME

### Memory Trick

MOVE EBS

=

SNAPSHOT + RESTORE

---

## EBS Delete on Termination

### Root EBS

By default:

TERMINATE EC2

↓

ROOT EBS DELETED

### Additional EBS

By default:

TERMINATE EC2

↓

ADDITIONAL EBS PRESERVED

Think:

ROOT

=

DELETE

EXTRA

=

KEEP

---

## EBS Volume Types

### gp3

GENERAL PURPOSE SSD

Think:

MOST NORMAL WORKLOADS

↓

gp3

Key idea:

SIZE

and

IOPS / THROUGHPUT

can be adjusted independently.

---

### gp2

GENERAL PURPOSE SSD

Key difference:

SIZE ↑

↓

IOPS ↑

Think:

gp2

=

SIZE + PERFORMANCE LINKED

---

### io1 / io2

PROVISIONED IOPS SSD

Think:

MISSION-CRITICAL DATABASE

↓

io1 / io2

Use when you need:

HIGH

and

CONSISTENT IOPS

io2 Block Express provides:

VERY HIGH IOPS

SUB-MILLISECOND LATENCY

---

### st1

THROUGHPUT OPTIMIZED HDD

Think:

BIG DATA

DATA WAREHOUSE

LOG PROCESSING

↓

st1

### Memory Trick

st1 = STREAM LARGE DATA

---

### sc1

COLD HDD

Think:

INFREQUENT ACCESS

LOWEST COST

↓

sc1

### Memory Trick

sc1 = SUPER CHEAP COLD

---

## EBS Volume Type Decision

NORMAL APPLICATION

↓

gp3

OLD GENERAL-PURPOSE SIZE-LINKED PERFORMANCE

↓

gp2

DATABASE + HIGH IOPS

↓

io1 / io2

BIG SEQUENTIAL DATA

↓

st1

COLD + CHEAP DATA

↓

sc1

---

## EBS Boot Volume Rule

Can be boot volumes:

gp2

gp3

io1

io2

Cannot be boot volumes:

st1

sc1

### Memory Trick

BOOT

=

SSD

NOT HDD

---

## EBS Multi-Attach

Normally:

ONE EBS

↓

ONE EC2

Exception:

io1 / io2

↓

MULTI-ATTACH

Think:

EC2 #1

↘

io1 / io2

↗

EC2 #2

### Rules

MULTIPLE EC2

=

SAME AZ

MAX

=

16 EC2 INSTANCES

ACCESS

=

READ + WRITE

FILESYSTEM

=

CLUSTER-AWARE

CONCURRENT WRITES

=

APPLICATION RESPONSIBILITY

### Memory Trick

MULTI-ATTACH

=

io1/io2 + SAME AZ + 16 MAX

---

## EBS Encryption

Encrypted EBS provides:

DATA AT REST

=

ENCRYPTED

DATA BETWEEN EC2 + EBS

=

ENCRYPTED

SNAPSHOTS

=

ENCRYPTED

NEW VOLUMES FROM SNAPSHOT

=

ENCRYPTED

Encryption uses:

[AWS KMS](https://chatgpt.com/c/AWS%20KMS)

### Memory Trick

EBS ENCRYPTION

=

KMS

---

## Encrypt an Existing Unencrypted EBS Volume

Think:

UNENCRYPTED EBS

↓

CREATE SNAPSHOT

↓

COPY SNAPSHOT + ENCRYPT

↓

CREATE NEW EBS

↓

ATTACH NEW ENCRYPTED VOLUME

### Memory Trick

SNAPSHOT

↓

COPY + ENCRYPT

↓

NEW VOLUME

---

## EBS Snapshots

EBS Snapshot

=

POINT-IN-TIME EBS BACKUP

Think:

EBS

↓

SNAPSHOT

↓

BACKUP

You do not have to detach the volume before creating a snapshot.

But:

DETACH / STOP WRITES

↓

BETTER CONSISTENCY

---

## Snapshot Archive

Need:

LOWER-COST LONG-TERM SNAPSHOT

↓

EBS SNAPSHOT ARCHIVE

Think:

ARCHIVE

=

CHEAPER

SLOWER RESTORE

Restore can take:

24–72 HOURS

### Memory Trick

ARCHIVE = CHEAP + SLOW

---

## Snapshot Recycle Bin

Need protection from:

ACCIDENTAL SNAPSHOT DELETION

↓

RECYCLE BIN

Think:

DELETE

↓

RECYCLE BIN

↓

RECOVER

### Memory Trick

RECYCLE BIN = UNDELETE SNAPSHOT

---

## Fast Snapshot Restore

Need:

NO FIRST-USE LATENCY

when restoring from snapshot?

↓

FAST SNAPSHOT RESTORE

or:

FSR

Think:

FSR

=

FAST

EXPENSIVE

### Memory Trick

FSR = SPEED $$$

---

## AMI

AMI stands for:

AMAZON MACHINE IMAGE

AMI

=

CUSTOMIZED EC2 TEMPLATE

Think:

OS

SOFTWARE

CONFIGURATION

↓

AMI

↓

NEW EC2

### Memory Trick

AMI = PREBUILT EC2

---

## AMI Creation

Think:

START EC2

↓

CUSTOMIZE

↓

STOP FOR DATA INTEGRITY

↓

CREATE AMI

↓

EBS SNAPSHOTS CREATED

↓

LAUNCH NEW EC2

### Important

AMI

=

REGIONAL

But:

AMI CAN BE COPIED ACROSS REGIONS

---

## AMI vs Snapshot

AMI

=

SERVER TEMPLATE

SNAPSHOT

=

DISK BACKUP

Think:

LAUNCH SERVER

↓

AMI

RESTORE STORAGE

↓

SNAPSHOT

---

## EC2 Instance Store

Instance Store provides:

LOCAL HARDWARE STORAGE

Think:

EC2 HOST

↓

LOCAL DISK

↓

INSTANCE STORE

Main benefit:

VERY HIGH I/O

Main disadvantage:

EPHEMERAL

---

## Instance Store Data Loss

STOP EC2

↓

DATA LOST

TERMINATE EC2

↓

DATA LOST

HARDWARE FAILURE

↓

DATA MAY BE LOST

Think:

INSTANCE STORE

=

FAST + TEMPORARY

---

## Instance Store Use Cases

Best for:

CACHE

BUFFER

SCRATCH DATA

TEMPORARY CONTENT

Think:

CAN REBUILD DATA?

↓

INSTANCE STORE

MUST KEEP DATA?

↓

EBS

---

## EFS

EFS stands for:

ELASTIC FILE SYSTEM

EFS provides:

MANAGED NFS FILE STORAGE

Think:

EC2 #1

↘

EFS

↗

EC2 #2

EFS supports:

MANY EC2 INSTANCES

and:

MULTI-AZ ACCESS

### Memory Trick

EFS = SHARED LINUX DRIVE

---

## EFS Key Rules

EFS

=

FILE STORAGE

EFS

=

NFSv4.1

EFS

=

LINUX / POSIX

EFS

=

AUTO-SCALING STORAGE

EFS

=

PAY PER USE

EFS NETWORK ACCESS

=

SECURITY GROUP

EFS ENCRYPTION

=

KMS

---

## EFS Storage Classes

Frequently accessed:

EFS STANDARD

Infrequently accessed:

EFS-IA

Rarely accessed:

EFS ARCHIVE

Think:

HOT

↓

STANDARD

WARM

↓

IA

COLD

↓

ARCHIVE

Lifecycle policies can automatically move files to cheaper tiers.

---

## EFS Availability

### Standard

MULTI-AZ

Think:

PRODUCTION

↓

STANDARD

### One Zone

ONE AZ

Think:

LOWER COST

↓

ONE ZONE

---

## EBS vs EFS

### EBS

BLOCK

↓

ONE EC2 NORMALLY

↓

ONE AZ

### EFS

FILE

↓

MANY EC2

↓

MULTI-AZ

### Memory Trick

EBS

=

MY HARD DRIVE

EFS

=

OUR SHARED DRIVE

---

## EBS vs EFS vs Instance Store

EBS

=

NETWORK + BLOCK + PERSISTENT

EFS

=

NETWORK + FILE + SHARED

INSTANCE STORE

=

LOCAL + FAST + TEMPORARY

Think:

PERSISTENT DISK

↓

EBS

SHARED FILES

↓

EFS

TEMPORARY SPEED

↓

INSTANCE STORE

---

## Highest-Value Scenario Recognition

Need persistent block storage for EC2?

→ EBS

---

Need normal general-purpose SSD storage?

→ gp3

---

Need high consistent database IOPS?

→ io1 / io2

---

Need big sequential throughput workload?

→ st1

---

Need lowest-cost cold HDD?

→ sc1

---

Need EBS data in another AZ?

→ Snapshot + Restore

---

Need point-in-time backup of EBS?

→ EBS Snapshot

---

Need long-term cheap snapshot storage?

→ Snapshot Archive

---

Need protection against accidental snapshot deletion?

→ Recycle Bin

---

Need restored snapshot at full performance immediately?

→ Fast Snapshot Restore

---

Need reusable EC2 server configuration?

→ AMI

---

Need many identical EC2 instances?

→ AMI

---

Need very high-performance temporary disk?

→ Instance Store

---

Need cache or scratch storage?

→ Instance Store

---

Need multiple Linux EC2 instances sharing the same files?

→ EFS

---

Need shared WordPress files?

→ EFS

---

Need same EBS block device attached to several EC2 instances in one AZ?

→ io1/io2 Multi-Attach

---

## Highest-Value Exam Traps

EBS

≠

REGIONAL VOLUME

EBS

=

AZ LOCKED

---

EBS DOES NOT MOVE DIRECTLY BETWEEN AZs

↓

SNAPSHOT + RESTORE

---

ROOT EBS

=

DELETED BY DEFAULT ON TERMINATION

---

gp2

=

SIZE + IOPS LINKED

gp3

=

SIZE + IOPS INDEPENDENT

---

st1 / sc1

=

NOT BOOT VOLUMES

---

MULTI-ATTACH

≠

EFS

MULTI-ATTACH

=

SHARED BLOCK STORAGE

EFS

=

SHARED FILE STORAGE

---

INSTANCE STORE

≠

PERSISTENT

STOP

=

DATA LOST

---

AMI

≠

SNAPSHOT

AMI

=

SERVER TEMPLATE

SNAPSHOT

=

DISK BACKUP

---

EFS

≠

WINDOWS NATIVE FILESYSTEM

EFS

=

LINUX + NFS

---

## 10-Second Decision Tree

Need EC2 storage?

↓

PERSISTENT DISK?

→ EBS

SHARED FILESYSTEM?

→ EFS

TEMPORARY ULTRA-FAST DISK?

→ INSTANCE STORE

BACKUP OF EBS?

→ SNAPSHOT

EC2 TEMPLATE?

→ AMI

HIGH IOPS DATABASE?

→ io1 / io2

GENERAL PURPOSE SSD?

→ gp3

BIG DATA / LOG THROUGHPUT?

→ st1

COLD CHEAP HDD?

→ sc1

---

## Quick Cheat Sheet

EBS

=

PERSISTENT BLOCK STORAGE

SNAPSHOT

=

EBS BACKUP

AMI

=

EC2 TEMPLATE

INSTANCE STORE

=

LOCAL EPHEMERAL STORAGE

EFS

=

SHARED LINUX FILESYSTEM

gp3

=

GENERAL PURPOSE SSD

gp2

=

SIZE-LINKED IOPS

io1 / io2

=

HIGH IOPS

st1

=

THROUGHPUT HDD

sc1

=

COLD HDD

MULTI-ATTACH

=

io1 / io2

EBS LOCATION

=

ONE AZ

EFS STANDARD

=

MULTI-AZ

MOVE EBS

=

SNAPSHOT + RESTORE

EBS ENCRYPTION

=

KMS

INSTANCE STORE STOPPED

=

DATA LOST

---

## Master Memory Trick

EBS

=

HARD DRIVE

SNAPSHOT

=

BACKUP

AMI

=

SERVER BLUEPRINT

INSTANCE STORE

=

FAST SCRATCH DISK

EFS

=

SHARED LINUX DRIVE

gp3

=

GENERAL

io2

=

DATABASE PERFORMANCE

st1

=

STREAM

sc1

=

COLD

Think:

ONE SERVER DISK

↓

EBS

MANY SERVERS SAME FILES

↓

EFS

TEMPORARY SPEED

↓

INSTANCE STORE

BACKUP

↓

SNAPSHOT

SERVER TEMPLATE

↓

AMI

---

## Related Notes

- [EBS Volumes](https://chatgpt.com/c/EBS%20Volumes)
    
- [EBS Snapshots](https://chatgpt.com/c/EBS%20Snapshots)
    
- [EBS Volume Types](https://chatgpt.com/c/EBS%20Volume%20Types)
    
- [EBS Multi-Attach](https://chatgpt.com/c/EBS%20Multi-Attach)
    
- [EBS Encryption](https://chatgpt.com/c/EBS%20Encryption)
    
- [AMI](https://chatgpt.com/c/AMI)
    
- [EC2 Instance Store](https://chatgpt.com/c/EC2%20Instance%20Store)
    
- [EFS](https://chatgpt.com/c/EFS)
    
- [EFS vs EBS](https://chatgpt.com/c/EFS%20vs%20EBS)
    
- [EC2 Instance Storage Summary](https://chatgpt.com/c/EC2%20Instance%20Storage%20Summary)
    
- [EC2](https://chatgpt.com/c/EC2)
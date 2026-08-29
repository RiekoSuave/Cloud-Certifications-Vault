## What Problem Does It Solve?

EBS and EFS both provide storage for EC2, but they solve:

DIFFERENT STORAGE PROBLEMS

Think:

ONE EC2 NEEDS A DISK

↓

EBS

MULTIPLE EC2 INSTANCES NEED SAME FILES

↓

EFS

### Memory Trick

EBS = EC2 HARD DRIVE

EFS = SHARED LINUX FILESYSTEM

---

## EBS vs EFS Overview

### EBS

ELASTIC BLOCK STORE

=

BLOCK STORAGE

### EFS

ELASTIC FILE SYSTEM

=

FILE STORAGE

Think:

BLOCK

↓

EBS

FILES

↓

EFS

---

## EBS Architecture

Normally:

ONE EBS VOLUME

↓

ONE EC2 INSTANCE

EBS volumes are:

LOCKED TO ONE AVAILABILITY ZONE

Think:

AZ-A

↓

EC2

↓

EBS

### Memory Trick

EBS

=

ONE INSTANCE + ONE AZ

Remember the exception:

[EBS Multi-Attach](https://chatgpt.com/c/EBS%20Multi-Attach)

allows certain:

io1 / io2

volumes to attach to multiple EC2 instances.

---

## EFS Architecture

EFS allows:

MANY EC2 INSTANCES

to mount:

THE SAME FILESYSTEM

Think:

EC2 #1

↘

EFS

↗

EC2 #2

And these EC2 instances can exist across:

MULTIPLE AVAILABILITY ZONES

Think:

AZ-A

EC2

↓

EFS

↑

EC2

AZ-B

### Memory Trick

EFS

=

MANY INSTANCES + MULTI-AZ

---

## Availability Zone Difference

### EBS

EBS VOLUME

↓

ONE AZ

If you need the volume in another AZ:

EBS

↓

SNAPSHOT

↓

RESTORE

↓

NEW EBS IN NEW AZ

### EFS

EFS can be mounted by EC2 instances across:

MULTIPLE AZs

using EFS mount targets.

Think:

EBS

=

AZ LOCKED

EFS

=

MULTI-AZ FILE ACCESS

---

## Block Storage vs File Storage

This is the most important conceptual difference.

### EBS

BLOCK STORAGE

The EC2 instance sees EBS like:

A DISK DRIVE

Think:

EC2

↓

HARD DRIVE

↓

EBS

### EFS

FILE STORAGE

EC2 instances mount EFS like:

A NETWORK FILESYSTEM

Think:

MULTIPLE EC2

↓

SHARED DIRECTORY

↓

EFS

### Memory Trick

EBS = DISK

EFS = FOLDER

---

## Sharing Storage

Need storage for:

ONE EC2 INSTANCE

↓

EBS

Need storage shared across:

MANY EC2 INSTANCES

↓

EFS

### Exam Thinking

If an SAA question says:

"Multiple EC2 instances need simultaneous access to the same files"

Think:

EFS

not normal EBS.

---

## Linux Requirement

EFS is designed for:

LINUX

It provides:

POSIX

filesystem semantics.

Think:

LINUX EC2

↓

NFS

↓

EFS

EBS does not have this same Linux-only filesystem restriction because it is:

BLOCK STORAGE

The operating system formats the EBS disk with the desired filesystem.

---

## Scaling Difference

### EBS

You provision:

VOLUME SIZE

and possibly:

IOPS

or

THROUGHPUT

depending on the volume type.

Think:

CHOOSE CAPACITY

↓

EBS

### EFS

Storage automatically:

GROWS

and

SHRINKS

with usage.

Think:

FILES ADDED

↓

EFS GROWS

FILES REMOVED

↓

EFS SHRINKS

### Memory Trick

EBS = PROVISION CAPACITY

EFS = AUTO SCALE CAPACITY

---

## Pricing Difference

EBS generally costs less than EFS for equivalent storage.

Your course emphasizes:

EFS HAS A HIGHER PRICE POINT THAN EBS

Think:

EBS

=

LOWER COST

EFS

=

MORE EXPENSIVE + SHARED FEATURES

EFS can reduce cost through:

STORAGE TIERS

such as:

EFS-IA

and

EFS Archive

---

## EBS Performance Thinking

EBS performance depends on:

[EBS Volume Types](https://chatgpt.com/c/EBS%20Volume%20Types)

Examples:

gp3

↓

GENERAL PURPOSE

io1 / io2

↓

HIGH IOPS

st1

↓

HIGH THROUGHPUT

sc1

↓

LOWEST COST HDD

Think:

EBS

=

CHOOSE STORAGE PERFORMANCE PROFILE

---

## EFS Performance Thinking

EFS is built around:

SHARED FILE ACCESS

and can support:

HUNDREDS OR THOUSANDS OF CLIENTS

Think:

MANY EC2

↓

SAME FILESYSTEM

↓

EFS

This makes EFS more appropriate for horizontally scaled applications that require shared files.

---

## EBS Backup Thinking

EBS uses:

[EBS Snapshots](https://chatgpt.com/c/EBS%20Snapshots)

for backup.

Think:

EBS

↓

SNAPSHOT

↓

BACKUP

Snapshots are also used to:

MOVE EBS BETWEEN AZs

Think:

EBS

↓

SNAPSHOT

↓

RESTORE IN NEW AZ

---

## EFS Shared Website Example

Your course specifically uses:

WORDPRESS

as an EFS example.

Imagine:

LOAD BALANCER

↓

EC2 WEB SERVER #1

EC2 WEB SERVER #2

EC2 WEB SERVER #3

↓

ALL NEED SAME WEBSITE FILES

↓

EFS

Think:

MULTIPLE WEB SERVERS

↓

SHARED CONTENT

↓

EFS

---

## Why Not EBS for Shared Web Files?

Imagine:

EC2 #1

↓

EBS #1

EC2 #2

↓

EBS #2

Now each server has:

SEPARATE FILES

That can create synchronization problems.

Instead:

EC2 #1

↘

EFS

↗

EC2 #2

Now both instances see:

THE SAME FILES

### Memory Trick

SHARED WEBSITE FILES

=

EFS

---

## EBS Multi-Attach vs EFS

Multi-Attach can make the comparison confusing.

### EBS Multi-Attach

io1 / io2

↓

SHARED BLOCK DEVICE

↓

SAME AZ

↓

UP TO 16 EC2 INSTANCES

↓

CLUSTER-AWARE FILESYSTEM REQUIRED

### EFS

NFS FILESYSTEM

↓

MANY EC2 INSTANCES

↓

MULTI-AZ

↓

DESIGNED FOR SHARED FILE ACCESS

Think:

SPECIALIZED SHARED BLOCK STORAGE

↓

EBS MULTI-ATTACH

NORMAL SHARED LINUX FILESYSTEM

↓

EFS

---

## EBS vs EFS vs Instance Store

### EBS

NETWORK

BLOCK

PERSISTENT

### EFS

NETWORK

FILE

SHARED

### Instance Store

LOCAL

VERY FAST

TEMPORARY

Think:

PERSISTENT HARD DRIVE

↓

EBS

SHARED NETWORK FOLDER

↓

EFS

FAST TEMPORARY DISK

↓

[EC2 Instance Store](https://chatgpt.com/c/EC2%20Instance%20Store)

---

## Architecture Thinking

### Single Server Database

EC2

↓

EBS

Think:

DATABASE DISK

=

EBS

---

### Shared Web Application

LOAD BALANCER

↓

EC2

EC2

EC2

↓

EFS

Think:

SHARED APPLICATION FILES

=

EFS

---

### Temporary Processing

EC2

↓

INSTANCE STORE

Think:

CACHE / SCRATCH

=

INSTANCE STORE

---

## Scenario Recognition

Need persistent block storage for one EC2 instance?

→ EBS

---

Need an EC2 boot volume?

→ EBS

---

Need a high-IOPS database disk?

→ EBS io1 / io2

---

Need multiple Linux EC2 instances to access the same files?

→ EFS

---

Need shared WordPress files across many EC2 instances?

→ EFS

---

Need storage shared across Availability Zones?

→ EFS

---

Need to move an EBS volume between AZs?

→ EBS Snapshot + Restore

---

Need a filesystem that automatically grows?

→ EFS

---

Need predictable provisioned block storage capacity?

→ EBS

---

Need lowest-cost shared file storage for infrequently accessed files?

→ EFS storage tiers

---

Need extremely fast temporary local storage?

→ EC2 Instance Store

---

Need multiple EC2 instances in one AZ sharing a high-performance block device?

→ EBS Multi-Attach

---

## Exam Traps

EBS

=

BLOCK STORAGE

EFS

=

FILE STORAGE

EBS

=

AZ LOCKED

EFS

=

MULTI-AZ CAPABLE

EBS

=

ONE INSTANCE NORMALLY

EFS

=

MANY INSTANCES

EBS

=

PROVISION CAPACITY

EFS

=

AUTO SCALE CAPACITY

EBS

=

EC2 DISK

EFS

=

SHARED LINUX FILESYSTEM

EFS

=

NFS + POSIX

EFS

=

HIGHER PRICE POINT

EFS STORAGE TIERS

=

COST OPTIMIZATION

MULTIPLE SERVERS + SAME FILES

=

EFS

MULTIPLE SERVERS + SAME BLOCK DEVICE

=

EBS MULTI-ATTACH

---

## Quick Cheat Sheet

EBS

=

ELASTIC BLOCK STORE

EFS

=

ELASTIC FILE SYSTEM

EBS TYPE

=

BLOCK

EFS TYPE

=

FILE

EBS CONNECTION

=

NETWORK

EFS CONNECTION

=

NETWORK / NFS

EBS CLIENTS

=

ONE EC2 NORMALLY

EFS CLIENTS

=

MANY EC2

EBS LOCATION

=

ONE AZ

EFS STANDARD

=

MULTI-AZ

EBS CAPACITY

=

PROVISIONED

EFS CAPACITY

=

AUTOMATIC

EBS BOOT VOLUME

=

YES

EFS BOOT VOLUME

=

NO

EFS OS

=

LINUX

EBS BACKUP

=

SNAPSHOT

SHARED WEBSITE FILES

=

EFS

DATABASE DISK

=

EBS

TEMPORARY FAST DISK

=

INSTANCE STORE

---

## Master Memory Trick

ONE SERVER

↓

EBS

MANY SERVERS

↓

EFS

DISK

↓

EBS

SHARED FOLDER

↓

EFS

ONE AZ

↓

EBS

MULTI-AZ

↓

EFS

FAST TEMPORARY LOCAL STORAGE

↓

INSTANCE STORE

Think:

EBS

=

MY HARD DRIVE

EFS

=

OUR SHARED DRIVE

---

## Related Notes

- [EBS Volumes](https://chatgpt.com/c/EBS%20Volumes)
    
- [EBS Volume Types](https://chatgpt.com/c/EBS%20Volume%20Types)
    
- [EBS Snapshots](https://chatgpt.com/c/EBS%20Snapshots)
    
- [EBS Multi-Attach](https://chatgpt.com/c/EBS%20Multi-Attach)
    
- [EFS](https://chatgpt.com/c/EFS)
    
- [EC2 Instance Store](https://chatgpt.com/c/EC2%20Instance%20Store)
    
- [EC2](https://chatgpt.com/c/EC2)
    
- [SAA EC2 Storage Cheat Sheet](https://chatgpt.com/c/SAA%20EC2%20Storage%20Cheat%20Sheet)
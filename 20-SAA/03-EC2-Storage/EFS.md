## What Problem Does It Solve?

EFS provides:

SHARED FILE STORAGE

for:

MULTIPLE EC2 INSTANCES

Instead of attaching separate storage to each EC2 instance, many EC2 instances can access the same filesystem.

Think:

EC2 #1

↘

EFS

↗

EC2 #2

### Memory Trick

EFS = SHARED LINUX FILESYSTEM

---

## What Is EFS?

EFS stands for:

ELASTIC FILE SYSTEM

EFS is a:

MANAGED NETWORK FILE SYSTEM

It uses:

NFS

which stands for:

NETWORK FILE SYSTEM

Your course specifies:

NFSv4.1

Think:

EC2

↓

NETWORK

↓

EFS

### Memory Trick

EFS = MANAGED NFS

---

## Shared Storage

The major advantage of EFS is:

MULTIPLE EC2 INSTANCES

can access:

THE SAME FILESYSTEM

Think:

EC2 #1

↓

EFS

↑

EC2 #2

↑

EC2 #3

This makes EFS useful when multiple servers need access to the same files.

---

## EFS and Multiple Availability Zones

Unlike:

[EBS Volumes](https://chatgpt.com/c/EBS%20Volumes)

which are normally locked to:

ONE AVAILABILITY ZONE

EFS can work with EC2 instances across:

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

EBS = ONE AZ

EFS = MULTI-AZ

---

## High Availability

EFS is designed to be:

HIGHLY AVAILABLE

and:

SCALABLE

A standard EFS filesystem can support EC2 instances across multiple Availability Zones.

Think:

AZ-A

↓

EC2

↘

EFS

↗

EC2

↓

AZ-B

This makes EFS useful for applications that need shared storage without tying the filesystem to one EC2 instance.

---

## Linux Compatibility

EFS is designed primarily for:

LINUX

It uses:

NFS

and provides a:

POSIX-COMPATIBLE FILESYSTEM

Think:

LINUX EC2

↓

NFS

↓

EFS

Your course specifically notes that EFS is compatible with Linux-based AMIs and not Windows-based EC2 workloads.

### Memory Trick

EFS = LINUX

For Windows shared filesystems, think:

[FSx for Windows File Server](https://chatgpt.com/c/FSx%20for%20Windows%20File%20Server)

---

## POSIX File System

EFS provides a:

POSIX FILESYSTEM

This means applications can interact with files using normal Linux-style file operations.

Think:

APPLICATION

↓

NORMAL FILE API

↓

EFS

This differs from:

[S3](https://chatgpt.com/c/S3)

which provides:

OBJECT STORAGE

not a traditional filesystem.

---

## EFS Security Groups

Access to EFS is controlled using:

SECURITY GROUPS

Think:

EC2

↓

SECURITY GROUP RULES

↓

EFS

The security group controls which resources can connect to the EFS mount target.

### Memory Trick

EFS NETWORK ACCESS

=

SECURITY GROUP

---

## EFS Encryption

EFS supports:

ENCRYPTION AT REST

using:

[AWS KMS](https://chatgpt.com/c/AWS%20KMS)

Think:

EFS DATA

↓

KMS

↓

ENCRYPTED STORAGE

This provides protection for files stored inside the filesystem.

---

## Automatic Scaling

EFS storage automatically:

GROWS

and

SHRINKS

as files are added and removed.

You do not need to provision a fixed storage capacity ahead of time.

Think:

ADD FILES

↓

EFS GROWS

REMOVE FILES

↓

EFS SHRINKS

### Memory Trick

EFS = NO CAPACITY PLANNING

---

## EFS Pricing Model

EFS uses:

PAY-PER-USE

storage.

Think:

USE STORAGE

↓

PAY FOR STORAGE USED

You do not provision a fixed disk size like you do with EBS.

### EBS

PROVISION STORAGE

↓

PAY FOR PROVISIONED CAPACITY

### EFS

USE STORAGE

↓

PAY FOR USED CAPACITY

---

## EFS Common Use Cases

Your course highlights:

- Content management
    
- Web serving
    
- Data sharing
    
- WordPress
    

Think:

MULTIPLE WEB SERVERS

↓

SHARED WEBSITE FILES

↓

EFS

A common architecture is:

LOAD BALANCER

↓

MULTIPLE EC2 WEB SERVERS

↓

SHARED EFS FILESYSTEM

---

## EFS Scaling

EFS can support:

THOUSANDS OF CONCURRENT NFS CLIENTS

and can scale to:

PETABYTE-SCALE STORAGE

automatically.

Think:

MORE CLIENTS

MORE FILES

↓

EFS SCALES

### Memory Trick

EFS = ELASTIC FILESYSTEM

---

## EFS Performance Modes

Your course introduces two performance modes:

GENERAL PURPOSE

and

MAX I/O

Performance Mode is selected when the filesystem is created.

---

## General Purpose Performance Mode

General Purpose is:

THE DEFAULT

It is optimized for:

LATENCY-SENSITIVE APPLICATIONS

Examples include:

- Web servers
    
- Content management systems
    

Think:

LOWER LATENCY

↓

GENERAL PURPOSE

### Memory Trick

GENERAL PURPOSE = NORMAL EFS

---

## Max I/O Performance Mode

Max I/O is designed for:

HIGHLY PARALLEL WORKLOADS

It provides:

HIGHER THROUGHPUT

but also:

HIGHER LATENCY

Examples include:

- Big Data
    
- Media processing
    

Think:

MANY PARALLEL OPERATIONS

↓

MAX I/O

### Memory Trick

MAX I/O

=

MORE SCALE + MORE LATENCY

---

## EFS Throughput Modes

Your course introduces:

BURSTING

PROVISIONED

ELASTIC

---

## Bursting Throughput

With Bursting mode:

THROUGHPUT

depends partly on:

FILESYSTEM SIZE

Think:

MORE EFS STORAGE

↓

MORE AVAILABLE THROUGHPUT

Your course example:

1 TB

↓

50 MiB/s BASELINE

with bursts up to:

100 MiB/s

---

## Provisioned Throughput

Provisioned Throughput allows you to specify:

THROUGHPUT

independently from:

FILESYSTEM SIZE

Think:

SMALL FILESYSTEM

HIGH THROUGHPUT REQUIREMENT

↓

PROVISIONED THROUGHPUT

### Memory Trick

PROVISIONED

=

CHOOSE THROUGHPUT YOURSELF

---

## Elastic Throughput

Elastic Throughput automatically:

SCALES UP

and

SCALES DOWN

based on workload demand.

Think:

WORKLOAD ↑

↓

THROUGHPUT ↑

WORKLOAD ↓

↓

THROUGHPUT ↓

This is useful for:

UNPREDICTABLE WORKLOADS

### Memory Trick

ELASTIC THROUGHPUT

=

AWS ADJUSTS AUTOMATICALLY

---

## EFS Storage Classes

EFS provides different storage tiers based on:

ACCESS FREQUENCY

Your course introduces:

STANDARD

↓

INFREQUENT ACCESS

↓

ARCHIVE

Think:

HOT FILES

↓

STANDARD

WARM FILES

↓

EFS-IA

COLD FILES

↓

ARCHIVE

---

## EFS Standard

EFS Standard is designed for:

FREQUENTLY ACCESSED FILES

Think:

ACTIVE FILES

↓

STANDARD

---

## EFS Infrequent Access

EFS-IA stands for:

EFS INFREQUENT ACCESS

It provides:

LOWER STORAGE COST

for files that are not accessed often.

However:

RETRIEVAL COST

applies when those files are accessed.

Think:

INFREQUENT FILE

↓

LOWER STORAGE COST

RETRIEVAL COST

### Memory Trick

EFS-IA

=

CHEAPER STORAGE + PAY TO RETRIEVE

---

## EFS Archive

EFS Archive is designed for:

RARELY ACCESSED FILES

Your course describes files accessed only:

A FEW TIMES EACH YEAR

Think:

VERY COLD FILES

↓

EFS ARCHIVE

It provides an even lower-cost storage option for long-lived data with very infrequent access.

---

## EFS Lifecycle Management

EFS supports:

LIFECYCLE POLICIES

These automatically move files between storage tiers based on how long they have not been accessed.

Think:

EFS STANDARD

↓

NO ACCESS FOR N DAYS

↓

EFS-IA / ARCHIVE

### Memory Trick

LIFECYCLE

=

AUTOMATIC COST OPTIMIZATION

---

## EFS Standard vs One Zone

EFS also provides different availability options.

### EFS Standard

Stores data across:

MULTIPLE AVAILABILITY ZONES

Think:

PRODUCTION

↓

MULTI-AZ

↓

EFS STANDARD

### EFS One Zone

Stores data in:

ONE AVAILABILITY ZONE

Think:

LOWER COST

↓

ONE AZ

↓

EFS ONE ZONE

---

## EFS One Zone Use Cases

Your course suggests One Zone for things such as:

DEVELOPMENT

and workloads where the lower availability model is acceptable.

Think:

PRODUCTION + HIGH AVAILABILITY

↓

STANDARD

LOWER COST + ONE AZ ACCEPTABLE

↓

ONE ZONE

One Zone can also work with infrequent access storage:

EFS ONE ZONE-IA

---

## EFS vs EBS

This is one of the most important storage comparisons for SAA.

### EBS

BLOCK STORAGE

↓

ONE EC2 NORMALLY

↓

ONE AZ

### EFS

FILE STORAGE

↓

MANY EC2

↓

MULTI-AZ

Think:

EC2 HARD DRIVE

↓

EBS

SHARED NETWORK FOLDER

↓

EFS

### Memory Trick

EBS = BLOCK

EFS = FILE

---

## EFS vs EBS Multi-Attach

Do not confuse:

[EBS Multi-Attach](https://chatgpt.com/c/EBS%20Multi-Attach)

with:

EFS

### EBS Multi-Attach

SHARED BLOCK STORAGE

↓

io1 / io2

↓

SAME AZ

↓

MAX 16 EC2

### EFS

SHARED FILE STORAGE

↓

MANY EC2

↓

MULTI-AZ

Think:

SPECIALIZED SHARED BLOCK DEVICE

↓

EBS MULTI-ATTACH

NORMAL SHARED LINUX FILESYSTEM

↓

EFS

---

## EFS vs Instance Store

[EC2 Instance Store](https://chatgpt.com/c/EC2%20Instance%20Store)

=

LOCAL + TEMPORARY

EFS

=

NETWORK + SHARED + PERSISTENT

Think:

VERY FAST TEMPORARY LOCAL STORAGE

↓

INSTANCE STORE

SHARED FILES ACROSS SERVERS

↓

EFS

---

## EFS vs S3

EFS

=

FILE STORAGE

[S3](https://chatgpt.com/c/S3)

=

OBJECT STORAGE

Think:

LINUX FILESYSTEM

↓

EFS

BUCKET + OBJECTS

↓

S3

### Exam Trap

Need a filesystem that applications can mount?

→ EFS

Need scalable object storage accessed through S3 APIs?

→ S3

---

## EFS Architecture Thinking

A common architecture is:

USERS

↓

LOAD BALANCER

↓

EC2 #1

EC2 #2

EC2 #3

↓

SHARED EFS

All EC2 instances can access:

THE SAME APPLICATION FILES

This avoids storing separate copies of shared files on every EC2 server.

---

## Scenario Recognition

Need shared storage across multiple EC2 instances?

→ EFS

---

Need a managed NFS filesystem?

→ EFS

---

Need Linux EC2 instances in multiple AZs to access the same files?

→ EFS

---

Need a POSIX-compliant shared filesystem?

→ EFS

---

Need storage that automatically grows and shrinks?

→ EFS

---

Need no storage capacity planning?

→ EFS

---

Need shared storage for WordPress servers?

→ EFS

---

Need shared content for multiple web servers?

→ EFS

---

Need frequently accessed EFS files?

→ EFS Standard

---

Need cheaper storage for infrequently accessed EFS files?

→ EFS-IA

---

Need very rarely accessed EFS files?

→ EFS Archive

---

Need files automatically moved to cheaper tiers?

→ EFS Lifecycle Management

---

Need throughput that automatically adapts to an unpredictable workload?

→ Elastic Throughput

---

Need Windows-native shared filesystem storage?

→ FSx for Windows, not EFS

---

Need block storage for one EC2 instance?

→ EBS, not EFS

---

## Exam Traps

EFS

=

ELASTIC FILE SYSTEM

EFS

=

MANAGED NFS

EFS

=

FILE STORAGE

EFS

=

LINUX / POSIX

EFS

=

MANY EC2 INSTANCES

EFS

=

MULTI-AZ WITH STANDARD

EFS

=

AUTO-SCALING STORAGE

EFS

=

PAY PER USE

EFS ACCESS

=

SECURITY GROUPS

EFS ENCRYPTION

=

KMS

EFS ≠ EBS

EFS ≠ S3

EFS ≠ WINDOWS-NATIVE FILESYSTEM

STANDARD

=

FREQUENT ACCESS

EFS-IA

=

INFREQUENT ACCESS

ARCHIVE

=

RARE ACCESS

ONE ZONE

=

ONE AZ + LOWER COST

LIFECYCLE POLICY

=

AUTOMATIC TIERING

---

## Quick Cheat Sheet

EFS

=

ELASTIC FILE SYSTEM

TYPE

=

MANAGED FILE STORAGE

PROTOCOL

=

NFSv4.1

OPERATING SYSTEM

=

LINUX

FILESYSTEM

=

POSIX

SHARED ACCESS

=

MANY EC2 INSTANCES

STANDARD AVAILABILITY

=

MULTI-AZ

SCALING

=

AUTOMATIC

CAPACITY PLANNING

=

NONE

PRICING

=

PAY PER USE

NETWORK SECURITY

=

SECURITY GROUP

ENCRYPTION AT REST

=

KMS

GENERAL PURPOSE

=

DEFAULT + LATENCY SENSITIVE

MAX I/O

=

HIGHLY PARALLEL

BURSTING

=

THROUGHPUT RELATED TO SIZE

PROVISIONED

=

SET THROUGHPUT

ELASTIC

=

AUTO-SCALE THROUGHPUT

STANDARD

=

FREQUENT FILES

EFS-IA

=

INFREQUENT FILES

ARCHIVE

=

RARE FILES

ONE ZONE

=

SINGLE AZ

---

## Master Memory Trick

EBS

=

ONE SERVER HARD DRIVE

EFS

=

SHARED LINUX NETWORK DRIVE

S3

=

OBJECT STORAGE

INSTANCE STORE

=

FAST TEMPORARY LOCAL DISK

Think:

MANY LINUX EC2

↓

NEED SAME FILES

↓

EFS

---

## Related Notes

- [EBS Volumes](https://chatgpt.com/c/EBS%20Volumes)
    
- [EBS Multi-Attach](https://chatgpt.com/c/EBS%20Multi-Attach)
    
- [EC2 Instance Store](https://chatgpt.com/c/EC2%20Instance%20Store)
    
- [EC2](https://chatgpt.com/c/EC2)
    
- [AWS KMS](https://chatgpt.com/c/AWS%20KMS)
    
- [S3](https://chatgpt.com/c/S3)
    
- [FSx](https://chatgpt.com/c/FSx)
    
- [FSx for Windows File Server](https://chatgpt.com/c/FSx%20for%20Windows%20File%20Server)
    
- [SAA EC2 Storage Cheat Sheet](https://chatgpt.com/c/SAA%20EC2%20Storage%20Cheat%20Sheet)
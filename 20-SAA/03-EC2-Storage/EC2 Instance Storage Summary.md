## What Problem Does It Solve?

EC2 supports several storage options.

The challenge is knowing:

WHICH STORAGE SERVICE

to choose for:

WHICH WORKLOAD

Think:

EC2 STORAGE REQUIREMENT

↓

PERSISTENT DISK?

SHARED FILES?

TEMPORARY HIGH SPEED?

BACKUP?

SERVER TEMPLATE?

↓

CHOOSE THE RIGHT STORAGE OPTION

### Memory Trick

EC2 STORAGE

=

MATCH STORAGE TO THE WORKLOAD

---

## EC2 Storage Options

The main storage concepts in this section are:

[EBS Volumes](https://chatgpt.com/c/EBS%20Volumes)

↓

PERSISTENT BLOCK STORAGE

[EBS Snapshots](https://chatgpt.com/c/EBS%20Snapshots)

↓

EBS BACKUP

[AMI](https://chatgpt.com/c/AMI)

↓

EC2 MACHINE TEMPLATE

[EC2 Instance Store](https://chatgpt.com/c/EC2%20Instance%20Store)

↓

FAST TEMPORARY LOCAL STORAGE

[EFS](https://chatgpt.com/c/EFS)

↓

SHARED LINUX FILESYSTEM

Think:

DISK

↓

EBS

BACKUP

↓

SNAPSHOT

SERVER TEMPLATE

↓

AMI

TEMPORARY SPEED

↓

INSTANCE STORE

SHARED FILES

↓

EFS

---

## EBS Volumes

EBS provides:

NETWORK-ATTACHED BLOCK STORAGE

for EC2.

Think:

EC2

↓

NETWORK

↓

EBS

EBS is generally:

ONE VOLUME

↓

ONE EC2 INSTANCE

except for:

[EBS Multi-Attach](https://chatgpt.com/c/EBS%20Multi-Attach)

with certain:

io1 / io2

volumes.

### Memory Trick

EBS = EC2 HARD DRIVE

---

## EBS Availability Zone Rule

EBS volumes are:

LOCKED TO ONE AVAILABILITY ZONE

Think:

EBS

↓

ONE AZ

To move EBS storage to another AZ:

EBS

↓

SNAPSHOT

↓

RESTORE

↓

NEW EBS IN NEW AZ

### Memory Trick

MOVE EBS

=

SNAPSHOT + RESTORE

---

## EBS Snapshots

EBS Snapshots provide:

POINT-IN-TIME BACKUPS

of:

EBS VOLUMES

Think:

EBS

↓

SNAPSHOT

↓

BACKUP

Snapshots can also be used to:

TRANSFER EBS DATA BETWEEN AZs

Think:

AZ-A

↓

EBS

↓

SNAPSHOT

↓

RESTORE

↓

EBS

↓

AZ-B

### Memory Trick

SNAPSHOT = EBS BACKUP

---

## AMI

AMI stands for:

AMAZON MACHINE IMAGE

AMI provides:

READY-TO-LAUNCH EC2 CONFIGURATION

Think:

CONFIGURED EC2

↓

CREATE AMI

↓

LAUNCH NEW EC2

AMI can include:

- Operating system
    
- Software
    
- Configuration
    
- Monitoring
    

### Memory Trick

AMI = EC2 TEMPLATE

---

## AMI vs Snapshot

Do not confuse:

AMI

and

EBS SNAPSHOT

AMI

=

SERVER TEMPLATE

EBS SNAPSHOT

=

DISK BACKUP

Think:

BUILD EC2

↓

AMI

RESTORE EBS DATA

↓

SNAPSHOT

---

## EC2 Image Builder

EC2 Image Builder is used to:

AUTOMATE IMAGE CREATION

It can automate:

BUILD

↓

TEST

↓

MAINTAIN

↓

DISTRIBUTE

EC2 images.

Think:

MANUAL AMI PROCESS

↓

EC2 IMAGE BUILDER

↓

AUTOMATED AMI PIPELINE

### Memory Trick

IMAGE BUILDER

=

AUTOMATE AMIs

---

## EC2 Instance Store

Instance Store provides:

HIGH-PERFORMANCE LOCAL HARDWARE STORAGE

Think:

EC2 HOST

↓

LOCAL DISK

↓

INSTANCE STORE

It provides:

VERY HIGH I/O PERFORMANCE

but is:

EPHEMERAL

Think:

FAST

TEMPORARY

---

## Instance Store Data Loss

If the EC2 instance is:

STOPPED

or:

TERMINATED

Instance Store data is lost.

Think:

STOP / TERMINATE

↓

INSTANCE STORE

↓

DATA LOST

Best use cases include:

- Cache
    
- Buffer
    
- Scratch data
    
- Temporary content
    

### Memory Trick

INSTANCE STORE

=

FAST + TEMPORARY

---

## EFS

EFS stands for:

ELASTIC FILE SYSTEM

EFS provides:

SHARED NETWORK FILE STORAGE

Think:

EC2 #1

↘

EFS

↗

EC2 #2

EFS can be mounted by:

MANY EC2 INSTANCES

and can work across:

MULTIPLE AVAILABILITY ZONES

### Memory Trick

EFS = SHARED LINUX DRIVE

---

## EFS vs EBS

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

MY HARD DRIVE

↓

EBS

OUR SHARED DRIVE

↓

EFS

---

## EFS Infrequent Access

EFS provides lower-cost storage tiers for files that are:

NOT ACCESSED OFTEN

Think:

ACTIVE FILE

↓

EFS STANDARD

OLD / INFREQUENT FILE

↓

EFS-IA

Lifecycle policies can automatically move files to cheaper storage classes.

### Memory Trick

EFS-IA

=

CHEAPER INFREQUENT FILES

---

## FSx Storage Preview

Your course summary also introduces:

FSx

for specialized file systems.

### FSx for Windows File Server

Think:

WINDOWS SHARED FILESYSTEM

↓

FSx FOR WINDOWS

### FSx for Lustre

Think:

HIGH-PERFORMANCE COMPUTING

↓

FSx FOR LUSTRE

We'll cover these separately later.

---

## Storage Architecture Thinking

Start by asking:

WHAT KIND OF STORAGE DOES THE APPLICATION NEED?

### Persistent EC2 Disk

EC2

↓

EBS

---

### Shared Linux Files

MULTIPLE EC2

↓

EFS

---

### Extremely Fast Temporary Disk

EC2

↓

INSTANCE STORE

---

### EBS Backup

EBS

↓

SNAPSHOT

---

### Reusable EC2 Configuration

EC2

↓

AMI

---

### Automated AMI Creation

EC2 IMAGE BUILDER

↓

BUILD + TEST + DISTRIBUTE AMIs

---

## Storage Decision Tree

Need:

PERSISTENT BLOCK STORAGE?

↓

EBS

Need:

BACKUP OF EBS?

↓

EBS SNAPSHOT

Need:

REUSABLE EC2 SERVER IMAGE?

↓

AMI

Need:

AUTOMATED AMI PIPELINE?

↓

EC2 IMAGE BUILDER

Need:

VERY FAST TEMPORARY LOCAL DISK?

↓

INSTANCE STORE

Need:

SHARED LINUX FILESYSTEM?

↓

EFS

Need:

WINDOWS SHARED FILESYSTEM?

↓

FSx FOR WINDOWS

Need:

HPC FILESYSTEM?

↓

FSx FOR LUSTRE

---

## Scenario Recognition

Need a persistent virtual disk attached to EC2?

→ EBS

---

Need to move an EBS volume to another AZ?

→ Snapshot + Restore

---

Need a backup of an EBS volume?

→ EBS Snapshot

---

Need to preserve a reusable EC2 configuration?

→ AMI

---

Need to launch many identically configured EC2 instances?

→ AMI

---

Need to automate building and testing AMIs?

→ EC2 Image Builder

---

Need very high-performance temporary storage?

→ EC2 Instance Store

---

Need cache or scratch storage where data loss is acceptable?

→ EC2 Instance Store

---

Need many Linux EC2 instances to access the same files?

→ EFS

---

Need shared WordPress or web-server files?

→ EFS

---

Need cheaper EFS storage for infrequently accessed files?

→ EFS-IA / EFS storage tiers

---

Need Windows-native shared file storage?

→ FSx for Windows File Server

---

Need a high-performance filesystem for HPC?

→ FSx for Lustre

---

## Exam Traps

EBS

=

BLOCK STORAGE

EFS

=

FILE STORAGE

INSTANCE STORE

=

LOCAL TEMPORARY STORAGE

SNAPSHOT

=

EBS BACKUP

AMI

=

EC2 TEMPLATE

IMAGE BUILDER

=

AUTOMATE AMI CREATION

EBS

=

AZ LOCKED

MOVE EBS ACROSS AZ

=

SNAPSHOT + RESTORE

EFS

=

MANY EC2 + SHARED FILES

INSTANCE STORE STOPPED

=

DATA LOST

EBS ≠ EFS

EBS ≠ INSTANCE STORE

AMI ≠ SNAPSHOT

EFS ≠ WINDOWS FILESYSTEM

FSx FOR WINDOWS

=

WINDOWS FILESYSTEM

FSx FOR LUSTRE

=

HPC FILESYSTEM

---

## Quick Cheat Sheet

EBS

=

PERSISTENT BLOCK STORAGE

EBS LOCATION

=

ONE AZ

EBS BACKUP

=

SNAPSHOT

MOVE EBS

=

SNAPSHOT + RESTORE

AMI

=

READY-TO-USE EC2 TEMPLATE

EC2 IMAGE BUILDER

=

AUTOMATE BUILD + TEST + DISTRIBUTE AMIs

INSTANCE STORE

=

LOCAL HIGH PERFORMANCE

INSTANCE STORE

=

EPHEMERAL

STOP INSTANCE STORE EC2

=

DATA LOST

EFS

=

SHARED NETWORK FILESYSTEM

EFS

=

LINUX + NFS

EFS

=

MANY EC2

EFS STANDARD

=

MULTI-AZ

EFS-IA

=

INFREQUENT ACCESS COST SAVINGS

FSx WINDOWS

=

WINDOWS FILESYSTEM

FSx LUSTRE

=

HPC FILESYSTEM

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

SERVER TEMPLATE

IMAGE BUILDER

=

AMI FACTORY

INSTANCE STORE

=

FAST TEMPORARY DISK

EFS

=

SHARED LINUX DRIVE

FSx WINDOWS

=

WINDOWS DRIVE

FSx LUSTRE

=

HPC DRIVE

Think:

EC2 STORAGE QUESTION

↓

ASK WHAT THE DATA NEEDS

↓

PERSISTENT?

SHARED?

TEMPORARY?

BACKUP?

TEMPLATE?

SPECIALIZED FILESYSTEM?

↓

CHOOSE THE SERVICE

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
    
- [EC2 Image Builder](https://chatgpt.com/c/EC2%20Image%20Builder)
    
- [FSx](https://chatgpt.com/c/FSx)
    
- [FSx for Windows File Server](https://chatgpt.com/c/FSx%20for%20Windows%20File%20Server)
    
- [FSx for Lustre](https://chatgpt.com/c/FSx%20for%20Lustre)
    
- [SAA EC2 Storage Cheat Sheet](https://chatgpt.com/c/SAA%20EC2%20Storage%20Cheat%20Sheet)
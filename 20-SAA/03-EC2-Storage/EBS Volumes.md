## What Problem Does It Solve?

EBS provides:

PERSISTENT BLOCK STORAGE

for:

EC2 INSTANCES

Instead of storing important data on temporary local EC2 storage, you can attach a persistent virtual drive to an EC2 instance.

Think:

EC2 INSTANCE

↓

VIRTUAL HARD DRIVE

↓

EBS VOLUME

### Memory Trick

EBS = EC2 HARD DRIVE

---

## What Is EBS?

EBS stands for:

ELASTIC BLOCK STORE

An EBS Volume is:

NETWORK-ATTACHED BLOCK STORAGE

that can be attached to an EC2 instance.

Think:

EC2

↓

NETWORK

↓

EBS VOLUME

EBS is not a physical disk directly attached to the EC2 host.

Because EBS communicates with EC2 over the network, there can be some latency.

### Memory Trick

EBS = NETWORK HARD DRIVE

---

## Persistent Storage

One of the most important features of EBS is:

PERSISTENCE

EBS allows data to exist independently from the EC2 instance using it.

Think:

EC2 INSTANCE

↓

EBS VOLUME

↓

PERSISTENT DATA

This makes EBS useful for workloads that need data to survive beyond the normal lifecycle of an EC2 instance.

---

## EBS and Availability Zones

EBS volumes are:

LOCKED TO AN AVAILABILITY ZONE

Example:

EBS Volume

↓

us-east-1a

That volume can attach to an EC2 instance in:

us-east-1a

But it cannot directly attach to an EC2 instance in:

us-east-1b

Think:

EBS

↓

ONE AZ

### Memory Trick

EBS = AZ LOCKED

---

## Moving EBS Between Availability Zones

You cannot directly move an EBS volume from one Availability Zone to another.

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

Example:

EBS

us-east-1a

↓

SNAPSHOT

↓

RESTORE

↓

EBS

us-east-1b

We'll cover this further in:

[EBS Snapshots](https://chatgpt.com/c/EBS%20Snapshots)

### Memory Trick

MOVE EBS ACROSS AZ

=

SNAPSHOT + RESTORE

---

## Attaching EBS Volumes

An EC2 instance can have:

MULTIPLE EBS VOLUMES

Think:

EC2 INSTANCE

↓

ROOT EBS

ADDITIONAL EBS VOLUMES

EBS volumes can also be detached from one EC2 instance and attached to another EC2 instance in the same Availability Zone.

Think:

EC2-A

↓

DETACH EBS

↓

ATTACH EBS

↓

EC2-B

---

## EBS Multi-Attach

Normally think:

ONE EBS VOLUME

↓

ONE EC2 INSTANCE

However, SAA introduces an important exception:

MULTI-ATTACH

Certain:

io1

and

io2

EBS volumes can support attachment to multiple EC2 instances.

Think:

EC2

↘

EBS io1/io2

↗

EC2

We'll cover these volume types further in:

[EBS Volume Types](https://chatgpt.com/c/EBS%20Volume%20Types)

### Exam Trap

EBS can NEVER attach to multiple EC2 instances.

❌ WRONG

Certain io1/io2 volumes support:

MULTI-ATTACH

---

## EBS Capacity

EBS volumes have:

PROVISIONED CAPACITY

You choose the amount of storage required.

For example:

10 GB

50 GB

100 GB

500 GB

You are billed for the capacity that you provision.

Think:

PROVISION EBS STORAGE

↓

PAY FOR PROVISIONED CAPACITY

The capacity of an EBS volume can also be increased over time.

---

## EBS Performance

Depending on the EBS volume type, performance can involve:

IOPS

and

THROUGHPUT

Different workloads require different storage performance.

For example:

GENERAL WORKLOAD

↓

GENERAL PURPOSE SSD

DATABASE / HIGH IOPS

↓

PROVISIONED IOPS SSD

We'll cover this separately in:

[EBS Volume Types](https://chatgpt.com/c/EBS%20Volume%20Types)

---

## Delete on Termination

EBS has an important setting called:

DELETE ON TERMINATION

This controls what happens to an EBS volume when its EC2 instance is terminated.

### Root EBS Volume

By default:

EC2 TERMINATED

↓

ROOT EBS VOLUME

↓

DELETED

### Additional EBS Volume

By default:

EC2 TERMINATED

↓

ADDITIONAL EBS VOLUME

↓

PRESERVED

Think:

ROOT

=

DELETE BY DEFAULT

ADDITIONAL

=

KEEP BY DEFAULT

---

## Preserving the Root Volume

You can change the:

DELETE ON TERMINATION

setting.

Scenario:

Need to terminate an EC2 instance but preserve its root EBS volume?

↓

DISABLE DELETE ON TERMINATION

Then:

EC2 TERMINATED

↓

ROOT EBS

↓

PRESERVED

### Memory Trick

ROOT DIES BY DEFAULT

EXTRA DRIVE SURVIVES BY DEFAULT

---

## EBS Architecture Thinking

Think of basic EC2 storage like this:

EC2 INSTANCE

↓

EBS VOLUME

↓

PERSISTENT DATA

The connection is:

EC2

↓

NETWORK

↓

EBS

And the location relationship is:

AVAILABILITY ZONE

↓

EC2 + EBS

Both must be in the same AZ for direct attachment.

---

## EBS vs Instance Store

EBS

=

NETWORK STORAGE

INSTANCE STORE

=

LOCAL HARDWARE STORAGE

EBS

=

PERSISTENT

INSTANCE STORE

=

EPHEMERAL

Think:

NEED DATA TO SURVIVE?

↓

EBS

NEED VERY FAST TEMPORARY LOCAL STORAGE?

↓

[EC2 Instance Store](https://chatgpt.com/c/EC2%20Instance%20Store)

---

## EBS vs EFS

EBS is primarily:

BLOCK STORAGE

for EC2.

[EFS](https://chatgpt.com/c/EFS) provides:

SHARED FILE STORAGE

Think:

ONE EC2 DISK

↓

EBS

SHARED FILESYSTEM ACROSS MANY EC2 INSTANCES

↓

EFS

---

## Scenario Recognition

Need persistent block storage for an EC2 instance?

→ EBS

---

Need a virtual hard drive for EC2?

→ EBS

---

Need storage that can persist independently from EC2?

→ EBS

---

Need to move an EBS volume to another Availability Zone?

→ EBS Snapshot + Restore

---

Need to preserve a root EBS volume after terminating EC2?

→ Disable Delete on Termination

---

Need to increase EBS storage capacity?

→ Increase the EBS volume size

---

Need extremely high-performance temporary local storage?

→ EC2 Instance Store

---

Need shared filesystem storage across many EC2 instances?

→ EFS

---

Need the same EBS volume attached to multiple EC2 instances?

→ io1/io2 Multi-Attach

---

## Exam Traps

EBS = BLOCK STORAGE

EBS = NETWORK STORAGE

EBS = PERSISTENT STORAGE

EBS = AZ LOCKED

EBS ≠ REGION-WIDE VOLUME

EBS cannot directly move between AZs

SNAPSHOT + RESTORE = MOVE BETWEEN AZs

ROOT EBS = DELETED BY DEFAULT

ADDITIONAL EBS = PRESERVED BY DEFAULT

EBS ≠ INSTANCE STORE

EBS ≠ EFS

io1/io2 = MULTI-ATTACH POSSIBILITY

---

## Quick Cheat Sheet

EBS

=

ELASTIC BLOCK STORE

EBS

=

BLOCK STORAGE

EBS

=

EC2 VIRTUAL HARD DRIVE

EBS

=

NETWORK ATTACHED

EBS

=

PERSISTENT

EBS

=

AZ LOCKED

MOVE TO ANOTHER AZ

=

SNAPSHOT + RESTORE

ROOT EBS

=

DELETE ON TERMINATION BY DEFAULT

ADDITIONAL EBS

=

PRESERVED BY DEFAULT

io1 / io2

=

MULTI-ATTACH SUPPORT

INSTANCE STORE

=

TEMPORARY LOCAL STORAGE

EFS

=

SHARED FILE STORAGE

---

## Master Memory Trick

EC2

=

COMPUTE

EBS

=

PERSISTENT HARD DRIVE

EBS LOCATION

=

ONE AZ

MOVE EBS

=

SNAPSHOT + RESTORE

ROOT VOLUME

=

DELETE BY DEFAULT

EXTRA VOLUME

=

KEEP BY DEFAULT

---

## Related Notes

- [EC2](https://chatgpt.com/c/EC2)
    
- [EBS Snapshots](https://chatgpt.com/c/EBS%20Snapshots)
    
- [EBS Volume Types](https://chatgpt.com/c/EBS%20Volume%20Types)
    
- [EC2 Instance Store](https://chatgpt.com/c/EC2%20Instance%20Store)
    
- [EFS](https://chatgpt.com/c/EFS)
    
- [AMI](https://chatgpt.com/c/AMI)
    
- [EC2 Hibernate](https://chatgpt.com/c/EC2%20Hibernate)
    
- [SAA EC2 Storage Cheat Sheet](https://chatgpt.com/c/SAA%20EC2%20Storage%20Cheat%20Sheet)
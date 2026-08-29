See also: [[EBS]]

See also: [[02-Compute/EC2]]

## What Problem Does It Solve?

Creates point-in-time backups of EBS volumes.

Snapshots allow you to protect EBS data and recreate volumes when needed.

---

## Type

EBS Backup

---

## What Is an EBS Snapshot?

An EBS Snapshot is a backup of an EBS volume at a specific point in time.

### Memory Trick

EBS Volume = Hard Drive

EBS Snapshot = Backup of Hard Drive

---

## Creating a Snapshot

You can create a snapshot of an EBS volume.

It is not necessary to detach the EBS volume before creating the snapshot.

However, your course notes recommend detaching the volume when possible.

---

## Moving EBS Data Across Availability Zones

EBS volumes are tied to a specific Availability Zone.

A volume cannot simply be moved directly from one AZ to another.

Instead:

EBS Volume

↓

Create Snapshot

↓

Create New EBS Volume from Snapshot

↓

Choose Different Availability Zone

### Memory Trick

Need to move EBS to another AZ?

Snapshot it.

---

## Copying Snapshots

EBS Snapshots can be copied across:

- Availability Zones
- Regions

This makes snapshots useful when EBS data needs to be recreated in another location.

---

## EBS Volume vs EBS Snapshot

| EBS Volume | EBS Snapshot |
|---|---|
| Active block storage | Point-in-time backup |
| Attached to EC2 | Backup of volume |
| Bound to an AZ | Can be copied |
| Stores live data | Used to recreate volumes |

---

## EBS Snapshot and AMI Relationship

Creating an AMI from an EC2 instance also creates EBS snapshots.

Basic Process:

EC2 Instance

↓

Customize Instance

↓

Create AMI

↓

EBS Snapshots Created

↓

Launch New EC2 Instances

See:

[[02-Compute/EC2]]

---

## Common Use Cases

- Backing up EBS volumes
- Protecting EC2 data
- Moving EBS data between Availability Zones
- Copying EBS data to another Region
- Creating reusable EC2 configurations through AMIs

---

## Exam Scenarios

An EBS volume needs a point-in-time backup.

→ EBS Snapshot

---

An EBS volume in us-east-1a needs to be recreated in us-east-1b.

→ Create an EBS Snapshot and create a new volume in the destination AZ

---

A company wants to copy EBS data to another AWS Region.

→ Copy the EBS Snapshot to the other Region

---

A company creates an AMI from an EC2 instance.

What storage backup is created as part of the process?

→ EBS Snapshots

---

## Exam Keywords

Snapshot

Point-in-time backup

EBS

Backup

Availability Zone

Region

AMI

---

## Memory Tricks

EBS = Live Disk

Snapshot = Backup

Different AZ = Snapshot

Different Region = Copy Snapshot

AMI = Uses EBS Snapshots
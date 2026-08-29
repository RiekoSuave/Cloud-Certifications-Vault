See also: [[03-Storage/EBS Snapshots]]

See also: [[03-Storage/EC2 Instance Store]]

See also: [[02-Compute/EC2]]

See also: [[03-Storage/EFS]]

## What Problem Does It Solve?

Provides persistent block storage for EC2 instances.

EBS acts like a virtual hard drive that can store data independently from the EC2 instance using it.

---

## Type

Block Storage

---

## What Is EBS?

EBS stands for:

Elastic Block Store

An EBS volume is a network drive that can be attached to an EC2 instance.

### Memory Trick

EBS = EC2 Hard Drive

---

## Persistent Storage

EBS provides persistent storage.

This means your data can remain available independently from the EC2 instance using the volume.

This makes EBS useful for data that must survive beyond the life of an individual EC2 instance.

---

## Network Drive

EBS is a network drive.

It is NOT a physical disk directly attached to the EC2 server.

Because communication occurs over the network, there can be some latency compared with directly attached hardware storage.

### Memory Trick

EBS = Network Drive

Instance Store = Hardware Drive

---

## Attaching EBS Volumes

At the CCP level:

One EBS volume is attached to one EC2 instance at a time.

However, at the Associate level, some EBS volumes support:

Multi-Attach

This becomes more relevant for SAA.

---

## Availability Zone Requirement

EBS volumes are tied to a specific Availability Zone.

Example:

An EBS volume in:

us-east-1a

cannot directly attach to an EC2 instance in:

us-east-1b

### Memory Trick

EBS = AZ-Bound

---

## Moving EBS Across Availability Zones

To move EBS data to another Availability Zone:

EBS Volume

↓

Create Snapshot

↓

Create Volume from Snapshot

↓

Use Volume in New AZ

See:

[[03-Storage/EBS Snapshots]]

---

## Detaching and Reattaching

An EBS volume can be:

- Detached from an EC2 instance
- Attached to another EC2 instance

This provides flexibility when moving persistent storage between instances.

---

## Provisioned Capacity

With EBS, you provision storage capacity.

Examples include:

- Storage size in GB
- IOPS

You are billed based on the capacity you provision.

Storage capacity can also be increased over time.

---

## Delete on Termination

EBS has a:

Delete on Termination

attribute.

This controls what happens to an EBS volume when its EC2 instance is terminated.

---

## Root EBS Volume

By default:

Root EBS Volume

→ Deleted when EC2 terminates

Delete on Termination:

Enabled

---

## Additional EBS Volumes

By default:

Additional attached EBS volumes

→ NOT deleted when EC2 terminates

Delete on Termination:

Disabled

---

## Why Change Delete on Termination?

You may want to preserve an EBS volume even after its EC2 instance is terminated.

Example:

EC2 Instance

↓

Terminated

↓

EBS Volume Remains

↓

Data Preserved

---

## EBS Snapshots

EBS volumes can be backed up using:

EBS Snapshots

A snapshot captures the state of an EBS volume at a point in time.

Snapshots can also help transfer EBS data across:

- Availability Zones
- Regions

See:

[[03-Storage/EBS Snapshots]]

---

## Common Use Cases

- EC2 operating system volumes
- Databases
- Application storage
- Persistent EC2 data
- Workloads requiring block storage

---

## EBS vs Instance Store

### EBS

- Network attached
- Persistent
- Can be detached
- Supports snapshots
- AZ-bound

### Instance Store

- Hardware attached
- Ephemeral
- Higher I/O performance
- Data can be lost when the instance stops
- Good for temporary data

See:

[[03-Storage/EC2 Instance Store]]

---

## EBS vs EFS

### EBS

Block storage primarily associated with EC2 instances.

### EFS

Shared network file system that can be mounted by many EC2 instances.

| EBS | EFS |
|---|---|
| Block storage | File storage |
| AZ-bound | Multi-AZ |
| EC2 disk | Shared filesystem |
| Provision capacity | Automatically scales |

See:

[[03-Storage/EFS]]

---

## Compare Against

S3 → Object storage

EFS → Shared file storage

EC2 Instance Store → Temporary high-performance hardware storage

---

## Exam Scenarios

An EC2 instance needs persistent block storage.

→ EBS

---

An EC2 volume needs to be moved from one Availability Zone to another.

→ Create an EBS Snapshot and create a new volume in the destination AZ

---

A company needs data to remain after an EC2 instance is terminated.

→ Use persistent EBS storage and configure Delete on Termination appropriately

---

An application needs very high-performance temporary local storage.

→ EC2 Instance Store

---

Multiple Linux EC2 instances need simultaneous access to the same filesystem.

→ EFS

---

## Exam Keywords

Block storage

Persistent

EC2

Volume

Availability Zone

IOPS

Snapshot

Delete on Termination

---

## Memory Tricks

EBS = EC2 Hard Drive

EBS = Persistent

EBS = Network Drive

EBS = AZ-Bound

Snapshot = Backup / Move EBS

Instance Store = Temporary Hardware Disk
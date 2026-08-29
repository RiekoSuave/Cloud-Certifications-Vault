## What Problem Does It Solve?

Different workloads need different combinations of:

COST

↓

IOPS

↓

THROUGHPUT

↓

LATENCY

EBS provides multiple volume types so you can choose the right storage characteristics for the workload.

Think:

WORKLOAD REQUIREMENTS

↓

CHOOSE EBS TYPE

### Memory Trick

EBS TYPE

=

MATCH STORAGE TO WORKLOAD

---

## EBS Volume Types Overview

Your course groups EBS volumes into:

SSD

and

HDD

### SSD

- gp2
    
- gp3
    
- io1
    
- io2 Block Express
    

### HDD

- st1
    
- sc1
    

Think:

SSD

=

IOPS + LOW LATENCY

HDD

=

THROUGHPUT + LOWER COST

---

## How EBS Volumes Are Measured

EBS volume types are characterized by:

SIZE

↓

THROUGHPUT

↓

IOPS

IOPS stands for:

INPUT / OUTPUT OPERATIONS PER SECOND

Think:

IOPS

=

HOW MANY STORAGE OPERATIONS

THROUGHPUT

=

HOW MUCH DATA MOVES PER SECOND

---

## Boot Volume Rule

Only these EBS families can be used as:

BOOT VOLUMES

- gp2
    
- gp3
    
- io1
    
- io2
    

HDD volumes:

st1

and

sc1

cannot be boot volumes.

Think:

BOOT DISK

↓

SSD EBS

NOT

HDD EBS

### Memory Trick

BOOT = SSD

---

## gp3 — General Purpose SSD

gp3 is:

GENERAL PURPOSE SSD

It balances:

PRICE

PERFORMANCE

for a wide variety of workloads.

Common use cases include:

- Boot volumes
    
- Virtual desktops
    
- Development environments
    
- Test environments
    

Think:

NORMAL EC2 WORKLOAD

↓

gp3

### Memory Trick

gp3 = GENERAL PURPOSE

---

## gp3 Performance

gp3 provides a baseline of:

3,000 IOPS

and:

125 MiB/s THROUGHPUT

The important SAA feature is:

IOPS

and

THROUGHPUT

can be increased independently from:

VOLUME SIZE

Think:

STORAGE SIZE

≠

IOPS

≠

THROUGHPUT

You can tune them separately.

Your course specifies gp3 can scale up to:

16,000 IOPS

and

1,000 MiB/s THROUGHPUT

### Memory Trick

gp3

=

SIZE AND PERFORMANCE SEPARATE

---

## gp2 — General Purpose SSD

gp2 is also:

GENERAL PURPOSE SSD

But gp2 behaves differently from gp3.

With gp2:

VOLUME SIZE

and

IOPS

are linked.

Think:

MORE GB

↓

MORE IOPS

Your course specifies:

3 IOPS PER GiB

up to:

16,000 IOPS

Small gp2 volumes can also burst to:

3,000 IOPS

### Memory Trick

gp2

=

SIZE CONTROLS IOPS

---

## gp2 vs gp3

This is one of the most important EBS distinctions for SAA.

### gp2

SIZE ↑

↓

IOPS ↑

### gp3

SIZE

and

IOPS

are:

INDEPENDENT

Think:

gp2

=

LINKED

gp3

=

SEPARATE

### Master gp Memory Trick

gp2 = OLD LINKED MODEL

gp3 = FLEXIBLE MODEL

---

## io1 / io2 — Provisioned IOPS SSD

io1 and io2 are:

PROVISIONED IOPS SSD

They are designed for:

CRITICAL BUSINESS APPLICATIONS

and:

SUSTAINED HIGH IOPS

Think:

MISSION-CRITICAL

↓

DATABASE

↓

io1 / io2

---

## Provisioned IOPS Use Cases

Use Provisioned IOPS volumes when you need:

CONSISTENT STORAGE PERFORMANCE

or:

MORE THAN 16,000 IOPS

They are especially suited for:

DATABASE WORKLOADS

because databases can be sensitive to:

STORAGE PERFORMANCE

and

CONSISTENCY

### Memory Trick

io = I/O INTENSIVE

---

## io1

io1 supports:

PROVISIONED IOPS

that can be increased independently from:

STORAGE SIZE

Your course specifies:

64,000 IOPS

on Nitro-based EC2 instances

and:

32,000 IOPS

on other EC2 instances.

Think:

HIGH-PERFORMANCE DATABASE

↓

io1

---

## io2 Block Express

io2 Block Express is the highest-performance EBS SSD option covered here.

It provides:

SUB-MILLISECOND LATENCY

and up to:

256,000 IOPS

Your course also highlights an:

IOPS : GiB RATIO

of:

1000 : 1

Think:

EXTREME EBS PERFORMANCE

↓

io2 BLOCK EXPRESS

### Memory Trick

io2 BLOCK EXPRESS

=

MAXIMUM EBS SSD PERFORMANCE

---

## EBS Multi-Attach

io1 / io2 support:

MULTI-ATTACH

This allows:

ONE EBS VOLUME

↓

MULTIPLE EC2 INSTANCES

within:

THE SAME AVAILABILITY ZONE

Think:

EC2 #1

↘

io1 / io2 EBS

↗

EC2 #2

---

## Multi-Attach Details

Your course highlights:

- Same EBS volume attached to multiple EC2 instances
    
- Instances must be in the same AZ
    
- Full read/write permissions
    
- Up to 16 EC2 instances
    
- Application must manage concurrent writes
    
- Requires a cluster-aware file system
    

Think:

MULTI-ATTACH

≠

NORMAL SHARED FILESYSTEM

The application and filesystem must understand simultaneous access.

### Exam Trap

Multi-Attach does NOT turn EBS into:

[EFS](https://chatgpt.com/c/EFS)

EFS is designed as a shared network filesystem.

Multi-Attach is a specialized EBS capability.

---

## st1 — Throughput Optimized HDD

st1 stands for:

THROUGHPUT OPTIMIZED HDD

It is designed for:

FREQUENTLY ACCESSED

and

THROUGHPUT-INTENSIVE

workloads.

Common use cases include:

- Big Data
    
- Data Warehouses
    
- Log Processing
    

Think:

LARGE SEQUENTIAL DATA

↓

st1

### Memory Trick

st1 = STREAMING THROUGHPUT

---

## st1 Performance

Your course specifies:

MAX THROUGHPUT

=

500 MiB/s

MAX IOPS

=

500

The important concept is:

THROUGHPUT

not high random IOPS.

Think:

MOVE LARGE AMOUNTS OF DATA

↓

st1

---

## sc1 — Cold HDD

sc1 is:

COLD HDD

It is designed for:

INFREQUENTLY ACCESSED DATA

and situations where:

LOWEST COST

is important.

Think:

RARELY ACCESSED DATA

↓

sc1

### Memory Trick

sc1 = SUPER CHEAP COLD STORAGE

---

## sc1 Performance

Your course specifies:

MAX THROUGHPUT

=

250 MiB/s

MAX IOPS

=

250

sc1 prioritizes:

LOW COST

over:

PERFORMANCE

Think:

CHEAP

INFREQUENT ACCESS

↓

sc1

---

## HDD Limitation

Both:

st1

and

sc1

cannot be used as:

BOOT VOLUMES

Think:

HDD

↓

DATA VOLUME ONLY

NOT

BOOT VOLUME

---

## SSD vs HDD Architecture Thinking

Need:

LOW LATENCY

or

HIGH IOPS

↓

SSD

gp3 / gp2 / io1 / io2

Need:

HIGH SEQUENTIAL THROUGHPUT

↓

st1

Need:

LOWEST COST FOR COLD DATA

↓

sc1

---

## Scenario Recognition

Need a normal general-purpose EC2 boot volume?

→ gp3

---

Need general-purpose SSD where IOPS can be tuned separately from size?

→ gp3

---

Need general-purpose SSD where IOPS increases with disk size?

→ gp2

---

Need more than 16,000 IOPS?

→ io1 / io2

---

Need sustained high IOPS for a critical database?

→ io1 / io2

---

Need sub-millisecond latency and extremely high EBS performance?

→ io2 Block Express

---

Need one EBS volume attached to multiple EC2 instances?

→ io1 / io2 Multi-Attach

---

Need frequently accessed, throughput-heavy storage for Big Data?

→ st1

---

Need storage for data warehouse workloads?

→ st1

---

Need cheap storage for infrequently accessed data?

→ sc1

---

Need an HDD boot volume?

→ Not supported

---

## Exam Traps

gp2

=

IOPS LINKED TO SIZE

gp3

=

IOPS INDEPENDENT FROM SIZE

gp3

=

GENERAL PURPOSE SSD

io1 / io2

=

PROVISIONED IOPS SSD

io2 BLOCK EXPRESS

=

SUB-MILLISECOND LATENCY

io1 / io2

=

MULTI-ATTACH SUPPORT

st1

=

THROUGHPUT OPTIMIZED HDD

sc1

=

COLD HDD

st1 / sc1

=

CANNOT BE BOOT VOLUMES

HIGH RANDOM IOPS

≠

st1

LOWEST COST

=

sc1

BIG DATA / DATA WAREHOUSE / LOGS

=

st1

DATABASE + CONSISTENT HIGH IOPS

=

io1 / io2

---

## Quick Cheat Sheet

gp3

=

GENERAL PURPOSE SSD

gp3

=

3,000 BASELINE IOPS

gp3

=

125 MiB/s BASELINE THROUGHPUT

gp3

=

IOPS + THROUGHPUT INDEPENDENT OF SIZE

gp2

=

GENERAL PURPOSE SSD

gp2

=

3 IOPS PER GiB

gp2

=

SIZE + IOPS LINKED

io1 / io2

=

PROVISIONED IOPS SSD

io1 / io2

=

CRITICAL DATABASE WORKLOADS

io2 BLOCK EXPRESS

=

UP TO 256,000 IOPS

io2 BLOCK EXPRESS

=

SUB-MILLISECOND LATENCY

io1 / io2

=

MULTI-ATTACH

st1

=

THROUGHPUT OPTIMIZED HDD

st1

=

BIG DATA / LOGS / DATA WAREHOUSE

sc1

=

COLD HDD

sc1

=

LOWEST COST

BOOT VOLUME

=

gp2 / gp3 / io1 / io2

HDD BOOT VOLUME

=

NOT SUPPORTED

---

## Master Memory Trick

gp3

=

GENERAL + FLEXIBLE

gp2

=

GENERAL + SIZE-LINKED

io1 / io2

=

DATABASE + HIGH IOPS

st1

=

STREAM LARGE DATA

sc1

=

STORE COLD CHEAP

Think:

GENERAL

↓

gp3

DATABASE

↓

io2

BIG DATA

↓

st1

COLD DATA

↓

sc1

---

## Related Notes

- [EBS Volumes](https://chatgpt.com/c/EBS%20Volumes)
    
- [EBS Snapshots](https://chatgpt.com/c/EBS%20Snapshots)
    
- [EC2](https://chatgpt.com/c/EC2)
    
- [EC2 Instance Store](https://chatgpt.com/c/EC2%20Instance%20Store)
    
- [EFS](https://chatgpt.com/c/EFS)
    
- [SAA EC2 Storage Cheat Sheet](https://chatgpt.com/c/SAA%20EC2%20Storage%20Cheat%20Sheet)
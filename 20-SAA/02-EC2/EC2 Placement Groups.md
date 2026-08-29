## What Problem Does It Solve?

Placement Groups give you control over:

HOW EC2 INSTANCES ARE PLACED

on AWS infrastructure.

Different workloads may need:

LOW LATENCY

HIGH AVAILABILITY

or

FAILURE ISOLATION AT SCALE

### Memory Trick

Placement Group = WHERE EC2 INSTANCES LIVE

---

# Three Placement Strategies

There are three strategies:

CLUSTER

SPREAD

PARTITION

### Master Memory Trick

CLUSTER

= CLOSE TOGETHER

SPREAD

= FAR APART

PARTITION

= SEPARATE GROUPS

---

# Cluster Placement Group

Cluster places EC2 instances:

CLOSE TOGETHER

inside:

ONE AVAILABILITY ZONE

The goal is:

LOW LATENCY

+

HIGH NETWORK THROUGHPUT

### Memory Trick

Cluster = PERFORMANCE

---

## Cluster Networking

Your course highlights:

10 Gbps BANDWIDTH

between instances when:

ENHANCED NETWORKING

is enabled.

Think:

EC2 ↔ EC2 ↔ EC2

↓

VERY FAST NETWORK

---

## Cluster Advantage

Great for:

HIGH-PERFORMANCE NETWORKING

because instances are placed close together.

---

## Cluster Disadvantage

Cluster instances are located in:

THE SAME AZ

Therefore:

AZ FAILURE

↓

ALL INSTANCES MAY FAIL TOGETHER

### Memory Trick

Cluster = FAST BUT TOGETHER

---

## Cluster Use Cases

Your course lists:

BIG DATA JOB

that needs to complete quickly

and:

APPLICATIONS REQUIRING

EXTREMELY LOW LATENCY

+

HIGH NETWORK THROUGHPUT

---

# Spread Placement Group

Spread places EC2 instances across:

DIFFERENT PHYSICAL HARDWARE

The goal is:

REDUCE SIMULTANEOUS FAILURE

### Memory Trick

Spread = HIGH AVAILABILITY

---

## Spread Across AZs

Spread Placement Groups can span:

MULTIPLE AVAILABILITY ZONES

Think:

AZ-A

↓

EC2 on Hardware 1

EC2 on Hardware 2

AZ-B

↓

EC2 on Hardware 3

EC2 on Hardware 4

AZ-C

↓

EC2 on Hardware 5

EC2 on Hardware 6

---

## Spread Advantage

Instances run on:

DIFFERENT PHYSICAL HARDWARE

This reduces the risk of:

SIMULTANEOUS FAILURE

### Memory Trick

Spread = ISOLATE EACH INSTANCE

---

## Spread Limitation

Your course states:

MAXIMUM 7 INSTANCES

per:

AZ

per:

PLACEMENT GROUP

### Exam Number

SPREAD

= 7 INSTANCES PER AZ PER GROUP

---

## Spread Use Cases

Best for applications that need:

MAXIMUM HIGH AVAILABILITY

and:

CRITICAL APPLICATIONS

where each instance should be isolated from failures affecting other instances.

---

# Partition Placement Group

Partition divides EC2 instances into:

SEPARATE PARTITIONS

Each partition relies on:

DIFFERENT SETS OF RACKS

Think:

PARTITION 1

↓

EC2
EC2
EC2

PARTITION 2

↓

EC2
EC2
EC2

PARTITION 3

↓

EC2
EC2
EC2

### Memory Trick

Partition = GROUPS ON DIFFERENT RACKS

---

## Partition Failure Isolation

Instances inside one partition:

DO NOT SHARE RACKS

with instances in:

OTHER PARTITIONS

Therefore:

PARTITION 1 FAILS

↓

INSTANCES IN PARTITION 1 MAY FAIL

BUT

↓

OTHER PARTITIONS ARE NOT AFFECTED

### Memory Trick

Partition = CONTAIN THE FAILURE

---

## Partition Scale

Unlike Spread, Partition Placement Groups can support:

HUNDREDS OF EC2 INSTANCES

### Memory Trick

Spread

= SMALL NUMBER OF CRITICAL INSTANCES

Partition

= LARGE DISTRIBUTED SYSTEM

---

## Partition Across AZs

Partition Placement Groups can span:

MULTIPLE AZs

within the:

SAME REGION

---

## Number of Partitions

Your course states:

UP TO 7 PARTITIONS

per:

AZ

Do not confuse this with Spread.

### Important

SPREAD

= 7 INSTANCES PER AZ PER GROUP

PARTITION

= 7 PARTITIONS PER AZ

---

## Partition Metadata

EC2 instances can access:

PARTITION INFORMATION

as:

METADATA

---

## Partition Use Cases

Your course lists:

- HDFS
- HBase
- Cassandra
- Kafka

Think:

LARGE DISTRIBUTED DATA SYSTEM

↓

PARTITION

---

# The Big Comparison

| Strategy | Main Goal | Placement | Scale | Think |
| --- | --- | --- | --- | --- |
| Cluster | Performance | Close together, one AZ | Multiple instances | FAST |
| Spread | High availability | Different hardware, can span AZs | 7 instances/AZ/group | ISOLATE |
| Partition | Failure isolation at scale | Different rack partitions, can span AZs | Hundreds of instances | GROUPS |

---

# Cluster vs Spread

## Cluster

Instances:

CLOSE TOGETHER

Goal:

PERFORMANCE

Risk:

AZ FAILURE AFFECTS ALL

### Think

FAST

---

## Spread

Instances:

SEPARATED

Goal:

HIGH AVAILABILITY

Risk:

REDUCED SIMULTANEOUS FAILURE

### Think

SAFE

---

# Spread vs Partition

This distinction is especially important.

## Spread

Each EC2 instance is placed on:

DIFFERENT PHYSICAL HARDWARE

Best for:

SMALL NUMBER OF CRITICAL INSTANCES

Limit:

7 INSTANCES PER AZ PER GROUP

---

## Partition

Instances are organized into:

GROUPS / PARTITIONS

Each partition uses:

DIFFERENT RACKS

Best for:

LARGE DISTRIBUTED APPLICATIONS

Can support:

HUNDREDS OF INSTANCES

### Memory Trick

Spread = EACH INSTANCE

Partition = GROUPS OF INSTANCES

---

# Scenario Recognition

Need extremely low latency between EC2 instances?

→ CLUSTER

---

Need high network throughput between EC2 instances?

→ CLUSTER

---

Big Data job needs to finish as quickly as possible?

→ CLUSTER

---

Need maximum high availability for a small number of critical EC2 instances?

→ SPREAD

---

Need each critical EC2 instance isolated on different physical hardware?

→ SPREAD

---

Need hundreds of EC2 instances for Cassandra?

→ PARTITION

---

Need Kafka with rack-level failure isolation?

→ PARTITION

---

Need HDFS or HBase across many EC2 instances?

→ PARTITION

---

# Exam Traps

CLUSTER

= ONE AZ

CLUSTER

= LOW LATENCY + HIGH THROUGHPUT

CLUSTER

= HIGHER CORRELATED FAILURE RISK

---

SPREAD

= DIFFERENT HARDWARE

SPREAD

= CAN SPAN AZs

SPREAD

= 7 INSTANCES PER AZ PER GROUP

---

PARTITION

= DIFFERENT SETS OF RACKS

PARTITION

= CAN SPAN AZs IN SAME REGION

PARTITION

= HUNDREDS OF EC2 INSTANCES

PARTITION

= 7 PARTITIONS PER AZ

---

# Quick Cheat Sheet

CLUSTER

= PERFORMANCE

= CLOSE

= ONE AZ

---

SPREAD

= HIGH AVAILABILITY

= DIFFERENT HARDWARE

= 7 INSTANCES / AZ / GROUP

---

PARTITION

= DISTRIBUTED SYSTEMS

= DIFFERENT RACK GROUPS

= HUNDREDS OF INSTANCES

= 7 PARTITIONS / AZ

---

# Master Memory Trick

Need:

SPEED?

→ CLUSTER

Need:

EACH INSTANCE ISOLATED?

→ SPREAD

Need:

HUNDREDS OF DISTRIBUTED INSTANCES?

→ PARTITION

Or simply:

CLUSTER = TOGETHER

SPREAD = APART

PARTITION = GROUPED APART

---

## Related Notes

- [[EC2]]
- [[EC2 Instance Types]]
- [[Elastic Network Interfaces]]
- [[Private vs Public IP]]
- [[EC2 Comparison]]
- [[SAA EC2 Cheat Sheet]]
## What Problem Does It Solve?

This note helps answer:

WHICH EC2 OPTION SHOULD I CHOOSE?

Think:

EC2 QUESTION

↓

IDENTIFY REQUIREMENT

↓

COMPUTE?

INSTANCE TYPE?

PRICING?

SECURITY?

NETWORKING?

PLACEMENT?

PERSISTENCE?

↓

CHOOSE THE RIGHT EC2 FEATURE

### Memory Trick

EC2

=

RENT COMPUTE

---

## Master EC2 Map

Need:

VIRTUAL SERVER

↓

[EC2](https://chatgpt.com/c/EC2)

Need:

AUTOMATIC COMMANDS AT LAUNCH

↓

[EC2 User Data](https://chatgpt.com/c/EC2%20User%20Data)

Need:

RIGHT CPU / RAM / NETWORK PROFILE

↓

[EC2 Instance Types](https://chatgpt.com/c/EC2%20Instance%20Types)

Need:

RIGHT PRICING MODEL

↓

[EC2 Purchasing Options](https://chatgpt.com/c/EC2%20Purchasing%20Options)

Need:

EC2 FIREWALL

↓

[EC2 Security Groups](https://chatgpt.com/c/EC2%20Security%20Groups)

Need:

EC2 ACCESS TO AWS SERVICES

↓

[EC2 IAM Roles](https://chatgpt.com/c/EC2%20IAM%20Roles)

Need:

FIXED PUBLIC IPv4

↓

[Elastic IP](https://chatgpt.com/c/Elastic%20IP)

Need:

CONTROL PHYSICAL INSTANCE PLACEMENT

↓

[EC2 Placement Groups](https://chatgpt.com/c/EC2%20Placement%20Groups)

Need:

MOVABLE VIRTUAL NETWORK CARD

↓

[Elastic Network Interfaces](https://chatgpt.com/c/Elastic%20Network%20Interfaces)

Need:

PRESERVE RAM + FAST RESTART

↓

[EC2 Hibernate](https://chatgpt.com/c/EC2%20Hibernate)

---

## EC2

EC2 stands for:

ELASTIC COMPUTE CLOUD

EC2 provides:

VIRTUAL MACHINES

in AWS.

Think:

PHYSICAL SERVER

↓

VIRTUAL SERVER

↓

EC2

EC2 is:

INFRASTRUCTURE AS A SERVICE

or:

IaaS

### Memory Trick

EC2 = COMPUTE

---

## EC2 Configuration

When launching EC2, think:

OS

↓

CPU

↓

RAM

↓

STORAGE

↓

NETWORK

↓

SECURITY

You choose the resources required by the workload.

---

## EC2 User Data

EC2 User Data provides:

BOOTSTRAPPING

Think:

EC2 STARTS

↓

USER DATA SCRIPT

↓

AUTOMATIC CONFIGURATION

User Data can:

- Install software
    
- Install updates
    
- Download files
    
- Configure the instance
    

### Important

User Data runs:

AS ROOT

and normally runs:

ON FIRST BOOT

### Memory Trick

USER DATA = BOOT SCRIPT

---

## EC2 Instance Types

Instance families are optimized for different workloads.

Think:

WORKLOAD

↓

CHOOSE INSTANCE FAMILY

---

## General Purpose

General Purpose provides a balance of:

COMPUTE

MEMORY

NETWORKING

Examples:

T

M

Think:

NORMAL APPLICATION

↓

GENERAL PURPOSE

### Memory Trick

GENERAL PURPOSE = BALANCED

---

## Compute Optimized

Compute Optimized instances are designed for:

HIGH CPU PERFORMANCE

Common use cases:

- Batch processing
    
- Media transcoding
    
- High-performance web servers
    
- Scientific modeling
    
- Machine learning
    
- Gaming servers
    

Think:

CPU HEAVY

↓

COMPUTE OPTIMIZED

### Memory Trick

C = COMPUTE

---

## Memory Optimized

Memory Optimized instances are designed for:

LARGE AMOUNTS OF RAM

Common use cases:

- In-memory databases
    
- Distributed caches
    
- Real-time processing
    

Think:

RAM HEAVY

↓

MEMORY OPTIMIZED

### Memory Trick

R = RAM

---

## Storage Optimized

Storage Optimized instances are designed for workloads requiring:

HIGH LOCAL STORAGE PERFORMANCE

Common use cases:

- Data warehouses
    
- Distributed file systems
    
- High-frequency transaction systems
    

Think:

LOCAL STORAGE HEAVY

↓

STORAGE OPTIMIZED

### Memory Trick

I / D / H

=

STORAGE-FOCUSED FAMILIES

---

## Instance Type Memory Trick

GENERAL

=

BALANCED

COMPUTE

=

CPU

MEMORY

=

RAM

STORAGE

=

LOCAL DISK PERFORMANCE

Think:

CPU?

↓

C

RAM?

↓

R

BALANCED?

↓

M / T

STORAGE?

↓

I / D / H

---

## EC2 Purchasing Options

The major purchasing choices are:

ON-DEMAND

↓

RESERVED

↓

SAVINGS PLANS

↓

SPOT

↓

DEDICATED HOST

↓

DEDICATED INSTANCE

↓

CAPACITY RESERVATION

---

## On-Demand Instances

On-Demand means:

PAY AS YOU GO

No long-term commitment.

Best for:

SHORT-TERM

UNPREDICTABLE

NON-INTERRUPTIBLE

workloads.

### Memory Trick

ON-DEMAND = FLEXIBILITY

---

## Reserved Instances

Reserved Instances provide:

DISCOUNTS

in exchange for:

LONG-TERM COMMITMENT

Usually:

1 YEAR

or

3 YEARS

Best for:

STEADY

PREDICTABLE

workloads.

Think:

DATABASE RUNNING 24/7

↓

RESERVED INSTANCE

### Memory Trick

RESERVED = COMMIT + SAVE

---

## Convertible Reserved Instances

Convertible RIs provide:

MORE FLEXIBILITY

than Standard Reserved Instances.

They allow changes to certain instance attributes.

But:

MORE FLEXIBILITY

=

LOWER DISCOUNT

Think:

STANDARD RI

=

MORE SAVINGS

CONVERTIBLE RI

=

MORE FLEXIBILITY

---

## Savings Plans

Savings Plans require a commitment to:

CONSISTENT COMPUTE USAGE

measured in:

$/HOUR

Think:

COMMIT TO SPEND

↓

RECEIVE DISCOUNT

### Memory Trick

SAVINGS PLAN

=

COMMIT TO COMPUTE SPEND

---

## Spot Instances

Spot provides:

VERY LARGE DISCOUNTS

but AWS can:

INTERRUPT THE INSTANCE

Think:

CHEAPEST COMPUTE

↓

INTERRUPTION POSSIBLE

Best for:

- Batch jobs
    
- Data analysis
    
- Distributed workloads
    
- Flexible workloads
    
- Fault-tolerant workloads
    

Bad for:

CRITICAL DATABASE

or:

NON-INTERRUPTIBLE APPLICATION

### Memory Trick

SPOT

=

CHEAP + INTERRUPTIBLE

---

## Dedicated Hosts

Dedicated Host gives you:

AN ENTIRE PHYSICAL SERVER

Think:

AWS HARDWARE

↓

DEDICATED TO YOU

Useful for:

COMPLIANCE

and:

SOFTWARE LICENSES

that are tied to physical server characteristics such as:

SOCKETS

CORES

VMs

### Memory Trick

DEDICATED HOST = WHOLE PHYSICAL SERVER

---

## Dedicated Instances

Dedicated Instances run on:

HARDWARE DEDICATED TO YOUR ACCOUNT

But you do not control the physical host in the same way as:

DEDICATED HOST

Think:

DEDICATED INSTANCE

=

DEDICATED HARDWARE

DEDICATED HOST

=

DEDICATED PHYSICAL SERVER CONTROL

---

## Capacity Reservations

Capacity Reservations reserve:

EC2 CAPACITY

in:

A SPECIFIC AVAILABILITY ZONE

Think:

NEED GUARANTEED CAPACITY

↓

CAPACITY RESERVATION

Important:

CAPACITY RESERVATION

≠

PRICING DISCOUNT

### Memory Trick

CAPACITY RESERVATION = RESERVE CAPACITY, NOT PRICE

---

## Purchasing Decision

SHORT + UNPREDICTABLE

↓

ON-DEMAND

LONG + STEADY

↓

RESERVED

FLEXIBLE COMPUTE COMMITMENT

↓

SAVINGS PLAN

FAULT-TOLERANT + CHEAP

↓

SPOT

PHYSICAL SERVER LICENSING

↓

DEDICATED HOST

GUARANTEED AZ CAPACITY

↓

CAPACITY RESERVATION

---

## EC2 Security Groups

Security Groups act as:

EC2 FIREWALLS

They control:

INBOUND

and

OUTBOUND

traffic.

Think:

INTERNET

↓

SECURITY GROUP

↓

EC2

### Memory Trick

SECURITY GROUP = FIREWALL

---

## Security Groups Are Stateful

Security Groups are:

STATEFUL

If traffic is allowed into the instance:

RETURN TRAFFIC

is automatically allowed.

Think:

REQUEST ALLOWED

↓

RESPONSE AUTOMATICALLY ALLOWED

### Memory Trick

SECURITY GROUP = STATEFUL

---

## Security Group Rules

Security Groups contain:

ALLOW RULES

There are no:

DENY RULES

Think:

ALLOW

=

YES

NO RULE

=

BLOCKED

### Important

Security Groups can reference:

OTHER SECURITY GROUPS

This is extremely useful for application architectures.

Think:

LOAD BALANCER SG

↓

ALLOWED BY

↓

EC2 SG

---

## Security Group Troubleshooting

TIMEOUT

↓

THINK SECURITY GROUP

CONNECTION REFUSED

↓

THINK APPLICATION / SERVICE

### Memory Trick

TIMEOUT = NETWORK RULE

REFUSED = APPLICATION RESPONDED

---

## EC2 IAM Roles

EC2 instances should access AWS services using:

IAM ROLES

Think:

EC2

↓

IAM ROLE

↓

AWS SERVICE

Examples:

EC2

↓

ROLE

↓

S3

or:

EC2

↓

ROLE

↓

DYNAMODB

### Memory Trick

EC2 + AWS PERMISSIONS = IAM ROLE

---

## Never Store AWS Credentials on EC2

Do not place:

ACCESS KEY

SECRET ACCESS KEY

directly on an EC2 instance.

Instead:

EC2

↓

IAM ROLE

↓

TEMPORARY CREDENTIALS

### Memory Trick

EC2 CREDENTIALS

=

ROLE

NOT

ACCESS KEYS

---

## Private vs Public IP

### Private IP

Used for:

PRIVATE AWS NETWORK COMMUNICATION

Think:

EC2

↓

PRIVATE IP

↓

INTERNAL NETWORK

Private IP remains associated with the instance across:

STOP

and

START

---

## Public IP

Public IP allows communication over:

THE INTERNET

Think:

INTERNET

↓

PUBLIC IP

↓

EC2

A normal public IPv4 address can change when an EC2 instance is:

STOPPED

and

STARTED

### Memory Trick

PRIVATE IP = INTERNAL

PUBLIC IP = INTERNET

---

## Elastic IP

Elastic IP provides:

STATIC PUBLIC IPv4

Think:

EC2 PUBLIC IP CHANGES

↓

NEED FIXED ADDRESS

↓

ELASTIC IP

### Memory Trick

ELASTIC IP = STATIC PUBLIC IP

---

## Elastic IP Architecture Thinking

Elastic IP can be moved from:

ONE EC2 INSTANCE

to:

ANOTHER EC2 INSTANCE

Think:

EC2-A FAILS

↓

MOVE ELASTIC IP

↓

EC2-B

However, your course recommends avoiding Elastic IP when possible.

Instead, prefer architectures using:

DNS

or:

LOAD BALANCERS

### Exam Thinking

FIXED PUBLIC IPv4 REQUIRED

↓

ELASTIC IP

HIGHLY AVAILABLE APPLICATION ENDPOINT

↓

LOAD BALANCER / DNS

---

## EC2 Placement Groups

Placement Groups control:

HOW EC2 INSTANCES ARE PLACED

on AWS infrastructure.

There are three strategies:

CLUSTER

PARTITION

SPREAD

### Memory Trick

PLACEMENT GROUPS

=

CLUSTER

PARTITION

SPREAD

---

## Cluster Placement Group

Cluster means:

PACK INSTANCES CLOSE TOGETHER

Think:

EC2 EC2 EC2

↓

SAME AZ

↓

CLOSE HARDWARE

Benefit:

HIGH NETWORK PERFORMANCE

LOW LATENCY

Risk:

HIGHER CORRELATED FAILURE RISK

### Memory Trick

CLUSTER = CLOSE + FAST

---

## Spread Placement Group

Spread means:

SEPARATE INSTANCES ACROSS HARDWARE

Think:

EC2

↓

DIFFERENT HARDWARE

EC2

↓

DIFFERENT HARDWARE

Best for:

CRITICAL INSTANCES

where failure isolation is important.

Limited to:

7 INSTANCES PER AZ

per placement group.

### Memory Trick

SPREAD = SEPARATE

---

## Partition Placement Group

Partition means:

GROUP INSTANCES INTO PARTITIONS

Each partition uses:

SEPARATE HARDWARE

Think:

PARTITION 1

↓

EC2 EC2

PARTITION 2

↓

EC2 EC2

PARTITION 3

↓

EC2 EC2

Useful for distributed systems such as:

HADOOP

CASSANDRA

KAFKA

### Memory Trick

PARTITION = GROUP FAILURE DOMAINS

---

## Placement Group Decision

MAXIMUM NETWORK PERFORMANCE

↓

CLUSTER

CRITICAL INSTANCES MUST BE SEPARATED

↓

SPREAD

LARGE DISTRIBUTED APPLICATION

↓

PARTITION

---

## Elastic Network Interfaces

ENI stands for:

ELASTIC NETWORK INTERFACE

An ENI is:

A VIRTUAL NETWORK CARD

Think:

EC2

↓

VIRTUAL NIC

↓

ENI

### Memory Trick

ENI = NETWORK CARD

---

## ENI Characteristics

An ENI can contain:

PRIVATE IPv4 ADDRESSES

↓

ELASTIC IP

↓

PUBLIC IPv4

↓

MAC ADDRESS

↓

SECURITY GROUPS

An EC2 instance can have:

MULTIPLE ENIs

---

## ENI Failover

An ENI can be moved between EC2 instances in:

THE SAME AVAILABILITY ZONE

Think:

EC2-A FAILS

↓

DETACH ENI

↓

ATTACH ENI

↓

EC2-B

This can be useful for:

NETWORK FAILOVER

### Memory Trick

ENI = MOVABLE NETWORK CARD

---

## EC2 Hibernate

Normally when you stop an EC2 instance:

RAM

↓

CLEARED

When you hibernate:

RAM CONTENTS

↓

SAVED TO ROOT EBS

Think:

RUNNING

↓

HIBERNATE

↓

RAM → EBS

↓

START

↓

RAM RESTORED

### Memory Trick

HIBERNATE = SAVE RAM

---

## Why Hibernate?

Hibernate allows:

FASTER APPLICATION STARTUP

because the operating system and applications do not need to fully restart.

Useful when:

APPLICATION INITIALIZATION

takes a long time.

Think:

LONG BOOT PROCESS

↓

HIBERNATE

↓

RESUME FASTER

---

## Hibernate Requirement

Because RAM is written to:

ROOT EBS

the root EBS volume must be:

ENCRYPTED

and large enough to store:

RAM CONTENTS

Think:

RAM

↓

ENCRYPTED ROOT EBS

### Memory Trick

HIBERNATE

=

RAM → ENCRYPTED EBS

---

## Stop vs Hibernate vs Terminate

### Stop

CPU

=

OFF

RAM

=

LOST

EBS

=

PRESERVED

---

### Hibernate

CPU

=

OFF

RAM

=

SAVED TO EBS

EBS

=

PRESERVED

---

### Terminate

INSTANCE

=

DELETED

ROOT EBS

=

DELETED BY DEFAULT

Think:

STOP

=

KEEP DISK

HIBERNATE

=

KEEP DISK + RAM STATE

TERMINATE

=

DELETE INSTANCE

---

## EC2 Architecture Thinking

A common highly available architecture is:

USERS

↓

LOAD BALANCER

↓

EC2 INSTANCES

↓

EBS STORAGE

And:

AUTO SCALING GROUP

↓

ADD / REMOVE EC2

Security around EC2:

SECURITY GROUP

↓

EC2

AWS permissions:

EC2

↓

IAM ROLE

↓

AWS SERVICES

Think:

ELB

=

DISTRIBUTE

EC2

=

COMPUTE

EBS

=

STORAGE

ASG

=

SCALE

SG

=

FIREWALL

IAM ROLE

=

AWS PERMISSIONS

---

## Highest-Value Scenario Recognition

Need a virtual machine?

→ EC2

---

Need commands to run automatically when EC2 launches?

→ User Data

---

Need CPU-intensive compute?

→ Compute Optimized

---

Need large RAM?

→ Memory Optimized

---

Need balanced CPU and RAM?

→ General Purpose

---

Need short-term unpredictable compute?

→ On-Demand

---

Need steady long-term compute?

→ Reserved Instances / Savings Plans

---

Need cheapest fault-tolerant compute?

→ Spot

---

Need physical server visibility for licensing?

→ Dedicated Host

---

Need guaranteed EC2 capacity in one AZ?

→ Capacity Reservation

---

Need firewall rules around EC2?

→ Security Group

---

Need EC2 to access S3 without storing credentials?

→ IAM Role

---

Need fixed public IPv4?

→ Elastic IP

---

Need maximum EC2-to-EC2 network performance?

→ Cluster Placement Group

---

Need critical instances isolated from hardware failure?

→ Spread Placement Group

---

Need large distributed application separated into failure domains?

→ Partition Placement Group

---

Need movable virtual network interface?

→ ENI

---

Need RAM preserved across stop/start?

→ Hibernate

---

## Highest-Value Exam Traps

EC2

=

COMPUTE

NOT STORAGE

---

USER DATA

=

FIRST BOOT BOOTSTRAPPING

---

GENERAL PURPOSE

=

BALANCED

COMPUTE OPTIMIZED

=

CPU

MEMORY OPTIMIZED

=

RAM

---

SPOT

=

CAN BE INTERRUPTED

Do not choose Spot for a workload that:

CANNOT TOLERATE INTERRUPTION

---

RESERVED INSTANCE

≠

CAPACITY RESERVATION

RI

=

PRICING DISCOUNT

CAPACITY RESERVATION

=

GUARANTEED CAPACITY

---

SECURITY GROUP

=

STATEFUL

SECURITY GROUP

=

ALLOW RULES ONLY

---

EC2 AWS ACCESS

=

IAM ROLE

NOT

HARDCODED ACCESS KEYS

---

PUBLIC IP

=

CAN CHANGE AFTER STOP / START

ELASTIC IP

=

STATIC PUBLIC IPv4

---

CLUSTER

=

PERFORMANCE

SPREAD

=

FAILURE ISOLATION

PARTITION

=

DISTRIBUTED SYSTEM

---

ENI

=

VIRTUAL NETWORK CARD

ENI

=

AZ BOUND

---

HIBERNATE

≠

NORMAL STOP

HIBERNATE

=

RAM SAVED TO EBS

---

## 10-Second EC2 Decision Tree

Need:

SERVER?

↓

EC2

CPU HEAVY?

↓

COMPUTE OPTIMIZED

RAM HEAVY?

↓

MEMORY OPTIMIZED

NORMAL BALANCED WORKLOAD?

↓

GENERAL PURPOSE

CHEAP INTERRUPTIBLE COMPUTE?

↓

SPOT

STEADY LONG-TERM COMPUTE?

↓

RESERVED / SAVINGS PLAN

GUARANTEED AZ CAPACITY?

↓

CAPACITY RESERVATION

FIREWALL?

↓

SECURITY GROUP

AWS SERVICE PERMISSIONS?

↓

IAM ROLE

STATIC PUBLIC IP?

↓

ELASTIC IP

MAX NETWORK PERFORMANCE?

↓

CLUSTER PLACEMENT GROUP

FAILURE ISOLATION?

↓

SPREAD PLACEMENT GROUP

DISTRIBUTED SYSTEM?

↓

PARTITION PLACEMENT GROUP

MOVABLE NETWORK CARD?

↓

ENI

SAVE RAM?

↓

HIBERNATE

---

## Quick Cheat Sheet

EC2

=

VIRTUAL SERVER

EC2

=

IaaS

USER DATA

=

BOOTSTRAP

GENERAL PURPOSE

=

BALANCED

COMPUTE OPTIMIZED

=

CPU

MEMORY OPTIMIZED

=

RAM

ON-DEMAND

=

FLEXIBLE

RESERVED

=

COMMIT + SAVE

SAVINGS PLAN

=

COMMIT TO COMPUTE SPEND

SPOT

=

CHEAP + INTERRUPTIBLE

DEDICATED HOST

=

PHYSICAL SERVER

CAPACITY RESERVATION

=

GUARANTEED AZ CAPACITY

SECURITY GROUP

=

STATEFUL FIREWALL

IAM ROLE

=

EC2 AWS PERMISSIONS

PRIVATE IP

=

INTERNAL

PUBLIC IP

=

INTERNET + CAN CHANGE

ELASTIC IP

=

STATIC PUBLIC IPv4

CLUSTER

=

CLOSE + FAST

SPREAD

=

SEPARATE + SAFE

PARTITION

=

DISTRIBUTED FAILURE DOMAINS

ENI

=

VIRTUAL NETWORK CARD

HIBERNATE

=

SAVE RAM TO EBS

---

## Master Memory Trick

EC2

=

COMPUTE

USER DATA

=

CONFIGURE

INSTANCE TYPE

=

SIZE FOR WORKLOAD

PURCHASING OPTION

=

PAY THE RIGHT WAY

SECURITY GROUP

=

FIREWALL

IAM ROLE

=

PERMISSIONS

ELASTIC IP

=

STATIC PUBLIC IP

PLACEMENT GROUP

=

PHYSICAL PLACEMENT

ENI

=

NETWORK CARD

HIBERNATE

=

SAVE RAM

Think:

LAUNCH

↓

CONFIGURE

↓

SIZE

↓

PRICE

↓

SECURE

↓

CONNECT

↓

PLACE

↓

RUN

↓

HIBERNATE

---

## Related Notes

- [EC2](https://chatgpt.com/c/EC2)
    
- [EC2 User Data](https://chatgpt.com/c/EC2%20User%20Data)
    
- [EC2 Instance Types](https://chatgpt.com/c/EC2%20Instance%20Types)
    
- [EC2 Purchasing Options](https://chatgpt.com/c/EC2%20Purchasing%20Options)
    
- [EC2 Security Groups](https://chatgpt.com/c/EC2%20Security%20Groups)
    
- [EC2 IAM Roles](https://chatgpt.com/c/EC2%20IAM%20Roles)
    
- [Private vs Public IP](https://chatgpt.com/c/Private%20vs%20Public%20IP)
    
- [Elastic IP](https://chatgpt.com/c/Elastic%20IP)
    
- [EC2 Placement Groups](https://chatgpt.com/c/EC2%20Placement%20Groups)
    
- [Elastic Network Interfaces](https://chatgpt.com/c/Elastic%20Network%20Interfaces)
    
- [EC2 Hibernate](https://chatgpt.com/c/EC2%20Hibernate)
    
- [EBS Volumes](https://chatgpt.com/c/EBS%20Volumes)
    
- [SAA EC2 Storage Cheat Sheet](https://chatgpt.com/c/SAA%20EC2%20Storage%20Cheat%20Sheet)
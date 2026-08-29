## What Problem Does It Solve?

EC2 Purchasing Options let you choose:

HOW YOU PAY

and, in some cases:

HOW CAPACITY IS RESERVED

for EC2.

The best option depends on:

- Workload duration
- Predictability
- Interruptibility
- Capacity requirements
- Licensing
- Compliance

### Memory Trick

EC2 Purchasing = MATCH THE PAYMENT MODEL TO THE WORKLOAD

---

# On-Demand Instances

## What Is On-Demand?

On-Demand means:

PAY FOR WHAT YOU USE

There is:

NO LONG-TERM COMMITMENT

and:

NO UPFRONT PAYMENT

Your course describes On-Demand as having the:

HIGHEST COST

compared with discounted commitment options.

### Best For

SHORT-TERM

+

UNINTERRUPTED

+

UNPREDICTABLE WORKLOADS

### Memory Trick

On-Demand = PAY AS YOU GO

---

## On-Demand Billing

Your course states:

Linux / Windows

→ billed per second after the first minute

Other operating systems

→ billed per hour

### Exam Recognition

Need EC2 temporarily and don't know how long you'll need it?

→ ON-DEMAND

---

# Reserved Instances

## What Are Reserved Instances?

Reserved Instances provide a discount compared with On-Demand in exchange for:

LONG-TERM COMMITMENT

Your course lists:

1 YEAR

or

3 YEARS

Longer commitment:

↓

GREATER DISCOUNT

### Best For

STEADY-STATE USAGE

Example:

DATABASE

### Memory Trick

Reserved = STEADY + LONG TERM

---

## Reserved Instance Attributes

Your course says Reserved Instances reserve specific attributes such as:

- Instance Type
- Region
- Tenancy
- Operating System

---

## Reserved Instance Payment Options

### No Upfront

Lower discount

### Partial Upfront

Higher discount

### All Upfront

Highest discount

Think:

MORE UPFRONT

↓

MORE DISCOUNT

---

## Reserved Instance Scope

Reserved Instances can have:

REGIONAL

or

ZONAL

scope.

Your course notes that a:

ZONAL RESERVED INSTANCE

can reserve capacity in an:

AVAILABILITY ZONE

---

## Convertible Reserved Instances

Convertible Reserved Instances provide additional flexibility.

Your course says you can change things such as:

- Instance Type
- Instance Family
- Operating System
- Scope
- Tenancy

But the discount is lower than the highest Reserved Instance discount.

### Memory Trick

Convertible RI = LONG TERM + MORE FLEXIBLE

---

# Savings Plans

## What Are Savings Plans?

Savings Plans provide discounts based on:

LONG-TERM USAGE COMMITMENT

Instead of reserving a specific instance configuration, you commit to a certain amount of:

USAGE PER HOUR

Example from the course:

$10 / HOUR

for:

1 YEAR

or

3 YEARS

### Memory Trick

Savings Plan = COMMIT TO SPEND PER HOUR

---

## Savings Plan Flexibility

Your course describes EC2 Savings Plans as locked to a specific:

INSTANCE FAMILY

+

AWS REGION

Example:

M5

in:

us-east-1

But flexible across:

- Instance Size
- Operating System
- Tenancy

### Example

m5.xlarge

↓

m5.2xlarge

can still fit within the same instance-family commitment.

### Memory Trick

Savings Plan = FAMILY + REGION

but flexible on:

SIZE + OS + TENANCY

---

## Usage Beyond the Savings Plan

If your usage exceeds the committed amount:

EXTRA USAGE

↓

ON-DEMAND PRICE

---

# Spot Instances

## What Are Spot Instances?

Spot Instances provide the:

MOST COST-EFFICIENT

EC2 pricing option in your course.

They can offer very large discounts compared with On-Demand.

BUT:

THE INSTANCE CAN BE LOST / INTERRUPTED

when Spot conditions require it.

### Memory Trick

Spot = CHEAP BUT INTERRUPTIBLE

---

## Best Spot Workloads

Your course lists:

- Batch jobs
- Data analysis
- Image processing
- Distributed workloads
- Workloads with flexible start/end times

Think:

CAN HANDLE FAILURE?

↓

YES

↓

SPOT

---

## Bad Spot Workloads

Your course specifically says Spot is NOT suitable for:

CRITICAL JOBS

or

DATABASES

### Exam Trap

Critical database?

❌ SPOT

Fault-tolerant batch processing?

✅ SPOT

---

# Dedicated Hosts

## What Is a Dedicated Host?

A Dedicated Host is:

AN ENTIRE PHYSICAL SERVER

with EC2 instance capacity:

FULLY DEDICATED TO YOU

### Memory Trick

Dedicated Host = WHOLE SERVER

---

## Dedicated Host Use Cases

Your course emphasizes:

COMPLIANCE

and

SOFTWARE LICENSING

Especially:

BYOL

Bring Your Own License

This is useful for server-bound licensing models such as:

PER-SOCKET

PER-CORE

PER-VM

### Memory Trick

LICENSING / COMPLIANCE

→ DEDICATED HOST

---

## Dedicated Host Pricing

Your course describes Dedicated Hosts as:

THE MOST EXPENSIVE OPTION

Purchasing options include:

ON-DEMAND

or

RESERVED

---

# Dedicated Instances

## What Are Dedicated Instances?

Dedicated Instances run on:

HARDWARE DEDICATED TO YOU

But unlike Dedicated Hosts:

YOU DO NOT CONTROL INSTANCE PLACEMENT

Your course notes that the hardware can change after:

STOP / START

### Memory Trick

Dedicated Instance = DEDICATED HARDWARE

Dedicated Host = CONTROL THE PHYSICAL HOST

---

# Dedicated Host vs Dedicated Instance

| Feature | Dedicated Host | Dedicated Instance |
| --- | --- | --- |
| Dedicated hardware | Yes | Yes |
| Physical server dedicated to you | Yes | Hardware dedicated to you |
| Placement control | Greater host-level control | No placement control |
| Licensing use case | Strong | Not the main distinction |
| Think | WHOLE SERVER | INSTANCE ON DEDICATED HARDWARE |

### Master Memory Trick

HOST

= PHYSICAL SERVER

INSTANCE

= INSTANCE

---

# Capacity Reservations

## What Is a Capacity Reservation?

Capacity Reservations reserve:

ON-DEMAND EC2 CAPACITY

inside a:

SPECIFIC AVAILABILITY ZONE

for:

ANY DURATION

### Memory Trick

Capacity Reservation = GUARANTEE CAPACITY

---

## Capacity Reservation Commitment

There is:

NO TIME COMMITMENT

You can:

CREATE

or

CANCEL

at any time.

BUT:

THERE IS NO BILLING DISCOUNT

### Important

You are charged at the:

ON-DEMAND RATE

whether you:

RUN THE INSTANCE

or

NOT

### Memory Trick

Capacity Reservation = PAY FOR THE SEAT EVEN IF IT'S EMPTY

---

## Capacity Reservation Best Use

Your course recommends it for:

SHORT-TERM

+

UNINTERRUPTED WORKLOADS

that must run in a:

SPECIFIC AZ

Think:

MUST HAVE CAPACITY IN THIS AZ

↓

CAPACITY RESERVATION

---

## Capacity Reservation + Discounts

Capacity Reservations can be combined with:

REGIONAL RESERVED INSTANCES

or

SAVINGS PLANS

to receive billing discounts.

This is an important distinction:

CAPACITY RESERVATION

↓

GUARANTEES CAPACITY

RI / SAVINGS PLAN

↓

CAN PROVIDE DISCOUNT

---

# Reserved Instance vs Capacity Reservation

This is an important exam comparison.

## Reserved Instance

Primary idea:

LONG-TERM DISCOUNT

Can be:

Regional

or

Zonal

Zonal scope can reserve capacity in an AZ.

---

## Capacity Reservation

Primary idea:

GUARANTEE ON-DEMAND CAPACITY

in:

ONE SPECIFIC AZ

No discount by itself.

### Memory Trick

RESERVED INSTANCE

= DISCOUNT / LONG TERM

CAPACITY RESERVATION

= CAPACITY

---

# The Big Comparison

| Option | Best For | Memory Trick |
| --- | --- | --- |
| On-Demand | Short-term unpredictable workload | PAY AS YOU GO |
| Reserved Instance | Steady long-term workload | COMMIT |
| Savings Plan | Long-term usage commitment | COMMIT TO $/HOUR |
| Spot | Fault-tolerant flexible workload | CHEAP |
| Dedicated Host | Licensing/compliance | WHOLE SERVER |
| Dedicated Instance | Dedicated hardware | DEDICATED INSTANCE |
| Capacity Reservation | Guaranteed AZ capacity | GUARANTEE CAPACITY |

---

# Scenario Recognition

Need a short-term workload with no commitment?

→ ON-DEMAND

---

Need a steady database running for years?

→ RESERVED INSTANCE

---

Want a long-term discount but flexibility across instance size, OS, and tenancy?

→ SAVINGS PLAN

---

Need the cheapest option for fault-tolerant batch processing?

→ SPOT

---

Need inexpensive compute for distributed data analysis that can tolerate interruption?

→ SPOT

---

Need an uninterrupted critical database?

→ NOT SPOT

---

Need an entire physical server for licensing requirements?

→ DEDICATED HOST

---

Need dedicated hardware but don't need placement control?

→ DEDICATED INSTANCE

---

Need guaranteed EC2 capacity in one specific AZ?

→ CAPACITY RESERVATION

---

Need guaranteed AZ capacity but also want a billing discount?

→ CAPACITY RESERVATION

+

REGIONAL RI / SAVINGS PLAN

---

# Exam Traps

On-Demand

= NO COMMITMENT

Reserved

= LONG-TERM / STEADY STATE

Savings Plans

= COMMIT TO USAGE PER HOUR

Spot

= CAN BE INTERRUPTED

Dedicated Host

= PHYSICAL SERVER

Dedicated Instance

= NO PLACEMENT CONTROL

Capacity Reservation

= SPECIFIC AZ CAPACITY

Capacity Reservation

≠ DISCOUNT

Reserved Instance

≠ AUTOMATICALLY JUST CAPACITY

---

# Resort Memory Trick

Your course uses a resort/hotel analogy:

ON-DEMAND

= Show up whenever you want and pay full price

RESERVED

= Plan a long stay and get a discount

SAVINGS PLAN

= Commit to spending a certain amount per hour

SPOT

= Cheap empty room, but you can get kicked out

DEDICATED HOST

= Book the entire building

CAPACITY RESERVATION

= Book a room and pay full price even if you don't use it

---

# Quick Cheat Sheet

ON-DEMAND

= NO COMMITMENT

RESERVED

= STEADY + LONG TERM

SAVINGS PLAN

= $/HOUR COMMITMENT

SPOT

= CHEAP + INTERRUPTIBLE

DEDICATED HOST

= WHOLE PHYSICAL SERVER

DEDICATED INSTANCE

= DEDICATED HARDWARE

CAPACITY RESERVATION

= GUARANTEED AZ CAPACITY

---

# Master Memory Trick

UNPREDICTABLE?

→ ON-DEMAND

STEADY?

→ RESERVED

FLEXIBLE LONG-TERM COMMITMENT?

→ SAVINGS PLAN

CAN BE INTERRUPTED?

→ SPOT

LICENSING / COMPLIANCE?

→ DEDICATED HOST

DEDICATED HARDWARE?

→ DEDICATED INSTANCE

MUST HAVE CAPACITY IN THIS AZ?

→ CAPACITY RESERVATION

---

## Related Notes

- [[EC2]]
- [[EC2 Instance Types]]
- [[EC2 Spot Instances]]
- [[EC2 Instance Lifecycle]]
- [[EC2 Placement Groups]]
- [[EC2 Comparison]]
- [[SAA EC2 Cheat Sheet]]
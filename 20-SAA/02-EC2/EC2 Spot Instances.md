## What Problem Does It Solve?

Spot Instances provide:

VERY LOW-COST EC2 COMPUTE

for workloads that can tolerate:

INTERRUPTIONS

### Memory Trick

Spot = CHEAP BUT INTERRUPTIBLE

---

## What Are Spot Instances?

Spot Instances can provide a large discount compared with:

ON-DEMAND

Your course describes them as useful for:

- Batch jobs
- Data analysis
- Failure-resilient workloads

They are NOT a good choice for:

- Critical jobs
- Databases

### Memory Trick

CAN IT FAIL AND RESTART?

YES → SPOT

NO → DON'T USE SPOT

---

## Spot Pricing

Your course describes Spot pricing as varying based on:

OFFER

+

CAPACITY

A Spot request can define a:

MAXIMUM SPOT PRICE

Think:

Your Maximum Price

↓

Current Spot Price

↓

Can the instance run?

---

## Maximum Spot Price

Your course describes this relationship:

CURRENT SPOT PRICE

<

YOUR MAX PRICE

↓

INSTANCE CAN RUN

If:

CURRENT SPOT PRICE

>

YOUR MAX PRICE

↓

INSTANCE CAN BE INTERRUPTED

---

## Spot Interruption

If the current Spot price exceeds your maximum price, your course says you can choose to:

STOP

or

TERMINATE

the instance.

It also identifies a:

2-MINUTE GRACE PERIOD

### Memory Trick

Spot Interruption = 2 MINUTES

---

# Spot Instance Requests

A Spot request can contain information such as:

MAXIMUM PRICE

DESIRED NUMBER OF INSTANCES

LAUNCH SPECIFICATION

REQUEST TYPE

VALID FROM

VALID UNTIL

Think:

SPOT REQUEST

↓

WHAT DO I WANT?

+

HOW MUCH WILL I PAY?

---

## Launch Specification

The Spot request determines what type of instances should be launched.

Think:

REQUEST

↓

LAUNCH SPECIFICATION

↓

EC2 INSTANCES

---

# One-Time vs Persistent

Your course shows two Spot request types:

ONE-TIME

and

PERSISTENT

---

## One-Time Request

Think:

REQUEST INSTANCE

↓

INSTANCE RUNS

↓

REQUEST DOES NOT KEEP TRYING TO MAINTAIN IT

### Memory Trick

One-Time = ONE REQUEST

---

## Persistent Request

A persistent request can continue attempting to maintain the requested Spot capacity.

The course diagram shows persistent requests returning through states such as:

OPEN

ACTIVE

DISABLED

and back into the request process.

### Memory Trick

Persistent = KEEP REQUESTING

---

# Spot Request States

Your course diagram includes states such as:

OPEN

ACTIVE

DISABLED

CLOSED

CANCELLED

FAILED

You do NOT need to overcomplicate these.

The major exam idea is understanding that:

SPOT REQUEST

and

SPOT INSTANCE

are related but separate.

---

# Cancelling Spot Instances

This is an important course distinction.

Cancelling a:

SPOT REQUEST

does NOT automatically:

TERMINATE THE INSTANCE

### Correct Order

FIRST

↓

CANCEL THE SPOT REQUEST

THEN

↓

TERMINATE THE SPOT INSTANCE

### Memory Trick

CANCEL REQUEST

↓

THEN TERMINATE INSTANCE

---

## Why Order Matters

If you're dealing with a persistent Spot request, you don't want the request continuing to seek Spot capacity after you terminate an associated instance.

Think:

CANCEL REQUEST

↓

STOP REQUESTING CAPACITY

↓

TERMINATE INSTANCE

---

## Which Spot Requests Can Be Cancelled?

Your course states that you can cancel Spot Instance requests that are:

OPEN

ACTIVE

or

DISABLED

---

# Spot Fleets

A Spot Fleet is a:

SET OF SPOT INSTANCES

+

OPTIONAL ON-DEMAND INSTANCES

The fleet attempts to meet:

TARGET CAPACITY

while respecting:

PRICE CONSTRAINTS

### Memory Trick

Spot Fleet = GROUP OF CAPACITY OPTIONS

---

## Spot Fleet Launch Pools

You can define multiple:

LAUNCH POOLS

Your course gives characteristics such as:

- Instance Type
- Operating System
- Availability Zone

Example:

m5.large

+

Linux

+

us-east-1a

The fleet can choose between multiple pools.

### Why?

More options give the Spot Fleet more ways to obtain the required capacity.

---

## Spot Fleet Stops Launching When

The fleet reaches:

TARGET CAPACITY

or

MAXIMUM COST

Think:

CAPACITY MET?

→ STOP

MAX COST REACHED?

→ STOP

---

# Spot Fleet Allocation Strategies

Your course identifies four strategies:

LOWEST PRICE

DIVERSIFIED

CAPACITY OPTIMIZED

PRICE CAPACITY OPTIMIZED

---

## Lowest Price

Select instances from the pool with the:

LOWEST PRICE

Best course association:

COST OPTIMIZATION

+

SHORT WORKLOAD

### Memory Trick

Lowest Price = CHEAPEST POOL

---

## Diversified

Distribute instances across:

ALL POOLS

Best course association:

AVAILABILITY

+

LONG WORKLOADS

### Memory Trick

Diversified = SPREAD OUT

---

## Capacity Optimized

Select the pool with the:

OPTIMAL CAPACITY

for the required number of instances.

### Memory Trick

Capacity Optimized = CAPACITY FIRST

---

## Price Capacity Optimized

Your course marks this as:

RECOMMENDED

It first considers pools with:

HIGH CAPACITY AVAILABLE

then selects:

LOWEST PRICE

among those pools.

The course describes it as:

BEST CHOICE FOR MOST WORKLOADS

### Memory Trick

Price Capacity Optimized

=

CAPACITY + PRICE

---

# Spot Fleet Strategy Comparison

| Strategy | Main Goal | Memory Trick |
| --- | --- | --- |
| Lowest Price | Lowest-cost pool | CHEAPEST |
| Diversified | Spread across pools | AVAILABILITY |
| Capacity Optimized | Optimal available capacity | CAPACITY |
| Price Capacity Optimized | Capacity + price | RECOMMENDED |

---

# Scenario Recognition

Need very inexpensive compute for batch jobs?

→ SPOT

---

Need inexpensive compute for data analysis that can tolerate failure?

→ SPOT

---

Need a critical production database?

→ NOT SPOT

---

Need Spot capacity distributed across multiple pools for availability?

→ DIVERSIFIED

---

Need the pool with the lowest price?

→ LOWEST PRICE

---

Need to prioritize available Spot capacity?

→ CAPACITY OPTIMIZED

---

Need the strategy recommended by your course for most workloads?

→ PRICE CAPACITY OPTIMIZED

---

Need to completely stop a Spot request and its instances?

→ CANCEL REQUEST FIRST

→ TERMINATE INSTANCES SECOND

---

# Exam Traps

Spot

= INTERRUPTIBLE

Spot

≠ CRITICAL DATABASES

Cancelling Spot Request

≠ TERMINATING INSTANCE

Correct termination order:

CANCEL REQUEST

↓

TERMINATE INSTANCE

Spot Fleet

= SPOT + OPTIONAL ON-DEMAND

Lowest Price

= COST

Diversified

= AVAILABILITY

Capacity Optimized

= CAPACITY

Price Capacity Optimized

= CAPACITY + PRICE

---

# Quick Cheat Sheet

SPOT

= CHEAP + INTERRUPTIBLE

BEST FOR

= FAILURE-RESILIENT WORKLOADS

BAD FOR

= CRITICAL JOBS / DATABASES

INTERRUPTION

= 2-MINUTE GRACE PERIOD

ONE-TIME

= ONE REQUEST

PERSISTENT

= KEEP REQUESTING

SPOT FLEET

= SPOT + OPTIONAL ON-DEMAND

LOWEST PRICE

= CHEAPEST

DIVERSIFIED

= SPREAD

CAPACITY OPTIMIZED

= CAPACITY

PRICE CAPACITY OPTIMIZED

= RECOMMENDED

---

# Master Memory Trick

CAN THE WORKLOAD HANDLE INTERRUPTION?

YES

↓

SPOT

Need multiple Spot options?

↓

SPOT FLEET

Need recommended allocation strategy?

↓

PRICE CAPACITY OPTIMIZED

Need to shut everything down?

↓

CANCEL REQUEST

↓

TERMINATE INSTANCE

---

## Related Notes

- [[EC2]]
- [[EC2 Instance Types]]
- [[EC2 Purchasing Options]]
- [[EC2 Instance Lifecycle]]
- [[Auto Scaling Groups]]
- [[EC2 Comparison]]
- [[SAA EC2 Cheat Sheet]]
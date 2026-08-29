## What Problem Does It Solve?

AWS provides different EC2 purchasing options so you can balance:

- Cost
- Flexibility
- Availability
- Workload duration
- Compliance requirements

---

## On-Demand Instances

Pay for compute capacity as you use it.

### Best For

- Short-term workloads
- Unpredictable workloads
- Workloads that cannot be interrupted
- Applications where long-term usage is unknown

### Key Characteristics

- No upfront payment
- No long-term commitment
- Highest cost compared with discounted purchasing options

### Memory Trick

On-Demand = No commitment

---

## Reserved Instances

Commit to EC2 usage for:

- 1 year
- 3 years

Designed primarily for long-running, steady-state workloads.

### Best For

- Databases
- Applications that run continuously
- Predictable workloads

### Payment Options

- No Upfront
- Partial Upfront
- All Upfront

Longer commitments and larger upfront payments generally provide greater discounts.

### Memory Trick

Reserved = Predictable long-term workload

---

## Convertible Reserved Instances

A more flexible type of Reserved Instance.

Can change characteristics such as:

- Instance type
- Instance family
- Operating system
- Scope
- Tenancy

Provides greater flexibility than a standard Reserved Instance.

### Memory Trick

Convertible = Reserved but changeable

---

## Savings Plans

Provide discounts in exchange for committing to a certain amount of usage for:

- 1 year
- 3 years

Usage beyond the Savings Plan commitment is charged at On-Demand rates.

Provides flexibility across areas such as:

- Instance size
- Operating system
- Tenancy

### Memory Trick

Savings Plans = Commit to usage

---

## Spot Instances

Use unused EC2 capacity at very low prices.

### Best For

Workloads that can tolerate interruptions:

- Batch jobs
- Data analysis
- Image processing
- Distributed workloads
- Flexible workloads

### Not Good For

- Critical applications
- Databases
- Workloads that cannot tolerate interruption

### Key Benefit

Spot Instances are the most cost-efficient EC2 purchasing option in these notes.

### Memory Trick

Spot = Cheapest but interruptible

---

## Dedicated Hosts

An entire physical EC2 server is dedicated to your use.

### Best For

- Compliance requirements
- Regulatory requirements
- Server-bound software licenses
- BYOL (Bring Your Own License)

### Key Characteristic

Provides control over the underlying physical server.

### Memory Trick

Dedicated Host = Whole physical server

---

## Dedicated Instances

EC2 instances run on hardware dedicated to your account.

Unlike Dedicated Hosts, you do not control instance placement on the physical server.

### Memory Trick

Dedicated Instance = Dedicated hardware

Dedicated Host = Control the host

---

## Capacity Reservations

Reserve EC2 capacity inside a specific Availability Zone.

### Key Characteristics

- Capacity is available when you need it
- No long-term commitment
- Can be created or canceled
- Does not provide a billing discount by itself
- Charged at the On-Demand rate whether the capacity is used or not

### Best For

Workloads that:

- Cannot be interrupted
- Must run in a specific Availability Zone
- Require guaranteed EC2 capacity

### Memory Trick

Capacity Reservation = Guarantee capacity

---

## Purchasing Options Comparison

| Option | Best For | Commitment | Key Benefit |
|---|---|---|---|
| On-Demand | Unpredictable workloads | None | Flexibility |
| Reserved | Steady workloads | 1 or 3 years | Lower cost |
| Convertible Reserved | Steady workloads needing flexibility | 1 or 3 years | Can change configuration |
| Savings Plans | Long-term usage | 1 or 3 years | Flexible discount |
| Spot | Interruptible workloads | None | Lowest cost |
| Dedicated Host | Licensing/compliance | Varies | Physical server control |
| Dedicated Instance | Dedicated hardware | Varies | Hardware isolation |
| Capacity Reservation | Guaranteed AZ capacity | None | Capacity guarantee |

---

## Exam Scenarios

Need EC2 for an unpredictable application with no long-term commitment?

→ On-Demand

---

Need the lowest-cost EC2 option for fault-tolerant batch processing?

→ Spot Instances

---

Database will run continuously for several years?

→ Reserved Instances or Savings Plans

---

Company has server-bound software licenses?

→ Dedicated Host

---

Company absolutely needs EC2 capacity available in one particular AZ?

→ Capacity Reservation

---

## Exam Traps

Spot does NOT guarantee that your instance will continue running.

Capacity Reservation guarantees capacity but does NOT automatically provide a pricing discount.

Dedicated Host and Dedicated Instance are NOT the same thing.

Reserved Instances are primarily suited to predictable, steady-state usage.

---

## Quick Cheat Sheet

On-Demand = Flexible

Reserved = Predictable

Convertible Reserved = Flexible reservation

Savings Plans = Usage commitment

Spot = Cheap + Interruptible

Dedicated Host = Physical server control

Dedicated Instance = Dedicated hardware

Capacity Reservation = Guaranteed capacity
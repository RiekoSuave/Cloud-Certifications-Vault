## What Problem Does It Solve?

Normally, after an EC2 instance starts:

OS BOOTS

↓

APPLICATION STARTS

↓

CACHES WARM UP

This can take:

TIME

EC2 Hibernate solves this by preserving:

RAM STATE

### Memory Trick

Hibernate = SAVE RAM

---

## What Is EC2 Hibernate?

EC2 Hibernate preserves the:

IN-MEMORY STATE

of an EC2 instance.

In other words:

RAM

IS PRESERVED

This allows the instance to resume much faster.

### Memory Trick

Hibernate = PAUSE AND RESUME

---

## How Hibernate Works

When an instance hibernates:

RAM STATE

↓

WRITTEN TO A FILE

↓

ROOT EBS VOLUME

The root EBS volume must be:

ENCRYPTED

Think:

RAM

↓

ENCRYPTED ROOT EBS

↓

HIBERNATE

↓

RESUME

---

## Why Is Resume Faster?

With a normal start:

OS BOOTS

↓

APPLICATION STARTS

↓

CACHES WARM UP

With Hibernate:

RAM STATE IS PRESERVED

and the course states that the:

OS IS NOT STOPPED / RESTARTED

This makes the instance boot/resume:

MUCH FASTER

### Memory Trick

Normal Start = REBUILD STATE

Hibernate = RESTORE STATE

---

# Hibernate Use Cases

Your course lists three main use cases:

- Long-running processing
- Saving RAM state
- Services that take time to initialize

---

## Long-Running Processing

If an EC2 instance is performing:

LONG-RUNNING PROCESSING

and you want to preserve its in-memory state:

→ HIBERNATE

---

## Slow Application Initialization

Some services take significant time to:

START

↓

INITIALIZE

↓

WARM CACHES

Hibernate can preserve the existing state so the instance can resume faster.

### Exam Keyword

SERVICES THAT TAKE TIME TO INITIALIZE

→ HIBERNATE

---

# Hibernate Requirements

Your course gives several requirements and limitations.

---

## RAM Requirement

Instance RAM must be:

LESS THAN 150 GB

### Memory Trick

Hibernate RAM

< 150 GB

---

## Bare Metal

Hibernate is:

NOT SUPPORTED

for:

BARE METAL INSTANCES

---

## Root Volume

The root volume must be:

EBS

+

ENCRYPTED

+

LARGE ENOUGH

It cannot be:

INSTANCE STORE

### Memory Trick

Hibernate Root

= ENCRYPTED EBS

---

## Supported Purchasing Options

Your course states Hibernate is available for:

ON-DEMAND

RESERVED

SPOT

instances.

---

## Supported AMIs

Your course gives examples including:

- Amazon Linux 2
- Linux AMI
- Ubuntu
- RHEL
- CentOS
- Windows

---

## Supported Instance Families

Your course lists examples such as:

- C3
- C4
- C5
- I3
- M3
- M4
- R3
- R4
- T2
- T3

The important exam concept is:

HIBERNATE IS NOT SUPPORTED BY EVERY POSSIBLE CONFIGURATION

---

## Hibernate Duration

Your course states an instance cannot remain hibernated for more than:

60 DAYS

### Memory Trick

Hibernate Limit = 60 DAYS

---

# Stop vs Hibernate

## Stop

EBS data:

PRESERVED

RAM state:

NOT PRESERVED THROUGH HIBERNATION

Following start:

OS BOOTS

↓

APPLICATION STARTS

↓

CACHES WARM UP

---

## Hibernate

EBS data:

PRESERVED

RAM state:

PRESERVED

Resume:

FASTER

### Memory Trick

STOP

= SAVE DISK

HIBERNATE

= SAVE DISK + RAM

---

# Hibernate vs Terminate

## Hibernate

Instance state can later:

RESUME

RAM:

PRESERVED

---

## Terminate

Instance is:

ENDED

EBS volumes configured for deletion can be:

LOST

### Memory Trick

HIBERNATE = COME BACK

TERMINATE = DONE

---

# Scenario Recognition

Need to preserve EC2 RAM?

→ HIBERNATE

---

Application takes a long time to initialize?

→ HIBERNATE

---

Need to preserve a long-running in-memory process?

→ HIBERNATE

---

Need faster EC2 resume?

→ HIBERNATE

---

Need Hibernate but root volume uses Instance Store?

→ NOT SUPPORTED

---

Need Hibernate but root EBS isn't encrypted?

→ NOT SUPPORTED

---

Need Hibernate on bare metal?

→ NOT SUPPORTED

---

# Exam Traps

HIBERNATE

= PRESERVES RAM

HIBERNATE

≠ NORMAL STOP

RAM STATE

→ ROOT EBS

ROOT EBS

= ENCRYPTED

INSTANCE STORE ROOT

= NOT SUPPORTED

BARE METAL

= NOT SUPPORTED

COURSE RAM LIMIT

= LESS THAN 150 GB

COURSE HIBERNATION LIMIT

= 60 DAYS

---

# Quick Cheat Sheet

HIBERNATE

= SAVE RAM

RAM SAVED TO

= ROOT EBS

ROOT EBS

= ENCRYPTED

BENEFIT

= FASTER RESUME

BEST FOR

= LONG INITIALIZATION / LONG PROCESSING

RAM

= < 150 GB

BARE METAL

= NO

INSTANCE STORE ROOT

= NO

ON-DEMAND

= YES

RESERVED

= YES

SPOT

= YES

MAX COURSE DURATION

= 60 DAYS

---

# Master Memory Trick

Need to:

SAVE RAM?

↓

HIBERNATE

How?

↓

RAM

↓

ENCRYPTED ROOT EBS

↓

RESUME LATER

Remember:

STOP = SAVE DISK

HIBERNATE = SAVE DISK + RAM

TERMINATE = END

---

## Related Notes

- [[EC2]]
- [[EC2 Instance Lifecycle]]
- [[EC2 User Data]]
- [[EC2 Purchasing Options]]
- [[EBS Volumes]]
- [[03-Storage/EC2 Instance Store]]
- [[EC2 Comparison]]
- [[SAA EC2 Cheat Sheet]]
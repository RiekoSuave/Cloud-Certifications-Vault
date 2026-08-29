## What Problem Does It Solve?

Understanding the EC2 instance lifecycle helps you know what happens to:

DATA

OPERATING SYSTEM

APPLICATIONS

and

MEMORY

when an EC2 instance changes state.

The important actions in this section are:

STOP

TERMINATE

START

HIBERNATE

---

# Stop

When you:

STOP

an EC2 instance, your course states that the data on:

EBS

is kept intact for the:

NEXT START

Think:

RUNNING

↓

STOP

↓

EBS DATA REMAINS

↓

START AGAIN

### Memory Trick

STOP = EBS DATA STAYS

---

# Start

What happens when an instance starts depends on whether it is the:

FIRST START

or a:

FOLLOWING START

---

## First Start

On the first start:

OPERATING SYSTEM BOOTS

↓

EC2 USER DATA RUNS

Remember:

[[EC2 User Data]]

is associated with:

FIRST START

### Memory Trick

FIRST START

= OS BOOT + USER DATA

---

## Following Starts

On following starts:

OPERATING SYSTEM BOOTS

Then:

APPLICATION STARTS

↓

CACHES WARM UP

This process can:

TAKE TIME

### Memory Trick

NORMAL START

= BOOT + APP + CACHE

---

# Terminate

When you:

TERMINATE

an EC2 instance, EBS volumes configured to be:

DESTROYED ON TERMINATION

are:

LOST

Your course specifically highlights the:

ROOT EBS VOLUME

when configured this way.

### Memory Trick

TERMINATE = WATCH YOUR EBS DELETE SETTING

---

# Stop vs Terminate

| Action | Key Course Behavior |
| --- | --- |
| Stop | EBS data remains intact for next start |
| Terminate | EBS volumes configured for destruction are lost |

### Memory Trick

STOP

= COME BACK LATER

TERMINATE

= INSTANCE IS DONE

---

# Why Starting Can Take Time

A normal start can involve:

OS BOOT

↓

APPLICATION START

↓

CACHE WARM-UP

For applications that take a long time to initialize, this startup process may be undesirable.

This leads to:

EC2 HIBERNATE

---

# Hibernate

Hibernate is designed to preserve the:

IN-MEMORY STATE

of an EC2 instance.

Think:

RAM

↓

SAVE

↓

HIBERNATE

↓

RESTORE LATER

### Memory Trick

Hibernate = SAVE RAM

---

## What Happens During Hibernate?

Instead of losing the contents of RAM:

RAM STATE

↓

WRITTEN TO FILE

↓

ROOT EBS VOLUME

When the instance resumes, that saved state can be restored.

---

## Hibernate vs Normal Stop

### Normal Stop

RAM STATE

→ NOT PRESERVED BY THIS HIBERNATION MECHANISM

Next start requires:

OS BOOT

↓

APPLICATION START

↓

CACHE WARM-UP

---

### Hibernate

RAM STATE

→ PRESERVED

The course says the:

OS IS NOT STOPPED / RESTARTED

in the same way.

This results in:

FASTER BOOT / RESUME

### Memory Trick

STOP = START OVER

HIBERNATE = RESUME

---

# Hibernate Storage Requirement

The RAM state is written to:

ROOT EBS VOLUME

Therefore, your course requires the root EBS volume to be:

ENCRYPTED

Think:

RAM

↓

ROOT EBS

↓

ENCRYPTED

### Memory Trick

Hibernate = ENCRYPTED ROOT EBS

---

# Hibernate Use Cases

Your course lists:

LONG-RUNNING PROCESSING

SAVING RAM STATE

SERVICES THAT TAKE TIME TO INITIALIZE

### Scenario

Application takes a long time to:

START

and

WARM ITS CACHE

Need to preserve its in-memory state?

→ HIBERNATE

---

# Hibernate Requirements From Course

Your slides list several requirements and limitations.

### Supported Instance Families

Examples include:

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

---

### RAM

Instance RAM must be:

LESS THAN 150 GB

---

### Bare Metal

Hibernate is:

NOT SUPPORTED

for:

BARE METAL INSTANCES

---

### AMIs

Course examples include:

- Amazon Linux 2
- Linux AMI
- Ubuntu
- RHEL
- CentOS
- Windows

---

### Root Volume

Must be:

EBS

ENCRYPTED

LARGE ENOUGH

Cannot be:

INSTANCE STORE

---

### Purchasing Options

Your course states Hibernate is available for:

ON-DEMAND

RESERVED

SPOT

instances.

---

### Hibernate Duration

Your course states an instance cannot remain hibernated for more than:

60 DAYS

---

# Stop vs Hibernate vs Terminate

| Action | EBS | RAM | Think |
| --- | --- | --- | --- |
| Stop | Kept | Not preserved via hibernation | PAUSE SERVER |
| Hibernate | Kept | Preserved | SAVE RAM |
| Terminate | Delete-configured volumes lost | Not preserved | END INSTANCE |

---

# Scenario Recognition

Need to stop an instance and keep its EBS data?

→ STOP

---

Need to permanently end an EC2 instance?

→ TERMINATE

---

Need to preserve RAM state?

→ HIBERNATE

---

Application takes a long time to initialize?

→ HIBERNATE

---

Need faster resume while preserving in-memory state?

→ HIBERNATE

---

First time an EC2 instance starts?

→ OS BOOTS + USER DATA RUNS

---

Following normal start?

→ OS BOOTS + APPLICATION STARTS + CACHES WARM UP

---

# Exam Traps

STOP

≠ TERMINATE

STOP

= EBS DATA KEPT

TERMINATE

= DELETE-CONFIGURED EBS VOLUMES LOST

FIRST START

= USER DATA RUNS

HIBERNATE

= RAM PRESERVED

HIBERNATE

= ROOT EBS REQUIRED

HIBERNATE ROOT EBS

= ENCRYPTED

HIBERNATE

≠ INSTANCE STORE ROOT

---

# Quick Cheat Sheet

STOP

= KEEP EBS

START

= BOOT OS

FIRST START

= USER DATA

TERMINATE

= END INSTANCE

HIBERNATE

= SAVE RAM

RAM SAVED TO

= ROOT EBS

HIBERNATE EBS

= ENCRYPTED

HIBERNATE BENEFIT

= FASTER RESUME

---

# Master Memory Trick

STOP

= SAVE DISK

HIBERNATE

= SAVE DISK + RAM STATE

TERMINATE

= END

FIRST START

= USER DATA

---

## Related Notes

- [[EC2]]
- [[EC2 User Data]]
- [[EC2 Purchasing Options]]
- [[EC2 Hibernate]]
- [[EBS Volumes]]
- [[03-Storage/EC2 Instance Store]]
- [[EC2 Comparison]]
- [[SAA EC2 Cheat Sheet]]
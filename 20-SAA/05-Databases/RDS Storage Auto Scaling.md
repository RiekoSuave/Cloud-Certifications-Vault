## What Problem Does It Solve?

A relational database can grow over time.

If the RDS database runs out of storage:

DATABASE WRITES

↓

MAY FAIL

Manually monitoring storage and constantly increasing it can create:

OPERATIONAL OVERHEAD

RDS Storage Auto Scaling automatically:

INCREASES DATABASE STORAGE

when available storage becomes low.

Think:

DATABASE GROWS

↓

FREE STORAGE DECREASES

↓

RDS DETECTS LOW STORAGE

↓

STORAGE AUTOMATICALLY INCREASES

### Memory Trick

RDS STORAGE AUTO SCALING

=

AUTO GROW DATABASE DISK

---

## What Is RDS Storage Auto Scaling?

RDS Storage Auto Scaling allows RDS to:

AUTOMATICALLY INCREASE

the amount of storage allocated to a database.

Think:

CURRENT STORAGE

↓

100 GB

DATABASE GROWS

↓

MORE SPACE NEEDED

↓

RDS INCREASES STORAGE

The goal is to avoid:

MANUALLY SCALING STORAGE

every time the database grows.

### Memory Trick

STORAGE AUTO SCALING

=

RDS ADDS SPACE FOR YOU

---

## Why Is Storage Auto Scaling Useful?

Database storage requirements may be:

DIFFICULT TO PREDICT

Imagine:

DATABASE

↓

100 GB

↓

150 GB

↓

220 GB

↓

350 GB

Instead of constantly monitoring and manually increasing storage:

RDS

↓

MONITORS FREE STORAGE

↓

AUTOMATICALLY INCREASES STORAGE

This is especially useful for:

UNPREDICTABLE WORKLOADS

### Memory Trick

UNPREDICTABLE DATABASE GROWTH

=

STORAGE AUTO SCALING

---

## Maximum Storage Threshold

When enabling Storage Auto Scaling, you define:

MAXIMUM STORAGE THRESHOLD

This determines:

HOW LARGE RDS IS ALLOWED TO GROW

Think:

ALLOCATED STORAGE

=

100 GB

MAXIMUM STORAGE THRESHOLD

=

500 GB

RDS can automatically grow:

100 GB

↓

200 GB

↓

300 GB

↓

UP TO 500 GB

### Memory Trick

MAX STORAGE THRESHOLD

=

AUTO SCALING CEILING

---

## Why Set a Maximum Storage Threshold?

Without a limit:

STORAGE

could continue growing.

The Maximum Storage Threshold provides:

CONTROL

over how much storage RDS can automatically allocate.

Think:

AUTO SCALE

↓

BUT ONLY UP TO

↓

MAXIMUM THRESHOLD

### Memory Trick

AUTO SCALE

≠

UNLIMITED SCALE

---

## Storage Auto Scaling Trigger

Your SAA course gives three important conditions.

RDS automatically modifies storage when:

FREE STORAGE

is less than:

10%

of allocated storage

AND

the low-storage condition lasts for at least:

5 MINUTES

AND

at least:

6 HOURS

have passed since the last storage modification.

Think:

FREE STORAGE < 10%

↓

FOR 5 MINUTES

↓

LAST MODIFICATION ≥ 6 HOURS AGO

↓

RDS INCREASES STORAGE

### Memory Trick

10

↓

5

↓

6

10% FREE

5 MINUTES

6 HOURS

---

## The 10-5-6 Rule

This is an important number sequence to recognize.

10%

=

FREE STORAGE THRESHOLD

5 MINUTES

=

LOW STORAGE DURATION

6 HOURS

=

TIME SINCE LAST STORAGE MODIFICATION

Think:

10

↓

5

↓

6

### Memory Trick

RDS STORAGE AUTO SCALING

=

10 - 5 - 6

---

## Example

Imagine an RDS database has:

100 GB

of allocated storage.

Free storage falls below:

10 GB

because:

10 GB

=

10% OF 100 GB

The condition remains for:

5 MINUTES

And the last storage modification occurred:

MORE THAN 6 HOURS AGO

Think:

FREE SPACE < 10%

↓

5 MINUTES

↓

6 HOURS SINCE LAST CHANGE

↓

STORAGE AUTO SCALING

RDS can now automatically:

INCREASE ALLOCATED STORAGE

---

## Storage Scaling Is Automatic

Once configured, you do not need to:

MANUALLY MODIFY STORAGE

every time available space becomes low.

Think:

CLOUDWATCH / RDS MONITORING

↓

LOW FREE STORAGE

↓

RDS

↓

AUTOMATIC STORAGE MODIFICATION

### Memory Trick

SET THE MAXIMUM

↓

LET RDS GROW

---

## Storage Can Increase

RDS Storage Auto Scaling:

INCREASES

allocated storage.

Think:

100 GB

↓

150 GB

↓

200 GB

It is designed to handle:

DATABASE STORAGE GROWTH

### Exam Thinking

Question says:

DATABASE KEEPS GROWING

and wants:

MINIMAL ADMINISTRATION

↓

RDS STORAGE AUTO SCALING

---

## Storage Auto Scaling vs Compute Scaling

Do not confuse:

DATABASE STORAGE

with:

DATABASE COMPUTE

### Storage Auto Scaling

Changes:

STORAGE CAPACITY

Think:

GB / TB

---

### Compute Scaling

Changes:

DB INSTANCE SIZE

Think:

CPU

↓

RAM

### Memory Trick

STORAGE AUTO SCALING

=

MORE DISK

NOT

MORE CPU

---

## Storage Auto Scaling vs Read Replicas

Do not confuse:

STORAGE CAPACITY

with:

READ CAPACITY

### Storage Auto Scaling

Problem:

RUNNING OUT OF DISK SPACE

Solution:

INCREASE STORAGE

---

### Read Replica

Problem:

TOO MANY READ REQUESTS

Solution:

ADD READ CAPACITY

Think:

DISK FULL?

↓

STORAGE AUTO SCALING

READ TRAFFIC HIGH?

↓

READ REPLICA

### Memory Trick

STORAGE

=

SPACE

READ REPLICA

=

PERFORMANCE

---

## Storage Auto Scaling vs Multi-AZ

Do not confuse:

STORAGE GROWTH

with:

HIGH AVAILABILITY

### Storage Auto Scaling

Purpose:

MORE DATABASE STORAGE

### Multi-AZ

Purpose:

DATABASE FAILOVER

Think:

NEED MORE SPACE?

↓

STORAGE AUTO SCALING

NEED TO SURVIVE FAILURE?

↓

MULTI-AZ

---

## Supported Database Engines

RDS Storage Auto Scaling supports:

ALL RDS DATABASE ENGINES

Think:

RDS ENGINE

↓

STORAGE AUTO SCALING AVAILABLE

This makes it useful across different relational database deployments.

### Memory Trick

RDS STORAGE AUTO SCALING

=

ALL RDS ENGINES

---

## Unpredictable Workloads

One of the strongest exam clues is:

UNPREDICTABLE DATABASE STORAGE GROWTH

Example:

An application stores customer records.

The company does not know:

HOW FAST THE DATABASE WILL GROW

Requirements:

MINIMAL ADMINISTRATION

↓

AVOID RUNNING OUT OF STORAGE

↓

AUTOMATICALLY INCREASE STORAGE

Answer:

RDS STORAGE AUTO SCALING

### Memory Trick

UNPREDICTABLE GROWTH

+

MINIMAL ADMIN

=

STORAGE AUTO SCALING

---

## Architecture Thinking

Imagine:

APPLICATION

↓

RDS

↓

ALLOCATED STORAGE

Database grows:

DATA ↑

↓

FREE STORAGE ↓

↓

FREE STORAGE < 10%

↓

REMAINS LOW FOR 5 MINUTES

↓

LAST MODIFICATION ≥ 6 HOURS

↓

RDS STORAGE AUTO SCALING

↓

MORE STORAGE

The application continues using:

THE SAME DATABASE

while RDS manages the storage increase.

---

## Maximum Threshold Architecture

Think:

INITIAL STORAGE

↓

100 GB

MAXIMUM STORAGE

↓

1000 GB

RDS can automatically grow:

100 GB

↓

200 GB

↓

400 GB

↓

...

but cannot automatically exceed:

1000 GB MAXIMUM THRESHOLD

### Memory Trick

INITIAL STORAGE

=

START

MAXIMUM THRESHOLD

=

STOP

---

## Scenario Recognition

Database storage growth is unpredictable?

→ RDS Storage Auto Scaling

---

Need RDS storage to automatically increase?

→ RDS Storage Auto Scaling

---

Need to reduce manual database storage management?

→ RDS Storage Auto Scaling

---

Need to prevent an RDS database from running out of storage?

→ RDS Storage Auto Scaling

---

Need to define how far storage can automatically grow?

→ Maximum Storage Threshold

---

Free storage falls below 10% for at least 5 minutes?

→ Storage Auto Scaling condition

---

Question mentions 6 hours since the last storage modification?

→ RDS Storage Auto Scaling

---

Need more CPU or RAM?

→ Not Storage Auto Scaling

Think:

SCALE DB INSTANCE

---

Need more read capacity?

→ RDS Read Replicas

---

Need database failover?

→ RDS Multi-AZ

---

## Exam Traps

RDS STORAGE AUTO SCALING

=

STORAGE

NOT

COMPUTE

---

STORAGE AUTO SCALING

=

AUTOMATIC STORAGE INCREASE

---

MAXIMUM STORAGE THRESHOLD

=

AUTO SCALING LIMIT

---

FREE STORAGE

<

10%

---

LOW STORAGE CONDITION

=

5 MINUTES

---

TIME SINCE LAST STORAGE MODIFICATION

=

6 HOURS

---

MEMORY SEQUENCE

=

10 - 5 - 6

---

UNPREDICTABLE STORAGE GROWTH

=

STORAGE AUTO SCALING

---

STORAGE AUTO SCALING

≠

READ REPLICA

---

STORAGE AUTO SCALING

≠

MULTI-AZ

---

READ REPLICA

=

READ SCALING

MULTI-AZ

=

HIGH AVAILABILITY

STORAGE AUTO SCALING

=

DISK CAPACITY

---

## Quick Cheat Sheet

PURPOSE

=

AUTOMATICALLY INCREASE RDS STORAGE

BEST USE CASE

=

UNPREDICTABLE DATABASE GROWTH

MAXIMUM STORAGE THRESHOLD

=

MAX AUTO-SCALING STORAGE

FREE STORAGE TRIGGER

=

LESS THAN 10%

LOW STORAGE DURATION

=

5 MINUTES

LAST STORAGE MODIFICATION

=

AT LEAST 6 HOURS

MEMORY RULE

=

10 - 5 - 6

SUPPORTED ENGINES

=

ALL RDS DATABASE ENGINES

STORAGE AUTO SCALING

=

MORE DISK

READ REPLICA

=

MORE READ CAPACITY

MULTI-AZ

=

HIGH AVAILABILITY

---

## Master Memory Trick

DATABASE GROWS

↓

FREE STORAGE FALLS

↓

10%

↓

5 MINUTES

↓

6 HOURS

↓

RDS ADDS STORAGE

Remember:

10

=

PERCENT

5

=

MINUTES

6

=

HOURS

And:

STORAGE AUTO SCALING

=

MORE SPACE

READ REPLICA

=

MORE READS

MULTI-AZ

=

MORE AVAILABILITY

### Final Rule

UNPREDICTABLE DATABASE GROWTH

+

MINIMAL ADMINISTRATION

↓

RDS STORAGE AUTO SCALING

---

## Related Notes

- [RDS Overview](<RDS Overview>)
- [RDS Read Replicas](<RDS Read Replicas>)
- [RDS Multi-AZ](<RDS Multi-AZ>)
- [RDS Backups](<RDS Backups>)
- [Aurora](04-Databases/Aurora.md)
- [RDS Proxy](<RDS Proxy>)
- [EBS Volumes](<EBS Volumes>)
- [CloudWatch](07-Monitoring/CloudWatch.md)
- [SAA Databases Cheat Sheet](<SAA Databases Cheat Sheet>)
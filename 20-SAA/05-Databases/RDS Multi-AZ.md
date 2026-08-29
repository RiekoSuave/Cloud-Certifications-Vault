## What Problem Does It Solve?

A production database can fail because of:

DATABASE INSTANCE FAILURE

↓

STORAGE FAILURE

↓

NETWORK FAILURE

↓

AVAILABILITY ZONE FAILURE

If an application depends on:

ONE DATABASE

in:

ONE AVAILABILITY ZONE

then a database failure can cause:

APPLICATION DOWNTIME

RDS Multi-AZ provides:

HIGH AVAILABILITY

and:

DISASTER RECOVERY

by maintaining a standby database in:

ANOTHER AVAILABILITY ZONE

Think:

PRIMARY FAILS

↓

STANDBY TAKES OVER

### Memory Trick

RDS MULTI-AZ

=

DATABASE FAILOVER

---

## What Is RDS Multi-AZ?

RDS Multi-AZ maintains:

PRIMARY DATABASE

and:

STANDBY DATABASE

in:

DIFFERENT AVAILABILITY ZONES

Think:

AZ-A

↓

PRIMARY RDS

↓

SYNCHRONOUS REPLICATION

↓

AZ-B

↓

STANDBY RDS

The standby exists primarily for:

HIGH AVAILABILITY

and:

FAILOVER

### Memory Trick

MULTI-AZ

=

PRIMARY + STANDBY

---

## Multi-AZ Architecture

Imagine:

APPLICATION

↓

RDS DNS NAME

↓

PRIMARY DB

↓

AZ-A

At the same time:

PRIMARY DB

↓

SYNC REPLICATION

↓

STANDBY DB

↓

AZ-B

Think:

APPLICATION

↓

ONE DATABASE ENDPOINT

↓

PRIMARY

↓

SYNC

↓

STANDBY

If the primary fails:

STANDBY

↓

BECOMES NEW PRIMARY

---

## Synchronous Replication

RDS Multi-AZ uses:

SYNCHRONOUS REPLICATION

Think:

APPLICATION WRITE

↓

PRIMARY DATABASE

↓

SYNC REPLICATION

↓

STANDBY DATABASE

The goal is to keep the standby:

UP TO DATE

for failover.

### Memory Trick

MULTI-AZ

=

SYNC

---

## Why Synchronous Replication?

The standby must be ready to:

TAKE OVER

if the primary fails.

Think:

PRIMARY

↓

DATA WRITTEN

↓

STANDBY UPDATED

↓

READY FOR FAILOVER

This is different from:

[RDS Read Replicas](<RDS Read Replicas>)

which use:

ASYNCHRONOUS REPLICATION

### Memory Trick

MULTI-AZ

=

SYNC FOR SURVIVAL

READ REPLICA

=

ASYNC FOR SCALING

---

## Standby Database

The Multi-AZ standby is:

NOT

primarily used to serve application traffic.

Think:

APPLICATION

↓

PRIMARY

NOT:

APPLICATION

↓

STANDBY FOR READS

The standby waits for:

FAILOVER

### Memory Trick

STANDBY

=

WAITING TO TAKE OVER

---

## Multi-AZ Is Not Read Scaling

This is one of the biggest SAA exam traps.

RDS Multi-AZ is:

NOT USED FOR SCALING

Think:

NEED MORE READ CAPACITY?

↓

NOT MULTI-AZ

↓

USE READ REPLICA

Need:

HIGH AVAILABILITY?

↓

MULTI-AZ

### Memory Trick

MULTI-AZ

=

AVAILABILITY

NOT

PERFORMANCE

---

## One DNS Name

RDS Multi-AZ uses:

ONE DNS NAME

for the database connection.

Think:

APPLICATION

↓

DATABASE DNS NAME

↓

CURRENT PRIMARY

The application does not need to know:

WHICH PHYSICAL DATABASE INSTANCE

is currently primary.

### Memory Trick

ONE DNS NAME

=

AWS HANDLES FAILOVER

---

## Automatic Failover

If the primary database fails:

RDS

↓

DETECTS FAILURE

↓

FAILS OVER

↓

STANDBY BECOMES PRIMARY

The application continues using:

THE SAME DATABASE DNS NAME

Think:

PRIMARY FAILURE

↓

AUTOMATIC FAILOVER

↓

STANDBY PROMOTED

↓

DNS POINTS TO NEW PRIMARY

### Memory Trick

MULTI-AZ

=

AUTOMATIC FAILOVER

---

## No Manual Application Intervention

Your application does not need to manually:

CHANGE DATABASE ENDPOINTS

during normal Multi-AZ failover.

Think:

APPLICATION

↓

SAME DNS NAME

↓

AWS CHANGES BACKEND DATABASE

### Memory Trick

SAME DNS

↓

NEW PRIMARY

This reduces:

MANUAL FAILOVER WORK

---

## What Can Trigger Failover?

Your SAA course highlights several failure scenarios.

Failover can occur because of:

LOSS OF AVAILABILITY ZONE

↓

LOSS OF NETWORK

↓

DATABASE INSTANCE FAILURE

↓

STORAGE FAILURE

Think:

DATABASE CAN'T SERVE PROPERLY

↓

RDS FAILOVER

↓

STANDBY TAKES OVER

### Memory Trick

AZ

NETWORK

INSTANCE

STORAGE

↓

FAILOVER

---

## Availability Zone Failure

Imagine:

AZ-A

↓

PRIMARY RDS

AZ-B

↓

STANDBY RDS

Then:

AZ-A FAILS

↓

PRIMARY UNAVAILABLE

↓

RDS FAILOVER

↓

AZ-B STANDBY

↓

NEW PRIMARY

This provides:

HIGH AVAILABILITY

across Availability Zones.

### Memory Trick

AZ FAILURE

=

MULTI-AZ SURVIVES

---

## Instance Failure

Imagine the primary database instance experiences:

INSTANCE FAILURE

Think:

PRIMARY RDS

↓

FAILS

↓

STANDBY

↓

PROMOTED

The application continues connecting through:

THE RDS DNS NAME

---

## Storage Failure

If the primary experiences:

STORAGE FAILURE

Multi-AZ can fail over to:

THE STANDBY DATABASE

Think:

PRIMARY STORAGE FAILS

↓

STANDBY TAKES OVER

### Exam Thinking

Question mentions:

DATABASE STORAGE FAILURE

+

MINIMIZE DOWNTIME

↓

THINK RDS MULTI-AZ

---

## Network Failure

If connectivity to the primary database is lost:

NETWORK FAILURE

↓

PRIMARY UNREACHABLE

↓

FAILOVER

↓

STANDBY

This is another reason Multi-AZ improves:

DATABASE AVAILABILITY

---

## Multi-AZ and Disaster Recovery

RDS Multi-AZ is designed for:

DISASTER RECOVERY

within the database deployment.

Think:

PRIMARY DATABASE FAILURE

↓

STANDBY READY

↓

AUTOMATIC FAILOVER

Your course repeatedly associates:

MULTI-AZ

with:

DR

### Memory Trick

MULTI-AZ

=

DR

---

## Multi-AZ and High Availability

Multi-AZ increases:

AVAILABILITY

because the database is not dependent on:

ONE AZ

Think:

ONE AZ

=

SINGLE FAILURE DOMAIN

MULTI-AZ

=

SECOND DATABASE IN ANOTHER AZ

### Memory Trick

MULTI-AZ

=

SURVIVE DATABASE FAILURE

---

## Read Replica vs Multi-AZ

This distinction is critical.

### Read Replica

PURPOSE

=

READ SCALABILITY

REPLICATION

=

ASYNCHRONOUS

APPLICATION READ TRAFFIC

=

YES

REPLICATION LAG

=

POSSIBLE

---

### Multi-AZ

PURPOSE

=

HIGH AVAILABILITY / DR

REPLICATION

=

SYNCHRONOUS

STANDBY FOR NORMAL READ SCALING

=

NO

FAILOVER

=

AUTOMATIC

### Memory Trick

READ REPLICA

=

PERFORMANCE

MULTI-AZ

=

SURVIVAL

---

## Async vs Sync

### Read Replica

PRIMARY

↓

ASYNC

↓

READ REPLICA

Think:

READ PERFORMANCE

+

POSSIBLE LAG

---

### Multi-AZ

PRIMARY

↓

SYNC

↓

STANDBY

Think:

HIGH AVAILABILITY

+

FAILOVER

### Memory Trick

ASYNC

=

READ REPLICA

SYNC

=

MULTI-AZ

---

## Read Traffic vs Failover

Need:

MORE READS?

↓

READ REPLICA

Need:

DATABASE FAILOVER?

↓

MULTI-AZ

Think:

TRAFFIC PROBLEM

↓

READ REPLICA

FAILURE PROBLEM

↓

MULTI-AZ

---

## Read Replica Can Be Multi-AZ

A Read Replica can itself be configured as:

MULTI-AZ

for:

DISASTER RECOVERY

Think:

PRIMARY

↓

READ REPLICA

↓

READ SCALING

Then:

READ REPLICA

↓

MULTI-AZ

↓

HIGH AVAILABILITY

This shows that:

READ REPLICAS

and:

MULTI-AZ

solve different problems and can be:

COMBINED

### Memory Trick

READ REPLICA

=

SCALE

MULTI-AZ

=

PROTECT

---

## Converting Single-AZ to Multi-AZ

A Single-AZ RDS database can be changed into:

MULTI-AZ

Think:

SINGLE-AZ RDS

↓

ENABLE MULTI-AZ

↓

PRIMARY

+

STANDBY

AWS manages the process of creating the standby.

### Exam Thinking

Need to improve availability of an existing RDS database?

↓

ENABLE MULTI-AZ

---

## Multi-AZ Does Not Require Application Changes

Because the application uses:

ONE DNS NAME

you do not normally need to redesign the application to manually choose:

PRIMARY

or:

STANDBY

Think:

APP

↓

SAME ENDPOINT

↓

AWS MANAGES PRIMARY LOCATION

### Memory Trick

MULTI-AZ FAILOVER

=

DATABASE CHANGES

APP ENDPOINT DOESN'T

---

## Multi-AZ Network Cost

For RDS Multi-AZ:

REPLICATION TRAFFIC

between the primary and standby does not incur the same cross-AZ replication charge associated with ordinary cross-AZ Read Replica traffic.

Think:

PRIMARY

↓

SYNC REPLICATION

↓

STANDBY

↓

MULTI-AZ

### Exam Thinking

Do not confuse:

CROSS-AZ READ REPLICA

with:

MULTI-AZ STANDBY

They have different:

PURPOSES

and:

COST BEHAVIOR

---

## Multi-AZ Architecture Thinking

A highly available application might use:

USERS

↓

[Application Load Balancer](<Application Load Balancer>)

↓

[Auto Scaling Groups](<Auto Scaling Groups>)

↓

EC2 INSTANCES ACROSS MULTIPLE AZs

↓

RDS DNS NAME

↓

PRIMARY RDS

↓

SYNC REPLICATION

↓

STANDBY RDS

Think:

APPLICATION TIER

=

MULTI-AZ EC2

DATABASE TIER

=

MULTI-AZ RDS

This removes dependence on:

ONE APPLICATION SERVER

and:

ONE DATABASE AZ

---

## Failure Architecture

Normal operation:

APPLICATION

↓

DNS NAME

↓

PRIMARY

AZ-A

↓

SYNC

↓

STANDBY

AZ-B

Then:

AZ-A FAILS

↓

PRIMARY LOST

↓

RDS AUTOMATIC FAILOVER

↓

STANDBY PROMOTED

↓

DNS POINTS TO NEW PRIMARY

↓

APPLICATION RECONNECTS

### Memory Trick

FAIL

↓

PROMOTE

↓

DNS

↓

RECONNECT

---

## Multi-AZ vs Backups

Do not confuse:

HIGH AVAILABILITY

with:

BACKUPS

### Multi-AZ

Purpose:

KEEP DATABASE AVAILABLE

during infrastructure failure.

### Backups

Purpose:

RECOVER DATA

from an earlier point in time.

Think:

SERVER / AZ FAILURE

↓

MULTI-AZ

ACCIDENTALLY DELETE DATA

↓

BACKUP / POINT-IN-TIME RESTORE

### Memory Trick

MULTI-AZ

=

AVAILABILITY

BACKUP

=

RECOVERY

---

## Multi-AZ Does Not Replace Backups

Even with Multi-AZ:

YOU STILL NEED BACKUPS

Why?

If bad data is written to the primary:

BAD WRITE

↓

SYNC REPLICATION

↓

BAD WRITE ALSO REACHES STANDBY

Think:

MULTI-AZ

=

INFRASTRUCTURE PROTECTION

NOT:

UNDO BUTTON

### Exam Thinking

Need protection from:

ACCIDENTAL DELETION

↓

BACKUPS

Need protection from:

DATABASE INSTANCE / AZ FAILURE

↓

MULTI-AZ

---

## Scenario Recognition

Need RDS high availability?

→ RDS Multi-AZ

---

Need automatic database failover?

→ RDS Multi-AZ

---

Need disaster recovery for an RDS deployment?

→ RDS Multi-AZ

---

Need synchronous replication?

→ RDS Multi-AZ

---

Need standby database in another AZ?

→ RDS Multi-AZ

---

Need one DNS name with automatic failover?

→ RDS Multi-AZ

---

Need database availability during an AZ outage?

→ RDS Multi-AZ

---

Need failover after network failure?

→ RDS Multi-AZ

---

Need failover after database instance failure?

→ RDS Multi-AZ

---

Need failover after storage failure?

→ RDS Multi-AZ

---

Need more read capacity?

→ RDS Read Replica

NOT:

RDS Multi-AZ

---

Need reporting queries offloaded from primary?

→ RDS Read Replica

---

Need recovery after accidental data deletion?

→ RDS Backups

NOT:

RDS Multi-AZ

---

## Exam Traps

RDS MULTI-AZ

=

HIGH AVAILABILITY

---

RDS MULTI-AZ

=

DISASTER RECOVERY

---

MULTI-AZ

=

SYNCHRONOUS REPLICATION

---

READ REPLICA

=

ASYNCHRONOUS REPLICATION

---

MULTI-AZ

=

ONE DNS NAME

---

FAILOVER

=

AUTOMATIC

---

APPLICATION

=

NO MANUAL ENDPOINT CHANGE

---

STANDBY

=

NOT USED FOR NORMAL READ SCALING

---

MULTI-AZ

=

NOT USED FOR SCALING

---

READ REPLICA

=

READ SCALING

---

READ REPLICA

=

PERFORMANCE

MULTI-AZ

=

AVAILABILITY

---

MULTI-AZ

≠

BACKUP

---

MULTI-AZ

=

INFRASTRUCTURE FAILURE PROTECTION

BACKUP

=

DATA RECOVERY

---

BAD DATA WRITTEN TO PRIMARY

↓

CAN REPLICATE TO STANDBY

Therefore:

MULTI-AZ

≠

UNDO ACCIDENTAL DATA CHANGES

---

## Quick Cheat Sheet

RDS MULTI-AZ

=

HIGH AVAILABILITY / DR

ARCHITECTURE

=

PRIMARY + STANDBY

AZs

=

DIFFERENT

REPLICATION

=

SYNCHRONOUS

DNS

=

ONE DNS NAME

FAILOVER

=

AUTOMATIC

MANUAL APP INTERVENTION

=

NO

STANDBY READ SCALING

=

NO

SCALING PURPOSE

=

NO

READ REPLICA

=

READ SCALING

READ REPLICA REPLICATION

=

ASYNC

MULTI-AZ REPLICATION

=

SYNC

AZ FAILURE

=

FAILOVER

NETWORK FAILURE

=

FAILOVER

INSTANCE FAILURE

=

FAILOVER

STORAGE FAILURE

=

FAILOVER

BACKUP

=

DATA RECOVERY

MULTI-AZ

=

AVAILABILITY

---

## Master Memory Trick

PRIMARY RDS

↓

SYNC

↓

STANDBY RDS

Think:

PRIMARY

=

WORK

STANDBY

=

WAIT

FAILURE

↓

STANDBY TAKES OVER

And remember:

READ REPLICA

=

READ MORE

MULTI-AZ

=

FAIL SAFELY

BACKUP

=

GO BACK IN TIME

### Final Rule

QUESTION SAYS:

MORE READ TRAFFIC

↓

READ REPLICA

QUESTION SAYS:

PRIMARY / AZ FAILURE

↓

MULTI-AZ

QUESTION SAYS:

ACCIDENTAL DELETE / RESTORE DATA

↓

BACKUP

---

## Related Notes

- [RDS Overview](<RDS Overview>)
- [RDS Storage Auto Scaling](<RDS Storage Auto Scaling>)
- [RDS Read Replicas](<RDS Read Replicas>)
- [RDS Backups](<RDS Backups>)
- [Aurora](04-Databases/Aurora.md)
- [RDS Proxy](<RDS Proxy>)
- [Application Load Balancer](<Application Load Balancer>)
- [Auto Scaling Groups](<Auto Scaling Groups>)
- [Scalability & High Availability](<Scalability & High Availability>)
- [SAA Databases Cheat Sheet](<SAA Databases Cheat Sheet>)
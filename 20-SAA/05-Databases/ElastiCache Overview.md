## What Problem Does It Solve?

Applications often repeatedly request:

THE SAME DATA

from a database.

Think:

APPLICATION

↓

DATABASE QUERY

↓

DATABASE QUERY

↓

DATABASE QUERY

↓

DATABASE QUERY

This creates:

MORE DATABASE LOAD

↓

HIGHER LATENCY

↓

MORE DATABASE CPU / I/O

ElastiCache stores frequently accessed data in:

MEMORY

so applications can retrieve it:

MUCH FASTER

without querying the primary database every time.

Think:

APPLICATION

↓

ELASTICACHE

↓

FAST RESPONSE

### Memory Trick

ELASTICACHE

=

FAST IN-MEMORY CACHE

---

## What Is ElastiCache?

ElastiCache is a:

MANAGED IN-MEMORY DATABASE / CACHE SERVICE

Think:

RDS

=

MANAGED RELATIONAL DATABASE

ElastiCache

=

MANAGED IN-MEMORY CACHE

ElastiCache provides managed:

REDIS

and:

MEMCACHED

### Memory Trick

ELASTICACHE

=

MANAGED REDIS / MEMCACHED

---

## In-Memory Database

ElastiCache stores data in:

MEMORY

or:

RAM

Think:

DISK DATABASE

↓

SLOWER

IN-MEMORY CACHE

↓

FASTER

Memory provides:

VERY HIGH PERFORMANCE

and:

LOW LATENCY

### Memory Trick

RAM

=

FAST

---

## Why Is ElastiCache Fast?

Traditional databases frequently retrieve data from:

STORAGE

ElastiCache keeps frequently accessed data in:

MEMORY

Think:

DATABASE STORAGE

↓

READ

vs:

MEMORY

↓

READ

Memory access is much faster.

### Memory Trick

CACHE

=

KEEP HOT DATA IN RAM

---

## Redis and Memcached

ElastiCache provides managed support for:

REDIS

and:

MEMCACHED

Think:

ELASTICACHE

↓

REDIS

or:

MEMCACHED

These engines have different architectures and capabilities.

We'll compare them separately in:

[Redis vs Memcached](<Redis vs Memcached>)

### Memory Trick

ELASTICACHE ENGINE?

↓

REDIS OR MEMCACHED

---

## ElastiCache Reduces Database Load

One of the main reasons to use ElastiCache is:

REDUCE DATABASE READ LOAD

Think:

WITHOUT CACHE

APPLICATION

↓

RDS

↓

RDS

↓

RDS

↓

RDS

With ElastiCache:

APPLICATION

↓

ELASTICACHE

↓

ONLY CACHE MISSES GO TO RDS

This can significantly reduce:

READ-INTENSIVE DATABASE TRAFFIC

### Memory Trick

CACHE

=

PROTECT DATABASE FROM REPEATED READS

---

## Read-Intensive Workloads

ElastiCache is especially useful when:

THE SAME DATA

is read:

AGAIN AND AGAIN

Think:

POPULAR PRODUCT

↓

100,000 USERS

↓

SAME PRODUCT INFORMATION

Instead of:

100,000 DATABASE QUERIES

use:

DATABASE

↓

CACHE DATA

↓

ELASTICACHE

↓

SERVE REPEATED READS

### Memory Trick

READ-HEAVY

=

THINK CACHE

---

## DB Cache Architecture

The SAA slides show the following caching pattern:

APPLICATION

↓

QUERY ELASTICACHE

If data exists:

CACHE HIT

↓

RETURN DATA

If data does not exist:

CACHE MISS

↓

QUERY RDS

↓

GET DATA

↓

WRITE DATA TO CACHE

↓

RETURN DATA

### Memory Trick

CHECK CACHE FIRST

↓

DB ONLY IF NEEDED

---

## Cache Hit

A:

CACHE HIT

means:

REQUESTED DATA EXISTS IN ELASTICACHE

Think:

APPLICATION

↓

ELASTICACHE

↓

DATA FOUND

↓

FAST RESPONSE

The application does not need to query:

RDS

### Memory Trick

CACHE HIT

=

FOUND IT

---

## Cache Miss

A:

CACHE MISS

means:

REQUESTED DATA IS NOT IN CACHE

Think:

APPLICATION

↓

ELASTICACHE

↓

NOT FOUND

↓

RDS

↓

READ DATA

↓

STORE IN CACHE

↓

RETURN DATA

### Memory Trick

CACHE MISS

=

GO TO DATABASE

---

## Cache Hit vs Cache Miss

### Cache Hit

DATA FOUND IN CACHE

↓

FAST

↓

DATABASE NOT QUERIED

---

### Cache Miss

DATA NOT FOUND

↓

QUERY DATABASE

↓

CACHE RESULT

↓

RETURN DATA

### Memory Trick

HIT

=

CACHE

MISS

=

DATABASE

---

## Cache Invalidation

Caching creates an important problem:

CACHED DATA CAN BECOME OLD

Suppose:

DATABASE

=

PRICE $100

Cache:

=

PRICE $100

Then database changes:

PRICE

=

$80

But the cache still contains:

$100

This is:

STALE DATA

Therefore a cache needs an:

INVALIDATION STRATEGY

### Memory Trick

CACHE

=

FAST

BUT

CAN BECOME STALE

---

## Why Cache Invalidation Matters

The SAA slides emphasize that the cache must have an:

INVALIDATION STRATEGY

to ensure applications use:

CURRENT DATA

Think:

DATABASE CHANGES

↓

CACHE MUST EVENTUALLY CHANGE

Otherwise:

APPLICATION

↓

OLD CACHE DATA

↓

INCORRECT RESPONSE

### Memory Trick

CACHE SPEED

WITHOUT INVALIDATION

=

STALE DATA RISK

---

## ElastiCache and Stateless Applications

ElastiCache can help make applications:

STATELESS

Think:

WITHOUT SHARED SESSION STORAGE

USER

↓

EC2 #1

↓

SESSION STORED LOCALLY

If next request goes to:

EC2 #2

↓

SESSION MISSING

Instead:

EC2 #1

↓

ELASTICACHE

↓

SESSION DATA

Then:

EC2 #2

↓

ELASTICACHE

↓

SAME SESSION DATA

### Memory Trick

SHARED CACHE

=

STATELESS APP SERVERS

---

## User Session Store

ElastiCache can store:

USER SESSION DATA

Think:

USER LOGS IN

↓

APPLICATION INSTANCE #1

↓

WRITE SESSION

↓

ELASTICACHE

Later:

USER REQUEST

↓

APPLICATION INSTANCE #2

↓

READ SESSION

↓

ELASTICACHE

↓

USER STILL LOGGED IN

### Memory Trick

SESSION STORE

=

ANY APP SERVER CAN FIND USER STATE

---

## Why Session Storage Helps Auto Scaling

With:

[Auto Scaling Groups](<Auto Scaling Groups>)

application instances can be:

ADDED

and:

REMOVED

If sessions are stored locally:

USER SESSION

↓

TIED TO ONE SERVER

This makes scaling harder.

If sessions are stored in:

ELASTICACHE

Think:

EC2 INSTANCES

↓

STATELESS

↓

ANY INSTANCE CAN SERVE USER

### Memory Trick

ASG + SHARED SESSION STORE

=

EASIER HORIZONTAL SCALING

---

## Session Store Architecture

Think:

USER

↓

[Application Load Balancer](<Application Load Balancer>)

↓

EC2 #1

↓

WRITE SESSION

↓

ELASTICACHE

Then:

USER

↓

ALB

↓

EC2 #3

↓

READ SESSION

↓

ELASTICACHE

The user does not need to return to:

THE SAME EC2 INSTANCE

### Memory Trick

SESSION IN CACHE

=

NO SERVER AFFINITY REQUIRED

---

## ElastiCache vs Load Balancer Stickiness

Do not confuse:

SESSION STORAGE

with:

[Load Balancer Stickiness](<Load Balancer Stickiness>)

### Stickiness

SAME USER

↓

SAME EC2 INSTANCE

---

### ElastiCache Session Store

SAME USER

↓

ANY EC2 INSTANCE

↓

SHARED SESSION DATA

Think:

STICKINESS

=

KEEP USER ON SERVER

ELASTICACHE

=

MOVE SESSION OFF SERVER

### Memory Trick

STATELESS DESIGN

=

SHARED SESSION STORE

---

## Managed Service

AWS manages much of the ElastiCache infrastructure.

Your course highlights:

OS MAINTENANCE

↓

PATCHING

↓

OPTIMIZATIONS

↓

SETUP

↓

CONFIGURATION

↓

MONITORING

↓

FAILURE RECOVERY

↓

BACKUPS

Think:

ELASTICACHE

=

MANAGED CACHE INFRASTRUCTURE

### Memory Trick

YOU USE CACHE

AWS RUNS CACHE INFRASTRUCTURE

---

## Application Changes Required

An important SAA point:

USING ELASTICACHE

usually requires:

APPLICATION CODE CHANGES

The application must understand:

WHEN TO QUERY CACHE

↓

WHEN TO QUERY DATABASE

↓

WHEN TO WRITE CACHE

↓

WHEN TO INVALIDATE CACHE

Think:

APPLICATION

↓

CACHE LOGIC

↓

DATABASE LOGIC

### Memory Trick

ELASTICACHE

=

NOT MAGIC

APP MUST USE CACHE

---

## Why Code Changes Are Needed

Without ElastiCache:

APPLICATION

↓

DATABASE

With ElastiCache:

APPLICATION

↓

CHECK CACHE

↓

IF HIT

RETURN DATA

↓

IF MISS

QUERY DATABASE

↓

WRITE CACHE

↓

RETURN DATA

The application must implement this behavior.

### Exam Trap

ADDING ELASTICACHE

≠

AUTOMATICALLY CACHE ALL DATABASE QUERIES

---

## ElastiCache vs RDS Proxy

Do not confuse:

[ElastiCache](ElastiCache)

with:

[RDS Proxy](<RDS Proxy>)

### ElastiCache

Caches:

DATA

Purpose:

REDUCE REPEATED DATABASE READS

---

### RDS Proxy

Pools:

DATABASE CONNECTIONS

Purpose:

REDUCE CONNECTION PRESSURE

Think:

SLOW / REPEATED READS?

↓

ELASTICACHE

TOO MANY CONNECTIONS?

↓

RDS PROXY

### Memory Trick

ELASTICACHE

=

DATA

RDS PROXY

=

CONNECTIONS

---

## ElastiCache vs Read Replicas

Both can reduce load on a primary database.

But they work differently.

### Read Replica

Stores:

FULL DATABASE REPLICA

Purpose:

READ SCALABILITY

Think:

READ DATABASE COPY

---

### ElastiCache

Stores:

FREQUENTLY ACCESSED DATA

in:

MEMORY

Purpose:

VERY FAST READS

Think:

HOT DATA CACHE

### Memory Trick

READ REPLICA

=

MORE DATABASE READERS

ELASTICACHE

=

FASTER REPEATED READS

---

## ElastiCache vs RDS

### RDS

PRIMARY DATABASE

↓

PERSISTENT RELATIONAL DATA

↓

SQL

---

### ElastiCache

CACHE LAYER

↓

IN-MEMORY DATA

↓

FAST ACCESS

ElastiCache usually does:

NOT REPLACE

the main relational database.

Think:

APPLICATION

↓

ELASTICACHE

↓

RDS

### Memory Trick

RDS

=

SOURCE OF TRUTH

ELASTICACHE

=

FAST COPY OF HOT DATA

---

## Source of Truth

In a common cache architecture:

RDS

is the:

SOURCE OF TRUTH

ElastiCache stores:

TEMPORARY / CACHED DATA

Think:

DATABASE

=

AUTHORITATIVE DATA

CACHE

=

FAST ACCESS COPY

### Exam Thinking

If cache data disappears:

APPLICATION SHOULD STILL BE ABLE TO GET DATA

from the underlying database.

---

## Cache-Aside Pattern Preview

The DB cache architecture shown in the slides is commonly called:

LAZY LOADING

or:

CACHE-ASIDE

Think:

APPLICATION

↓

CHECK CACHE

↓

MISS

↓

DATABASE

↓

WRITE CACHE

We'll cover caching strategies separately.

See:

[ElastiCache Caching Strategies](<ElastiCache Caching Strategies>)

---

## Lazy Loading Preview

With Lazy Loading:

ONLY REQUESTED DATA

is placed into the cache.

Think:

CACHE MISS

↓

READ DATABASE

↓

WRITE CACHE

Potential issue:

STALE DATA

### Memory Trick

LAZY

=

CACHE WHEN REQUESTED

---

## Write Through Preview

Another caching strategy is:

WRITE THROUGH

Think:

DATABASE WRITE

↓

UPDATE CACHE TOO

This helps reduce:

STALE CACHE DATA

We'll cover this separately in:

[ElastiCache Caching Strategies](<ElastiCache Caching Strategies>)

---

## Session Store Preview

Another caching pattern is:

SESSION STORE

Think:

LOGIN SESSION

↓

ELASTICACHE

Session data is usually:

TEMPORARY

and often uses:

TTL

or:

TIME TO LIVE

### Memory Trick

SESSION

=

TEMPORARY STATE

---

## TTL

TTL stands for:

TIME TO LIVE

TTL controls:

HOW LONG CACHE DATA EXISTS

Think:

CACHE ITEM

↓

TTL EXPIRES

↓

ITEM REMOVED

This is useful for:

TEMPORARY SESSION DATA

### Memory Trick

TTL

=

CACHE EXPIRATION TIMER

---

## High-Level Architecture

A scalable web application can look like:

USERS

↓

[Application Load Balancer](<Application Load Balancer>)

↓

[Auto Scaling Groups](<Auto Scaling Groups>)

↓

EC2 APPLICATION INSTANCES

↓

ELASTICACHE

↓

RDS

Think:

ALB

=

DISTRIBUTE

ASG

=

SCALE APP SERVERS

ELASTICACHE

=

FAST CACHE / SESSION STORE

RDS

=

PERSISTENT DATABASE

---

## Read Architecture

Application needs data:

APPLICATION

↓

ELASTICACHE

Cache Hit?

YES

↓

RETURN FAST

NO

↓

RDS

↓

GET DATA

↓

STORE IN ELASTICACHE

↓

RETURN

Think:

CACHE FIRST

↓

DATABASE SECOND

---

## Session Architecture

User logs in:

USER

↓

APPLICATION #1

↓

SESSION

↓

ELASTICACHE

Next request:

USER

↓

APPLICATION #2

↓

ELASTICACHE

↓

SESSION FOUND

Think:

SESSION OUTSIDE EC2

↓

EC2 BECOMES STATELESS

---

## Scenario Recognition

Need an AWS-managed Redis cache?

→ ElastiCache

---

Need an AWS-managed Memcached cache?

→ ElastiCache

---

Need very low-latency in-memory access?

→ ElastiCache

---

Need to reduce read load on RDS?

→ ElastiCache

---

Need to cache frequently accessed database data?

→ ElastiCache

---

Need repeated reads to become much faster?

→ ElastiCache

---

Need application servers to become stateless?

→ ElastiCache Session Store

---

Need session data shared across EC2 instances?

→ ElastiCache

---

Need any application server to retrieve user session state?

→ ElastiCache

---

Need database connection pooling?

→ RDS Proxy

NOT ElastiCache

---

Need full database read copies?

→ RDS Read Replicas

NOT ElastiCache

---

Need cache data expiration?

→ TTL

---

Need cache consistency with database updates?

→ Cache Invalidation Strategy

---

Need caching with no application code changes?

→ ElastiCache may NOT be ideal

because:

APPLICATION MUST USE CACHE LOGIC

---

## Exam Traps

ELASTICACHE

=

MANAGED REDIS / MEMCACHED

---

ELASTICACHE

=

IN-MEMORY

---

IN-MEMORY

=

HIGH PERFORMANCE + LOW LATENCY

---

ELASTICACHE

=

REDUCE DATABASE READ LOAD

---

CACHE HIT

=

DATA FOUND IN CACHE

---

CACHE MISS

=

QUERY DATABASE

---

CACHE

=

CAN BECOME STALE

---

CACHE INVALIDATION

=

KEEP DATA CURRENT

---

ELASTICACHE

=

CAN STORE SESSION DATA

---

SESSION STORE

=

HELPS MAKE APP SERVERS STATELESS

---

ELASTICACHE

≠

RDS PROXY

---

ELASTICACHE

=

CACHE DATA

RDS PROXY

=

POOL CONNECTIONS

---

ELASTICACHE

≠

READ REPLICA

---

READ REPLICA

=

DATABASE READ SCALING

ELASTICACHE

=

FAST REPEATED READ ACCESS

---

USING ELASTICACHE

=

APPLICATION CODE CHANGES REQUIRED

---

RDS

=

SOURCE OF TRUTH

ELASTICACHE

=

CACHE LAYER

---

## Quick Cheat Sheet

ELASTICACHE

=

MANAGED CACHE SERVICE

ENGINES

=

REDIS + MEMCACHED

STORAGE

=

MEMORY

PERFORMANCE

=

HIGH

LATENCY

=

LOW

MAIN BENEFIT

=

REDUCE DATABASE READ LOAD

CACHE HIT

=

DATA FOUND

CACHE MISS

=

QUERY DATABASE

CACHE INVALIDATION

=

PREVENT STALE DATA

SESSION STORE

=

SHARED USER STATE

STATELESS APPS

=

ELASTICACHE CAN HELP

TTL

=

CACHE EXPIRATION

AWS MANAGES

=

PATCHING

SETUP

MONITORING

FAILURE RECOVERY

BACKUPS

APPLICATION CODE CHANGES

=

YES

RDS PROXY

=

CONNECTION POOL

ELASTICACHE

=

DATA CACHE

READ REPLICA

=

READ DATABASE COPY

ELASTICACHE

=

HOT DATA IN MEMORY

---

## Master Memory Trick

APPLICATION

↓

CHECK ELASTICACHE

↓

HIT?

↓

RETURN FAST

MISS?

↓

QUERY RDS

↓

STORE RESULT IN CACHE

↓

RETURN

Think:

ELASTICACHE

=

FAST MEMORY LAYER

And:

RDS

=

SOURCE OF TRUTH

ELASTICACHE

=

HOT DATA

RDS PROXY

=

DB CONNECTIONS

READ REPLICA

=

READ SCALE

### Final Rule

QUESTION SAYS:

REPEATED READS

+

LOW LATENCY

+

REDUCE DATABASE LOAD

↓

ELASTICACHE

QUESTION SAYS:

SHARED USER SESSION

+

STATELESS EC2

↓

ELASTICACHE

QUESTION SAYS:

TOO MANY DATABASE CONNECTIONS

↓

RDS PROXY

---

## Related Notes

- [Redis vs Memcached](<Redis vs Memcached>)
- [ElastiCache Caching Strategies](<ElastiCache Caching Strategies>)
- [RDS Overview](<RDS Overview>)
- [RDS Read Replicas](<RDS Read Replicas>)
- [RDS Proxy](<RDS Proxy>)
- [Aurora](Aurora)
- [Application Load Balancer](<Application Load Balancer>)
- [Auto Scaling Groups](<Auto Scaling Groups>)
- [Load Balancer Stickiness](<Load Balancer Stickiness>)
- [SAA Databases Cheat Sheet](<SAA Databases Cheat Sheet>)
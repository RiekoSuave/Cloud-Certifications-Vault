## What Problem Does It Solve?

ElastiCache supports two major cache engines:

REDIS

and:

MEMCACHED

Both provide:

FAST

↓

IN-MEMORY

↓

LOW-LATENCY

data access.

But they are designed differently.

Think:

NEED HIGH AVAILABILITY / REPLICATION?

↓

REDIS

Need:

SIMPLE DISTRIBUTED CACHE + MULTITHREADING?

↓

MEMCACHED

### Memory Trick

REDIS

=

FEATURE-RICH

MEMCACHED

=

SIMPLE DISTRIBUTED CACHE

---

## Redis Overview

Redis supports:

MULTI-AZ

↓

AUTO FAILOVER

↓

READ REPLICAS

↓

PERSISTENCE

↓

BACKUP / RESTORE

↓

ADVANCED DATA STRUCTURES

Think:

REDIS

=

MORE DATABASE-LIKE FEATURES

### Memory Trick

REDIS

=

HA + REPLICATION + PERSISTENCE

---

## Memcached Overview

Memcached focuses on:

SIMPLE IN-MEMORY CACHING

with:

MULTIPLE NODES

↓

SHARDING

↓

MULTITHREADED ARCHITECTURE

Think:

MEMCACHED

=

SCALE CACHE HORIZONTALLY

### Memory Trick

MEMCACHED

=

SHARD + THREAD

---

## Redis Multi-AZ

Redis supports:

MULTI-AZ

with:

AUTO FAILOVER

Think:

AZ-A

↓

REDIS PRIMARY

AZ-B

↓

REDIS REPLICA

If the primary fails:

↓

AUTO FAILOVER

↓

REPLICA TAKES OVER

### Memory Trick

REDIS

=

MULTI-AZ HA

---

## Redis Auto Failover

Redis can automatically recover from:

PRIMARY NODE FAILURE

Think:

PRIMARY

↓

FAILS

↓

REPLICA

↓

PROMOTED

This improves:

HIGH AVAILABILITY

### Memory Trick

REDIS FAILURE

=

PROMOTE REPLICA

---

## Redis Read Replicas

Redis supports:

READ REPLICAS

Think:

PRIMARY

↓

REPLICATION

↓

READ REPLICA #1

READ REPLICA #2

Read Replicas help:

SCALE READS

and:

IMPROVE HIGH AVAILABILITY

### Memory Trick

REDIS READ REPLICA

=

READ SCALE

---

## Redis Replication

Redis can replicate data from:

PRIMARY

to:

REPLICAS

Think:

WRITE

↓

PRIMARY

↓

REPLICATE

↓

READERS

This is one major difference from:

MEMCACHED

### Memory Trick

REDIS

=

REPLICATION

MEMCACHED

=

NO REPLICATION HA

---

## Redis Data Durability

Redis supports:

AOF PERSISTENCE

AOF stands for:

APPEND ONLY FILE

Think:

REDIS WRITE

↓

APPEND OPERATION TO FILE

↓

DATA CAN BE RECOVERED

This provides greater:

DATA DURABILITY

than a purely non-persistent cache.

### Memory Trick

REDIS AOF

=

PERSIST DATA

---

## Redis Backup and Restore

Redis supports:

BACKUP

and:

RESTORE

features.

Think:

REDIS DATA

↓

BACKUP

↓

RESTORE LATER

This makes Redis appropriate when the cache data has:

MORE IMPORTANCE

than a purely disposable cache.

### Memory Trick

REDIS

=

CAN BACK UP CACHE DATA

---

## Redis Data Structures

Redis supports advanced data structures including:

SETS

and:

SORTED SETS

Think:

DATA

↓

UNIQUE ELEMENTS

↓

ORDERING / RANKING

This makes Redis useful for workloads beyond:

SIMPLE KEY-VALUE CACHE

### Memory Trick

REDIS

=

SMART DATA STRUCTURES

---

## Redis Sorted Sets

A particularly important SAA use case is:

SORTED SETS

Sorted Sets provide:

UNIQUENESS

and:

ORDERING

Think:

PLAYER

↓

SCORE

↓

RANK

Redis automatically keeps elements:

SORTED

### Memory Trick

SORTED SET

=

UNIQUE + RANKED

---

## Gaming Leaderboards

The SAA slides specifically highlight:

GAMING LEADERBOARDS

as a Redis use case.

Think:

PLAYER A

↓

100 POINTS

PLAYER B

↓

250 POINTS

PLAYER C

↓

175 POINTS

Redis Sorted Sets:

↓

RANK AUTOMATICALLY

Result:

1. PLAYER B

2. PLAYER C

3. PLAYER A

### Memory Trick

REAL-TIME LEADERBOARD

=

REDIS SORTED SET

---

## Memcached Sharding

Memcached supports:

MULTIPLE NODES

for:

DATA PARTITIONING

or:

SHARDING

Think:

CACHE DATA

↓

NODE #1

NODE #2

NODE #3

Different cache items are stored across:

DIFFERENT NODES

### Memory Trick

MEMCACHED

=

SHARD ACROSS NODES

---

## What Is Sharding?

Sharding means:

SPLITTING DATA

across:

MULTIPLE NODES

Think:

CACHE KEYS A-F

↓

NODE #1

CACHE KEYS G-M

↓

NODE #2

CACHE KEYS N-Z

↓

NODE #3

The goal is:

HORIZONTAL CACHE SCALING

### Memory Trick

SHARDING

=

SPLIT DATA

---

## Memcached Multi-Node Architecture

Think:

APPLICATION

↓

MEMCACHED CLUSTER

↓

NODE #1

NODE #2

NODE #3

The data is:

PARTITIONED

across nodes.

This differs from Redis Read Replicas, where data is:

REPLICATED

### Memory Trick

MEMCACHED

=

PARTITION

REDIS

=

REPLICATE

---

## Memcached Has No High Availability Replication

Your course emphasizes:

MEMCACHED

does not provide:

HIGH AVAILABILITY THROUGH REPLICATION

Think:

NODE FAILS

↓

CACHED DATA ON NODE MAY BE LOST

There is no Redis-style:

PRIMARY

↓

REPLICA

↓

AUTO FAILOVER

architecture.

### Memory Trick

MEMCACHED

=

NO REPLICA HA

---

## Memcached Is Non-Persistent

Memcached is:

NON-PERSISTENT

Think:

CACHE DATA

↓

MEMORY ONLY

↓

NODE LOST

↓

DATA CAN DISAPPEAR

This is often acceptable because cached data can usually be:

RECREATED

from the source database.

### Memory Trick

MEMCACHED

=

DISPOSABLE CACHE

---

## Memcached and Source of Truth

A common architecture is:

RDS

=

SOURCE OF TRUTH

MEMCACHED

=

TEMPORARY CACHE

If Memcached loses data:

APPLICATION

↓

CACHE MISS

↓

RDS

↓

GET DATA AGAIN

↓

REPOPULATE CACHE

### Memory Trick

MEMCACHED DATA LOST?

↓

REBUILD FROM DATABASE

---

## Memcached Backup and Restore

The SAA slides note:

BACKUP AND RESTORE

for:

MEMCACHED SERVERLESS

Think:

MEMCACHED SERVERLESS

↓

BACKUP / RESTORE CAPABILITY

### Exam Thinking

Do not memorize the older blanket statement:

MEMCACHED NEVER SUPPORTS BACKUPS

The course specifically notes:

BACKUP / RESTORE

for:

SERVERLESS

---

## Memcached Multi-Threaded Architecture

Memcached uses a:

MULTI-THREADED ARCHITECTURE

Think:

ONE CACHE NODE

↓

MULTIPLE CPU THREADS

↓

PROCESS MANY OPERATIONS

### Memory Trick

MEMCACHED

=

MULTI-THREADED

---

## Redis vs Memcached Architecture

### Redis

PRIMARY

↓

READ REPLICAS

↓

MULTI-AZ

↓

AUTO FAILOVER

Think:

REPLICATION

---

### Memcached

NODE #1

NODE #2

NODE #3

Think:

SHARDING

### Memory Trick

REDIS

=

COPY DATA

MEMCACHED

=

SPLIT DATA

---

## Replication vs Sharding

Do not confuse:

REPLICATION

with:

SHARDING

### Replication

SAME DATA

↓

MULTIPLE NODES

Purpose:

HIGH AVAILABILITY

and:

READ SCALING

Think:

REDIS

---

### Sharding

DIFFERENT DATA

↓

DIFFERENT NODES

Purpose:

DISTRIBUTE DATA / CAPACITY

Think:

MEMCACHED

### Memory Trick

REPLICATION

=

COPY

SHARDING

=

SPLIT

---

## Redis High Availability

Need:

CACHE HIGH AVAILABILITY

Think:

REDIS

because it supports:

MULTI-AZ

↓

READ REPLICAS

↓

AUTO FAILOVER

### Memory Trick

HIGH AVAILABILITY CACHE

=

REDIS

---

## Memcached Scaling

Need:

SIMPLE CACHE

distributed across many nodes?

Think:

MEMCACHED

↓

MULTI-NODE SHARDING

### Memory Trick

SCALE OUT SIMPLE CACHE

=

MEMCACHED

---

## Redis Persistence vs Memcached

### Redis

CAN BE PERSISTENT

using:

AOF

Think:

DATA DURABILITY

---

### Memcached

NON-PERSISTENT

Think:

TEMPORARY CACHE

### Memory Trick

REDIS

=

REMEMBERS

MEMCACHED

=

FORGETS

---

## Redis vs Memcached Data Structures

### Redis

Supports richer data structures such as:

SETS

↓

SORTED SETS

This enables use cases like:

LEADERBOARDS

---

### Memcached

Primarily optimized for:

SIMPLE CACHE VALUES

Think:

KEY

↓

VALUE

### Memory Trick

COMPLEX CACHE DATA?

↓

REDIS

SIMPLE CACHE?

↓

MEMCACHED

---

## Redis vs Memcached Failure Thinking

### Redis

NODE FAILURE

↓

REPLICA AVAILABLE

↓

AUTO FAILOVER

---

### Memcached

NODE FAILURE

↓

CACHE DATA MAY BE LOST

↓

APPLICATION REBUILDS CACHE

Think:

REDIS

=

RESILIENT CACHE

MEMCACHED

=

DISPOSABLE CACHE

---

## Redis vs Memcached Decision Tree

Need:

MULTI-AZ?

↓

REDIS

---

Need:

AUTO FAILOVER?

↓

REDIS

---

Need:

READ REPLICAS?

↓

REDIS

---

Need:

DATA PERSISTENCE?

↓

REDIS

---

Need:

SETS / SORTED SETS?

↓

REDIS

---

Need:

REAL-TIME LEADERBOARD?

↓

REDIS

---

Need:

MULTI-NODE SHARDING?

↓

MEMCACHED

---

Need:

MULTI-THREADED CACHE ENGINE?

↓

MEMCACHED

---

Need:

SIMPLE NON-PERSISTENT CACHE?

↓

MEMCACHED

---

## Redis + Session Store

Redis can be a strong choice for:

SESSION STORAGE

Think:

USER SESSION

↓

REDIS

↓

ANY APP SERVER

Because Redis can provide:

HIGH AVAILABILITY

for shared session state.

### Memory Trick

IMPORTANT SESSION STATE

↓

REDIS

---

## Memcached + Simple Cache

Memcached can be ideal when the cache contains:

TEMPORARY

↓

EASILY RECREATED

↓

SIMPLE KEY-VALUE DATA

Think:

CACHE LOST?

↓

NO BIG DEAL

↓

RELOAD FROM DATABASE

### Memory Trick

THROWAWAY CACHE

=

MEMCACHED

---

## Architecture Thinking

### Redis Architecture

APPLICATION

↓

REDIS PRIMARY

↓

REPLICATION

↓

READ REPLICAS

across:

MULTIPLE AZs

If:

PRIMARY FAILS

↓

AUTO FAILOVER

---

### Memcached Architecture

APPLICATION

↓

MEMCACHED NODES

↓

SHARD #1

SHARD #2

SHARD #3

Data is:

DISTRIBUTED

rather than replicated for HA.

---

## Redis vs RDS Read Replicas

Do not confuse:

REDIS READ REPLICAS

with:

RDS READ REPLICAS

Both can:

SCALE READS

But:

REDIS

=

IN-MEMORY CACHE

RDS

=

RELATIONAL DATABASE

Think:

FAST CACHED DATA

↓

REDIS

RELATIONAL SQL DATA

↓

RDS

---

## Scenario Recognition

Need ElastiCache Multi-AZ?

→ Redis

---

Need cache Auto Failover?

→ Redis

---

Need cache Read Replicas?

→ Redis

---

Need persistent ElastiCache data?

→ Redis

---

Need AOF persistence?

→ Redis

---

Need backup and restore with Redis?

→ Redis

---

Need Sets or Sorted Sets?

→ Redis

---

Need real-time gaming leaderboard?

→ Redis

---

Need uniqueness + ranking?

→ Redis Sorted Sets

---

Need data partitioned across multiple cache nodes?

→ Memcached

---

Need cache sharding?

→ Memcached

---

Need multi-threaded cache architecture?

→ Memcached

---

Need simple non-persistent distributed cache?

→ Memcached

---

Need high availability through replication?

→ Redis

NOT Memcached

---

## Exam Traps

REDIS

=

MULTI-AZ

---

REDIS

=

AUTO FAILOVER

---

REDIS

=

READ REPLICAS

---

REDIS

=

AOF PERSISTENCE

---

REDIS

=

BACKUP / RESTORE

---

REDIS

=

SETS + SORTED SETS

---

REDIS SORTED SET

=

REAL-TIME LEADERBOARD

---

MEMCACHED

=

MULTI-NODE

---

MEMCACHED

=

SHARDING

---

MEMCACHED

=

NO HA REPLICATION

---

MEMCACHED

=

NON-PERSISTENT

---

MEMCACHED

=

MULTI-THREADED

---

REDIS

=

REPLICATION

MEMCACHED

=

SHARDING

---

REDIS

=

FEATURE-RICH

MEMCACHED

=

SIMPLE CACHE

---

## Quick Cheat Sheet

REDIS MULTI-AZ

=

YES

REDIS AUTO FAILOVER

=

YES

REDIS READ REPLICAS

=

YES

REDIS PERSISTENCE

=

AOF

REDIS BACKUP / RESTORE

=

YES

REDIS SETS

=

YES

REDIS SORTED SETS

=

YES

REDIS LEADERBOARDS

=

YES

MEMCACHED MULTI-NODE

=

YES

MEMCACHED SHARDING

=

YES

MEMCACHED HA REPLICATION

=

NO

MEMCACHED PERSISTENCE

=

NO

MEMCACHED MULTI-THREADED

=

YES

REPLICATION

=

REDIS

SHARDING

=

MEMCACHED

---

## Master Memory Trick

REDIS

=

RICH

Think:

R

=

REPLICAS

E

=

EXTRA FEATURES

D

=

DURABILITY

I

=

IN-MEMORY

S

=

SORTED SETS

And:

MEMCACHED

=

SIMPLE SCALE-OUT CACHE

Think:

MULTI-NODE

↓

SHARD DATA

↓

MULTI-THREADED

↓

NON-PERSISTENT

### Final Rule

QUESTION SAYS:

HIGH AVAILABILITY

↓

REDIS

QUESTION SAYS:

FAILOVER

↓

REDIS

QUESTION SAYS:

PERSISTENCE

↓

REDIS

QUESTION SAYS:

LEADERBOARD

↓

REDIS

QUESTION SAYS:

SHARDING

↓

MEMCACHED

QUESTION SAYS:

MULTI-THREADED

↓

MEMCACHED

---

## Related Notes

- [ElastiCache Overview](<ElastiCache Overview>)
- [ElastiCache Caching Strategies](<ElastiCache Caching Strategies>)
- [RDS Overview](<RDS Overview>)
- [RDS Read Replicas](<RDS Read Replicas>)
- [RDS Proxy](<RDS Proxy>)
- [Auto Scaling Groups](<Auto Scaling Groups>)
- [SAA Databases Cheat Sheet](<SAA Databases Cheat Sheet>)
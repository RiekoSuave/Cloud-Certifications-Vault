See also: [[Database Fundamentals]]

See also: [[RDS]]

See also: [[04-Databases/Aurora]]

See also: [[04-Databases/DynamoDB]]

## What Problem Does It Solve?

Improves application and database performance by storing frequently accessed data in memory.

Instead of repeatedly retrieving the same data from a database, an application can retrieve frequently used data from ElastiCache.

### Memory Trick

ElastiCache = Speed

---

## Type

Managed In-Memory Cache

---

## What Is ElastiCache?

ElastiCache is a managed AWS service for in-memory caching.

It helps reduce the amount of work performed by a database by caching frequently accessed data.

Basic Idea:

Application

↓

ElastiCache

↓

Database

Frequently requested data can be retrieved from the cache instead of repeatedly querying the database.

---

## Why Use In-Memory Caching?

Memory is much faster to access than traditional database storage.

Caching frequently requested data can:

- Improve application performance
- Reduce database load
- Reduce database queries
- Provide faster responses

### Memory Trick

Cache = Keep Frequently Used Data Close

---

## Supported Technologies

Your course identifies two technologies:

- Redis
- Memcached

These are commonly used as in-memory caching technologies.

---

## Redis

Redis is one of the technologies supported by ElastiCache.

Think:

ElastiCache for Redis

→ Managed Redis caching

---

## Memcached

Memcached is another technology supported by ElastiCache.

Think:

ElastiCache for Memcached

→ Managed Memcached caching

---

## Basic Caching Concept

Without Cache:

Application

↓

Database

↓

Retrieve Data

Every request may need to reach the database.

---

With ElastiCache:

Application

↓

ElastiCache

↓

Database

Frequently requested data can be returned from memory.

---

## Cache Hit

If the requested data already exists in the cache:

Application

↓

ElastiCache

↓

Data Returned Quickly

The database may not need to be queried.

---

## Cache Miss

If the requested data is not currently cached:

Application

↓

ElastiCache

↓

Database

↓

Retrieve Data

The data can then be cached for future requests.

### Memory Trick

Cache Hit = Found in Cache

Cache Miss = Go to Database

---

## ElastiCache and Database Performance

Imagine thousands of users repeatedly requesting the same information.

Without caching:

Database gets queried repeatedly.

With caching:

Frequently requested information can be served from memory.

This reduces pressure on the underlying database.

---

## ElastiCache vs DAX

This distinction is important.

### DAX

DynamoDB Accelerator

Designed specifically for:

[[04-Databases/DynamoDB]]

### ElastiCache

Provides caching that can be used with other database workloads.

| DAX | ElastiCache |
|---|---|
| DynamoDB-specific | General caching service |
| Integrated with DynamoDB | Redis / Memcached |
| In-memory | In-memory |
| Accelerates DynamoDB | Accelerates applications/databases |

### Memory Trick

DAX = DynamoDB Cache

ElastiCache = General Cache

---

## ElastiCache vs DynamoDB

### DynamoDB

Stores application data as a NoSQL database.

### ElastiCache

Caches frequently accessed data in memory.

| DynamoDB | ElastiCache |
|---|---|
| NoSQL database | In-memory cache |
| Stores application data | Caches frequently used data |
| Persistent database service | Performance optimization |
| Key-value database | Redis / Memcached |

### Memory Trick

DynamoDB = Store Data

ElastiCache = Speed Up Data Access

---

## ElastiCache vs RDS

### RDS

Managed relational SQL database.

### ElastiCache

In-memory caching service.

ElastiCache can help reduce repeated database queries by caching frequently accessed information.

Basic Idea:

Application

↓

ElastiCache

↓

RDS

See:

[[RDS]]

---

## ElastiCache vs Aurora

The same general concept applies to:

[[04-Databases/Aurora]]

Aurora stores relational application data.

ElastiCache can cache frequently accessed data to improve application performance and reduce repeated database queries.

---

## Common Use Cases

- Frequently accessed data
- Database query caching
- Improving application response times
- Reducing database load
- Performance optimization

---

## Exam Scenarios

A database is receiving the same queries repeatedly and application performance needs to improve.

→ ElastiCache

---

An application needs frequently requested data served from memory.

→ ElastiCache

---

A company wants a managed Redis caching solution.

→ ElastiCache

---

A company wants a managed Memcached caching solution.

→ ElastiCache

---

A DynamoDB application specifically needs an integrated in-memory accelerator.

→ DAX

---

A relational application needs a database to permanently store structured SQL data.

→ RDS or Aurora

NOT ElastiCache

---

## Don't Confuse These

### RDS

Relational SQL database

### DynamoDB

NoSQL database

### ElastiCache

In-memory cache

### DAX

DynamoDB-specific cache

---

## Exam Keywords

Cache

In-memory

Redis

Memcached

Performance

Frequently accessed data

Reduce database load

DAX

---

## Memory Tricks

ElastiCache = Speed

ElastiCache = In-Memory

Redis + Memcached = ElastiCache

Cache Hit = Found in Cache

Cache Miss = Go to Database

DAX = DynamoDB Only

ElastiCache = General Cache
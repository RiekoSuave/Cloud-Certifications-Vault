## Core Concept

Caching stores frequently accessed data:

**Closer to where it is needed**

so the system does not repeatedly retrieve or recompute:

**The same information**

Caching can improve:

- Performance
- Latency
- Scalability
- Backend capacity
- Cost efficiency

> [!tip] Memory Trick
> **Cache = Don't Fetch It Again If You Already Have It**

---

# Why Use Caching?

Without caching:

User  
↓  
Application  
↓  
Database  
↓  
Retrieve Same Data Again

With caching:

User  
↓  
Application  
↓  
Cache  
↓  
Fast Response

Only when the cache misses:

Application  
↓  
Database

### Killer Exam Clue

> **Application repeatedly reads the same data and database load is too high**
>
> → **Use caching**

---

# Cache Hit

A:

**Cache Hit**

occurs when requested data is:

**Already in the cache**

Architecture:

Request  
↓  
Cache  
↓  
Data Found  
↓  
Response

### Result

- Faster response
- Less backend load
- Lower latency

### Memory Trick

**Hit = Cache Had It**

---

# Cache Miss

A:

**Cache Miss**

occurs when requested data is:

**Not in the cache**

Architecture:

Request  
↓  
Cache  
↓  
Not Found  
↓  
Backend  
↓  
Retrieve Data  
↓  
Populate Cache  
↓  
Response

### Memory Trick

**Miss = Go to Source**

---

# Cache Hit Ratio

The:

**Cache Hit Ratio**

measures how often requests are served by:

**The cache**

Higher hit ratio generally means:

**More requests avoid the backend**

### Exam Principle

> **Caching is most effective when workloads repeatedly request the same data**

---

# Where Can Caching Happen?

Caching can occur at multiple layers:

- Edge
- API
- Application
- Database/query layer
- Browser/client

For SAA, important AWS caching services include:

- [[CloudFront]]
- [[ElastiCache]]
- API Gateway caching
- DynamoDB DAX

---

# CloudFront

[[CloudFront]] provides:

**Edge caching**

Content is cached at:

**AWS edge locations**

closer to users.

Architecture:

User  
↓  
CloudFront Edge  
↓  
Origin

Possible origins:

- S3
- ALB
- EC2
- API endpoints

### Killer Exam Clue

> **Global users repeatedly request the same static or cacheable content**
>
> → **CloudFront**

### Memory Trick

**CloudFront = Cache Near the User**

---

# CloudFront Cache Hit

If an object exists at the edge:

User  
↓  
CloudFront  
↓  
Cached Object  
↓  
Response

The request does not need to travel back to:

**The origin**

### Benefits

- Lower latency
- Reduced origin load
- Reduced repeated data transfer from origin

---

# CloudFront Cache Miss

If the object is not cached:

User  
↓  
CloudFront  
↓  
Origin  
↓  
Retrieve Object  
↓  
Cache at Edge  
↓  
Return to User

Future requests may receive:

**The cached copy**

---

# CloudFront TTL

A:

**Time to Live — TTL**

determines how long content may remain:

**Cached**

before CloudFront needs to:

**Refresh or revalidate it**

### Memory Trick

**TTL = How Long Cache Trusts the Copy**

---

# Long TTL

Long TTL works well for:

**Content that rarely changes**

Examples:

- Images
- Videos
- Versioned JavaScript
- CSS

Benefits:

- Higher cache hit ratio
- Lower origin load

---

# Short TTL

Short TTL may be better when:

**Content changes frequently**

but it can cause:

**More origin requests**

### Exam Principle

> **Cache duration should match how frequently data changes**

---

# Cache Invalidation

CloudFront invalidation forces cached objects to:

**Be removed before their normal expiration**

Example:

Old Website Asset  
↓  
CloudFront Cache

Application deploys:

New Asset

Need immediate change:

**Invalidate cached object**

### Killer Exam Clue

> **Updated content must replace cached CloudFront content immediately**
>
> → **Cache Invalidation**

---

# Versioned Objects

Instead of repeatedly invalidating objects, applications can use:

**Versioned filenames**

Example:

`app-v1.js`

becomes:

`app-v2.js`

CloudFront treats this as:

**A new object**

### Exam Principle

> **Versioning cached assets can simplify deployments**

---

# CloudFront vs ElastiCache

This distinction is critical.

## CloudFront

Think:

**Edge cache for users**

Commonly caches:

- Static content
- HTTP responses
- Web assets

## [[ElastiCache]]

Think:

**Application/database cache**

Commonly caches:

- Database results
- Sessions
- Frequently accessed application data

### Killer Shortcut

**Global web content**
→ CloudFront

**Database/application data**
→ ElastiCache

---

# ElastiCache

[[ElastiCache]] provides:

**Managed in-memory caching**

It supports engines such as:

- Redis/Valkey-style workloads
- Memcached depending on service capabilities

For SAA, focus on:

**Fast application-side caching**

### Killer Exam Clue

> **Repeated database reads are causing high latency and database load**
>
> → **ElastiCache**

---

# In-Memory Performance

ElastiCache stores data primarily in:

**Memory**

rather than slower persistent storage.

This provides:

**Very low-latency access**

### Memory Trick

**RAM = Fast**

---

# Cache-Aside Pattern

One common architecture is:

**Cache-Aside**

Flow:

Application  
↓  
Check Cache

If found:

→ Return Data

If not found:

Application  
↓  
Database  
↓  
Retrieve Data  
↓  
Write Data to Cache  
↓  
Return Response

### Memory Trick

**Check Cache First**

---

# Cache-Aside Steps

1. Application requests data
2. Check cache
3. Cache miss
4. Query database
5. Put result in cache
6. Return result

Future requests:

**Hit cache**

---

# Cache-Aside Advantage

The cache contains:

**Only data that is actually requested**

This can be efficient for:

**Read-heavy workloads**

---

# Cache-Aside Problem

Cached data can become:

**Stale**

if the underlying database changes but:

**The cached value does not**

### Exam Principle

> **Caching introduces consistency tradeoffs**

---

# Stale Data

Suppose:

Database:

Price = 100

Cache:

Price = 100

Database changes:

Price = 80

Cache still contains:

100

until:

- TTL expires
- Cache is updated
- Cache is invalidated

### Memory Trick

**Fast Data Can Be Old Data**

---

# Write-Through Caching

In a:

**Write-Through**

pattern, data is written to:

**The cache**

when it is written to:

**The backend store**

This helps keep:

**Frequently used cached data current**

### Concept

Application  
↓  
Write Cache  
↓  
Write Database

or coordinated writes depending on implementation.

### Exam Principle

> **Write-through can reduce cache misses after writes but introduces extra write work**

---

# Lazy Loading

Another common term for cache-aside behavior is:

**Lazy Loading**

Data enters the cache:

**Only when requested**

### Killer Shortcut

**Load into cache only when needed**
→ Lazy Loading / Cache-Aside

---

# Session Caching

ElastiCache can hold:

**Shared user-session data**

Architecture:

ALB  
↓  
Stateless EC2 Fleet  
↓  
ElastiCache

This allows any EC2 instance to:

**Retrieve the user's session**

### Killer Exam Clue

> **Need shared low-latency session storage for Auto Scaling instances**
>
> → **ElastiCache**

---

# ElastiCache and Stateless Architecture

By moving sessions out of:

**Local EC2 memory**

application servers become more:

**Stateless**

This improves:

- Scaling
- Replacement
- Multi-AZ design

### Memory Trick

**Move State Out → Scale Compute Better**

---

# DAX

DynamoDB Accelerator — DAX — provides:

**In-memory acceleration for DynamoDB**

Architecture:

Application  
↓  
DAX  
↓  
[[DynamoDB]]

### Killer Exam Clue

> **DynamoDB application needs microsecond-style read performance for repeated reads**
>
> → **DAX**

---

# DAX vs ElastiCache

## DAX

Purpose-built for:

**DynamoDB**

## ElastiCache

General-purpose application cache for:

**Many data sources**

### Killer Shortcut

**DynamoDB cache**
→ DAX

**RDS/application cache**
→ ElastiCache

---

# DAX Is Not for Every DynamoDB Workload

DAX is most useful when:

**Repeated reads**

benefit from caching.

If every request is:

**Unique**

the cache hit ratio may be poor.

### Exam Principle

> **Caching only helps when access patterns are cache-friendly**

---

# API Gateway Caching

[[API Gateway]] can cache:

**API responses**

This can reduce calls to:

**Backend integrations**

Architecture:

Client  
↓  
API Gateway Cache  
↓  
Backend only on cache miss

### Killer Exam Clue

> **Reduce repeated calls from API Gateway to backend for identical requests**
>
> → **API Gateway Caching**

---

# API Cache Benefits

- Lower backend load
- Faster response
- Lower repeated compute/database usage

This can be useful when:

**Responses are safe to cache**

---

# Caching Dynamic Content

Dynamic content can sometimes be cached if:

**The response remains valid for a defined period**

The key is:

**Correct cache key + TTL**

### Exam Principle

> **Dynamic does not automatically mean uncacheable**

---

# Cache Key

A:

**Cache Key**

determines whether two requests are considered:

**The same cached request**

Possible inputs include:

- URL path
- Query strings
- Headers
- Cookies

### Killer Exam Concept

> **Incorrect cache-key design can return the wrong cached response**

---

# Personalized Content

Be careful caching:

**User-specific data**

If cache keys do not separate users correctly:

One user could receive:

**Another user's cached response**

### Exam Principle

> **Personalized caching requires careful cache-key design**

---

# Database Read Replicas vs Cache

These solve similar but different problems.

## Read Replica

Provides:

**Additional database read capacity**

Requests still reach:

**The database**

## Cache

May prevent requests from reaching:

**The database at all**

### Killer Shortcut

**Need more database read capacity**
→ Read Replica

**Repeated identical reads**
→ Cache

---

# Cache + Read Replica

These can be used:

**Together**

Architecture:

Application  
↓  
Cache  
↓  
Read Replica  
↓  
Primary Database

This can significantly reduce:

**Primary database load**

---

# Cache vs Scaling Database Vertically

If the problem is:

**Repeated identical reads**

increasing database instance size may be:

**Less efficient**

than caching.

### Killer Exam Principle

> **Fix the access pattern, not just the instance size**

---

# Cache and Availability

Caches improve performance but should not become:

**A new single point of failure**

Architecture should consider:

- Replication
- Multi-AZ support
- Failover
- Cluster design

depending on:

**Cache engine and requirements**

---

# Cache Failure

A resilient application should often be able to:

**Fall back to the source**

if the cache becomes unavailable.

Example:

Cache unavailable  
↓  
Application  
↓  
Database

### Exam Principle

> **Cache should often accelerate the source, not become the only copy of critical data**

---

# Cache Is Usually Not the System of Record

The:

**System of Record**

is the authoritative source of data.

Typically:

- Database
- S3
- Durable data store

The cache usually contains:

**Temporary copies**

### Memory Trick

**Cache = Copy**

**Database = Truth**

---

# Cache Eviction

Cache systems may remove entries due to:

- TTL expiration
- Memory pressure
- Explicit invalidation

Applications should therefore not assume:

**Cached data always exists**

---

# Hot Data

Frequently accessed information is sometimes called:

**Hot Data**

Caching works especially well for:

**Hot data**

Examples:

- Popular products
- Common API responses
- Session data
- Trending pages

---

# Cold Data

Rarely accessed data provides:

**Less caching benefit**

because cache entries may expire before:

**They are requested again**

---

# CloudFront + S3 Architecture

A classic high-performance architecture:

Users  
↓  
[[CloudFront]]  
↓  
[[S3]]

Use for:

- Images
- JavaScript
- CSS
- Downloads
- Static websites

### Killer Exam Clue

> **Globally distribute static S3 content with low latency**
>
> → **CloudFront + S3**

---

# CloudFront + ALB Architecture

Dynamic web applications can use:

Users  
↓  
CloudFront  
↓  
[[Application Load Balancer]]  
↓  
Application

CloudFront may cache:

**Cacheable responses**

and reduce:

**Origin traffic**

---

# Application Cache + RDS

Architecture:

Application  
↓  
ElastiCache  
↓  
[[RDS]]

Use when:

**RDS receives frequent repeated reads**

### Killer Exam Clue

> **Frequently queried reference data changes infrequently**
>
> → **ElastiCache**

---

# Multi-Layer Caching

Some architectures use:

**Multiple cache layers**

Example:

User  
↓  
CloudFront  
↓  
Application  
↓  
ElastiCache  
↓  
Database

Each layer reduces load on:

**The next layer**

### Memory Trick

**Cache at the Edge**

**Cache in the App**

---

# Caching and Cost

Caching can reduce:

- Database load
- Backend compute
- Origin requests
- Repeated data transfer

But caching itself also has:

**A cost**

### Exam Principle

> **Use caching when performance and backend savings justify it**

---

# Caching and Consistency

The tradeoff:

**Performance**

vs:

**Freshness**

Long TTL:

- Better cache efficiency
- Greater stale-data risk

Short TTL:

- Fresher data
- More backend requests

### Memory Trick

> **Long TTL = Faster + Older Risk**
>
> **Short TTL = Fresher + More Backend Load**

---

# Architecture Thinking

## Scenario 1 — Global Images

Users worldwide repeatedly download:

**The same product images**

Choose:

**CloudFront**

---

## Scenario 2 — Repeated Database Queries

Application repeatedly queries:

**The same product catalog records**

Choose:

**ElastiCache**

---

## Scenario 3 — DynamoDB Read Latency

DynamoDB workload performs:

**Repeated reads of the same items**

and needs extremely low latency.

Choose:

**DAX**

---

## Scenario 4 — API Backend Overloaded

Clients repeatedly request:

**Identical API responses**

Choose:

**API Gateway Caching**

where appropriate.

---

## Scenario 5 — Users Receive Old Prices

Application cache returns:

**Outdated values**

Think:

- TTL too long
- Cache invalidation/update issue

---

## Scenario 6 — Cache Fails

Application must continue functioning.

Design:

Cache  
❌  
↓  
Fallback to Database

---

## Scenario 7 — Read Heavy Database

Database has heavy read volume but requests are:

**Not highly repetitive**

A:

**Read Replica**

may be more appropriate than relying primarily on cache.

---

## Scenario 8 — Session State

Multiple Auto Scaling instances need:

**Shared sessions**

Choose:

**ElastiCache**

or another appropriate shared durable store depending on requirements.

---

# Scenario Recognition

Immediately think:

**CloudFront**

when you see:

- Global users
- Edge caching
- Static content
- Reduce origin load

---

## Think ElastiCache When You See

- Repeated database reads
- In-memory
- Sessions
- Frequently accessed data

---

## Think DAX When You See

- DynamoDB
- Read acceleration
- In-memory DynamoDB cache

---

## Think API Gateway Cache When You See

- Repeated API responses
- Reduce backend invocations

---

# Exam Traps

## Trap 1 — CloudFront Is a Database Cache

❌

Think:

**ElastiCache / DAX**

CloudFront is primarily:

**Edge HTTP/content caching**

---

## Trap 2 — ElastiCache Replaces the Database

❌

The database usually remains:

**The system of record**

---

## Trap 3 — Caching Guarantees Fresh Data

❌

Caches can contain:

**Stale data**

---

## Trap 4 — Longer TTL Is Always Better

❌

Long TTL increases:

**Stale-data risk**

---

## Trap 5 — Read Replica and Cache Are Identical

❌

Read Replica:

**Still processes database queries**

Cache:

**May avoid database query entirely**

---

## Trap 6 — DAX Is a General RDS Cache

❌

DAX is purpose-built for:

**DynamoDB**

---

## Trap 7 — Sticky Sessions Are the Same as Session Caching

❌

Sticky sessions:

**Send user back to same server**

Shared session cache:

**Lets any server retrieve state**

---

# Quick Cheat Sheet

| Exam Clue | Answer |
|---|---|
| Global Edge Cache | CloudFront |
| Static Content | CloudFront |
| Reduce Origin Load | CloudFront |
| Database/Application Cache | ElastiCache |
| Fast Shared Sessions | ElastiCache |
| DynamoDB Cache | DAX |
| API Response Cache | API Gateway |
| Cache Expiration | TTL |
| Force CloudFront Refresh | Invalidation |
| More DB Read Capacity | Read Replica |
| Repeated Identical Reads | Cache |
| Cache Miss | Query Source |
| Cache Hit | Return Cached Data |

---

# Caching Decision Map

Need:

**Global web-content cache**

→ CloudFront

Need:

**Repeated database-read cache**

→ ElastiCache

Need:

**DynamoDB read acceleration**

→ DAX

Need:

**API response caching**

→ API Gateway Cache

Need:

**More relational database read capacity**

→ Read Replica

Need:

**Shared fast sessions**

→ ElastiCache

---

# Performance Decision Map

> **USERS FAR FROM CONTENT**
> → CLOUDFRONT
>
> **DATABASE REPEATED READS**
> → ELASTICACHE
>
> **DYNAMODB REPEATED READS**
> → DAX
>
> **REPEATED API RESPONSE**
> → API GATEWAY CACHE
>
> **READ LOAD BUT LOW CACHE REUSE**
> → READ REPLICA

---

# Final Exam Rapid-Fire

> **EDGE CACHE**
> → CLOUDFRONT
>
> **GLOBAL STATIC CONTENT**
> → CLOUDFRONT
>
> **DATABASE CACHE**
> → ELASTICACHE
>
> **SESSION CACHE**
> → ELASTICACHE
>
> **DYNAMODB CACHE**
> → DAX
>
> **API CACHE**
> → API GATEWAY
>
> **CACHE EXPIRATION**
> → TTL
>
> **REMOVE CLOUDFRONT CACHE NOW**
> → INVALIDATION
>
> **CACHE FOUND**
> → HIT
>
> **CACHE NOT FOUND**
> → MISS
>
> **DATABASE TRUTH**
> → SYSTEM OF RECORD
>
> **MORE DATABASE READERS**
> → READ REPLICA

---

## Master Memory Trick

> [!tip] Caching Architecture Master Memory Trick
> Imagine a popular restaurant.
>
> Every customer orders:
>
> **THE SAME SAUCE**
>
> Without caching, the chef makes:
>
> **A NEW BATCH FOR EVERY CUSTOMER**
>
> That's slow.
>
> Instead, keep a ready container:
>
> **NEXT TO THE SERVING LINE**
>
> Now the common request is answered:
>
> **IMMEDIATELY**
>
> That's:
>
> **CACHE**
>
> For global web content:
>
> put the sauce near:
>
> **THE CUSTOMER**
>
> → CloudFront
>
> For application/database data:
>
> put it near:
>
> **THE APPLICATION**
>
> → ElastiCache
>
> For DynamoDB:
>
> use:
>
> **DAX**

So remember:

> **CLOUDFRONT**
> → USER CACHE
>
> **ELASTICACHE**
> → APPLICATION CACHE
>
> **DAX**
> → DYNAMODB CACHE
>
> **TTL**
> → HOW LONG
>
> **HIT**
> → FOUND
>
> **MISS**
> → FETCH
>
> **DATABASE**
> → SOURCE OF TRUTH

And the killer SAA question:

> **"Is the system repeatedly retrieving the same data or content when a nearby cached copy could satisfy the request faster and reduce backend load?"**
>
> YES
>
> → **Use an appropriate caching layer**

---

## Related Notes

- [[Architecture Principles]]
- [[Stateless vs Stateful Architecture]]
- [[CloudFront]]
- [[ElastiCache]]
- [[DynamoDB]]
- [[RDS]]
- [[Aurora]]
- [[API Gateway]]
- [[Application Load Balancer]]
- [[S3]]
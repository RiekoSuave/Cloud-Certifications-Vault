## What Problem Does It Solve?

DynamoDB provides:

MILLISECOND LATENCY

But some applications require:

EXTREMELY FAST READS

and may generate:

HEAVY READ TRAFFIC

This can create:

READ CONGESTION

DAX solves this by adding:

AN IN-MEMORY CACHE

in front of DynamoDB.

Think:

APPLICATION

↓

DAX

↓

DYNAMODB

### Memory Trick

DAX

=

DYNAMODB READ ACCELERATOR

---

## What Is DAX?

DAX stands for:

DYNAMODB ACCELERATOR

It is a:

FULLY MANAGED

HIGHLY AVAILABLE

SEAMLESS

IN-MEMORY CACHE

for:

[[DynamoDB Overview]]

Think:

DYNAMODB

+

CACHE

↓

DAX

### Memory Trick

DAX

=

CACHE BUILT FOR DYNAMODB

---

## Why Use DAX?

DAX helps solve:

READ CONGESTION

by:

CACHING DATA

Instead of repeatedly retrieving the same data directly from DynamoDB:

APPLICATION

↓

DAX CACHE

↓

RETURN CACHED DATA

This reduces repeated reads against:

DYNAMODB

### Memory Trick

REPEATED DYNAMODB READS?

↓

DAX

---

## DAX Latency

DynamoDB normally provides:

MILLISECOND LATENCY

DAX can provide:

MICROSECOND LATENCY

for:

CACHED DATA

Think:

DYNAMODB

↓

MILLISECONDS

DAX CACHE HIT

↓

MICROSECONDS

### Memory Trick

DAX

=

MICROSECOND READS

---

## DAX Architecture

Basic architecture:

APPLICATION

↓

DAX CLUSTER

↓

DYNAMODB TABLES

The DAX cluster contains:

NODES

Think:

APP

↓

CACHE

↓

DATABASE

### Memory Trick

DAX SITS BETWEEN

APPLICATION

and:

DYNAMODB

---

## Cache Hit

If requested data already exists in:

DAX CACHE

Think:

APPLICATION REQUEST

↓

DAX

↓

CACHE HIT

↓

RETURN DATA

The application receives:

CACHED DATA

with:

MICROSECOND LATENCY

### Memory Trick

CACHE HIT

=

VERY FAST READ

---

## Cache Miss

If the requested data is not available in the cache:

APPLICATION

↓

DAX

↓

CACHE MISS

↓

DYNAMODB

DynamoDB provides the data.

DAX can then cache that data for subsequent requests.

Think:

FIRST READ

↓

DYNAMODB

LATER READS

↓

DAX

### Memory Trick

MISS

=

GO TO DYNAMODB

---

## DAX Is Fully Managed

DAX is:

FULLY MANAGED

AWS manages the underlying cache infrastructure.

Think:

NO MANUAL CACHE SERVER MANAGEMENT

↓

DAX

This fits the managed-service architecture commonly tested on the SAA exam.

### Memory Trick

DAX

=

MANAGED DYNAMODB CACHE

---

## DAX Is Highly Available

DAX is designed to be:

HIGHLY AVAILABLE

The course architecture represents DAX as a:

CLUSTER

containing:

MULTIPLE NODES

Think:

DAX CLUSTER

↓

NODES

↓

HIGH AVAILABILITY

### Memory Trick

DAX

=

CACHE CLUSTER

---

## Seamless Integration

DAX is designed specifically for:

DYNAMODB

It is compatible with existing:

DYNAMODB APIs

The course emphasizes that DAX does not require:

APPLICATION LOGIC MODIFICATION

Think:

EXISTING DYNAMODB APPLICATION

↓

DAX

↓

MINIMAL APPLICATION CHANGE

### Memory Trick

DAX

=

DYNAMODB-COMPATIBLE CACHE

---

## DAX Default TTL

Cached data in DAX has a default:

5-MINUTE TTL

TTL means:

TIME TO LIVE

Think:

DATA ENTERS CACHE

↓

5 MINUTES

↓

CACHE ENTRY EXPIRES

by default.

### Memory Trick

DAX DEFAULT TTL

=

5 MINUTES

---

## Why Cache Data?

Suppose an application repeatedly requests:

PRODUCT #123

Without DAX:

APPLICATION

↓

DYNAMODB

↓

APPLICATION

↓

DYNAMODB

↓

APPLICATION

↓

DYNAMODB

With DAX:

FIRST REQUEST

↓

DYNAMODB

↓

CACHE DATA

Later requests:

↓

DAX

↓

CACHED RESULT

### Memory Trick

SAME READ AGAIN?

↓

USE CACHE

---

## Read Congestion Scenario

Imagine a popular application where thousands of users repeatedly request:

THE SAME DYNAMODB DATA

Requirement:

REDUCE READ CONGESTION

and:

IMPROVE READ LATENCY

Think:

HEAVY REPEATED READS

↓

DAX

This is one of the strongest DAX exam signals.

### Memory Trick

DYNAMODB + READ CONGESTION

=

DAX

---

## DAX vs DynamoDB Capacity

Do not confuse:

MORE DYNAMODB CAPACITY

with:

DAX CACHING

[[DynamoDB Capacity Modes]]

controls:

READ / WRITE CAPACITY

DAX provides:

AN IN-MEMORY READ CACHE

Think:

CAPACITY PROBLEM

↓

PROVISIONED / ON-DEMAND

REPEATED READ PROBLEM

↓

DAX

### Memory Trick

CAPACITY MODE

=

THROUGHPUT

DAX

=

CACHE

---

## DAX vs ElastiCache

Both provide:

IN-MEMORY CACHING

But they solve different caching problems.

### DAX

Designed specifically for:

DYNAMODB

Can cache:

INDIVIDUAL OBJECTS

and:

QUERY / SCAN RESULTS

Think:

DYNAMODB CACHE

↓

DAX

---

### ElastiCache

Can be used as a more general caching layer.

The course comparison highlights storing things such as:

AGGREGATION RESULTS

Think:

GENERAL APPLICATION CACHE

↓

[[ElastiCache Overview]]

### Memory Trick

DYNAMODB-SPECIFIC CACHE

=

DAX

GENERAL CACHE

=

ELASTICACHE

---

## DAX Object Cache

DAX can cache:

INDIVIDUAL OBJECTS

Think:

GET ITEM

↓

DAX

↓

CACHED OBJECT

This is useful when the same DynamoDB items are:

READ REPEATEDLY

### Memory Trick

DAX

=

OBJECT CACHE

---

## DAX Query and Scan Cache

The SAA slides also highlight:

QUERY CACHE

and:

SCAN CACHE

Think:

DYNAMODB QUERY

↓

DAX

↓

CACHED RESULT

or:

DYNAMODB SCAN

↓

DAX

↓

CACHED RESULT

### Memory Trick

DAX

=

OBJECTS + QUERY + SCAN CACHE

---

## DAX vs ElastiCache Decision

Question says:

DYNAMODB

+

MICROSECOND READ LATENCY

↓

DAX

---

Question says:

DYNAMODB

+

READ CONGESTION

↓

DAX

---

Question says:

DYNAMODB

+

SEAMLESS CACHE

↓

DAX

---

Question says:

GENERAL APPLICATION CACHING

↓

[[ElastiCache Overview]]

### Memory Trick

DYNAMODB NAMED?

↓

THINK DAX FIRST

---

## DAX Does Not Replace DynamoDB

DAX is not:

A DATABASE REPLACEMENT

DynamoDB remains the:

DATABASE

DAX is the:

CACHING LAYER

Think:

APPLICATION

↓

DAX

↓

DYNAMODB

### Memory Trick

DAX

=

CACHE

NOT:

DATABASE

---

## DAX and DynamoDB Reads

The DynamoDB course summary describes DAX as:

READ CACHE

Think:

WRITE / STORE DATA

↓

DYNAMODB

FAST REPEATED READS

↓

DAX

The important exam association is:

DAX

=

READ PERFORMANCE

### Memory Trick

DAX

=

READ FAST

---

## DAX and DynamoDB Consistency

DAX is primarily an exam answer when the requirement emphasizes:

CACHING

READ CONGESTION

MICROSECOND READ LATENCY

If the question instead emphasizes DynamoDB read consistency behavior:

↓

[[DynamoDB Streams]]

### Memory Trick

LATENCY / CACHE

=

DAX

CONSISTENCY

=

DYNAMODB CONSISTENCY

---

## Architecture Scenario

Imagine:

MOBILE APPLICATION

↓

API

↓

DYNAMODB

The application experiences:

HEAVY REPEATED READS

Add:

DAX

Think:

MOBILE APPLICATION

↓

API

↓

DAX

↓

DYNAMODB

Result:

CACHED DYNAMODB READS

### Memory Trick

READ-HEAVY DYNAMODB APP

↓

PUT DAX IN FRONT

---

## Serverless Architecture Scenario

The course architecture examples use DAX as a:

CACHING LAYER

for DynamoDB reads.

Think:

APPLICATION

↓

API GATEWAY

↓

LAMBDA

↓

DAX

↓

DYNAMODB

DAX improves:

DATABASE READ PERFORMANCE

while API Gateway caching operates at a different layer.

### Memory Trick

DAX

=

DATABASE CACHE

---

## DAX vs API Gateway Cache

Do not confuse:

DAX

with:

API GATEWAY CACHING

### DAX

Caches:

DYNAMODB READS

Think:

DATABASE LAYER

---

### API Gateway Cache

Caches:

API RESPONSES

Think:

API LAYER

### Memory Trick

DATABASE CACHE

=

DAX

API RESPONSE CACHE

=

API GATEWAY

---

## When DAX Is a Strong Answer

Look for requirements such as:

DYNAMODB

+

READ-HEAVY WORKLOAD

+

REPEATED READS

+

READ CONGESTION

+

MICROSECOND LATENCY

These strongly point toward:

DAX

### Memory Trick

DYNAMODB + FAST READS

=

DAX

---

## When DAX Is NOT the Best Answer

Need:

GENERAL DATABASE / APPLICATION CACHE

↓

[[ElastiCache Overview]]

Need:

CHANGE DYNAMODB CAPACITY

↓

[[DynamoDB Capacity Modes]]

Need:

GLOBAL MULTI-REGION DYNAMODB

↓

[[DynamoDB Global Tables]]

Need:

PROCESS ITEM CHANGES

↓

[[DynamoDB Streams]]

Need:

ALTERNATIVE QUERY ACCESS PATTERNS

↓

[[DynamoDB Indexes]]

### Memory Trick

DAX HAS ONE MAIN JOB

=

ACCELERATE DYNAMODB READS

---

## Scenario Recognition

Need microsecond latency for cached DynamoDB data?

→ DAX

---

Need to solve DynamoDB read congestion?

→ DAX

---

Need a fully managed DynamoDB cache?

→ DAX

---

Need a highly available DynamoDB cache?

→ DAX

---

Need seamless caching compatible with DynamoDB APIs?

→ DAX

---

Need caching without major application logic modification?

→ DAX

---

Need to cache individual DynamoDB objects?

→ DAX

---

Need Query and Scan caching?

→ DAX

---

Need a general-purpose application cache?

→ [[ElastiCache Overview]]

---

Need to increase or automatically manage DynamoDB throughput?

→ [[DynamoDB Capacity Modes]]

---

Need API response caching?

→ API Gateway Cache

NOT DAX

---

## Exam Traps

DAX

=

DYNAMODB ACCELERATOR

---

DAX

=

IN-MEMORY CACHE

---

DAX

=

FULLY MANAGED

---

DAX

=

HIGHLY AVAILABLE

---

DAX

=

DYNAMODB-SPECIFIC

---

DAX

=

SOLVES READ CONGESTION

---

DAX CACHED DATA

=

MICROSECOND LATENCY

---

DYNAMODB

=

MILLISECOND LATENCY

---

DAX DEFAULT CACHE TTL

=

5 MINUTES

---

DAX

=

COMPATIBLE WITH DYNAMODB APIs

---

DAX

=

NO MAJOR APPLICATION LOGIC MODIFICATION

---

DAX CAN CACHE

=

INDIVIDUAL OBJECTS

+

QUERY RESULTS

+

SCAN RESULTS

---

DAX

≠

GENERAL-PURPOSE DATABASE CACHE

---

DAX

≠

DYNAMODB CAPACITY MODE

---

DAX

≠

DYNAMODB DATABASE REPLACEMENT

---

DAX

≠

API GATEWAY CACHE

---

## Quick Cheat Sheet

DAX

=

DYNAMODB ACCELERATOR

TYPE

=

IN-MEMORY CACHE

MANAGEMENT

=

FULLY MANAGED

AVAILABILITY

=

HIGHLY AVAILABLE

PURPOSE

=

SOLVE READ CONGESTION

LATENCY

=

MICROSECONDS FOR CACHED DATA

DYNAMODB NORMAL LATENCY

=

MILLISECONDS

DEFAULT CACHE TTL

=

5 MINUTES

API

=

COMPATIBLE WITH DYNAMODB APIs

APPLICATION LOGIC CHANGE

=

NOT REQUIRED

CACHE TYPES

=

OBJECTS

+

QUERY

+

SCAN

DYNAMODB-SPECIFIC CACHE

=

DAX

GENERAL CACHE

=

ELASTICACHE

READ PERFORMANCE

=

DAX

CAPACITY MANAGEMENT

=

PROVISIONED / ON-DEMAND

---

## Master Memory Trick

DAX

=

DYNAMODB

ACCELERATOR

Think:

APPLICATION

↓

DAX

↓

DYNAMODB

Then remember:

DYNAMODB

=

MILLISECONDS

DAX CACHE

=

MICROSECONDS

And:

READ CONGESTION

↓

CACHE IT

↓

DAX

### Final Rule

QUESTION SAYS:

DYNAMODB

+

READ CONGESTION

+

MICROSECOND LATENCY

↓

DAX

QUESTION SAYS:

GENERAL APPLICATION CACHE

↓

ELASTICACHE

QUESTION SAYS:

DYNAMODB THROUGHPUT / CAPACITY

↓

PROVISIONED OR ON-DEMAND

---

## Related Notes

- [[DynamoDB Overview]]
- [[DynamoDB Primary Keys]]
- [[DynamoDB Capacity Modes]]
- [[DynamoDB Streams]]
- [[DynamoDB Indexes]]
- [[DynamoDB Streams]]
- [[DynamoDB Global Tables]]
- [[DynamoDB TTL]]
- [[DynamoDB Backups]]
- [[ElastiCache Overview]]
- [[ElastiCache Caching Strategies]]
- [[SAA Databases Cheat Sheet]]
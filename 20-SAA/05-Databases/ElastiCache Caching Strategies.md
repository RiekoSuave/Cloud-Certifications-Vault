## What Problem Does It Solve?

Using a cache creates an important design question:

WHEN SHOULD DATA ENTER THE CACHE?

and:

WHEN SHOULD DATA LEAVE THE CACHE?

A poor caching strategy can cause:

STALE DATA

↓

UNNECESSARY DATABASE LOAD

↓

WASTED CACHE SPACE

↓

INCORRECT APPLICATION RESULTS

ElastiCache caching strategies define:

HOW DATA IS LOADED

↓

HOW DATA IS UPDATED

↓

HOW LONG DATA IS KEPT

### Memory Trick

CACHING STRATEGY

=

HOW CACHE DATA LIVES

---

## Main ElastiCache Patterns

Your SAA course highlights three important patterns:

LAZY LOADING

↓

WRITE THROUGH

↓

SESSION STORE

Think:

READ DATA ON DEMAND?

↓

LAZY LOADING

KEEP CACHE UPDATED WHEN DB CHANGES?

↓

WRITE THROUGH

STORE USER LOGIN STATE?

↓

SESSION STORE

### Memory Trick

LAZY

=

READ

WRITE THROUGH

=

WRITE

SESSION STORE

=

USER STATE

---

## Lazy Loading

Lazy Loading means:

DATA IS LOADED INTO CACHE

only when:

THE APPLICATION REQUESTS IT

Think:

APPLICATION

↓

CHECK CACHE

↓

CACHE HIT?

YES

↓

RETURN DATA

NO

↓

QUERY DATABASE

↓

WRITE RESULT TO CACHE

↓

RETURN DATA

### Memory Trick

LAZY LOADING

=

CACHE IT WHEN NEEDED

---

## Lazy Loading Architecture

Think:

STEP 1

APPLICATION REQUESTS DATA

↓

STEP 2

CHECK ELASTICACHE

↓

STEP 3

CACHE MISS

↓

STEP 4

QUERY RDS

↓

STEP 5

STORE RESULT IN ELASTICACHE

↓

STEP 6

RETURN RESULT

Next request:

APPLICATION

↓

ELASTICACHE

↓

CACHE HIT

↓

RETURN FAST

### Memory Trick

MISS ONCE

↓

CACHE IT

↓

HIT NEXT TIME

---

## Cache Hit

A:

CACHE HIT

means:

REQUESTED DATA EXISTS IN CACHE

Think:

APPLICATION

↓

ELASTICACHE

↓

FOUND

↓

FAST RESPONSE

The database does not need to be queried.

### Memory Trick

HIT

=

CACHE HAS IT

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

DATABASE

↓

READ DATA

↓

STORE IN CACHE

### Memory Trick

MISS

=

GO TO DATABASE

---

## Lazy Loading Benefit

Lazy Loading caches:

ONLY DATA THAT IS ACTUALLY REQUESTED

Think:

DATABASE HAS:

1,000,000 RECORDS

But users only access:

10,000 RECORDS

Lazy Loading:

↓

CACHE ONLY HOT DATA

This makes efficient use of:

CACHE MEMORY

### Memory Trick

LAZY

=

ONLY CACHE WHAT USERS WANT

---

## Lazy Loading Reduces Database Reads

After the first:

CACHE MISS

future requests may become:

CACHE HITS

Think:

FIRST REQUEST

↓

DATABASE

SECOND REQUEST

↓

CACHE

THIRD REQUEST

↓

CACHE

FOURTH REQUEST

↓

CACHE

This reduces:

READ LOAD

on:

RDS / AURORA

---

## Lazy Loading Problem

The major downside is:

STALE DATA

Suppose:

DATABASE

=

PRODUCT PRICE $100

Cache:

=

PRODUCT PRICE $100

Database changes:

↓

PRODUCT PRICE $80

But cache still says:

$100

Think:

DATABASE

≠

CACHE

This is:

STALE DATA

### Memory Trick

LAZY LOADING

=

FAST READS

BUT

STALE DATA POSSIBLE

---

## Why Lazy Loading Can Become Stale

Lazy Loading normally updates the cache when:

DATA IS READ AFTER A CACHE MISS

But a database write may occur:

WITHOUT IMMEDIATELY UPDATING CACHE

Think:

DATABASE WRITE

↓

CACHE UNAWARE

↓

OLD VALUE REMAINS

Therefore:

CACHE INVALIDATION

becomes important.

---

## Cache Invalidation

Cache Invalidation means:

REMOVING

or:

UPDATING

cached data when it should no longer be used.

Think:

DATABASE CHANGES

↓

CACHE ENTRY OLD

↓

INVALIDATE CACHE

↓

NEXT REQUEST GETS FRESH DATA

### Memory Trick

INVALIDATE

=

THROW AWAY OLD CACHE

---

## Invalidation Strategy

Your course emphasizes that a cache should have:

AN INVALIDATION STRATEGY

to ensure:

CURRENT DATA

is returned.

Think:

CACHE

=

FAST

but:

DATABASE

=

SOURCE OF TRUTH

The cache must not keep incorrect values forever.

### Memory Trick

CACHE WITHOUT INVALIDATION

=

STALE DATA RISK

---

## TTL

TTL stands for:

TIME TO LIVE

TTL defines:

HOW LONG DATA REMAINS IN CACHE

Think:

CACHE ENTRY CREATED

↓

TTL = 300 SECONDS

↓

300 SECONDS PASS

↓

CACHE ENTRY EXPIRES

### Memory Trick

TTL

=

EXPIRATION TIMER

---

## TTL and Stale Data

TTL can reduce:

STALE DATA RISK

because old cache entries eventually:

EXPIRE

Think:

OLD DATA

↓

TTL EXPIRES

↓

CACHE MISS

↓

DATABASE READ

↓

FRESH DATA CACHED

### Memory Trick

TTL

=

AUTOMATIC CACHE REFRESH OPPORTUNITY

---

## TTL Tradeoff

A very long TTL:

MORE CACHE HITS

↓

LESS DATABASE LOAD

but:

GREATER STALE DATA RISK

A very short TTL:

FRESHER DATA

but:

MORE DATABASE QUERIES

Think:

LONG TTL

=

FAST + STALE RISK

SHORT TTL

=

FRESH + MORE DB LOAD

### Memory Trick

TTL

=

FRESHNESS VS PERFORMANCE

---

## Write Through

Write Through means:

WHEN DATA IS WRITTEN TO THE DATABASE

the application also:

ADDS

or:

UPDATES

the cache.

Think:

APPLICATION WRITE

↓

DATABASE

+

ELASTICACHE

### Memory Trick

WRITE THROUGH

=

WRITE DB + CACHE

---

## Write Through Architecture

Think:

APPLICATION

↓

UPDATE PRODUCT PRICE

↓

DATABASE UPDATED

and:

CACHE UPDATED

Now:

DATABASE

=

$80

CACHE

=

$80

Future reads:

↓

CACHE HIT

↓

CURRENT DATA

### Memory Trick

WRITE ONCE

↓

UPDATE BOTH

---

## Write Through Benefit

Write Through helps prevent:

STALE CACHE DATA

because cache values are updated when:

DATABASE WRITES OCCUR

Think:

DB CHANGES

↓

CACHE CHANGES TOO

Your course describes Write Through as:

NO STALE DATA

in the basic pattern.

### Memory Trick

WRITE THROUGH

=

KEEP CACHE CURRENT

---

## Write Through Downside

Write Through may place:

DATA IN CACHE

that is:

NEVER READ

Think:

APPLICATION WRITES:

100,000 RECORDS

But users only read:

10,000

Write Through may populate cache with:

UNNEEDED DATA

This can use:

MORE CACHE MEMORY

### Memory Trick

WRITE THROUGH

=

FRESH

BUT MAY CACHE UNUSED DATA

---

## Lazy Loading vs Write Through

### Lazy Loading

CACHE POPULATED:

WHEN DATA IS READ

Benefit:

ONLY REQUESTED DATA CACHED

Problem:

STALE DATA POSSIBLE

---

### Write Through

CACHE POPULATED / UPDATED:

WHEN DATABASE IS WRITTEN

Benefit:

CACHE STAYS CURRENT

Problem:

MAY CACHE UNUSED DATA

### Memory Trick

LAZY

=

READ → CACHE

WRITE THROUGH

=

WRITE → CACHE

---

## Combining Lazy Loading + Write Through

These strategies can be:

COMBINED

Think:

READS

↓

LAZY LOADING

WRITES

↓

WRITE THROUGH

This provides:

CACHE DATA ON DEMAND

+

UPDATE CACHE WHEN DATA CHANGES

Think:

READ MISS

↓

LOAD CACHE

WRITE

↓

UPDATE DB + CACHE

### Memory Trick

LAZY + WRITE THROUGH

=

LOAD WHEN READ

KEEP FRESH WHEN WRITTEN

---

## Session Store

ElastiCache can also act as a:

SESSION STORE

Think:

USER LOGS IN

↓

SESSION DATA

↓

ELASTICACHE

Application servers can retrieve that session later.

### Memory Trick

SESSION STORE

=

USER STATE IN CACHE

---

## Session Store Architecture

Think:

USER

↓

APPLICATION INSTANCE #1

↓

LOGIN

↓

WRITE SESSION

↓

ELASTICACHE

Next request:

USER

↓

APPLICATION INSTANCE #2

↓

READ SESSION

↓

ELASTICACHE

↓

USER STILL LOGGED IN

This helps application servers remain:

STATELESS

---

## Session Store + TTL

Session data is usually:

TEMPORARY

Therefore TTL is useful.

Think:

USER SESSION

↓

TTL = 30 MINUTES

↓

NO ACTIVITY

↓

SESSION EXPIRES

### Memory Trick

SESSION STORE

+

TTL

=

AUTO-EXPIRE LOGIN STATE

---

## Why TTL Fits Sessions

User sessions should not normally exist:

FOREVER

Think:

LOGIN

↓

SESSION CREATED

↓

USER STOPS USING APP

↓

TTL EXPIRES

↓

SESSION REMOVED

This helps:

FREE CACHE MEMORY

and:

CONTROL SESSION LIFETIME

---

## Session Store and Stateless Apps

Without shared sessions:

EC2 #1

↓

USER SESSION

If next request reaches:

EC2 #2

↓

SESSION MISSING

With ElastiCache:

EC2 #1

↓

ELASTICACHE

↑

EC2 #2

Now:

ANY APP INSTANCE

can retrieve:

THE SAME SESSION

### Memory Trick

SESSION OUTSIDE SERVER

=

STATELESS SERVERS

---

## Session Store vs Stickiness

Do not confuse:

SESSION STORE

with:

[Load Balancer Stickiness](<Load Balancer Stickiness>)

### Stickiness

USER

↓

SAME EC2 INSTANCE

---

### Session Store

USER

↓

ANY EC2 INSTANCE

↓

SHARED ELASTICACHE SESSION

Think:

STICKINESS

=

KEEP USER ON SERVER

SESSION STORE

=

KEEP USER STATE OFF SERVER

### Memory Trick

SHARED SESSION

=

MORE FLEXIBLE SCALING

---

## Cache-Aside Pattern

Lazy Loading is also commonly known as:

CACHE-ASIDE

Think:

APPLICATION

controls:

CACHE

and:

DATABASE

The cache does not automatically query the database.

Think:

APP CHECKS CACHE

↓

APP CHECKS DB

↓

APP WRITES CACHE

### Memory Trick

CACHE-ASIDE

=

APP MANAGES CACHE FLOW

---

## Database Remains Source of Truth

In common ElastiCache architectures:

RDS / AURORA

remains:

THE SOURCE OF TRUTH

Think:

DATABASE

=

AUTHORITATIVE

CACHE

=

TEMPORARY FAST COPY

If cache data disappears:

APPLICATION

↓

DATABASE

↓

REBUILD CACHE

### Memory Trick

DB

=

TRUTH

CACHE

=

SPEED

---

## Caching Requires Application Logic

Your application must know:

WHEN TO CHECK CACHE

↓

WHEN TO QUERY DATABASE

↓

WHEN TO UPDATE CACHE

↓

WHEN TO INVALIDATE CACHE

This is why ElastiCache generally requires:

APPLICATION CODE CHANGES

### Memory Trick

CACHE STRATEGY

=

APP RESPONSIBILITY

---

## Lazy Loading Scenario

Imagine a product catalog.

FIRST USER REQUEST:

PRODUCT 123

↓

CACHE MISS

↓

RDS

↓

PRODUCT DATA

↓

CACHE PRODUCT 123

NEXT 10,000 REQUESTS:

PRODUCT 123

↓

CACHE HIT

↓

FAST RESPONSE

Think:

POPULAR READ DATA

↓

LAZY LOADING

---

## Write Through Scenario

Imagine product price changes:

OLD PRICE

=

$100

Admin updates:

PRICE

=

$80

Write Through:

APPLICATION

↓

RDS = $80

+

CACHE = $80

Future reads return:

$80

without stale cache.

Think:

FREQUENT UPDATES

+

NEED CURRENT CACHE

↓

WRITE THROUGH

---

## Session Store Scenario

Imagine users can hit any EC2 instance in an:

[Auto Scaling Groups](<Auto Scaling Groups>)

User logs in through:

EC2 #1

Session stored:

↓

ELASTICACHE

Later request reaches:

EC2 #7

EC2 #7:

↓

READ SESSION

↓

USER STILL AUTHENTICATED

Think:

AUTO-SCALED APP SERVERS

+

SHARED LOGIN STATE

↓

SESSION STORE

---

## Strategy Decision Tree

Need:

CACHE ONLY WHEN DATA IS REQUESTED?

↓

LAZY LOADING

---

Need:

MINIMIZE UNUSED CACHE DATA?

↓

LAZY LOADING

---

Need:

CACHE UPDATED WHEN DATABASE WRITES OCCUR?

↓

WRITE THROUGH

---

Need:

REDUCE STALE DATA?

↓

WRITE THROUGH

and/or:

TTL / INVALIDATION

---

Need:

TEMPORARY USER SESSION DATA?

↓

SESSION STORE

---

Need:

AUTOMATIC SESSION EXPIRATION?

↓

TTL

---

Need:

STATELESS APPLICATION INSTANCES?

↓

SESSION STORE

---

## Scenario Recognition

Application should check cache before querying RDS?

→ Lazy Loading

---

Cache miss should query database and then populate cache?

→ Lazy Loading

---

Need only requested data stored in cache?

→ Lazy Loading

---

Question says cached data may become stale?

→ Lazy Loading / Cache Invalidation

---

Need cache updated when database is written?

→ Write Through

---

Need database and cache updated together?

→ Write Through

---

Need to minimize stale cached values?

→ Write Through

---

Need temporary login state in ElastiCache?

→ Session Store

---

Need user session to work across multiple EC2 instances?

→ Session Store

---

Need session data to expire automatically?

→ TTL

---

Need stale entries eventually removed?

→ TTL / Cache Invalidation

---

## Exam Traps

LAZY LOADING

=

READ DATA → CACHE IT

---

LAZY LOADING

=

CACHE MISS → DB → CACHE

---

LAZY LOADING

=

STALE DATA POSSIBLE

---

WRITE THROUGH

=

DB WRITE → CACHE UPDATE

---

WRITE THROUGH

=

HELPS PREVENT STALE DATA

---

SESSION STORE

=

TEMPORARY USER STATE

---

SESSION STORE

=

TTL COMMONLY USED

---

TTL

=

TIME TO LIVE

---

TTL

=

CACHE EXPIRATION

---

LONG TTL

=

MORE HITS + MORE STALE RISK

---

SHORT TTL

=

FRESHER + MORE DATABASE LOAD

---

CACHE INVALIDATION

=

REMOVE / UPDATE STALE CACHE

---

CACHE

≠

SOURCE OF TRUTH

---

DATABASE

=

SOURCE OF TRUTH

---

LAZY LOADING

≠

WRITE THROUGH

---

LAZY

=

READ PATH

WRITE THROUGH

=

WRITE PATH

---

## Quick Cheat Sheet

LAZY LOADING

=

CACHE ON READ

CACHE HIT

=

RETURN CACHE

CACHE MISS

=

QUERY DB + POPULATE CACHE

LAZY LOADING PROBLEM

=

STALE DATA

WRITE THROUGH

=

UPDATE DB + CACHE

WRITE THROUGH BENEFIT

=

FRESHER CACHE

SESSION STORE

=

TEMPORARY USER STATE

TTL

=

TIME TO LIVE

TTL PURPOSE

=

EXPIRE CACHE DATA

CACHE INVALIDATION

=

REMOVE / UPDATE OLD DATA

DATABASE

=

SOURCE OF TRUTH

CACHE

=

FAST TEMPORARY COPY

STATELESS APP SERVERS

=

SESSION STORE CAN HELP

---

## Master Memory Trick

READ?

↓

LAZY LOADING

WRITE?

↓

WRITE THROUGH

SESSION?

↓

SESSION STORE

EXPIRE?

↓

TTL

STALE?

↓

INVALIDATE

Think:

LAZY

=

LOAD WHEN READ

WRITE THROUGH

=

UPDATE WHEN WRITTEN

SESSION STORE

=

SAVE USER STATE

TTL

=

DELETE LATER

### Final Rule

QUESTION SAYS:

CACHE MISS

↓

RDS

↓

PUT RESULT IN CACHE

↓

LAZY LOADING

QUESTION SAYS:

DB WRITE

↓

UPDATE CACHE

↓

WRITE THROUGH

QUESTION SAYS:

USER LOGIN STATE

↓

ELASTICACHE + TTL

↓

SESSION STORE

---

## Related Notes

- [ElastiCache Overview](<ElastiCache Overview>)
- [Redis vs Memcached](<Redis vs Memcached>)
- [RDS Overview](<RDS Overview>)
- [Aurora](Aurora)
- [RDS Proxy](<RDS Proxy>)
- [Auto Scaling Groups](<Auto Scaling Groups>)
- [Load Balancer Stickiness](<Load Balancer Stickiness>)
- [SAA Databases Cheat Sheet](<SAA Databases Cheat Sheet>)
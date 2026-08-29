## What Problem Does It Solve?

[[Route 53 TTL]] controls **how long a DNS resolver caches a DNS record before asking [[Route 53]] for the record again**.

TTL stands for:

**Time To Live**

It solves the problem of balancing:

- DNS query traffic
- DNS caching
- Cost
- How quickly DNS changes are seen by users

Think:

**TTL = How long DNS remembers the answer**

---

## How TTL Works

Suppose a client wants to access:

myapp.example.com

The client performs a DNS query:

Client  
↓  
DNS Query  
↓  
[[Route 53]]  
↓  
A Record: 12.34.56.78  
↓  
DNS Resolver caches result  
↓  
Client connects to 12.34.56.78

The DNS response includes a TTL value.

Example:

TTL = 300 seconds

That means the resolver can reuse the cached answer for:

**5 minutes**

During that time, it does not need to ask Route 53 for the same record again.

> [!tip] Memory Trick
> **TTL = DNS Memory Timer**
>
> Until the timer expires, the resolver remembers the previous answer.

---

## TTL Architecture Thinking

Conceptually:

Client  
↓  
DNS Resolver  
↓  
[[Route 53]]

First request:

DNS Resolver  
↓ asks Route 53  
[[Route 53]]  
↓ returns 12.34.56.78 + TTL  
DNS Resolver  
↓ caches answer  
Client

Later request before TTL expires:

Client  
↓  
DNS Resolver  
↓  
Cached 12.34.56.78

Route 53 does **not need to be queried again**.

Once the TTL expires:

DNS Resolver  
↓  
[[Route 53]]  
↓  
Retrieve latest DNS record

---

## High TTL

A **high TTL** means the DNS record remains cached for a longer period.

Example:

**24 hours**

### Advantages

- Fewer DNS requests sent to [[Route 53]]
- Lower Route 53 query traffic
- Lower DNS query cost
- Less DNS lookup activity

### Disadvantages

The cached DNS record may become **outdated**.

Suppose:

Old Record:

myapp.example.com  
↓  
10.0.0.10

You change Route 53 to:

myapp.example.com  
↓  
10.0.0.20

A resolver that still has the old answer cached may continue sending users to:

10.0.0.10

until the TTL expires.

### Architecture Thinking

High TTL means:

**Better caching**

but

**Slower DNS changes**

> [!tip] Memory Trick
> **High TTL = Hold the answer longer**

---

## Low TTL

A **low TTL** means DNS resolvers keep the cached record for a shorter period.

Example:

**60 seconds**

### Advantages

- DNS changes take effect more quickly
- Old DNS records disappear from caches sooner
- Easier to change records during migrations or cutovers

### Disadvantages

- More DNS queries sent to [[Route 53]]
- More Route 53 traffic
- Potentially higher DNS query cost

### Architecture Thinking

Low TTL means:

**Less caching**

but

**Faster DNS changes**

> [!tip] Memory Trick
> **Low TTL = Look again sooner**

---

## High TTL vs Low TTL

| Requirement | Better Choice |
|---|---|
| Reduce Route 53 query traffic | High TTL |
| Reduce DNS query cost | High TTL |
| Stable DNS records | High TTL |
| Change DNS quickly | Low TTL |
| Minimize stale DNS records | Low TTL |
| Migration / cutover | Low TTL |
| Frequent DNS changes | Low TTL |

---

## The TTL Tradeoff

This is the core SAA concept.

### High TTL

Think:

**Cache longer → Query Route 53 less**

But:

**Changes propagate more slowly**

---

### Low TTL

Think:

**Cache less → Query Route 53 more**

But:

**Changes propagate more quickly**

---

## Architecture Thinking

### Scenario 1 — Stable Website

A company's production website has a DNS record that almost never changes.

They want to minimize DNS queries and reduce unnecessary Route 53 traffic.

**Choose → Higher TTL**

Why?

The record is stable, so caching it longer is beneficial.

---

### Scenario 2 — Planned Migration

A company will migrate an application from:

Server A  
↓  
Server B

They need users to begin using the new destination shortly after the DNS record changes.

Before the migration:

**Reduce the TTL**

Why?

DNS resolvers will refresh the record more frequently.

When the destination changes, fewer clients will continue using the old cached value for a long period.

---

## DNS Migration Strategy

This is a useful architecture pattern.

Suppose:

Current Application  
↓  
IP A

Tomorrow, you plan to migrate to:

New Application  
↓  
IP B

If the current TTL is:

24 hours

many DNS resolvers may continue caching IP A long after you change the record.

### Better Strategy

Before the migration:

1. Lower the TTL
2. Wait for existing high-TTL cached records to expire
3. Perform the DNS change
4. Clients begin refreshing more frequently
5. After the migration is stable, increase the TTL again if appropriate

Conceptually:

High TTL  
↓  
Lower TTL before migration  
↓  
Wait for old cache entries to expire  
↓  
Change DNS destination  
↓  
Clients refresh quickly  
↓  
Increase TTL later

> [!tip] Architecture Pattern
> **Before an important DNS cutover → Lower TTL in advance**

---

## TTL and Stale DNS Records

A **stale record** is a cached DNS response that no longer reflects the current record in Route 53.

Example:

Route 53 currently says:

example.com  
↓  
2.2.2.2

But a DNS resolver previously cached:

example.com  
↓  
1.1.1.1

If the TTL has not expired yet, the resolver may continue returning:

1.1.1.1

This is normal DNS caching behavior.

### Important

Changing a Route 53 record does **not necessarily mean every client immediately sees the new value**.

The old DNS response may remain cached until its TTL expires.

---

## TTL and Route 53 Cost

Lower TTL values cause DNS resolvers to query [[Route 53]] more frequently.

Therefore:

Low TTL  
↓  
More DNS queries  
↓  
More Route 53 query traffic  
↓  
Potentially greater cost

High TTL:

High TTL  
↓  
More caching  
↓  
Fewer Route 53 queries  
↓  
Potentially lower cost

### Exam Recognition

If the question asks how to:

> Reduce Route 53 DNS query traffic

Think:

**Increase TTL**

---

## TTL Is Normally Required

For standard Route 53 DNS records:

**TTL is required.**

The important exception is:

**[[Route 53 Alias Records]]**

With Alias Records, you do **not manually configure the TTL**.

AWS manages that behavior for the underlying resource.

This distinction becomes important when comparing:

- Standard DNS records
- CNAME records
- Alias records

---

## TTL vs DNS Routing Policy

Do not confuse these two.

### TTL

Controls:

> **How long is the DNS answer cached?**

### Routing Policy

Controls:

> **Which DNS answer should Route 53 return?**

Example routing policies include:

- Simple
- Weighted
- Latency
- Failover
- Geolocation
- Geoproximity
- Multi-Value

So:

**TTL = How long**

**Routing Policy = Which destination**

---

## Scenario Recognition

### Exam Keywords

Immediately think **TTL** when you see:

- DNS caching
- Cached DNS response
- Stale DNS record
- DNS propagation delay
- Reduce Route 53 queries
- Faster DNS changes
- DNS migration
- DNS cutover
- Cached IP address
- Old DNS response

---

## Exam Traps

### Trap 1 — Changing DNS Is Not Always Immediate

A Route 53 record may be updated immediately in Route 53.

But users may continue using the old destination because DNS resolvers still have the old response cached.

Think:

**Route 53 changed ≠ every DNS cache changed**

TTL controls when those cached responses expire.

---

### Trap 2 — High TTL Means Faster Changes

This is backwards.

**High TTL → slower DNS changes**

because resolvers keep the existing response longer.

**Low TTL → faster DNS changes**

because resolvers ask again sooner.

---

### Trap 3 — Low TTL Reduces DNS Queries

Also backwards.

**Low TTL → more queries**

because cached records expire more frequently.

**High TTL → fewer queries**

because responses remain cached longer.

---

### Trap 4 — TTL Decides Which Server Gets Traffic

TTL does not choose the destination.

That is handled by:

- DNS record values
- [[Route 53 Routing Policies]]

TTL only controls:

**How long the answer is cached**

---

### Trap 5 — Alias Records Use Manually Configured TTL

Standard Route 53 records generally require TTL.

But:

**[[Route 53 Alias Records]] do not allow you to manually set TTL.**

AWS manages the TTL behavior.

---

## Quick Cheat Sheet

| TTL Choice | Effect |
|---|---|
| High TTL | Cache longer |
| High TTL | Fewer Route 53 queries |
| High TTL | Lower DNS query traffic |
| High TTL | Changes seen more slowly |
| High TTL | More chance of stale records |
| Low TTL | Cache for less time |
| Low TTL | More Route 53 queries |
| Low TTL | Changes seen more quickly |
| Low TTL | Better for migrations/cutovers |
| Alias Record | TTL managed automatically |

---

## Master Memory Trick

> [!tip] Master Memory Trick
> **TTL = DNS Memory**
>
> Ask:
>
> **"How long should DNS remember this answer?"**

Remember:

**HIGH TTL**

**Hold the answer**

- Fewer queries
- Lower traffic
- Slower changes

**LOW TTL**

**Look again**

- More queries
- Faster changes
- Less stale data

And for migrations:

> **Lower TTL BEFORE the DNS cutover**

---

## Related Notes

- [[Route 53]]
- [[Route 53 Records]]
- [[Route 53 CNAME vs Alias]]
- [[Route 53 Alias Records]]
- [[Route 53 Routing Policies]]
- [[Route 53 Hosted Zones]]
- [[Route 53 Health Checks]]
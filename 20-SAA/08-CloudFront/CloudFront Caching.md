## What Problem Does It Solve?

[[CloudFront Caching]] reduces latency and origin load by storing copies of content at CloudFront Edge Locations for a period of time.

It solves the problem of:

> **"How can I avoid sending every user request all the way back to the origin?"**

Without caching:

User  
↓  
CloudFront  
↓  
Origin  
↓  
Response

Every request may reach the origin.

With caching:

User  
↓  
CloudFront Edge Location  
↓  
Cached Object  
↓  
Response

> [!tip] Memory Trick
> **CloudFront Cache = Serve nearby instead of going home**

---

## Core Caching Architecture

CloudFront Edge Locations maintain:

**Local Cache**

Architecture:

Origin  
↓  
CloudFront Edge Location  
↓  
Cached Object  
↓  
User

The first request may require CloudFront to retrieve the object from the origin.

Later requests can often be served directly from the Edge Location.

---

# Cache Hit

A:

**Cache Hit**

means CloudFront already has the requested content stored at the Edge Location.

Architecture:

User  
↓  
CloudFront  
↓  
Cache Lookup  
↓  
Object Found ✅  
↓  
Return Object

Benefits:

- Lower latency
- Faster response
- Less traffic to origin
- Reduced origin workload

### Memory Trick

**HIT = CloudFront has it**

---

# Cache Miss

A:

**Cache Miss**

means CloudFront does not currently have a usable cached copy.

Architecture:

User  
↓  
CloudFront  
↓  
Cache Lookup  
↓  
Object Missing ❌  
↓  
Origin  
↓  
Retrieve Object  
↓  
Cache Object  
↓  
Return to User

Future requests may then become:

**Cache Hits**

### Memory Trick

**MISS = Go back to origin**

---

# TTL — Time To Live

Cached objects remain in CloudFront for a:

**TTL**

TTL means:

**Time To Live**

The Maarek slides describe CloudFront files as being cached for a TTL.

Example:

Object Cached  
↓  
TTL = 24 Hours  
↓  
CloudFront Serves Cached Copy  
↓  
TTL Expires  
↓  
CloudFront Checks Origin Again When Needed

> [!tip] Memory Trick
> **TTL = How long CloudFront trusts its cached copy**

---

# Why TTL Matters

A longer TTL means:

- More cache hits
- Less origin traffic
- Better performance
- Potentially older content

A shorter TTL means:

- Fresher content
- More origin requests
- Less caching benefit

### Architecture Tradeoff

Long TTL  
↓  
Performance ↑  
Origin Load ↓  
Freshness ↓

Short TTL  
↓  
Freshness ↑  
Origin Load ↑  
Caching Benefit ↓

---

# Static Content

CloudFront caching is especially useful for:

**Static content**

Examples:

- Images
- Videos
- CSS
- JavaScript
- Documents
- Software downloads

The Maarek slides specifically describe CloudFront as:

**Great for static content that must be available everywhere**

Architecture:

[[S3]]  
↓  
[[CloudFront]]  
↓  
Global Edge Cache  
↓  
Users

---

# Dynamic Content

CloudFront can also deliver:

**Dynamic content**

Not every response must be cached.

Architecture:

User  
↓  
CloudFront  
↓  
Dynamic Request  
↓  
Application Origin

CloudFront may still improve delivery through AWS global infrastructure.

### Exam Trap

Do not think:

> **CloudFront = only static files**

CloudFront can handle:

**Static + Dynamic HTTP/S content**

---

# Cache Freshness

Suppose the origin contains:

`index.html`

CloudFront currently caches:

Version 1

Then you upload:

Version 2

to the origin.

CloudFront does NOT automatically know immediately that the file changed.

It may continue serving:

**Version 1**

until:

**TTL expires**

This is one of the most important CloudFront exam behaviors.

> [!warning] Exam Rule
> **Changing the origin does not instantly refresh CloudFront cache**

---

# Origin Update Example

Initial state:

S3 Origin  
↓  
index.html Version 1

CloudFront  
↓  
Caches Version 1

Then:

S3 Origin  
↓  
index.html Version 2

CloudFront may still serve:

**Version 1**

until:

TTL expiration

or:

[[CloudFront Cache Invalidations]]

---

# Cache Invalidation

If you cannot wait for TTL expiration:

Use:

[[CloudFront Cache Invalidations]]

This forces CloudFront to remove cached content before the TTL naturally expires.

Architecture:

Origin Updated  
↓  
CloudFront Still Has Old Cache  
↓  
Invalidation  
↓  
Cached Object Removed  
↓  
Next Request Fetches New Version

### Memory Trick

**TTL = Wait**

**Invalidation = Force Refresh**

---

# Partial vs Full Invalidation

You can invalidate:

**Specific paths**

Example:

`/index.html`

or:

`/images/*`

You can also invalidate:

**Everything**

using:

`*`

### Exam Thinking

If only one section changed:

Use targeted invalidation.

If the entire distribution needs refreshing:

Use broader invalidation.

---

# CloudFront vs S3 Cross-Region Replication

This comparison appears directly in the Maarek slides and is very exam-friendly.

## CloudFront

Uses:

**Global Edge Network**

Content is:

**Cached**

for a TTL.

Best for:

**Static content that should be available globally**

---

## [[S3 Cross-Region Replication]]

Copies objects between:

**Specific AWS Regions**

Objects are updated:

**Near real-time**

Best when:

You need actual copies in selected Regions.

### Memory Trick

**CloudFront = CACHE everywhere**

**CRR = COPY to chosen Regions**

---

# CloudFront Cache Is Not Replication

This is an important distinction.

CloudFront does not create permanent authoritative copies in every AWS Region.

Instead:

It creates:

**Temporary cached copies at Edge Locations**

The origin remains:

**Source of truth**

### Exam Trap

Do not choose CloudFront if the requirement is:

> **"Maintain permanent replicated objects in another Region."**

Choose:

[[S3 Cross-Region Replication]]

---

# Origin Load Reduction

Caching can dramatically reduce requests reaching the backend.

Without cache:

10,000 Users  
↓  
10,000 Origin Requests

With CloudFront caching:

10,000 Users  
↓  
Edge Cache  
↓  
Far fewer Origin Requests

This can reduce load on:

- [[S3]]
- [[Application Load Balancer]]
- [[EC2]]
- Application servers
- APIs

### Architecture Thinking

If the origin is becoming overloaded by repeated read requests:

Think:

**CloudFront caching**

---

# Global Performance

Caching works because Edge Locations are geographically closer to users.

Architecture:

Origin in U.S.  
↓  
CloudFront Cache in Europe  
↓  
European Users

Instead of:

European User  
↓  
U.S. Origin every time

This improves:

**Read latency**

and:

**User experience**

---

# Cacheable Content Architecture

A common design is:

[[S3]]  
↓  
CloudFront  
↓  
Static Content Cache

and:

Application Backend  
↓  
CloudFront  
↓  
Dynamic Requests

This lets a single distribution handle different types of application content.

---

# Architecture Thinking

## Scenario 1 — Global Images

A company stores product images in S3.

Millions of users worldwide request the same images repeatedly.

**Choose → CloudFront Caching**

Why?

Images are highly cacheable.

---

## Scenario 2 — Origin Overloaded

An application server receives thousands of repeated GET requests for the same content.

The company wants to reduce backend traffic.

**Choose → CloudFront**

Cache repeated responses at Edge Locations.

---

## Scenario 3 — Website Updated but Users See Old Version

A developer uploads a new `index.html`.

Some users still receive the old page.

Why?

CloudFront is serving:

**Cached content**

until TTL expires.

Possible solution:

[[CloudFront Cache Invalidations]]

---

## Scenario 4 — Content Must Refresh Immediately

A critical website update must become visible immediately around the world.

Waiting for TTL is unacceptable.

**Choose → CloudFront Invalidation**

---

## Scenario 5 — Need Permanent Regional Copies

A compliance requirement says S3 objects must physically exist in:

- us-east-1
- eu-west-1

**Do NOT choose → CloudFront caching**

Choose:

[[S3 Cross-Region Replication]]

---

# CloudFront Caching vs ElastiCache

Both involve caching, but they solve different problems.

## CloudFront

Caches:

**HTTP/S content near global users**

Think:

Edge cache

---

## [[ElastiCache]]

Caches:

**Application/database data in memory**

Think:

Backend cache

### Memory Trick

**CloudFront = Front-end / Edge Cache**

**ElastiCache = Back-end / Data Cache**

---

# CloudFront Caching vs DAX

## CloudFront

Caches:

**Web content**

---

## [[DAX]]

Caches:

**DynamoDB reads**

### Exam Decision

Global web content  
→ CloudFront

DynamoDB microsecond reads  
→ DAX

---

# CloudFront Caching vs Browser Cache

Browser caching happens:

**On the user's device**

CloudFront caching happens:

**At AWS Edge Locations**

These can work together.

Architecture:

Origin  
↓  
CloudFront Edge Cache  
↓  
Browser Cache  
↓  
User

---

# Scenario Recognition

## Immediately Think CloudFront Caching When You See

- Global users
- Repeated GET requests
- Static content
- Images
- Videos
- CSS / JavaScript
- Reduce origin traffic
- Edge cache
- Cache Hit
- Cache Miss
- TTL
- Stale CloudFront content
- Improve read performance

### Strongest Exam Pattern

> **"Same content repeatedly accessed by global users"**
>
> → **CloudFront Caching**

---

# Exam Traps

## Trap 1 — CloudFront Contacts Origin for Every Request

False.

A:

**Cache Hit**

can be served directly from the Edge Location.

---

## Trap 2 — Origin Update Immediately Updates CloudFront

False.

Cached content may remain until:

**TTL expires**

or:

**Invalidation occurs**

---

## Trap 3 — CloudFront Cache Is Permanent Replication

False.

CloudFront stores:

**Temporary cached copies**

The origin remains the source of truth.

---

## Trap 4 — Longer TTL Always Better

False.

Longer TTL improves caching but can make content:

**Less fresh**

Architecture decisions must balance:

Performance

vs:

Freshness

---

## Trap 5 — CloudFront Only Caches S3

False.

CloudFront can sit in front of several origins, including:

- S3
- ALB
- EC2
- Other HTTP origins

---

## Trap 6 — Cache Invalidation Changes the Origin

False.

Invalidation removes:

**Cached CloudFront copies**

It does not modify the origin itself.

---

## Trap 7 — CloudFront and CRR Solve the Same Problem

False.

CloudFront:

**Global caching**

CRR:

**Regional replication**

---

# Quick Cheat Sheet

| Requirement | CloudFront Caching |
|---|---|
| Cache at Edge Locations | ✅ |
| Improve Global Reads | ✅ |
| Reduce Origin Requests | ✅ |
| Static Content | Excellent |
| Dynamic Content | Supported |
| Cache Hit | Served from Edge |
| Cache Miss | Fetch from Origin |
| TTL Controls Cache Lifetime | ✅ |
| Origin Update Refreshes Cache Immediately | ❌ |
| Force Refresh Before TTL | Invalidation |
| Permanent Regional Object Copy | ❌ |
| Global Temporary Copies | ✅ |

---

## Master Memory Trick

> [!tip] Master Memory Trick
> **CloudFront Cache = Copy, Clock, Clear**
>
> **COPY**
>
> → CloudFront caches content at the edge
>
> **CLOCK**
>
> → TTL determines how long it stays
>
> **CLEAR**
>
> → Invalidation removes it early

Then:

**HIT**
→ Edge serves it

**MISS**
→ Origin serves it

And remember:

> **CloudFront = CACHE**
>
> **S3 CRR = COPY**

The killer exam behavior:

> **Origin changed but CloudFront still shows old content**
>
> → **TTL or Invalidation**

---

## Related Notes

- [[CloudFront]]
- [[CloudFront Origin Access Control]]
- [[CloudFront Cache Invalidations]]
- [[CloudFront Geo Restriction]]
- [[S3]]
- [[S3 Cross-Region Replication]]
- [[Application Load Balancer]]
- [[EC2]]
- [[ElastiCache]]
- [[DAX]]
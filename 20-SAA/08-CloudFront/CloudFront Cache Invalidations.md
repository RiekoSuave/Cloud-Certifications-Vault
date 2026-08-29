## What Problem Does It Solve?

[[CloudFront Cache Invalidations]] force CloudFront to remove cached content **before its TTL expires**.

They solve the problem of:

> **"I updated the origin, but CloudFront is still serving the old version. How do I refresh it now?"**

Normally:

Origin Updated  
↓  
CloudFront Still Has Cached Copy  
↓  
Wait for TTL  
↓  
CloudFront Fetches New Version

With an invalidation:

Origin Updated  
↓  
Create Invalidation  
↓  
Cached Copy Removed  
↓  
Next Request Fetches Fresh Content

> [!tip] Memory Trick
> **Invalidation = Don't wait for the clock**

---

## Why Stale Content Happens

CloudFront does not continuously check the origin to see whether every cached object has changed.

Suppose:

S3 Origin  
↓  
`index.html` Version 1

CloudFront retrieves and caches:

`index.html` Version 1

Then you update S3:

`index.html` Version 2

CloudFront may continue serving:

**Version 1**

because the cached copy is still valid according to its:

**TTL**

---

# TTL Behavior

[[CloudFront Caching]] stores objects for a:

**Time To Live**

or:

**TTL**

Architecture:

Object Cached  
↓  
TTL Running  
↓  
CloudFront Serves Cached Copy  
↓  
TTL Expires  
↓  
CloudFront Can Retrieve Fresh Version

If you are willing to wait:

**Do nothing**

CloudFront eventually refreshes the content after the TTL expires.

---

# When Invalidation Is Needed

Use:

[[CloudFront Cache Invalidations]]

when:

**Waiting for TTL expiration is unacceptable**

Example:

Critical Website Update  
↓  
Origin Updated  
↓  
Old Page Still Cached  
↓  
Invalidation  
↓  
Fresh Page Retrieved

> [!tip] Exam Pattern
> **Origin changed + users still see old content + update must appear immediately**
>
> → **CloudFront Invalidation**

---

# Full Cache Invalidation

CloudFront can invalidate:

**All cached files**

using:

`*`

Architecture:

CloudFront Cache  
↓  
Invalidate `*`  
↓  
All Matching Cached Content Removed

Use this when:

A large portion of the distribution has changed.

---

# Partial Cache Invalidation

You can also invalidate:

**Specific paths**

Example:

`/index.html`

or:

`/images/*`

Architecture:

CloudFront Cache  
├── index.html
├── images/
├── videos/
└── css/

Invalidate:

`/images/*`

Result:

images/  
↓  
Removed from Cache

Other cached content:

**Can remain**

> [!tip] Memory Trick
> **Specific change = Specific invalidation**

---

# Path Wildcards

A wildcard can invalidate everything beneath a particular path.

Example:

`/images/*`

can target cached objects under:

`/images/`

Conceptually:

`/images/logo.png`

`/images/header.jpg`

`/images/product1.png`

↓  

Invalidated

while unrelated content such as:

`/videos/demo.mp4`

can remain cached.

---

# What Happens After Invalidation?

Invalidation does not directly copy the updated content from the origin into every Edge Location.

Instead:

Cached Object  
↓  
Invalidated  
↓  
Removed / Marked Invalid

Then:

Next Viewer Request  
↓  
CloudFront Cache Miss  
↓  
Origin  
↓  
Retrieve New Object  
↓  
Cache New Version  
↓  
Return to Viewer

### Architecture Thinking

Invalidation causes:

**The next request to fetch fresh content**

---

# Invalidation Does Not Modify the Origin

This is an important distinction.

Invalidation changes:

**CloudFront's cached copy**

It does NOT modify:

- S3 object
- ALB application
- EC2 application
- Original file

Architecture:

Origin  
↓  
Still Source of Truth

CloudFront Cache  
↓  
Invalidation affects this layer

> [!warning] Exam Trap
> **Invalidation clears cache**
>
> It does NOT update the origin.

---

# Invalidation vs TTL

These are two ways CloudFront gets fresh content.

## TTL Expiration

Natural refresh.

Architecture:

Cached Content  
↓  
Wait  
↓  
TTL Expires  
↓  
Fresh Copy Retrieved

Best when:

Immediate freshness is not required.

---

## Cache Invalidation

Manual / explicit refresh.

Architecture:

Cached Content  
↓  
Invalidate  
↓  
TTL Bypassed  
↓  
Fresh Copy Retrieved on next request

Best when:

Content must update:

**Immediately or before TTL expiration**

### Memory Trick

**TTL = WAIT**

**Invalidation = NOW**

---

# Invalidation vs Short TTL

You could configure a very short TTL.

But that causes CloudFront to contact the origin:

**More frequently**

This can reduce caching efficiency.

Alternative:

Keep an appropriate TTL  
↓  
Use invalidation when exceptional updates require immediate freshness

### Architecture Thinking

Longer TTL  
↓  
Better Cache Efficiency

Occasional Critical Update  
↓  
Invalidation

This can be more efficient than setting extremely short TTL values for everything.

---

# Invalidation and S3

A common architecture:

Developer  
↓  
Updates S3 Object  
↓  
CloudFront Cache Still Has Old Object  
↓  
Create Invalidation  
↓  
CloudFront Fetches Updated S3 Object

Example:

`index.html`

Old:

Version 1

S3 Updated:

Version 2

Invalidate:

`/index.html`

Next CloudFront request:

Version 2

---

# Invalidation and Other Origins

Cache invalidation is not limited to:

[[S3]]

CloudFront may use origins such as:

- [[Application Load Balancer]]
- [[EC2]]
- Custom HTTP servers

The same caching principle applies:

Origin Updated  
↓  
CloudFront Cached Version Remains  
↓  
Invalidation if immediate refresh required

---

# Targeted vs Broad Invalidations

## Targeted Invalidation

Example:

`/index.html`

Best when:

Only one object changed.

---

## Directory-Style Invalidation

Example:

`/images/*`

Best when:

Multiple related files changed.

---

## Full Invalidation

Example:

`*`

Best when:

Nearly everything changed.

### Exam Strategy

Prefer understanding:

**Which cached content actually needs refreshing**

rather than automatically invalidating everything.

---

# Architecture Thinking

## Scenario 1 — Updated Homepage

A company updates:

`index.html`

in S3.

CloudFront users still see the previous page.

The new page must appear immediately.

**Choose → Invalidate `/index.html`**

---

## Scenario 2 — Entire Image Library Updated

A website replaces all files under:

`/images/`

The rest of the website did not change.

**Choose → Invalidate `/images/*`**

---

## Scenario 3 — Entire Site Rebuilt

Nearly every cached file changed.

The organization needs CloudFront to stop serving all previous cached versions.

**Choose → Invalidate `*`**

---

## Scenario 4 — Update Can Wait

A non-critical file changes.

Its CloudFront TTL expires in a short period and the business does not require immediate propagation.

**Do NOT necessarily invalidate**

Allow:

**TTL expiration**

to refresh the cache naturally.

---

## Scenario 5 — Origin Changed but Cache Did Not

A developer assumes CloudFront detects S3 updates automatically.

Users still receive old content.

Why?

CloudFront cached the old object according to:

**TTL**

Solution:

Wait for TTL

or:

Use Invalidation

---

# Cache Invalidation vs S3 Versioning

These solve completely different problems.

## [[S3 Versioning]]

Protects:

**Object history inside S3**

Example:

Version 1  
Version 2  
Version 3

---

## CloudFront Invalidation

Controls:

**Which cached version CloudFront serves**

### Memory Trick

**Versioning = S3 history**

**Invalidation = CloudFront freshness**

---

# Cache Invalidation vs S3 Replication

## [[S3 Replication]]

Creates:

**Copies of objects in another bucket**

---

## CloudFront Invalidation

Removes:

**Cached Edge copies**

so fresh content can be fetched.

### Exam Decision

Need another permanent object copy  
→ Replication

Need CloudFront to stop serving stale content  
→ Invalidation

---

# Cache Invalidation vs Browser Cache

CloudFront invalidation affects:

**CloudFront Edge caches**

It does not necessarily remove content already cached:

**Inside the user's browser**

These are separate cache layers.

Architecture:

Origin  
↓  
CloudFront Cache  
↓  
Browser Cache

### Exam Thinking

CloudFront Invalidation:

Targets:

**CloudFront**

not every downstream client cache.

---

# Scenario Recognition

## Immediately Think CloudFront Invalidation When You See

- Stale CloudFront content
- Origin updated
- Users see old file
- Cannot wait for TTL
- Force refresh
- Refresh Edge cache
- Invalidate `*`
- Invalidate `/images/*`
- Immediate content update

### Strongest Exam Pattern

> **"CloudFront is serving an old version after the origin was updated."**
>
> → **Cache Invalidation**

---

# Exam Traps

## Trap 1 — CloudFront Automatically Detects Origin Changes

False.

CloudFront may continue serving the cached object until:

**TTL expiration**

---

## Trap 2 — Invalidation Updates the Origin

False.

It affects:

**CloudFront cache**

not the origin.

---

## Trap 3 — You Must Invalidate the Entire Distribution

False.

You can invalidate:

**Specific files or paths**

Example:

`/images/*`

---

## Trap 4 — Invalidation Permanently Disables Caching

False.

After invalidation:

CloudFront can fetch and cache the new content again.

---

## Trap 5 — Invalidation Is Required for Every Origin Change

False.

If waiting for TTL expiration is acceptable:

No invalidation is required.

---

## Trap 6 — Invalidation and TTL Are the Same

False.

TTL:

**Natural expiration**

Invalidation:

**Forced early expiration**

---

# Quick Cheat Sheet

| Requirement | Best Choice |
|---|---|
| Wait for cached content to refresh naturally | TTL |
| Refresh before TTL expires | Invalidation |
| Refresh one file | `/index.html` |
| Refresh path | `/images/*` |
| Refresh everything | `*` |
| Origin updated but CloudFront stale | Invalidation |
| Invalidation modifies origin | ❌ |
| Content can be cached again afterward | ✅ |
| Permanent regional copy | S3 Replication |

---

## Master Memory Trick

> [!tip] Master Memory Trick
> **CloudFront Invalidation = Evict the old copy**
>
> Origin says:
>
> **"I have Version 2."**
>
> CloudFront says:
>
> **"I'm still holding Version 1 until my TTL ends."**
>
> Invalidation says:
>
> **"Throw Version 1 away now."**

Remember:

**TTL**
→ Wait for expiration

**Invalidation**
→ Force expiration

Then:

**One file**
→ `/index.html`

**One section**
→ `/images/*`

**Everything**
→ `*`

The killer exam phrase:

> **Updated origin + stale CloudFront + can't wait**
>
> → **INVALIDATE**

---

## Related Notes

- [[CloudFront]]
- [[CloudFront Caching]]
- [[CloudFront Origin Access Control]]
- [[CloudFront Geo Restriction]]
- [[S3]]
- [[S3 Versioning]]
- [[S3 Replication]]
- [[Application Load Balancer]]
- [[EC2]]
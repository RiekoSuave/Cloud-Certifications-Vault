## What Problem Does It Solve?

[[CloudFront Geo Restriction]] controls access to a CloudFront distribution based on the viewer's:

**Country**

It solves the problem of:

> **"How can I allow or block CloudFront content based on where the user is located?"**

Think:

User  
↓  
CloudFront  
↓  
Geo-IP Check  
↓  
Country Allowed?  
├── Yes → Serve Content
└── No → Block Access

> [!tip] Memory Trick
> **Geo Restriction = Country Gate**

---

## How CloudFront Determines Location

CloudFront determines the viewer's country using:

**Geo-IP information**

The Maarek slides specify that the country is determined using a:

**Third-party Geo-IP database**

Architecture:

Viewer IP Address  
↓  
Geo-IP Lookup  
↓  
Country Determined  
↓  
Allowlist / Blocklist Check

---

# Two Geo Restriction Modes

CloudFront supports two main approaches:

1. **Allowlist**
2. **Blocklist**

---

# Allowlist

An:

**Allowlist**

means:

> Only users from approved countries may access the distribution.

Architecture:

Allowed Country  
↓  
CloudFront  
↓  
Content ✅

Unlisted Country  
↓  
CloudFront  
↓  
Blocked ❌

### Example

Approved countries:

- United States
- Canada
- United Kingdom

Users from those countries:

**Allowed**

Users from all other countries:

**Blocked**

### Memory Trick

**Allowlist = Everyone blocked EXCEPT the list**

---

# Blocklist

A:

**Blocklist**

means:

> Users from specific countries are denied access.

Architecture:

Normal Country  
↓  
CloudFront  
↓  
Content ✅

Blocked Country  
↓  
CloudFront  
↓  
Denied ❌

### Example

Blocked countries:

- Country A
- Country B

Users from those countries:

**Blocked**

Everyone else:

**Allowed**

### Memory Trick

**Blocklist = Everyone allowed EXCEPT the list**

---

# Allowlist vs Blocklist

| Requirement | Use |
|---|---|
| Only approved countries may access | Allowlist |
| Specific countries must be denied | Blocklist |
| Most countries should be blocked | Allowlist |
| Most countries should be allowed | Blocklist |

> [!tip] Fast Exam Trick
> **ONLY these countries**
>
> → Allowlist
>
> **EVERYWHERE except these countries**
>
> → Blocklist

---

# Common Use Case — Copyright Restrictions

The Maarek slides specifically highlight:

**Copyright laws**

as a major Geo Restriction use case.

Example:

A streaming company has distribution rights for a movie only in:

- United States
- Canada

Architecture:

U.S. / Canada Viewer  
↓  
CloudFront  
↓  
Allowed ✅

Other Country  
↓  
CloudFront  
↓  
Blocked ❌

Use:

**Allowlist**

---

# Content Licensing

Geo Restriction is useful when content licenses differ by country.

Examples:

- Movies
- Sports broadcasts
- Music
- Digital publications
- Software distribution

### Architecture Thinking

Requirement:

> **"Users outside licensed countries must not access this content."**

Think:

[[CloudFront Geo Restriction]]

---

# Geo Restriction Happens at CloudFront

The restriction applies at the:

**CloudFront distribution**

This means requests can be blocked before reaching:

**The origin**

Architecture:

Blocked Viewer  
↓  
CloudFront Edge  
↓  
Geo Restriction  
↓  
DENIED

Origin:

**Not contacted**

This helps keep geographic access control close to the viewer.

---

# Geo Restriction + Private S3

A secure content-distribution architecture may look like:

Viewer  
↓  
CloudFront  
↓  
Geo Restriction  
↓  
[[CloudFront Origin Access Control]]  
↓  
Private [[S3]]

This combines:

**Country-based viewer restriction**

with:

**Private origin protection**

---

# Geo Restriction + Signed URLs

Geo Restriction can also be combined with:

[[CloudFront Signed URLs]]

Example requirement:

- User must be authenticated
- User must have a valid signed URL
- User must be in an approved country

Architecture:

Viewer  
↓  
Signed URL Check  
↓  
Geo Restriction  
↓  
CloudFront  
↓  
Private Origin

### Architecture Lesson

These controls solve different problems.

**Signed URL**
→ Who is authorized?

**Geo Restriction**
→ Where are they located?

---

# Geo Restriction + Signed Cookies

The same concept applies to:

[[CloudFront Signed Cookies]]

Signed Cookies can control:

**Viewer authorization**

Geo Restriction controls:

**Viewer country**

They can work together.

---

# Geo Restriction vs WAF

These are easy to confuse.

## CloudFront Geo Restriction

Simple country-based access control.

Think:

**Country Allowlist / Blocklist**

---

## [[06-Security/WAF]]

Provides more flexible request filtering.

Can inspect things such as:

- IP addresses
- HTTP headers
- URI paths
- Query strings
- Request patterns

### Exam Decision

**Simple country restriction**
→ CloudFront Geo Restriction

**Complex web filtering**
→ WAF

---

# Geo Restriction vs Route 53 Geolocation Routing

This is an important exam distinction.

## CloudFront Geo Restriction

Purpose:

**ALLOW or BLOCK content**

Question:

> Should this country be allowed to access the distribution?

---

## [[Route 53 Geolocation Routing]]

Purpose:

**Route users to different endpoints based on geographic location**

Question:

> Which endpoint should this user receive?

### Memory Trick

**CloudFront Geo = BLOCK**

**Route 53 Geo = ROUTE**

---

# Geo Restriction vs Route 53 Latency Routing

[[Route 53 Latency-Based Routing]] chooses an endpoint based on:

**Lowest network latency**

Geo Restriction does not choose the fastest Region.

It simply determines:

**Allowed or blocked**

### Exam Trap

Do not choose Geo Restriction when the question asks:

> **"Route users to the Region with the lowest latency."**

Think:

[[Route 53 Latency-Based Routing]]

---

# Geo Restriction vs Global Accelerator

[[05-Networking/Global Accelerator]] improves:

**Global network performance**

Geo Restriction controls:

**Country access**

These are unrelated architecture goals.

### Memory Trick

**Geo Restriction = Permission by location**

**Global Accelerator = Performance by network path**

---

# Architecture Thinking

## Scenario 1 — Streaming Rights

A video provider is licensed to distribute content only in:

- United States
- Canada

Users from every other country must be blocked.

**Choose → CloudFront Allowlist**

Allow only:

United States  
Canada

---

## Scenario 2 — Ban Several Countries

An application is globally available except in three countries because of legal restrictions.

**Choose → CloudFront Blocklist**

Block those countries.

Allow everyone else.

---

## Scenario 3 — Route European Users to Europe

A company wants European users routed to a European application endpoint.

**Do NOT choose → CloudFront Geo Restriction**

Choose:

[[Route 53 Geolocation Routing]]

if geographic routing is the requirement.

---

## Scenario 4 — Lowest-Latency Region

Users should automatically connect to whichever AWS Region provides the lowest latency.

**Do NOT choose → Geo Restriction**

Think:

[[Route 53 Latency-Based Routing]]

or another global routing architecture.

---

## Scenario 5 — Private Content + Country Restriction

A company stores premium videos in private S3.

Only users in approved countries may access them.

Architecture:

Viewer  
↓  
CloudFront Geo Restriction  
↓  
CloudFront  
↓  
[[CloudFront Origin Access Control]]  
↓  
Private S3

---

# Scenario Recognition

## Immediately Think CloudFront Geo Restriction When You See

- Country restriction
- Copyright laws
- Licensing restrictions
- Approved countries
- Banned countries
- Allowlist
- Blocklist
- Geo-IP
- Restrict distribution by country

### Strongest Exam Pattern

> **"Allow or deny CloudFront content based on the viewer's country."**
>
> → **CloudFront Geo Restriction**

---

# Exam Traps

## Trap 1 — Geo Restriction Routes Users to Different Regions

False.

It:

**Allows or blocks**

It does not perform geographic endpoint routing.

---

## Trap 2 — Allowlist Means Listed Countries Are Blocked

False.

Allowlist means:

**Only listed countries are allowed**

---

## Trap 3 — Blocklist Means Only Listed Countries Are Allowed

False.

Blocklist means:

**Listed countries are denied**

Everyone else remains allowed.

---

## Trap 4 — Geo Restriction Uses the User's AWS Region

False.

CloudFront determines the user's country using:

**Geo-IP**

---

## Trap 5 — Geo Restriction and WAF Are Identical

False.

Geo Restriction provides:

**Simple country-level controls**

WAF provides:

**More flexible HTTP/S request filtering**

---

## Trap 6 — Geo Restriction Protects S3 from Direct Access

Not by itself.

Use:

[[CloudFront Origin Access Control]]

to keep the S3 origin private.

Otherwise, users might bypass CloudFront if the S3 object itself is publicly accessible.

---

# Quick Cheat Sheet

| Requirement | Best Choice |
|---|---|
| Only approved countries allowed | Allowlist |
| Specific countries denied | Blocklist |
| Country determined by | Geo-IP |
| Copyright restriction | Geo Restriction |
| Content licensing | Geo Restriction |
| Route by user location | Route 53 Geolocation |
| Route to lowest latency | Route 53 Latency Routing |
| Protect private S3 origin | OAC |
| More advanced request filtering | WAF |

---

## Master Memory Trick

> [!tip] Master Memory Trick
> **CloudFront Geo Restriction = Bouncer with a Country List**
>
> Viewer arrives.
>
> CloudFront asks:
>
> **"Which country are you coming from?"**
>
> Then:
>
> **ALLOWLIST**
>
> → You're only coming in if your country is on the list.
>
> **BLOCKLIST**
>
> → You're coming in unless your country is on the banned list.

Remember:

> **CloudFront Geo = ALLOW / BLOCK**
>
> **Route 53 Geo = ROUTE**

And the killer exam clue:

> **Copyright / licensing by country**
>
> → **CloudFront Geo Restriction**

---

## Related Notes

- [[CloudFront]]
- [[CloudFront Caching]]
- [[CloudFront Origin Access Control]]
- [[CloudFront Signed URLs]]
- [[CloudFront Signed Cookies]]
- [[06-Security/WAF]]
- [[Route 53]]
- [[Route 53 Geolocation Routing]]
- [[Route 53 Latency-Based Routing]]
- [[05-Networking/Global Accelerator]]
- [[S3]]
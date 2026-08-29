## What Problem Does It Solve?

[[Route 53 Weighted Routing]] lets you control **what percentage of DNS responses should point to each resource**.

It solves the problem of:

> **"How can I gradually split traffic between multiple versions, Regions, or endpoints?"**

Example:

Version A → Weight 80  
Version B → Weight 20

Route 53 will return Version A more often than Version B based on those relative weights.

> [!tip] Memory Trick
> **Weighted = Percentage Split**
>
> If the exam says:
>
> **10%, 20%, 80%, gradual migration, canary, blue/green**
>
> Think → [[Route 53 Weighted Routing]]

---

## How Weighted Routing Works

Each DNS record is assigned a:

**Relative Weight**

Example:

app.example.com

Record A:

Weight 70

Record B:

Weight 20

Record C:

Weight 10

Conceptually:

[[Route 53]]  
↓  
70% → Resource A  
20% → Resource B  
10% → Resource C

The higher the relative weight, the more often Route 53 returns that record in DNS responses.

---

## Weights Are Relative

This is important.

Weights do **not** need to add up to 100.

Example:

Resource A → Weight 7  
Resource B → Weight 2  
Resource C → Weight 1

Total weight:

10

So the approximate traffic distribution is:

Resource A → 70%

Resource B → 20%

Resource C → 10%

Another example:

Resource A → Weight 70  
Resource B → Weight 20  
Resource C → Weight 10

The relative proportions are the same.

> [!tip] Memory Trick
> **Weights are ratios, not required percentages.**

---

## Traffic Distribution Formula

Conceptually:

Traffic Share  
=  
Resource Weight  
÷  
Total Weight of All Records

Example:

Resource A = 70  
Resource B = 20  
Resource C = 10

Total:

100

So:

A → 70%

B → 20%

C → 10%

If instead:

A = 7  
B = 2  
C = 1

The result is still:

A → 70%

B → 20%

C → 10%

---

## DNS Records Must Match

For Weighted Routing, the DNS records must have the same:

- Record name
- Record type

Example:

app.example.com → A → Resource A

app.example.com → A → Resource B

app.example.com → A → Resource C

You would not normally mix:

app.example.com → A

with:

other.example.com → AAAA

inside the same weighted routing decision.

---

## Weighted Routing and Health Checks

Weighted records **can be associated with [[Route 53 Health Checks]]**.

This allows Route 53 to avoid returning unhealthy resources.

Architecture:

[[Route 53 Health Checks]]  
↓  
Resource Health  
↓  
[[Route 53 Weighted Routing]]  
↓  
Weighted DNS Responses

This makes Weighted Routing useful when you need both:

- Traffic distribution
- Health awareness

---

## Common Use Case — Testing a New Application Version

This is one of the strongest exam patterns.

Suppose:

Version 1 = Stable production

Version 2 = New release

You want:

90% → Version 1  
10% → Version 2

Architecture:

Users  
↓  
[[Route 53]]  
↓  
├── Weight 90 → Version 1  
└── Weight 10 → Version 2

This allows a small percentage of users to test the new version.

### This Is a Canary-Style Deployment

You can then gradually change the weights:

90 / 10  
↓  
70 / 30  
↓  
50 / 50  
↓  
0 / 100

until the new application receives all traffic.

> [!tip] Architecture Pattern
> **Gradual deployment → Weighted Routing**

---

## Common Use Case — Blue/Green Deployment

Suppose:

Blue = Current production

Green = New environment

Initially:

Blue → Weight 100  
Green → Weight 0

Then:

Blue → 90  
Green → 10

Later:

Blue → 50  
Green → 50

Finally:

Blue → 0  
Green → 100

This provides controlled DNS-based migration.

### Memory Trick

**Weighted Routing = Traffic Dimmer Switch**

You can slowly turn one environment down while turning another up.

---

## Common Use Case — Multi-Region Distribution

Weighted Routing can also distribute traffic between Regions.

Example:

us-east-1 → Weight 70

eu-west-1 → Weight 30

Architecture:

Users  
↓  
[[Route 53]]  
↓  
├── 70% → us-east-1  
└── 30% → eu-west-1

Important:

This is based on **configured weights**, not latency.

If you want users sent to the Region with the best network performance:

Choose → [[Route 53 Latency Routing]]

---

## Weight of Zero

A very important exam detail:

You can assign:

**Weight = 0**

to a resource.

This effectively stops Route 53 from sending traffic to that resource when other weighted records have nonzero weights.

Example:

Resource A → Weight 80  
Resource B → Weight 20  
Resource C → Weight 0

Result:

Resource C effectively receives no weighted traffic.

### Useful For

- Temporarily disabling an environment
- Removing a version from traffic
- Preparing an endpoint before activation
- Blue/green deployments

---

## What Happens If All Weights Are Zero?

This is an easy detail to miss.

If:

Resource A → 0

Resource B → 0

Resource C → 0

Then Route 53 returns the records **equally**.

So:

All weights zero  
≠  
No traffic

Instead:

All weights zero  
→  
Equal distribution

> [!warning] Exam Trap
> **Weight 0 stops traffic only when other records have nonzero weights.**
>
> If all records are 0, Route 53 treats them equally.

---

## Architecture Thinking

### Scenario 1 — 90/10 New Version Test

A company wants:

90% → Current application  
10% → New application

**Choose → [[Route 53 Weighted Routing]]**

Why?

The requirement explicitly defines a traffic percentage.

---

### Scenario 2 — Gradual Migration Between Regions

A company currently serves all users from:

us-east-1

They are migrating to:

us-west-2

They want to gradually shift traffic:

100 / 0  
↓  
80 / 20  
↓  
50 / 50  
↓  
0 / 100

**Choose → Weighted Routing**

---

### Scenario 3 — Active-Passive Disaster Recovery

A company wants:

Primary Region  
↓ if unhealthy  
Secondary Region

**Do NOT choose → Weighted Routing**

Choose:

[[Route 53 Failover Routing]]

Why?

The requirement is primary/secondary failover, not percentage-based traffic splitting.

---

### Scenario 4 — Best Performing Region

A global application runs in several AWS Regions.

Users should automatically be sent to the Region with the lowest network latency.

**Do NOT choose → Weighted Routing**

Choose:

[[Route 53 Latency Routing]]

---

### Scenario 5 — Temporarily Disable One Version

A company has:

Version A → Weight 90

Version B → Weight 10

They want Version B to stop receiving traffic temporarily.

Set:

Version B → Weight 0

---

## Weighted Routing and DNS Caching

Remember:

Route 53 Weighted Routing operates at the **DNS level**.

It does not control every individual HTTP request.

Example:

Client asks DNS  
↓  
Route 53 returns Version A  
↓  
DNS answer is cached based on [[Route 53 TTL]]  
↓  
Client may keep using Version A until the cache expires

Therefore:

**Weighted percentages are approximate over DNS queries**

not exact per-request percentages.

> [!warning] Exam Trap
> **Weighted Routing is not application-request load balancing.**

---

## Weighted Routing vs Load Balancer

### Weighted Routing

Operates at:

**DNS level**

Controls:

**Which endpoint is returned**

Good for:

- Regions
- Versions
- Environments
- DNS-based migrations

### [[Elastic Load Balancing]]

Operates at:

**Application/network traffic level**

Distributes actual incoming connections or requests across targets.

### Memory Trick

**Route 53 Weighted = DNS split**

**ELB = Request/connection split**

---

## Weighted vs Failover

### Weighted

Both endpoints may receive traffic simultaneously.

Example:

80 / 20

### Failover

Normally:

Primary = Active

Secondary = Standby

### Exam Decision

**Percentages → Weighted**

**Primary/Backup → Failover**

---

## Weighted vs Latency

### Weighted

Decision based on:

**Configured weight**

Example:

70 / 30

### Latency

Decision based on:

**Lowest network latency**

### Exam Decision

**Business wants exact relative traffic control → Weighted**

**Business wants best user performance → Latency**

---

## Weighted vs Geolocation

### Weighted

Does not care where the user is located.

It uses:

**Relative weights**

### Geolocation

Uses:

**User location**

Example:

Germany → Endpoint A

Canada → Endpoint B

### Memory Trick

**Weighted = How much**

**Geolocation = From where**

---

## Scenario Recognition

### Immediately Think Weighted Routing When You See

- Percentage
- Relative weight
- Traffic split
- 90/10
- 80/20
- Canary deployment
- Blue/green deployment
- New version testing
- Gradual migration
- Shift traffic progressively
- Load balancing between Regions by percentage

---

## Exam Traps

### Trap 1 — Weights Must Add Up to 100

False.

Weights are relative.

Example:

7 / 2 / 1

works just like:

70 / 20 / 10

---

### Trap 2 — Weight 0 Always Means No Traffic

Not always.

If at least one other record has a nonzero weight:

**Weight 0 → No weighted traffic**

But if:

**All weights = 0**

Route 53 returns all records equally.

---

### Trap 3 — Weighted Routing Guarantees Exact Request Percentages

False.

Weighted Routing works through DNS responses.

Because of DNS caching and [[Route 53 TTL]], the real application request distribution may not be mathematically exact.

---

### Trap 4 — Weighted Routing Chooses the Lowest-Latency Region

False.

That is:

[[Route 53 Latency Routing]]

Weighted Routing follows:

**configured weights**

---

### Trap 5 — Weighted Routing Is Only for Regions

False.

It can also be used for:

- Application versions
- Canary testing
- Blue/green deployments
- Gradual migrations
- Multiple resources

---

### Trap 6 — Weighted Records Cannot Use Health Checks

False.

Weighted Routing **can be associated with [[Route 53 Health Checks]]**.

---

## Quick Cheat Sheet

| Feature | Weighted Routing |
|---|---|
| Purpose | Percentage-based DNS distribution |
| Weight Type | Relative |
| Must Total 100 | ❌ |
| Same Name Required | ✅ |
| Same Record Type Required | ✅ |
| Health Checks | ✅ |
| Weight 0 | Stops traffic if others are nonzero |
| All Weights 0 | Equal distribution |
| Canary Deployment | ✅ |
| Blue/Green Deployment | ✅ |
| Regional Traffic Split | ✅ |
| Exact Per-Request Distribution | ❌ |
| DNS-Level Routing | ✅ |

---

## Master Memory Trick

> [!tip] Master Memory Trick
> **Weighted = Traffic Percentage Knob**
>
> Ask:
>
> **"How much traffic should each destination receive?"**

Remember:

**90 / 10 → Weighted**

**50 / 50 → Weighted**

**Gradual migration → Weighted**

**Canary → Weighted**

**Blue/Green → Weighted**

And:

**Weights are RELATIVE**

not required to total 100.

One sneaky exam rule:

> **All weights = 0 → Equal distribution**

---

## Related Notes

- [[Route 53]]
- [[Route 53 Routing Policies]]
- [[Route 53 Simple Routing]]
- [[Route 53 Latency Routing]]
- [[Route 53 Failover Routing]]
- [[Route 53 Health Checks]]
- [[Route 53 TTL]]
- [[Elastic Load Balancing]]
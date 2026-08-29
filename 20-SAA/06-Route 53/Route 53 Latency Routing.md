## What Problem Does It Solve?

[[Route 53 Latency Routing]] sends users to the AWS Region that provides the **lowest network latency**.

It solves the problem of:

> **"Which Region should this user connect to for the best network performance?"**

Example:

User  
↓  
[[Route 53]]  
↓  
Compare latency to available Regions  
↓  
Return lowest-latency endpoint

> [!tip] Memory Trick
> **Latency Routing = Fastest Region**
>
> If the exam emphasizes:
>
> **lowest latency, best performance, fastest response**
>
> Think → [[Route 53 Latency Routing]]

---

## How Latency Routing Works

Suppose an application runs in:

- us-east-1
- eu-west-1
- ap-southeast-1

A user performs a DNS query:

app.example.com?

[[Route 53]] evaluates which AWS Region provides the lowest latency for that user.

Conceptually:

User  
↓  
[[Route 53]]  
↓  
Compare Regional Latency  
↓  
Lowest-Latency Region Returned  
↓  
User Connects to Application

Important:

Route 53 does **not** carry the application traffic.

It simply returns the DNS answer.

---

## Latency Is Based on Network Performance

Latency Routing is based on the network latency between:

**Users ↔ AWS Regions**

This is not the same as geographic distance.

For example:

A user located in Germany might actually be routed to a resource in the United States if that Region currently provides lower network latency.

That means:

**Closer geographically ≠ always faster**

> [!tip] Memory Trick
> **Latency = Network Speed, not Map Distance**

---

## Architecture Thinking

Imagine:

Application Stack A  
↓  
us-east-1

Application Stack B  
↓  
eu-west-1

Application Stack C  
↓  
ap-southeast-1

A user asks:

app.example.com?

Route 53 determines:

Which Region provides the best latency?

Then returns that Region's resource.

Example:

User  
↓  
[[Route 53]]  
↓  
eu-west-1 provides lowest latency  
↓  
Return European endpoint  
↓  
User connects directly

---

## Common Architecture Pattern

A typical global architecture:

Users Worldwide  
↓  
[[Route 53 Latency Routing]]  
↓  
├── [[Application Load Balancer]] → us-east-1  
├── [[Application Load Balancer]] → eu-west-1  
└── [[Application Load Balancer]] → ap-southeast-1

Each Region contains its own application stack.

Example:

[[Application Load Balancer]]  
↓  
[[Auto Scaling]]  
↓  
[[EC2]]

Route 53 chooses which **regional endpoint** users should receive.

---

## Latency Routing and Health Checks

Latency Routing can be associated with:

[[Route 53 Health Checks]]

This gives the architecture a failover capability.

Example:

User  
↓  
[[Route 53]]  
↓  
Check latency + resource health  
↓  
Return best healthy Region

Suppose:

eu-west-1 = Lowest latency

But:

eu-west-1 = Unhealthy

Route 53 can avoid returning that unhealthy endpoint and instead return another healthy Region.

### Architecture Thinking

Without health checks:

**Lowest latency wins**

With health checks:

**Lowest-latency healthy resource wins**

> [!tip] Memory Trick
> **Latency + Health Check = Fast AND Healthy**

---

## Architecture Thinking

### Scenario 1 — Global Low-Latency Application

A company runs its application in:

- North America
- Europe
- Asia

Users should automatically connect to whichever AWS Region provides the lowest network latency.

**Choose → [[Route 53 Latency Routing]]**

---

### Scenario 2 — European User May Go to US

A user in Germany accesses an application.

The U.S. Region currently provides lower measured network latency than the European Region.

Which endpoint may Route 53 return?

**The U.S. Region**

Why?

Latency Routing chooses:

**lowest network latency**

not:

**closest geographic Region**

---

### Scenario 3 — Regional Endpoint Failure

A company uses Latency Routing with applications in multiple Regions.

The lowest-latency Region becomes unhealthy.

The company wants users to be sent to another healthy Region.

**Choose → Latency Routing + [[Route 53 Health Checks]]**

---

### Scenario 4 — Country-Specific Website

A company wants:

German users → German website  
French users → French website  
Canadian users → Canadian website

The requirement is based specifically on **user location**, not performance.

**Do NOT choose → Latency Routing**

Choose:

[[Route 53 Geolocation Routing]]

---

### Scenario 5 — 80/20 Regional Split

A company wants:

80% → us-east-1  
20% → eu-west-1

The requirement is based on a configured percentage.

**Do NOT choose → Latency Routing**

Choose:

[[Route 53 Weighted Routing]]

---

## Latency vs Weighted

### Latency Routing

Decision based on:

**Network performance**

Question:

> Which Region is fastest for this user?

### Weighted Routing

Decision based on:

**Configured relative weights**

Question:

> What percentage of DNS responses should go to each resource?

### Memory Trick

**Latency = Fastest**

**Weighted = Percentage**

---

## Latency vs Geolocation

This is one of the biggest Route 53 exam traps.

### Latency Routing

Based on:

**Network latency**

User location itself does not directly determine the answer.

### Geolocation Routing

Based on:

**Where the user is located**

Example:

Germany → Endpoint A

Canada → Endpoint B

### Exam Decision

If the requirement says:

**Best performance / lowest latency → Latency**

If the requirement says:

**Country / continent / state → Geolocation**

---

## Latency vs Geoproximity

These sound similar, but they solve different problems.

### Latency Routing

Uses:

**Measured network latency**

Goal:

**Best application performance**

### Geoproximity Routing

Uses:

**Geographic location of users and resources**

and can influence routing with:

**Bias**

Goal:

**Control geographic traffic distribution**

### Memory Trick

**Latency = Network**

**Geoproximity = Geography**

---

## Latency Routing and DNS Caching

Remember that this is still DNS.

Route 53 returns the lowest-latency endpoint.

The DNS result can then be cached according to:

[[Route 53 TTL]]

Conceptually:

Client  
↓  
[[Route 53]]  
↓  
Lowest-Latency Endpoint  
↓  
DNS Resolver Caches Answer  
↓  
Client Uses Cached Endpoint

Therefore:

Route 53 is not continuously reevaluating latency for every HTTP request.

The routing decision occurs during DNS resolution.

---

## Scenario Recognition

### Immediately Think Latency Routing When You See

- Lowest latency
- Best performance
- Global application
- Multiple AWS Regions
- Minimize user latency
- Fastest Region
- Performance-based routing
- User experience is the priority

### Strongest Keyword

> **Lowest Latency → Latency-Based Routing**

---

## Exam Traps

### Trap 1 — Closest Region Means Lowest Latency

False.

A geographically close Region may not provide the best network performance.

Route 53 uses:

**Latency between the user and AWS Regions**

---

### Trap 2 — Latency Routing Uses User Country Rules

False.

That is:

[[Route 53 Geolocation Routing]]

Latency Routing is performance based.

---

### Trap 3 — Latency Routing Cannot Fail Over

False.

Latency records can be associated with:

[[Route 53 Health Checks]]

This allows unhealthy endpoints to be excluded.

---

### Trap 4 — Latency Routing Routes Every HTTP Request

False.

It operates at the DNS layer.

Route 53 returns the endpoint.

The client then communicates directly with the application.

---

### Trap 5 — Latency Routing Splits Traffic by Percentage

False.

That is:

[[Route 53 Weighted Routing]]

Latency Routing chooses based on network performance.

---

### Trap 6 — Latency Routing Requires One Region

That would defeat the purpose.

Latency Routing is especially useful when the same application is deployed across **multiple AWS Regions**.

---

## Quick Cheat Sheet

| Feature | Latency Routing |
|---|---|
| Primary Goal | Lowest network latency |
| Best For | Global applications |
| Decision Based On | User ↔ AWS Region latency |
| Geographic Distance | Not necessarily |
| Multiple Regions | ✅ |
| Health Checks | ✅ |
| Failover Capability | ✅ |
| Percentage-Based | ❌ |
| Country-Based | ❌ |
| DNS-Level Decision | ✅ |

---

## Master Memory Trick

> [!tip] Master Memory Trick
> **Latency = Fastest Route 53 Answer**
>
> Ask:
>
> **"Which AWS Region gives this user the best network performance?"**

Remember:

**Percentage → Weighted**

**Primary / Backup → Failover**

**Fastest Region → Latency**

**User Location → Geolocation**

**Distance + Bias → Geoproximity**

And the sneaky exam rule:

> **The geographically closest Region does NOT have to be the lowest-latency Region.**

---

## Related Notes

- [[Route 53]]
- [[Route 53 Routing Policies]]
- [[Route 53 Weighted Routing]]
- [[Route 53 Failover Routing]]
- [[Route 53 Geolocation Routing]]
- [[Route 53 Geoproximity Routing]]
- [[Route 53 Health Checks]]
- [[Route 53 TTL]]
- [[Application Load Balancer]]
- [[Auto Scaling]]
- [[EC2]]
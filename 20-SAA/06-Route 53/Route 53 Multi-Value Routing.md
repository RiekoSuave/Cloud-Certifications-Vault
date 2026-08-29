## What Problem Does It Solve?

[[Route 53 Multi-Value Routing]] lets Route 53 return **multiple healthy resources in a single DNS response**.

It solves the problem of:

> **"How can I return several healthy endpoints instead of only one?"**

Example:

app.example.com  
↓  
[[Route 53]]  
↓  
Returns multiple healthy IP addresses  
↓  
Client chooses one

> [!tip] Memory Trick
> **Multi-Value = Many Healthy Answers**
>
> If the exam says:
>
> **multiple healthy records, several IPs, health-aware DNS**
>
> Think → [[Route 53 Multi-Value Routing]]

---

## How Multi-Value Routing Works

Suppose you have several public application endpoints:

- Server A
- Server B
- Server C
- Server D

Each endpoint has its own Route 53 record.

Example:

app.example.com → 1.1.1.1

app.example.com → 2.2.2.2

app.example.com → 3.3.3.3

app.example.com → 4.4.4.4

Route 53 can return several of these values in the DNS response.

Architecture:

Client  
↓  
DNS Query  
[[Route 53]]  
↓  
Multiple Healthy Records  
↓  
Client chooses one endpoint

---

## Health Checks

Multi-Value records can be associated with:

[[Route 53 Health Checks]]

This is one of the biggest differences between:

[[Route 53 Simple Routing]]

and:

[[Route 53 Multi-Value Routing]]

### With Health Checks

Server A → Healthy

Server B → Healthy

Server C → Unhealthy

Server D → Healthy

Route 53 can return:

- Server A
- Server B
- Server D

while excluding:

- Server C

> [!tip] Architecture Thinking
> **Multi-Value = Return several answers, but only healthy ones**

---

## Up to 8 Healthy Records Per Query

For each Multi-Value DNS query, Route 53 can return:

**Up to 8 healthy records**

Example:

You have:

12 healthy servers

Route 53 does not return all 12 in one Multi-Value response.

It can return:

**Up to 8**

### Memory Trick

**Multi-Value Magic Number = 8**

---

## Multi-Value Is Not an ELB

This is a major exam trap.

[[Route 53 Multi-Value Routing]] is **not a replacement for [[Elastic Load Balancing]]**.

Why?

Because Route 53 operates at the:

**DNS layer**

It returns multiple DNS answers.

An ELB operates at the:

**Application / Network traffic layer**

and actively distributes requests or connections across backend targets.

---

## Multi-Value vs ELB

### Multi-Value

Route 53 says:

> "Here are several healthy endpoints."

Then the client chooses one.

Architecture:

Client  
↓  
[[Route 53]]  
↓  
A  
B  
C  
↓  
Client chooses one

---

### [[Elastic Load Balancing]]

Client connects to:

One Load Balancer

Then:

Load Balancer  
↓  
Chooses Healthy Backend Target

Architecture:

Client  
↓  
[[Application Load Balancer]]  
↓  
├── EC2 A  
├── EC2 B  
└── EC2 C

### Key Difference

**Multi-Value = DNS-level distribution**

**ELB = Request/connection-level distribution**

---

## Why Multi-Value Can Improve Availability

Suppose Route 53 returns:

- 1.1.1.1
- 2.2.2.2
- 3.3.3.3

If one endpoint later becomes unavailable, clients may still have other returned endpoints available.

Combined with health checks, Route 53 can stop including unhealthy records in future DNS responses.

This provides a basic form of:

**DNS-level availability**

But again:

> It is still not equivalent to a real load balancer.

---

## Architecture Thinking

### Scenario 1 — Several Healthy Web Servers

A company has six public web servers.

They want Route 53 to return multiple healthy server IP addresses in each DNS response.

**Choose → [[Route 53 Multi-Value Routing]]**

Why?

The requirement is:

**Multiple healthy DNS answers**

---

### Scenario 2 — Eight Healthy Records

A company has 15 healthy endpoints configured with Multi-Value Routing.

How many healthy records can Route 53 return in one DNS query?

**Up to 8**

---

### Scenario 3 — One Unhealthy Server

A company has:

Server A → Healthy

Server B → Healthy

Server C → Unhealthy

Server D → Healthy

Each Multi-Value record is associated with a health check.

What can Route 53 return?

- A
- B
- D

It should avoid returning:

- C

---

### Scenario 4 — Application Load Balancing

A company needs:

- Sticky sessions
- Request-level distribution
- Backend target health checks
- Routing HTTP requests across many EC2 instances

**Do NOT choose → Multi-Value Routing**

Choose:

[[Application Load Balancer]]

Why?

The requirement is true application-level load balancing.

---

### Scenario 5 — Primary and Backup

A company wants:

Primary Resource  
↓ failure  
Secondary Resource

**Do NOT choose → Multi-Value**

Choose:

[[Route 53 Failover Routing]]

---

## Multi-Value vs Simple

This is one of the biggest Route 53 exam comparisons.

### Simple Routing

Can return:

**Multiple values**

But:

- Cannot associate records with health checks
- No health-aware DNS response

### Multi-Value Routing

Can return:

**Multiple healthy values**

and supports:

[[Route 53 Health Checks]]

### Memory Trick

**Simple = Multiple values**

**Multi-Value = Multiple HEALTHY values**

---

## Multi-Value vs Failover

### Multi-Value

Returns:

**Several healthy endpoints**

Best for:

Basic DNS-level distribution

### Failover

Returns:

**Primary OR Secondary**

Best for:

Active-passive disaster recovery

### Exam Decision

**Many healthy endpoints → Multi-Value**

**Primary/Backup → Failover**

---

## Multi-Value vs Weighted

### Multi-Value

Goal:

Return multiple healthy records.

No explicit percentage split.

### Weighted

Goal:

Control relative traffic distribution.

Example:

80 / 20

### Memory Trick

**Multi-Value = Many answers**

**Weighted = How much traffic**

---

## Multi-Value vs Latency

### Multi-Value

Returns several healthy resources.

### Latency

Returns the endpoint associated with the:

**Lowest-latency Region**

### Exam Decision

**Several healthy answers → Multi-Value**

**Fastest Region → Latency**

---

## Health Check Architecture

Example:

Server A  
↓  
Health Check A

Server B  
↓  
Health Check B

Server C  
↓  
Health Check C

Server D  
↓  
Health Check D

Then:

[[Route 53 Multi-Value Routing]]  
↓  
Filter Unhealthy Records  
↓  
Return up to 8 Healthy Records

This is the core architecture to remember.

---

## DNS Caching Still Applies

Multi-Value Routing is still DNS-based.

The returned records may be cached according to:

[[Route 53 TTL]]

Therefore:

Route 53 returns multiple endpoints  
↓  
DNS Resolver caches response  
↓  
Client continues using cached values until TTL expires

Health check changes affect future DNS responses, but existing cached DNS answers may remain temporarily.

---

## Scenario Recognition

### Immediately Think Multi-Value When You See

- Multiple healthy endpoints
- Multiple DNS answers
- Return several IP addresses
- Health-aware DNS
- Up to 8 healthy records
- Basic DNS-level load distribution
- Several public servers

### Strongest Keyword Pair

> **Multiple + Healthy → Multi-Value**

---

## Exam Traps

### Trap 1 — Multi-Value Is a Load Balancer

False.

The Maarek slides explicitly emphasize:

**Multi-Value is NOT a substitute for ELB.**

---

### Trap 2 — Multi-Value Cannot Use Health Checks

False.

Health checks are one of its most important features.

Route 53 can return only:

**Healthy resources**

---

### Trap 3 — Multi-Value Returns Unlimited Records

False.

Route 53 returns:

**Up to 8 healthy records per query**

---

### Trap 4 — Simple and Multi-Value Are the Same

False.

Both can involve multiple DNS values.

But:

**Simple → No Health Checks**

**Multi-Value → Health Checks Supported**

---

### Trap 5 — Route 53 Chooses the Final Backend Request

False.

Route 53 returns DNS answers.

The client chooses or uses one of the returned endpoints.

It does not perform request-level load balancing.

---

## Quick Cheat Sheet

| Feature | Multi-Value Routing |
|---|---|
| Purpose | Return multiple healthy resources |
| Multiple DNS Answers | ✅ |
| Health Checks | ✅ |
| Excludes Unhealthy Records | ✅ |
| Maximum Healthy Records Returned | 8 |
| DNS-Level Distribution | ✅ |
| ELB Replacement | ❌ |
| Primary/Secondary DR | ❌ |
| Percentage Split | ❌ |
| Client Receives Multiple Values | ✅ |

---

## Master Memory Trick

> [!tip] Master Memory Trick
> **Multi-Value = DNS Gives You a Healthy Shortlist**
>
> Route 53 says:
>
> **"Here are several healthy places you can go."**

Remember:

**Simple = Multiple values**

**Multi-Value = Multiple HEALTHY values**

**Failover = Primary + Backup**

**Weighted = Percentage**

**Latency = Fastest**

And the magic number:

> **Multi-Value → Up to 8 healthy records**

Most important exam warning:

> **Multi-Value is NOT an ELB**

---

## Related Notes

- [[Route 53]]
- [[Route 53 Routing Policies]]
- [[Route 53 Simple Routing]]
- [[Route 53 Weighted Routing]]
- [[Route 53 Failover Routing]]
- [[Route 53 Latency Routing]]
- [[Route 53 Health Checks]]
- [[Route 53 TTL]]
- [[Elastic Load Balancing]]
- [[Application Load Balancer]]
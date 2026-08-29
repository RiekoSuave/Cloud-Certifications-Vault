## What Problem Does It Solve?

[[Route 53 Simple Routing]] is the most basic Route 53 routing policy.

It solves the problem of:

> **"I just need this DNS name to point to a resource without any advanced routing logic."**

Typical use:

example.com  
↓  
[[Route 53]]  
↓  
Single Resource

Simple routing is best when you do **not** need:

- Weighted traffic splitting
- Failover
- Latency optimization
- Geographic routing
- Health-aware DNS decisions

> [!tip] Memory Trick
> **Simple = Just send me somewhere**
>
> No percentages.  
> No geography.  
> No failover logic.

---

## How Simple Routing Works

Simple Routing typically sends traffic to:

**One resource**

Example:

foo.example.com  
↓  
A Record  
↓  
11.22.33.44

Architecture:

Client  
↓  
DNS Query  
[[Route 53]]  
↓  
11.22.33.44  
↓  
Client connects to resource

This is the simplest Route 53 routing model.

---

## Simple Routing with a Single Value

The most common setup is:

foo.example.com  
↓  
A Record  
↓  
11.22.33.44

When a client asks:

foo.example.com?

Route 53 returns:

11.22.33.44

The client then connects directly to that resource.

### Architecture Thinking

Use Simple Routing when:

> **There is no decision to make.**

One DNS name simply maps to one destination.

---

## Simple Routing Can Return Multiple Values

Simple Routing can also contain **multiple values in the same DNS record**.

Example:

foo.example.com

A Record:

- 11.22.33.44
- 55.66.77.88
- 99.11.22.33

Route 53 can return all of those values.

Conceptually:

Client  
↓  
foo.example.com?  
↓  
[[Route 53]]  
↓  
11.22.33.44  
55.66.77.88  
99.11.22.33

The client then chooses one of the returned values.

### Important

Route 53 is **not selecting the final resource** in this scenario.

The client chooses one of the values returned in the DNS response.

> [!tip] Memory Trick
> **Simple can return many, but the client chooses one.**

---

## Simple Routing Is Not Load Balancing

This is important.

If Simple Routing returns:

- Server A
- Server B
- Server C

that does **not** mean Route 53 is intelligently balancing traffic across them.

There is no:

- Weighting
- Health awareness
- Regional intelligence
- Latency decision

The client simply receives multiple DNS answers and chooses one.

### Exam Rule

> **Multiple values in Simple Routing ≠ Load Balancer**

If you need actual application-level load balancing:

Think → [[Elastic Load Balancing]]

---

## Simple Routing with Alias Records

Simple Routing can also use:

[[Route 53 Alias Records]]

Example:

example.com  
↓  
Alias  
↓  
[[Application Load Balancer]]

When Alias is enabled in a Simple Routing record:

**Only one AWS resource can be specified.**

So you cannot configure one Simple Alias record to simultaneously point to multiple AWS resources.

### Architecture Thinking

Simple Alias:

Domain  
↓  
[[Route 53]]  
↓  
One AWS Resource

Example:

example.com  
↓  
Alias  
↓  
[[Application Load Balancer]]

---

## Simple Routing and Health Checks

A major limitation:

**Simple Routing cannot be associated with [[Route 53 Health Checks]].**

This matters on the exam.

If the architecture requires:

> "Do not return an unhealthy resource"

Simple Routing is usually **not** the right answer.

You may need another policy such as:

- [[Route 53 Failover Routing]]
- [[Route 53 IP-Based Routing]]
- Other health-check-aware routing policies

> [!warning] Exam Trap
> **Simple Routing = No Health Checks**

---

## Architecture Thinking

### Scenario 1 — One Public Web Server

A company has one public web server.

They want:

www.example.com

to resolve to:

192.0.2.10

No failover or special routing is required.

**Choose → Simple Routing**

Architecture:

Client  
↓  
www.example.com  
↓  
[[Route 53]]  
↓  
192.0.2.10

---

### Scenario 2 — One Application Load Balancer

A company has one [[Application Load Balancer]].

They want:

example.com

to point directly to that ALB.

No additional routing logic is needed.

**Choose → Simple Routing + Alias Record**

Architecture:

Client  
↓  
example.com  
↓  
[[Route 53]]  
↓ Alias  
[[Application Load Balancer]]

---

### Scenario 3 — Several IP Addresses

A company wants one DNS record to contain:

- 10.0.0.10
- 10.0.0.20
- 10.0.0.30

They do not need health checks or intelligent routing.

**Choose → Simple Routing with multiple values**

Route 53 can return multiple IP addresses.

The client chooses one.

---

### Scenario 4 — Primary and Backup Server

A company wants:

Primary Server  
↓ if unhealthy  
Backup Server

**Do NOT choose → Simple Routing**

Choose:

[[Route 53 Failover Routing]]

Why?

Simple Routing does not provide health-check-driven primary/secondary failover.

---

### Scenario 5 — 80/20 Deployment

A company wants:

80% → Application Version A  
20% → Application Version B

**Do NOT choose → Simple Routing**

Choose:

[[Route 53 Weighted Routing]]

---

## Simple vs Weighted

### Simple

Use when:

**No traffic distribution logic is required**

Example:

example.com  
↓  
Server A

### Weighted

Use when:

**Traffic must be distributed by relative percentage**

Example:

80% → Server A  
20% → Server B

### Memory Trick

**Simple = Straight**

**Weighted = Split**

---

## Simple vs Failover

### Simple

No health-check-driven backup logic.

### Failover

Provides:

**Primary → Secondary**

when the primary becomes unhealthy.

### Exam Decision

**Basic mapping → Simple**

**Disaster recovery → Failover**

---

## Simple vs Multi-Value

This distinction can be tricky because both can return multiple values.

### Simple Routing

Can return:

**Multiple values**

But:

- No health checks
- Client chooses a returned value
- No health-aware DNS distribution

### [[Route 53 IP-Based Routing]]

Can return:

**Multiple healthy resources**

and supports:

[[Route 53 Health Checks]]

### Exam Decision

If the question emphasizes:

> **Multiple healthy resources**

Think:

**Multi-Value**

not Simple.

---

## Scenario Recognition

### Immediately Think Simple Routing When You See

- Basic DNS
- One resource
- One destination
- No special routing requirement
- Straightforward hostname mapping
- Single ALB
- Single website endpoint

### Watch for Another Policy When You See

- Percentage split
- Health checks
- Primary / secondary
- Lowest latency
- User location
- Geographic bias
- Multiple healthy endpoints

---

## Exam Traps

### Trap 1 — Simple Routing Supports Health Checks

False.

Simple Routing:

**Cannot be associated with Route 53 Health Checks.**

---

### Trap 2 — Multiple Simple Values Means Load Balancing

Not really.

Route 53 may return multiple values, but:

**the client chooses one of them.**

There is no sophisticated health-aware or weighted load distribution.

---

### Trap 3 — Route 53 Selects One Random Server

Be careful with the wording.

When multiple values are returned with Simple Routing:

**the client chooses one of the returned values.**

Do not think Route 53 is acting like an application load balancer.

---

### Trap 4 — Multiple Alias Targets in One Simple Record

When Alias is enabled:

**Simple Routing can specify only one AWS resource.**

---

### Trap 5 — Simple Is Best for Disaster Recovery

False.

If you see:

- Primary
- Secondary
- Health check
- Backup Region

Think:

[[Route 53 Failover Routing]]

---

## Quick Cheat Sheet

| Feature | Simple Routing |
|---|---|
| Primary Purpose | Basic DNS mapping |
| Typical Resources | One |
| Multiple Values | ✅ |
| Client Chooses Returned Value | ✅ |
| Health Checks | ❌ |
| Percentage-Based Routing | ❌ |
| Latency-Based Routing | ❌ |
| Geographic Routing | ❌ |
| Alias Support | ✅ |
| Multiple Alias Targets in One Record | ❌ |
| Best For | Straightforward DNS |

---

## Master Memory Trick

> [!tip] Master Memory Trick
> **Simple = No Decision**
>
> Route 53 is basically saying:
>
> **"Here is the destination."**

Remember:

**One destination → Simple**

**Multiple basic values → Simple can do it**

But:

**Health checks → Not Simple**

**Percentages → Weighted**

**Backup → Failover**

**Fastest Region → Latency**

**Many healthy answers → Multi-Value**

---

## Related Notes

- [[Route 53]]
- [[Route 53 Routing Policies]]
- [[Route 53 Alias Records]]
- [[Route 53 Health Checks]]
- [[Route 53 Weighted Routing]]
- [[Route 53 Failover Routing]]
- [[Route 53 Latency Routing]]
- [[Route 53 IP-Based Routing]]
- [[Elastic Load Balancing]]
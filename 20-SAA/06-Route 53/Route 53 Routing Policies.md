## What Problem Does It Solve?

[[Route 53 Routing Policies]] define **how Route 53 responds to DNS queries when multiple possible destinations exist**.

They solve the problem of:

> **"Which endpoint should Route 53 return to the client?"**

Important:

**Route 53 does not route application traffic itself.**

It only answers DNS queries.

Think:

Client  
↓ DNS Query  
[[Route 53]]  
↓ Returns DNS Answer  
Client  
↓ Connects Directly  
Application

> [!tip] Memory Trick
> **Route 53 chooses the answer, not the network path.**

---

## What Is a Routing Policy?

A routing policy tells [[Route 53]] how to choose which DNS record or resource should be returned.

Example:

A company has:

- Server A
- Server B
- Server C

A client asks:

example.com?

Route 53 must decide:

> **Which destination should I return?**

That decision is controlled by the routing policy.

---

## Important Architecture Concept

Do not confuse Route 53 routing with:

- [[Application Load Balancer]]
- [[Network Load Balancer]]
- Network routing
- VPC route tables

Route 53 performs **DNS-level decision making**.

### Architecture

Client  
↓  
DNS Query  
[[Route 53]]  
↓  
Returns Endpoint A

Then:

Client  
↓  
Connects directly to Endpoint A

Route 53 is no longer in the data path.

---

## Route 53 Routing Policies

The major routing policies are:

- Simple
- Weighted
- Failover
- Latency
- Geolocation
- Geoproximity
- Multi-Value

Each solves a different architecture problem.

---

## Simple Routing

Use when:

> **One DNS name should resolve to one or more basic destinations without advanced routing logic.**

Think:

**Simple = No special decision logic**

Example:

example.com  
↓  
[[Route 53]]  
↓  
Server

Use when you do not need:

- Weighting
- Geographic routing
- Failover logic
- Latency optimization

---

## Weighted Routing

Use when:

> **Traffic should be distributed across multiple resources based on percentages or relative weights.**

Example:

Server A → Weight 70  
Server B → Weight 30

Conceptually:

70% of DNS responses  
↓  
Server A

30%  
↓  
Server B

Common use cases:

- Blue/green deployments
- Canary deployments
- Gradual traffic migration
- Testing a new version

> [!tip] Memory Trick
> **Weighted = What percentage goes where?**

---

## Failover Routing

Use when:

> **You need active-passive disaster recovery.**

Architecture:

Primary Resource  
↓ healthy  
Serve traffic

If unhealthy:

Secondary Resource  
↓  
Serve traffic

Failover routing is commonly combined with:

[[Route 53 Health Checks]]

Think:

**Primary fails → Secondary takes over**

> [!tip] Memory Trick
> **Failover = Backup plan**

---

## Latency-Based Routing

Use when:

> **Users should be sent to the AWS Region that provides the lowest latency.**

Example:

User in North America  
↓  
us-east-1

User in Europe  
↓  
eu-west-1

The decision is based on:

**Lowest network latency**

not simply geographic distance.

> [!tip] Memory Trick
> **Latency = Fastest Region**

---

## Geolocation Routing

Use when:

> **Traffic should be routed based on where the user is located.**

Possible location rules include:

- Continent
- Country
- U.S. State

Example:

Users in France  
↓  
European Application

Users in United States  
↓  
U.S. Application

Common use cases:

- Localization
- Content restrictions
- Compliance
- Regional websites

> [!tip] Memory Trick
> **Geolocation = Where is the user?**

---

## Geoproximity Routing

Use when:

> **Traffic should be routed based on the geographic distance between users and resources, with the ability to influence traffic using bias.**

This is more advanced than geolocation.

Think:

**Geolocation = User location rules**

**Geoproximity = Distance to resources + bias**

A positive or negative bias can shift traffic toward or away from a resource.

> [!tip] Memory Trick
> **Geoproximity = Geography + Pull**

---

## Multi-Value Routing

Use when:

> **You want Route 53 to return multiple healthy resources in a DNS response.**

Route 53 can:

- Return multiple values
- Associate records with health checks
- Return only healthy resources

Important:

**Multi-Value is not a replacement for an ELB.**

It provides basic DNS-level distribution.

> [!tip] Memory Trick
> **Multi-Value = Many healthy answers**

---

## Routing Policy Comparison

| Requirement | Best Routing Policy |
|---|---|
| Basic DNS response | Simple |
| Split traffic by percentage | Weighted |
| Active-passive DR | Failover |
| Lowest network latency | Latency |
| Route by user location | Geolocation |
| Route by distance + bias | Geoproximity |
| Return multiple healthy endpoints | Multi-Value |

---

## Architecture Thinking

### Scenario 1 — Canary Deployment

A company deploys a new version of its application.

They want:

90% of users → Old Version  
10% of users → New Version

**Choose → Weighted Routing**

Why?

Traffic must be split by relative percentage.

---

### Scenario 2 — Disaster Recovery

A company has:

Primary Region  
Secondary Region

Traffic should go to the secondary Region only when the primary application becomes unhealthy.

**Choose → Failover Routing**

Usually combined with:

[[Route 53 Health Checks]]

---

### Scenario 3 — Global Application

A company has application stacks in:

- us-east-1
- eu-west-1
- ap-southeast-1

Users should be routed to the Region with the **lowest network latency**.

**Choose → Latency-Based Routing**

---

### Scenario 4 — Country-Specific Content

A company wants:

German users → German website  
Canadian users → Canadian website  
Other users → Default website

**Choose → Geolocation Routing**

Why?

The decision is based on the user's location.

---

### Scenario 5 — Shift Geographic Traffic

A company wants users to normally go to their geographically closest resource but wants to intentionally send more traffic toward one Region.

**Choose → Geoproximity Routing**

Why?

Bias lets you influence geographic traffic distribution.

---

### Scenario 6 — Multiple Healthy Web Servers

A company has several public web servers.

Route 53 should return multiple healthy IP addresses in each DNS response.

**Choose → Multi-Value Routing**

---

## Simple vs Multi-Value

These can look similar.

### Simple

Can return one or more values.

But:

- No advanced health-aware load distribution
- Best for straightforward DNS mappings

### Multi-Value

Designed to return:

**Multiple healthy resources**

Can integrate with:

[[Route 53 Health Checks]]

### Exam Decision

If the question emphasizes:

**Multiple healthy endpoints**

Think:

**Multi-Value**

---

## Weighted vs Multi-Value

### Weighted

Controls:

**How much DNS traffic each resource receives**

Example:

80 / 20

### Multi-Value

Returns:

**Multiple healthy answers**

### Memory Trick

**Weighted = Percentages**

**Multi-Value = Multiple answers**

---

## Geolocation vs Latency

This is a common exam trap.

### Geolocation

Decision based on:

**Where the user is**

Example:

User is in Germany

### Latency

Decision based on:

**Which Region provides the lowest latency**

These may produce different results.

A physically closer Region is not always the lowest-latency Region.

### Memory Trick

**Geolocation = Location**

**Latency = Performance**

---

## Geolocation vs Geoproximity

Another common trap.

### Geolocation

Uses explicit user-location rules.

Example:

Users from Canada  
↓  
Endpoint A

### Geoproximity

Routes based on geographic distance between users and resources.

Can also use:

**Bias**

to shift traffic.

### Memory Trick

**Geolocation = Rules**

**Geoproximity = Distance + Bias**

---

## Failover vs Weighted

### Failover

Designed for:

**Primary / Secondary**

Traffic normally goes to the primary.

Secondary is used when primary fails.

### Weighted

Designed for:

**Traffic distribution**

Both resources can actively receive traffic.

Example:

50 / 50

### Exam Decision

**Disaster recovery → Failover**

**Gradual traffic split → Weighted**

---

## Routing Policies and Health Checks

Some Route 53 routing policies can work with:

[[Route 53 Health Checks]]

Health checks allow Route 53 to avoid returning unhealthy resources.

This is especially important with:

- Failover
- Multi-Value
- Other advanced routing configurations

Architecture:

[[Route 53 Health Checks]]  
↓  
Resource Health  
↓  
[[Route 53 Routing Policies]]  
↓  
DNS Response

We will cover health checks separately.

---

## Scenario Recognition

### Simple

Look for:

- Basic DNS
- Single resource
- No special routing requirement

### Weighted

Look for:

- Percentage
- Traffic split
- Canary
- Blue/green
- Migration

### Failover

Look for:

- Primary
- Secondary
- Active-passive
- Disaster recovery
- Backup endpoint

### Latency

Look for:

- Lowest latency
- Best performance
- Closest network response
- Multi-Region application

### Geolocation

Look for:

- Country
- Continent
- State
- Localization
- Geographic restrictions

### Geoproximity

Look for:

- Geographic distance
- Bias
- Shift traffic geographically

### Multi-Value

Look for:

- Multiple healthy resources
- Return several IP addresses
- DNS-level basic load distribution

---

## Exam Traps

### Trap 1 — Route 53 Routes Application Traffic

False.

Route 53 only returns a DNS answer.

The client then connects directly to the target resource.

---

### Trap 2 — Latency Means Closest Geographic Region

Not necessarily.

Latency-based routing chooses the endpoint with:

**Lowest network latency**

not shortest geographic distance.

---

### Trap 3 — Geolocation Means Lowest Latency

False.

Geolocation routing uses:

**User location rules**

not performance measurements.

---

### Trap 4 — Multi-Value Replaces ELB

False.

Multi-Value can return several healthy endpoints but is **not a substitute for [[Elastic Load Balancing]]**.

---

### Trap 5 — Weighted Routing Guarantees Exact Percentages for Every User

Weighted routing influences the proportion of DNS responses over time.

DNS caching and TTL mean it should not be thought of as exact per-request load balancing.

---

### Trap 6 — Failover Is Active-Active

Failover routing is primarily:

**Active-Passive**

Primary first.

Secondary if primary is unhealthy.

---

## Quick Cheat Sheet

| Policy | Best For |
|---|---|
| Simple | Basic DNS |
| Weighted | Percentage-based traffic split |
| Failover | Active-passive DR |
| Latency | Lowest-latency Region |
| Geolocation | User location |
| Geoproximity | Distance + bias |
| Multi-Value | Multiple healthy answers |

---

## Master Memory Trick

> [!tip] Master Memory Trick
> Ask one question:
>
> **"WHY am I choosing between multiple destinations?"**

Then map the requirement:

**Nothing special → Simple**

**Percentage → Weighted**

**Backup → Failover**

**Fastest → Latency**

**User location → Geolocation**

**Distance + influence → Geoproximity**

**Many healthy answers → Multi-Value**

And always remember:

> **Route 53 chooses the DNS answer. It does not carry the application traffic.**

---

## Related Notes

- [[Route 53]]
- [[Route 53 TTL]]
- [[Route 53 Alias Records]]
- [[Route 53 Health Checks]]
- [[Route 53 Simple Routing]]
- [[Route 53 Weighted Routing]]
- [[Route 53 Failover Routing]]
- [[Route 53 Latency Routing]]
- [[Route 53 Geolocation Routing]]
- [[Route 53 Geoproximity Routing]]
- [[Route 53 IP-Based Routing]]
- [[Elastic Load Balancing]]
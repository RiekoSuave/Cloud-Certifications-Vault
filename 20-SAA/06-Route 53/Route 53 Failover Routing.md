## What Problem Does It Solve?

[[Route 53 Failover Routing]] provides **active-passive DNS failover**.

It solves the problem of:

> **"If my primary application becomes unhealthy, how can Route 53 automatically send users to a backup resource?"**

Architecture:

Primary Resource  
↓  
[[Route 53 Health Checks]]  
↓  
Healthy?  
├── Yes → Return Primary  
└── No → Return Secondary

> [!tip] Memory Trick
> **Failover = Primary + Backup**
>
> If the exam says:
>
> **active-passive, disaster recovery, primary/secondary**
>
> Think → [[Route 53 Failover Routing]]

---

## Active-Passive Architecture

Failover Routing is designed around two roles:

- **Primary**
- **Secondary**

The primary resource normally receives traffic.

The secondary resource is used for:

**Disaster Recovery**

Conceptually:

Users  
↓  
[[Route 53]]  
↓  
Primary Healthy?  
├── Yes → Primary Resource  
└── No → Secondary Resource

This is an:

**Active-Passive architecture**

---

## Primary Resource

The Primary resource is the normal production endpoint.

Example:

Primary Region  
↓  
[[Application Load Balancer]]  
↓  
[[Auto Scaling]]  
↓  
[[EC2]]

Under normal conditions:

[[Route 53]]  
↓  
Primary

The secondary resource receives little or no normal production traffic.

---

## Secondary Resource

The Secondary resource acts as the:

**Disaster Recovery endpoint**

Example:

Primary  
↓ unhealthy  
[[Route 53]]  
↓  
Secondary

The secondary could be:

- Another [[EC2]] instance
- Another [[Application Load Balancer]]
- Another AWS Region
- A disaster recovery environment
- Another supported endpoint

### Architecture Thinking

Think:

**Primary = Production**

**Secondary = Standby**

---

## Health Check Is Mandatory for the Primary

This is a key SAA detail.

For Failover Routing:

**The Primary record must have a health check.**

Why?

Route 53 needs a way to determine when the primary has failed.

Architecture:

Primary Resource  
↓  
[[Route 53 Health Checks]]  
↓  
Healthy / Unhealthy  
↓  
[[Route 53 Failover Routing]]

Without that health signal, Route 53 would not know when to switch to the secondary.

> [!warning] Exam Rule
> **Primary Failover Record → Health Check Required**

---

## Automated DNS Failover

Failover Routing enables:

**Automated DNS Failover**

Example:

Primary healthy:

Client  
↓  
[[Route 53]]  
↓  
Primary

Then:

Primary fails  
↓  
Health Check fails  
↓  
Route 53 marks Primary unhealthy  
↓  
Future DNS responses return Secondary

This removes the need for manual DNS changes during a failure.

---

## Multi-Region Disaster Recovery

A common SAA architecture uses Failover Routing across Regions.

Example:

### Primary Region

us-east-1  
↓  
[[Application Load Balancer]]  
↓  
Application

### Secondary Region

us-west-2  
↓  
[[Application Load Balancer]]  
↓  
Disaster Recovery Application

Architecture:

Users  
↓  
[[Route 53 Failover Routing]]  
↓  
Primary Health Check  
├── Healthy → us-east-1  
└── Unhealthy → us-west-2

This is a classic:

**Active-Passive Multi-Region DR architecture**

---

## Failover Routing and TTL

Remember that Route 53 operates through DNS.

Even after Route 53 detects that the primary is unhealthy:

Some users may temporarily keep using the old DNS answer because of:

[[Route 53 TTL]]

Conceptually:

Primary fails  
↓  
Health Check detects failure  
↓  
Route 53 starts returning Secondary  
↓  
Existing DNS caches may still contain Primary  
↓  
TTL expires  
↓  
Clients retrieve Secondary

### Architecture Lesson

Failover Routing is automatic, but:

**DNS failover is not always instantaneous for every client.**

---

## Failover Routing vs High Availability Inside One Region

Do not confuse Route 53 failover with:

- [[Auto Scaling]]
- [[Elastic Load Balancing]]
- Multi-AZ application design

Those services usually provide resilience **inside an application architecture**.

Route 53 Failover Routing operates at the:

**DNS endpoint level**

Example:

[[Route 53]]  
↓  
Primary Regional Stack  
or  
Secondary Regional Stack

### Architecture Thinking

Use multiple layers together:

[[Route 53 Failover Routing]]  
↓  
Regional [[Application Load Balancer]]  
↓  
Multi-AZ [[Auto Scaling]]  
↓  
[[EC2]]

This provides:

**Regional HA + Cross-Region DR**

---

## Architecture Thinking

### Scenario 1 — Primary and DR Region

A company runs production in:

us-east-1

and maintains a disaster recovery environment in:

us-west-2

Users should normally use us-east-1.

If us-east-1 becomes unhealthy, users should automatically resolve to us-west-2.

**Choose → [[Route 53 Failover Routing]]**

---

### Scenario 2 — 80/20 Traffic Split

A company wants:

80% → Region A  
20% → Region B

Both resources should actively receive traffic.

**Do NOT choose → Failover Routing**

Choose:

[[Route 53 Weighted Routing]]

Why?

The requirement is:

**Active-Active percentage distribution**

not active-passive DR.

---

### Scenario 3 — Best Performing Region

A company wants users routed to the Region with the lowest network latency.

**Do NOT choose → Failover Routing**

Choose:

[[Route 53 Latency Routing]]

---

### Scenario 4 — Primary Becomes Unhealthy

A company's primary application fails its Route 53 Health Check.

The secondary disaster recovery resource is configured as the Failover secondary.

What happens?

Future Route 53 DNS responses can return:

**The Secondary Resource**

---

## Failover vs Weighted

### Failover

Architecture:

Primary  
↓ failure  
Secondary

Designed for:

- Disaster recovery
- Active-passive
- Backup endpoints

### Weighted

Architecture:

Resource A → 80%  
Resource B → 20%

Designed for:

- Canary
- Blue/green
- Gradual migration
- Active-active traffic split

### Memory Trick

**Failover = Backup**

**Weighted = Split**

---

## Failover vs Latency

### Failover

Decision based on:

**Primary health**

### Latency

Decision based on:

**Network performance**

### Exam Decision

**Primary/Secondary → Failover**

**Fastest Region → Latency**

---

## Failover vs Multi-Value

### Failover

Returns:

**Primary OR Secondary**

based on health.

### Multi-Value

Can return:

**Multiple healthy resources**

in one DNS response.

### Memory Trick

**Failover = One backup path**

**Multi-Value = Many healthy answers**

---

## Active-Passive vs Active-Active

This distinction matters a lot on the SAA exam.

### Active-Passive

One environment handles normal traffic.

The backup waits.

Example:

Primary  
↓ failure  
Secondary

Think:

**Failover Routing**

---

### Active-Active

Multiple environments receive traffic at the same time.

Examples:

- Weighted Routing
- Latency Routing
- Multi-Value Routing

Think:

**Traffic distributed across multiple active endpoints**

> [!tip] Memory Trick
> **Failover = Passive backup waiting in the wings**

---

## Scenario Recognition

### Immediately Think Failover Routing When You See

- Active-passive
- Primary / secondary
- Disaster recovery
- Backup Region
- Standby application
- Automatic DNS failover
- Route to secondary if primary fails
- Health-check-driven failover

### Strongest Keyword Pair

> **Primary + Secondary → Failover**

---

## Exam Traps

### Trap 1 — Failover Routing Is Active-Active

False.

Failover Routing is:

**Active-Passive**

---

### Trap 2 — Secondary Receives a Percentage of Normal Traffic

Not in the normal failover model.

The secondary is primarily there for:

**Disaster recovery**

---

### Trap 3 — No Health Check Needed

False.

The primary must have a health check so Route 53 can determine when to fail over.

---

### Trap 4 — Failover Is Immediate for Every User

Not necessarily.

DNS caching and [[Route 53 TTL]] may cause some clients to temporarily retain the old primary DNS answer.

---

### Trap 5 — Failover Routing Replaces Multi-AZ Architecture

False.

You still want resilient application architecture within each Region.

Example:

[[Route 53 Failover Routing]]  
↓  
Regional [[Application Load Balancer]]  
↓  
Multi-AZ [[Auto Scaling]]  
↓  
[[EC2]]

---

## Quick Cheat Sheet

| Feature | Failover Routing |
|---|---|
| Architecture | Active-Passive |
| Primary Record | ✅ |
| Secondary Record | ✅ |
| Primary Health Check | Mandatory |
| Automatic DNS Failover | ✅ |
| Disaster Recovery | ✅ |
| Cross-Region DR | ✅ |
| Percentage Split | ❌ |
| Lowest Latency Decision | ❌ |
| Multiple Active Endpoints | Not the primary purpose |
| DNS-Level Routing | ✅ |

---

## Master Memory Trick

> [!tip] Master Memory Trick
> **Failover = Plan B DNS**
>
> Route 53 asks:
>
> **"Is Primary alive?"**

If yes:

**Primary**

If no:

**Secondary**

Remember:

**Primary + Backup = Failover**

**Percentage = Weighted**

**Fastest = Latency**

**Location = Geolocation**

And:

> **Failover Routing = Active-Passive Disaster Recovery**

---

## Related Notes

- [[Route 53]]
- [[Route 53 Routing Policies]]
- [[Route 53 Health Checks]]
- [[Route 53 Weighted Routing]]
- [[Route 53 Latency Routing]]
- [[Route 53 Geolocation Routing]]
- [[Route 53 IP-Based Routing]]
- [[Route 53 TTL]]
- [[Application Load Balancer]]
- [[Auto Scaling]]
- [[EC2]]
- [[Disaster Recovery]]
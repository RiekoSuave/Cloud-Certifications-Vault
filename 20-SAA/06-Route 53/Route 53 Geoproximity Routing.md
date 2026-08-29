## What Problem Does It Solve?

[[Route 53 Geoproximity Routing]] routes traffic based on the **geographic location of both users and resources**.

It also lets you intentionally shift more or less traffic toward a resource using:

**Bias**

It solves the problem of:

> **"How can I route users toward geographically nearby resources while also controlling how large each resource's geographic traffic area should be?"**

Think:

User Location  
+  
Resource Location  
+  
Bias  
↓  
[[Route 53 Geoproximity Routing]]

> [!tip] Memory Trick
> **Geoproximity = Geography + Pull**
>
> Resources can **pull more traffic toward themselves** or **push traffic away** using bias.

---

## How Geoproximity Routing Works

Route 53 considers:

1. Where the user is located
2. Where the resource is located
3. Any configured bias

Conceptually:

User  
↓  
[[Route 53]]  
↓  
Compare Geographic Location  
↓  
Apply Bias  
↓  
Choose Resource

Without bias, users are generally routed based on geographic proximity to available resources.

With bias, you can intentionally change the geographic area served by a resource.

---

## Resource Location

Route 53 needs to know where each resource is located.

Resources can be:

- AWS resources
- Non-AWS resources

How you define the location depends on the resource type.

---

## AWS Resources

For AWS resources, specify the:

**AWS Region**

Example:

Resource A  
↓  
us-east-1

Resource B  
↓  
eu-west-1

Route 53 understands the geographic location of those AWS Regions.

Architecture:

Users  
↓  
[[Route 53 Geoproximity Routing]]  
↓  
├── us-east-1 Resource
└── eu-west-1 Resource

---

## Non-AWS Resources

Geoproximity Routing can also work with resources outside AWS.

For non-AWS resources, specify:

- Latitude
- Longitude

Example:

On-Premises Data Center  
↓  
Latitude + Longitude  
↓  
[[Route 53 Geoproximity Routing]]

This means Geoproximity Routing can be useful in:

**Hybrid architectures**

Example:

Users  
↓  
[[Route 53]]  
↓  
├── AWS Region
└── On-Premises Data Center

> [!tip] Architecture Thinking
> **AWS Resource → Specify Region**
>
> **Non-AWS Resource → Specify Latitude + Longitude**

---

## What Is Bias?

**Bias** lets you change how much geographic traffic is attracted toward a resource.

Think of each resource as having a geographic territory.

Without bias:

Resource A ← Geographic Boundary → Resource B

Bias lets you move that boundary.

---

## Positive Bias

A **positive bias** expands the geographic area from which Route 53 sends traffic to a resource.

Valid positive values:

**1 to 99**

Example:

Resource A  
Bias = +50

Result:

Resource A's geographic traffic area becomes larger.

More users may be routed to Resource A even if another resource would normally be geographically closer.

> [!tip] Memory Trick
> **Positive = Pull more traffic**

---

## Negative Bias

A **negative bias** shrinks the geographic area from which Route 53 sends traffic to a resource.

Valid negative values:

**-1 to -99**

Example:

Resource A  
Bias = -50

Result:

Resource A's geographic traffic area becomes smaller.

More users are pushed toward other resources.

> [!tip] Memory Trick
> **Negative = Push traffic away**

---

## Bias = Zero

A bias of:

**0**

means:

**No geographic adjustment**

Route 53 uses the normal geographic relationship between users and resources.

Think:

0 = Neutral

Positive = Expand

Negative = Shrink

---

## Visualizing Bias

Imagine two resources:

Resource A ←──────── Boundary ────────→ Resource B

Without bias, Route 53 determines the geographic boundary normally.

### Positive Bias on Resource A

Resource A receives a positive bias:

Resource A ←──────────────── Boundary ─→ Resource B

Resource A's territory expands.

Result:

**More traffic → Resource A**

---

### Negative Bias on Resource A

Resource A receives a negative bias:

Resource A ←── Boundary ───────────────→ Resource B

Resource A's territory shrinks.

Result:

**Less traffic → Resource A**

---

## Why Would You Use Bias?

Bias is useful when geographic distance alone should **not** determine traffic distribution.

Example:

Two Regions serve an application:

Region A  
Capacity = Large

Region B  
Capacity = Small

You may want Region A to serve a larger geographic area.

Configure:

Region A → Positive Bias

Result:

More traffic is attracted toward Region A.

### Architecture Thinking

Bias lets business or infrastructure requirements influence geographic routing.

Examples:

- More capacity in one Region
- Reduce traffic to an overloaded Region
- Shift users during maintenance
- Gradually move geographic traffic
- Favor one data center
- Hybrid AWS/on-premises routing

---

## Geoproximity Requires Route 53 Traffic Flow

This is an important exam detail.

To use Geoproximity Routing:

**You must use Route 53 Traffic Flow.**

Traffic Flow provides a visual editor for creating complex routing configurations.

> [!warning] Exam Rule
> **Geoproximity → Requires Route 53 Traffic Flow**

---

## Architecture Thinking

### Scenario 1 — Favor Higher-Capacity Region

A company operates applications in:

us-east-1  
us-west-2

The us-east-1 deployment has significantly more capacity.

The company wants us-east-1 to serve a larger geographic area.

**Choose → Geoproximity Routing + Positive Bias on us-east-1**

Why?

Positive bias:

**Expands the resource's geographic traffic area**

---

### Scenario 2 — Reduce Traffic to a Region

A Region is experiencing capacity constraints.

The company wants fewer geographically nearby users sent there without completely removing the Region.

**Choose → Negative Bias**

Why?

Negative bias:

**Shrinks the resource's geographic traffic area**

---

### Scenario 3 — Hybrid Architecture

A company has:

AWS Application  
↓  
us-east-1

and:

On-Premises Data Center  
↓  
Detroit

Traffic should be routed geographically between both resources.

**Choose → Geoproximity Routing**

Configure:

AWS Resource → AWS Region

On-Premises Resource → Latitude + Longitude

---

### Scenario 4 — Country-Specific Content

A company wants:

Canada → Canadian Website

France → French Website

Germany → German Website

The requirement is based on explicit user-location rules.

**Do NOT choose → Geoproximity**

Choose:

[[Route 53 Geolocation Routing]]

---

### Scenario 5 — Lowest Network Latency

A company wants users sent to whichever AWS Region provides the best network performance.

**Do NOT choose → Geoproximity**

Choose:

[[Route 53 Latency Routing]]

---

## Geoproximity vs Geolocation

This is the biggest Geoproximity exam distinction.

### Geolocation

Routes based on:

**Where the user is located**

Uses explicit rules such as:

Canada → Endpoint A

Europe → Endpoint B

California → Endpoint C

---

### Geoproximity

Routes based on:

**User location + Resource location**

and supports:

**Bias**

### Memory Trick

**Geolocation = Location Rule**

**Geoproximity = Geographic Distance + Bias**

---

## Geoproximity vs Latency

### Geoproximity

Decision based primarily on:

**Geographic location**

Can modify the decision using:

**Bias**

### Latency

Decision based on:

**Network latency**

Goal:

Best performance.

### Exam Decision

**Geographic traffic control → Geoproximity**

**Fastest network performance → Latency**

---

## Geoproximity vs Weighted

These can both influence how much traffic reaches a resource, but they do it differently.

### Weighted

You explicitly configure relative traffic weights.

Example:

80 → Resource A

20 → Resource B

Think:

**Percentage-style distribution**

---

### Geoproximity

You modify:

**Geographic traffic boundaries**

Example:

Resource A → +40 Bias

This does not mean:

40% of traffic

It means:

**Expand Resource A's geographic coverage**

> [!warning] Exam Trap
> **Bias is NOT a traffic percentage.**

---

## Bias Direction

This is worth memorizing.

### Positive Bias

+1 through +99

Means:

**Expand**

Result:

**More traffic**

---

### Zero Bias

0

Means:

**Neutral**

---

### Negative Bias

-1 through -99

Means:

**Shrink**

Result:

**Less traffic**

---

## Scenario Recognition

### Immediately Think Geoproximity When You See

- Geographic distance
- Location of users and resources
- Bias
- Positive bias
- Negative bias
- Expand geographic traffic area
- Shrink geographic traffic area
- Shift geographic traffic
- AWS Region + on-premises location
- Latitude and longitude
- Route 53 Traffic Flow

### Strongest Keyword

> **Bias → Geoproximity**

---

## Exam Traps

### Trap 1 — Geoproximity and Geolocation Are the Same

False.

Geolocation:

**User location rules**

Geoproximity:

**User + Resource geography + Bias**

---

### Trap 2 — Positive Bias Reduces Traffic

False.

Positive bias:

**Expands geographic territory**

Therefore:

**More traffic**

---

### Trap 3 — Negative Bias Attracts More Traffic

False.

Negative bias:

**Shrinks geographic territory**

Therefore:

**Less traffic**

---

### Trap 4 — Bias Is a Percentage

False.

Bias does not mean:

+50 = 50% traffic

It changes:

**The size of the geographic region from which traffic is routed to the resource**

---

### Trap 5 — Geoproximity Only Works with AWS Resources

False.

Resources can be:

**AWS → Specify Region**

or:

**Non-AWS → Specify Latitude + Longitude**

---

### Trap 6 — Geoproximity Means Lowest Latency

False.

If the requirement is explicitly:

**Lowest network latency**

Choose:

[[Route 53 Latency Routing]]

---

### Trap 7 — Geoproximity Is Configured Like Every Other Routing Policy

The Maarek slides specifically call out:

**Route 53 Traffic Flow is required for Geoproximity Routing.**

---

## Quick Cheat Sheet

| Feature | Geoproximity Routing |
|---|---|
| Based On | User + Resource Geography |
| Bias | ✅ |
| Positive Bias | Expand territory |
| Positive Range | +1 to +99 |
| Negative Bias | Shrink territory |
| Negative Range | -1 to -99 |
| Zero Bias | No adjustment |
| AWS Resource Location | AWS Region |
| Non-AWS Resource Location | Latitude + Longitude |
| Hybrid Resources | ✅ |
| Traffic Flow Required | ✅ |
| Bias = Percentage | ❌ |
| Lowest Latency | ❌ |
| Explicit Country Rules | ❌ |

---

## Master Memory Trick

> [!tip] Master Memory Trick
> **Geoproximity = Geographic Magnet**
>
> Each resource acts like a magnet pulling nearby users toward it.
>
> **Positive Bias = Stronger Magnet**
>
> Pulls traffic from a larger area.
>
> **Negative Bias = Weaker Magnet**
>
> Pulls traffic from a smaller area.

Remember:

**User location rule → Geolocation**

**Fastest network → Latency**

**Percentage → Weighted**

**Geographic distance + Bias → Geoproximity**

And the strongest exam giveaway:

> **BIAS = GEOPROXIMITY**

---

## Related Notes

- [[Route 53]]
- [[Route 53 Routing Policies]]
- [[Route 53 Geolocation Routing]]
- [[Route 53 Latency Routing]]
- [[Route 53 Weighted Routing]]
- [[Route 53 Traffic Flow]]
- [[Route 53 Health Checks]]
- [[Hybrid Cloud]]
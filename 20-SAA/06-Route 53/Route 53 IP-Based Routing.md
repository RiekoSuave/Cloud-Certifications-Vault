## What Problem Does It Solve?

[[Route 53 IP-Based Routing]] routes DNS traffic based on the **client's IP address**.

It solves the problem of:

> **"I already know which client IP ranges should be routed to which endpoints."**

You define:

**Client CIDR Range → Destination**

Example:

203.0.113.0/24  
↓  
Endpoint A

200.5.4.0/24  
↓  
Endpoint B

> [!tip] Memory Trick
> **IP-Based Routing = I know your IP, so I know where to send you.**

---

## How IP-Based Routing Works

With IP-Based Routing, you provide Route 53 with:

1. Client IP address ranges
2. Corresponding endpoints

The IP ranges are defined using:

**CIDR blocks**

Example:

Location 1:

203.0.113.0/24

Location 2:

200.5.4.0/24

Then Route 53 can map:

203.0.113.0/24 → Endpoint A

200.5.4.0/24 → Endpoint B

Architecture:

Client  
↓  
Client IP Address  
↓  
[[Route 53]]  
↓  
Match IP to CIDR  
↓  
Return Configured Endpoint

---

## CIDR Collections

IP-Based Routing uses:

**CIDR Collections**

A CIDR Collection contains groups of client IP ranges that you want to associate with particular locations.

Example:

CIDR Collection

├── location-1  
│   └── 203.0.113.0/24  
│
└── location-2  
    └── 200.5.4.0/24

Then Route 53 records can reference those locations.

Conceptually:

Client IP  
↓  
CIDR Collection  
↓  
Location Match  
↓  
Route 53 Record  
↓  
Endpoint

---

## Example Architecture

Suppose:

User A:

203.0.113.56

User B:

200.5.4.100

You configure:

203.0.113.0/24 → location-1

200.5.4.0/24 → location-2

And:

location-1 → 1.2.3.4

location-2 → 5.6.7.8

### User A

203.0.113.56  
↓  
Matches 203.0.113.0/24  
↓  
location-1  
↓  
[[Route 53]] returns 1.2.3.4

### User B

200.5.4.100  
↓  
Matches 200.5.4.0/24  
↓  
location-2  
↓  
[[Route 53]] returns 5.6.7.8

The key is:

> **You explicitly define which IP ranges map to which endpoints.**

---

## Why Use IP-Based Routing?

IP-Based Routing gives you very precise control when you already understand the network origins of your users.

Common use cases include:

- Optimizing application performance
- Reducing network costs
- Routing particular ISP networks to specific endpoints
- Directing known client networks to preferred infrastructure

---

## ISP-Based Routing Example

This is an important example from the SAA slides.

Suppose users from:

ISP A

typically originate from a known CIDR range.

You know Endpoint A provides better connectivity for that ISP.

Configure:

ISP A CIDR Range  
↓  
[[Route 53 IP-Based Routing]]  
↓  
Endpoint A

Meanwhile:

ISP B CIDR Range  
↓  
Endpoint B

This gives you explicit network-based routing control.

> [!tip] Architecture Thinking
> **Known network range + known preferred endpoint = IP-Based Routing**

---

## IP-Based vs Geolocation

These can look similar because both may result in different users receiving different endpoints.

### IP-Based Routing

Uses:

**Explicit client IP/CIDR mappings**

You tell Route 53:

> "These IP ranges go here."

### [[Route 53 Geolocation Routing]]

Uses:

**User geographic location**

You tell Route 53:

> "Users from this country, continent, or U.S. state go here."

### Exam Decision

**CIDR / Client IP Range → IP-Based**

**Country / Continent / State → Geolocation**

---

## IP-Based vs Geoproximity

### IP-Based

Decision based on:

**Client IP CIDR**

No geographic bias is required.

### [[Route 53 Geoproximity Routing]]

Decision based on:

**User + Resource geography**

and supports:

**Bias**

### Memory Trick

**IP-Based = CIDR**

**Geoproximity = Geography + Bias**

---

## IP-Based vs Latency

### IP-Based

You explicitly configure:

**Which IP ranges use which endpoint**

### [[Route 53 Latency Routing]]

Route 53 determines:

**Which AWS Region provides the lowest network latency**

### Exam Decision

**Administrator knows preferred endpoint → IP-Based**

**Route 53 should determine fastest Region → Latency**

---

## IP-Based vs Weighted

### IP-Based

Routes according to:

**Source IP range**

### [[Route 53 Weighted Routing]]

Routes according to:

**Relative weights**

Example:

80 / 20

### Memory Trick

**IP-Based = Who are you?**

**Weighted = How much traffic?**

---

## Architecture Thinking

### Scenario 1 — Specific ISP

A company knows users from a particular ISP originate from:

203.0.113.0/24

Those users should always resolve to Endpoint A because it provides better network connectivity.

**Choose → [[Route 53 IP-Based Routing]]**

---

### Scenario 2 — Reduce Network Costs

A company knows certain client networks are cheaper to serve from a specific endpoint.

The company has a list of client CIDR ranges.

**Choose → IP-Based Routing**

Why?

The company already knows:

**Client Network → Preferred Endpoint**

---

### Scenario 3 — Canadian Users

A company wants all users geographically located in Canada to receive Canadian content.

No CIDR ranges are provided.

**Do NOT choose → IP-Based Routing**

Choose:

[[Route 53 Geolocation Routing]]

---

### Scenario 4 — Lowest Latency

A company operates globally and wants Route 53 to automatically determine which AWS Region gives each user the best network performance.

**Do NOT choose → IP-Based Routing**

Choose:

[[Route 53 Latency Routing]]

---

### Scenario 5 — Known Corporate Networks

A company has known client network ranges and wants:

Network A → Endpoint A

Network B → Endpoint B

Network C → Endpoint C

**Choose → IP-Based Routing**

The giveaway is:

**Known CIDR ranges**

---

## Scenario Recognition

### Immediately Think IP-Based Routing When You See

- Client IP address
- Source IP
- CIDR
- CIDR Collection
- Known network ranges
- User-IP-to-endpoint mapping
- Particular ISP
- Route specific client networks
- Reduce network costs using known IP ranges

### Strongest Keyword

> **CIDR → IP-Based Routing**

---

## Exam Traps

### Trap 1 — IP-Based Means Geolocation

False.

IP-Based Routing uses:

**Explicit CIDR mappings**

Geolocation uses:

**Geographic location rules**

---

### Trap 2 — Route 53 Automatically Finds the Lowest-Latency Endpoint

Not with IP-Based Routing.

You provide the:

**IP Range → Endpoint mapping**

For automatic lowest-latency selection:

Choose:

[[Route 53 Latency Routing]]

---

### Trap 3 — IP-Based Uses Percentages

False.

Percentage-based routing is:

[[Route 53 Weighted Routing]]

IP-Based uses:

**CIDR ranges**

---

### Trap 4 — IP-Based Requires Geographic Bias

False.

Bias belongs to:

[[Route 53 Geoproximity Routing]]

---

### Trap 5 — Client IP Means Individual IP Addresses Only

No.

CIDR blocks let you define entire network ranges.

Example:

203.0.113.0/24

can represent a group of client IP addresses.

---

## Quick Cheat Sheet

| Feature | IP-Based Routing |
|---|---|
| Decision Based On | Client IP |
| CIDR Blocks | ✅ |
| CIDR Collections | ✅ |
| User-IP-to-Endpoint Mapping | ✅ |
| Specific ISP Routing | ✅ |
| Performance Optimization | ✅ |
| Network Cost Optimization | ✅ |
| Country-Based | ❌ |
| Percentage-Based | ❌ |
| Lowest-Latency Automatic Selection | ❌ |
| Geographic Bias | ❌ |
| DNS-Level Routing | ✅ |

---

## Master Memory Trick

> [!tip] Master Memory Trick
> **IP-Based = CIDR Map**
>
> Think:
>
> **"If your IP belongs to THIS network, Route 53 gives you THAT endpoint."**

Remember:

**CIDR → IP-Based**

**Percentage → Weighted**

**Fastest → Latency**

**Country / Continent / State → Geolocation**

**Distance + Bias → Geoproximity**

And the strongest scenario clue:

> **Specific ISP → Specific Endpoint = IP-Based Routing**

---

## Related Notes

- [[Route 53]]
- [[Route 53 Routing Policies]]
- [[Route 53 Weighted Routing]]
- [[Route 53 Latency Routing]]
- [[Route 53 Geolocation Routing]]
- [[Route 53 Geoproximity Routing]]
- [[Route 53 Multi-Value Routing]]
- [[CIDR]]
- [[05-Networking/VPC]]
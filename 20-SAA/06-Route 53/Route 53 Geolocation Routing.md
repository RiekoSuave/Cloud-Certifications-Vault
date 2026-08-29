## What Problem Does It Solve?

[[Route 53 Geolocation Routing]] routes users based on **where the user is physically located**.

It solves the problem of:

> **"I want users from different geographic locations to receive different DNS answers."**

Examples:

Germany → European Website

United States → U.S. Website

Canada → Canadian Website

> [!tip] Memory Trick
> **Geolocation = Where is the USER?**
>
> If the exam mentions:
>
> **country, continent, U.S. state, localization, content restrictions**
>
> Think → [[Route 53 Geolocation Routing]]

---

## How Geolocation Routing Works

Route 53 looks at the user's geographic location and matches it against configured location rules.

You can define routing based on:

- Continent
- Country
- U.S. State

Example:

Users in Europe  
↓  
Endpoint A

Users in Canada  
↓  
Endpoint B

Users in California  
↓  
Endpoint C

Everyone else  
↓  
Default Endpoint

---

## Most Precise Location Wins

If multiple geolocation rules overlap, Route 53 chooses the:

**Most specific matching location**

Example:

You configure:

North America → Endpoint A

United States → Endpoint B

California → Endpoint C

A user in California matches all three.

Route 53 chooses:

**California → Endpoint C**

because it is the most specific rule.

> [!tip] Memory Trick
> **Specific beats broad**
>
> State beats Country  
> Country beats Continent

---

## Default Record

You should create a:

**Default Geolocation Record**

Why?

Some users may not match any configured geographic rule.

Example:

Europe → Endpoint A

Canada → Endpoint B

Default → Endpoint C

If a user comes from:

South America

and no specific rule exists:

Route 53 returns the:

**Default Record**

> [!warning] Exam Rule
> **Geolocation should include a Default record for unmatched locations.**

---

## Common Use Case — Website Localization

A company operates localized versions of its website.

Example:

Germany  
↓  
de.example.com

France  
↓  
fr.example.com

United States  
↓  
us.example.com

Route 53 can use Geolocation Routing to direct users based on location.

### Architecture Thinking

User Location  
↓  
[[Route 53 Geolocation Routing]]  
↓  
Localized Endpoint

---

## Common Use Case — Content Restrictions

Geolocation Routing can also be used to control which endpoint serves users in specific regions.

Example:

Users in Region A  
↓  
Restricted Content Endpoint

Users elsewhere  
↓  
General Endpoint

This is useful when content must differ because of:

- Licensing
- Legal restrictions
- Regional requirements
- Business policies

---

## Common Use Case — Geographic Load Distribution

Geolocation can also distribute users geographically.

Example:

Europe → Europe Stack

North America → North America Stack

Asia → Asia Stack

This gives you location-based routing across multiple application deployments.

Important:

This is not based on measured latency.

It is based on:

**Where the user is located**

---

## Geolocation Routing and Health Checks

Geolocation records can be associated with:

[[Route 53 Health Checks]]

This lets Route 53 avoid returning an unhealthy endpoint for a geographic rule.

Architecture:

User in Europe  
↓  
[[Route 53]]  
↓  
Europe Record  
↓  
Health Check  
├── Healthy → Return Europe Endpoint  
└── Unhealthy → Use another applicable healthy record

---

## Architecture Thinking

### Scenario 1 — Country-Specific Website

A company wants:

German users → German website

French users → French website

Canadian users → Canadian website

**Choose → [[Route 53 Geolocation Routing]]**

Why?

The routing rule is based on the user's country.

---

### Scenario 2 — U.S. State Routing

A company wants users in California to receive a different endpoint from users in the rest of the United States.

**Choose → Geolocation Routing**

Why?

Geolocation supports routing by:

**U.S. State**

---

### Scenario 3 — European Users Should Get European Content

The requirement says:

All users located in Europe should receive localized European content.

**Choose → Geolocation Routing**

Why?

The rule is based on continent.

---

### Scenario 4 — Lowest-Latency Region

A company wants every user routed to whichever AWS Region gives them the best network performance.

**Do NOT choose → Geolocation Routing**

Choose:

[[Route 53 Latency Routing]]

---

### Scenario 5 — Shift More Traffic Toward One Region

A company wants geographic routing, but also wants to intentionally expand one resource's traffic territory.

**Do NOT choose → Geolocation Routing**

Choose:

[[Route 53 Geoproximity Routing]]

because that policy supports:

**Bias**

---

## Geolocation vs Latency

This is a major exam distinction.

### Geolocation

Decision based on:

**User location**

Examples:

- Country
- Continent
- U.S. State

Question:

> Where is the user?

### Latency

Decision based on:

**Network performance**

Question:

> Which Region is fastest?

### Memory Trick

**Geolocation = WHERE**

**Latency = FASTEST**

---

## Geolocation vs Geoproximity

These two sound very similar.

### Geolocation

Uses explicit geographic rules.

Example:

Canada → Endpoint A

Europe → Endpoint B

### Geoproximity

Uses geographic distance between:

- Users
- Resources

and can modify the routing area using:

**Bias**

### Memory Trick

**Geolocation = Location Rules**

**Geoproximity = Distance + Bias**

---

## Geolocation vs Weighted

### Geolocation

Traffic distribution depends on:

**Where users are**

### Weighted

Traffic distribution depends on:

**Configured weights**

Example:

80 / 20

### Exam Decision

**Country / continent / state → Geolocation**

**Percentage → Weighted**

---

## Geolocation vs Failover

### Geolocation

Routes by:

**Location**

### Failover

Routes by:

**Primary health**

### Exam Decision

**Localization → Geolocation**

**Disaster Recovery → Failover**

---

## Scenario Recognition

### Immediately Think Geolocation Routing When You See

- Country
- Continent
- U.S. State
- User location
- Localization
- Country-specific content
- Regional website
- Geographic restrictions
- Legal/content restrictions
- Default geographic rule

### Strongest Keyword

> **Route based on where the user is located → Geolocation**

---

## Exam Traps

### Trap 1 — Geolocation Means Lowest Latency

False.

A user in Germany does not automatically get the endpoint with the best latency.

Geolocation uses:

**Location rules**

not latency measurements.

---

### Trap 2 — Geolocation Uses Resource Location

The key decision is based on:

**User location**

Do not confuse it with Geoproximity, which considers both user and resource geography.

---

### Trap 3 — No Default Record Needed

Bad idea.

If no location rule matches, Route 53 needs a default response.

Remember:

**Create a Default Record**

---

### Trap 4 — Overlapping Rules Are Random

False.

When location rules overlap:

**Most precise location wins**

Example:

California beats United States

United States beats North America

---

### Trap 5 — Geolocation Cannot Use Health Checks

False.

Geolocation records:

**Can be associated with [[Route 53 Health Checks]]**

---

## Quick Cheat Sheet

| Feature | Geolocation Routing |
|---|---|
| Decision Based On | User location |
| Continent | ✅ |
| Country | ✅ |
| U.S. State | ✅ |
| Most Precise Match Wins | ✅ |
| Default Record Recommended | ✅ |
| Health Checks | ✅ |
| Localization | ✅ |
| Content Restrictions | ✅ |
| Lowest Latency | ❌ |
| Bias | ❌ |
| DNS-Level Routing | ✅ |

---

## Master Memory Trick

> [!tip] Master Memory Trick
> **Geolocation = Where is the USER?**
>
> Route 53 asks:
>
> **"Where are you coming from?"**

Remember:

**Country / Continent / State → Geolocation**

**Fastest Region → Latency**

**Distance + Bias → Geoproximity**

**Percentage → Weighted**

**Primary / Backup → Failover**

And the sneaky rule:

> **When rules overlap, the most precise location wins.**

---

## Related Notes

- [[Route 53]]
- [[Route 53 Routing Policies]]
- [[Route 53 Latency Routing]]
- [[Route 53 Geoproximity Routing]]
- [[Route 53 Weighted Routing]]
- [[Route 53 Failover Routing]]
- [[Route 53 Health Checks]]
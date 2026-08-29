## Route 53 Exam Decision Map

When you see a Route 53 question, first ask:

> **"What is Route 53 being asked to decide?"**

| Requirement | Think |
|---|---|
| One basic DNS destination | [[Route 53 Simple Routing]] |
| Percentage / traffic split | [[Route 53 Weighted Routing]] |
| Lowest network latency | [[Route 53 Latency Routing]] |
| Primary + backup | [[Route 53 Failover Routing]] |
| User country / continent / U.S. state | [[Route 53 Geolocation Routing]] |
| Geography + bias | [[Route 53 Geoproximity Routing]] |
| Client IP / CIDR | [[Route 53 IP-Based Routing]] |
| Multiple healthy DNS answers | [[Route 53 Multi-Value Routing]] |

> [!tip] Master Routing Memory Trick
> **Simple = One**
>
> **Weighted = Percentage**
>
> **Latency = Fastest**
>
> **Failover = Backup**
>
> **Geolocation = Where is the user?**
>
> **Geoproximity = Geography + Bias**
>
> **IP-Based = CIDR**
>
> **Multi-Value = Many Healthy Answers**

---

## Route 53 Core Architecture

[[Route 53]] is:

- Highly available
- Scalable
- Fully managed
- Authoritative DNS
- Domain registrar
- DNS routing service
- Health checking service

Route 53 connects:

Domain Name  
↓  
DNS Record  
↓  
AWS Resource / IP Address

Example:

www.example.com  
↓  
[[Route 53]]  
↓  
[[Application Load Balancer]]

---

## Route 53 Records

Important record types:

| Record | Purpose |
|---|---|
| A | Hostname → IPv4 |
| AAAA | Hostname → IPv6 |
| CNAME | Hostname → Another hostname |
| NS | Hosted Zone Name Servers |
| Alias | Hostname → Supported AWS resource |

Other records can appear, but these are especially important for SAA architecture questions.

---

## A Record

Maps:

**Hostname → IPv4**

Example:

example.com  
↓  
192.0.2.10

Think:

**A = IPv4 Address**

---

## AAAA Record

Maps:

**Hostname → IPv6**

Example:

example.com  
↓  
2001:db8::1

Think:

**AAAA = IPv6**

---

## CNAME Record

Maps:

**Hostname → Another hostname**

Example:

www.example.com  
↓  
app.example.net

Important limitation:

CNAME cannot be used at the:

**Zone Apex**

Example:

example.com

cannot normally be a CNAME.

But:

www.example.com

can.

---

## Alias Record

[[Route 53 Alias Records]] map a hostname to supported AWS resources.

Examples:

- [[Application Load Balancer]]
- [[Network Load Balancer]]
- [[05-Networking/CloudFront]]
- [[S3]] website endpoint
- [[API Gateway]]
- Another Route 53 record

Major advantages:

- Can work at Zone Apex
- Native AWS integration
- No charge for Alias queries to supported AWS targets
- Can evaluate target health

> [!tip] Memory Trick
> **AWS Resource + Zone Apex → Think Alias**

---

## Alias vs CNAME

| Feature | Alias | CNAME |
|---|---|---|
| AWS-specific Route 53 feature | ✅ | ❌ |
| Points to hostname | ✅ | ✅ |
| Zone Apex | ✅ | ❌ |
| Supported AWS Resources | ✅ | Generic |
| Evaluate Target Health | ✅ | ❌ |
| Standard DNS Record | ❌ | ✅ |

### Exam Pattern

Need:

example.com  
↓  
[[Application Load Balancer]]

**Choose → Alias**

---

## Route 53 TTL

[[Route 53 TTL]] controls how long DNS resolvers cache a DNS response.

### High TTL

Advantages:

- Fewer DNS queries
- Lower DNS query cost

Disadvantages:

- DNS changes propagate more slowly

### Low TTL

Advantages:

- Faster DNS changes
- Useful during migrations

Disadvantages:

- More DNS queries
- Higher DNS query cost

> [!tip] Memory Trick
> **High TTL = Cheap + Slow Change**
>
> **Low TTL = Costlier + Fast Change**

---

# Routing Policies

## Simple Routing

[[Route 53 Simple Routing]]

Use when:

> **"Just send users to this resource."**

Characteristics:

- Basic DNS routing
- Can return multiple values
- No health checks

### Exam Keyword

**Basic / Single Resource → Simple**

---

## Weighted Routing

[[Route 53 Weighted Routing]]

Routes according to:

**Relative weights**

Example:

80 → Production

20 → New Version

Use cases:

- Blue/green deployments
- Canary releases
- Gradual migrations
- A/B testing
- Traffic splitting

Weights do not need to add to 100.

### Special Rule

Weight:

**0**

can stop traffic from being sent to a resource.

### Exam Keyword

> **Percentage / Traffic Split → Weighted**

---

## Latency Routing

[[Route 53 Latency Routing]]

Routes users to the AWS Region providing:

**Lowest network latency**

Important:

Geographically closest does NOT necessarily mean lowest latency.

Example:

German User  
↓  
U.S. Region

is possible if the U.S. Region provides lower network latency.

Can work with:

[[Route 53 Health Checks]]

### Exam Keyword

> **Best Performance / Lowest Latency → Latency**

---

## Failover Routing

[[Route 53 Failover Routing]]

Provides:

**Active-Passive DNS Failover**

Architecture:

Primary  
↓ unhealthy  
Secondary

Used for:

- Disaster recovery
- Primary / backup architectures
- Cross-Region failover

The Primary record requires a:

[[Route 53 Health Checks|Health Check]]

### Exam Keyword

> **Primary + Secondary → Failover**

---

## Geolocation Routing

[[Route 53 Geolocation Routing]]

Routes according to:

**User location**

Supports:

- Continent
- Country
- U.S. State

When multiple rules overlap:

**Most precise location wins**

Example:

California  
beats  
United States  
beats  
North America

Create a:

**Default Record**

for users who do not match another location.

### Exam Keyword

> **Country / Continent / State → Geolocation**

---

## Geoproximity Routing

[[Route 53 Geoproximity Routing]]

Routes based on:

- User location
- Resource location

and supports:

**Bias**

### Positive Bias

Expands geographic traffic area.

**More traffic**

### Negative Bias

Shrinks geographic traffic area.

**Less traffic**

AWS Resource:

Specify AWS Region

Non-AWS Resource:

Specify Latitude + Longitude

Associated with:

[[Route 53 Traffic Flow]]

### Exam Keyword

> **BIAS → Geoproximity**

---

## IP-Based Routing

[[Route 53 IP-Based Routing]]

Routes according to:

**Client IP address / CIDR range**

You define:

Client CIDR  
↓  
Endpoint

Useful for:

- Known ISP networks
- Performance optimization
- Network cost optimization
- Explicit network-to-endpoint mapping

Uses:

**CIDR Collections**

### Exam Keyword

> **CIDR / Client IP → IP-Based**

---

## Multi-Value Routing

[[Route 53 Multi-Value Routing]]

Returns:

**Multiple healthy DNS records**

Supports:

[[Route 53 Health Checks]]

Can return:

**Up to 8 healthy records per DNS query**

Important:

> **Multi-Value is NOT a replacement for ELB.**

### Exam Keyword

> **Multiple Healthy Answers → Multi-Value**

---

# Routing Policy Comparison

| Policy | Decision Based On | Health Checks | Key Scenario |
|---|---|---:|---|
| Simple | Basic DNS | ❌ | One/basic resource |
| Weighted | Relative weights | ✅ | Traffic percentage |
| Latency | Network latency | ✅ | Fastest Region |
| Failover | Primary health | ✅ | Active-passive DR |
| Geolocation | User location | ✅ | Country / continent |
| Geoproximity | Geography + Bias | Depends on architecture | Shift geographic traffic |
| IP-Based | Client CIDR | Depends on record | Known network |
| Multi-Value | Resource health | ✅ | Several healthy answers |

---

# Route 53 Health Checks

[[Route 53 Health Checks]] enable:

**Automated DNS Failover**

Three important types:

1. Endpoint
2. Calculated
3. CloudWatch Alarm

---

## Endpoint Health Checks

Can directly monitor public endpoints using:

- HTTP
- HTTPS
- TCP

HTTP/HTTPS success:

**2xx / 3xx**

Default interval:

**30 seconds**

Faster option:

**10 seconds**

but costs more.

Default threshold:

**3 consecutive checks**

Can inspect the first:

**5120 bytes**

of the response for expected text.

---

## Calculated Health Checks

[[Route 53 Calculated Health Checks]] combine other health checks.

Supports:

- AND
- OR
- NOT

Maximum:

**256 child health checks**

Think:

> **"How healthy must the overall system be?"**

---

## Private Resource Health Checks

Route 53 health checkers are outside your VPC.

Therefore:

They cannot directly check private resources.

Use:

Private Resource  
↓  
[[07-Monitoring/CloudWatch]] Metric  
↓  
[[CloudWatch Alarms|CloudWatch Alarm]]  
↓  
Route 53 Health Check

> [!tip] Memory Trick
> **Public = Direct Check**
>
> **Private = CloudWatch Alarm**

---

# Route 53 Resolver

[[20-SAA/06-Route 53/Route 53 Resolver]] provides DNS resolution inside a [[05-Networking/VPC]] and enables hybrid DNS.

VPC Resolver address:

**VPC CIDR + 2**

Example:

10.0.0.0/16  
↓  
10.0.0.2

Also available at:

169.254.169.253

---

## Resolver Direction

This is one of the most important Route 53 architecture patterns.

### On-Prem → AWS

Use:

[[Route 53 Resolver Inbound Endpoint]]

Think:

**DNS enters AWS**

---

### AWS → On-Prem

Use:

[[Route 53 Resolver Outbound Endpoint]]

+

[[Route 53 Resolver Rules]]

Think:

**DNS exits AWS**

---

## Inbound Endpoint

[[Route 53 Resolver Inbound Endpoint]]

Use when:

**On-Premises needs to resolve AWS private DNS**

Architecture:

On-Prem DNS  
↓  
[[05-Networking/Site-to-Site VPN]] / [[05-Networking/Direct Connect]]  
↓  
Inbound Endpoint  
↓  
Route 53 Private DNS

### Memory Trick

**On-Prem → AWS = INBOUND**

---

## Outbound Endpoint

[[Route 53 Resolver Outbound Endpoint]]

Use when:

**AWS needs to resolve On-Premises DNS**

Architecture:

[[EC2]]  
↓  
[[20-SAA/06-Route 53/Route 53 Resolver]]  
↓  
[[Route 53 Resolver Rules|Resolver Rule]]  
↓  
Outbound Endpoint  
↓  
On-Prem DNS

### Memory Trick

**AWS → On-Prem = OUTBOUND**

---

## Resolver Rules

[[Route 53 Resolver Rules]] provide:

**Conditional DNS Forwarding**

Example:

corp.internal  
↓  
Forward to  
10.50.0.10

Think:

> **IF domain = corp.internal → send to corporate DNS**

Important:

**Most specific matching rule wins**

Rules can be shared across accounts using:

[[AWS RAM]]

---

## Hybrid DNS Architecture

Two-way DNS:

On-Premises  
↓  
Inbound Endpoint  
↓  
AWS DNS

and:

AWS  
↓  
Outbound Endpoint + Resolver Rule  
↓  
On-Prem DNS

> [!tip] Master Memory Trick
> **Follow the DNS query arrow**
>
> Into AWS = Inbound
>
> Out of AWS = Outbound

---

## Resolver Does Not Create Connectivity

Route 53 Resolver solves:

**DNS**

It does not create:

**Network connectivity**

Hybrid networking still requires something such as:

- [[05-Networking/Site-to-Site VPN]]
- [[05-Networking/Direct Connect]]

### Exam Trap

DNS successfully resolves:

database.corp.internal  
↓  
10.50.20.25

but EC2 cannot connect.

Check:

- Routing
- VPN / Direct Connect
- [[Security Groups]]
- Network ACLs

not necessarily DNS.

---

# Third-Party Registrar

[[3rd Party Registrar with Route 53]]

Domain registration and DNS hosting can be separate.

Example:

Registrar  
↓  
GoDaddy

DNS  
↓  
[[Route 53]]

To use Route 53 DNS:

1. Create Public Hosted Zone
2. Get Route 53 Name Servers
3. Update NS records at registrar
4. Route 53 becomes authoritative DNS

### Exam Rule

> **You do NOT need to transfer the domain to Route 53.**

### Memory Trick

**Registrar owns the NAME**

**Route 53 can answer for the NAME**

**NS records connect them**

---

# DNSSEC

[[Route 53 DNSSEC]]

Protects DNS against:

- Spoofing
- Cache poisoning
- DNS record tampering

Provides:

- Authentication
- Integrity

Does NOT provide:

- Encryption
- Confidentiality

---

## DNSSEC Signing vs Validation

### Signing

Sign your:

**Public Hosted Zone**

Think:

> **Create DNS signatures**

### Validation

[[20-SAA/06-Route 53/Route 53 Resolver]] verifies:

**DNSSEC signatures**

Think:

> **Verify DNS signatures**

---

## DNSSEC Keys

### ZSK

**Zone-Signing Key**

Signs:

DNS records

### KSK

**Key-Signing Key**

Signs:

ZSK

Architecture:

KSK  
↓  
ZSK  
↓  
DNS Records

KSK uses:

[[06-Security/KMS]]

Remember:

**KMS key → us-east-1**

---

## DS Record

The:

**Delegation Signer Record**

connects your signed zone to the parent DNS hierarchy.

Think:

Parent Zone  
↓  
DS Record  
↓  
Your Signed Zone

This establishes the:

**Chain of Trust**

---

# Traffic Flow

[[Route 53 Traffic Flow]]

Provides a:

**Visual DNS routing policy editor**

Best for:

- Complex routing
- Multiple routing decisions
- Reusable traffic policies
- Multi-Region DNS architectures

Think:

Routing Policies  
↓  
Building Blocks

Traffic Flow  
↓  
Visual Architecture Builder

Strong association:

[[Route 53 Geoproximity Routing]]

↓

**Traffic Flow**

---

# High-Value Exam Comparisons

## Weighted vs Latency

**Weighted**

Question:

> How much traffic?

**Latency**

Question:

> Which Region is fastest?

---

## Latency vs Geolocation

**Latency**

Based on:

Network performance

**Geolocation**

Based on:

User location

---

## Geolocation vs Geoproximity

**Geolocation**

Country / continent / U.S. state rules

**Geoproximity**

User + resource geography + bias

---

## Simple vs Multi-Value

**Simple**

Multiple values possible

No health checks

**Multi-Value**

Multiple healthy values

Health checks supported

Up to 8 healthy records

---

## Failover vs Multi-Value

**Failover**

Primary OR Secondary

**Multi-Value**

Several healthy endpoints

---

## Alias vs CNAME

**CNAME**

Hostname → Hostname

Cannot use Zone Apex

**Alias**

Hostname → Supported AWS Resource

Can use Zone Apex

---

## Inbound vs Outbound Resolver

**On-Prem → AWS**

Inbound

**AWS → On-Prem**

Outbound + Rule

---

# Scenario Recognition

## If You See...

### "20% of traffic"

→ [[Route 53 Weighted Routing]]

### "Lowest latency"

→ [[Route 53 Latency Routing]]

### "Primary and disaster recovery"

→ [[Route 53 Failover Routing]]

### "Users in Germany"

→ [[Route 53 Geolocation Routing]]

### "Bias"

→ [[Route 53 Geoproximity Routing]]

### "Client CIDR"

→ [[Route 53 IP-Based Routing]]

### "Return several healthy endpoints"

→ [[Route 53 Multi-Value Routing]]

### "example.com → ALB"

→ [[Route 53 Alias Records]]

### "On-prem resolves AWS private DNS"

→ [[Route 53 Resolver Inbound Endpoint]]

### "EC2 resolves on-prem DNS"

→ [[Route 53 Resolver Outbound Endpoint]] + [[Route 53 Resolver Rules]]

### "Private endpoint health"

→ [[CloudWatch Alarms|CloudWatch Alarm]] + [[Route 53 Health Checks]]

### "DNS spoofing"

→ [[Route 53 DNSSEC]]

### "Third-party registrar"

→ Update **NS records** to Route 53 Name Servers

---

# Biggest Exam Traps

## Trap 1 — Geographically Closest = Lowest Latency

False.

[[Route 53 Latency Routing]] uses network performance.

---

## Trap 2 — Geolocation = Geoproximity

False.

**Geolocation = User location rules**

**Geoproximity = Geography + Bias**

---

## Trap 3 — Multi-Value = ELB

False.

Multi-Value operates at:

**DNS level**

[[Elastic Load Balancing]] operates at:

**Traffic/request level**

---

## Trap 4 — CNAME at Zone Apex

Not allowed.

Use:

[[Route 53 Alias Records]]

for supported AWS resources.

---

## Trap 5 — Route 53 Directly Health Checks Private Resources

No.

Use:

[[CloudWatch Alarms]]

---

## Trap 6 — Reverse Inbound and Outbound

Follow the DNS query:

**On-Prem → AWS = Inbound**

**AWS → On-Prem = Outbound**

---

## Trap 7 — DNSSEC Encrypts DNS

False.

DNSSEC provides:

**Integrity + Authentication**

---

## Trap 8 — Bias = Percentage

False.

Bias changes:

**Geographic traffic boundaries**

Weighted Routing controls:

**Relative traffic distribution**

---

## Trap 9 — Route 53 Resolver Creates Hybrid Connectivity

False.

Resolver provides:

**DNS**

[[05-Networking/Site-to-Site VPN]] / [[05-Networking/Direct Connect]] provide:

**Network connectivity**

---

## Final Quick Cheat Sheet

| Exam Phrase | Answer |
|---|---|
| Basic DNS | Simple |
| Percentage | Weighted |
| Lowest latency | Latency |
| Primary / Secondary | Failover |
| Country / Continent / State | Geolocation |
| Bias | Geoproximity |
| CIDR | IP-Based |
| Multiple healthy answers | Multi-Value |
| Public endpoint health | Endpoint Health Check |
| Private endpoint health | CloudWatch Alarm |
| On-Prem → AWS DNS | Inbound Resolver |
| AWS → On-Prem DNS | Outbound Resolver + Rule |
| Domain-specific forwarding | Resolver Rule |
| Zone Apex → AWS Resource | Alias |
| External registrar + Route 53 | Change NS records |
| DNS authenticity / integrity | DNSSEC |
| Complex visual DNS | Traffic Flow |

---

## Master Memory Trick

> [!tip] Route 53 Master Memory Trick
> **WHO gets traffic?**
>
> Country → **Geolocation**
>
> CIDR → **IP-Based**
>
> **HOW MUCH traffic?**
>
> Percentage → **Weighted**
>
> **WHERE should traffic go?**
>
> Fastest → **Latency**
>
> Primary fails → **Failover**
>
> Geography + Bias → **Geoproximity**
>
> Several healthy endpoints → **Multi-Value**
>
> **HOW does hybrid DNS flow?**
>
> On-Prem → AWS → **Inbound**
>
> AWS → On-Prem → **Outbound + Rule**
>
> **HOW do I trust DNS?**
>
> → **DNSSEC**
>
> **HOW do I point the root domain to AWS?**
>
> → **Alias**

---

## Related Notes

- [[Route 53]]
- [[Route 53 Records]]
- [[Route 53 Alias Records]]
- [[Route 53 TTL]]
- [[Route 53 Routing Policies]]
- [[Route 53 Simple Routing]]
- [[Route 53 Weighted Routing]]
- [[Route 53 Latency Routing]]
- [[Route 53 Failover Routing]]
- [[Route 53 Geolocation Routing]]
- [[Route 53 Geoproximity Routing]]
- [[Route 53 IP-Based Routing]]
- [[Route 53 Multi-Value Routing]]
- [[Route 53 Health Checks]]
- [[20-SAA/06-Route 53/Route 53 Resolver]]
- [[Route 53 Resolver Inbound Endpoint]]
- [[Route 53 Resolver Outbound Endpoint]]
- [[Route 53 Resolver Rules]]
- [[Route 53 DNSSEC]]
- [[Route 53 Traffic Flow]]
- [[3rd Party Registrar with Route 53]]
- [[AWS RAM]]
- [[05-Networking/Direct Connect]]
- [[05-Networking/Site-to-Site VPN]]
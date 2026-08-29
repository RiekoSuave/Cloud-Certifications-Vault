## What Problem Does It Solve?

[[Route 53 Resolver Outbound Endpoint]] allows DNS queries originating inside AWS to be **forwarded to DNS resolvers outside AWS**.

Its most important SAA use case is:

> **"How can resources in my VPC resolve private DNS names hosted on-premises?"**

Think:

AWS  
↓ DNS Query  
[[Route 53 Resolver Outbound Endpoint]]  
↓  
On-Premises DNS

> [!tip] Memory Trick
> **Outbound = DNS goes OUT of AWS**
>
> **AWS → On-Prem = OUTBOUND**

---

## The Hybrid DNS Problem

Suppose a company has:

### AWS

[[EC2]] instances inside a [[05-Networking/VPC]]

### On-Premises

A private DNS zone:

corp.internal

with:

database.corp.internal  
↓  
10.50.20.25

An EC2 application needs to connect to:

database.corp.internal

But the DNS record exists only on the company's:

**On-Premises DNS Servers**

Solution:

**Route 53 Resolver Outbound Endpoint + Resolver Rule**

---

## Outbound Endpoint Architecture

Architecture:

[[EC2]]  
↓  
DNS Query for database.corp.internal  
↓  
[[20-SAA/06-Route 53/Route 53 Resolver]]  
↓  
[[Route 53 Resolver Rules|Resolver Rule]]  
↓  
[[Route 53 Resolver Outbound Endpoint]]  
↓  
[[05-Networking/Site-to-Site VPN]] / [[05-Networking/Direct Connect]]  
↓  
On-Premises DNS Server  
↓  
DNS Answer

The answer then returns to the EC2 application.

---

## Follow the DNS Query

The easiest way to recognize an Outbound Endpoint is to follow the DNS query.

Ask:

> **Which direction is the DNS query moving relative to AWS?**

If:

AWS  
↓  
On-Premises

the query is leaving AWS.

Therefore:

**Outbound Endpoint**

### Master Direction Rule

**On-Prem → AWS = [[Route 53 Resolver Inbound Endpoint|INBOUND]]**

**AWS → On-Prem = OUTBOUND**

---

## Outbound Endpoints Work with Resolver Rules

This is extremely important.

An Outbound Endpoint alone does not know:

> **Which DNS queries should be sent on-premises?**

That decision is controlled by:

[[Route 53 Resolver Rules]]

A Resolver Rule defines:

**Domain → Target DNS Servers**

Example:

corp.internal  
↓  
Forward To  
↓  
10.50.0.10  
10.50.0.11

Architecture:

Query for:

database.corp.internal  
↓  
Rule matches corp.internal  
↓  
Outbound Endpoint  
↓  
On-Prem DNS Servers

> [!tip] Memory Trick
> **Outbound = Exit Door**
>
> **Resolver Rule = Directions telling DNS which door to use**

---

## Conditional Forwarding

Resolver Rules provide:

**Conditional Forwarding**

This means Route 53 forwards only queries that match a particular DNS namespace.

Example:

corp.internal  
↓  
Forward to On-Prem DNS

But:

amazonaws.com  
↓  
Resolve normally

and:

example.com  
↓  
Normal DNS resolution

### Architecture Thinking

You are telling Route 53:

> **"If the query ends in corp.internal, send it to our corporate DNS servers."**

---

## Example

Suppose the on-premises environment hosts:

company.internal

On-prem DNS Servers:

10.100.0.10  
10.100.0.11

Create a Resolver Rule:

Domain:

company.internal

Target IPs:

10.100.0.10  
10.100.0.11

Then associate the rule with the VPC.

Now:

[[EC2]]  
↓  
app.company.internal?  
↓  
[[20-SAA/06-Route 53/Route 53 Resolver]]  
↓  
Matches company.internal  
↓  
Outbound Endpoint  
↓  
10.100.0.10 / 10.100.0.11  
↓  
DNS Answer

---

## Resolver Rule Association

Resolver Rules are associated with:

[[05-Networking/VPC]]

This determines which VPCs use the rule.

Example:

Resolver Rule:

corp.internal  
↓  
Associated with VPC-A

Resources in:

VPC-A

can use that forwarding rule.

This becomes especially important in:

- Multi-VPC architectures
- Multi-account architectures
- Centralized networking designs

---

## Outbound Endpoint IP Addresses

Like Inbound Endpoints, Outbound Endpoints are created inside your:

[[05-Networking/VPC]]

They use IP addresses from VPC subnets.

For high availability, deploy endpoint IPs across multiple:

[[Availability Zones]]

Example:

VPC  
├── AZ-A
│   └── Outbound Resolver IP
│
└── AZ-B
    └── Outbound Resolver IP

> [!tip] Architecture Pattern
> **Production Resolver Endpoint → Multi-AZ**

---

## Network Connectivity Is Required

The Outbound Endpoint does **not** create connectivity to your on-premises DNS server.

You still need:

- [[05-Networking/Site-to-Site VPN]]
- [[05-Networking/Direct Connect]]

Architecture:

AWS DNS Query  
↓  
Outbound Endpoint  
↓  
Hybrid Network Connection  
↓  
On-Prem DNS

Think:

**Resolver = DNS**

**VPN / Direct Connect = Connectivity**

---

## Security Groups

Resolver Outbound Endpoints use:

[[Security Groups]]

The Security Group must permit DNS traffic toward the target DNS servers.

DNS commonly uses:

- UDP port 53
- TCP port 53

If traffic is blocked:

Outbound Endpoint  
↓  
X Security Group / Network  
↓  
On-Prem DNS

DNS resolution fails.

---

## Outbound Endpoint Does Not Host DNS Records

This is important.

The Outbound Endpoint does not contain:

- DNS zones
- DNS records
- Hostname mappings

It simply provides a path for DNS queries to leave AWS.

The actual DNS records remain on:

**On-Premises DNS Servers**

### Memory Trick

**Outbound Endpoint = DNS Highway**

**On-Prem DNS = Destination holding the records**

---

## Resolver Rules Can Be Shared

In larger AWS environments, multiple accounts or VPCs may need the same forwarding rules.

Resolver Rules can be shared using:

[[AWS RAM]]

Example:

Central Networking Account  
↓  
Resolver Rule:
corp.internal  
↓  
[[AWS RAM]]  
↓  
Application Account A  
Application Account B  
Application Account C

This allows centralized hybrid DNS management.

---

## Centralized DNS Architecture

A common enterprise architecture is:

Central Networking Account  
↓  
Outbound Resolver Endpoint  
↓  
On-Premises DNS

Then:

Resolver Rules  
↓  
Shared with other accounts using [[AWS RAM]]

Application VPCs  
↓  
Use Shared Resolver Rules

This avoids creating duplicate forwarding configurations in every AWS account.

---

## Architecture Thinking

### Scenario 1 — EC2 Resolves Corporate DNS

An EC2 application needs to resolve:

database.corp.internal

The DNS record exists only on the company's on-premises DNS servers.

**Choose → Outbound Endpoint + Resolver Rule**

Architecture:

[[EC2]]  
↓  
Resolver Rule  
↓  
Outbound Endpoint  
↓  
[[05-Networking/Direct Connect]] / [[05-Networking/Site-to-Site VPN]]  
↓  
Corporate DNS

---

### Scenario 2 — On-Premises Resolves AWS Private Zone

An on-premises application needs to resolve:

database.aws.internal

which exists in a Route 53 Private Hosted Zone.

**Do NOT choose → Outbound**

Choose:

[[Route 53 Resolver Inbound Endpoint]]

Why?

The DNS query is:

On-Prem → AWS

---

### Scenario 3 — Only Corporate Domain Goes On-Premises

A company wants:

corp.internal  
↓  
On-Prem DNS

but all normal public DNS queries should continue using standard Route 53 Resolver behavior.

**Choose → Resolver Rule for corp.internal**

This is:

**Conditional Forwarding**

---

### Scenario 4 — Multiple Accounts Need Corporate DNS

Twenty AWS accounts need to resolve:

corp.internal

through the same corporate DNS infrastructure.

Instead of independently managing the same rules everywhere:

Create Resolver Rules centrally  
↓  
Share using [[AWS RAM]]

---

## Outbound vs Inbound

| Requirement | Endpoint |
|---|---|
| AWS → On-Prem DNS | Outbound |
| On-Prem → AWS DNS | Inbound |
| EC2 resolves corporate DNS | Outbound |
| Corporate DNS resolves Private Hosted Zone | Inbound |
| Query exits AWS | Outbound |
| Query enters AWS | Inbound |
| Resolver Rule commonly required | Outbound |

---

## Outbound Endpoint vs Resolver Rule

These are complementary but different.

### Outbound Endpoint

Provides:

**The network path for DNS queries to leave Route 53 Resolver**

Think:

**Where DNS exits AWS**

---

### Resolver Rule

Defines:

**Which DNS queries should be forwarded and where**

Think:

**Which domain goes to which DNS server**

### Memory Trick

**Outbound Endpoint = HOW it leaves**

**Resolver Rule = WHAT gets forwarded + WHERE it goes**

---

## Scenario Recognition

### Immediately Think Outbound Endpoint When You See

- AWS → On-Premises
- EC2 resolving corporate DNS
- Private on-premises domain
- DNS queries leaving AWS
- Forward DNS to on-premises
- Conditional forwarding
- Resolver Rule
- Corporate DNS server
- Hybrid DNS from VPC

### Strongest Exam Pattern

> **AWS needs On-Prem DNS = OUTBOUND + RULE**

---

## Exam Traps

### Trap 1 — Outbound Means On-Premises Queries AWS

False.

That is:

[[Route 53 Resolver Inbound Endpoint]]

Outbound means:

**DNS leaves AWS**

---

### Trap 2 — Outbound Endpoint Alone Handles Domain Matching

False.

Use:

[[Route 53 Resolver Rules]]

to determine which domains are forwarded.

---

### Trap 3 — Resolver Rule Creates Network Connectivity

False.

You still need:

[[05-Networking/Site-to-Site VPN]]

or:

[[05-Networking/Direct Connect]]

---

### Trap 4 — Outbound Endpoint Stores Corporate DNS Records

False.

The records remain on the authoritative:

**On-Premises DNS Server**

---

### Trap 5 — All AWS DNS Must Be Forwarded On-Premises

False.

Resolver Rules provide conditional forwarding.

Only matching DNS namespaces need to be forwarded.

---

### Trap 6 — Resolver Rules Must Be Recreated in Every Account

Not necessarily.

They can be shared using:

[[AWS RAM]]

---

## Quick Cheat Sheet

| Feature | Outbound Endpoint |
|---|---|
| Primary Direction | AWS → On-Prem |
| DNS Query Leaves AWS | ✅ |
| EC2 Resolves Corporate DNS | ✅ |
| Resolver Rule | ✅ |
| Conditional Forwarding | ✅ |
| Lives in VPC | ✅ |
| Multi-AZ for HA | ✅ |
| Security Group | ✅ |
| DNS Port | 53 |
| VPN / Direct Connect Still Needed | ✅ |
| Rules Shareable with AWS RAM | ✅ |
| Stores DNS Records | ❌ |
| On-Prem → AWS DNS | ❌ |

---

## Master Memory Trick

> [!tip] Master Memory Trick
> **Stand inside AWS and follow the DNS query.**
>
> AWS  
> ↓  
> ↓  
> **OUT to On-Prem**
>
> = **OUTBOUND**
>
> Then ask:
>
> **"Which domain should leave AWS?"**
>
> That is the:
>
> **Resolver Rule**

Remember:

**AWS → On-Prem = Outbound + Rule**

**On-Prem → AWS = Inbound**

**Resolver = DNS**

**VPN / Direct Connect = Network**

---

## Related Notes

- [[Route 53]]
- [[20-SAA/06-Route 53/Route 53 Resolver]]
- [[Route 53 Resolver Inbound Endpoint]]
- [[Route 53 Resolver Rules]]
- [[Route 53 Private Hosted Zones]]
- [[05-Networking/VPC]]
- [[Availability Zones]]
- [[Security Groups]]
- [[05-Networking/Site-to-Site VPN]]
- [[05-Networking/Direct Connect]]
- [[AWS RAM]]
- [[AWS Organizations]]
- [[Hybrid Cloud]]
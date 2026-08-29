## What Problem Does It Solve?

[[Route 53 Resolver Rules]] control **how DNS queries are handled for specific domain names**.

Their most important hybrid DNS use case is:

> **"When an AWS resource queries a particular private domain, where should Route 53 send that DNS query?"**

Example:

corp.internal  
↓  
Forward to On-Prem DNS

Other DNS Names  
↓  
Resolve Normally

> [!tip] Memory Trick
> **Resolver Rule = DNS Traffic Sign**
>
> It tells Route 53:
>
> **"If you see THIS domain, send it THERE."**

---

## Resolver Rules and Conditional Forwarding

Resolver Rules provide:

**Conditional DNS Forwarding**

Instead of forwarding every DNS query to the same destination, you define rules for specific domains.

Example:

corp.internal  
↓  
On-Prem DNS

partner.internal  
↓  
Partner DNS

Everything Else  
↓  
Normal Route 53 Resolution

This gives you precise control over hybrid DNS resolution.

---

## How Resolver Rules Work

Suppose an [[EC2]] instance queries:

database.corp.internal

You configure a Resolver Rule:

Domain:

corp.internal

Target DNS Servers:

10.50.0.10  
10.50.0.11

Architecture:

[[EC2]]  
↓  
database.corp.internal?  
↓  
[[20-SAA/06-Route 53/Route 53 Resolver]]  
↓  
Rule matches corp.internal  
↓  
[[Route 53 Resolver Outbound Endpoint]]  
↓  
10.50.0.10 / 10.50.0.11  
↓  
On-Prem DNS  
↓  
DNS Answer

---

## Resolver Rule Components

A forwarding rule essentially defines:

### Domain Name

Which DNS namespace should match?

Example:

corp.internal

### Target IP Addresses

Which DNS servers should receive matching queries?

Example:

10.50.0.10  
10.50.0.11

### VPC Association

Which VPCs should use the rule?

Together:

Domain  
+  
Target DNS Server  
+  
VPC Association  
↓  
Conditional DNS Forwarding

---

## Forward Rules

A **Forward Rule** sends matching DNS queries to external DNS resolvers.

Example:

Rule:

corp.internal  
↓  
Forward  
↓  
10.50.0.10

Architecture:

AWS Resource  
↓  
[[20-SAA/06-Route 53/Route 53 Resolver]]  
↓  
Forward Rule  
↓  
[[Route 53 Resolver Outbound Endpoint]]  
↓  
On-Premises DNS

This is the most important Resolver Rule type for SAA hybrid DNS scenarios.

---

## System Rules

Route 53 Resolver also has:

**System Rules**

System Rules tell Route 53 Resolver to resolve certain domains using its normal AWS DNS behavior rather than forwarding them elsewhere.

Think:

**Forward Rule = Send it somewhere else**

**System Rule = Route 53 handles it**

This becomes useful when broader forwarding rules exist but certain namespaces should continue using AWS DNS.

---

## Recursive Internet Resolution

Route 53 Resolver can also perform normal recursive DNS resolution for public domains.

Example:

[[EC2]]  
↓  
www.example.com?  
↓  
[[20-SAA/06-Route 53/Route 53 Resolver]]  
↓  
Public DNS Resolution  
↓  
DNS Answer

You do not need an outbound forwarding rule for every public Internet domain.

Resolver Rules are mainly useful when special handling is required.

---

## Most Specific Rule Wins

This is an important architecture rule.

Suppose you have:

Rule 1:

internal

↓  
DNS Server A

Rule 2:

corp.internal

↓  
DNS Server B

A query arrives for:

database.corp.internal

Both rules could theoretically match.

Route 53 uses the:

**Most specific matching domain**

Therefore:

database.corp.internal  
↓  
corp.internal rule  
↓  
DNS Server B

> [!tip] Memory Trick
> **DNS Rules = Most Specific Wins**

---

## Example of Rule Specificity

Suppose:

example.internal  
↓  
DNS Server A

engineering.example.internal  
↓  
DNS Server B

Query:

server.engineering.example.internal

Route 53 chooses:

engineering.example.internal

because it is the more specific match.

This allows you to create hierarchical DNS forwarding architectures.

---

## Resolver Rules and Outbound Endpoints

These two components work together but solve different problems.

### Resolver Rule

Answers:

> **Which DNS queries should be forwarded and where?**

Think:

**Decision**

---

### [[Route 53 Resolver Outbound Endpoint]]

Answers:

> **How does the DNS query leave AWS?**

Think:

**Path**

---

## Architecture

[[EC2]]  
↓  
DNS Query  
↓  
[[20-SAA/06-Route 53/Route 53 Resolver]]  
↓  
Resolver Rule  
↓  
Outbound Endpoint  
↓  
[[05-Networking/Site-to-Site VPN]] / [[05-Networking/Direct Connect]]  
↓  
On-Prem DNS

### Memory Trick

**Rule = Where**

**Outbound Endpoint = Way Out**

---

## VPC Association

A Resolver Rule must be associated with the VPCs that should use it.

Example:

Rule:

corp.internal  
↓  
Associated with VPC-A

Then resources in:

VPC-A

can use that forwarding behavior.

If another VPC also needs the rule:

Associate the rule with that VPC as well.

---

## Multi-VPC Architecture

Suppose:

VPC-A  
VPC-B  
VPC-C

all need to resolve:

corp.internal

You can use the same forwarding logic across the VPCs.

Architecture:

VPC-A  
VPC-B  
VPC-C  
↓  
Resolver Rule  
↓  
Outbound Resolver Endpoint  
↓  
On-Prem DNS

This simplifies DNS administration.

---

## Sharing Resolver Rules with AWS RAM

Resolver Rules can be shared across AWS accounts using:

[[AWS RAM]]

This is extremely useful in multi-account environments.

Example:

### Networking Account

Creates:

corp.internal Resolver Rule

Then:

[[AWS RAM]]  
↓  
Shares Rule  
↓  
Application Account A  
Application Account B  
Application Account C

The application accounts can associate the shared rule with their VPCs.

> [!tip] Architecture Pattern
> **Centralized Hybrid DNS → Resolver Rules + AWS RAM**

---

## AWS Organizations Architecture

In larger environments:

[[AWS Organizations]]  
↓  
Multiple AWS Accounts  
↓  
Central Networking Account  
↓  
Resolver Rules  
↓  
[[AWS RAM]]  
↓  
Application Accounts

This reduces:

- Duplicate DNS configuration
- Administrative overhead
- Inconsistent forwarding rules

---

## Resolver Rules and Hybrid Connectivity

Resolver Rules do not create connectivity.

If a rule forwards:

corp.internal  
↓  
10.50.0.10

AWS still needs network connectivity to:

10.50.0.10

using something such as:

- [[05-Networking/Site-to-Site VPN]]
- [[05-Networking/Direct Connect]]

### Architecture Rule

**Resolver Rule = DNS instruction**

**Outbound Endpoint = DNS exit**

**VPN / Direct Connect = Network path**

All three may be required.

---

## Architecture Thinking

### Scenario 1 — Corporate Domain

EC2 instances must resolve:

database.corp.internal

using on-premises DNS servers.

**Choose:**

[[Route 53 Resolver Outbound Endpoint]]

+

**Resolver Forward Rule for corp.internal**

---

### Scenario 2 — Only One Namespace Goes On-Premises

A company wants:

corp.internal  
↓  
On-Prem DNS

but:

amazonaws.com  
↓  
AWS DNS

and:

example.com  
↓  
Normal Internet DNS

**Choose → Resolver Rule**

Why?

It provides:

**Conditional Forwarding**

---

### Scenario 3 — Multiple Corporate Domains

A company has:

corp.internal  
↓  
DNS Server A

partner.internal  
↓  
DNS Server B

Create separate Resolver Rules:

corp.internal  
↓  
DNS Server A

partner.internal  
↓  
DNS Server B

Route 53 chooses the appropriate rule based on the queried domain.

---

### Scenario 4 — More Specific Domain

Rules:

internal  
↓  
DNS Server A

finance.internal  
↓  
DNS Server B

Query:

database.finance.internal

**Choose → finance.internal rule**

Why?

The:

**Most specific matching rule wins**

---

### Scenario 5 — Twenty AWS Accounts

Twenty AWS accounts need identical DNS forwarding to corporate DNS.

Instead of manually recreating rules:

Central Networking Account  
↓  
Create Resolver Rule  
↓  
[[AWS RAM]]  
↓  
Share Rule with Accounts

---

## Resolver Rule vs Private Hosted Zone

These solve different problems.

### [[Route 53 Private Hosted Zones]]

Stores:

**Private AWS DNS records**

Example:

database.aws.internal  
↓  
10.0.20.10

---

### Resolver Rule

Controls:

**Where DNS queries should be forwarded**

Example:

corp.internal  
↓  
On-Prem DNS

### Memory Trick

**Private Hosted Zone = Records**

**Resolver Rule = Forwarding Instructions**

---

## Resolver Rule vs Inbound Endpoint

### [[Route 53 Resolver Inbound Endpoint]]

Used when:

**On-Prem → AWS**

It allows external DNS queries to enter Route 53 Resolver.

### Resolver Rule

Most commonly appears with:

**AWS → On-Prem**

It determines which DNS queries should be forwarded through an Outbound Endpoint.

---

## Scenario Recognition

### Immediately Think Resolver Rule When You See

- Conditional forwarding
- Specific domain
- DNS namespace
- Forward corp.internal
- Target DNS server
- Domain matching
- Most specific rule
- VPC association
- Share DNS forwarding
- AWS RAM
- Centralized hybrid DNS

### Strongest Exam Pattern

> **"Forward queries for this domain to these DNS servers"**
>
> = **Resolver Rule**

---

## Exam Traps

### Trap 1 — Resolver Rule Is the Outbound Endpoint

False.

Rule:

**Decides what gets forwarded**

Outbound Endpoint:

**Provides the path out of AWS**

---

### Trap 2 — Resolver Rule Creates VPN Connectivity

False.

You still need network connectivity such as:

[[05-Networking/Site-to-Site VPN]]

or:

[[05-Networking/Direct Connect]]

---

### Trap 3 — All DNS Queries Are Forwarded

Not necessarily.

Resolver Rules provide:

**Conditional Forwarding**

Only matching namespaces are forwarded.

---

### Trap 4 — Broadest Rule Wins

False.

When multiple rules match:

**Most specific domain wins**

---

### Trap 5 — Rules Must Be Duplicated Across AWS Accounts

Not necessarily.

Use:

[[AWS RAM]]

to share Resolver Rules.

---

### Trap 6 — Resolver Rules Store DNS Records

False.

DNS records remain on the authoritative DNS system.

Resolver Rules only control:

**Where queries are sent**

---

## Quick Cheat Sheet

| Feature | Resolver Rules |
|---|---|
| Purpose | DNS forwarding logic |
| Conditional Forwarding | ✅ |
| Domain Matching | ✅ |
| Target DNS Servers | ✅ |
| VPC Association | ✅ |
| Forward Rule | Send to external DNS |
| System Rule | Use Route 53 Resolver |
| Most Specific Match Wins | ✅ |
| Works with Outbound Endpoint | ✅ |
| Share Across Accounts | [[AWS RAM]] |
| Creates Network Connectivity | ❌ |
| Stores DNS Records | ❌ |

---

## Master Memory Trick

> [!tip] Master Memory Trick
> **Resolver Rule = DNS IF Statement**
>
> Think:
>
> **IF domain = corp.internal**
>
> **THEN forward to corporate DNS**
>
> Example:
>
> corp.internal  
> ↓  
> Resolver Rule  
> ↓  
> Outbound Endpoint  
> ↓  
> On-Prem DNS

Remember:

**Rule = WHAT + WHERE**

**Outbound = WAY OUT**

**VPN / Direct Connect = NETWORK PATH**

And:

> **If multiple rules match → Most specific wins**

---

## Related Notes

- [[Route 53]]
- [[20-SAA/06-Route 53/Route 53 Resolver]]
- [[Route 53 Resolver Inbound Endpoint]]
- [[Route 53 Resolver Outbound Endpoint]]
- [[Route 53 Private Hosted Zones]]
- [[05-Networking/VPC]]
- [[05-Networking/Site-to-Site VPN]]
- [[05-Networking/Direct Connect]]
- [[AWS RAM]]
- [[AWS Organizations]]
- [[Hybrid Cloud]]
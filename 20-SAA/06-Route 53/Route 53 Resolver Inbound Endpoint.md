## What Problem Does It Solve?

[[Route 53 Resolver Inbound Endpoint]] allows DNS queries from **outside a VPC to enter AWS** and use [[20-SAA/06-Route 53/Route 53 Resolver]].

Its most important SAA use case is:

> **"How can my on-premises environment resolve private DNS names hosted in AWS?"**

Think:

On-Premises  
↓ DNS Query  
AWS  
↓  
[[Route 53 Resolver Inbound Endpoint]]  
↓  
AWS Private DNS

> [!tip] Memory Trick
> **Inbound = DNS comes INTO AWS**
>
> **On-Prem → AWS = INBOUND**

---

## The Hybrid DNS Problem

Suppose a company has:

### AWS

A [[Route 53 Private Hosted Zones|Private Hosted Zone]]:

aws.internal

with:

database.aws.internal  
↓  
10.0.10.50

### On-Premises

An application needs to connect to:

database.aws.internal

The problem:

Private Hosted Zones are designed for DNS resolution within associated VPCs.

The on-premises DNS environment needs a way to forward the query into AWS.

Solution:

**Route 53 Resolver Inbound Endpoint**

---

## Inbound Endpoint Architecture

Architecture:

On-Premises Application  
↓  
On-Premises DNS Resolver  
↓  
DNS Query for aws.internal  
↓  
[[05-Networking/Direct Connect]] / [[05-Networking/Site-to-Site VPN]]  
↓  
[[Route 53 Resolver Inbound Endpoint]]  
↓  
[[20-SAA/06-Route 53/Route 53 Resolver]]  
↓  
[[Route 53 Private Hosted Zones|Private Hosted Zone]]  
↓  
DNS Answer

Then the answer returns to the on-premises client.

---

## Follow the DNS Query

This is the easiest way to recognize the correct endpoint.

Ask:

> **Which direction is the DNS query moving relative to AWS?**

If:

On-Premises  
↓  
AWS

the query is entering AWS.

Therefore:

**Inbound Endpoint**

### Master Direction Rule

**On-Prem → AWS = INBOUND**

**AWS → On-Prem = [[Route 53 Resolver Outbound Endpoint|OUTBOUND]]**

---

## Inbound Endpoints Use VPC IP Addresses

A Resolver Inbound Endpoint is created inside your:

[[05-Networking/VPC]]

It receives IP addresses from subnets in that VPC.

Conceptually:

VPC  
├── Subnet A
│   └── Inbound Resolver IP
│
└── Subnet B
    └── Inbound Resolver IP

Your on-premises DNS servers forward queries to these IP addresses.

---

## High Availability

For high availability, Resolver Endpoints should use:

**Multiple Availability Zones**

Example:

VPC  
├── [[Availability Zones|AZ-A]]
│   └── Resolver IP 1
│
└── [[Availability Zones|AZ-B]]
    └── Resolver IP 2

On-premises DNS can forward queries to both endpoint IP addresses.

### Architecture Thinking

If one Availability Zone becomes unavailable:

On-Prem DNS  
↓  
Other Resolver Endpoint IP  
↓  
DNS resolution continues

> [!tip] Memory Trick
> **Production Resolver Endpoint = At least two AZs**

---

## Conditional Forwarding from On-Premises

Your on-premises DNS server should forward the appropriate AWS private namespace to the inbound endpoint.

Example:

AWS Private Domain:

aws.internal

Configure on-premises DNS:

Queries for:

aws.internal  
↓  
Forward to Route 53 Inbound Endpoint IPs

But queries for other domains can continue using the organization's normal DNS process.

This is:

**Conditional Forwarding**

---

## Example

Suppose:

Private Hosted Zone:

cloud.company.internal

contains:

app.cloud.company.internal  
↓  
10.0.20.25

The on-premises DNS server is configured:

cloud.company.internal  
↓  
Forward to:
10.0.1.10  
10.0.2.10

Those IP addresses belong to:

[[Route 53 Resolver Inbound Endpoint]]

Now:

On-Premises Client  
↓  
app.cloud.company.internal?  
↓  
Corporate DNS  
↓  
Matches cloud.company.internal forwarding rule  
↓  
Inbound Endpoint  
↓  
Route 53 Private Hosted Zone  
↓  
10.0.20.25

---

## Network Connectivity Is Required

The inbound endpoint does **not** create connectivity between:

On-Premises ↔ AWS

You still need network connectivity such as:

- [[05-Networking/Site-to-Site VPN]]
- [[05-Networking/Direct Connect]]

Think of these as solving two different problems.

### Resolver Inbound Endpoint

Solves:

**DNS resolution**

### VPN / Direct Connect

Solves:

**Network connectivity**

> [!warning] Exam Trap
> **DNS resolution ≠ network connectivity**

You may successfully resolve:

database.aws.internal  
↓  
10.0.10.50

But without routing/connectivity to:

10.0.10.50

the application still cannot reach the database.

---

## Security Groups

Resolver Endpoints use:

[[Security Groups]]

The Security Group must allow DNS queries from the appropriate network.

DNS uses:

- UDP port 53
- TCP port 53

Architecture:

On-Prem DNS  
↓ Port 53  
Security Group  
↓  
Inbound Resolver Endpoint

If the Security Group blocks DNS:

On-Prem DNS  
↓  
X  
Inbound Endpoint

Resolution fails.

---

## Private Hosted Zone Integration

A major reason to use an inbound endpoint is access to:

[[Route 53 Private Hosted Zones]]

Example:

Private Hosted Zone:

aws.internal

Record:

db.aws.internal  
↓  
10.0.50.10

AWS resources in the associated VPC can resolve this normally.

For on-premises clients:

On-Prem DNS  
↓  
Inbound Endpoint  
↓  
Route 53 Resolver  
↓  
Private Hosted Zone

This extends AWS private DNS resolution into the hybrid environment.

---

## Inbound Endpoint Does Not Forward Queries to On-Premises

This is a crucial distinction.

Inbound is for:

**Queries entering AWS**

It is not used when:

[[EC2]]  
↓  
needs to resolve  
↓  
corp.internal  
↓  
On-Prem DNS

That requires:

[[Route 53 Resolver Outbound Endpoint]]

plus:

[[Route 53 Resolver Rules]]

---

## Architecture Thinking

### Scenario 1 — On-Premises Resolves AWS Private Zone

A company has:

Private Hosted Zone:

aws.internal

On-premises servers must resolve records inside it.

**Choose → Route 53 Resolver Inbound Endpoint**

Architecture:

On-Prem DNS  
↓  
[[05-Networking/Site-to-Site VPN]] / [[05-Networking/Direct Connect]]  
↓  
Inbound Endpoint  
↓  
Private Hosted Zone

---

### Scenario 2 — Corporate DNS Needs EC2 Private Names

An organization wants its on-premises DNS infrastructure to resolve private AWS DNS names.

The DNS queries originate on-premises and must enter the VPC.

**Choose → Inbound Endpoint**

---

### Scenario 3 — EC2 Resolves On-Premises Domain

An EC2 instance needs to resolve:

database.corp.internal

The authoritative DNS server is on-premises.

**Do NOT choose → Inbound Endpoint**

Choose:

[[Route 53 Resolver Outbound Endpoint]]

+

[[Route 53 Resolver Rules]]

---

### Scenario 4 — DNS Resolves but Application Cannot Connect

An on-premises application successfully resolves:

db.aws.internal

to:

10.0.50.10

but cannot establish a connection.

The Resolver configuration may already be correct.

Check:

- [[05-Networking/Site-to-Site VPN]]
- [[05-Networking/Direct Connect]]
- Route tables
- [[Security Groups]]
- Network ACLs

Why?

Resolver solved the:

**DNS problem**

but not necessarily the:

**network connectivity problem**

---

## Inbound vs Outbound

| Requirement | Endpoint |
|---|---|
| On-Prem → AWS DNS | Inbound |
| AWS → On-Prem DNS | Outbound |
| Resolve AWS Private Hosted Zone from On-Prem | Inbound |
| EC2 resolves corporate DNS | Outbound |
| Query enters AWS | Inbound |
| Query leaves AWS | Outbound |

---

## Scenario Recognition

### Immediately Think Inbound Endpoint When You See

- On-premises → AWS
- Resolve AWS private DNS from on-premises
- Private Hosted Zone from corporate network
- DNS queries entering AWS
- Corporate DNS forwards to AWS
- Hybrid DNS into Route 53
- Conditional forwarding toward AWS

### Strongest Exam Pattern

> **On-Prem needs AWS DNS = INBOUND**

---

## Exam Traps

### Trap 1 — Inbound Means AWS Queries On-Premises

False.

That reverses the direction.

Inbound means:

**DNS query enters AWS**

---

### Trap 2 — Inbound Endpoint Replaces VPN or Direct Connect

False.

You still need network connectivity between AWS and on-premises.

---

### Trap 3 — One Endpoint IP Is Ideal for Production

For resilient architectures, use endpoint IPs across multiple:

[[Availability Zones]]

---

### Trap 4 — DNS Port Is 443

No.

DNS normally uses:

**Port 53**

over:

- UDP
- TCP

---

### Trap 5 — Inbound Endpoint Is the Private Hosted Zone

False.

The Private Hosted Zone:

**Stores DNS records**

The Inbound Endpoint:

**Provides a path for external DNS queries to reach Route 53 Resolver**

---

### Trap 6 — Inbound Is Used for AWS → On-Premises Queries

False.

That requires:

**Outbound Endpoint + Resolver Rule**

---

## Quick Cheat Sheet

| Feature | Inbound Endpoint |
|---|---|
| Primary Direction | On-Prem → AWS |
| DNS Query Enters AWS | ✅ |
| Resolve AWS Private DNS from On-Prem | ✅ |
| Private Hosted Zone Integration | ✅ |
| Lives in VPC | ✅ |
| Uses VPC IP Addresses | ✅ |
| Multiple AZs for HA | ✅ |
| Security Group | ✅ |
| DNS Port | 53 |
| VPN / Direct Connect Still Needed | ✅ |
| AWS → On-Prem DNS | ❌ |
| Resolver Rule Required for Main Inbound Pattern | ❌ |

---

## Master Memory Trick

> [!tip] Master Memory Trick
> **Stand inside AWS and watch the DNS query.**
>
> On-Premises  
> ↓  
> ↓  
> **INTO AWS**
>
> = **INBOUND**
>
> So:
>
> **On-Prem → AWS Private DNS = Inbound Endpoint**

Then remember:

**Inbound = Enter AWS**

**Outbound = Exit AWS**

**Private Hosted Zone = Stores private records**

**Resolver = Resolves the names**

**VPN / Direct Connect = Provides the network path**

---

## Related Notes

- [[Route 53]]
- [[20-SAA/06-Route 53/Route 53 Resolver]]
- [[Route 53 Resolver Outbound Endpoint]]
- [[Route 53 Resolver Rules]]
- [[Route 53 Private Hosted Zones]]
- [[Route 53 Hosted Zones]]
- [[05-Networking/VPC]]
- [[Availability Zones]]
- [[Security Groups]]
- [[05-Networking/Site-to-Site VPN]]
- [[05-Networking/Direct Connect]]
- [[Hybrid Cloud]]
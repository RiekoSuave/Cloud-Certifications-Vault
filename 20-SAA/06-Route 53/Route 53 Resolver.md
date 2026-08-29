## What Problem Does It Solve?

[[20-SAA/06-Route 53/Route 53 Resolver]] provides DNS resolution for resources inside a [[05-Networking/VPC]] and helps connect DNS resolution between:

- AWS
- On-premises networks
- Hybrid environments

It solves questions such as:

> **"How can my on-premises servers resolve private AWS DNS names?"**

and:

> **"How can resources inside my VPC resolve DNS names hosted on-premises?"**

Think:

**Route 53 Resolver = DNS bridge between AWS and on-premises**

> [!tip] Memory Trick
> **Resolver = Resolve names across environments**
>
> AWS ↔ On-Premises

---

## Route 53 Resolver Inside a VPC

Route 53 Resolver is available by default inside every [[05-Networking/VPC]].

It provides DNS resolution for resources such as:

- [[EC2]]
- AWS service DNS names
- [[Route 53 Hosted Zones|Private Hosted Zones]]
- Internet DNS names

Conceptually:

[[EC2]]  
↓ DNS Query  
[[20-SAA/06-Route 53/Route 53 Resolver]]  
↓  
DNS Answer

This happens automatically when VPC DNS functionality is enabled.

---

## VPC DNS Resolver Address

Route 53 Resolver is available at:

**VPC CIDR base + 2**

Example:

VPC CIDR:

10.0.0.0/16

Route 53 Resolver:

10.0.0.2

Another special address is:

169.254.169.253

### Memory Trick

> **VPC DNS = +2**

Example:

10.0.0.0/16  
↓  
10.0.0.2

---

## The Hybrid DNS Problem

Suppose a company has:

### AWS

Private Hosted Zone:

aws.example.internal

### On-Premises

Private DNS Zone:

corp.example.internal

Now both environments need to resolve each other's DNS names.

Requirements:

On-Premises  
↓  
Resolve AWS private names

AWS  
↓  
Resolve on-premises private names

Normal public DNS cannot solve this because these are private DNS namespaces.

This is where Route 53 Resolver endpoints become important.

---

## Route 53 Resolver Endpoints

There are two major endpoint types:

- **Inbound Endpoint**
- **Outbound Endpoint**

The direction refers to the direction of the:

**DNS query relative to AWS**

> [!tip] Master Direction Trick
> **Inbound = DNS comes INTO AWS**
>
> **Outbound = DNS leaves AWS**

---

## Route 53 Resolver Inbound Endpoint

An **Inbound Resolver Endpoint** allows DNS queries from outside the VPC to enter AWS.

Typical use:

**On-Premises → AWS**

Example:

On-Premises DNS Server  
↓  
[[05-Networking/Direct Connect]] / [[05-Networking/Site-to-Site VPN]]  
↓  
Route 53 Resolver Inbound Endpoint  
↓  
[[Route 53 Hosted Zones|Private Hosted Zone]]

This allows on-premises systems to resolve private AWS DNS names.

---

## Inbound Endpoint Architecture

Suppose AWS has:

Private Hosted Zone:

aws.internal

and an on-premises server needs to resolve:

database.aws.internal

Architecture:

On-Premises Server  
↓  
On-Premises DNS Resolver  
↓  
DNS Query  
↓  
[[05-Networking/Direct Connect]] / [[05-Networking/Site-to-Site VPN]]  
↓  
Route 53 Resolver **Inbound Endpoint**  
↓  
[[Route 53 Hosted Zones|Private Hosted Zone]]  
↓  
DNS Answer

The answer then travels back to the on-premises client.

### Memory Trick

**On-Prem → AWS = INBOUND**

The DNS query is entering AWS.

---

## Inbound Endpoint IP Addresses

Inbound endpoints use IP addresses inside your VPC.

Typically, you deploy endpoint IP addresses across:

**At least two Availability Zones**

for high availability.

Conceptually:

On-Premises DNS  
↓  
├── Resolver Endpoint IP → AZ-A
└── Resolver Endpoint IP → AZ-B

This prevents one Availability Zone failure from eliminating hybrid DNS resolution.

---

## Route 53 Resolver Outbound Endpoint

An **Outbound Resolver Endpoint** allows DNS queries originating inside AWS to be forwarded to DNS resolvers outside AWS.

Typical use:

**AWS → On-Premises**

Example:

[[EC2]]  
↓  
Route 53 Resolver  
↓  
Resolver Rule  
↓  
Outbound Endpoint  
↓  
[[05-Networking/Direct Connect]] / [[05-Networking/Site-to-Site VPN]]  
↓  
On-Premises DNS Server

This allows AWS resources to resolve private on-premises DNS names.

---

## Outbound Endpoint Architecture

Suppose on-premises DNS hosts:

corp.internal

An EC2 instance needs to resolve:

database.corp.internal

Architecture:

[[EC2]]  
↓  
DNS Query  
↓  
[[20-SAA/06-Route 53/Route 53 Resolver]]  
↓  
Forwarding Rule for corp.internal  
↓  
Resolver **Outbound Endpoint**  
↓  
[[05-Networking/Direct Connect]] / [[05-Networking/Site-to-Site VPN]]  
↓  
On-Premises DNS Server  
↓  
DNS Answer

### Memory Trick

**AWS → On-Prem = OUTBOUND**

The DNS query is leaving AWS.

---

## Resolver Rules

Outbound endpoints work with:

**Route 53 Resolver Rules**

A forwarding rule tells Route 53:

> **"For this domain, forward DNS queries to these DNS servers."**

Example:

Domain:

corp.internal

Forward To:

10.20.0.10  
10.20.0.11

Architecture:

Query for:

database.corp.internal  
↓  
Rule matches corp.internal  
↓  
Outbound Endpoint  
↓  
10.20.0.10 / 10.20.0.11

---

## Conditional Forwarding

Resolver Rules provide:

**Conditional DNS Forwarding**

This means only queries matching a particular domain are forwarded.

Example:

corp.internal  
↓  
Forward to On-Prem DNS

But:

amazonaws.com  
↓  
Resolve normally through Route 53 Resolver

And:

example.com  
↓  
Resolve through normal public DNS resolution

### Architecture Thinking

Resolver Rules let you say:

> **"Only send THIS namespace to THAT DNS server."**

---

## Inbound vs Outbound

This is the core exam distinction.

### Inbound

DNS query:

**On-Premises → AWS**

Purpose:

Resolve AWS-hosted DNS names from outside AWS.

Architecture:

On-Prem  
↓  
Inbound Endpoint  
↓  
Route 53

---

### Outbound

DNS query:

**AWS → On-Premises**

Purpose:

Resolve on-premises DNS names from AWS.

Architecture:

AWS  
↓  
Outbound Endpoint  
↓  
On-Prem DNS

---

## Inbound + Outbound Together

A full hybrid DNS architecture commonly uses both.

### On-Premises Resolves AWS

On-Prem DNS  
↓  
Inbound Endpoint  
↓  
AWS Private DNS

### AWS Resolves On-Premises

AWS  
↓  
Outbound Endpoint  
↓  
On-Prem DNS

Together:

On-Premises  
↔  
Route 53 Resolver  
↔  
AWS

> [!tip] Architecture Pattern
> **Two-way Hybrid DNS = Inbound + Outbound**

---

## Network Connectivity Is Still Required

Resolver Endpoints do not create network connectivity.

You still need connectivity between AWS and on-premises through something such as:

- [[05-Networking/Site-to-Site VPN]]
- [[05-Networking/Direct Connect]]

Think:

DNS Resolution  
≠  
Network Connectivity

Route 53 Resolver can tell you:

> "That server is at this IP."

But your network still needs a route to actually reach that IP.

> [!warning] Exam Trap
> **Resolver solves DNS. VPN/DX solves connectivity.**

---

## Security Groups

Resolver Endpoints are associated with:

[[Security Groups]]

The Security Group must allow the required DNS traffic.

DNS commonly uses:

**UDP port 53**

and can also use:

**TCP port 53**

If DNS traffic is blocked:

Client  
↓  
Resolver Endpoint  
X Security Group  
↓  
DNS resolution fails

---

## Highly Available Resolver Endpoints

For production hybrid DNS architectures, Resolver Endpoint IP addresses should span multiple:

[[Availability Zones]]

Example:

VPC  
├── AZ-A → Resolver Endpoint IP
└── AZ-B → Resolver Endpoint IP

This improves availability if an AZ becomes unavailable.

---

## Resolver Rules Can Be Shared

Resolver Rules can be shared across AWS accounts using:

[[AWS RAM]]

This is useful in:

- Multi-account environments
- [[AWS Organizations]]
- Centralized networking architectures

Example:

Networking Account  
↓  
Resolver Rule  
↓  
[[AWS RAM]]  
↓  
Application Accounts

This prevents every account from independently rebuilding the same forwarding rules.

---

## Architecture Thinking

### Scenario 1 — On-Premises Needs AWS Private DNS

A company has an AWS Private Hosted Zone:

aws.internal

On-premises servers must resolve names inside that zone.

**Choose → Route 53 Resolver Inbound Endpoint**

Architecture:

On-Prem DNS  
↓  
[[05-Networking/Direct Connect]] / [[05-Networking/Site-to-Site VPN]]  
↓  
Inbound Endpoint  
↓  
Private Hosted Zone

---

### Scenario 2 — EC2 Needs On-Premises DNS

An EC2 application needs to resolve:

database.corp.internal

The domain exists only on the company's on-premises DNS servers.

**Choose → Outbound Endpoint + Resolver Rule**

Architecture:

[[EC2]]  
↓  
Resolver Rule  
↓  
Outbound Endpoint  
↓  
On-Prem DNS

---

### Scenario 3 — Two-Way Hybrid DNS

AWS applications need to resolve on-premises names.

On-premises applications also need to resolve AWS private names.

**Choose → Both Inbound and Outbound Resolver Endpoints**

---

### Scenario 4 — Multiple AWS Accounts Need Same Rule

A company has many AWS accounts that need to resolve:

corp.internal

through centralized on-premises DNS servers.

Create the Resolver Rule centrally and share it using:

[[AWS RAM]]

---

## Resolver vs Private Hosted Zone

These concepts are related but different.

### [[Route 53 Hosted Zones|Private Hosted Zone]]

Stores:

**Private DNS records**

Example:

database.aws.internal  
↓  
10.0.5.10

---

### Route 53 Resolver

Performs:

**DNS resolution and forwarding**

It helps clients reach the appropriate DNS system.

### Memory Trick

**Private Hosted Zone = Records**

**Resolver = Queries**

---

## Resolver vs Route 53 Health Checks

### Resolver

Purpose:

**DNS resolution**

Question:

> What IP belongs to this hostname?

### [[Route 53 Health Checks]]

Purpose:

**Endpoint health**

Question:

> Should Route 53 keep returning this resource?

These solve completely different problems.

---

## Scenario Recognition

### Immediately Think Inbound Endpoint When You See

- On-premises → AWS DNS
- Resolve Private Hosted Zone from on-premises
- External network querying AWS private DNS
- DNS queries entering AWS

### Immediately Think Outbound Endpoint When You See

- AWS → On-premises DNS
- EC2 resolving corporate DNS
- Forward DNS queries to on-premises
- Resolver Rule
- Conditional forwarding

### Strongest Memory Pattern

> **On-Prem → AWS = INBOUND**
>
> **AWS → On-Prem = OUTBOUND**

---

## Exam Traps

### Trap 1 — Reverse the Endpoint Direction

This is the biggest trap.

Always follow the DNS query.

If the query:

On-Prem → AWS

Choose:

**Inbound**

If the query:

AWS → On-Prem

Choose:

**Outbound**

---

### Trap 2 — Outbound Endpoint Alone Is Enough

Outbound DNS forwarding also requires:

**Resolver Rules**

The rule determines which DNS namespace should be forwarded.

---

### Trap 3 — Resolver Endpoint Creates Network Connectivity

False.

You still need:

[[05-Networking/Direct Connect]]

or:

[[05-Networking/Site-to-Site VPN]]

for hybrid network connectivity.

---

### Trap 4 — Private Hosted Zone and Resolver Are the Same

False.

Private Hosted Zone:

**Stores private DNS records**

Resolver:

**Processes and forwards DNS queries**

---

### Trap 5 — All DNS Queries Must Go On-Premises

False.

Resolver Rules provide conditional forwarding.

Only matching domains need to be forwarded.

Example:

corp.internal → On-Prem

Other domains → Normal Route 53 resolution

---

### Trap 6 — Resolver Endpoints Do Not Need Security Groups

False.

Resolver Endpoints use Security Groups.

DNS traffic must be permitted.

---

## Quick Cheat Sheet

| Requirement | Solution |
|---|---|
| DNS inside VPC | Route 53 Resolver |
| VPC DNS Address | VPC CIDR + 2 |
| Alternate Resolver Address | 169.254.169.253 |
| On-Prem → AWS DNS | Inbound Endpoint |
| AWS → On-Prem DNS | Outbound Endpoint |
| Forward Specific Domain | Resolver Rule |
| Hybrid Connectivity | VPN / Direct Connect |
| DNS Port | 53 |
| High Availability | Multiple AZs |
| Share Resolver Rules | AWS RAM |
| Store AWS Private DNS Records | Private Hosted Zone |

---

## Master Memory Trick

> [!tip] Master Memory Trick
> **Follow the DNS query arrow.**
>
> **On-Prem → AWS**
>
> Query comes **IN**
>
> → **Inbound Endpoint**
>
> **AWS → On-Prem**
>
> Query goes **OUT**
>
> → **Outbound Endpoint + Resolver Rule**

Then remember:

**Resolver = DNS**

**VPN / Direct Connect = Network**

And:

> **Two-way hybrid DNS = Inbound + Outbound**

---

## Related Notes

- [[Route 53]]
- [[Route 53 Hosted Zones]]
- [[Route 53 Private Hosted Zones]]
- [[Route 53 Resolver Inbound Endpoint]]
- [[Route 53 Resolver Outbound Endpoint]]
- [[Route 53 Resolver Rules]]
- [[05-Networking/Site-to-Site VPN]]
- [[05-Networking/Direct Connect]]
- [[05-Networking/VPC]]
- [[Security Groups]]
- [[AWS RAM]]
- [[AWS Organizations]]
- [[Hybrid Cloud]]
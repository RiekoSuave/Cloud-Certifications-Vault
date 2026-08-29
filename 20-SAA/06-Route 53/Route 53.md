## What Problem Does It Solve?

[[Route 53]] is a **highly available, scalable, fully managed authoritative DNS service**.

It solves the problem of:

> **"How do users find and connect to my application using a human-friendly domain name instead of an IP address?"**

Instead of users remembering:

54.22.33.44

They can use:

www.example.com

[[Route 53]] can translate the domain name into the address needed to reach the application.

Think:

**Domain Name → DNS → IP Address → Application**

> [!tip] Memory Trick
> **Route 53 = Internet Traffic Director**
>
> Users know the **name**.
>
> Route 53 tells them **where to go**.

---

## What Is DNS?

DNS stands for:

**Domain Name System**

DNS translates **human-friendly hostnames into machine-readable IP addresses**.

Example:

www.example.com  
↓  
DNS  
↓  
54.22.33.44  
↓  
Web Server

Without DNS, users would have to remember IP addresses instead of domain names.

DNS uses a **hierarchical naming structure**.

Example:

example.com  
├── www.example.com  
└── api.example.com

---

## Important DNS Terminology

Before getting deep into [[Route 53]], understand these terms.

### Domain Registrar

A **Domain Registrar** is where a domain name is registered.

Examples include:

- [[Route 53]]
- Third-party registrars

Important:

> **Domain Registrar ≠ DNS Service**

The same company may provide both, but they are technically different functions.

---

### DNS Record

A DNS record defines how DNS should respond to a request.

Important record types include:

- A
- AAAA
- CNAME
- NS

These become extremely important throughout [[Route 53]].

---

### Zone File

A **Zone File** contains DNS records for a domain.

Think:

Domain  
↓  
Zone File  
↓  
DNS Records

---

### Name Server

A **Name Server** resolves DNS queries.

Name servers can be:

- Authoritative
- Non-authoritative

[[Route 53]] is an **authoritative DNS service**.

---

### Top-Level Domain — TLD

The final portion of the domain.

Examples:

.com  
.org  
.gov  
.net  
.us

Example:

example.**com**

`.com` is the TLD.

---

### Second-Level Domain — SLD

The registered domain directly below the TLD.

Example:

example.com

`example` is the second-level domain.

---

### Subdomain

A domain underneath the main domain.

Examples:

www.example.com

api.example.com

shop.example.com

Here:

`www`, `api`, and `shop` are subdomains.

---

### Fully Qualified Domain Name — FQDN

An FQDN identifies the **complete domain name of a resource**.

Example:

api.example.com

Think:

**FQDN = Full DNS name**

---

## How DNS Resolution Works

Suppose a user enters:

example.com

The DNS resolution process conceptually looks like:

Browser  
↓  
Local DNS Resolver  
↓  
Root DNS Server  
↓  
TLD DNS Server  
↓  
Authoritative DNS Server  
↓  
IP Address Returned  
↓  
Web Server

### Step 1 — Browser Asks Local DNS Resolver

The user's device asks its configured DNS resolver:

> "What is the IP address for example.com?"

The local resolver may be operated by:

- An ISP
- A company
- Another DNS provider

---

### Step 2 — Root DNS Server

If the resolver doesn't already know the answer, it can begin walking the DNS hierarchy.

The Root DNS Server essentially points toward the appropriate TLD.

Example:

example.com

Root identifies:

`.com`

---

### Step 3 — TLD DNS Server

The `.com` TLD DNS server identifies the name servers responsible for:

example.com

---

### Step 4 — Authoritative Name Server

The authoritative name server contains the actual DNS records for the domain.

It can answer:

example.com  
↓  
9.10.11.12

---

### Step 5 — Client Connects

The IP address is returned to the client.

Browser  
↓  
9.10.11.12  
↓  
Web Server

> [!tip] Architecture Thinking
> DNS resolution follows a hierarchy:
>
> **Root → TLD → Authoritative DNS → Resource**

---

## What Is Route 53?

[[Route 53]] provides several important DNS capabilities.

It is:

- Highly available
- Scalable
- Fully managed
- Authoritative DNS
- A Domain Registrar
- Capable of performing resource health checks

### What Does Authoritative Mean?

**Authoritative** means that you control and can update the DNS records for your domain.

Example:

example.com  
↓  
[[Route 53]]  
↓  
54.22.33.44

If you control the Route 53 hosted zone, you control where the domain points.

### Why Is It Called Route 53?

Traditional DNS uses:

**Port 53**

So:

**Route 53 → Routing DNS traffic using port 53**

---

## Route 53 Records

A Route 53 record defines:

> **How should traffic for this domain or subdomain be routed?**

Each record contains important information.

### Name

The domain or subdomain.

Example:

example.com

www.example.com

---

### Record Type

Examples:

- A
- AAAA
- CNAME
- NS

---

### Value

The destination associated with the record.

Example:

12.34.56.78

---

### Routing Policy

Defines **how Route 53 responds to DNS queries**.

We'll cover the major routing policies separately because they are extremely important for the SAA exam.

---

### TTL

TTL stands for:

**Time To Live**

TTL controls how long a DNS resolver caches a DNS record.

Think:

Route 53  
↓  
DNS Response  
↓  
Resolver caches response  
↓  
TTL expires  
↓  
Resolver asks Route 53 again

> [!tip] Memory Trick
> **TTL = How long DNS remembers the answer**

---

## Important DNS Record Types

For SAA, the most important record types to recognize are:

- A
- AAAA
- CNAME
- NS

---

## A Record

An **A record** maps a hostname to an:

**IPv4 address**

Example:

example.com  
↓  
A Record  
↓  
192.0.2.10

### Scenario Recognition

If you see:

> Map hostname → IPv4

Think:

**A Record**

---

## AAAA Record

An **AAAA record** maps a hostname to an:

**IPv6 address**

Example:

example.com  
↓  
AAAA Record  
↓  
2001:db8::1

### Memory Trick

**A = IPv4**

**AAAA = IPv6**

---

## CNAME Record

A **CNAME record** maps:

**Hostname → Another hostname**

Example:

www.example.com  
↓  
CNAME  
↓  
myapp.example.net

The target hostname ultimately resolves through an A or AAAA record.

### Important CNAME Limitation

A CNAME **cannot be created for the zone apex**.

Example:

❌ example.com → CNAME

But:

✅ www.example.com → CNAME

### What Is the Zone Apex?

The zone apex is the **root/top-level name of your hosted zone**.

For:

example.com

The zone apex is:

example.com

This limitation becomes extremely important when comparing:

**CNAME vs Route 53 Alias Records**

> [!warning] Exam Trap
> **CNAME cannot be used at the zone apex.**
>
> `www.example.com` → CNAME is allowed.
>
> `example.com` → CNAME is not allowed.

---

## NS Record

NS stands for:

**Name Server**

An NS record identifies the **name servers responsible for the hosted zone**.

Think:

Domain  
↓  
NS Record  
↓  
Which DNS servers are authoritative?

NS records therefore help control how traffic for the domain reaches the correct DNS infrastructure.

---

## Route 53 Hosted Zones

A **Hosted Zone** is a container for DNS records that define how traffic should be routed for a domain and its subdomains.

Think:

[[Route 53]]  
↓  
Hosted Zone  
↓  
├── A Record  
├── AAAA Record  
├── CNAME Record  
├── NS Record  
└── Other Records

There are two major types:

1. **Public Hosted Zone**
2. **Private Hosted Zone**

---

## Public Hosted Zone

A **Public Hosted Zone** contains records that specify how traffic should be routed on the **public Internet**.

Example:

application1.example.com

Architecture:

Internet User  
↓  
[[Route 53]] Public Hosted Zone  
↓  
DNS Record  
↓  
Public Application

### Scenario Recognition

If the DNS name must be resolvable from the public Internet:

**Choose → Public Hosted Zone**

---

## Private Hosted Zone

A **Private Hosted Zone** contains records that specify how traffic should be routed **inside one or more [[05-Networking/VPC]]s**.

Example:

application1.company.internal

Architecture:

[[EC2]] Instance  
↓  
Private DNS Query  
↓  
[[Route 53]] Private Hosted Zone  
↓  
Internal Resource

The domain does **not need to be publicly resolvable on the Internet**.

### Scenario Recognition

If a company wants:

- Internal DNS
- Private application names
- DNS resolution inside VPCs
- Internal service discovery using DNS

Think:

**Private Hosted Zone**

---

## Public vs Private Hosted Zones

| Requirement | Hosted Zone |
|---|---|
| Public website | Public |
| Internet-accessible application | Public |
| Public DNS records | Public |
| Internal application | Private |
| Private VPC DNS | Private |
| Internal corporate hostname | Private |

### Memory Trick

**Public Hosted Zone = Internet DNS**

**Private Hosted Zone = VPC DNS**

---

## Architecture Thinking

### Scenario 1 — Public Website

A company hosts a public application and wants:

www.example.com

to resolve to the application's public endpoint.

**Choose → [[Route 53]] Public Hosted Zone**

---

### Scenario 2 — Internal Application

A company has an internal application running inside a [[05-Networking/VPC]].

Employees and applications should access it using:

app.company.internal

The hostname should not be publicly resolvable.

**Choose → [[Route 53]] Private Hosted Zone**

---

### Scenario 3 — IPv4 Address

A company needs:

app.example.com

to resolve directly to:

192.0.2.50

**Choose → A Record**

---

### Scenario 4 — IPv6 Address

A hostname must resolve directly to an IPv6 address.

**Choose → AAAA Record**

---

### Scenario 5 — Hostname to Hostname

A company wants:

www.example.com

to resolve to:

application.example.net

**Choose → CNAME**

Assuming `www.example.com` is **not the zone apex**.

---

## Scenario Recognition

### Exam Keywords

Immediately think **[[Route 53]]** when you see:

- DNS
- Domain name
- Domain registrar
- Authoritative DNS
- DNS records
- Hosted zone
- Public DNS
- Private DNS
- DNS routing
- DNS health checks
- Domain → IP address

### Record Recognition

**IPv4 → A**

**IPv6 → AAAA**

**Hostname → Hostname → CNAME**

**Name Servers → NS**

---

## Exam Traps

### Trap 1 — Domain Registrar vs DNS Service

These are not the same thing.

A:

**Domain Registrar**

registers ownership of the domain.

A:

**DNS Service**

answers DNS queries for the domain.

[[Route 53]] can perform **both roles**.

---

### Trap 2 — CNAME at the Zone Apex

You cannot create:

example.com → CNAME

But you can create:

www.example.com → CNAME

This limitation is one major reason Route 53 **Alias Records** are important.

---

### Trap 3 — Public vs Private Hosted Zone

If the domain should only resolve inside VPCs:

**Private Hosted Zone**

If Internet users need to resolve it:

**Public Hosted Zone**

---

### Trap 4 — DNS Does Not Carry the Application Traffic

Route 53 answers the DNS question:

> **"Where should I connect?"**

After DNS resolution, the client connects to the actual resource.

Conceptually:

Client  
↓ DNS query  
[[Route 53]]  
↓ IP/endpoint returned  
Client  
↓ actual application traffic  
Application

Route 53 is **not acting like a proxy for the application traffic**.

---

### Trap 5 — Confusing TTL with Routing

TTL does not determine **where traffic goes**.

TTL determines:

**How long the DNS answer remains cached.**

Routing policies determine how Route 53 chooses the DNS response.

---

## Quick Cheat Sheet

| Concept | Meaning |
|---|---|
| Route 53 | Managed authoritative DNS |
| DNS | Hostname → IP resolution |
| Domain Registrar | Registers domain names |
| Hosted Zone | Container for DNS records |
| Public Hosted Zone | Internet DNS |
| Private Hosted Zone | Internal VPC DNS |
| A Record | Hostname → IPv4 |
| AAAA Record | Hostname → IPv6 |
| CNAME | Hostname → Hostname |
| NS | Hosted Zone Name Servers |
| TTL | DNS cache duration |
| Authoritative DNS | You control the DNS records |

---

## Master Memory Trick

> [!tip] Master Memory Trick
> **Route 53 = AWS Internet Address Book + Traffic Director**
>
> Someone asks:
>
> **"Where is example.com?"**
>
> Route 53 answers:
>
> **"Go here."**

Remember:

**DNS = Name → Destination**

**A = IPv4**

**AAAA = IPv6**

**CNAME = Name → Name**

**NS = Name Servers**

**TTL = How long the answer is remembered**

**Public Hosted Zone = Internet**

**Private Hosted Zone = VPC**

---

## Related Notes

- [[Route 53 Records]]
- [[Route 53 Hosted Zones]]
- [[Route 53 TTL]]
- [[Route 53 CNAME vs Alias]]
- [[Route 53 Routing Policies]]
- [[Route 53 Health Checks]]
- [[20-SAA/06-Route 53/Route 53 Resolver]]
- [[05-Networking/VPC]]
- [[EC2]]
- [[Elastic Load Balancing]]
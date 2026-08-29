## What Problem Does It Solve?

[[3rd Party Registrar with Route 53]] lets you use [[Route 53]] as your DNS service **even when your domain was purchased from another domain registrar**.

It solves the problem of:

> **"My domain is registered somewhere else, but I want Route 53 to manage its DNS records."**

Example:

Domain Registrar  
↓  
GoDaddy

DNS Service  
↓  
[[Route 53]]

These do **not** have to be the same company.

> [!tip] Memory Trick
> **Registrar = Who sold you the name**
>
> **DNS Service = Who answers questions about the name**

---

## Domain Registrar vs DNS Service

These are two different functions.

### Domain Registrar

The registrar is where the domain name is:

**Registered / purchased**

Examples:

- GoDaddy
- Namecheap
- Other third-party registrars
- [[Route 53]]

The registrar maintains information about who is responsible for the domain.

---

### DNS Service

The DNS service hosts the DNS records that tell clients where the domain should point.

Examples:

example.com  
↓  
A Record  
↓  
192.0.2.10

or:

example.com  
↓  
Alias  
↓  
[[Application Load Balancer]]

[[Route 53]] can provide this DNS service even if it did not register the domain.

---

## Key Architecture Concept

Domain registration and DNS hosting are:

**Separate functions**

You can have:

Domain Registration  
↓  
Third-Party Registrar

while:

DNS Management  
↓  
[[Route 53]]

You do **not** have to transfer the domain registration to Route 53 just to use Route 53 DNS.

> [!tip] Architecture Rule
> **Using Route 53 DNS does NOT require transferring the domain to Route 53.**

---

## How to Use Route 53 with a Third-Party Registrar

The basic process is:

1. Create a [[Route 53 Hosted Zones|Public Hosted Zone]] for the domain
2. Route 53 generates authoritative Name Server records
3. Copy those Route 53 Name Servers
4. Update the Name Server records at the third-party registrar
5. The registrar delegates DNS resolution to Route 53

Architecture:

Domain Registered at Third Party  
↓  
Registrar NS Configuration  
↓  
Route 53 Name Servers  
↓  
[[Route 53 Hosted Zones|Public Hosted Zone]]  
↓  
DNS Records

---

## Step 1 — Create a Public Hosted Zone

Suppose you own:

example.com

at a third-party registrar.

In Route 53, create:

**Public Hosted Zone**

for:

example.com

Route 53 then creates important records including:

- NS
- SOA

The key records for this scenario are:

**NS Records**

---

## Step 2 — Route 53 Provides Name Servers

Route 53 assigns authoritative DNS servers to the hosted zone.

Conceptually:

example.com  
↓  
NS  
↓  
Route 53 Name Server 1  
Route 53 Name Server 2  
Route 53 Name Server 3  
Route 53 Name Server 4

These servers become responsible for answering DNS queries for your domain once delegation is configured.

---

## Step 3 — Update the Third-Party Registrar

Go back to the registrar where the domain is registered.

Replace the registrar's existing Name Server configuration with the:

**Route 53 Name Servers**

Conceptually:

Third-Party Registrar  
↓  
"Who manages DNS for example.com?"  
↓  
Route 53 Name Servers

This delegates DNS authority to Route 53.

---

## Step 4 — Route 53 Becomes Authoritative DNS

After the Name Server change propagates:

Client  
↓  
DNS Query for example.com  
↓  
DNS Hierarchy  
↓  
Route 53 Authoritative Name Servers  
↓  
[[Route 53 Hosted Zones|Public Hosted Zone]]  
↓  
DNS Answer

Route 53 now manages DNS resolution for the domain.

The domain itself can remain registered with the third-party registrar.

---

## Name Server Records Are the Key

This is the main SAA exam concept.

To use Route 53 with a third-party registrar:

> **Update the registrar's NS records to point to the Route 53 Name Servers.**

You do not need to:

- Transfer the domain
- Re-purchase the domain
- Move ownership to AWS

You simply change:

**DNS delegation**

---

## Architecture Thinking

### Scenario 1 — GoDaddy Domain + Route 53

A company purchased:

example.com

through GoDaddy.

They want Route 53 to manage all DNS records.

What should they do?

**Choose → Create a Route 53 Public Hosted Zone and update the registrar's Name Servers to the Route 53 Name Servers.**

No domain transfer is required.

---

### Scenario 2 — Company Does Not Want to Transfer Domain

A company must keep its existing registrar for business reasons.

However, it wants to use:

- [[Route 53 Routing Policies]]
- [[Route 53 Health Checks]]
- [[Route 53 Alias Records]]

Can it still use Route 53?

**Yes.**

Keep:

Domain Registration → Third Party

Use:

DNS Hosting → [[Route 53]]

Update:

**NS Records at Registrar**

---

### Scenario 3 — Transfer Domain to Route 53?

An exam question says:

> A domain is registered with a third-party registrar. The company wants Route 53 to provide DNS resolution. What is the most operationally efficient solution?

Do **not** automatically choose:

Transfer the domain to Route 53.

Instead:

1. Create Route 53 Public Hosted Zone
2. Retrieve Route 53 Name Servers
3. Update Name Servers at existing registrar

---

## Third-Party Registrar Architecture

Think of it as two separate layers:

### Registration Layer

Third-Party Registrar  
↓  
Owns / Registers  
example.com

### DNS Layer

[[Route 53]]  
↓  
Hosts DNS Records  
↓  
A / AAAA / Alias / CNAME / MX / etc.

The connection between them is:

**NS Records**

---

## Why This Architecture Is Useful

This separation gives organizations flexibility.

A company might keep its registrar because of:

- Existing contracts
- Corporate policy
- Centralized domain management
- Administrative requirements

while still using AWS DNS features such as:

- [[Route 53 Weighted Routing]]
- [[Route 53 Latency Routing]]
- [[Route 53 Failover Routing]]
- [[Route 53 Geolocation Routing]]
- [[Route 53 Health Checks]]
- [[Route 53 Alias Records]]

---

## NS vs DNS Records

Do not confuse the registrar's Name Server configuration with the DNS records inside the Route 53 Hosted Zone.

### Registrar NS Configuration

Answers:

> **"Which DNS servers are authoritative for this domain?"**

Points to:

**Route 53 Name Servers**

---

### Route 53 Hosted Zone Records

Answer:

> **"Where should this hostname resolve?"**

Examples:

example.com  
↓  
[[Application Load Balancer]]

mail.example.com  
↓  
Mail Server

www.example.com  
↓  
[[05-Networking/CloudFront]]

---

## Scenario Recognition

### Immediately Think Third-Party Registrar + Route 53 When You See

- Domain purchased outside AWS
- GoDaddy
- Namecheap
- External registrar
- Keep existing registrar
- Use Route 53 for DNS
- Delegate DNS to Route 53
- Update Name Servers
- NS records

### Strongest Exam Keyword

> **Third-party registrar + Route 53 DNS → Update NS Records**

---

## Exam Traps

### Trap 1 — Must Transfer Domain to Route 53

False.

Domain registration and DNS service are separate.

You can keep the domain at the existing registrar.

---

### Trap 2 — Create Only an A Record at the Registrar

That misses the architecture requirement.

If Route 53 should manage DNS:

**Delegate the domain to Route 53 using Name Servers.**

---

### Trap 3 — Change the SOA Record at the Registrar

The important delegation step is:

**Update the Name Server records**

to the Route 53 Name Servers.

---

### Trap 4 — Registrar and DNS Service Must Match

False.

You can use:

Registrar → Third Party

DNS → Route 53

---

### Trap 5 — Private Hosted Zone for Public Internet Domain

If public Internet users need DNS resolution:

Use:

[[Route 53 Hosted Zones|Public Hosted Zone]]

not a Private Hosted Zone.

---

## Quick Cheat Sheet

| Requirement | Action |
|---|---|
| Domain registered outside AWS | Keep registrar |
| Want Route 53 DNS | Create Public Hosted Zone |
| Connect registrar to Route 53 | Update NS Records |
| Transfer domain required | ❌ |
| Route 53 becomes authoritative DNS | ✅ |
| Registrar and DNS provider can differ | ✅ |
| Public Internet DNS | Public Hosted Zone |

---

## Master Memory Trick

> [!tip] Master Memory Trick
> **Registrar owns the NAME**
>
> **Route 53 can answer for the NAME**
>
> The bridge between them:
>
> **NS Records**

Remember the workflow:

**Third-Party Registrar**

↓ Update NS

**Route 53 Name Servers**

↓  

**Route 53 Public Hosted Zone**

And the big exam rule:

> **You do NOT need to transfer the domain to Route 53 to use Route 53 DNS.**

---

## Related Notes

- [[Route 53]]
- [[Route 53 Hosted Zones]]
- [[Route 53 Records]]
- [[Route 53 Alias Records]]
- [[Route 53 Routing Policies]]
- [[Route 53 Health Checks]]
- [[DNS]]
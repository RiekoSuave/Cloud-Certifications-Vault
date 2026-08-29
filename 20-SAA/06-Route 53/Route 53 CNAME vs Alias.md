## What Problem Does It Solve?

[[Route 53 CNAME vs Alias]] solves an important DNS architecture problem:

> **"How do I point my domain name to another hostname or AWS resource?"**

Both **CNAME records** and **Alias records** can point one DNS name toward another destination.

But they are **not interchangeable**.

The biggest SAA distinction is:

**CNAME → hostname to hostname**

**Alias → hostname to supported AWS resource**

And most importantly:

> **CNAME cannot be used at the zone apex.**
>
> **Alias can.**

> [!tip] Memory Trick
> **CNAME = Child names only**
>
> **Alias = AWS-friendly and Apex-friendly**

---

## Why This Matters

Many AWS resources expose a DNS hostname instead of giving you a permanent static IP address.

Examples include:

- [[Application Load Balancer]]
- [[Network Load Balancer]]
- [[05-Networking/CloudFront]]

Example AWS resource hostname:

my-alb-123456.us-east-1.elb.amazonaws.com

But you want users to access:

example.com

or:

www.example.com

[[Route 53]] needs a way to map your friendly domain name to that AWS resource.

That is where:

- CNAME
- Alias Records

become important.

---

## What Is a CNAME Record?

CNAME stands for:

**Canonical Name**

A CNAME maps:

**Hostname → Another hostname**

Example:

www.example.com  
↓  
CNAME  
↓  
app.example.net

The target hostname then resolves to its final IP address.

Conceptually:

Client  
↓  
www.example.com  
↓  
CNAME  
↓  
app.example.net  
↓  
A / AAAA Record  
↓  
IP Address

### Important

A CNAME does **not** map directly to an IP address.

It maps:

**Name → Name**

> [!tip] Memory Trick
> **CNAME = Name points to another Name**

---

## CNAME Limitation — Zone Apex

This is one of the most important Route 53 exam rules.

You **cannot use a CNAME at the zone apex**.

Suppose your hosted zone is:

example.com

The zone apex is:

example.com

So:

❌ example.com → CNAME

But:

✅ www.example.com → CNAME

✅ api.example.com → CNAME

✅ shop.example.com → CNAME

### Why This Matters

Companies commonly want their root domain:

example.com

to point directly to an AWS resource such as an [[Application Load Balancer]].

A standard CNAME cannot do this.

That is where a:

**Route 53 Alias Record**

becomes useful.

---

## What Is the Zone Apex?

The **zone apex** is the root name of the DNS namespace.

Example hosted zone:

example.com

Zone apex:

example.com

Subdomains:

www.example.com  
api.example.com  
shop.example.com

### Memory Trick

**Apex = Top**

So:

**example.com = Apex**

**www.example.com = Below the apex**

---

## What Is a Route 53 Alias Record?

An **Alias Record** is a Route 53 extension to standard DNS functionality.

It maps:

**Hostname → Supported AWS Resource**

Example:

example.com  
↓  
Alias Record  
↓  
[[Application Load Balancer]]

The important advantage is:

**Alias Records work at both the zone apex and subdomains.**

So:

✅ example.com → Alias → ALB

✅ www.example.com → Alias → ALB

---

## Alias Records and AWS Resources

Alias Records are designed to point Route 53 DNS names toward supported AWS resources.

Example:

example.com  
↓  
[[Route 53]] Alias  
↓  
my-alb-123456.us-east-1.elb.amazonaws.com  
↓  
[[Application Load Balancer]]

The ALB's underlying IP addresses may change over time.

Route 53 automatically tracks the AWS resource.

You do not need to manually update the record every time the resource changes.

> [!tip] Architecture Thinking
> **AWS-managed hostname + Route 53 = Think Alias first**

---

## CNAME vs Alias Architecture

### CNAME

www.example.com  
↓  
CNAME  
↓  
another-hostname.example.net  
↓  
IP Address

### Alias

example.com  
↓  
[[Route 53]] Alias  
↓  
AWS Resource  
↓  
AWS-managed endpoint

The biggest architecture difference:

**CNAME follows standard DNS rules**

while:

**Alias is Route 53's AWS-aware extension**

---

## Alias Records Can Be Used at the Root Domain

This is the biggest exam advantage.

Suppose users should access:

example.com

and your application is behind an:

[[Application Load Balancer]]

The ALB exposes:

my-alb-123456.us-east-1.elb.amazonaws.com

You cannot create:

example.com  
↓  
CNAME  
↓  
my-alb...

because the root domain is the zone apex.

Instead:

example.com  
↓  
Alias Record  
↓  
[[Application Load Balancer]]

**Choose → Alias Record**

---

## Alias Records Are Type A or AAAA

Alias Records still appear as DNS record types:

- A
- AAAA

But instead of pointing directly to an IP address, they point to a supported AWS resource.

Example:

Record Name:

example.com

Record Type:

A

Alias:

Enabled

Target:

[[Application Load Balancer]]

This is an AWS extension to normal DNS behavior.

---

## Alias Records Automatically Track AWS Resource Changes

AWS resources may change their underlying IP addresses.

Example:

[[Application Load Balancer]]

You should **not** hard-code the temporary IP addresses behind the ALB.

Instead:

example.com  
↓  
Alias  
↓  
ALB DNS Name  
↓  
AWS manages changing IP addresses

### Architecture Thinking

Alias Records provide an abstraction between:

**Your domain**

and

**AWS-managed infrastructure**

This reduces operational overhead.

---

## Alias Records and TTL

With standard DNS records, you normally configure a TTL.

With Route 53 Alias Records:

**You cannot manually configure the TTL.**

Route 53 uses the TTL behavior of the target AWS resource.

This is another exam distinction between:

**Normal DNS records**

and:

**Alias Records**

---

## Alias Records and Cost

The SAA slides highlight that Alias queries to AWS resources are:

**Free of charge**

This makes Alias Records especially attractive when integrating Route 53 with supported AWS services.

### Memory Trick

**Alias = AWS-native + Apex + Automatic**

---

## Alias Records and Health Checks

Alias Records provide **native health-check integration** with supported AWS resources.

This is useful in architectures involving:

- [[Route 53 Health Checks]]
- Failover
- Load balancing
- Highly available applications

The details become more important when we cover:

[[Route 53 Routing Policies]]

and:

[[Route 53 Health Checks]]

---

## Common Architecture Pattern — Route 53 + ALB

A very common SAA architecture looks like:

Users  
↓  
example.com  
↓  
[[Route 53]]  
↓ Alias Record  
[[Application Load Balancer]]  
↓  
[[EC2]] Instances

Why Alias?

Because:

- ALB provides a hostname
- ALB IP addresses can change
- Root domain may need to be used
- Alias integrates natively with AWS

---

## Architecture Thinking

### Scenario 1 — Root Domain to ALB

A company wants:

example.com

to point to an:

[[Application Load Balancer]]

The ALB exposes an AWS DNS hostname.

**Choose → Route 53 Alias Record**

Why?

The root domain is the zone apex.

CNAME cannot be used there.

---

### Scenario 2 — Subdomain to External Hostname

A company wants:

blog.example.com

to point to:

company.wordpress.com

The destination is not necessarily an AWS resource.

**Choose → CNAME**

Why?

The requirement is simply:

**Hostname → Hostname**

and the source is not the zone apex.

---

### Scenario 3 — Root Domain to CloudFront

A company wants:

example.com

to point to a [[05-Networking/CloudFront]] distribution.

**Choose → Alias Record**

Why?

Alias supports AWS resources and works at the zone apex.

---

### Scenario 4 — www Subdomain to AWS Resource

A company wants:

www.example.com

to point to an [[Application Load Balancer]].

Technically, because this is not the zone apex, CNAME may be possible.

But in Route 53:

**Alias is generally the better AWS-native choice**

because it integrates directly with supported AWS resources.

---

## CNAME vs Alias

| Feature | CNAME | Alias |
|---|---|---|
| Hostname → Hostname | ✅ | ✅ for supported AWS resources |
| Hostname → AWS Resource | Possible via AWS hostname | ✅ Native |
| Zone Apex | ❌ | ✅ |
| Subdomain | ✅ | ✅ |
| AWS-Aware | ❌ | ✅ |
| Tracks AWS Resource Changes | Indirectly | ✅ |
| Manual TTL | ✅ | ❌ |
| Free Alias Queries to AWS Resource | N/A | ✅ |
| Native Health Check Integration | ❌ | ✅ |

---

## Scenario Recognition

### Immediately Think CNAME When You See

- Hostname → another hostname
- Non-root domain
- External DNS hostname
- www.example.com → another hostname
- Standard DNS aliasing

### Immediately Think Alias When You See

- Root domain
- Zone apex
- AWS resource
- Load Balancer
- CloudFront
- AWS-managed endpoint
- Cannot use CNAME at root
- Route 53 native AWS integration

---

## Exam Traps

### Trap 1 — Using CNAME at the Root Domain

This is the classic trap.

You cannot create:

example.com → CNAME

because:

example.com

is the zone apex.

Use:

**Alias Record**

instead.

---

### Trap 2 — Hard-Coding ALB IP Addresses

An [[Application Load Balancer]] uses AWS-managed IP addresses that can change.

Do not point your DNS record to a manually discovered ALB IP address.

Use:

[[Route 53]]  
↓  
Alias  
↓  
[[Application Load Balancer]]

---

### Trap 3 — Thinking Alias Is a Standard DNS Record Type

Alias is **not a normal DNS record type** like:

- A
- AAAA
- CNAME

It is a Route 53 extension.

Alias Records commonly appear as:

**A or AAAA records with Alias enabled**

---

### Trap 4 — Manually Setting Alias TTL

You cannot manually configure TTL for a Route 53 Alias Record.

AWS manages it based on the target resource.

---

### Trap 5 — Always Choosing CNAME for Hostname-to-Hostname

A CNAME can point one hostname to another hostname.

But when the target is a supported AWS resource, especially at the root domain:

**Alias is usually the better Route 53 answer.**

---

## Quick Cheat Sheet

| Requirement | Best Choice |
|---|---|
| Hostname → IPv4 | A |
| Hostname → IPv6 | AAAA |
| Hostname → Hostname | CNAME |
| Root Domain → AWS Resource | Alias |
| Subdomain → AWS Resource | Alias |
| Zone Apex | Alias |
| External Hostname | CNAME |
| ALB Target | Alias |
| CloudFront Target | Alias |
| AWS Resource IPs May Change | Alias |

---

## Master Memory Trick

> [!tip] Master Memory Trick
> **CNAME = Child Name**
>
> **Alias = AWS + Apex**

Remember:

**CNAME**

- Name → Name
- No zone apex
- Standard DNS

**Alias**

- Name → AWS Resource
- Works at zone apex
- AWS-native
- No manual TTL
- Tracks AWS resource changes

The exam shortcut:

> **Root domain + AWS resource = Alias**

---

## Related Notes

- [[Route 53]]
- [[Route 53 TTL]]
- [[Route 53 Alias Records]]
- [[Route 53 Routing Policies]]
- [[Route 53 Health Checks]]
- [[Application Load Balancer]]
- [[Network Load Balancer]]
- [[05-Networking/CloudFront]]
- [[EC2]]
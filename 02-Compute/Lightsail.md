See also: [[02-Compute/EC2]]

See also: [[RDS]]

See also: [[Elastic Load Balancing (ELB)]]

## What Problem Does It Solve?

Provides a simple, easy-to-manage cloud environment for small applications and websites without requiring users to configure many separate AWS services.

---

## Type

Simplified Compute Service

---

## What Is Lightsail?

Lightsail provides simplified access to:

- Virtual servers
- Storage
- Databases
- Networking

It bundles common cloud resources into an easier-to-use service.

---

## Why Use Lightsail?

Building an application directly with AWS may require configuring multiple services such as:

- EC2
- RDS
- ELB
- EBS
- Route 53

Lightsail provides a simpler alternative.

### Memory Trick

Lightsail = Easy AWS hosting

---

## Pricing

Lightsail focuses on:

- Low pricing
- Predictable pricing

This makes costs easier to understand for simple workloads.

---

## Preconfigured Applications

Lightsail provides templates for common application stacks.

Examples from the course:

- LAMP
- Nginx
- MEAN
- Node.js

It also provides website templates such as:

- WordPress
- Magento
- Plesk
- Joomla

---

## Common Use Cases

### Simple Web Applications

Quickly deploy common web application stacks.

---

### Websites

Useful for applications such as:

- Blogs
- WordPress websites
- Small business websites

---

### Development and Testing

Can provide simple environments for:

- Development
- Testing

---

## Monitoring

Lightsail allows you to monitor resources and configure notifications.

---

## High Availability

Lightsail can provide high availability.

However, your course notes identify an important limitation:

Lightsail does NOT provide Auto Scaling.

---

## Limitations

Compared with using individual AWS services directly, Lightsail has:

- Limited AWS integrations
- Less flexibility
- No Auto Scaling

For more complex architectures, EC2 and other individual AWS services provide greater control.

---

## Lightsail vs EC2

| Lightsail | EC2 |
|---|---|
| Simpler | More configurable |
| Predictable pricing | More pricing options |
| Beginner friendly | Greater control |
| Bundled services | Build architecture using individual services |
| Limited integrations | Broad AWS integrations |

---

## Compare Against

EC2 → More control and customization

RDS → Dedicated managed relational database service

ELB → Dedicated load balancing service

Route 53 → Dedicated DNS service

---

## Exam Scenarios

A small business wants a simple WordPress website with predictable pricing.

→ Lightsail

---

A developer with little cloud experience wants to quickly deploy a simple application.

→ Lightsail

---

A company needs extensive AWS integrations and detailed infrastructure control.

→ Consider EC2 and individual AWS services instead of Lightsail

---

A workload requires automatic scaling of compute resources.

→ Lightsail is not the appropriate choice based on the course notes

---

## Exam Keywords

Simple

Beginner friendly

Predictable pricing

Virtual server

Website

WordPress

Preconfigured templates

---

## Memory Tricks

Lightsail = Easy EC2

Lightsail = Simple + Predictable

EC2 = More Control
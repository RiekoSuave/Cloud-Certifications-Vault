See also: [VPC](05-Networking/VPC.md)

See also: [VPC Peering](<05-Networking/VPC Peering.md>)

See also: [Direct Connect](<05-Networking/Direct Connect.md>)

See also: [Site-to-Site VPN](<05-Networking/Site-to-Site VPN.md>)

## What Problem Does It Solve?

Simplifies networking when many VPCs and on-premises networks need to communicate.

Instead of creating many individual connections between networks, Transit Gateway provides a centralized networking hub.

### Memory Trick

Transit Gateway = Router for VPCs

---

## Type

Network Hub

---

## What Is Transit Gateway?

Transit Gateway provides a central gateway for connecting multiple:

- VPCs
- On-premises networks

Think of Transit Gateway as the center of your network.

Basic Idea:

VPC A ↘

VPC B → Transit Gateway ← On-Premises

VPC C ↗

### Memory Trick

Transit Gateway = Central Network Hub

---

## Hub-and-Spoke Architecture

Your course describes Transit Gateway using a:

Hub-and-Spoke

or:

Star

architecture.

Transit Gateway acts as the:

Hub

The connected VPCs and networks act as:

Spokes

Example:

VPC A

↓

Transit Gateway

↑        ↑

VPC B   VPC C

### Memory Trick

Transit Gateway = Hub

VPCs = Spokes

---

## Why Use Transit Gateway?

Without centralized networking, connecting many VPCs individually can become complex.

Conceptually:

VPC A ↔ VPC B

VPC A ↔ VPC C

VPC B ↔ VPC C

As more VPCs are added, more individual connections may be required.

Transit Gateway simplifies this by providing:

One Central Gateway

↓

Many Connected Networks

### Memory Trick

Many Networks?

→ Transit Gateway

---

## Transitive Connectivity

Your course associates Transit Gateway with:

Transitive connectivity

between large numbers of VPCs and on-premises networks.

Think:

VPC A

↓

Transit Gateway

↓

VPC B

The central Transit Gateway provides the networking hub between connected environments.

### Memory Trick

Transit Gateway = Centralized Transitive Networking

---

## Scalability

Your course describes Transit Gateway as being designed to connect:

Thousands of VPCs

and:

On-Premises Networks

The important concept is:

Transit Gateway is designed for large-scale centralized networking.

---

## Transit Gateway and On-Premises Networks

Transit Gateway is not limited to VPC-to-VPC connectivity.

Your course notes that it can work with:

- VPN Connections
- Direct Connect Gateway

This allows Transit Gateway to participate in hybrid networking architectures.

Basic Concept:

VPCs

↓

Transit Gateway

↓

VPN / Direct Connect

↓

On-Premises

---

## Transit Gateway vs VPC Peering

This is one of the most important comparisons.

### VPC Peering

Direct connection between VPCs.

Think:

VPC A ↔ VPC B

### Transit Gateway

Central hub connecting many networks.

Think:

VPC A ↘

VPC B → Transit Gateway

VPC C ↗

| VPC Peering | Transit Gateway |
|---|---|
| Direct VPC connection | Central network hub |
| Point-to-point concept | Hub-and-spoke concept |
| VPC ↔ VPC | Many networks ↔ Hub |
| Simpler small connectivity | Centralized large-scale connectivity |

### Memory Trick

Peering = Direct

Transit Gateway = Hub

See:

[VPC Peering](<05-Networking/VPC Peering.md>)

---

## Transit Gateway vs Direct Connect

### Transit Gateway

Connects and routes between multiple networks through a central hub.

### Direct Connect

Provides dedicated private connectivity between an on-premises network and AWS.

They solve different problems and can work together.

### Memory Trick

Transit Gateway = Connect Many Networks

Direct Connect = Private Line to AWS

See:

[Direct Connect](<05-Networking/Direct Connect.md>)

---

## Transit Gateway vs Site-to-Site VPN

### Transit Gateway

Acts as a centralized networking hub.

### Site-to-Site VPN

Provides an encrypted connection between an on-premises network and AWS over the public internet.

Transit Gateway can work with VPN connections.

### Memory Trick

Transit Gateway = Hub

VPN = Encrypted Internet Connection

See:

[Site-to-Site VPN](<05-Networking/Site-to-Site VPN.md>)

---

## Common Use Cases

- Connecting many VPCs
- Connecting VPCs with on-premises networks
- Large organizations
- Multi-account AWS environments
- Centralized networking
- Hybrid networking

---

## Scenario Questions

A company has many VPCs and wants a centralized way to connect them.

→ Transit Gateway

---

An organization wants a hub-and-spoke network architecture for its VPCs.

→ Transit Gateway

---

A company needs to connect thousands of VPCs and on-premises networks through a centralized gateway.

→ Transit Gateway

---

Two VPCs need a direct private connection.

→ VPC Peering

---

A company needs a dedicated physical private connection between its data center and AWS.

→ Direct Connect

NOT Transit Gateway

---

A company needs an encrypted connection between its on-premises network and AWS over the public internet.

→ Site-to-Site VPN

NOT Transit Gateway

---

## Don't Confuse These

Transit Gateway = Central Network Hub

VPC Peering = Direct VPC ↔ VPC Connection

Direct Connect = Dedicated Private Connection to AWS

Site-to-Site VPN = Encrypted Connection Over Public Internet

Internet Gateway = VPC ↔ Internet

---

## Exam Keywords

Transit Gateway

Centralized Networking

Network Hub

Hub-and-Spoke

Star Architecture

Transitive Connectivity

Multiple VPCs

On-Premises Networks

Direct Connect Gateway

VPN Connections

---

## Quick Cheat Sheet

Transit Gateway = Router for VPCs

Transit Gateway = Central Hub

Hub = Transit Gateway

Spokes = VPCs / Networks

Peering = Direct VPC ↔ VPC

Transit Gateway = Many Networks ↔ Hub

Direct Connect = Private Line to AWS

Site-to-Site VPN = Encrypted Internet Connection
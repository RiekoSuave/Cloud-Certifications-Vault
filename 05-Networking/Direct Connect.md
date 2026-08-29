See also: [VPC](05-Networking/VPC.md)

See also: [Site-to-Site VPN](<05-Networking/Site-to-Site VPN.md>)

See also: [Transit Gateway](<05-Networking/Transit Gateway.md>)

## What Problem Does It Solve?

Provides a dedicated private physical connection between an on-premises network and AWS.

Unlike a Site-to-Site VPN, Direct Connect does not rely on the public internet for the connection.

### Memory Trick

Direct Connect = Private Line to AWS

---

## Type

Hybrid Networking

Private Networking

---

## What Is Direct Connect?

Direct Connect establishes a physical connection between:

On-Premises

↕

AWS

The connection travels over a:

Private Network

rather than the public internet.

### Memory Trick

Direct Connect = Dedicated Physical Connection

---

## Basic Architecture

On-Premises Network

↓

Direct Connect

↓

Private Network Connection

↓

AWS

The important concept is:

Direct Connect provides dedicated connectivity between an organization's network and AWS.

---

## Key Features

Your course associates Direct Connect with:

- Dedicated connectivity
- Private networking
- Secure connectivity
- Fast connectivity
- More reliable connectivity

### Memory Trick

Direct Connect = Dedicated + Private

---

## Public Internet

Direct Connect does not use the public internet for its Direct Connect connection.

This is one of the major differences between:

Direct Connect

and:

Site-to-Site VPN

### Memory Trick

VPN = Public Internet

Direct Connect = Private Network

---

## Connection Setup

Your course notes that Direct Connect:

Takes at least a month to establish

This is important because Direct Connect involves establishing a physical connection rather than simply creating an internet-based VPN connection.

### Memory Trick

Direct Connect = Physical Connection = Takes Time

---

## Direct Connect vs Site-to-Site VPN

Both can connect an on-premises environment to AWS.

### Direct Connect

- Physical connection
- Private network
- Secure and fast
- Takes longer to establish

### Site-to-Site VPN

- Uses the public internet
- Automatically encrypted
- Connects on-premises networks to AWS

| Direct Connect | Site-to-Site VPN |
|---|---|
| Private network | Public internet |
| Physical connection | VPN connection |
| Dedicated connectivity | Internet-based connectivity |
| Takes time to establish | Does not require dedicated physical connectivity |

### Memory Trick

Direct Connect = Private Line

Site-to-Site VPN = Encrypted Internet Connection

See:

[Site-to-Site VPN](<05-Networking/Site-to-Site VPN.md>)

---

## Direct Connect vs Internet Gateway

### Direct Connect

Connects:

On-Premises ↔ AWS

using dedicated private connectivity.

### Internet Gateway

Connects:

VPC ↔ Internet

### Memory Trick

Direct Connect = On-Prem → AWS

Internet Gateway = VPC → Internet

---

## Direct Connect vs VPC Peering

### Direct Connect

Connects:

On-Premises ↔ AWS

### VPC Peering

Connects:

VPC ↔ VPC

### Memory Trick

Direct Connect = On-Prem → AWS

Peering = VPC → VPC

---

## Common Use Cases

### Hybrid Cloud

Connect an organization's on-premises environment with AWS.

### Enterprise Networks

Provide dedicated private connectivity between enterprise infrastructure and AWS.

---

## Scenario Questions

A company needs a dedicated physical connection between its on-premises network and AWS.

→ Direct Connect

---

A company wants its AWS connection to travel over a private network instead of the public internet.

→ Direct Connect

---

A company needs an encrypted connection to AWS over the public internet.

→ Site-to-Site VPN

NOT Direct Connect

---

A company needs to connect two VPCs privately.

→ VPC Peering

NOT Direct Connect

---

A VPC needs connectivity to the public internet.

→ Internet Gateway

NOT Direct Connect

---

## Don't Confuse These

Direct Connect = Dedicated Private Connection

Site-to-Site VPN = Encrypted Connection Over Public Internet

VPC Peering = VPC ↔ VPC

Internet Gateway = VPC ↔ Internet

Transit Gateway = Central Network Hub

---

## Exam Keywords

Direct Connect

DX

Dedicated Connection

Physical Connection

Private Network

On-Premises

Hybrid Cloud

Enterprise Network

---

## Quick Cheat Sheet

Direct Connect = Private Line to AWS

DX = Dedicated Physical Connection

Direct Connect = On-Premises ↔ AWS

Direct Connect = Private Network

Site-to-Site VPN = Public Internet + Encryption

VPN = Faster to Establish

Direct Connect = Takes Time to Establish
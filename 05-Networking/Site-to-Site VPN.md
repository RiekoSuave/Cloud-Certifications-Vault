See also: [VPC](05-Networking/VPC.md)

See also: [Direct Connect](<05-Networking/Direct Connect.md>)

See also: [Transit Gateway](<05-Networking/Transit Gateway.md>)

## What Problem Does It Solve?

Connects an on-premises network to AWS using an encrypted VPN connection.

Site-to-Site VPN allows an organization to establish private communication between its on-premises network and AWS over the public internet.

### Memory Trick

Site-to-Site VPN = Encrypted Connection to AWS Over Internet

---

## Type

Hybrid Networking Connection

---

## What Is Site-to-Site VPN?

Site-to-Site VPN connects:

On-Premises Network

↕

Encrypted VPN Connection

↕

AWS

The connection travels over the:

Public Internet

But the VPN connection itself is:

Encrypted

### Memory Trick

VPN = Encrypted Over Public Internet

---

## Basic Architecture

Your course identifies two important components:

### Customer Gateway (CGW)

Located on the:

On-Premises side

### Virtual Private Gateway (VGW)

Located on the:

AWS side

Basic Architecture:

On-Premises Network

↓

Customer Gateway (CGW)

↓

Encrypted Site-to-Site VPN

↓

Public Internet

↓

Virtual Private Gateway (VGW)

↓

AWS VPC

---

## Customer Gateway (CGW)

The Customer Gateway represents the:

On-Premises side

of the Site-to-Site VPN connection.

### Memory Trick

Customer Gateway = Customer Side

CGW = On-Premises

---

## Virtual Private Gateway (VGW)

The Virtual Private Gateway represents the:

AWS side

of the Site-to-Site VPN connection.

### Memory Trick

Virtual Private Gateway = AWS Side

VGW = AWS

---

## CGW vs VGW

| Component | Location |
|---|---|
| Customer Gateway (CGW) | On-Premises |
| Virtual Private Gateway (VGW) | AWS |

### Memory Trick

CGW = Customer

VGW = VPC / AWS

---

## Encryption

Your course states that the Site-to-Site VPN connection is:

Automatically encrypted.

This allows network traffic to travel securely between the on-premises network and AWS.

### Memory Trick

Site-to-Site VPN = Encrypted

---

## Public Internet

Site-to-Site VPN travels over the:

Public Internet

This is one of the major differences between Site-to-Site VPN and Direct Connect.

### Memory Trick

VPN = Public Internet

Direct Connect = Private Network

---

## Site-to-Site VPN vs Direct Connect

Both can connect an on-premises environment with AWS.

The major difference is how the connection is established.

### Site-to-Site VPN

- Encrypted
- Uses the public internet

### Direct Connect

- Physical connection
- Private network
- Secure and fast
- Takes longer to establish

| Site-to-Site VPN | Direct Connect |
|---|---|
| Public internet | Private network |
| Automatically encrypted | Dedicated physical connection |
| VPN connection | Direct connection |
| On-Premises ↔ AWS | On-Premises ↔ AWS |

### Memory Trick

VPN = Encrypted Internet Connection

Direct Connect = Private Line to AWS

See:

[Direct Connect](<05-Networking/Direct Connect.md>)

---

## Site-to-Site VPN vs VPC Peering

### Site-to-Site VPN

Connects:

On-Premises ↔ AWS

### VPC Peering

Connects:

VPC ↔ VPC

### Memory Trick

VPN = On-Prem → AWS

Peering = VPC → VPC

---

## Site-to-Site VPN vs Client VPN

Your course also introduces:

Client VPN

These solve different connection needs.

### Site-to-Site VPN

Connects an:

On-Premises Network

to:

AWS

### Client VPN

Allows an individual computer to connect to a private network in AWS and on-premises using OpenVPN.

Your course notes that Client VPN travels over the public internet.

### Memory Trick

Site-to-Site = Network → Network

Client VPN = Computer → Private Network

---

## Client VPN

Your course describes Client VPN as allowing you to connect from your computer using:

OpenVPN

This can provide access to private resources such as EC2 instances using their private IP addresses.

Basic Idea:

Computer

↓

Client VPN

↓

Public Internet

↓

Private AWS Network

### Memory Trick

Client VPN = My Computer → Private AWS Network

---

## Common Use Cases

- Hybrid cloud connectivity
- Connecting an on-premises network to AWS
- Encrypted communication with AWS
- Extending an organization's network into AWS

---

## Scenario Questions

A company needs an encrypted connection between its on-premises network and AWS over the public internet.

→ Site-to-Site VPN

---

A company needs a dedicated physical private connection to AWS.

→ Direct Connect

NOT Site-to-Site VPN

---

Which component represents the on-premises side of a Site-to-Site VPN?

→ Customer Gateway (CGW)

---

Which component represents the AWS side of a Site-to-Site VPN?

→ Virtual Private Gateway (VGW)

---

An individual user needs to connect a computer to private AWS resources using OpenVPN.

→ Client VPN

---

Two VPCs need to communicate privately.

→ VPC Peering

NOT Site-to-Site VPN

---

## Don't Confuse These

Site-to-Site VPN = On-Premises ↔ AWS Over Public Internet

Direct Connect = On-Premises ↔ AWS Over Private Network

Customer Gateway = On-Premises Side

Virtual Private Gateway = AWS Side

Client VPN = Computer → Private Network

VPC Peering = VPC ↔ VPC

Transit Gateway = Central Network Hub

---

## Exam Keywords

Site-to-Site VPN

VPN

Encrypted

Public Internet

On-Premises

Customer Gateway

CGW

Virtual Private Gateway

VGW

Hybrid Networking

Client VPN

OpenVPN

---

## Quick Cheat Sheet

Site-to-Site VPN = Encrypted Public Internet Connection

VPN = On-Premises → AWS

CGW = Customer / On-Premises Side

VGW = AWS Side

Direct Connect = Private Physical Connection

Client VPN = Computer → Private Network

VPC Peering = VPC → VPC
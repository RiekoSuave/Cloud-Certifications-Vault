See also: [VPC](05-Networking/VPC.md)

See also: [Subnets](Subnets)

See also: [NAT Gateway](<NAT Gateway>)

## What Problem Does It Solve?

Provides internet connectivity for resources inside a VPC.

An Internet Gateway allows communication between a VPC and the internet.

### Memory Trick

Internet Gateway = Door to the Internet

---

## Type

VPC Networking Component

---

## What Is an Internet Gateway?

An Internet Gateway allows resources inside a VPC to communicate with the internet.

Basic Idea:

Internet

↕

Internet Gateway

↕

VPC

The Internet Gateway operates at the:

VPC level

---

## Internet Gateway and Public Subnets

A public subnet has a route to an:

Internet Gateway

Basic Flow:

Internet

↓

Internet Gateway

↓

Public Subnet

↓

AWS Resource

### Memory Trick

Public Subnet = Route to Internet Gateway

---

## Route Tables

Simply having an Internet Gateway associated with the VPC is not the entire concept.

The subnet's route table determines where network traffic should be sent.

For a public subnet:

Public Subnet

↓

Route Table

↓

Internet Gateway

↓

Internet

### Memory Trick

Route Table = Traffic Directions

Internet Gateway = Internet Destination

---

## Public Subnet Architecture

Example:

Internet

↓

Internet Gateway

↓

Public Subnet

↓

Internet-Facing Resource

This architecture is commonly used when resources need internet connectivity.

See:

[Subnets](Subnets)

---

## Internet Gateway vs NAT Gateway

These two are easy to confuse.

### Internet Gateway

Provides internet connectivity for the VPC.

Public subnets have a route to the Internet Gateway.

### NAT Gateway

Allows resources in private subnets to access the internet while remaining private.

### Basic Comparison

| Internet Gateway | NAT Gateway |
|---|---|
| VPC internet connectivity | Private subnet outbound internet access |
| Associated with VPC | Used by private subnets |
| Public subnet routes to it | Private subnet routes toward NAT |
| Internet Gateway = Internet access | NAT Gateway = Remain private |

### Memory Trick

IGW = Public → Internet

NAT Gateway = Private → Internet

See:

[NAT Gateway](<NAT Gateway>)

---

## Internet Gateway vs Route Table

### Internet Gateway

Provides the connection between the VPC and the internet.

### Route Table

Determines where network traffic is sent.

Think:

Route Table

→ Gives Directions

Internet Gateway

→ Provides the Door

### Memory Trick

Route Table = Directions

IGW = Door

---

## Common Use Cases

- Internet-facing applications
- Public subnets
- Web servers
- VPC internet connectivity

---

## Scenario Questions

A VPC needs connectivity to the internet.

→ Internet Gateway

---

A public subnet needs internet connectivity.

→ Route to an Internet Gateway

---

An EC2 instance is located in a private subnet and needs outbound internet access while remaining private.

→ NAT Gateway

NOT Internet Gateway alone

---

A company needs to determine where subnet traffic should be sent.

→ Route Table

---

## Don't Confuse These

VPC = Private AWS Network

Subnet = Section of VPC

Route Table = Traffic Directions

Internet Gateway = Door to Internet

NAT Gateway = Private Subnet → Internet

---

## Exam Keywords

Internet Gateway

IGW

Internet Access

VPC

Public Subnet

Route Table

---

## Quick Cheat Sheet

Internet Gateway = VPC Internet Access

IGW = Door to Internet

Public Subnet = Route to IGW

Route Table = Traffic Directions

NAT Gateway = Private → Internet
See also: [VPC](05-Networking/VPC.md)

See also: [VPC Peering](<05-Networking/VPC Peering.md>)

See also: [Internet Gateway](<Internet Gateway>)

See also: [NAT Gateway](<NAT Gateway>)

## What Problem Does It Solve?

Provides private connectivity between resources inside a VPC and supported AWS services.

A VPC Endpoint allows resources to access supported AWS services without requiring the traffic to use the public internet.

### Memory Trick

VPC Endpoint = Private Path to AWS Services

---

## Type

VPC Networking Component

---

## What Is a VPC Endpoint?

A VPC Endpoint provides private connectivity from a VPC to supported AWS services.

Basic Idea:

Resource in VPC

↓

VPC Endpoint

↓

AWS Service

### Memory Trick

Endpoint = VPC → AWS Service

---

## Why Use a VPC Endpoint?

Without private connectivity, accessing an AWS service may involve internet connectivity.

A VPC Endpoint provides a private path between your VPC and supported AWS services.

Think:

Private Resource

↓

Private Connection

↓

AWS Service

The important concept is:

Traffic does not need to travel through the public internet.

---

## Private Connectivity

VPC Endpoints are useful when resources inside a VPC need private access to supported AWS services.

Basic Architecture:

VPC

↓

Private Resource

↓

VPC Endpoint

↓

Supported AWS Service

### Memory Trick

Endpoint = Stay Private

---

## VPC Endpoint vs Internet Gateway

### VPC Endpoint

Provides private connectivity to supported AWS services.

### Internet Gateway

Provides internet connectivity for a VPC.

| VPC Endpoint | Internet Gateway |
|---|---|
| Private connectivity | Internet connectivity |
| VPC → AWS Service | VPC → Internet |
| Does not require public internet | Provides path to public internet |

### Memory Trick

Endpoint = Private AWS Access

IGW = Internet Access

---

## VPC Endpoint vs NAT Gateway

### VPC Endpoint

Provides private connectivity to supported AWS services.

### NAT Gateway

Allows resources in private subnets to initiate outbound internet connections while remaining private.

### Memory Trick

Endpoint = Private Path to AWS Service

NAT Gateway = Private → Internet

---

## VPC Endpoint vs VPC Peering

### VPC Endpoint

Connects:

VPC → Supported AWS Service

### VPC Peering

Connects:

VPC ↔ VPC

### Memory Trick

Endpoint = VPC to Service

Peering = VPC to VPC

See:

[VPC Peering](<05-Networking/VPC Peering.md>)

---

## Common Use Cases

- Private access to supported AWS services
- Keeping network traffic off the public internet
- Resources in private networks accessing AWS services

---

## Scenario Questions

Resources inside a VPC need private connectivity to a supported AWS service.

→ VPC Endpoint

---

A company wants AWS service traffic to avoid the public internet.

→ VPC Endpoint

---

Two VPCs need to communicate privately.

→ VPC Peering

NOT VPC Endpoint

---

A private EC2 instance needs general outbound internet access while remaining private.

→ NAT Gateway

NOT VPC Endpoint

---

A VPC needs connectivity to the public internet.

→ Internet Gateway

NOT VPC Endpoint

---

## Don't Confuse These

VPC Endpoint = VPC → AWS Service Privately

VPC Peering = VPC ↔ VPC

Internet Gateway = VPC ↔ Internet

NAT Gateway = Private Subnet → Internet

Transit Gateway = Central Network Hub

---

## Exam Keywords

VPC Endpoint

Private Connectivity

AWS Services

VPC

Private Access

No Public Internet

---

## Quick Cheat Sheet

VPC Endpoint = Private Path to AWS Services

Endpoint = VPC → AWS Service

Peering = VPC → VPC

Internet Gateway = VPC → Internet

NAT Gateway = Private → Internet
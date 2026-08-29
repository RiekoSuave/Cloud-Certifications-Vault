See also: [VPC](05-Networking/VPC.md)

See also: [Transit Gateway](<05-Networking/Transit Gateway.md>)

See also: [VPC Endpoints](<05-Networking/VPC Endpoints.md>)

## What Problem Does It Solve?

Allows two VPCs to communicate privately with each other.

VPC Peering provides private connectivity between VPC networks.

### Memory Trick

VPC Peering = VPC ↔ VPC

---

## Type

VPC Networking Connection

---

## What Is VPC Peering?

VPC Peering creates a private network connection between two VPCs.

Basic Idea:

VPC A

↕

VPC Peering Connection

↕

VPC B

Resources in the connected VPCs can communicate using private networking.

---

## Why Use VPC Peering?

Organizations may have resources separated into different VPCs.

For example:

VPC A

→ Application Resources

VPC B

→ Shared Resources

VPC Peering can provide private communication between the two VPCs.

### Memory Trick

Separate VPCs + Need Private Communication

→ VPC Peering

---

## Private Connectivity

VPC Peering is designed for private communication between VPCs.

Think:

VPC A

↓

Private Connection

↓

VPC B

### Memory Trick

Peering = Private VPC Connection

---

## VPC Peering vs Internet Gateway

### VPC Peering

Connects:

VPC ↔ VPC

### Internet Gateway

Connects:

VPC ↔ Internet

### Memory Trick

Peering = VPC to VPC

IGW = VPC to Internet

See:

[Internet Gateway](<Internet Gateway>)

---

## VPC Peering vs Transit Gateway

Both can be associated with connecting VPCs, but think about their basic purposes differently.

### VPC Peering

Direct private connection between VPCs.

Think:

VPC A ↔ VPC B

### Transit Gateway

Acts as a central networking hub.

Think:

VPC A ↘

VPC B → Transit Gateway

VPC C ↗

### Memory Trick

Peering = Direct Connection

Transit Gateway = Central Hub

See:

[Transit Gateway](<05-Networking/Transit Gateway.md>)

---

## VPC Peering vs VPC Endpoints

### VPC Peering

Connects one VPC with another VPC.

### VPC Endpoint

Provides private connectivity from a VPC to supported AWS services.

### Memory Trick

Peering = VPC → VPC

Endpoint = VPC → AWS Service

See:

[VPC Endpoints](<05-Networking/VPC Endpoints.md>)

---

## Common Use Cases

- Connecting two VPCs
- Private communication between VPC resources
- Connecting separated AWS network environments

---

## Scenario Questions

Two VPCs need to communicate privately.

→ VPC Peering

---

A company needs a direct private connection between two VPCs.

→ VPC Peering

---

A company needs a central networking hub for multiple VPCs.

→ Transit Gateway

NOT VPC Peering

---

Resources inside a VPC need private access to supported AWS services.

→ VPC Endpoint

NOT VPC Peering

---

A VPC needs connectivity to the public internet.

→ Internet Gateway

NOT VPC Peering

---

## Don't Confuse These

VPC Peering = VPC ↔ VPC

Internet Gateway = VPC ↔ Internet

VPC Endpoint = VPC → AWS Service

Transit Gateway = Central Network Hub

Direct Connect = On-Premises ↔ AWS Dedicated Connection

Site-to-Site VPN = On-Premises ↔ AWS Over Internet

---

## Exam Keywords

VPC Peering

VPC-to-VPC

Private Connectivity

Private Communication

VPC Connection

---

## Quick Cheat Sheet

VPC Peering = VPC ↔ VPC

Peering = Direct Private Connection

Internet Gateway = VPC ↔ Internet

VPC Endpoint = VPC → AWS Service

Transit Gateway = Central Hub
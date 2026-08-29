See also: [VPC](05-Networking/VPC.md)

See also: [Subnets](Subnets)

See also: [Internet Gateway](<Internet Gateway>)

## What Problem Does It Solve?

Allows resources in private subnets to access the internet while remaining private.

This is useful when private resources need outbound internet access without becoming directly accessible from the internet.

### Memory Trick

NAT Gateway = Private → Internet

---

## Type

VPC Networking Component

---

## What Is a NAT Gateway?

A NAT Gateway allows instances in a private subnet to access the internet while remaining private.

Basic Flow:

Private Subnet

↓

NAT Gateway

↓

Internet Gateway

↓

Internet

### Memory Trick

NAT = Private Resources Go Out

---

## Why Use a NAT Gateway?

Resources in private subnets may still need internet access.

For example, a private EC2 instance may need to:

- Download software
- Install updates
- Access resources on the internet

A NAT Gateway allows the private resource to initiate outbound internet connectivity while remaining private.

---

## Private Subnet Architecture

Basic Architecture:

Internet

↓

Internet Gateway

↓

Public Network Path

↓

NAT Gateway

↓

Private Subnet

↓

EC2 Instance

The important concept is:

The EC2 instance remains in the private subnet.

---

## NAT Gateway and Route Tables

Traffic from the private subnet must be routed toward the NAT Gateway.

Conceptually:

Private EC2 Instance

↓

Private Subnet

↓

Route Table

↓

NAT Gateway

↓

Internet Gateway

↓

Internet

### Memory Trick

Private Route → NAT

Public Route → IGW

---

## NAT Gateway vs Internet Gateway

These services solve different problems.

### Internet Gateway

Provides internet connectivity at the VPC level.

Public subnets have a route to the Internet Gateway.

### NAT Gateway

Allows resources in private subnets to access the internet while remaining private.

| Internet Gateway | NAT Gateway |
|---|---|
| VPC internet connectivity | Private subnet internet access |
| Used for public internet connectivity | Used by private resources |
| Public subnet routes toward IGW | Private subnet routes toward NAT |
| IGW = Internet door | NAT = Private outbound path |

### Memory Trick

IGW = Public → Internet

NAT = Private → Internet

See:

[Internet Gateway](<Internet Gateway>)

---

## NAT Gateway vs NAT Instance

Your course identifies two NAT options:

### NAT Gateway

AWS-managed

### NAT Instance

Self-managed

Both can allow instances in private subnets to access the internet while remaining private.

| NAT Gateway | NAT Instance |
|---|---|
| AWS-managed | Self-managed |
| NAT service | EC2-based NAT |
| Less infrastructure management | You manage the instance |

### Memory Trick

NAT Gateway = AWS Manages It

NAT Instance = You Manage It

---

## Public vs Private Internet Access

### Public Subnet

Public Subnet

↓

Internet Gateway

↓

Internet

### Private Subnet

Private Subnet

↓

NAT Gateway

↓

Internet Gateway

↓

Internet

### Quick Memory Trick

Public = IGW

Private = NAT → IGW

---

## Common Use Cases

- Private EC2 instances needing internet access
- Downloading software updates
- Accessing internet resources from private subnets
- Keeping application resources private

---

## Scenario Questions

An EC2 instance in a private subnet needs to access the internet while remaining private.

→ NAT Gateway

---

A company wants an AWS-managed NAT solution.

→ NAT Gateway

---

A company wants to manage its own NAT solution.

→ NAT Instance

---

A public subnet needs internet connectivity.

→ Internet Gateway

NOT NAT Gateway

---

A private subnet needs outbound internet connectivity.

→ NAT Gateway

---

## Don't Confuse These

Internet Gateway = VPC Internet Access

NAT Gateway = Private Subnet → Internet

NAT Instance = Self-Managed NAT

Route Table = Traffic Directions

Public Subnet = Route to IGW

Private Subnet = Route to NAT for Internet Access

---

## Exam Keywords

NAT Gateway

NAT Instance

Private Subnet

Outbound Internet Access

AWS-Managed

Self-Managed

Internet Gateway

Route Table

---

## Quick Cheat Sheet

NAT Gateway = Private → Internet

NAT Gateway = AWS-Managed

NAT Instance = Self-Managed

Public Subnet → IGW

Private Subnet → NAT Gateway → IGW

Route Table = Traffic Directions
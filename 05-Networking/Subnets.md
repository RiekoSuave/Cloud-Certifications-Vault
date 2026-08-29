See also: [VPC](05-Networking/VPC.md)

See also: [Internet Gateway](<Internet Gateway>)

See also: [NAT Gateway](<NAT Gateway>)

See also: [Security Groups vs NACLs](<Security Groups vs NACLs>)

## What Problem Does It Solve?

Divides a VPC into smaller network sections so resources can be organized and isolated.

Subnets help separate resources based on their networking and security requirements.

### Memory Trick

Subnet = Section of a VPC

---

## Type

VPC Network Segment

---

## What Is a Subnet?

A subnet is a partition of a VPC.

Basic Structure:

VPC

↓

Subnets

↓

AWS Resources

Example:

VPC

↓

Public Subnet

+

Private Subnet

---

## Regional vs Availability Zone

This distinction is important.

### VPC

A VPC is a:

Regional resource

### Subnet

A subnet is tied to:

One Availability Zone

### Memory Trick

VPC = Region

Subnet = Availability Zone

---

## Why Use Multiple Subnets?

Subnets allow you to separate resources based on their purpose.

Example:

VPC

↓

Public Subnet

→ Internet-facing resources

Private Subnet

→ Internal resources

This supports architectures where different resources require different levels of internet access.

---

## Public Subnet

Your course defines a public subnet as:

A subnet that is accessible from the internet.

A public subnet has a route to an:

Internet Gateway

Basic Idea:

Internet

↓

Internet Gateway

↓

Public Subnet

### Memory Trick

Public Subnet = Route to Internet Gateway

See:

[Internet Gateway](<Internet Gateway>)

---

## Private Subnet

Your course defines a private subnet as:

A subnet that is not directly accessible from the internet.

Typical resources may include:

- Internal application servers
- Databases
- Backend services

### Memory Trick

Private Subnet = No Direct Internet Access

---

## Private Subnet Internet Access

A resource in a private subnet may still need to initiate outbound internet connections.

Example:

Private EC2 instance needs to:

- Download software updates
- Access external services
- Retrieve packages

Your course says a:

NAT Gateway

or:

NAT Instance

can allow instances in private subnets to access the internet while remaining private.

Basic Flow:

Private Subnet

↓

NAT Gateway

↓

Internet Gateway

↓

Internet

See:

[NAT Gateway](<NAT Gateway>)

### Memory Trick

NAT Gateway = Private Subnet → Internet

---

## Route Tables

Route tables define:

- Access to the internet
- Communication between subnets
- Where network traffic should be sent

### Basic Idea

Traffic

↓

Route Table

↓

Destination

### Memory Trick

Route Table = Traffic Directions

---

## Public vs Private Subnet

| Public Subnet | Private Subnet |
|---|---|
| Internet accessible | Not directly internet accessible |
| Route to Internet Gateway | No direct route to Internet Gateway |
| Often hosts internet-facing resources | Often hosts internal resources |

---

## Basic Multi-Tier Architecture

A common design is:

Internet

↓

Internet Gateway

↓

Public Subnet

↓

Load Balancer

↓

Private Subnet

↓

Application Servers

↓

Private Database

This allows public-facing and internal resources to be separated.

---

## Subnets and Availability Zones

Because each subnet belongs to one Availability Zone, highly available architectures often use multiple subnets across multiple AZs.

Conceptually:

VPC

↓

Availability Zone A

→ Subnet A

Availability Zone B

→ Subnet B

This helps distribute resources across Availability Zones.

See:

[High Availability, Scalability, Elasticity](<High Availability, Scalability, Elasticity>)

---

## Subnet Security

Network ACLs operate at the:

Subnet level

This means a NACL can control inbound and outbound traffic for a subnet.

See:

[Security Groups vs NACLs](<Security Groups vs NACLs>)

### Memory Trick

NACL = Subnet Firewall

---

## Common Use Cases

- Separating public and private resources
- Multi-tier applications
- Network isolation
- Organizing resources by Availability Zone
- Controlling internet access

---

## Scenario Questions

A company wants to divide its VPC into smaller network sections.

→ Subnets

---

A subnet needs direct internet connectivity.

→ Public Subnet with a route to an Internet Gateway

---

A database should not be directly accessible from the internet.

→ Private Subnet

---

An EC2 instance in a private subnet needs outbound internet access while remaining private.

→ NAT Gateway

---

A company wants to deploy resources across multiple Availability Zones.

→ Use subnets in multiple Availability Zones

---

A company needs traffic filtering at the subnet level.

→ NACL

---

## Don't Confuse These

VPC = Entire private AWS network

Subnet = Section of VPC

Public Subnet = Route to Internet Gateway

Private Subnet = No direct internet route

Internet Gateway = VPC internet access

NAT Gateway = Private subnet outbound internet access

Route Table = Traffic directions

NACL = Subnet firewall

---

## Exam Keywords

Subnet

Availability Zone

Public Subnet

Private Subnet

Route Table

Internet Gateway

NAT Gateway

Network Isolation

---

## Quick Cheat Sheet

VPC = Regional

Subnet = One Availability Zone

Public Subnet = Internet Accessible

Private Subnet = Internal

Public Subnet → Internet Gateway

Private Subnet → NAT Gateway → Internet Gateway

Route Table = Traffic Directions

NACL = Subnet Security
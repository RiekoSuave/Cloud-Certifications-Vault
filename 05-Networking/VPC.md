See also: [Subnets](Subnets)

See also: [Internet Gateway](<Internet Gateway>)

See also: [NAT Gateway](<NAT Gateway>)

See also: [Security Groups vs NACLs](<Security Groups vs NACLs>)

See also: [VPC Flow Logs](<05-Networking/VPC Flow Logs.md>)

See also: [VPC Peering](<05-Networking/VPC Peering.md>)

See also: [VPC Endpoints](<05-Networking/VPC Endpoints.md>)

See also: [Site-to-Site VPN](<05-Networking/Site-to-Site VPN.md>)

See also: [Direct Connect](<05-Networking/Direct Connect.md>)

See also: [Transit Gateway](<05-Networking/Transit Gateway.md>)

## What Problem Does It Solve?

Provides a private, isolated network inside AWS where you can launch and control AWS resources.

A VPC allows you to control how resources communicate with:

- Other resources
- The internet
- Other VPCs
- On-premises networks

### Memory Trick

VPC = Your Private AWS Network

---

## Type

Networking Service

---

## What Is a VPC?

VPC stands for:

Virtual Private Cloud

A VPC is a logically isolated virtual network inside AWS.

You control important networking components such as:

- IP address ranges
- Subnets
- Route tables
- Internet connectivity
- Network security

---

## Basic VPC Architecture

Think of the VPC as the large network boundary.

Inside the VPC:

VPC

↓

Subnets

↓

AWS Resources

Example:

VPC

↓

Public Subnet → Internet-facing resources

Private Subnet → Internal resources

### Memory Trick

VPC = Network

Subnet = Section of the Network

---

## IP Address Range

When creating a VPC, you define an IP address range for the network.

This determines the range of private IP addresses available inside the VPC.

Your SAA material will expand this concept further when we cover:

CIDR

For now, remember:

VPC = Defined IP Address Range

---

## Subnets

A VPC can be divided into:

Subnets

Subnets allow resources to be separated into different portions of the network.

Common architecture:

VPC

↓

Public Subnet

+

Private Subnet

See:

[Subnets](Subnets)

---

## Public Subnet

A public subnet is designed for resources that need direct connectivity to the internet.

Example:

Internet

↓

Internet Gateway

↓

Public Subnet

↓

Web Server

### Memory Trick

Public Subnet = Can Reach Internet Directly

---

## Private Subnet

A private subnet is designed for resources that should not receive direct inbound traffic from the internet.

Examples may include:

- Application servers
- Databases
- Internal services

### Memory Trick

Private Subnet = Protected From Direct Internet Access

---

## Internet Gateway

An Internet Gateway provides connectivity between a VPC and the internet.

Basic Idea:

Internet

↕

Internet Gateway

↕

VPC

See:

[Internet Gateway](<Internet Gateway>)

### Memory Trick

Internet Gateway = Door to the Internet

---

## NAT Gateway

A NAT Gateway allows resources in a private subnet to initiate outbound connections while remaining private from unsolicited inbound internet connections.

Basic Idea:

Private Subnet

↓

NAT Gateway

↓

Internet Gateway

↓

Internet

### Exam Clue

Private EC2 instance needs outbound internet access?

→ NAT Gateway

See:

[NAT Gateway](<NAT Gateway>)

### Memory Trick

NAT Gateway = Private → Internet

---

## Route Tables

Route tables determine where network traffic is directed.

Think:

Traffic arrives

↓

Route Table checks destination

↓

Send traffic to correct destination

Routes can direct traffic toward resources such as:

- Internet Gateway
- NAT Gateway
- Other network connections

### Memory Trick

Route Table = Traffic Directions

---

## Security Groups

Security Groups control traffic to AWS resources such as EC2 instances.

Think:

Resource-Level Firewall

See:

[Security Groups vs NACLs](<Security Groups vs NACLs>)

### Memory Trick

Security Group = Resource Security

---

## Network ACLs

Network ACLs are commonly called:

NACLs

They provide network traffic controls at the subnet level.

Think:

Subnet-Level Firewall

See:

[Security Groups vs NACLs](<Security Groups vs NACLs>)

### Memory Trick

NACL = Subnet Security

---

## Security Group vs NACL

Basic distinction:

Security Group

→ Resource Level

NACL

→ Subnet Level

We'll cover the deeper differences in:

[Security Groups vs NACLs](<Security Groups vs NACLs>)

---

## VPC Flow Logs

VPC Flow Logs capture information about network traffic.

They can help with:

- Monitoring
- Troubleshooting
- Security analysis

See:

[VPC Flow Logs](<05-Networking/VPC Flow Logs.md>)

### Memory Trick

Flow Logs = Network Traffic Records

---

## VPC Peering

VPC Peering allows:

VPC

↔

VPC

This allows two VPCs to communicate privately.

See:

[VPC Peering](<05-Networking/VPC Peering.md>)

### Memory Trick

Peering = VPC to VPC

---

## VPC Endpoints

VPC Endpoints allow private connectivity between a VPC and supported AWS services without requiring traffic to travel through the public internet.

See:

[VPC Endpoints](<05-Networking/VPC Endpoints.md>)

### Memory Trick

VPC Endpoint = Private Path to AWS Services

---

## Connecting AWS to On-Premises

AWS provides multiple ways to connect a VPC with an on-premises network.

Two important options are:

Site-to-Site VPN

and:

Direct Connect

---

## Site-to-Site VPN

Provides an encrypted connection between an on-premises network and AWS.

The connection travels over the internet.

See:

[Site-to-Site VPN](<05-Networking/Site-to-Site VPN.md>)

### Memory Trick

VPN = Encrypted Connection Over Internet

---

## Direct Connect

Provides a dedicated private network connection between an organization's network and AWS.

See:

[Direct Connect](<05-Networking/Direct Connect.md>)

### Memory Trick

Direct Connect = Dedicated Connection to AWS

---

## Transit Gateway

Transit Gateway can act as a central networking hub for connecting multiple networks.

Think:

VPC A

↘

VPC B → Transit Gateway ← On-Premises

↗

VPC C

See:

[Transit Gateway](<05-Networking/Transit Gateway.md>)

### Memory Trick

Transit Gateway = Network Hub

---

## Basic Multi-Tier Architecture

A common AWS architecture can look like:

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

This allows internet-facing components and internal resources to be separated.

---

## Common Use Cases

- Network isolation
- Secure cloud infrastructure
- Multi-tier applications
- Public and private resources
- Hybrid networking
- Connecting multiple AWS networks

---

## Scenario Questions

A company needs an isolated virtual network inside AWS.

→ VPC

---

A public EC2 instance needs connectivity to the internet.

→ Internet Gateway

---

An EC2 instance in a private subnet needs outbound internet access without accepting unsolicited inbound internet connections.

→ NAT Gateway

---

A company wants to control traffic at the EC2/resource level.

→ Security Group

---

A company wants network controls at the subnet level.

→ NACL

---

Two VPCs need private communication.

→ VPC Peering

---

Resources inside a VPC need private connectivity to supported AWS services.

→ VPC Endpoint

---

A company needs an encrypted connection from its on-premises network to AWS over the internet.

→ Site-to-Site VPN

---

A company needs a dedicated private network connection to AWS.

→ Direct Connect

---

A company needs a central hub connecting multiple VPCs and networks.

→ Transit Gateway

---

## Don't Confuse These

VPC = Private AWS Network

Subnet = Section of VPC

Route Table = Traffic Directions

Internet Gateway = VPC ↔ Internet

NAT Gateway = Private Subnet → Internet

Security Group = Resource-Level Security

NACL = Subnet-Level Security

VPC Peering = VPC ↔ VPC

VPC Endpoint = Private Access to AWS Services

Site-to-Site VPN = Encrypted Connection Over Internet

Direct Connect = Dedicated Connection

Transit Gateway = Central Network Hub

---

## Exam Keywords

Virtual Private Cloud

Network Isolation

Subnets

Public Subnet

Private Subnet

Route Tables

Internet Gateway

NAT Gateway

Security Groups

NACLs

VPC Flow Logs

VPC Peering

VPC Endpoints

Site-to-Site VPN

Direct Connect

Transit Gateway

---

## Quick Cheat Sheet

VPC = Your Private AWS Network

Subnet = Section of VPC

Public Subnet = Internet Facing

Private Subnet = Internal

Route Table = Traffic Directions

Internet Gateway = Door to Internet

NAT Gateway = Private → Internet

Security Group = Resource Firewall

NACL = Subnet Firewall

Flow Logs = Traffic Records

Peering = VPC → VPC

Endpoint = Private Path to AWS

VPN = Encrypted Internet Connection

Direct Connect = Dedicated Connection

Transit Gateway = Network Hub
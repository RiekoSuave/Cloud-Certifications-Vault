## Core Networking

VPC = Private AWS Network

Subnet = Section of VPC

Route Table = Traffic Directions

Internet Gateway = VPC → Internet

NAT Gateway = Private Subnet → Internet

VPC Flow Logs = Network Traffic Records

---

## Network Security

Security Group = Resource-Level Firewall

NACL = Subnet-Level Firewall

Security Group = Stateful

NACL = Stateless

Security Group = Allow Rules

NACL = Allow + Deny Rules

### Memory Trick

Instance = Security Group

Subnet = NACL

---

## VPC Connectivity

VPC Peering = VPC ↔ VPC

VPC Endpoint = VPC → AWS Service Privately

Transit Gateway = Central Network Hub

### Memory Trick

Peering = Direct

Endpoint = Private AWS Service Access

Transit Gateway = Hub

---

## Hybrid Networking

Site-to-Site VPN = Encrypted Connection Over Public Internet

Direct Connect = Dedicated Private Connection

Customer Gateway (CGW) = On-Premises Side

Virtual Private Gateway (VGW) = AWS Side

### Memory Trick

VPN = Encrypted Internet

Direct Connect = Private Line

---

## Traffic & Scaling

ELB = Distribute Traffic

ASG = Adjust Capacity

ALB = HTTP / HTTPS

NLB = High-Performance Network Traffic

GWLB = Security Appliances

### Memory Trick

ASG = How Many Servers?

ELB = Where Does Traffic Go?

---

## Global Networking

Route 53 = DNS

CloudFront = Content Delivery Network

Global Accelerator = Global Application Performance

### Memory Trick

Route 53 = Find Destination

CloudFront = Content

Global Accelerator = Application

---

## Scaling & Availability

Vertical Scaling = Scale Up / Down

Horizontal Scaling = Scale Out / In

High Availability = Multi-AZ

Elasticity = Automatic Scaling

Agility = Quickly Provision Resources

---

## Fast Scenario Clues

Need a private AWS network?

→ VPC

Need to divide a VPC?

→ Subnet

Need public internet access?

→ Internet Gateway

Private subnet needs outbound internet?

→ NAT Gateway

Need network traffic records?

→ VPC Flow Logs

Need resource-level traffic control?

→ Security Group

Need subnet-level traffic control?

→ NACL

Need to block a specific IP at the subnet level?

→ NACL

Need direct VPC-to-VPC connectivity?

→ VPC Peering

Need private access to a supported AWS service?

→ VPC Endpoint

Need a central hub for many networks?

→ Transit Gateway

Need encrypted on-premises connectivity over the internet?

→ Site-to-Site VPN

Need dedicated private on-premises connectivity?

→ Direct Connect

Need DNS?

→ Route 53

Need cached content delivered globally?

→ CloudFront

Need improved global application performance?

→ Global Accelerator

Need traffic distributed across servers?

→ ELB

Need servers automatically added or removed?

→ Auto Scaling Group

---

## 30-Second Memory Review

VPC = Network

Subnet = Network Section

IGW = Public → Internet

NAT = Private → Internet

SG = Resource Security

NACL = Subnet Security

Flow Logs = Traffic Records

Peering = VPC → VPC

Endpoint = VPC → AWS Service

Transit Gateway = Hub

VPN = Encrypted Internet

Direct Connect = Private Line

Route 53 = DNS

CloudFront = Content

Global Accelerator = Application Performance

ELB = Spread Traffic

ASG = Adjust Capacity
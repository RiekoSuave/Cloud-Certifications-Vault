## Core Networking Services

| Service | Primary Purpose | Best For |
|---|---|---|
| VPC | Private AWS network | Network isolation |
| Subnet | Divide a VPC | Organizing public/private resources |
| Internet Gateway | VPC internet connectivity | Public internet access |
| NAT Gateway | Outbound internet for private resources | Private subnets |
| VPC Flow Logs | Record network traffic information | Monitoring and troubleshooting |
| VPC Peering | Direct private VPC-to-VPC connection | Connecting two VPCs |
| VPC Endpoint | Private access to supported AWS services | Avoiding public internet |
| Transit Gateway | Central network hub | Connecting many networks |

---

## Internet Gateway vs NAT Gateway

| Internet Gateway | NAT Gateway |
|---|---|
| VPC internet connectivity | Private subnet outbound internet access |
| Public subnet routes toward IGW | Private subnet routes toward NAT |
| VPC → Internet | Private → Internet |
| Associated with VPC | Used for private subnet connectivity |

### Memory Trick

Internet Gateway = Door to Internet

NAT Gateway = Private → Internet

---

## Security Groups vs NACLs

| Security Group | NACL |
|---|---|
| Resource / instance level | Subnet level |
| Stateful | Stateless |
| Allow rules | Allow and deny rules |
| Protect individual resources | Protect subnet traffic |

### Memory Trick

Security Group = Security Guard at the Door

NACL = Neighborhood Gate

Instance = Security Group

Subnet = NACL

See also: [Security Groups vs NACLs](<Security Groups vs NACLs>)

---

## VPC Peering vs Transit Gateway

| VPC Peering | Transit Gateway |
|---|---|
| Direct VPC connection | Central networking hub |
| VPC ↔ VPC | Many networks ↔ Hub |
| Point-to-point concept | Hub-and-spoke concept |
| Direct connectivity | Centralized connectivity |

### Memory Trick

VPC Peering = Direct

Transit Gateway = Hub

---

## Site-to-Site VPN vs Direct Connect

| Site-to-Site VPN | Direct Connect |
|---|---|
| Uses public internet | Uses private network |
| Automatically encrypted | Dedicated physical connection |
| VPN connection | Direct connection |
| On-Premises ↔ AWS | On-Premises ↔ AWS |

### Memory Trick

VPN = Encrypted Internet Connection

Direct Connect = Private Line to AWS

---

## VPC Peering vs VPC Endpoint

| VPC Peering | VPC Endpoint |
|---|---|
| Connects VPCs | Connects VPC to supported AWS service |
| VPC ↔ VPC | VPC → AWS Service |
| Private VPC communication | Private service access |

### Memory Trick

Peering = VPC → VPC

Endpoint = VPC → AWS Service

---

## Route 53 vs ELB

| Route 53 | ELB |
|---|---|
| DNS | Load balancing |
| Finds application destination | Distributes application traffic |
| DNS routing | Traffic distribution |
| Domain-related services | Application availability |

### Memory Trick

Route 53 = Find the Destination

ELB = Distribute the Traffic

---

## CloudFront vs Global Accelerator

| CloudFront | Global Accelerator |
|---|---|
| Content Delivery Network | Networking optimization |
| Caches content | Improves application performance |
| Uses Edge Locations | Uses AWS global network |
| Content delivery | Global application traffic |
| Think content | Think application |

### Memory Trick

CloudFront = Content

Global Accelerator = Application

---

## Route 53 vs CloudFront vs Global Accelerator

| Service | Think | Primary Purpose |
|---|---|---|
| Route 53 | DNS | Find the destination |
| CloudFront | CDN | Deliver cached content |
| Global Accelerator | Performance | Improve global application traffic |

### Memory Trick

Route 53 = Where?

CloudFront = Content

Global Accelerator = Faster Application

---

## ELB vs Auto Scaling

| ELB | Auto Scaling |
|---|---|
| Distributes traffic | Adjusts capacity |
| Routes requests across targets | Adds/removes EC2 instances |
| Traffic management | Capacity management |

Together:

ELB + ASG = High Availability + Scalability

### Memory Trick

ASG = How Many Servers?

ELB = Where Does Traffic Go?

---

## Public vs Private Subnet

| Public Subnet | Private Subnet |
|---|---|
| Route to Internet Gateway | No direct route to Internet Gateway |
| Often internet-facing resources | Often internal resources |
| Public-facing architecture | Protected backend architecture |

### Memory Trick

Public = IGW

Private = NAT → IGW for outbound internet

---

## Hybrid Networking Comparison

| Service | Connection |
|---|---|
| Site-to-Site VPN | On-Premises ↔ AWS over encrypted public internet |
| Direct Connect | On-Premises ↔ AWS over dedicated private connection |
| Transit Gateway | Central hub for multiple networks |
| VPC Peering | Direct VPC ↔ VPC |

---

## Scenario Quick Picks

Need a private AWS network?

→ VPC

Need to divide a VPC?

→ Subnet

Need public internet connectivity?

→ Internet Gateway

Private subnet needs outbound internet?

→ NAT Gateway

Need network traffic records?

→ VPC Flow Logs

Two VPCs need direct private communication?

→ VPC Peering

Need private access to supported AWS services?

→ VPC Endpoint

Need subnet-level traffic filtering?

→ NACL

Need resource-level traffic filtering?

→ Security Group

Need encrypted on-premises connectivity over the internet?

→ Site-to-Site VPN

Need dedicated private on-premises connectivity?

→ Direct Connect

Need to connect many networks through a central hub?

→ Transit Gateway

Need DNS?

→ Route 53

Need content delivered globally through caching?

→ CloudFront

Need improved global application performance?

→ Global Accelerator

Need traffic distributed across application targets?

→ ELB

Need EC2 capacity automatically adjusted?

→ Auto Scaling Group

---

## Fastest Memory Review

VPC = Private Network

Subnet = Section of VPC

IGW = Public → Internet

NAT Gateway = Private → Internet

Security Group = Resource Firewall

NACL = Subnet Firewall

Flow Logs = Observe Network Traffic

VPC Peering = VPC ↔ VPC

VPC Endpoint = VPC → AWS Service

Site-to-Site VPN = Encrypted Internet Connection

Direct Connect = Private Line

Transit Gateway = Network Hub

Route 53 = DNS

ELB = Distribute Traffic

CloudFront = Content

Global Accelerator = Application Performance

ASG = Adjust Capacity
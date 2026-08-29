
See also: [[02-Compute/EC2 Instance Types]]

See also: [[02-Compute/EC2 Purchasing Options]]

See also: [[02-Compute/EC2 User Data]]

## What Problem Does It Solve?

Provides scalable virtual machines in the cloud when you need full control over the operating system and server configuration.

---

## Type

Infrastructure as a Service (IaaS)

---

## What Is EC2?

EC2 stands for:

Elastic Compute Cloud

It allows you to rent virtual machines called instances.

EC2 is one of the core building blocks of AWS compute.

---

## EC2 Works With Other AWS Services

EC2 commonly works with:

- EBS → persistent virtual drives
- EFS → network file storage
- ELB → distributes traffic
- Auto Scaling Groups → automatically adjusts capacity
- Security Groups → firewall rules
- IAM Roles → permissions for EC2

---

## EC2 Configuration Options

When launching an EC2 instance, you choose:

### Operating System

Examples:

- Linux
- Windows
- macOS

---

### Compute

Choose:

- CPU
- Number of cores

---

### Memory

Choose:

- RAM

---

### Storage

Options include:

- EBS
- EFS
- EC2 Instance Store

---

### Networking

Configure:

- Network performance
- Public IP address

---

### Security

Use:

- Security Groups

Security Groups control inbound and outbound traffic.

---

### Startup Automation

Use:

- EC2 User Data

This allows commands to run automatically when an instance first starts.

See:

[[02-Compute/EC2 User Data]]

---

## EC2 Instance Components

Think of an EC2 instance as:

AMI

+

Instance Size

+

Storage

+

Security Groups

+

User Data

---

## AMI

AMI stands for:

Amazon Machine Image

An AMI provides the template used to launch an EC2 instance.

It can include:

- Operating system
- Software
- Configuration

---

## Security Groups

Security Groups act as firewalls for EC2 instances.

They control:

- Inbound traffic
- Outbound traffic
- Allowed ports
- Authorized IP ranges

### Important Defaults

- Inbound traffic is blocked by default
- Outbound traffic is allowed by default
- Security Groups contain allow rules

See also:

[[Security Groups vs NACLs]]

---

## Common Ports

| Port | Protocol | Purpose |
|---|---|---|
| 21 | FTP | File transfer |
| 22 | SSH | Linux remote access |
| 22 | SFTP | Secure file transfer |
| 80 | HTTP | Unsecured websites |
| 443 | HTTPS | Secured websites |
| 3389 | RDP | Windows remote access |

---

## SSH

SSH is commonly used to connect to Linux EC2 instances.

Default port:

22

### Memory Trick

SSH = Linux remote login

---

## EC2 Instance Role

An IAM Role can be attached to an EC2 instance.

This allows the instance to access AWS services without storing long-term credentials directly on the server.

---

## Shared Responsibility Model for EC2

### AWS Is Responsible For

- Physical infrastructure
- Global network security
- Isolation of physical hosts
- Replacing failed hardware
- Compliance validation

### Customer Is Responsible For

- Security Group rules
- Operating system patches
- Installed software
- IAM Roles and permissions
- Data security

### Memory Trick

AWS = Physical infrastructure

Customer = What runs inside EC2

---

## Common Use Cases

- Web servers
- Application servers
- Databases
- Custom software
- Development environments

---

## Compare Against

Lambda → Run code without managing servers

Lightsail → Simpler virtual server experience

ECS/EKS → Container workloads

Fargate → Containers without EC2 management

---

## Exam Keywords

Virtual machine

Instance

IaaS

AMI

Security Group

SSH

User Data

IAM Role

---

## Exam Scenarios

A company needs full control over the operating system.

→ Amazon EC2

---

A Linux administrator needs remote access to an EC2 instance.

→ SSH on port 22

---

An EC2 instance needs permission to access another AWS service.

→ Attach an IAM Role

---

A company wants startup commands to automatically run when an EC2 instance launches.

→ EC2 User Data

---

## Memory Trick

EC2 = Rent a computer in AWS

AMI = Server template

Security Group = EC2 firewall

SSH = Linux login

IAM Role = AWS permissions for EC2
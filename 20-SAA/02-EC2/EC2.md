## What Problem Does It Solve?

EC2 provides:

VIRTUAL SERVERS

in the AWS Cloud.

Instead of buying and maintaining physical servers, you can rent computing capacity from AWS.

Think:

PHYSICAL SERVER

↓

VIRTUAL SERVER IN AWS

↓

EC2

### Memory Trick

EC2 = RENT A VIRTUAL SERVER

---

## What Is EC2?

EC2 stands for:

ELASTIC COMPUTE CLOUD

EC2 is:

INFRASTRUCTURE AS A SERVICE

or:

IaaS

It is one of AWS's most popular services and is fundamental to understanding how cloud computing works.

### Memory Trick

EC2 = COMPUTE

---

## What Does EC2 Include?

Your course introduces EC2 as part of a larger compute architecture.

### Virtual Machines

[[EC2]]

→ Rent virtual machines

### Virtual Drives

[[EBS Volumes]]

→ Store data on virtual drives

### Load Balancing

[[Elastic Load Balancing]]

→ Distribute traffic across machines

### Scaling

[[Auto Scaling Groups]]

→ Automatically scale compute capacity

Think:

EC2

↓

COMPUTE

EBS

↓

STORAGE

ELB

↓

DISTRIBUTE TRAFFIC

ASG

↓

SCALE

---

## EC2 Configuration

When launching an EC2 instance, you can choose several configuration options.

---

## Operating System

Choose an operating system such as:

- Linux
- Windows
- macOS

Think:

EC2

↓

CHOOSE OS

---

## Compute

Choose:

CPU

and

NUMBER OF CORES

The amount of compute power depends on the workload.

We'll cover this further in:

[[02-Compute/EC2 Instance Types]]

---

## Memory

Choose the amount of:

RAM

Different workloads require different amounts of memory.

---

## Storage

EC2 supports different storage options.

### Network-Attached Storage

- [[EBS Volumes]]
- [[03-Storage/EFS]]

### Hardware-Attached Storage

- [[03-Storage/EC2 Instance Store]]

Think:

EC2 STORAGE

↓

NETWORK

or

LOCAL HARDWARE

---

## Networking

EC2 configuration includes:

NETWORK CARD

This affects things such as:

- Network performance
- Public IP addressing

We'll cover networking concepts later in:

[[Private vs Public IP]]

[[Elastic IP]]

[[Elastic Network Interfaces]]

---

## Firewall

EC2 uses:

[[EC2 Security Groups]]

to control network traffic.

Think:

EC2

↓

SECURITY GROUP

↓

FIREWALL RULES

### Memory Trick

Security Group = EC2 FIREWALL

---

## Bootstrapping

EC2 supports:

[[02-Compute/EC2 User Data]]

User Data allows you to run a script when an instance is launched.

Think:

EC2 STARTS

↓

USER DATA

↓

AUTOMATIC CONFIGURATION

Examples include:

- Installing updates
- Installing software
- Downloading files

We'll cover this separately in:

[[02-Compute/EC2 User Data]]

---

## EC2 Architecture Thinking

Think of an EC2 deployment like this:

USER

↓

LOAD BALANCER

↓

EC2 INSTANCES

↓

EBS STORAGE

And:

AUTO SCALING GROUP

↓

ADD / REMOVE EC2 INSTANCES

This connects four important AWS concepts:

EC2

= COMPUTE

EBS

= STORAGE

ELB

= LOAD BALANCING

ASG

= SCALING

---

## EC2 Is IaaS

EC2 is:

INFRASTRUCTURE AS A SERVICE

This means AWS provides the underlying cloud infrastructure while you configure the virtual machine for your workload.

### Memory Trick

EC2 = IaaS

---

## EC2 Sizing Decisions

When selecting an EC2 instance, think about:

OS

↓

CPU

↓

RAM

↓

STORAGE

↓

NETWORK

↓

SECURITY

Different workloads require different combinations.

This leads directly into:

[[02-Compute/EC2 Instance Types]]

---

## Scenario Recognition

Need a virtual machine in AWS?

→ EC2

---

Need to choose Linux or Windows for a cloud server?

→ EC2

---

Need more CPU or RAM for an application?

→ Choose an appropriate EC2 configuration / instance type

---

Need persistent virtual disk storage attached to EC2?

→ EBS

---

Need to distribute incoming traffic across multiple EC2 instances?

→ ELB

---

Need to automatically increase or decrease the number of EC2 instances?

→ Auto Scaling Group

---

Need firewall rules around an EC2 instance?

→ Security Group

---

Need commands to automatically run when launching an EC2 instance?

→ EC2 User Data

---

## Exam Traps

EC2 = COMPUTE

EC2 ≠ STORAGE

EBS = virtual drive

ELB = distribute load

ASG = scaling

Security Group = firewall

User Data = bootstrapping

EC2 = IaaS

---

## Quick Cheat Sheet

EC2

= ELASTIC COMPUTE CLOUD

EC2

= VIRTUAL MACHINES

EC2

= IaaS

CPU

= COMPUTE POWER

RAM

= MEMORY

EBS / EFS

= NETWORK-ATTACHED STORAGE

INSTANCE STORE

= HARDWARE STORAGE

SECURITY GROUP

= FIREWALL

USER DATA

= BOOTSTRAP

ELB

= DISTRIBUTE TRAFFIC

ASG

= SCALE

---

## Master Memory Trick

EC2

=

RENT COMPUTE

EBS

=

STORE DATA

ELB

=

DISTRIBUTE TRAFFIC

ASG

=

SCALE COMPUTE

---

## Related Notes

- [[02-Compute/EC2 User Data]]
- [[02-Compute/EC2 Instance Types]]
- [[02-Compute/EC2 Purchasing Options]]
- [[EC2 Security Groups]]
- [[EC2 IAM Roles]]
- [[Private vs Public IP]]
- [[Elastic IP]]
- [[EC2 Placement Groups]]
- [[Elastic Network Interfaces]]
- [[EBS Volumes]]
- [[03-Storage/EFS]]
- [[03-Storage/EC2 Instance Store]]
- [[Elastic Load Balancing]]
- [[Auto Scaling Groups]]
- [[EC2 Comparison]]
- [[SAA EC2 Cheat Sheet]]
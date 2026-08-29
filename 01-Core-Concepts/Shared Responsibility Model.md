## Overview

The AWS Shared Responsibility Model defines:

**Which security responsibilities belong to AWS**

and:

**Which security responsibilities belong to the customer**

The fundamental rule is:

> **AWS = Security OF the Cloud**
>
> **Customer = Security IN the Cloud**

The exact division of responsibility changes depending on:

**Which AWS service you use**

> [!tip] Memory Trick
> **AWS protects the CLOUD**
>
> **You protect what you put IN the CLOUD**

---

## Security OF the Cloud

AWS is responsible for protecting:

**The infrastructure that runs AWS services**

This includes:

- Hardware
- Software
- Physical facilities
- Networking infrastructure
- AWS global infrastructure

### Simple Model

AWS  
↓  
Physical Infrastructure  
↓  
Hardware  
↓  
Networking  
↓  
AWS Services

### Killer Exam Clue

> **Who is responsible for the physical AWS data centers?**
>
> → **AWS**

---

## Security IN the Cloud

The customer is responsible for:

**How AWS resources and data are configured and used**

Depending on the service, customer responsibilities can include:

- IAM
- Data
- Security configuration
- Network configuration
- Encryption choices
- Application configuration
- Guest operating system management

### Killer Exam Clue

> **Who is responsible for configuring access to customer resources?**
>
> → **Customer**

---

## The Responsibility Changes by Service

This is one of the most important CCP concepts.

The amount of responsibility handled by AWS depends on:

**How managed the AWS service is**

For a service where the customer controls more infrastructure:

**The customer has more responsibility**

For a highly managed service:

**AWS handles more of the underlying infrastructure**

### Memory Trick

> **MORE CUSTOMER CONTROL**
> → MORE CUSTOMER RESPONSIBILITY
>
> **MORE AWS MANAGEMENT**
> → MORE AWS RESPONSIBILITY

---

## EC2 Shared Responsibility

With [[EC2]], the customer manages more of:

**The computing environment**

AWS manages:

- Physical infrastructure
- Physical servers
- AWS networking infrastructure
- Underlying cloud infrastructure

The customer is responsible for areas such as:

- Guest operating system
- Security patches
- Operating system updates
- Firewall/network configuration
- IAM
- Application data encryption

---

## EC2 Guest Operating System

With EC2:

**The customer manages the guest OS**

This includes:

- Security patches
- Updates

### Killer Exam Clue

> **Who patches the operating system running inside an EC2 instance?**
>
> → **Customer**

### Memory Trick

> **EC2 = Your Virtual Server**
>
> AWS owns the hardware.
>
> **You manage the guest OS.**

---

## EC2 Network Configuration

For EC2, the customer is responsible for:

**Firewall and network configuration**

This includes properly configuring security controls associated with:

**The workload**

### Killer Exam Clue

> **Who configures the firewall rules for an EC2 workload?**
>
> → **Customer**

---

## EC2 IAM

The customer is responsible for:

**IAM configuration**

This means the customer decides:

- Who receives access
- Which permissions are granted
- Which roles are used

See:

[[IAM]]

---

## Customer Data

The customer remains responsible for:

**Customer data**

This includes making appropriate decisions about:

- Access
- Encryption
- Configuration

### Killer Exam Principle

> **Putting data in AWS does not transfer responsibility for the data itself to AWS**

---

## Application Data Encryption

The course identifies:

**Encrypting application data**

as a customer responsibility.

The customer determines:

**How their application data should be protected**

### Killer Exam Clue

> **Who decides whether application data should be encrypted?**
>
> → **Customer**

---

## RDS Shared Responsibility

[[RDS]] is a:

**Managed database service**

Because RDS is more managed than running a database yourself on EC2:

**AWS handles more responsibilities**

---

## AWS Responsibilities for RDS

For RDS, AWS handles responsibilities such as:

- Managing the underlying EC2 infrastructure
- Disabling SSH access to the underlying instance
- Automated database patching
- Automated operating system patching
- Auditing the underlying instance and disks
- Ensuring the underlying infrastructure functions

### Killer Exam Clue

> **Who performs operating system patching for RDS?**
>
> → **AWS**

---

## Customer Responsibilities for RDS

The customer still controls important database settings.

Examples include:

- Security Group inbound rules
- Ports and allowed IP addresses
- In-database users
- Database permissions
- Whether the database has public access
- Database parameter configuration
- SSL connection requirements
- Database encryption settings

### Killer Exam Principle

> **Managed does NOT mean AWS configures your database security for you**

---

## EC2 Database vs RDS

Suppose you run a database:

**On EC2**

You manage:

- Guest OS
- OS patching
- Database software
- Database configuration
- Security configuration

With:

**RDS**

AWS handles more of:

**The underlying database infrastructure and patching**

while you still manage:

**Your database access and configuration**

### Memory Trick

> **DATABASE ON EC2**
> → YOU MANAGE MORE
>
> **RDS**
> → AWS MANAGES MORE

---

## S3 Shared Responsibility

[[S3]] is another:

**Highly managed AWS service**

AWS handles much of:

**The underlying storage infrastructure**

while the customer remains responsible for:

**How their buckets and data are configured**

---

## AWS Responsibilities for S3

The course identifies AWS responsibilities such as:

- Providing the underlying storage capability
- Providing encryption capability
- Separating customer data
- Protecting customer data from unauthorized AWS employee access

AWS manages:

**The storage infrastructure itself**

---

## Customer Responsibilities for S3

The customer is responsible for areas such as:

- Bucket configuration
- Bucket policies
- Public access settings
- IAM users
- IAM roles
- Enabling/configuring encryption

### Killer Exam Clue

> **Who is responsible for accidentally making an S3 bucket public?**
>
> → **Customer**

---

## S3 Configuration Responsibilities

For S3, customer-controlled configuration includes:

- Versioning
- Bucket Policies
- Replication setup
- Logging and monitoring
- Storage class selection
- Data encryption choices

### Exam Principle

> **AWS operates S3**
>
> **You configure how your S3 resources are used**

---

## EC2 Storage Shared Responsibility

For services such as:

- EBS
- EFS

AWS is responsible for underlying infrastructure tasks such as:

- Replication of storage infrastructure
- Replacing faulty hardware
- Protecting customer data from unauthorized AWS employee access

The customer is responsible for decisions such as:

- Backup and snapshot procedures
- Data encryption
- Data stored on the drives
- Understanding the risks of EC2 Instance Store

### Memory Trick

> **AWS protects the storage infrastructure**
>
> **You protect and manage your data strategy**

---

## Shared Controls

Not every responsibility belongs entirely to:

**AWS**

or entirely to:

**The customer**

The course identifies several:

**Shared Controls**

including:

- Patch Management
- Configuration Management
- Awareness & Training

These responsibilities may involve:

**Both AWS and the customer**

depending on:

**Which layer is being managed**

---

## Patch Management

Patch responsibility depends on:

**The service**

Example:

EC2 Guest OS  
→ Customer

RDS Underlying OS  
→ AWS

### Killer Exam Rule

> **Before answering a patching question, identify the service first**

---

## Configuration Management

AWS configures and manages:

**Its infrastructure**

The customer configures:

**Their AWS resources and applications**

### Example

AWS  
→ Maintains underlying S3 infrastructure

Customer  
→ Configures S3 bucket policies

---

## Awareness and Training

Security awareness is also described as:

**A shared control**

AWS maintains security awareness for:

**AWS personnel and operations**

Customers remain responsible for appropriate security awareness within:

**Their own organization**

---

## IAM Shared Responsibility

For [[IAM]], AWS manages the underlying:

- Infrastructure
- Global network security
- Configuration and vulnerability analysis
- Compliance validation

The customer manages:

- Users
- Groups
- Roles
- Policies
- Monitoring
- MFA
- Access permissions
- Access patterns

---

## Customer IAM Responsibilities

The course specifically emphasizes:

- Manage users, groups, roles, and policies
- Enable MFA
- Rotate keys
- Apply appropriate permissions
- Analyze access patterns
- Review permissions

### Killer Exam Clue

> **Who determines which IAM user can access an S3 bucket?**
>
> → **Customer**

---

## Root Account Security

AWS provides:

**The AWS account system**

but the customer is responsible for properly securing:

**Their account access**

This includes following IAM security practices such as:

**MFA**

See:

[[IAM]]

---

## Responsibility Depends on Abstraction

Think of AWS services on a spectrum.

### More Customer Management

EC2  
↓  
Customer manages more

### More AWS Management

RDS  
↓  
AWS manages more underlying infrastructure

S3  
↓  
AWS manages even more underlying infrastructure

### Core Principle

> **As AWS manages more of the technology stack, the customer's infrastructure-management responsibility decreases**

But the customer still remains responsible for:

**Their data, access, and configuration**

---

## Shared Responsibility Comparison

| Area | AWS | Customer |
|---|---|---|
| Physical Data Centers | ✅ | ❌ |
| Physical Hardware | ✅ | ❌ |
| AWS Global Infrastructure | ✅ | ❌ |
| Customer Data | ❌ | ✅ |
| IAM Configuration | ❌ | ✅ |
| EC2 Guest OS Patching | ❌ | ✅ |
| RDS Underlying OS Patching | ✅ | ❌ |
| S3 Bucket Policy | ❌ | ✅ |
| S3 Public Access Configuration | ❌ | ✅ |
| RDS Security Group Configuration | ❌ | ✅ |
| Application Data Encryption Decision | ❌ | ✅ |

---

## Service Responsibility Comparison

| Service | AWS Manages | Customer Manages |
|---|---|---|
| EC2 | Physical infrastructure | Guest OS + application configuration |
| RDS | Infrastructure + OS/DB patching | Database access + configuration |
| S3 | Storage infrastructure | Bucket + data configuration |

### Memory Trick

> **EC2**
> → YOU MANAGE MORE
>
> **RDS**
> → AWS MANAGES MORE
>
> **S3**
> → AWS MANAGES MOST OF THE INFRASTRUCTURE

---

## Responsibility Decision Process

When the exam asks:

> **Who is responsible?**

First ask:

### Step 1

Is the responsibility related to:

**AWS physical infrastructure?**

YES  
→ AWS

---

### Step 2

Is it related to:

**Customer data or access?**

YES  
→ Customer

---

### Step 3

Is it related to:

**The operating system?**

Ask:

Which service?

EC2 guest OS  
→ Customer

Managed RDS underlying OS  
→ AWS

---

### Step 4

Is it related to:

**Resource configuration?**

Usually:

→ Customer

Examples:

- Security Groups
- IAM policies
- S3 Bucket Policies
- Public access settings

---

## Scenario 1 — Physical Server Failure

An AWS physical server fails.

Who replaces:

**The hardware?**

→ **AWS**

---

## Scenario 2 — EC2 Security Patch

A Linux vulnerability requires:

**A guest OS patch**

on an EC2 instance.

Who patches it?

→ **Customer**

---

## Scenario 3 — RDS OS Patch

The underlying operating system supporting RDS requires:

**Patching**

Who handles it?

→ **AWS**

---

## Scenario 4 — Public S3 Bucket

A customer configures an S3 bucket to allow:

**Public access**

Who is responsible for:

**That configuration?**

→ **Customer**

---

## Scenario 5 — IAM Permissions

An IAM user receives:

**Too many permissions**

Who is responsible?

→ **Customer**

---

## Scenario 6 — AWS Data Center Security

Who protects:

**The physical AWS facility?**

→ **AWS**

---

## Scenario 7 — RDS Security Group

The RDS Security Group allows:

**Too much inbound access**

Who is responsible?

→ **Customer**

---

## Scenario 8 — Database User Permissions

A database user receives:

**Excessive permissions**

inside RDS.

Who is responsible?

→ **Customer**

---

## CCP Exam Traps

### Trap 1 — AWS Is Responsible for Everything Because It Is the Cloud

❌ Wrong

AWS manages:

**Security OF the Cloud**

Customer manages:

**Security IN the Cloud**

---

### Trap 2 — Customer Must Maintain AWS Physical Hardware

❌ Wrong

AWS manages:

**The underlying physical infrastructure**

---

### Trap 3 — AWS Patches the Guest OS on EC2

❌ Wrong

For EC2:

**Customer manages the guest OS**

---

### Trap 4 — Customer Patches the Underlying RDS Operating System

❌ Wrong

For managed RDS:

**AWS handles underlying OS patching**

---

### Trap 5 — AWS Is Responsible for S3 Bucket Policies

❌ Wrong

The customer configures:

**Bucket Policies**

---

### Trap 6 — Managed Service Means Customer Has No Security Responsibility

❌ Wrong

Even with managed services, customers still manage important areas such as:

- Data
- Access
- IAM
- Configuration

---

### Trap 7 — Shared Responsibility Is Identical for Every AWS Service

❌ Wrong

The responsibility split changes according to:

**The service being used**

---

## Killer Exam Clues

> **Physical data center**
>
> → AWS

> **Physical hardware**
>
> → AWS

> **AWS networking infrastructure**
>
> → AWS

> **Customer data**
>
> → CUSTOMER

> **IAM permissions**
>
> → CUSTOMER

> **EC2 guest OS patches**
>
> → CUSTOMER

> **RDS underlying OS patches**
>
> → AWS

> **S3 Bucket Policy**
>
> → CUSTOMER

> **S3 public access**
>
> → CUSTOMER

> **RDS Security Group**
>
> → CUSTOMER

> **Database users**
>
> → CUSTOMER

---

## Quick Cheat Sheet

| Exam Phrase | Answer |
|---|---|
| Security OF the Cloud | AWS |
| Security IN the Cloud | Customer |
| Physical Facilities | AWS |
| Physical Servers | AWS |
| AWS Networking Infrastructure | AWS |
| EC2 Guest OS | Customer |
| EC2 OS Patching | Customer |
| IAM | Customer |
| Customer Data | Customer |
| RDS Underlying Infrastructure | AWS |
| RDS OS Patching | AWS |
| RDS DB Patching | AWS |
| RDS Security Group | Customer |
| RDS Database Users | Customer |
| S3 Infrastructure | AWS |
| S3 Bucket Configuration | Customer |
| S3 Bucket Policy | Customer |
| S3 Public Access | Customer |
| S3 Encryption Configuration | Customer |

---

## Final Rapid-Fire

> **AWS**
> → OF THE CLOUD
>
> **CUSTOMER**
> → IN THE CLOUD
>
> **HARDWARE**
> → AWS
>
> **DATA CENTER**
> → AWS
>
> **CUSTOMER DATA**
> → CUSTOMER
>
> **IAM**
> → CUSTOMER
>
> **EC2 OS**
> → CUSTOMER
>
> **RDS OS**
> → AWS
>
> **S3 BUCKET POLICY**
> → CUSTOMER
>
> **RDS SECURITY GROUP**
> → CUSTOMER
>
> **MORE MANAGED SERVICE**
> → AWS MANAGES MORE

---

## Master Memory Trick

> [!tip] Shared Responsibility Master Memory Trick
> Imagine AWS is:
>
> **YOUR LANDLORD**
>
> AWS owns and protects:
>
> **THE BUILDING**
>
> **THE FOUNDATION**
>
> **THE ELECTRICAL SYSTEM**
>
> **THE PHYSICAL SECURITY**
>
> That's:
>
> **SECURITY OF THE CLOUD**
>
> You rent an apartment inside.
>
> You decide:
>
> **WHO GETS A KEY**
>
> **WHAT YOU STORE INSIDE**
>
> **HOW YOU CONFIGURE YOUR SPACE**
>
> That's:
>
> **SECURITY IN THE CLOUD**

Then ask:

> **HOW MUCH OF THE APARTMENT DOES AWS MANAGE FOR ME?**

With EC2:

> **You manage more**

With RDS:

> **AWS manages more**

With S3:

> **AWS manages most of the underlying infrastructure**

But one rule remains:

> **YOUR DATA + YOUR ACCESS + YOUR CONFIGURATION**
>
> → **YOUR RESPONSIBILITY**

The ultimate CCP question:

> **"Is this responsibility part of AWS's underlying cloud infrastructure, or is it something the customer configures and controls?"**

Underlying infrastructure:

→ **AWS**

Customer-controlled data/access/configuration:

→ **Customer**

---

## Related Notes

- [[What is Cloud Computing]]
- [[Global Infrastructure]]
- [[IAM]]
- [[EC2]]
- [[RDS]]
- [[S3]]
- [[Cloud Adoption Framework]]
- [[Well-Architected Framework]]
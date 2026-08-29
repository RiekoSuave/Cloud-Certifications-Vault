## What Problem Does It Solve?

Defines which security and operational responsibilities belong to AWS and which belong to the customer.

AWS and the customer share responsibility for securing workloads running in AWS.

The exact responsibilities can change depending on the AWS service being used.

### Memory Trick

AWS = Security OF the Cloud

Customer = Security IN the Cloud

---

## What Is the Shared Responsibility Model?

AWS is responsible for protecting the infrastructure that runs AWS services.

The customer is responsible for how they configure and use AWS services.

Think:

AWS

↓

Cloud Infrastructure

+

Customer

↓

Resources, Data & Configuration

=

Shared Responsibility

---

## AWS Responsibility

Your course repeatedly associates AWS with responsibilities such as:

- AWS infrastructure
- Global network security
- Physical infrastructure
- Replacing faulty hardware
- Physical host isolation
- Configuration and vulnerability analysis
- Compliance validation

### Memory Trick

AWS = Infrastructure

---

## Customer Responsibility

Your responsibilities depend on the AWS service being used.

Your course gives examples involving:

- Security configuration
- IAM permissions
- Data security
- Encryption
- Backups
- Monitoring
- Operating system patching on EC2
- Security Groups

### Memory Trick

Customer = Configuration + Data + Access

---

## Shared Responsibility Changes by Service

One of the most important concepts is:

Your responsibility depends on the AWS service.

Your course demonstrates this with:

- EC2
- S3
- EC2 Storage
- IAM
- Managed Databases

You manage more when using services where you control more of the underlying environment.

---

## Shared Responsibility for EC2

EC2 provides a clear example of the Shared Responsibility Model.

### AWS Responsibilities

Your course identifies AWS as responsible for:

- Infrastructure
- Global network security
- Isolation on physical hosts
- Replacing faulty hardware
- Compliance validation

### Customer Responsibilities

You are responsible for:

- Security Group rules
- Operating system patches and updates
- Software and utilities installed on EC2
- IAM Roles assigned to EC2
- IAM user access management
- Data security on the instance

### Memory Trick

EC2 = You Manage the Operating System

---

## EC2 Example

Suppose an EC2 instance needs an operating system security update.

Who is responsible?

→ Customer

Suppose the physical server running the EC2 instance fails.

Who is responsible?

→ AWS

### Memory Trick

Physical Hardware = AWS

Guest OS = Customer

---

## Shared Responsibility for S3

S3 has a different responsibility model because AWS manages more of the underlying infrastructure.

### AWS Responsibilities

Your course identifies AWS as responsible for:

- Infrastructure
- Global security
- Durability
- Availability
- Configuration and vulnerability analysis
- Compliance validation

### Customer Responsibilities

You are responsible for:

- S3 Versioning
- S3 Bucket Policies
- S3 Replication setup
- Logging and monitoring
- S3 Storage Classes
- Data encryption at rest and in transit

### Memory Trick

AWS Runs S3

You Configure Your S3 Data

---

## S3 Example

A company accidentally makes an S3 bucket publicly accessible because of its bucket policy.

Who is responsible?

→ Customer

Why?

The customer manages:

S3 Bucket Policies

---

## Shared Responsibility for EC2 Storage

Your course also applies the model to:

- EBS
- EFS
- EC2 Instance Store

### AWS Responsibilities

AWS handles:

- Infrastructure
- Data replication for EBS and EFS
- Replacing faulty hardware
- Ensuring AWS employees cannot access customer data

### Customer Responsibilities

You handle:

- Backup and snapshot procedures
- Data encryption
- Data stored on the drives
- Understanding the risks of EC2 Instance Store

### Memory Trick

AWS = Storage Infrastructure

Customer = Data + Backups + Encryption

---

## Shared Responsibility for IAM

IAM also follows the Shared Responsibility Model.

### AWS Responsibilities

Your course identifies AWS as responsible for:

- Infrastructure
- Global network security
- Configuration and vulnerability analysis
- Compliance validation

### Customer Responsibilities

You are responsible for:

- Users
- Groups
- Roles
- Policies
- IAM monitoring
- Enabling MFA
- Rotating keys
- Applying appropriate permissions
- Analyzing access patterns
- Reviewing permissions

### Memory Trick

AWS Provides IAM

You Configure IAM

---

## IAM Example

An IAM user is accidentally given AdministratorAccess when they only need S3 access.

Who is responsible?

→ Customer

This involves:

IAM Permissions

and

Least Privilege

---

## Shared Responsibility for Managed Databases

Your course also demonstrates how responsibility changes when using managed database services.

AWS can handle tasks such as:

- Operating system patching
- Automated backup and restore
- Operations
- Upgrades
- High availability capabilities
- Monitoring and alerting capabilities

This reduces the amount of infrastructure management required from the customer.

---

## Database on EC2 vs Managed Database

Your course makes an important distinction.

### Database Running on EC2

You must handle more yourself, including:

- Resiliency
- Backups
- Patching
- High availability
- Fault tolerance
- Scaling

### Managed AWS Database

AWS handles more of the underlying operational work.

### Memory Trick

More Managed Service

=

Less Infrastructure Management for You

---

## Common Scenario Questions

An EC2 operating system needs security patches.

→ Customer

---

Physical AWS hardware fails.

→ AWS

---

An S3 bucket policy accidentally exposes data publicly.

→ Customer

---

An IAM user has excessive permissions.

→ Customer

---

An EBS backup strategy was never configured.

→ Customer

---

AWS needs to replace faulty physical hardware.

→ AWS

---

A managed AWS database requires operating system patching.

→ AWS

---

## Don't Confuse These

AWS Responsibility = Infrastructure

Customer Responsibility = Configuration & Data

EC2 OS Patching = Customer

Physical Hardware = AWS

IAM Permissions = Customer

S3 Bucket Policies = Customer

Managed Database OS Patching = AWS

---

## Exam Keywords

Shared Responsibility Model

AWS Responsibility

Customer Responsibility

Security

Infrastructure

Data

Configuration

Operating System

Patching

IAM

Encryption

Security Groups

Compliance

---

## Quick Cheat Sheet

AWS = Security OF the Cloud

Customer = Security IN the Cloud

Physical Infrastructure = AWS

Physical Hardware = AWS

EC2 Guest OS = Customer

EC2 Security Groups = Customer

Customer Data = Customer

IAM Permissions = Customer

S3 Bucket Policies = Customer

Backups / Snapshots = Customer

Managed Database OS Patching = AWS

More Managed Service = AWS Handles More
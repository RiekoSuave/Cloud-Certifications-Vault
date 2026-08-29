See also: [Systems Manager](<Systems Manager>)

## What Problem Does It Solve?

Automates infrastructure deployment using code.

AWS CloudFormation solves manual infrastructure setup and configuration problems by allowing you to define AWS resources in templates.

Instead of manually creating resources one at a time:

Define Infrastructure

↓

CloudFormation Template

↓

AWS Creates Resources Automatically

### Memory Trick

CloudFormation = Build Infrastructure with Code

---

## Type

Infrastructure as Code (IaC)

---

## What Is CloudFormation?

CloudFormation is a declarative way to define AWS infrastructure.

You describe:

WHAT infrastructure you want

and CloudFormation handles:

HOW to create it.

### Memory Trick

You Describe It

CloudFormation Builds It

---

## Infrastructure as Code (IaC)

Infrastructure as Code means infrastructure is defined using code instead of manually creating resources.

Benefits include:

- Repeatable deployments
- Standardized infrastructure
- Automation
- Easier infrastructure changes
- Better control

Your course emphasizes:

No resources need to be manually created.

Infrastructure changes can be reviewed through code.

### Memory Trick

IaC = Infrastructure Defined as Code

---

## CloudFormation Templates

A CloudFormation template describes the AWS resources you want.

Your course gives an example containing:

- Security Group
- Two EC2 instances
- S3 bucket
- Elastic Load Balancer

Think:

CloudFormation Template

↓

Security Group

EC2 Instances

S3 Bucket

ELB

↓

Complete AWS Infrastructure

---

## Automatic Resource Creation

CloudFormation creates resources:

In the Right Order

and with:

The Exact Configuration You Specify

You don't need to manually determine the order in which resources should be created.

### Memory Trick

CloudFormation Handles the Order

---

## Declarative Programming

CloudFormation uses a:

Declarative Approach

You specify the desired infrastructure.

CloudFormation handles:

- Ordering
- Orchestration
- Resource creation

### Memory Trick

Declarative = Say WHAT You Want

---

## Repeatable Infrastructure

CloudFormation makes it possible to reproduce infrastructure.

Your course's deployment summary emphasizes that CloudFormation can be repeated across:

- Regions
- Accounts

This is useful for creating standardized environments.

Example:

Development Environment

↓

Same Template

↓

Test Environment

↓

Same Template

↓

Production Environment

### Memory Trick

One Template = Repeatable Infrastructure

---

## Infrastructure Changes

Because infrastructure is represented as code:

Changes can be reviewed through code.

This provides greater control than manually changing infrastructure.

Think:

Infrastructure Change

↓

Modify Code

↓

Review

↓

Deploy

---

## Cost Benefits

Your course identifies several cost-related benefits.

Resources within a CloudFormation deployment can be associated with identifiers that help determine the cost of the infrastructure.

You can also:

Estimate resource costs using the CloudFormation template.

Your course gives a development-environment example:

Delete infrastructure at 5 PM

↓

Re-create it at 8 AM

↓

Avoid paying while it is not needed

### Memory Trick

Repeatable Infrastructure Can Help Control Cost

---

## Productivity Benefits

CloudFormation allows you to:

- Destroy infrastructure
- Re-create infrastructure
- Automate deployments
- Reuse templates

Your course also emphasizes:

Don't Reinvent the Wheel

Existing templates and AWS documentation can be reused.

---

## AWS Resource Support

CloudFormation supports:

Almost All AWS Resources

Your course notes that most AWS resources can be defined using CloudFormation.

For unsupported resources, the course mentions:

Custom Resources

### Memory Trick

CloudFormation = Infrastructure Across AWS

---

## CloudFormation vs Systems Manager

These services both involve automation but solve different problems.

### CloudFormation

Deploys:

Infrastructure

### Systems Manager

Manages:

Existing Systems and Operations

| CloudFormation | Systems Manager |
| --- | --- |
| Infrastructure deployment | Operational management |
| Infrastructure as Code | Systems operations |
| Build resources | Manage resources |
| Templates | Patching / commands / configuration |

### Memory Trick

CloudFormation = BUILD

Systems Manager = MANAGE

See:

[Systems Manager](<Systems Manager>)

---

## Common Use Cases

- Infrastructure automation
- Infrastructure as Code
- Repeatable deployments
- Standardized environments
- Creating multiple AWS resources together
- Reproducing infrastructure across accounts or Regions

---

## Scenario Questions

A company wants to define its AWS infrastructure using code.

→ AWS CloudFormation

---

A company wants repeatable infrastructure deployments.

→ AWS CloudFormation

---

A company wants to automatically create EC2 instances, Security Groups, S3 buckets, and an ELB from a defined template.

→ AWS CloudFormation

---

A company wants infrastructure changes to be reviewed through code instead of making resources manually.

→ AWS CloudFormation

---

A company wants to reproduce the same AWS infrastructure across Regions or accounts.

→ AWS CloudFormation

---

A company wants to patch and run commands across a fleet of existing servers.

→ AWS Systems Manager

NOT CloudFormation

---

## Don't Confuse These

CloudFormation = Infrastructure Deployment

Systems Manager = Operational Management

CloudFormation = Infrastructure as Code

CloudFormation = Templates

CloudFormation = Build Resources

Systems Manager = Manage Existing Systems

---

## Exam Keywords

AWS CloudFormation

Infrastructure as Code

IaC

Templates

Declarative

Automation

Repeatable Deployment

Infrastructure

Standardized Environment

---

## Quick Cheat Sheet

CloudFormation = Infrastructure as Code

CloudFormation = Templates

CloudFormation = Build Infrastructure

Declarative = Say WHAT You Want

CloudFormation Handles Resource Order

One Template = Repeatable Infrastructure

Repeat Across Regions & Accounts

CloudFormation = BUILD

Systems Manager = MANAGE
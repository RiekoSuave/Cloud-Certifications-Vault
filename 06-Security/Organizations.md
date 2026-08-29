See also: [IAM](IAM)

See also: [Control Tower](<Control Tower>)

## What Problem Does It Solve?

Allows an organization to centrally manage multiple AWS accounts.

AWS Organizations helps solve the problem of managing many separate AWS accounts by providing centralized:

- Account management
- Governance
- Billing
- Policy controls

### Memory Trick

Organizations = Manage Many AWS Accounts

---

## Type

Multi-Account Management

---

## What Is AWS Organizations?

AWS Organizations is a:

Global Service

It allows you to centrally manage multiple AWS accounts.

Think:

AWS Organization

↓

Multiple AWS Accounts

↓

Centralized Management

### Memory Trick

Organizations = AWS Account Manager

---

## Management Account

An AWS Organization has a primary account responsible for managing the organization.

Your course refers to this as the:

Master Account

This account manages the AWS Organization and its member accounts.

### Memory Trick

Management Account = Controls the Organization

---

## Consolidated Billing

One major benefit of AWS Organizations is:

Consolidated Billing

Multiple AWS accounts can use:

One Payment Method

Instead of managing separate payments for every account.

Basic Idea:

Account A

Account B

Account C

↓

AWS Organizations

↓

Single Consolidated Bill

### Memory Trick

Organizations = One Bill for Many Accounts

---

## Aggregated Usage

AWS Organizations can combine usage across accounts.

This can provide pricing benefits from:

Aggregated Usage

Your course gives examples involving:

- EC2
- S3

Combining usage across accounts can help qualify for volume pricing benefits.

### Memory Trick

Combine Usage = Potential Savings

---

## Reserved Instance Pooling

Your course also identifies:

Pooling of Reserved EC2 Instances

as a cost benefit.

This can help optimize savings across accounts within the organization.

---

## Automated Account Creation

AWS Organizations provides an:

API

that can be used to automate the creation of AWS accounts.

### Memory Trick

Organizations = Automate Account Creation

---

## Organizational Units (OUs)

Organizational Units allow accounts to be grouped together.

Think:

AWS Organization

↓

OU

↓

AWS Accounts

Accounts can be organized based on different requirements.

Examples from your course include:

- Department
- Cost Center
- Development / Test / Production
- Regulatory Requirements

### Memory Trick

OU = Folder for AWS Accounts

---

## Multi-Account Strategies

Your course gives several reasons for using multiple AWS accounts.

Examples include:

- Separate departments
- Separate cost centers
- Separate Dev / Test / Prod environments
- Regulatory restrictions
- Better resource isolation
- Separate service limits
- Dedicated logging accounts

### Memory Trick

Multiple Accounts = Better Isolation & Organization

---

## Centralized Logging

Your course gives examples of centralized logging across AWS accounts.

### CloudTrail

Enable CloudTrail across accounts and send logs to a:

Central S3 Account

### CloudWatch Logs

CloudWatch Logs can be sent to a:

Central Logging Account

Basic Idea:

Multiple AWS Accounts

↓

Logs

↓

Central Logging Account

---

## Service Control Policies (SCPs)

One of the most important AWS Organizations concepts is:

Service Control Policies

SCPs can be used to restrict privileges across AWS accounts.

They can be applied at:

- Organizational Unit level
- Account level

### Memory Trick

SCP = Permission Guardrail for AWS Accounts

---

## SCP Allow / Deny Strategy

Your course describes SCPs using:

Whitelist

or

Blacklist

strategies for IAM actions.

SCPs can be used to restrict which AWS services or actions are available within accounts.

Example:

Prevent accounts from using:

Amazon EMR

---

## SCPs and Users / Roles

Your course emphasizes that an SCP applied to an account affects:

- IAM Users
- IAM Roles
- Root User

within that account.

### Important

SCPs do NOT apply to the organization's management account.

Your course refers to this as the:

Master Account

---

## Service-Linked Roles

Your course notes that SCPs do not affect:

Service-Linked Roles

Service-linked roles allow AWS services to integrate with AWS Organizations.

### Memory Trick

Service-Linked Roles = Exception to SCP Restrictions

---

## SCP Explicit Allow

Your course emphasizes:

An SCP must have an explicit Allow.

It does not automatically allow permissions by itself.

### Important Concept

SCPs are used to control the permissions available to accounts in the organization.

---

## SCP Use Cases

Your course gives examples such as:

### Restrict AWS Services

Example:

Prevent an account from using Amazon EMR.

### Compliance

SCPs can help enforce compliance requirements.

Example:

Explicitly disabling services to help enforce PCI requirements.

---

## Organizations vs IAM

### AWS Organizations

Manages:

AWS Accounts

### IAM

Manages:

Users, Groups, Roles, and Permissions

| Organizations | IAM |
|---|---|
| Multiple AWS accounts | Identities and permissions |
| OUs | Users / Groups / Roles |
| SCPs | IAM Policies |
| Consolidated billing | Access control |

### Memory Trick

Organizations = ACCOUNTS

IAM = USERS & PERMISSIONS

See:

[IAM](IAM)

---

## Organizations vs Control Tower

### AWS Organizations

Provides:

- Multi-account management
- Organizational Units
- Consolidated billing
- SCPs

### AWS Control Tower

Provides:

- Automated multi-account setup
- Governance
- Guardrails
- Compliance monitoring

Control Tower operates on top of:

AWS Organizations

### Memory Trick

Organizations = Organize Accounts

Control Tower = Govern Accounts

See:

[Control Tower](<Control Tower>)

---

## Common Use Cases

- Managing multiple AWS accounts
- Consolidated billing
- Enterprise account management
- Separating Dev / Test / Prod
- Centralized logging
- Applying organization-wide restrictions
- Compliance governance

---

## Scenario Questions

A company wants to centrally manage many AWS accounts.

→ AWS Organizations

---

A company wants one payment method across multiple AWS accounts.

→ AWS Organizations + Consolidated Billing

---

A company wants to group AWS accounts by department.

→ Organizational Units (OUs)

---

A company wants to restrict which AWS services accounts can use.

→ Service Control Policies (SCPs)

---

A company wants to organize separate Development, Test, and Production accounts.

→ AWS Organizations

---

A company wants automated multi-account governance with guardrails.

→ AWS Control Tower

---

A company wants to control permissions for individual IAM users.

→ IAM

NOT AWS Organizations

---

## Don't Confuse These

Organizations = Manage AWS Accounts

OU = Group AWS Accounts

SCP = Restrict Account Permissions

IAM = Users / Roles / Permissions

Control Tower = Automated Multi-Account Governance

Consolidated Billing = One Bill for Multiple Accounts

---

## Exam Keywords

AWS Organizations

Multiple Accounts

Consolidated Billing

Organizational Units

OU

Service Control Policies

SCP

Aggregated Usage

Multi-Account

Centralized Management

Account Isolation

---

## Quick Cheat Sheet

Organizations = Manage Many Accounts

Organizations = Global Service

Consolidated Billing = One Bill

OU = Group Accounts

SCP = Permission Guardrail

SCP → OU or Account

SCP → Users / Roles / Root in Member Accounts

SCP ≠ Management Account

IAM = Users & Permissions

Organizations = Accounts

Control Tower = Automated Governance
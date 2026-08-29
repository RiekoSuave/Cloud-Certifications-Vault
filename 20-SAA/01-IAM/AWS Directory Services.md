## What Problem Does It Solve?

AWS Directory Services help organizations use:

MICROSOFT ACTIVE DIRECTORY

with AWS.

This is especially useful when a company already has:

WINDOWS USERS

+

GROUPS

+

ON-PREMISES ACTIVE DIRECTORY

and needs to integrate them with AWS.

### Memory Trick

Directory Service = ACTIVE DIRECTORY ON / WITH AWS

---

## First: What Is Microsoft Active Directory?

Microsoft Active Directory (AD) is commonly found on:

WINDOWS SERVER

using:

AD DOMAIN SERVICES

It stores objects such as:

- User Accounts
- Computers
- Printers
- File Shares
- Security Groups

It provides:

CENTRALIZED SECURITY MANAGEMENT

Think:

Users

+

Computers

+

Permissions

↓

ACTIVE DIRECTORY

---

## Active Directory Structure

Active Directory objects are organized into:

TREES

A group of trees is called a:

FOREST

### Memory Trick

Objects → Trees → Forest

---

## AWS Directory Services

Your course focuses on three options:

1. AWS Managed Microsoft AD
2. AD Connector
3. Simple AD

These three are important to distinguish on the SAA exam.

---

## AWS Managed Microsoft AD

AWS Managed Microsoft AD allows you to:

CREATE YOUR OWN AD IN AWS

You manage your users:

LOCALLY IN AWS

It also:

- Supports MFA
- Can establish trust connections with an on-premises AD

Think:

On-Premises AD

↓

TRUST

↓

AWS Managed Microsoft AD

### Memory Trick

Managed Microsoft AD = REAL AD IN AWS

---

## AWS Managed Microsoft AD + On-Premises

If your organization already has:

ON-PREMISES ACTIVE DIRECTORY

AWS Managed Microsoft AD can establish a:

TRUST RELATIONSHIP

with it.

Think:

On-Prem AD

↔

TRUST

↔

AWS Managed Microsoft AD

### Exam Keyword

TRUST

→ AWS Managed Microsoft AD

---

## AD Connector

AD Connector works differently.

It is a:

DIRECTORY GATEWAY / PROXY

that redirects authentication requests to your:

ON-PREMISES ACTIVE DIRECTORY

Think:

AWS

↓

AD CONNECTOR

↓

ON-PREMISES AD

### Memory Trick

AD Connector = PROXY

---

## Where Are AD Connector Users Managed?

This is important.

With AD Connector:

USERS STAY MANAGED ON-PREMISES

You are NOT creating another directory containing those users in AWS.

Think:

AWS Authentication Request

↓

AD Connector

↓

Existing On-Prem AD

### Memory Trick

Connector = CONNECT TO WHAT YOU ALREADY HAVE

---

## AD Connector Features

AD Connector:

- Acts as a proxy
- Redirects to on-premises AD
- Supports MFA
- Keeps users managed in the on-premises AD

### Exam Keyword

PROXY

→ AD Connector

---

## Simple AD

Simple AD provides an:

AD-COMPATIBLE MANAGED DIRECTORY

on AWS.

But there is an important limitation:

Simple AD

CANNOT BE JOINED

with your on-premises Active Directory.

### Memory Trick

Simple AD = SIMPLE AWS DIRECTORY

---

## Simple AD Limitation

Think:

Simple AD

↓

AWS

❌

On-Premises AD Integration

### Exam Trap

Need to join/integrate with existing on-premises AD?

Do NOT choose:

Simple AD

---

## The Big Comparison

| Service | Main Idea | On-Prem AD Relationship |
| --- | --- | --- |
| AWS Managed Microsoft AD | Microsoft AD in AWS | TRUST |
| AD Connector | Proxy to existing AD | PROXY |
| Simple AD | AD-compatible AWS directory | NO JOIN |

---

## Fastest Memory Trick

AWS MANAGED MICROSOFT AD

=

TRUST

AD CONNECTOR

=

PROXY

SIMPLE AD

=

NO JOIN

---

## AWS Managed Microsoft AD vs AD Connector

This is an important distinction.

### AWS Managed Microsoft AD

You have:

AD IN AWS

and can establish:

TRUST

with your on-premises AD.

---

### AD Connector

AWS does NOT become where your users are managed.

Instead:

AWS

↓

PROXY

↓

ON-PREMISES AD

### Memory Trick

Managed AD = DIRECTORY IN AWS

Connector = SEND REQUEST BACK HOME

---

## IAM Identity Center Integration

AWS Directory Services also connects with:

[[IAM Identity Center]]

Your course shows two important setups.

---

## Identity Center + AWS Managed Microsoft AD

IAM Identity Center can connect to:

AWS MANAGED MICROSOFT AD

The integration is:

OUT OF THE BOX

Think:

[[IAM Identity Center]]

↓

AWS Managed Microsoft AD

↓

Users & Groups

---

## Identity Center + Self-Managed Directory

For a:

SELF-MANAGED DIRECTORY

your course gives two approaches:

### Option 1

AWS Managed Microsoft AD

+

TWO-WAY TRUST RELATIONSHIP

### Option 2

AD Connector

↓

PROXY

↓

Self-Managed AD

---

## Scenario Recognition

A company wants to create and manage Microsoft Active Directory directly in AWS.

→ AWS Managed Microsoft AD

---

A company wants its AWS directory to establish a trust relationship with its existing on-premises Active Directory.

→ AWS Managed Microsoft AD

---

A company wants AWS authentication requests redirected to its existing on-premises Active Directory.

→ AD Connector

---

A company wants users to continue being managed entirely in its on-premises Active Directory.

→ AD Connector

---

A company wants an inexpensive/simple AD-compatible managed directory in AWS and does NOT need to join it with on-premises AD.

→ Simple AD

---

A company wants IAM Identity Center connected directly to AWS Managed Microsoft AD.

→ Supported

---

A company wants IAM Identity Center to use a self-managed directory.

Think:

Two-Way Trust

or

AD Connector

---

## Exam Traps

AWS Managed Microsoft AD ≠ AD Connector

Managed Microsoft AD = AD IN AWS

AD Connector = PROXY

Simple AD = AD-COMPATIBLE

Simple AD cannot join with on-premises AD

AD Connector users remain managed on-premises

AWS Managed Microsoft AD can establish trust with on-premises AD

Both AWS Managed Microsoft AD and AD Connector support MFA

---

## Quick Cheat Sheet

Microsoft AD

→ USERS + COMPUTERS + GROUPS

→ CENTRALIZED SECURITY

AWS Managed Microsoft AD

→ AD IN AWS

→ TRUST

→ MFA

AD Connector

→ PROXY

→ USERS STAY ON-PREM

→ MFA

Simple AD

→ AD-COMPATIBLE

→ NO ON-PREM JOIN

IAM Identity Center

→ Can integrate with Directory Services

---

## Master Memory Trick

Need REAL MICROSOFT AD IN AWS?

→ AWS MANAGED MICROSOFT AD

Need AWS to talk to EXISTING ON-PREM AD?

→ AD CONNECTOR

Need SIMPLE AD-compatible directory with no on-prem join?

→ SIMPLE AD

### Three Words

Managed AD = TRUST

Connector = PROXY

Simple AD = NO JOIN

---

## Related Notes

- [[IAM Identity Center]]
- [[IAM Users and Groups]]
- [[IAM Roles]]
- [[IAM Policies]]
- [[IAM Comparison]]
- [[SAA IAM Cheat Sheet]]
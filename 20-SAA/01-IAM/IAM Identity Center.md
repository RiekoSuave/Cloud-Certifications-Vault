## What Problem Does It Solve?

IAM Identity Center provides:

SINGLE SIGN-ON (SSO)

for accessing multiple AWS accounts and applications.

Think:

ONE LOGIN

↓

MULTIPLE AWS ACCOUNTS

+

APPLICATIONS

### Memory Trick

IAM Identity Center = ONE LOGIN

---

## What Is IAM Identity Center?

IAM Identity Center is the successor to:

AWS SINGLE SIGN-ON

It provides one login for access to:

- AWS accounts in AWS Organizations
- Business cloud applications
- SAML 2.0-enabled applications
- EC2 Windows instances

### Memory Trick

Identity Center = CENTRALIZED ACCESS

---

## AWS Organizations

IAM Identity Center can manage access across:

MULTIPLE AWS ACCOUNTS

inside:

AWS ORGANIZATIONS

Think:

User

↓

IAM Identity Center

↓

AWS Organization

↓

Account A

Account B

Account C

### Memory Trick

Many AWS Accounts + One Login

→ IAM Identity Center

---

## Identity Providers

IAM Identity Center supports different identity sources.

Your course shows:

### Built-In Identity Store

IAM Identity Center can maintain its own:

USERS

and

GROUPS

Think:

IAM Identity Center

↓

Built-In Identity Store

---

## Third-Party Identity Providers

Your course gives examples including:

- Active Directory (AD)
- OneLogin
- Okta

Think:

Existing Company Identities

↓

IAM Identity Center

↓

AWS Access

### Memory Trick

Existing Identity Provider + AWS

→ IAM Identity Center

---

## Permission Sets

One of the most important SAA concepts is:

PERMISSION SETS

A Permission Set is a collection of:

ONE OR MORE IAM POLICIES

assigned to:

USERS

or

GROUPS

to define AWS access.

Think:

User / Group

↓

Permission Set

↓

IAM Policies

↓

AWS Access

### Memory Trick

Permission Set = PACKAGE OF IAM POLICIES

---

## Multi-Account Permissions

IAM Identity Center provides:

MULTI-ACCOUNT PERMISSIONS

This allows you to manage access across AWS accounts in:

AWS ORGANIZATIONS

Think:

Identity Center

↓

Permission Set

↓

Dev Account

Prod Account

Other Accounts

### Memory Trick

Multi-Account Access = IDENTITY CENTER

---

## Permission Set Example

Your course shows a:

DB ADMINS

Permission Set.

Think:

Database Admins

↓

DB Admin Permission Set

↓

AWS Organization

↓

Dev Account

+

Prod Account

↓

Database Access

### Exam Recognition

Same group needs defined permissions across multiple AWS accounts?

→ IAM Identity Center + Permission Sets

---

## Application Assignments

IAM Identity Center can also provide SSO access to:

SAML 2.0 BUSINESS APPLICATIONS

Your course gives examples such as:

- Salesforce
- Box
- Microsoft 365

Think:

ONE LOGIN

↓

AWS

+

BUSINESS APPLICATIONS

---

## SAML 2.0 Applications

For SAML 2.0 applications, your course mentions providing required:

- URLs
- Certificates
- Metadata

### Memory Trick

SAML App + SSO

→ IAM Identity Center

---

## Attribute-Based Access Control

IAM Identity Center also supports:

ATTRIBUTE-BASED ACCESS CONTROL

ABAC

Permissions can be based on user attributes stored in the:

IAM IDENTITY CENTER IDENTITY STORE

Your course gives examples such as:

- Cost center
- Title
- Locale

### Memory Trick

ABAC = ACCESS BY ATTRIBUTE

---

## Why ABAC Is Useful

Your course gives this use case:

DEFINE PERMISSIONS ONCE

↓

CHANGE USER ATTRIBUTE

↓

AWS ACCESS CHANGES

Think:

User Attribute

↓

Determines Access

Instead of constantly creating different permission configurations.

---

## IAM Identity Center vs IAM Users

Don't confuse:

[[IAM Users and Groups]]

with:

IAM Identity Center

### IAM Users

Individual identities inside IAM.

### IAM Identity Center

Centralized access across:

MULTIPLE AWS ACCOUNTS

and

APPLICATIONS

### Memory Trick

IAM User = ONE AWS IDENTITY

Identity Center = CENTRALIZED SSO

---

## Identity Center vs IAM Role

Don't confuse:

[[IAM Roles]]

with:

IAM Identity Center

### IAM Role

Provides permissions for a particular role/job/service.

### IAM Identity Center

Centralizes:

IDENTITIES

+

SSO

+

MULTI-ACCOUNT ACCESS

+

PERMISSION SETS

---

## Scenario Recognition

A company wants employees to use one login across multiple AWS accounts.

→ IAM Identity Center

---

A company uses AWS Organizations and wants centralized user access across its accounts.

→ IAM Identity Center

---

A company wants to assign a collection of IAM policies to users and groups for AWS access.

→ Permission Sets

---

A company already uses Active Directory and wants centralized AWS access.

→ IAM Identity Center

---

A company wants employees to access Salesforce, Microsoft 365, and AWS through SSO.

→ IAM Identity Center

---

A company wants permissions based on attributes such as department, cost center, or job title.

→ ABAC

---

## Exam Traps

IAM Identity Center = successor to AWS SSO

Identity Center = ONE LOGIN

AWS Organizations = MULTI-ACCOUNT ACCESS

Permission Set = COLLECTION OF IAM POLICIES

Permission Sets can be assigned to users and groups

SAML 2.0 applications = supported

Active Directory = supported identity provider

ABAC = ATTRIBUTE-BASED ACCESS

Do NOT confuse IAM Identity Center with ordinary IAM Users.

---

## Quick Cheat Sheet

IAM Identity Center = SSO

Successor to = AWS SINGLE SIGN-ON

AWS Organizations = MULTI-ACCOUNT ACCESS

Permission Set = IAM POLICY PACKAGE

Built-In Identity Store = USERS + GROUPS

Active Directory / OneLogin / Okta = IDENTITY PROVIDERS

SAML 2.0 = APPLICATION SSO

ABAC = ACCESS BY ATTRIBUTE

---

## Master Memory Trick

ONE LOGIN

↓

IAM IDENTITY CENTER

↓

AWS ORGANIZATION ACCOUNTS

+

BUSINESS APPLICATIONS

Permission Sets

=

WHAT ACCESS THEY GET

---

## Related Notes

- [[IAM Users and Groups]]
- [[IAM Policies]]
- [[IAM Roles]]
- [[IAM Policy Evaluation Logic]]
- [[AWS Organizations SCP]]
- [[IAM Comparison]]
- [[SAA IAM Cheat Sheet]]
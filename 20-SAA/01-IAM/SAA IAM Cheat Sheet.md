## IAM Core

IAM = Identity and Access Management

GLOBAL SERVICE

Root Account:

→ Created by default

→ DON'T use/share for everyday work

### Core Pattern

USER

→ PERSON

GROUP

→ USERS

POLICY

→ PERMISSIONS

ROLE

→ ASSUMED PERMISSIONS

### Memory Trick

WHO?

→ User

WHO TOGETHER?

→ Group

WHAT CAN THEY DO?

→ Policy

WHAT PERMISSIONS ARE ASSUMED?

→ Role

---

## Users & Groups

Users = people within your organization

Groups = collections of users

Important:

- Groups contain USERS only
- Groups cannot contain other groups
- User does NOT have to belong to a group
- User CAN belong to multiple groups

### Exam Trap

GROUP INSIDE GROUP?

→ NO

---

## Least Privilege

Give users:

ONLY THE PERMISSIONS THEY NEED

### Memory Trick

Least Privilege = NOTHING EXTRA

---

## IAM Policies

IAM Policies are:

JSON DOCUMENTS

that define:

PERMISSIONS

Important policy elements:

- Version
- Statement
- Sid
- Effect
- Principal
- Action
- Resource
- Condition

### Fast Recognition

Effect

→ Allow / Deny

Action

→ WHAT?

Resource

→ WHICH RESOURCE?

Principal

→ WHO?

Condition

→ ONLY IF?

---

## IAM Password Policy

Can enforce:

- Minimum password length
- Uppercase letters
- Lowercase letters
- Numbers
- Non-alphanumeric characters
- Password expiration
- Prevent password reuse
- Allow users to change passwords

### Memory Trick

Password Policy = PASSWORD RULES

---

## MFA

MFA =

PASSWORD YOU KNOW

+

DEVICE YOU OWN

Main benefit:

Stolen password alone does NOT compromise the account.

Protect:

ROOT

+

IAM USERS

### Memory Trick

MFA = PASSWORD + DEVICE

---

## AWS Access Methods

| Method | Think | Authentication |
| --- | --- | --- |
| Console | CLICK | Password + MFA |
| CLI | TYPE | Access Keys |
| SDK | CODE | Access Keys |

Access Key ID

≈ USERNAME

Secret Access Key

≈ PASSWORD

### Important

ACCESS KEYS ARE SECRET

DO NOT SHARE

---

## IAM Roles

AWS service needs permissions?

→ IAM ROLE

Common examples:

EC2

→ EC2 Instance Role

Lambda

→ Lambda Function Role

CloudFormation

→ CloudFormation Role

### Memory Trick

SERVICE NEEDS PERMISSION?

→ ROLE

---

## IAM Security Tools

### Credentials Report

ACCOUNT LEVEL

Shows:

USERS

+

CREDENTIAL STATUS

### Access Advisor

USER LEVEL

Shows:

PERMISSIONS

+

LAST ACCESSED

Can help revise policies.

### Memory Trick

REPORT = ACCOUNT

ADVISOR = USER

---

## IAM Best Practices

Root

→ ACCOUNT SETUP ONLY

One physical user

→ One AWS user

Users

→ Groups

Permissions

→ Policies

Strong authentication

→ Password Policy + MFA

AWS services

→ Roles

CLI / SDK

→ Access Keys

Audit

→ Credentials Report + Access Advisor

Never share:

IAM USERS

or

ACCESS KEYS

---

# ADVANCED IAM

## IAM Conditions

`aws:SourceIp`

→ IP ADDRESS

`aws:RequestedRegion`

→ REGION

`ec2:ResourceTag`

→ TAG

`aws:MultiFactorAuthPresent`

→ MFA

### Memory Trick

SourceIp = WHERE FROM?

RequestedRegion = WHICH REGION?

ResourceTag = WHICH TAG?

MultiFactorAuthPresent = MFA?

---

## IAM for S3

Remember the distinction:

`s3:ListBucket`

→ BUCKET LEVEL

Example resource:

`arn:aws:s3:::test`

Object actions such as:

`s3:GetObject`

`s3:PutObject`

`s3:DeleteObject`

→ OBJECT LEVEL

Example resource:

`arn:aws:s3:::test/*`

### Memory Trick

ListBucket = BUCKET

Get/Put/DeleteObject = OBJECTS

---

## aws:PrincipalOrgID

Can be used in:

RESOURCE POLICIES

to restrict access to accounts that belong to an:

AWS ORGANIZATION

### Memory Trick

PrincipalOrgID = ONLY MY ORGANIZATION

---

## IAM Role vs Resource-Based Policy

Both can help with:

CROSS-ACCOUNT ACCESS

### IAM Role

ASSUME ROLE

↓

Give up original permissions

↓

Use Role permissions

### Resource-Based Policy

Principal:

KEEPS ORIGINAL PERMISSIONS

### Memory Trick

ROLE = SWITCH

RESOURCE POLICY = KEEP

---

## Resource-Based Policy Examples

Course examples include:

- S3 Buckets
- SNS Topics
- SQS Queues

Policy is attached to the:

RESOURCE

---

## EventBridge Security

Your course gives this target pattern:

### Resource-Based Policy

- Lambda
- SNS
- SQS
- S3
- API Gateway

### IAM Role

- EC2 Auto Scaling
- Systems Manager Run Command
- ECS Task

---

## IAM Permission Boundaries

Permission Boundary

=

MAXIMUM PERMISSIONS

### Supported

Users ✅

Roles ✅

Groups ❌

### Memory Trick

IAM Policy

= WHAT YOU GET

Permission Boundary

= MOST YOU CAN GET

Use cases:

- Delegate IAM responsibilities
- Prevent privilege escalation
- Allow developers to manage permissions without becoming admins
- Restrict a specific user

---

## Permission Boundary vs SCP

Permission Boundary

→ USER / ROLE LIMIT

SCP

→ ORGANIZATION / ACCOUNT GUARDRAIL

### Memory Trick

BOUNDARY = IDENTITY LIMIT

SCP = ORGANIZATION LIMIT

---

## IAM Policy Evaluation

Start with:

DENY

Need applicable permissions to perform an action.

### Most Important Rule

EXPLICIT DENY WINS

Think:

ALLOW

+

EXPLICIT DENY

=

DENY

### Fast Exam Flow

REQUEST

↓

DENY?

→ YES = DENY

↓

NO

↓

ALLOWED?

→ NO = DENY

↓

YES

↓

Check applicable permission limits

↓

FINAL EFFECTIVE PERMISSION

---

# IAM IDENTITY CENTER

## IAM Identity Center

Successor to:

AWS SINGLE SIGN-ON

Think:

ONE LOGIN

for:

- AWS Organization accounts
- Business applications
- SAML 2.0 applications
- EC2 Windows instances

### Memory Trick

IAM Identity Center = SSO

---

## Identity Providers

Can use:

BUILT-IN IDENTITY STORE

or third-party identity providers.

Course examples:

- Active Directory
- OneLogin
- Okta

---

## Permission Sets

Permission Set

=

COLLECTION OF ONE OR MORE IAM POLICIES

assigned to:

USERS

or

GROUPS

to define AWS access.

### Memory Trick

Permission Set = POLICY PACKAGE

---

## Multi-Account Permissions

Need centralized access across:

MULTIPLE AWS ACCOUNTS

inside AWS Organizations?

→ IAM IDENTITY CENTER

---

## ABAC

ABAC

=

ATTRIBUTE-BASED ACCESS CONTROL

Permissions based on user attributes.

Course examples:

- Cost center
- Title
- Locale

### Memory Trick

ABAC = ACCESS BY ATTRIBUTE

---

# AWS DIRECTORY SERVICES

## Microsoft Active Directory

Centralized management of objects such as:

- Users
- Computers
- Printers
- File Shares
- Security Groups

Objects

↓

TREES

↓

FOREST

---

## Directory Services Comparison

| Service | Think |
| --- | --- |
| AWS Managed Microsoft AD | TRUST |
| AD Connector | PROXY |
| Simple AD | NO JOIN |

---

## AWS Managed Microsoft AD

Microsoft AD:

IN AWS

Supports:

MFA

Can establish:

TRUST

with on-premises AD.

### Memory Trick

Managed AD = TRUST

---

## AD Connector

Directory:

PROXY

Authentication requests go to:

ON-PREMISES AD

Users remain managed:

ON-PREMISES

### Memory Trick

Connector = PROXY

---

## Simple AD

AD-compatible managed directory:

IN AWS

Cannot be joined with:

ON-PREMISES AD

### Memory Trick

Simple AD = NO JOIN

---

# HIGH-VALUE SAA SCENARIOS

Need an EC2 instance to access AWS resources?

→ IAM ROLE

Need common permissions for multiple users?

→ IAM GROUP + POLICY

Need maximum permissions for a user or role?

→ PERMISSION BOUNDARY

Need to prevent developer privilege escalation?

→ PERMISSION BOUNDARY

Need cross-account access while retaining original permissions?

→ RESOURCE-BASED POLICY

Need account-wide credential status?

→ CREDENTIALS REPORT

Need user's permissions + last accessed services?

→ ACCESS ADVISOR

Need API calls restricted by IP?

→ `aws:SourceIp`

Need API calls restricted by Region?

→ `aws:RequestedRegion`

Need access controlled using EC2 tags?

→ `ec2:ResourceTag`

Need MFA required for an action?

→ `aws:MultiFactorAuthPresent`

Need one login across multiple AWS accounts?

→ IAM IDENTITY CENTER

Need collection of IAM policies for Identity Center access?

→ PERMISSION SET

Need Active Directory running in AWS with on-premises trust?

→ AWS MANAGED MICROSOFT AD

Need AWS to proxy authentication to existing on-premises AD?

→ AD CONNECTOR

Need simple AD-compatible AWS directory with no on-premises join?

→ SIMPLE AD

---

# EXAM TRAPS

Groups contain USERS only

Groups cannot contain groups

User can belong to multiple groups

IAM is GLOBAL

Least Privilege = minimum necessary permissions

Console = Password + MFA

CLI / SDK = Access Keys

Access Keys = SECRET

Service needs AWS permissions = ROLE

Credentials Report = ACCOUNT

Access Advisor = USER

Policy = GRANT

Permission Boundary = MAXIMUM

Permission Boundary applies to Users + Roles, NOT Groups

Role = SWITCH permissions

Resource-Based Policy = KEEP original permissions

Explicit Deny = WINS

Identity Center = SSO

Permission Set = POLICY PACKAGE

Managed Microsoft AD = TRUST

AD Connector = PROXY

Simple AD = NO JOIN

---

# 30-SECOND IAM REVIEW

USER = PERSON

GROUP = USERS

POLICY = PERMISSIONS

ROLE = ASSUMED PERMISSIONS

LEAST PRIVILEGE = NOTHING EXTRA

MFA = PASSWORD + DEVICE

CONSOLE = CLICK

CLI = TYPE

SDK = CODE

ACCESS KEYS = SECRET

CREDENTIALS REPORT = ACCOUNT

ACCESS ADVISOR = USER

CONDITION = ONLY IF

ROLE = SWITCH

RESOURCE POLICY = KEEP

POLICY = GRANT

BOUNDARY = MAX

SCP = ORGANIZATION GUARDRAIL

EXPLICIT DENY = WINS

IDENTITY CENTER = ONE LOGIN

PERMISSION SET = POLICY PACKAGE

ABAC = ACCESS BY ATTRIBUTE

MANAGED AD = TRUST

AD CONNECTOR = PROXY

SIMPLE AD = NO JOIN

---

## Related Notes

- [[IAM Users and Groups]]
- [[IAM Policies]]
- [[IAM Policy Structure]]
- [[IAM Password Policy]]
- [[MFA]]
- [[AWS Access Methods]]
- [[IAM Roles]]
- [[IAM Security Tools]]
- [[IAM Best Practices]]
- [[IAM Conditions]]
- [[IAM Roles vs Resource-Based Policies]]
- [[IAM Permission Boundaries]]
- [[IAM Policy Evaluation Logic]]
- [[IAM Identity Center]]
- [[AWS Directory Services]]
- [[IAM Comparison]]
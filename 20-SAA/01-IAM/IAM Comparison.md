## IAM Core Identity Comparison

| Concept | Best For | Memory Trick |
| --- | --- | --- |
| IAM User | Individual person | USER = PERSON |
| IAM Group | Organizing users | GROUP = USERS |
| IAM Role | Temporary/assumed permissions | ROLE = PERMISSIONS FOR A JOB |
| IAM Policy | Defines permissions | POLICY = WHAT YOU CAN DO |

### Key Rules

IAM is a:

GLOBAL SERVICE

Groups contain:

USERS ONLY

Users:

- Do not have to belong to a group
- Can belong to multiple groups

Policies:

DEFINE PERMISSIONS

Use:

LEAST PRIVILEGE

→ Don't give more permissions than necessary

---

## Users vs Groups vs Roles

### IAM User

Think:

PERSON

↓

IAM USER

---

### IAM Group

Think:

MULTIPLE USERS

↓

COMMON PERMISSIONS

Groups contain users.

Groups do NOT contain other groups.

---

### IAM Role

Think:

PERMISSIONS ASSUMED FOR A PURPOSE

Common course examples:

- EC2 Instance Role
- Lambda Function Role
- CloudFormation Role

### Memory Trick

USER = PERSON

GROUP = COLLECTION OF USERS

ROLE = ASSUMED PERMISSIONS

---

## IAM Policy vs Permission Boundary

| Concept | Purpose | Memory Trick |
| --- | --- | --- |
| IAM Policy | Grants permissions | WHAT YOU GET |
| Permission Boundary | Maximum permissions | MOST YOU CAN GET |

Think:

IAM POLICY

↓

GRANTS

Permission Boundary

↓

LIMITS

### Exam Trap

Permission Boundary does NOT grant permissions.

It defines the:

MAXIMUM

permissions an IAM entity can receive.

Supported:

Users ✅

Roles ✅

Groups ❌

See:

[[IAM Permission Boundaries]]

---

## IAM Policy vs Permission Boundary vs SCP

| Control | Think |
| --- | --- |
| IAM Policy | Permissions |
| Permission Boundary | Identity permission ceiling |
| SCP | Organization/account guardrail |

### Memory Trick

POLICY = GRANT

BOUNDARY = MAX

SCP = ORGANIZATION LIMIT

See:

[[IAM Policy Evaluation Logic]]

---

## IAM Role vs Resource-Based Policy

Both can be used for:

CROSS-ACCOUNT ACCESS

But they behave differently.

| Method | Original Permissions |
| --- | --- |
| Assume IAM Role | Given up |
| Resource-Based Policy | Retained |

### Memory Trick

ROLE = SWITCH

RESOURCE POLICY = KEEP

### Example

User in Account A needs to:

READ DYNAMODB IN ACCOUNT A

and

WRITE TO S3 IN ACCOUNT B

Resource-Based Policy can allow access to the S3 bucket while the user retains their original permissions.

See:

[[IAM Roles vs Resource-Based Policies]]

---

## Credentials Report vs Access Advisor

| Tool | Level | Shows |
| --- | --- | --- |
| Credentials Report | Account | Users + credential status |
| Access Advisor | User | Permissions + last accessed |

### Memory Trick

REPORT = ACCOUNT

ADVISOR = USER

### Scenario

Need account-wide credential information?

→ CREDENTIALS REPORT

Need to see when a user's permitted services were last accessed?

→ ACCESS ADVISOR

See:

[[IAM Security Tools]]

---

## Console vs CLI vs SDK

| Access Method | Think | Course Authentication |
| --- | --- | --- |
| Management Console | Browser | Password + MFA |
| CLI | Commands | Access Keys |
| SDK | Code | Access Keys |

### Memory Trick

CONSOLE = CLICK

CLI = TYPE

SDK = CODE

And:

Access Key ID ≈ USERNAME

Secret Access Key ≈ PASSWORD

Access Keys:

DO NOT SHARE

See:

[[AWS Access Methods]]

---

## Password vs MFA vs Access Keys

### Password

Used for:

MANAGEMENT CONSOLE

---

### MFA

Adds:

SECOND AUTHENTICATION FACTOR

Think:

PASSWORD

+

DEVICE

---

### Access Keys

Used for:

CLI

and

SDK

### Memory Trick

Console = PASSWORD + MFA

Programmatic Access = ACCESS KEYS

See:

[[MFA]]

---

## IAM Conditions Comparison

| Condition | Think |
| --- | --- |
| `aws:SourceIp` | IP |
| `aws:RequestedRegion` | Region |
| `ec2:ResourceTag` | Tag |
| `aws:MultiFactorAuthPresent` | MFA |

### Memory Trick

WHERE FROM?

→ SourceIp

WHICH REGION?

→ RequestedRegion

WHICH TAG?

→ ResourceTag

MFA?

→ MultiFactorAuthPresent

See:

[[IAM Conditions]]

---

## IAM vs IAM Identity Center

### IAM

Think:

AWS IDENTITY + PERMISSIONS

Includes:

- Users
- Groups
- Roles
- Policies

---

### IAM Identity Center

Think:

CENTRALIZED SSO

Provides:

ONE LOGIN

across:

- AWS Organization accounts
- Business applications
- SAML 2.0 applications

Uses:

PERMISSION SETS

### Memory Trick

IAM = PERMISSIONS

IDENTITY CENTER = ONE LOGIN

See:

[[IAM Identity Center]]

---

## IAM User vs Identity Center User

### IAM User

Identity exists within:

IAM

Think:

INDIVIDUAL AWS IDENTITY

---

### Identity Center

Designed for:

CENTRALIZED ACCESS

across multiple AWS accounts and applications.

Think:

SSO

+

AWS ORGANIZATIONS

### Exam Recognition

Many accounts + centralized login?

→ IAM Identity Center

---

## Permission Set vs IAM Policy

### IAM Policy

Defines:

PERMISSIONS

---

### Permission Set

Your course describes a Permission Set as:

COLLECTION OF ONE OR MORE IAM POLICIES

assigned to users and groups to define AWS access through IAM Identity Center.

### Memory Trick

IAM Policy = PERMISSION DOCUMENT

Permission Set = POLICY PACKAGE

---

## Directory Services Comparison

| Service | Main Idea | Memory Trick |
| --- | --- | --- |
| AWS Managed Microsoft AD | Microsoft AD in AWS | TRUST |
| AD Connector | Proxy to on-prem AD | PROXY |
| Simple AD | AD-compatible AWS directory | NO JOIN |

---

## AWS Managed Microsoft AD

Think:

REAL MICROSOFT AD IN AWS

Can establish:

TRUST

with on-premises AD.

Supports:

MFA

---

## AD Connector

Think:

PROXY

AWS authentication requests

↓

AD Connector

↓

ON-PREMISES AD

Users remain managed:

ON-PREMISES

---

## Simple AD

Think:

AD-COMPATIBLE DIRECTORY

But:

CANNOT JOIN ON-PREMISES AD

### Master Memory Trick

Managed Microsoft AD = TRUST

AD Connector = PROXY

Simple AD = NO JOIN

See:

[[AWS Directory Services]]

---

## Policy Evaluation Comparison

### Default

DENY

### Applicable Allow

Potentially:

ALLOW

### Explicit Deny

DENY

### Memory Trick

EXPLICIT DENY WINS

And remember:

IAM Policy

→ GRANT

Permission Boundary

→ MAXIMUM

SCP

→ ORGANIZATION GUARDRAIL

See:

[[IAM Policy Evaluation Logic]]

---

## SAA Scenario Recognition

Need permissions for an EC2 instance?

→ IAM ROLE

---

Need permissions shared among multiple users?

→ IAM GROUP + POLICY

---

Need maximum permissions for a user or role?

→ PERMISSION BOUNDARY

---

Need cross-account access while retaining original permissions?

→ RESOURCE-BASED POLICY

---

Need account-wide credential status?

→ CREDENTIALS REPORT

---

Need user's service permissions and last-access information?

→ ACCESS ADVISOR

---

Need terminal access?

→ CLI + ACCESS KEYS

---

Need application code to interact with AWS?

→ SDK + ACCESS KEYS

---

Need one login across multiple AWS accounts?

→ IAM IDENTITY CENTER

---

Need a package of policies for Identity Center users/groups?

→ PERMISSION SET

---

Need Microsoft AD running in AWS with on-prem trust?

→ AWS MANAGED MICROSOFT AD

---

Need AWS to proxy authentication to existing on-prem AD?

→ AD CONNECTOR

---

Need an AD-compatible directory without on-prem integration?

→ SIMPLE AD

---

## Master Comparison Cheat Sheet

USER

= PERSON

GROUP

= USERS

ROLE

= ASSUMED PERMISSIONS

POLICY

= WHAT YOU CAN DO

PERMISSION BOUNDARY

= MOST YOU CAN DO

SCP

= ORGANIZATION GUARDRAIL

RESOURCE-BASED POLICY

= POLICY ON RESOURCE

CREDENTIALS REPORT

= ACCOUNT

ACCESS ADVISOR

= USER

CONSOLE

= CLICK

CLI

= TYPE

SDK

= CODE

IAM IDENTITY CENTER

= ONE LOGIN

PERMISSION SET

= POLICY PACKAGE

MANAGED MICROSOFT AD

= TRUST

AD CONNECTOR

= PROXY

SIMPLE AD

= NO JOIN

EXPLICIT DENY

= WINS

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
- [[SAA IAM Cheat Sheet]]
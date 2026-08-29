## What Problem Does It Solve?

IAM Best Practices help reduce security risk by ensuring AWS identities, credentials, and permissions are managed securely.

Think:

IAM

↓

SECURE IDENTITIES

+

SECURE CREDENTIALS

+

CORRECT PERMISSIONS

### Memory Trick

IAM Best Practices = SECURE WHO CAN DO WHAT

---

## 1. Don't Use the Root Account

Do NOT use the root account except for:

AWS ACCOUNT SETUP

For normal AWS activities, use IAM identities instead.

### Memory Trick

Root = SETUP ONLY

---

## 2. One Physical User = One AWS User

Your course recommends:

ONE PHYSICAL USER

↓

ONE AWS USER

Do NOT have multiple people sharing the same IAM user.

Think:

Alice → Alice's User

Bob → Bob's User

### Memory Trick

One Person = One User

---

## 3. Use Groups for Permissions

Instead of repeatedly managing permissions for individual users:

USERS

↓

IAM GROUP

↓

PERMISSIONS

Example:

Developers

↓

Developer Permissions

↓

Alice + Bob + Charles

See:

[[IAM Users and Groups]]

### Memory Trick

Users → Groups → Permissions

---

## 4. Create a Strong Password Policy

Use:

[[IAM Password Policy]]

to strengthen IAM passwords.

Password policies can control things such as:

- Minimum length
- Character requirements
- Password expiration
- Password reuse

### Memory Trick

Password Policy = STRONG PASSWORD RULES

---

## 5. Use MFA

Use and enforce:

[[MFA]]

MFA adds another authentication factor beyond the password.

Think:

PASSWORD

+

DEVICE

↓

STRONGER AUTHENTICATION

### Memory Trick

MFA = PASSWORD + DEVICE

---

## 6. Use IAM Roles for AWS Services

When AWS services need permissions:

USE IAM ROLES

Think:

AWS Service

↓

[[IAM Roles]]

↓

Permissions

Examples from your course include:

- EC2 Instance Roles
- Lambda Function Roles
- Roles for CloudFormation

### Memory Trick

AWS Service Needs Permission?

→ ROLE

---

## 7. Use Access Keys for Programmatic Access

For programmatic access using:

CLI

or

SDK

use:

ACCESS KEYS

See:

[[AWS Access Methods]]

### Memory Trick

Console = Password + MFA

CLI / SDK = Access Keys

---

## 8. Audit IAM Permissions

Use:

[[IAM Security Tools]]

Your course identifies:

IAM Credentials Report

and

IAM Access Advisor

### Credentials Report

ACCOUNT LEVEL

### Access Advisor

USER LEVEL

These tools help audit IAM credentials and permissions.

### Memory Trick

Report = ACCOUNT

Advisor = USER

---

## 9. Never Share IAM Users

IAM users should NOT be shared.

Remember:

ONE PHYSICAL USER

=

ONE AWS USER

Sharing users makes identity and access management harder to control.

### Memory Trick

IAM User = ONE PERSON

---

## 10. Never Share Access Keys

Access Keys are:

SECRET

Do NOT share them.

Remember from [[AWS Access Methods]]:

Access Key ID ≈ Username

Secret Access Key ≈ Password

### Memory Trick

Access Keys = KEEP SECRET

---

## Best Practices Architecture

Think of secure IAM like this:

PHYSICAL USER

↓

Individual IAM User

↓

Appropriate Group

↓

[[IAM Policies]]

↓

Least Privilege

PLUS:

Strong [[IAM Password Policy]]

+

[[MFA]]

+

Audit with [[IAM Security Tools]]

For AWS services:

AWS SERVICE

↓

[[IAM Roles]]

↓

Required Permissions

---

## Scenario Recognition

Employees are sharing one IAM user.

→ BAD PRACTICE

Use one AWS user per physical user.

---

A company routinely uses the root account for daily administration.

→ BAD PRACTICE

Use root only for account setup.

---

Twenty developers require the same permissions.

→ Assign users to a group and assign permissions to the group.

---

A company wants stronger login security.

→ [[IAM Password Policy]] + [[MFA]]

---

An EC2 instance needs permission to access AWS resources.

→ [[IAM Roles]]

---

A developer needs programmatic AWS access through the CLI.

→ Access Keys

→ [[AWS Access Methods]]

---

A company wants to audit account credentials and user permissions.

→ [[IAM Security Tools]]

---

An employee wants to give another employee their access keys.

→ NEVER SHARE ACCESS KEYS

---

## Exam Traps

Root Account = DON'T USE FOR DAILY WORK

One Physical User = One AWS User

Users → Groups → Permissions

Password Security = [[IAM Password Policy]]

Additional Authentication = [[MFA]]

AWS Service Permissions = [[IAM Roles]]

CLI / SDK = Access Keys

Audit = [[IAM Security Tools]]

Never share IAM users

Never share Access Keys

---

## Quick Cheat Sheet

Root = SETUP ONLY

User = ONE PERSON

Group = MANAGE USERS

Policy = PERMISSIONS

Password Policy = PASSWORD SECURITY

MFA = EXTRA AUTHENTICATION

Role = AWS SERVICE PERMISSIONS

CLI / SDK = ACCESS KEYS

Credentials Report = ACCOUNT AUDIT

Access Advisor = USER AUDIT

IAM Users = DON'T SHARE

Access Keys = DON'T SHARE

---

## Master Memory Trick

PEOPLE

→ USERS

USERS

→ GROUPS

PERMISSIONS

→ POLICIES

LOGIN SECURITY

→ PASSWORD POLICY + MFA

AWS SERVICES

→ ROLES

PROGRAMMATIC ACCESS

→ ACCESS KEYS

AUDITING

→ SECURITY TOOLS

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
- [[IAM Shared Responsibility]]
- [[IAM Comparison]]
- [[SAA IAM Cheat Sheet]]
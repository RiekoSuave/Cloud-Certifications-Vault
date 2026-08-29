## What Problem Does It Solve?

AWS Identity and Access Management (IAM) controls **who can access AWS and what they are allowed to do**.

Think:

WHO?

↓

WHAT CAN THEY DO?

↓

IAM

### Memory Trick

IAM = WHO CAN DO WHAT

---

## IAM Is a Global Service

IAM is:

GLOBAL

It is not tied to a specific AWS Region.

### Memory Trick

IAM = GLOBAL

---

## Root Account

When an AWS account is created:

ROOT ACCOUNT

↓

Created by default

The root account:

- Has powerful access to the AWS account
- Should NOT be used for everyday tasks
- Should NOT be shared

### Memory Trick

Root = LOCK IT DOWN

---

## IAM Users

IAM Users represent:

PEOPLE

within your organization.

Examples:

Alice

Bob

Charles

Each person can have their own IAM user.

### Memory Trick

User = PERSON

---

## IAM Groups

IAM Groups are collections of:

USERS

Groups make it easier to manage permissions for multiple users.

Example:

Developers

↓

Alice

Bob

Charles

Instead of managing permissions separately for each developer, permissions can be associated with the group.

### Memory Trick

Group = COLLECTION OF USERS

---

## Important Group Rule

IAM Groups can contain:

USERS

IAM Groups CANNOT contain:

OTHER GROUPS

Think:

Group

↓

Users ✅

Groups ❌

### Exam Trap

You cannot create nested IAM groups.

---

## Do Users Have to Belong to a Group?

NO.

An IAM user:

- Does NOT have to belong to a group
- CAN belong to multiple groups

Example:

Alice

↓

[[Developers]]

AND

↓

Audit Team

### Memory Trick

User = Zero, One, or Multiple Groups

---

## Users vs Groups

| IAM Identity | Represents | Can Receive Permissions? |
| --- | --- | --- |
| User | Individual person | Yes |
| Group | Collection of users | Yes |

### Key Difference

User = ONE PERSON

Group = MANY USERS

---

## Permissions

Users and Groups can be assigned:

POLICIES

Policies are JSON documents that define permissions.

Think:

User / Group

↓

[[IAM Policies]]

↓

Permissions

---

## Least Privilege

AWS recommends the:

PRINCIPLE OF LEAST PRIVILEGE

Meaning:

Give users only the permissions they need.

NOT:

Give everyone administrator access.

Think:

Required Permissions

↓

ONLY

↓

Nothing Extra

### Memory Trick

Least Privilege = MINIMUM NECESSARY ACCESS

---

## Architecture Example

A company has 20 developers who all need similar AWS permissions.

Bad approach:

Configure permissions separately for every developer.

Better approach:

Developers

↓

IAM Group

↓

Attach appropriate permissions

↓

Add developer users to group

### Why?

Centralized permission management.

---

## Scenario Recognition

A company needs to represent an individual employee in IAM.

→ IAM User

---

A company wants to organize developers who need similar permissions.

→ IAM Group

---

A user needs permissions from both the Developers team and an Audit team.

→ User can belong to multiple groups

---

A company wants to place one IAM group inside another IAM group.

→ NOT SUPPORTED

Groups contain users, not groups.

---

A company wants every employee to receive administrator permissions even though they don't require them.

→ Violates Least Privilege

---

## Exam Traps

IAM = GLOBAL SERVICE

User = PERSON

Group = USERS

Groups cannot contain groups

Users don't have to belong to a group

Users can belong to multiple groups

Permissions are defined using [[IAM Policies]]

Use Least Privilege

Avoid using the root account for everyday activities

---

## Quick Cheat Sheet

IAM = WHO CAN DO WHAT

IAM = GLOBAL

Root = DON'T USE EVERY DAY

User = PERSON

Group = COLLECTION OF USERS

Group inside Group = NO

User in Multiple Groups = YES

[[IAM Policies]] = PERMISSIONS

Least Privilege = ONLY WHAT YOU NEED

---

## Related Notes

- [[IAM Policies]]
- [[IAM Policy Structure]]
- [[IAM Password Policy]]
- [[MFA]]
- [[AWS Access Methods]]
- [[IAM Roles]]
- [[IAM Security Tools]]
- [[IAM Best Practices]]
- [[IAM Shared Responsibility]]
- [[IAM Comparison]]
- [[SAA IAM Cheat Sheet]]
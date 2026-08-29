## What Problem Does It Solve?

IAM Policies define **what actions a user or group is allowed or denied to perform in AWS**.

Think:

WHO

↓

User / Group

↓

POLICY

↓

WHAT CAN THEY DO?

### Memory Trick

IAM Policy = PERMISSIONS

---

## What Is an IAM Policy?

An IAM Policy is a:

JSON DOCUMENT

that defines permissions.

Policies can be assigned to:

- IAM Users
- IAM Groups

Think:

[[IAM Users and Groups]]

↓

[[IAM Policies]]

↓

AWS Permissions

### Memory Trick

Policy = Permission Rules

---

## What Do Policies Control?

Policies determine what AWS actions are allowed or denied.

Example:

User

↓

IAM Policy

↓

Allow EC2 Describe Actions

The policy determines what that identity can do with AWS resources.

---

## Least Privilege Principle

One of the most important IAM concepts is:

LEAST PRIVILEGE

AWS recommends:

Give a user ONLY the permissions they need.

NOT:

Give users unnecessary permissions.

Think:

Required Access

↓

Minimum Permissions

↓

Least Privilege

### Memory Trick

Least Privilege = ONLY WHAT YOU NEED

---

## Why Least Privilege Matters

Suppose a developer only needs to:

VIEW EC2 INSTANCES

The developer should receive permissions necessary to view EC2 information.

They should NOT automatically receive permission to:

- Delete EC2 instances
- Modify unrelated resources
- Administer the entire AWS account

### Architecture Principle

More permissions than necessary

↓

Larger security risk

Minimum necessary permissions

↓

Smaller security exposure

---

## Policy Inheritance

Permissions can come from different places.

For example, a user may receive permissions through an IAM Group.

Think:

Alice

↓

Developers Group

↓

Developer Policy

↓

Alice receives those permissions

---

## Multiple Groups

Remember from [[IAM Users and Groups]]:

A user can belong to multiple groups.

That means a user can receive permissions associated with multiple groups.

Example:

Alice

↓

Developers Group

+

Audit Team

↓

Permissions associated with both

### Exam Recognition

User belongs to multiple groups

→ Permissions can come through those groups

---

## Inline Policy

Your course's policy inheritance example also shows an:

INLINE POLICY

Think:

Policy attached directly to an identity

rather than permissions received only through group membership.

### Memory Trick

Inline = DIRECT

---

## Policies Are JSON

IAM policies use:

JSON

A policy can contain information such as:

- Effect
- Action
- Resource

We'll break the full JSON structure down separately in:

[[IAM Policy Structure]]

For now, remember:

Effect = ALLOW or DENY

Action = WHAT ACTION

Resource = WHICH RESOURCE

---

## Simple Policy Logic

Think of a policy as answering:

WHO?

↓

WHAT ACTION?

↓

ON WHICH RESOURCE?

↓

ALLOW OR DENY?

This becomes especially important when reading SAA scenario questions.

---

## Scenario Recognition

A company needs to define what AWS actions its developers can perform.

→ IAM Policy

---

A developer only needs permission to view EC2 information.

→ Grant only the necessary permissions

→ Least Privilege

---

A company gives every developer full administrator access even though they only need EC2 read access.

→ Violates Least Privilege

---

A user belongs to both the Developers group and Audit Team.

→ The user can receive permissions through both groups

---

A policy needs to be attached directly to an identity.

→ Inline Policy

---

## Exam Traps

IAM Policies = JSON documents

Policies = PERMISSIONS

Users can receive permissions

Groups can receive permissions

Users can inherit permissions through groups

Users can belong to multiple groups

Inline = policy attached directly to an identity

Least Privilege = don't give more permissions than needed

---

## Quick Cheat Sheet

IAM Policy = PERMISSIONS

Policy Format = JSON

Least Privilege = MINIMUM ACCESS

Group Policy = Permissions through group

Inline Policy = DIRECT

Effect = ALLOW / DENY

Action = WHAT

Resource = WHERE

---

## Related Notes

- [[IAM Users and Groups]]
- [[IAM Policy Structure]]
- [[IAM Roles]]
- [[IAM Best Practices]]
- [[IAM Security Tools]]
- [[IAM Comparison]]
- [[SAA IAM Cheat Sheet]]
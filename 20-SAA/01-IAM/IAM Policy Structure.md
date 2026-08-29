## What Problem Does It Solve?

IAM Policy Structure defines **how AWS permission rules are written inside a JSON policy document**.

Think:

IAM Policy

↓

JSON

↓

Permission Rules

### Memory Trick

Policy Structure = HOW PERMISSIONS ARE WRITTEN

---

## IAM Policy Structure

An IAM policy can contain:

- Version
- Id
- Statement

The most important part is:

STATEMENT

A policy can contain one or more statements.

---

## Version

Version defines the:

POLICY LANGUAGE VERSION

Your course says to always include:

2012-10-17

### Memory Trick

Version = POLICY LANGUAGE

---

## Id

Id is an:

OPTIONAL

identifier for the policy.

### Memory Trick

Id = Policy Identifier

---

## Statement

Statement is:

REQUIRED

It contains one or more individual permission statements.

Think:

Policy

↓

Statement

↓

Permission Rules

### Memory Trick

Statement = THE ACTUAL RULES

---

## Statement Components

A Statement can contain:

- Sid
- Effect
- Principal
- Action
- Resource
- Condition

---

## Sid

Sid means:

STATEMENT IDENTIFIER

It is:

OPTIONAL

Think:

Sid = Name / Identifier for a Statement

---

## Effect

Effect determines whether the statement:

ALLOWS

or

DENIES

access.

Possible values:

Allow

Deny

### Memory Trick

Effect = ALLOW OR DENY

---

## Principal

Principal identifies the:

ACCOUNT

USER

or

ROLE

to which the policy applies.

Think:

Principal = WHO

### Memory Trick

Principal = WHO

---

## Action

Action specifies:

WHAT AWS ACTIONS

are allowed or denied.

Example concept:

ec2:Describe*

Think:

Action = WHAT CAN THEY DO?

### Memory Trick

Action = WHAT

---

## Resource

Resource specifies:

WHICH AWS RESOURCES

the actions apply to.

Think:

Action

↓

performed on

↓

Resource

### Memory Trick

Resource = WHERE / WHAT RESOURCE

---

## Condition

Condition specifies:

WHEN

the policy should be in effect.

Condition is:

OPTIONAL

### Memory Trick

Condition = WHEN

---

## Reading a Policy

When you see an IAM policy on the exam, mentally ask:

Principal

→ WHO?

Action

→ WHAT?

Resource

→ WHICH RESOURCE?

Effect

→ ALLOW OR DENY?

Condition

→ UNDER WHAT CONDITIONS?

---

## Policy Reading Formula

WHO

↓

can do WHAT

↓

to WHICH RESOURCE

↓

ALLOW or DENY

↓

under WHAT CONDITIONS

---

## Example Recognition

If you see:

Effect = Allow

Think:

The specified action is being permitted.

---

If you see:

Effect = Deny

Think:

The specified action is being denied.

---

If you see:

Action = ec2:Describe*

Think:

Actions beginning with:

ec2:Describe

---

If you see:

Resource = *

Think:

The statement specifies all resources for that Resource element.

---

## Scenario Recognition

A question asks which IAM policy element determines whether access is permitted or rejected.

→ Effect

---

A question asks which element lists the AWS operations covered by the policy.

→ Action

---

A question asks which element identifies the resources affected by the permissions.

→ Resource

---

A question asks which element identifies an account, user, or role to which a policy applies.

→ Principal

---

A question asks which element controls when a policy takes effect.

→ Condition

---

## Exam Traps

Version = POLICY LANGUAGE VERSION

Statement = REQUIRED

Sid = OPTIONAL

Effect = ALLOW / DENY

Principal = WHO

Action = WHAT

Resource = WHICH RESOURCE

Condition = WHEN

Do NOT confuse:

Action

with

Resource

Action = WHAT YOU DO

Resource = WHAT YOU DO IT TO

---

## Quick Cheat Sheet

Version = POLICY LANGUAGE

Id = POLICY IDENTIFIER

Statement = RULES

Sid = STATEMENT IDENTIFIER

Effect = ALLOW / DENY

Principal = WHO

Action = WHAT

Resource = WHICH RESOURCE

Condition = WHEN

---

## Master Memory Trick

WHO?

→ Principal

WHAT?

→ Action

WHERE / WHICH RESOURCE?

→ Resource

ALLOW OR DENY?

→ Effect

WHEN?

→ Condition

---

## Related Notes

- [[IAM Policies]]
- [[IAM Users and Groups]]
- [[IAM Roles]]
- [[IAM Best Practices]]
- [[IAM Comparison]]
- [[SAA IAM Cheat Sheet]]
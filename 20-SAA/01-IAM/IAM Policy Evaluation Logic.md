## What Problem Does It Solve?

IAM Policy Evaluation Logic determines whether an AWS request is ultimately:

ALLOWED

or

DENIED

when multiple permission controls may apply.

Think:

USER MAKES REQUEST

↓

AWS EVALUATES PERMISSIONS

↓

ALLOW or DENY

### Memory Trick

Policy Evaluation = FINAL PERMISSION DECISION

---

## Start With Deny

By default, access is:

DENIED

A permission must allow the requested action before it can be performed.

### Memory Trick

No Allow = NO ACCESS

---

## Explicit Deny

An:

EXPLICIT DENY

takes priority over an Allow.

Think:

ALLOW

+

EXPLICIT DENY

↓

DENY

### Master Memory Trick

EXPLICIT DENY WINS

---

## Allow

If the request has an applicable:

ALLOW

and there is no overriding Deny:

↓

REQUEST CAN BE ALLOWED

Think:

Allow Exists

+

No Deny Blocking It

↓

ALLOW

---

## Basic Evaluation Logic

Think through exam questions like this:

REQUEST

↓

Is there an applicable DENY?

YES

→ DENY

NO

↓

Is the action ALLOWED?

YES

→ ALLOW

NO

→ DENY

---

## IAM Policies

Remember:

[[IAM Policies]]

define permissions.

A policy may specify:

Effect

↓

Allow / Deny

Action

↓

What operation?

Resource

↓

Which resource?

Condition

↓

Under what circumstances?

See:

[[IAM Policy Structure]]

---

## Permission Boundaries

Remember from:

[[IAM Permission Boundaries]]

A Permission Boundary defines:

MAXIMUM PERMISSIONS

an IAM user or role can receive.

Think:

IAM Policy

↓

GRANTS PERMISSION

BUT

Permission Boundary

↓

LIMITS MAXIMUM

The requested permission must fit within the boundary.

### Memory Trick

Policy = WHAT YOU GET

Boundary = MOST YOU CAN GET

---

## Organizations SCPs

[[AWS Organizations SCP]]

can also restrict what permissions are available within AWS Organizations.

Think:

SCP

↓

ORGANIZATION / ACCOUNT GUARDRAIL

This can combine with:

IAM Policies

+

Permission Boundaries

+

Other applicable permission controls

when AWS evaluates access.

---

## Permission Intersection Concept

A useful way to think about advanced IAM:

IAM Policy

↓

What permissions are granted?

Permission Boundary

↓

What is the maximum?

SCP

↓

What is permitted by the organization?

The effective permission must survive the applicable restrictions.

### Memory Trick

Permission must pass ALL applicable limits.

---

## Example: Allowed by Policy but Outside Boundary

IAM Policy:

ALLOW EC2

Permission Boundary:

ONLY S3

Result:

EC2 NOT AVAILABLE

Why?

The policy tried to grant a permission outside the maximum allowed by the boundary.

---

## Example: Allow + Explicit Deny

Policy A:

ALLOW ACTION

Policy B:

DENY ACTION

Result:

DENY

### Memory Trick

DENY BEATS ALLOW

---

## Example: No Allow

User requests:

SQS ACTION

But no applicable permission allows it.

Result:

DENY

### Memory Trick

Not Allowed = Denied

---

## Course Policy Questions

Your course follows the evaluation-logic slide with an example IAM policy and asks whether the principal can perform:

`sqs:CreateQueue`

`sqs:DeleteQueue`

`ec2:DescribeInstances`

The purpose is to practice reading the policy and deciding whether each requested action is permitted.

---

## How to Solve These Questions

When the exam gives you a policy:

### Step 1

Identify:

ACTION

What is the user trying to do?

---

### Step 2

Look for:

ALLOW

Does an applicable policy allow the action?

---

### Step 3

Look for:

DENY

Is there an applicable Deny?

---

### Step 4

Check applicable limits such as:

[[IAM Permission Boundaries]]

or

[[AWS Organizations SCP]]

---

### Step 5

Determine:

FINAL EFFECTIVE PERMISSION

---

## Scenario Recognition

An action is explicitly denied even though another policy allows it.

→ DENY

---

No policy allows the requested action.

→ DENY

---

An IAM Policy grants a permission, but the Permission Boundary does not permit it.

→ Permission cannot exceed the Boundary

---

A developer asks why attaching an Allow policy did not automatically give them access.

Think:

Are there other applicable permission restrictions?

→ Permission Boundary

→ SCP

→ Explicit Deny

---

## Exam Traps

ALLOW does NOT always mean final access

Explicit Deny can override Allow

No applicable Allow = Deny

Permission Boundary = MAXIMUM

SCP = ORGANIZATION / ACCOUNT GUARDRAIL

You must determine the:

EFFECTIVE PERMISSIONS

not simply find the word "Allow"

---

## Quick Cheat Sheet

DEFAULT = DENY

ALLOW = POSSIBLE ACCESS

EXPLICIT DENY = WINS

NO ALLOW = DENY

IAM Policy = GRANT

Permission Boundary = MAXIMUM

SCP = ORGANIZATION GUARDRAIL

Final Result = EFFECTIVE PERMISSIONS

---

## Master Memory Trick

DENY?

→ STOP

NO DENY?

↓

ALLOW?

→ YES = Continue Evaluation

→ NO = DENY

Then make sure the permission fits within applicable:

BOUNDARIES

and

SCPs

---

## Related Notes

- [[IAM Policies]]
- [[IAM Policy Structure]]
- [[IAM Conditions]]
- [[IAM Permission Boundaries]]
- [[IAM Roles vs Resource-Based Policies]]
- [[AWS Organizations SCP]]
- [[IAM Identity Center]]
- [[IAM Comparison]]
- [[SAA IAM Cheat Sheet]]
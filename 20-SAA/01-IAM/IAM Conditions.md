## What Problem Does It Solve?

IAM Conditions make permissions more specific by controlling **when or under what circumstances an IAM policy applies**.

Think:

ALLOW / DENY

↓

ONLY IF...

↓

CONDITION

### Memory Trick

Condition = ONLY IF

---

## Where Do Conditions Fit?

Remember from [[IAM Policy Structure]]:

An IAM policy can include:

- Effect
- Principal
- Action
- Resource
- Condition

The:

CONDITION

adds extra requirements before the policy applies.

Think:

WHO?

↓

WHAT?

↓

WHICH RESOURCE?

↓

ONLY IF WHAT?

### Memory Trick

Condition = EXTRA RULE

---

## aws:SourceIp

`aws:SourceIp`

restricts:

THE CLIENT IP ADDRESS

from which API calls are made.

Think:

Allow API Call

↓

ONLY FROM APPROVED IP

### Memory Trick

SourceIp = WHERE ARE YOU CONNECTING FROM?

---

## Source IP Scenario

A company wants AWS API calls to be allowed only when employees connect from an approved corporate IP address.

Think:

IP RESTRICTION

↓

aws:SourceIp

---

## aws:RequestedRegion

`aws:RequestedRegion`

restricts:

THE AWS REGION

where API calls can be made.

Think:

API Call

↓

ONLY IN APPROVED REGION

### Memory Trick

RequestedRegion = WHICH REGION?

---

## Requested Region Scenario

A company wants users to perform AWS API actions only in approved Regions.

Think:

REGION RESTRICTION

↓

aws:RequestedRegion

---

## ec2:ResourceTag

`ec2:ResourceTag`

restricts access based on:

RESOURCE TAGS

Think:

EC2 Resource

↓

TAG

↓

Permission Decision

### Memory Trick

ResourceTag = ACCESS BY TAG

---

## Resource Tag Scenario

A company wants developers to perform actions only on EC2 resources with an appropriate tag.

Think:

TAG-BASED ACCESS

↓

ec2:ResourceTag

---

## aws:MultiFactorAuthPresent

`aws:MultiFactorAuthPresent`

can be used to:

FORCE MFA

Think:

User Requests Action

↓

Is MFA Present?

↓

YES → Continue

NO → Restrict

### Memory Trick

MultiFactorAuthPresent = REQUIRE MFA

See:

[[MFA]]

---

## MFA Condition Scenario

A company wants a sensitive AWS action to be performed only when the user has authenticated with MFA.

Think:

MFA REQUIRED

↓

aws:MultiFactorAuthPresent

---

## Condition Key Comparison

| Condition Key | Restricts Based On | Think |
| --- | --- | --- |
| `aws:SourceIp` | Client IP address | WHERE FROM |
| `aws:RequestedRegion` | AWS Region | WHICH REGION |
| `ec2:ResourceTag` | EC2 tags | WHICH TAG |
| `aws:MultiFactorAuthPresent` | MFA status | MFA REQUIRED |

---

## SAA Scenario Recognition

Need to restrict API calls by IP address?

→ `aws:SourceIp`

---

Need to restrict API calls to specific AWS Regions?

→ `aws:RequestedRegion`

---

Need to control EC2 access based on tags?

→ `ec2:ResourceTag`

---

Need to require MFA before an action is allowed?

→ `aws:MultiFactorAuthPresent`

---

## Architecture Thinking

Without Conditions:

User

↓

Permission

↓

AWS Resource

With Conditions:

User

↓

Permission

↓

CONDITION CHECK

↓

AWS Resource

### Example

User has permission to perform action

BUT

Condition requires MFA

↓

No MFA

↓

Action restricted

---

## Exam Traps

Condition ≠ Action

Action = WHAT the user can do

Condition = WHEN / UNDER WHAT CIRCUMSTANCES

`aws:SourceIp` = IP restriction

`aws:RequestedRegion` = Region restriction

`ec2:ResourceTag` = Tag-based restriction

`aws:MultiFactorAuthPresent` = MFA requirement

---

## Quick Cheat Sheet

Condition = ONLY IF

SourceIp = IP

RequestedRegion = REGION

ResourceTag = TAG

MultiFactorAuthPresent = MFA

---

## Master Memory Trick

WHERE FROM?

→ SourceIp

WHICH REGION?

→ RequestedRegion

WHICH TAG?

→ ResourceTag

MFA REQUIRED?

→ MultiFactorAuthPresent

---

## Related Notes

- [[IAM Policies]]
- [[IAM Policy Structure]]
- [[MFA]]
- [[02-Compute/EC2]]
- [[IAM Roles]]
- [[IAM Permission Boundaries]]
- [[IAM Policy Evaluation Logic]]
- [[IAM Comparison]]
- [[SAA IAM Cheat Sheet]]
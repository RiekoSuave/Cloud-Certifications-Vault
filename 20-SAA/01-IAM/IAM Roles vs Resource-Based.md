## What Problem Does It Solve?

IAM Roles and Resource-Based Policies are two ways to give a principal access to AWS resources.

They are especially important when designing:

CROSS-ACCOUNT ACCESS

Think:

Account A

↓

Needs Resource in Account B

↓

ROLE

or

RESOURCE-BASED POLICY

---

## The Key Difference

### IAM Role

When a:

- User
- Application
- Service

assumes an IAM Role:

ORIGINAL PERMISSIONS

↓

GIVEN UP

↓

ROLE PERMISSIONS

### Memory Trick

Assume Role = SWITCH PERMISSIONS

---

## Resource-Based Policy

With a Resource-Based Policy:

PRINCIPAL

↓

KEEPS ORIGINAL PERMISSIONS

+

↓

Receives access through the resource policy

### Memory Trick

Resource Policy = KEEP YOUR PERMISSIONS

---

## Master Comparison

| Method | Original Permissions |
| --- | --- |
| Assume IAM Role | Given up |
| Resource-Based Policy | Kept |

### Memory Trick

ROLE = SWITCH

RESOURCE POLICY = KEEP

---

## Cross-Account Example

Your course gives this example:

User in:

ACCOUNT A

needs to:

SCAN DYNAMODB TABLE

in Account A

AND

DUMP THE DATA

into an:

S3 BUCKET

in Account B.

Think:

Account A

DynamoDB

↓

User

↓

S3 Bucket

Account B

---

## Why Resource-Based Policy Helps

The user needs their existing permissions in:

ACCOUNT A

to access DynamoDB.

They also need access to the S3 bucket in:

ACCOUNT B.

With a Resource-Based Policy:

ORIGINAL ACCOUNT A PERMISSIONS

↓

RETAINED

+

S3 BUCKET ACCESS

↓

Account B

### SAA Recognition

Need access to another account's resource while retaining original permissions?

→ RESOURCE-BASED POLICY

---

## Services Supporting Resource-Based Policies

Your course gives examples including:

- Amazon S3 Buckets
- SNS Topics
- SQS Queues

Think:

RESOURCE

↓

POLICY ATTACHED TO RESOURCE

### Memory Trick

Resource-Based Policy = POLICY ON THE RESOURCE

---

## IAM Role Approach

With an IAM Role:

Principal

↓

ASSUME ROLE

↓

Original Permissions Given Up

↓

Role Permissions Used

This is different from:

[[IAM Roles]]

where we initially focused on AWS services receiving permissions.

For SAA, remember that roles can be assumed by:

- Users
- Applications
- Services

---

## EventBridge Example

Your course also shows how EventBridge obtains permissions on different targets.

When an EventBridge rule runs:

EVENTBRIDGE

↓

NEEDS PERMISSION ON TARGET

Depending on the target, your course shows either:

RESOURCE-BASED POLICY

or

IAM ROLE

---

## EventBridge + Resource-Based Policy

Your course lists these examples:

- Lambda
- SNS
- SQS
- S3 Buckets
- API Gateway

Think:

EventBridge

↓

Target Resource

↓

Resource-Based Policy

Example:

Lambda

↓

Resource-Based Policy

↓

Allow EventBridge

---

## EventBridge + IAM Role

Your course lists these examples:

- EC2 Auto Scaling
- Systems Manager Run Command
- ECS Task

Think:

EventBridge

↓

IAM Role

↓

Target

### Exam Recognition

EventBridge needs permissions on its target.

The permission mechanism can depend on the target service.

---

## Role vs Resource Policy

### IAM Role

Principal assumes:

ROLE PERMISSIONS

Original permissions:

GIVEN UP

Think:

SWITCH IDENTITY / PERMISSIONS

---

### Resource-Based Policy

Policy is attached to:

RESOURCE

Principal's original permissions:

RETAINED

Think:

KEEP IDENTITY / PERMISSIONS

---

## Scenario Recognition

A user assumes an IAM Role.

What happens to their original permissions?

→ They give them up and use the Role permissions.

---

A principal receives access through a Resource-Based Policy.

What happens to their original permissions?

→ They retain them.

---

A user in Account A needs to access DynamoDB in Account A and write the results into an S3 bucket in Account B.

→ Resource-Based Policy is useful because the user can retain their original permissions.

---

An EventBridge rule targets Lambda.

Your course pattern:

→ Resource-Based Policy

---

An EventBridge rule targets EC2 Auto Scaling.

Your course pattern:

→ IAM Role

---

## Exam Traps

IAM Role ≠ Resource-Based Policy

Assume Role = ORIGINAL PERMISSIONS GIVEN UP

Resource-Based Policy = ORIGINAL PERMISSIONS RETAINED

Role = POLICY PERMISSIONS ARE ASSUMED

Resource Policy = POLICY ATTACHED TO RESOURCE

S3 / SNS / SQS can support Resource-Based Policies

Cross-account access can involve either approach

---

## Quick Cheat Sheet

IAM ROLE

→ ASSUME

→ SWITCH PERMISSIONS

→ ORIGINAL PERMISSIONS GIVEN UP

RESOURCE-BASED POLICY

→ POLICY ON RESOURCE

→ KEEP ORIGINAL PERMISSIONS

### EventBridge Course Examples

Lambda / SNS / SQS / S3 / API Gateway

→ RESOURCE-BASED POLICY

EC2 Auto Scaling / SSM Run Command / ECS Task

→ IAM ROLE

---

## Master Memory Trick

ROLE

=

SWITCH

RESOURCE POLICY

=

KEEP

---

## Related Notes

- [[IAM Roles]]
- [[IAM Policies]]
- [[IAM Policy Structure]]
- [[IAM Conditions]]
- [[S3]]
- [[SNS]]
- [[SQS]]
- [[02-Compute/Lambda]]
- [[20-SAA/10-Messaging/EventBridge]]
- [[IAM Permission Boundaries]]
- [[IAM Policy Evaluation Logic]]
- [[IAM Comparison]]
- [[SAA IAM Cheat Sheet]]
## What Problem Does It Solve?

An EC2 instance may need permission to:

ACCESS OTHER AWS SERVICES

Example:

EC2

↓

S3

Instead of treating the EC2 instance like a human user, AWS uses:

IAM ROLES

### Memory Trick

EC2 NEEDS AWS PERMISSIONS?

→ IAM ROLE

---

## What Is an EC2 Instance Role?

An EC2 Instance Role gives an:

EC2 INSTANCE

permissions to perform actions against AWS services.

Think:

EC2 INSTANCE

↓

IAM ROLE

↓

AWS SERVICE

---

## Why Does EC2 Need a Role?

AWS services sometimes need to:

PERFORM ACTIONS ON YOUR BEHALF

IAM Roles provide the required:

PERMISSIONS

Your course gives common role examples:

- EC2 Instance Roles
- Lambda Function Roles
- CloudFormation Roles

### Memory Trick

AWS SERVICE NEEDS PERMISSION

→ ROLE

---

## EC2 Accessing S3

Your course specifically illustrates:

EC2 INSTANCE

↓

EC2 INSTANCE ROLE

↓

IAM PERMISSIONS

↓

S3 BUCKET

Think:

EC2 needs S3 access?

↓

ATTACH IAM ROLE

↓

ROLE CONTAINS REQUIRED PERMISSIONS

↓

EC2 ACCESSES S3

---

## Role Permissions

The IAM Role determines:

WHAT THE EC2 INSTANCE IS ALLOWED TO DO

For example, permissions could determine whether EC2 can perform permitted actions against an S3 bucket.

The exact permissions depend on the:

IAM POLICIES

associated with the role.

Think:

IAM POLICY

↓

DEFINES PERMISSIONS

↓

IAM ROLE

↓

USED BY EC2

---

## EC2 Role Architecture

EC2 INSTANCE

↓

ASSUMES / USES ROLE

↓

IAM PERMISSIONS

↓

AWS SERVICE

### Memory Trick

INSTANCE

→ ROLE

→ PERMISSIONS

→ SERVICE

---

## EC2 Role vs IAM User

### IAM User

Think:

PERSON / LONG-TERM IDENTITY

### IAM Role

Think:

ASSUMED PERMISSIONS

For an EC2 instance needing AWS permissions:

USE A ROLE

### Memory Trick

PERSON

→ USER

EC2

→ ROLE

---

## EC2 Role vs Security Group

Don't confuse these.

### IAM Role

Controls:

WHAT AWS API ACTIONS EC2 CAN PERFORM

### Security Group

Controls:

NETWORK TRAFFIC

### Memory Trick

ROLE

= PERMISSIONS

SECURITY GROUP

= NETWORK

---

## Example

Suppose an application running on EC2 needs to read data from S3.

Architecture:

APPLICATION

↓

EC2 INSTANCE

↓

IAM ROLE

↓

IAM PERMISSIONS

↓

S3 BUCKET

The role provides the AWS permissions required by the instance.

---

## Scenario Recognition

EC2 needs to access an S3 bucket?

→ EC2 INSTANCE ROLE

---

EC2 needs permission to make AWS API calls?

→ IAM ROLE

---

Lambda needs AWS permissions?

→ LAMBDA FUNCTION ROLE

---

CloudFormation needs permissions?

→ CLOUDFORMATION ROLE

---

Need to control network traffic into EC2?

→ NOT IAM ROLE

→ SECURITY GROUP

---

Need to determine which AWS actions EC2 may perform?

→ IAM ROLE + IAM POLICIES

---

## Exam Traps

EC2 accessing AWS services?

→ IAM ROLE

IAM Role

= AWS PERMISSIONS

Security Group

= NETWORK TRAFFIC

IAM User

≠ EC2 INSTANCE

EC2 Instance Role

= ROLE USED BY EC2

---

## Quick Cheat Sheet

EC2

↓

IAM ROLE

↓

IAM PERMISSIONS

↓

AWS SERVICE

ROLE

= PERMISSIONS

SECURITY GROUP

= NETWORK

EC2 → S3

= IAM ROLE

SERVICE NEEDS PERMISSIONS?

= ROLE

---

## Master Memory Trick

WHO NEEDS ACCESS?

PERSON?

→ IAM USER

EC2?

→ IAM ROLE

WHAT DOES ROLE CONTROL?

→ AWS PERMISSIONS

WHAT CONTROLS NETWORK TRAFFIC?

→ SECURITY GROUP

---

## Related Notes

- [[EC2]]
- [[EC2 Security Groups]]
- [[IAM Roles]]
- [[IAM Policies]]
- [[IAM Best Practices]]
- [[S3]]
- [[SAA IAM Cheat Sheet]]
- [[SAA EC2 Cheat Sheet]]
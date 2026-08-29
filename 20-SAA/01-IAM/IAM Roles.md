## What Problem Does It Solve?

IAM Roles allow AWS services to receive permissions so they can perform actions on your behalf.

Think:

AWS SERVICE

↓

IAM ROLE

↓

PERMISSIONS

↓

ACCESS AWS RESOURCES

### Memory Trick

IAM Role = PERMISSIONS FOR AWS SERVICES

---

## What Is an IAM Role?

Some AWS services need permission to interact with other AWS resources.

Instead of thinking:

AWS Service → No Permissions

Think:

AWS Service

↓

IAM Role

↓

AWS Permissions

↓

Perform Required Action

### Memory Trick

Role = GIVE THE SERVICE PERMISSION

---

## Why Do AWS Services Need Roles?

An AWS service may need to perform actions on your behalf.

Example:

[[02-Compute/EC2]]

↓

Needs Access to AWS

↓

IAM Role

↓

Permissions

The IAM Role provides the permissions needed by the service.

---

## Common IAM Roles

Your SAA course identifies these common examples:

- EC2 Instance Roles
- Lambda Function Roles
- Roles for CloudFormation

These are important because all three services appear throughout SAA.

---

## EC2 Instance Role

An EC2 instance may need to access another AWS resource.

Think:

[[02-Compute/EC2]]

↓

EC2 Instance Role

↓

IAM Permissions

↓

Access AWS

### Memory Trick

EC2 Needs AWS Access?

→ IAM ROLE

---

## Lambda Function Role

A [[02-Compute/Lambda]] function may need permission to perform AWS actions.

Think:

Lambda Function

↓

IAM Role

↓

Permissions

↓

AWS Resources

### Memory Trick

Lambda Needs Permissions?

→ IAM ROLE

---

## CloudFormation Role

[[CloudFormation]] may need permissions to perform AWS actions while working with resources.

Think:

CloudFormation

↓

IAM Role

↓

AWS Permissions

### Memory Trick

Service Acts on Your Behalf?

→ ROLE

---

## Important SAA Architecture Pattern

This pattern will appear repeatedly throughout SAA:

SERVICE A

↓

needs access to

↓

SERVICE B

The question becomes:

HOW SHOULD SERVICE A RECEIVE AWS PERMISSIONS?

Think:

IAM ROLE

---

## EC2 Access Example

Your course later reinforces this architecture when discussing an EC2 instance accessing an S3 bucket.

Think:

[[02-Compute/EC2]]

↓

EC2 Instance Role

↓

IAM Permissions

↓

[[S3]]

### Exam Recognition

EC2 needs permission to access an AWS resource.

→ IAM Role

---

## Role vs IAM User

Don't confuse:

[[IAM Users and Groups]]

with

IAM Roles

### IAM User

Think:

PERSON

### IAM Role

Think:

PERMISSIONS ASSUMED FOR A PURPOSE

For this section of your course, the major emphasis is:

AWS SERVICE

↓

IAM ROLE

↓

PERMISSIONS

### Memory Trick

User = PERSON

Role = PERMISSIONS FOR A JOB

---

## Role vs Access Keys

Don't confuse:

IAM ROLE

with

ACCESS KEYS

From [[AWS Access Methods]]:

Access Keys are credentials used for programmatic access.

But when an AWS service such as EC2 needs AWS permissions, your course emphasizes:

IAM ROLE

### SAA Recognition

EC2 needs AWS permissions?

→ IAM Role

NOT:

Put access keys on the EC2 instance

### Memory Trick

AWS Service = ROLE

---

## Scenario Recognition

An EC2 instance needs permission to access another AWS service.

→ EC2 Instance Role

---

A Lambda function needs permissions to perform AWS actions.

→ Lambda Function Role

---

CloudFormation needs permissions to perform AWS actions.

→ Role for CloudFormation

---

An AWS service needs to perform actions on your behalf.

→ IAM Role

---

An EC2 instance needs access to an S3 bucket.

Think:

EC2

↓

IAM Role

↓

IAM Permissions

↓

S3

---

## Exam Traps

IAM Role = PERMISSIONS

AWS services can use IAM Roles

EC2 Instance Role = EC2 permissions

Lambda Function Role = Lambda permissions

CloudFormation Role = CloudFormation permissions

AWS service needs AWS access?

→ Think IAM Role

Don't confuse IAM Roles with [[IAM Users and Groups]]

Don't confuse IAM Roles with access keys from [[AWS Access Methods]]

---

## Quick Cheat Sheet

IAM Role = SERVICE PERMISSIONS

EC2 → INSTANCE ROLE

Lambda → FUNCTION ROLE

CloudFormation → ROLE

Service needs AWS permissions?

→ IAM ROLE

User = PERSON

Role = PERMISSIONS FOR A JOB

---

## Master Memory Trick

AWS SERVICE

↓

NEEDS PERMISSION

↓

IAM ROLE

---

## Related Notes

- [[IAM Users and Groups]]
- [[IAM Policies]]
- [[AWS Access Methods]]
- [[02-Compute/EC2]]
- [[02-Compute/Lambda]]
- [[S3]]
- [[CloudFormation]]
- [[IAM Security Tools]]
- [[IAM Best Practices]]
- [[IAM Comparison]]
- [[SAA IAM Cheat Sheet]]
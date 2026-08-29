See also: [Organizations](Organizations)

## What Problem Does It Solve?

Controls who can access AWS resources and what actions they are allowed to perform.

IAM stands for:

Identity and Access Management

IAM manages:

WHO

can do

WHAT

in AWS.

### Memory Trick

IAM = Who Can Do What?

---

## Type

Identity and Access Management

---

## What Is IAM?

IAM is AWS's service for managing identities and permissions.

IAM includes:

- Users
- Groups
- Roles
- Policies
- Password policies
- MFA
- Access keys

IAM is a:

Global Service

It is not tied to a specific AWS Region.

### Memory Trick

IAM = AWS Access Control

---

## Root Account

The AWS root account is created when the AWS account is created.

Your course recommends:

Do NOT use or share the root account for everyday activities.

The root account should generally only be used when necessary for account-level tasks.

### Memory Trick

Root = Powerful

Don't Use It Daily

---

## IAM Users

IAM Users represent people or identities within your AWS account.

Example:

Company

↓

IAM Users

- Alice
- Bob
- John

Each person should have their own IAM user rather than sharing credentials.

### Best Practice

One Physical User = One AWS User

---

## IAM Groups

IAM Groups contain:

IAM Users

Groups make it easier to assign permissions to multiple users.

Example:

Developers Group

↓

Alice

Bob

John

Permissions can be assigned to the group instead of individually assigning the same permissions to every user.

### Important Rules

Groups contain users.

Groups do NOT contain other groups.

A user:

- Does not have to belong to a group
- Can belong to multiple groups

### Memory Trick

Group = Collection of Users

---

## IAM Policies

IAM Policies define permissions.

Your course describes policies as:

JSON Documents

Policies determine which actions are allowed.

Basic Idea:

User / Group / Role

↓

IAM Policy

↓

Permissions

### Memory Trick

Policy = Permissions

---

## Principle of Least Privilege

One of the most important IAM security concepts is:

Least Privilege

This means:

Do not give users more permissions than they need.

Example:

If a user only needs access to S3:

Give S3 permissions

NOT administrator permissions.

### Memory Trick

Least Privilege = Only What You Need

---

## Password Policies

AWS allows you to configure password policies for IAM users.

Password policies can include:

- Minimum password length
- Uppercase letters
- Lowercase letters
- Numbers
- Non-alphanumeric characters
- Password expiration
- Prevent password reuse

You can also allow users to change their own passwords.

### Memory Trick

Password Policy = Password Rules

---

## Multi-Factor Authentication (MFA)

MFA adds another layer of security to AWS accounts.

MFA combines:

Something You Know

+

Something You Own

Example:

Password

+

MFA Device

The major benefit:

If a password is stolen, the password alone is not enough to access the account.

### Best Practice

Protect:

- Root account
- IAM users

with MFA.

### Memory Trick

MFA = Password + Security Device

---

## Ways to Access AWS

Your course identifies three major ways users can access AWS.

### AWS Management Console

Protected using:

Password + MFA

---

### AWS Command Line Interface (CLI)

Protected using:

Access Keys

---

### AWS Software Development Kit (SDK)

Used by applications/code.

Protected using:

Access Keys

---

## Access Keys

Access keys provide programmatic access to AWS.

An access key contains:

Access Key ID

+

Secret Access Key

Your course compares them conceptually to:

Access Key ID ≈ Username

Secret Access Key ≈ Password

### Important

Access keys are secret.

Never share them.

Users manage their own access keys.

### Memory Trick

Access Keys = Programmatic Access

---

## AWS CLI

CLI stands for:

Command Line Interface

The AWS CLI allows you to interact with AWS services using commands from a command-line shell.

It provides direct access to AWS service APIs.

Common uses include:

- Managing AWS resources
- Automating tasks
- Creating scripts

### Memory Trick

CLI = AWS From Terminal

---

## AWS SDK

SDK stands for:

Software Development Kit

AWS SDKs allow applications to interact with AWS programmatically.

SDKs are available for many programming languages.

Examples from your course include:

- JavaScript
- Python
- PHP
- .NET
- Ruby
- Java
- Go
- Node.js
- C++

There are also mobile SDKs.

### Memory Trick

SDK = AWS From Code

---

## Console vs CLI vs SDK

| Access Method | Authentication | Think |
|---|---|---|
| Management Console | Password + MFA | Browser |
| AWS CLI | Access Keys | Terminal |
| AWS SDK | Access Keys | Application Code |

### Memory Trick

Console = Browser

CLI = Terminal

SDK = Code

---

## IAM Roles

IAM Roles provide permissions that can be assumed by AWS services.

Some AWS services need permission to perform actions on your behalf.

Instead of giving the service an IAM user's credentials, you can assign:

IAM Role

Common examples from your course:

- EC2 Instance Roles
- Lambda Function Roles
- CloudFormation Roles

Basic Idea:

AWS Service

↓

IAM Role

↓

Permissions

### Memory Trick

Role = Permissions for AWS Services

---

## IAM Security Tools

Your course identifies two important IAM security tools:

1. IAM Credentials Report
2. IAM Access Advisor

---

## IAM Credentials Report

IAM Credentials Report works at the:

Account Level

It provides a report containing:

- IAM users
- Status of their credentials

### Memory Trick

Credentials Report = Account-Wide Credential Report

---

## IAM Access Advisor

IAM Access Advisor works at the:

User Level

It shows:

- Service permissions granted to a user
- When those services were last accessed

This information can help administrators revise permissions.

Example:

User has permission for 10 AWS services

↓

Only uses 3

↓

Review unnecessary permissions

↓

Apply Least Privilege

### Memory Trick

Access Advisor = What Has This User Actually Used?

---

## Credentials Report vs Access Advisor

| Credentials Report | Access Advisor |
|---|---|
| Account level | User level |
| Users and credential status | Service permissions |
| Credential auditing | Last accessed information |

### Memory Trick

Credentials Report = ACCOUNT

Access Advisor = USER

---

## IAM Best Practices

Your course recommends:

- Don't use the root account except when necessary for AWS account setup
- One physical user = one AWS user
- Assign users to groups
- Assign permissions to groups
- Create strong password policies
- Use and enforce MFA
- Use IAM Roles for AWS services
- Use Access Keys for programmatic access
- Audit permissions using IAM security tools
- Never share IAM users
- Never share Access Keys
- Apply least privilege

---

## Shared Responsibility Model for IAM

IAM follows the AWS Shared Responsibility Model.

### AWS Responsibility

Your course identifies AWS as responsible for:

- Infrastructure
- Global network security
- Configuration and vulnerability analysis
- Compliance validation

---

### Customer Responsibility

You are responsible for:

- Managing users
- Managing groups
- Managing roles
- Managing policies
- Enabling MFA
- Rotating keys
- Applying appropriate permissions
- Reviewing access patterns
- Reviewing permissions

### Memory Trick

AWS = Security OF the Cloud

Customer = Security IN the Cloud

---

## IAM vs Organizations

### IAM

Controls:

Access and permissions within AWS.

Think:

Who Can Do What?

### AWS Organizations

Manages:

Multiple AWS accounts.

Think:

How Are My AWS Accounts Organized?

### Memory Trick

IAM = Users & Permissions

Organizations = AWS Accounts

See:

[Organizations](Organizations)

---

## Scenario Questions

A company needs to control what actions users can perform in AWS.

→ IAM

---

A company wants to give users only the permissions required to perform their jobs.

→ Principle of Least Privilege

---

A company wants additional protection if a user's password is stolen.

→ MFA

---

An EC2 instance needs permission to access another AWS service.

→ IAM Role

---

A developer needs to interact with AWS from the command line.

→ AWS CLI + Access Keys

---

An application needs to interact with AWS programmatically.

→ AWS SDK + Access Keys

---

An administrator wants an account-wide report showing IAM users and the status of their credentials.

→ IAM Credentials Report

---

An administrator wants to see which AWS services a user has permission to access and when they were last accessed.

→ IAM Access Advisor

---

A company needs to manage multiple AWS accounts.

→ AWS Organizations

NOT IAM

---

## Don't Confuse These

IAM User = Identity

IAM Group = Collection of Users

IAM Policy = Permissions

IAM Role = Permissions That Can Be Assumed

MFA = Additional Authentication

Access Keys = Programmatic Access

Credentials Report = Account-Level Credential Report

Access Advisor = User-Level Permission Usage

Organizations = Multiple AWS Accounts

---

## Exam Keywords

IAM

Identity

Users

Groups

Roles

Policies

Permissions

Least Privilege

MFA

Access Keys

CLI

SDK

Credentials Report

Access Advisor

Root Account

Global Service

---

## Quick Cheat Sheet

IAM = Who Can Do What?

User = Identity

Group = Collection of Users

Policy = Permissions

Role = Assumable Permissions

Least Privilege = Only What You Need

MFA = Password + Device

Console = Password + MFA

CLI = Access Keys

SDK = Access Keys

Credentials Report = Account Level

Access Advisor = User Level

Root = Don't Use Daily

IAM = Global Service

Organizations = Multiple Accounts
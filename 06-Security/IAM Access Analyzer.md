See also: [IAM](IAM)

See also: [Security Hub](<06-Security/Security Hub.md>)

## What Problem Does It Solve?

Identifies AWS resources that are shared with entities outside your organization or account.

IAM Access Analyzer helps you discover resources that may be accessible externally.

### Memory Trick

Access Analyzer = Who Outside Has Access?

---

## Type

Access Analysis / Security Service

---

## What Is IAM Access Analyzer?

IAM Access Analyzer helps identify:

Resources Shared Externally

This helps you understand when AWS resources can be accessed from outside your intended environment.

Think:

AWS Resources

↓

IAM Access Analyzer

↓

Analyze Access

↓

Identify External Sharing

### Memory Trick

Access Analyzer = Find External Access

---

## External Resource Sharing

The main concept from your course is:

External Sharing

IAM Access Analyzer helps identify which resources are shared externally.

For CCP questions, look for phrases such as:

- Shared externally
- External access
- Resources accessible outside the organization
- Identify external resource sharing

### Memory Trick

Externally Shared Resource?

→ IAM Access Analyzer

---

## IAM Access Analyzer vs IAM Access Advisor

This is an important distinction.

### IAM Access Analyzer

Identifies:

Resources Shared Externally

Think:

Who Outside Can Access This?

### IAM Access Advisor

Shows:

- Service permissions granted to a user
- When those services were last accessed

Think:

What Services Has This User Used?

| Access Analyzer | Access Advisor |
|---|---|
| External resource access | User permission usage |
| Finds externally shared resources | Shows service permissions |
| Security analysis | Helps review permissions |
| Think OUTSIDE access | Think USER activity |

### Memory Trick

Analyzer = External Access

Advisor = User Access History

See:

[IAM](IAM)

---

## IAM Access Analyzer vs IAM Credentials Report

### IAM Access Analyzer

Identifies:

Externally Shared Resources

### IAM Credentials Report

Provides:

Account-Level Credential Information

### Memory Trick

Access Analyzer = External Sharing

Credentials Report = Credential Status

---

## IAM Access Analyzer and Security Hub

Your course identifies IAM Access Analyzer as one of the services that can integrate with:

AWS Security Hub

Basic Idea:

IAM Access Analyzer

↓

Security Finding

↓

Security Hub

↓

Central Security View

### Memory Trick

Access Analyzer Finds

Security Hub Collects

See:

[Security Hub](<06-Security/Security Hub.md>)

---

## Common Use Cases

- Identifying externally shared resources
- Reviewing external access
- Finding unintended resource sharing
- Security analysis

---

## Scenario Questions

A company wants to identify AWS resources that are shared externally.

→ IAM Access Analyzer

---

A security administrator wants to determine which resources can be accessed from outside the organization.

→ IAM Access Analyzer

---

An administrator wants to review which AWS services an IAM user has permission to access and when they were last accessed.

→ IAM Access Advisor

NOT IAM Access Analyzer

---

An administrator wants an account-wide report containing IAM users and the status of their credentials.

→ IAM Credentials Report

NOT IAM Access Analyzer

---

## Don't Confuse These

IAM Access Analyzer = External Resource Sharing

IAM Access Advisor = User Service Access

IAM Credentials Report = Credential Status

IAM Policies = Permissions

### Memory Trick

Analyzer = EXTERNAL

Advisor = USER USAGE

Credentials Report = CREDENTIALS

---

## Exam Keywords

IAM Access Analyzer

External Access

External Sharing

Shared Resources

Access Analysis

Security

---

## Quick Cheat Sheet

Access Analyzer = Find External Access

Access Analyzer = Resources Shared Externally

Access Advisor = User Service Access

Credentials Report = Account-Level Credential Status

External Sharing → Access Analyzer
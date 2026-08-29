## What Problem Does It Solve?

IAM Security Tools help you review AWS account credentials and understand which permissions users actually use.

Your SAA course focuses on two tools:

- IAM Credentials Report
- IAM Access Advisor

### Memory Trick

Credentials Report = ACCOUNT

Access Advisor = USER

---

## IAM Credentials Report

IAM Credentials Report operates at the:

ACCOUNT LEVEL

It generates a report containing:

ALL USERS IN THE ACCOUNT

+

STATUS OF THEIR CREDENTIALS

Think:

AWS Account

↓

Credentials Report

↓

Users + Credential Status

### Memory Trick

Credentials Report = ACCOUNT-WIDE CREDENTIAL CHECK

---

## What Does the Credentials Report Show?

Your course describes it as a report that lists:

- Users in the AWS account
- Status of their various credentials

Think:

WHO HAS CREDENTIALS?

↓

WHAT IS THEIR STATUS?

↓

Credentials Report

---

## IAM Access Advisor

IAM Access Advisor operates at the:

USER LEVEL

It shows:

SERVICE PERMISSIONS GRANTED TO A USER

+

WHEN THOSE SERVICES WERE LAST ACCESSED

Think:

IAM User

↓

Access Advisor

↓

Permissions + Last Access

### Memory Trick

Access Advisor = WHAT DID THIS USER ACTUALLY USE?

---

## Why Is Access Advisor Useful?

Access Advisor information can help you:

REVISE IAM POLICIES

For example:

User has permissions

↓

Some services haven't been accessed

↓

Review those permissions

↓

Revise [[IAM Policies]]

This connects directly to:

LEAST PRIVILEGE

---

## Access Advisor + Least Privilege

Remember from [[IAM Policies]]:

Least Privilege

=

ONLY THE PERMISSIONS REQUIRED

Access Advisor can help identify permissions that may no longer be needed.

Think:

Permissions Granted

↓

Check Last Access

↓

Review Unused Permissions

↓

Revise Policy

### Memory Trick

Access Advisor = CLEAN UP PERMISSIONS

---

## Credentials Report vs Access Advisor

| Tool | Level | Shows | Think |
| --- | --- | --- | --- |
| IAM Credentials Report | Account | Users + credential status | CREDENTIALS |
| IAM Access Advisor | User | Service permissions + last accessed | PERMISSIONS |

---

## The Exam Distinction

### ACCOUNT LEVEL?

→ IAM Credentials Report

### USER LEVEL?

→ IAM Access Advisor

This is the fastest way to separate them.

---

## Scenario Recognition

A security administrator needs a report listing all IAM users in the account and the status of their credentials.

→ IAM Credentials Report

---

A security administrator wants to determine when a user's permitted AWS services were last accessed.

→ IAM Access Advisor

---

A company wants to review a user's permissions and remove permissions that are no longer needed.

→ IAM Access Advisor

↓

Revise [[IAM Policies]]

↓

Apply Least Privilege

---

A company wants an account-level view of users and their credential status.

→ IAM Credentials Report

---

## Exam Traps

Credentials Report ≠ Access Advisor

Credentials Report = ACCOUNT LEVEL

Access Advisor = USER LEVEL

Credentials Report = USERS + CREDENTIAL STATUS

Access Advisor = PERMISSIONS + LAST ACCESSED

Access Advisor can help revise policies

Access Advisor supports Least Privilege

---

## Quick Cheat Sheet

Credentials Report

→ ACCOUNT

→ USERS

→ CREDENTIAL STATUS

Access Advisor

→ USER

→ PERMISSIONS

→ LAST ACCESSED

### Memory Trick

REPORT = ACCOUNT

ADVISOR = USER

---

## Master Memory Trick

Need credential information across the ACCOUNT?

→ CREDENTIALS REPORT

Need to see what a USER has access to and last used?

→ ACCESS ADVISOR

---

## Related Notes

- [[IAM Users and Groups]]
- [[IAM Policies]]
- [[IAM Roles]]
- [[IAM Best Practices]]
- [[IAM Shared Responsibility]]
- [[IAM Comparison]]
- [[SAA IAM Cheat Sheet]]
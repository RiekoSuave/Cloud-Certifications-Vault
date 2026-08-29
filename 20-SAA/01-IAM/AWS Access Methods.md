## What Problem Does It Solve?

AWS provides different methods for humans and applications to interact with AWS resources.

Think:

HOW DO I ACCESS AWS?

↓

Console

CLI

SDK

### Memory Trick

AWS Access = CONSOLE / CLI / SDK

---

## Three Ways to Access AWS

Your course identifies three main access methods:

1. AWS Management Console
2. AWS Command Line Interface (CLI)
3. AWS Software Development Kit (SDK)

Each method uses different credentials.

---

## AWS Management Console

The AWS Management Console provides:

WEB-BASED ACCESS

Your course associates Console access with:

PASSWORD

+

[[MFA]]

Think:

Browser

↓

AWS Management Console

↓

Password + MFA

### Memory Trick

Console = CLICK

---

## AWS Command Line Interface (CLI)

AWS CLI allows you to interact with AWS using:

COMMANDS

from a command-line shell.

Think:

Terminal

↓

AWS CLI

↓

AWS Commands

The CLI is protected using:

ACCESS KEYS

### Memory Trick

CLI = COMMANDS

---

## AWS Software Development Kit (SDK)

AWS SDK allows applications and code to interact with AWS.

Think:

APPLICATION CODE

↓

AWS SDK

↓

AWS SERVICES

Your course associates SDK access with:

ACCESS KEYS

### Memory Trick

SDK = CODE

---

## Access Method Comparison

| Access Method | Think | Course Authentication |
| --- | --- | --- |
| Management Console | Browser / GUI | Password + [[MFA]] |
| CLI | Terminal commands | Access Keys |
| SDK | Application code | Access Keys |

### Master Memory Trick

Console = CLICK

CLI = TYPE

SDK = CODE

---

## Access Keys

Access Keys are generated through the:

AWS CONSOLE

Your course states that:

USERS MANAGE THEIR OWN ACCESS KEYS

Access keys should be treated as:

SECRET

just like passwords.

### Important

DO NOT SHARE ACCESS KEYS.

---

## Access Key ID

Your course compares:

ACCESS KEY ID

to a:

USERNAME

Think:

Access Key ID ≈ Username

---

## Secret Access Key

Your course compares:

SECRET ACCESS KEY

to a:

PASSWORD

Think:

Secret Access Key ≈ Password

### Memory Trick

Access Key ID = WHO

Secret Access Key = SECRET

---

## Access Keys vs Console Password

Don't confuse:

CONSOLE PASSWORD

with

ACCESS KEYS

### Console

Password + [[MFA]]

### CLI

Access Keys

### SDK

Access Keys

---

## CLI vs SDK

### CLI

Think:

HUMAN TYPES COMMANDS

Example concept:

Administrator using a terminal to interact with AWS.

### SDK

Think:

CODE TALKS TO AWS

Example concept:

Application code interacting with AWS services.

### Memory Trick

CLI = HUMAN COMMANDS

SDK = APPLICATION CODE

---

## Scenario Recognition

A systems administrator wants to manage AWS using terminal commands.

→ AWS CLI

---

A developer wants application code to interact with AWS services.

→ AWS SDK

---

A user wants to interact with AWS through a web browser.

→ AWS Management Console

---

A user is accessing AWS through the Management Console.

→ Password + [[MFA]]

---

A user is accessing AWS using the CLI.

→ Access Keys

---

Application code needs to interact with AWS using an AWS programming library.

→ AWS SDK

---

A developer asks whether a Secret Access Key can be shared with another developer.

→ NO

Access keys are secret.

---

## Exam Traps

Console = Password + MFA

CLI = Access Keys

SDK = Access Keys

Access Key ID ≈ Username

Secret Access Key ≈ Password

Access Keys = SECRET

Do NOT share Access Keys

CLI ≠ SDK

CLI = COMMANDS

SDK = CODE

---

## Quick Cheat Sheet

Console = CLICK

CLI = TYPE

SDK = CODE

Console = Password + MFA

CLI = Access Keys

SDK = Access Keys

Access Key ID ≈ USERNAME

Secret Access Key ≈ PASSWORD

Access Keys = DON'T SHARE

---

## Related Notes

- [[MFA]]
- [[IAM Users and Groups]]
- [[IAM Roles]]
- [[IAM Best Practices]]
- [[IAM Security Tools]]
- [[IAM Comparison]]
- [[SAA IAM Cheat Sheet]]
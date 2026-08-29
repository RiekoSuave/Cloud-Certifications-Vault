## What Problem Does It Solve?

Multi-Factor Authentication (MFA) protects AWS accounts by requiring more than just a password to sign in.

Think:

PASSWORD

+

SECURITY DEVICE

↓

MFA

↓

STRONGER ACCOUNT PROTECTION

### Memory Trick

MFA = SOMETHING YOU KNOW + SOMETHING YOU OWN

---

## Why MFA Matters

IAM users can potentially:

- Change AWS configurations
- Access resources
- Delete resources

AWS therefore recommends protecting:

ROOT ACCOUNTS

and

IAM USERS

with MFA.

---

## How MFA Works

MFA combines:

PASSWORD YOU KNOW

+

SECURITY DEVICE YOU OWN

↓

SUCCESSFUL AUTHENTICATION

### Memory Trick

MFA = PASSWORD + DEVICE

---

## Main Benefit

If a password is:

STOLEN

or

HACKED

the password alone is not enough to access the account when MFA is enabled.

Think:

Stolen Password

↓

Still Need MFA Device

↓

Account Better Protected

### Memory Trick

Stolen Password ≠ Stolen Account

---

## Virtual MFA Device

AWS supports:

VIRTUAL MFA DEVICES

Your course gives examples such as:

- Google Authenticator
- Authy

These run on a phone.

### Memory Trick

Virtual MFA = AUTHENTICATOR APP

---

## U2F Security Key

Your course also covers:

UNIVERSAL 2ND FACTOR (U2F)

security keys.

Example:

YubiKey by Yubico

A security key can support multiple:

- Root users
- IAM users

### Memory Trick

U2F = PHYSICAL SECURITY KEY

---

## Hardware Key Fob

AWS also supports:

HARDWARE KEY FOB MFA DEVICES

Your course lists:

Gemalto

as an example third-party provider.

For:

AWS GovCloud (US)

your course lists:

SurePassID

### Memory Trick

Hardware MFA = PHYSICAL TOKEN

---

## MFA Device Comparison

| MFA Type | Course Example | Think |
| --- | --- | --- |
| Virtual MFA | Google Authenticator / Authy | Phone app |
| U2F Security Key | YubiKey | Security key |
| Hardware Key Fob | Gemalto | Physical token |
| GovCloud Hardware Key Fob | SurePassID | GovCloud token |

---

## MFA vs Password Policy

### [[IAM Password Policy]]

Controls:

PASSWORD REQUIREMENTS

Examples:

- Length
- Complexity
- Expiration
- Password reuse

### MFA

Adds:

SECOND AUTHENTICATION FACTOR

### Memory Trick

Password Policy = STRONGER PASSWORD

MFA = ADD ANOTHER FACTOR

---

## AWS Console Access

Your course associates AWS Management Console access with:

PASSWORD

+

MFA

We'll compare this against CLI and SDK authentication in:

[[AWS Access Methods]]

### Memory Trick

Console = Password + MFA

CLI / SDK = Access Keys

---

## Scenario Recognition

A company wants to protect accounts even if employee passwords are stolen.

→ MFA

---

A company wants additional protection for its AWS root account.

→ MFA

---

A company wants employees to authenticate using a mobile authenticator application.

→ Virtual MFA Device

---

A company wants users to authenticate with a physical security key.

→ U2F Security Key

---

A company wants stronger password complexity requirements.

→ [[IAM Password Policy]]

NOT MFA

---

## Exam Traps

MFA ≠ Password Policy

MFA = PASSWORD + DEVICE

Protect root accounts with MFA

Protect IAM users with MFA

Virtual MFA = Authenticator App

U2F = Security Key

Hardware Key Fob = Physical Token

Stolen password alone should not be enough when MFA is enabled

---

## Quick Cheat Sheet

MFA = PASSWORD + DEVICE

Virtual MFA = PHONE APP

U2F = SECURITY KEY

Hardware MFA = PHYSICAL TOKEN

Root Account = PROTECT WITH MFA

IAM Users = PROTECT WITH MFA

Password Policy = PASSWORD RULES

MFA = EXTRA FACTOR

---

## Related Notes

- [[IAM Password Policy]]
- [[IAM Users and Groups]]
- [[AWS Access Methods]]
- [[IAM Best Practices]]
- [[IAM Security Tools]]
- [[IAM Shared Responsibility]]
- [[IAM Comparison]]
- [[SAA IAM Cheat Sheet]]
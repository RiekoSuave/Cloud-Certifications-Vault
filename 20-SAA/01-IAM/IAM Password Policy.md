## What Problem Does It Solve?

IAM Password Policies improve AWS account security by defining **password requirements for IAM users**.

Think:

IAM Users

↓

Password Requirements

↓

Stronger Account Security

### Memory Trick

Password Policy = PASSWORD RULES

---

## Why Use a Password Policy?

Strong passwords provide:

HIGHER SECURITY

AWS allows you to configure password requirements for IAM users.

Think:

Weak Passwords

↓

Higher Risk

Strong Password Policy

↓

Better Security

---

## Minimum Password Length

AWS allows you to define a:

MINIMUM PASSWORD LENGTH

This requires IAM users to create passwords that meet the configured length requirement.

### Memory Trick

Minimum Length = HOW LONG

---

## Character Requirements

A password policy can require specific character types.

These include:

- Uppercase letters
- Lowercase letters
- Numbers
- Non-alphanumeric characters

Think:

UPPERCASE

+

lowercase

+

123

+

!@#

### Memory Trick

Character Requirements = PASSWORD COMPLEXITY

---

## Users Changing Their Own Passwords

AWS can allow:

IAM USERS

↓

CHANGE THEIR OWN PASSWORDS

This allows users to manage their own password changes.

---

## Password Expiration

AWS can require users to:

CHANGE THEIR PASSWORD

↓

AFTER A PERIOD OF TIME

This is called:

PASSWORD EXPIRATION

### Memory Trick

Expiration = CHANGE AFTER TIME

---

## Prevent Password Reuse

AWS can prevent:

PASSWORD RE-USE

This stops users from repeatedly using previous passwords.

### Memory Trick

No Reuse = NEW PASSWORD

---

## Password Policy Controls

| Setting | Purpose |
| --- | --- |
| Minimum password length | Controls password length |
| Character requirements | Controls password complexity |
| User password changes | Allows users to change their passwords |
| Password expiration | Requires password changes after time |
| Prevent password reuse | Prevents reuse of previous passwords |

---

## Password Policy vs MFA

Don't confuse:

[[IAM Password Policy]]

with

[[MFA]]

### Password Policy

Controls:

PASSWORD REQUIREMENTS

### MFA

Adds:

ANOTHER AUTHENTICATION FACTOR

Think:

Password Policy

= Make the PASSWORD stronger

MFA

= Add ANOTHER layer

### Memory Trick

Password Policy = PASSWORD RULES

MFA = PASSWORD + DEVICE

---

## Scenario Recognition

A company wants IAM users to have passwords of a minimum length.

→ IAM Password Policy

---

A company wants passwords to contain uppercase letters, lowercase letters, numbers, and special characters.

→ IAM Password Policy

---

A company wants users to change passwords after a certain amount of time.

→ Password Expiration

---

A company wants to prevent employees from reusing old passwords.

→ Prevent Password Reuse

---

A company wants protection even if a user's password is stolen.

→ [[MFA]]

NOT just a Password Policy

---

## Exam Traps

Password Policy = PASSWORD REQUIREMENTS

Minimum Length = HOW LONG

Character Requirements = COMPLEXITY

Password Expiration = CHANGE AFTER TIME

Prevent Reuse = DON'T REUSE OLD PASSWORDS

Password Policy ≠ MFA

[[MFA]] adds another authentication factor

---

## Quick Cheat Sheet

Password Policy = PASSWORD RULES

Minimum Length = LENGTH

Uppercase / Lowercase / Numbers / Symbols = COMPLEXITY

Expiration = CHANGE PASSWORD

Prevent Reuse = NO OLD PASSWORDS

[[MFA]] = PASSWORD + DEVICE

---

## Related Notes

- [[IAM Users and Groups]]
- [[IAM Policies]]
- [[IAM Policy Structure]]
- [[MFA]]
- [[IAM Best Practices]]
- [[IAM Security Tools]]
- [[IAM Comparison]]
- [[SAA IAM Cheat Sheet]]
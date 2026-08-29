See also: [Organizations](Organizations)

See also: [WAF](06-Security/WAF.md)

See also: [Shield](06-Security/Shield.md)

## What Problem Does It Solve?

Centrally manages security rules across an AWS Organization.

AWS Firewall Manager helps organizations consistently manage security rules across multiple AWS accounts.

### Memory Trick

Firewall Manager = Manage Security Rules Across Accounts

---

## Type

Centralized Security Management

---

## What Is AWS Firewall Manager?

AWS Firewall Manager provides centralized management of security rules across:

AWS Organizations

Your course specifically associates Firewall Manager with services such as:

- AWS WAF
- AWS Shield

Think:

AWS Organization

↓

Multiple AWS Accounts

↓

Firewall Manager

↓

Central Security Rule Management

### Memory Trick

Firewall Manager = Central Security Manager

---

## Multi-Account Security Management

The key concept from your course is:

Organization-Wide Security Management

Instead of managing security rules separately across multiple AWS accounts:

Firewall Manager

↓

Centralizes Management

↓

Across the Organization

### Memory Trick

Many AWS Accounts + Security Rules

→ Firewall Manager

---

## Firewall Manager and AWS Organizations

Firewall Manager is associated with:

AWS Organizations

### AWS Organizations

Manages:

Multiple AWS Accounts

### Firewall Manager

Manages:

Security Rules Across Those Accounts

### Memory Trick

Organizations = Manage Accounts

Firewall Manager = Manage Security Rules Across Accounts

See:

[Organizations](Organizations)

---

## Firewall Manager and WAF

AWS WAF:

Filters incoming web requests based on rules.

Firewall Manager:

Helps centrally manage security rules across an AWS Organization.

### Memory Trick

WAF = Web Firewall

Firewall Manager = Manage Firewall Rules

See:

[WAF](06-Security/WAF.md)

---

## Firewall Manager and Shield

AWS Shield:

Provides DDoS protection.

Firewall Manager:

Helps centrally manage security protections across an AWS Organization.

### Memory Trick

Shield = DDoS Protection

Firewall Manager = Central Management

See:

[Shield](06-Security/Shield.md)

---

## Firewall Manager vs WAF

These are NOT the same service.

| WAF | Firewall Manager |
|---|---|
| Filters web requests | Centrally manages security rules |
| Web application protection | Organization-wide management |
| Security rules are applied to web traffic | Helps manage rules across accounts |

### Memory Trick

WAF = Protection

Firewall Manager = Management

---

## Firewall Manager vs Organizations

### AWS Organizations

Manages:

AWS Accounts

### Firewall Manager

Manages:

Security Rules Across the Organization

### Memory Trick

Organizations = Accounts

Firewall Manager = Security Rules

---

## Common Use Cases

- Centralized security management
- Managing security rules across multiple AWS accounts
- Managing WAF-related security rules across an organization
- Managing Shield-related security protections across an organization

---

## Scenario Questions

A company wants to centrally manage security rules across multiple AWS accounts in an AWS Organization.

→ AWS Firewall Manager

---

A company wants centralized management of WAF and Shield security protections across its organization.

→ AWS Firewall Manager

---

A company wants to filter malicious web requests.

→ AWS WAF

NOT Firewall Manager

---

A company wants DDoS protection.

→ AWS Shield

NOT Firewall Manager

---

A company wants to centrally manage multiple AWS accounts.

→ AWS Organizations

---

## Don't Confuse These

Firewall Manager = Manage Security Rules Across Organization

Organizations = Manage AWS Accounts

WAF = Filter Web Requests

Shield = DDoS Protection

### Memory Trick

Organizations = ACCOUNTS

Firewall Manager = SECURITY RULES

WAF = WEB

Shield = DDoS

---

## Exam Keywords

AWS Firewall Manager

Centralized Security

AWS Organizations

Multiple AWS Accounts

Security Rules

WAF

Shield

---

## Quick Cheat Sheet

Firewall Manager = Central Security Management

Firewall Manager = Manage Security Rules Across Organization

Organizations = Manage Accounts

WAF = Filter Web Requests

Shield = DDoS Protection

Multiple Accounts + Security Rules → Firewall Manager
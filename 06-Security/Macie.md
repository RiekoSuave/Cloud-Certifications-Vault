See also: [Security Hub](<06-Security/Security Hub.md>)

See also: [GuardDuty](06-Security/GuardDuty.md)

## What Problem Does It Solve?

Discovers and protects sensitive data stored in Amazon S3.

Amazon Macie helps identify sensitive information stored inside S3 buckets.

### Memory Trick

Macie = Sensitive Data in S3

---

## Type

Data Security Service

---

## What Is Amazon Macie?

Amazon Macie is a fully managed data security and data privacy service.

Your course emphasizes that Macie uses:

- Machine Learning
- Pattern Matching

to discover sensitive data stored in:

Amazon S3

Think:

S3 Buckets

↓

Macie

↓

Scan Data

↓

Discover Sensitive Information

### Memory Trick

Macie = Scan S3 for Sensitive Data

---

## Sensitive Data Discovery

Macie helps discover sensitive information stored in S3.

The major example from your course is:

Personally Identifiable Information

or:

PII

### Memory Trick

PII in S3?

→ Macie

---

## Personally Identifiable Information (PII)

PII is information that can identify an individual.

For the exam, the important association from your course is:

Sensitive Data / PII

+

Amazon S3

=

Amazon Macie

---

## Machine Learning

Macie uses:

Machine Learning

to help discover sensitive data.

This allows Macie to analyze data stored in S3 and identify information that may need additional protection.

### Memory Trick

Macie = Machine Learning for Sensitive S3 Data

---

## Pattern Matching

Macie also uses:

Pattern Matching

to identify sensitive information.

Think:

S3 Data

↓

Machine Learning + Pattern Matching

↓

Sensitive Data Discovery

---

## Macie and Security Hub

Security Hub can integrate with Macie.

Basic Idea:

Macie

↓

Sensitive Data Finding

↓

Security Hub

↓

Central Security View

### Memory Trick

Macie Finds

Security Hub Collects

See:

[Security Hub](<06-Security/Security Hub.md>)

---

## Macie vs GuardDuty

These services solve different security problems.

### Macie

Finds:

Sensitive Data in S3

### GuardDuty

Finds:

Threats and Suspicious Activity

| Macie | GuardDuty |
|---|---|
| Data security | Threat detection |
| Sensitive data | Suspicious activity |
| S3 | AWS activity/logs |
| PII discovery | Threat discovery |

### Memory Trick

Macie = Sensitive Data

GuardDuty = Threats

See:

[GuardDuty](06-Security/GuardDuty.md)

---

## Macie vs Inspector

### Macie

Looks for:

Sensitive Data in S3

### Inspector

Looks for:

Software Vulnerabilities

### Memory Trick

Macie = Data

Inspector = Vulnerabilities

---

## Macie vs Security Hub

### Macie

Discovers:

Sensitive Data

### Security Hub

Aggregates:

Security Findings

### Memory Trick

Macie = Find Sensitive Data

Security Hub = Collect Findings

---

## Common Use Cases

- Discovering sensitive data
- Finding PII
- Protecting data stored in S3
- Data security
- Data privacy

---

## Scenario Questions

A company wants to discover sensitive data stored in S3 buckets.

→ Amazon Macie

---

A company wants to identify PII stored in Amazon S3.

→ Amazon Macie

---

A company wants a service that uses machine learning and pattern matching to discover sensitive S3 data.

→ Amazon Macie

---

A company wants to detect suspicious API calls and network activity.

→ GuardDuty

NOT Macie

---

A company wants to identify software vulnerabilities in EC2 instances.

→ Inspector

NOT Macie

---

A company wants a centralized dashboard containing findings from multiple security services.

→ Security Hub

NOT Macie

---

## Don't Confuse These

Macie = Sensitive Data in S3

GuardDuty = Threat Detection

Inspector = Vulnerability Detection

Security Hub = Security Findings Aggregation

### Memory Trick

Macie = DATA

GuardDuty = THREATS

Inspector = VULNERABILITIES

Security Hub = FINDINGS

---

## Exam Keywords

Amazon Macie

Sensitive Data

Personally Identifiable Information

PII

Amazon S3

Machine Learning

Pattern Matching

Data Security

Data Privacy

---

## Quick Cheat Sheet

Macie = Sensitive Data in S3

Macie = PII

Macie = Machine Learning + Pattern Matching

Macie → S3

GuardDuty = Threat Detection

Inspector = Vulnerability Scanning

Security Hub = Aggregate Findings

PII + S3 → Macie
## Core Security Services

| Service | Primary Purpose | Memory Shortcut |
| --- | --- | --- |
| IAM | Identity & access management | Who can do what |
| Organizations | Manage multiple AWS accounts | Manage many accounts |
| Control Tower | Automated multi-account governance | Govern accounts |
| IAM Access Analyzer | Find externally shared resources | Who outside has access? |
| CloudTrail | Track API calls/account activity | Who did what? |
| Config | Track configurations & compliance | What changed? |
| GuardDuty | Threat detection | Detect threats |
| Inspector | Vulnerability management | Find vulnerabilities |
| Macie | Find sensitive data/PII in S3 | Sensitive data in S3 |
| Detective | Investigate security issues | Find root cause |
| Security Hub | Aggregate security findings | Central security dashboard |

---

## Network & Application Protection

| Service | Primary Purpose | Memory Shortcut |
| --- | --- | --- |
| Security Groups | Instance/ENI traffic control | Instance firewall |
| NACLs | Subnet traffic control | Subnet firewall |
| AWS Network Firewall | Protect VPC from network attacks | VPC firewall |
| WAF | Filter malicious web requests | Web firewall |
| Shield | DDoS protection | Stop the flood |
| Firewall Manager | Manage security rules across an Organization | Central firewall management |

---

## Encryption & Certificates

| Service | Primary Purpose | Memory Shortcut |
| --- | --- | --- |
| KMS | Encryption key management | Manage keys |
| CloudHSM | Hardware encryption / customer-managed keys | You manage the keys |
| AWS Certificate Manager (ACM) | SSL/TLS certificate management | Manage certificates |

---

## Compliance & Reporting

| Service | Primary Purpose | Memory Shortcut |
| --- | --- | --- |
| Artifact | Compliance reports & agreements | Compliance documents |
| AWS Abuse | Report abusive/illegal use of AWS resources | Report abuse |

---

## High-Value Exam Comparisons

| If You See... | Think... |
| --- | --- |
| Users, groups, roles, policies | IAM |
| Multiple AWS accounts | Organizations |
| Automated multi-account governance | Control Tower |
| Resource shared externally | IAM Access Analyzer |
| API calls / "Who did what?" | CloudTrail |
| Configuration changes / compliance | Config |
| Malicious or suspicious activity | GuardDuty |
| Software vulnerabilities | Inspector |
| Sensitive data / PII in S3 | Macie |
| Root cause of security issue | Detective |
| Central security findings | Security Hub |
| DDoS attack | Shield |
| Malicious HTTP/web request | WAF |
| Network attack against VPC | AWS Network Firewall |
| Security rules across an Organization | Firewall Manager |
| Encryption keys | KMS |
| Hardware encryption + customer manages keys | CloudHSM |
| SSL/TLS certificates | ACM |
| Compliance reports | Artifact |
| Report abusive/illegal AWS resource usage | AWS Abuse |

---

## Security Layer Comparison

| Service | Protection Level | Key Concept |
| --- | --- | --- |
| Security Group | Instance / ENI | Stateful |
| NACL | Subnet | Stateless |
| AWS Network Firewall | VPC / Network | Network attacks |
| WAF | Application / Web | Layer 7 / HTTP |
| Shield | DDoS | Traffic floods |

### Memory Trick

Security Group = Instance

NACL = Subnet

Network Firewall = VPC

WAF = Web

Shield = DDoS

---

## Detection vs Investigation vs Aggregation

| Service | Job |
| --- | --- |
| GuardDuty | Detect threats |
| Inspector | Find vulnerabilities |
| Macie | Find sensitive data |
| Detective | Investigate root cause |
| Security Hub | Aggregate findings |

### Memory Trick

GuardDuty = THREATS

Inspector = VULNERABILITIES

Macie = DATA

Detective = INVESTIGATE

Security Hub = GATHER

---

## IAM vs Organizations vs Control Tower

| Service | Think |
| --- | --- |
| IAM | Users & permissions |
| Organizations | Multiple AWS accounts |
| Control Tower | Automated account governance |
| Firewall Manager | Security rules across accounts |

### Memory Trick

IAM = PEOPLE

Organizations = ACCOUNTS

Control Tower = GOVERNANCE

Firewall Manager = SECURITY RULES

---

## KMS vs CloudHSM vs ACM

| Service | Think |
| --- | --- |
| KMS | Encryption keys |
| CloudHSM | Hardware encryption / customer manages keys |
| ACM | SSL/TLS certificates |

### Memory Trick

KMS = KEYS

CloudHSM = HARDWARE KEYS

ACM = CERTIFICATES

---

## Fast Exam Recognition

IAM → Who can do what?

Organizations → Manage many accounts

Control Tower → Govern accounts

Access Analyzer → External access

CloudTrail → Who did what?

Config → What changed?

GuardDuty → Threats

Inspector → Vulnerabilities

Macie → Sensitive data in S3

Detective → Root cause

Security Hub → Gather findings

Security Group → Instance

NACL → Subnet

Network Firewall → VPC

WAF → Web requests

Shield → DDoS

Firewall Manager → Security rules across accounts

KMS → Encryption keys

CloudHSM → Hardware keys

ACM → Certificates

Artifact → Compliance documents

AWS Abuse → Report abuse
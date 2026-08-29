## What Problem Does It Solve?

[[Route 53 DNSSEC]] protects DNS responses against **DNS spoofing and tampering** by allowing clients to verify that DNS data is authentic and has not been modified.

DNS normally tells a client:

example.com  
↓  
192.0.2.10

But an attacker may attempt to manipulate DNS and return:

example.com  
↓  
Malicious IP Address

DNSSEC adds:

**Cryptographic signatures**

so DNS resolvers can verify the authenticity of DNS responses.

> [!tip] Memory Trick
> **DNSSEC = Signed DNS**
>
> It answers:
>
> **"Can I trust this DNS answer?"**

---

## What DNSSEC Protects Against

DNSSEC helps protect against attacks such as:

- DNS spoofing
- DNS cache poisoning
- DNS response tampering
- Forged DNS records

The goal is:

**DNS Data Integrity + Authentication**

It helps prove:

1. The DNS response came from the expected DNS zone
2. The DNS response was not modified

---

## What DNSSEC Does NOT Do

DNSSEC does **not** encrypt DNS queries or responses.

It provides:

- Authentication
- Integrity

It does NOT provide:

- Confidentiality
- DNS traffic encryption

### Memory Trick

**DNSSEC = Sign**

Not:

**Encrypt**

> [!warning] Exam Trap
> DNSSEC protects the **authenticity and integrity** of DNS data, not its secrecy.

---

## DNSSEC in Route 53

There are two different DNSSEC capabilities to understand:

1. **DNSSEC Signing**
2. **DNSSEC Validation**

These happen on different sides of DNS.

---

## DNSSEC Signing

DNSSEC Signing protects DNS records hosted in:

[[Route 53 Hosted Zones|Public Hosted Zones]]

Route 53 cryptographically signs DNS records so DNSSEC-aware resolvers can verify them.

Architecture:

[[Route 53 Hosted Zones|Public Hosted Zone]]  
↓  
DNS Records  
↓  
DNSSEC Signatures  
↓  
DNS Resolver  
↓  
Verify Signature

### Key Question

> **"How do I cryptographically sign my Route 53 public DNS zone?"**

Think:

**DNSSEC Signing**

---

## DNSSEC Validation

DNSSEC Validation occurs when:

[[20-SAA/06-Route 53/Route 53 Resolver]]

checks DNSSEC signatures returned by DNS servers.

Architecture:

[[EC2]]  
↓  
DNS Query  
↓  
[[20-SAA/06-Route 53/Route 53 Resolver]]  
↓  
DNSSEC Validation  
↓  
Verify DNS Response  
↓  
Return Validated Answer

### Key Question

> **"How can Route 53 Resolver verify that DNS responses have not been tampered with?"**

Think:

**DNSSEC Validation**

---

## Signing vs Validation

This distinction is important for the exam.

### DNSSEC Signing

Occurs on:

**Your DNS zone**

Purpose:

Sign DNS records.

Think:

> **"I own the zone and want to sign it."**

---

### DNSSEC Validation

Occurs during:

**DNS resolution**

Purpose:

Verify DNSSEC signatures.

Think:

> **"I received a DNS response and want to verify it."**

---

## Route 53 DNSSEC Signing Architecture

For a Route 53 Public Hosted Zone:

Public Hosted Zone  
↓  
Zone Signing Key  
↓  
DNS Records Signed  
↓  
DNSSEC-Aware Resolver  
↓  
Signature Verification

The cryptographic system includes:

- Key-Signing Key
- Zone-Signing Key

These are commonly abbreviated:

**KSK**

and:

**ZSK**

---

## Zone-Signing Key — ZSK

The:

**Zone-Signing Key**

is used to sign the DNS records in the hosted zone.

Think:

DNS Records  
↓  
ZSK  
↓  
Signed DNS Records

### Memory Trick

**ZSK = Signs the Zone**

---

## Key-Signing Key — KSK

The:

**Key-Signing Key**

signs the:

**Zone-Signing Key**

Conceptually:

KSK  
↓ signs  
ZSK  
↓ signs  
DNS Records

This creates part of the DNSSEC:

**Chain of Trust**

> [!tip] Memory Trick
> **KSK signs the signer**
>
> **ZSK signs the zone**

---

## KSK and KMS

For Route 53 DNSSEC signing, the Key-Signing Key uses:

[[06-Security/KMS]]

The KMS key must meet specific requirements.

A major exam detail:

> The KMS key must be in **us-east-1**.

This applies even if your resources are primarily located elsewhere.

### Memory Trick

**Route 53 DNSSEC KMS → us-east-1**

---

## KMS Key Type

The KMS key used with Route 53 DNSSEC uses:

**ECC_NIST_P256**

This is an asymmetric cryptographic key type.

For most SAA questions, the highest-value facts are:

- DNSSEC uses KMS for the KSK
- KMS key must be in us-east-1

---

## Chain of Trust

DNSSEC relies on a:

**Chain of Trust**

Conceptually:

DNS Root  
↓  
Top-Level Domain  
↓  
Your Domain  
↓  
Signed DNS Records

Each layer can verify the next layer.

This allows a DNS resolver to determine whether the response can be trusted.

---

## DS Record

After enabling DNSSEC signing, you must establish trust with the parent DNS zone.

This involves a:

**DS Record**

DS stands for:

**Delegation Signer**

The DS record is configured with the domain registrar / parent zone.

Architecture:

Parent DNS Zone  
↓  
DS Record  
↓  
Your DNSSEC-Signed Zone  
↓  
DNS Records

The DS record connects your zone into the DNSSEC:

**Chain of Trust**

> [!tip] Memory Trick
> **DS = Delegation Security Link**

---

## DNSSEC Signing Workflow

Conceptually:

1. Create / configure KMS key
2. Create KSK
3. Enable DNSSEC signing
4. Route 53 signs the hosted zone
5. Create DS record with the parent / registrar
6. DNSSEC chain of trust is established

Architecture:

Registrar / Parent Zone  
↓  
DS Record  
↓  
KSK  
↓  
ZSK  
↓  
Signed DNS Records

---

## Public Hosted Zones

DNSSEC Signing applies to:

[[Route 53 Hosted Zones|Public Hosted Zones]]

It is designed to protect DNS information distributed through the public DNS hierarchy.

### Exam Recognition

If the question says:

> Protect a Route 53 Public Hosted Zone against DNS spoofing or DNS tampering

Think:

**Enable DNSSEC Signing**

---

## DNSSEC Validation with Route 53 Resolver

Route 53 Resolver can perform:

**DNSSEC Validation**

for DNS queries originating from resources in a VPC.

Architecture:

[[EC2]]  
↓  
[[20-SAA/06-Route 53/Route 53 Resolver]]  
↓  
Query DNSSEC-enabled domain  
↓  
Receive Signed Response  
↓  
Validate Signature  
↓  
Return DNS Answer

If validation fails, the DNS response should not be trusted.

---

## Architecture Thinking

### Scenario 1 — Prevent DNS Spoofing

A company hosts:

example.com

in a Route 53 Public Hosted Zone.

Security requirements state that DNS resolvers must be able to verify that DNS records have not been forged or modified.

**Choose → Enable Route 53 DNSSEC Signing**

---

### Scenario 2 — Verify External DNS Responses

EC2 instances perform DNS queries through Route 53 Resolver.

The company wants Route 53 Resolver to verify DNSSEC signatures on DNS responses.

**Choose → DNSSEC Validation**

---

### Scenario 3 — KMS Key Location

A company enables DNSSEC signing for a Route 53 Public Hosted Zone.

Where must the required KMS key be created?

**us-east-1**

Even if workloads run elsewhere.

---

### Scenario 4 — Encrypt DNS Queries

A company wants DNS queries encrypted so observers cannot read them.

Would DNSSEC solve this?

**No.**

DNSSEC provides:

- Authentication
- Integrity

not:

- Confidentiality

---

### Scenario 5 — Establish Parent Trust

A company has enabled DNSSEC signing in Route 53 but needs to connect the signed zone to the DNS hierarchy.

What is required?

**DS Record**

The DS record is placed with the:

**Parent zone / registrar**

to establish the chain of trust.

---

## DNSSEC vs HTTPS

Do not confuse DNSSEC with HTTPS.

### DNSSEC

Protects:

**DNS information**

Provides:

- Authentication
- Integrity

---

### HTTPS

Protects:

**Application communication**

Provides:

- Encryption
- Server authentication
- Data integrity

Architecture:

DNSSEC  
↓  
Trust DNS Answer

HTTPS  
↓  
Secure Application Connection

They solve different layers of the security problem.

---

## DNSSEC vs Route 53 Health Checks

### DNSSEC

Question:

> **Can I trust this DNS answer?**

### [[Route 53 Health Checks]]

Question:

> **Is this endpoint healthy?**

DNSSEC protects:

**DNS authenticity**

Health Checks protect:

**Availability routing decisions**

---

## Scenario Recognition

### Immediately Think DNSSEC When You See

- DNS spoofing
- DNS cache poisoning
- DNS tampering
- DNS authenticity
- DNS integrity
- Cryptographically signed DNS
- KSK
- ZSK
- DS Record
- Chain of trust
- KMS + Route 53
- Verify DNS responses

### Strongest Keyword Pair

> **DNS + Integrity → DNSSEC**

---

## Exam Traps

### Trap 1 — DNSSEC Encrypts DNS

False.

DNSSEC provides:

**Authentication + Integrity**

not confidentiality.

---

### Trap 2 — Signing and Validation Are the Same

False.

**Signing = Create signatures**

**Validation = Verify signatures**

---

### Trap 3 — KSK Signs Every DNS Record Directly

The architecture is:

KSK  
↓  
ZSK  
↓  
DNS Records

Think:

**KSK signs the signer**

---

### Trap 4 — KMS Key Can Be in Any Region

For Route 53 DNSSEC signing, remember:

**KMS key → us-east-1**

---

### Trap 5 — DS Record Goes Inside the Application

False.

The DS record participates in DNS delegation and is configured with the:

**Parent zone / domain registrar**

---

### Trap 6 — DNSSEC Replaces HTTPS

False.

DNSSEC protects DNS.

HTTPS protects application traffic.

Use them for different security layers.

---

## Quick Cheat Sheet

| Feature | DNSSEC |
|---|---|
| DNS Authentication | ✅ |
| DNS Integrity | ✅ |
| DNS Encryption | ❌ |
| Protect Against Spoofing | ✅ |
| Protect Against Cache Poisoning | ✅ |
| Public Hosted Zone Signing | ✅ |
| Resolver Validation | ✅ |
| Key-Signing Key | KSK |
| Zone-Signing Key | ZSK |
| KSK Uses KMS | ✅ |
| KMS Region | us-east-1 |
| Parent Trust | DS Record |
| Chain of Trust | ✅ |

---

## Master Memory Trick

> [!tip] Master Memory Trick
> **DNSSEC = Put a signature on DNS**
>
> It answers:
>
> **"Did this DNS answer really come from who I think it did, and was it changed?"**

Remember the key chain:

**KSK**

↓ signs

**ZSK**

↓ signs

**DNS Records**

And:

**DS Record → Connects trust to parent**

**KMS → Protects KSK**

**KMS Region → us-east-1**

Finally:

> **DNSSEC SIGNING = Sign your zone**
>
> **DNSSEC VALIDATION = Verify someone else's signature**
>
> **DNSSEC ≠ Encryption**

---

## Related Notes

- [[Route 53]]
- [[Route 53 Hosted Zones]]
- [[20-SAA/06-Route 53/Route 53 Resolver]]
- [[Route 53 Records]]
- [[DNS]]
- [[06-Security/KMS]]
- [[HTTPS]]
- [[Route 53 Health Checks]]
- [[Security]]
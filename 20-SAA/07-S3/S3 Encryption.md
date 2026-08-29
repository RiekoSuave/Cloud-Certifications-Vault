## What Problem Does It Solve?

[[S3 Encryption]] protects S3 objects from unauthorized access by encrypting data:

- At rest
- In transit
- Before it even reaches S3

The main SAA question is:

> **"Who should control the encryption keys, and where should encryption happen?"**

There are four major object-encryption approaches:

1. [[S3 SSE-S3]]
2. [[S3 SSE-KMS]]
3. [[S3 SSE-C]]
4. [[S3 Client-Side Encryption]]

> [!tip] Memory Trick
> **Encryption choice = Who owns the key?**
>
> **SSE-S3 → AWS owns it**
>
> **SSE-KMS → KMS manages it**
>
> **SSE-C → Customer provides it**
>
> **Client-Side → Customer encrypts everything**

---

# Encryption at Rest vs Encryption in Transit

These protect data at different stages.

## Encryption at Rest

Protects:

**Objects stored inside S3**

Examples:

- SSE-S3
- SSE-KMS
- SSE-C
- Client-Side Encryption

---

## Encryption in Transit

Protects:

**Data traveling between the client and S3**

Uses:

**HTTPS / TLS**

Architecture:

Client  
↓ HTTPS  
[[S3]]  
↓  
Encrypted Object Storage

### Memory Trick

**At Rest = Sitting in S3**

**In Transit = Moving to/from S3**

---

# Server-Side Encryption

With server-side encryption:

The client sends the object to S3.

Then:

**S3 performs the encryption**

Architecture:

Client  
↓ Upload  
[[S3]]  
↓ Encrypt  
Encrypted Object

The key-management model determines which SSE option is used.

---

# SSE-S3

[[S3 SSE-S3]] uses encryption keys that are:

**Handled, managed, and owned by AWS**

The object is encrypted:

**Server-side**

Encryption algorithm:

**AES-256**

SSE-S3 is enabled by default for:

- New S3 buckets
- New objects

> [!tip] Memory Trick
> **SSE-S3 = S3 handles everything**

---

## SSE-S3 Architecture

Client  
↓ Upload Object  
[[S3]]  
↓  
S3-Owned Encryption Key  
↓  
AES-256 Encryption  
↓  
Encrypted Object

The customer does not manage the underlying encryption key.

### Best Fit

Use SSE-S3 when:

- You need encryption at rest
- AWS-managed keys are acceptable
- You want minimum key-management overhead
- No custom KMS auditing/control is required

---

## SSE-S3 Request Header

The Maarek slides show the header:

`x-amz-server-side-encryption: AES256`

For exam purposes, the bigger point is:

**AES-256 → SSE-S3**

---

# SSE-KMS

[[S3 SSE-KMS]] encrypts S3 objects using keys managed through:

[[06-Security/KMS]]

The object is still encrypted:

**Server-side**

But KMS gives you significantly more control over the key.

Architecture:

Client  
↓ Upload  
[[S3]]  
↓  
[[06-Security/KMS]] Key  
↓  
Encrypted Object

---

## Why Use SSE-KMS?

Major advantages:

- Control over encryption keys
- Key policies
- IAM integration
- Key rotation capabilities
- Audit key usage with [[06-Security/CloudTrail]]

> [!tip] Memory Trick
> **SSE-KMS = Control + Audit**

If the exam emphasizes:

**Auditing key usage**

or:

**Control over encryption keys**

Think:

[[S3 SSE-KMS]]

---

## SSE-KMS Request Header

The Maarek slides show:

`x-amz-server-side-encryption: aws:kms`

Exam recognition:

**aws:kms → SSE-KMS**

---

# SSE-KMS and KMS API Calls

This is a very important SAA architecture detail.

SSE-KMS introduces calls to:

[[06-Security/KMS]]

### Upload

When an object is uploaded:

S3 calls:

**GenerateDataKey**

### Download

When an encrypted object is downloaded:

S3 calls:

**Decrypt**

Architecture:

Upload  
↓  
S3  
↓  
GenerateDataKey  
↓  
KMS

Download  
↓  
S3  
↓  
Decrypt  
↓  
KMS

---

# SSE-KMS Performance Limitation

Because SSE-KMS uses KMS APIs:

S3 workloads can be affected by:

**KMS request quotas**

High-volume S3 workloads may generate large numbers of:

- GenerateDataKey calls
- Decrypt calls

These calls count toward:

**KMS requests-per-second quotas**

If the workload exceeds the quota:

**KMS throttling can occur**

### Architecture Thinking

High S3 request rate  
+  
SSE-KMS  
↓  
Large number of KMS API calls  
↓  
KMS throttling

Possible solution:

**Request a quota increase through Service Quotas**

> [!warning] Exam Trap
> **S3 itself may scale fine while KMS becomes the bottleneck.**

---

# SSE-C

[[S3 SSE-C]] means:

**Server-Side Encryption with Customer-Provided Keys**

The customer manages the encryption keys:

**Outside AWS**

S3 performs the encryption and decryption, but:

> **S3 does NOT store the encryption key you provide.**

---

## SSE-C Architecture

Client  
↓  
Object + Customer Encryption Key  
↓ HTTPS  
[[S3]]  
↓  
Encrypt Object  
↓  
Do Not Store Customer Key

When downloading:

Client  
↓  
Provides Same Key  
↓ HTTPS  
S3  
↓  
Decrypt Object

### Memory Trick

**SSE-C = Customer brings the key every time**

---

# SSE-C Requires HTTPS

This is a major exam rule.

Because the encryption key is sent in request headers:

**HTTPS is mandatory**

You should never send the encryption key over unencrypted HTTP.

> [!warning] Exam Rule
> **SSE-C → HTTPS ONLY**

---

## SSE-C Key Requirement

The customer must provide the encryption key in the HTTP request headers for:

**Every relevant request**

S3 does not retain the key for later.

Therefore:

Upload  
↓  
Provide Key

Download  
↓  
Provide Key Again

---

## Who Manages the SSE-C Key?

The customer is responsible for:

- Generating the key
- Storing the key
- Protecting the key
- Providing the key to S3
- Maintaining the key lifecycle

AWS does not manage this key in KMS.

### Architecture Thinking

If the requirement says:

> **"The company must fully control and manage encryption keys outside AWS, but S3 should perform encryption."**

Choose:

[[S3 SSE-C]]

---

# Client-Side Encryption

[[S3 Client-Side Encryption]] moves the encryption responsibility completely to the client.

The client:

1. Encrypts data before uploading
2. Sends ciphertext to S3
3. Downloads encrypted data
4. Decrypts it locally

Architecture:

Plaintext Object  
↓  
Client Encrypts  
↓  
Encrypted Object  
↓  
[[S3]]

On download:

[[S3]]  
↓  
Encrypted Object  
↓  
Client Decrypts  
↓  
Plaintext

---

## Who Manages Client-Side Encryption?

The customer fully manages:

- Encryption keys
- Encryption process
- Decryption process
- Key lifecycle

S3 never needs the plaintext encryption key.

### Memory Trick

**Client-Side = S3 never sees plaintext before upload**

---

## Client-Side vs SSE-C

These are easy to confuse.

### SSE-C

Client provides the key.

But:

**S3 performs encryption/decryption**

Architecture:

Client  
↓ Object + Key  
S3  
↓ Encrypt

---

### Client-Side Encryption

Client performs:

**Encryption AND decryption**

Architecture:

Client Encrypts  
↓  
Encrypted Object  
↓  
S3

### Master Difference

> **SSE-C = Customer owns key, S3 encrypts**
>
> **Client-Side = Customer owns key AND encrypts**

---

# Encryption in Transit

[[S3]] supports:

- HTTP endpoint
- HTTPS endpoint

### HTTP

Traffic:

**Not encrypted in transit**

### HTTPS

Traffic:

**Encrypted using TLS**

AWS recommends:

**HTTPS**

Most modern clients use HTTPS by default.

---

## HTTPS Is Mandatory with SSE-C

Again, remember:

[[S3 SSE-C]]

requires:

**HTTPS**

because the customer-provided encryption key travels with the request.

---

# Force Encryption in Transit

You can use an:

[[S3 Bucket Policies|S3 Bucket Policy]]

to deny requests that are not using HTTPS.

The key condition is:

`aws:SecureTransport`

Architecture:

Client using HTTPS  
↓  
Allowed

Client using HTTP  
↓  
Bucket Policy Deny  
↓  
Blocked

> [!tip] Memory Trick
> **aws:SecureTransport = Force HTTPS**

---

# Default Encryption

S3 automatically applies:

[[S3 SSE-S3]]

to new objects by default.

This means new objects are encrypted at rest even if the client does not explicitly request encryption.

---

# Default Encryption vs Bucket Policy

This distinction matters.

## Default Encryption

S3 says:

> **"If you upload the object, I will encrypt it."**

---

## Bucket Policy

A bucket policy can say:

> **"I refuse your upload unless you explicitly request the required encryption method."**

Example:

Require:

[[S3 SSE-KMS]]

or:

[[S3 SSE-C]]

and deny uploads without the required encryption header.

---

## Evaluation Order

Important Maarek exam detail:

**Bucket Policies are evaluated before Default Encryption**

So:

Request  
↓  
Bucket Policy  
↓  
Allowed or Denied  
↓  
Default Encryption

### Exam Trap

A bucket may have default SSE-S3 encryption enabled.

But if the bucket policy requires:

**SSE-KMS**

and the request does not include the correct header:

The request can still be:

**Denied**

Default encryption does not override the policy.

---

# Encryption Method Comparison

| Method | Who Manages Key? | Who Encrypts? | KMS | HTTPS Required |
|---|---|---|---|---|
| [[S3 SSE-S3]] | AWS | S3 | ❌ | Recommended |
| [[S3 SSE-KMS]] | KMS / Customer Control | S3 | ✅ | Recommended |
| [[S3 SSE-C]] | Customer outside AWS | S3 | ❌ | ✅ Mandatory |
| [[S3 Client-Side Encryption]] | Customer | Client | Optional | Recommended |

---

# Architecture Thinking

## Scenario 1 — Simplest Encryption

A company needs encryption at rest for S3 objects.

They want:

- Minimal administration
- AWS to manage keys
- No custom key policies

**Choose → [[S3 SSE-S3]]**

---

## Scenario 2 — Audit Encryption Key Usage

A security team needs:

- Encryption at rest
- Control over key permissions
- Audit records showing key usage

**Choose → [[S3 SSE-KMS]]**

Why?

KMS integrates with:

[[06-Security/CloudTrail]]

for key usage auditing.

---

## Scenario 3 — Customer Must Keep Keys Outside AWS

A company must manage its encryption keys on-premises.

They want S3 to perform encryption but do not want AWS to store the keys.

**Choose → [[S3 SSE-C]]**

Remember:

**HTTPS mandatory**

---

## Scenario 4 — S3 Must Never Perform Encryption

A company requires data to be encrypted before it leaves the client.

The client must also handle decryption.

**Choose → [[S3 Client-Side Encryption]]**

---

## Scenario 5 — KMS Throttling

A workload performs enormous numbers of S3 reads and writes using SSE-KMS.

Requests begin getting throttled even though S3 can handle the workload.

Investigate:

**KMS request quotas**

Possible solution:

**Increase KMS quota**

---

## Scenario 6 — Force HTTPS

A company requires every S3 request to use encryption in transit.

**Choose → S3 Bucket Policy using `aws:SecureTransport`**

Deny requests where SecureTransport is false.

---

## Scenario 7 — Require SSE-KMS Uploads

A bucket uses default encryption, but company policy requires every object to use SSE-KMS.

**Choose → Bucket Policy that denies PUT requests without SSE-KMS**

Do not rely only on default SSE-S3 encryption.

---

# SSE-S3 vs SSE-KMS

## SSE-S3

Best for:

- Simple encryption
- Minimal overhead
- AWS-owned keys

## SSE-KMS

Best for:

- Customer control
- Auditing
- Key policies
- Compliance requirements

### Exam Decision

**Simple encryption → SSE-S3**

**Control / Audit → SSE-KMS**

---

# SSE-KMS vs SSE-C

## SSE-KMS

Key managed through:

[[06-Security/KMS]]

AWS infrastructure manages the key service.

---

## SSE-C

Key managed:

**Completely outside AWS**

Customer sends key with each request.

### Exam Decision

**AWS KMS key control → SSE-KMS**

**Customer-held external key → SSE-C**

---

# SSE-C vs Client-Side

## SSE-C

Customer owns key.

S3 encrypts.

## Client-Side

Customer owns key.

Customer encrypts.

### Memory Trick

**C in SSE-C = Customer Key**

**Client-Side = Client Does Everything**

---

# Scenario Recognition

## Immediately Think SSE-S3 When You See

- AWS-managed keys
- AES-256
- Simplest encryption
- Default S3 encryption
- Minimal management

---

## Immediately Think SSE-KMS When You See

- KMS
- Key control
- Audit key usage
- CloudTrail
- Key policies
- GenerateDataKey
- Decrypt
- KMS throttling

---

## Immediately Think SSE-C When You See

- Customer-provided key
- Key managed outside AWS
- S3 must not store key
- HTTPS mandatory
- Key sent with every request

---

## Immediately Think Client-Side Encryption When You See

- Encrypt before upload
- Client encrypts
- Client decrypts
- S3 should only store ciphertext
- Customer controls full encryption lifecycle

---

# Exam Traps

## Trap 1 — SSE-S3 Uses KMS

False.

SSE-S3 uses:

**S3-managed AWS-owned keys**

---

## Trap 2 — SSE-KMS Has No Scaling Considerations

False.

High request volumes can hit:

**KMS quotas**

---

## Trap 3 — SSE-C Stores Your Key

False.

S3 does:

**Not store the customer-provided encryption key**

---

## Trap 4 — SSE-C Can Use HTTP

False.

**HTTPS is mandatory**

---

## Trap 5 — Client-Side Encryption Means S3 Encrypts with Customer Key

False.

That describes:

[[S3 SSE-C]]

Client-Side Encryption means:

**The client encrypts before upload**

---

## Trap 6 — Encryption at Rest Automatically Means Encryption in Transit

False.

Encryption at rest protects:

**Stored objects**

Encryption in transit protects:

**Data moving between the client and S3**

For transport security:

**Use HTTPS / enforce `aws:SecureTransport`**

---

## Trap 7 — Default Encryption Overrides Bucket Policy

False.

Bucket Policy evaluation happens:

**Before Default Encryption**

So a request can be denied before default encryption ever applies.

---

# Quick Cheat Sheet

| Requirement | Best Choice |
|---|---|
| Simplest managed encryption | [[S3 SSE-S3]] |
| AES-256 / AWS-owned keys | [[S3 SSE-S3]] |
| KMS key control | [[S3 SSE-KMS]] |
| Audit key usage | [[S3 SSE-KMS]] |
| Customer key outside AWS | [[S3 SSE-C]] |
| S3 must not store key | [[S3 SSE-C]] |
| Customer encrypts before upload | [[S3 Client-Side Encryption]] |
| Force encrypted transport | HTTPS + `aws:SecureTransport` |
| High SSE-KMS request volume | Watch KMS quotas |
| Default S3 encryption | SSE-S3 |

---

## Master Memory Trick

> [!tip] Master Memory Trick
> Ask:
>
> **"WHO controls the key, and WHO performs encryption?"**
>
> **AWS owns key + S3 encrypts**
>
> → **SSE-S3**
>
> **KMS manages key + S3 encrypts**
>
> → **SSE-KMS**
>
> **Customer owns key + S3 encrypts**
>
> → **SSE-C**
>
> **Customer owns key + Customer encrypts**
>
> → **Client-Side Encryption**

And remember the two killer exam rules:

> **SSE-C = HTTPS mandatory**
>
> **SSE-KMS = KMS quota can become the bottleneck**

Finally:

**At Rest = SSE**

**In Transit = HTTPS**

---

## Related Notes

- [[S3]]
- [[S3 SSE-S3]]
- [[S3 SSE-KMS]]
- [[S3 SSE-C]]
- [[S3 Client-Side Encryption]]
- [[S3 Bucket Policies]]
- [[06-Security/KMS]]
- [[06-Security/CloudTrail]]
- [[S3 Replication]]
- [[S3 Versioning]]
- [[HTTPS]]
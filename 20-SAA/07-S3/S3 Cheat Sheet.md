## S3 Exam Strategy

For SAA questions, do not think of [[S3]] as simply:

**"Object Storage"**

Instead, identify what the architecture needs:

| Requirement | Immediately Think |
|---|---|
| Store objects | [[S3]] |
| Cheap infrequent access | [[S3 Standard-IA]] |
| Cheap infrequent access + Multi-AZ not required | [[S3 One Zone-IA]] |
| Unknown/changing access patterns | [[S3 Intelligent-Tiering]] |
| Archive with retrieval in minutes/hours | [[S3 Glacier Flexible Retrieval]] |
| Lowest-cost long-term archive | [[S3 Glacier Deep Archive]] |
| Automatic transition/deletion | [[S3 Lifecycle Rules]] |
| Protect against accidental overwrite/delete | [[S3 Versioning]] |
| Replicate to another Region | [[S3 Cross-Region Replication]] |
| Replicate within same Region | [[S3 Same-Region Replication]] |
| Replicate existing objects | [[S3 Batch Replication]] |
| Temporary private access | [[S3 Pre-Signed URLs]] |
| Shared bucket with complex permissions | [[S3 Access Points]] |
| Transform object during retrieval | [[S3 Object Lambda]] |
| React to object upload/delete | [[S3 Event Notifications]] |
| Bulk action on existing objects | [[S3 Batch Operations]] |
| Scheduled object listing | [[S3 Inventory]] |
| Organization-wide S3 metrics | [[S3 Storage Lens]] |
| Audit S3 requests | [[S3 Access Logs]] |
| WORM object protection | [[S3 Object Lock]] |
| Immutable Glacier vault policy | [[S3 Glacier Vault Lock]] |
| Requester pays download costs | [[S3 Requester Pays]] |
| Large upload | [[S3 Multipart Upload]] |
| Global long-distance transfer | [[S3 Transfer Acceleration]] |
| Parallel large download | [[S3 Byte-Range Fetches]] |

> [!tip] S3 Master Question
> Before answering an S3 exam question, ask:
>
> **Storage?**
>
> **Security?**
>
> **Replication?**
>
> **Performance?**
>
> **Automation?**
>
> **Cost?**
>
> **Compliance?**

---

## S3 Core Facts

[[S3]] is:

**Object Storage**

Objects are stored inside:

**Buckets**

Each object has:

- Key
- Value
- Metadata
- Optional tags
- Version ID when versioning is enabled

Maximum object size:

**5 TB**

---

## S3 Is Regional

S3 buckets are created in:

**A specific AWS Region**

But bucket names must be:

**Globally unique**

### Memory Trick

**Bucket LOCATION = Regional**

**Bucket NAME = Global**

---

## S3 Storage Classes

### S3 Standard

Use for:

- Frequently accessed data
- Low latency
- High throughput
- General-purpose storage

Architecture:

Frequent Access  
↓  
[[S3 Standard]]

---

### S3 Standard-IA

IA means:

**Infrequent Access**

Use when:

- Data is accessed less frequently
- Multi-AZ resilience is still required
- Retrieval charges are acceptable

Think:

**Infrequent + Multi-AZ**

---

### S3 One Zone-IA

Stores data in:

**One Availability Zone**

Use when:

- Data is infrequently accessed
- Data can be recreated
- Lower cost matters
- Multi-AZ resilience is unnecessary

> [!warning] Exam Trap
> If the AZ is destroyed:
>
> **Data can be lost**

### Memory Trick

**One Zone = One AZ = Cheaper + Less Resilient**

---

## S3 Intelligent-Tiering

Use:

[[S3 Intelligent-Tiering]]

when access patterns are:

**Unknown or unpredictable**

S3 automatically moves objects between access tiers based on usage.

Best clue:

> **"Access patterns are unpredictable."**

### Memory Trick

**Don't know the pattern? Let S3 decide.**

---

## Glacier Storage Classes

### S3 Glacier Instant Retrieval

Think:

**Archive pricing + millisecond retrieval**

Use when:

- Data is rarely accessed
- Immediate retrieval is still required

---

### S3 Glacier Flexible Retrieval

Use for:

**Archive data**

with retrieval options ranging from:

Minutes  
↓  
Hours

Think:

**Archive + Flexible retrieval**

---

### S3 Glacier Deep Archive

Use for:

**Lowest-cost long-term archive**

Retrieval takes:

**Hours**

Best for:

- Regulatory archives
- Long-term backups
- Rarely retrieved records

### Memory Trick

**Deep Archive = Cheapest + Slowest**

---

## Storage Class Decision Tree

Frequent access?  
↓ YES  
[[S3 Standard]]

Unknown access pattern?  
↓ YES  
[[S3 Intelligent-Tiering]]

Infrequent access?  
↓  
Need Multi-AZ?  
↓ YES  
[[S3 Standard-IA]]

Infrequent access?  
↓  
Data can be recreated and one AZ is acceptable?  
↓ YES  
[[S3 One Zone-IA]]

Archive + millisecond retrieval?  
↓ YES  
[[S3 Glacier Instant Retrieval]]

Archive + minutes/hours retrieval?  
↓ YES  
[[S3 Glacier Flexible Retrieval]]

Cheapest long-term archive?  
↓ YES  
[[S3 Glacier Deep Archive]]

---

## S3 Lifecycle Rules

[[S3 Lifecycle Rules]] automate:

**Transitions**

and:

**Expiration**

Example:

S3 Standard  
↓ 30 days  
Standard-IA  
↓ 90 days  
Glacier  
↓ 365 days  
Delete

### Immediately Think Lifecycle When You See

- After X days
- Transition automatically
- Delete automatically
- Old object versions
- Expired delete markers
- Incomplete multipart uploads

> [!tip] Memory Trick
> **Lifecycle = AGE causes ACTION**

---

## S3 Versioning

[[S3 Versioning]] keeps multiple versions of an object.

Example:

report.pdf  
↓  
Version 1  
Version 2  
Version 3

If accidentally overwritten:

Restore:

**Previous Version**

### Delete Marker

Deleting a versioned object normally creates:

**Delete Marker**

The previous object versions remain.

### Memory Trick

**Versioning = Undo Button**

---

## S3 MFA Delete

[[S3 MFA Delete]] adds additional protection against destructive operations.

Requires MFA for certain actions such as:

- Permanently deleting object versions
- Changing versioning state

Think:

**Extra authentication before destructive action**

---

## S3 Replication

Replication requires:

[[S3 Versioning]]

on:

**Source + Destination**

### Cross-Region Replication

[[S3 Cross-Region Replication]]

Source Region  
↓  
Different Region

Use for:

- Disaster recovery
- Compliance
- Lower-latency regional copies
- Cross-account replication

### Memory Trick

**CRR = Cross Region**

### Same-Region Replication

[[S3 Same-Region Replication]]

Source Bucket  
↓  
Same Region  
↓  
Destination Bucket

Use for:

- Log aggregation
- Production/test replication
- Same-region compliance

### Memory Trick

**SRR = Same Region**

---

## Existing Objects + Replication

Normal replication primarily handles objects after replication is configured.

For:

**Existing objects**

think:

[[S3 Batch Replication]]

> [!tip] Exam Pattern
> **Old objects + replication**
>
> → **Batch Replication**

---

## S3 Encryption

Know the major options:

| Encryption | Key Management |
|---|---|
| SSE-S3 | S3-managed keys |
| SSE-KMS | KMS-managed keys |
| DSSE-KMS | Two layers using KMS |
| SSE-C | Customer provides key |
| Client-Side Encryption | Client encrypts before upload |

### SSE-S3

S3 manages:

**Encryption + Keys**

Think:

**S3 handles the key management**

---

### SSE-KMS

Uses:

[[06-Security/KMS]]

Advantages:

- Key control
- Audit through [[06-Security/CloudTrail]]
- Key policies
- Rotation options

Important exam consideration:

**KMS API quotas**

High S3 request rates with SSE-KMS can also generate high KMS API activity.

---

### SSE-C

C means:

**Customer-provided key**

S3 performs:

**Encryption**

but does NOT store:

**The encryption key**

HTTPS is required.

### Memory Trick

**SSE-C = Customer brings the key**

---

### Client-Side Encryption

Client  
↓  
Encrypt Object  
↓  
Upload Ciphertext  
↓  
S3

S3 never receives:

**Plaintext**

### Memory Trick

**Client encrypts BEFORE S3**

---

## Encryption Exam Decision

**Simplest server-side encryption**  
→ SSE-S3

**Control/audit encryption keys**  
→ SSE-KMS

**Customer must provide encryption key**  
→ SSE-C

**S3 must never receive plaintext**  
→ Client-Side Encryption

---

## S3 Bucket Policies

[[S3 Bucket Policies]] are:

**Resource-Based Policies**

They can control:

- Public access
- Cross-account access
- Required encryption
- Allowed principals
- Allowed actions
- Denied actions

### Memory Trick

**IAM Policy = What can this identity do?**

**Bucket Policy = Who can access this bucket?**

---

## S3 Block Public Access

[[S3 Block Public Access]] helps prevent accidental public exposure.

Can be configured at:

- Account level
- Bucket level

> [!tip] Exam Pattern
> **Prevent accidental public S3 exposure**
>
> → **Block Public Access**

---

## S3 CORS

[[S3 CORS]] matters when browser-based applications make:

**Cross-Origin Requests**

Example:

app.example.com  
↓  
Browser  
↓  
assets.example.com

Different Origin  
↓  
CORS Required

### Memory Trick

**Browser + Different Origin = CORS**

---

## S3 Static Website Hosting

[[S3 Static Website Hosting]] can host:

- HTML
- CSS
- JavaScript
- Images

It cannot run:

**Server-side application code**

Think:

Static Website  
↓  
S3

Dynamic Backend  
↓  
Not S3 alone

---

## S3 Pre-Signed URLs

[[S3 Pre-Signed URLs]] provide:

**Temporary access**

to private S3 objects.

GET:

**Temporary Download**

PUT:

**Temporary Upload**

The bucket can remain:

**Private**

### Critical Rule

The URL uses the permissions of:

**The principal that generated it**

> [!tip] Exam Pattern
> **Private S3 + External User + Limited Time**
>
> → **Pre-Signed URL**

---

## S3 Access Points

[[S3 Access Points]] simplify access management when:

**Many applications or teams share one bucket**

Think:

One Bucket  
↓  
Many Doors

Each Access Point gets:

- Dedicated DNS name
- Dedicated policy

### Memory Trick

**Access Point = Separate Door into Same Bucket**

---

## S3 Object Lambda

[[S3 Object Lambda]] transforms objects:

**During retrieval**

Architecture:

Original S3 Object  
↓  
Lambda  
↓  
Modified Response

Use cases:

- Redact PII
- XML → JSON
- Enrich data
- Different views for different applications

### Killer Distinction

**Object CREATED**  
→ Event Notification

**Object REQUESTED**  
→ Object Lambda

---

## S3 Event Notifications

[[S3 Event Notifications]] react when something happens.

Examples:

- ObjectCreated
- ObjectRemoved
- ObjectRestore
- Replication events

Traditional targets:

- [[02-Compute/Lambda]]
- [[SQS]]
- [[SNS]]

### Memory Trick

**Need CODE**  
→ Lambda

**Need BUFFER**  
→ SQS

**Need FAN-OUT**  
→ SNS

---

## S3 + EventBridge

Use:

[[20-SAA/10-Messaging/EventBridge]]

when you need:

- Advanced JSON filtering
- More destination types
- Archive
- Replay
- Complex event routing

### Decision

**Simple S3 event**  
→ Event Notification

**Advanced routing**  
→ EventBridge

---

## S3 Performance

Memorize:

**3,500**

PUT / COPY / POST / DELETE requests per second:

**Per prefix**

**5,500**

GET / HEAD requests per second:

**Per prefix**

### Memory Trick

**3.5K Writes**

**5.5K Reads**

**Per Prefix**

---

## Multiple Prefixes

Different prefixes can scale independently.

Example:

4 prefixes  
×  
5,500 GET/HEAD  
=  
**22,000 GET/HEAD requests per second**

> [!warning] Exam Trap
> The performance number is:
>
> **Per prefix**
>
> NOT:
>
> **Per bucket**

---

## S3 Multipart Upload

[[S3 Multipart Upload]]

Recommended:

**Over 100 MB**

Required:

**Over 5 GB**

Benefits:

- Parallel uploads
- Retry individual parts
- Better large-file performance

### Memory Trick

**100 MB = Recommended**

**5 GB = Required**

---

## S3 Transfer Acceleration

[[S3 Transfer Acceleration]] improves:

**Long-distance S3 transfers**

Architecture:

Global User  
↓  
Nearest AWS Edge Location  
↓  
AWS Global Network  
↓  
S3 Bucket

### Memory Trick

**Far away → Enter AWS sooner**

---

## S3 Byte-Range Fetches

[[S3 Byte-Range Fetches]] parallelize:

**Downloads**

Architecture:

Large Object  
↓  
Range 1 + Range 2 + Range 3 + Range 4  
↓  
Parallel GETs

### Memory Trick

**Multipart = Parallel UPLOAD**

**Byte Range = Parallel DOWNLOAD**

---

## S3 Performance Decision

| Requirement | Technique |
|---|---|
| Very high request throughput | Multiple Prefixes |
| Large upload | Multipart Upload |
| Long-distance transfer | Transfer Acceleration |
| Large + distant upload | Multipart + Transfer Acceleration |
| Large download | Byte-Range Fetches |

---

## S3 Batch Operations

[[S3 Batch Operations]] performs:

**One operation across many existing objects**

Use for:

- Modify metadata
- Copy objects
- Encrypt old objects
- Restore Glacier objects
- Invoke Lambda per object

### Memory Trick

**Existing + Millions + Same Action = BATCH**

---

## S3 Inventory

[[S3 Inventory]] generates:

**Scheduled object reports**

Think:

> **What objects exist?**

Can feed:

[[09-Analytics/Athena]]

and:

[[S3 Batch Operations]]

---

## Inventory + Athena + Batch Operations

This is a major architecture pattern.

[[S3 Inventory]]  
↓  
Find Objects  
↓  
[[09-Analytics/Athena]]  
↓  
Filter Objects  
↓  
[[S3 Batch Operations]]  
↓  
Perform Action

### Memory Trick

**Inventory = FIND**

**Athena = FILTER**

**Batch = FIX**

---

## S3 Storage Lens

[[S3 Storage Lens]] provides:

**Aggregated S3 metrics and insights**

across:

- Organization
- Accounts
- Regions
- Buckets
- Prefixes

Use for:

- Storage trends
- Cost optimization
- Data protection
- Activity metrics
- Status codes

### Killer Distinction

**Inventory = Individual Objects**

**Storage Lens = Aggregated Insights**

---

## S3 Access Logs

[[S3 Access Logs]] record:

**Requests made to S3**

including:

- Authorized requests
- Denied requests

Logs go to:

**Another S3 bucket**

in the:

**Same Region**

> [!warning] Major Exam Trap
> Never send access logs into the same bucket being monitored.
>
> This creates:
>
> **Logging Loop**

### Memory Trick

**Access Logs = Security Camera**

---

## S3 Object Lock

[[S3 Object Lock]] provides:

**WORM**

Write Once, Read Many.

Requires:

[[S3 Versioning]]

### Governance Mode

Protected from most users.

Users with special permissions can override protection.

Think:

**Strong, but bypassable**

### Compliance Mode

Object version cannot be deleted or overwritten during retention.

Even:

**Root user**

cannot bypass it.

Think:

**Absolute lock**

### Legal Hold

Protects an object:

**Indefinitely**

until the hold is removed.

Unlike retention periods:

Legal Hold does not require a fixed expiration date.

---

## S3 Glacier Vault Lock

[[S3 Glacier Vault Lock]] also supports:

**WORM**

But remember the distinction:

**Object Lock**  
→ Locks object versions

**Vault Lock**  
→ Locks the vault retention policy

Once the Vault Lock Policy is locked:

**Cannot change**

**Cannot delete**

### Memory Trick

**Object Lock = Lock FILE**

**Vault Lock = Lock RULEBOOK**

---

## S3 Requester Pays

[[S3 Requester Pays]] changes:

**Who pays**

Bucket Owner:

**Storage**

Requester:

**Requests + Downloads**

### Memory Trick

**Owner stores it**

**Requester moves it**

Important:

Requester Pays does NOT grant:

**Permissions**

---

## S3 Cost Decision Tricks

### Reduce Storage Cost

Think:

- [[S3 Storage Classes]]
- [[S3 Lifecycle Rules]]
- [[S3 Intelligent-Tiering]]

### Reduce Global Transfer Latency

Think:

[[S3 Transfer Acceleration]]

### Stop Paying Other People's Download Costs

Think:

[[S3 Requester Pays]]

### Find Storage Waste

Think:

[[S3 Storage Lens]]

---

## S3 Security Decision Tricks

### Temporary External Access

[[S3 Pre-Signed URLs]]

### Prevent Public Exposure

[[S3 Block Public Access]]

### Complex Shared-Bucket Permissions

[[S3 Access Points]]

### Immutable Object Version

[[S3 Object Lock]]

### Immutable Glacier Retention Policy

[[S3 Glacier Vault Lock]]

### Audit Bucket Requests

[[S3 Access Logs]]

### AWS-Wide API Audit

[[06-Security/CloudTrail]]

---

## S3 Automation Decision Tricks

### Object Uploaded

[[S3 Event Notifications]]

### Object Retrieved and Must Be Modified

[[S3 Object Lambda]]

### Object Reaches Certain Age

[[S3 Lifecycle Rules]]

### Millions of Existing Objects Need Same Action

[[S3 Batch Operations]]

### Existing Objects Need Replication

[[S3 Batch Replication]]

---

## S3 Mega Scenario Recognition

### "Unpredictable access patterns"

→ [[S3 Intelligent-Tiering]]

### "Data can be recreated and only one AZ is required"

→ [[S3 One Zone-IA]]

### "Cheapest long-term archive"

→ [[S3 Glacier Deep Archive]]

### "Move objects automatically after 90 days"

→ [[S3 Lifecycle Rules]]

### "Recover accidentally overwritten object"

→ [[S3 Versioning]]

### "Replicate data to another Region"

→ [[S3 Cross-Region Replication]]

### "Replicate old objects"

→ [[S3 Batch Replication]]

### "User needs private file for 15 minutes"

→ [[S3 Pre-Signed URLs]]

### "Many teams share one bucket"

→ [[S3 Access Points]]

### "Remove PII before returning object"

→ [[S3 Object Lambda]]

### "Run Lambda when file uploaded"

→ [[S3 Event Notifications]]

### "Advanced filtering + event replay"

→ [[20-SAA/10-Messaging/EventBridge]]

### "Upload 10 GB object"

→ [[S3 Multipart Upload]]

### "Users worldwide upload slowly"

→ [[S3 Transfer Acceleration]]

### "Parallelize large download"

→ [[S3 Byte-Range Fetches]]

### "Encrypt millions of old objects"

→ [[S3 Batch Operations]]

### "Generate scheduled list of millions of objects"

→ [[S3 Inventory]]

### "Analyze S3 usage across organization"

→ [[S3 Storage Lens]]

### "Audit who accessed bucket"

→ [[S3 Access Logs]]

### "Object must never be deleted during retention"

→ [[S3 Object Lock]]

### "Glacier retention policy must become immutable"

→ [[S3 Glacier Vault Lock]]

### "Consumers should pay their download costs"

→ [[S3 Requester Pays]]

---

## Biggest S3 Exam Traps

### Trap 1 — Bucket Names Are Regional

False.

Bucket names are:

**Globally unique**

Buckets themselves exist in:

**A Region**

---

### Trap 2 — Versioning Prevents Deletion

False.

Normal deletion creates:

**Delete Marker**

Previous versions remain.

---

### Trap 3 — Replication Works Without Versioning

False.

Replication requires:

**Versioning on source + destination**

---

### Trap 4 — CRR Automatically Replicates All Old Objects

False.

Think:

[[S3 Batch Replication]]

for existing objects.

---

### Trap 5 — Multipart Upload Only Starts at 5 GB

False.

Recommended:

**Over 100 MB**

Required:

**Over 5 GB**

---

### Trap 6 — S3 Request Performance Numbers Are Per Bucket

False.

They are:

**Per prefix**

---

### Trap 7 — Pre-Signed URL Makes Object Public

False.

The object remains:

**Private**

Access is temporarily authorized through the URL.

---

### Trap 8 — Requester Pays Grants Access

False.

Requester Pays controls:

**Billing**

IAM / Bucket Policies control:

**Authorization**

---

### Trap 9 — Object Lambda Reacts to Uploads

False.

Object Lambda:

**Transforms retrieval**

Event Notifications:

**React to events**

---

### Trap 10 — Inventory Modifies Objects

False.

Inventory:

**Reports**

Batch Operations:

**Acts**

---

### Trap 11 — Storage Lens Gives Exact Object Listing

False.

Storage Lens:

**Aggregated metrics**

Inventory:

**Object listing**

---

### Trap 12 — Access Logs Can Be Stored in Same Monitored Bucket

False.

This creates:

**Logging Loop**

---

### Trap 13 — Object Lock and Vault Lock Are Identical

False.

Object Lock:

**Object Versions**

Vault Lock:

**Glacier Vault Policy**

---

## Quick Cheat Sheet

| Exam Clue | Answer |
|---|---|
| Frequent access | S3 Standard |
| Unknown access | Intelligent-Tiering |
| Infrequent + Multi-AZ | Standard-IA |
| Infrequent + One AZ | One Zone-IA |
| Archive + milliseconds | Glacier Instant Retrieval |
| Archive + minutes/hours | Glacier Flexible Retrieval |
| Cheapest archive | Glacier Deep Archive |
| Automatic transition | Lifecycle Rules |
| Recover overwritten file | Versioning |
| Another Region | CRR |
| Same Region | SRR |
| Existing replication | Batch Replication |
| Temporary private access | Pre-Signed URL |
| Shared bucket permissions | Access Points |
| Transform GET response | Object Lambda |
| React to upload | Event Notifications |
| Advanced event routing | EventBridge |
| Large upload | Multipart Upload |
| Long-distance transfer | Transfer Acceleration |
| Parallel download | Byte-Range Fetch |
| Millions of existing objects | Batch Operations |
| Object report | Inventory |
| Organization-wide metrics | Storage Lens |
| Audit S3 requests | Access Logs |
| WORM object | Object Lock |
| WORM vault policy | Glacier Vault Lock |
| Consumer pays download | Requester Pays |

---

## Master Memory Trick

> [!tip] S3 Master Memory Trick
> Think of S3 as a giant warehouse.
>
> **Storage Class**
> → Which shelf?
>
> **Lifecycle**
> → When should the box move?
>
> **Versioning**
> → Keep old copies
>
> **Replication**
> → Copy warehouse contents elsewhere
>
> **Encryption**
> → Lock the box
>
> **Bucket Policy**
> → Who can enter?
>
> **Access Point**
> → Give each team its own door
>
> **Pre-Signed URL**
> → Temporary visitor pass
>
> **Event Notification**
> → Alarm when something happens
>
> **Object Lambda**
> → Modify package on the way out
>
> **Multipart**
> → Ship large package in pieces
>
> **Transfer Acceleration**
> → Use AWS express highway
>
> **Batch Operations**
> → Assembly line for existing boxes
>
> **Inventory**
> → Warehouse clipboard
>
> **Storage Lens**
> → Executive dashboard
>
> **Access Logs**
> → Security camera
>
> **Object Lock**
> → Lock the box
>
> **Vault Lock**
> → Lock the rulebook
>
> **Requester Pays**
> → Customer pays shipping

---

## Final Exam Rapid-Fire

> **AGE → Lifecycle**
>
> **UNKNOWN ACCESS → Intelligent-Tiering**
>
> **ACCIDENTAL DELETE → Versioning**
>
> **ANOTHER REGION → CRR**
>
> **OLD OBJECT REPLICATION → Batch Replication**
>
> **TEMPORARY ACCESS → Pre-Signed URL**
>
> **MANY TEAMS → Access Points**
>
> **TRANSFORM GET → Object Lambda**
>
> **UPLOAD EVENT → Event Notification**
>
> **COMPLEX EVENTS → EventBridge**
>
> **BIG UPLOAD → Multipart**
>
> **FAR-AWAY TRANSFER → Transfer Acceleration**
>
> **BIG DOWNLOAD → Byte Range**
>
> **MILLIONS OF OLD OBJECTS → Batch Operations**
>
> **LIST OBJECTS → Inventory**
>
> **S3 METRICS → Storage Lens**
>
> **AUDIT REQUESTS → Access Logs**
>
> **WORM OBJECT → Object Lock**
>
> **WORM VAULT POLICY → Vault Lock**
>
> **CONSUMER PAYS → Requester Pays**

---

## Related Notes

- [[S3]]
- [[S3 Storage Classes]]
- [[S3 Lifecycle Rules]]
- [[S3 Versioning]]
- [[S3 Replication]]
- [[S3 Cross-Region Replication]]
- [[S3 Same-Region Replication]]
- [[S3 Batch Replication]]
- [[S3 Encryption]]
- [[S3 Bucket Policies]]
- [[S3 Block Public Access]]
- [[S3 CORS]]
- [[S3 Static Website Hosting]]
- [[S3 Pre-Signed URLs]]
- [[S3 Access Points]]
- [[S3 Object Lambda]]
- [[S3 Event Notifications]]
- [[S3 Performance]]
- [[S3 Multipart Upload]]
- [[S3 Transfer Acceleration]]
- [[S3 Byte-Range Fetches]]
- [[S3 Batch Operations]]
- [[S3 Inventory]]
- [[S3 Storage Lens]]
- [[S3 Access Logs]]
- [[S3 Object Lock]]
- [[S3 Glacier Vault Lock]]
- [[S3 Requester Pays]]
- [[09-Analytics/Athena]]
- [[20-SAA/10-Messaging/EventBridge]]
- [[06-Security/CloudTrail]]
- [[CloudFront]]
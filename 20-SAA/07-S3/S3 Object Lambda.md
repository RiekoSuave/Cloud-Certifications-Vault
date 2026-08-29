## What Problem Does It Solve?

[[S3 Object Lambda]] lets you **modify or transform an S3 object as it is being retrieved**, without changing the original object stored in S3.

It solves the problem of:

> **"How can different applications receive different versions of the same S3 object without storing multiple copies?"**

Think:

Original Object in S3  
↓  
[[S3 Object Lambda]]  
↓  
[[02-Compute/Lambda]] transforms response  
↓  
Caller receives modified object

> [!tip] Memory Trick
> **Object Lambda = Change the object on the way OUT**

---

## Core Architecture

The original object stays in:

[[S3]]

Then:

Application  
↓  
S3 Object Lambda Access Point  
↓  
[[02-Compute/Lambda]]  
↓  
Transform Object  
↓  
Return Modified Object

The underlying object in S3 is not necessarily modified.

### Architecture Thinking

Think:

**Store once**

**Transform on retrieval**

---

## One Bucket, Multiple Views

This is the biggest architectural advantage.

Without Object Lambda:

Original Data  
↓  
Create Redacted Copy  
↓  
Create Analytics Copy  
↓  
Create Converted Copy  
↓  
Store Multiple Objects

With Object Lambda:

One Original Object  
↓  
Different Object Lambda Access Points  
↓  
Different transformations

Example:

Original Customer Data  
↓  
├── Redacted View
├── Enriched View
└── Converted View

> [!tip] Memory Trick
> **One Object → Many Views**

---

## Object Lambda Uses Lambda Functions

[[S3 Object Lambda]] uses:

[[02-Compute/Lambda]]

to transform the data before it reaches the caller.

The Lambda function receives the retrieval request and can modify the object.

Examples:

- Remove fields
- Mask sensitive information
- Change formats
- Add information
- Filter content

Architecture:

Original Object  
↓  
Lambda Function  
↓  
Modified Response

---

## Access Point Architecture

The Maarek slides emphasize that Object Lambda is built on top of:

[[S3 Access Points]]

You typically have:

S3 Bucket  
↓  
S3 Access Point  
↓  
S3 Object Lambda Access Point  
↓  
Application

This means you do not need separate buckets for each transformed version.

> [!tip] Architecture Pattern
> **S3 Bucket + Access Point + Object Lambda Access Point**

---

# Use Case — Redacting PII

This is one of the strongest exam scenarios.

Suppose an S3 object contains:

- Customer name
- Email
- Address
- Social Security Number
- Purchase history

The analytics team needs the data but should not see:

**Personally Identifiable Information**

Instead of storing a separate redacted copy:

Original Object  
↓  
[[S3 Object Lambda]]  
↓  
Lambda Redacts PII  
↓  
Analytics Application

The original object remains intact.

---

## Architecture Thinking — PII Redaction

Production Application  
↓  
Original S3 Object

Analytics Application  
↓  
Object Lambda Access Point  
↓  
Redacting Lambda  
↓  
Sanitized Object

### Memory Trick

> **Same object, different audience**
>
> → **Object Lambda**

---

# Use Case — Non-Production Environments

A production S3 object may contain sensitive information.

Developers or testers need the same dataset but without confidential fields.

Instead of creating duplicate sanitized datasets:

Production S3 Object  
↓  
Object Lambda  
↓  
Remove Sensitive Fields  
↓  
Development / Test Environment

This reduces:

- Duplicate storage
- Data synchronization work
- Operational overhead

---

# Use Case — Format Conversion

Another explicit Maarek use case is:

**Data format conversion**

Example:

S3 stores:

XML

Application requires:

JSON

Architecture:

XML Object  
↓  
[[S3 Object Lambda]]  
↓  
[[02-Compute/Lambda]] converts XML → JSON  
↓  
Application receives JSON

The original XML object remains stored in S3.

> [!tip] Memory Trick
> **Store XML, serve JSON → Object Lambda**

---

# Use Case — Data Enrichment

A Lambda function can also enrich an S3 object before returning it.

Example:

Original Object  
↓  
Lambda  
↓  
Fetch Additional Data  
↓  
Add Information  
↓  
Return Enriched Object

Conceptually:

S3 Object  
+  
Database Information  
↓  
Object Lambda  
↓  
Enriched Response

---

# Why Not Store Multiple Copies?

Suppose three applications need three versions of one dataset.

Without Object Lambda:

Original  
+  
Redacted Copy  
+  
Converted Copy  
+  
Enriched Copy

Problems:

- Additional storage cost
- Copies may become inconsistent
- More lifecycle management
- More replication complexity

With Object Lambda:

One Original  
↓  
Transform dynamically

### Architecture Lesson

> **Transform at retrieval instead of maintaining duplicate datasets.**

---

# Object Lambda vs Regular Lambda Trigger

Do not confuse S3 Object Lambda with:

**S3 Event Notification → Lambda**

These solve different problems.

---

## S3 Event Notification + Lambda

Triggered when something happens to an object.

Example:

Object Uploaded  
↓  
[[S3 Event Notifications]]  
↓  
[[02-Compute/Lambda]]  
↓  
Process Object

This happens:

**After an event**

---

## S3 Object Lambda

Runs when an application:

**Retrieves the object**

Example:

Application GET  
↓  
Object Lambda  
↓  
Transform Response

### Memory Trick

**Event Lambda = Something happened**

**Object Lambda = Someone requested the object**

---

# Object Lambda vs S3 Access Points

## [[S3 Access Points]]

Provide:

**Dedicated access paths and policies**

They simplify:

- Permissions
- Network access
- Shared-bucket management

---

## S3 Object Lambda

Adds:

**Data transformation**

to the retrieval path.

### Architecture Relationship

Access Point  
↓  
Controls ACCESS

Object Lambda  
↓  
Transforms DATA

---

# Object Lambda vs S3 Batch Operations

## Object Lambda

Transforms objects:

**On retrieval**

Think:

Real-time response transformation

---

## S3 Batch Operations

Performs operations across:

**Large groups of existing objects**

Think:

Bulk processing

### Exam Decision

**Modify response when requested → Object Lambda**

**Process millions of stored objects → Batch Operations**

---

# Object Lambda vs Creating Another Bucket

Suppose:

Analytics users need redacted objects.

One option:

Original Bucket  
↓  
ETL Job  
↓  
Redacted Bucket

Another option:

Original Bucket  
↓  
Object Lambda  
↓  
Redacted Response

If the requirement emphasizes:

- Avoid duplicate storage
- Transform dynamically
- Same underlying object
- Different consumer views

Choose:

[[S3 Object Lambda]]

---

# Architecture Thinking

## Scenario 1 — Redact Sensitive Information

A data lake stores customer data containing personally identifiable information.

Analytics users must receive the dataset with sensitive fields removed.

The company does not want to maintain another copy.

**Choose → S3 Object Lambda + Redacting Lambda**

---

## Scenario 2 — XML to JSON

An application reads objects from S3.

Objects are stored as XML, but the application requires JSON.

The company does not want to rewrite all stored objects.

**Choose → S3 Object Lambda**

Use Lambda to:

**Convert XML → JSON during retrieval**

---

## Scenario 3 — Different Views for Different Applications

Application A needs original objects.

Application B needs redacted versions.

Application C needs enriched versions.

**Choose → Multiple Object Lambda Access Points**

All can use:

**One underlying S3 bucket**

---

## Scenario 4 — Process Every New Upload

Every new image uploaded to S3 must automatically generate a thumbnail.

**Do NOT choose → S3 Object Lambda**

Choose:

[[S3 Event Notifications]]  
↓  
[[02-Compute/Lambda]]

Why?

The requirement is triggered by:

**Object creation**

not retrieval.

---

## Scenario 5 — Permanently Convert Millions of Existing Objects

A company wants to permanently transform millions of stored objects.

**Do NOT automatically choose → Object Lambda**

Consider:

**S3 Batch Operations**

because the requirement is bulk modification of stored objects rather than dynamic retrieval transformation.

---

# Scenario Recognition

## Immediately Think S3 Object Lambda When You See

- Transform object during retrieval
- Modify S3 response
- Redact PII
- Different views of same object
- XML to JSON
- Enrich object before returning
- Avoid duplicate S3 copies
- Lambda in S3 GET path
- Object Lambda Access Point

### Strongest Exam Pattern

> **"Modify the object before the caller receives it"**
>
> → **S3 Object Lambda**

---

# Exam Traps

## Trap 1 — Object Lambda Modifies the Original Object Automatically

False.

Its core purpose is to:

**Transform the object before returning it to the caller**

The stored original can remain unchanged.

---

## Trap 2 — Separate Bucket Required for Each Transformation

False.

The Maarek architecture specifically emphasizes:

**One S3 bucket**

with:

- S3 Access Points
- Object Lambda Access Points

---

## Trap 3 — Object Lambda Is for Upload Events

False.

That scenario points toward:

[[S3 Event Notifications]]

Object Lambda is about:

**Retrieval-time transformation**

---

## Trap 4 — Object Lambda Replaces S3 Access Points

False.

Object Lambda works:

**On top of S3 Access Points**

---

## Trap 5 — Object Lambda Is Only for PII

False.

Other transformations include:

- XML → JSON
- Data enrichment
- Filtering
- Formatting
- Custom response modification

---

# Quick Cheat Sheet

| Requirement | S3 Object Lambda |
|---|---|
| Transform object during GET | ✅ |
| Lambda Function Used | ✅ |
| Redact PII | ✅ |
| Convert XML → JSON | ✅ |
| Enrich Data | ✅ |
| One Underlying Bucket | ✅ |
| Different Views of Same Object | ✅ |
| Requires Access Point Architecture | ✅ |
| Automatically Modify Original | ❌ |
| Triggered by Object Upload | ❌ |
| Duplicate Bucket Required | ❌ |

---

## Master Memory Trick

> [!tip] Master Memory Trick
> **Object Lambda = Sunglasses for S3**
>
> The object itself stays the same.
>
> Different applications can see it differently depending on the lens.

Remember:

**Original Object**
↓
**Object Lambda**
↓
**Modified View**

Examples:

**PII → Redacted**

**XML → JSON**

**Basic Data → Enriched**

And the killer exam distinction:

> **Upload event → Event Notification + Lambda**
>
> **GET transformation → Object Lambda**

---

## Related Notes

- [[S3]]
- [[S3 Access Points]]
- [[02-Compute/Lambda]]
- [[S3 Event Notifications]]
- [[S3 Batch Operations]]
- [[S3 Bucket Policies]]
- [[S3 Object Lock]]
- [[Data Analytics]]
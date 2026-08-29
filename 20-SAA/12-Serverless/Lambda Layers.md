## What Problem Does It Solve?

[[Lambda Layers]] let you package:

**Shared code and dependencies separately from the main Lambda function code**

This helps reduce:

- Duplicate libraries
- Deployment package size
- Repeated dependency management

Architecture:

Lambda Function  
↓  
Uses Layer  
↓  
Shared Libraries / Dependencies

> [!tip] Memory Trick
> **Layer = Shared Dependency Package**

---

## Core Concept

Without Layers:

Function A  
→ Includes Library X

Function B  
→ Includes Library X

Function C  
→ Includes Library X

Same dependency is packaged:

**Over and over**

With Layers:

Shared Layer  
↓  
├── Function A
├── Function B
└── Function C

This improves:

**Reuse**

---

## What Can a Layer Contain?

A Layer can include:

- Libraries
- Custom runtimes
- SDKs
- Shared utilities
- Configuration files
- Dependencies

Think:

**Reusable supporting code**

rather than:

**Main function business logic**

---

## Why Use Layers?

Layers help when multiple Lambda functions need:

**The same dependency**

Example:

10 Lambda Functions  
↓  
All use:
`pandas`

Instead of packaging `pandas` 10 times:

Create:

**One shared Layer**

---

## Shared Libraries

Example:

Lambda A  
↓  
Shared Logging Layer

Lambda B  
↓  
Shared Logging Layer

Lambda C  
↓  
Shared Logging Layer

This can centralize:

- Logging utilities
- Common validation
- Shared SDKs
- Helper functions

### Memory Trick

**Common Code = Layer**

---

## Deployment Package Separation

A Lambda deployment can be thought of as:

Main Function Code  
+  
Layer(s)

This helps separate:

**Business logic**

from:

**Dependencies**

---

## Layer Versions

Layers support:

**Versioning**

When you update a Layer:

You publish:

**A new Layer Version**

Existing Lambda functions referencing the old version continue using:

**That old Layer version**

until explicitly updated.

### Memory Trick

**Layer Version = Immutable Dependency Snapshot**

---

## Why Layer Versioning Matters

Suppose:

Layer Version 1  
→ Library v1

Layer Version 2  
→ Library v2

Production Lambda:

→ Layer Version 1

Test Lambda:

→ Layer Version 2

This allows:

**Controlled dependency upgrades**

---

## Multiple Layers

A Lambda function can use:

**Multiple Layers**

Example:

Lambda Function  
↓  
├── Logging Layer
├── Database Layer
└── Utility Layer

This can improve modularity.

---

## Layer Order

When multiple layers are used:

Their files are combined into:

**The Lambda execution environment**

For SAA, you usually do not need detailed filesystem behavior.

The important exam concept is:

> **Layers provide reusable code and dependencies**

---

## Layers and Function Code

Do NOT use Layers to avoid writing:

**Application-specific business logic**

The function should still contain:

**Its own logic**

Layers are better for:

**Reusable supporting components**

---

## Layers and Runtime Compatibility

A Layer must be compatible with:

**The Lambda runtime and architecture**

Example:

A Python dependency Layer must match:

**The expected Python environment**

Native libraries may also need compatibility with:

**Lambda's execution environment**

### Exam Thinking

If a library depends on native binaries:

Make sure it is built for:

**The Lambda runtime environment**

---

## Lambda Layers and Custom Runtimes

Layers can also contain:

**Custom runtimes**

This allows Lambda to support languages or runtime behavior beyond:

**Standard managed runtimes**

### Killer Exam Clue

> **Need to package a custom Lambda runtime**
>
> → **Lambda Layer**

---

## Layers vs Container Images

Lambda functions can be packaged in two broad ways:

### ZIP Package

May use:

**Lambda Layers**

### Container Image

Packages:

**Code + dependencies together**

and is stored in:

[[ECR]]

### Memory Trick

**ZIP + Shared Dependencies**
→ Layers

**Container Packaging**
→ ECR Image

---

## Layers vs ECR

### Lambda Layers

Store:

**Reusable function dependencies**

### [[ECR]]

Stores:

**Container images**

These solve different problems.

---

## Layers vs Environment Variables

### Lambda Layer

Stores:

**Code / dependencies**

### [[Lambda Environment Variables]]

Stores:

**Configuration**

### Memory Trick

**LAYER = CODE**

**ENV VAR = CONFIG**

---

## Layers vs Secrets Manager

### Layer

Reusable code

### [[Secrets Manager]]

Sensitive values

Do NOT put secrets inside:

**Layers**

Why?

Layers can be shared across functions and versions.

Secrets should be retrieved securely at:

**Runtime**

---

## Layers vs S3

S3 can store:

**Objects and deployment artifacts**

but Lambda Layers are specifically designed to:

**Attach reusable code/dependencies to Lambda functions**

---

## Layer Sharing

Layers can be shared:

- Across Lambda functions
- Across AWS accounts, depending on permissions

This can help centralize:

**Common organizational dependencies**

---

## Cross-Account Layer Sharing

A Layer can use:

**Resource-based permissions**

to allow another AWS account to use:

**A Layer version**

Architecture:

Account A  
↓  
Shared Layer

Account B  
↓  
Lambda Function  
↓  
Uses Layer

### Exam Pattern

> **Multiple AWS accounts need access to the same Lambda dependency package**
>
> → **Shared Lambda Layer + permissions**

---

## Layer Size Considerations

Layers count toward:

**Lambda deployment package limits**

You cannot use Layers as:

**Unlimited external storage**

For very large application packaging:

Think about:

**Lambda container images**

or another compute service depending on workload.

---

## Why Layers Can Improve Deployment Speed

Suppose only:

**Function business logic**

changes.

If large shared dependencies are stored in a Layer:

The function deployment package can remain:

**Smaller**

This can simplify:

**Deployments**

---

## Layers and CI/CD

A CI/CD pipeline can independently publish:

**Layer versions**

and:

**Function versions**

Example:

Shared Utility Updated  
↓  
Publish Layer Version 4

Application Tested  
↓  
Update Function to Layer Version 4

This enables:

**Controlled dependency management**

---

## Architecture Thinking

### Scenario 1 — Shared Python Library

Twenty Lambda functions use:

**The same Python library**

Choose:

**Lambda Layer**

---

### Scenario 2 — Shared Logging Code

Many functions need:

**The same logging helper**

Choose:

**Lambda Layer**

---

### Scenario 3 — Different Dev/Prod Table Names

Need configuration difference.

Do NOT use:

Layer

Choose:

**Environment Variables**

---

### Scenario 4 — Database Password

Need sensitive credential.

Do NOT use:

Layer

Choose:

[[Secrets Manager]]

---

### Scenario 5 — Custom Runtime

Lambda needs:

**A custom runtime**

Choose:

**Lambda Layer**

---

### Scenario 6 — Large Container-Based Application

Application already uses:

**Container images**

with many dependencies.

Think:

Lambda Container Image  
↓  
[[ECR]]

rather than assuming Layers are required.

---

### Scenario 7 — Dependency Upgrade

Production uses:

Layer Version 2

Test uses:

Layer Version 3

This allows:

**Safe testing before production upgrade**

---

### Scenario 8 — Cross-Account Sharing

A central platform team maintains:

**Approved shared libraries**

for Lambda functions in many AWS accounts.

Think:

**Shared Lambda Layer with resource permissions**

---

## Scenario Recognition

Immediately think:

**Lambda Layers**

when you see:

- Shared dependencies
- Shared libraries
- Reusable code
- Common utility package
- Custom runtime
- Reduce duplicate deployment packages
- Multiple Lambda functions use same dependency

---

## Think Environment Variables When You See

- Configuration
- Table names
- Bucket names
- Environment settings
- Feature flags

---

## Think Secrets Manager When You See

- Passwords
- Credentials
- API keys
- Secret rotation

---

## Think Container Image When You See

- Containerized Lambda package
- Large dependency bundle
- Existing Docker workflow
- ECR image

---

## Exam Traps

### Trap 1 — Layers Store Environment Configuration

❌

Environment Variables:

**Configuration**

Layers:

**Code / Dependencies**

---

### Trap 2 — Layers Are Best for Secrets

❌

Use:

**Secrets Manager**

---

### Trap 3 — Updating a Layer Automatically Changes Every Function Using It

❌

Functions reference:

**Specific Layer Versions**

A new Layer version does not automatically replace old references.

---

### Trap 4 — Layers Are Mutable

❌

Published Layer versions are:

**Immutable**

---

### Trap 5 — Layers Replace Function Code

❌

They supplement:

**The main function code**

---

### Trap 6 — Layers Provide Unlimited Storage

❌

They still count toward:

**Lambda package limits**

---

### Trap 7 — Every Lambda Function Must Use Layers

❌

Use Layers only when:

**Reuse or dependency separation is useful**

---

## Quick Cheat Sheet

| Exam Clue | Answer |
|---|---|
| Shared Dependency | Lambda Layer |
| Shared Library | Lambda Layer |
| Shared Utility Code | Lambda Layer |
| Custom Runtime | Lambda Layer |
| Different Config Values | Environment Variables |
| Secret Password | Secrets Manager |
| Containerized Lambda Package | ECR Container Image |
| Layer Update | New Layer Version |
| Layer Version | Immutable |
| Cross-Account Shared Dependency | Layer Permissions |

---

## Layer vs Environment Variable vs Secret

| Requirement | Feature |
|---|---|
| Shared Code | Lambda Layer |
| Shared Library | Lambda Layer |
| Runtime Configuration | Environment Variable |
| Password / API Key | Secrets Manager |
| Container Image | ECR |

---

## Final Exam Rapid-Fire

> **SHARED LIBRARY**
> → LAMBDA LAYER
>
> **COMMON UTILITY CODE**
> → LAMBDA LAYER
>
> **CUSTOM RUNTIME**
> → LAMBDA LAYER
>
> **CONFIG**
> → ENVIRONMENT VARIABLE
>
> **SECRET**
> → SECRETS MANAGER
>
> **CONTAINER PACKAGE**
> → ECR
>
> **UPDATE DEPENDENCY**
> → NEW LAYER VERSION
>
> **LAYER VERSION**
> → IMMUTABLE
>
> **SHARE DEPENDENCY ACROSS ACCOUNTS**
> → LAYER PERMISSIONS

---

## Master Memory Trick

> [!tip] Lambda Layers Master Memory Trick
> Imagine several workers all need:
>
> **The same toolbox**
>
> Instead of giving every worker:
>
> **A separate identical toolbox**
>
> you provide:
>
> **A shared equipment shelf**
>
> That's:
>
> **LAMBDA LAYER**
>
> The worker still brings:
>
> **Their own job instructions**
>
> That's:
>
> **FUNCTION CODE**

So remember:

> **FUNCTION CODE**
> → Unique Job Logic
>
> **LAYER**
> → Shared Tools
>
> **ENVIRONMENT VARIABLE**
> → Configuration
>
> **SECRETS MANAGER**
> → Secrets
>
> **ECR**
> → Container Image

And the killer SAA clue:

> **"Multiple Lambda functions use the same libraries and dependencies."**
>
> → **Lambda Layers**

---

## Related Notes

- [[Lambda]]
- [[Lambda Environment Variables]]
- [[Lambda Execution Roles]]
- [[Secrets Manager]]
- [[ECR]]
- [[S3]]
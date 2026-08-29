## What Problem Does It Solve?

[[Lambda Environment Variables]] let you store:

**Configuration values outside your function code**

Examples:

- S3 bucket name
- DynamoDB table name
- API endpoint
- Environment name
- Feature flag
- Region-specific configuration

Architecture:

Lambda Function  
↓  
Reads Environment Variable  
↓  
Uses Configuration

> [!tip] Memory Trick
> **Environment Variable = CONFIG, not CODE**

---

## Core Concept

Instead of hardcoding:

`TABLE_NAME = "prod-orders-table"`

inside the function,

you can define:

`TABLE_NAME`

as an environment variable.

Then the same code can run in:

- Development
- Test
- Production

with different configuration values.

---

## Why Environment Variables Matter

They help separate:

**Application logic**

from:

**Deployment configuration**

Example:

Same Lambda Code  
↓  
Different Environment Variables  
↓

Dev  
→ `orders-dev`

Test  
→ `orders-test`

Prod  
→ `orders-prod`

### SAA Principle

> **Keep environment-specific values outside the code when practical**

---

## Common Uses

Environment variables are useful for:

- Resource names
- URLs
- Configuration flags
- Log levels
- Application modes
- Deployment settings

Examples:

`ENVIRONMENT=prod`

`LOG_LEVEL=INFO`

`TABLE_NAME=Orders`

`BUCKET_NAME=processed-images`

---

## Runtime Access

Lambda code can read environment variables during execution.

Example concept:

Application Code  
↓  
Read `TABLE_NAME`  
↓  
Use DynamoDB Table

The function does not need the resource name:

**Hardcoded into source code**

---

## Environment Variables Are Version-Specific

Lambda environment variables are associated with:

**A function version configuration**

When you publish a Lambda version:

That version's configuration becomes:

**Immutable**

This includes its:

**Environment-variable configuration**

### Memory Trick

**Version = Code + Configuration Snapshot**

---

## Environment Variables and Aliases

[[Lambda]] aliases point to:

**Published versions**

Example:

`prod`  
↓  
Version 5

Version 5 includes:

- Code
- Environment configuration

If you update environment variables in `$LATEST`:

That does NOT silently modify:

**Previously published versions**

---

## Encryption at Rest

Lambda environment variables are encrypted:

**At rest**

using:

**AWS KMS**

Lambda can use an AWS-managed key by default, and you can use:

**A customer managed KMS key**

when additional control is required.

### Killer Exam Clue

> **Need control over the KMS key used to encrypt Lambda environment variables**
>
> → **Use a customer managed KMS key**

---

## Environment Variables and KMS

Architecture:

Environment Variable  
↓  
Encrypted at Rest  
↓  
[[06-Security/KMS]]

If a customer managed key is used:

IAM and key-policy permissions must allow:

**The required encryption/decryption operations**

---

## Sensitive Values

Environment variables can technically contain:

**Sensitive information**

but for secrets such as:

- Database passwords
- API keys
- Tokens
- Credentials

prefer:

[[Secrets Manager]]

or:

Systems Manager Parameter Store

depending on requirements.

### SAA Principle

> **Configuration belongs in environment variables**
>
> **Secrets belong in a secrets-management service**

---

## Why Not Hardcode Secrets?

Bad:

Lambda Code  
↓  
`password = "SuperSecret123"`

Problems:

- Secret stored with code
- Harder rotation
- Higher exposure risk
- Poor operational practice

Better:

Lambda  
↓  
Execution Role  
↓  
Secrets Manager  
↓  
Retrieve Secret

---

## Environment Variables vs Secrets Manager

### Environment Variables

Best for:

- Non-sensitive configuration
- Resource names
- Feature flags
- URLs
- Runtime settings

### [[Secrets Manager]]

Best for:

- Passwords
- Database credentials
- API keys
- Secrets requiring rotation

### Memory Trick

**ENV VAR = CONFIG**

**SECRETS MANAGER = SECRET**

---

## Environment Variables vs Parameter Store

Systems Manager Parameter Store can also hold:

**Configuration values**

including:

- Plain text parameters
- Encrypted SecureString values

Use Parameter Store when configuration should be:

- Centrally managed
- Shared across applications
- Retrieved dynamically

### Exam Thinking

Simple per-function configuration:

→ Environment Variable

Centralized reusable configuration:

→ Parameter Store

Managed secret rotation:

→ Secrets Manager

---

## Dynamic Configuration

Environment variables are loaded into:

**The Lambda execution environment**

If a configuration value changes frequently and the application needs:

**The newest value without function configuration updates**

consider retrieving it dynamically from:

- Parameter Store
- AppConfig
- Secrets Manager

depending on the requirement.

---

## Environment Variable Updates

Changing environment variables updates:

**Function configuration**

This may cause Lambda to create:

**New execution environments**

with the updated configuration.

Existing warm environments are eventually replaced.

### Exam Concept

Do NOT treat environment variables as:

**A real-time distributed configuration database**

---

## Environment Variables + Deployment Stages

Example:

One codebase  
↓  
Multiple Lambda Functions

`orders-dev`  
Environment:
`TABLE=OrdersDev`

`orders-prod`  
Environment:
`TABLE=OrdersProd`

This provides:

**Environment separation**

without duplicating application code.

---

## Environment Variables + SAM / CloudFormation

Environment variables can be defined through:

**Infrastructure as Code**

such as:

- CloudFormation
- AWS SAM

This helps make deployments:

**Repeatable and consistent**

---

## Environment Variables + CI/CD

CI/CD pipeline:

Code  
↓  
Build  
↓  
Deploy Lambda  
↓  
Set Environment Variables

This allows different environments to receive:

**Different configuration automatically**

---

## Environment Variables + Execution Role

Environment variables define:

**What resource or configuration to use**

The execution role defines:

**Whether Lambda is allowed to access it**

Example:

Environment Variable:

`BUCKET_NAME=my-reports`

Execution Role:

Allows:

`s3:GetObject`

on:

`my-reports`

Both pieces matter.

### Memory Trick

**ENV VAR = WHERE**

**IAM ROLE = WHETHER YOU'RE ALLOWED**

---

## Example — DynamoDB Table

Environment Variable:

`TABLE_NAME=Orders`

Lambda code reads:

`TABLE_NAME`

then calls:

DynamoDB

Execution Role must also allow:

Required DynamoDB actions.

---

## Example — S3 Bucket

Environment Variable:

`OUTPUT_BUCKET=processed-images`

Lambda uses:

That bucket name

Execution Role allows:

`s3:PutObject`

Environment variable does NOT grant:

**Permission**

---

## Environment Variables Do Not Provide IAM Access

This is an exam trap.

Setting:

`BUCKET_NAME=private-bucket`

does NOT mean Lambda can:

**Access that bucket**

You still need:

**Execution Role permissions**

---

## Environment Variables and Logging

Be careful not to log:

**Sensitive environment-variable values**

into CloudWatch Logs.

Example:

Avoid:

`print(DB_PASSWORD)`

because logs may be accessible to:

**Other operators or systems**

---

## Lambda Layers vs Environment Variables

These solve different problems.

### Lambda Layers

Store:

**Shared code/dependencies**

### Environment Variables

Store:

**Configuration**

### Memory Trick

**LAYER = CODE**

**ENV VAR = CONFIG**

---

## Versions and Configuration

When publishing a version:

Lambda captures configuration such as:

- Environment variables
- Memory
- Timeout
- Code

The published version is:

**Immutable**

This helps provide:

**Repeatable deployments**

---

## Aliases and Environment Separation

A Lambda alias can point to:

**A specific version**

Example:

`prod`  
→ Version 10

`test`  
→ Version 11

Each version may contain:

**Different environment configuration**

This can help support:

**Controlled releases**

---

## Architecture Thinking

### Scenario 1 — Different Table Names

Same Lambda code runs in:

- Dev
- Prod

Each environment uses a different DynamoDB table.

Choose:

**Environment Variables**

---

### Scenario 2 — Database Password

Lambda needs:

**Database credentials**

Do NOT primarily use a plaintext environment variable.

Choose:

[[Secrets Manager]]

---

### Scenario 3 — Centralized Configuration

Many applications need:

**The same configuration value**

and administrators want to update it centrally.

Think:

**Parameter Store / AppConfig**

rather than duplicating environment variables everywhere.

---

### Scenario 4 — Encrypt Config with Custom Key

Security requires control over:

**The encryption key for Lambda environment variables**

Choose:

**Customer Managed KMS Key**

---

### Scenario 5 — Environment Variable Set but S3 Access Fails

`BUCKET_NAME` is correct.

Lambda receives:

AccessDenied.

Problem:

**Environment variable does not grant permissions**

Check:

**Execution Role**

---

### Scenario 6 — Rotate API Key

A third-party API key must be:

**Rotated securely**

Think:

[[Secrets Manager]]

rather than manually replacing:

**Hardcoded or plain configuration**

---

### Scenario 7 — Immutable Production Version

Production alias points to:

Version 7.

Someone changes `$LATEST` environment variables.

Does Version 7 change?

**No**

Published versions are:

**Immutable**

---

## Scenario Recognition

Immediately think:

**Lambda Environment Variables**

when you see:

- Function configuration
- Different dev/prod values
- Bucket name
- Table name
- Endpoint
- Feature flag
- Runtime configuration
- Avoid hardcoding non-secret config

---

## Think Secrets Manager When You See

- Password
- Credential
- API key
- Secret rotation
- Sensitive token

---

## Think Parameter Store / AppConfig When You See

- Central configuration
- Shared configuration
- Dynamic configuration
- Application configuration management

---

## Exam Traps

### Trap 1 — Environment Variables Grant AWS Permissions

❌

They provide:

**Configuration**

IAM provides:

**Authorization**

---

### Trap 2 — Hardcode Environment-Specific Values in Code

Poor design.

Use:

**Environment Variables**

---

### Trap 3 — Environment Variables Are Always Best for Secrets

❌

For managed secrets:

Think:

[[Secrets Manager]]

---

### Trap 4 — Published Version Environment Variables Can Be Edited

❌

Published Lambda versions are:

**Immutable**

---

### Trap 5 — Changing `$LATEST` Changes Old Versions

❌

Published versions remain:

**Unchanged**

---

### Trap 6 — Environment Variables Replace Parameter Store

❌

Parameter Store can provide:

**Centralized dynamic configuration**

---

### Trap 7 — KMS Encryption Means Anyone Can Read the Variables

❌

Access still depends on:

- IAM
- KMS permissions
- Function configuration access

---

### Trap 8 — Lambda Layers Store Runtime Configuration

❌

Layers:

**Dependencies**

Environment Variables:

**Configuration**

---

## Quick Cheat Sheet

| Exam Clue | Answer |
|---|---|
| Function Configuration | Environment Variables |
| Different Dev/Prod Values | Environment Variables |
| Bucket/Table Name | Environment Variable |
| Secret Password | Secrets Manager |
| API Key Rotation | Secrets Manager |
| Central Shared Config | Parameter Store / AppConfig |
| Environment Variable Encryption | KMS |
| Custom Encryption Key | Customer Managed KMS Key |
| Config Grants AWS Access | ❌ Use Execution Role |
| Published Version Config | Immutable |
| Shared Code | Lambda Layer |

---

## Config vs Secret Decision

Need to store:

**Bucket name**
→ Environment Variable

**Table name**
→ Environment Variable

**Feature flag**
→ Environment Variable / AppConfig

**Database password**
→ Secrets Manager

**Rotating API key**
→ Secrets Manager

**Central shared application parameter**
→ Parameter Store / AppConfig

---

## IAM + Config Shortcut

> **WHAT RESOURCE?**
> → Environment Variable
>
> **CAN I ACCESS IT?**
> → Execution Role
>
> **IS IT SECRET?**
> → Secrets Manager
>
> **WHO ENCRYPTS IT?**
> → KMS

---

## Final Exam Rapid-Fire

> **CONFIG OUTSIDE CODE**
> → ENVIRONMENT VARIABLES
>
> **DEV VS PROD TABLE NAME**
> → ENVIRONMENT VARIABLES
>
> **PASSWORD**
> → SECRETS MANAGER
>
> **ROTATING SECRET**
> → SECRETS MANAGER
>
> **CENTRAL CONFIG**
> → PARAMETER STORE / APPCONFIG
>
> **ENCRYPT ENV VARS**
> → KMS
>
> **CUSTOM KMS CONTROL**
> → CUSTOMER MANAGED KEY
>
> **ENV VAR SAYS BUCKET NAME**
> → DOES NOT GRANT ACCESS
>
> **AWS ACCESS**
> → EXECUTION ROLE
>
> **PUBLISHED VERSION**
> → IMMUTABLE
>
> **SHARED DEPENDENCY**
> → LAMBDA LAYER

---

## Master Memory Trick

> [!tip] Lambda Environment Variables Master Memory Trick
> Imagine Lambda is a worker receiving a sticky note before starting.
>
> The sticky note says:
>
> **"Use the OrdersProd table."**
>
> or:
>
> **"Write files to processed-images."**
>
> That's:
>
> **ENVIRONMENT VARIABLE**
>
> But the sticky note does NOT give the worker:
>
> **Permission to enter the storage room**
>
> That's:
>
> **EXECUTION ROLE**
>
> And you should not write:
>
> **The company safe combination**
>
> on the sticky note.
>
> Put that in:
>
> **SECRETS MANAGER**

So remember:

> **ENVIRONMENT VARIABLE**
> → CONFIG
>
> **EXECUTION ROLE**
> → PERMISSION
>
> **SECRETS MANAGER**
> → SECRET
>
> **KMS**
> → ENCRYPTION
>
> **LAYER**
> → SHARED CODE

And the killer SAA clue:

> **"The same Lambda code must use different resource names in development and production without changing the code."**
>
> → **Lambda Environment Variables**

---

## Related Notes

- [[Lambda]]
- [[Lambda Execution Roles]]
- [[Lambda Layers]]
- [[Secrets Manager]]
- [[06-Security/KMS]]
- [[S3]]
- [[04-Databases/DynamoDB]]
- [[07-Monitoring/CloudWatch]]
- [[IAM]]
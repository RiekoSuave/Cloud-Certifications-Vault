## What Problem Does It Solve?

[[Cognito]] provides:

**User identity, authentication, and authorization for applications**

It helps applications handle:

- User sign-up
- User sign-in
- Password management
- Social identity providers
- SAML/OIDC federation
- Temporary AWS credentials
- Token-based application access

> [!tip] Memory Trick
> **Cognito = Identity for application users**
>
> Think:
>
> **WHO IS THE USER?**
> → Cognito

---

## Core Concept

Cognito has two major components:

1. **User Pools**
2. **Identity Pools**

These solve:

**Different identity problems**

### Master Memory Trick

**User Pool = Authenticate Users**

**Identity Pool = Give AWS Credentials**

---

# Cognito User Pools

A:

**User Pool**

is a:

**User directory**

for application users.

It handles:

- Sign-up
- Sign-in
- Passwords
- MFA
- Account recovery
- User attributes
- Token issuance

Architecture:

User  
↓  
Cognito User Pool  
↓  
Authenticate  
↓  
JWT Tokens  
↓  
Application

### Killer Exam Clue

> **Need user registration and login for a web/mobile application**
>
> → **Cognito User Pool**

---

## User Pool Tokens

After successful authentication, Cognito can issue:

**JWT tokens**

Important token types include:

- ID Token
- Access Token
- Refresh Token

---

## ID Token

The:

**ID Token**

contains information about:

**The authenticated user**

Examples:

- Username
- Email
- User attributes

Think:

> **WHO IS THIS USER?**

---

## Access Token

The:

**Access Token**

is used to authorize access to:

**Protected application resources**

Think:

> **WHAT IS THIS USER ALLOWED TO ACCESS?**

---

## Refresh Token

The:

**Refresh Token**

can be used to obtain:

**New ID and access tokens**

without requiring the user to:

**Sign in again immediately**

---

## Token Memory Trick

> **ID TOKEN**
> → WHO YOU ARE
>
> **ACCESS TOKEN**
> → WHAT YOU CAN ACCESS
>
> **REFRESH TOKEN**
> → GET NEW TOKENS

---

# User Pool + API Gateway

A common architecture:

User  
↓  
Cognito User Pool  
↓  
JWT  
↓  
[[API Gateway]]  
↓  
[[Lambda]]

API Gateway validates:

**The user's token**

before allowing access to:

**The backend**

### Killer Exam Clue

> **Authenticate web/mobile users before they call a serverless API**
>
> → **Cognito User Pool + API Gateway**

---

# Hosted UI

Cognito can provide a:

**Hosted UI**

for authentication.

This can support:

- Sign-in
- Sign-up
- Password reset
- Federated identity providers

The application does not have to build:

**Every login screen from scratch**

---

# MFA

User Pools can support:

**Multi-Factor Authentication**

Examples can include:

- SMS
- Authenticator applications

### Exam Thinking

> **Application users require MFA**
>
> → **Cognito User Pool**

---

# Password Policies

User Pools can enforce:

**Password policies**

such as:

- Minimum length
- Complexity requirements

This centralizes:

**User authentication rules**

---

# Account Recovery

Cognito can support:

**Account recovery**

for users through configured mechanisms.

This reduces the amount of:

**Custom identity code**

the application must maintain.

---

# User Attributes

A User Pool can store:

**User profile attributes**

Examples:

- Email
- Phone number
- Name
- Custom attributes

---

# Social Identity Providers

Cognito can federate application users through providers such as:

- Google
- Facebook
- Apple

Architecture:

User  
↓  
Social Provider  
↓  
Cognito User Pool  
↓  
Application

### Killer Exam Clue

> **Allow users to sign in with social accounts**
>
> → **Cognito User Pool Federation**

---

# Enterprise Federation

Cognito can integrate with enterprise identity providers using standards such as:

- SAML
- OpenID Connect

Architecture:

Corporate IdP  
↓  
Cognito  
↓  
Application

### Exam Pattern

> **Employees should sign into an application using the company's existing identity provider**
>
> → **Cognito federation**

---

# Cognito Identity Pools

An:

**Identity Pool**

provides:

**Temporary AWS credentials**

to application users.

Architecture:

User  
↓  
Authenticate  
↓  
Cognito Identity Pool  
↓  
Temporary AWS Credentials  
↓  
AWS Services

### Killer Exam Clue

> **Application user needs temporary direct access to AWS resources**
>
> → **Cognito Identity Pool**

---

# Identity Pool Use Case

Suppose a mobile application needs users to upload directly to:

[[S3]]

Architecture:

User  
↓  
Authentication  
↓  
Identity Pool  
↓  
Temporary AWS Credentials  
↓  
S3

This can eliminate the need to proxy every upload through:

**Your backend server**

---

# Identity Pool + IAM Roles

Identity Pools map users to:

**IAM Roles**

The role determines:

**What AWS resources the user can access**

Example:

Authenticated Users Role  
↓  
Allows:

`s3:PutObject`

to:

`user-uploads/*`

### Memory Trick

**Identity Pool = AWS Credentials**

**IAM Role = AWS Permissions**

---

# Authenticated vs Unauthenticated Identities

Identity Pools can support:

- Authenticated identities
- Unauthenticated guest identities

This enables applications to grant different permissions to:

**Signed-in users**

versus:

**Guests**

---

# Authenticated Role

Signed-in user  
↓  
Identity Pool  
↓  
Authenticated IAM Role  
↓  
AWS Resources

Permissions can be:

**More extensive**

than guest access.

---

# Guest Access

Unauthenticated user  
↓  
Identity Pool  
↓  
Guest IAM Role  
↓  
Limited AWS Access

Example:

Guest can:

**Read public content**

but cannot:

**Upload or modify data**

---

# User Pool vs Identity Pool

This is the biggest Cognito distinction.

## User Pool

Provides:

**Authentication**

Think:

- User directory
- Sign-up
- Sign-in
- JWT tokens

## Identity Pool

Provides:

**AWS credentials**

Think:

- Temporary credentials
- IAM roles
- Direct AWS service access

### Master Memory Trick

> **USER POOL**
> → WHO ARE YOU?
>
> **IDENTITY POOL**
> → HERE ARE AWS CREDENTIALS

---

# User Pool + Identity Pool Together

They can work together.

Architecture:

User  
↓  
User Pool  
↓  
Authenticate  
↓  
JWT Token  
↓  
Identity Pool  
↓  
Temporary AWS Credentials  
↓  
AWS Service

This is a very important architecture.

### Example

Mobile User  
↓  
User Pool Login  
↓  
Identity Pool  
↓  
Temporary Credentials  
↓  
S3 Upload

---

# User Pool Alone

Use User Pool alone when the application only needs:

**Authentication into an API/application**

Example:

User  
↓  
User Pool  
↓  
API Gateway  
↓  
Lambda

The user does NOT need:

**Direct AWS credentials**

---

# Identity Pool Alone

An Identity Pool can work with:

**External identity providers**

and exchange verified identities for:

**Temporary AWS credentials**

But for application user directories and managed sign-up/sign-in:

Think:

**User Pools**

---

# Cognito vs IAM

This distinction is important.

## IAM

Best for:

- AWS employees
- Administrators
- AWS workloads
- AWS service identities

## Cognito

Best for:

- Web application customers
- Mobile application users
- Large-scale external user populations

### Killer Shortcut

**AWS workforce identity**
→ IAM / IAM Identity Center

**Application customer identity**
→ Cognito

---

# Cognito vs IAM Identity Center

[[IAM Identity Center]] is designed primarily for:

**Workforce access to AWS accounts and applications**

Cognito is designed primarily for:

**Application end users**

### Memory Trick

**Identity Center = Employees**

**Cognito = Customers**

---

# Cognito vs Lambda Authorizer

### Cognito

Provides:

**Managed user authentication**

### Lambda Authorizer

Provides:

**Custom authorization logic**

Use Lambda Authorizer when:

- Custom tokens
- Legacy auth
- Custom authorization rules

are required.

---

# Cognito vs API Keys

API Keys do NOT provide:

**User authentication**

Cognito does.

### Memory Trick

**API Key = Usage Meter**

**Cognito = User Identity**

---

# Cognito + API Gateway Security

Architecture:

User  
↓  
Cognito  
↓  
Token  
↓  
API Gateway  
↓  
Lambda

This separates:

**Authentication**

from:

**Application business logic**

---

# Cognito + S3

A direct-access architecture:

User  
↓  
Cognito User Pool  
↓  
Identity Pool  
↓  
Temporary AWS Credentials  
↓  
[[S3]]

This can support:

**Direct browser/mobile uploads**

without exposing:

**Permanent AWS credentials**

---

# Cognito + DynamoDB

Architecture:

User  
↓  
Cognito  
↓  
Temporary Credentials  
↓  
[[DynamoDB]]

IAM conditions can potentially restrict:

**Which items a user can access**

based on application identity.

### Exam Pattern

> **Users should directly access only their own DynamoDB records**
>
> → **Cognito Identity Pool + Fine-Grained IAM**

---

# Temporary Credentials

Identity Pools use:

**Temporary AWS credentials**

rather than:

**Permanent IAM access keys**

This is a major security advantage.

### SAA Principle

> **Never embed long-term AWS credentials inside mobile or browser applications**

---

# Why Permanent Credentials Are Dangerous

Bad architecture:

Mobile App  
↓  
Hardcoded AWS Access Key

Problems:

- Credentials can be extracted
- Difficult rotation
- Broad compromise risk
- Long-lived access

Better:

Mobile App  
↓  
Cognito  
↓  
Temporary Credentials

---

# Cognito Groups

User Pools can organize users into:

**Groups**

Examples:

- Admin
- Premium
- Standard

Groups can help support:

**Application authorization**

and can be represented in:

**Token claims**

---

# Lambda Triggers

Cognito can invoke:

[[Lambda]]

at various points in authentication workflows.

Examples can include:

- Customize sign-up
- Validate users
- Modify token claims
- Custom authentication flows

### Exam Concept

> **Cognito authentication flows can be customized with Lambda triggers**

---

# Pre Sign-Up Trigger

Can run before:

**User registration completes**

Possible uses:

- Validate registration
- Auto-confirm trusted users
- Apply custom signup logic

---

# Post Confirmation Trigger

Can run after:

**User confirmation**

Example:

New User Confirmed  
↓  
Lambda  
↓  
Create application profile

---

# Pre Token Generation Trigger

Can customize:

**Token claims**

before tokens are issued.

This can support:

**Application-specific authorization data**

---

# Cognito User Pool Security

Important security features include:

- MFA
- Password policies
- Account recovery
- Token-based authentication
- Federation
- Advanced security capabilities depending on configuration

---

# Token Expiration

JWT tokens have:

**Expiration periods**

Applications should not assume:

**Tokens remain valid indefinitely**

Refresh tokens can help obtain:

**New tokens**

---

# Authentication vs Authorization

Cognito primarily helps answer:

> **Who is this user?**

Authorization still depends on:

**What the user is allowed to do**

Possible authorization layers include:

- API Gateway authorizers
- IAM roles
- Application logic
- Resource policies

---

# Architecture Thinking

## Scenario 1 — Mobile User Sign-In

Need:

- Sign-up
- Sign-in
- Password reset
- MFA

Choose:

**Cognito User Pool**

---

## Scenario 2 — User Calls API

Authenticated users need to access:

API Gateway.

Choose:

User Pool  
↓  
JWT  
↓  
API Gateway

---

## Scenario 3 — User Uploads Directly to S3

Mobile users should upload files directly to:

S3

without backend proxying.

Choose:

User Pool  
↓  
Identity Pool  
↓  
Temporary AWS Credentials  
↓  
S3

---

## Scenario 4 — Guest Access

Unauthenticated visitors should read:

**Public application assets**

but not upload.

Choose:

**Identity Pool with guest role**

---

## Scenario 5 — Social Login

Users should sign in using:

Google.

Choose:

**Cognito Federation**

---

## Scenario 6 — Corporate Login

Employees accessing an application should authenticate using:

**Existing SAML identity provider**

Choose:

**Cognito Federation**

---

## Scenario 7 — Direct DynamoDB Access

Mobile application users need temporary credentials allowing them to:

**Read only their own records**

Choose:

**Identity Pool + IAM Role Conditions**

---

## Scenario 8 — API Keys

Application currently uses API keys to identify users.

Need:

**Real user authentication**

Do NOT rely on API keys.

Choose:

**Cognito**

---

## Scenario 9 — AWS Administrator

Employee needs access to:

**AWS Management Console**

Do NOT choose Cognito.

Think:

**IAM Identity Center / IAM**

---

# Scenario Recognition

Immediately think:

**Cognito User Pool**

when you see:

- Sign-up
- Sign-in
- Mobile users
- Web users
- User directory
- MFA
- JWT
- Social login
- Application authentication

---

## Immediately Think Identity Pool When You See

- Temporary AWS credentials
- Direct S3 access
- Direct DynamoDB access
- IAM roles for application users
- Guest AWS access

---

## Think Both When You See

- Authenticate application user
- Then give user direct AWS service access

Architecture:

**User Pool → Identity Pool**

---

# Exam Traps

## Trap 1 — User Pools Give AWS Credentials

❌

User Pools primarily provide:

**Authentication + tokens**

Identity Pools provide:

**Temporary AWS credentials**

---

## Trap 2 — Identity Pools Are the Main User Directory

❌

That is:

**User Pools**

---

## Trap 3 — Cognito Is for AWS Administrators

❌

Cognito is mainly for:

**Application users**

---

## Trap 4 — API Keys Replace Cognito

❌

API keys:

**Meter usage**

Cognito:

**Authenticates users**

---

## Trap 5 — Mobile Apps Should Store IAM Access Keys

❌

Use:

**Cognito Identity Pools + temporary credentials**

---

## Trap 6 — User Pool and Identity Pool Are Competing Services

❌

They often work:

**Together**

---

## Trap 7 — Cognito Automatically Decides Every Application Authorization Rule

❌

Authentication and authorization are:

**Separate concerns**

---

# Quick Cheat Sheet

| Exam Clue | Answer |
|---|---|
| User Sign-Up / Sign-In | User Pool |
| Managed User Directory | User Pool |
| JWT Tokens | User Pool |
| MFA for App Users | User Pool |
| Social Login | User Pool Federation |
| SAML/OIDC App Federation | User Pool |
| Temporary AWS Credentials | Identity Pool |
| Direct S3 Access | Identity Pool |
| Direct DynamoDB Access | Identity Pool |
| Guest AWS Access | Identity Pool |
| App Auth + AWS Credentials | User Pool + Identity Pool |
| AWS Workforce | IAM Identity Center |
| Custom API Auth Logic | Lambda Authorizer |

---

# Token Cheat Sheet

| Token | Purpose |
|---|---|
| ID Token | User Identity |
| Access Token | Resource/API Authorization |
| Refresh Token | Obtain New Tokens |

---

# User Pool vs Identity Pool

| Requirement | User Pool | Identity Pool |
|---|---:|---:|
| Sign-Up | ✅ | ❌ |
| Sign-In | ✅ | ❌ |
| User Directory | ✅ | ❌ |
| JWT Tokens | ✅ | ❌ Primary |
| Temporary AWS Credentials | ❌ | ✅ |
| IAM Role Mapping | ❌ | ✅ |
| Guest AWS Access | ❌ | ✅ |
| Direct AWS Service Access | ❌ | ✅ |

---

# Decision Tree

Need:

**Application user login?**

→ User Pool

Need:

**Temporary AWS credentials?**

→ Identity Pool

Need both?

→ User Pool + Identity Pool

Need:

**AWS employee access?**

→ IAM Identity Center

Need:

**Custom API token logic?**

→ Lambda Authorizer

---

# Final Exam Rapid-Fire

> **USER SIGN-UP**
> → USER POOL
>
> **USER SIGN-IN**
> → USER POOL
>
> **JWT**
> → USER POOL
>
> **MFA**
> → USER POOL
>
> **SOCIAL LOGIN**
> → USER POOL FEDERATION
>
> **TEMP AWS CREDENTIALS**
> → IDENTITY POOL
>
> **DIRECT S3 ACCESS**
> → IDENTITY POOL
>
> **GUEST AWS ACCESS**
> → IDENTITY POOL
>
> **AUTHENTICATE + AWS ACCESS**
> → USER POOL + IDENTITY POOL
>
> **EMPLOYEE AWS ACCESS**
> → IAM IDENTITY CENTER
>
> **CUSTOM API AUTH**
> → LAMBDA AUTHORIZER
>
> **PERMANENT KEYS IN MOBILE APP**
> → WRONG

---

## Master Memory Trick

> [!tip] Cognito Master Memory Trick
> Imagine entering an amusement park.
>
> First you go to:
>
> **THE MEMBERSHIP DESK**
>
> They verify who you are:
>
> **USER POOL**
>
> You receive:
>
> **TOKENS**
>
> Then you want access to special AWS-controlled areas.
>
> You go to:
>
> **THE CREDENTIAL DESK**
>
> They give you temporary access credentials:
>
> **IDENTITY POOL**
>
> Those credentials map to:
>
> **IAM ROLES**

So remember:

> **USER POOL**
> → AUTHENTICATE
>
> **IDENTITY POOL**
> → AWS CREDENTIALS
>
> **IAM ROLE**
> → AWS PERMISSIONS
>
> **ID TOKEN**
> → WHO YOU ARE
>
> **ACCESS TOKEN**
> → WHAT YOU CAN ACCESS
>
> **REFRESH TOKEN**
> → NEW TOKENS

And the killer SAA question:

> **"Does the application need to authenticate the user, or give the user AWS credentials?"**
>
> Authenticate user  
> → **User Pool**
>
> Give AWS credentials  
> → **Identity Pool**
>
> Need both  
> → **User Pool + Identity Pool**

---

## Related Notes

- [[API Gateway]]
- [[API Gateway Security]]
- [[Lambda]]
- [[DynamoDB]]
- [[S3]]
- [[IAM]]
- [[IAM Identity Center]]
- [[Lambda Authorizer]]
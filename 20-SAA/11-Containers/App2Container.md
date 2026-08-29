## What Problem Does It Solve?

App2Container is a:

**Command-line tool that helps modernize existing applications into containers**

It helps organizations take applications currently running on:

- EC2
- On-premises servers
- Virtual machines

and convert them into:

**Containerized applications**

that can be deployed to services such as:

- [[ECS]]
- [[EKS]]

> [!tip] Memory Trick
> **App2Container = Existing App → Container**
>
> Think:
>
> **MODERNIZE an existing application**

---

## Core App2Container Idea

Many organizations have traditional applications running directly on:

**Servers**

Example:

Legacy Application  
↓  
EC2 / On-Premises Server

They want to modernize the application without:

**Manually rebuilding the entire container architecture**

App2Container helps analyze and package the application into:

**Containers**

Architecture:

Existing Application  
↓  
App2Container  
↓  
Container Image  
↓  
ECS / EKS

---

## What Applications Does It Target?

App2Container is designed primarily for existing:

- Java applications
- .NET applications

running on:

- Linux
- Windows

The key exam concept is not memorizing every supported runtime.

The important idea is:

> **Existing application running on servers → Container modernization**

---

## Discovery and Analysis

App2Container can:

**Inventory and analyze applications**

running on servers.

Conceptually:

Server  
↓  
App2Container  
↓  
Discover Application  
↓  
Analyze Dependencies  
↓  
Create Containerization Artifacts

This reduces:

**Manual discovery work**

during modernization.

---

## Containerization

After analyzing an application, App2Container helps create:

**Container artifacts**

needed to package the application.

Conceptually:

Existing App  
↓  
Analysis  
↓  
Container Configuration  
↓  
Container Image

This allows the application to move from:

**Server-based deployment**

to:

**Container-based deployment**

---

## Container Image

The resulting application can be packaged into:

**A container image**

which can then be stored in:

[[ECR]]

Architecture:

Existing Application  
↓  
App2Container  
↓  
Container Image  
↓  
ECR

### Memory Trick

**App2Container = CREATE**

**ECR = STORE**

---

## App2Container + ECR

A common modernization flow:

Application on Server  
↓  
App2Container  
↓  
Container Image  
↓  
[[ECR]]  
↓  
ECS / EKS

ECR becomes:

**The container image registry**

for the modernized application.

---

## App2Container + ECS

After containerization, the application can be deployed to:

[[ECS]]

Architecture:

Legacy Application  
↓  
App2Container  
↓  
Container Image  
↓  
ECR  
↓  
ECS

### Killer Exam Clue

> **Convert an existing server-based application into containers and deploy it to ECS**
>
> → **App2Container**

---

## App2Container + EKS

Applications can also be modernized for deployment to:

[[EKS]]

Architecture:

Existing Application  
↓  
App2Container  
↓  
Container Image  
↓  
ECR  
↓  
EKS

Use EKS when:

**Kubernetes is required**

---

## Deployment Artifacts

App2Container can help generate artifacts needed for:

**Container deployment**

This reduces the amount of:

**Manual infrastructure configuration**

required during modernization.

The generated artifacts can support deployment to:

- ECS
- EKS

---

## Infrastructure as Code

App2Container can help generate:

**Infrastructure-as-Code artifacts**

for the containerized application.

This helps automate:

**Deployment infrastructure**

instead of requiring everything to be configured manually.

### SAA Principle

> **Modernization should be repeatable and automated where possible.**

---

## CI/CD Integration

App2Container can also help create artifacts that support:

**CI/CD pipelines**

Conceptually:

Existing Application  
↓  
App2Container  
↓  
Containerized Application  
↓  
CI/CD Pipeline  
↓  
ECR  
↓  
ECS / EKS

This helps transition applications toward:

**Modern deployment practices**

---

## Application Modernization

App2Container is primarily a:

**Modernization tool**

rather than:

**A runtime service**

This distinction matters.

### App2Container

Helps:

**Containerize applications**

### ECS / EKS

Actually:

**Run and orchestrate containers**

### ECR

Stores:

**Container images**

---

## App2Container Is Not a Runtime

App2Container does NOT:

**Run production containers**

Instead:

App2Container  
↓  
Creates Containerized Application

Then:

ECS / EKS  
↓  
Runs Application

### Memory Trick

**App2Container = CONVERT**

**ECR = STORE**

**ECS/EKS = RUN**

---

## App2Container vs ECS

### App2Container

Purpose:

**Modernize existing application into containers**

### [[ECS]]

Purpose:

**Run and orchestrate containers**

### Killer Exam Shortcut

Existing app needs containerization:

→ App2Container

Containers already exist and need orchestration:

→ ECS

---

## App2Container vs EKS

### App2Container

Converts:

**Existing applications into containers**

### [[EKS]]

Runs:

**Kubernetes workloads**

They can work together:

Existing App  
↓  
App2Container  
↓  
Container  
↓  
EKS

---

## App2Container vs ECR

### App2Container

Creates:

**Containerization artifacts**

### [[ECR]]

Stores:

**Container images**

Architecture:

App2Container  
↓  
ECR

---

## App2Container vs Fargate

### App2Container

Think:

**Modernization**

### [[Fargate]]

Think:

**Serverless container compute**

Example:

Existing Application  
↓  
App2Container  
↓  
Container Image  
↓  
ECR  
↓  
ECS  
↓  
Fargate

---

## App2Container vs App Runner

This distinction can be easy to confuse.

### App2Container

Think:

**Convert existing application into containers**

### [[App Runner]]

Think:

**Deploy a web application/API with minimal infrastructure management**

### Memory Trick

**App2Container = CONVERT**

**App Runner = SERVE**

---

## App2Container vs Migration Hub

Migration services may help:

**Track or coordinate migrations**

App2Container specifically focuses on:

**Application containerization**

### Exam Shortcut

Need:

**Migration tracking**
→ Migration Hub

Need:

**Convert existing app to containers**
→ App2Container

---

## App2Container vs Application Migration Service

Application Migration Service focuses on:

**Migrating servers to AWS**

Think:

Server  
↓  
AWS

App2Container focuses on:

**Modernizing the application into containers**

Think:

Application  
↓  
Container

### Memory Trick

**Migration Service = MOVE SERVER**

**App2Container = MODERNIZE APP**

---

## Rehost vs Replatform / Modernize

This distinction is useful for SAA.

### Rehost

Move application largely unchanged.

Example:

On-Premises Server  
↓  
EC2

Think:

**Lift and shift**

---

### Container Modernization

Existing application  
↓  
App2Container  
↓  
Container  
↓  
ECS / EKS

Think:

**Modernize deployment architecture**

### Killer Exam Clue

> **Company wants to move away from server-based application deployment and adopt containers**
>
> → **App2Container**

---

## Modernization Architecture

Traditional:

Users  
↓  
Load Balancer  
↓  
EC2 Application Servers

Modernized:

Users  
↓  
Load Balancer  
↓  
ECS / EKS  
↓  
Containerized Application

App2Container helps with:

**The transformation step**

between the two architectures.

---

## Why Containerize?

Containerization can provide:

- Deployment consistency
- Application portability
- Easier scaling
- Improved CI/CD
- Better resource utilization
- Modern orchestration

The exam may frame App2Container as a way to:

**Accelerate application modernization**

---

## Source Application Stays Conceptually Intact

The goal is generally not:

**Rewrite the entire application from scratch**

Instead, App2Container helps:

**Package the existing application into containers**

This can reduce:

**Modernization effort**

compared with a complete rewrite.

---

## App2Container Workflow

A simplified workflow:

### Step 1 — Discover

Identify:

**Running applications**

---

### Step 2 — Analyze

Determine:

- Application components
- Dependencies
- Runtime configuration

---

### Step 3 — Containerize

Generate:

**Container artifacts**

---

### Step 4 — Store

Push image to:

[[ECR]]

---

### Step 5 — Deploy

Deploy to:

- [[ECS]]
- [[EKS]]

---

## Workflow Memory Trick

> **DISCOVER**
> ↓
> **ANALYZE**
> ↓
> **CONTAINERIZE**
> ↓
> **STORE**
> ↓
> **DEPLOY**

---

## Architecture Thinking

### Scenario 1 — Existing Java Application

A company has:

**Java applications running on EC2**

It wants to:

- Containerize them
- Minimize manual modernization effort
- Deploy to ECS

Choose:

**App2Container**

---

## Scenario 2 — Existing .NET Application

A company has:

**Traditional .NET applications**

and wants to modernize them into:

**Containers**

Choose:

**App2Container**

---

## Scenario 3 — Move Server Without Modernizing

A company simply wants to:

**Move an existing server to AWS**

with minimal changes.

Do NOT automatically choose App2Container.

Think:

**Application Migration Service**

---

## Scenario 4 — Container Already Exists

A company already has:

**Docker images**

and needs to run them.

Do NOT choose App2Container.

Think:

- ECS
- EKS
- App Runner

depending on requirements.

---

## Scenario 5 — Store Container Image

The application has already been containerized.

Need:

**Private AWS image registry**

Choose:

[[ECR]]

not:

App2Container

---

## Scenario 6 — Kubernetes Required

Existing application must be:

1. Containerized
2. Deployed using Kubernetes

Choose:

App2Container  
↓  
ECR  
↓  
[[EKS]]

---

## Scenario 7 — Serverless Container Compute

Existing application should be:

1. Containerized
2. Run without EC2 management

Possible architecture:

App2Container  
↓  
ECR  
↓  
ECS  
↓  
[[Fargate]]

---

## Scenario 8 — Simple New Web Application

Developers have a new web application and simply want:

**Source code → managed web service**

App2Container is probably unnecessary.

Think:

[[App Runner]]

---

## Scenario Recognition

Immediately think:

**App2Container**

when you see:

- Existing application
- Legacy application
- Java / .NET
- Running on servers
- Containerize
- Modernize to containers
- Move application to ECS
- Move application to EKS
- Generate containerization artifacts

---

## Do Not Think App2Container When You See

- Already containerized
- Need container orchestration
- Need image storage
- Need Kubernetes management
- Need simple web hosting
- Lift-and-shift server migration

Those point toward:

- ECS
- EKS
- ECR
- App Runner
- Application Migration Service

depending on requirements.

---

## Exam Traps

### Trap 1 — App2Container Runs Containers

False.

It helps:

**Containerize applications**

ECS / EKS:

**Run containers**

---

## Trap 2 — App2Container Stores Container Images

False.

[[ECR]] stores:

**Container images**

---

## Trap 3 — App2Container Is a Container Orchestrator

False.

[[ECS]] and [[EKS]] provide:

**Container orchestration**

---

## Trap 4 — App2Container Is for Every New Container Application

False.

Its major use case is:

**Modernizing existing applications**

---

## Trap 5 — App2Container Is the Same as App Runner

False.

App2Container:

**Convert**

App Runner:

**Deploy and serve**

---

## Trap 6 — App2Container Is Primarily Lift-and-Shift

False.

Lift-and-shift keeps:

**The server architecture**

App2Container moves toward:

**Container architecture**

---

## Trap 7 — App2Container Replaces ECR

False.

They complement each other:

App2Container  
→ Creates container

ECR  
→ Stores container

---

## Trap 8 — App2Container Replaces ECS/EKS

False.

App2Container:

**Prepares the application**

ECS/EKS:

**Runs the application**

---

## Quick Cheat Sheet

| Exam Clue | Answer |
|---|---|
| Existing App → Container | App2Container |
| Java/.NET Modernization | App2Container |
| Generate Containerization Artifacts | App2Container |
| Store Container Image | ECR |
| Run AWS-Native Containers | ECS |
| Run Kubernetes Containers | EKS |
| Serverless Container Compute | Fargate |
| Simple Managed Web App | App Runner |
| Lift-and-Shift Server | Application Migration Service |

---

## Service Comparison

| Service | Main Purpose |
|---|---|
| App2Container | Convert Existing Apps to Containers |
| ECR | Store Container Images |
| ECS | AWS-Native Container Orchestration |
| EKS | Kubernetes Orchestration |
| Fargate | Serverless Container Compute |
| App Runner | Simple Managed Web App/API Deployment |
| Application Migration Service | Lift-and-Shift Servers |

---

## Container Modernization Shortcut

> **EXISTING APP**
> ↓
> App2Container
>
> **CONTAINER IMAGE**
> ↓
> [[ECR]]
>
> **AWS-NATIVE ORCHESTRATION**
> ↓
> [[ECS]]
>
> **KUBERNETES**
> ↓
> [[EKS]]
>
> **NO SERVER MANAGEMENT**
> ↓
> [[Fargate]]

---

## Final Exam Rapid-Fire

> **LEGACY APP → CONTAINER**
> → APP2CONTAINER
>
> **JAVA/.NET → CONTAINER**
> → APP2CONTAINER
>
> **CONTAINER IMAGE STORAGE**
> → ECR
>
> **RUN CONTAINERS**
> → ECS
>
> **RUN KUBERNETES**
> → EKS
>
> **SERVERLESS CONTAINER COMPUTE**
> → FARGATE
>
> **SIMPLE WEB APP DEPLOYMENT**
> → APP RUNNER
>
> **LIFT-AND-SHIFT SERVER**
> → APPLICATION MIGRATION SERVICE

---

## Master Memory Trick

> [!tip] App2Container Master Memory Trick
> Imagine an old application lives inside:
>
> **A traditional house**
>
> The company wants to move it into:
>
> **A standardized shipping container**
>
> App2Container:
>
> **PACKS THE APPLICATION**
>
> [[ECR]]:
>
> **STORES THE CONTAINER**
>
> [[ECS]] / [[EKS]]:
>
> **ORGANIZE AND RUN THE CONTAINERS**
>
> [[Fargate]]:
>
> **PROVIDES THE COMPUTE**

So remember:

> **APP2CONTAINER**
> → CONVERT
>
> **ECR**
> → STORE
>
> **ECS**
> → ORCHESTRATE
>
> **EKS**
> → KUBERNETES
>
> **FARGATE**
> → SERVERLESS COMPUTE
>
> **APP RUNNER**
> → SIMPLE WEB DEPLOYMENT

And the killer SAA clue:

> **"Modernize an existing Java or .NET application running on servers by converting it to containers."**
>
> → **App2Container**

---

## Related Notes

- [[ECS]]
- [[EKS]]
- [[ECR]]
- [[Fargate]]
- [[App Runner]]
- [[Application Migration Service]]
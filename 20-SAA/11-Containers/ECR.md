## What Problem Does It Solve?

[[ECR]] stands for:

**Amazon Elastic Container Registry**

It is AWS's:

**Fully managed container image registry**

ECR solves the problem:

> **"Where should I securely store, version, scan, and retrieve container images used by ECS, EKS, or other container platforms?"**

Architecture:

Developer / CI/CD  
↓  
Build Container Image  
↓  
Push Image to ECR  
↓  
ECS / EKS / Other Runtime  
↓  
Pull Image  
↓  
Run Container

> [!tip] Memory Trick
> **ECR = Container Image Warehouse**
>
> **ECR STORES**
>
> **ECS RUNS**

---

## What Is a Container Registry?

A container registry stores:

**Container images**

Think:

Source Code  
↓  
Docker Build  
↓  
Container Image  
↓  
Registry

The registry lets applications later:

**Pull that image**

and start:

**Containers**

---

## ECR Core Purpose

ECR stores:

- Docker images
- OCI-compatible container images
- Image versions
- Image tags
- Image metadata

Think:

Application Image  
↓  
ECR Repository  
↓  
Container Runtime

---

## ECR Repository

An:

**ECR Repository**

is where related container images are stored.

Example:

`orders-service`

could contain:

- `orders-service:v1`
- `orders-service:v2`
- `orders-service:v3`
- `orders-service:latest`

### Memory Trick

**Repository = Folder for Images**

---

## Image Tags

Tags identify:

**Specific image versions**

Examples:

`latest`

`v1`

`v2.1`

`production`

`2026-08-26`

Example:

`orders-service:v2`

### Exam Thinking

Tags make it easier to:

**Identify and deploy image versions**

---

## Image Digest

Container images can also be identified by:

**Digest**

A digest is based on:

**Image content**

and provides a more immutable way to identify:

**A specific image**

### Memory Trick

**TAG = Friendly Name**

**DIGEST = Exact Image Identity**

---

## Private Repositories

ECR repositories are commonly:

**Private**

Access is controlled using:

- IAM
- Repository policies

This allows organizations to securely store:

**Internal application images**

---

## Public ECR

AWS also supports:

**Public container images**

through:

**Amazon ECR Public**

Think:

Public Repository  
↓  
Anyone can pull according to repository settings

For SAA, the stronger association is usually:

> **ECR = Managed AWS container image registry**

---

## ECR + ECS

This is one of the most important container architectures.

Developer  
↓  
Build Image  
↓  
ECR  
↓  
[[ECS]]  
↓  
Task

ECS pulls:

**The container image**

from ECR and uses it to start:

**ECS tasks**

### Killer Exam Clue

> **Where should ECS container images be stored?**
>
> → **ECR**

---

## ECR + Fargate

[[02-Compute/Fargate]] tasks can also pull images from:

[[ECR]]

Architecture:

ECR  
↓  
ECS Task Definition  
↓  
Fargate Task

Fargate provides:

**Compute**

ECR provides:

**Image storage**

---

## ECR + EKS

[[02-Compute/EKS]] can also pull container images from ECR.

Architecture:

ECR  
↓  
EKS Cluster  
↓  
Pods

This means ECR is not:

**ECS-only**

It is a general AWS container registry.

---

## ECR + CI/CD

A common deployment pipeline:

Developer  
↓  
Git Repository  
↓  
Build Pipeline  
↓  
Build Container Image  
↓  
Push to ECR  
↓  
Deploy to ECS / EKS

This supports:

**Automated container deployments**

---

## Example CI/CD Flow

Code Change  
↓  
CodeBuild  
↓  
Docker Build  
↓  
ECR  
↓  
ECS Deployment

This separates:

**Building the image**

from:

**Running the image**

---

## ECR Authentication

Clients need permission to:

**Authenticate and interact with ECR**

Common operations include:

- Push images
- Pull images
- List repositories
- Read image metadata

Access is controlled through:

**IAM**

---

## IAM Permissions

Different principals may need different permissions.

Example:

Developer / CI Pipeline  
→ Push Image

ECS Runtime  
→ Pull Image

Administrator  
→ Manage Repository

### SAA Principle

> **Use least-privilege IAM permissions for ECR access**

---

## ECS Task Execution Role + ECR

This is a very important exam distinction.

When ECS needs to:

**Pull an image from ECR**

the relevant role is typically:

**ECS Task Execution Role**

Architecture:

ECS Runtime  
↓  
Task Execution Role  
↓  
ECR  
↓  
Pull Image

### Killer Exam Clue

> **ECS task cannot start because it cannot pull the private ECR image**
>
> → **Check the Task Execution Role**

---

## Task Role vs ECR

Do NOT confuse:

**Task Role**

with:

**Task Execution Role**

### Task Role

Used by:

**Application code**

Example:

Container app reads S3.

---

### Execution Role

Used by:

**ECS during task startup**

Example:

Pull image from ECR.

### Memory Trick

**APP ACCESS**
→ Task Role

**IMAGE PULL**
→ Execution Role

---

## ECR Encryption

ECR supports:

**Encryption at rest**

Images stored in ECR are encrypted.

ECR can integrate with:

[[06-Security/KMS]]

for encryption-key management depending on repository configuration.

### Exam Pattern

> **Container images must be encrypted at rest using customer-controlled keys**
>
> → **ECR + KMS**

---

## Encryption in Transit

Image transfers use:

**HTTPS**

for encryption:

**In transit**

This protects images when:

- Pushing
- Pulling

---

## Image Scanning

ECR supports:

**Container image scanning**

This helps identify:

**Software vulnerabilities**

inside images.

Think:

Container Image  
↓  
ECR Scan  
↓  
Vulnerability Findings

### Killer Exam Clue

> **Identify known vulnerabilities in stored container images**
>
> → **ECR Image Scanning**

---

## Why Image Scanning Matters

A container image may include:

- OS packages
- Libraries
- Runtime dependencies

Some may contain:

**Known vulnerabilities**

Scanning helps teams identify:

**Risk before deployment**

---

## Scan on Push

ECR can be configured to:

**Scan images when they are pushed**

Architecture:

Push Image  
↓  
ECR  
↓  
Automatic Scan  
↓  
Findings

This helps incorporate:

**Security into deployment pipelines**

---

## Enhanced Scanning

ECR can support more advanced vulnerability scanning integrations, including capabilities associated with:

**Amazon Inspector**

The main SAA takeaway:

> **ECR can scan container images for vulnerabilities**

---

## ECR Lifecycle Policies

Container repositories can accumulate:

**Many old images**

Example:

v1  
v2  
v3  
v4  
v5  
v6  
...

ECR Lifecycle Policies can automatically:

**Expire or remove old images**

based on rules.

### Killer Exam Clue

> **Automatically clean up old container images**
>
> → **ECR Lifecycle Policy**

---

## Lifecycle Policy Example

Requirement:

Keep only:

**The latest 20 production images**

Older images:

**Automatically expire**

This helps reduce:

- Storage usage
- Repository clutter
- Manual maintenance

---

## Image Tag Mutability

Repositories can control whether:

**Image tags can be overwritten**

### Mutable Tags

Example:

`latest`

can be moved from:

Image A  
to  
Image B

---

### Immutable Tags

A tag cannot be:

**Overwritten after creation**

This can improve:

**Deployment consistency**

### Exam Thinking

> **Prevent an existing image tag from being overwritten**
>
> → **Tag immutability**

---

## Why Immutable Tags Matter

Suppose production deploys:

`app:v1`

If someone later replaces the image behind:

`v1`

you could deploy:

**Different code with the same tag**

Tag immutability helps prevent:

**This ambiguity**

---

## Cross-Account ECR Access

ECR repository policies can allow:

**Other AWS accounts**

to access images.

Architecture:

Account A  
↓  
ECR Repository

Account B  
↓  
Authorized Pull

This is useful when:

- Central image repository exists
- Multiple application accounts deploy the same image

---

## ECR Repository Policies

ECR supports:

**Repository policies**

which are:

**Resource-based policies**

These can control:

**Who can access the repository**

### Memory Trick

**IAM Policy = What can this identity do?**

**Repository Policy = Who can access this repository?**

---

## Cross-Region Replication

ECR can support:

**Cross-Region replication**

of container images.

Architecture:

Region A  
↓  
ECR Repository  
↓  
Replication  
↓  
Region B

This can support:

- Multi-Region applications
- Faster local image pulls
- Disaster recovery
- Regional deployment pipelines

---

## Cross-Account Replication

ECR replication can also support architectures involving:

**Other AWS accounts**

This is useful for:

**Centralized container image management**

---

## Why Replicate Images?

Suppose an application runs in:

- us-east-1
- eu-west-1

Instead of pulling everything from one Region:

Image  
↓  
Replicate  
↓  
Local ECR Repository per Region

This can improve:

- Deployment resilience
- Regional independence
- Operational simplicity

---

## ECR vs Docker Hub

Both can store:

**Container images**

### ECR

Think:

- AWS-native
- IAM integration
- ECS/EKS integration
- Private repositories
- AWS security integration

### Docker Hub

Think:

**External container registry platform**

### Exam Shortcut

> **AWS-native private container image storage**
>
> → **ECR**

---

## ECR vs ECS

This is the most important distinction.

### [[ECR]]

Purpose:

**Store container images**

### [[ECS]]

Purpose:

**Run and orchestrate containers**

### Memory Trick

**R = Registry**

**S = Service**

---

## ECR vs Fargate

### ECR

Stores:

**Images**

### [[02-Compute/Fargate]]

Provides:

**Serverless compute for containers**

Architecture:

ECR  
↓  
ECS / EKS  
↓  
Fargate  
↓  
Running Container

---

## ECR vs EKS

### ECR

Container registry

### [[02-Compute/EKS]]

Kubernetes orchestration

EKS can:

**Pull images from ECR**

---

## ECR vs S3

Both store data, but their purposes differ.

### [[S3]]

General:

**Object storage**

### ECR

Specialized:

**Container image registry**

Do NOT choose S3 when the requirement specifically calls for:

**Managed container image registry functionality**

---

## ECR vs CodeArtifact

### ECR

Stores:

**Container images**

### CodeArtifact

Stores:

**Software packages**

such as package-manager artifacts.

### Memory Trick

**Container Image**
→ ECR

**Package Dependency**
→ CodeArtifact

---

## Architecture Thinking

### Scenario 1 — Store ECS Images

A company builds Docker images for:

[[ECS]]

The images need:

- Private storage
- AWS IAM integration

**Choose → ECR**

---

### Scenario 2 — ECS Cannot Pull Image

An ECS task remains unable to start because:

**Its private image cannot be pulled**

Check:

**Task Execution Role**

and ECR permissions.

---

### Scenario 3 — Vulnerability Scanning

Security needs to scan:

**Container images for known software vulnerabilities**

Choose:

**ECR Image Scanning**

---

### Scenario 4 — Old Images

A CI/CD pipeline creates:

**Hundreds of old image versions**

Need automatic cleanup.

Choose:

**ECR Lifecycle Policy**

---

### Scenario 5 — Prevent Tag Replacement

Production wants:

`release-v1`

to always reference:

**The exact same image**

Choose:

**Tag Immutability**

---

### Scenario 6 — Multi-Region Deployment

A container application runs in:

**Multiple AWS Regions**

Images should exist locally in each Region.

Choose:

**ECR Cross-Region Replication**

---

### Scenario 7 — Central Container Repository

One AWS account stores approved images.

Workloads in other accounts need:

**Controlled image pull access**

Choose:

**ECR Repository Policy / Cross-Account Access**

---

### Scenario 8 — Application Needs S3

The image runs successfully, but application code needs:

**S3 access**

Do NOT change ECR permissions.

Use:

**ECS Task Role**

---

### Scenario 9 — Kubernetes Deployment

A Kubernetes application on EKS requires:

**Private AWS-hosted container images**

Choose:

**ECR + EKS**

---

## Scenario Recognition

Immediately think:

[[ECR]]

when you see:

- Container registry
- Docker image storage
- OCI images
- Container image repository
- ECS image
- EKS image
- Push image
- Pull image
- Image tag
- Image scanning
- Lifecycle policy
- Cross-Region image replication

---

## Exam Traps

### Trap 1 — ECR Runs Containers

False.

ECR:

**Stores images**

ECS / EKS:

**Run containers**

---

### Trap 2 — ECS Task Role Is Used to Pull ECR Images

Usually wrong.

Think:

**Task Execution Role**

---

### Trap 3 — ECR Is General Object Storage Like S3

False.

ECR is specialized for:

**Container images**

---

### Trap 4 — Image Tags Are Always Immutable

False.

Repositories can allow:

**Mutable tags**

unless immutability is configured.

---

### Trap 5 — Old Images Must Be Deleted Manually

False.

Use:

**Lifecycle Policies**

---

### Trap 6 — ECR Cannot Scan Images

False.

ECR supports:

**Image vulnerability scanning**

---

### Trap 7 — ECR Only Works with ECS

False.

It can be used with:

- ECS
- EKS
- Other compatible container runtimes

---

### Trap 8 — Cross-Account Image Access Requires Making the Repository Public

False.

Use:

**IAM + Repository Policies**

---

### Trap 9 — Multi-Region ECS Must Pull Images from One Central Region

Not necessarily.

Use:

**ECR replication**

when appropriate.

---

## Quick Cheat Sheet

| Exam Clue | Answer |
|---|---|
| Store Container Images | ECR |
| Private AWS Container Registry | ECR |
| ECS Pulls Image | ECR |
| EKS Pulls Image | ECR |
| Image Pull Permission for ECS Startup | Task Execution Role |
| App AWS Permissions | Task Role |
| Scan Container Image | ECR Image Scanning |
| Remove Old Images Automatically | Lifecycle Policy |
| Prevent Tag Overwrite | Tag Immutability |
| Cross-Account Image Access | Repository Policy |
| Multi-Region Image Copies | ECR Replication |
| Encrypt Images with Key Control | ECR + KMS |

---

## ECR vs ECS Quick Comparison

| Requirement | ECR | ECS |
|---|---:|---:|
| Store Images | ✅ | ❌ |
| Run Containers | ❌ | ✅ |
| Image Repository | ✅ | ❌ |
| Task Orchestration | ❌ | ✅ |
| Image Scanning | ✅ | ❌ Primary Role |
| Services / Tasks | ❌ | ✅ |

---

## Container Service Shortcut

> **BUILD IMAGE**
> ↓
> Docker / CI Pipeline
>
> **STORE IMAGE**
> ↓
> [[ECR]]
>
> **RUN IMAGE**
> ↓
> [[ECS]] / [[02-Compute/EKS]]
>
> **NO SERVERS**
> ↓
> [[02-Compute/Fargate]]

---

## Final Exam Rapid-Fire

> **CONTAINER IMAGE STORAGE**
> → ECR
>
> **RUN CONTAINERS**
> → ECS
>
> **KUBERNETES**
> → EKS
>
> **SERVERLESS CONTAINER COMPUTE**
> → FARGATE
>
> **ECS PULLS PRIVATE IMAGE**
> → EXECUTION ROLE
>
> **APP ACCESSES AWS SERVICE**
> → TASK ROLE
>
> **VULNERABILITY SCAN**
> → ECR IMAGE SCANNING
>
> **DELETE OLD IMAGES**
> → LIFECYCLE POLICY
>
> **PREVENT TAG OVERWRITE**
> → TAG IMMUTABILITY
>
> **COPY IMAGES BETWEEN REGIONS**
> → ECR REPLICATION
>
> **OTHER ACCOUNT PULLS IMAGE**
> → REPOSITORY POLICY

---

## Master Memory Trick

> [!tip] ECR Master Memory Trick
> Think of a warehouse.
>
> Developers build:
>
> **Container Images**
>
> The warehouse is:
>
> **ECR**
>
> Each shelf is:
>
> **Repository**
>
> Labels on boxes are:
>
> **Tags**
>
> Exact fingerprints are:
>
> **Digests**
>
> Security checks are:
>
> **Image Scans**
>
> Cleanup rules are:
>
> **Lifecycle Policies**
>
> ECS or EKS arrives later and:
>
> **PULLS THE BOX**
>
> then:
>
> **RUNS THE CONTAINER**

So remember:

> **ECR = STORE**
>
> **ECS = ORCHESTRATE**
>
> **FARGATE = COMPUTE**
>
> **EKS = KUBERNETES**

And the killer role distinction:

> **ECS NEEDS IMAGE**
> → EXECUTION ROLE
>
> **APP NEEDS AWS SERVICE**
> → TASK ROLE

---

## Related Notes

- [[ECS]]
- [[ECS IAM Roles]]
- [[ECS Auto Scaling]]
- [[ECS Solutions Architectures]]
- [[02-Compute/Fargate]]
- [[02-Compute/EKS]]
- [[S3]]
- [[06-Security/KMS]]
- [[IAM]]
- [[07-Monitoring/CloudWatch]]
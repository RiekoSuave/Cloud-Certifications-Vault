## What Problem Does It Solve?

AWS App Runner is a:

**Fully managed service for deploying web applications and APIs**

It can deploy applications directly from:

- Source code
- Container images

without requiring you to manage:

- Servers
- Container orchestration
- Load balancers
- Infrastructure scaling

Architecture:

Source Code / Container Image  
↓  
App Runner  
↓  
Running Web Application / API

> [!tip] Memory Trick
> **App Runner = Give AWS your app → AWS runs the web service**
>
> Think:
>
> **Simpler than managing ECS infrastructure yourself**

---

## Main App Runner Idea

App Runner is designed for developers who want:

**A simple path from application code or container image to a running web service**

AWS handles much of the infrastructure automatically.

Think:

Application  
↓  
App Runner  
↓  
Public Web Service

---

## What AWS Manages

App Runner manages infrastructure such as:

- Compute
- Deployment
- Load balancing
- Scaling
- HTTPS endpoint
- Health monitoring

The goal is:

**Minimum infrastructure management**

---

## App Runner Sources

App Runner can deploy from:

### Source Code Repository

Application Source  
↓  
App Runner  
↓  
Build  
↓  
Deploy

or:

### Container Image

Container Image  
↓  
App Runner  
↓  
Deploy

---

## Source Code Deployment

With source-based deployment:

Developer  
↓  
Source Repository  
↓  
App Runner  
↓  
Build Application  
↓  
Run Web Service

App Runner can handle:

**Build and deployment**

without requiring the developer to manually create:

**Container infrastructure**

---

## Container Image Deployment

App Runner can also deploy:

**Container images**

A common AWS architecture:

Developer  
↓  
Build Container Image  
↓  
[[ECR]]  
↓  
App Runner  
↓  
Web Application

### Killer Exam Clue

> **Deploy a containerized web application from ECR with minimal infrastructure management**
>
> → **App Runner**

---

## App Runner + ECR

[[ECR]] stores:

**Container images**

App Runner:

**Deploys and runs the application**

Architecture:

ECR  
↓  
App Runner  
↓  
Application

### Memory Trick

**ECR = STORE**

**App Runner = DEPLOY + RUN**

---

## Automatic Deployments

App Runner can support:

**Automatic deployments**

When application source or container images change:

Change  
↓  
App Runner  
↓  
New Deployment

This simplifies:

**Continuous application delivery**

---

## App Runner Endpoint

App Runner provides the application with:

**A secure web endpoint**

This means you do not have to manually configure:

- EC2
- ECS cluster
- ALB
- Auto Scaling Group

just to expose:

**A web application**

---

## HTTPS

App Runner provides:

**HTTPS support**

for deployed web services.

Think:

Internet  
↓  
HTTPS  
↓  
App Runner Service

This reduces the need to manually manage:

**Basic TLS infrastructure**

---

## Custom Domains

Applications can use:

**Custom domain names**

instead of relying only on:

**The default App Runner service URL**

Conceptually:

`api.example.com`  
↓  
App Runner

---

## Auto Scaling

App Runner automatically scales:

**Application compute capacity**

based on demand.

Traffic ↑  
↓  
App Runner  
↓  
More Application Capacity

Traffic ↓  
↓  
Scale Down

The developer does not manually manage:

**ECS task scaling or EC2 Auto Scaling Groups**

---

## Scaling Configuration

App Runner scaling behavior can be configured using concepts such as:

- Minimum instances
- Maximum instances
- Concurrency

The broad SAA takeaway:

> **App Runner automatically scales web applications without requiring infrastructure-level scaling management.**

---

## Concurrency

Concurrency represents:

**How many simultaneous requests an application instance can handle before App Runner scales**

Conceptually:

Requests ↑  
↓  
Concurrency Threshold Reached  
↓  
Scale Out

### Exam Thinking

App Runner scaling is focused on:

**Application request demand**

rather than manually configuring:

**Server capacity**

---

## App Runner Health Checks

App Runner performs:

**Health checks**

to determine whether:

**Application instances are healthy**

Unhealthy capacity can be:

**Replaced**

This supports:

**Application availability**

---

## App Runner + IAM

Applications running in App Runner may need access to:

**AWS services**

Examples:

- S3
- DynamoDB
- SQS
- Secrets Manager

IAM roles can provide:

**Application permissions**

### SAA Principle

> Give the application only the AWS permissions it actually needs.

---

## App Runner Instance Role

An:

**Instance Role**

can provide permissions to:

**The running application**

Example:

App Runner Application  
↓  
IAM Role  
↓  
DynamoDB

### Killer Exam Clue

> **Application running in App Runner needs AWS API access**
>
> → **App Runner instance role**

---

## ECR Access Role

When App Runner needs to access:

**A private ECR image**

it may require appropriate permissions for:

**Image retrieval**

Do not confuse:

**Image access**

with:

**Application runtime AWS permissions**

The same conceptual distinction appears elsewhere in container architectures:

> **Deployment permissions and application permissions are separate concerns.**

---

## App Runner Networking

By default, App Runner is designed to make it easy to run:

**Web-facing services**

It abstracts much of the:

**Network infrastructure**

that you would otherwise configure manually.

---

## Outbound VPC Access

Some applications need access to:

**Private VPC resources**

Examples:

- RDS database
- ElastiCache cluster
- Internal services

App Runner can use:

**VPC connectivity**

for outbound access to private resources.

Architecture:

App Runner  
↓  
VPC Connector  
↓  
Private VPC Resource

---

## App Runner + RDS

Example:

Internet  
↓  
App Runner Web API  
↓  
VPC Connector  
↓  
[[RDS]]

This allows the application to access:

**A private database**

without placing the database:

**Directly on the Internet**

---

## App Runner + DynamoDB

For DynamoDB:

App Runner  
↓  
IAM Role  
↓  
DynamoDB

Since DynamoDB is an AWS managed service, the application primarily needs:

**Correct IAM permissions and network access architecture**

---

## App Runner + Secrets Manager

Applications should not hardcode:

- Database passwords
- API keys
- Credentials

Instead use services such as:

[[Secrets Manager]]

Architecture:

App Runner  
↓  
IAM Role  
↓  
Secrets Manager

---

## App Runner vs ECS

This is an important comparison.

### [[ECS]]

Provides:

**Container orchestration**

You control concepts such as:

- Task definitions
- Services
- Networking
- Load balancers
- Scaling configuration
- EC2 vs Fargate

### App Runner

Provides:

**Higher-level web application deployment**

AWS abstracts more infrastructure.

### Memory Trick

**ECS = More Control**

**App Runner = More Simplicity**

---

## App Runner vs Fargate

[[Fargate]] is:

**Serverless container compute**

App Runner is:

**Managed web application platform**

Fargate usually works underneath:

**ECS or EKS orchestration**

App Runner abstracts much more of the:

**Container infrastructure**

### Exam Shortcut

Need control over:

- Tasks
- Services
- Networking
- Container orchestration

→ ECS + Fargate

Need:

**Simple managed web application deployment**

→ App Runner

---

## App Runner vs Lambda

### [[02-Compute/Lambda]]

Think:

- Functions
- Event-driven
- Short-lived execution
- Trigger-based architecture

### App Runner

Think:

- Web applications
- APIs
- Continuously available HTTP services

### Killer Exam Shortcut

**Event-driven function**
→ Lambda

**Always-running managed web API**
→ App Runner

---

## App Runner vs Elastic Beanstalk

Both simplify:

**Application deployment**

but the abstraction differs.

### Elastic Beanstalk

Think:

- Managed application platform
- More visible underlying AWS infrastructure
- EC2-based environments
- More infrastructure customization

### App Runner

Think:

- Source/container → web service
- Greater infrastructure abstraction
- Automatic HTTPS/load balancing/scaling

### Memory Trick

**Beanstalk = Managed Environment**

**App Runner = Managed Web Service**

---

## App Runner vs ECS + Fargate

This is likely the most useful architecture comparison.

### ECS + Fargate

You still configure:

- ECS cluster/service concepts
- Task definitions
- Networking
- Load balancer architecture
- Auto Scaling policies

You gain:

**More architectural control**

---

### App Runner

You provide:

**Code or container**

AWS handles much of:

- Deployment
- Scaling
- Load balancing
- HTTPS
- Runtime infrastructure

You gain:

**More simplicity**

---

## Control vs Simplicity

Think of a spectrum:

App Runner  
↓  
**Highest Simplicity**

ECS + Fargate  
↓  
**More Control**

ECS + EC2  
↓  
**Most Infrastructure Control**

### Exam Strategy

If the requirement says:

**Least operational overhead**

look closely at:

**App Runner**

when the workload is specifically:

**A web application or API**

---

## App Runner vs EKS

[[EKS]] is appropriate when:

**Kubernetes is required**

App Runner is appropriate when:

**The developer simply needs to deploy a web service**

Do NOT choose EKS merely because:

**The application uses containers**

---

## App Runner Use Cases

Good use cases include:

- Web applications
- REST APIs
- Backend services
- Microservices
- Containerized web services
- Source-code web services

---

## Poor App Runner Fit

App Runner is not primarily designed for:

- Kubernetes requirements
- Complex container orchestration
- Deep host-level control
- Arbitrary EC2 infrastructure
- Large custom cluster architectures

For those requirements, consider:

- ECS
- EKS
- EC2

---

## Architecture Thinking

### Scenario 1 — Simple Web API

A development team has:

**Source code**

and wants:

- HTTPS
- Automatic scaling
- Minimal infrastructure management

Choose:

**App Runner**

---

### Scenario 2 — Containerized Web Application

Company has:

**Container image in ECR**

Need:

- Public web endpoint
- Auto Scaling
- No ECS cluster management

Choose:

**ECR + App Runner**

---

### Scenario 3 — Detailed Container Control

Company requires:

- Multiple ECS services
- Custom task definitions
- Advanced networking
- Detailed load balancer configuration

Do NOT choose App Runner.

Choose:

**ECS**

---

### Scenario 4 — Serverless Containers with More Control

Company does not want EC2 management but requires:

- ECS task definitions
- Services
- Custom ALB architecture

Choose:

**ECS + Fargate**

---

### Scenario 5 — Kubernetes

Company requires:

**Kubernetes APIs**

Choose:

[[EKS]]

not:

App Runner

---

### Scenario 6 — Event-Driven Function

Code runs only when:

**An S3 object is uploaded**

Choose:

[[02-Compute/Lambda]]

not:

App Runner

---

### Scenario 7 — Private Database

App Runner application needs:

**Private RDS access**

Choose:

App Runner  
↓  
VPC Connector  
↓  
RDS

---

### Scenario 8 — AWS API Access

App Runner application needs to:

**Read from S3**

Use:

**Appropriate App Runner runtime IAM role**

---

### Scenario 9 — Automatic Deployment

Developers want application changes to:

**Automatically deploy**

with minimal infrastructure tooling.

Think:

**App Runner automatic deployments**

---

## Scenario Recognition

Immediately think:

**App Runner**

when you see:

- Web application
- Web API
- Source code
- Container image
- Automatic deployment
- Automatic HTTPS
- Automatic load balancing
- Automatic scaling
- Minimal infrastructure management
- Developer-focused deployment

---

## Think ECS + Fargate Instead When You See

- Task definitions
- ECS services
- Detailed container networking
- Multiple container workloads
- Custom load balancing
- More orchestration control

---

## Think EKS Instead When You See

- Kubernetes
- Pods
- Kubernetes APIs
- Kubernetes ecosystem

---

## Think Lambda Instead When You See

- Event-driven function
- Short-lived execution
- Trigger-based compute

---

## Exam Traps

### Trap 1 — App Runner Is the Same as Fargate

False.

Fargate:

**Container compute**

App Runner:

**Managed web application service**

---

### Trap 2 — App Runner Requires You to Configure an ALB

Not for the normal managed App Runner architecture.

App Runner handles:

**Load balancing**

for the service.

---

### Trap 3 — App Runner Requires an ECS Cluster

False.

App Runner abstracts:

**Container orchestration infrastructure**

from the user.

---

### Trap 4 — App Runner Is Kubernetes

False.

For Kubernetes:

→ [[EKS]]

---

### Trap 5 — App Runner Is Best for Every Container Workload

False.

It is optimized around:

**Web applications and APIs**

Complex container architectures may fit:

**ECS or EKS**

better.

---

### Trap 6 — App Runner Gives Maximum Infrastructure Control

False.

Its advantage is:

**Abstraction and simplicity**

For more control:

→ ECS / EKS / EC2

---

### Trap 7 — Application Credentials Should Be Hardcoded into the Image

False.

Use:

- IAM
- Secrets Manager

---

### Trap 8 — App Runner Cannot Access Private VPC Resources

False.

It can use:

**VPC connectivity**

for outbound access to private resources.

---

## Quick Cheat Sheet

| Exam Clue | Answer |
|---|---|
| Simple Managed Web App | App Runner |
| Simple Managed Web API | App Runner |
| Source → Running Web Service | App Runner |
| ECR Image → Web Service | App Runner |
| Automatic HTTPS | App Runner |
| Automatic Web Scaling | App Runner |
| Minimum Web Infrastructure Management | App Runner |
| More Container Control | ECS + Fargate |
| Host Control | ECS + EC2 |
| Kubernetes | EKS |
| Event-Driven Function | Lambda |
| Private VPC Resource Access | VPC Connector |

---

## Container Service Comparison

| Requirement | App Runner | ECS + Fargate | EKS |
|---|---:|---:|---:|
| Web App / API | ✅ | ✅ | ✅ |
| Container Support | ✅ | ✅ | ✅ |
| Server Management | ❌ | ❌ | Depends |
| ECS Concepts Required | ❌ | ✅ | ❌ |
| Kubernetes | ❌ | ❌ | ✅ |
| Detailed Container Control | Lower | High | High |
| Infrastructure Simplicity | Highest | High | Lower |
| Custom Orchestration | Limited | ECS | Kubernetes |

---

## Decision Shortcut

Need a:

**Simple web app/API**

with:

**Minimum infrastructure management**

→ App Runner

Need:

**Container orchestration control**

without managing servers

→ ECS + Fargate

Need:

**Kubernetes**

→ EKS

Need:

**Host control**

→ ECS/EKS + EC2

Need:

**Event-driven function**

→ Lambda

---

## Final Exam Rapid-Fire

> **SOURCE CODE → WEB SERVICE**
> → APP RUNNER
>
> **ECR IMAGE → SIMPLE WEB SERVICE**
> → APP RUNNER
>
> **AUTOMATIC HTTPS + LOAD BALANCING**
> → APP RUNNER
>
> **MINIMUM WEB INFRASTRUCTURE**
> → APP RUNNER
>
> **MORE CONTAINER CONTROL**
> → ECS + FARGATE
>
> **HOST CONTROL**
> → ECS + EC2
>
> **KUBERNETES**
> → EKS
>
> **EVENT-DRIVEN FUNCTION**
> → LAMBDA
>
> **PRIVATE VPC RESOURCE**
> → VPC CONNECTOR

---

## Master Memory Trick

> [!tip] App Runner Master Memory Trick
> Imagine you own a food recipe.
>
> With:
>
> **EC2**
>
> you build and maintain the entire restaurant.
>
> With:
>
> **ECS + Fargate**
>
> AWS provides the kitchen, but you still manage how the restaurant operates.
>
> With:
>
> **App Runner**
>
> you hand AWS:
>
> **The recipe or packaged meal**
>
> and say:
>
> **"Put this online and serve customers."**
>
> AWS handles:
>
> - Infrastructure
> - Scaling
> - Load balancing
> - HTTPS
> - Deployment

So remember:

> **APP RUNNER**
> → SIMPLE WEB APP
>
> **ECS**
> → CONTAINER ORCHESTRATION
>
> **FARGATE**
> → SERVERLESS CONTAINER COMPUTE
>
> **EKS**
> → KUBERNETES
>
> **LAMBDA**
> → SERVERLESS FUNCTIONS

And the killer SAA clue:

> **"Deploy a web application or API from source code/container image with the least infrastructure management."**
>
> → **App Runner**

---

## Related Notes

- [[ECS]]
- [[Fargate]]
- [[ECR]]
- [[EKS]]
- [[02-Compute/Lambda]]
- [[Application Load Balancer]]
- [[RDS]]
- [[S3]]
- [[Secrets Manager]]
- [[IAM]]
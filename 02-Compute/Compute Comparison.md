## Compute Service Comparison

| Service | Problem Solved | Server Management | Memory Trick |
|---|---|---|---|
| EC2 | Virtual machines | Yes | Rent a computer |
| Lightsail | Simple hosting | Minimal | Easy EC2 |
| Lambda | Run functions/code | No | Serverless functions |
| Elastic Beanstalk | Deploy applications | Mostly managed | Upload code |
| ECS | Container orchestration | Depends | AWS containers |
| EKS | Kubernetes | Depends | Kubernetes |
| Fargate | Serverless container compute | No | Serverless containers |
| ECR | Store container images | No | Container repository |

---

## EC2

Best when you need:

- Full server control
- Operating system access
- Custom software
- Long-running applications

You manage more of the infrastructure.

### Shortcut

EC2 = Virtual Machine

---

## Lightsail

Best when you need:

- Simple website hosting
- Predictable pricing
- Easy setup
- Preconfigured applications

Provides less flexibility than building directly with individual AWS services.

### Shortcut

Lightsail = Easy Hosting

---

## Lambda

Best when you need:

- Serverless functions
- Event-driven processing
- Short-running code
- Automatic scaling

Maximum invocation time:

15 minutes

### Shortcut

Lambda = Run Code Without Servers

---

## Elastic Beanstalk

Best when developers want to:

- Deploy applications
- Focus primarily on code
- Let AWS handle deployment
- Use EC2, ELB and Auto Scaling behind the scenes

### Shortcut

Beanstalk = Deploy My App

---

## ECS

Best when you need:

- Docker containers
- AWS-native container orchestration

Can use:

- EC2
- Fargate

### Shortcut

ECS = AWS Containers

---

## EKS

Best when you specifically need:

Kubernetes

Can run workloads using:

- EC2
- Fargate

### Shortcut

EKS = Kubernetes

---

## Fargate

Best when you need:

Containers without managing the underlying servers.

Works with:

- ECS
- EKS

### Shortcut

Fargate = Serverless Containers

---

## ECR

Best when you need:

A private repository for container images.

Common Flow:

ECR

↓

ECS / EKS

↓

EC2 or Fargate

### Shortcut

ECR = Store Container Images

---

## How The Container Services Fit Together

Docker

↓

Container Technology

↓

ECR

Stores Container Images

↓

ECS or EKS

Orchestrates Containers

↓

EC2 or Fargate

Provides Compute

---

## Common Exam Decisions

Need a virtual machine with OS control?

→ EC2

---

Need a simple small website with predictable pricing?

→ Lightsail

---

Need event-driven serverless code?

→ Lambda

---

Need to easily deploy an application while AWS handles infrastructure provisioning?

→ Elastic Beanstalk

---

Need AWS-native container orchestration?

→ ECS

---

Need Kubernetes?

→ EKS

---

Need containers without managing EC2?

→ Fargate

---

Need somewhere to store Docker/container images?

→ ECR

---

## Quick Cheat Sheet

EC2 = Virtual Machines

Lightsail = Easy Hosting

Lambda = Serverless Functions

Beanstalk = Application Deployment

ECS = AWS Containers

EKS = Kubernetes

Fargate = Serverless Containers

ECR = Container Image Storage
See also: [[02-Compute/EC2]]

See also: [[Elastic Load Balancing (ELB)]]

See also: [[Auto Scaling Groups (ASG)]]

See also: [[RDS]]

See also: [[07-Monitoring/CloudWatch]]

## What Problem Does It Solve?

Simplifies deploying and managing applications on AWS.

Instead of manually configuring all the infrastructure needed for an application, Elastic Beanstalk can handle tasks such as:

- Capacity provisioning
- Load balancing
- Auto Scaling
- Application health monitoring
- Application deployment

---

## Type

Platform as a Service (PaaS)

---

## What Is Elastic Beanstalk?

Elastic Beanstalk provides a developer-focused way to deploy applications on AWS.

You provide your application code.

Elastic Beanstalk helps deploy and manage the underlying environment.

### Memory Trick

Beanstalk = Upload code and AWS handles deployment

---

## Services Used Behind Beanstalk

Elastic Beanstalk can use AWS services such as:

- EC2
- Auto Scaling Groups
- Elastic Load Balancing
- RDS

Instead of configuring all of these separately, Beanstalk provides a simpler view for deploying the application.

---

## What Beanstalk Manages

Elastic Beanstalk can handle:

- Instance configuration
- Operating system
- Capacity provisioning
- Load balancing
- Auto Scaling
- Deployment
- Application health monitoring

The deployment strategy is configurable, but Elastic Beanstalk performs the deployment.

---

## Developer Responsibility

The developer focuses primarily on:

Application Code

You still have control over the configuration of the environment.

### Memory Trick

Developer = Code

Beanstalk = Deployment + Infrastructure Management

---

## Pricing

Elastic Beanstalk itself is free.

You pay for the underlying AWS resources it uses.

Examples:

- EC2
- Load Balancers
- RDS

### Exam Trap

"Elastic Beanstalk is free" does NOT mean the infrastructure running your application is free.

---

## Architecture Models

Elastic Beanstalk supports different application architectures.

### Single Instance

One instance runs the application.

Best For:

- Development environments

### Memory Trick

Single Instance = Dev

---

### Load Balancer + Auto Scaling Group

Uses:

- Load Balancer
- Auto Scaling Group
- Multiple instances

Best For:

- Production web applications
- Pre-production web applications

Benefits:

- Scalability
- High Availability
- Load distribution

### Memory Trick

LB + ASG = Production Web App

---

### Auto Scaling Group Only

Uses Auto Scaling without a Load Balancer.

Best For:

- Production non-web applications
- Worker applications

### Memory Trick

ASG Only = Workers / Non-Web

---

## Health Monitoring

Elastic Beanstalk monitors application health.

A health agent sends metrics to:

CloudWatch

Beanstalk can:

- Check application health
- Publish health events
- Monitor application responsiveness

See:

[[07-Monitoring/CloudWatch]]

---

## Elastic Beanstalk vs EC2

### EC2

You have more direct control and manually manage more of the infrastructure.

### Elastic Beanstalk

AWS simplifies deployment and infrastructure management.

| EC2 | Elastic Beanstalk |
|---|---|
| IaaS | PaaS |
| Manage more infrastructure | Managed deployment |
| More manual configuration | Automated provisioning |
| Full server control | Developer-focused |

---

## Elastic Beanstalk vs Lambda

### Elastic Beanstalk

Deploys traditional applications using infrastructure such as EC2.

### Lambda

Runs serverless functions.

| Service | Best For |
|---|---|
| Elastic Beanstalk | Deploy applications |
| Lambda | Serverless functions |

---

## Key Features

- Platform as a Service
- Managed application deployment
- Capacity provisioning
- Load balancing
- Auto Scaling
- Health monitoring
- Supports multiple platforms

---

## Exam Scenarios

A developer wants to deploy an application without manually configuring EC2, Auto Scaling, and Load Balancing.

→ Elastic Beanstalk

---

A developer wants to focus primarily on application code while AWS handles deployment.

→ Elastic Beanstalk

---

A development environment only needs one application instance.

→ Single Instance deployment

---

A production web application needs scaling and load balancing.

→ Load Balancer + Auto Scaling Group architecture

---

A production worker application does not receive web traffic.

→ Auto Scaling Group only

---

## Exam Keywords

PaaS

Application deployment

Developer focused

Capacity provisioning

Load balancing

Auto Scaling

Health monitoring

---

## Memory Tricks

Beanstalk = Deploy My Application

EC2 = Manage My Server

Lambda = Run My Function

Single Instance = Development

LB + ASG = Production Web

ASG Only = Workers
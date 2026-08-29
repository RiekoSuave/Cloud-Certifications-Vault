## What Problem Does It Solve?

Automates application deployments.

**CodeDeploy** solves the problem of manually deploying and upgrading applications onto servers.

Think:

Application

↓

CodeDeploy

↓

Servers

### Memory Trick

CodeDeploy = Deploy Software

---

## Type

Deployment Automation

---

## What Is AWS CodeDeploy?

AWS CodeDeploy is used to:

Deploy

and

Upgrade

applications automatically.

Your course emphasizes that CodeDeploy works with:

- EC2 instances
- On-premises servers

### Memory Trick

CodeDeploy = DEPLOY CODE

---

## Hybrid Service

CodeDeploy is a:

Hybrid Service

because it can deploy applications to:

AWS

↓

EC2 Instances

and

On-Premises

↓

Servers

### Memory Trick

CodeDeploy = AWS + On-Premises

---

## EC2 Deployments

CodeDeploy works with:

[[02-Compute/EC2]]

Think:

Application Code

↓

[[CodeDeploy]]

↓

EC2 Instance

### Memory Trick

Deploy to EC2 = CodeDeploy

---

## On-Premises Deployments

CodeDeploy can also deploy applications to:

On-Premises Servers

This is why your course identifies CodeDeploy as:

HYBRID

### Memory Trick

On-Premises Deployment = CodeDeploy

---

## CodeDeploy Agent

Your course emphasizes an important requirement.

The:

Servers / Instances

must be:

Provisioned

and

Configured

ahead of time with the:

CodeDeploy Agent

Think:

Provision Server

↓

Configure CodeDeploy Agent

↓

[[CodeDeploy]]

↓

Deploy Application

### Memory Trick

CodeDeploy Agent = Prepare Server for Deployment

---

## Common Use Cases

- Automated application deployments
- Deploying applications to EC2
- Deploying applications to on-premises servers
- Upgrading applications on servers
- Continuous delivery

---

## CodeDeploy vs CodeBuild

### [[CodeBuild]]

Think:

BUILD + TEST

### [[CodeDeploy]]

Think:

DEPLOY

Think:

[[CodeBuild]]

↓

Build Application

↓

[[CodeDeploy]]

↓

Deploy Application

### Memory Trick

CodeBuild = BUILD

CodeDeploy = DEPLOY

---

## CodeDeploy vs CodeCommit

### [[CodeCommit]]

Think:

STORE CODE

### [[CodeDeploy]]

Think:

DEPLOY CODE

### Memory Trick

CodeCommit = STORE

CodeDeploy = DEPLOY

---

## CodeDeploy vs CodePipeline

### [[CodeDeploy]]

Performs the:

DEPLOYMENT

### [[CodePipeline]]

Orchestrates the:

ENTIRE CI/CD PIPELINE

Think:

Code

↓

Build

↓

Test

↓

Deploy

### Memory Trick

CodeDeploy = DEPLOYMENT STEP

CodePipeline = WHOLE PROCESS

---

## CodeDeploy vs Systems Manager

Both can work with infrastructure in AWS and on-premises.

### [[CodeDeploy]]

Think:

DEPLOY / UPGRADE APPLICATIONS

### [[Systems Manager]]

Think:

PATCH / CONFIGURE / RUN COMMANDS AT SCALE

### Memory Trick

CodeDeploy = DEPLOY APPS

Systems Manager = MANAGE SYSTEMS

---

## Developer Tools Workflow

[[CodeCommit]]

↓

STORE CODE

↓

[[CodeBuild]]

↓

BUILD + TEST

↓

[[CodeDeploy]]

↓

DEPLOY CODE

[[CodePipeline]]

↓

ORCHESTRATES THE PROCESS

### Memory Trick

Commit = STORE

Build = BUILD

Deploy = DEPLOY

Pipeline = ORCHESTRATE

---

## Scenario Questions

A company wants to automatically deploy an application onto EC2 instances.

→ CodeDeploy

---

A company wants to automatically deploy an application onto on-premises servers.

→ CodeDeploy

---

A company needs a hybrid application deployment service.

→ CodeDeploy

---

A company needs to deploy and upgrade applications onto servers.

→ CodeDeploy

---

A company needs to prepare servers for CodeDeploy.

→ Install and configure the CodeDeploy Agent

---

A company needs to compile source code and run tests.

→ [[CodeBuild]]

NOT CodeDeploy

---

A company needs a private Git repository.

→ [[CodeCommit]]

NOT CodeDeploy

---

A company needs to orchestrate the entire CI/CD process.

→ [[CodePipeline]]

NOT CodeDeploy

---

A company needs to patch and configure servers at scale.

→ [[Systems Manager]]

NOT CodeDeploy

---

## Don't Confuse These

[[CodeCommit]] = Store Code

[[CodeBuild]] = Build + Test Code

[[CodeDeploy]] = Deploy Code

[[CodePipeline]] = Orchestrate Pipeline

[[Systems Manager]] = Manage / Patch Systems

---

## Exam Keywords

AWS CodeDeploy

Deployment

Application Deployment

Automated Deployment

EC2

On-Premises

Hybrid

CodeDeploy Agent

Application Upgrade

---

## Memory Tricks

CodeDeploy = DEPLOY SOFTWARE

CodeDeploy = DEPLOY CODE

CodeDeploy = EC2 + ON-PREMISES

CodeDeploy = HYBRID

CodeDeploy Agent = PREPARE SERVER

CodeCommit = STORE

CodeBuild = BUILD

CodePipeline = ORCHESTRATE

---

## Quick Cheat Sheet

CodeDeploy = DEPLOY CODE

CodeDeploy = Automated Deployment

CodeDeploy = EC2

CodeDeploy = On-Premises

CodeDeploy = Hybrid Service

CodeDeploy = Deploy + Upgrade Applications

CodeDeploy Agent = Required on Servers / Instances

CodeCommit = STORE

CodeBuild = BUILD + TEST

CodeDeploy = DEPLOY

CodePipeline = ORCHESTRATE

---

## Related Notes

- [[CodeCommit]]
- [[CodeBuild]]
- [[CodePipeline]]
- [[02-Compute/EC2]]
- [[Systems Manager]]
- [[Developer Tools Comparison]]
- [[Developer Tools Cheat Sheet]]
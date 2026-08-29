## What Problem Does It Solve?

Automatically builds and tests application code.

**CodeBuild** solves the overhead of managing your own build servers.

Think:

Source Code

↓

CodeBuild

↓

Compile + Test

↓

Deployable Package

### Memory Trick

CodeBuild = Build Software

---

## Type

Build Automation

---

## What Is AWS CodeBuild?

AWS CodeBuild is a:

Cloud Code Building Service

It can:

- Compile source code
- Run tests
- Produce software packages ready for deployment

Think:

CODE

↓

BUILD

↓

TEST

↓

PACKAGE

### Memory Trick

CodeBuild = Compile + Test

---

## Fully Managed & Serverless

CodeBuild is:

Fully Managed

and

Serverless

You do not need to manage your own:

Build Servers

AWS handles the infrastructure needed to perform the builds.

### Memory Trick

CodeBuild = Build Without Managing Build Servers

---

## Scalable & Highly Available

Your course identifies CodeBuild as:

Continuously Scalable

and

Highly Available

This allows AWS to handle the infrastructure required for your builds.

---

## Pay-As-You-Go

CodeBuild uses:

Pay-As-You-Go Pricing

Your course emphasizes:

You only pay for the:

Build Time

### Memory Trick

CodeBuild = Pay for Build Time

---

## Secure

Your course also identifies CodeBuild as:

Secure

For CCP, keep this association high-level.

---

## Common Use Cases

- Compiling application code
- Running automated tests
- Producing deployable software packages
- CI/CD pipelines
- Automated testing

---

## CodeBuild vs CodeCommit

### [[CodeBuild]]

Think:

BUILD + TEST CODE

### [[CodeCommit]]

Think:

STORE CODE

### Memory Trick

CodeCommit = STORE

CodeBuild = BUILD

---

## CodeBuild vs CodeDeploy

This is one of the most important comparisons.

### [[CodeBuild]]

Compiles and tests the application.

Think:

BUILD

### [[CodeDeploy]]

Deploys the application.

Think:

DEPLOY

### Memory Trick

CodeBuild = BUILD

CodeDeploy = DEPLOY

---

## CodeBuild vs CodePipeline

### [[CodeBuild]]

Performs the:

BUILD / TEST

step.

### [[CodePipeline]]

Orchestrates the overall:

CI/CD WORKFLOW

Think:

Code

↓

Build

↓

Test

↓

Deploy

### Memory Trick

CodeBuild = BUILD STEP

CodePipeline = WHOLE PROCESS

---

## Developer Tools Workflow

The basic workflow from your course is:

[[CodeCommit]]

↓

STORE CODE

↓

[[CodeBuild]]

↓

BUILD + TEST CODE

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

Pipeline = AUTOMATE / CONNECT

---

## Scenario Questions

A company needs to automatically compile source code.

→ CodeBuild

---

A company needs to automatically run tests against its application code.

→ CodeBuild

---

A company wants to produce software packages that are ready to deploy.

→ CodeBuild

---

A company doesn't want to manage its own build servers.

→ CodeBuild

---

A company needs a fully managed, serverless build service.

→ CodeBuild

---

A company needs somewhere to store source code in Git repositories.

→ [[CodeCommit]]

NOT CodeBuild

---

A company needs to automatically deploy an application.

→ [[CodeDeploy]]

NOT CodeBuild

---

A company needs to orchestrate the entire CI/CD process.

→ [[CodePipeline]]

NOT CodeBuild

---

## Don't Confuse These

[[CodeCommit]] = Store Code

[[CodeBuild]] = Build + Test Code

[[CodeDeploy]] = Deploy Code

[[CodePipeline]] = Orchestrate Pipeline

---

## Exam Keywords

AWS CodeBuild

Build

Compile

Source Code

Testing

Automated Testing

Build Automation

Build Server

Software Package

CI/CD

Fully Managed

Serverless

Scalable

Pay-As-You-Go

Build Time

---

## Memory Tricks

CodeBuild = BUILD SOFTWARE

CodeBuild = COMPILE + TEST

CodeBuild = BUILD WITHOUT BUILD SERVERS

CodeCommit = STORE

CodeBuild = BUILD

CodeDeploy = DEPLOY

CodePipeline = ORCHESTRATE

---

## Quick Cheat Sheet

CodeBuild = BUILD + TEST

CodeBuild = Compile Source Code

CodeBuild = Run Tests

CodeBuild = Produce Deployable Packages

CodeBuild = Fully Managed

CodeBuild = Serverless

CodeBuild = Scalable + Highly Available

CodeBuild = Pay for Build Time

CodeCommit = STORE

CodeBuild = BUILD

CodeDeploy = DEPLOY

CodePipeline = ORCHESTRATE

---

## Related Notes

- [[CodeCommit]]
- [[CodeDeploy]]
- [[CodePipeline]]
- [[Developer Tools Comparison]]
- [[Developer Tools Cheat Sheet]]
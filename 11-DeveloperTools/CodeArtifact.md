## What Problem Does It Solve?

Stores software packages and dependencies in AWS.

**CodeArtifact** solves the need for developers to store the software packages and dependencies used by their applications.

Think:

Application

↓

Needs Packages / Dependencies

↓

CodeArtifact

### Memory Trick

CodeArtifact = Store Packages

---

## Type

Software Package Storage

---

## What Is AWS CodeArtifact?

AWS CodeArtifact is used to:

STORE SOFTWARE PACKAGES

and

STORE DEPENDENCIES

on AWS.

### Memory Trick

CodeArtifact = Package Storage

---

## Software Packages & Dependencies

Applications often rely on:

Packages

and

Dependencies

CodeArtifact provides a place in AWS to store them.

Think:

SOURCE CODE

↓

[[CodeCommit]]

PACKAGES / DEPENDENCIES

↓

[[CodeArtifact]]

### Memory Trick

CodeCommit = CODE

CodeArtifact = PACKAGES

---

## CodeArtifact vs CodeCommit

This is the most important comparison for CCP.

### [[CodeCommit]]

Stores:

SOURCE CODE

Think:

Git Repository

### [[CodeArtifact]]

Stores:

SOFTWARE PACKAGES / DEPENDENCIES

### Memory Trick

CodeCommit = STORE CODE

CodeArtifact = STORE PACKAGES

---

## Developer Services Workflow

Your course groups CodeArtifact with the AWS Developer Services:

[[CodeCommit]]

↓

STORE CODE

[[CodeBuild]]

↓

BUILD + TEST CODE

[[CodeDeploy]]

↓

DEPLOY CODE

[[CodePipeline]]

↓

ORCHESTRATE PIPELINE

[[CodeArtifact]]

↓

STORE PACKAGES / DEPENDENCIES

[[AWS CDK]]

↓

DEFINE INFRASTRUCTURE WITH CODE

---

## Scenario Questions

A company needs to store software packages on AWS.

→ CodeArtifact

---

Developers need somewhere to store application dependencies in AWS.

→ CodeArtifact

---

A company needs to store source code in a private Git repository.

→ [[CodeCommit]]

NOT CodeArtifact

---

A company needs to compile and test source code.

→ [[CodeBuild]]

NOT CodeArtifact

---

A company needs to deploy application code.

→ [[CodeDeploy]]

NOT CodeArtifact

---

A company needs to orchestrate its CI/CD pipeline.

→ [[CodePipeline]]

NOT CodeArtifact

---

## Don't Confuse These

[[CodeCommit]] = Store Source Code

[[CodeArtifact]] = Store Packages / Dependencies

[[CodeBuild]] = Build + Test

[[CodeDeploy]] = Deploy

[[CodePipeline]] = Orchestrate

[[AWS CDK]] = Define Infrastructure Using Programming Language

---

## Exam Keywords

AWS CodeArtifact

Software Packages

Dependencies

Package Storage

---

## Memory Tricks

CodeArtifact = STORE PACKAGES

CodeArtifact = STORE DEPENDENCIES

CodeCommit = CODE

CodeArtifact = PACKAGES

---

## Quick Cheat Sheet

CodeArtifact = STORE PACKAGES

CodeArtifact = STORE DEPENDENCIES

CodeCommit = SOURCE CODE

CodeBuild = BUILD + TEST

CodeDeploy = DEPLOY

CodePipeline = ORCHESTRATE

AWS CDK = INFRASTRUCTURE WITH PROGRAMMING LANGUAGE

---

## Related Notes

- [[CodeCommit]]
- [[CodeBuild]]
- [[CodeDeploy]]
- [[CodePipeline]]
- [[AWS CDK]]
- [[Developer Tools Comparison]]
- [[Developer Tools Cheat Sheet]]
## What Problem Does It Solve?

Automates configuration tasks when an EC2 instance is first launched.

---

## What Is Bootstrapping?

Bootstrapping means automatically running commands when a machine starts.

EC2 User Data can be used as a bootstrap script.

---

## When Does It Run?

The User Data script runs when the EC2 instance is first started.

It runs with root privileges.

---

## Common Uses

EC2 User Data can automatically:

- Install system updates
- Install software
- Download files
- Configure applications
- Perform startup configuration

---

## Example Scenario

You launch 20 EC2 web servers.

Instead of manually installing Apache on every server, User Data can automatically install and configure the software when each instance launches.

---

## Why It Matters

User Data makes EC2 deployment:

- Faster
- Repeatable
- Automated
- Less dependent on manual configuration

---

## Exam Keywords

Bootstrap

First launch

Startup script

Automation

EC2 configuration

---

## Memory Trick

User Data = Setup script when EC2 launches

---

## Exam Scenario

A company wants every newly launched EC2 instance to automatically install required software.

Answer:

EC2 User Data
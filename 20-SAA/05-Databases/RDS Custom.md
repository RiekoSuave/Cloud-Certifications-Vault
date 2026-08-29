## What Problem Does It Solve?

Normal RDS is a:

MANAGED DATABASE SERVICE

AWS manages:

OPERATING SYSTEM

↓

DATABASE SOFTWARE

↓

PATCHING

↓

UNDERLYING INFRASTRUCTURE

This is convenient, but some workloads require:

OPERATING SYSTEM ACCESS

↓

DATABASE CUSTOMIZATION

↓

SPECIAL PATCHES

↓

NATIVE DATABASE FEATURES

Normal RDS does not provide this level of control.

RDS Custom provides:

MANAGED DATABASE BENEFITS

+

LOW-LEVEL ADMINISTRATIVE ACCESS

Think:

NEED RDS

BUT ALSO NEED OS ACCESS?

↓

RDS CUSTOM

### Memory Trick

RDS CUSTOM

=

MANAGED DB + CUSTOM OS ACCESS

---

## What Is RDS Custom?

RDS Custom is a managed database option designed for workloads that require:

DATABASE CUSTOMIZATION

and:

OPERATING SYSTEM CUSTOMIZATION

Think:

NORMAL RDS

↓

AWS CONTROLS OS

RDS CUSTOM

↓

YOU CAN ACCESS OS

### Memory Trick

CUSTOM

=

MORE CONTROL

---

## Supported Database Engines

Your SAA course specifically highlights RDS Custom for:

ORACLE

and:

MICROSOFT SQL SERVER

Think:

RDS CUSTOM

↓

ORACLE

or:

SQL SERVER

### Memory Trick

RDS CUSTOM

=

ORACLE + SQL SERVER

---

## Why RDS Custom Exists

Some enterprise database applications require:

SPECIAL OPERATING SYSTEM SETTINGS

↓

CUSTOM DATABASE CONFIGURATION

↓

MANUAL PATCHING

↓

NATIVE DATABASE FEATURES

These requirements may not fit:

STANDARD RDS

RDS Custom provides:

MORE ADMINISTRATIVE CONTROL

while retaining AWS database management capabilities.

### Memory Trick

LEGACY / SPECIAL DATABASE REQUIREMENTS

↓

RDS CUSTOM

---

## Standard RDS vs RDS Custom

### Standard RDS

AWS manages:

DATABASE

and:

OPERATING SYSTEM

You do not normally have:

SSH ACCESS

or:

HOST-LEVEL ADMIN ACCESS

Think:

MORE AWS MANAGEMENT

↓

LESS LOW-LEVEL CONTROL

---

### RDS Custom

You receive:

ADMINISTRATIVE ACCESS

to:

DATABASE

and:

UNDERLYING OS

Think:

MORE CUSTOMER CONTROL

↓

MORE CUSTOMIZATION

### Memory Trick

RDS

=

AWS CONTROLS OS

RDS CUSTOM

=

YOU CAN CUSTOMIZE OS

---

## Underlying EC2 Instance

RDS Custom runs on underlying infrastructure that you can access.

Think:

RDS CUSTOM DATABASE

↓

UNDERLYING EC2 INSTANCE

↓

OPERATING SYSTEM

↓

DATABASE SOFTWARE

Unlike normal RDS, you can access and customize this environment.

### Memory Trick

RDS CUSTOM

=

ACCESS UNDERLYING INSTANCE

---

## SSH Access

RDS Custom allows access to the underlying EC2 instance using:

SSH

Think:

ADMINISTRATOR

↓

SSH

↓

UNDERLYING EC2

↓

CUSTOMIZE DATABASE HOST

This is a major distinction from:

NORMAL RDS

### Memory Trick

NEED SSH?

↓

RDS CUSTOM

---

## SSM Session Manager Access

You can also access the underlying instance using:

SSM SESSION MANAGER

Think:

ADMINISTRATOR

↓

[Systems Manager](<Systems Manager>)

↓

SESSION MANAGER

↓

RDS CUSTOM HOST

This provides another method for managing the underlying environment.

### Memory Trick

RDS CUSTOM ACCESS

=

SSH OR SSM

---

## What Can You Customize?

Your course highlights several customization capabilities.

You can:

CONFIGURE SETTINGS

↓

INSTALL PATCHES

↓

ENABLE NATIVE FEATURES

Think:

RDS CUSTOM

↓

CUSTOM OS / DATABASE CONFIGURATION

### Memory Trick

CONFIGURE

PATCH

ENABLE

=

RDS CUSTOM

---

## Configure Settings

Some applications require specific:

OPERATING SYSTEM SETTINGS

or:

DATABASE SETTINGS

With RDS Custom:

YOU CAN MODIFY THESE SETTINGS

Think:

APPLICATION REQUIREMENT

↓

CUSTOM DB SETTING

↓

RDS CUSTOM

This is not normally possible at the same level with:

STANDARD RDS

---

## Install Patches

RDS Custom allows you to:

INSTALL PATCHES

Think:

CUSTOM APPLICATION

↓

REQUIRES SPECIFIC PATCH

↓

ADMINISTRATOR APPLIES PATCH

This gives you more control over:

PATCH TIMING

and:

PATCH CONTENT

than standard managed RDS.

### Memory Trick

SPECIAL PATCH?

↓

RDS CUSTOM

---

## Enable Native Features

Certain Oracle or SQL Server workloads may depend on:

NATIVE DATABASE FEATURES

that require:

HOST / DATABASE CUSTOMIZATION

RDS Custom allows you to:

ENABLE THESE FEATURES

Think:

APPLICATION REQUIRES NATIVE DB FEATURE

↓

RDS CUSTOM

### Memory Trick

NATIVE FEATURE REQUIREMENT

=

RDS CUSTOM CLUE

---

## Full Administrative Access

The SAA slides describe RDS Custom as providing:

FULL ADMIN ACCESS

to:

UNDERLYING OS

and:

DATABASE

Think:

ADMINISTRATOR

↓

OS ACCESS

+

DATABASE ACCESS

This is the core difference from:

STANDARD RDS

### Memory Trick

RDS CUSTOM

=

FULLER ADMIN CONTROL

---

## Automation Mode

RDS Custom still includes AWS management automation.

But when performing certain customizations, your course says to:

DEACTIVATE AUTOMATION MODE

Think:

AWS AUTOMATION ACTIVE

↓

NEED CUSTOMIZATION

↓

DISABLE AUTOMATION MODE

↓

MAKE CUSTOM CHANGES

### Memory Trick

CUSTOMIZE?

↓

AUTOMATION MODE OFF

---

## Why Disable Automation Mode?

AWS automation normally manages aspects of the RDS Custom environment.

When you need to perform:

LOW-LEVEL CUSTOMIZATION

you temporarily disable:

AUTOMATION MODE

Think:

AWS MANAGING

↓

PAUSE AUTOMATION

↓

YOU CUSTOMIZE

This helps prevent AWS automation from interfering while changes are being made.

---

## Take a Snapshot First

Your course specifically recommends:

TAKE A DB SNAPSHOT

before performing RDS Custom modifications.

Think:

BEFORE CUSTOMIZATION

↓

DB SNAPSHOT

↓

DISABLE AUTOMATION MODE

↓

CUSTOMIZE

### Memory Trick

SNAPSHOT FIRST

↓

CUSTOMIZE SECOND

---

## Safe Customization Workflow

Think:

RDS CUSTOM DATABASE

↓

TAKE DB SNAPSHOT

↓

DEACTIVATE AUTOMATION MODE

↓

ACCESS HOST

↓

SSH / SSM

↓

MAKE CUSTOMIZATION

↓

DATABASE CONTINUES WITH CUSTOM CONFIG

### Memory Trick

SNAPSHOT

↓

AUTOMATION OFF

↓

CUSTOMIZE

---

## Why Take a Snapshot?

Custom OS or database modifications introduce:

CHANGE RISK

Think:

PATCH

↓

CONFIGURATION CHANGE

↓

NATIVE FEATURE

↓

POSSIBLE PROBLEM

A snapshot provides:

RECOVERY OPTION

before performing the customization.

### Memory Trick

BEFORE RISKY DB CHANGE

=

SNAPSHOT

---

## RDS Custom vs Database on EC2

Both can provide:

OPERATING SYSTEM ACCESS

But they represent different management models.

### Database on EC2

YOU MANAGE:

EC2

↓

OS

↓

DATABASE INSTALLATION

↓

PATCHING

↓

BACKUPS

↓

DATABASE OPERATIONS

Think:

MAXIMUM CONTROL

+

MAXIMUM MANAGEMENT

---

### RDS Custom

AWS still provides:

RDS MANAGEMENT CAPABILITIES

while giving you:

OS + DATABASE ADMIN ACCESS

Think:

MANAGED DATABASE

+

CUSTOM CONTROL

### Memory Trick

EC2 DATABASE

=

YOU MANAGE EVERYTHING

RDS CUSTOM

=

MANAGED + CUSTOMIZABLE

---

## RDS Custom vs Standard RDS

### Standard RDS

Best when:

AWS CAN MANAGE THE HOST

and you do not need:

OS-LEVEL ACCESS

---

### RDS Custom

Best when:

APPLICATION REQUIRES OS / DATABASE CUSTOMIZATION

Think:

NO OS ACCESS NEEDED?

↓

STANDARD RDS

OS ACCESS REQUIRED?

↓

RDS CUSTOM

### Memory Trick

STANDARD

=

MANAGED

CUSTOM

=

MANAGED + ACCESS

---

## RDS Custom vs Aurora

Do not confuse:

RDS CUSTOM

with:

[Aurora](Aurora)

### Aurora

AWS-designed relational database compatible with:

MYSQL

and:

POSTGRESQL

Designed for:

PERFORMANCE

↓

SCALABILITY

↓

HIGH AVAILABILITY

---

### RDS Custom

Designed for:

ORACLE

and:

SQL SERVER

workloads requiring:

UNDERLYING OS / DATABASE ACCESS

Think:

CLOUD-OPTIMIZED MYSQL / POSTGRES?

↓

AURORA

CUSTOM ORACLE / SQL SERVER HOST?

↓

RDS CUSTOM

---

## Normal RDS SSH Trap

Remember:

NORMAL RDS

does:

NOT

provide SSH access.

Think:

NEED SSH TO NORMAL RDS?

↓

NOT POSSIBLE

Need:

MANAGED DB + SSH?

↓

RDS CUSTOM

### Memory Trick

RDS

=

NO SSH

RDS CUSTOM

=

SSH / SSM

---

## Enterprise Application Scenario

Imagine a company runs a:

LEGACY ORACLE APPLICATION

The application requires:

CUSTOM OS SETTINGS

↓

SPECIFIC DATABASE PATCH

↓

NATIVE ORACLE FEATURE

The company still wants:

AWS MANAGED DATABASE OPERATIONS

Think:

DATABASE ON EC2?

↓

FULL CONTROL BUT HIGH MANAGEMENT

STANDARD RDS?

↓

NOT ENOUGH CONTROL

RDS CUSTOM?

↓

MANAGED + CUSTOMIZATION

Answer:

RDS CUSTOM

---

## SQL Server Scenario

Imagine a Microsoft SQL Server workload requires:

HOST-LEVEL CONFIGURATION

and:

CUSTOM DATABASE SETTINGS

Requirement:

KEEP DATABASE MANAGED WHERE POSSIBLE

but:

NEED OS ACCESS

Think:

SQL SERVER

+

OS ACCESS

↓

RDS CUSTOM

### Memory Trick

SQL SERVER + CUSTOM HOST

=

RDS CUSTOM

---

## Architecture Thinking

Normal RDS:

APPLICATION

↓

RDS

↓

AWS-MANAGED DATABASE + OS

↓

NO HOST ACCESS

RDS Custom:

APPLICATION

↓

RDS CUSTOM

↓

DATABASE

↓

UNDERLYING EC2 / OS

↑

ADMINISTRATOR

↓

SSH / SSM

Think:

APPLICATION USES DATABASE

while:

ADMINISTRATOR CAN CUSTOMIZE HOST

---

## Management Responsibility Thinking

As AWS gives you:

MORE ACCESS

you also take on:

MORE RESPONSIBILITY

Think:

STANDARD RDS

↓

MORE AWS CONTROL

RDS CUSTOM

↓

MORE CUSTOMER CONTROL

DATABASE ON EC2

↓

MOST CUSTOMER CONTROL

### Memory Trick

MORE CONTROL

=

MORE RESPONSIBILITY

---

## Control Spectrum

Think:

STANDARD RDS

↓

MOST MANAGED

↓

RDS CUSTOM

↓

MANAGED + CUSTOMIZABLE

↓

DATABASE ON EC2

↓

MOST CONTROL

### Memory Trick

RDS

↓

RDS CUSTOM

↓

EC2 DATABASE

=

INCREASING CONTROL

---

## Scenario Recognition

Need managed Oracle with operating system customization?

→ RDS Custom

---

Need managed SQL Server with operating system customization?

→ RDS Custom

---

Need SSH access to the underlying database host?

→ RDS Custom

---

Need SSM Session Manager access to the database host?

→ RDS Custom

---

Need to install custom database or OS patches?

→ RDS Custom

---

Need to configure host-level settings?

→ RDS Custom

---

Need native Oracle / SQL Server features requiring host access?

→ RDS Custom

---

Need full administrative access to the underlying OS?

→ RDS Custom

---

Need to customize a normal RDS MySQL database host through SSH?

→ Normal RDS does not support this

---

Need AWS to manage the database completely with no host access?

→ Standard RDS

---

Need complete infrastructure control and are willing to manage everything?

→ Database on EC2

---

Need AWS-optimized MySQL / PostgreSQL?

→ Aurora

NOT RDS Custom

---

## Exam Traps

RDS CUSTOM

=

ORACLE + SQL SERVER

---

RDS CUSTOM

=

OS CUSTOMIZATION

---

RDS CUSTOM

=

DATABASE CUSTOMIZATION

---

RDS CUSTOM

=

SSH ACCESS

---

RDS CUSTOM

=

SSM SESSION MANAGER ACCESS

---

NORMAL RDS

=

NO SSH

---

RDS CUSTOM

=

FULL ADMIN ACCESS TO OS + DATABASE

---

CUSTOM SETTINGS

=

RDS CUSTOM

---

CUSTOM PATCHES

=

RDS CUSTOM

---

NATIVE DATABASE FEATURES

=

RDS CUSTOM

---

BEFORE CUSTOMIZATION

=

TAKE DB SNAPSHOT

---

CUSTOMIZATION

=

DEACTIVATE AUTOMATION MODE

---

RDS CUSTOM

≠

DATABASE ON EC2

---

RDS CUSTOM

=

MANAGED + CUSTOMIZABLE

EC2 DATABASE

=

CUSTOMER MANAGES EVERYTHING

---

RDS CUSTOM

≠

AURORA

---

AURORA

=

MYSQL / POSTGRES COMPATIBLE CLOUD-NATIVE DB

RDS CUSTOM

=

ORACLE / SQL SERVER CUSTOM HOST ACCESS

---

## Quick Cheat Sheet

RDS CUSTOM

=

MANAGED DATABASE + HOST ACCESS

SUPPORTED ENGINES IN COURSE

=

ORACLE

SQL SERVER

UNDERLYING OS ACCESS

=

YES

DATABASE ADMIN ACCESS

=

YES

SSH

=

YES

SSM SESSION MANAGER

=

YES

CUSTOM SETTINGS

=

YES

CUSTOM PATCHES

=

YES

NATIVE FEATURES

=

YES

AUTOMATION MODE

=

DEACTIVATE FOR CUSTOMIZATION

BEFORE CUSTOMIZATION

=

TAKE DB SNAPSHOT

STANDARD RDS SSH

=

NO

RDS CUSTOM SSH

=

YES

STANDARD RDS

=

MORE MANAGED

RDS CUSTOM

=

MORE CONTROL

DATABASE ON EC2

=

MOST CONTROL + MOST MANAGEMENT

---

## Master Memory Trick

QUESTION:

DO I NEED TO TOUCH THE DATABASE HOST?

NO

↓

STANDARD RDS

YES

↓

RDS CUSTOM

Think:

RDS CUSTOM

=

ORACLE / SQL SERVER

↓

SSH / SSM

↓

OS ACCESS

↓

DATABASE ACCESS

↓

CUSTOM SETTINGS

↓

CUSTOM PATCHES

↓

NATIVE FEATURES

Before changing:

SNAPSHOT

↓

AUTOMATION MODE OFF

↓

CUSTOMIZE

### Final Rule

MANAGED DATABASE

+

ORACLE / SQL SERVER

+

NEED OS ACCESS

↓

RDS CUSTOM

---

## Related Notes

- [RDS Overview](<RDS Overview>)
- [RDS & Aurora Security](<RDS & Aurora Security>)
- [RDS Backups](<RDS Backups>)
- [RDS Multi-AZ](<RDS Multi-AZ>)
- [RDS Proxy](<RDS Proxy>)
- [Aurora](Aurora)
- [EC2](EC2)
- [Systems Manager](<Systems Manager>)
- [SAA Databases Cheat Sheet](<SAA Databases Cheat Sheet>)
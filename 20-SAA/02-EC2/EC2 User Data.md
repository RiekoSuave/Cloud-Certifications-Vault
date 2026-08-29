## What Problem Does It Solve?

EC2 User Data lets you:

AUTOMATE TASKS

when an EC2 instance launches.

Instead of manually configuring every new server, you can provide a script that performs startup tasks automatically.

### Memory Trick

User Data = AUTOMATE EC2 STARTUP

---

## What Is EC2 User Data?

EC2 User Data is used to:

BOOTSTRAP

an EC2 instance.

Bootstrapping means:

LAUNCHING COMMANDS

when a machine starts.

Think:

EC2 LAUNCHES

↓

USER DATA SCRIPT

↓

AUTOMATIC SETUP

### Memory Trick

User Data = BOOTSTRAP

---

## When Does User Data Run?

Your course states that the EC2 User Data script:

RUNS ONCE

at the:

FIRST START

of the EC2 instance.

Think:

FIRST BOOT

↓

RUN SCRIPT

### Exam Keyword

FIRST BOOT

→ EC2 USER DATA

---

## What Can User Data Do?

EC2 User Data can automate boot tasks such as:

- Installing updates
- Installing software
- Downloading common files from the internet
- Performing other startup configuration tasks

Think:

NEW EC2 INSTANCE

↓

UPDATE

↓

INSTALL

↓

DOWNLOAD

↓

CONFIGURE

---

## User Data Permissions

EC2 User Data scripts run with:

ROOT USER

privileges.

This means the startup commands have elevated permissions on the instance.

### Memory Trick

User Data = ROOT

---

## Example Architecture

Without User Data:

Launch EC2

↓

Connect to Instance

↓

Install Software Manually

↓

Configure Server Manually

With User Data:

Launch EC2

↓

USER DATA

↓

Install / Configure Automatically

↓

SERVER READY

---

## Bootstrapping Example

Imagine you need to launch a web server.

User Data could perform startup tasks such as:

EC2 LAUNCH

↓

UPDATE SERVER

↓

INSTALL WEB SERVER

↓

DOWNLOAD FILES

↓

INSTANCE CONFIGURED

This avoids performing the same setup manually every time a new EC2 instance launches.

---

## Why User Data Matters

User Data is useful when EC2 instances need:

REPEATABLE INITIAL CONFIGURATION

Think:

Launch Instance #1

↓

Same Startup Script

Launch Instance #2

↓

Same Startup Script

Launch Instance #3

↓

Same Startup Script

### Memory Trick

User Data = REPEATABLE STARTUP

---

## User Data vs Manual Configuration

| Method | Setup |
| --- | --- |
| Manual | Configure after launch |
| User Data | Automate startup tasks |

### Memory Trick

Manual = YOU DO IT

User Data = EC2 DOES IT

---

## Scenario Recognition

Need to automatically install software when an EC2 instance launches?

→ EC2 User Data

---

Need commands to execute during the first startup of an EC2 instance?

→ EC2 User Data

---

Need to automatically download common files when launching an instance?

→ EC2 User Data

---

Need to bootstrap an EC2 instance?

→ EC2 User Data

---

Need startup commands with root privileges?

→ EC2 User Data

---

## Exam Traps

User Data = BOOTSTRAPPING

User Data runs:

ONCE

at:

FIRST START

User Data scripts run with:

ROOT PRIVILEGES

User Data is commonly used for:

UPDATES

INSTALLATION

DOWNLOADS

STARTUP TASKS

---

## Quick Cheat Sheet

EC2 USER DATA

= BOOTSTRAP

BOOTSTRAP

= COMMANDS AT STARTUP

RUNS

= ONCE

WHEN?

= FIRST START

PRIVILEGES

= ROOT

COMMON TASKS

= UPDATE + INSTALL + DOWNLOAD + CONFIGURE

---

## Master Memory Trick

EC2 STARTS

↓

USER DATA RUNS

↓

SERVER CONFIGURES ITSELF

### Four Things to Remember

USER DATA

=

BOOTSTRAP

FIRST START

ROOT

AUTOMATION

---

## Related Notes

- [[EC2]]
- [[02-Compute/EC2 Instance Types]]
- [[EC2 Security Groups]]
- [[EC2 IAM Roles]]
- [[Auto Scaling Groups]]
- [[SAA EC2 Cheat Sheet]]
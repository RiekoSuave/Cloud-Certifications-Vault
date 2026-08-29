## What Problem Does It Solve?

IAM Permission Boundaries limit the:

MAXIMUM PERMISSIONS

an IAM entity can receive.

Think:

IAM Policy

↓

Wants to grant permissions

BUT

↓

Permission Boundary

↓

Sets the MAXIMUM

### Memory Trick

Permission Boundary = PERMISSION CEILING

---

## What Is a Permission Boundary?

A Permission Boundary is an advanced IAM feature that uses a:

MANAGED POLICY

to define the maximum permissions an IAM entity can receive.

Think:

Possible Permissions

↑

BOUNDARY / CEILING

↑

Cannot Go Above This

### Memory Trick

Boundary = HOW HIGH PERMISSIONS CAN GO

---

## Supported IAM Identities

Permission Boundaries are supported for:

IAM USERS ✅

IAM ROLES ✅

They are NOT supported for:

IAM GROUPS ❌

### Exam Trap

Users = YES

Roles = YES

Groups = NO

---

## Permission Boundary vs IAM Policy

This distinction is extremely important.

### IAM Policy

Grants permissions.

Think:

WHAT ARE YOU ALLOWED TO DO?

### Permission Boundary

Sets the maximum permissions that can be granted.

Think:

WHAT IS THE MOST YOU COULD EVER BE ALLOWED TO DO?

### Memory Trick

Policy = GRANT

Boundary = LIMIT

---

## How They Work Together

Think:

IAM POLICY

+

PERMISSION BOUNDARY

↓

EFFECTIVE PERMISSIONS

The permissions must fit within the boundary.

---

## Example

Imagine a Permission Boundary allows:

S3

ONLY

But an IAM Policy grants:

EC2

The IAM Policy is trying to grant EC2 access.

However:

EC2

↓

OUTSIDE BOUNDARY

↓

NO EC2 PERMISSION

### Memory Trick

Policy cannot break through the Boundary.

---

## Course Example

Your SAA course shows that:

IAM Permission Boundary

+

IAM Permissions Through IAM Policy

can result in:

NO PERMISSIONS

This demonstrates that attaching an IAM policy does NOT automatically mean those permissions become usable.

The permissions must also fit within the Permission Boundary.

---

## Prevent Privilege Escalation

One major use case is preventing:

PRIVILEGE ESCALATION

Think:

Developer

↓

Can Manage Own Permissions

BUT

↓

Permission Boundary

↓

Cannot Become Administrator

### Memory Trick

Boundary = YOU CAN'T MAKE YOURSELF ADMIN

---

## Developer Scenario

A company wants developers to:

SELF-ASSIGN POLICIES

and

MANAGE THEIR OWN PERMISSIONS

But the company does NOT want developers to:

MAKE THEMSELVES ADMINISTRATORS

Solution:

IAM PERMISSION BOUNDARY

Think:

Developer Freedom

↓

Inside Boundary

↓

No Privilege Escalation

---

## Delegating IAM Administration

Permission Boundaries can also allow organizations to delegate responsibilities to:

NON-ADMINISTRATORS

Example:

Allow someone to:

CREATE IAM USERS

while still keeping their permissions within an approved boundary.

### Architecture Idea

Delegate Tasks

↓

Permission Boundary

↓

Limit Maximum Authority

---

## Restrict One Specific User

Your course highlights another useful distinction.

Need to restrict:

ONE SPECIFIC USER

→ Permission Boundary

Need broader account-level restrictions?

→ [[AWS Organizations SCP]]

### Memory Trick

Boundary = IDENTITY LIMIT

SCP = ORGANIZATION / ACCOUNT LIMIT

---

## Permission Boundary + SCP

Permission Boundaries can be used together with:

[[AWS Organizations SCP]]

Think:

AWS Organizations SCP

+

Permission Boundary

+

IAM Policy

↓

Permission Evaluation

We'll connect these concepts later in:

[[IAM Policy Evaluation Logic]]

---

## Permission Boundary vs SCP

### Permission Boundary

Applies to specific:

USERS

or

ROLES

Think:

IDENTITY LEVEL

### SCP

Used through:

AWS ORGANIZATIONS

Think:

ORGANIZATION / ACCOUNT GOVERNANCE

### Memory Trick

Boundary = PERSON / ROLE LIMIT

SCP = ORGANIZATION LIMIT

---

## Scenario Recognition

A company wants to define the maximum permissions an IAM user can ever receive.

→ IAM Permission Boundary

---

A developer can manage their own IAM permissions but must never be able to make themselves an administrator.

→ IAM Permission Boundary

---

A company wants a non-administrator to create IAM users but wants to limit how powerful those users can become.

→ IAM Permission Boundary

---

A company wants to restrict one specific IAM user rather than applying a restriction across an AWS account.

→ IAM Permission Boundary

---

A company wants to apply a Permission Boundary to an IAM Group.

→ NOT SUPPORTED

---

## Exam Traps

Permission Boundary ≠ IAM Policy

IAM Policy = GRANTS PERMISSIONS

Permission Boundary = MAXIMUM PERMISSIONS

Permission Boundary does NOT mean:

"Give these permissions"

It means:

"Permissions cannot exceed this limit"

Users = Supported

Roles = Supported

Groups = NOT Supported

Permission Boundaries can help prevent privilege escalation.

---

## Quick Cheat Sheet

Permission Boundary = MAXIMUM PERMISSIONS

Policy = GRANT

Boundary = LIMIT

Users = YES

Roles = YES

Groups = NO

Developer self-manages permissions?

→ Boundary prevents ADMIN escalation

Restrict one identity?

→ Permission Boundary

Organization/account restriction?

→ SCP

---

## Master Memory Trick

IAM POLICY

=

WHAT YOU GET

PERMISSION BOUNDARY

=

MOST YOU CAN GET

---

## Related Notes

- [[IAM Policies]]
- [[IAM Roles]]
- [[IAM Conditions]]
- [[IAM Policy Evaluation Logic]]
- [[AWS Organizations SCP]]
- [[IAM Comparison]]
- [[SAA IAM Cheat Sheet]]
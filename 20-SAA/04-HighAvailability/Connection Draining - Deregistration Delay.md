## What Problem Does It Solve?

When an EC2 instance is removed from a Load Balancer:

ACTIVE USERS

may still have:

IN-FLIGHT REQUESTS

If the target is removed immediately:

ACTIVE REQUEST

↓

TARGET REMOVED

↓

REQUEST INTERRUPTED

Connection Draining / Deregistration Delay gives existing requests time to:

FINISH

before the target is fully removed.

### Memory Trick

DEREGISTRATION DELAY

=

FINISH CURRENT REQUESTS BEFORE LEAVING

---

## What Is Connection Draining?

Connection Draining allows a Load Balancer to:

STOP SENDING NEW REQUESTS

to a target that is:

DEREGISTERING

or:

UNHEALTHY

while allowing:

EXISTING CONNECTIONS

to complete.

Think:

TARGET BEING REMOVED

↓

NO NEW CONNECTIONS

↓

FINISH EXISTING CONNECTIONS

↓

REMOVE TARGET

### Memory Trick

DRAIN

=

NO NEW WORK

BUT

FINISH CURRENT WORK

---

## Connection Draining vs Deregistration Delay

AWS uses different terminology depending on the Load Balancer.

### Classic Load Balancer

CONNECTION DRAINING

### Application Load Balancer

DEREGISTRATION DELAY

### Network Load Balancer

DEREGISTRATION DELAY

Think:

CLB

=

CONNECTION DRAINING

ALB / NLB

=

DEREGISTRATION DELAY

### Memory Trick

OLD CLB

=

DRAINING

NEWER ALB / NLB

=

DEREGISTRATION DELAY

---

## How It Works

Imagine:

USER A

↓

LOAD BALANCER

↓

EC2 #1

EC2 #1 is currently processing:

A LONG REQUEST

Now EC2 #1 begins:

DEREGISTRATION

The Load Balancer will:

STOP SENDING NEW REQUESTS

to EC2 #1.

But:

USER A'S EXISTING REQUEST

can continue.

Think:

EC2 #1

↓

DEREGISTERING

↓

NEW REQUESTS = NO

EXISTING REQUESTS = FINISH

---

## New Requests During Deregistration

While a target is draining:

NEW REQUESTS

are sent to:

OTHER HEALTHY TARGETS

Think:

EC2 #1

=

DRAINING

EC2 #2

=

HEALTHY

EC2 #3

=

HEALTHY

New traffic:

LOAD BALANCER

↓

EC2 #2 / EC2 #3

Existing traffic on EC2 #1:

↓

ALLOWED TO COMPLETE

---

## Deregistration Delay Timeout

The Deregistration Delay can be configured between:

1 SECOND

and:

3600 SECONDS

The default is:

300 SECONDS

Think:

MINIMUM

=

1 SECOND

DEFAULT

=

300 SECONDS

MAXIMUM

=

3600 SECONDS

### Memory Trick

DEREGISTRATION DELAY

=

1 → 300 DEFAULT → 3600

---

## What Happens During the Delay?

During the Deregistration Delay:

TARGET

↓

FINISHES ACTIVE REQUESTS

while:

LOAD BALANCER

↓

STOPS SENDING NEW REQUESTS

When the timeout expires:

TARGET

↓

FULLY DEREGISTERED

Think:

DRAIN

↓

WAIT

↓

REMOVE

---

## Why Is the Default 300 Seconds?

The default:

300 SECONDS

gives applications time to complete:

IN-FLIGHT REQUESTS

before the target disappears.

Think:

TARGET REMOVAL

↓

5-MINUTE DEFAULT WINDOW

↓

ACTIVE REQUESTS FINISH

### Memory Trick

300 SECONDS

=

5 MINUTES

---

## Long Requests

If your application has:

LONG-LIVED REQUESTS

or:

LONG PROCESSING TIMES

you may want a:

HIGHER DEREGISTRATION DELAY

Think:

REQUEST TAKES MINUTES

↓

LONGER DRAINING PERIOD

↓

ALLOW REQUEST TO COMPLETE

### Memory Trick

LONG REQUESTS

=

LONGER DELAY

---

## Short Requests

If your application has:

VERY SHORT REQUESTS

you may want a:

LOWER DEREGISTRATION DELAY

Think:

REQUESTS COMPLETE QUICKLY

↓

NO NEED TO WAIT 300 SECONDS

↓

LOWER DELAY

This allows instances to:

DEREGISTER FASTER

### Memory Trick

SHORT REQUESTS

=

SHORTER DELAY

---

## Example

Imagine an application where requests normally take:

1 SECOND

Waiting:

300 SECONDS

for an instance to deregister may be unnecessary.

You could configure a lower value such as:

30 SECONDS

Think:

FAST APPLICATION

↓

SHORT DRAINING WINDOW

↓

FASTER INSTANCE REMOVAL

---

## Connection Draining and Auto Scaling

Connection Draining is especially important with:

[Auto Scaling Groups](<Auto Scaling Groups>)

Imagine traffic decreases.

The Auto Scaling Group decides to:

TERMINATE EC2 #3

Think:

ASG

↓

SCALE IN

↓

EC2 #3 SELECTED

↓

LOAD BALANCER DEREGISTERS TARGET

↓

DEREGISTRATION DELAY

↓

EXISTING REQUESTS FINISH

↓

INSTANCE REMOVED

### Memory Trick

ASG SCALE IN

+

DEREGISTRATION DELAY

=

GRACEFUL REMOVAL

---

## Why This Matters for Scaling In

Without Deregistration Delay:

ASG SCALE IN

↓

INSTANCE REMOVED

↓

ACTIVE REQUESTS INTERRUPTED

With Deregistration Delay:

ASG SCALE IN

↓

STOP NEW REQUESTS

↓

FINISH ACTIVE REQUESTS

↓

REMOVE INSTANCE

Think:

DEREGISTRATION DELAY

=

GRACEFUL SCALE IN

---

## Connection Draining and Unhealthy Targets

Connection Draining also applies when an instance becomes:

UNHEALTHY

Think:

LOAD BALANCER

↓

TARGET UNHEALTHY

↓

STOP NEW CONNECTIONS

↓

ALLOW EXISTING CONNECTIONS TO COMPLETE

The key concept is:

DO NOT SEND NEW TRAFFIC

to a target that should no longer receive requests.

---

## Connection Draining Is Not a Health Check

Do not confuse:

HEALTH CHECK

with:

CONNECTION DRAINING

### Health Check

Determines:

IS THE TARGET HEALTHY?

### Connection Draining

Determines:

WHAT HAPPENS TO EXISTING CONNECTIONS WHEN THE TARGET IS REMOVED?

Think:

HEALTH CHECK

=

SHOULD I SEND TRAFFIC?

DRAINING

=

HOW DO I STOP SENDING TRAFFIC GRACEFULLY?

---

## Connection Draining Is Not Stickiness

Do not confuse:

[Load Balancer Stickiness](<Load Balancer Stickiness>)

with:

CONNECTION DRAINING

### Stickiness

SAME CLIENT

↓

SAME TARGET

### Connection Draining

TARGET LEAVING

↓

FINISH ACTIVE REQUESTS

Think:

STICKINESS

=

WHERE CLIENT RETURNS

DRAINING

=

HOW TARGET LEAVES

---

## Architecture Thinking

Imagine:

USERS

↓

ALB

↓

EC2 #1

EC2 #2

EC2 #3

The Auto Scaling Group decides:

EC2 #3

↓

TERMINATE

Before termination:

EC2 #3

↓

DEREGISTERING

↓

NO NEW REQUESTS

↓

EXISTING REQUESTS FINISH

↓

DEREGISTRATION DELAY EXPIRES

↓

TARGET REMOVED

↓

INSTANCE TERMINATED

This prevents:

ACTIVE USER REQUESTS

from being unnecessarily interrupted.

---

## Scenario Recognition

Need existing requests to finish before removing a Load Balancer target?

→ Connection Draining / Deregistration Delay

---

Need to stop new requests while allowing current requests to complete?

→ Connection Draining / Deregistration Delay

---

Question mentions Classic Load Balancer?

→ Connection Draining

---

Question mentions Application Load Balancer?

→ Deregistration Delay

---

Question mentions Network Load Balancer?

→ Deregistration Delay

---

Need graceful EC2 removal during Auto Scaling scale-in?

→ Deregistration Delay

---

Application has long-running requests?

→ Increase Deregistration Delay

---

Application requests complete almost immediately?

→ Lower Deregistration Delay

---

Need the default Deregistration Delay?

→ 300 seconds

---

Need the configurable range?

→ 1 to 3600 seconds

---

## Exam Traps

CLB

=

CONNECTION DRAINING

---

ALB / NLB

=

DEREGISTRATION DELAY

---

DEREGISTERING TARGET

=

NO NEW REQUESTS

---

EXISTING REQUESTS

=

ALLOWED TO COMPLETE

---

DEFAULT DELAY

=

300 SECONDS

---

300 SECONDS

=

5 MINUTES

---

CONFIGURABLE RANGE

=

1 TO 3600 SECONDS

---

LONG REQUESTS

=

HIGHER DELAY

---

SHORT REQUESTS

=

LOWER DELAY

---

CONNECTION DRAINING

≠

HEALTH CHECK

---

CONNECTION DRAINING

≠

STICKINESS

---

DEREGISTRATION DELAY

=

GRACEFUL TARGET REMOVAL

---

## Quick Cheat Sheet

CONNECTION DRAINING

=

CLB TERM

DEREGISTRATION DELAY

=

ALB / NLB TERM

PURPOSE

=

FINISH IN-FLIGHT REQUESTS

NEW REQUESTS

=

STOP

EXISTING REQUESTS

=

FINISH

DEFAULT

=

300 SECONDS

MINIMUM

=

1 SECOND

MAXIMUM

=

3600 SECONDS

LONG REQUESTS

=

LONGER DELAY

SHORT REQUESTS

=

SHORTER DELAY

ASG SCALE IN

=

GRACEFUL INSTANCE REMOVAL

---

## Master Memory Trick

TARGET LEAVING

↓

STOP NEW REQUESTS

↓

FINISH CURRENT REQUESTS

↓

WAIT FOR DELAY

↓

REMOVE TARGET

Think:

RESTAURANT IS CLOSING

↓

STOP SEATING NEW CUSTOMERS

↓

LET CURRENT CUSTOMERS FINISH

↓

CLOSE

That is:

CONNECTION DRAINING

or:

DEREGISTRATION DELAY

Remember:

CLB

=

DRAINING

ALB / NLB

=

DEREGISTRATION DELAY

And:

1

↓

300 DEFAULT

↓

3600

---

## Related Notes

- [Elastic Load Balancing](<Elastic Load Balancing>)
- [Application Load Balancer](<Application Load Balancer>)
- [Network Load Balancer](<Network Load Balancer>)
- [Load Balancer Stickiness](<Load Balancer Stickiness>)
- [Cross-Zone Load Balancing](<Cross-Zone Load Balancing>)
- [Load Balancer SSL Certificates](<Load Balancer SSL Certificates>)
- [Auto Scaling Groups](<Auto Scaling Groups>)
- [EC2](EC2)
- [SAA High Availability Cheat Sheet](<SAA High Availability Cheat Sheet>)
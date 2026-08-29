## What Problem Does It Solve?

An Auto Scaling Group knows:

HOW TO ADD AND REMOVE EC2 INSTANCES

But it still needs to know:

WHEN SHOULD I SCALE?

and:

HOW MUCH SHOULD I SCALE?

Scaling Policies define:

WHEN

and:

HOW

an Auto Scaling Group changes capacity.

Think:

APPLICATION LOAD

↓

METRIC / SCHEDULE / PREDICTION

↓

SCALING POLICY

↓

AUTO SCALING GROUP

↓

ADD OR REMOVE EC2

### Memory Trick

SCALING POLICY

=

RULES FOR WHEN ASG SHOULD SCALE

---

## Scaling Policies Overview

The major scaling approaches are:

TARGET TRACKING SCALING

↓

SIMPLE / STEP SCALING

↓

SCHEDULED SCALING

↓

PREDICTIVE SCALING

Think:

KEEP A METRIC AT A TARGET?

↓

TARGET TRACKING

REACT TO AN ALARM?

↓

SIMPLE / STEP

KNOW WHEN TRAFFIC WILL CHANGE?

↓

SCHEDULED

WANT AWS TO FORECAST TRAFFIC?

↓

PREDICTIVE

---

## Dynamic Scaling

Dynamic Scaling means:

RESPOND TO CHANGING DEMAND

Think:

LOAD CHANGES

↓

METRIC CHANGES

↓

SCALING POLICY RESPONDS

↓

ASG CHANGES CAPACITY

Two important Dynamic Scaling approaches are:

TARGET TRACKING

and:

SIMPLE / STEP SCALING

### Memory Trick

DYNAMIC

=

REACT TO DEMAND

---

## Target Tracking Scaling

Target Tracking Scaling attempts to keep a metric around:

A SPECIFIC TARGET VALUE

Example:

KEEP AVERAGE ASG CPU

around:

40%

Think:

TARGET

=

40% CPU

CPU ↑ ABOVE TARGET

↓

SCALE OUT

CPU ↓ BELOW TARGET

↓

SCALE IN

### Memory Trick

TARGET TRACKING

=

KEEP METRIC NEAR TARGET

---

## Target Tracking Thermostat

The easiest way to remember Target Tracking is:

THERMOSTAT

Imagine:

THERMOSTAT TARGET

=

72°F

Temperature too high?

↓

COOL

Temperature too low?

↓

HEAT

Auto Scaling works similarly:

CPU TARGET

=

40%

CPU TOO HIGH

↓

ADD EC2

CPU TOO LOW

↓

REMOVE EC2

### Memory Trick

TARGET TRACKING

=

ASG THERMOSTAT

---

## Why Use Target Tracking?

Target Tracking is:

SIMPLE TO SET UP

You define:

THE METRIC

and:

THE TARGET VALUE

AWS handles the scaling behavior required to keep the metric near that target.

Think:

YOU SAY:

KEEP CPU AROUND 40%

↓

ASG

↓

FIGURES OUT WHEN TO SCALE

### Exam Thinking

Question says:

MAINTAIN

KEEP

TARGET

AVERAGE CPU AROUND X%

↓

THINK TARGET TRACKING

---

## Simple / Step Scaling

Simple / Step Scaling responds to:

CLOUDWATCH ALARMS

Think:

CLOUDWATCH METRIC

↓

CLOUDWATCH ALARM

↓

SCALING POLICY

↓

ASG ACTION

Example:

CPU > 70%

↓

ADD 2 INSTANCES

CPU < 30%

↓

REMOVE 1 INSTANCE

### Memory Trick

STEP SCALING

=

IF THIS HAPPENS → SCALE BY THIS MUCH

---

## Scale-Out Policy

A Scale-Out Policy:

INCREASES

the number of EC2 instances.

Example:

AVERAGE CPU > 70%

↓

CLOUDWATCH ALARM

↓

SCALE OUT

↓

ADD 2 EC2 INSTANCES

Think:

HIGH LOAD

↓

MORE CAPACITY

### Memory Trick

OUT

=

ADD

---

## Scale-In Policy

A Scale-In Policy:

DECREASES

the number of EC2 instances.

Example:

AVERAGE CPU < 30%

↓

CLOUDWATCH ALARM

↓

SCALE IN

↓

REMOVE 1 EC2 INSTANCE

Think:

LOW LOAD

↓

LESS CAPACITY

### Memory Trick

IN

=

REMOVE

---

## CloudWatch Alarms and ASG

An Auto Scaling Group can scale based on:

CLOUDWATCH ALARMS

A CloudWatch Alarm monitors:

A METRIC

Examples include:

AVERAGE CPU

or:

CUSTOM METRIC

Think:

CLOUDWATCH

↓

MONITOR METRIC

↓

ALARM TRIGGERS

↓

ASG SCALING POLICY

↓

SCALE OUT / SCALE IN

### Memory Trick

CLOUDWATCH

=

WATCH

ASG

=

ACT

---

## ASG-Level Metrics

Metrics such as:

AVERAGE CPU

can be calculated across:

THE ENTIRE AUTO SCALING GROUP

Think:

EC2 #1 CPU

+

EC2 #2 CPU

+

EC2 #3 CPU

↓

AVERAGE ASG CPU

↓

CLOUDWATCH ALARM

↓

SCALING ACTION

This is important because scaling decisions commonly consider:

THE FLEET

rather than only one individual EC2 instance.

---

## Custom Metrics

Scaling is not limited to:

CPU UTILIZATION

You can create scaling behavior based on:

CUSTOM CLOUDWATCH METRICS

Think:

APPLICATION

↓

CUSTOM METRIC

↓

CLOUDWATCH

↓

ALARM

↓

ASG

↓

SCALE

### Exam Thinking

If CPU does not accurately represent application demand:

USE A MORE APPROPRIATE METRIC

---

## Step Scaling Architecture

Imagine:

AUTO SCALING GROUP

↓

3 EC2 INSTANCES

CloudWatch sees:

CPU > 70%

↓

ALARM

↓

STEP SCALING POLICY

↓

ADD 2

↓

5 EC2 INSTANCES

Later:

CPU < 30%

↓

ALARM

↓

STEP SCALING POLICY

↓

REMOVE 1

↓

4 EC2 INSTANCES

Think:

THRESHOLD

↓

DEFINED ACTION

---

## Target Tracking vs Step Scaling

### Target Tracking

Goal:

MAINTAIN A METRIC

Example:

KEEP CPU AROUND 40%

Think:

TARGET VALUE

↓

AUTOMATIC ADJUSTMENT

---

### Step Scaling

Goal:

PERFORM A SPECIFIC ACTION

when an alarm threshold is crossed.

Example:

CPU > 70%

↓

ADD 2

Think:

THRESHOLD

↓

DEFINED ACTION

### Memory Trick

TARGET TRACKING

=

KEEP IT HERE

STEP SCALING

=

IF THIS, DO THAT

---

## Scheduled Scaling

Scheduled Scaling allows you to:

ANTICIPATE SCALING

based on:

KNOWN USAGE PATTERNS

Think:

YOU KNOW TRAFFIC WILL INCREASE

↓

SCHEDULE CAPACITY IN ADVANCE

Example:

EVERY FRIDAY

↓

5 PM

↓

INCREASE MINIMUM CAPACITY TO 10

### Memory Trick

SCHEDULED SCALING

=

I KNOW WHEN

---

## Scheduled Scaling Example

Imagine an application receives heavy traffic:

EVERY FRIDAY AT 5 PM

Instead of waiting for:

CPU TO INCREASE

you can scale:

BEFORE THE TRAFFIC ARRIVES

Think:

4:55 PM

↓

INCREASE CAPACITY

↓

5:00 PM TRAFFIC ARRIVES

↓

CAPACITY ALREADY AVAILABLE

### Exam Thinking

KNOWN TIME

+

KNOWN TRAFFIC PATTERN

↓

SCHEDULED SCALING

---

## Predictive Scaling

Predictive Scaling:

CONTINUOUSLY FORECASTS LOAD

and schedules scaling:

AHEAD OF TIME

Think:

HISTORICAL LOAD

↓

FORECAST FUTURE LOAD

↓

ASG PREPARES CAPACITY

↓

TRAFFIC ARRIVES

### Memory Trick

PREDICTIVE

=

FORECAST THEN SCALE

---

## Predictive Scaling Architecture

Imagine traffic follows a recurring pattern:

MORNING

↓

LOW

AFTERNOON

↓

HIGH

EVENING

↓

LOW

Predictive Scaling analyzes the pattern:

PAST TRAFFIC

↓

FORECAST

↓

FUTURE CAPACITY REQUIREMENT

↓

SCALE IN ADVANCE

This helps capacity become available:

BEFORE

the predicted demand arrives.

---

## Scheduled vs Predictive Scaling

### Scheduled Scaling

YOU KNOW:

WHEN

capacity must change.

Example:

FRIDAY AT 5 PM

Think:

YOU CREATE THE SCHEDULE

---

### Predictive Scaling

AWS:

FORECASTS LOAD

based on historical patterns.

Think:

AWS PREDICTS FUTURE DEMAND

### Memory Trick

SCHEDULED

=

YOU KNOW WHEN

PREDICTIVE

=

AWS FORECASTS WHEN

---

## Combining Scaling Policies

Scaling approaches can be used together.

For example:

PREDICTIVE SCALING

↓

PREPARE BASE CAPACITY

Then:

DYNAMIC SCALING

↓

RESPOND TO REAL-TIME CHANGES

Think:

PREDICT

↓

PREPARE

↓

TRAFFIC ARRIVES

↓

DYNAMICALLY ADJUST

This creates an architecture that can handle:

EXPECTED DEMAND

and:

UNEXPECTED DEMAND

---

## Scaling Cooldown

After a scaling activity occurs, an Auto Scaling Group enters a:

COOLDOWN PERIOD

The default cooldown is:

300 SECONDS

Think:

SCALING ACTION

↓

ADD / REMOVE EC2

↓

COOLDOWN

↓

WAIT FOR METRICS TO STABILIZE

### Memory Trick

COOLDOWN

=

WAIT AFTER SCALING

---

## Why Does Cooldown Exist?

Launching or terminating EC2 instances changes:

APPLICATION CAPACITY

But metrics do not necessarily stabilize:

IMMEDIATELY

Without a cooldown:

CPU HIGH

↓

ADD EC2

↓

CPU STILL LOOKS HIGH

↓

ADD MORE EC2

↓

ADD MORE EC2

This could cause:

UNNECESSARY SCALING

With cooldown:

SCALE

↓

WAIT

↓

METRICS STABILIZE

↓

REEVALUATE

### Memory Trick

COOLDOWN

=

DON'T OVERREACT

---

## Default Cooldown

The default Scaling Cooldown is:

300 SECONDS

which equals:

5 MINUTES

Think:

SCALING ACTION

↓

300 SECONDS

↓

METRICS STABILIZE

↓

NEXT SCALING DECISION

### Memory Trick

ASG COOLDOWN

=

300 SECONDS

---

## Cooldown and New Instances

During cooldown, the ASG gives newly launched instances time to:

START

↓

INITIALIZE

↓

BEGIN SERVING TRAFFIC

↓

AFFECT METRICS

Think:

NEW EC2

↓

NOT INSTANTLY USEFUL

↓

WAIT

↓

METRICS STABILIZE

---

## Reduce Cooldown with a Ready-to-Use AMI

Your course recommends using:

A READY-TO-USE AMI

to reduce:

INSTANCE CONFIGURATION TIME

Think:

GENERIC AMI

↓

LONG STARTUP CONFIGURATION

vs:

READY-TO-USE AMI

↓

FAST STARTUP

↓

SERVE REQUESTS SOONER

↓

SHORTER COOLDOWN POSSIBLE

### Memory Trick

PRE-BAKED AMI

=

FASTER SCALE OUT

---

## Why Fast Instance Startup Matters

Suppose an instance launches but requires:

10 MINUTES

to install software and configure the application.

Think:

ASG ADDS EC2

↓

EC2 EXISTS

↓

APPLICATION NOT READY

↓

CAPACITY HAS NOT REALLY INCREASED YET

A ready-to-use AMI reduces this delay.

Think:

AMI ALREADY CONFIGURED

↓

INSTANCE STARTS

↓

APPLICATION READY FASTER

### Exam Thinking

Need faster Auto Scaling response?

→ Reduce instance initialization time

→ Consider a ready-to-use AMI

---

## Cooldown vs Deregistration Delay

Do not confuse:

SCALING COOLDOWN

with:

[Connection Draining - Deregistration Delay](<Connection Draining - Deregistration Delay>)

### Scaling Cooldown

Occurs:

AFTER A SCALING ACTION

Purpose:

ALLOW METRICS TO STABILIZE

---

### Deregistration Delay

Occurs when:

TARGET IS BEING REMOVED

Purpose:

ALLOW IN-FLIGHT REQUESTS TO FINISH

Think:

COOLDOWN

=

WAIT BEFORE MORE SCALING

DEREGISTRATION DELAY

=

WAIT FOR REQUESTS TO FINISH

### Memory Trick

COOLDOWN

=

CALM THE ASG

DRAINING

=

FINISH THE REQUEST

---

## Scaling Policy Decision Tree

Question says:

KEEP CPU AROUND 40%

↓

TARGET TRACKING

---

Question says:

CPU > 70% → ADD 2

↓

STEP SCALING

---

Question says:

EVERY FRIDAY AT 5 PM

↓

SCHEDULED SCALING

---

Question says:

FORECAST FUTURE LOAD

↓

PREDICTIVE SCALING

---

Question says:

WAIT AFTER SCALING FOR METRICS TO STABILIZE

↓

SCALING COOLDOWN

---

## Architecture Thinking

Imagine:

USERS

↓

[Application Load Balancer](<Application Load Balancer>)

↓

AUTO SCALING GROUP

↓

EC2 EC2 EC2

CloudWatch monitors:

AVERAGE CPU

↓

TARGET TRACKING POLICY

↓

TARGET = 40%

Traffic increases:

CPU ↑

↓

ASG SCALE OUT

↓

ADD EC2

↓

COOLDOWN

↓

METRICS STABILIZE

Traffic decreases:

CPU ↓

↓

ASG SCALE IN

↓

REMOVE EC2

Think:

CLOUDWATCH

=

OBSERVE

SCALING POLICY

=

DECIDE

ASG

=

ACT

---

## Scenario Recognition

Need average CPU maintained around 40%?

→ Target Tracking Scaling

---

Need scaling to behave like a thermostat?

→ Target Tracking Scaling

---

Need to add 2 instances when CPU exceeds 70%?

→ Simple / Step Scaling

---

Need to remove 1 instance when CPU falls below 30%?

→ Simple / Step Scaling

---

Need scaling based on a CloudWatch Alarm?

→ Dynamic Scaling

---

Need scaling based on an application-specific metric?

→ Custom CloudWatch Metric + Scaling Policy

---

Know demand increases every Friday at 5 PM?

→ Scheduled Scaling

---

Need capacity available before a known event?

→ Scheduled Scaling

---

Need AWS to forecast future demand?

→ Predictive Scaling

---

Need scaling based on historical recurring patterns?

→ Predictive Scaling

---

Need to prevent repeated scaling actions before metrics stabilize?

→ Scaling Cooldown

---

Need the default Scaling Cooldown?

→ 300 seconds

---

Need new instances to become useful faster?

→ Ready-to-use AMI

---

## Exam Traps

TARGET TRACKING

=

MAINTAIN TARGET METRIC

---

TARGET CPU 40%

=

TARGET TRACKING

---

STEP SCALING

=

ALARM THRESHOLD → DEFINED ACTION

---

CPU > 70%

↓

ADD 2

=

STEP SCALING

---

SCHEDULED SCALING

=

KNOWN TIME / PATTERN

---

PREDICTIVE SCALING

=

FORECAST FUTURE LOAD

---

CLOUDWATCH ALARM

=

CAN TRIGGER SCALE OUT / SCALE IN

---

SCALING COOLDOWN

=

WAIT FOR METRICS TO STABILIZE

---

DEFAULT COOLDOWN

=

300 SECONDS

---

300 SECONDS

=

5 MINUTES

---

COOLDOWN

≠

DEREGISTRATION DELAY

---

COOLDOWN

=

WAIT AFTER SCALING

DEREGISTRATION DELAY

=

FINISH IN-FLIGHT REQUESTS

---

READY-TO-USE AMI

=

FASTER INSTANCE STARTUP

---

## Quick Cheat Sheet

TARGET TRACKING

=

KEEP METRIC NEAR TARGET

EXAMPLE

=

CPU AROUND 40%

STEP SCALING

=

THRESHOLD → ACTION

EXAMPLE

=

CPU > 70% → ADD 2

SCHEDULED SCALING

=

KNOWN TIME

EXAMPLE

=

FRIDAY 5 PM

PREDICTIVE SCALING

=

FORECAST LOAD

CLOUDWATCH

=

MONITOR METRIC

SCALE OUT

=

ADD EC2

SCALE IN

=

REMOVE EC2

COOLDOWN

=

WAIT FOR METRICS TO STABILIZE

DEFAULT COOLDOWN

=

300 SECONDS

READY-TO-USE AMI

=

FASTER SCALING RESPONSE

---

## Master Memory Trick

TARGET TRACKING

=

THERMOSTAT

STEP SCALING

=

IF THIS → DO THAT

SCHEDULED

=

I KNOW WHEN

PREDICTIVE

=

AWS FORECASTS WHEN

COOLDOWN

=

WAIT AND STABILIZE

Think:

CLOUDWATCH

↓

SEES METRIC

↓

SCALING POLICY

↓

DECIDES

↓

ASG

↓

ADDS / REMOVES EC2

↓

COOLDOWN

↓

METRICS STABILIZE

Remember:

TARGET

=

KEEP IT HERE

STEP

=

REACT

SCHEDULED

=

PLAN

PREDICTIVE

=

FORECAST

COOLDOWN

=

WAIT

---

## Related Notes

- [Auto Scaling Groups](<Auto Scaling Groups>)
- [Scalability & High Availability](<Scalability & High Availability>)
- [Elastic Load Balancing](<Elastic Load Balancing>)
- [Application Load Balancer](<Application Load Balancer>)
- [Connection Draining - Deregistration Delay](<Connection Draining - Deregistration Delay>)
- [EC2](EC2)
- [EC2 User Data](<EC2 User Data>)
- [AMI](AMI)
- [CloudWatch](07-Monitoring/CloudWatch.md)
- [SAA High Availability Cheat Sheet](<SAA High Availability Cheat Sheet>)
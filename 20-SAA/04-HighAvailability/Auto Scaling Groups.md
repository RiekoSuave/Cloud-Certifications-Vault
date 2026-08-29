## What Problem Does It Solve?

The load on an application can:

INCREASE

and:

DECREASE

over time.

If you always run too few EC2 instances:

TRAFFIC ↑

↓

EC2 CAPACITY TOO LOW

↓

APPLICATION PERFORMANCE SUFFERS

If you always run too many:

LOW TRAFFIC

↓

EXTRA EC2 INSTANCES

↓

WASTED MONEY

An:

AUTO SCALING GROUP

or:

ASG

automatically adjusts the number of EC2 instances to match demand.

### Memory Trick

ASG

=

ADD / REMOVE EC2 AUTOMATICALLY

---

## What Is an Auto Scaling Group?

An Auto Scaling Group manages a:

GROUP OF EC2 INSTANCES

and can automatically:

SCALE OUT

↓

ADD EC2 INSTANCES

and:

SCALE IN

↓

REMOVE EC2 INSTANCES

Think:

TRAFFIC ↑

↓

ADD EC2

TRAFFIC ↓

↓

REMOVE EC2

### Memory Trick

ASG

=

SCALE OUT + SCALE IN

---

## Why Use an Auto Scaling Group?

The goal of an ASG is to:

- Scale out when load increases
- Scale in when load decreases
- Maintain a minimum number of EC2 instances
- Maintain a maximum number of EC2 instances
- Maintain a desired number of EC2 instances
- Automatically register new instances with a Load Balancer
- Replace unhealthy instances

Think:

APPLICATION DEMAND

↓

ASG

↓

RIGHT NUMBER OF EC2 INSTANCES

---

## ASG Architecture

A common architecture is:

USERS

↓

LOAD BALANCER

↓

AUTO SCALING GROUP

↓

EC2 #1

EC2 #2

EC2 #3

The:

LOAD BALANCER

distributes traffic.

The:

AUTO SCALING GROUP

controls how many EC2 instances exist.

### Memory Trick

ELB

=

DISTRIBUTE

ASG

=

SCALE

---

## Scale Out

Scale Out means:

ADD EC2 INSTANCES

Think:

TRAFFIC ↑

↓

CURRENT EC2 CAPACITY NOT ENOUGH

↓

ASG ADDS EC2

Example:

2 EC2

↓

4 EC2

### Memory Trick

SCALE OUT

=

MORE SERVERS

---

## Scale In

Scale In means:

REMOVE EC2 INSTANCES

Think:

TRAFFIC ↓

↓

EXCESS EC2 CAPACITY

↓

ASG REMOVES EC2

Example:

4 EC2

↓

2 EC2

### Memory Trick

SCALE IN

=

FEWER SERVERS

---

## ASG Size Settings

An Auto Scaling Group has three important capacity settings:

MINIMUM CAPACITY

↓

DESIRED CAPACITY

↓

MAXIMUM CAPACITY

Think:

MIN

=

LOWEST ALLOWED

DESIRED

=

CURRENT TARGET

MAX

=

HIGHEST ALLOWED

---

## Minimum Capacity

Minimum Capacity determines:

THE MINIMUM NUMBER OF EC2 INSTANCES

that the ASG should maintain.

Example:

MINIMUM

=

2

The ASG should not normally scale below:

2 EC2 INSTANCES

Think:

ASG

↓

NEVER GO BELOW MINIMUM

### Memory Trick

MIN

=

FLOOR

---

## Desired Capacity

Desired Capacity represents:

THE NUMBER OF INSTANCES THE ASG WANTS RUNNING

Example:

MIN

=

2

DESIRED

=

4

MAX

=

10

Think:

ASG

↓

TRY TO MAINTAIN 4 INSTANCES

If one instance disappears:

4

↓

3

↓

ASG LAUNCHES REPLACEMENT

↓

4

### Memory Trick

DESIRED

=

TARGET NUMBER

---

## Maximum Capacity

Maximum Capacity determines:

THE MAXIMUM NUMBER OF EC2 INSTANCES

the ASG can scale to.

Example:

MAXIMUM

=

10

Even if traffic continues increasing:

ASG

↓

WILL NOT SCALE ABOVE 10

unless the configuration is changed.

### Memory Trick

MAX

=

CEILING

---

## Min vs Desired vs Max

Think:

MINIMUM

↓

2

DESIRED

↓

4

MAXIMUM

↓

10

The ASG can operate between:

2 AND 10 INSTANCES

while trying to maintain:

4

when no scaling policy changes the desired capacity.

### Memory Trick

MIN

=

FLOOR

DESIRED

=

TARGET

MAX

=

CEILING

---

## ASG Uses a Launch Template

The Auto Scaling Group needs to know:

WHAT TYPE OF EC2 INSTANCE SHOULD I CREATE?

This configuration is commonly defined using:

LAUNCH TEMPLATE

Think:

LAUNCH TEMPLATE

↓

EC2 BLUEPRINT

↓

AUTO SCALING GROUP

↓

NEW EC2 INSTANCES

The Launch Template can define information such as:

- AMI
- Instance type
- EC2 User Data
- EBS volumes
- Security Groups
- SSH key pair
- IAM Instance Profile

### Memory Trick

LAUNCH TEMPLATE

=

EC2 BLUEPRINT

---

## ASG + Load Balancer

An ASG can automatically register new EC2 instances with:

A LOAD BALANCER

Think:

TRAFFIC ↑

↓

ASG LAUNCHES EC2 #4

↓

EC2 #4 REGISTERED

↓

LOAD BALANCER

↓

STARTS ROUTING TRAFFIC

This makes:

HORIZONTAL SCALING

much easier.

### Memory Trick

ASG CREATES

↓

ELB DISTRIBUTES

---

## ASG + Target Groups

With modern Load Balancers:

ALB

and:

NLB

EC2 instances are registered with:

TARGET GROUPS

Think:

ASG

↓

NEW EC2

↓

TARGET GROUP

↓

LOAD BALANCER

When an instance is removed:

ASG

↓

DEREGISTER TARGET

↓

LOAD BALANCER

See:

[Connection Draining - Deregistration Delay](<Connection Draining - Deregistration Delay>)

---

## ASG Across Multiple Availability Zones

An Auto Scaling Group can launch EC2 instances across:

MULTIPLE AVAILABILITY ZONES

Think:

AUTO SCALING GROUP

↓

AZ-A

EC2 EC2

+

AZ-B

EC2 EC2

This helps provide:

HIGH AVAILABILITY

### Memory Trick

ASG + MULTI-AZ

=

SCALING + HIGH AVAILABILITY

---

## ASG Rebalances Across AZs

A well-designed ASG attempts to maintain capacity across:

MULTIPLE AVAILABILITY ZONES

Think:

AZ-A

↓

2 EC2

AZ-B

↓

2 EC2

If capacity changes or instances are lost:

ASG

↓

LAUNCH / REPLACE INSTANCES

↓

RESTORE HEALTHY CAPACITY

The architecture should avoid depending on:

ONE AVAILABILITY ZONE

---

## ASG Health Checks

An Auto Scaling Group can determine whether instances are:

HEALTHY

or:

UNHEALTHY

If an instance becomes unhealthy:

ASG

↓

TERMINATE UNHEALTHY INSTANCE

↓

LAUNCH REPLACEMENT

Think:

BAD EC2

↓

REMOVE

↓

NEW EC2

### Memory Trick

ASG

=

SELF-HEALING EC2 FLEET

---

## EC2 Health Checks

ASG can use:

EC2 STATUS CHECKS

to determine whether an instance is healthy.

Think:

EC2 INSTANCE FAILS

↓

EC2 HEALTH CHECK

↓

ASG DETECTS FAILURE

↓

REPLACE INSTANCE

---

## Load Balancer Health Checks

An ASG can also integrate with:

LOAD BALANCER HEALTH CHECKS

Think:

LOAD BALANCER

↓

APPLICATION HEALTH CHECK FAILS

↓

ASG

↓

REPLACE UNHEALTHY EC2

This is useful because an EC2 instance may technically be:

RUNNING

while the:

APPLICATION

is unhealthy.

### Memory Trick

EC2 HEALTH

=

IS SERVER RUNNING?

ELB HEALTH

=

IS APPLICATION RESPONDING?

---

## Automatic Instance Replacement

Suppose:

DESIRED CAPACITY

=

3

You have:

EC2 #1

EC2 #2

EC2 #3

Then:

EC2 #2

↓

UNHEALTHY

ASG terminates it:

3 INSTANCES

↓

2 HEALTHY INSTANCES

But desired capacity is:

3

So:

ASG

↓

LAUNCHES NEW EC2

↓

BACK TO 3

### Memory Trick

DESIRED = 3

MEANS

ASG KEEPS TRYING FOR 3

---

## ASG Cost Savings

Auto Scaling helps reduce cost because you can:

RUN MORE INSTANCES

when needed

and:

RUN FEWER INSTANCES

when demand decreases.

Think:

HIGH TRAFFIC

↓

MORE EC2

LOW TRAFFIC

↓

FEWER EC2

↓

PAY FOR APPROPRIATE CAPACITY

### Memory Trick

ASG

=

MATCH CAPACITY TO DEMAND

---

## ASG and CloudWatch

Auto Scaling Groups commonly use:

CLOUDWATCH METRICS

and:

CLOUDWATCH ALARMS

to determine when scaling should occur.

Think:

CLOUDWATCH

↓

METRIC

↓

ALARM

↓

ASG

↓

SCALE

Example:

CPU > 70%

↓

CLOUDWATCH ALARM

↓

ASG ADDS INSTANCES

### Memory Trick

CLOUDWATCH

=

WATCH

ASG

=

ACT

---

## Scaling Policies

ASG supports multiple ways to control scaling.

The major strategies include:

MANUAL SCALING

↓

DYNAMIC SCALING

↓

SCHEDULED SCALING

↓

PREDICTIVE SCALING

Think:

HOW SHOULD ASG DECIDE WHEN TO SCALE?

↓

SCALING POLICY

---

## Manual Scaling

Manual Scaling means:

YOU CHANGE THE ASG SIZE

Think:

ADMINISTRATOR

↓

CHANGE DESIRED CAPACITY

↓

ASG ADJUSTS INSTANCES

Example:

DESIRED

2

↓

MANUALLY CHANGE TO 5

↓

ASG LAUNCHES 3 MORE EC2 INSTANCES

### Memory Trick

MANUAL

=

HUMAN DECIDES

---

## Dynamic Scaling

Dynamic Scaling responds to:

CHANGING DEMAND

Think:

LOAD CHANGES

↓

METRIC CHANGES

↓

ASG RESPONDS

Important Dynamic Scaling approaches include:

SIMPLE / STEP SCALING

and:

TARGET TRACKING SCALING

---

## Simple / Step Scaling

Simple / Step Scaling reacts to:

CLOUDWATCH ALARMS

Example:

CPU > 70%

↓

ADD 2 INSTANCES

Then:

CPU < 30%

↓

REMOVE 1 INSTANCE

Think:

IF METRIC CROSSES THRESHOLD

↓

TAKE SCALING ACTION

### Memory Trick

STEP SCALING

=

IF THIS → DO THAT

---

## Target Tracking Scaling

Target Tracking Scaling tries to maintain a metric around:

A TARGET VALUE

Example:

KEEP AVERAGE ASG CPU

around:

40%

Think:

CPU ABOVE 40%

↓

SCALE OUT

CPU BELOW 40%

↓

SCALE IN

The goal is:

KEEP METRIC NEAR TARGET

### Memory Trick

TARGET TRACKING

=

THERMOSTAT

---

## Target Tracking Thermostat Example

Think about a thermostat:

TARGET TEMPERATURE

=

72°F

Too hot?

↓

COOL

Too cold?

↓

HEAT

Target Tracking works similarly:

TARGET CPU

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

## Scheduled Scaling

Scheduled Scaling is used when you:

KNOW IN ADVANCE

that capacity requirements will change.

Think:

KNOWN TRAFFIC PATTERN

↓

SCHEDULE SCALE EVENT

Example:

EVERY FRIDAY

↓

5 PM

↓

INCREASE MINIMUM CAPACITY TO 10

This is useful for:

PREDICTABLE TIME-BASED DEMAND

### Memory Trick

SCHEDULED

=

I KNOW WHEN

---

## Predictive Scaling

Predictive Scaling uses:

MACHINE LEARNING

to analyze historical traffic patterns and:

PREDICT FUTURE LOAD

Think:

PAST TRAFFIC

↓

MACHINE LEARNING

↓

PREDICT FUTURE TRAFFIC

↓

PROVISION EC2 IN ADVANCE

### Memory Trick

PREDICTIVE

=

AWS PREDICTS WHEN

---

## Predictive Scaling vs Scheduled Scaling

### Scheduled Scaling

YOU KNOW:

WHEN

capacity will be needed.

Think:

EVERY FRIDAY AT 5 PM

↓

SCHEDULED

### Predictive Scaling

AWS ANALYZES:

HISTORICAL PATTERNS

and predicts:

FUTURE DEMAND

Think:

MACHINE LEARNING

↓

PREDICTIVE

### Memory Trick

SCHEDULED

=

YOU KNOW

PREDICTIVE

=

AWS LEARNS

---

## Scaling Policy Decision

Need to manually change capacity?

↓

MANUAL SCALING

Need to react to CloudWatch thresholds?

↓

SIMPLE / STEP SCALING

Need to maintain average CPU around 40%?

↓

TARGET TRACKING

Know traffic increases every Friday at 5 PM?

↓

SCHEDULED SCALING

Need AWS to learn recurring traffic patterns?

↓

PREDICTIVE SCALING

---

## ASG and Deregistration Delay

When an ASG scales in:

INSTANCE SELECTED FOR TERMINATION

↓

LOAD BALANCER

↓

STOP NEW REQUESTS

↓

ALLOW IN-FLIGHT REQUESTS TO COMPLETE

↓

INSTANCE REMOVED

This works with:

[Connection Draining - Deregistration Delay](<Connection Draining - Deregistration Delay>)

Think:

ASG SCALE IN

↓

GRACEFUL TARGET REMOVAL

---

## ASG Architecture Thinking

A common scalable and highly available architecture is:

USERS

↓

[Application Load Balancer](<Application Load Balancer>)

↓

TARGET GROUP

↓

AUTO SCALING GROUP

↓

AZ-A

EC2 EC2

+

AZ-B

EC2 EC2

CloudWatch monitors:

CPU / METRICS

↓

SCALING POLICY

↓

AUTO SCALING GROUP

Then:

HIGH LOAD

↓

ADD EC2

LOW LOAD

↓

REMOVE EC2

UNHEALTHY EC2

↓

REPLACE EC2

### Memory Trick

ELB

=

DISTRIBUTE

ASG

=

SCALE

CLOUDWATCH

=

MONITOR

---

## Scenario Recognition

Need EC2 instances automatically added as traffic increases?

→ Auto Scaling Group

---

Need EC2 instances automatically removed when traffic decreases?

→ Auto Scaling Group

---

Need to maintain a minimum number of EC2 instances?

→ Auto Scaling Group Minimum Capacity

---

Need a target number of EC2 instances?

→ Desired Capacity

---

Need to prevent scaling beyond a certain number?

→ Maximum Capacity

---

Need a reusable configuration describing new EC2 instances?

→ Launch Template

---

Need new EC2 instances automatically registered with a Load Balancer?

→ Auto Scaling Group + Load Balancer

---

Need unhealthy EC2 instances automatically replaced?

→ Auto Scaling Group

---

Need EC2 instances distributed across multiple AZs?

→ Multi-AZ Auto Scaling Group

---

Need to react when CPU exceeds 70%?

→ Dynamic Scaling / Step Scaling

---

Need average CPU maintained around 40%?

→ Target Tracking Scaling

---

Need capacity increased every Friday at 5 PM?

→ Scheduled Scaling

---

Need AWS to predict recurring demand using machine learning?

→ Predictive Scaling

---

Need graceful instance removal during scale-in?

→ Deregistration Delay

---

## Exam Traps

ASG

=

ADD / REMOVE EC2

---

ELB

=

DISTRIBUTE TRAFFIC

ASG

=

SCALE CAPACITY

---

SCALE OUT

=

ADD INSTANCES

---

SCALE IN

=

REMOVE INSTANCES

---

MINIMUM

=

FLOOR

DESIRED

=

TARGET

MAXIMUM

=

CEILING

---

LAUNCH TEMPLATE

=

EC2 CONFIGURATION

---

ASG

=

CAN AUTOMATICALLY REGISTER INSTANCES WITH LOAD BALANCER

---

ASG

=

CAN REPLACE UNHEALTHY INSTANCES

---

MULTI-AZ ASG

=

HIGH AVAILABILITY

---

STEP SCALING

=

CLOUDWATCH THRESHOLD → ACTION

---

TARGET TRACKING

=

MAINTAIN TARGET METRIC

---

SCHEDULED SCALING

=

KNOWN TIME

---

PREDICTIVE SCALING

=

MACHINE LEARNING FORECAST

---

ASG

≠

LOAD BALANCER

ASG

=

CONTROLS NUMBER OF INSTANCES

LOAD BALANCER

=

CONTROLS TRAFFIC DISTRIBUTION

---

## Quick Cheat Sheet

ASG

=

AUTO SCALING GROUP

PURPOSE

=

ADJUST EC2 CAPACITY

SCALE OUT

=

ADD EC2

SCALE IN

=

REMOVE EC2

MINIMUM

=

LOWEST CAPACITY

DESIRED

=

TARGET CAPACITY

MAXIMUM

=

HIGHEST CAPACITY

LAUNCH TEMPLATE

=

EC2 BLUEPRINT

LOAD BALANCER INTEGRATION

=

AUTOMATIC REGISTRATION

UNHEALTHY INSTANCE

=

REPLACE

MULTI-AZ

=

HIGH AVAILABILITY

CLOUDWATCH

=

MONITOR METRICS

STEP SCALING

=

THRESHOLD → ACTION

TARGET TRACKING

=

MAINTAIN METRIC

SCHEDULED

=

KNOWN TIME

PREDICTIVE

=

MACHINE LEARNING FORECAST

---

## Master Memory Trick

CLOUDWATCH

↓

SEES LOAD

↓

AUTO SCALING GROUP

↓

DECIDES CAPACITY

↓

EC2 INSTANCES

↓

LOAD BALANCER

↓

DISTRIBUTES TRAFFIC

Think:

TRAFFIC ↑

↓

ASG SCALE OUT

↓

ADD EC2

TRAFFIC ↓

↓

ASG SCALE IN

↓

REMOVE EC2

INSTANCE FAILS

↓

ASG REPLACES IT

And remember:

MIN

=

FLOOR

DESIRED

=

TARGET

MAX

=

CEILING

ELB

=

DISTRIBUTE

ASG

=

SCALE

CLOUDWATCH

=

WATCH

---

## Related Notes

- [Scalability & High Availability](<Scalability & High Availability>)
- [Elastic Load Balancing](<Elastic Load Balancing>)
- [Application Load Balancer](<Application Load Balancer>)
- [Network Load Balancer](<Network Load Balancer>)
- [Connection Draining - Deregistration Delay](<Connection Draining - Deregistration Delay>)
- [EC2](EC2)
- [EC2 User Data](<EC2 User Data>)
- [EC2 Security Groups](<EC2 Security Groups>)
- [CloudWatch](07-Monitoring/CloudWatch.md)
- [SAA High Availability Cheat Sheet](<SAA High Availability Cheat Sheet>)
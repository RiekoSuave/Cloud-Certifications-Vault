## What Problem Does It Solve?

DynamoDB needs a way to determine:

HOW MUCH READ CAPACITY

and:

HOW MUCH WRITE CAPACITY

your table should have.

Different workloads behave differently.

Some are:

PREDICTABLE

while others are:

UNPREDICTABLE

DynamoDB provides two capacity modes:

PROVISIONED

and:

ON-DEMAND

Think:

KNOWN TRAFFIC?

↓

PROVISIONED

UNKNOWN / SPIKY TRAFFIC?

↓

ON-DEMAND

### Memory Trick

DYNAMODB CAPACITY

=

PLAN IT

or:

LET AWS HANDLE IT

---

## What Are DynamoDB Capacity Modes?

Capacity Modes determine:

HOW DYNAMODB MANAGES

READ / WRITE THROUGHPUT

for a table.

Think:

APPLICATION

↓

READS + WRITES

↓

DYNAMODB CAPACITY MODE

↓

TABLE THROUGHPUT

The two main modes are:

PROVISIONED MODE

and:

ON-DEMAND MODE

### Memory Trick

CAPACITY MODE

=

HOW TABLE THROUGHPUT IS PROVIDED

---

## Provisioned Mode

With Provisioned Mode:

YOU SPECIFY

how much read and write capacity the table should support.

Think:

EXPECTED TRAFFIC

↓

CHOOSE CAPACITY

↓

DYNAMODB TABLE

You provision:

READ CAPACITY UNITS

and:

WRITE CAPACITY UNITS

### Memory Trick

PROVISIONED

=

YOU PLAN CAPACITY

---

## Provisioned Mode Is the Default

Your SAA course identifies:

PROVISIONED MODE

as the:

DEFAULT

capacity mode.

Think:

DYNAMODB TABLE

↓

PROVISIONED CAPACITY

↓

RCU + WCU

### Memory Trick

PROVISIONED

=

DEFAULT MODE

---

## Read Capacity Units

RCU stands for:

READ CAPACITY UNIT

Think:

RCU

=

READ THROUGHPUT

RCUs represent the amount of:

READ CAPACITY

allocated to the table.

### Memory Trick

R

in RCU

=

READ

---

## Write Capacity Units

WCU stands for:

WRITE CAPACITY UNIT

Think:

WCU

=

WRITE THROUGHPUT

WCUs represent the amount of:

WRITE CAPACITY

allocated to the table.

### Memory Trick

W

in WCU

=

WRITE

---

## RCU + WCU

Provisioned DynamoDB capacity is based on:

RCU

and:

WCU

Think:

READ TRAFFIC

↓

RCU

WRITE TRAFFIC

↓

WCU

You configure them based on:

EXPECTED APPLICATION DEMAND

### Memory Trick

READS

=

RCU

WRITES

=

WCU

---

## Capacity Planning

Provisioned Mode requires:

CAPACITY PLANNING

Think:

HOW MANY READS PER SECOND?

↓

HOW MANY WRITES PER SECOND?

↓

PROVISION RCU + WCU

This works well when traffic is:

KNOWN

or:

PREDICTABLE

### Memory Trick

PREDICTABLE

=

PROVISIONED

---

## Provisioned Mode Architecture

Imagine an application normally performs:

CONSISTENT READS

and:

CONSISTENT WRITES

Think:

TRAFFIC

↓

100

↓

110

↓

95

↓

105

The workload is:

PREDICTABLE

You can provision:

APPROPRIATE RCU

+

APPROPRIATE WCU

### Memory Trick

STEADY LOAD

=

PROVISION IT

---

## Paying for Provisioned Capacity

With Provisioned Mode:

YOU PAY FOR THE CAPACITY YOU PROVISION

Think:

PROVISION:

100 RCU

+

50 WCU

↓

PAY FOR PROVISIONED CAPACITY

Even if usage is temporarily:

LOWER

you have still provisioned that capacity.

### Memory Trick

PROVISIONED

=

PAY FOR PROVISIONED THROUGHPUT

---

## Provisioned Capacity Risk

If you provision:

TOO LITTLE CAPACITY

then application traffic can exceed:

AVAILABLE THROUGHPUT

Think:

TRAFFIC

>

PROVISIONED CAPACITY

↓

REQUESTS MAY BE THROTTLED

This makes proper capacity planning important.

### Memory Trick

UNDER-PROVISION

=

THROTTLING RISK

---

## Over-Provisioning

The opposite problem is:

TOO MUCH CAPACITY

Think:

PROVISION:

1000 RCU

but use:

100 RCU

Result:

UNUSED PROVISIONED CAPACITY

↓

UNNECESSARY COST

### Memory Trick

OVER-PROVISION

=

WASTE MONEY

---

## Provisioned Auto Scaling

Provisioned Mode can use:

AUTO SCALING

for:

RCU

and:

WCU

Think:

TRAFFIC ↑

↓

AUTO SCALE CAPACITY ↑

TRAFFIC ↓

↓

AUTO SCALE CAPACITY ↓

This helps reduce the need to manually resize:

READ CAPACITY

and:

WRITE CAPACITY

### Memory Trick

PROVISIONED + AUTO SCALING

=

PLANNED MODE WITH FLEXIBILITY

---

## Auto Scaling Does Not Make It On-Demand

A common exam trap is assuming:

AUTO SCALING ENABLED

means:

ON-DEMAND MODE

It does not.

Think:

PROVISIONED MODE

↓

RCU + WCU

↓

OPTIONAL AUTO SCALING

This is still:

PROVISIONED MODE

### Memory Trick

AUTO SCALING

≠

ON-DEMAND

---

## On-Demand Mode

With On-Demand Mode:

DYNAMODB AUTOMATICALLY

scales read and write capacity based on:

ACTUAL WORKLOAD

Think:

TRAFFIC ↑

↓

CAPACITY ↑

TRAFFIC ↓

↓

CAPACITY ↓

You do not manually specify:

RCU

or:

WCU

in the same way as Provisioned Mode.

### Memory Trick

ON-DEMAND

=

AWS HANDLES CAPACITY

---

## No Capacity Planning

On-Demand Mode requires:

NO CAPACITY PLANNING

Think:

DON'T KNOW TRAFFIC?

↓

ON-DEMAND

AWS automatically adjusts capacity as workload changes.

### Memory Trick

UNKNOWN CAPACITY

=

ON-DEMAND

---

## On-Demand Scaling

Your SAA slides emphasize that reads and writes:

AUTOMATICALLY SCALE UP

and:

AUTOMATICALLY SCALE DOWN

with your workload.

Think:

QUIET

↓

LOW CAPACITY

TRAFFIC SPIKE

↓

MORE CAPACITY

QUIET AGAIN

↓

LESS CAPACITY

### Memory Trick

ON-DEMAND

=

FOLLOW THE TRAFFIC

---

## Best On-Demand Workloads

On-Demand Mode is ideal for:

UNPREDICTABLE WORKLOADS

and:

STEEP SUDDEN SPIKES

Think:

NORMAL TRAFFIC

↓

SUDDEN HUGE SPIKE

↓

NORMAL AGAIN

If you cannot accurately predict:

WHEN

or:

HOW LARGE

the spike will be:

ON-DEMAND

is a strong choice.

### Memory Trick

SPIKY

=

ON-DEMAND

---

## Sudden Spike Scenario

Imagine:

NORMAL TRAFFIC

=

1,000 REQUESTS

Then suddenly:

100,000 REQUESTS

Think:

1K

↓

100K

↓

1K

A workload like this can be difficult to provision accurately.

On-Demand Mode:

↓

AUTOMATICALLY ADJUSTS CAPACITY

### Memory Trick

SURPRISE TRAFFIC

=

ON-DEMAND

---

## New Application Scenario

Suppose you are launching a:

NEW APPLICATION

You do not know:

HOW MANY USERS

or:

HOW MUCH TRAFFIC

it will receive.

Think:

NO HISTORICAL DATA

↓

NO CAPACITY FORECAST

↓

ON-DEMAND

### Memory Trick

NEW APP + UNKNOWN TRAFFIC

=

ON-DEMAND

---

## Pay for What You Use

With On-Demand Mode:

YOU PAY FOR ACTUAL READ / WRITE USAGE

Think:

USE MORE

↓

PAY MORE

USE LESS

↓

PAY LESS

This provides:

OPERATIONAL SIMPLICITY

because capacity does not need to be manually provisioned.

### Memory Trick

ON-DEMAND

=

PAY PER USE

---

## On-Demand Cost

Your SAA course specifically notes that On-Demand is:

MORE EXPENSIVE

than Provisioned Mode.

Think:

ON-DEMAND

=

FLEXIBILITY

but:

HIGHER COST

### Memory Trick

ON-DEMAND

=

EASY BUT EXPENSIVE

---

## Provisioned vs On-Demand

### Provisioned Mode

YOU:

PLAN CAPACITY

and configure:

RCU + WCU

Best for:

PREDICTABLE TRAFFIC

Pricing:

PAY FOR PROVISIONED CAPACITY

Optional:

AUTO SCALING

---

### On-Demand Mode

AWS:

AUTOMATICALLY SCALES CAPACITY

No:

CAPACITY PLANNING

Best for:

UNPREDICTABLE / SPIKY TRAFFIC

Pricing:

PAY FOR ACTUAL USAGE

but generally:

MORE EXPENSIVE

### Memory Trick

PROVISIONED

=

PREDICT

ON-DEMAND

=

REACT

---

## Predictable vs Unpredictable

### Predictable Workload

Think:

TRAFFIC PATTERN KNOWN

↓

PROVISIONED

Example:

BUSINESS APP

↓

SIMILAR DAILY LOAD

↓

KNOWN THROUGHPUT

---

### Unpredictable Workload

Think:

TRAFFIC UNKNOWN

↓

ON-DEMAND

Example:

VIRAL MOBILE APP

↓

SUDDEN USERS

↓

UNEXPECTED SPIKES

### Memory Trick

KNOW IT?

↓

PROVISION

DON'T KNOW IT?

↓

ON-DEMAND

---

## Cost vs Convenience

Provisioned Mode can provide:

LOWER COST

for workloads where capacity is:

KNOWN

and:

WELL UTILIZED

On-Demand Mode provides:

MORE SIMPLICITY

but:

HIGHER COST

Think:

COST OPTIMIZATION

↓

PROVISIONED

OPERATIONAL SIMPLICITY

↓

ON-DEMAND

### Memory Trick

PROVISIONED

=

OPTIMIZE

ON-DEMAND

=

SIMPLIFY

---

## Read and Write Capacity Are Separate

DynamoDB separates:

READ CAPACITY

from:

WRITE CAPACITY

Think:

READ DEMAND

↓

RCU

WRITE DEMAND

↓

WCU

A workload might be:

READ HEAVY

or:

WRITE HEAVY

and require different capacity levels.

### Memory Trick

READS

and:

WRITES

=

DECOUPLED

---

## Read-Heavy Example

Imagine:

100,000 READS

and:

1,000 WRITES

Think:

HIGH READ CAPACITY

↓

LOWER WRITE CAPACITY

In Provisioned Mode:

RCU

may need to be much higher than:

WCU

### Memory Trick

READ-HEAVY

=

MORE RCU

---

## Write-Heavy Example

Imagine:

5,000 READS

and:

100,000 WRITES

Think:

LOWER READ CAPACITY

↓

HIGH WRITE CAPACITY

In Provisioned Mode:

WCU

may need to be much higher than:

RCU

### Memory Trick

WRITE-HEAVY

=

MORE WCU

---

## Provisioned Auto Scaling Architecture

Think:

APPLICATION

↓

DYNAMODB

↓

PROVISIONED RCU / WCU

Then:

TRAFFIC ↑

↓

AUTO SCALING

↓

RCU / WCU ↑

Later:

TRAFFIC ↓

↓

AUTO SCALING

↓

RCU / WCU ↓

This helps maintain:

CAPACITY UTILIZATION

without switching to:

ON-DEMAND

---

## On-Demand Architecture

Think:

APPLICATION

↓

DYNAMODB ON-DEMAND

↓

AWS MANAGES READ / WRITE CAPACITY

Traffic:

LOW

↓

HIGH

↓

VERY HIGH

↓

LOW

Capacity:

↓

AUTOMATICALLY FOLLOWS DEMAND

### Memory Trick

APP SENDS TRAFFIC

↓

DYNAMODB HANDLES CAPACITY

---

## Provisioned Mode Scenario

A company runs a DynamoDB workload with:

STABLE TRAFFIC

The engineering team knows:

EXPECTED READS

and:

EXPECTED WRITES

Requirements:

MINIMIZE COST

↓

PROVISIONED MODE

Optionally:

ENABLE AUTO SCALING

### Memory Trick

KNOWN + COST-CONSCIOUS

=

PROVISIONED

---

## On-Demand Mode Scenario

A company launches a new application.

Traffic may:

SPIKE WITHOUT WARNING

The company wants:

NO CAPACITY PLANNING

and:

MINIMAL OPERATIONAL MANAGEMENT

Answer:

ON-DEMAND MODE

### Memory Trick

UNKNOWN + SIMPLE

=

ON-DEMAND

---

## On-Demand vs Aurora Serverless

Both can appear in questions involving:

AUTOMATIC CAPACITY

But they are different database types.

### DynamoDB On-Demand

DATABASE TYPE

=

NOSQL

Capacity automatically adjusts based on:

REQUEST LOAD

---

### Aurora Serverless

DATABASE TYPE

=

RELATIONAL SQL

Compatible with:

MYSQL / POSTGRESQL

Think:

SERVERLESS NOSQL

↓

DYNAMODB ON-DEMAND

SERVERLESS SQL

↓

[[Aurora Serverless]]

### Memory Trick

NOSQL

=

DYNAMODB

SQL

=

AURORA

---

## Capacity Modes vs DAX

Do not confuse:

CAPACITY SCALING

with:

DATABASE CACHING

### Capacity Modes

Determine:

READ / WRITE THROUGHPUT

---

### DAX

Provides:

IN-MEMORY READ CACHE

Think:

NEED CAPACITY?

↓

PROVISIONED / ON-DEMAND

Need:

MICROSECOND CACHED READS?

↓

[[DAX]]

### Memory Trick

CAPACITY MODE

=

THROUGHPUT

DAX

=

CACHE

---

## Scenario Recognition

Traffic is predictable?

→ Provisioned Mode

---

Need to specify reads and writes per second?

→ Provisioned Mode

---

Question mentions RCU?

→ Provisioned Mode

---

Question mentions WCU?

→ Provisioned Mode

---

Need automatic scaling of provisioned RCU and WCU?

→ Provisioned Mode + Auto Scaling

---

Need cost optimization for predictable, steady traffic?

→ Provisioned Mode

---

Traffic is unpredictable?

→ On-Demand Mode

---

Need no capacity planning?

→ On-Demand Mode

---

Need automatic read/write scaling?

→ On-Demand Mode

---

Need to handle steep sudden traffic spikes?

→ On-Demand Mode

---

Launching a new app with unknown traffic?

→ On-Demand Mode

---

Need pay-for-use capacity?

→ On-Demand Mode

---

Need microsecond cached reads?

→ [[DAX]]

NOT a Capacity Mode

---

## Exam Traps

PROVISIONED MODE

=

DEFAULT

---

PROVISIONED

=

RCU + WCU

---

RCU

=

READ CAPACITY

---

WCU

=

WRITE CAPACITY

---

PROVISIONED

=

CAPACITY PLANNING REQUIRED

---

PROVISIONED

=

OPTIONAL AUTO SCALING

---

AUTO SCALING

≠

ON-DEMAND MODE

---

ON-DEMAND

=

NO CAPACITY PLANNING

---

ON-DEMAND

=

AUTOMATIC READ / WRITE SCALING

---

ON-DEMAND

=

PAY FOR WHAT YOU USE

---

ON-DEMAND

=

MORE EXPENSIVE

---

UNPREDICTABLE WORKLOAD

=

ON-DEMAND

---

SUDDEN SPIKES

=

ON-DEMAND

---

PREDICTABLE WORKLOAD

=

PROVISIONED

---

READ CAPACITY

and:

WRITE CAPACITY

=

SEPARATE

---

## Quick Cheat Sheet

CAPACITY MODES

=

PROVISIONED + ON-DEMAND

PROVISIONED

=

DEFAULT

PROVISIONED CAPACITY

=

RCU + WCU

RCU

=

READ CAPACITY UNIT

WCU

=

WRITE CAPACITY UNIT

PROVISIONED

=

PLAN CAPACITY

PROVISIONED AUTO SCALING

=

SUPPORTED

PROVISIONED BEST FOR

=

PREDICTABLE TRAFFIC

ON-DEMAND

=

NO CAPACITY PLANNING

ON-DEMAND SCALING

=

AUTOMATIC

ON-DEMAND BILLING

=

PAY FOR USE

ON-DEMAND COST

=

MORE EXPENSIVE

ON-DEMAND BEST FOR

=

UNPREDICTABLE TRAFFIC

SPIKES

=

ON-DEMAND

DAX

=

READ CACHE

NOT CAPACITY MODE

---

## Master Memory Trick

ASK:

CAN I PREDICT THE TRAFFIC?

YES

↓

PROVISIONED

↓

RCU + WCU

↓

OPTIONAL AUTO SCALING

NO

↓

ON-DEMAND

↓

AWS SCALES AUTOMATICALLY

↓

PAY FOR ACTUAL USE

Remember:

R

=

READ

↓

RCU

W

=

WRITE

↓

WCU

And:

STEADY

=

PROVISIONED

SPIKY

=

ON-DEMAND

### Final Rule

QUESTION SAYS:

KNOWN THROUGHPUT

+

COST OPTIMIZATION

↓

PROVISIONED

QUESTION SAYS:

UNKNOWN TRAFFIC

+

SUDDEN SPIKES

+

NO CAPACITY PLANNING

↓

ON-DEMAND

---

## Related Notes

- [[DynamoDB Overview]]
- [[DynamoDB Primary Keys]]
- [[DynamoDB Streams]]
- [[DynamoDB Indexes]]
- [[DAX]]
- [[DynamoDB Streams]]
- [[DynamoDB Global Tables]]
- [[DynamoDB TTL]]
- [[DynamoDB Backups]]
- [[Aurora Serverless]]
- [[SAA Databases Cheat Sheet]]
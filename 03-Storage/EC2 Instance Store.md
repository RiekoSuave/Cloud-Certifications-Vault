See also: [[EBS]]

See also: [[02-Compute/EC2]]

## What Problem Does It Solve?

Provides very high-performance local storage for EC2 instances.

It is useful when speed matters more than long-term data persistence.

---

## Type

Ephemeral Local Storage

---

## What Is EC2 Instance Store?

EC2 Instance Store is storage physically attached to the EC2 host.

Unlike EBS, it is not a network-attached drive.

### Memory Trick

Instance Store = Local Hardware Disk

---

## Performance

Instance Store provides:

- High I/O performance
- Fast local storage access

Your course notes position it as the better choice when higher disk performance is needed than EBS can provide.

---

## Ephemeral Storage

Instance Store is temporary.

Data is lost if the EC2 instance is:

- Stopped
- Terminated

There is also a risk of data loss if the underlying hardware fails.

### Memory Trick

Instance Store = Fast but Temporary

---

## Best Use Cases

Good for temporary data such as:

- Buffers
- Cache
- Scratch data
- Temporary files
- Temporary processing data

---

## Backup Responsibility

Backups and replication are your responsibility.

Do NOT use Instance Store as the only location for critical data that must survive instance failure or shutdown.

---

## Instance Store vs EBS

| Instance Store | EBS |
|---|---|
| Local hardware storage | Network-attached storage |
| Very high performance | Persistent block storage |
| Ephemeral | Persistent |
| Data lost on stop/termination | Data can remain |
| Good for temporary data | Good for important data |

---

## When To Choose Instance Store

Choose Instance Store when:

- You need very fast local disk performance
- Data is temporary
- Data can be recreated
- You can tolerate data loss

---

## When NOT To Choose Instance Store

Avoid it when:

- Data must persist
- Data is critical
- You need snapshots
- You need storage independent of the EC2 host

Use:

[[EBS]]

instead.

---

## Exam Scenarios

An application needs very fast temporary scratch storage.

→ EC2 Instance Store

---

A workload uses temporary cache data that can be recreated.

→ EC2 Instance Store

---

An application must retain data after the EC2 instance stops.

→ EBS

---

A company needs a persistent boot volume for EC2.

→ EBS

---

## Exam Keywords

Ephemeral

Local storage

High performance

Temporary data

Cache

Scratch

EC2

---

## Memory Tricks

Instance Store = Fast + Temporary

EBS = Persistent + Network Attached

Instance Store = Lose Data on Stop

EBS = Keep Data
See also: [[S3]]

See also: [[03-Storage/S3 Storage Classes]]

See also: [[S3 Lifecycle Policies]]

See also: [[S3 Glacier]]

## What Problem Does It Solve?

Provides the lowest-cost S3 storage for long-term archival data that is very rarely accessed.

It is designed for data that must be retained but does not need fast retrieval.

---

## Type

Deep Archive Storage

---

## What Is S3 Glacier Deep Archive?

S3 Glacier Deep Archive is designed for:

- Long-term archives
- Rarely accessed data
- Compliance records
- Legal archives
- Long-term backups

It provides extremely low storage cost in exchange for slow retrieval.

### Memory Trick

Deep Archive = Put It Away and Forget It

---

## Retrieval Times

Your course identifies two retrieval options:

### Standard

Approximately:

12 hours

### Bulk

Approximately:

48 hours

### Memory Trick

Deep Archive = Retrieval Can Wait

---

## Minimum Storage Duration

Deep Archive has a minimum storage duration of:

180 days

This is longer than:

- Glacier Instant Retrieval → 90 days
- Glacier Flexible Retrieval → 90 days

### Memory Trick

Deep Archive = Long-Term Commitment

---

## Best For

Choose Deep Archive when:

- Data is almost never accessed
- Retrieval can take many hours
- Long-term retention is required
- Lowest archival storage cost is important

---

## Common Use Cases

### Compliance Records

Organizations may need to retain records for long periods even though the records are rarely accessed.

---

### Legal Archives

Historical legal information can be stored for long-term retention.

---

### Long-Term Backups

Backups that are unlikely to be restored frequently can use Deep Archive.

---

### Rarely Accessed Data

Data that must be retained but is almost never retrieved.

---

## Deep Archive vs Glacier Instant

### Glacier Instant Retrieval

Archive storage with millisecond retrieval.

### Deep Archive

Long-term archive with retrieval measured in hours.

| Glacier Instant | Deep Archive |
|---|---|
| Millisecond retrieval | Hours |
| 90-day minimum | 180-day minimum |
| Archive needing fast access | Rarely accessed archive |

---

## Deep Archive vs Glacier Flexible

### Glacier Flexible Retrieval

Provides multiple retrieval speeds ranging from minutes to hours.

### Deep Archive

Designed for even longer-term storage where retrieval can wait much longer.

| Glacier Flexible | Deep Archive |
|---|---|
| Expedited, Standard, Bulk | Standard or Bulk |
| Minutes to hours | Hours to days |
| 90-day minimum | 180-day minimum |
| Cold archive | Deep archive |

---

## Deep Archive vs S3 Standard

### S3 Standard

Designed for frequently accessed data.

### Deep Archive

Designed for extremely infrequent access.

### Memory Trick

Standard = Use It

Deep Archive = Store It

---

## Lifecycle Connection

Older S3 objects can eventually be moved into Deep Archive as part of a storage lifecycle strategy.

Example:

S3 Standard

↓

Standard-IA

↓

Glacier

↓

Deep Archive

See:

[[S3 Lifecycle Policies]]

---

## Exam Scenarios

A company must retain compliance records for years and almost never accesses them.

→ S3 Glacier Deep Archive

---

A company wants the lowest-cost storage option for long-term archives.

→ S3 Glacier Deep Archive

---

Archived data needs millisecond retrieval.

→ Glacier Instant Retrieval

NOT Deep Archive

---

Archived data may need to be retrieved within minutes.

→ Glacier Flexible Retrieval

NOT Deep Archive

---

A company can wait many hours to retrieve its long-term backups.

→ S3 Glacier Deep Archive

---

## Exam Keywords

Lowest cost

Long-term archive

Rarely accessed

Compliance

180 days

12-hour retrieval

48-hour retrieval

---

## Memory Tricks

Deep Archive = Cheapest Archive

Deep Archive = 180 Days

Standard Retrieval = 12 Hours

Bulk Retrieval = 48 Hours

Deep Archive = Put It Away and Forget It
# EC2 Instance Store

- Physical disk attached directly to the host server — not a network drive
- Highest I/O performance possible (no network overhead)
- **Ephemeral**: data is lost when the instance is stopped or terminated
- Risk of data loss if the underlying hardware fails
- Backups and replication are your responsibility

## When to use it

Use Instance Store only when you need maximum I/O and can afford to lose the data:
- Buffer / cache
- Temporary files and scratch data
- Data you will regenerate anyway

Do not use for anything that needs to persist.

## vs EBS

| | EBS | Instance Store |
|---|---|---|
| Performance | Good | Best |
| Persistence | Yes | No — lost on stop/terminate |
| Attached via | Network | Physical |
| Cost | Pay per GB provisioned | Included with instance |

## Exam trap

- "Highest IOPS possible" → Instance Store (not even io2 matches it for raw throughput)
- "Temporary storage / scratch space / buffer" → Instance Store
- Any mention of data that must survive a restart → EBS, not Instance Store

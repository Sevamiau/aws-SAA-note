# EBS vs EFS vs EC2 Instance Store

## Comparison table

| | EBS | EFS | Instance Store |
|---|---|---|---|
| Type | Block storage | Network file system | Physical disk on host |
| Attached to | 1 instance (except io1/io2 Multi-Attach) | Many instances across AZs | 1 instance |
| AZ scope | Locked to 1 AZ | Multi-AZ | Locked to 1 AZ (tied to instance) |
| Persistence | Persists after instance stop | Persists independently | Lost when instance stops/terminates |
| OS compatibility | Linux + Windows | Linux only (POSIX/NFS) | Linux + Windows |
| Performance | Good (network-based) | Good (network-based) | Best (physically attached) |
| Cost | Pay for provisioned size | Pay per GB used | Included with instance |
| Backup | Snapshots (manual or automated) | AWS Backup / EFS Backup | Your responsibility |

---

## When to use each

**EBS**: default choice for EC2 storage — boot volumes, databases, single-instance apps.

**EFS**: when multiple EC2 instances need to share the same files — shared content, WordPress, web servers in an ASG all serving the same files.

**Instance Store**: when you need maximum I/O performance and can tolerate data loss — cache, buffer, temp files, scratch data.

---

## Exam traps

- EFS is 3x more expensive than gp2 EBS — the exam may ask "cost-effective shared storage" → still EFS if it needs to be shared across instances
- EFS is Linux only — if the question mentions Windows, EFS is wrong
- Instance Store data is permanently lost on stop/termination — never use it for data you need to keep
- To move an EBS volume to another AZ: snapshot it, restore in the target AZ
- Avoid running EBS snapshots during peak traffic — snapshots consume I/O

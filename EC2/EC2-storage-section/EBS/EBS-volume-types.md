# EBS Volume Types

Only **gp2/gp3** and **io1/io2** can be used as boot volumes.

## Quick decision table

| Type | Category | Pick this when |
|---|---|---|
| gp3 | SSD | Default choice for most workloads |
| gp2 | SSD | Legacy — prefer gp3 for new volumes |
| io2 Block Express | SSD | Database needing > 16,000 IOPS or sub-ms latency |
| io1 | SSD | Database needing > 16,000 IOPS (older option) |
| st1 | HDD | Big Data, logs, data warehouses — high throughput, low cost |
| sc1 | HDD | Infrequently accessed data — lowest cost possible |

**Exam trap**: if the question says "lowest cost" and the data is rarely accessed → sc1. If it says "high throughput for sequential reads" → st1. If it says "boot volume" → only SSD types (gp or io).

---

## General Purpose SSD (gp2 / gp3)

- Cost-effective, low-latency
- Used for: system boot volumes, virtual desktops, dev/test environments
- Size: 1 GiB to 16 TiB

**gp3** (prefer this):
- Baseline: 3,000 IOPS and 125 MiB/s throughput
- Can scale IOPS up to 16,000 and throughput up to 1,000 MiB/s independently

**gp2** (legacy):
- IOPS linked to size: 3 IOPS per GiB, max 16,000 IOPS (reached at 5,334 GiB)
- Small volumes can burst to 3,000 IOPS

---

## Provisioned IOPS SSD (io1 / io2)

- For critical workloads that need sustained IOPS or more than 16,000 IOPS
- The only types that support **EBS Multi-Attach**

**io1** (4 GiB - 16 TiB):
- Max 64,000 IOPS on Nitro instances, 32,000 on others
- IOPS configurable independently from size

**io2 Block Express** (4 GiB - 64 TiB):
- Sub-millisecond latency
- Max 256,000 IOPS with IOPS:GiB ratio of 1,000:1
- Best choice when you need maximum performance

---

## Hard Disk Drives (HDD)

- Cannot be a boot volume
- Size: 125 GiB to 16 TiB

**st1 - Throughput Optimized**:
- For frequently accessed, throughput-intensive workloads
- Use cases: Big Data, data warehouses, log processing
- Max throughput: 500 MiB/s, max IOPS: 500

**sc1 - Cold HDD**:
- For infrequently accessed data
- Lowest cost EBS option
- Max throughput: 250 MiB/s, max IOPS: 250

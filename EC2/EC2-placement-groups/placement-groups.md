# EC2 Placement Groups

Control over how EC2 instances are physically placed within AWS infrastructure.

## Quick decision table

| Strategy | Hardware | AZ scope | Pick this when |
|---|---|---|---|
| Cluster | Same rack, same AZ | Single AZ | Need maximum network speed between instances |
| Spread | Different racks | Multi-AZ | Need to isolate instances from each other's failures |
| Partition | Different racks per partition | Multi-AZ | Large distributed systems (Hadoop, Kafka, Cassandra) |

---

## Cluster

- All instances on the same rack in the same AZ
- Pros: 10 Gbps network between instances (with Enhanced Networking)
- Cons: if the AZ or rack fails, all instances fail at once
- Use for: HPC, Big Data jobs that need to finish fast, extremely low latency + high throughput

## Spread

- Each instance on a separate physical rack
- Max 7 instances per AZ per placement group
- Pros: maximizes availability — a rack failure only takes down 1 instance
- Use for: small number of critical instances that must be isolated from each other

## Partition

- Instances divided into partitions — each partition uses a different rack
- Up to 7 partitions per AZ, hundreds of EC2 instances total
- A partition failure affects only instances in that partition
- Instances can see which partition they are in (via metadata)
- Use for: distributed big data systems — HDFS, HBase, Cassandra, Kafka

---

## Exam trap

- "Low latency between instances" → Cluster
- "Isolate each instance from hardware failure" → Spread
- "Large-scale distributed system like Kafka or HDFS" → Partition
- Spread has a hard limit of 7 instances per AZ — if the question describes more than 7, Spread won't work

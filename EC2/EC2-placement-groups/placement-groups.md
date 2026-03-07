# Placement Groups

-Sometimes you want control over the EC2 instance placement strategy
-That strategy can be defined using placement Groups
-When you create a placement group you specify one of the following strategies for the group:
    .Cluster: Cluster instances into a low-latency group in a single Availability Zone
    .Spread: Spreads instances across underlying hardware(max 7 instances per group per AZ)
    .Partition: Spreads instances across many different partitions (which rely on different sets of racks) within an AZ. Scales to 100s of EC2 instances per group (Hadoop, Cassandra, Kafka)

# Placement Groups Clusters (low-latency, 10Gbps network)

-Pros: Great network (10Gbps bandwidth between instances with Enhanced Network enabled(recommended))
-Cons: If the AZ fails, all instances fails at the same time
-Use case:
    .Big Data job that needs to complete fast
    .Application that needs extremely low low-latency and high network throughput


# Placement Groups Spread

-Pros: 
    .Can span across AZ
    .Reduced risk of simultaneous failure
    .EC2 instances are on different physical hardware

Cons:
    .Limited to 7 instances per AZ per placement group

Use case:
    .Application that needs to maximize high Availability
    .Critical Application where each instance must be isolated from failure from each other

# Placement Groups Partition:

-Up to 7 partitions per AZ
-Can span across multiple AZ's in the same region
-Up to 100's of EC2 instances
-The instances in a partition do not share racks with the instances in the other partitions 
-A partition failure can affect many EC2 but wont affect other partitions
-EC2 instances get acces to the partition info as metadata

-Use cases:
    .HDFS, HBase, Cassandra, Kafka.

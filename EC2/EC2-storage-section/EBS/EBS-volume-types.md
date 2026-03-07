# EBS Volume Types

-EBS Volumes com in 6 types:
    .gp2/gp3 (SSD): General purpose SSD Volume that balances price and performance for a wide variety of workloads
    .io1/ io2 Block Express (SSD): Highest-Performance SSD volume for mission-critical low-latency or high-troughput workloads
    .st 1 (HDD): Low cost HDD volume designed for frequently accessed, throughput intensive workloads 
    .sc 1 (HDD): Lowest cost HDD volume desgned for less frequently accessed workloads

-EBS Volumes are characterized in Size / throughput / IOPS (I/O per sec)
-When in doubt always consult the AWS doc 
-Only gp2/gp3 and io1/io2 Block Express can be used as boot Volumes


# EBS Volume Types use cases

-Cost effective storage, low-latency
-System boot Volumes, virtual desktops, development and test environments
- 1 GiB up to 16TiB
-gp3:
    .Baseline of 3000 IOPS and throughput of 125 MiB/sec
    .Can increase IOPS up tu 16,000 and throughput up to 1000 MiB/sec independently

-gp2:
    .Small gp2 Volumes can burst IOPS to 3000
    .Size of the volume and IOPS are linked, mas IOPS us 16,000
    .3 IOPS per GiB, means at 5,334 GiB we are at the max IOPS

## Provisioned IOPS (PIOPS) SSD

-Critical Business app with sustained IOPS performance
-Or apps that need more than 16,000 IOPS
-Great for databases workloads(sensitive to storage perf and consistency)

-io 1 (4GiB - 15Tib):
    .Max PIOPS: 64,000 for Nitro EC2 instances & 32,000 for other
    .Can increase PIOPS independently from storage Size
-io 2 Block Express (4 GiB - 64 TiB):
    .Sub-milisecond latency 
    .Max PIOPS: 256,000 with an IOPS:GiB ratio of 1000:1 
Support EBS Multi-attach

## Hard Disk Drives (HHD)

-Cannot be a boot volume
-125 GiB to 16TiB
-throughput optimized HHD (stl)
    .Big Data, Data Warehouses, log procesing
    .Max throughput 500 MiB/s - mas IOPS 500

-Cold HHD (scl):
    .For data that is infrequently accessed
    .Scenarios where lowest cost is important 
    .Max throughput 250 MiB/s - max IOPS 250



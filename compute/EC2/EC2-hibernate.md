# EC2 Hibernate

-We know we can stop, terminate instances:
    .Stop: The data on disk (EBS) is kept intact in the next start
    .Terminate: Any EBS volumes (root) also set-up to be destroyed is lost

-On start, the following happens:
    .First start: The OS boots & the EC2 User Data script runs 
    .Following starts:  The OS boots up 
    .The your application starts, caches get warmed up, and that can take time!


-Introducing EC2 Hibernate:
    .The in-memory (RAM) state is preserved
    .The instance boot is much faster
    .Under the hood: The RAM stat is written to a file in the root EBS volumes  
    .The root EBS volume must be encrypted

-Use cases:
    .Long-running processing
    .Saving the RAM state
    .Services that take time to initialize


# GOOD TO KNOW 

-Supported instances families: C3, C4, C5, M3, M4, R3, R4, T2, T3 ...
-instances RAM size: Must be less than 150 GB
-Instance size: Not Supported for bare metal instances
-AMI: Amazon linux, linux ami, ubuntu, rhel, centos and win
-Root Volume: Must be EBS encrypted, not instance store, and large
-Available for on demand, reserved and spot instances

-An instance can NOT be Hibernated more than 60 days

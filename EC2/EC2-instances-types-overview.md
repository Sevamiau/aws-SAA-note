# EC2 Instances types overview

-You can use different types of EC2 instances that are optimised for different use cases
-AWS has the following naming convention:

    .m5.2xlarge 
    .m: instance class
    .5: generation (AWS imrpoves them over time)
    .2xlarge: size within the instance class

### instance type - General Purpose

-Great for a diversity of workloads such as we servers or code respositories
-Balance between:
    .Compute
    .Memory
    .Networking

### Compute Optimized (C name)

-Great for compute-intensive workloads that require high performance processors
    .Batch processing workloads
    .Media trasncoding
    .High performance web servers
    .High performance computing (HPC)
    .Scientific modeling and machine learning
    .Dedicated gaming servers

### Memory Optimized (R name)

-Use cases:
    .High performance relational/non-relational databases
    .Ditributed web scale cache
    .In-memory databases optimized for BI (business intelligence)
    .Applications performing real-tine processing of big structured data

### Storage Optimized (I name)

-Great for Storage-intensive tasks that require high sequential read and write acces to large data sets on local Storage
-Use cases:
    .High frequency online transation processing (OLTP) systems
    .Relational and noSQL databases
    .Cache for In-memory databases (for example, redis)
    .Data warehousing Applications
    .Ditributed file systems

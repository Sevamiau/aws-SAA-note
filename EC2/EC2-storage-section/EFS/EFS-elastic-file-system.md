# Amazon EFS - Elastic File System

-Managed NFS (Network File System) that can be mounted on many EC2
-EFS works with EC2 instances in multi AZ 
-Highly available, scalable and expensive (3x expensive than a gp2), pay per use.

-Use cases:
    .Content management, web serving, data sharing, Wordpress.
-Uses NFSv4.1 protocol
-Uses security group to control access to EFS
-Compatible with Linux based AMI only (not win)
-Encryption at res using KMS

-POSIX file System (~Linux) that has a standard file API 
-File System scales automatically. pay per use for each GiB of data you use.




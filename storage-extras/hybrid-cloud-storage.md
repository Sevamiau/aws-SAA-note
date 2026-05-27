# Hybrid Cloud for Storage

- AWS is pushing for "Hybrid cloud"
    * Part of your infrastructure is on the cloud 
    * Part of your infra is on-premises 

- This can be due to:
    * Long cloud migrations
    * Security requirements 
    * Compliance requirements
    * IT strategy 
- S3 is a proprietary storage technology (unlike EFS/NFS) so in order to expose the S3 data on-premises we use **AWS Storage Gateway**


# AWS Storage Gateway
- Bridge between on-premises data and cloud data 
- **Use Cases:** 
    * Disaster recovery
    * Back-up & restore
    * Tiered storage 
    * on-premises cache & low-latency file access

- Types of Storage Gateway:
    * **S3 file Gateway:**
        * Configured S3 buckets are accessible using the NFS and SMB protocol
        * Most recently used data is cached in the File Gateway
        * Supports S3 Standard, S3 Standard IA, S3 One Zone IA, S3 Intelligent Tiering
        * Transition to S3 Glacier using a Lifecycle Policy
        * Bucket access using IAM roles for each File Gateway
        * SMB protocol has integration with Active Directory (AD) for user authentication
    * **Volume Gateway:**
        * Block storage using iSCSI (Internet Small Computer Systems Interface) protocol backed by S3
        * Backed by EBS snapshots which can help restore on-premises volumes 
        * **Cached Volumes**: Low latency access to most recent data    
        * **Stored Volumes:** Entire dataset is on premise, scheduled backups to S3  
    * **Tape Gateway:**
        * Some companies have backup processes using physical tapes 
        * With Tape Gateway, companies use the same processes but in the cloud 
        * Virtual Tape Library (VTL) backed by Amazon S3 and Glacier 
        * Works with leading backup software vendors 

# EBS Multi-Attach - io1/io2 familiy

-Attach the same EBS volume to multiple EC2 instances in the same AZ
-Each instance has full read & write permissions to the high-performance volume
-Use case:
    .Achieve higher application availability in clustered Linux apps (ex:Teradata)
    .Applications must manage concurrent write operations

-Up to 16 EC2 instances at a time 
-Must use a file system thats cluster-aware (not XFS, EXT4, etc...)

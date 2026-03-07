# AMI Overview

-AMI = Amazon Machine Image
-AMI are a customization of an EC2 instance
    .You add your own software, config, OS, monitoring...
    .Faster boot/config time because all your software is pre-packaged
-AMI are built for specific region (and can be copied across regions)
-You can launch EC2 instances provided:
    .By a public AMI: AWS provided
    .Your own AMI: you make and maintain them yourself
    .An AWS Marketplace: an AMI someone else made (an potentially sales)

# AMI Process (from and EC2 instance)

-Start an EC2 instance and customize it
-Stop the instance (for data integrity)
-Build an AMI - This will al create EBS snapshots
-Launch instances from other AMIS's 

# EBS vs EFS - Elastic bloc storage

-EBS volumes:
    .One instance (except multi-attach io1/io2)
    .are locked at the AZ level
    .gp2: IO increases if the disk size increases
    .gp3: & io1 can increase IO independently 

-To migrate an EBS volume across AZ:
    .Take a snapshot
    .Restore the snapshot to another AZ
    .EBS backups use IO and you shouldnt run them while  your app is handling a lot of traffic

-Root EBS volumes of instance get terminated by default if the EC2 instance gets terminated (you can disable that feature)


-EFS File system:
    .Mounting 100s of instances across AZ
    .EFS share website files (Wordpress)
    .Only for linux instances (POSIX)

    .EFS has higher proce point than EBS
    .Can leverage storage tiers for cost savings

-Remember:EFS vs EBS vs instance store

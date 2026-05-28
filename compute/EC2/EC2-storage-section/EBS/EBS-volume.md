# Whats an EBS Volume?

-An EBS (Elastic Block Store) Volume is a network drive you can attach to your instances while they run 
-It allows your instance to persist data, even after their termination
-They can only be mounted to one instance at a time (at the CPP level (certified cloud practitioner)) At associate level (Solutions architect, Developer, SysOps) there's a multi attach feature for some EBS
-They are bound to a specific availability zone

-Think of them as a 'network USB stick'

# EBS Volume

-Its a network drive (i.e not a physical drive)
    .It uses the network to communicate the instance, which means there might be a but of latency
    .It can be detached from an EC2 instance and attached to another one quickly

-Its locked to an AZ
    .An EBS Volume in us-east-1 cannot be attached to us-east-1b
    .To move volume across, you first need to snapshot it

-Have a provisioned capacity (size in GBs, and IOPS)
    .You get billed for all the provisioned capacity
    .You can increase the capacity of the drive over time


# EBS Delete on termination attribute

-Controls the EBS behaviour whe an EC2 instance terminates
    .By default, the root EBS volume is deleted (attribute enabled)
    .By default, any other attached EBS volume is not deleted (attribute disabled)
-This con be controlled by the AWS console/ AWS CLI


-Use case: Preserve root volume when instance is terminated

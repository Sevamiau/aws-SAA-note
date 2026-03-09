# Whats an Auto Scaling Group?

-In real-life the load on your website and apps can change
-In the cloud, you can create an get rid of servers very quickly

-The goal of a ASG is to:

    .Scale out (add EC2 instances) to match an increased load
    .Scale in (remove EC2 instances) to match a drecreased load
    .Ensure we have a minimum and maximum number of EC2 instances running
    .Automatically register new instances to a load balancer
    .Re-create an EC2 instance in case a previous one is terminated (ex. If unhelathy)

-ASG are free (You only pay for the underlying EC2 instances)

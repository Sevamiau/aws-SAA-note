# ECS Service Auto-Scaling 

- Automatically increase/decrease the desired number of ECS Tasks 

- Amazon ECS Auto Scaling uses AWS Application Auto Scaling 
    * ECS Service Average CPU utilization
    * ECS Service Average Memory utilization - Scale on RAM
    * ALB Request Count Per Target - metric coming from the ALB

- **Target Tracking:** Scale based on target value for a specific ClowdWatch metric 
- **Step Scaling:** Scale based on a specified ClowdWatch Alarm 
- **Scheduled Scaling:** Scale based on a specified date/time (predictable changes)

- ECS Service Auto Scaling (task level) is not EC2 Auto Scaling (EC2 instance leve)
- Fargate Auto Scaling is much easier to setup (because **serverless** )


## ECS Launch Type - Auto Scaling EC2 instances 

- Accommodate ECS Service Scaling by adding underlying EC2 instances 

- **Auto Scaling Group Scaling**
    * Scale your ASG based on CPU utilization
    * Add EC2 instances over time 

- **ECS Cluster Capacity Provider**
    * Used to Automatically provision and scale the infrastructure for your ECS tasks 
    * Capacity Provider paired with and Auto Scaling Group
    * Add EC2 instances when youre missing capacity (CPU, RAM)



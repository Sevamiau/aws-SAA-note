# Application Load Balancer Target Groups

-EC2 instances (Can be managed by an Auto Scaling Group) - HTTP
-ECS tasks (managed by ECS itself) - HTTP
-Lambda functions - HTTP request is translated into a JSON event
-IP Addresses - must be private IPs

-ALB can route to multiple target Groups
-Health checks are at the target Group level

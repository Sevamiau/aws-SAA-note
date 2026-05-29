# Amazon ECS - EC2 Launch Type 

- ECS = Elastic Container Service 
- Launch Docker containers on AWS = Launch ECS Tasks on ECS Clusters 
- EC2 Launch Type: You mus provision and mantain the infrastructure (the EC2 instances)
- Each EC2 instance must run the ECS agent to register in the ECS Cluster 
- AWS takes car of starting/stopping containers 
 

## Amazon ECS - Fargate Launch Type 

- Launch Docker containers on AWS 
- You do not provision the infrastructure (no EC2 instances to manage)
- Its all Serverless
- You just create task definitions 
- AWS just runs ECS Tasks for you based on the CPU/RAM you need 
- To scale just increase the number of tasks. Simple, no more EC2 Instances 


## IAM Roles for ECS 

- EC2 instance Profile (EC2 Launch Type only)
    * Used by the ECS agent
    * Makes API calls to ECS Service
    * Send container logs to Cloudwatch Logs 
    * Pull Docker image from ECR 
    * Reference sensitive data in Secrets Manager or SSM Parameter Store 

- ECS Task Role:
    * Allows each task to have a specific role 
    * Use different roles for the different ECS Services your run 
    * Task Role is defined in the task definition 


## Load Balancer Integrations 

- Application Load Balancer supported and works for most use cases 
- Network Load Balancer recommender only for high throughput/high performance use cases, or to pair it with AWS Private Link 
- Classic Load Balancer supported but not recommended 


# Data Volumes (EFS)

- Mount EFS file systems onto ECS tasks
- Works for both EC2 and Fargate launch types 
- Tasks running in any AZ will share the same data in the EFS file system 
- Fargate + EFS = Serverless 

- **Use Cases:** Persistent multi-AZ shared Storage for your containers 

- note: Amazon s3 cannot be mounted as a file system 

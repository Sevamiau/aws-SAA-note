# Route 53 - Health Checks

----------

- HTTP Health Checks are only for public resources
- Health Check => Automated DNS Failover:
  * Health Checks that monitor and endpoint (app, server, other AWS resources)
  * Health Checks that monitor other Health Checks (calculated Health Checks)
  * Health Checks that monitor CloudWatch Alarms (full control!) - e.g: trhottles of DynamoDB, alarms on RDS, custom metrics (helpful for private resources)

- Health checks are integrated with CW metrics  

----------

## Monitor and endpoint 

- About 15 global health checkers will check the endpoint health
  * Healthy/Unhealthy threshold — 3 (default)
  * Interval — 30 sec (can set to 10 sec at higher cost)
  * Supported protocol: HTTP, HTTPS, and TCP.
  * if > 18% of health checkers report the endpoint is healthy. otherwise its Unhealthy
  * Ability to choose which locations you want Route 53 to use 

- Health Checks pass only when the endpoint responds with the 2xx and 3xx status code 
- Health Checks can be setup to pass/fail based on the text in the first 5120 bytes of the response 
- Configure your router/firewall to allow incoming request from route 53 health checkers

----------

## Calculated Health Checks

- Combine the results of multiple Health checks into a single Health Check 
- You can use OR, AND or NOT 
- Can monitor UP to 256 child Health Checks
- Specify how many of the health checks need to pass to make the parent pass 
- Usage: Perform maintenance  to your website without causing all health checks to fail 

----------

## How to monitor the Health of a Private resource - Private Hosted Zones

- Route 53 health Checkers are outside the VPC
- They cant access private endpoints (private VPC or on-premises resources)

- You can create a CloudWatch metric and associate a CloudWatch alarm, then create a health check that checks that checks the alarm itself 

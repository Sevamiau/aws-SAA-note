# Why use an Elastic Load Balancer?

-An Elastic Load Balancer is a managed load Balancer
    .AWS guarantess that it will be working
    .AWS takes care fot upgrades, maintenance, high availability
    .AWS provides only a few configuration knobs

-It cost less to setup your own load balances but it will be a lot more effort on your end 

-It is integrated with many AWS offering/services
    .EC2,EC2 auto scaling groups, amazon ECS 
    .AWS Certificate Manager (ACM), CloudWhatch
    .Route 53, AWS WAF, AWS Global Accelerator


## Health Checks

-Heal Checks are crucial for load balancers
-They enable the load balances to know if instances it forward traffic to are available to reply to request
-The health check is done on a port and a route (/health is common)
-If the response is not 200(OK), then the instances is unhealthy 

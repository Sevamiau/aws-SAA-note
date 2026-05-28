# Amazon Global Accelerator

- You have deployed an app and have global users who want to access it directly
- They go over the public internet which can add a lot of latency due to many hops
- We wish to go as fast as possible through the AWS network to minimize latency 

## Unicast IP vs Anycast IP 

- **Unicast IP:** One server holds one IP address
- **Anycast IP:** All servers hold the same IP address and the client is routed to the nearest one 

## Amazon Global Accelerator uses that Anycast IP concept

- Leverage the AWS internal network to route to your application
- **2 Anycast IP** are created for your application 
- The Anycast IP sends traffic directly to Edge Locations
- the Edge Location sends the traffic to your application


- Works with Elastic IP, EC2 instances, ALB, NLB, public or private
- Consistent Performance
    * Intelligent routing to lowest latency and fast regional failover
    * No issue with client cache (because the IP does not change)
    * Internal AWS network
 
- Health Checks
    * Global Accelerator performs a health check of your applications
    * Helps make your application global (failover less than 1 minute for unhealthy)
    * Great for disaster recovery (thanks to the health checks)

- Security 
    * Only 2 external IP need to be whitelisted
    * DDoS protection thanks to AWS Shield 


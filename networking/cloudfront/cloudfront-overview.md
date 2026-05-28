# Amazon CloudFront Overview

- Content Delivery Network (CDN)
- Improves read performance, content is cached at the edge
- Improves user experience 
- Hundreds of Points of Presence globally (Edge location, caches)
- DDoS protection (because worldwide), integration with Shield, AWS Web Application Firewall

# CloudFront Origins

- S3 bucket
    * For distributing files and caching them at the edge
    * For uploading files to S3 through CloudFront
    * Secured using Origin Access Control (OAC)

- VPC Origin 
    * For applications hosted in VPC private subnets 
    * Private Application Load Balancer / Network Load Balancer / EC2 Instances
    
- Custom Origin (HTTP)
    * S3 Website (must first enable the bucket as a static s3 website)
    * Any public HTTP backend 


# CloudFront vs S3 Cross Region Replication

- **CloudFront:**
    * Global Edge Network
    * Files are cached for a TTL (maybe a day)
    * Great for static content that must be available everywhere

- **S3 Cross Region Replication**
    * Must be setup for each region you want replication to happen
    * Files are updated in near real-time
    * Read Only
    * Great for dynamic content that needs to be available at low-latency in few regions 


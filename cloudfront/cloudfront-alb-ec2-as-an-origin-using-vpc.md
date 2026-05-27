# Amazon Cloudfront - ALB or EC2 as an Origin Using VPC Origins

- Allows you to deliver content from your application hosted in your VPC private subnets (no need to expose them on the internet)
- Deliver traffic to **private**:
    * Application Load Balancer
    * Network Load Balancer
    * EC2 instances 


### **CloudFront - VPC Origin (Private Delivery)**

*   **The Concept:** CloudFront (the global CDN) can now connect **directly** to resources inside your private VPC without them ever being exposed to the public internet.
*   **The Workflow:** 
    1.  Users connect to the global **CloudFront Edge Location**.
    2.  CloudFront uses a secure, private tunnel (**VPC Origin**) to enter your network.
    3.  It delivers the traffic directly to an **ALB, NLB, or EC2 instance**.
*   **The Big Win:** These resources (ALB/EC2) stay in a **Private Subnet**. They do **not** need a Public IP address and they do **not** need to be "Open to the World" to use the CDN.

---

### **Exam "Cheat Sheet" for SAA-C03:**

| If the question asks for... | The Answer is **CloudFront VPC Origin** |
| :--- | :--- |
| **"Highest security for a CDN"** | Keep the Load Balancer private and use VPC Origin. |
| **"Serve private content globally"** | Connect CloudFront directly to a private ALB. |
| **"Minimize public surface area"** | Eliminate public IPs on your origins by using VPC Origin. |




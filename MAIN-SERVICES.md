
### **1. Compute (The "Engine")**
*   **EC2:** Virtual machines (The AWS version of your KVM/Fedora VMs).
*   **Lambda:** "Serverless" code. Runs only when triggered; you don't manage the OS.
*   **ECS / EKS:** Container orchestrators. ECS is AWS-native; **EKS is managed Kubernetes**.
*   **Fargate:** "Serverless" containers. You run Docker without managing the underlying EC2 hosts.
*   **ASG (Auto Scaling Group):** Automatically adds/removes EC2 instances based on demand.

### **2. Storage (The "Warehouse")**
*   **S3:** Object storage. Infinite, durable, used for files/backups/web hosting.
*   **EBS:** Network drives for EC2 (The "C:" or "Virtual Disk" for your VMs).
*   **EFS:** Managed NFS for Linux. Can be mounted by hundreds of EC2s at once.
*   **FSx:** Specialized file systems (Windows, Lustre, NetApp, ZFS).

### **3. Networking (The "Cables & Routers")**
*   **VPC:** Your private virtual network. This is your **MikroTik** world.
*   **Route 53:** Managed DNS. Handles domain names and health checks.
*   **ALB (Application Load Balancer):** Layer 7. Routes HTTP traffic to different targets.
*   **NLB (Network Load Balancer):** Layer 4. Handles millions of requests/sec with ultra-low latency.
*   **CloudFront:** CDN. Caches content globally at Edge Locations.

### **4. Databases (The "Memory")**
*   **RDS:** Managed Relational Database (MySQL, Postgres, SQL Server).
*   **Aurora:** AWS-exclusive relational database. 5x faster than standard MySQL.
*   **DynamoDB:** NoSQL Key-Value database. High performance at any scale (milliseconds).
*   **ElastiCache:** In-memory cache (Redis/Memcached). Speeds up read-heavy apps.
*   **Redshift:** Data Warehouse. For "Big Data" analytics, not for running a website.

### **5. Application Integration (The "DevOps Glue")**
*   **SQS (Simple Queue Service):** Decouples applications using message queues.
*   **SNS (Simple Notification Service):** Sends emails, SMS, or triggers for many subscribers at once.
*   **EventBridge:** The "Traffic Cop" we discussed. Routes events between services.
*   **API Gateway:** The "Front Door" for your APIs. Connects users to Lambda functions.

### **6. Security & Monitoring (The "Guard & Camera")**
*   **IAM:** Identity and Access Management. Who can do what.
*   **KMS:** Key Management Service. Manages the "Master Keys" for encryption.
*   **CloudWatch:** **Observability.** Monitors metrics (CPU, RAM) and stores logs.
*   **CloudTrail:** **Auditing.** Records every single API call (Who did what and when).
*   **WAF (Web Application Firewall):** Protects against SQL injection and hackers at the Edge.

---

### **Cheat Sheet**
When you look at this list, don't try to memorize every feature. Instead, learn the **"VS" (Versus)**. 

The exam loves to put two similar services in the answers to see if you know the subtle difference:
*   **EBS vs. EFS:** (Single VM vs. Shared by many).
*   **RDS vs. DynamoDB:** (SQL/Structure vs. NoSQL/Speed).
*   **ALB vs. NLB:** (HTTP vs. TCP/UDP).
*   **CloudWatch vs. CloudTrail:** (Performance metrics vs. Security audit).


----------


### **1. Compute (The Core)**
*   **Amazon EC2:** Provides scalable computing capacity via virtual servers.
*   **AWS Lambda:** A serverless, event-driven compute service that lets you run code without provisioning or managing servers.
*   **AWS Fargate:** A serverless, pay-as-you-go compute engine that lets you build applications without managing servers (used for ECS/EKS).
*   **Amazon EKS:** A managed service to run **Kubernetes** on AWS without needing to install, operate, and maintain your own control plane.

### **2. Storage (Data Management)**
*   **Amazon S3:** An object storage service offering industry-leading scalability, data availability, security, and performance.
*   **Amazon EBS:** High-performance block-storage service designed for use with EC2 for both throughput and transaction-intensive workloads.
*   **Amazon EFS:** A serverless, fully elastic **NFS** file system that lets you share file data without provisioning or managing storage.
*   **Amazon FSx:** Provides fully managed, high-performance file systems for **Windows, Lustre, NetApp ONTAP, and OpenZFS**.

### **3. Networking (Connectivity)**
*   **Amazon VPC:** Lets you provision a logically isolated section of the AWS Cloud where you can launch resources in a virtual network you define.
*   **Amazon Route 53:** A highly available and scalable cloud **DNS** web service designed to give developers a reliable way to route users to internet applications.
*   **Amazon CloudFront:** A content delivery network (CDN) service built for high performance, security, and developer convenience.
*   **Elastic Load Balancing (ELB):** Automatically distributes incoming application traffic across multiple targets, such as EC2 instances, containers, and IP addresses.

### **4. Databases (Persistence)**
*   **Amazon RDS:** A managed service that makes it easy to set up, operate, and scale a **Relational Database** (MySQL, PostgreSQL, etc.) in the cloud.
*   **Amazon Aurora:** A MySQL and PostgreSQL-compatible relational database built for the cloud that combines the performance of high-end commercial databases with simplicity.
*   **Amazon DynamoDB:** A fully managed, serverless, **NoSQL** database designed to run high-performance applications at any scale.
*   **Amazon ElastiCache:** A fully managed **in-memory** caching service (Redis or Memcached) to accelerate application and database performance.

### **5. Application Integration (The "Glue")**
*   **Amazon SQS:** A fully managed **message queuing** service that enables you to decouple and scale microservices, distributed systems, and serverless applications.
*   **Amazon SNS:** A fully managed **Pub/Sub** messaging service for both microservices-to-microservices and microservices-to-person communication.
*   **Amazon EventBridge:** A serverless **event bus** that helps you receive, filter, transform, route, and deliver events.
*   **Amazon API Gateway:** A fully managed service that makes it easy for developers to create, publish, maintain, monitor, and secure **APIs** at any scale.

### **6. Security, Monitoring & Governance**
*   **AWS IAM:** Securely manage access to AWS services and resources by creating and managing AWS users, groups, and roles.
*   **AWS KMS:** A managed service that makes it easy for you to create and control the **cryptographic keys** used to protect your data.
*   **Amazon CloudWatch:** A monitoring and observability service that provides data and actionable insights to monitor applications and respond to system-wide performance changes.
*   **AWS CloudTrail:** Monitors and records **account activity** across your AWS infrastructure, giving you control over storage, analysis, and remediation actions.

---

### **Cheat Sheet**
In the exam, when you see these **official** phrases, your brain should immediately go to the service:
*   *"Logically isolated"* $\rightarrow$ **VPC**
*   *"Decouple microservices"* $\rightarrow$ **SQS**
*   *"Event-driven compute"* $\rightarrow$ **Lambda**
*   *"Block-storage for EC2"* $\rightarrow$ **EBS**
*   *"Auditing and API calls"* $\rightarrow$ **CloudTrail**


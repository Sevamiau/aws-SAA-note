# Amazon MQ 

- SQS, SNS are "cloud native" services: proprietary protocols from AWS 
- Traditional apps running from on-premises may use open protocols such as: MQTT, AMQP, STOMP, Openwire, WSS 
- When migrating to the cloud instead of re-engineering the app to use SQS and SNS we can use Amazon MQ
- Amazon MQ is a managed message broker service for RabbitMQ and Active MQ 

- Amazon MQ does not "scale" as much as SQS / SNS 
- Amazon MQ runs on servers, can run in multi-az with failover 
- Amazon MQ has both queue fueature SQS and topic features SNS 


## Aamazon MQ - HA 


Unlike SQS or SNS (which are serverless and handle HA automatically), Amazon MQ is a managed service that runs on specific instances, so you have to choose this specific architecture if you want to avoid downtime.

### **Amazon MQ - High Availability (Active/Standby)**

*   **The Goal:** To ensure the message broker stays online even if a whole AWS Availability Zone (AZ) fails.
*   **The Components:**
    *   **Active Broker:** Located in **AZ 1a**. This is the primary server that handles all client requests and message processing.
    *   **Standby Broker:** Located in **AZ 1b**. It is "sleeping" and does not process messages while the Active broker is healthy.
    *   **Amazon EFS (Shared Storage):** This is the **most important part**. Both brokers are connected to the same EFS file system. This ensures that if the Active broker dies, the Standby broker already has access to all the stored messages.
*   **The Failover Process:**
    1.  If the Active Broker or its AZ fails, AWS automatically detects it.
    2.  The Standby Broker "wakes up" and becomes **Active**.
    3.  The **Client** (your application) automatically reconnects to the new Active broker using the failover transport URL.

---

### **Exam Summary for your notes:**

| Feature | Amazon MQ HA (Active/Standby) |
| :--- | :--- |
| **Setup Type** | Multi-AZ (Spans two Availability Zones). |
| **Shared Storage** | **Amazon EFS** (Used to sync messages between brokers). |
| **Logic** | Only **one** broker is active at a time (Failover model). |
| **Primary Goal** | **Reliability** and **High Availability** for legacy messaging. |

---

### **DevOps/Linux Comparison:**
Think of this as a **Linux Cluster (Heartbeat/Corosync)** with a **Shared Drive**. 
*   In your Fedora/KVM world, it’s like having two VMs, but only one is running the `service`. They both have the same `/var/lib/messages` folder mounted via **NFS** (EFS). If VM1 hangs, VM2 starts the service and takes over the disk.

**Why use this instead of SQS?** 
Again, only use this if you have a legacy app that *needs* ActiveMQ or RabbitMQ features. If you are building a new app, SQS is better because it doesn't require you to manage this Active/Standby complexity!


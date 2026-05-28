# AWS Global Accelerator vs Cloudfront

- They both use the AWS Global network and its edge locations around the world
- Both services integrate with AWS Shield for DDoS Protection

## **Differences**

- **Cloudfront**
    * Improves performance for both cacheable content (such as images and videos)
    * Dynamic content (such as API Acceleration and Dynamic site delivery)
    * Content is served at the edge

- **Global Accelerator**
    * Improves performance for a wide range of apps over TCP or UDP 
    * Proxying packets at the edge to applications running in one or more AWS Regions.
    * Good fit for non-HTTP use cases, such as gaming (UDP), IoT (MQTT), or voice over IP 
    * Good for HTTP use cases that require static IP Addresses
    * Good for HTTP use cases that required deterministic, fast regional failover


**CloudFront is about the CONTENT. Global Accelerator is about the NETWORK.**

---

### **1. CloudFront = The Cache (Layer 7)**
*   **Goal:** To serve files (images, video, HTML) faster by storing copies close to the user.
*   **Protocol:** Only **HTTP/HTTPS**.
*   **Key Feature:** **Caching.** It remembers the data so the origin server doesn't have to work as hard.
*   **IP Addresses:** You get a **DNS name** (e.g., `d123.cloudfront.net`). The IP addresses change all the time.

### **2. Global Accelerator = The Fast Lane (Layer 4)**
*   **Goal:** To improve network performance and provide instant failover for applications.
*   **Protocol:** **TCP or UDP** (Anything! Gaming, VoIP, IoT, HTTP).
*   **Key Feature:** **Static Anycast IPs.** You get **two fixed, permanent public IP addresses**. No matter where the user is, they hit those same two IPs, and AWS routes them over their private fiber-optic backbone to your server.
*   **Caching:** **NONE.** It does not "remember" files; it just moves packets faster.

---

### **The "Exam Duel" Comparison**

| Feature | Amazon CloudFront | AWS Global Accelerator |
| :--- | :--- | :--- |
| **Does it cache?** | **YES** | **NO** |
| **What layer?** | Layer 7 (App level) | Layer 4 (Network level) |
| **IP Addresses** | Dynamic / DNS name | **2 Static Anycast IPs** |
| **Best for...** | Static content, Video, Web. | Gaming, VoIP, Non-HTTP apps. |
| **Failover** | Based on DNS (Slow). | **Instant** (AWS-level routing). |

---

### **How to answer on the Exam:**
*   If the question mentions **"Cache," "Static Content,"** or **"S3,"** pick **CloudFront**.
*   If the question mentions **"Static IPs," "UDP," "Gaming,"** or **"Fastest Failover,"** pick **Global Accelerator**.


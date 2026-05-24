# What is CORS?

- Cross-Origin Resource Sharing (CORS)
- Origin = scheme (protocol) + host (domain) + port 
    * example: https://www.example.com (implied port is 443 for HTTPS, 80 for HTTP)
- Web Browser based mechanism to allow request to other origins while visiting the main origin 
- Same origin: http://example.com/app1 & http://example.com/app2 
- Different origins: http://www.example.com & http://other.example.com 
- The request wont be fulfilled unless the other origin allows for the requests, using CORS Headers (example: Acces-Control-Allow-Origin)



### 1. The Problem: Same-Origin Policy
By default, web browsers are paranoid. If you are visiting `website-A.com`, the browser will block that website from requesting data from `website-B.com` for security reasons. This is called the **Same-Origin Policy**.

**What defines an "Origin"?**
Three things must match exactly: **Protocol** (http vs https), **Host** (domain), and **Port**.
*   `http://my-site.com` and `https://my-site.com` are **different origins** (different protocol).
*   `http://my-site.com` and `http://api.my-site.com` are **different origins** (different subdomain).

---

### 2. The Solution: CORS
**CORS (Cross-Origin Resource Sharing)** is a way for a server (like an S3 bucket) to tell the browser: *"It's okay, I know Website A, you can let them have my data."*

#### The Real-World S3 Scenario:
1.  You host a **Static Website** in **Bucket A** (`my-web-site.s3-website...`).
2.  Your website uses Javascript to pull images or fonts from **Bucket B** (`my-data-storage.s3...`).
3.  **The Browser** stops the request and says: "Hey! These are different buckets. I'm blocking this."
4.  **The Fix:** you go to **Bucket B**, and you add a **CORS Configuration** (a small JSON file) that says: "Allow requests coming from Bucket A."

---

### 3. What the CORS Configuration looks like
```json
[
  {
    "AllowedOrigins": ["http://my-web-site.com"], 
    "AllowedMethods": ["GET", "HEAD"],
    "AllowedHeaders": ["*"]
  }
]
```
*   `AllowedOrigins`: Who is allowed to ask for data?
*   `AllowedMethods`: What can they do? (Usually just GET).

---

### 4. SAA-C03 Exam "Cheat Sheet":

| If you see this in the question... | The Answer is **CORS** |
| :--- | :--- |
| A website is hosted on S3 and needs to load **fonts** or **scripts** from another bucket. | **Enable CORS** on the source bucket. |
| You get an error: **"Cross-Origin Request Blocked"** in the browser console. | **Enable CORS** on the destination bucket. |
| A client-side Javascript app is failing to call an S3 URL. | **Enable CORS**. |

###  Crucial Exam Tip:
**CORS is NOT for server-to-server communication.** 
*   If an **EC2 instance** (server) is pulling data from S3, you use **IAM Roles**.
*   If a **Browser** (user) is pulling data from S3 while visiting another site, you use **CORS**.


(./images/WhatsApp Image 2026-05-24 at 3.46.09 PM.jpeg)

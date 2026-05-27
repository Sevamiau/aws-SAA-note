 # Amazon SNS (Simple Notification Service)

- The "event producer" only sends message to one SNS topic 
- As many "event receivers" (subscriptions) as we want to listen to the SNS topic Notifications
- Each subscriber to the topic will get all the messages (note: New features to filter messages)
- Up to 12,500,000 subscriptions per topic 
- 100,00 topics limit



*   **Definition:** A fully managed **Pub/Sub** (Publish/Subscribe) messaging service used to **push** messages to multiple subscribers.
*   **The Model:** **Push-based.** Unlike SQS (where you ask for mail), SNS "broadcasts" the message immediately to everyone "tuned in."
*   **The "Fan-out" Pattern:** One message sent to an SNS **Topic** can be delivered simultaneously to many different destinations (SQS, Lambda, Email, SMS, HTTP webhooks).
*   **Decoupling:** Allows a single event (like a "Purchase") to trigger multiple independent actions (Billing, Shipping, and Email) without the services knowing about each other.
*   **Key Limitation:** **No Persistence.** If a subscriber is not active or correctly configured when the message is sent, the message is lost (unless you use SQS as a subscriber to catch it).

**Exam Keyword:** If you see **"Broadcast"** or **"Fan-out"** to multiple receivers, the answer is **SNS**.


## SNS integrates with a lot of AWS services 

- Many AWS services can send data directly to SNS for notifications 


## SNS - How to Publish 

- Topic Publish (Using the SDK)
    * Create a topic 
    * Create a subscriptions (or many)
    * Publish to the topic 

- Direct Publish (for mobile apps SDK)
    * Create a platform app 
    * Create a platform endpoint 
    * Publish to the platform endpoint
    * Works with Google GCM, Apple APNS, Amazon ADM

## SNS - Security 

- Encryption:
    * In-flight Encryption using HTTPS API 
    * At-rest Encryption using KMS keys 
    * Client-side Encryption if the client wants to perform Encryption/decryption itself 
    
- Access Controls: IAM policies to regulate access to the SNS API 

- SNS Access Policies (Similar to S3 bucket policies)
    * Useful for cross-account access to SNS topics 
    * Useful for allowing other services (S3...) to write to an SNS topic

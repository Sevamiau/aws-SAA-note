# Introduction to Messagin in Amazon AWS 

- When we start deploying  multiple apps they will inevitably need to communicate with one another
- There are two patterns of application communication:
    * Synchronous communications (app to app)
    * Asynchronous/Event Based (app to queue to app)

- Synchronous between apps can be problematic if there are sudden spikes of traffic
- What if you need to suddenly encode 1000 videos but usually its 10?

- In that case its better to **decouple** your apps:
    * Using SQS: queue model
    * Using SNS: pub/sub model
    * Using Kinesis: real-time streaming model 

- These services can scale independently for our app 

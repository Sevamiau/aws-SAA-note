# Amazon SQS - Producing Messages

- Produced to SQS using SDK (SendMessagesAPI)
- The message is persisted in SQS until a consumer deletes it 
- Message retention: default 4 days, up to 14 days 

- Example: Send and order to be processed
    * Order id 
    * Customer ID 
    * Any attributes you want 

- SQS Standard: Unlimited throughtput 

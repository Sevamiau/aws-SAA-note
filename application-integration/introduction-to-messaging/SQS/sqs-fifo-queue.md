# Amazon SQS - FIFO Queue 

- FIFO = Firs In First Out (Ordering of messages in the Queue)
- Limited throughput: 300 msg/s without batching, 3000 msg/s with 
- Exactly-once send capability (by removing duplicates using Deduplication ID)
- Messages are processed in order by the consumer 
- Ordering by Message Group ID (all messages in the same group are ordered) - mandatory parameter 

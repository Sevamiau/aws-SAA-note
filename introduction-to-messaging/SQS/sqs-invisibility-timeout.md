# SQS Message Visibility Timeout

- After a Message is pooled by a consumer it becomes invisible to other consumers 
- By default the "message Visibility Timeout" is 30 seconds 
- That means the message has 30 seconds to be processed 
- After the message Visibility timeout is over, the message is "visible" in SQS 

 - If a message is not processed within the visibility timeout it will be processed twice 
 - A consumer could call the ChangeMEssageVisibility API to get more time 
 - If visibility timeout is high (hours) and consumer crashes, re-processing will take time 
 - If visibility timeout is too low (seconds) we may get duplicates 




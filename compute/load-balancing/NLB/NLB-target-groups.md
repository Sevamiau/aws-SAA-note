# Network Load Balancer - Target Groups

-Target groups can be EC2 instances. This means that your NBL can redirect TCP or UPD traffic to them
-You can also register IP Addresses (must be private IP's) You can send the private IP of an instance that you own, but also the private IP of a server. Both can be fronted by the same NBL
-You can have an NBL in front of an ALB (application load balancer) Thanks to the NBL you can get the fixed IP Addresses and thanks to the ALB you can have all the rules that you have around handling HTTP traffic 


Now one last thing you need to know for the exam is that the health checks performed by the network load balancer target groups are support three different kind of protocols.

They support the TCP protocol, the HTTP protocol and the HTTPS protocol.

So if your backend application supports the HTTP or HTTPS protocol, then it is definitely possible for you to define a health check on these protocols.


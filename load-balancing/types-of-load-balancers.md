# Types of load balancers on AWS

-AWS has 4 kinds of managed load balancers
-Classic Load Balancer(v1 -  old generation) - 2009 - CLB
    .HTTP, HTTPS, TCP, SSL(secure TCP)
-Application Load Balancer(v2 - new gen ) 2016 - ALB
    .HTTP, HTTPS, WebSocket
-Network Load Balancer(v2 - new gen) 2017 - NLB
    .TCP, TLS(secure TCP), UDP
-Gateway Load Balancer 2020 - GWLB
    .Operates at layer 3 (network layer) - IP Protocol

-Overall, its recommended to use the newer gen load balancers as they provide more features
-Some load balancers can be setup as internal (Private) or external (public) ELBs


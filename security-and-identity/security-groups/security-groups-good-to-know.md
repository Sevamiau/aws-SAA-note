# Security Groups good to know

-Can be attached to multiple instances
-Locked down to a region / VPC combination
-Does live 'outside' the EC2 - if traffic is blocked the EC2 instance wont see it
- -*Its good to mantain one separate Security group for SSH access*-
-If your application is not accesible (time out) then its a Security group issue
-If your application gices a 'connection refused' error, then, its an application error or its not launched
-All inbound traffic is blocked by default
-All outboudn traffic is authorized by default

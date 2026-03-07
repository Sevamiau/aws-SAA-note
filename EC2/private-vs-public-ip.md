# Private vs Public IP (IPv4) - Fundamental differences


-Public IP:
    .Public ip  means the machine can be identified on the internet (WWW)
    .Must be unique across the whole web (no two machines can have the same public IP)
    .Can be geo-located easily

-Private IP:
    .Private IP means the machine can only be identified on a private network only
    .The IP must be unique accost the private network
    .But two different private networks (two companies) can have the same private IP
    .Machines connect to WWW using an internet gateway (a proxy)
    .Only a specified range of IPs can be used as a private IP

-Elastic IP:
    .When you stop and the start an EC2 instance, it can change its public IP.
    .If you need to have a fixed public IP for your instance, you need and elastic IP
    .An Elastic IP is a public IPv4 you own as long as you dont delete it
    .You can attach it to one instance at a time
    .With an Elastic IP address you can mas the failure of an instance or software by rapidly remapping the address to another instance in your account
    .You can only have 5 elastic IP in your account (You can ask AWS to increase that)

-Overall, try to avoid using Elastic IP:
    .They often reflect poor architectural decisions
    .Instead, use a random public IP and register a DNS name to it.
    .Or, as we will see later, use a Load Balancer and dont user public IP

# Application Load Balancer Good To Know

-Fixed hostname (XXX.region.elb.amazonaws.com)
-The app servers dont see the ip of the client direclty:
    .The true ip of the client is inserted in the header X-Forwarded-for
    .We can also get port (X-Forwarded-Port) and Proto (X-Forwarded-Proto)


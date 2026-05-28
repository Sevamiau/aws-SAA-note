# SSL/TLS - Basics

-An SSL Certificate allows traffic between your clients and your load balancer to be encrypted in transit (in-flight encryption)

-SSL refers to Secure Socket Layer, used to encrypt connections
-TLS refers to Transport Layer Security, which is a newer version
-Nowadays TLS certificates are mainly used, but people still refer to them as SSL

-Public SSL certificates are issued  by Certificate Authorities (CA)
-Comodo, Symantec, GoDaddy, GlobalSign, Digicert, Letsencrypt, etc...

-SSL certificates have an expiration date (that you set) and must be renwed


## How does this work from a Load Balancer perspective?

-The load balancer uses an X.509 certificate (SSL/TLS server certificate)
-You can manage certificates using ACM (AWS Certificate Manager)
-You can create upload your own certificates alternatively
-HTTPS listener:
    .You must specify a default certificate   
    .You can add an optional list of certs to support multiple domains
    .Clients can use SNI (Server Name Indication) to specify the hostname they reach 
    .Ability to specify a Security policy to support older versions of SSL/TLS (legacy clients)

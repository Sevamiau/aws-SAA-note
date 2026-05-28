# SSL - Server Name Indication

*With SNI you are able to have multiple target groups for diferent websites using diferents SSL certificates *

-SNI solves the problem of loading multimple SSL certificates onto one web server  (to serve multiple websites)
-It's a "newer" protocol and requires the client to indicate the hostname of the target server in the initial SSL handshake
-The server will then find the correct certificate or return the default one

-Note: 
      .Only work for ALB and NLB (newer gen) and cloudfront
      .Does not work for CLB (older gen)


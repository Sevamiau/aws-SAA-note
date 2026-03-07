# Application Load Balancer (v2)

-Application Load Balancers is Layer 7 (HTTP)

-Load Balancing to multiple HTTP apps across machines (target groups)
-Load Balancing to multiple apps on the same machine (ex:Containers)
-Support for HTTP/2 and WebSocket
-Support redirects (from HTTP to HTTPS for example)

-Routing tables to different target groups:

    .Routing base on path in URL (example.com/users & example.com/posts) 
    .Routing base on hostname in URL (one.example.com & other.example.com)
    .Routing base on Query strings, Headers (example.com/users?id=1234&order=false)

-ALB are great fit for micro services & container-based apps (example: Docker & Amazon ECS)
-Has a port mapping feature to redirect to a dynamic port in ECS
-In comparison, we'd need multiple classic load Balancer per app 


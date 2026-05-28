# Sticky Sessions (Session Affinity)

Sticky Sessions (also known as Session Affinity) is a feature that allows a load balancer to "bind" a user's session to a specific backend server.

-It is possible to implement stickiness so that the same client is redirected to the same instance behind a load balancer 
-This works for Classic load balancer, Application load balancer and Network load balancer.
-The "cookie" used for stickiness has an expiration date you control
-Use case: Make sure the user doesn't lose his session data 
-Enabling stickiness may bring imbalance to the load over the backend EC2 instances 

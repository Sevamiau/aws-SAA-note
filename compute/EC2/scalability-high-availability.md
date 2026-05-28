# Scalability and High Availability



-Scalability mean that an app/system can handle greater load by adapting
-There are two kinds of Scalability: 
    .Vertical Scalability
    .Horizontal Scalability(Elasticity)

-Scalability is linked but different to High Availability


## Vertical Scalability

-Vertical scaling: Increase size (scale up,down)
    

-Vertical Scalability means increasing the size of the instance
-For example, your app runs in a t2.micro. Scaling that app Vertically means running it on a t2.large
-Vertical Scalability is very common for non distributed systems, such as databases
-RDS, ElastiCache are services that can scale vertically 
-Theres usually a limit to how much you can vertically scale (hardware limit)

## Horizontal Scalability

-Horizontal scaling: Increase the number of instances (scale up/down)


-Horizontal Scalability means increasing the number of instances/systems for your app
-Horizontal scaling implies distributed systems.
-This is very common for web apps/modern apps.

-Its easy to horizontally scale thanks to the cloud offering such as Amazon EC2

## High Availability

-High Availability: Run instances for the same app across multiple AZ

-high Availability usually goes hand in hand with horizontal scaling 
-High Availability means running your app/system in at least 2 data centers, this means to run this app in different Availability Zones AZ 
-The goal of high Availability is to survive a data center loss

-The high Availability can be passive (For RDS multi AZ for example)
-The high Availability can be active (For horizontal scaling)




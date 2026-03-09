# Elastic Load Balancers - SSL certificates

-Classic Load Balancers (v1):
      .Support only one SSL certificates
      .Must use multiple CLB for multiple hostname with multiple SSL certificates

-Application Load Balancers:
      .Supports multiple listeners with multiple SSL certificates
      .Uses Server Name Indication (SNI) to make it work

-Network Load Balancer:
      .Supports multiple listeners with multiple SSL certificates
      .Uses Server Name Indication (SNI) to make it work

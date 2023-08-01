# Load Balancer

## Classic LB

Classic load balancers support both IPv4 and IPv6. They support HTTP/1 and HTTP/1.1, but only application load balancers support HTTP/2. Further, you must register individual instances, rather than target groups, with classic load balancers; registering target groups is a functionality only available with application load balancers.


An ELB is an elastic load balancer and generally refers to a classic load balancer. An ALB is an application load balancer.

Classic load balancers operate at both the connection (Level 4) and the request (Level 7) layer of the TCP stack.


## Application LB

An ALB offers SSL termination and makes the SSL offload process very simple through tight integration with SSL processes. While an ELB will handle SSL termination, it does not offer the management features that ALBs do.



## Network LB

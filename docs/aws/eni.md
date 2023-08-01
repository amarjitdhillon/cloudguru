An `Elastic Network Interface (ENI)` is virtual and can have:

- multiple IPv4 and IPv6 addresses
- security groups
- a MAC address
- a `source/destination check` flag.

  
!!! tip

    - Traffic follows the network interface rather than sticking to any particular instance. So in the case when ENI is moved from one instance to another, the traffic is redirected to the new instance but stays targeted at the elastic network interface  
    - An elastic network interface can only be attached to a single instance at one time but can be moved from one instance to another.
    - ==We can attach multiple elastic network interfaces to an instance==
    - An instance’s primary ENI cannot be detached.


# Virtual Network

- VNet enables many types of Azure resources, such as Azure Virtual Machines (VM), to securely communicate with each other, isolation.

- Virtual networks and subnets span all availability zones in a region. You don't need to divide them by availability zones to accommodate zonal resources


!!! warning "Default communication to Internet"
    All resources in a VNet can communicate outbound to the internet, by default. You can communicate inbound to a resource by assigning a public IP address or a public Load Balancer.


## VNET peering

`Virtual network peering` enables you to seamlessly connect two or more `Virtual Networks` in Azure. The virtual networks appear as one for connectivity purposes. The traffic between virtual machines in peered virtual networks uses the Microsoft backbone infrastructure. ==Like traffic between virtual machines in the same network, traffic is routed through Microsoft's private network only.==

Azure supports the following types of peering:

1. `Virtual network peering`: Connecting virtual networks within the same Azure region.
2. `Global virtual network peering`: Connecting virtual networks across Azure regions.



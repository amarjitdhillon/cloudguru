# VPN gateways
A VPN gateway is a type of virtual network gateway. Azure VPN Gateway instances are deployed in a dedicated subnet of the virtual network and enable the following connectivity:

- Connect on-premises datacenters to virtual networks through a `site-to-site` connection.
- Connect individual devices to virtual networks through a `point-to-site` connection.
- Connect virtual networks to other virtual networks through a `network-to-network` connection.

!!! question "How many VPN's can be deployed?"
    You can deploy only one VPN gateway in each virtual network. However, you can use one gateway to connect to multiple locations, which includes other virtual networks or on-premises datacenters.


## Types of VPM GW

There are 2 types of VPN gateways:

1. `Policy-based VPN gateways`: They specify statically the IP address of packets that should be encrypted through each tunnel. This type of device evaluates every data packet against those sets of IP addresses to choose the tunnel where that packet is going to be sent through.

2. `Route-based gateways`: IPSec tunnels are modeled as a network interface or virtual tunnel interface. IP routing (either static routes or dynamic routing protocols) decides which one of these tunnel interfaces to use when sending each packet. Route-based VPNs are the preferred connection method for on-premises devices. They're more resilient to topology changes such as the creation of new subnets.
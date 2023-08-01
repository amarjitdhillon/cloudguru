

## Region
Each Azure region features datacenters deployed within a latency-defined perimeter. They're connected through a dedicated regional low-latency network. 

## Region pairs
Most Azure regions are paired with another region within the same geography (such as US, Europe, or Asia) at least 300 miles away. For example, if a region in a pair was affected by a natural disaster, services would automatically fail over to the other region in its region pair.

## Sovereign Regions
In addition to `regular regions`, Azure also has `sovereign regions`. Sovereign regions are instances of Azure that are isolated from the main instance of Azure. You may need to use a sovereign region for compliance or legal purposes.

## AZ
Azure az's are physically separate locations within each Azure region that are tolerant to local failures.

!!! remember ""
    - To ensure resiliency, a minimum of three separate availability zones are present in all `AZ-enabled regions`.
    - AZ's are connected by a high-performance network with a round-trip latency of less than `2ms`. 
    - AZ's are designed so that if one zone is affected, then services are supported by the remaining 2 zones.

## Resource groups
Resource groups are simply groupings of resources. When you create a resource, you’re required to place it into a `resource group`. While a resource group can contain many resources, a single resource can only be in one resource group at a time. 

!!! note
    Some resources may be moved between resource groups, but when you move a resource to a new group, it will no longer be associated with the former group. Additionally, resource groups can't be nested, meaning you can’t put resource group B inside of resource group A.

### Benefit of using RG

When you `apply an action` to a resource group, that action will apply to all the resources within the resource group. If you `delete a resource group`, all the resources will be deleted. If you `grant` or `deny access` to a resource group, you’ve granted or denied access to all the resources within the resource group.

## Azure Subscription
In Azure, subscriptions are a unit of management, billing, and scale. Similar to how resource groups are a way to logically organize resources, subscriptions allow you to logically organize your resource groups and facilitate billing.

An account can have multiple subscriptions, but it’s only required to have one. In a multi-subscription account, you can use the subscriptions to configure different billing models and apply different access-management policies.

## Management groups

### Wny do we need it?
If you have many subscriptions, you might need a way to efficiently manage access, policies, and compliance for those subscriptions.

### Solution
Azure management groups provide a level of scope above subscriptions. You organize subscriptions into containers called management groups and apply governance conditions to the management groups. All subscriptions within a management group automatically inherit the conditions applied to the management group, the same way that resource groups inherit settings from subscriptions and resources inherit from resource groups.


## Virtual machine scale sets

Virtual machine scale sets let you create and manage a group of identical, load-balanced VMs.  Scale sets allow you to centrally manage, configure, and update a large number of VMs in minutes. The number of VM instances can automatically increase or decrease in response to demand, or you can set it to scale based on a defined schedule.

!!! tip
    Virtual machine scale sets also automatically deploy a load balancer to make sure that your resources are being used efficiently

## Azure Container Instances
Azure Container Instances offer the fastest and simplest way to run a container in Azure; without having to manage any virtual machines or adopt any additional services. Azure Container Instances are a `platform as a service (PaaS)` offering. Azure Container Instances allow you to upload your containers and then the service will run the containers for you.

## Azure Functions
Azure Functions is an event-driven, serverless compute option that doesn’t require maintaining virtual machines or containers. If you build an app using VMs or containers, those resources have to be “running” in order for your app to function. With Azure Functions, an event wakes the function, alleviating the need to keep resources provisioned when there are no events.

Azure Functions runs your code when it's triggered and automatically deallocates resources when the function is finished. In this model, you're only charged for the CPU time used while your function runs.

!!! remember
    Functions can be either stateless or stateful. When they're stateless (the default), they behave as if they're restarted every time they respond to an event. When they're stateful (called Durable Functions), a context is passed through the function to track prior activity.

## Connecting with On-Premise 

### ExpressRoute
An `ExpressRoute` instance is the only connection between an `Azure VNet` and an `on-premise network` that does not cross into the internet. The connection is private and managed directly by an `ExpressRoute partner`.

Azure ExpressRoute lets you extend your `on-premises` networks into the Microsoft cloud over a private connection, with the help of a `connectivity provider`. This connection is called an `ExpressRoute Circuit`. With ExpressRoute, you can establish connections to Microsoft cloud services, such as Microsoft Azure and Microsoft 365. This allows you to connect offices, datacenters, or other facilities to the Microsoft cloud. Each location would have its own ExpressRoute circuit.

!!! question "How does Expressroute work on high level?"
    ExpressRoute uses the `BGP`. BGP is used to exchange routes between on-premises networks and resources running in Azure. This protocol enables dynamic routing between your on-premises network and services running in the Microsoft cloud.


### Point-to-Site Connection (VPN) 
A point-to-site (P2S) connection, on the other hand, is an inexpensive solution for connecting any supported Azure resource to one existing in another network.

### Site-to-Site Connection (VPN) 
Unlike P2S, traffic passing through a `site-to-site (S2S)` connection is sent within an `encrypted tunnel` across the internet. 

!!! info ""
    The primary difference is that the connectivity happens between Azure VPN Gateway and an on-premise VPN device.

## NSG and ASG
NSG's (Network Security Group) & ASG's (Application Security Group) are the main Azure Resources that are used to administrate and control network traffic within a virtual network (vNET).


### Network Security Group (NSG)

NSG's control access by permitting or denying network traffic in a number of ways, whether it be:-

1. Communication between different workloads on a vNET
2. Network connectivity from on-site environment into Azure
3. Direct internet connection

Theoretically speaking, it is just a group of Access Control List rules that either allow or deny network traffic to a specific destination located on your vNET. 

!!! remember
    NSG's can be applied either on a virtual machine or subnet (one NSG can be applied to multiple subnets or virtual machines


### Application Security Group

An ASG provides the ability to group a set of Azure VMs and define NSGs specifically for that group. An application security group is a logical collection of virtual machines (NICs). You join virtual machines to the application security group, and then use the application security group as a source or destination in NSG rules.

!!! remember
    A Virtual Machine can be attached to more than one Application Security Group. This helps in cases of multi-application servers.

<center> <img src="../images/amardhillon_diagrams-asg.drawio.png" width="100%"> </center>

==As per the rules defined in NSG, the WebServer and AppServer ASG are able to communicate with one another while the  WebServer and DbServer ASG are not.==

!!! tldr
    `Application Security Groups` helps to manage the security of Virtual Machines by grouping them according the applications that runs on them. It is a feature that allows the application-centric use of Network Security Groups.

ASG allow us to define fine-grained network security policies based on applications instead of explicit IP addresses.

!!! info "Using alias/monikers"
    We can define ASG by providing a alias/moniker that fits our needs.

!!! warning "NSGs and ASGs are not omnipresent"
    When NSGs and ASGs are discussed by IT professionals working with Azure, those conversations generally occur within the context of Azure resources such as Azure VNets and Azure VMs. This is because you cannot currently configure NSGs or ASGs for Azure resources that exist outside of a VNet. There are no Azure-wide capabilities to configure NSGs or ASGs for Azure App Service, Azure Storage, or Azure Event Hub


## Networking

### Home address

!!! question "What is special about `127.0.0.1` ?"
    The `127.0.0.1` IPv4 address is commonly referred to as a `loopback address`. The IP address is typically mapped to the host name `localhost` and can be referred to as home in networking. This is useful when accessing a website hosted on the machine that you are currently logged into. For example, `http://localhost` accesses a website hosted on the currently logged into machine. The IPv6 address for localhost is `::1`

### NAT

AT simplifies outbound Internet connectivity for virtual networks. When configured on a subnet, all outbound connectivity uses the Virtual Network NAT's static public IP addresses.

!!! example 
    As shown in the below diagram the address for VMs in the VNET are `10.0.0.*`. As we know that this address are not accessible on the internet (they are private). A NAT translates the `private IP address` into a `public IP address`. In other words, the NAT device has both a `private IP` address as well as a `public IP` 

    <center> <img src="../images/amardhillon_diagrams-nat.drawio.png" width="90%"> </center>

    How does the router know the response from browser that has the destination address that is now 155.35.25.26 needs to be directed to `10.0.0.4`? The answer is found by digging into a socket.

    A `socket` is the combination of an `IP address:port number`. More specifically, it has a source IP address, source port, destination IP address, and destination port    

## Network Peering

Peering allows two virtual networks to connect directly to each other. Network traffic between peered networks is private, and travels on the Microsoft backbone network, never entering the public internet. Peering enables resources in each virtual network to communicate with each other. These virtual networks can be in separate regions, which allows you to create a global interconnected network through Azure.

### UDR

User-defined routes (UDR) allow you to control the routing tables between subnets within a virtual network or between virtual networks. This allows for greater control over network traffic flow.




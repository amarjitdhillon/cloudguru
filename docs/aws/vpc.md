# VPC

## Elements in VPC


### Elastic network interface 
 
 It is a logical networking component in a VPC that represents a virtual network card.

### Subnet 
 A range of IP addresses in your VPC. You can add AWS resources to a specified subnet. Use a public subnet for resources that must connect to the internet, and a private subnet for resources that don't connect to the internet.

### Security group 
  We can use security groups to control access to the AWS resources in each subnet.

### Access control list (ACL)
It uses a network ACL to provide additional security in a subnet. The default subnet ACL allows all inbound and outbound traffic.

- A subnet can only be associated with a single NACL at a time.
- NACL rules have
    -  rule number,
    -  protocol,
    -  choice of ALLOW or DENY,
    -  CIDR range 
    -  port or port range for inbound and outbound traffic.

### Route table 
-  contains a set of routes that AWS uses to direct the network traffic for your VPC. You can explicitly associate a subnet with a particular route table. 

!!! remember
    By default, the subnet is associated with the main route table.

### Route

Each route in a `route table` specifies a range of IP addresses and the destination where Lambda sends the traffic for that range. The route also specifies a target, which is the gateway, network interface, or connection through which to send the traffic.

### NAT gateway

 An AWS Network Address Translation (NAT) service that controls access from a private VPC private subnet to the Internet.

### **VPC endpoints**

You can use an Amazon VPC endpoint to create private connectivity to services hosted in AWS, without requiring access over the internet or through a NAT device, VPN connection, or AWS Direct Connect connection.


## Notes

- NACL applies to all instances in an associated subnet.
- NACLs are always evaluated first because they exist at the border of a subnet. As security groups are attached to instances, they are not processed until traffic passes through the NACL and into the instance’s subnet.
- NACLs are associated with subnets, not VPC.
- Each rule in an NACL has a number, and those rules are evaluated using those numbers, moving from low to high.
- Each subnet in your VPC must be associated with an NACL.
- An NACL is associated with a subnet, not an instance or VPC. It can be associated with a single subnet or multiple subnets.
- A VPC spans all the availability zones in a region.
- You must always select a region to create a VPC, and you must always provide a CIDR block. VPCs span all the AZs in a region, so that is not required.
- While you can add secondary IPv4 CIDR blocks, you cannot add additional CIDR blocks for IPv6 at this time.
- When creating a VPC, you can specify an option name (no description needed), a required IPv4 CIDR block, and an optional IPv6 CIDR block.
- A VPN-only subnet routes traffic through a virtual private gateway rather than an internet gateway
- At a minimum, a VPC-only subnet must have a routing table routing traffic and a virtual private gateway to which traffic is routed.
- You can only create 5 VPCs per region by default. Creating more requires a request to AWS.
- You can create 200 subnets per VPC.
- You’re allowed 5 elastic IP addresses per region unless you have the default limits raised by AWS.
- A security group denies all traffic unless explicitly allowed. This means it functions as a whitelist.
- A VPC endpoint is a connection to an AWS service and explicitly does not use internet gateways or VPN connections.
- `Bastion hosts` should be in a public subnet so that they can be accessed via the public Internet. They can then route traffic into a private subnet.
- `Bastion hosts` are also sometimes called jump servers because they allow a connection to “jump” to the bastion and then into a private subnet.
- Internet gateways scale horizontally, not vertically. They are also redundant and highly available automatically.
- Default VPC has an internet gateway automatically attached.
- Load Balancers
    - Application load balancers operate at the Application layer, which is layer 7 of the OSI model. 
    - ELBs (classic load balancers) operate at the Transport layer, layer 4, as well as layer 7.
    - Network load balancers operate at layer 4 as well
- A NAT device—network address translation—provides routing for instances to an internet gateway but can prevent undesired inbound traffic.
- A site-to-site connection is going to require a private subnet on the AWS side with private instances within it.
- An `egress-only gateway` is for use with IPv6 traffic and only allows outbound traffic. They are stateful.
- The default VPC has an internet gateway attached by default while custom VPC do not
- The default VPC has a CIDR block of /16, but the default subnet in each AZ is a /20.
- Default VPC does get a subnet automatically (as well as an internet gateway).
- While the default VPC automatically creates a subnet, while custom VPCs do not create a subnet. 
- With custom VPC, You do automatically get a security group, route table, and NACL.
- A VPC endpoint can connect to S3 and DynamoDB, as well as a host of additional AWS services. It does not require an internet gateway or a VPN connection and does not route traffic over the public Internet.
- A VPC endpoint is a virtual device that provides redundancy via AWS (and automatically).
- A VPC endpoint provides a connection over the Amazon network between your VPC and service, such as S3. This avoids leaving the network and routing over the public Internet, which inherently provides greater security for the traffic involved
- VPCs can peer with other VPCs, in the same account or different ones


### VPC flow logs

VPC flow logs: We can use them for troubleshooting to see if there is some attack on the VPC. Also, they can let us know why the communication between the VPC’s is not working out.

VPC Flow Logs is a feature that enables you to capture information about the IP traffic going to and from network interfaces in your VPC.

You can create a flow log for a VPC, a subnet, or a network interface. If you create a flow log for a subnet or VPC, each network interface in that subnet or VPC is monitored.
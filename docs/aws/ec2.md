
- EC2 instances, as well as ECS containers, can both be scaled up and down by - Auto Scaling
- A launch configuration contains an AMI ID, key pair, instance type, security - groups, and possibly a block device mapping.
- There are a number of valid scaling policies for Auto Scaling:
    - `Maintain current instance levels`: use to ensure that a specific number of - instances is running at all times.
    - `Manual scaling`: Manual scaling allows you to specify a minimum and a maximum - number of instances as well as the desired capacity. The Auto Scaling policy - then handles maintaining that capacity.
    - `Schedule-based scaling`: 
    - `Demand-based scaling`: Demand-based scaling allows you to specify parameters to - control scaling. One of those parameters can be CPU utilization
- InService and Standby are valid states for an instance in an auto-scaling group.
- You have to create a launch configuration first, then an Auto Scaling group, - and then you can verify your configuration and group.   
- A `launch configuration` needs a single AMI ID to use for all instances it - launches.
- Default security groups prevent all incoming traffic and allow all traffic out - whereas the new SG allows all the outgoing traffic and blocks all the incoming - traffic.
- It is generally better to allow AWS to handle encryption in cases where you - want to ensure all encryption is the same across a data store.
- A bastion host is a publicly accessible host that allows traffic to connect to - it. Then, an additional connection is made from the bastion host into a private - subnet and the hosts within that subnet.
- The security of the bastion must be different from the hosts in the private - subnet. The bastion host should be hardened significantly as it is public, but - also accessible; this is in many ways the opposite of the security requirements - of hosts within a private subnet.
- For private subnet instances, you need a route out to a NAT gateway, and that - NAT gateway must be in a public subnet—otherwise, it would not itself be able - to provide outbound traffic access to the Internet.
- NAT gateway is essentially a managed service and a NAT instance as an instance (- which you manage) for networking.
- all custom NACLs disallow all inbound and outbound traffic. It is only a VPC’s - default NACL that has an “allow all” policy.
- Security groups only contain allow rules, not deny rules.
- A security group can actually have no inbound or outbound rules.
- A security group does require a name and description, though.
- A security group can be attached to multiple constructs, like an EC2 instance, - but is ultimately associated with a network interface, which in turn is - attached to individual instances.
- by default SG has 
    - Outbound   `0.0.0.0/0` for all protocols allowed for IPV4
    - Outbound `::/0` for all protocols allowed for IPV6
- Security group rules have a protocol and a description. They do not have a - subnet, although they can have CIDR blocks or single IP addresses. Instances - can associate with a security group, but a security group does not itself refer - to a specific instance.
- Client-side encryption involves the client (you, in this example) managing the - entire encryption and decryption process. AWS only provides storage.
- SSE-S3, SSE-KMS, and SSE-C are all valid approaches to server-side S3 - encryption.
- SSE-KMS provides a very good audit trail and security.
- SSE-S3 requires that Amazon S3 manage the data and master encryption keys while - SSE-KMS requires that AWS manage the data key but you manage the customer - master key (CMK) in AWS KMS.
- An instance has a primary network interface in all cases but can have - additional network interfaces attached.
- You can only assign a single role to an instance.
- By default, root volumes are terminated on instance deletion, and by default, additional EBS volumes attached to an instance are not.

## Boot volumes

This is easiest to remember by noting that HDD types are not available to use as boot volumes. General SSD and Provisioned IOPS are.
 

## EC2 Placement groups
When you launch a new EC2 instance, the EC2 service attempts to place the instance in such a way that all of your instances are spread out across underlying hardware to minimize correlated failures. You can use placement groups to influence the placement of a group of interdependent instances to meet the needs of your workload. Depending on the type of workload, you can create a placement group using one of the following placement strategies:

`Cluster`: It means placing the instances in the same rack and AZ so that there is low latency and high throughput. It packs instances close together inside an Availability Zone. This strategy enables workloads to achieve the low-latency network performance necessary for tightly-coupled node-to-node communication that is typical of HPC applications.

`Spread`: A spread placement group is a group of instances that are each placed on distinct racks, with each rack having its own network and power source. The following image shows seven instances in a single Availability Zone that are placed into a spread placement group. The seven instances are placed on seven different racks. Spread placement groups are recommended for applications that have a small number of critical instances that should be kept separate from each other.
            
`Partition`: Same as Spread but with a difference that in this, we can have multiple instances in the same partition. In this case, the different racks have a different power source. Use case: HDFS, Cassandra, etc.


Partition placement groups help reduce the likelihood of correlated hardware failures for your application. When using partition placement groups, Amazon EC2 divides each group into logical segments called partitions. Amazon EC2 ensures that each partition within a placement group has its own set of racks. Each rack has its own network and power source. No two partitions within a placement group share the same racks, allowing you to isolate the impact of a hardware failure within your application.

The following image is a simple visual representation of a partition placement group in a single Availability Zone. It shows instances that are placed into a partition placement group with three partitions—Partition 1, Partition 2, and Partition 3. Each partition comprises multiple instances. The instances in a partition do not share racks with the instances in the other partitions, allowing you to contain the impact of a single hardware failure to only the associated partition.



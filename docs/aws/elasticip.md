# Elastic IP


An Elastic IP address is a static and public IPv4 address designed for dynamic cloud computing. An Elastic IP address is associated with your AWS account. With an Elastic IP address, you can mask the failure of an instance or software by rapidly remapping the address to another instance in your account.



An Elastic IP address is a reserved public IP address that you can assign to any EC2 instance in a particular region until you choose to release it. 

When you associate an Elastic IP address with an instance or its primary network interface, the instance's public IPv4 address (if it had one) is released back into Amazon's pool of public IPv4 addresses. You cannot reuse a public IPv4 address, and you cannot convert a public IPv4 address to an Elastic IP address.

When you associate an Elastic IP address with an instance that previously had a public IPv4 address, the public DNS hostname of the instance changes to match the Elastic IP address.


To use an elastic IP, you must:

- Allocate it for use in a VPC.
- Associate it with an instance in that VPC.

!!! success "Remember"
    - By default, all AWS accounts are limited to 5 Elastic IP addresses per Region, because public (IPv4) internet addresses are a scarce public resource.
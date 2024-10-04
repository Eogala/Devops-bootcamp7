# AWS VPC Project
## What is a VPC?
A VPC (Virtual Private Cloud) in AWS (Amazon Web Services) is a service that allows you to launch AWS resources in a logically isolated virtual network that you define. Here are the key components and features of an AWS VPC:

Subnets: A VPC can be divided into multiple subnets, which are sections of the VPC IP address range where you can place groups of isolated resources. Subnets can be either public (with access to the internet) or private (isolated from the internet).

IP Addressing: You can choose your own IP address range for the VPC using IPv4 or IPv6 addresses.

Route Tables: Control the routing of network traffic within the VPC and between subnets. You can create custom route tables to direct traffic as needed.

Internet Gateway: A VPC component that allows communication between instances in your VPC and the internet. You need to attach an Internet Gateway to a VPC to enable internet access for your instances.

NAT Gateway and NAT Instances: These allow instances in a private subnet to connect to the internet or other AWS services without exposing themselves to incoming traffic from the internet.

Security Groups: Act as virtual firewalls for your instances to control inbound and outbound traffic at the instance level.

Network ACLs (Access Control Lists): Provide an additional layer of security, controlling traffic at the subnet level.

VPC Peering: Allows you to connect one VPC with another VPC to route traffic between them using private IP addresses.

VPN Gateway: Enables you to establish a secure connection between your VPC and your on-premises network.

VPC Endpoints: Allow you to privately connect your VPC to supported AWS services and VPC endpoint services powered by AWS PrivateLink without requiring an Internet Gateway, NAT device, VPN connection, or AWS Direct Connect connection.

AWS Direct Connect: Provides a dedicated network connection from your premises to AWS, enhancing security and reducing network costs.
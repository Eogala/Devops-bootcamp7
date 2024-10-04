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

Understand VPC Requirements
As a DevOps engineer, you need to understand the VPC requirements by asking questions to the relevant teams.

When working in real projects, following are some of the important questions that will help you understand the VPC requirements better.

Identifying Your Hosting Needs: What do you want to host?
Meeting Compliance Standards: What are its compliance requirements?
Handling Sensitive Information: Does it have applications dealing with PCI/PII data?
Public vs. Private Accessibility: Are the applications internet-facing?
Connecting to On-Premise Systems: Does the VPC require a Hybrid connectivity to an on-premise environment? If yes, is it DNS or IP-based connectivity?
User Accessibility to VPC Services: How are users going to connect to the services hosted in VPC?
VPC to VPC Connectivity: Does it need access to services hosted on other VPCs that are part of organizations network? It is always best to document these requirements.
Note: Organizations typically keep a questionnaire to understand the VPC requirements from network, security, and compliance perspectives.

VPC Network Design
Ideally in most organizations the VPC is created and managed by a dedicated Network team. However, devops engineers working with the application team need to come up with the VPC requirements that can host all the required applications.

How to choose CIDR for VPC?
The CIDR block for a VPC depends on the number of servers we plan to deploy in a VPC. This includes both self-hosted and AWS-managed services

We not only consider the immediate requirements but also the future expansion. We might start with a total of 15 servers now and in the future, it might grow to 1000+ servers.

So for our requirement, 10.0.0.0/20 CIDR is more than enough. Which would give you 4,096 usable IP addresses. We also need to factor on subnets in different availability zones.

However, for the project, we will choose the 10.0.0.0/16 CIDR range for our VPC. This will allow you up to 65,536 private IP addresses and it will make the subnetting easier.

Note: In actual project environments, VPC ranges are decided only based the requirements. Typically, the Application/DevOps/Network team will have a discussion and decide on the required ranges so that over/under allocation doesn’t happen

Avoiding IP Address Conflicts
Let’s take a scenario where 10.0.0.0/16 range is already allocated to a project in an on-prem environment. Even if there is no hybrid cloud connectivity to on-prem, we should not re-use 10.0.0.0/16 for VPC. Because in the future, if hybrid connectivity is set up, it could lead to IP conflicts.

Network teams in organizations ensure there are no IP range conflicts by keeping track of private IP addresses reserved for projects. This way, there won’t be any IP conflicts. Typically they use IP Address Management (IPAM) tools to track IP address allocation. These tools provide a centralized view of the IP address space used within the organization.

The following image shows an example dashboard of an open-source IPAM tool called Netbox.

Note: If you use AWS Private NAT gateway you can avoid IP conflicts even if two VPCs have the same CIDR ranges.

Subnet Design
Based on our application architecture and components we would need the following public and private subnets.

Public Subnets (Public): To deploy Load balancers for the Java app autoscaling group
Application Subnets (Private): To deploy the Java app autoscaling group
Database Subnets (Private): To deploy the RDS MYSQL instance
Management Subnets (Private): To deploy CI/CD tools and platform tools.
Platform Tools Subnets (Private): To deploy and manage all the platform tools.
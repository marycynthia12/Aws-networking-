AWS Networking Project

In this project, I created a secure cloud networking environment using services from Amazon Web Services. My goal was to design a virtual Private Cloud (VPC) with public and private subnets across multiple availability zones, configure a NAT Gateway for private internet access, and implement security controls using Security Groups and Network ACLs.

This project demonstrates basic networking architecture using Amazon VPC and compute resources from Amazon EC2.

Objectives

In this project I:

Created a Virtual Private Cloud (VPC)
Configured public and private subnets across different availability zones
 Set up a NAT Gateway to allow private instances access the internet
Implemented Security Groups
Configured Network Access Control Lists (NACLs)
 Tested internet connectivity from a private subnet
Documented the architecture and configuration

 Step 1: Creating the Virtual Private Cloud (VPC)

I began by creating a Virtual Private Cloud to isolate my cloud resources.

Steps I followed:

1. I logged into the AWS Management Console.
2. I navigated to the VPC Dashboard.
3. I clicked Create VPC
4. I selected VPC only
5. I configured the following settings:

Name: mary-vpc
IPv4 CIDR block: 10.1.0.0/24
Tenancy: Default


This CIDR block provided enough IP addresses to create multiple subnets inside the VPC.

After creating the VPC, it became the network environment for all resources in this project.

 Step 2: Creating Subnets in Different Availability Zones

Next, I created both public and private subnets across multiple availability zones for high availability.

 Public Subnets

I created two public subnets

Public subnets allow resources like bastion hosts or NAT Gateways to connect to the internet.

Private Subnets

I also created two private subnets

These private subnets host instances that should not be directly accessible from the internet.

 Step 3: Creating and Attaching an Internet Gateway

To allow internet access for public resources, I created an Internet Gateway

Steps I followed:

1. I navigated to Internet Gateways in the VPC dashboard.
2. I clicked Create Internet Gateway.
3. I named it:
mary-igw
4. I attached the Internet Gateway to my VPC.

This gateway allows communication between the VPC and the public internet.

Step 4: Configuring Route Tables

I created route tables to control how traffic flows between subnets and the internet.

 Public Route Table

I created a route table for the public subnets and added the following route:

Destination: 0.0.0.0/0
Target: Internet Gateway

I then associated this route table with both public subnets.

This allowed resources in the public subnet to access the internet directly.

Step 5: Creating a NAT Gateway

Since instances in private subnets cannot access the internet directly, I created a NAT Gateway.

Steps I followed:

1. I navigated to NAT Gateways in the VPC dashboard.
2. I clicked Create NAT Gateway.
3. I configured the following:

Subnet: Public Subnet
Elastic IP: Allocate new Elastic IP
Name: mary-nat

The NAT Gateway enables instances in private subnets to access the internet for updates or downloads while remaining private.

Step 6: Configuring Private Route Table

Next, I created a route table for the private subnets.

I added the following route:

Destination: 0.0.0.0/0
Target: NAT Gateway

Then I associated this route table with both private subnets.

This configuration ensures that outbound internet traffic from private instances passes through the NAT Gateway.

 Step 7: Implementing Security Groups

I created a security group to control inbound and outbound traffic to EC2 instances.

Configuration:

Security Group Name: mary-sg

Inbound Rules:

SSH (22) – My IP
HTTP (80) – Anywhere

Outbound Rules:

Allow all traffic

Security groups act as virtual firewalls at the instance level.

Step 8: Implementing Network Access Control Lists (NACL)

I also configured a Network ACL to control subnet-level traffic.

Inbound Rules:

Allow HTTP (Port 80)
Allow SSH (Port 22)

Outbound Rules:

Allow All Traffic

Unlike security groups, NACLs operate at the subnet level, adding an extra layer of security.

Step 9: Testing the NAT Gateway

To confirm that the NAT Gateway works correctly, I tested internet connectivity from a private subnet.

Steps I followed:

1. I launched an EC2 instance inside the private subnet.
2. I ensured the instance had no public IP address.
3. I connected to the instance 
4. It  connected and showed where I can run command


In this project, I successfully built a secure networking environment in AWS by designing a VPC architecture with both public and private subnets. I configured a NAT Gateway to allow controlled internet access for private instances and implemented security mechanisms using Security Groups and Network ACLs.

This project helped me understand core AWS networking concepts such as routing, subnet design, internet gateways, NAT gateways, and traffic control mechanisms.

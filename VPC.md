# VPC

## What is a VPC?

VPC stands for Virtual Private Cloud and it is an AWS service that allows a user to lauch AWS resources into a user-defined virtual network.

![VPC](https://user-images.githubusercontent.com/99980305/187666002-3d0c8d95-2731-4f7d-88ed-316e36850242.jpeg)

## VPC Features

### Subnets

- Range of IP addresses within a VPC
- Subnets reside in a single Availability Zone
- After subnets added, AWS resources can be deployed in a VPC

### Route Tables

- Used to determine where network traffic, from the gateway, is to be directed 

### Gateways

- Allows the connection of a VPC to another network

### Internet Gateway

- Allows the connection of a VPC to the internet

### Endpoint

- Allows private connection of a VPC to AWS services

### CIDR

- Stands for Classless Inter-Domain Routing
- A CIDR block is an IP address range
- Method of assigning IP addresses
- VPC can have two CIDR blocks- IPv4 and IPv6

## NACL vs Security Group

### What is an NACL?

- NACL stands for Network Access Control List
- Controls traffic to and from a subnet with a set of inbound and outbound rules
- Represents network level security
- Each subnet is to be associated with one NACL
- One NACL can be associated with multiple subnets

### Use case for NACL

- Inbound rule can deny incoming traffic from certain IP addresses
- Outbound rule might allow certain traffic to leave the subnet

### What is a Security Group?

- Controls traffic to or from an EC2 instance
- Represents instance-level security
- Each security group can be applied to multiple instances, even across subnets
- Each instance is to be associated with one or more security groups

### Use case for Security Group

- Inbound rule to allow traffic from an IP address to access the instance

## Stateless vs Stateful

### What is a Stateful Firewall?

- Security groups are stateful
- Any changes made to an incoming rule is automatically applied to the outgoing rule

### What is a Stateless Firewall?

- NACLs are stateless
- Any changes made to an incoming rule is not automatically applied to the outgoing rule

## Building a VPC

### Dependencies for a VPC

- Internet Gateway
- Subnet
- Route table

### Steps

1. Navigate to VPC Management Console and select Your VPCs
2. Create a VPC and select the following settings:

- VPC only
- Name tag appropriately
- IPv4 CIDR manual input- 10.0.0.0/16
- No IPv6 CIDR block

3. Select Internet gateways from the VPC Management Console and Create internet gateway

- Attach the internet gateway to the VPC

4. Select Subnets from the VPC Management Console with and Create subnet with following settings:

- Name the subnet
- No preference of Availability Zone 

5. Create a Security group with the required permissions
6. The route table must enable an inbound rule that allows all IP addresses through the internet gateway to the public subnet

- The route table connecting to the internet gateway makes the subnet public

7. You must ensure that the route table, public subnet and internet gateway are all part of the same VPC and are all interlinked

- This can be checked from their respective dashboards

8. The aforementioned steps can be repeated to add the private subnet for the database; the difference is that the route table for the private subnet does not have a route to the internet gateway

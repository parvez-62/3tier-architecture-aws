# 3tier-architecture-aws

# AWS Three-Tier Architecture

## Overview

This project demonstrates the deployment of a three-tier architecture on AWS. The architecture includes the following layers:
1. *Presentation Tier*: User interface layer.
2. *Application Tier*: Business logic layer.
3. *Data Tier*: Database layer.

## Architecture Diagram

![Three-Tier Architecture Diagram](path_to_diagram.png)

## Steps to Create the Architecture

### Step 1: Creating a VPC
1. Go to *EC2*.
2. Click on *VPC* and then *Create VPC*.
3. In Resource to Create, select *VPC only*.
4. Provide a name and IPv4 CIDR block (e.g., 10.0.0.0/16).
5. Click *Create VPC*.

### Step 2: Creating Subnets
#### Public Subnets for Web Tier
1. Create the first subnet:
   - Name: Webtier-Public
   - IPv4 CIDR: 10.0.32.0/24
2. Create the second subnet:
   - Name: Webtier2-Public
   - IPv4 CIDR: 10.0.0.0/24

#### Private Subnets for Application Tier
1. Create the first subnet:
   - Name: Applicationtier-Private
   - IPv4 CIDR: 10.0.160.0/24
2. Create the second subnet:
   - Name: Applicationtier2-Private
   - IPv4 CIDR: 10.0.128.0/24

#### Private Subnets for Database Tier
1. Create the first subnet:
   - Name: Databasetier-Private
   - IPv4 CIDR: 10.0.96.0/24
2. Create the second subnet:
   - Name: Databasetier2-Private
   - IPv4 CIDR: 10.0.64.0/24

### Step 3: Creating an Internet Gateway
1. Create and name the Internet Gateway (e.g., igw-3tier-application).
2. Attach it to the VPC.

### Step 4: Creating Route Tables
1. Create and name a route table for private subnets (e.g., Route-Private).
2. Create and name a route table for public subnets (e.g., Route-Public).
3. Associate public subnets with the public route table.
4. Add a route to the public route table with destination 0.0.0.0/0 and target the Internet Gateway.
5. Associate private subnets with the private route table.

### Step 5: Creating a NAT Gateway
1. Create and name the NAT Gateway (e.g., nat-3tier-application).
2. Allocate an Elastic IP for it.
3. Update the private route table to route 0.0.0.0/0 traffic through the NAT Gateway.

### Step 6: Launch Templates and Auto Scaling Groups
#### Web Tier
1. Create a launch template:
   - AMI: Amazon Linux 2
   - Instance Type: t2.micro
   - Key Pair: Create or use an existing one
   - Security Group: Allow SSH and HTTP
   - User Data: Install Apache and set up a simple webpage
2. Create an Auto Scaling group for the web tier, using the web subnets.

#### Application Tier
1. Create a launch template:
   - AMI: Amazon Linux 2
   - Instance Type: t2.micro
   - Security Group: Allow SSH, HTTP, and MySQL
2. Create an Auto Scaling group for the application tier, using the application subnets.

### Step 7: Setting up RDS
1. Create an RDS instance with MySQL.
   - Instance Type: t2.micro
   - VPC: Use the existing VPC
   - Security Group: Allow MySQL connections from the application security group
2. Configure inbound rules to allow necessary traffic.

### Final Steps
1. Connect to your instances using SSH.
2. Set up security group rules as needed.
3. Test connectivity between the tiers.
4. Verify your application setup by accessing the web tier.

## Result
You should be able to connect to the MySQL instance from the application tier and see the web tier's simple webpage indicating successful deployment.

## Notes
- Ensure all resources are properly tagged.
- Follow best practices for security and resource management.



---

Thank you for using this AWS three-tier architecture guide!

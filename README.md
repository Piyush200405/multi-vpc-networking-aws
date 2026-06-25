# AWS Multi-VPC Networking Project

## Project Overview

This project demonstrates how to build a secure multi-VPC networking architecture on AWS. It connects two Virtual Private Clouds (VPCs) using **VPC Peering**, allowing private communication between EC2 instances while maintaining network isolation.

The project also implements **public and private subnets**, **Internet Gateway**, **NAT Gateway**, **Route Tables**, and **Security Groups** to provide secure internet access and controlled communication.

---

## Architecture

```
                        Internet
                            |
                     Internet Gateway
                            |
                   VPC-A (10.0.0.0/16)
          ---------------------------------
          |                               |
    Public Subnet                  Private Subnet
    10.0.1.0/24                   10.0.2.0/24
          |                               |
     Bastion Host                  Private EC2
          |                               |
          |--------- VPC Peering ---------|
                                          |
                                  VPC-B (10.1.0.0/16)
                                  --------------------
                                  Public Subnet
                                  10.1.1.0/24
                                          |
                                     Server-B EC2
```

---

## AWS Services Used

- Amazon VPC
- VPC Peering
- Public Subnets
- Private Subnets
- Internet Gateway (IGW)
- NAT Gateway
- Route Tables
- Security Groups
- EC2 Instances

---

## Features

- Created two separate VPCs
- Configured public and private subnets
- Internet access through Internet Gateway
- Private subnet internet access using NAT Gateway
- Secure Bastion Host architecture
- VPC Peering for private communication
- Security Group-based access control
- Route Table configuration
- Verified connectivity using SSH and Ping

---

## Network Configuration

### VPC-A

| Resource | Value |
|----------|-------|
| CIDR Block | 10.0.0.0/16 |
| Public Subnet | 10.0.1.0/24 |
| Private Subnet | 10.0.2.0/24 |

### VPC-B

| Resource | Value |
|----------|-------|
| CIDR Block | 10.1.0.0/16 |
| Public Subnet | 10.1.1.0/24 |

---

## Project Workflow

### Step 1
Created two VPCs:
- VPC-A
- VPC-B

### Step 2
Created:
- Public Subnet
- Private Subnet

### Step 3
Attached Internet Gateway to VPC-A.

### Step 4
Created NAT Gateway inside the Public Subnet.

### Step 5
Configured Route Tables.

### Step 6
Launched EC2 Instances:
- Bastion Host
- Private Server
- Server-B

### Step 7
Configured Security Groups.

### Step 8
Established VPC Peering.

### Step 9
Updated Route Tables for VPC Peering.

### Step 10
Verified:
- SSH Connectivity
- Internet Connectivity from Private EC2
- Ping between VPCs

---

## Connectivity Tests

### Test 1 - NAT Gateway

Command:

```bash
sudo apt update
```

Result:

- Private EC2 successfully accessed the internet through the NAT Gateway.

---

### Test 2 - VPC Peering

Command:

```bash
ping 10.1.1.246
```

Result:

- Successfully communicated with the EC2 instance in VPC-B using its private IP.

---

## Screenshots

The project includes screenshots of:

- VPC-A
- VPC-B
- Public & Private Subnets
- Internet Gateway
- NAT Gateway
- Route Tables
- Security Groups
- Bastion Host
- Private Server
- Server-B
- VPC Peering
- Successful Ping Test

Screenshots are available in the **screenshots/** folder.

---

## Learning Outcomes

Through this project, I gained practical experience with:

- AWS VPC Networking
- Internet Gateway
- NAT Gateway
- Public & Private Subnets
- Route Tables
- Security Groups
- Bastion Host
- VPC Peering
- Secure EC2 Communication
- AWS Networking Best Practices

---

## Author

**Piyush Sontakke**

GitHub: https://github.com/YOUR_GITHUB_USERNAME
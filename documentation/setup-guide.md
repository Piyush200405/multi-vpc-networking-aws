# AWS Multi-VPC Networking Setup Guide

## Objective

Build a secure AWS networking architecture using two VPCs connected with VPC Peering. Configure public and private subnets, Internet Gateway, NAT Gateway, route tables, and security groups to enable secure communication between EC2 instances.

---

# Architecture

* VPC-A (10.0.0.0/16)

  * Public Subnet (10.0.1.0/24)
  * Private Subnet (10.0.2.0/24)

* VPC-B (10.1.0.0/16)

  * Public Subnet (10.1.1.0/24)

---

# Step 1: Create VPCs

### VPC-A

* CIDR: 10.0.0.0/16

### VPC-B

* CIDR: 10.1.0.0/16

---

# Step 2: Create Subnets

### VPC-A

* Public Subnet: 10.0.1.0/24
* Private Subnet: 10.0.2.0/24

### VPC-B

* Public Subnet: 10.1.1.0/24

---

# Step 3: Create Internet Gateway

* Create an Internet Gateway.
* Attach it to VPC-A.

---

# Step 4: Create NAT Gateway

* Allocate an Elastic IP.
* Create a NAT Gateway in the public subnet of VPC-A.
* Wait until the NAT Gateway status becomes **Available**.

---

# Step 5: Configure Route Tables

## Public Route Table (VPC-A)

Routes:

* 10.0.0.0/16 → Local
* 0.0.0.0/0 → Internet Gateway

Associate with:

* Public Subnet

---

## Private Route Table (VPC-A)

Routes:

* 10.0.0.0/16 → Local
* 0.0.0.0/0 → NAT Gateway

Associate with:

* Private Subnet

---

## Route Table (VPC-B)

Routes:

* 10.1.0.0/16 → Local
* 0.0.0.0/0 → Internet Gateway

Associate with:

* Public Subnet

---

# Step 6: Launch EC2 Instances

## Bastion Host

* VPC-A Public Subnet
* Public IP Enabled

## Private Server

* VPC-A Private Subnet
* Public IP Disabled

## Server-B

* VPC-B Public Subnet
* Public IP Enabled

---

# Step 7: Configure Security Groups

## Bastion Host

* SSH (22) from My IP

## Private Server

* SSH (22) from Bastion Security Group
* ICMP from 10.1.0.0/16

## Server-B

* SSH (22) from 10.0.0.0/16
* ICMP from 10.0.0.0/16

---

# Step 8: Create VPC Peering

* Create a peering connection between VPC-A and VPC-B.
* Accept the peering request.

---

# Step 9: Update Route Tables

### VPC-A

* 10.1.0.0/16 → VPC Peering

### VPC-B

* 10.0.0.0/16 → VPC Peering

---

# Step 10: Connectivity Testing

## SSH to Bastion Host

```bash
ssh -i ubantu.pem ubuntu@<Bastion-Public-IP>
```

## SSH to Private Server

```bash
ssh -i ubantu.pem ubuntu@<Private-IP>
```

## Test NAT Gateway

```bash
sudo apt update
```

## Test VPC Peering

```bash
ping <Server-B-Private-IP>
```

---

# Expected Results

* Internet access from the private subnet through the NAT Gateway.
* Successful SSH access to the Private Server via the Bastion Host.
* Successful communication between VPC-A and VPC-B using private IP addresses through VPC Peering.

---

# Conclusion

This project demonstrates secure AWS networking using multiple VPCs, public and private subnets, NAT Gateway, Internet Gateway, route tables, security groups, and VPC Peering. It provides hands-on experience in designing and validating secure cloud network architectures.

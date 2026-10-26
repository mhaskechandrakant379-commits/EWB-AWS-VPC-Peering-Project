# EWB AWS VPC Peering Project

## Project Overview
This project demonstrates AWS VPC Peering between two VPCs in the Sydney region (ap-southeast-2).

The design includes a public bastion host in VPC A and private application instances in VPC A and VPC B.

## AWS Resources
- VPC A: 10.10.0.0/16
- VPC B: 10.20.0.0/16
- Public subnet A: 10.10.1.0/24
- Private subnet A: 10.10.2.0/24
- Private subnet B: 10.20.1.0/24
- VPC Peering ID: pcx-0aad5a1f97347483d (observed Active)
- Bastion private IP: 10.10.1.10
- App-A private IP: 10.10.2.10
- App-B private IP: 10.20.1.10

## Configured Components
- Two VPCs with non-overlapping CIDR ranges
- Public and private subnets
- VPC peering connection and route tables
- Internet Gateway attached to VPC A
- Security groups for bastion and application instances
- Three EWB EC2 instances

## Verification Status
AWS console screenshots document the configured VPCs, subnets, route tables, security groups, peering status, and EC2 instances.

Important: End-to-end SSH and ICMP ping verification was not completed successfully. This repository does not claim successful connectivity tests.

## Screenshots
Numbered PNG files in this repository document the available AWS configuration evidence.

## Region
AWS Asia Pacific (Sydney): ap-southeast-2

## Author
Chandrakant Ananta Mhaske

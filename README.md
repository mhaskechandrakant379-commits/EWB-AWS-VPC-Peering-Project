

# EWB AWS VPC Peering Project



## 1. Project Overview



This project demonstrates the configuration of VPC Peering between two Amazon Virtual Private Clouds (VPCs) in the AWS Asia Pacific (Sydney) Region.



The architecture includes a public bastion host in VPC A and private application instances in VPC A and VPC B. Route tables and security groups were configured to support the intended network communication.



**Important:** The VPC peering connection was observed in the Active state. End-to-end SSH and ICMP ping connectivity tests were not successfully completed, so successful private communication is not claimed.



## 2. AWS Region



- Region: Asia Pacific (Sydney)

- Region Code: `ap-southeast-2`



## 3. VPC Configuration



| Resource | Name | Resource ID | CIDR |

|---|---|---|---|

| VPC A | EWB-VPC-A | `vpc-05aff696bd706d33f` | `10.10.0.0/16` |

| VPC B | EWB-VPC-B | `vpc-0928b5ce593db9051` | `10.20.0.0/16` |



The VPCs use non-overlapping IPv4 CIDR ranges.



## 4. Subnet Configuration



| Subnet | Subnet ID | VPC | CIDR | Availability Zone |

|---|---|---|---|---|

| Public Subnet A | `subnet-089e38ea920deed2e` | VPC A | `10.10.1.0/24` | `ap-southeast-2a` |

| Private Subnet A | `subnet-0fe48ca0f9e81f73b` | VPC A | `10.10.2.0/24` | `ap-southeast-2a` |

| Private Subnet B | `subnet-0332a9f9de1529765` | VPC B | `10.20.1.0/24` | `ap-southeast-2a` |



The public subnet is configured to auto-assign public IPv4 addresses. The two application subnets do not auto-assign public IPv4 addresses.



## 5. VPC Peering



- Connection Name: `ewb-a-b-peer`

- Peering Connection ID: `pcx-0aad5a1f97347483d`

- Requester: VPC A

- Accepter: VPC B

- Observed State: Active



## 6. Route Table Configuration



### Public Route Table A



- Route Table ID: `rtb-0968cc7fcd22b0189`

- Associated subnet: Public Subnet A

- `10.10.0.0/16` → local

- `10.20.0.0/16` → VPC Peering connection

- `0.0.0.0/0` → Internet Gateway `igw-0a7159dae6d1719f7`



### Private Route Table A



- Route Table ID: `rtb-0b995a389e250729e`

- Associated subnet: Private Subnet A

- `10.10.0.0/16` → local

- `10.20.0.0/16` → VPC Peering connection



### Private Route Table B



- Route Table ID: `rtb-0a1d8c2afdbe88bd6`

- Associated subnet: Private Subnet B

- `10.20.0.0/16` → local

- `10.10.0.0/16` → VPC Peering connection



## 7. Internet Gateway



- Name: `EWB-IGW-A`

- Internet Gateway ID: `igw-0a7159dae6d1719f7`

- Attached VPC: VPC A



The Internet Gateway is associated with VPC A. Internet access also depends on the subnet route table and security configuration.



## 8. EC2 Instances



| Instance | Instance ID | Private IP | Public IP | Observed Status |

|---|---|---|---|---|

| EWB-Bastion | `i-0e510cd33f777ef5e` | `10.10.1.10` | `3.107.202.29` | Running |

| EWB-App-A | `i-00ca1e021d676e0ae` | `10.10.2.10` | None | Running |

| EWB-App-B | `i-0b252e6da42b91d71` | `10.20.1.10` | None | Running |



The EC2 instances were observed as Running, with 3/3 status checks reported in the AWS console screenshots.



## 9. Security Groups



### EWB-Bastion-SG



- Security Group ID: `sg-0eed2064a69541af2`

- Inbound: SSH TCP port 22 from `157.32.216.53/32` (configured source IP at the time of testing).

- Outbound: Default outbound rules.



### EWB-App-A-SG



- Security Group ID: `sg-0c9ff4daec4812708`

- Inbound: SSH TCP port 22 from `10.10.1.10/32`.

- Inbound: All ICMP-IPv4 from `10.20.1.10/32`.

- Outbound: Default outbound rules.



### EWB-App-B-SG



- Security Group ID: `sg-0642bea925f596e24`

- Inbound: All ICMP-IPv4 from `10.10.2.10/32`.

- Inbound: SSH TCP port 22 from `10.10.1.10/32`.

- Outbound: Default outbound rules.



These entries document the configured rules; they do not establish that end-to-end connectivity was successful.



## 10. Evidence and Screenshots



The repository includes screenshots documenting:



- VPC configuration

- VPC Peering connection state

- Subnet configuration

- Public and private route tables

- Bastion and application security groups

- Internet Gateway

- EC2 instance status and private IP addresses



See the numbered PNG files in the repository for the available configuration evidence.



## 11. Verification Status and Limitations



- The VPC Peering connection was observed in the Active state.

- Route tables and security group configurations are documented in screenshots.

- EC2 instances were observed in the Running state with 3/3 status checks.

- End-to-end SSH connectivity was not successfully verified.

- ICMP ping connectivity was not successfully verified.

- Controlled failure and recovery tests are not documented as completed.

- AWS resource cleanup has not been documented as completed.



An Active peering state alone does not prove successful end-to-end connectivity.



## 12. Conclusion



This project documents the configuration of two AWS VPCs, their subnets, a VPC Peering connection, route tables, an Internet Gateway, security groups, and EC2 instances.



The configuration evidence is included in this repository. End-to-end connectivity verification and cleanup evidence remain outstanding and are not claimed as completed.



## Author
## Author

Chandrakant Ananta Mhaske

## Repository

https://github.com/mhaskechandrakant379-commits/EWB-AWS-VPC-Peering-Project


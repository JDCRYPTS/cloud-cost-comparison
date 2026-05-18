# AWS vs Azure Cost Comparison Report

## 1. Introduction
This report compares the monthly hosting cost of a small 
web application on AWS and Microsoft Azure. The goal is 
to identify which provider is more cost-effective and 
under what circumstances.

## 2. Application Specifications

| Resource | Specification |
|---|---|
| Compute | 2 vCPU, 8 GB RAM |
| Operating System | Linux (primary), Windows (Azure comparison) |
| Block Storage | 100 GB SSD |
| Object Storage | 50 GB |
| Monthly Egress | 100 GB outbound to internet |
| Availability | Single region, single zone |
| Usage Hours | 730 hours/month (24/7) |

## 3. AWS Cost Breakdown

| Service | Specification | Monthly Cost |
|---|---|---|
| EC2 t3.medium (Linux) | 2 vCPU, 4 GB RAM, 730 hrs | included in total |
| EBS Storage (gp2) | 100 GB SSD | included in total |
| S3 Standard | 50 GB object storage | included in total |
| S3 Data Transfer Out | 100 GB egress | included in total |
| Total | | $46.05 |

Notes:
- t3.medium was used in place of t3.large due to 
  calculator availability at the time of estimation.
- gp2 storage was selected as gp3 was not available 
  in the calculator at the time of estimation.

AWS Estimate Link: (paste your AWS link here)

## 4. Azure Cost Breakdown

| Service | Specification | Monthly Cost |
|---|---|---|
| Linux VM D2ads v6 (Ubuntu) | 2 vCPU, 8 GB RAM, 730 hrs | included in total |
| Windows VM D2 v3 (Hybrid Benefit ON) | 2 vCPU, 8 GB RAM, 730 hrs | $70.08 |
| Windows VM D2 v3 (Hybrid Benefit OFF) | 2 vCPU, 8 GB RAM, 730 hrs | $137.24 |
| Blob Storage (Hot, LRS) | 50 GB | included in total |
| Data Retrieval | 100 GB | included in total |
| Total (all services combined) | | $196.75 |

Notes:
- Ubuntu was selected as the Linux operating system type.
- D2ads v6 was selected as the closest available match 
  to the required 2 vCPU, 8 GB RAM specification.
- D2 v3 was selected for the Windows VM comparison.
- Data retrieval (100 GB) was used as the closest 
  available option to egress in the Azure calculator.

Azure Estimate Link: (paste your Azure link here)

## 5. Networking Cost Analysis

### Egress Fees (100 GB/month)
Egress means data leaving the cloud to reach your users.

AWS:   First 1 GB free, then $0.09/GB. Total for 100 GB: ~$9.00
Azure: First 5 GB free, then $0.087/GB. Total for 100 GB: ~$8.70

Azure is slightly cheaper on egress at this volume.

### Inter-Zone Transfer Fees
Both AWS and Azure charge $0.01/GB each way when data 
moves between availability zones in the same region.

Key lesson: Keeping your server and storage in the same 
zone eliminates this cost entirely.

## 6. Discount Mechanisms

### AWS
Savings Plans:
- Commit to a minimum hourly spend for 1 or 3 years
- Up to 66% off On-Demand prices
- Flexible across EC2, Lambda and Fargate
- Best for teams that want flexibility long term

Reserved Instances:
- Commit to a specific instance type for 1 or 3 years
- Up to 72% off On-Demand prices
- Less flexible than Savings Plans
- Best for stable predictable workloads running 24/7

### Azure
Reserved VM Instances:
- Commit to a specific VM size for 1 or 3 years
- Up to 72% off Pay-as-you-go pricing
- Can exchange or cancel with some restrictions
- Best for stable workloads

Azure Savings Plan for Compute:
- Commit to a fixed hourl

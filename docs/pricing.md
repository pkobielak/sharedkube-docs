---
sidebar_position: 3
title: Pricing
slug: /pricing
---

# Pricing

Welcome to the General Purpose (g1) zones pricing guide. This document outlines
the cost structure for various zone sizes available in our service. All prices
listed below include VAT.

## Zone Sizes and Pricing

We offer a range of General Purpose zones, each suited to different workload sizes.
Below, you'll find the monthly pricing for each zone size, along with their per-minute
costs.

Additionally, we’ve compared these prices to the equivalent AWS stack, which
includes an EKS cluster, equivalent EC2 instance, load balancer, and NAT gateway.

| Zone Size | vCPU | Memory | Monthly Cost (USD) | Sharedkube Zone Per Minute Price (USD) | Cost Difference | AWS Equivalent Per Minute Price (USD) |
|-----------|------|--------|-------------------:|---------------------------------------:|----------------:|--------------------------------------:|
| g1.nano   | 0.2  | 1 GB   |               3.00 |                               0.000069 |      **-97.6%** |                              0.002852 |
| g1.micro  | 0.5  | 1 GB   |               9.00 |                               0.000208 |      **-92.9%** |                              0.002928 |
| g1.small  | 1    | 2 GB   |              20.00 |                               0.000463 |      **-84.9%** |                              0.003062 |
| g1.medium | 2    | 4 GB   |              45.00 |                               0.001042 |      **-68.7%** |                              0.003328 |
| g1.large  | 3    | 12 GB  |              60.00 |                               0.001389 |      **-64.5%** |                              0.003912 |


## How Costs Are Calculated

- **Monthly Cost:** The cost you pay for using the zone always-on for a full month
  (30 days).
- **Per Minute Price:** The cost per minute of usage.
- **AWS Equivalent:** An estimate of the equivalent cost for running the same
  configuration on AWS, including an EKS cluster, equivalent EC2 instance, load
  balancer, and NAT gateway.
- **Cost Difference:** The percentage by which Sharedkube reduces costs compared
  to the equivalent AWS stack.

## VAT Information

All prices provided in this guide include VAT. There are no hidden fees or
additional costs—what you see is what you pay.

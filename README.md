# Self-Healing Cloud Infrastructure with Auto Scaling (AWS)

A cloud infrastructure project that automatically detects instance failures, replaces unhealthy servers, and scales compute resources up or down based on real-time traffic — built entirely on AWS.

## Overview

Traditional infrastructure relies on manual monitoring to catch server failures and workload spikes, which leads to downtime and inconsistent performance. This project implements a **self-healing, auto-scaling infrastructure** using core AWS services so the system can detect problems and correct them on its own, with no manual intervention.

## Problem Statement

- Manual monitoring is slow and error-prone.
- Failed servers cause downtime until a human notices and fixes them.
- Fixed-capacity infrastructure either wastes money (over-provisioned) or fails under load (under-provisioned).

## AWS Services Used

| Service | Role |
|---|---|
| **Amazon EC2** | Compute layer that runs the application |
| **Elastic Load Balancing (ELB)** | Distributes incoming traffic across healthy instances |
| **EC2 Auto Scaling** | Launches/terminates instances based on demand and health |
| **Amazon CloudWatch** | Monitors health/metrics and triggers alarms for scaling and recovery |
| **Amazon VPC** | Isolated, secure network with public/private subnets |

## Architecture

```
Users / Traffic
      │
      ▼
Elastic Load Balancer (ELB)
      │
 ┌────┼────┐
 ▼    ▼    ▼
EC2  EC2  EC2   (Auto Scaling Group, spread across Availability Zones)
 │    │    │
 └────┼────┘
      ▼
Amazon CloudWatch (health checks, metrics, alarms)
```

CloudWatch continuously monitors instance health. If an instance fails a health check, the Auto Scaling Group terminates it and launches a replacement automatically. When traffic/CPU utilization crosses a threshold, Auto Scaling adds or removes instances, and the Load Balancer redistributes traffic accordingly.

## Key Features

- Automatic detection of failed/unhealthy EC2 instances
- Automatic replacement of failed instances (self-healing)
- Dynamic scaling based on real-time traffic and CPU/memory utilization
- Traffic distribution via Elastic Load Balancer
- Continuous monitoring and alerting via CloudWatch
- Secure networking using VPC with public/private subnets
- Cost optimization — resources scale down automatically during low demand

## Advantages

- High availability with minimal downtime
- Better performance during traffic spikes
- Lower operational cost through demand-based scaling
- Reduced human error from manual server management
- Improved fault tolerance across multiple Availability Zones

## Limitations

- Vendor lock-in to AWS
- Requires careful tuning of scaling policies and health check thresholds
- Sudden extreme spikes can cause brief delay while new instances boot
- Poorly tuned thresholds can increase billing from excess scaling activity

## Future Scope

- Predictive (ML-based) scaling to anticipate spikes before they happen
- Multi-cloud / hybrid-cloud extension to reduce vendor lock-in
- Serverless self-healing actions using AWS Lambda
- Centralized logging/analytics dashboard (CloudWatch Dashboards or Grafana)
- Automated cost-optimization recommendations based on historical scaling data

## Conclusion

This project shows how combining EC2, ELB, Auto Scaling, and CloudWatch produces a resilient, cost-efficient infrastructure that detects and recovers from failures on its own while scaling to meet real demand — reducing downtime and operational overhead compared to traditional, manually managed systems.

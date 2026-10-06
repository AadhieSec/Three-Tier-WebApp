# AWS Three-Tier Web Application

A highly available three-tier web application deployed on AWS using
separate presentation, application, and database layers.

## Architecture

![AWS Three-Tier Architecture](architecture/aws-architecture.png)

### Architecture Overview

The application follows a three-tier architecture:

- Presentation Tier
- Application Tier
- Database Tier

Traffic flows through the public-facing entry point into the application
tier, while the database remains isolated from direct internet access.

## AWS Services

| Service | Purpose |
|---|---|
| Amazon VPC | Network isolation |
| Application Load Balancer | Distributes application traffic |
| Amazon EC2 | Hosts application workloads |
| Amazon RDS | Database layer |
| IAM | Access control |
| Security Groups | Network-level access control |
| CloudWatch | Monitoring and logging |

## Architecture Flow

```text
Presentation Tier
AWS S3 (Cloudfront OAC)
  |
  v
AWS Cloudfront CDN
  |
  v
Application Tier
(API Gateway + Lambda)
  |
  v
Database Tier
(DynamoDB)

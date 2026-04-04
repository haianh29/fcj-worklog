---
title: "Solution Architecture & IaC"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 5.2. </b> "
---

## Solution Architecture & Infrastructure-as-Code

This section explains the overall architecture of the IMS system on AWS and how you can provision it using Infrastructure-as-Code (IaC).

### Logical Architecture

At a high level, the system follows this flow:

- **Browser / Frontend** - React SPA built from the `frontend/` folder.
- **CDN & Static Hosting** - React build artifacts hosted on Amazon S3 and served via Amazon CloudFront.
- **DNS & Routing** - Custom domain managed in Amazon Route 53, pointing to CloudFront (frontend) and ALB (backend API).
- **Backend API** - Spring Boot application from `backend/backend`, packaged as a Docker image and run on Amazon ECS (Fargate) behind an Application Load Balancer.
- **Database** - Amazon RDS (PostgreSQL) stores orders, production plans, line performance, and AI analysis results.
- **File Storage** - Multiple S3 buckets for:
  - Frontend static assets.
  - Production documents (POM/SOOP, forms, attachments).
  - Deployment artifacts and backups.
- **Messaging & Notifications** - Amazon SQS for background jobs, Amazon SNS and SES for alerts and emails.
- **Security & Config** - AWS Secrets Manager for credentials and API keys, IAM roles for ECS tasks and CI/CD.
- **Monitoring** - Amazon CloudWatch for logs, metrics, alarms, and dashboards.

### Mapping Repo to Architecture

- `backend/backend` -> Docker image -> ECS Task Definition -> ECS Service -> ALB Target Group.
- `frontend/` -> Vite build output -> S3 website bucket -> CloudFront distribution.
- Database schema (Flyway migrations under `src/main/resources/db/migration/`) -> Amazon RDS.
- Email template `otp-email.html` -> SES-based OTP and notification flows.

### Infrastructure-as-Code Options

You can implement the above architecture in different ways:

- Manual console setup for step-by-step learning.
- CloudFormation / AWS CDK templates to define VPC, ECS, RDS, S3, CloudFront, and related resources.
- Terraform if you prefer a multi-cloud style IaC approach.

For this workshop, you can start with console + CLI to understand each component, then optionally refactor into IaC templates as an extension.

### Difference from the Serverless Workshop

Compared to the serverless Travel Guide app in Workshop 5 (Lambda + API Gateway + DynamoDB):

- Here you run long-lived container services on ECS Fargate instead of short-lived Lambda functions.
- You use a relational database (RDS PostgreSQL) instead of DynamoDB.
- You manage container images in ECR and deployments via ECS/ALB.

This architecture is closer to how many existing Spring Boot + React enterprise systems are migrated to AWS.

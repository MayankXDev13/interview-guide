## Designing a Highly Available and Scalable Multi-Tier Application on AWS

### Question

Explain how you will design a highly available and scalable multi-tier
application.

### Short explanation of the question

This question evaluates your understanding of AWS architecture design.
Interviewers expect you to explain how to build an application that
remains available during failures and automatically scales to handle
increased traffic.

### Answer

A highly available and scalable multi-tier application separates the
workload into independent layers:

-   Presentation Layer (Load Balancer)
-   Application Layer (EC2/Lambda/ECS/EKS)
-   Database Layer (RDS/Aurora)
-   Storage Layer (S3/EFS)

The application is deployed across multiple Availability Zones (AZs)
with Auto Scaling and monitoring to eliminate single points of failure.

### Detailed explanation of the answer for readers' understanding

Typical AWS architecture:

``` text
                 Internet
                     │
                     ▼
          Route 53 (DNS)
                     │
                     ▼
        Application Load Balancer
             (Public Subnets)
             AZ-A        AZ-B
               │          │
      ┌────────┴──────────┴────────┐
      ▼                           ▼
 EC2 / ECS / EKS             EC2 / ECS / EKS
 (Private Subnet)            (Private Subnet)
      │                           │
      └──────────────┬────────────┘
                     ▼
              Amazon RDS/Aurora
             Multi-AZ Deployment
                     │
      ┌──────────────┴─────────────┐
      ▼                            ▼
 Amazon S3                     Amazon EFS
 Static Files                 Shared Storage
```

------------------------------------------------------------------------

## 1. Presentation Layer

Use:

-   Amazon Route 53
-   Application Load Balancer (ALB)

Responsibilities:

-   DNS resolution
-   SSL termination
-   Health checks
-   Traffic distribution

------------------------------------------------------------------------

## 2. Application Layer

Deploy application servers in **private subnets** across at least two
Availability Zones.

Use:

-   EC2 + Auto Scaling Group
-   Amazon ECS
-   Amazon EKS
-   AWS Lambda (serverless workloads)

Benefits:

-   High availability
-   Automatic scaling
-   Fault tolerance

------------------------------------------------------------------------

## 3. Database Layer

Use:

-   Amazon RDS
-   Amazon Aurora

Best practices:

-   Multi-AZ deployment
-   Automated backups
-   Read Replicas (for read-heavy workloads)
-   Encryption at rest

------------------------------------------------------------------------

## 4. Storage Layer

Use Amazon S3 for:

-   Images
-   Static websites
-   Backups
-   Documents

Use Amazon EFS when multiple compute instances need shared file storage.

------------------------------------------------------------------------

## 5. Networking

Create a VPC with:

-   Public subnets
-   Private subnets
-   Internet Gateway
-   NAT Gateway
-   Route Tables

Resources requiring internet access remain in public subnets, while
application and database servers remain private.

------------------------------------------------------------------------

## 6. Auto Scaling

Configure an Auto Scaling Group.

Example policy:

-   Scale out when CPU \> 70%
-   Scale in when CPU \< 30%

This ensures efficient resource utilization.

------------------------------------------------------------------------

## 7. High Availability

Deploy resources across multiple Availability Zones.

If one AZ fails:

-   Load Balancer redirects traffic.
-   Auto Scaling launches replacement instances.
-   RDS Multi-AZ automatically fails over.

------------------------------------------------------------------------

## 8. Monitoring

Use:

-   Amazon CloudWatch
-   AWS CloudTrail
-   Prometheus
-   Grafana

Monitor:

-   CPU
-   Memory (via CloudWatch Agent)
-   Request latency
-   Error rate
-   Disk usage

------------------------------------------------------------------------

## 9. Security

Implement:

-   IAM Roles
-   Security Groups
-   Network ACLs
-   AWS WAF
-   AWS Secrets Manager
-   KMS encryption

------------------------------------------------------------------------

## Typical interview answer

> I design a multi-tier application using Route 53, an Application Load
> Balancer, Auto Scaling Groups across multiple Availability Zones,
> private subnets for application servers, and Amazon RDS Multi-AZ for
> the database. Static content is stored in S3, shared storage uses EFS
> if required, and CloudWatch monitors the environment. This
> architecture eliminates single points of failure and automatically
> scales based on demand.

### Best practices

-   Deploy across multiple AZs.
-   Use Auto Scaling.
-   Keep databases in private subnets.
-   Enable Multi-AZ for RDS.
-   Store static content in S3.
-   Monitor using CloudWatch and alerts.
-   Secure resources with IAM and Security Groups.

### Key takeaways

-   Separate presentation, application, database, and storage layers.
-   Use multiple Availability Zones for high availability.
-   Auto Scaling and Load Balancers provide scalability.
-   Private subnets improve security.
-   Monitoring and backups are essential for production workloads.

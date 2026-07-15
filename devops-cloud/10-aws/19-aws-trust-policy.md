## AWS Trust Policy

### Question

What is a Trust Policy in AWS and why is it used?

### Short explanation of the question

Tests IAM role concepts.

### Answer

A Trust Policy defines **who can assume an IAM role**. It specifies
trusted principals such as AWS accounts, IAM users, roles, or AWS
services.

### Detailed explanation

Example trusted principal: - Lambda - EC2 - Another AWS Account

Without a trust policy, a role cannot be assumed.

### Typical interview answer

> A trust policy specifies who is allowed to assume an IAM role,
> enabling secure service-to-service and cross-account access.

### Key takeaways

-   Attached to IAM roles.
-   Controls AssumeRole access.

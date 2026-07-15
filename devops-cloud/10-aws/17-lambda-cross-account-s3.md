## Lambda in One Account Accessing S3 in Another

### Question

How can an AWS Lambda in one account connect to an S3 bucket in another
account?

### Short explanation of the question

Tests cross-account IAM access.

### Answer

Grant the Lambda execution role permission through an S3 bucket policy
or by assuming a cross-account IAM role using AWS STS.

### Detailed explanation

Flow: Lambda → IAM Role → STS AssumeRole (optional) → S3 Bucket Policy →
S3 Bucket

### Typical interview answer

> I grant cross-account access using an S3 bucket policy or an assumable
> IAM role with AWS STS, following the principle of least privilege.

### Key takeaways

-   Bucket policy or AssumeRole.
-   Least privilege.

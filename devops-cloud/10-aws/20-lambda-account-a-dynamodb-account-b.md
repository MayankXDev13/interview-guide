## Lambda in Account A Accessing DynamoDB in Account B

### Question

How can a Lambda function in AWS Account A interact with DynamoDB in
Account B?

### Short explanation of the question

Tests cross-account IAM architecture.

### Answer

Create an IAM role in Account B with DynamoDB permissions and a trust
policy allowing Account A to assume it. The Lambda uses AWS STS
AssumeRole to obtain temporary credentials.

### Detailed explanation

Flow: Lambda (Account A) → STS AssumeRole → IAM Role (Account B) →
DynamoDB

### Typical interview answer

> I create a cross-account IAM role in Account B, configure its trust
> policy for Account A, then use STS AssumeRole from Lambda to obtain
> temporary credentials for DynamoDB access.

### Key takeaways

-   Cross-account role.
-   Trust policy.
-   STS AssumeRole.

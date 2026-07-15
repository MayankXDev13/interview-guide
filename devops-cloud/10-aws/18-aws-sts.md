## AWS STS

### Question

What is AWS STS and how does it work?

### Short explanation of the question

Tests understanding of temporary credentials.

### Answer

AWS Security Token Service (STS) issues temporary security credentials
for IAM users, roles, or federated identities.

### Detailed explanation

Common APIs: - AssumeRole - AssumeRoleWithWebIdentity - GetSessionToken

Flow: User/Lambda → STS → Temporary credentials → AWS Service

### Typical interview answer

> STS provides temporary credentials that expire automatically and are
> commonly used for cross-account access and federation.

### Key takeaways

-   Temporary credentials.
-   Supports AssumeRole.

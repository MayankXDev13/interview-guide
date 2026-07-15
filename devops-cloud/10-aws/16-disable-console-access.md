## Disable AWS Console Access for IAM Users

### Question

How do you disable AWS Console access to IAM users?

### Short explanation of the question

Tests IAM administration knowledge.

### Answer

Disable or remove the IAM user's console password, require role-based
access, and use IAM Identity Center or federation where possible.

### Detailed explanation

Methods: - Delete console password. - Disable login profile. - Enforce
MFA. - Prefer IAM roles over long-lived users.

### Typical interview answer

> I remove the user's login profile or console password, enforce MFA
> where required, and encourage role-based access instead of IAM users.

### Key takeaways

-   Remove login profile.
-   Prefer IAM roles.

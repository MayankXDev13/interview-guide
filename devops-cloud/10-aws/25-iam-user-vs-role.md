## Difference Between IAM User and IAM Role

### Question

What is the difference between IAM User and IAM Role?

### Short explanation of the question

This question evaluates IAM fundamentals.

### Answer

An IAM User represents a permanent identity with long-term credentials,
whereas an IAM Role provides temporary credentials that are assumed when
needed.

### Detailed explanation

  -----------------------------------------------------------------------
  IAM User                            IAM Role
  ----------------------------------- -----------------------------------
  Long-term credentials               Temporary credentials

  Password/Access Keys                Assumed via STS

  Used by people                      Used by AWS services, applications
                                      and cross-account access
  -----------------------------------------------------------------------

### Typical interview answer

> IAM Users are for permanent identities, while IAM Roles are assumed
> temporarily by AWS services, applications or other AWS accounts. In
> production, we prefer IAM Roles over long-term access keys.

### Key takeaways

-   User = permanent identity.
-   Role = temporary identity.
-   Prefer roles in production.

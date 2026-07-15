## Prevent Accidental Resource Deletion

### Question

Your team can delete resources. How do you prevent accidental deletion?

### Short explanation

Tests Azure governance.

### Answer

Use Azure Resource Locks, RBAC, Azure Policy and backups.

### Detailed explanation

Apply CanNotDelete locks on critical resources and grant least-privilege
RBAC.

### Typical interview answer

> I protect production resources with Delete Locks and RBAC while
> ensuring backups exist.

### Key takeaways

-   Resource Locks.
-   Least privilege.

## Service Principals vs Managed Identities

### Question

Service Principals vs Managed Identities. Which one is better?

### Short explanation

Tests Azure identity.

### Answer

Managed Identities are preferred because Azure manages credential
rotation automatically. Service Principals are used when identities are
needed outside Azure-managed resources.

### Typical interview answer

> I prefer Managed Identities whenever possible because they eliminate
> secret management.

### Key takeaways

-   Managed Identity preferred.
-   No secret rotation.

## Secure App-to-App Communication in AKS

### Question

In an AKS cluster how will you secure app-to-app communication?

### Short explanation

Tests Kubernetes security.

### Answer

Use Network Policies, mTLS with a service mesh, Managed
Identity/Workload Identity, Kubernetes Secrets and TLS.

### Typical interview answer

> I secure communication using Network Policies and mTLS through a
> service mesh while authenticating workloads with Managed Identity.

### Key takeaways

-   Network Policies.
-   mTLS.

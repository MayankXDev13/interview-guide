## Communication Between Different Subnets in a VPC

### Question

Can applications in different subnets of a VPC interact by default? If
no, why?

### Short explanation of the question

This question checks your understanding of VPC networking, route tables,
Security Groups, and Network ACLs.

### Answer

Yes, **applications in different subnets of the same VPC can communicate
by default**, provided that: - Route tables allow traffic. - Security
Groups permit the required ports. - Network ACLs do not block the
traffic.

Subnets inside the same VPC automatically have a **local route** that
enables communication.

### Detailed explanation of the answer for readers' understanding

``` text
VPC (10.0.0.0/16)
 ├── Public Subnet (10.0.1.0/24)
 └── Private Subnet (10.0.2.0/24)

Route Table
10.0.0.0/16 → local
```

The **local** route allows communication between subnets. However,
Security Groups and NACLs can still deny traffic.

### Typical interview answer

> Subnets in the same VPC can communicate using the automatically
> created local route. Communication succeeds only if Security Groups
> and Network ACLs allow it.

### Key takeaways

-   Same VPC → local routing exists by default.
-   Security Groups and NACLs control whether traffic is allowed.

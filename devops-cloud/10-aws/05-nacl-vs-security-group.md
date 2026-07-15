## Difference Between Network ACL and Security Group

### Question

Explain NACL vs Security Group and which one do you use in your
organization?

### Short explanation of the question

Interviewers want to know the differences between subnet-level and
instance-level firewalls.

### Answer

A **Security Group (SG)** is a **stateful firewall** attached to an EC2
instance or ENI, while a **Network ACL (NACL)** is a **stateless
firewall** attached to a subnet.

### Detailed explanation

  Feature          Security Group   Network ACL
  ---------------- ---------------- ----------------------------
  Level            Instance         Subnet
  Stateful         Yes              No
  Allow Rules      Yes              Yes
  Deny Rules       No               Yes
  Return Traffic   Automatic        Must be explicitly allowed

### Which one is commonly used?

Most organizations primarily use **Security Groups** for day-to-day
access control because they are stateful and easier to manage. NACLs are
used as an additional subnet-level security layer when required.

### Typical interview answer

> We mainly use Security Groups to control application traffic. NACLs
> are used only for subnet-level protection or specific compliance
> requirements.

### Key takeaways

-   SG = Stateful, instance level.
-   NACL = Stateless, subnet level.
-   SGs are used more frequently in production.

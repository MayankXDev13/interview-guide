## OpenTofu vs Terraform

### Question

Have you heard about OpenTofu? Do you think it is better than Terraform?

### Short explanation of the question

This question checks whether you are aware of **OpenTofu**, an
open-source fork of Terraform. Interviewers want to know why it was
created, how it compares to Terraform, and when you might choose one
over the other.

### Answer

Yes. OpenTofu is an **open-source fork of Terraform** created by the
Linux Foundation after HashiCorp changed Terraform's license from the
Mozilla Public License (MPL 2.0) to the Business Source License (BSL).

OpenTofu is highly compatible with existing Terraform configurations and
providers. Whether it is "better" depends on an organization's
requirements.

### Detailed explanation of the answer for readers' understanding

  Feature                   Terraform                       OpenTofu
  ------------------------- ------------------------------- -------------------------------
  License                   Business Source License (BSL)   MPL 2.0 (Open Source)
  Community                 Large and mature                Rapidly growing
  Terraform Cloud           Available                       Not available
  Enterprise Features       Yes                             Community-driven alternatives
  Provider Compatibility    Native                          Largely compatible
  Existing Terraform Code   Supported                       Mostly compatible

------------------------------------------------------------------------

### Why was OpenTofu created?

HashiCorp changed Terraform's license from **MPL 2.0** to **BSL**.

Some companies and community members preferred a fully open-source
Infrastructure as Code tool, leading to the creation of OpenTofu.

------------------------------------------------------------------------

### Advantages of OpenTofu

-   Completely open source.
-   Community-driven development.
-   Compatible with most existing Terraform code.
-   Supports existing providers and modules.
-   No vendor lock-in concerns related to licensing.

------------------------------------------------------------------------

### Advantages of Terraform

-   Larger ecosystem and user community.
-   Official Terraform Cloud platform.
-   Terraform Enterprise for governance and compliance.
-   Extensive documentation and long-term adoption in many
    organizations.

------------------------------------------------------------------------

### Typical interview answer

> Yes, I am familiar with OpenTofu. It is an open-source fork of
> Terraform created after the Terraform license changed. It is highly
> compatible with existing Terraform configurations. For organizations
> that prefer a fully open-source solution, OpenTofu is a strong choice.
> Terraform remains a mature option with a larger ecosystem and
> enterprise offerings such as Terraform Cloud and Terraform Enterprise.

### When should you choose each?

-   **Choose Terraform** when you need Terraform Cloud, Enterprise
    features, or are already invested in the HashiCorp ecosystem.
-   **Choose OpenTofu** when your organization prefers a fully
    open-source Infrastructure as Code solution while maintaining
    compatibility with Terraform code.

### Key takeaways

-   OpenTofu is an open-source fork of Terraform.
-   Most Terraform configurations work with OpenTofu with minimal
    changes.
-   Terraform provides a larger ecosystem and enterprise products.
-   The best choice depends on licensing preferences, governance
    requirements, and organizational needs.
## Should You Store the Terraform Statefile in Git?

### Question

Have you considered storing the statefile in Git instead of AWS S3 or
Azure Blob?

### Short explanation of the question

This question tests whether you understand **Terraform state management
best practices**. While Git is excellent for storing Terraform code, it
is **not designed to store the Terraform statefile**, especially in
collaborative environments.

### Answer

No. Storing the Terraform statefile in Git is considered a bad practice
for production environments.

Instead, Terraform state should be stored in a **remote backend** such
as: - AWS S3 (with DynamoDB for state locking) - Azure Blob Storage -
Google Cloud Storage (GCS) - Terraform Cloud - Terraform Enterprise

These backends provide versioning, security, collaboration, and state
locking.

### Detailed explanation of the answer for readers' understanding

  -----------------------------------------------------------------------
  Git Repository                      Remote Backend
  ----------------------------------- -----------------------------------
  Stores Terraform code               Stores Terraform state

  No state locking                    Supports state locking

  Merge conflicts are possible        Prevents concurrent updates

  May expose sensitive information    Supports encryption and access
                                      control

  Not designed for infrastructure     Purpose-built for Terraform state
  state                               
  -----------------------------------------------------------------------

------------------------------------------------------------------------

#### Why storing the statefile in Git is not recommended

1.  **Sensitive information**
    -   The statefile may contain resource IDs, IP addresses, secrets,
        or other metadata.
2.  **No state locking**
    -   Multiple engineers can overwrite the same statefile.
3.  **Merge conflicts**
    -   Since the statefile changes after almost every
        `terraform apply`, conflicts become common.
4.  **Collaboration issues**
    -   Git cannot coordinate concurrent infrastructure operations.

------------------------------------------------------------------------

#### Recommended AWS backend example

``` hcl
terraform {
  backend "s3" {
    bucket         = "company-terraform-state"
    key            = "prod/network/terraform.tfstate"
    region         = "ap-south-1"
    dynamodb_table = "terraform-locks"
    encrypt        = true
  }
}
```

In this configuration:

-   **S3** stores the statefile.
-   **DynamoDB** provides state locking.
-   **Encryption** protects the stored state.

### Key takeaways

-   Store Terraform **code** in Git.
-   Store the Terraform **statefile** in a remote backend.
-   Remote backends provide versioning, encryption, access control, and
    state locking.
-   Git should never be used as the primary storage location for
    production Terraform state.
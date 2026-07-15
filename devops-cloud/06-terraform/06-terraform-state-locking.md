## What Happens if Two DevOps Engineers Update the Terraform Statefile at the Same Time?

### Question

Two DevOps Engineers attempt to update the Terraform statefile at once.
What happens?

### Short explanation of the question

This question tests your understanding of **Terraform state locking**.
In a collaborative environment, multiple engineers may run
`terraform apply` simultaneously. Terraform uses **state locking** to
prevent concurrent updates that could corrupt the statefile.

### Answer

If **state locking is enabled**, the first engineer acquires the lock
and proceeds with the operation. Any other engineer attempting to modify
the same state must wait until the lock is released or receives an error
indicating that the state is locked.

If **state locking is not enabled**, both engineers may modify the state
at the same time, leading to state corruption, failed deployments, or
infrastructure drift.

### Detailed explanation of the answer for readers' understanding

The sequence is as follows:

``` text
Engineer A
terraform apply
      │
      ▼
Acquires State Lock
      │
      ▼
Updates Infrastructure
      │
      ▼
Updates Statefile
      │
      ▼
Releases Lock
```

At the same time:

``` text
Engineer B
terraform apply
      │
      ▼
Attempts to Acquire Lock
      │
      ▼
Lock Already Held
      │
      ▼
Operation Waits or Fails
```

------------------------------------------------------------------------

### Example error

If Engineer B runs:

``` bash
terraform apply
```

Terraform may display an error similar to:

``` text
Error: Error acquiring the state lock

Lock Info:
  ID:        12345678
  Operation: OperationTypeApply
  Who:       engineer-a@example.com
```

This indicates that another Terraform operation is already modifying the
state.

------------------------------------------------------------------------

### How state locking works

Different backends provide locking in different ways:

  Backend                State Locking
  ---------------------- ------------------
  AWS S3 + DynamoDB      Yes
  Azure Blob Storage     Yes (Blob Lease)
  Google Cloud Storage   Yes
  Terraform Cloud        Yes
  Local State            No

------------------------------------------------------------------------

### What happens without state locking?

Without locking:

1.  Engineer A starts `terraform apply`.
2.  Engineer B also starts `terraform apply`.
3.  Both read the same state.
4.  Both attempt to update infrastructure.
5.  The last write may overwrite the previous state.

Possible consequences:

-   Corrupted statefile
-   Duplicate resources
-   Failed deployments
-   Infrastructure drift
-   Inconsistent Terraform state

------------------------------------------------------------------------

### Best practices

-   Always use a remote backend.
-   Enable state locking.
-   Avoid force-unlocking unless absolutely necessary.
-   Wait for running Terraform operations to finish before starting
    another.

### Key takeaways

-   State locking ensures only one Terraform operation updates the state
    at a time.
-   A second user cannot modify the state until the current lock is
    released.
-   Without state locking, concurrent updates can corrupt the statefile
    and cause infrastructure inconsistencies.
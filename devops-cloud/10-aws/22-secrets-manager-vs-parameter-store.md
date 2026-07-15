## AWS Secrets Manager vs Parameter Store

### Question

AWS Secrets Manager vs Parameter Store

### Short explanation of the question

This question tests when to use each service for configuration and
secrets.

### Answer

Secrets Manager is designed for sensitive secrets with automatic
rotation, while Parameter Store stores configuration values and can also
store encrypted secrets.

### Detailed explanation

  Feature                Secrets Manager   Parameter Store
  ---------------------- ----------------- -----------------
  Secret Rotation        Yes               No
  Cost                   Higher            Lower
  Password Storage       Yes               Yes
  Configuration Values   Limited           Yes

### Typical interview answer

> I use Secrets Manager for database passwords and API keys that require
> rotation, while Parameter Store is used for application configuration
> and non-rotating parameters.

### Key takeaways

-   Secrets → Secrets Manager.
-   Configuration → Parameter Store.

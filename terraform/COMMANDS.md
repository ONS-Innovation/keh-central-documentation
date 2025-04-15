# Terraform Commands

This page outlines the general commands for managing infrastructure using Terraform.

## Updating Resources with Terraform

When infrastructure code has been modified, follow these steps to update the deployed resources:

- Change directory to the terraform configuration directory:

  ```bash
  cd terraform/<directory-name>
  ```

- Update any required variables in the appropriate environment variable file (e.g. env/dev/dev.tfvars or env/prod/prod.tfvars)

- Initialize terraform with the appropriate backend configuration:

  ```bash
  terraform init -backend-config=env/<environment>/backend-<environment>.tfbackend -reconfigure
  ```

  The reconfigure option ensures that the backend state is reconfigured to point to the appropriate state storage location.

  **_Please Note:_** This step requires appropriate credentials to be loaded into the environment if not already in place.
  For AWS, this can be done using:

  ```bash
  export AWS_ACCESS_KEY_ID="<aws_access_key_id>"
  export AWS_SECRET_ACCESS_KEY="<aws_secret_access_key>"
  ```

- Refresh the local state to ensure it is in sync with the backend:

  ```bash
  terraform refresh -var-file=env/<environment>/<environment>.tfvars
  ```

- Plan the changes to review what will be modified:

  ```bash
  terraform plan -var-file=env/<environment>/<environment>.tfvars
  ```

- Apply the changes to update the infrastructure:

  ```bash
  terraform apply -var-file=env/<environment>/<environment>.tfvars
  ```

- Once terraform has completed successfully, your infrastructure will be updated according to your configuration changes.

## Destroying Resources

To remove all resources managed by your terraform configuration:

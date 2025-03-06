# Terraform Commands

This page outlines the commands for updating the running service using Terraform.

### Updating the running service using Terraform

If the application has been modified then the following can be performed to update the running service:

- Build a new version of the container image and upload to ECR as per the instructions earlier in this guide.
- Change directory to the **service terraform**

  ```bash
  cd terraform/<directory-name>
  ```

- In the appropriate environment variable file env/dev/dev.tfvars or env/prod/prod.tfvars
  - Change the _container_ver_ variable to the new version of your container.
  - Change the _force_deployment_ variable to _true_.

- Initialise terraform for the appropriate environment config file _backend-dev.tfbackend_ or _backend-prod.tfbackend_ run:

  ```bash
  terraform init -backend-config=env/<environment>/backend-<environment>.tfbackend -reconfigure
  ```

  The reconfigure options ensures that the backend state is reconfigured to point to the appropriate S3 bucket.

  **_Please Note:_** This step requires an **AWS_ACCESS_KEY_ID** and **AWS_SECRET_ACCESS_KEY** to be loaded into the environment if not already in place.
  This can be done using:

  ```bash
  export AWS_ACCESS_KEY_ID="<aws_access_key_id>"
  export AWS_SECRET_ACCESS_KEY="<aws_secret_access_key>"
  ```

- Refresh the local state to ensure it is in sync with the backend

  ```bash
  terraform refresh -var-file=env/<environment>/<environment>.tfvars
  ```

- Plan the changes, ensuring you use the correct environment config (depending upon which env you are configuring):

  E.g. for the dev environment run

  ```bash
  terraform plan -var-file=env/<environment>/<environment>.tfvars
  ```

- Apply the changes, ensuring you use the correct environment config (depending upon which env you are configuring):

  E.g. for the dev environment run

  ```bash
  terraform apply -var-file=env/<environment>/<environment>.tfvars
  ```

- When the terraform has applied successfully the running task will have been replaced by a task running the container version you specified in the tfvars file.

### Destroy the Main Service Resources

Delete the service resources by running the following ensuring your reference the correct environment files for the backend-config and var files:

```bash
cd terraform/service

terraform init -backend-config=env/dev/backend-dev.tfbackend -reconfigure

terraform refresh -var-file=env/dev/dev.tfvars

terraform destroy -var-file=env/dev/dev.tfvars
```


# Example (dev):

Change directory to the service terraform directory:
```bash
cd terraform/service
```

Initialise terraform for the dev environment:
```bash
terraform init -backend-config=env/dev/backend-dev.tfbackend -reconfigure
```

Refresh the local state to ensure it is in sync with the backend:
```bash
terraform refresh -var-file=env/dev/dev.tfvars
```

Plan the changes for the dev environment:
```bash 
terraform plan -var-file=env/dev/dev.tfvars
```

Apply the changes for the dev environment:
```bash
terraform apply -var-file=env/dev/dev.tfvars
```


Destroy the service resources for the dev environment:
```bash
terraform destroy -var-file=env/dev/dev.tfvars
```


# Example (prod):

Change directory to the service terraform directory:
```bash
cd terraform/service
```

Initialise terraform for the prod environment:
```bash
terraform init -backend-config=env/prod/backend-prod.tfbackend -reconfigure
```

Refresh the local state to ensure it is in sync with the backend:
```bash
terraform refresh -var-file=env/prod/prod.tfvars
```

Plan the changes for the prod environment:
```bash 
terraform plan -var-file=env/prod/prod.tfvars
```

Apply the changes for the prod environment:
```bash
terraform apply -var-file=env/prod/prod.tfvars
```


Destroy the service resources for the prod environment:
```bash
terraform destroy -var-file=env/prod/prod.tfvars
```


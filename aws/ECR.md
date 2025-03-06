# Storing the container on AWS Elastic Container Registry (ECR)

These instructions assume:

1. You have a repository set up in your AWS account named github-audit-dashboard.
2. You have created an AWS IAM user with permissions to read/write to ECR (e.g AmazonEC2ContainerRegistryFullAccess policy) and that you have created the necessary access keys for this user.
3. The credentials for this user are stored in ~/.aws/credentials and can be used by accessing aws --profile <aws-credentials-profile>, if these are the only credentials in your file then the profile name is default. See [Setup.md](Setup.md) for more information.

You can find the AWS repo push commands under your repository in ECR by selecting the "View Push Commands" button. This will display a guide to the following (replace <aws-credentials-profile>, <aws-account-id> and <version> accordingly):

### Logging in to AWS CLI

Get an authentication token and authenticate your docker client for pushing images to ECR:
```bash
aws ecr --profile <aws-credentials-profile> get-login-password --region eu-west-2 | docker login --username AWS --password-stdin <aws-account-id>.dkr.ecr.eu-west-2.amazonaws.com
```

### Building and tagging ECR:

1. Build and tag in one go (recommended):

    Alternatively, you can build the image and name it as the ECR repository name:
    ```bash
    docker build -t <aws-account-id>.dkr.ecr.eu-west-2.amazonaws.com/<app-name>:<version> .
    ```

2. Build and tag separately:

    Build you container:
    ```bash
    docker build -t <app-name> .
    ```

    Tag your latest built docker image for ECR (assumes you have run docker build -t github-audit-dashboard . locally first)
    ```bash
    docker tag <app-name>:latest <aws-account-id>.dkr.ecr.eu-west-2.amazonaws.com/<app-name>:<version>
    ```

Note: To find the <version> to build look at the latest tagged version in ECR and increment appropriately

### Pushing to ECR

Push the version up to ECR:
```bash
docker push <aws-account-id>.dkr.ecr.eu-west-2.amazonaws.com/<app-name>:<version>
```

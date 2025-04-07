# Setup AWS CLI

Install AWS CLI

```bash
brew install awscli
```


Configure default AWS CLI:
```bash
aws configure
```


Configure AWS CLI Profile:
```bash
aws configure --profile <profile-name>
```

You will be prompted to enter the following:

```cmd
AWS Access Key ID [Required]:       <aws-access-key-id>
AWS Secret Access Key [Required]:   <aws-secret-access-key>
Default region name [Optional]:     <aws-region>
Default output format [Optional]:   <aws-output-format>
```

Your AWS credentials are stored in `~/.aws/credentials`.

Use the following command to view your credentials:

```bash
nano ~/.aws/credentials
```

This file will look like the following:

```bash
[default]
aws_access_key_id = AB99999999999999999YZ
aws_secret_access_key = AB99999999999999999YZ

[sdp-dev-ecr-user]
aws_access_key_id = AB99999999999999999YZ
aws_secret_access_key = AB99999999999999999YZ
```

### Naming convention

The profile name should follow the following convention:

```bash
<environment>-<iam-user-name>
```

For example: ```sdp-dev-ecr-user```

Usage:
```bash     
aws ecr --profile sdp-dev-ecr-user get-login-password --region eu-west-2
```

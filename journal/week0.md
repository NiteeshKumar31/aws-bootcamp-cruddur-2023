# Week 0 — Billing and Architecture

## Getting Started with AWS CLI

- We will be making use of Gitpod as part of AWS CLI installation.
- Open Gitpod through your Github repositoty and start executing the below commands.
-  [AWS CLI Reference Documentation](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/index.html)

```
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
      unzip awscliv2.zip
      sudo ./aws/install
```
## Configure your aws account in Gitpod

- Make use of below commands, add your account details and run them in CLI.

```
export AWS_ACCESS_KEY_ID=""
export AWS_SECRET_ACCESS_KEY=""
export AWS_DEFAULT_REGION=""
```
### As we don't want to configure our account every time we run a workspace, we better save the variable details in gitpod.

- Save above aws account details in gitpod environmental variables, run them in CLI.

```
gp env AWS_ACCESS_KEY_ID=""
gp env AWS_SECRET_ACCESS_KEY=""
gp env AWS_DEFAULT_REGION=""
```

- Check whether user existed in Gitpod AWS CLI

```
aws sts get-caller-identity
```

You should get something like this with details :).

```
{
    "UserId": "",
    "Account": "",
    "Arn": ""
}
```


# Project Implementation

- clone my Repository: [Repository Link](https://github.com/sonam-niit/Devops-Capstone-Oct-2025.git)
- or else you can manually create folder named frontend
    - under that create index.html
    - copy code shown here
- create folder for infra   
    - create terraform
        - main.tf
        - variables.tf
        - outputs.tf
        - terraform.tfvars
- create folder for CICD
    - .github
        - workflows
            - terraform.yml
            - frontend.yml
            - backend-deploy.yml
- create folder for Backend
    - create folder generate-presigned-url
        - main.py (add code)
    - create folder process-uploaded-file
        - main.py (add code)


## Make sure AWS is Configured in  yor system

- verify

```bash
aws configure list
aws sts get-caller-identity
```
- if you don't have any of this 
- download aws cli in your system
- install verify using: aws --version

- next step is go to AWS Console Create IAM user with policy administrator Access
- click on create Access Key.
- you can see Access Key and Secret Key
- go to your system and run: aws configure
- enter access key then secret key and then region: us-east-1, format: json
- after this It will be configured.

## For Project we need 3 Buckets

1. S3 Remote Backend (create manually)
2. frontend Hosting (create using terraform)
3. Backend uploading files (create using terraform)

## Let's create bucket for Remote Backend and DynamoDb for Locking table

```bash
# Create S3 bucket for Terraform state
aws s3api create-bucket \
  --bucket devops-accelerator-platform-tf-state-sonam \
  --region us-east-1

# Create DynamoDB table for state locking
aws dynamodb create-table \
  --table-name devops-accelerator-tf-locker \
  --attribute-definitions AttributeName=LockID,AttributeType=S \
  --key-schema AttributeName=LockID,KeyType=HASH \
  --billing-mode PAY_PER_REQUEST \
  --region us-east-1
```


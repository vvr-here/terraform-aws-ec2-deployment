# Deploy an AWS EC2 Instance Using Terraform

## Project Overview

This project demonstrates how to provision an Amazon EC2 instance on AWS using **Terraform (Infrastructure as Code)**.

Using Terraform, I automated the process of creating an EC2 instance, configuring its instance type, selecting an Ubuntu AMI, and assigning a custom name through AWS resource tags.

I also practiced managing the Terraform workflow, from initialization and execution to destroying the infrastructure after successful deployment.

## Technologies Used

- **Cloud Provider:** Amazon Web Services (AWS)
- **Infrastructure as Code:** Terraform
- **Compute Service:** Amazon EC2
- **Operating System:** Ubuntu 20.04 LTS
- **Instance Type:** t3.micro
- **AWS Region:** Asia Pacific (Sydney) — `ap-southeast-2`

## AWS IAM User & Permissions

Used a dedicated **AWS IAM User** to authenticate Terraform with AWS. Attached the following managed policies to support current and future AWS projects:

- `AmazonEC2FullAccess`
- `AmazonRDSFullAccess`
- `IAMFullAccess`
- `AmazonS3FullAccess`
- `AmazonDynamoDBFullAccess`
- `AmazonRoute53FullAccess`

**Note:** These permissions were configured for learning and future hands-on projects. Production environments should follow the Principle of Least Privilege.

## Project Architecture

The project provisions the following AWS resource:

| Resource      | Configuration             |
| ------------- | ------------------------- |
| EC2 Instance  | Amazon EC2                |
| AMI           | Ubuntu 20.04 LTS          |
| Instance Type | t3.micro                  |
| Region        | ap-southeast-2            |
| Instance Name | My-Terraform-EC2-Instance |

## Project Structure

```text
terraform-ec2-project/
│
├── main.tf
├── .terraform.lock.hcl
├── .gitignore
└── README.md
```

## Terraform Configuration

The following Terraform configuration was used to provision the EC2 instance.

**main.tf**

```hcl
terraform {
  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "~> 3.0"
    }
  }
}

provider "aws" {
  region = "ap-southeast-2"
}

resource "aws_instance" "aws_instance" {
  ami           = "ami-0dd60a46ecc6eac16" # Ubuntu 20.04 LTS // ap-southeast-2
  instance_type = "t3.micro"

  tags = {
    Name = "My-Terraform-EC2-Instance"
  }
}
```

## Deployment Steps

### 1. Configure AWS Credentials

Before running Terraform, configure AWS credentials using the AWS CLI.

```bash
aws configure
```

Provide your AWS Access Key, Secret Access Key, default region, and output format.

Ensure your IAM identity has the required permissions and that no AWS Organizations SCP explicitly denies the required operations.

### 2. Initialize Terraform

```bash
terraform init
```

Initializes the Terraform working directory and downloads the required AWS provider plugin.

### 3. Review the Execution Plan

```bash
terraform plan
```

Generates an execution plan showing the infrastructure Terraform intends to create.

### 4. Deploy the EC2 Instance

```bash
terraform apply
```

Creates the EC2 instance using the configuration defined in `main.tf`.

Confirm the deployment when prompted.

### 5. Verify the EC2 Instance

After successful deployment, navigate to:

**AWS Console → EC2 → Instances**

Verify the following:

- Instance state: Running
- Instance type: t3.micro
- AMI: Ubuntu 20.04 LTS
- Name: My-Terraform-EC2-Instance

## Infrastructure Cleanup

After verifying that the EC2 instance was successfully created, I used the following command to remove the infrastructure.

```bash
terraform destroy
```

Terraform identifies the resources it manages and destroys them after confirmation.

This helps avoid unnecessary AWS resource charges.

n What I Learned

Through this hands-oproject, I gained practical experience with:

- Understanding Infrastructure as Code (IaC).
- Configuring Terraform with the AWS provider.
- Initializing Terraform using `terraform init`.
- Reviewing infrastructure changes using `terraform plan`.
- Provisioning AWS EC2 instances using `terraform apply`.
- Defining EC2 instance properties such as AMI and instance type.
- Assigning resource tags for better identification.
- Managing infrastructure lifecycle using `terraform destroy`.
- Understanding basic Terraform and AWS deployment troubleshooting.

## Important Notes

- AWS credentials should never be hardcoded into Terraform configuration files or uploaded to GitHub.
- The AMI ID used in this project is specific to the AWS region and architecture.
- AWS resources may incur charges while they are running.
- The infrastructure was destroyed after successful testing.

## Author

**Vineet Vikram Rao**

---

*This project is part of my hands-on learning journey in AWS Cloud Computing, Terraform, and Infrastructure as Code.*

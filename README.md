Automating Amazon S3 Bucket Deployment with Terraform

This project demonstrates how to use Terraform to provision an Amazon S3 bucket end‑to‑end, including environment setup, AWS authentication, bucket creation, access‑control configuration, and object upload. It reflects my hands‑on learning with Infrastructure‑as‑Code (IaC) and AWS cloud automation. 

<img width="941" height="587" alt="Screenshot 2026-04-28 234304" src="https://github.com/user-attachments/assets/3fab5765-6373-4189-b23d-21d03dde5847" />

Project Overview 

Using Terraform, I automated the creation of: 

A secure, private S3 bucket 

A public access block to enforce security 

A tagged bucket for easy identification 

An uploaded S3 object managed as part of Terraform state 

This project helped me understand how Terraform interacts with AWS services and how IaC enables consistent, repeatable cloud deployments. 

Tools & Technologies 

Terraform (Infrastructure‑as‑Code) 

Amazon S3 

AWS IAM (Access keys for authentication) 

AWS CLI (Local credential configuration) 

Windows Terminal / PowerShell 

Project Structure 

Code 

network-terraform/ 
│ 
├── main.tf 
└── image.png 
 

main.tf includes three core blocks: 

Provider Block Configures AWS as the provider and sets the region. 

S3 Bucket Resource Creates a globally unique S3 bucket. 

Public Access Block Ensures the bucket is fully private. 

S3 Object Resource Uploads image.png into the bucket. 

Terraform Configuration (main.tf) 

hcl 

provider "aws" { 
 region = "your-region-code" 
} 
 
resource "aws_s3_bucket" "my_bucket" { 
 bucket = "nextwork-unique-bucket-danfordwilliams-1714" 
 
 tags = { 
   Project = "Create an S3 Bucket with Terraform" 
 } 
} 
 
resource "aws_s3_bucket_public_access_block" "my_bucket_public_access_block" { 
 bucket                  = aws_s3_bucket.my_bucket.id 
 block_public_acls       = true 
 ignore_public_acls      = true 
 block_public_policy     = true 
 restrict_public_buckets = true 
} 
 
resource "aws_s3_object" "image" { 
 bucket = aws_s3_bucket.my_bucket.id 
 key    = "image.png" 
 source = "image.png" 
} 
 

Deployment Workflow 

1. Initialize Terraform 

Code 

terraform init 
 

2. Fix Missing Credentials  

Terraform initially returned: 

“no valid credentials found” 

I resolved this by configuring AWS CLI: 

Code 

aws configure 
 

3. Preview Changes 

Code 

terraform plan 
 

4. Apply the Configuration 

Code 

terraform apply 
 

Terraform created: 

The S3 bucket 

The public access block 

The uploaded object (after updating the config) 

Validation 

I verified the deployment by: 

Opening the AWS S3 console 

Confirming the bucket was created 

Checking that tags were applied 

Ensuring the uploaded image appeared in the bucket 

Downloading the object to confirm integrity 

Key Learnings 

How Terraform manages desired vs. actual state 

How AWS IAM credentials enable Terraform authentication 

How S3 buckets and objects are separate resources 

How to debug Terraform errors (e.g., missing credentials) 

Importance of the init → plan → apply workflow 

Future Improvements 

Add versioning to the S3 bucket 

Add lifecycle rules 

Move resources into reusable Terraform modules 

Add remote backend for Terraform state 

Integrate CI/CD for automated deployments 

Author 

Danford Amos Project: Create S3 Buckets with Terraform 

 

 
---

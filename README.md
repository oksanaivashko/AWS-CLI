# AWS-CLI

### What is CLI?
- CLI is a commend-linen program that accept input to execute functions (API to AWS). 
- AWS provides us the option of accessing thir user services with CLI.

### Why use AWS CLI?
- Save time - Acton are in the command vs clicking on th console.
- Less human errors
- Automation 

### 
- GUI - Grafical User Interface
- CLI - Command line Interface
- SDK - Softaware Development Environment 
- IDE - Integrade Development Environment 
- Tools - VS Code, Eclipse, Atom

### AWS-CLI 

- aws configure - configure your aws with the region, access secret id and access secret key. 

- aws s3 ls - list all bucket 

### To create a bucket outside of the ``us-east-1`` region 

The following create-bucket example creates a bucket named my-bucket in the eu-west-1 region. Regions outside of us-east-1 require the appropriate LocationConstraint to be specified in order to create the bucket in the desired region. 

~~~
aws s3api create-bucket \ 
    --bucket my-bucket \ 
    --region eu-west-1 \ 
    --create-bucket-configuration LocationConstraint=eu-west-1 
    

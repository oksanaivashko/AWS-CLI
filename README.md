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

~~~

    
    

### To create an IAM role and instance profile (AWS CLI)

Create the following trust policy and save it in a text file named ec2-role-trust-policy.json.

~~~


{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": { "Service": "ec2.amazonaws.com"},
      "Action": "sts:AssumeRole"
    }
  ]
}

~~~

### Create the IAM Instance Role 


~~~
aws iam create-role \
    --role-name iamInstanceRole \
    --assume-role-policy-document file://ec2-role-trust-policy.jason
~~~



### To create a security group for ec2 Instance

This example creates a security group named InstanceRoleSecurityGroup 

~~~

aws ec2 create-security-group
 --group-name InstanceRoleSecurityGroup
 --description "This group to allow traffic for InstanceRoleSecurityGroup " 
 ~~~

### To get information about an IAM role 

- The following get-role command gets information about the role named Test-Role: 

~~~
aws iam get-role \ 
    --role-name
~~~

### Finding your security group (SG) IDs 

 
- Amazon EC2 create and OpenSearch create domain CTs require a security group ID. This will be in the form sg-02ce123456e7893c7.  To discover your security groups: 

- AWS Console: Use the EC2 or VPC console to view all security groups for the selected VPC. 

API/CLI (when logged into your AMS account): 

List your security groups thru AWS-CLI 
~~~

aws ec2 describe-security-groups
~~~

Create ec2 with AWS-CLI 
~~~

aws ec2 run-instances \ 

    --image-id ami-0b5eea76982371e91 \ 

    --count 1 \ 

    --instance-type t2.micro \ 

    --key-name your@key \ 

    --security-group-ids sg-089ac8cb2447d8c78 \ 

    --subnet-id subnet-0d3173490a9b6aa5d \ 
~~~

### Attach the IAM role to an existing EC2 instance that was originally launched without an IAM role 

- You are now ready to attach the IAM role, YourNewRole, to the EC2 instance, YourInstanceId. To attach the role: 

Call the associate-iam-instance-profile command to attach the instance profile, YourNewRole-Instance-Profile, for the newly created IAM role, YourNewRole, to your EC2 instance, YourInstanceId. 

~~~

aws ec2 associate-iam-instance-profile 
--instance-id i-0a72edd38d0d7067c
--iam-instance-profile Name=aimInstanceRole
~~~

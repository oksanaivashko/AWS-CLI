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

- configure your AWS-CLI with the region, access secret id and access secret key
~~~
aws configure
~~~
- to list your config file
~~~
ls ~/.aws/config
~~~

- to read your config file 
~~~

cat ~/.aws/config  
~~~

### S3 Bucket

- list all bucket 
~~~
aws s3 ls
~~~
- To list all the files inside S3 bucket
~~~
aws mb s3://bucketName
~~~
- To copy file to S3 Bucket 
~~~
aws s3 cp LocalfileName s3://bucketName
~~~


- To create a bucket outside of the ``us-east-1`` region 

(The following create-bucket example creates a bucket named my-bucket in the eu-west-1 region. Regions outside of us-east-1 require the appropriate LocationConstraint to be specified in order to create the bucket in the desired region.)

~~~
aws s3api create-bucket \ 
    --bucket my-bucket \ 
    --region eu-west-1 \ 
    --create-bucket-configuration LocationConstraint=eu-west-1 

~~~

    
    

### Create an IAM role and instance profile (AWS CLI)

- Create the following trust policy and save it in a text file named "ec2-role-trust-policy.json"

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
- Now, once we have the policies created, we can create IAM Instance Role 
~~~
aws iam create-role --role-name IamInstanceRole --assume-role-policy-document file://ec2-role-trust-policy.jason
~~~



~~~
aws iam create-role \
    --role-name iamInstanceRole \
    --assume-role-policy-document file://ec2-role-trust-policy.jason
~~~



### Create a security group for ec2 Instance

- This example creates a security group named InstanceRoleSecurityGroup 

~~~
aws ec2 create-security-group
 --group-name InstanceRoleSecurityGroup
 --description "This group to allow traffic for InstanceRoleSecurityGroup " 
 ~~~
### To add a rule that allows inbound SSH traffic

- The following example enables inbound traffic on TCP port 22 (SSH). If the command succeeds, no output is returned.

~~~
aws ec2 authorize-security-group-ingress \
    --group-name MySecurityGroup \
    --protocol tcp \
    --port 22 \
    --cidr 0.0.0.0\24
~~~


### To get information about an IAM role 

- The following get-role command gets information about the role named iamInstanceRole

~~~
aws iam get-role \ 
    --role-name iamInstanceRole
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
- With this command you will create ec2 Instance with the existing security group that was created on the previos command 
### These command assume: 
 
- you have an existing security group (was created with the previous command)
- you have ssh key on aws your console
~~~

aws ec2 run-instances --image-id ami-0b5eea76982371e91 --count 1 --instance-type t2.micro --key-name windows@key --security-group-ids sg-0e78ef54c22022dff  --subnet-id subnet-0d3173490a9b6aa5d 
~~~

### Attach the IAM role to an existing EC2 instance that was originally created without an IAM role ( on the previous command)


- You are now ready to attach the IAM role, YourNewRole, to the EC2 instance, YourInstanceId. To attach the role: 

- Call the associate-iam-instance-profile command to attach the instance profile, YourNewRole-Instance-Profile, for the newly created IAM role, YourNewRole, to your EC2 instance, YourInstanceId. 

~~~

aws ec2 associate-iam-instance-profile 
--instance-id i-0a72edd38d0d7067c
--iam-instance-profile Name=aimInstanceRole
~~~

### Delete security group
~~~
aws ec2 delete-security-group --group-id sg-089ac8cb2447d8c78
~~~

### Delete ec2 instance

~~~
aws ec2 terminate-instances --instance-ids i-0474562cd25bf8275
~~~
- Create Instance profile 

~~~
aws iam create-instance-profile --instance-profile-name AWS-CLI-Instance
~~~

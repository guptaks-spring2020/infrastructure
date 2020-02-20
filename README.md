# infrastructure

AWS CloudFormation:
AWS Networking Setup:

Here what you need to do for networking infrastructure setup:

1. Create Virtual Private Cloud (VPC).
2. Create subnets in your VPC. You must create 3 subnets, each in different availability zone in the same region in the same VPC.
3. Create Internet Gateway resource. and attach the Internet Gateway to the VPC.
4. Create a public route table. Attach all subnets created above to the route table.
5. Create a public route in the public route table created above with destination CIDR block 0.0.0.0/0 and internet gateway created above as the target.

Expected Command Line Arguments:

Variables should be declared for following properties. Values are provided as command line arguments at run time. For any property not listed below, you may set default values for them.

1. AWS region
2. VPC CIDR block
3. Subnets CIDR block
4. VPC name

Infrastructure as Code with AWS CloudFormation:

    Install and setup AWS command line interface
    Create CloudFormation template networking.json or networking.yaml that can be used to setup required networking resources

AWS-CLI Instructions:
Install AWS-CLI:

curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"

unzip awscliv2.zip

sudo ./aws/install
Configure AWS-CLI:

aws configure profile [profile-name]
Create CloudFormation stack:

aws cloudformation create-stack \

--stack-name [stack-name] \

--parameters [networking_parameters.json filepath]\

--template-body [networking.yaml filepath] \

--region [region-name] \

--profile [profile-name]
Delete CloudFormation stack:

aws cloudformation delete-stack \

--stack-name [stack-name] \

--profile [profile-name]
Wait for CloudFormation Stack Deletion

aws cloudformation wait stack-delete-complete

--stack-name [stack-name]
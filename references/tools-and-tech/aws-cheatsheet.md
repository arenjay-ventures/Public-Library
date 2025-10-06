---
layout: default
title: AWS Cheatsheet
parent: Tools & Technology
grand_parent: References
nav_order: 10
---

# AWS Cheatsheet

## **What is AWS?**

Amazon Web Services (AWS) is a comprehensive cloud computing platform offering over 200 services. It's essential for:
- **Cloud Computing**: Scalable infrastructure and services
- **DevOps**: CI/CD, automation, monitoring
- **Data Analytics**: Big data processing and machine learning
- **Career Growth**: High demand for AWS-certified professionals
- **Cost Optimization**: Pay-as-you-go pricing model

## **Getting Started**

### **AWS Account Setup**
1. **Create Account**: [aws.amazon.com](https://aws.amazon.com/)
2. **Enable MFA**: Multi-factor authentication for security
3. **Set Billing Alerts**: Monitor costs and prevent surprises
4. **Create IAM User**: Don't use root account for daily operations
5. **Configure CLI**: Install and configure AWS CLI

### **AWS CLI Installation**
```bash
# Install AWS CLI
pip install awscli

# Configure credentials
aws configure
# Enter: Access Key ID, Secret Access Key, Region, Output format

# Verify configuration
aws sts get-caller-identity
```

## **Core Services**

### **EC2 (Elastic Compute Cloud)**
**Virtual servers in the cloud**

#### **Key Concepts**
- **Instances**: Virtual machines
- **AMIs**: Amazon Machine Images (templates)
- **Security Groups**: Virtual firewalls
- **Key Pairs**: SSH access authentication

#### **Common Commands**
```bash
# List instances
aws ec2 describe-instances

# Launch instance
aws ec2 run-instances \
    --image-id ami-0abcdef1234567890 \
    --instance-type t2.micro \
    --key-name my-key-pair \
    --security-group-ids sg-12345678

# Start/stop instances
aws ec2 start-instances --instance-ids i-1234567890abcdef0
aws ec2 stop-instances --instance-ids i-1234567890abcdef0

# Terminate instance
aws ec2 terminate-instances --instance-ids i-1234567890abcdef0
```

#### **Instance Types**
- **t2.micro**: Free tier, 1 vCPU, 1 GB RAM
- **t3.small**: 2 vCPU, 2 GB RAM
- **m5.large**: 2 vCPU, 8 GB RAM
- **c5.xlarge**: 4 vCPU, 8 GB RAM (compute optimized)

### **S3 (Simple Storage Service)**
**Object storage for files and data**

#### **Key Concepts**
- **Buckets**: Containers for objects
- **Objects**: Files stored in buckets
- **Regions**: Geographic locations
- **Storage Classes**: Different pricing tiers

#### **Common Commands**
```bash
# List buckets
aws s3 ls

# Create bucket
aws s3 mb s3://my-bucket-name

# Upload file
aws s3 cp local-file.txt s3://my-bucket-name/

# Download file
aws s3 cp s3://my-bucket-name/file.txt ./

# Sync directory
aws s3 sync ./local-folder s3://my-bucket-name/

# Remove object
aws s3 rm s3://my-bucket-name/file.txt

# Delete bucket
aws s3 rb s3://my-bucket-name --force
```

#### **Storage Classes**
- **Standard**: General purpose, frequently accessed
- **IA (Infrequent Access)**: Lower cost for infrequent access
- **Glacier**: Long-term archival storage
- **Glacier Deep Archive**: Lowest cost for long-term retention

### **RDS (Relational Database Service)**
**Managed database service**

#### **Supported Engines**
- **MySQL**: Popular open-source database
- **PostgreSQL**: Advanced open-source database
- **MariaDB**: MySQL-compatible database
- **Oracle**: Enterprise database
- **SQL Server**: Microsoft database
- **Aurora**: AWS-optimized MySQL/PostgreSQL

#### **Common Commands**
```bash
# List DB instances
aws rds describe-db-instances

# Create DB instance
aws rds create-db-instance \
    --db-instance-identifier mydb \
    --db-instance-class db.t2.micro \
    --engine mysql \
    --master-username admin \
    --master-user-password mypassword

# Create DB snapshot
aws rds create-db-snapshot \
    --db-instance-identifier mydb \
    --db-snapshot-identifier mydb-snapshot
```

### **Lambda (Serverless Computing)**
**Run code without managing servers**

#### **Key Concepts**
- **Functions**: Code that runs in response to events
- **Triggers**: Events that invoke functions
- **Runtime**: Programming language environment
- **Layers**: Shared code and libraries

#### **Common Commands**
```bash
# List functions
aws lambda list-functions

# Create function
aws lambda create-function \
    --function-name my-function \
    --runtime python3.9 \
    --role arn:aws:iam::123456789012:role/lambda-role \
    --handler index.handler \
    --zip-file fileb://function.zip

# Invoke function
aws lambda invoke \
    --function-name my-function \
    --payload '{"key": "value"}' \
    response.json
```

### **VPC (Virtual Private Cloud)**
**Isolated network environment**

#### **Key Components**
- **Subnets**: Network segments within VPC
- **Route Tables**: Control traffic routing
- **Internet Gateway**: Internet access for VPC
- **NAT Gateway**: Outbound internet access for private subnets
- **Security Groups**: Instance-level firewall
- **NACLs**: Subnet-level firewall

#### **Common Commands**
```bash
# List VPCs
aws ec2 describe-vpcs

# Create VPC
aws ec2 create-vpc --cidr-block 10.0.0.0/16

# Create subnet
aws ec2 create-subnet \
    --vpc-id vpc-12345678 \
    --cidr-block 10.0.1.0/24 \
    --availability-zone us-east-1a

# Create internet gateway
aws ec2 create-internet-gateway
aws ec2 attach-internet-gateway \
    --vpc-id vpc-12345678 \
    --internet-gateway-id igw-12345678
```

## **Security & Identity**

### **IAM (Identity and Access Management)**
**Manage users, groups, and permissions**

#### **Key Concepts**
- **Users**: Individual accounts
- **Groups**: Collections of users
- **Roles**: Permissions for services
- **Policies**: Permission documents

#### **Common Commands**
```bash
# List users
aws iam list-users

# Create user
aws iam create-user --user-name myuser

# Create access key
aws iam create-access-key --user-name myuser

# Attach policy to user
aws iam attach-user-policy \
    --user-name myuser \
    --policy-arn arn:aws:iam::aws:policy/AmazonS3ReadOnlyAccess

# Create role
aws iam create-role \
    --role-name myrole \
    --assume-role-policy-document file://trust-policy.json
```

#### **Best Practices**
- **Principle of Least Privilege**: Grant minimum required permissions
- **Use Roles**: Prefer roles over access keys
- **Enable MFA**: Multi-factor authentication
- **Regular Audits**: Review permissions regularly

### **Security Groups**
**Virtual firewalls for EC2 instances**

```bash
# Create security group
aws ec2 create-security-group \
    --group-name my-security-group \
    --description "My security group"

# Add inbound rule
aws ec2 authorize-security-group-ingress \
    --group-id sg-12345678 \
    --protocol tcp \
    --port 22 \
    --cidr 0.0.0.0/0

# Add outbound rule
aws ec2 authorize-security-group-egress \
    --group-id sg-12345678 \
    --protocol tcp \
    --port 80 \
    --cidr 0.0.0.0/0
```

## **Monitoring & Logging**

### **CloudWatch**
**Monitoring and observability service**

#### **Key Features**
- **Metrics**: Performance data
- **Logs**: Application and system logs
- **Alarms**: Automated responses to metrics
- **Dashboards**: Visual monitoring

#### **Common Commands**
```bash
# List metrics
aws cloudwatch list-metrics

# Get metric statistics
aws cloudwatch get-metric-statistics \
    --namespace AWS/EC2 \
    --metric-name CPUUtilization \
    --dimensions Name=InstanceId,Value=i-1234567890abcdef0 \
    --start-time 2023-01-01T00:00:00Z \
    --end-time 2023-01-01T23:59:59Z \
    --period 3600 \
    --statistics Average

# Create alarm
aws cloudwatch put-metric-alarm \
    --alarm-name "High CPU Usage" \
    --alarm-description "Alarm when CPU exceeds 80%" \
    --metric-name CPUUtilization \
    --namespace AWS/EC2 \
    --statistic Average \
    --period 300 \
    --threshold 80 \
    --comparison-operator GreaterThanThreshold
```

### **CloudTrail**
**Audit and compliance logging**

```bash
# List trails
aws cloudtrail describe-trails

# Create trail
aws cloudtrail create-trail \
    --name my-trail \
    --s3-bucket-name my-cloudtrail-bucket

# Start logging
aws cloudtrail start-logging --name my-trail
```

## **DevOps & Automation**

### **CodeDeploy**
**Automated application deployments**

```bash
# Create application
aws deploy create-application \
    --application-name my-app

# Create deployment group
aws deploy create-deployment-group \
    --application-name my-app \
    --deployment-group-name my-group \
    --service-role-arn arn:aws:iam::123456789012:role/CodeDeployRole

# Create deployment
aws deploy create-deployment \
    --application-name my-app \
    --deployment-group-name my-group \
    --s3-location bucket=my-bucket,key=my-app.zip,bundleType=zip
```

### **CloudFormation**
**Infrastructure as Code**

```yaml
# template.yaml
AWSTemplateFormatVersion: '2010-09-09'
Resources:
  MyEC2Instance:
    Type: AWS::EC2::Instance
    Properties:
      ImageId: ami-0abcdef1234567890
      InstanceType: t2.micro
      SecurityGroups:
        - !Ref MySecurityGroup
  
  MySecurityGroup:
    Type: AWS::EC2::SecurityGroup
    Properties:
      GroupDescription: My security group
      SecurityGroupIngress:
        - IpProtocol: tcp
          FromPort: 22
          ToPort: 22
          CidrIp: 0.0.0.0/0
```

```bash
# Deploy stack
aws cloudformation create-stack \
    --stack-name my-stack \
    --template-body file://template.yaml

# Update stack
aws cloudformation update-stack \
    --stack-name my-stack \
    --template-body file://template.yaml

# Delete stack
aws cloudformation delete-stack --stack-name my-stack
```

## **Cost Optimization**

### **Cost Management**
```bash
# Get cost and usage
aws ce get-cost-and-usage \
    --time-period Start=2023-01-01,End=2023-01-31 \
    --granularity MONTHLY \
    --metrics BlendedCost

# List cost allocation tags
aws ce list-cost-allocation-tags

# Get cost forecast
aws ce get-cost-forecast \
    --time-period Start=2023-02-01,End=2023-02-28 \
    --metric BLENDED_COST \
    --granularity MONTHLY
```

### **Cost Optimization Strategies**
- **Right-sizing**: Match instance types to workload
- **Reserved Instances**: 1-3 year commitments for discounts
- **Spot Instances**: Use spare capacity for cost savings
- **S3 Lifecycle**: Automatically transition storage classes
- **Auto Scaling**: Scale resources based on demand

## **Best Practices**

### **Security**
- **Enable CloudTrail**: Audit all API calls
- **Use IAM Roles**: Avoid hardcoded credentials
- **Encrypt Data**: Use KMS for encryption
- **Network Security**: Use VPCs and security groups
- **Regular Updates**: Keep systems patched

### **Cost Management**
- **Set Budgets**: Monitor and control spending
- **Use Tags**: Organize and track resources
- **Regular Reviews**: Audit unused resources
- **Reserved Instances**: For predictable workloads

### **Operational Excellence**
- **Infrastructure as Code**: Use CloudFormation/Terraform
- **Monitoring**: Set up comprehensive monitoring
- **Backup**: Regular backups and disaster recovery
- **Documentation**: Maintain up-to-date documentation

## **Learning Resources**

### **Documentation**
- **[AWS Documentation](https://docs.aws.amazon.com/)** - Official documentation
- **[AWS Well-Architected Framework](https://aws.amazon.com/architecture/well-architected/)** - Best practices
- **[AWS Architecture Center](https://aws.amazon.com/architecture/)** - Reference architectures

### **Training**
- **[AWS Training](https://aws.amazon.com/training/)** - Official training
- **[AWS re:Invent](https://reinvent.awsevents.com/)** - Annual conference
- **[AWS YouTube Channel](https://www.youtube.com/user/AmazonWebServices)** - Video content

### **Certifications**
- **Cloud Practitioner**: Entry-level certification
- **Solutions Architect**: Design distributed systems
- **Developer**: Develop and maintain applications
- **SysOps Administrator**: Deploy and manage systems
- **DevOps Engineer**: Automate and optimize processes

### **Practice**
- **[AWS Free Tier](https://aws.amazon.com/free/)** - Free services for learning
- **[AWS Hands-on Labs](https://aws.amazon.com/training/learning-paths/)** - Guided practice
- **[AWS Well-Architected Labs](https://wellarchitectedlabs.com/)** - Hands-on exercises

Remember: **AWS is vast - start with the fundamentals**. Master EC2, S3, and IAM first, then expand to other services based on your needs. Always follow security best practices and monitor costs. The AWS ecosystem is constantly evolving, so stay updated with new services and features!
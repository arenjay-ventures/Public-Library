---
layout: default
title: Google Cloud Cheatsheet
parent: Tools & Technology
grand_parent: References
nav_order: 12
---

# Google Cloud Cheatsheet

## **What is Google Cloud Platform (GCP)?**

Google Cloud Platform is a suite of cloud computing services that runs on the same infrastructure that Google uses internally. It's essential for:
- **Cloud Computing**: Scalable infrastructure and services
- **Data Analytics**: BigQuery, Dataflow, Pub/Sub
- **Machine Learning**: AI Platform, AutoML, TensorFlow
- **Kubernetes**: Google Kubernetes Engine (GKE)
- **Career Growth**: Growing demand for GCP-certified professionals

## **Getting Started**

### **GCP Account Setup**
1. **Create Account**: [cloud.google.com](https://cloud.google.com/)
2. **Free Tier**: $300 credit for 90 days
3. **Set Billing Alerts**: Monitor costs and prevent surprises
4. **Create Projects**: Organize resources logically
5. **Configure CLI**: Install and configure gcloud CLI

### **gcloud CLI Installation**
```bash
# Install gcloud CLI
# Windows: Download from cloud.google.com/sdk
# macOS: brew install google-cloud-sdk
# Linux: curl https://sdk.cloud.google.com | bash

# Initialize gcloud
gcloud init

# Set project
gcloud config set project PROJECT_ID

# Verify configuration
gcloud config list
gcloud auth list
```

## **Core Services**

### **Compute Engine**
**Virtual machines in the cloud**

#### **Key Concepts**
- **Machine Types**: E2 (general purpose), N1 (legacy), N2 (high performance)
- **Images**: Public images, custom images, family images
- **Preemptible VMs**: Cost-effective, short-lived instances
- **Sustained Use Discounts**: Automatic discounts for long-running VMs

#### **Common Commands**
```bash
# List instances
gcloud compute instances list

# Create instance
gcloud compute instances create my-instance \
    --zone=us-central1-a \
    --machine-type=e2-medium \
    --image-family=ubuntu-2004-lts \
    --image-project=ubuntu-os-cloud \
    --boot-disk-size=10GB \
    --boot-disk-type=pd-standard

# Start/stop instance
gcloud compute instances start my-instance --zone=us-central1-a
gcloud compute instances stop my-instance --zone=us-central1-a

# Delete instance
gcloud compute instances delete my-instance --zone=us-central1-a
```

#### **Machine Types**
- **e2-micro**: 1 vCPU, 1 GB RAM (free tier)
- **e2-small**: 2 vCPU, 2 GB RAM
- **e2-medium**: 2 vCPU, 4 GB RAM
- **e2-standard-4**: 4 vCPU, 16 GB RAM
- **n1-standard-1**: 1 vCPU, 3.75 GB RAM

### **Cloud Storage**
**Object storage for files and data**

#### **Storage Classes**
- **Standard**: Frequently accessed data
- **Nearline**: Infrequently accessed data (30+ days)
- **Coldline**: Infrequently accessed data (90+ days)
- **Archive**: Long-term archival (365+ days)

#### **Common Commands**
```bash
# Create bucket
gsutil mb gs://my-bucket-name

# List buckets
gsutil ls

# Upload file
gsutil cp local-file.txt gs://my-bucket-name/

# Download file
gsutil cp gs://my-bucket-name/remote-file.txt ./

# Sync directory
gsutil -m rsync -r ./local-folder gs://my-bucket-name/

# Set storage class
gsutil rewrite -s nearline gs://my-bucket-name/file.txt

# Delete object
gsutil rm gs://my-bucket-name/file.txt
```

### **Cloud SQL**
**Managed relational database service**

#### **Database Engines**
- **MySQL**: Popular open-source database
- **PostgreSQL**: Advanced open-source database
- **SQL Server**: Microsoft database
- **SQL Server Express**: Free edition

#### **Common Commands**
```bash
# Create Cloud SQL instance
gcloud sql instances create my-instance \
    --database-version=MYSQL_8_0 \
    --tier=db-f1-micro \
    --region=us-central1

# Create database
gcloud sql databases create my-database --instance=my-instance

# Create user
gcloud sql users create my-user \
    --instance=my-instance \
    --password=MyPassword123!

# Connect to instance
gcloud sql connect my-instance --user=my-user --database=my-database
```

### **Cloud Functions**
**Serverless compute service**

#### **Key Concepts**
- **Triggers**: HTTP, Cloud Storage, Pub/Sub, Firestore
- **Runtime**: Node.js, Python, Go, Java, .NET
- **Memory**: 128 MB to 8 GB
- **Timeout**: Up to 9 minutes

#### **Common Commands**
```bash
# Deploy function
gcloud functions deploy my-function \
    --runtime nodejs18 \
    --trigger-http \
    --allow-unauthenticated \
    --source=./function-source

# List functions
gcloud functions list

# Call function
gcloud functions call my-function

# Delete function
gcloud functions delete my-function
```

### **App Engine**
**Platform for web applications**

#### **App Engine Environments**
- **Standard**: Managed runtime environment
- **Flexible**: Custom runtime environment

#### **Common Commands**
```bash
# Deploy app
gcloud app deploy

# Deploy specific service
gcloud app deploy service.yaml

# View app
gcloud app browse

# List services
gcloud app services list

# Set traffic split
gcloud app services set-traffic default --splits=version=1.0,version=2.0=0.5
```

## **Networking**

### **Virtual Private Cloud (VPC)**
**Isolated network environment**

#### **Key Components**
- **Subnets**: Network segments within VPC
- **Firewall Rules**: Control traffic
- **Routes**: Custom routing
- **Load Balancers**: Distribute traffic
- **Cloud NAT**: Outbound internet access

#### **Common Commands**
```bash
# Create VPC
gcloud compute networks create my-vpc \
    --subnet-mode=custom

# Create subnet
gcloud compute networks subnets create my-subnet \
    --network=my-vpc \
    --range=10.0.1.0/24 \
    --region=us-central1

# Create firewall rule
gcloud compute firewall-rules create allow-ssh \
    --network=my-vpc \
    --allow=tcp:22 \
    --source-ranges=0.0.0.0/0

# Create load balancer
gcloud compute forwarding-rules create my-load-balancer \
    --global \
    --target-http-proxy=my-http-proxy \
    --ports=80
```

### **Cloud Load Balancing**
**Distribute incoming traffic**

```bash
# Create health check
gcloud compute health-checks create http my-health-check \
    --port=80 \
    --request-path=/health

# Create backend service
gcloud compute backend-services create my-backend-service \
    --protocol=HTTP \
    --health-checks=my-health-check \
    --global

# Add backend to service
gcloud compute backend-services add-backend my-backend-service \
    --instance-group=my-instance-group \
    --global
```

## **Security & Identity**

### **Identity and Access Management (IAM)**
**Manage users, groups, and permissions**

#### **Key Concepts**
- **Members**: Users, groups, service accounts
- **Roles**: Collections of permissions
- **Resources**: Projects, folders, organizations
- **Policies**: Bindings between members and roles

#### **Common Commands**
```bash
# List IAM policies
gcloud projects get-iam-policy PROJECT_ID

# Add IAM policy binding
gcloud projects add-iam-policy-binding PROJECT_ID \
    --member="user:user@example.com" \
    --role="roles/storage.admin"

# Create service account
gcloud iam service-accounts create my-service-account \
    --display-name="My Service Account"

# Create service account key
gcloud iam service-accounts keys create key.json \
    --iam-account=my-service-account@PROJECT_ID.iam.gserviceaccount.com
```

### **Cloud KMS**
**Key management service**

```bash
# Create keyring
gcloud kms keyrings create my-keyring \
    --location=global

# Create key
gcloud kms keys create my-key \
    --keyring=my-keyring \
    --location=global \
    --purpose=encryption

# Encrypt data
echo "sensitive data" | gcloud kms encrypt \
    --key=my-key \
    --keyring=my-keyring \
    --location=global \
    --plaintext-file=- \
    --ciphertext-file=encrypted.txt

# Decrypt data
gcloud kms decrypt \
    --key=my-key \
    --keyring=my-keyring \
    --location=global \
    --ciphertext-file=encrypted.txt \
    --plaintext-file=decrypted.txt
```

## **Monitoring & Logging**

### **Cloud Monitoring**
**Comprehensive monitoring solution**

#### **Key Features**
- **Metrics**: Performance data
- **Logs**: Application and system logs
- **Alerts**: Automated responses to conditions
- **Dashboards**: Visual monitoring

#### **Common Commands**
```bash
# Create uptime check
gcloud monitoring uptime create \
    --display-name="My Uptime Check" \
    --http-check-path="/health" \
    --http-check-port=80 \
    --http-check-use-ssl=false

# Create alerting policy
gcloud alpha monitoring policies create \
    --policy-from-file=alert-policy.yaml

# List metrics
gcloud logging read "resource.type=gce_instance"
```

### **Cloud Logging**
**Centralized logging service**

```bash
# View logs
gcloud logging read "resource.type=gce_instance" --limit=50

# Export logs
gcloud logging export my-export \
    --destination=gs://my-bucket/logs/ \
    --log-filter="resource.type=gce_instance"

# Create log sink
gcloud logging sinks create my-sink \
    gs://my-bucket/logs/ \
    --log-filter="resource.type=gce_instance"
```

## **Data & Analytics**

### **BigQuery**
**Data warehouse and analytics**

#### **Key Features**
- **SQL Queries**: Standard SQL interface
- **Data Transfer**: Automated data ingestion
- **Machine Learning**: Built-in ML capabilities
- **Real-time Analytics**: Streaming data processing

#### **Common Commands**
```bash
# Create dataset
bq mk --dataset PROJECT_ID:my_dataset

# Create table
bq mk --table PROJECT_ID:my_dataset.my_table schema.json

# Query data
bq query --use_legacy_sql=false \
    "SELECT * FROM \`PROJECT_ID.my_dataset.my_table\` LIMIT 10"

# Export data
bq extract PROJECT_ID:my_dataset.my_table gs://my-bucket/data.csv

# Load data
bq load --source_format=CSV \
    PROJECT_ID:my_dataset.my_table \
    gs://my-bucket/data.csv \
    schema.json
```

### **Cloud Dataflow**
**Stream and batch data processing**

```bash
# Run Dataflow job
gcloud dataflow jobs run my-job \
    --gcs-location=gs://my-bucket/templates/WordCount \
    --parameters=inputFile=gs://my-bucket/input.txt,output=gs://my-bucket/output

# List jobs
gcloud dataflow jobs list

# Cancel job
gcloud dataflow jobs cancel JOB_ID
```

### **Pub/Sub**
**Messaging and event streaming**

```bash
# Create topic
gcloud pubsub topics create my-topic

# Create subscription
gcloud pubsub subscriptions create my-subscription \
    --topic=my-topic

# Publish message
gcloud pubsub topics publish my-topic \
    --message="Hello, World!"

# Pull messages
gcloud pubsub subscriptions pull my-subscription \
    --limit=10
```

## **Machine Learning**

### **AI Platform**
**ML platform and services**

#### **Key Services**
- **Training**: Custom model training
- **Prediction**: Model serving
- **Notebooks**: Jupyter notebook environment
- **AutoML**: Automated ML model creation

#### **Common Commands**
```bash
# Create AI Platform job
gcloud ai-platform jobs submit training my-job \
    --package-path=./trainer \
    --module-name=trainer.task \
    --staging-bucket=gs://my-bucket \
    --region=us-central1

# Create model
gcloud ai-platform models create my-model

# Create model version
gcloud ai-platform versions create v1 \
    --model=my-model \
    --origin=gs://my-bucket/model/ \
    --runtime-version=2.1

# Get prediction
gcloud ai-platform predict \
    --model=my-model \
    --version=v1 \
    --json-instances=input.json
```

### **AutoML**
**Automated machine learning**

```bash
# Create dataset
gcloud automl datasets create \
    --display-name="My Dataset" \
    --region=us-central1

# Import data
gcloud automl datasets import \
    --dataset=my-dataset \
    --gcs-input-uris=gs://my-bucket/data.csv \
    --region=us-central1

# Train model
gcloud automl models create \
    --dataset=my-dataset \
    --display-name="My Model" \
    --region=us-central1
```

## **Kubernetes**

### **Google Kubernetes Engine (GKE)**
**Managed Kubernetes service**

#### **Key Features**
- **Clusters**: Managed Kubernetes clusters
- **Node Pools**: Groups of nodes with same configuration
- **Auto-scaling**: Automatic cluster scaling
- **Workload Identity**: Secure pod-to-service authentication

#### **Common Commands**
```bash
# Create cluster
gcloud container clusters create my-cluster \
    --zone=us-central1-a \
    --num-nodes=3 \
    --machine-type=e2-medium

# Get credentials
gcloud container clusters get-credentials my-cluster \
    --zone=us-central1-a

# List clusters
gcloud container clusters list

# Delete cluster
gcloud container clusters delete my-cluster \
    --zone=us-central1-a
```

### **Kubernetes Operations**
```bash
# Deploy application
kubectl apply -f deployment.yaml

# Scale deployment
kubectl scale deployment my-app --replicas=5

# Expose service
kubectl expose deployment my-app --port=80 --type=LoadBalancer

# View pods
kubectl get pods

# View services
kubectl get services
```

## **DevOps & Automation**

### **Cloud Build**
**CI/CD platform**

```bash
# Submit build
gcloud builds submit --tag gcr.io/PROJECT_ID/my-app .

# Create build trigger
gcloud builds triggers create github \
    --repo-name=my-repo \
    --repo-owner=my-username \
    --branch-pattern="^main$" \
    --build-config=cloudbuild.yaml

# List builds
gcloud builds list
```

### **Cloud Deployment Manager**
**Infrastructure as Code**

```yaml
# config.yaml
resources:
- name: my-instance
  type: compute.v1.instance
  properties:
    zone: us-central1-a
    machineType: zones/us-central1-a/machineTypes/e2-medium
    disks:
    - deviceName: boot
      type: PERSISTENT
      boot: true
      autoDelete: true
      initializeParams:
        sourceImage: projects/ubuntu-os-cloud/global/images/family/ubuntu-2004-lts
```

```bash
# Deploy configuration
gcloud deployment-manager deployments create my-deployment \
    --config=config.yaml

# Update deployment
gcloud deployment-manager deployments update my-deployment \
    --config=config.yaml

# Delete deployment
gcloud deployment-manager deployments delete my-deployment
```

## **Cost Management**

### **Cost Optimization**
```bash
# List billing accounts
gcloud billing accounts list

# Link project to billing account
gcloud billing projects link PROJECT_ID \
    --billing-account=BILLING_ACCOUNT_ID

# Create budget
gcloud billing budgets create \
    --billing-account=BILLING_ACCOUNT_ID \
    --budget-amount=1000USD \
    --budget-filter-projects=projects/PROJECT_ID
```

### **Cost Optimization Strategies**
- **Preemptible VMs**: Use for fault-tolerant workloads
- **Sustained Use Discounts**: Automatic discounts for long-running VMs
- **Committed Use Discounts**: 1-3 year commitments for discounts
- **Right-sizing**: Match VM sizes to workload
- **Auto-scaling**: Scale resources based on demand

## **Best Practices**

### **Security**
- **Enable MFA**: Multi-factor authentication
- **Use IAM**: Role-based access control
- **Encrypt data**: Use Cloud KMS
- **Network security**: Use VPC and firewall rules
- **Regular updates**: Keep systems patched

### **Cost Management**
- **Set budgets**: Monitor and control spending
- **Use labels**: Organize and track resources
- **Regular reviews**: Audit unused resources
- **Committed use**: For predictable workloads

### **Operational Excellence**
- **Infrastructure as Code**: Use Deployment Manager
- **Monitoring**: Set up comprehensive monitoring
- **Backup**: Regular backups and disaster recovery
- **Documentation**: Maintain up-to-date documentation

## **Learning Resources**

### **Documentation**
- **[Google Cloud Documentation](https://cloud.google.com/docs)** - Official documentation
- **[Google Cloud Architecture Center](https://cloud.google.com/architecture)** - Reference architectures
- **[Google Cloud Well-Architected Framework](https://cloud.google.com/architecture/framework)** - Best practices

### **Training**
- **[Google Cloud Training](https://cloud.google.com/training)** - Official training
- **[Google Cloud Certifications](https://cloud.google.com/certification)** - Official certifications
- **[Google Cloud YouTube Channel](https://www.youtube.com/user/googlecloudplatform)** - Video content

### **Certifications**
- **Cloud Digital Leader**: Entry-level certification
- **Associate Cloud Engineer**: Deploy and manage applications
- **Professional Cloud Architect**: Design cloud solutions
- **Professional Data Engineer**: Design data processing systems
- **Professional Machine Learning Engineer**: Design ML systems

### **Practice**
- **[Google Cloud Free Tier](https://cloud.google.com/free)** - Free services for learning
- **[Google Cloud Hands-on Labs](https://cloud.google.com/training)** - Guided practice
- **[Google Cloud Well-Architected Labs](https://cloud.google.com/architecture)** - Hands-on exercises

Remember: **GCP is about data and machine learning**. Start with the fundamentals, understand the Google ecosystem, then expand to advanced services like BigQuery and AI Platform. Always follow security best practices and monitor costs. The GCP platform is constantly evolving, so stay updated with new services and features!

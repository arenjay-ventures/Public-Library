---
layout: default
title: Azure Cheatsheet
parent: Tools & Technology
grand_parent: References
nav_order: 11
---

# Azure Cheatsheet

## **What is Microsoft Azure?**

Microsoft Azure is a comprehensive cloud computing platform offering over 200 services. It's essential for:
- **Cloud Computing**: Scalable infrastructure and services
- **Enterprise Integration**: Seamless Microsoft ecosystem integration
- **Hybrid Cloud**: On-premises and cloud connectivity
- **AI & Machine Learning**: Cognitive services and ML platforms
- **Career Growth**: High demand for Azure-certified professionals

## **Getting Started**

### **Azure Account Setup**
1. **Create Account**: [portal.azure.com](https://portal.azure.com/)
2. **Free Tier**: $200 credit for 30 days
3. **Set Billing Alerts**: Monitor costs and prevent surprises
4. **Create Resource Groups**: Organize resources logically
5. **Configure CLI**: Install and configure Azure CLI

### **Azure CLI Installation**
```bash
# Install Azure CLI
# Windows: Download from azure.microsoft.com
# macOS: brew install azure-cli
# Linux: curl -sL https://aka.ms/InstallAzureCLIDeb | sudo bash

# Login to Azure
az login

# Set subscription
az account set --subscription "Your Subscription Name"

# Verify configuration
az account show
```

## **Core Services**

### **Virtual Machines (VMs)**
**Scalable compute instances in the cloud**

#### **Key Concepts**
- **VM Sizes**: B-series (burstable), D-series (general purpose), F-series (compute optimized)
- **Images**: Windows Server, Linux distributions, custom images
- **Availability Sets**: Protect against hardware failures
- **Availability Zones**: Protect against datacenter failures

#### **Common Commands**
```bash
# List VMs
az vm list

# Create VM
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --size Standard_B1s \
    --admin-username azureuser \
    --generate-ssh-keys

# Start/stop VM
az vm start --resource-group myResourceGroup --name myVM
az vm stop --resource-group myResourceGroup --name myVM

# Delete VM
az vm delete --resource-group myResourceGroup --name myVM
```

#### **VM Sizes**
- **B1s**: 1 vCPU, 1 GB RAM (burstable)
- **D2s_v3**: 2 vCPU, 8 GB RAM (general purpose)
- **F2s_v2**: 2 vCPU, 4 GB RAM (compute optimized)
- **E4s_v3**: 4 vCPU, 32 GB RAM (memory optimized)

### **Azure Storage**
**Scalable object storage for files and data**

#### **Storage Types**
- **Blob Storage**: Unstructured data (images, videos, documents)
- **File Storage**: SMB/NFS file shares
- **Queue Storage**: Message queuing
- **Table Storage**: NoSQL key-value store

#### **Common Commands**
```bash
# Create storage account
az storage account create \
    --name mystorageaccount \
    --resource-group myResourceGroup \
    --location eastus \
    --sku Standard_LRS

# List storage accounts
az storage account list

# Create container
az storage container create \
    --name mycontainer \
    --account-name mystorageaccount

# Upload file
az storage blob upload \
    --account-name mystorageaccount \
    --container-name mycontainer \
    --name myfile.txt \
    --file ./local-file.txt

# Download file
az storage blob download \
    --account-name mystorageaccount \
    --container-name mycontainer \
    --name myfile.txt \
    --file ./downloaded-file.txt
```

### **Azure SQL Database**
**Managed relational database service**

#### **Service Tiers**
- **Basic**: 5 DTU, 2 GB storage
- **Standard**: 10-3000 DTU, 250 GB-1 TB storage
- **Premium**: 125-4000 DTU, 500 GB-4 TB storage
- **Hyperscale**: Up to 100 TB storage

#### **Common Commands**
```bash
# Create SQL server
az sql server create \
    --name mysqlserver \
    --resource-group myResourceGroup \
    --location eastus \
    --admin-user sqladmin \
    --admin-password MyPassword123!

# Create SQL database
az sql db create \
    --resource-group myResourceGroup \
    --server mysqlserver \
    --name mydatabase \
    --service-objective S0

# List databases
az sql db list --resource-group myResourceGroup --server mysqlserver
```

### **Azure Functions**
**Serverless compute service**

#### **Key Concepts**
- **Triggers**: HTTP, Timer, Blob, Queue, Event Hub
- **Bindings**: Input/output connections to Azure services
- **Consumption Plan**: Pay per execution
- **Premium Plan**: Always warm instances

#### **Common Commands**
```bash
# Create function app
az functionapp create \
    --resource-group myResourceGroup \
    --consumption-plan-location eastus \
    --runtime node \
    --runtime-version 18 \
    --functions-version 4 \
    --name myfunctionapp \
    --storage-account mystorageaccount

# Deploy function
func azure functionapp publish myfunctionapp
```

### **Azure App Service**
**Platform for web applications**

#### **App Service Plans**
- **Free**: 1 GB RAM, shared infrastructure
- **Shared**: 1 GB RAM, shared infrastructure
- **Basic**: 1.75 GB RAM, dedicated infrastructure
- **Standard**: 1.75 GB RAM, auto-scaling
- **Premium**: 3.5 GB RAM, advanced features

#### **Common Commands**
```bash
# Create app service plan
az appservice plan create \
    --name myAppServicePlan \
    --resource-group myResourceGroup \
    --sku FREE

# Create web app
az webapp create \
    --resource-group myResourceGroup \
    --plan myAppServicePlan \
    --name mywebapp \
    --runtime "NODE|18-lts"

# Deploy from GitHub
az webapp deployment source config \
    --name mywebapp \
    --resource-group myResourceGroup \
    --repo-url https://github.com/user/repo \
    --branch main \
    --manual-integration
```

## **Networking**

### **Virtual Network (VNet)**
**Isolated network environment**

#### **Key Components**
- **Subnets**: Network segments within VNet
- **Route Tables**: Control traffic routing
- **Network Security Groups**: Firewall rules
- **Load Balancers**: Distribute traffic
- **Application Gateways**: Layer 7 load balancing

#### **Common Commands**
```bash
# Create VNet
az network vnet create \
    --resource-group myResourceGroup \
    --name myVNet \
    --address-prefix 10.0.0.0/16 \
    --subnet-name mySubnet \
    --subnet-prefix 10.0.1.0/24

# Create subnet
az network vnet subnet create \
    --resource-group myResourceGroup \
    --vnet-name myVNet \
    --name mySubnet \
    --address-prefix 10.0.2.0/24

# Create NSG
az network nsg create \
    --resource-group myResourceGroup \
    --name myNSG

# Add NSG rule
az network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNSG \
    --name AllowSSH \
    --priority 1000 \
    --source-address-prefixes '*' \
    --source-port-ranges '*' \
    --destination-address-prefixes '*' \
    --destination-port-ranges 22 \
    --access Allow \
    --protocol Tcp
```

### **Load Balancer**
**Distribute incoming traffic**

```bash
# Create public IP
az network public-ip create \
    --resource-group myResourceGroup \
    --name myPublicIP \
    --allocation-method Static

# Create load balancer
az network lb create \
    --resource-group myResourceGroup \
    --name myLoadBalancer \
    --public-ip-address myPublicIP \
    --frontend-ip-name myFrontEnd \
    --backend-pool-name myBackEndPool

# Create health probe
az network lb probe create \
    --resource-group myResourceGroup \
    --lb-name myLoadBalancer \
    --name myHealthProbe \
    --protocol Http \
    --port 80 \
    --path /
```

## **Security & Identity**

### **Azure Active Directory (Azure AD)**
**Identity and access management**

#### **Key Concepts**
- **Tenants**: Isolated identity environments
- **Users**: Individual accounts
- **Groups**: Collections of users
- **Applications**: Service principals
- **Roles**: Permission assignments

#### **Common Commands**
```bash
# List users
az ad user list

# Create user
az ad user create \
    --display-name "John Doe" \
    --user-principal-name "john@mytenant.onmicrosoft.com" \
    --password "MyPassword123!"

# Create group
az ad group create \
    --display-name "Developers" \
    --mail-nickname "developers"

# Add user to group
az ad group member add \
    --group "Developers" \
    --member-id "user-object-id"
```

### **Key Vault**
**Secure storage for secrets**

```bash
# Create Key Vault
az keyvault create \
    --name myKeyVault \
    --resource-group myResourceGroup \
    --location eastus

# Create secret
az keyvault secret set \
    --vault-name myKeyVault \
    --name mySecret \
    --value "MySecretValue"

# Get secret
az keyvault secret show \
    --vault-name myKeyVault \
    --name mySecret
```

## **Monitoring & Logging**

### **Azure Monitor**
**Comprehensive monitoring solution**

#### **Key Features**
- **Metrics**: Performance data
- **Logs**: Application and system logs
- **Alerts**: Automated responses to conditions
- **Dashboards**: Visual monitoring

#### **Common Commands**
```bash
# Create log analytics workspace
az monitor log-analytics workspace create \
    --resource-group myResourceGroup \
    --workspace-name myWorkspace \
    --location eastus

# Create alert rule
az monitor metrics alert create \
    --name "High CPU Usage" \
    --resource-group myResourceGroup \
    --scopes "/subscriptions/subscription-id/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM" \
    --condition "avg Percentage CPU > 80" \
    --description "Alert when CPU exceeds 80%"
```

### **Application Insights**
**Application performance monitoring**

```bash
# Create Application Insights
az monitor app-insights component create \
    --app myAppInsights \
    --location eastus \
    --resource-group myResourceGroup

# Get instrumentation key
az monitor app-insights component show \
    --app myAppInsights \
    --resource-group myResourceGroup \
    --query instrumentationKey
```

## **DevOps & Automation**

### **Azure DevOps**
**DevOps platform and services**

#### **Key Services**
- **Azure Repos**: Git repositories
- **Azure Pipelines**: CI/CD pipelines
- **Azure Boards**: Work item tracking
- **Azure Test Plans**: Testing services
- **Azure Artifacts**: Package management

### **ARM Templates**
**Infrastructure as Code**

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "vmName": {
      "type": "string",
      "defaultValue": "myVM"
    }
  },
  "resources": [
    {
      "type": "Microsoft.Compute/virtualMachines",
      "apiVersion": "2021-03-01",
      "name": "[parameters('vmName')]",
      "location": "[resourceGroup().location]",
      "properties": {
        "hardwareProfile": {
          "vmSize": "Standard_B1s"
        },
        "storageProfile": {
          "imageReference": {
            "publisher": "Canonical",
            "offer": "UbuntuServer",
            "sku": "18.04-LTS",
            "version": "latest"
          }
        }
      }
    }
  ]
}
```

### **Deploy ARM Template**
```bash
# Deploy template
az deployment group create \
    --resource-group myResourceGroup \
    --template-file template.json \
    --parameters @parameters.json
```

## **AI & Machine Learning**

### **Cognitive Services**
**Pre-built AI services**

#### **Key Services**
- **Computer Vision**: Image analysis
- **Text Analytics**: Sentiment analysis
- **Speech Services**: Speech-to-text, text-to-speech
- **Language Understanding**: Natural language processing
- **Translator**: Text translation

### **Azure Machine Learning**
**ML platform and services**

```bash
# Create ML workspace
az ml workspace create \
    --resource-group myResourceGroup \
    --workspace-name myMLWorkspace \
    --location eastus

# Create compute cluster
az ml compute create \
    --resource-group myResourceGroup \
    --workspace-name myMLWorkspace \
    --name myComputeCluster \
    --size Standard_DS3_v2 \
    --min-instances 0 \
    --max-instances 4
```

## **Cost Management**

### **Cost Optimization**
```bash
# Get cost analysis
az consumption usage list \
    --start-date 2023-01-01 \
    --end-date 2023-01-31

# Create budget
az consumption budget create \
    --budget-name myBudget \
    --resource-group myResourceGroup \
    --amount 1000 \
    --category Cost \
    --time-grain Monthly
```

### **Cost Optimization Strategies**
- **Reserved Instances**: 1-3 year commitments for discounts
- **Spot VMs**: Use spare capacity for cost savings
- **Auto-scaling**: Scale resources based on demand
- **Resource tagging**: Track costs by project/department
- **Right-sizing**: Match VM sizes to workload

## **Best Practices**

### **Security**
- **Enable MFA**: Multi-factor authentication
- **Use RBAC**: Role-based access control
- **Encrypt data**: Use Azure Key Vault
- **Network security**: Use NSGs and firewalls
- **Regular updates**: Keep systems patched

### **Cost Management**
- **Set budgets**: Monitor and control spending
- **Use tags**: Organize and track resources
- **Regular reviews**: Audit unused resources
- **Reserved instances**: For predictable workloads

### **Operational Excellence**
- **Infrastructure as Code**: Use ARM templates
- **Monitoring**: Set up comprehensive monitoring
- **Backup**: Regular backups and disaster recovery
- **Documentation**: Maintain up-to-date documentation

## **Learning Resources**

### **Documentation**
- **[Azure Documentation](https://docs.microsoft.com/en-us/azure/)** - Official documentation
- **[Azure Architecture Center](https://docs.microsoft.com/en-us/azure/architecture/)** - Reference architectures
- **[Azure Well-Architected Framework](https://docs.microsoft.com/en-us/azure/architecture/framework/)** - Best practices

### **Training**
- **[Microsoft Learn](https://docs.microsoft.com/en-us/learn/)** - Free training modules
- **[Azure Certifications](https://docs.microsoft.com/en-us/learn/certifications/)** - Official certifications
- **[Azure Friday](https://docs.microsoft.com/en-us/shows/azure-friday/)** - Weekly video series

### **Certifications**
- **Azure Fundamentals (AZ-900)**: Entry-level certification
- **Azure Administrator (AZ-104)**: Manage Azure resources
- **Azure Developer (AZ-204)**: Develop Azure solutions
- **Azure Solutions Architect (AZ-305)**: Design Azure solutions
- **Azure Security Engineer (AZ-500)**: Implement security controls

### **Practice**
- **[Azure Free Account](https://azure.microsoft.com/en-us/free/)** - Free services for learning
- **[Azure Hands-on Labs](https://docs.microsoft.com/en-us/learn/)** - Guided practice
- **[Azure Well-Architected Labs](https://docs.microsoft.com/en-us/azure/architecture/)** - Hands-on exercises

Remember: **Azure is about integration and enterprise features**. Start with the fundamentals, understand the Microsoft ecosystem, then expand to advanced services. Always follow security best practices and monitor costs. The Azure platform is constantly evolving, so stay updated with new services and features!

# Azure Part 1

## What is Azure Cloud Computing?
- Cloud computing is a model of delivering computing services over the internet(the cloud) instead of relying on local servers or personal devices
- It allows user to access and use computing resources such as servers, storage, databases, networking, software, and analytics, on as-needed basis or on a pay-as-you-go basis or a yearly subscription service
- It has 280+ microsoft-managed data centers

## Microsoft Azure Key services
    1. Virtual Machines
    2. Aure Storage
    3. Azure SQL Databases
    4. Azure Virtual Network
    5. Azure OpenAi
    6. Kubernetes

## Strengths
- Integration with Microsoft products(Windows Server, Active Directory, Office 365)
- Strong Hybrid cloud support
- Enterprise-grade solutions
- Wide range of AI and machine learning service

## Types of Cloud Services Models
1. Infrastructure as a Service(IaaS)
    - It is a cloud computing model provided by Microsoft Azure that offers virtualized computing resources over the internet
    - Examples Virtual machines(Windows and Linux), Networks(Load balancers, subnets), storage(Azure file shares, Azure disks)

2. Platform as a Services(Paas)
    - It provides a platform allowing customers to develop, run, and manage applications without dealing with the underlying infrastructure
    - Rapidly deploy databases as service
    - Examples: SQL databases, MySQL databases, Cosmos Databases

3. Software as a Service(Saas)
    - Delivers software applications over the internet, on a subscription basis
    - It is hosted and managed by a service provider and accessed via a web browser, they are normally billed as a monthly or yearly subscription-based service
    - Examples: Gmail, Microsoft 365, One Drive, Salesforce, Drop Box

## Cloud Deployment Models
1. Public Cloud:
    - It is cloud computing services offered by third-party providers over the public internet, making them available to anyone who wants to use or reach them
    - These services include computing power, storage, databases, networking, and other services on pay per user basis
    - They are highly scalable, cost effective and accessible from anywhere

2. Hybrid Cloud
    -  Combines both public and private clouds, allowing data and applications to be shared between them
    - By allowing data to move between private and public clouds, hybrid clouds gives business greater flexibility and movre deployment options
    - Examples: Syncing On-premise Windows active directory with azure entra id, syncing on-premise file shares with azure file shares

## Benefits of cloud services
1. Cost Efficiency
    - Uses the Opex model, (expenses are fully tax deductible at the time of use)
    - Use pay-as-you-go model, pay only what you use
2. Scalability and flexibility
    - Easy to scale resources up or down as needed
3. Accessibility
4. Disaster Recovery and collaboration

## Shared Responsibility Model
- It refers to the division of security and operational responsibilities between the cloud service provider(CSP) and the customer
- The CSP is responsible for the security of the cloud, while the customer is responsible for security in the cloud


## Resource Group
- It is like a folder that helps you organize and manage related resources in Microsoft Azure
- You can group resources/instances(like virtual machines, databases, storage accounts) that belong to the same project or application
- All resources in a group share the same location(region) for easier management though they can be from different services 
- To create or deploy any resources in Azure you must have a resource group first because resource need to live in a resource group
- Resources are instances of Azure services that you create or deploy like virtual machines, storage accounts, sql databases, networks, security groups and etc..

## Naming Resource group
- Implement a consistent naming convention for resource groups to improve organization and manageability
- Example: Sydney-office-RG, Sydney-NSG(RG-Resource group, NSG- Network Security Group)

## Renaming Resource Groups
- Azure doesn't support renaming a resource group directly
- To rename, you must create a new resource group with desired name and then move all the resources from the existing group to new one 

## Deleting Resource Groups
- It deletes all resources contained within
- It deletes permanently, ensure you have backups
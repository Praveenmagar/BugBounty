# AZ-900 Certificate

## Shared Responsibility Model
- With the shared responsibility model, these responsibilities get shared between the cloud provider and the consumer
1. Cloud provider responsibility
    - Physical security, 
    - power, 
    - cooling, and 
    - network connectivity 
2. Consumer Responsibility
    - Data and information stored in the cloud
    - Access security, meaning you only give access to those who need it.

- Other responsibility depend on condition
    - Using cloud SQL database: cloud provider would be responsible for maintaining the actual database
    - Using virtual machine and installed an SQL database on it, you’d be responsible for database patches and updates, as well as maintaining the data and information stored in the database

- Basics
    1. IaaS: places the most responsibility on the consumer, with the cloud provider being responsible for the basics of physical security, power, and connectivity. E.g Microsoft azure virtual machine, Amazon web service EC2
    2. SaaS: places most of the responsibility with the cloud provider. E.g. Salesforce, Microsoft365
    3. PaaS: being a middle ground between IaaS and SaaS, rests somewhere in the middle and evenly distributes responsibility between the cloud provider and the consumer. E.g. Microsoft azure app service, Google app engine

    ![Screenshot](/images/shared-responsibility-model.png)


## Cloud Deployment Model
![Screenshot](/images/cloud-deployment-models.png)
1. Public cloud: Suit for A small online retail startup with limited budget, faster growth, small team with quick deployment
2. Private cloud: Suit for Government healthcare organization which require high security, control
3. Hybrid Cloud: Suit for large International Enterprise

#### Azure Arc
-  It is a set of technologies that helps manage your cloud environment

#### Azure Vmware Solution
- Already established with VMware in a private cloud environment but want to migrate to a public or hybrid cloud?
- Azure VMware Solution lets you run your VMware workloads in Azure with seamless integration and scalability



## Consumption Based Model
- Pay as you go model, rent computer power and storage and release those resources when you're done
- In traditional IT budgeting,
    - Capital expenditure (CapEx):
        - It is traditional on-premises
        - refers to up-front spending on physical infrastructure like servers, network hardware, and datacenter space. 
    - operational expenditure (OpEx):
        - It is Consumption-Based Cloud
        - refers to ongoing spending on services over time.

    ![Screenshot](/images/capacity-planning-comparison.png)



## During cloud deployment two important factor are
1. Uptime or availability
2. Ability to handle demand or scale

1. Highly availability
- Service level Agreements(SLAs)
    - It is formal agreement between Service provider and customer that guarantees customer a stated level of service
    - Example:
        - for 99% : 3.65 days/year downtime
        - for 99.9% : 8.76 hours/year downtime
        - for 99.99% : 52.6 min/year downtime
        - 100% uptime is difficult and expensive to achieve because it allows no time for taking service down for maintenance, backuptime and duplicating component


2. Scalability:

![Screenshot](/images/scalability.png)


3. Reliability

![Screenshot](/images/reliability.png)


4. Predictability

![Screenshot](/images/predictability.png)

- Here two parameter
    - Performance:
        -  focuses on predicting the resources needed to deliver a positive experience for your customers
        - Require more or less resources : autoscaling will automatically deploy it
        - Heavy traffic: load balancing redirect some of overload to less stressed area

    - Cost
        - focused on predicting the cost of the cloud spend.
        -  You can use tools like the Azure Pricing Calculator to get an estimate of potential cloud spend.



## Security and Governance in Cloud

![Screenshot](/images/security-governance.png)


## Manageability in cloud
- Two types
    1. Management of cloud

    ![Screenshot](/images/management-of-cloud.png)

    2. Management in cloud

    ![Screenshot](/images/management-in-cloud.png)
    

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
    1. IaaS: places the most responsibility on the consumer, with the cloud provider being responsible for the basics of physical security, power, and connectivity
    2. SaaS: places most of the responsibility with the cloud provider. 
    3. PaaS: being a middle ground between IaaS and SaaS, rests somewhere in the middle and evenly distributes responsibility between the cloud provider and the consumer.

    ![Screenshot](/images/shared-responsibility-model.png)


## Cloud Deployment Model
![Screenshot](/images/cloud-deployment-models.png)
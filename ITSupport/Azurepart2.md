# Azure Entra ID(Azure Active Directory)

## What is Azure Entra ID(Active Directory)
- It is cloud based identity and access management service provided by microsoft
- It helps organizations manage and secure user identities and control access to resources, such as applications, services, and data
- It is not a direct replacement for Windows Active Directory(AD), but it serves as a complementary cloud-based identity and access management service, while there is some overlap in functionality
- Azure Entra ID and Windows AD are designed for different use cases and environments

## Windows AD(Active Directory):
- This is an on-premises directory service for managing traditional systems and devices and supports Group Policy(GPOs), OUs, Computer Accounts, Forests, Trusts, LDAP, NTLM, Kerberos and legacy windows system

## Azure Entra ID(Azure Active Directory)
- It doesn't support for Group Policy Objects(GPOs), Organizational units(OUs), Computer accounts, forests, or trusts

## Azure ID Roles
1. Global Administrator
    - Full access to all Azure AD settings and services, can manage users, groups, policies and other admin roles, can reset passwords for all users and administrators
2. Privileged Role Administrator
    - Can manage role assignments in Azure AD, can assign or remove any role, including Global Administrator
3. User Adminnistrator
    - Manages users and groups, resets passwords for non-admin users
4. security administrator
    - Manages security settings(MFA, conditional access, security alerts)


## Azure Entra ID Objects(imp)
- Objeects are entities that represent various componenets and resources within the directory
- Objects are Users, groups, applications, devices, roles, administrative units and policies

## What is Domain Controller? (imp)
- DC is any windows server running the active directory role

## Microsoft Entra ID User Accounts
- It is like a digital ID card for a person in Microsoft's cloud
- It allows users to sign in to Microsoft services like Azure, Microsoft 365, and other app securely

## Security Groups
- Instead of adding special permissions to individual users, you create a group that applies the special permissions to every memeber of that group

## 365 Groups
- They are used for  collaboration and establish a single set of permission across Microsoft 365 apps including Outlook, SharePoint, and OneNote
- They can only have memebers
- External users can also be part of group
- You cannot add devices to 365 groups


- **Microsoft 365 Security Groups also allow you to give people outside of your organization access to the group**

## Recover Deleted Users
- It depends on serveral factors such as your subscription level, and how long ago the account was deleted
- If user was deleted more than 30 days ago, their data might be permanently deleted and you won't be able to restore it(But if you have azure site recovery backup then you can backup otherwise gone)

## Recovery deleted Security Groups
- By default doesn't allow you to recover a deleted security groups, as they are not supported for soft-delete, so any deletion made is a hard delete

## Recover Deleted 365 Groups
- It involves a similar process to recovering other deleted objects
- Possible to recovery only if done in less than 30 days retention period

- **99.99% Of company have Windows AD synchronizing with Azure AD for recovery**

## User Management
- This stores and manages information about users like login credentials, roles and permissions

## Single sign-On(SSO)
- Users cam log in once and access multiple applications or services without needing to log in again

## Access Control
- This ensures that only authorized  users can access specific resources

## Security and intergration
- Provides features like MFA to add an extra layer of security to user logins, and it works seamlessly with other Microsoft services and third-party applications


## Azure AD Licensing(Free):
- This plan is suitable for small businesses and basic identity management needs
- You can create up to 300,000 objects per AD tenant, you can send a request to Microsoft and they will upgrade you 500,000 Objects for free, but that's the limit, if require more objects you will then need to purchase a license

## Free Licensing Tier Features
- Basic user and group management
- On-premises Active Directory sunchronization
- Bsic reports and alerting
- Multifactor Authentication(MFA) for Azure AD Global administrators
- Single sign-on for up tp 10 apps per user
- Self-service password change for cloud users
- Community support

## Azure AD Licensing(Paid)
- This plan is suitable for Enterprises requiring comprehensive identity protection, governance, and privileged access, you can also have 2.15 billion objects in your Azure Entra ID lifecycle

## Fefatures of Paid licensed
- Azure AD identity protection to detect and respond to identity based risks
- On-premises AD synchronization and MFA for users
- Privileged Identity Management(PIM) to control, monitor and audit access to critical resources, and Self-service password reset for hybrid users
- Access reviews to ensure that user's access rights are regularly reviewed and appropriately maintained and advanced group management, including dynamic groups
- Microsoft Agreement support for issues


## Role Based Access Control(RBAC)
- Let's you control who can do what on which resources
- Who
    - A user, group, or service principal(This is an identity used by apps, services, to access Azure resources, it lets your app log in to Azure and do things securely, using only the permissions you give it)
- What
    - Permissions like read, write, delete
- Which resources
    - Azure resources like VMs, storage etc
    - You assign roles to users at a scope like a subscription, resource group, or resource

## RBAC Permissions
1. Least Privilege Principle
    - Assign the most restrictive role that allows user to perform their tasks
2. Combine with Custom Roles
    - When built-in roles do no meet specific needs, create roles to provide the necessary permissions
3. Understand the scope

## RBAC built in roles
- These are predefined roles provided and come with a set of default permissions
- It vary and typically cover a range of administrative and user tasks

## RBAC Custom roles
- You can achieve find-grained access control tailored to your organizations specific needs and requirements, thus enhancing both security and operational efficiency

## Documentation
- Maintain clear documentation for each custom role, including its purpose and the permissions it includes

## License
- You need to have anAzure ID license, either P1 or P2 license in order to create custom any type of custom roles

## Azure Bash command
```
az ad user create --display-name "John Smith" --password "1@fdae344" --user-principal-name John@prabinmagar711gmail.onmicrosoft.com
```
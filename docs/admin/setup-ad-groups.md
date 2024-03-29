---
title: Set up deployment groups
titleSuffix: Azure DevOps Server
description: Set up groups for use in Azure DevOps on-premises
ms.topic: conceptual
ms.manager: jillfra
ms.author: aaronha
author: aaronhallberg
ms.date: 05/24/2019
ms.prod: devops-server
ms.technology: tfs-admin
---

# Set up groups for use in Azure DevOps on-premises

[!INCLUDE [temp](../_shared/version-tfs-all-versions.md)]

Managing users in Azure DevOps Server is much easier if you create Windows or Active Directory groups for them, particularly if your deployment includes SharePoint Foundation and SQL Server Reporting Services.

## Users, groups, and permissions in Azure DevOps Server deployments

Azure DevOps Server, SharePoint Products, and SQL Server Reporting Services all maintain their own information about groups, users, and permissions. To make managing users and permissions across these programs simpler, you can create groups of users with similar access requirements in the deployment, give those groups appropriate access in the different software programs, and then just add or remove users from a group as needed. This is much easier than maintaining individual users or groups of users separately in three separate programs.

If your server is in an Active Directory domain, one option is to create specific Active Directory groups to manage your users, like a group of developers and testers for all projects in the project collection, or a group of users who can create and administer projects in the collection. Similarly, you can create an Active Directory account for services that can't be configured to use the Network Service system account as the service account. To do so, create an Active Directory account for SharePoint Foundation and as the read-access data source account for reports in SQL Server Reporting Services.

> [!IMPORTANT]
> If you decide to use Active Directory groups in Azure DevOps Server, consider creating specific ones whose purpose is dedicated to user management in Azure DevOps Server. Using previously existing groups that were created for another purpose, particularly if they are managed by others who are not familiar with Azure DevOps Server, can lead to unexpected user consequences when membership changes to support some other function.

The default choice during installation is to use the Network Service system account as the service account for Azure DevOps Server and SQL Server. If you want to use a specific account as the service account for security purposes or other reasons, such as a scaled-out deployment, you can. You might also want to create a specific Active Directory account to use as the service account for SharePoint Foundation and as the data source reader account for SQL Server Reporting Services.

If your server is in an Active Directory domain but you don't have permissions to create Active Directory groups or accounts, or if you're installing your server in a workgroup instead of a domain, you can create and use local groups to manage users across SQL Server, SharePoint Foundation, and Azure DevOps Server. Similarly, you can create a local account to use as the service account. However, keep in mind that local groups and accounts are not as robust as domain groups and accounts. For example, in the event of a server failure, you would need to recreate the groups and accounts from scratch on the new server. If you use Active Directory groups and accounts, the groups and accounts will be preserved even if the server hosting Azure DevOps Server fails.

For example, after reviewing business requirements for the new deployment and the security requirements with the project managers, you might decide to create three groups to manage the majority of users in the deployment:

-   A general group for developers and testers who will participate fully in all projects in the default project collection. This group will contain the majority of users. You might name this group TFS\_ProjectContributors.

-   A small group of project administrators who will have permissions to create and manage projects in the collection. You might name this group TFS\_ProjectAdmins.

-   A special, restricted group of contractors who will only have access to one of the projects. You might name this group TFS\_RestrictedAccess.

Later on, as the deployment expands, you might decide to create other groups.

### To create a group in Active Directory

-   Create a security group that is a local domain, global, or universal group in Active Directory, as best meets your business needs. For example, if the group needs to contain users from more than one domain, the universal group type will best suit your needs. For more information, see [Create a New Group (Active Directory Domain Services)](http://go.microsoft.com/fwlink/?LinkId=235815).

### To create a local group on the server

-   Create a local group and give it a name that will quickly identify its purpose. By default, any group you create will have the equivalent permissions of the Users default group on that computer. For more information, see [Create a local group](http://go.microsoft.com/fwlink/?LinkId=235816).

### To create an account to use as a service account in Active Directory

-   Create an account in Active Directory, set the password policy according to your business requirements, and make sure that **Account is trusted for delegation** is selected for the account. For more information, see [Create a New User Account (Active Directory Domain Services)](http://go.microsoft.com/fwlink/?LinkId=235817) and [Understanding User Accounts (Active Directory Domain Services)](http://go.microsoft.com/fwlink/?LinkId=235818).

### To create a local account to use as the service account on the server

-   Create a local account to use as the service account and then modify its group membership and other properties according to the security requirements for your business. For more information, see [Create a local user account](http://go.microsoft.com/fwlink/?LinkId=235819).

## Try this next
> [!div class="nextstepaction"]
> [Add users to projects](/azure/devops/security/add-users-team-project) 

## Q & A

**Q: Can I use groups to restrict access to projects or features in Azure DevOps Server?**

**A:** Yes, you can. You can create specific groups for [granting or restricting access to select features, functions, and projects](/azure/devops/security/restrict-access), for [managing access levels](/azure/devops/security/change-access-levels), and other purposes.


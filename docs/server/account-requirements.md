---
title: Service account requirements 
titleSuffix: Azure DevOps Server & TFS 
description: Service account requirements for Azure DevOps Server and Team Foundation server
ms.prod: devops-server
ms.technology: tfs-admin
toc: show
ms.manager: jillfra
ms.author: aaronha
author: elbatk
ms.topic: conceptual
ms.date: 02/20/2019
---

# Service account requirements

[!INCLUDE [temp](_shared/version-tfs-all-versions.md)]



<a name="accounts"></a> 

You must use service accounts To install Azure DevOps Server or Team Foundation Server, Team Foundation Build, and Team Foundation Server Proxy. If you use reporting, you also must have a report reader account when you install Azure DevOps Server or Team Foundation Server. 
Azure DevOps Server and Team Foundation Server require multiple identities for installation, but you can use a single account for all the identities if that account meets the requirements for all the identities for which you use it.

> [!TIP]
> Confused about accounts? A tutorial is available that covers how to create accounts and groups for a single-server installation. For more information, see [Set up groups for use in TFS deployments](./admin/setup-ad-groups.md). 


## Best practices for accounts

Here are some best practices for working with accounts in Azure DevOps Server or TFS:

-   If you use domain accounts for your service accounts, use a different identity for the report reader account.
-   If you are installing a component in a workgroup, you must use local accounts for user accounts.

## Report reader account

The report reader account is the identity that's used to gather information for reports. If you use reporting, you must specify a report reader account when you install Azure DevOps Server or Team Foundation Server.

If you install Azure DevOps Server or Team Foundation Server with the default options, the report reader account is also used as the identity of the service account for SharePoint Foundation.

| Feature | Sample user logon name<sup>1</sup> | Requirements |
| --- | --- | --- |
| Reporting | **AzureDevOpsServerReports** | You must specify a user account that has **Allow log on locally** permissions. <br /> Default: You're prompted for this account. You can't use a built-in account for the report reader account. |

<sup>1</sup> To make it easier to discuss the different accounts that Azure DevOps Server or Team Foundation Server require, this article uses example placeholder names. You don't have to use these placeholder names for any accounts that you might create.

## Network Service or built-in accounts

Azure DevOps Server, Team Foundation Server, Team Foundation Build, and Team Foundation Server Proxy all require a service account. These service accounts become the identity for the installed component. By default, every component uses a built-in account (such as Network Service) as its service account. You can change this account to a user account when you install the component, but you must ensure that any user accounts that you use have **Log on as a service** permissions.

> [!TIP]
> Built-in accounts don't use passwords. Built-in accounts already have **Log on as a service** permissions, so they're easier to manage, especially in a domain environment. 

## Service accounts for Azure DevOps Server or TFS

The service accounts in the following table are the identities for Azure DevOps Server or Team Foundation Server and their components.

The service account for Azure DevOps Server or Team Foundation Server is also used in Internet Information Services (IIS) as the identity of the application pool for Azure DevOps Server or Team Foundation Server.

| Component | Sample user logon name<sup>1</sup> | Requirements |
| --- | --- | --- |
| Azure DevOps Server or Team Foundation Server | **AzureDevOpsService** | You can specify a built-in account or a user account. If you specify a user account, it must have **Log on as a service** permissions. <br /><br /> You must not use the account that you use to install Azure DevOps Server or Team Foundation Server as the account for AzureDevOpsService. For example, if you are logged in as domain\user1 when you install Azure DevOps Server or Team Foundation Server, don't use domain\user1 as the account for AzureDevOpsService. <br /><br /> If your SharePoint site wasn't installed at the same time as Team Foundation Server, you must add AzureDevOpsService to the Farm Administrators group for the SharePoint Central Administration site. For more information, see [Add the service account for Team Foundation Server to the Farm Administrators group](./install/sharepoint/setup-remote-sharepoint.md#tfs-svc-acct-to-farm-admin-group). <br /> Default: Network Service |
| Team Foundation Build | **TFSBUILD** | You can specify a built-in account or a user account. If you use a user account, it must have **Log on as a service** permissions. |
| Azure DevOps Server Proxy or Team Foundation Server Proxy | **AzureDevOpsServerProxy** | You can specify a built-in account or a user account. If you use a user account, it must have **Log on as a service** permissions. |

<sup>1</sup> To make it easier to discuss the different accounts that Azure DevOps Server or Team Foundation Server require, this article uses example placeholder names. You don't have to use these placeholder names for any accounts that you might create.

## Service accounts for Release Management for Visual Studio 2013

The service accounts in the following table are the identities for Release Management Server and the Microsoft Deployment Agent.

| Component | Sample user logon name<sup>1</sup> | Requirements |
| --- | --- | --- |
| Release Management Server | **RMSERVER** | This is the identity used in IIS uses for the application pool and the **Release Management Monitor** Windows service. <br /><br />Default: Network Service |
| Microsoft Deployment Agent | **DEPLOY** | This identity is used to configure the machines in your environment for release. Make sure that the identity you use has the necessary permissions to do whatever tasks are required. For example, if you need to install your application on this machine as part of your release, add this identity to the local Windows Administrators security group. If this identity needs to access builds on the network, make sure it has access to the network drop location. For step-by-step procedures, see [Install deployment agent and set up machines for an environment](/azure/devops/build-release/archive/release/previous-version/install-release-management/install-deployment-agent). <br /><br />Default: You are prompted for an account. |

<sup>1</sup> To make it easier to discuss the different accounts that Azure DevOps Server or Team Foundation Server require, this article uses example placeholder names. You don't have to use these placeholder names for any accounts that you might create.

#### Connect Release Management to TFS account

If you connect Release Management to Azure DevOps Server or TFS, you need an account to act as an intermediary account. For step-by-step procedures, see 
[Connect Release Management to TFS](/azure/devops/build-release/archive/release/previous-version/install-release-management/connect-to-tfs).

| Component | Sample user logon name<sup>1</sup> | Requirements |
| --- | --- | --- |
| Release Management Server (connected to TFS) | **RMAzureDevOpsServer** | A TFS user that is a member of **Project Collection Administrators** ([minimal permissions that this account must have](http://blogs.msdn.com/b/visualstudioalm/archive/2013/12/19/how-to-configure-team-foundation-server-with-release-management.aspx)) group and has **Make requests on behalf of others** permissions set to **allow** in TFS. |

<sup>1</sup> To make it easier to discuss the different accounts that TFS requires, this article uses example placeholder names. You don't have to use these placeholder names for any accounts that you might create.

## Service accounts for additional software

The following table lists the service accounts that are the identities used to run Windows services for SharePoint Products and SQL Server.

The service account for SharePoint Products is also the identity of the application pool for the SharePoint Central Administration site.

| Component | Sample user logon name<sup>1</sup> | Requirements |
| --- | --- | --- |
| SharePoint Products | **WSSSERVICE** | You must specify a user account. <br /><br /> Default: If you install Team Foundation Server with the default options, the account that you specified as the report reader account is also used for this account. |
| SQL Server | **SQLSERVICE** | You can use a built-in system account or set up an account before you install SQL Server. Azure DevOps Server and Team Foundation Server has no requirements for this account. |

<sup>1</sup> To make it easier to discuss the different accounts that Azure DevOps Server or Team Foundation Server require, this article uses example placeholder names. You don't have to use these placeholder names for any accounts that you might create.


## Related articles

- [Service accounts and dependencies](./admin/service-accounts-dependencies-tfs.md).
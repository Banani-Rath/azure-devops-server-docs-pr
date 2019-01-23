---
title: Requirements and compatibility | Azure DevOps Server and Team Foundation Server setup, upgrade, and administration
description: This article describes many kinds of requirements and compatibility for Azure DevOps Server and TFS, including hardware, operating systems, SQL Server, client versions, server versions, and browsers.
ms.prod: devops-server
ms.technology: tfs-admin
toc: show
ms.manager: douge
ms.author: elbatk
author: elbatk
ms.topic: conceptual
ms.date: 11/14/2018
---

# Requirements and compatibility

**Azure DevOps Server 2019 RC1** | **TFS 2018** | **TFS 2017** | **TFS 2015** | **TFS 2013**

## <a name="operating-systems"></a> Operating systems

The following operating systems are supported for the indicated versions of Azure DevOps Server and Team Foundation Server (TFS).

### Server or client installation

- **Azure DevOps Server**
  - Runs on either a Windows Server operating system or a Windows client operating system.
  - Azure DevOps Server 2019 RC1, TFS 2018, and TFS 2017 run only on a 64-bit operating system.

- **Team Foundation Server**: 
  - Runs on either a Windows Server operating system or a Windows client operating system.
  - Earlier versions of TFS run on either a 64-bit or a 32-bit operating system when a 32-bit version is available. We recommend that you use a server operating system unless your Azure DevOps Server or Team Foundation Server instance is for evaluation or personal use.

### Server operating systems
  
Azure DevOps Server or TFS version | Supported server operating systems
------------|--------------------------------
Azure DevOps Server 2019 RC1 | Windows Server 2019<br/>Windows Server 2016<br/>Windows Server 2012 R2 (Essentials, Standard, Datacenter)<br/>Windows Server 2012 (Essentials, Standard, Datacenter)
TFS 2018 | Windows Server 2016<br/>Windows Server 2012 R2 (Essentials, Standard, Datacenter)<br/>Windows Server 2012 (Essentials, Standard, Datacenter)
TFS 2017 | Windows Server 2016<br/>Windows Server 2012 R2 (Essentials, Standard, Datacenter)<br/>Windows Server 2012 (Essentials, Standard, Datacenter)<br/>Windows Server 2008 R2 (minimum SP1) (Standard, Enterprise, Datacenter)
TFS 2015 | Windows Server 2016<br/>Windows Server 2012 R2 (Essentials, Standard, Datacenter)<br/>Windows Server 2012 (Essentials, Standard, Datacenter)<br/>Windows Server 2008 R2 (minimum SP1) (Standard, Enterprise, Datacenter)
TFS 2013 | Windows Server 2012 R2 (Essentials, Standard, Datacenter)<br/>Windows Server 2012 (Essentials, Standard, Datacenter)<br/>Windows Server 2008 R2 (minimum SP1) (Standard, Enterprise, Datacenter)
TFS 2012 | Windows Server 2012 R2 (Essentials, Standard, Datacenter)<br/>Windows Server 2012 (Essentials, Standard, Datacenter)<br/>Windows Server 2008 R2 (Standard, Enterprise, Datacenter)<br/>Windows Server 2008 (minimum SP2)<br/>Windows Small Business Server 2011 (Standard, Essentials, Premium Add-On)<br/>Windows Home Server 2011
TFS 2010 | Windows Server 2008 R2 (Standard, Enterprise, Datacenter)<br/>Windows Server 2008 (minimum SP2)<br/>Windows Server 2003 R2<br/>Windows Server 2003 (minimum SP2)

The [Server Core](https://msdn.microsoft.com/library/dd184075.aspx) installation option is supported only for Azure DevOps Server 2019 RC1, TFS 2018, and TFS 2017. [Windows Server version 1709](/windows-server/get-started/get-started-with-1709) isn't supported.

### Client operating systems

Azure DevOps Server or TFS version | Supported client operating systems
------------|--------------------------------
Azure DevOps Server 2019 RC1 | Windows 10 (Professional, Enterprise) Version 1607 or later
TFS 2018 | Windows 10 (Professional, Enterprise) Version 1607 or later
TFS 2017 | Windows 10 (Home, Professional, Enterprise)<br/>Windows 8.1 (Basic, Professional, Enterprise)<br/>Windows 7 (minimum SP1) (Home Premium, Professional, Enterprise, Ultimate)
TFS 2015 | Windows 10 (Home, Professional, Enterprise)<br/>Windows 8.1 (Basic, Professional, Enterprise)<br/>Windows 7 (minimum SP1) (Home Premium, Professional, Enterprise, Ultimate)
TFS 2013 | Windows 8.1 (Basic, Professional, Enterprise)<br/>Windows 7 (minimum SP1) (Home Premium, Professional, Enterprise, Ultimate)
TFS 2012 | Windows 8.1 (Basic, Professional, Enterprise)<br/>Windows 7 (Home Premium, Professional, Enterprise, Ultimate)
TFS 2010 | Windows 7 (Home Premium, Professional, Enterprise, Ultimate)<br/>Windows Vista SP2

Although you can install Azure DevOps Server and TFS on client operating systems, we don't recommend client operating system installation except for evaluation purposes or personal use. Client operating systems have the following restrictions:

- Azure DevOps Server and TFS installations on client operating systems don't support integration with SharePoint Products or SharePoint Reporting.
- You can't install Azure DevOps Server Proxy and Team Foundation Server Proxy on client operating systems. 

If you need to use any of these features, install Azure DevOps Server or TFS on a server operating system.

## <a name="proxy-server"></a> System requirements for Azure DevOps Server Proxy or Team Foundation Server Proxy

The proxy feature is available only if you install Azure DevOps Server or Team Foundation Server on a server operating system.

Review the following hardware recommendations to determine the optimal hardware to use for Azure DevOps Server Proxy or Team Foundation Server Proxy.

Unlike operating system requirements, hardware recommendations for proxy are different from hardware recommendations for setting up the application tier of Azure DevOps Server or Team Foundation Server. The application tier of Team Foundation Server requires more robust hardware than the proxy feature.

Recommended hardware is based on the size of the team that will use the proxy server. Usually, this is the team in your remote office. The larger your team, the more robust your hardware must be.

| Remote team size | Hardware recommendations (CPU/RAM) for Azure DevOps Server Proxy or Team Foundation Server Proxy |
|---|---|
| 450 or fewer users | One processor, 2.2-GHz CPU, 2 GB of RAM |
| Between 451 and 2,200 users | Two processors, 2.0-GHz CPU, 2 GB of RAM |
| Between 2,201 and 3,600 users | Four processors, 2.0-GHz CPU, 2 GB of RAM |
			
### <a name="gvfs-proxy-server"></a> GVFS proxy additional requirements
The Git Virtual File System (GVFS) proxy feature supports intensive input/output (I/O) operations. In addition to the basic requirements for Azure DevOps Server Proxy or Team Foundation Server Proxy, GVFS proxying requires a fast, large disk to operate efficiently on the repository. Recommended hardware is based on the size of the repository that the GVFS proxy serves.

| Hardware | Recommended value |
|---|---|
| RAM | As large as the tip of a typical branch |
| Disk space | Four times the repository's entire size |
| Disk hardware | A solid-state drive (SSD) |

For example, if a repository has 50 GB at the tip of **master** and 200 GB of history, we recommend 50 GB of RAM and 800 GB of SSD-based storage.

## Virtualization

Microsoft supports Azure DevOps Server or Team Foundation Server virtualization in supported virtualization environments.

For more information, see the following articles:

* [Microsoft server software and supported virtualization environments](http://go.microsoft.com/fwlink/?LinkId=196061)
* [Support policy for Microsoft software running in non-Microsoft hardware virtualization software](http://go.microsoft.com/fwlink/?LinkId=196062)
* [Support partners for non-Microsoft hardware virtualization software](http://go.microsoft.com/fwlink/?LinkId=196063)
* [Server virtualization](http://go.microsoft.com/fwlink/?LinkId=196072) (officially supported products)

## <a name="sql-server"></a> SQL Server

Use one of the following versions of SQL Server for Azure DevOps Server or TFS:

Azure DevOps Server or TFS version | Support SQL Server version
-------------------|------------------------------------
Azure DevOps Server 2019 RC1 | SQL Server 2017<br/>SQL Server 2016 (minimum SP1)
TFS 2018 | SQL Server 2017<br/>SQL Server 2016 (minimum SP1)
TFS 2017 Update 1 | SQL Server 2016 (minimum SP1)<br/>SQL Server 2014<br/>
TFS 2017 | SQL Server 2016<br/>SQL Server 2014<br/>
TFS 2015 Update 3 | SQL Server 2016<br/>SQL Server 2014<br/>SQL Server 2012 (minimum SP1)
TFS 2015 | SQL Server 2014<br/>SQL Server 2012 (minimum SP1)
TFS 2013 Update 2  | SQL Server 2014<br/>SQL Server 2012 (minimum SP1)
TFS 2013 | SQL Server 2012 (minimum SP1)
TFS 2012 | SQL Server 2012<br/>SQL Server 2008 R2
TFS 2010 | SQL Server 2008 R2<br/>SQL Server 2008

### SQL Server version additional information

The following information applies to the indicated SQL Server version:

- **SQL Server on Linux**: SQL Server on Linux isn't supported.

- **SQL Server 2016**: If you use SQL Server 2016, you must install a Visual C++ runtime [update](http://support.microsoft.com/kb/3138367). 

- **SQL Server 2014**: SQL Server 2014 has more robust hardware requirements than earlier SQL Server versions. Some hardware configurations might reduce performance in Azure DevOps Server or Team Foundation Server. For more information, see [TFS 2013 Update 2: Performance considerations for using SQL Server 2014](http://support.microsoft.com/kb/2953452).

- **SQL Server 2012 SP1**: If you use SQL Server 2012 SP1, we recommend that you apply [Cumulative Update 2](http://support.microsoft.com/kb/2790947) on top of SP1 to address a critical SQL Server bug related to resource consumption. This isn't a requirement because the bug affects only a small number of SQL Server 2012 SP1 instances, but it's important to be aware of it.

  If you don't apply Cumulative Update 2, apply a SQL Server hotfix ([KB2793634](http://support.microsoft.com/kb/2793634)) to address a separate issue in which SQL Server 2012 SP1 might request an excessive number of restarts.

Azure DevOps Server and TFS support Express, Standard, and Enterprise [SQL Server editions](https://www.microsoft.com/sql-server/sql-server-2017-editions). The Express edition is recommended only for evaluation purposes, personal use, or for very small teams. We recommend the SQL Server Standard or Enterprise versions for all other scenarios.

## <a name="hardware-recommendations"></a> Hardware recommendations

Azure DevOps Server and Team Foundation Server can scale from an Express installation on a laptop that's used by a single person to a highly available deployment that's used by thousands of people. It can support high-use scenarios that have multiple application tiers behind a load balancer and multiple SQL instances that use SQL Always On. 

The following recommendations apply to most Azure DevOps Server and TFS deployments. Your requirements might vary depending on how your team uses Azure DevOps Server or TFS. For example, if you have particularly large Git repositories or Team Foundation Version Control branches, you might need higher-spec machines than those listed in the following sections. All the machines that are described in the next sections can be either physical or virtual.

### Single-server deployment

A single-server deployment consists of a single machine with one dual-core processor, 4 GB of RAM, and a fast hard-disk drive. This configuration typically supports up to 250 users of core source control (Team Foundation Version Control or Git) and work item tracking functionality. Extensive use of automated build, test, or release likely will cause performance issues. We don't recommend use of search or reporting features for this configuration.

When you scale up a single server, the server can handle a larger number of users and an increased use of automated build, test, or release. A scaled-up server can also use search or reporting features. For example, increasing RAM to 8 GB should enable a single-server deployment to scale up to 500 users.

For evaluation or personal use, you can use a basic configuration with as little as 1 GB of RAM. This configuration isn't recommended for a production server that's used by more than one person.

### Multi-server deployments

The following scenarios might require a multiple-server deployment:

- Scaling beyond 500 users
- Extensive use of automated build, test, or release
- Using Code Search
- Using reporting features
- Using SharePoint integration
 
For a team of more than 500 users, consider the following setup:

- An application tier with one dual-core processor, 8 GB of memory, and a fast hard-disk drive.
- A data tier with one quad-core processor, 8 GB of memory, and high-performance storage, such as an SSD.

For a team of more than 2,000 users, consider the following setup:

- An application tier with one quad-core processor, 16 GB or more of memory, and a fast hard-disk drive.
- A data tier with two or more quad-core processors, 16 GB or more of memory, and advanced high-performance storage, like an SSD or high-performance SAN.

If you plan to use build, test, or release automation extensively, we recommend that you use higher-spec application and data tiers to avoid performance issues. For example, a team of 250 might use a multiple-server deployment that is more in line with the recommendations for a team of 500 to 2,000 users. We also recommend that you monitor your automated processes to ensure that they are efficient. For example, retrieve data from source control incrementally during builds whenever possible instead of fully refreshing with each build. 

> [!NOTE]
> Except for very small teams that have extremely limited use of these features, we don't recommend installing build, test, or release agents on your Azure DevOps Server or TFS application tiers.
>

If you plan to use Code Search, we recommend that you set up a separate server for Code Search. For more information, see the [hardware requirements for Code Search](/azure/devops/project/search/administration?view=tfs-2017).

If you plan to use reporting features, we recommend that you set up a separate server for your warehouse database and SQL Server Analysis Services cube. Another option is to use a higher-spec data tier.

If you plan to use SharePoint integration, we recommend that you set up a separate server for your SharePoint instance or that you use a higher-spec application tier. 

If you want to guarantee high availability, consider using multiple application tiers behind a load balancer and multiple SQL Server instances. In this scenario, we recommend that you put your Azure DevOps Server or TFS databases in an Always On Availability Group.

## <a name="sharepoint"></a> SharePoint

TFS 2018 and Azure DevOps Server no longer support integration with Office SharePoint and the TFS Extension for SharePoint. For information about TFS integration with SharePoint, see [TFS-SharePoint version compatibility](/azure/devops/report/sharepoint-dashboards/about-sharepoint-integration?#compat).

## Active Directory

You can install Azure DevOps Server or Team Foundation Server on more than one server if the servers are all joined to an Azure Active Directory domain that's based on a functional level that the servers support. You can install Azure DevOps Server or TFS on a single server that's joined to an Active Directory domain or that is a member of a workgroup.

You can't install Azure DevOps Server or TFS on servers that are joined to domains if the domain controllers are running Windows NT Server 4.0. The following table shows which functional levels for Active Directory domains Azure DevOps Server and TFS don't support:

| Functional levels for Active Directory domains | Supported |
| --- | --- |
| **Windows 2000 mixed mode**: Domain controllers that are running Windows Server 2003 R2, Windows Server 2003, Windows 2000, and Windows NT Server 4.0. | No |
|**Windows Server 2003 interim mode**: Domain controllers that are running Windows Server 2003 R2, Windows Server 2003, and Windows NT Server 4.0. | No |

## <a name="accounts"></a> Accounts

You must use service accounts to install Azure DevOps Server or Team Foundation Server, Team Foundation Build, and Team Foundation Server Proxy. If you use reporting, you also must have a report reader account when you install Azure DevOps Server or Team Foundation Server. This article describes the requirements for service accounts and the report reader account for installation. For more information, see [Service accounts and dependencies in Team Foundation Server](./admin/service-accounts-dependencies-tfs.md).

Azure DevOps Server and Team Foundation Server require multiple identities for installation, but you can use a single account for all the identities if that account meets the requirements for all the identities for which you use it.

> [!TIP]
> Confused about accounts? A tutorial is available that covers how to create accounts and groups for a single-server installation. For more information, see [Set up groups for use in TFS deployments](./admin/setup-ad-groups.md). 

### Best practices for accounts

Here are some best practices for working with accounts in Azure DevOps Server or TFS:

-   If you use domain accounts for your service accounts, use a different identity for the report reader account.
-   If you are installing a component in a workgroup, you must use local accounts for user accounts.

### Report reader account

The report reader account is the identity that's used to gather information for reports. If you use reporting, you must specify a report reader account when you install Azure DevOps Server or Team Foundation Server.

If you install Azure DevOps Server or Team Foundation Server with the default options, the report reader account is also used as the identity of the service account for SharePoint Foundation.

| Feature | Sample user logon name<sup>1</sup> | Requirements |
| --- | --- | --- |
| Reporting | **AzureDevOpsServerReports** | You must specify a user account that has **Allow log on locally** permissions. <br /> Default: You're prompted for this account. You can't use a built-in account for the report reader account. |

<sup>1</sup> To make it easier to discuss the different accounts that Azure DevOps Server or Team Foundation Server require, this article uses example placeholder names. You don't have to use these placeholder names for any accounts that you might create.

### Service accounts

Azure DevOps Server, Team Foundation Server, Team Foundation Build, and Team Foundation Server Proxy all require a service account. These service accounts become the identity for the installed component. By default, every component uses a built-in account (such as Network Service) as its service account. You can change this account to a user account when you install the component, but you must ensure that any user accounts that you use have **Log on as a service** permissions.

> [!TIP]
> Built-in accounts don't use passwords. Built-in accounts already have **Log on as a service** permissions, so they're easier to manage, especially in a domain environment. 

#### Service accounts for Azure DevOps Server or TFS

The service accounts in the following table are the identities for Azure DevOps Server or Team Foundation Server and their components.

The service account for Azure DevOps Server or Team Foundation Server is also used in Internet Information Services (IIS) as the identity of the application pool for Azure DevOps Server or Team Foundation Server.

| Component | Sample user logon name<sup>1</sup> | Requirements |
| --- | --- | --- |
| Azure DevOps Server or Team Foundation Server | **AzureDevOpsService** | You can specify a built-in account or a user account. If you specify a user account, it must have **Log on as a service** permissions. <br /><br /> You must not use the account that you use to install Azure DevOps Server or Team Foundation Server as the account for AzureDevOpsService. For example, if you are logged in as domain\user1 when you install Azure DevOps Server or Team Foundation Server, don't use domain\user1 as the account for AzureDevOpsService. <br /><br /> If your SharePoint site wasn't installed at the same time as Team Foundation Server, you must add AzureDevOpsService to the Farm Administrators group for the SharePoint Central Administration site. For more information, see [Add the service account for Team Foundation Server to the Farm Administrators group](./install/sharepoint/setup-remote-sharepoint.md#tfs-svc-acct-to-farm-admin-group). <br /> Default: Network Service |
| Team Foundation Build | **TFSBUILD** | You can specify a built-in account or a user account. If you use a user account, it must have **Log on as a service** permissions. |
| Azure DevOps Server Proxy or Team Foundation Server Proxy | **AzureDevOpsServerProxy** | You can specify a built-in account or a user account. If you use a user account, it must have **Log on as a service** permissions. |

<sup>1</sup> To make it easier to discuss the different accounts that Azure DevOps Server or Team Foundation Server require, this article uses example placeholder names. You don't have to use these placeholder names for any accounts that you might create.

#### Service accounts for Release Management for Visual Studio 2013

The service accounts in the following table are the identities for Release Management Server and the Microsoft Deployment Agent.

| Component | Sample user logon name<sup>1</sup> | Requirements |
| --- | --- | --- |
| Release Management Server | **RMSERVER** | This is the identity used in IIS uses for the application pool and the **Release Management Monitor** Windows service. <br /><br />Default: Network Service |
| Microsoft Deployment Agent | **DEPLOY** | This identity is used to configure the machines in your environment for release. Make sure that the identity you use has the necessary permissions to do whatever tasks are required. For example, if you need to install your application on this machine as part of your release, add this identity to the local Windows Administrators security group. If this identity needs to access builds on the network, make sure it has access to the network drop location. For step-by-step procedures, see [Install deployment agent and set up machines for an environment](/azure/devops/build-release/archive/release/previous-version/install-release-management/install-deployment-agent). <br /><br />Default: You are prompted for an account. |

<sup>1</sup> To make it easier to discuss the different accounts that Azure DevOps Server or Team Foundation Server require, this article uses example placeholder names. You don't have to use these placeholder names for any accounts that you might create.

#### Connect Release Management to Azure DevOps Server or TFS account

If you connect Release Management to Azure DevOps Server or TFS, you need an account to act as an intermediary account. For step-by-step procedures, see 
[Connect Release Management to TFS](/azure/devops/build-release/archive/release/previous-version/install-release-management/connect-to-tfs).

| Component | Sample user logon name<sup>1</sup> | Requirements |
| --- | --- | --- |
| Release Management Server (connected to Azure DevOps Server or TFS) | **RMAzureDevOpsServer** | An Azure DevOps Server or TFS user that is a member of **Project Collection Administrators** ([minimal permissions that this account must have](http://blogs.msdn.com/b/visualstudioalm/archive/2013/12/19/how-to-configure-team-foundation-server-with-release-management.aspx)) group and has **Make requests on behalf of others** permissions set to **allow** in TFS. |

<sup>1</sup> To make it easier to discuss the different accounts that Azure DevOps Server or Team Foundation Server require, this article uses example placeholder names. You don't have to use these placeholder names for any accounts that you might create.

#### Service accounts for additional software

The following table lists the service accounts that are the identities used to run Windows services for SharePoint Products and SQL Server.

The service account for SharePoint Products is also the identity of the application pool for the SharePoint Central Administration site.

| Component | Sample user logon name<sup>1</sup> | Requirements |
| --- | --- | --- |
| SharePoint Products | **WSSSERVICE** | You must specify a user account. <br /><br /> Default: If you install Team Foundation Server with the default options, the account that you specified as the report reader account is also used for this account. |
| SQL Server | **SQLSERVICE** | You can use a built-in system account or set up an account before you install SQL Server. Azure DevOps Server and Team Foundation Server has no requirements for this account. |

<sup>1</sup> To make it easier to discuss the different accounts that Azure DevOps Server or Team Foundation Server require, this article uses example placeholder names. You don't have to use these placeholder names for any accounts that you might create.

## <a name="project-server"></a> Project Server

TFS 2017 and later versions no longer support native integration with Office Project Server. For information about TFS integration with Project Server, see [TFS-Project Server version compatibility](/azure/devops/reference/tfs-ps-sync/system-and-setup-requirements?view=vsts#tfs-project-server-version-compability).

## Major releases and service packs

Microsoft doesn't always immediately support major new versions of dependencies like SQL Server. Sometimes, we must release updates to add support for those versions. 
However, when Microsoft supports a major version, we always support the latest service pack immediately when it's released. We work with product teams to test service packs before they're released.

### Build service hardware requirements

The XAML build service has the same operating system requirements as Azure DevOps Server and TFS. Usually, it makes sense to run the build service on a separate machine from the application tier. Hardware requirements for the build service are the same as the operating system on which it's running. However, you can optimize build service performance by tailoring the hardware specs of your build machine to the types of builds your team will use.

<!-- For more information, see System requirements for Team Foundation Build Service  -->

## <a name="languages"></a> Natural languages

You can install Azure DevOps Server and TFS in various languages on supported operating systems. However, you can't use any combination of localized operating system with Azure DevOps Server and TFS. Also, you can't install multiple languages on a single Azure DevOps Server or TFS server. The language of the SharePoint Products installation can also complicate your deployment. However, you can add an appropriate language pack to the server that's running SharePoint Products to meet requirements for Team Foundation Server.

The following table outlines the language combinations that are supported:

| Operating system | Azure DevOps Server or Team Foundation Server | Sharepoint Products |
| --- | --- | --- |
| English | English | English |
| English | Language other than English | Language (or language pack) must match Team Foundation Server |
| Language other than English | English | English (or English language pack added) |
| Language other than English | Language must match the operating system | Language (or language pack added) to match Team Foundation Server |

The following rules clarify the language requirements for Azure DevOps Server and Team Foundation Server installations.

-   If you're running an English language operating system, you can install any language version of Azure DevOps Server or Team Foundation Server. If you aren't running an English language operating system, you must install the English version of Azure DevOps Server or Team Foundation Server or the version that has been localized for the same language as the operating system.

-   If you want to use SharePoint Products, the SharePoint Products installation must match the language of the Team Foundation Server installation. Alternately, you can install the language pack that matches the language of your Team Foundation Server installation.

	For example, you can install a Japanese version of Team Foundation Server on an English or Japanese operating system but not on a German operating system. If you install a Japanese version of Team Foundation Server, you must also have either a Japanese version of SharePoint Products or the Japanese language pack for SharePoint Products installed on the server that's running SharePoint Products.

The following components don't have additional language requirements specific to working with Azure DevOps Server or Team Foundation Server:

-   Team Foundation Build service
-   Team Foundation Server Proxy
-   Team Explorer
-   Visual Studio Lab Management

Test controllers and agents have their own language requirements. For more information, see [Test controller and test agent requirements](https://msdn.microsoft.com/library/ff937706.aspx).

## More information

For more information about Azure DevOps Server or TFS requirements for companion products, see the following articles:

* [SQL Server requirements for Azure DevOps Server or Team Foundation Server](#sql-server)
 
	Azure DevOps Server and Team Foundation Server require SQL Server. However, you have many options for installing SQL Server. One option is to let Azure DevOps Server or Team Foundation Server automatically install SQL Server Express.

* [SharePoint Products requirements for Team Foundation Server](requirements.md#sharepoint)  

	Azure DevOps Server and Team Foundation Server don't require SharePoint Products.

* [Azure Artifacts and version compatibility](/azure/devops/artifacts/overview?view=vsts#versions-and-compatibility)


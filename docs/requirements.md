---
title: Requirements for setup, upgrade, and administration
titleSuffix: Azure DevOps Server & TFS  
description: hardware, operating systems, SQL Server requirements to install Azure DevOps Server and TFS
ms.prod: devops-server
ms.technology: tfs-admin
toc: show
ms.manager: jillfra
ms.author: aaronha
author: aaronhallberg
ms.topic: conceptual
monikerRange: '>= tfs-2013'
ms.date: 03/05/2019
---

# Requirements for Azure DevOps on-premises

[!INCLUDE [temp](_shared/version-tfs-all-versions.md)]

Prior to installing or upgrading an Azure DevOps deployment, review the requirements provided in this article. 

In addition to these requirements, review the following articles as well: 

- [Client and on-premises build compatibility](compatibility.md)
- [Service account requirements](account-requirements.md)
- [Architecture overview](./architecture/architecture.md)
- [Default network ports and protocols](./architecture/architecture.md#default-network-settings)
- [Customizable network settings](./architecture/architecture.md#customizable-network-settings)
- [Azure Artifacts and version compatibility](/azure/devops/artifacts/overview?view=vsts#versions-and-compatibility)


<a name="hardware-recommendations"></a> 
## Hardware recommendations 

Azure DevOps on-premises can scale from an Express installation on a laptop that's used by a single person to a highly available deployment that's used by thousands of people. It can support high-use scenarios that have multiple application tiers behind a load balancer and multiple SQL instances that use SQL Always On. 

The following recommendations apply to most Azure DevOps deployments. Your requirements might vary depending on how your team uses Azure DevOps. For example, if you have particularly large Git repositories or Team Foundation version control (TVC) branches, you might need higher-spec machines than those listed in the following sections. All the machines that are described in the next sections can be either physical or virtual.

### Single-server deployment

A single-server deployment consists of a single machine with one dual-core processor, 4 GB of RAM, and a fast hard-disk drive. This configuration typically supports up to 250 users of core source control (Team Foundation Version Control or Git) and work item tracking functionality. Extensive use of automated build, test, or release likely will cause performance issues. We don't recommend use of search or reporting features for this configuration.

When you scale up a single server, the server can handle a larger number of users and an increased use of automated build, test, or release. A scaled-up server can also use search or reporting features. For example, increasing RAM to 8 GB should enable a single-server deployment to scale up to 500 users.

For evaluation or personal use, you can use a basic configuration with as little as 1 GB of RAM. This configuration isn't recommended for a production server that's used by more than one person.

### Multi-server deployments

The following scenarios might require a multiple-server deployment:

::: moniker range=">= tfs-2018"

- Scaling beyond 500 users
- Extensive use of automated build, test, or release
- Using Code Search
- Using reporting features
::: moniker-end

::: moniker range="<= tfs-2017"

- Scaling beyond 500 users
- Extensive use of automated build, test, or release
- Using Code Search
- Using reporting features
- Using SharePoint integration
::: moniker-end

For a team of more than 500 users, consider the following setup:

- An application tier with one dual-core processor, 8 GB of memory, and a fast hard-disk drive.
- A data tier with one quad-core processor, 8 GB of memory, and high-performance storage, such as an SSD.

For a team of more than 2,000 users, consider the following setup:

- An application tier with one quad-core processor, 16 GB or more of memory, and a fast hard-disk drive.
- A data tier with two or more quad-core processors, 16 GB or more of memory, and advanced high-performance storage, like an SSD or high-performance SAN.

If you plan to use build, test, or release automation extensively, we recommend that you use higher-spec application and data tiers to avoid performance issues. For example, a team of 250 might use a multiple-server deployment that is more in line with the recommendations for a team of 500 to 2,000 users. We also recommend that you monitor your automated processes to ensure that they are efficient. For example, retrieve data from source control incrementally during builds whenever possible instead of fully refreshing with each build. 

> [!NOTE]
> Except for very small teams that have extremely limited use of these features, we don't recommend installing build, test, or release agents on your Azure DevOps Server or TFS application tiers.


If you plan to use Code Search, we recommend that you set up a separate server for Code Search. For more information, see the [hardware requirements for Code Search](/azure/devops/project/search/administration?view=tfs-2017).

If you plan to use reporting features, we recommend that you set up a separate server for your warehouse database and SQL Server Analysis Services cube. Another option is to use a higher-spec data tier.

::: moniker range="<= tfs-2017"

If you plan to use SharePoint integration, we recommend that you set up a separate server for your SharePoint instance or that you use a higher-spec application tier. 
::: moniker-end

If you want to guarantee high availability, consider using multiple application tiers behind a load balancer and multiple SQL Server instances. In this scenario, we recommend that you put your Azure DevOps databases in an Always On Availability Group.

### Build service hardware requirements

The XAML build service has the same operating system requirements as Azure DevOps Server and TFS. Usually, it makes sense to run the build service on a separate machine from the application tier. Hardware requirements for the build service are the same as the operating system on which it's running. However, you can optimize build service performance by tailoring the hardware specs of your build machine to the types of builds your team will use.

<!-- QUESTION: For more information, see System requirements for Team Foundation Build Service  -->

<a name="operating-systems"></a> 
## Operating systems

The following operating systems are supported for the indicated versions of Azure DevOps Server and Team Foundation Server (TFS).

### Server or client installation

- **Azure DevOps Server**
  - Runs on either a Windows Server operating system or a Windows client operating system.
  - Azure DevOps Server 2019, TFS 2018, and TFS 2017 run only on a 64-bit operating system.

- **Team Foundation Server**: 
  - Runs on either a Windows Server operating system or a Windows client operating system.
  - Earlier versions of TFS run on either a 64-bit or a 32-bit operating system when a 32-bit version is available. We recommend that you use a server operating system unless your Azure DevOps Server or Team Foundation Server instance is for evaluation or personal use.

### Server operating systems
  
Azure DevOps Server or TFS version | Supported server operating systems
------------|--------------------------------
Azure DevOps Server 2019 | Windows Server 2019<br/>Windows Server 2016<br/>Windows Server 2012 R2 (Essentials, Standard, Datacenter)<br/>Windows Server 2012 (Essentials, Standard, Datacenter)
TFS 2018 | Windows Server 2016<br/>Windows Server 2012 R2 (Essentials, Standard, Datacenter)<br/>Windows Server 2012 (Essentials, Standard, Datacenter)
TFS 2017 | Windows Server 2016<br/>Windows Server 2012 R2 (Essentials, Standard, Datacenter)<br/>Windows Server 2012 (Essentials, Standard, Datacenter)<br/>Windows Server 2008 R2 (minimum SP1) (Standard, Enterprise, Datacenter)
TFS 2015 | Windows Server 2016<br/>Windows Server 2012 R2 (Essentials, Standard, Datacenter)<br/>Windows Server 2012 (Essentials, Standard, Datacenter)<br/>Windows Server 2008 R2 (minimum SP1) (Standard, Enterprise, Datacenter)
TFS 2013 | Windows Server 2012 R2 (Essentials, Standard, Datacenter)<br/>Windows Server 2012 (Essentials, Standard, Datacenter)<br/>Windows Server 2008 R2 (minimum SP1) (Standard, Enterprise, Datacenter)
TFS 2012 | Windows Server 2012 R2 (Essentials, Standard, Datacenter)<br/>Windows Server 2012 (Essentials, Standard, Datacenter)<br/>Windows Server 2008 R2 (Standard, Enterprise, Datacenter)<br/>Windows Server 2008 (minimum SP2)<br/>Windows Small Business Server 2011 (Standard, Essentials, Premium Add-On)<br/>Windows Home Server 2011
TFS 2010 | Windows Server 2008 R2 (Standard, Enterprise, Datacenter)<br/>Windows Server 2008 (minimum SP2)<br/>Windows Server 2003 R2<br/>Windows Server 2003 (minimum SP2)

The [Server Core](/windows-server/administration/server-core/what-is-server-core) installation option is supported only for Azure DevOps Server 2019, TFS 2018, and TFS 2017. [Windows Server version 1709](/windows-server/get-started/get-started-with-1709) isn't supported.

### Client operating systems

Azure DevOps Server version | Supported client operating systems
------------|--------------------------------
Azure DevOps Server 2019 | Windows 10 (Professional, Enterprise) Version 1607 or later
TFS 2018 | Windows 10 (Professional, Enterprise) Version 1607 or later
TFS 2017 | Windows 10 (Home, Professional, Enterprise)<br/>Windows 8.1 (Basic, Professional, Enterprise)<br/>Windows 7 (minimum SP1) (Home Premium, Professional, Enterprise, Ultimate)
TFS 2015 | Windows 10 (Home, Professional, Enterprise)<br/>Windows 8.1 (Basic, Professional, Enterprise)<br/>Windows 7 (minimum SP1) (Home Premium, Professional, Enterprise, Ultimate)
TFS 2013 | Windows 8.1 (Basic, Professional, Enterprise)<br/>Windows 7 (minimum SP1) (Home Premium, Professional, Enterprise, Ultimate)
TFS 2012 | Windows 8.1 (Basic, Professional, Enterprise)<br/>Windows 7 (Home Premium, Professional, Enterprise, Ultimate)
TFS 2010 | Windows 7 (Home Premium, Professional, Enterprise, Ultimate)<br/>Windows Vista SP2

Although you can install Azure DevOps Server on client operating systems, we don't recommend client operating system installation except for evaluation purposes or personal use. Client operating systems have the following restrictions:

- Client operating systems don't support integration with SharePoint Products or SharePoint Reporting.
- You can't install Azure DevOps Server Proxy and Team Foundation Server Proxy on client operating systems. 

If you need to use any of these features, install Azure DevOps Server on a server operating system.

<a name="proxy-server"></a> 
## Proxy server requirements

The proxy feature is available when you install Azure DevOps Server or TFS on a server operating system.

Review the following hardware recommendations to determine the optimal hardware to use for Azure DevOps Server Proxy or Team Foundation Server Proxy.

Unlike operating system requirements, hardware recommendations for proxy are different from hardware recommendations for setting up the application tier of Azure DevOps Server or Team Foundation Server. The application tier of Team Foundation Server requires more robust hardware than the proxy feature.

Recommended hardware is based on the size of the team that will use the proxy server. Usually, this is the team in your remote office. The larger your team, the more robust your hardware must be.

| Remote team size | Hardware recommendations (CPU/RAM) for Azure DevOps Server Proxy or Team Foundation Server Proxy |
|---|---|
| 450 or fewer users | One processor, 2.2-GHz CPU, 2 GB of RAM |
| Between 451 and 2,200 users | Two processors, 2.0-GHz CPU, 2 GB of RAM |
| Between 2,201 and 3,600 users | Four processors, 2.0-GHz CPU, 2 GB of RAM |

<a name="gvfs-proxy-server"></a> 			
### GVFS proxy additional requirements
The Git Virtual File System (GVFS) proxy feature supports intensive input/output (I/O) operations. In addition to the basic requirements for Azure DevOps Server Proxy or Team Foundation Server Proxy, GVFS proxying requires a fast, large disk to operate efficiently on the repository. Recommended hardware is based on the size of the repository that the GVFS proxy serves.

| Hardware | Recommended value |
|---|---|
| RAM | As large as the tip of a typical branch |
| Disk space | Four times the repository's entire size |
| Disk hardware | A solid-state drive (SSD) |

For example, if a repository has 50 GB at the tip of **master** and 200 GB of history, we recommend 50 GB of RAM and 800 GB of SSD-based storage.

## Virtualization

Microsoft supports Azure DevOps Server virtualization in supported virtualization environments.

For more information, see the following articles:

* [Microsoft server software and supported virtualization environments](http://go.microsoft.com/fwlink/?LinkId=196061)
* [Support policy for Microsoft software running in non-Microsoft hardware virtualization software](http://go.microsoft.com/fwlink/?LinkId=196062)
* [Support partners for non-Microsoft hardware virtualization software](http://go.microsoft.com/fwlink/?LinkId=196063)
* [Server virtualization](http://go.microsoft.com/fwlink/?LinkId=196072) (officially supported products)

<a name="sql-server"></a> 
## Azure SQL Database and SQL Server

Azure DevOps on-premise deployments require some version of SQL Server. Azure DevOps Server supports Express, Standard, and Enterprise [SQL Server editions](https://www.microsoft.com/sql-server/sql-server-2017-editions). The Express edition is recommended only for evaluation purposes, personal use, or for very small teams. We recommend the SQL Server Standard or Enterprise versions for all other scenarios.

For production deployments, use one of the following versions of SQL Server.

> [!div class="mx-tdCol2BreakAll"]  
> |Azure DevOps version | Supported SQL Server version
> |-------------------|------------------------------------
> |Azure DevOps Server 2019 | Azure SQL Database<br/>SQL Server 2017<br/>SQL Server 2016 (minimum SP1) |
> |TFS 2018 | SQL Server 2017<br/>SQL Server 2016 (minimum SP1) |
> |TFS 2017 Update 1 | SQL Server 2016 (minimum SP1)<br/>SQL Server 2014 |
> |TFS 2017 | SQL Server 2016<br/>SQL Server 2014 |
> |TFS 2015 Update 3 | SQL Server 2016<br/>SQL Server 2014<br/>SQL Server 2012 (minimum SP1) |
> |TFS 2015 | SQL Server 2014<br/>SQL Server 2012 (minimum SP1) |
> |TFS 2013 Update 2  | SQL Server 2014<br/>SQL Server 2012 (minimum SP1) |
> |TFS 2013 | SQL Server 2012 (minimum SP1) |
> |TFS 2012 | SQL Server 2012<br/>SQL Server 2008 R2 |
> |TFS 2010 | SQL Server 2008 R2<br/>SQL Server 2008 |

> [!NOTE]   
> SQL Server on Linux  isn't supported. 

### Additional version notes

The following information applies to the indicated SQL Server version:

- **Azure SQL Database**: Only supported when you also use Azure Virtual Machines. For details, see [Use Azure SQL Database with Azure DevOps Server](install/install-azure-sql.md). 
- **SQL Server 2016**: If you use SQL Server 2016, you must install a Visual C++ runtime [update](http://support.microsoft.com/kb/3138367).  
- **SQL Server 2014**: SQL Server 2014 has more robust hardware requirements than earlier SQL Server versions. Some hardware configurations might reduce performance in Azure DevOps Server or Team Foundation Server. For more information, see [TFS 2013 Update 2: Performance considerations for using SQL Server 2014](http://support.microsoft.com/kb/2953452).  
- **SQL Server 2012 SP1**: If you use SQL Server 2012 SP1, we recommend that you apply [Cumulative Update 2](http://support.microsoft.com/kb/2790947) on top of SP1 to address a critical SQL Server bug related to resource consumption. This isn't a requirement because the bug affects only a small number of SQL Server 2012 SP1 instances, but it's important to be aware of it.  

	If you don't apply Cumulative Update 2, apply a SQL Server hotfix ([KB2793634](http://support.microsoft.com/kb/2793634)) to address a separate issue in which SQL Server 2012 SP1 might request an excessive number of restarts.




## Active Directory

You can install Azure DevOps on more than one server if the servers are all joined to an Azure Active Directory domain that's based on a functional level that the servers support. You can install Azure DevOps on a single server that's joined to an Active Directory domain or that is a member of a workgroup.

You can't install Azure DevOps on servers that are joined to domains if the domain controllers are running Windows NT Server 4.0. The following table shows which functional levels for Active Directory domains Azure DevOps Server and TFS don't support:

| Functional levels for Active Directory domains | Supported |
| --- | --- |
| **Windows 2000 mixed mode**: Domain controllers that are running Windows Server 2003 R2, Windows Server 2003, Windows 2000, and Windows NT Server 4.0. | No |
|**Windows Server 2003 interim mode**: Domain controllers that are running Windows Server 2003 R2, Windows Server 2003, and Windows NT Server 4.0. | No |



## Major releases and service packs

Microsoft doesn't always immediately support major new versions of dependencies like SQL Server. Sometimes, we must release updates to add support for those versions. 
However, when Microsoft supports a major version, we always support the latest service pack immediately when it's released. We work with product teams to test service packs before they're released.


## <a name="languages"></a> Natural languages

::: moniker range=">= tfs-2018"
You can install Azure DevOps in various languages on supported operating systems. However, you can't use any combination of localized operating system with Azure DevOps Server and TFS. Also, you can't install multiple languages on a single Azure DevOps Server or TFS server. 

::: moniker-end

::: moniker range="<= tfs-2017"
You can install Azure DevOps in various languages on supported operating systems. However, you can't use any combination of localized operating system with Azure DevOps Server and TFS. Also, you can't install multiple languages on a single Azure DevOps Server or TFS server. The language of the SharePoint Products installation can also complicate your deployment. However, you can add an appropriate language pack to the server that's running SharePoint Products to meet requirements for Team Foundation Server.



The following table outlines the language combinations that are supported:

| Operating system | Azure DevOps Server or Team Foundation Server | Sharepoint Products |
| --- | --- | --- |
| English | English | English |
| English | Language other than English | Language (or language pack) must match Team Foundation Server |
| Language other than English | English | English (or English language pack added) |
| Language other than English | Language must match the operating system | Language (or language pack added) to match Team Foundation Server |

The following rules clarify the language requirements for Azure DevOps Server and Team Foundation Server installations.

-   If you're running an English language operating system, you can install any language version of Azure DevOps Server or Team Foundation Server. If you aren't running an English language operating system, you must install the English version of Azure DevOps Server or Team Foundation Server or the version that has been localized for the same language as the operating system.

- The following components don't have additional language requirements specific to working with Azure DevOps Server or TFS:

	-   Team Foundation Build server
	-   Team Foundation Server Proxy
	-   Team Explorer
	-   Visual Studio Lab Management (deprecated with TFS 2017 and later versions) 

::: moniker range="<= tfs-2017"
-   If you want to use SharePoint Products, the SharePoint Products installation must match the language of the Team Foundation Server installation. Alternately, you can install the language pack that matches the language of your Team Foundation Server installation.

	For example, you can install a Japanese version of Team Foundation Server on an English or Japanese operating system but not on a German operating system. If you install a Japanese version of Team Foundation Server, you must also have either a Japanese version of SharePoint Products or the Japanese language pack for SharePoint Products installed on the server that's running SharePoint Products.
::: moniker-end


Test controllers and agents have their own language requirements. For more information, see [Test controller and test agent requirements](/visualstudio/test/test-controller-and-test-agent-requirements-for-load-testing).

::: moniker range="<= tfs-2018"
<a name="sharepoint"></a> 
## SharePoint

TFS 2018 and Azure DevOps Server no longer support integration with Office SharePoint and the TFS Extension for SharePoint. For information about TFS integration with SharePoint, see [TFS-SharePoint version compatibility](/azure/devops/report/sharepoint-dashboards/about-sharepoint-integration?#compat).

::: moniker-end

::: moniker range="<= tfs-2017"
<a name="project-server"></a> 
## Project Server

TFS 2017 and later versions no longer support native integration with Office Project Server. For information about TFS integration with Project Server, see [TFS-Project Server version compatibility](/azure/devops/reference/tfs-ps-sync/system-and-setup-requirements?view=vsts#tfs-project-server-version-compability).

::: moniker-end

## Related articles
- [Client and on-premises build compatibility](compatibility.md)
- [Service account requirements](account-requirements.md)
- [Architecture overview](./architecture/architecture.md)
- [Default network ports and protocols](./architecture/architecture.md#default-network-settings)
- [Customizable network settings](./architecture/architecture.md#customizable-network-settings)
- [Azure Artifacts and version compatibility](/azure/devops/artifacts/overview?view=vsts#versions-and-compatibility)


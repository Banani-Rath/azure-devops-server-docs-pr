---
title: Application areas and resource dependencies
titleSuffix: Azure DevOps Server
description: Understand what application services require configured resources  
ms.topic: conceptual
ms.manager: jillfra
ms.author: aaronha
author: aaronhallberg
ms.prod: devops-server
ms.technology: tfs-admin
monikerRange: '>= tfs-2013'
ms.date: 07/28/2019
--- 

# Application areas and resource dependencies

[!INCLUDE [temp](../_shared/version-tfs-all-versions.md)]

You configure and manage Azure DevOps Server and additional
resources to support your teams. These resources include the
application-tier and data-tier server(s), project collections which
host projects, and optional resources. 

::: moniker range=">= tfs-2018"

Optional resources can include report servers, build servers, and more. For
information on Azure DevOps Server components and architecture, see [Architecture overview](../architecture/architecture.md).

::: moniker-end

::: moniker range="<= tfs-2017"

Optional resources can include report servers,
SharePoint products, build servers, Lab Management, and more. For
information on Azure DevOps Server components and architecture, see [Architecture overview](../architecture/architecture.md).

::: moniker-end

> [!IMPORTANT]  
> You should not manually modify any Azure DevOps databases unless you're
> either instructed to do so by Microsoft Support or when you're
> following the procedures described for [manually backing up the databases](backup/manually-backup-tfs.md).  Any other modifications can invalidate your service agreement.

## Add or remove resources

You can add or remove resources to your deployment to better meet the
changing needs of your business and your software projects. You can add or remove reporting at
any time. You can also use more than one instance of SQL Server to host
the databases for your deployment. For example, you can add a server
that is running SQL Server Reporting Services to your deployment after
you install and initially configure Azure DevOps. 

::: moniker range="<= tfs-2017"

You can also upgrade the
version of SharePoint Products that supports your deployment and add its
capabilities of that product to the projects that already exist in
your deployment.

::: moniker-end

## Core service functions

When you create a project, you automatically gain access to the
following functions:

-   **Web portal** - provides a web interface to Azure DevOps Server that grants access to
    projects, Agile planning and tracking tools, version control,
    and builds. For an overview, see [Web portal navigation](/azure/devops/project/navigation/index).

-   **Source control repository** - uses [Git repositories](/azure/devops/repos/git/gitquickstart) or [Team Foundation Version Control](/azure/devops/repos/tfvc/overview).

-   **Azure Boards** - teams can create work items and work item
    queries to track, monitor, and report on the development of a
    product and its features. A work item is a database record that
    stores the definition, assignment, priority, and state of work. Your
    team can create only those types of work items that are defined in
    the process template (used to create the project), or
    types that are added to the project after it is created.

    Team members can work in the web portal or Team Explorer. To learn more about
    these and other clients that connect to Azure DevOps Server, see [Which tools and clients connect to Azure DevOps Server](/azure/devops/user-guide/tools).

## Required resources to support additional services

The following table indicates any additional servers and functionality
that you must configure for your team to have access to the
corresponding feature. You can add resources before or after you have
created your project.


::: moniker range=">= tfs-2018"

> [!div class="mx-tdCol2BreakAll"]
> | Feature area | Required resources | Related topics |
> | --- | --- | --- |
> | **Builds** | Team Foundation Build | [Configure and manage your build system](/azure/devops/build-release/overview) <br/> The **Builds** page lists the build definitions defined for your project. This page appears only when Team Foundation Build is installed and configured. Team Foundation Build enables your team to create and manage product builds. For example, a team can run daily builds and post them to a shared server. Team Foundation Build also supports build reports about the status and quality of each build. <br/>Access to the Team Foundation Build Service requires that the project collection has been configured to use a build controller. Each build controller is dedicated to a single project collection. The controller accepts build requests from any project in its collection. See [Build the application](/azure/devops/pipelines/index). |
> | **Reports** | SQL Server Analysis Services <br/>SQL Server Reporting Services | [Add reports to a project](/azure/devops/report/admin/add-reports-to-a-team-project) <br/> The **Report** page appears only when the project collection that hosts your project has been configured with both SQL Server Reporting Services and SQL Server Analysis Services. This page provides access to Report Manager and the default and custom reports that you upload to the server that hosts SQL Server Reporting Services. <br/>For an overview of the default reports, see [Reporting Services reports](/azure/devops/report/sql-reports/reporting-services-reports). |
> | Remote-site | Team Foundation | [How to: Install Azure DevOps Proxy Server and set up a remote site](../install/install-proxy-setup-remote.md) <br/>[Configure Visual Studio to connect to Azure DevOps Proxy Server](/azure/devops/organizations/projects/connect-to-projects) <br/> If some team members are located remotely from the main location for version control, you may want to install and configure Azure DevOps Proxy Server to support them.  Azure DevOps Proxy Server manages a cache of downloaded version control files in the location of the distributed team, which significantly reduces the bandwidth needed for distant connections. <br/>If clients are configured to use Azure DevOps Proxy Server, management of the files is transparent to the user. Any metadata exchange and file uploads continue to interface directly with Azure DevOps Server. See [Connect to projects in Azure DevOps Server](/azure/devops/organizations/projects/connect-to-projects). |

::: moniker-end


::: moniker range="<= tfs-2017"

> [!div class="mx-tdCol2BreakAll"]
> | Feature area | Required resources | Related topics |
> | --- | --- | --- |
> | **Builds** | Team Foundation Build | [Configure and manage your build system](/azure/devops/build-release/overview) <br/> The **Builds** page lists the build definitions defined for your project. This page appears only when Team Foundation Build is installed and configured. Team Foundation Build enables your team to create and manage product builds. For example, a team can run daily builds and post them to a shared server. Team Foundation Build also supports build reports about the status and quality of each build. <br/>Access to the Team Foundation Build Service requires that the project collection has been configured to use a build controller. Each build controller is dedicated to a single project collection. The controller accepts build requests from any project in its collection. See [Build the application](/azure/devops/pipelines/index). |
> | **Documents** (project portal) | SharePoint Products | [Add SharePoint products to your deployment](add-sharepoint-to-tfs.md) <br/>[Configure a default location for project portals](/previous-versions/visualstudio/visual-studio-2012/dd386357(v=vs.110)) <br/> The **Documents** page appears only when your project has been configured with SharePoint Products.  After the project is created, you can configure a SharePoint site or another web location as the project portal.  You may need to [configure dashboard compatibility](config-ent-sharepoint0710-dashboards.md) and [configure an enterprise application definition](../install/sharepoint/config-enterprise-app-def.md).  See also [Share information using the project portal](/previous-versions/visualstudio/visual-studio-2013/ms242883(v=vs.120)). |
> | Excel reports | SharePoint Products <br/>SQL Server Analysis Services | [Add Sharepoint products to your deployment](add-sharepoint-to-tfs.md) <br/>[Add a report server](/azure/devops/report/admin/add-a-report-server) <br/> Microsoft Excel reports are uploaded to the **Document** node Documents folder when you configure your project with a SharePoint site. With these reports you can track your project's burn rate, bug backlog, software quality, test progress, and other metrics. Many of these reports display within your project's dashboards. In addition to the SharePoint Products dependency, Excel reports depend on your project collection that hosts your project has been configured with both SQL Server Reporting Services and SQL Server Analysis Services. <br/>For an overview of the default Excel reports, see [Excel reports](/azure/devops/report/excel/excel-reports) or [Excel reports (CMMI)](/azure/devops/report/excel/excel-reports-cmmi). <br/>If your project doesn't have a SharePoint site, you can still use Excel to create status and trend reports. See [Create Excel reports from a work item query](/azure/devops/report/excel/create-status-and-trend-excel-reports). |
> | **Reports** | SQL Server Analysis Services <br/>SQL Server Reporting Services | [Add reports to a project](/azure/devops/report/admin/add-reports-to-a-team-project) <br/> The **Report** page appears only when the project collection that hosts your project has been configured with both SQL Server Reporting Services and SQL Server Analysis Services. This page provides access to Report Manager and the default and custom reports that you upload to the server that hosts SQL Server Reporting Services. <br/>For an overview of the default reports, see [Reporting Services reports](https://msdn.microsoft.com/library/dd380714). |
> | Remote-site | Team Foundation | [How to: Install Team Foundation Server Proxy and set up a remote site](../install/install-proxy-setup-remote.md) <br/>[Configure Visual Studio to connect to Team Foundation Server Proxy](/azure/devops/organizations/projects/connect-to-projects) <br/> If some team members are located remotely from the main location for version control, you may want to install and configure Team Foundation Server Proxy to support them.  Team Foundation Server Proxy manages a cache of downloaded version control files in the location of the distributed team, which significantly reduces the bandwidth needed for distant connections. <br/>If clients are configured to use Team Foundation Server Proxy, management of the files is transparent to the user. Any metadata exchange and file uploads continue to interface directly with Azure DevOps Server. See [Connect to projects in Azure DevOps Server](/azure/devops/organizations/projects/connect-to-projects). |

::: moniker-end

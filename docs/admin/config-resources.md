---
title: Configure and manage resources
titleSuffix: Azure DevOps Server & TFS  
description: Configure and manage Team Foundation Server resources
ms.topic: conceptual
ms.manager: jillfra
ms.author: aaronha
author: aaronhallberg
ms.prod: devops-server
ms.technology: tfs-admin
monikerRange: '>= tfs-2013'
ms.date: 03/05/2019
--- 

# Configure and manage resources for Azure DevOps on-premises

[!INCLUDE [temp](../_shared/version-tfs-all-versions.md)]

<!--- NEEDS UPDATE, move table info into admin-quick-ref and see how to simplify 
Currently this is a mish-mosh of info, needs some IA love -->

You configure and manage Azure DevOps Server, previously named Team Foundation Server (TFS), and additional
resources to support your teams. These resources include the
application-tier and data-tier server(s), project collections which
host projects, and optional resources. 

Optional resources can include report servers,
SharePoint products, build servers, lab management, and more. For
information on TFS components and architecture, see <span>[Team Foundation Server architecture](../architecture/architecture.md).

> Important:
> You should not manually modify any of the TFS databases unless you're
> either instructed to do so by Microsoft Support or when you're
> following the procedures described for [manually backing up the databases](backup/manually-backup-tfs.md).  Any other modifications can invalidate your service agreement.

Through the Team Foundation Server Administration Console, you can
manage and monitor your server configuration. Tasks you can accomplish
through the administration console are indicated with this image: ![Team Foundation Server Administration Console](_img/admin-console-button.png).

 


## Application areas and resource dependencies

You can add or remove resources to your deployment to better meet the
changing needs of your business and the software projects that you
support with TFS. You can add or remove reporting and Web resources at
any time. You can also use more than one instance of SQL Server to host
the databases for your deployment. For example, you can add a server
that is running SQL Server Reporting Services to your deployment after
you install and initially configure TFS. You can also upgrade the
version of SharePoint Products that supports your deployment and add its
capabilities of that product to the projects that already exist in
your deployment.

When you create a project, you automatically gain access to the
following functions:

-   Web portal: provides a web interface to Azure DevOps services that grants access to
    projects, Agile planning and tracking tools, version control,
    and builds. For an overview, see [Web portal navigation](/azure/devops/project/navigation/index).

-   Source control repository using Team Foundation [version
    control](/azure/devops/git/overview) or [Git repositories](/azure/devops/git/gitquickstart).

-   Work item tracking: teams can create work items and work item
    queries to track, monitor, and report on the development of a
    product and its features. A work item is a database record that
    stores the definition, assignment, priority, and state of work. Your
    team can create only those types of work items that are defined in
    the process template that is used to create the project or
    types that are added to the project after it is created.

    Team members can work in TWA or Team Explorer. To learn more about
    these and other clients that connect to TFS, see [Choose the Team Foundation client to support your tasks](https://msdn.microsoft.com/library/ms181304.aspx).

The following table indicates the additional servers and functionality
that you must configure for your team to have access to the
corresponding feature. You can add resources before or after you have
created your project.

| Feature area | Required resources | Related topics | Notes |
| --- | --- | --- | --- |
| **Builds** | Team Foundation Build | [Configure and manage your build system](/azure/devops/build-release/overview) | The **Builds** page lists the build definitions defined for your project. This page appears only when Team Foundation Build is installed and configured. Team Foundation Build enables your team to create and manage product builds. For example, a team can run daily builds and post them to a shared server. Team Foundation Build also supports build reports about the status and quality of each build. </br> Access to Team Foundation Build Service requires that the project collection has been configured to use a build controller. Each build controller is dedicated to a single project collection. The controller accepts build requests from any project in a specified collection. See <span>[Build the application](https://msdn.microsoft.com/library/ms181709). |
| **Documents** (project portal) | SharePoit Products | [Add SharePoint products to your deployment](add-sharepoint-to-tfs.md) </br> [Configure a Default Location for Project Portals](https://msdn.microsoft.com/library/dd386357) | The **Documents** page appears only when your project has been configured with SharePoint Products.  After the project is created, you can configure a SharePoint site or another web location as the project portal.  You may need to [configure dashboard compatibility](config-ent-sharepoint0710-dashboards.md) and [configure an enterprise application definition](../install/sharepoint/config-enterprise-app-def.md).  See also [Share information using the project portal](https://msdn.microsoft.com/library/ms242883(v=vs.120).aspx). |
| Excel reports | SharePoint Products </br> SQL Server Analysis Services | [Add Sharepoint products to your deployment](add-sharepoint-to-tfs.md) </br> [Add a report server](/azure/devops/report/admin/add-a-report-server) | Microsoft Excel reports are uploaded to the **Document** node Documents folder when you configure your project with a SharePoint site. With these reports you can track your project's burn rate, bug backlog, software quality, test progress, and other metrics. Many of these reports display within your project's dashboards. In addition to the SharePoint Products dependency, Excel reports depend on your project collection that hosts your project has been configured with both SQL Server Analysis Services. </br> For an overview of the default Excel reports, see [Excel reports](https://msdn.microsoft.com/library/dd997876) or [Excel reports (CMMI)](https://msdn.microsoft.com/library/ee461589). </br> If your project doesn't have a SharePoint site, you can still use Excel to create status and trend reports. See [Creating Reports in Microsoft Excel by Using Work Item Queries](/azure/devops/report/excel/create-status-and-trend-excel-reports). |
| **Reports** | SQL Server Analysis Services </br> SQL Server Reporting Services | [Add reports to a project](/azure/devops/report/admin/add-reports-to-a-team-project) | The **Report** page appears only when the project collection that hosts your project has been configured with both SQL Server Reporting Services and SQL Server Analysis Services. This page provides access to Report Manager and the default and custom reports that you upload to the server that hosts SQL Server Reporting Services. </br> For an overview of the default reports, see [Reporting Services Reports](https://msdn.microsoft.com/library/dd380714). |
| Remote-site | Team Foundation | [How to: Install Team Foundation Proxy and set up a remote site](../install/install-proxy-setup-remote.md) </br> [Configure Visual Studio to connect to TFS Proxy](/azure/devops/user-guide/connect-team-projects) | If some team members are located remotely from the main location for version control, you may want to install and configure Team Foundation Server Proxy to support them.  TFS Proxy manages a cache of downloaded version control files in the location of the distributed team, which significantly reduces the bandwidth that is needed across wide area connections. </br> If clients are configured to use Team Foundation Server Proxy, management of the files is transparent to the user. Any metadata exchange and file uploads continue to interface directly with TFS. See [Connect to projects in Team Foundation Server](). |
| Virtual environments | Visual Studio Lab Management | [Configure Lab Management for SCVMM environments](config-lab-scvmm-envs.md) | By using Lab Management, your team can create, assign, and track virtual environments to support application development, deployment, and tests. Testing teams can test applications by using Microsoft Test Manager when their project is configured to use these virtual environments. |
|Automate deployments | Release Management | [Automate deployments with Release Management](https://msdn.microsoft.com/library/dn217874.aspx) | You can support a rapid release cadence and manage simultaneous releases using Release Management. Set up release paths that represent your stages from development to production. Run actions to deploy your app to an environment for that stage. |
| Synchronize with Project Server (deprecated for TFS 2017) | TFS-Project server Integration | [Synchronize Team Foundation Server with Project Server](https://msdn.microsoft.com/library/gg455680.aspx) | To support data to flow from work items TFS to tasks in enterprise project plans in Project Server, you install Team Foundation Server Extensions for Project Server on the server hosting Project Server. This integration enables project managers and software development teams to use the tools that they prefer, work at the level of precision that supports their needs, and share information transparently. |
| Capture production incidents | Preemptive Analytics | [Preemptive Analytics](https://www.preemptive.com/pa) | With PreEmptive Analytics for Team Foundation Server, development teams can capture production incidents (unhandled, caught, and thrown exceptions) and create and update TFS work items based on custom rules and thresholds. </br> You configure PreEmptive Analytics through the Team Foundation Administrator Console. |



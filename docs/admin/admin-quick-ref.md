---
title: What are the administrative tasks?
titleSuffix: Azure DevOps Server & TFS
description: Administrative tasks quick reference for Azure DevOps Server and Team Foundation Server
ms.topic: conceptual
ms.manager: jillfra
ms.author: kaelli
author: aaronhallberg
ms.prod: devops-server
ms.technology: tfs-admin
monikerRange: '>= tfs-2013'
ms.date: 05/31/2019
--- 

# Administrative tasks quick reference 

[!INCLUDE [temp](../_shared/version-tfs-all-versions.md)]

Use this index to quickly access information about tasks for managing Azure DevOps on-premises servers. 


## Install, upgrade, and general admin tasks 

<ul>
<li><a href="../install/get-started.md" data-raw-source="[Install get started](../install/get-started.md)">Install get started</a></li>
<li><a href="../install/sql-server/install-sql-server.md" data-raw-source="[Install SQL Server](../install/sql-server/install-sql-server.md)">Install SQL Server</a>
<li><a href="../upgrade/get-started.md" data-raw-source="[Upgrade get started](../upgrade/get-started.md)">Upgrade get started</a></li>
<li><a href="../upgrade/express.md" data-raw-source="[Upgrade TFS Express](../upgrade/express.md)">Upgrade TFS Express</a></li>
<li><a href="open-admin-console.md" data-raw-source="[Open the Administration Console](open-admin-console.md)">Open the Administration Console</a></li>
</ul>


## Server-level administrative tasks

Members of the [Azure DevOps Server Administrators or Team Foundation Server Administrators](add-administrator.md) group are tasked with server maintenance and configuring resources for all project collections. They also can perform all tasks to administer projects, collections and server instances.   

Many tasks are performed from the Azure DevOps Server Administration Console. The main task they perform from the web portal is to [set access levels for a user or security group](/azure/devops/organizations/security/change-access-levels?toc=/azure/devops/server/toc.json&bc=/azure/devops/server/breadcrumb/toc.json). 


<table valign="top">
<tbody valign="top">
<tr>
<td width="50%"> 
<h3>Manage users and access</h3>
<ul>
<li><a href="add-administrator.md" data-raw-source="[Add administration console users](add-administrator.md)">Add administration console users</a></li> 
<li><a href="add-administrator.md" data-raw-source="[Add server-level administrators](add-administrator.md)">Add server-level administrators</a></li>
<li><a href="/azure/devops/organizations/security/change-access-levels?toc=/azure/devops/server/toc.json&amp;bc=/azure/devops/server/breadcrumb/toc.json" data-raw-source="[Change access levels](/azure/devops/organizations/security/change-access-levels?toc=/azure/devops/server/toc.json&amp;bc=/azure/devops/server/breadcrumb/toc.json)">Change access levels</a></li>
<li><a href="setup-ad-groups.md" data-raw-source="[Set up groups for use in Azure DevOps deployments](setup-ad-groups.md)">Set up groups for use in Azure DevOps deployments</a></li>
</ul>

<h3>Server configuration </h3>
<ul>
<li><a href="change-caching-app-tier.md" data-raw-source="[Change cache settings for an application-tier server](change-caching-app-tier.md)">Change cache settings for an application-tier server</a></li>
<li><a href="websitesettings.md" data-raw-source="[Change SSH Settings](websitesettings.md)">Change SSH Settings</a></li>
<li><a href="setup-customize-alerts.md" data-raw-source="[Configure an SMTP server](setup-customize-alerts.md)">Configure an SMTP server</a></li>
<li><a href="setup-customize-alerts.md" data-raw-source="[Customize email for alerts and feedback requests](setup-customize-alerts.md)">Customize email for alerts and feedback requests</a></li>
<li><a href="open-admin-console.md#public-url" data-raw-source="[View or change the Public URL](open-admin-console.md#public-url)">View or change the Public URL</a></li>
</ul>

<h3>Server maintenance </h3>
<ul>
<li><a href="change-service-account-password.md" data-raw-source="[Change the service account or password for TFS](change-service-account-password.md)">Change the service account or password for TFS</a></li>
<li><a href="change-caching-app-tier.md" data-raw-source="[Change cache settings for an application-tier server](change-caching-app-tier.md)">Change cache settings for an application-tier server</a></li>
<li><a href="stop-start-services-pools.md" data-raw-source="[Stop and start services, application pools, and websites](stop-start-services-pools.md)">Stop and start services, application pools, and websites</a></li>
</ul>


</td>
<td width="50%"> 
<h3>Manage databases</h3>
<ul>
<li><a href="backup/back-up-restore.md" data-raw-source="[Back up and restore](backup/back-up-restore.md)">Back up and restore</a></li>
<li><a href="backup/config-backup-sched-plan.md" data-raw-source="[Configure a backup schedule and plan](backup/config-backup-sched-plan.md)">Configure a backup schedule and plan</a></li>
<li><a href="backup/backup-db-architecture.md" data-raw-source="[Understand backing up Azure DevOps on-premises](backup/backup-db-architecture.md)">Understand backing up Azure DevOps on-premises</a></li>
</ul>
<h3>SQL Server reporting</h3>
<ul>
<li><a href="/azure/devops/report/admin/add-reports-to-a-team-project?toc=/azure/devops/server/toc.json&amp;bc=/azure/devops/server/breadcrumb/toc.json" data-raw-source="[Add reports to a project](/azure/devops/report/admin/add-reports-to-a-team-project?toc=/azure/devops/server/toc.json&amp;bc=/azure/devops/server/breadcrumb/toc.json)">Add reports to a project</a></li>
<li><a href="/azure/devops/report/admin/manage-reports-data-warehouse-cube?toc=/azure/devops/server/toc.json&amp;bc=/azure/devops/server/breadcrumb/toc.json" data-raw-source="[Manage the data warehouse and analysis services cube](/azure/devops/report/admin/manage-reports-data-warehouse-cube?toc=/azure/devops/server/toc.json&amp;bc=/azure/devops/server/breadcrumb/toc.json)">Manage the data warehouse and analysis services cube</a></li>
<li><a href="change-service-account-or-password-sql-reporting.md" data-raw-source="[Change the service account or password for SQL Server Reporting Services](change-service-account-or-password-sql-reporting.md)">Change the service account or password for SQL Server Reporting Services</a></li> 
</ul>
<h3>SharePoint product integration (valid for TFS 2017 and earlier versions)</h3>
<ul>
<li><a href="add-sharepoint-to-tfs.md" data-raw-source="[Add SharePoint products to your deployment](add-sharepoint-to-tfs.md)">Add SharePoint products to your deployment</a></li>
<li><a href="/azure/devops/report/sharepoint-dashboards/configure-or-add-a-project-portal?toc=/azure/devops/server/toc.json&amp;bc=/azure/devops/server/breadcrumb/toc.json" data-raw-source="[Configure or add a project portal](/azure/devops/report/sharepoint-dashboards/configure-or-add-a-project-portal?toc=/azure/devops/server/toc.json&amp;bc=/azure/devops/server/breadcrumb/toc.json)">Configure or add a project portal</a></li>
</ul>
</td>
</tr>
</tbody>
</table>


## Project collection administrative tasks

Members of the [Project Collection Administrators group](/azure/devops/security/set-project-collection-level-permissions?toc=/azure/devops/server/toc.json&bc=/azure/devops/server/breadcrumb/toc.json) are tasked with configuring resources for all projects defined for a collection. They also can perform all tasks to add projects, manage projects, and manage permissions for the collection, a project, or an object.   

Before you add a a project or project collection, review the information provided in [About projects and scaling your organization](/azure/devops/organizations/projects/about-projects?toc=/azure/devops/server/toc.json&bc=/azure/devops/server/breadcrumb/toc.json).

<table valign="top">
<tbody valign="top">
<tr>
<td width="50%"> 
<h3>Add and manage project collections</h3>
<ul>

<li><a href="/azure/devops/organizations/projects/create-project" data-raw-source="[Add a project](/azure/devops/organizations/projects/create-project)">Add a project</a></li>
<li><a href="manage-project-collections.md" data-raw-source="[Add a project collection](manage-project-collections.md)">Add a project collection</a></li>
<li><a href="manage-project-collections.md" data-raw-source="[Delete/detach a project collection](manage-project-collections.md)">Delete/detach a project collection</a></li>
<li><a href="/azure/devops/organizations/security/set-project-collection-level-permissions?toc=/azure/devops/server/toc.json&amp;bc=/azure/devops/server/breadcrumb/toc.json" data-raw-source="[Add collection-level administrators](/azure/devops/organizations/security/set-project-collection-level-permissions?toc=/azure/devops/server/toc.json&amp;bc=/azure/devops/server/breadcrumb/toc.json)">Add collection-level administrators</a></li>
<li><a href="/azure/devops/notifications/howto-manage-organization-notifications?toc=/azure/devops/server/toc.json&amp;bc=/azure/devops/server/breadcrumb/toc.json" data-raw-source="[Manage collection-level notifications](/azure/devops/notifications/howto-manage-organization-notifications?toc=/azure/devops/server/toc.json&amp;bc=/azure/devops/server/breadcrumb/toc.json)">Manage collection-level notifications</a> </li>
<li><a href="move-project-collection.md" data-raw-source="[Move a project collection](move-project-collection.md)">Move a project collection</a> </li>
<li><a href="open-admin-console.md" data-raw-source="[Open the Administration Console](open-admin-console.md)">Open the Administration Console</a></li>
<li><a href="split-team-project-collection.md" data-raw-source="[Split a project collection](split-team-project-collection.md)">Split a project collection</a> </li>
</ul>

<h3>Boards/Process and work tracking customizations</h3>
<ul>
<li><a href="/azure/devops/reference/customize-work?toc=/azure/devops/server/toc.json&amp;bc=/azure/devops/server/breadcrumb/toc.json" data-raw-source="[Customize your work tracking experience](/azure/devops/reference/customize-work?toc=/azure/devops/server/toc.json&amp;bc=/azure/devops/server/breadcrumb/toc.json)">Customize your work tracking experience</a></li>
<li><a href="/azure/devops/reference/on-premises-xml-process-model?toc=/azure/devops/server/toc.json&amp;bc=/azure/devops/server/breadcrumb/toc.json" data-raw-source="[On-premises XML process model](/azure/devops/reference/on-premises-xml-process-model?toc=/azure/devops/server/toc.json&amp;bc=/azure/devops/server/breadcrumb/toc.json)">On-premises XML process model</a></li>
<li><a href="/azure/devops/organizations/settings/work/inheritance-process-model?toc=/azure/devops/server/toc.json&amp;bc=/azure/devops/server/breadcrumb/toc.json" data-raw-source="[About process customization and inherited processes](/azure/devops/organizations/settings/work/inheritance-process-model?toc=/azure/devops/server/toc.json&amp;bc=/azure/devops/server/breadcrumb/toc.json)">About process customization and inherited processes</a>
<ul>
<li><a href="/azure/devops/organizations/settings/work/customize-process?toc=/azure/devops/server/toc.json&amp;bc=/azure/devops/server/breadcrumb/toc.json" data-raw-source="[Customize a project](/azure/devops/organizations/settings/work/customize-process?toc=/azure/devops/server/toc.json&amp;bc=/azure/devops/server/breadcrumb/toc.json)">Customize a project</a></li>
<li><a href="/azure/devops/organizations/settings/work/manage-process?toc=/azure/devops/server/toc.json&amp;bc=/azure/devops/server/breadcrumb/toc.json" data-raw-source="[Add and manage processes](/azure/devops/organizations/settings/work/manage-process?toc=/azure/devops/server/toc.json&amp;bc=/azure/devops/server/breadcrumb/toc.json)">Add and manage processes</a></li>
</ul>
</li>
</ul>

</td>

<td width="50%">
<h3>Analytics (valid for Azure DevOps Server 2019)</h3>
<ul>
<li><a href="/azure/devops/report/dashboards/analytics-extension">Enable or install Analytics</a></li>
</ul>
<h3>Extensions</h3>
<ul>
<li><a href="/azure/devops/marketplace/install-extension?toc=/azure/devops/server/toc.json&amp;bc=/azure/devops/server/breadcrumb/toc.json" data-raw-source="[Install and manage Marketplace extensions](/azure/devops/marketplace/install-extension?toc=/azure/devops/server/toc.json&amp;bc=/azure/devops/server/breadcrumb/toc.json)">Install and manage Marketplace extensions</a></li>
<li><a href="/azure/devops/marketplace/approve-extensions?toc=/azure/devops/server/toc.json&amp;bc=/azure/devops/server/breadcrumb/toc.json" data-raw-source="[Approve extensions](/azure/devops/marketplace/approve-extensions?toc=/azure/devops/server/toc.json&amp;bc=/azure/devops/server/breadcrumb/toc.json)">Approve extensions</a></li>
<li><a href="/azure/devops/marketplace/assign-paid-extensions?toc=/azure/devops/server/toc.json&amp;bc=/azure/devops/server/breadcrumb/toc.json" data-raw-source="[Assign paid extension access to users](/azure/devops/marketplace/assign-paid-extensions?toc=/azure/devops/server/toc.json&amp;bc=/azure/devops/server/breadcrumb/toc.json)">Assign paid extension access to users</a></li>
<li><a href="/azure/devops/marketplace/how-to/grant-permissions?toc=/azure/devops/server/toc.json&amp;bc=/azure/devops/server/breadcrumb/toc.json" data-raw-source="[Grant permissions to manage extensions](/azure/devops/marketplace/how-to/grant-permissions?toc=/azure/devops/server/toc.json&amp;bc=/azure/devops/server/breadcrumb/toc.json)">Grant permissions to manage extensions</a></li>
<li><a href="/azure/devops/marketplace/uninstall-disable-extensions?toc=/azure/devops/server/toc.json&amp;bc=/azure/devops/server/breadcrumb/toc.json" data-raw-source="[Uninstall or disable extensions](/azure/devops/marketplace/uninstall-disable-extensions?toc=/azure/devops/server/toc.json&amp;bc=/azure/devops/server/breadcrumb/toc.json)">Uninstall or disable extensions</a></li>
</ul>
<h3>Pipelines, Build and release, Agent pools, Deployment pools</h3>
<ul>
<li><a href="/azure/devops/pipelines/policies/retention?toc=/azure/devops/server/toc.json&amp;bc=/azure/devops/server/breadcrumb/toc.json" data-raw-source="[Set retention policies](/azure/devops/pipelines/policies/retention?toc=/azure/devops/server/toc.json&amp;bc=/azure/devops/server/breadcrumb/toc.json)">Set retention policies</a></li>
<li><a href="/azure/devops/pipelines/licensing/concurrent-pipelines-ts?toc=/azure/devops/server/toc.json&amp;bc=/azure/devops/server/breadcrumb/toc.json" data-raw-source="[Set resource limits for pipelines](/azure/devops/pipelines/licensing/concurrent-pipelines-ts?toc=/azure/devops/server/toc.json&amp;bc=/azure/devops/server/breadcrumb/toc.json)">Set resource limits for pipelines</a></li>
<li><a href="/azure/devops/pipelines/agents/pools-queues?toc=/azure/devops/server/toc.json&amp;bc=/azure/devops/server/breadcrumb/toc.json" data-raw-source="[Add and manage agent pools](/azure/devops/pipelines/agents/pools-queues?toc=/azure/devops/server/toc.json&amp;bc=/azure/devops/server/breadcrumb/toc.json)">Add and manage agent pools</a></li>
<li><a href="/azure/devops/pipelines/release/deployment-groups/index?toc=/azure/devops/server/toc.json&amp;bc=/azure/devops/server/breadcrumb/toc.json" data-raw-source="[Add and manage deployment pools](/azure/devops/pipelines/release/deployment-groups/index?toc=/azure/devops/server/toc.json&amp;bc=/azure/devops/server/breadcrumb/toc.json)">Add and manage deployment pools</a></li>
</ul>

</td>
</tr>

</tbody>
</table>

## Project administrative tasks 

Members of the [Project Administrators group](/azure/devops/security/set-project-collection-level-permissions?toc=/azure/devops/server/toc.json&bc=/azure/devops/server/breadcrumb/toc.json) are tasked with configuring resources for a project and managing permissions at the project-level. Members of the Project Collection Administrators group can configure project and team settings as well. See also [Get started as an administrator](/azure/devops/user-guide/project-admin-tutorial?toc=/azure/devops/server/toc.json&bc=/azure/devops/server/breadcrumb/toc.json).

<table valign="top">
<tbody valign="top">
<tr>
<td width="50%"> 

<h3>Manage users and permissions</h3>
<ul>
<li><a href="/azure/devops/organizations/security/add-users-team-project?toc=/azure/devops/server/toc.json&amp;bc=/azure/devops/server/breadcrumb/toc.json" data-raw-source="[Add users to a project](/azure/devops/organizations/security/add-users-team-project?toc=/azure/devops/server/toc.json&amp;bc=/azure/devops/server/breadcrumb/toc.json)">Add users to a project</a></li>
<li><a href="/azure/devops/organizations/security/set-project-collection-level-permissions?toc=/azure/devops/server/toc.json&amp;bc=/azure/devops/server/breadcrumb/toc.json" data-raw-source="[Add project administrators](/azure/devops/organizations/security/set-project-collection-level-permissions?toc=/azure/devops/server/toc.json&amp;bc=/azure/devops/server/breadcrumb/toc.json)">Add project administrators</a></li>
<li><a href="/azure/devops/organizations/security/change-individual-permissions?toc=/azure/devops/server/toc.json&amp;bc=/azure/devops/server/breadcrumb/toc.json" data-raw-source="[Change individual permissions, grant select access to specific functions](/azure/devops/organizations/security/change-individual-permissions?toc=/azure/devops/server/toc.json&amp;bc=/azure/devops/server/breadcrumb/toc.json)">Change individual permissions, grant select access to specific functions</a></li>
<li><a href="/azure/devops/organizations/security/restrict-access?toc=/azure/devops/server/toc.json&amp;bc=/azure/devops/server/breadcrumb/toc.json" data-raw-source="[Grant or restrict access to select features](/azure/devops/organizations/security/restrict-access?toc=/azure/devops/server/toc.json&amp;bc=/azure/devops/server/breadcrumb/toc.json)">Grant or restrict access to select features</a></li>
<li><a href="/azure/devops/pipelines/policies/set-permissions?toc=/azure/devops/server/toc.json&amp;bc=/azure/devops/server/breadcrumb/toc.json" data-raw-source="[Set build and release permissions](/azure/devops/pipelines/policies/set-permissions?toc=/azure/devops/server/toc.json&amp;bc=/azure/devops/server/breadcrumb/toc.json)">Set build and release permissions</a></li>
</ul>

<h3>Manage projects</h3>
<ul>
<li><a href="/azure/devops/organizations/settings/set-services?toc=/azure/devops/server/toc.json&amp;bc=/azure/devops/server/breadcrumb/toc.json" data-raw-source="[Change service visibility](/azure/devops/organizations/settings/set-services?toc=/azure/devops/server/toc.json&amp;bc=/azure/devops/server/breadcrumb/toc.json)">Change service visibility</a> </li>
<li><a href="/azure/devops/organizations/projects/connect-to-projects?toc=/azure/devops/server/toc.json&amp;bc=/azure/devops/server/breadcrumb/toc.json" data-raw-source="[Connect to projects](/azure/devops/organizations/projects/connect-to-projects?toc=/azure/devops/server/toc.json&amp;bc=/azure/devops/server/breadcrumb/toc.json)">Connect to projects</a></li>
<li><a href="/azure/devops/report/sharepoint-dashboards/share-information-using-the-project-portal?toc=/azure/devops/server/toc.json&amp;bc=/azure/devops/server/breadcrumb/toc.json" data-raw-source="[Configure a project portal](/azure/devops/report/sharepoint-dashboards/share-information-using-the-project-portal?toc=/azure/devops/server/toc.json&amp;bc=/azure/devops/server/breadcrumb/toc.json)">Configure a project portal</a></li>
<li><a href="/azure/devops/service-hooks/index?toc=/azure/devops/server/toc.json&amp;bc=/azure/devops/server/breadcrumb/toc.json" data-raw-source="[Configure service hooks](/azure/devops/service-hooks/index?toc=/azure/devops/server/toc.json&amp;bc=/azure/devops/server/breadcrumb/toc.json)">Configure service hooks</a></li>
<li><a href="/azure/devops/organizations/projects/delete-project?toc=/azure/devops/server/toc.json&amp;bc=/azure/devops/server/breadcrumb/toc.json" data-raw-source="[Delete a project](/azure/devops/organizations/projects/delete-project?toc=/azure/devops/server/toc.json&amp;bc=/azure/devops/server/breadcrumb/toc.json)">Delete a project</a></li>
<li><a href="/azure/devops/organizations/projects/rename-project?toc=/azure/devops/server/toc.json&amp;bc=/azure/devops/server/breadcrumb/toc.json" data-raw-source="[Rename a project](/azure/devops/organizations/projects/rename-project?toc=/azure/devops/server/toc.json&amp;bc=/azure/devops/server/breadcrumb/toc.json)">Rename a project</a></li>
<li><a href="/azure/devops/organizations/projects/restore-project?toc=/azure/devops/server/toc.json&amp;bc=/azure/devops/server/breadcrumb/toc.json" data-raw-source="[Restore a project](/azure/devops/organizations/projects/restore-project?toc=/azure/devops/server/toc.json&amp;bc=/azure/devops/server/breadcrumb/toc.json)">Restore a project</a></li>
<li><a href="/azure/devops/organizations/projects/save-project-data?toc=/azure/devops/server/toc.json&amp;bc=/azure/devops/server/breadcrumb/toc.json" data-raw-source="[Save project data](/azure/devops/organizations/projects/save-project-data?toc=/azure/devops/server/toc.json&amp;bc=/azure/devops/server/breadcrumb/toc.json)">Save project data</a></li>
</ul>


<h3>Manage teams and project configuration</h3>
<ul>
<li><a href="/azure/devops/organizations/settings/add-teams?toc=/azure/devops/server/toc.json&amp;bc=/azure/devops/server/breadcrumb/toc.json" data-raw-source="[Add a team](/azure/devops/organizations/settings/add-teams?toc=/azure/devops/server/toc.json&amp;bc=/azure/devops/server/breadcrumb/toc.json)">Add a team</a></li>
<li><a href="/azure/devops/organizations/settings/add-team-administrator?toc=/azure/devops/server/toc.json&amp;bc=/azure/devops/server/breadcrumb/toc.json" data-raw-source="[Add a team administrator](/azure/devops/organizations/settings/add-team-administrator?toc=/azure/devops/server/toc.json&amp;bc=/azure/devops/server/breadcrumb/toc.json)">Add a team administrator</a></li>
<li><a href="/azure/devops/organizations/settings/set-area-paths?toc=/azure/devops/server/toc.json&amp;bc=/azure/devops/server/breadcrumb/toc.json" data-raw-source="[Define area paths](/azure/devops/organizations/settings/set-area-paths?toc=/azure/devops/server/toc.json&amp;bc=/azure/devops/server/breadcrumb/toc.json)">Define area paths</a></li>
<li><a href="/azure/devops/organizations/settings/set-iteration-paths-sprints?toc=/azure/devops/server/toc.json&amp;bc=/azure/devops/server/breadcrumb/toc.json" data-raw-source="[Define iteration paths or sprints](/azure/devops/organizations/settings/set-iteration-paths-sprints?toc=/azure/devops/server/toc.json&amp;bc=/azure/devops/server/breadcrumb/toc.json)">Define iteration paths or sprints</a></li>
<li><a href="/azure/devops/report/dashboards/dashboard-permissions?toc=/azure/devops/server/toc.json&amp;bc=/azure/devops/server/breadcrumb/toc.json" data-raw-source="[Set default dashboard permissions](/azure/devops/report/dashboards/dashboard-permissions?toc=/azure/devops/server/toc.json&amp;bc=/azure/devops/server/breadcrumb/toc.json)">Set default dashboard permissions</a></li>
<li><a href="/azure/devops/notifications/howto-manage-team-notifications?toc=/azure/devops/server/toc.json&amp;bc=/azure/devops/server/breadcrumb/toc.json" data-raw-source="[Manage project-level notifications](/azure/devops/notifications/howto-manage-team-notifications?toc=/azure/devops/server/toc.json&amp;bc=/azure/devops/server/breadcrumb/toc.json)">Manage project-level notifications</a></li>
</ul>

</td>
<td width="50%"> 

<h3>Wiki</h3>
<ul>
<li><a href="/azure/devops/project/wiki/wiki-create-repo?toc=/azure/devops/server/toc.json&amp;bc=/azure/devops/server/breadcrumb/toc.json" data-raw-source="[Create a wiki for your project](/azure/devops/project/wiki/wiki-create-repo?toc=/azure/devops/server/toc.json&amp;bc=/azure/devops/server/breadcrumb/toc.json)">Create a wiki for your project</a></li>
<li><a href="/azure/devops/project/wiki/publish-repo-to-wiki?toc=/azure/devops/server/toc.json&amp;bc=/azure/devops/server/breadcrumb/toc.json" data-raw-source="[Publish a Git repository to a wiki](/azure/devops/project/wiki/publish-repo-to-wiki?toc=/azure/devops/server/toc.json&amp;bc=/azure/devops/server/breadcrumb/toc.json)">Publish a Git repository to a wiki</a> </li>
<li><a href="/azure/devops/project/wiki/manage-readme-wiki-permissions?toc=/azure/devops/server/toc.json&amp;bc=/azure/devops/server/breadcrumb/toc.json" data-raw-source="[Manage README and Wiki permissions](/azure/devops/project/wiki/manage-readme-wiki-permissions?toc=/azure/devops/server/toc.json&amp;bc=/azure/devops/server/breadcrumb/toc.json)">Manage README and Wiki permissions</a></li>
</ul>

<h3>Pipelines, Build and release, Agent Pools</h3>
<ul>
<li><a href="/azure/devops/pipelines/agents/pools-queues?toc=/azure/devops/server/toc.json&amp;bc=/azure/devops/server/breadcrumb/toc.json" data-raw-source="[Manage Agent queues and agent pools](/azure/devops/pipelines/agents/pools-queues?toc=/azure/devops/server/toc.json&amp;bc=/azure/devops/server/breadcrumb/toc.json)">Manage Agent queues and agent pools</a></li>
<li><a href="/azure/devops/pipelines/library/service-endpoints?toc=/azure/devops/server/toc.json&amp;bc=/azure/devops/server/breadcrumb/toc.json" data-raw-source="[Manage service connections](/azure/devops/pipelines/library/service-endpoints?toc=/azure/devops/server/toc.json&amp;bc=/azure/devops/server/breadcrumb/toc.json)">Manage service connections</a></li>
<li><a href="/azure/devops/pipelines/release/deployment-groups/index?toc=/azure/devops/server/toc.json&amp;bc=/azure/devops/server/breadcrumb/toc.json" data-raw-source="[Manage deployment pools and groups](/azure/devops/pipelines/release/deployment-groups/index?toc=/azure/devops/server/toc.json&amp;bc=/azure/devops/server/breadcrumb/toc.json)">Manage deployment pools and groups</a></li>
<li><a href="/azure/devops/pipelines/policies/retention?toc=/azure/devops/server/toc.json&amp;bc=/azure/devops/server/breadcrumb/toc.json" data-raw-source="[Set retention policies](/azure/devops/pipelines/policies/retention?toc=/azure/devops/server/toc.json&amp;bc=/azure/devops/server/breadcrumb/toc.json)">Set retention policies</a></li>
</ul>


<h3>Repos, Code, version control</h3>
<ul>
<li><a href="/azure/devops/repos/git/creatingrepo?toc=/azure/devops/server/toc.json&amp;bc=/azure/devops/server/breadcrumb/toc.json" data-raw-source="[Create additional Git repos](/azure/devops/repos/git/creatingrepo?toc=/azure/devops/server/toc.json&amp;bc=/azure/devops/server/breadcrumb/toc.json)">Create additional Git repos</a></li>
<li><a href="/azure/devops/organizations/security/set-git-tfvc-repository-permissions?toc=/azure/devops/server/toc.json&amp;bc=/azure/devops/server/breadcrumb/toc.json" data-raw-source="[Manage repository permissions](/azure/devops/organizations/security/set-git-tfvc-repository-permissions?toc=/azure/devops/server/toc.json&amp;bc=/azure/devops/server/breadcrumb/toc.json)">Manage repository permissions</a></li>
<li><a href="/azure/devops/repos/git/branch-policies?toc=/azure/devops/server/toc.json&amp;bc=/azure/devops/server/breadcrumb/toc.json" data-raw-source="[Manage branch policies](/azure/devops/repos/git/branch-policies?toc=/azure/devops/server/toc.json&amp;bc=/azure/devops/server/breadcrumb/toc.json)">Manage branch policies</a></li>
<li><a href="/azure/devops/repos/tfvc/add-check-policies?toc=/azure/devops/server/toc.json&amp;bc=/azure/devops/server/breadcrumb/toc.json" data-raw-source="[Add TFVC Check-In Policies](/azure/devops/repos/tfvc/add-check-policies?toc=/azure/devops/server/toc.json&amp;bc=/azure/devops/server/breadcrumb/toc.json)">Add TFVC Check-In Policies</a></li>
<li><a href="manage-file-types.md" data-raw-source="[Manage TFVC file types](manage-file-types.md)">Manage TFVC file types</a></li>
</ul>


<h3>Test plans, Test </h3>
<ul>
<li><a href="/azure/devops/test/how-long-to-keep-test-results?toc=/azure/devops/server/toc.json&amp;bc=/azure/devops/server/breadcrumb/toc.json" data-raw-source="[Set test retention policies](/azure/devops/test/how-long-to-keep-test-results?toc=/azure/devops/server/toc.json&amp;bc=/azure/devops/server/breadcrumb/toc.json)">Set test retention policies</a></li>
<li><a href="/azure/devops/organizations/security/set-project-collection-level-permissions?toc=/azure/devops/server/toc.json&amp;bc=/azure/devops/server/breadcrumb/toc.json" data-raw-source="[Manage test-related permissions at project level](/azure/devops/organizations/security/set-project-collection-level-permissions?toc=/azure/devops/server/toc.json&amp;bc=/azure/devops/server/breadcrumb/toc.json)">Manage test-related permissions at project level</a></li>
<li><a href="/azure/devops/organizations/security/set-permissions-access-work-tracking#create-child-nodes-modify-work-items-under-an-area-path?toc=/azure/devops/server/toc.json&amp;bc=/azure/devops/server/breadcrumb/toc.json" data-raw-source="[Set area path-level test permissions](/azure/devops/organizations/security/set-permissions-access-work-tracking#create-child-nodes-modify-work-items-under-an-area-path?toc=/azure/devops/server/toc.json&amp;bc=/azure/devops/server/breadcrumb/toc.json)">Set area path-level test permissions</a></li>
</ul>
</td>
</tr>
</tbody>
</table>




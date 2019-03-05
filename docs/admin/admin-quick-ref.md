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
ms.date: 03/05/2019
--- 

# Administrative tasks quick reference 

[!INCLUDE [temp](../_shared/version-tfs-all-versions.md)]

Use this index to quickly access information about tasks for managing Azure DevOps on-premises servers. 


## Install, upgrade, and general admin tasks 

<ul>
<li>[Install get started](../install/get-started.md)</li>
<li>[Install SQL Server](../install/sql-server/install-sql-server.md)
<li>[Upgrade get started](../upgrade/get-started.md)</li>
<li>[Upgrade TFS Express](../upgrade/express.md)</li>
<li>[Open the Administration Console](open-admin-console.md)</li>
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
<li>[Add administration console users](add-administrator.md)</li> 
<li>[Add server-level administrators](add-administrator.md)</li>
<li>[Change access levels](/azure/devops/organizations/security/change-access-levels?toc=/azure/devops/server/toc.json&bc=/azure/devops/server/breadcrumb/toc.json)</li>
<li>[Set up groups for use in Azure DevOps deployments](setup-ad-groups.md)</li>
</ul>

<h3>Server configuration </h3>
<ul>
<li>[Change cache settings for an application-tier server](change-caching-app-tier.md)</li>
<li>[Configure an SMTP server](setup-customize-alerts.md)</li>
<li>[Customize email for alerts and feedback requests](setup-customize-alerts.md)</li>
</ul>

<h3>Server maintenance </h3>
<ul>
<li>[Change the service account or password for TFS](change-service-account-password.md)</li>
<li>[Change cache settings for an application-tier server](change-caching-app-tier.md)</li>
<li>[Stop and start services, application pools, and websites](stop-start-services-pools.md)</li>
</ul>


</td>
<td width="50%"> 
<h3>Manage databases</h3>
<ul>
<li>[Back up and restore](backup/back-up-restore.md)</li>
<li>[Configure a backup schedule and plan](backup/config-backup-sched-plan.md)</li>
<li>[Understand backing up Azure DevOps on-premises](backup/backup-db-architecture.md)</li>
</ul>
<h3>SQL Server reporting</h3>
<ul>
<li>[Add reports to a project](/azure/devops/report/admin/add-reports-to-a-team-project?toc=/azure/devops/server/toc.json&bc=/azure/devops/server/breadcrumb/toc.json)</li>
<li>[Manage the data warehouse and analysis services cube](/azure/devops/report/admin/manage-reports-data-warehouse-cube?toc=/azure/devops/server/toc.json&bc=/azure/devops/server/breadcrumb/toc.json)</li>
<li>[Change the service account or password for SQL Server Reporting Services](change-service-account-or-password-sql-reporting.md)</li> 
</ul>
<h3>SharePoint product integration (valid for TFS 2017 and earlier versions)</h3>
<ul>
<li>[Add SharePoint products to your deployment](add-sharepoint-to-tfs.md)</li>
<li>[Configure or add a project portal](/azure/devops/report/sharepoint-dashboards/configure-or-add-a-project-portal?toc=/azure/devops/server/toc.json&bc=/azure/devops/server/breadcrumb/toc.json)</li>
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

<li>[Add a project](/azure/devops/organizations/projects/create-project)</li>
<li>[Add a project collection](manage-project-collections.md)</li>
<li>[Delete/detach a project collection](manage-project-collections.md)</li>
<li>[Add collection-level administrators](/azure/devops/organizations/security/set-project-collection-level-permissions?toc=/azure/devops/server/toc.json&bc=/azure/devops/server/breadcrumb/toc.json)</li>
<li>[Manage collection-level notifications](/azure/devops/notifications/howto-manage-organization-notifications?toc=/azure/devops/server/toc.json&bc=/azure/devops/server/breadcrumb/toc.json) </li>
<li>[Move a project collection](move-project-collection.md) </li>
<li>[Open the Administration Console](open-admin-console.md)</li>
<li>[Split a project collection](split-team-project-collection.md) </li>
</ul>

<h3>Boards/Process and work tracking customizations</h3>
<ul>
<li>[Customize your work tracking experience](/azure/devops/reference/customize-work?toc=/azure/devops/server/toc.json&bc=/azure/devops/server/breadcrumb/toc.json)</li>
<li>[On-premises XML process model](/azure/devops/reference/on-premises-xml-process-model?toc=/azure/devops/server/toc.json&bc=/azure/devops/server/breadcrumb/toc.json)</li>
<li>[About process customization and inherited processes](/azure/devops/organizations/settings/work/inheritance-process-model?toc=/azure/devops/server/toc.json&bc=/azure/devops/server/breadcrumb/toc.json)
<ul>
<li>[Customize a project](/azure/devops/organizations/settings/work/customize-process?toc=/azure/devops/server/toc.json&bc=/azure/devops/server/breadcrumb/toc.json)</li>
<li>[Add and manage processes](/azure/devops/organizations/settings/work/manage-process?toc=/azure/devops/server/toc.json&bc=/azure/devops/server/breadcrumb/toc.json)</li>
</ul>
</li>
</ul>

</td>

<td width="50%">
<h3>Extensions</h3>
<ul>
<li>[Install and manage Marketplace extensions](/azure/devops/marketplace/install-extension?toc=/azure/devops/server/toc.json&bc=/azure/devops/server/breadcrumb/toc.json)</li>
<li>[Approve extensions](/azure/devops/marketplace/approve-extensions?toc=/azure/devops/server/toc.json&bc=/azure/devops/server/breadcrumb/toc.json)</li>
<li>[Assign paid extension access to users](/azure/devops/marketplace/assign-paid-extensions?toc=/azure/devops/server/toc.json&bc=/azure/devops/server/breadcrumb/toc.json)</li>
<li>[Grant permissions to manage extensions](/azure/devops/marketplace/how-to/grant-permissions?toc=/azure/devops/server/toc.json&bc=/azure/devops/server/breadcrumb/toc.json)</li>
<li>[Uninstall or disable extensions](/azure/devops/marketplace/uninstall-disable-extensions?toc=/azure/devops/server/toc.json&bc=/azure/devops/server/breadcrumb/toc.json)</li>
</ul>
<h3>Pipelines, Build and release, Agent pools, Deployment pools</h3>
<ul>
<li>[Set retention policies](/azure/devops/pipelines/policies/retention?toc=/azure/devops/server/toc.json&bc=/azure/devops/server/breadcrumb/toc.json)</li>
<li>[Set resource limits for pipelines](/azure/devops/pipelines/licensing/concurrent-pipelines-ts?toc=/azure/devops/server/toc.json&bc=/azure/devops/server/breadcrumb/toc.json)</li>
<li>[Add and manage agent pools](/azure/devops/pipelines/agents/pools-queues?toc=/azure/devops/server/toc.json&bc=/azure/devops/server/breadcrumb/toc.json)</li>
<li>[Add and manage deployment pools](/azure/devops/pipelines/release/deployment-groups/index?toc=/azure/devops/server/toc.json&bc=/azure/devops/server/breadcrumb/toc.json)</li>
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
<li>[Add users to a project](/azure/devops/organizations/security/add-users-team-project?toc=/azure/devops/server/toc.json&bc=/azure/devops/server/breadcrumb/toc.json)</li>
<li>[Add project administrators](/azure/devops/organizations/security/set-project-collection-level-permissions?toc=/azure/devops/server/toc.json&bc=/azure/devops/server/breadcrumb/toc.json)</li>
<li>[Change individual permissions, grant select access to specific functions](/azure/devops/organizations/security/change-individual-permissions?toc=/azure/devops/server/toc.json&bc=/azure/devops/server/breadcrumb/toc.json)</li>
<li>[Grant or restrict access to select features](/azure/devops/organizations/security/restrict-access?toc=/azure/devops/server/toc.json&bc=/azure/devops/server/breadcrumb/toc.json)</li>
<li>[Set build and release permissions](/azure/devops/pipelines/policies/set-permissions?toc=/azure/devops/server/toc.json&bc=/azure/devops/server/breadcrumb/toc.json)</li>
</ul>

<h3>Manage projects</h3>
<ul>
<li>[Change service visibility](/azure/devops/organizations/settings/set-services?toc=/azure/devops/server/toc.json&bc=/azure/devops/server/breadcrumb/toc.json) </li>
<li>[Connect to projects](/azure/devops/organizations/projects/connect-to-projects?toc=/azure/devops/server/toc.json&bc=/azure/devops/server/breadcrumb/toc.json)</li>
<li>[Configure a project portal](/azure/devops/report/sharepoint-dashboards/share-information-using-the-project-portal?toc=/azure/devops/server/toc.json&bc=/azure/devops/server/breadcrumb/toc.json)</li>
<li>[Configure service hooks](/azure/devops/service-hooks/index?toc=/azure/devops/server/toc.json&bc=/azure/devops/server/breadcrumb/toc.json)</li>
<li>[Delete a project](/azure/devops/organizations/projects/delete-project?toc=/azure/devops/server/toc.json&bc=/azure/devops/server/breadcrumb/toc.json)</li>
<li>[Rename a project](/azure/devops/organizations/projects/rename-project?toc=/azure/devops/server/toc.json&bc=/azure/devops/server/breadcrumb/toc.json)</li>
<li>[Restore a project](/azure/devops/organizations/projects/restore-project?toc=/azure/devops/server/toc.json&bc=/azure/devops/server/breadcrumb/toc.json)</li>
<li>[Save project data](/azure/devops/organizations/projects/save-project-data?toc=/azure/devops/server/toc.json&bc=/azure/devops/server/breadcrumb/toc.json)</li>
</ul>


<h3>Manage teams and project configuration</h3>
<ul>
<li>[Add a team](/azure/devops/organizations/settings/add-teams?toc=/azure/devops/server/toc.json&bc=/azure/devops/server/breadcrumb/toc.json)</li>
<li>[Add a team administrator](/azure/devops/organizations/settings/add-team-administrator?toc=/azure/devops/server/toc.json&bc=/azure/devops/server/breadcrumb/toc.json)</li>
<li>[Define area paths](/azure/devops/organizations/settings/set-area-paths?toc=/azure/devops/server/toc.json&bc=/azure/devops/server/breadcrumb/toc.json)</li>
<li>[Define iteration paths or sprints](/azure/devops/organizations/settings/set-iteration-paths-sprints?toc=/azure/devops/server/toc.json&bc=/azure/devops/server/breadcrumb/toc.json)</li>
<li>[Set default dashboard permissions](/azure/devops/report/dashboards/dashboard-permissions?toc=/azure/devops/server/toc.json&bc=/azure/devops/server/breadcrumb/toc.json)</li>
<li>[Manage project-level notifications](/azure/devops/notifications/howto-manage-team-notifications?toc=/azure/devops/server/toc.json&bc=/azure/devops/server/breadcrumb/toc.json)</li>
</ul>

</td>
<td width="50%"> 

<h3>Wiki</h3>
<ul>
<li>[Create a wiki for your project](/azure/devops/project/wiki/wiki-create-repo?toc=/azure/devops/server/toc.json&bc=/azure/devops/server/breadcrumb/toc.json)</li>
<li>[Publish a Git repository to a wiki](/azure/devops/project/wiki/publish-repo-to-wiki?toc=/azure/devops/server/toc.json&bc=/azure/devops/server/breadcrumb/toc.json) </li>
<li>[Manage README and Wiki permissions](/azure/devops/project/wiki/manage-readme-wiki-permissions?toc=/azure/devops/server/toc.json&bc=/azure/devops/server/breadcrumb/toc.json)</li>
</ul>

<h3>Pipelines, Build and release, Agent Pools</h3>
<ul>
<li>[Manage Agent queues and agent pools](/azure/devops/pipelines/agents/pools-queues?toc=/azure/devops/server/toc.json&bc=/azure/devops/server/breadcrumb/toc.json)</li>
<li>[Manage service connections](/azure/devops/pipelines/library/service-endpoints?toc=/azure/devops/server/toc.json&bc=/azure/devops/server/breadcrumb/toc.json)</li>
<li>[Manage deployment pools and groups](/azure/devops/pipelines/release/deployment-groups/index?toc=/azure/devops/server/toc.json&bc=/azure/devops/server/breadcrumb/toc.json)</li>
<li>[Set retention policies](/azure/devops/pipelines/policies/retention?toc=/azure/devops/server/toc.json&bc=/azure/devops/server/breadcrumb/toc.json)</li>
</ul>


<h3>Repos, Code, version control</h3>
<ul>
<li>[Create additional Git repos](/azure/devops/repos/git/creatingrepo?toc=/azure/devops/server/toc.json&bc=/azure/devops/server/breadcrumb/toc.json)</li>
<li>[Manage repository permissions](/azure/devops/organizations/security/set-git-tfvc-repository-permissions?toc=/azure/devops/server/toc.json&bc=/azure/devops/server/breadcrumb/toc.json)</li>
<li>[Manage branch policies](/azure/devops/repos/git/branch-policies?toc=/azure/devops/server/toc.json&bc=/azure/devops/server/breadcrumb/toc.json)</li>
<li>[Add TFVC Check-In Policies](/azure/devops/repos/tfvc/add-check-policies?toc=/azure/devops/server/toc.json&bc=/azure/devops/server/breadcrumb/toc.json)</li>
<li>[Manage TFVC file types](manage-file-types.md)</li>
</ul>


<h3>Test plans, Test </h3>
<ul>
<li>[Set test retention policies](/azure/devops/test/how-long-to-keep-test-results?toc=/azure/devops/server/toc.json&bc=/azure/devops/server/breadcrumb/toc.json)</li>
<li>[Manage test-related permissions at project level](/azure/devops/organizations/security/set-project-collection-level-permissions?toc=/azure/devops/server/toc.json&bc=/azure/devops/server/breadcrumb/toc.json)</li>
<li>[Set area path-level test permissions](/azure/devops/organizations/security/set-permissions-access-work-tracking#create-child-nodes-modify-work-items-under-an-area-path?toc=/azure/devops/server/toc.json&bc=/azure/devops/server/breadcrumb/toc.json)</li>
</ul>
</td>
</tr>
</tbody>
</table>




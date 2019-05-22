---
title: SQL Server Reporting Services Roles
titleSuffix: Azure DevOps Server  
description: SQL Server Reporting Services Roles
ms.manager: jillfra
ms.author: aaronha
author: aaronhallberg
ms.topic: conceptual
ms.date: 05/21/2019
ms.prod: devops-server
ms.technology: tfs-admin
---

# SQL Server Reporting Services roles

[!INCLUDE [temp](../../_shared/version-tfs-all-versions.md)]

You can use the roles in SQL Server Reporting Services to assign particular permissions to users in Azure DevOps Server. Every user and group in Azure DevOps Server must be assigned appropriate permissions in Reporting Services. Reporting Services provides default security through role assignments. You can use management tools for SQL Server, such as Management Studio and Report Manager, to assign users and groups to predefined roles.

You can use group membership in Azure DevOps Server to determine the appropriate membership in one of the predefined roles in Reporting Services. No additional configuration of the role is required. However, you can modify predefined roles and add custom roles to better meet your business needs. If you add custom roles or modify predefined roles, be sure that the roles have the permissions required for the appropriate level of access to reports and reporting features. For more information, see [Granting permissions on a Native Mode Report Server](/sql/reporting-services/security/granting-permissions-on-a-native-mode-report-server).

The following predefined roles are suggested for use with Azure DevOps Server:
-   System Administrator
-   Team Foundation Content Manager
-   Browser

For more information about predefined roles in Reporting Services, see [Using predefined roles](/sql/reporting-services/security/role-definitions-predefined-roles).

> [!IMPORTANT]
> You should restrict membership in Reporting Services to only those users who need the specific level of access and permissions granted by membership in that predefined role. Add a user or group to the predefined role that has the minimum permissions required to complete the user's or group's role within a project. For example, if a user only needs to view the project schedule, you should add the user to the Browser role but not to the Content Manager role.

## System Administrator

The System Administrator role includes permissions that are useful for a report server administrator who has overall responsibility for a report server, but not necessarily for the content within it. The System Administrator role does not convey the full range of permissions that a local administrator might have on a computer. You must add Azure DevOps Administrators to both the System Administrator role and the Content Manager role. Together, the two role definitions provide a complete set of permissions required by members of the Azure DevOps Administrators group.

## Team Foundation Content Manager

Make sure to [add your administrators to the Team Foundation Content Managers group](/azure/devops/report/admin/grant-permissions-to-reports) on the server that hosts SQL Server Reporting Services. Otherwise they might have problems, such as being blocked by a TF218027 error when trying to create a project.

Unlike the other roles described in this article, the Team Foundation Content Manager role is not a default role in SQL Server. The role is created specifically for integration between Azure DevOps Server and SQL Server Reporting Services when Azure DevOps Server is installed. Its structure and permissions are similar to the Content Manager role that is native to SQL Server. The Team Foundation Content Manager role includes permissions that are useful for users who manage reports and web content but that do not necessarily write reports or manage a web server or an instance of SQL Server. A content manager deploys reports, manages report models and data source connections, and decides how to use reports. The Team Foundation Content Manager role provides the typical range of permissions required by users who belong to the Project Administrators group in a project, in addition to users who belong to the Project Collection Administrators group. You should also add members of the Azure DevOps Administrators group to this role.

## Browser

The Browser role includes permissions that are useful for users who view reports, but do not necessarily write or manage them. This role provides basic capabilities for users who belong to either the Contributor or Reader group in a project.

## Related article

- [Understanding SQL Server and SQL Server Reporting Services](../../architecture/sql-server-databases.md) 

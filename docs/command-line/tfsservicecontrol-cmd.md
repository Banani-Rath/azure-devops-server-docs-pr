---
title: Stop or start Azure DevOps Server services or application pools with TFSServiceControl command
titleSuffix: Azure DevOps Server 
description: Start or stop Azure DevOps Server services from the command line using TFSServiceControl
ms.prod: devops-server
ms.technology: tfs-admin
ms.manager: jillfra
ms.author: aaronha
author: aaronhallberg
ms.topic: conceptual
monikerRange: '< azure-devops'
ms.date: 05/30/2019
---

# Use TFSServiceControl to start and stop services for Azure DevOps on-premises  

[!INCLUDE [temp](../_shared/version-tfs-all-versions.md)]

You can use the **TFSServiceControl** command to stop or start all of the services and application pools used by Azure DevOps Server. For example, you use this command when backing up or restoring databases, or when you are moving your deployment from one machine to another.

> [!NOTE]
> You must use the **TFSServiceControl** command to ensure that all necessary operations, services, and application pools are stopped for maintenance tasks such as backup and restore. You cannot manually perform all of the tasks carried out by the **TFSServiceControl** command.

## Prerequisites

-   You must be a member of the Team Foundation Administrators security group, a member of the Administrators group on the application-tier server, and a member of the sysadmin security group for any SQL Server databases that Azure DevOps Server uses. See [Set administrator permissions for Azure DevOps Server](../admin/add-administrator.md).

-   Even if you log on with administrative credentials, you must open an elevated Command Prompt window to perform this function.  

	TFSServiceControl [quiesce|unquiesce]

## Parameters

|Option|Description|
|---|---|
|**quiesce**|Stops or pauses all of the services, application pools, and operations in your deployment of Azure DevOps Server. This is required for certain maintenance tasks, such as restoring databases.|
|**unquiesce**|Starts or restarts all of the services, application pools, and operations in your deployment of Azure DevOps Server. This is required to return your server to operation after you run the command with the **quiesce** option.|

## Remarks

You use the **TFSServiceControl** command as part of specific maintenance tasks. After you specify the **quiesce** option, the server will not operate until you specify the **unquiesce** option. By default, the **TFSServiceControl** command is located in the %programfiles%\\TFS 12.0\\Tools directory.

## Example

The following example shows how to stop a deployment of Azure DevOps Server.

    TFSServiceControl quiesce

The following example shows how to start a deployment of Azure DevOps Server.

    TFSServiceControl unquiesce

## Related articles

- [Restore data to the same location](../admin/backup/restore-data-same-location.md)
- [Back up and restore Azure DevOps Server](../admin/backup/back-up-restore.md)
- [Administrative task quick reference](../admin/admin-quick-ref.md)
- [Restore a deployment to new hardware](../admin/backup/tut-single-svr-home.md)

---
title: Refresh the data caches on client computers
description: Refresh the data caches on client computers
ms.topic: conceptual
ms.manager: jillfra
ms.author: aaronha
author: aaronhallberg
ms.prod: devops-server
ms.technology: tfs-admin
monikerRange: '>= tfs-2013'
ms.date: 05/20/2019
---

# Refresh the data caches on client computers

[!INCLUDE [temp](../../_shared/version-tfs-all-versions.md)]

To prevent workspace errors from occurring during version control or build operations in Azure DevOps, the data cache on client computers must be updated after certain maintenance operations:

- After you move, restore, rename, or fail over a data-tier or application-tier server
- After you recover from a failure such as a hardware malfunction

In either case, you must refresh the cache for tracking work items, and users must refresh the version control cache on client computers.

## Prerequisites

To invoke the **StampWorkitemCache** web method, you must be a member of the **Administrators** security group on the application-tier server for Azure DevOps. For more information, see [Permission reference for Azure DevOps Server](/azure/devops/security/permissions).

To use the **tf workspaces** command on the client computer, your **Read** permission must be set to **Allow**.

## Refresh the work item cache

This procedure is optional. You should perform it only if errors occur with work item tracking.

To update the cache for tracking work items, invoke the **StampWorkitemCache** web method. This method forces client computers to update the cache the next time they connect to the application-tier server. This method also synchronizes the workspaces that are defined on the client computers.

> [!NOTE]  
> When you invoke the **StampWorkitemCache** web method, the performance of Visual Studio Azure DevOps Server may temporarily degrade. The performance impact depends on how many Azure DevOps users are connected when you invoke the method.

To refresh the cache for tracking work items on client computers:

1. On the new server, open Internet Explorer.

2. In the Address bar, enter the following address to connect to the **ClientService** web service:

   **http://**<em>PublicURL/VirtualDirectory</em>**:8080/WorkItemTracking/v3.0/ClientService.asmx**

   > [!NOTE]  
   > Even if you are logged on with administrative credentials, you may need to start Internet Explorer as an administrator, and you may be prompted for your credentials.

3. Select **StampWorkitemCache**, and then choose **Invoke**. The **StampWorkitemCache** method returns no data.

## Refresh the version control cache

To refresh the version control cache, each user runs the **tf workspaces** command on each computer that must be updated. They must update any computer that uses version control and that connects to a project collection whose databases were relocated.

To refresh the version control cache on client computers:

1. On the client computer, open a Command Prompt window with administrative permissions, and change directories to *Drive*:\\Program Files (x86)\\Microsoft Visual Studio 12.0\\Common7\\IDE.

2. At the command prompt, enter the following command, including the URL of the collection, which includes the server name and the port number of the new server:

   **tf workspaces /collection:http://**<em>ServerName:Port/VirtualDirectoryName/CollectionName</em>

   In the example deployment, a developer needs to refresh the version control cache for a project that is a member of the DefaultCollection collection, which is hosted in the FabrikamPrime deployment of Azure DevOps Server:

   **tf workspaces /collection:<http://FabrikamPrime:8080/tfs/DefaultCollection>**

   For more information, see [Workspaces command](/azure/devops/tfvc/workspaces-command).


## Related articles

- [Open the Azure DevOps Server Administration Console](../open-admin-console.md) 
- [Workspaces command](/azure/devops/tfvc/workspaces-command) 
- [Manage data](https://msdn.microsoft.com/library/ms253169) 

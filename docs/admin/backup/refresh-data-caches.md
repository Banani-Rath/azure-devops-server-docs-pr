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
ms.date: 03/05/2019
---

# Refresh the data caches on client computers

[!INCLUDE [temp](../../_shared/version-tfs-all-versions.md)]

To prevent workspace errors from occurring during version control or build operations in Team Foundation, the data cache on client computers must be updated after certain maintenance operations. After you move, restore, rename, or fail over a data-tier or application-tier server or after you recover from a failure such as a hardware malfunction, you must refresh the cache for tracking work items and users must refresh the version control cache on client computers.

## Prerequisites

To invoke the **StampWorkitemCache** Web method, you must be a member of the **Administrators** security group on the application-tier server for Team Foundation. For more information, see [Permission reference for Team Foundation Server](/azure/devops/security/permissions).

To use the **tf workspaces** command on the client computer, your **Read** permission must be set to **Allow**.

## Refresh the Work Item Cache

> [!NOTE]  
>This procedure is optional. You should perform it only if errors occur with work item tracking.


To update the cache for tracking work items, you invoke the **StampWorkitemCache** Web method. This method forces client computers to update the cache the next time that they connect to the application-tier server. This method also synchronizes the workspaces that are defined on the client computers.

> [!NOTE]  
>When you invoke the **StampWorkitemCache** Web method, the performance of Visual Studio Team Foundation Server might temporarily degrade. The performance impact depends on how many Team Foundation users are connected when you invoke the method.

To refresh the cache for tracking work items on client computers:

1.  On the new server, open Internet Explorer.

2.  In the Address bar, enter the following address to connect to the **ClientService** web service:

    **http://** *PublicURL/VirtualDirectory* **:8080/WorkItemTracking/v3.0/ClientService.asmx**

	> [!NOTE]  
	>Even if you are logged on with administrative credentials, you might need to start Internet Explorer as an administrator, and you might be prompted for your credentials.

3.  Choose **StampWorkitemCache**, and then choose **Invoke**.

	> [!NOTE]  
	>The StampWorkitemCache method returns no data.

## Refresh the Version Control Cache

To refresh the version control cache, each user runs the **tf workspaces** command on any computer that must be updated. They must update any computer that uses version control and that connects to a project collection whose databases were relocated.

To refresh the version control cache on client computers:

1.  On the client computer, open a Command Prompt window with administrative permissions, and change directories to *Drive*:\\Program Files (x86)\\Microsoft Visual Studio 12.0\\Common7\\IDE.

2.  At the command prompt, enter the following command, including the URL of the collection, which includes the server name and the port number of the new server:

    **tf workspaces /collection:http://** *ServerName:Port/VirtualDirectoryName/CollectionName*

    In the example deployment, a developer needs to refresh the version control cache for a project that is a member of the DefaultCollection collection, which is hosted in the FabrikamPrime deployment of Team Foundation Server. He types the following string:

    **tf workspaces /collection:http://FabrikamPrime:8080/tfs/DefaultCollection**

    For more information, see [Workspaces Command](/azure/devops/tfvc/workspaces-command).


## Related articles

 [Open the Azure DevOps Server Administration Console](../open-admin-console.md) 

 [Workspaces Command](/azure/devops/tfvc/workspaces-command) 

 [Managing Data](https://msdn.microsoft.com/library/ms253169) 

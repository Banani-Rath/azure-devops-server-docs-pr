---
title: Rebuild the client cache
titleSuffix: Azure DevOps Server & TFS 
description: Rebuild the client cache for Team Foundation Server
ms.topic: conceptual
ms.manager: jillfra
ms.author: aaronha
author: aaronhallberg
ms.date: 08/18/2016
ms.prod: devops-server
ms.technology: tfs-admin
---

# Rebuild the client cache for Azure DevOps on-premises

[!INCLUDE [temp](../_shared/version-tfs-all-versions.md)]

You can force a rebuild of the cache on each client computer the next time it connects to a project collection by using the **witadmin rebuildcache** command. 

To prevent workspace errors from occurring during version control or build operations in Team Foundation, the data cache on client computers must be updated after certain maintenance operations. After you move, restore, rename, or fail over a data-tier or application-tier server, you must refresh the cache for tracking work items and users must refresh the version control cache on client computers. 

> [!IMPORTANT]
> To avoid server performance issues, you should not run this command during normal operating hours.

To run the tool, open a Command Prompt window where where you�ve installed Visual Studio and enter:

  ```cd %programfiles(x86)%\Microsoft Visual Studio <version>\Common7\IDE```

On a 32-bit edition of Windows, replace ```%programfiles(x86)%``` with ```%programfiles%```. 

**Requirements:** To use the witadmin rebuildcache command, you must be a member of the Team Foundation Administrators security group or the Project Administrators security group for the project collection that you want to manage. Permission reference for Team Foundation Server. 

> [!NOTE]
> Even if you log on with administrative permissions, you must open an elevated Command Prompt window to perform this function on a server that is running Windows Server 2008. To open an elevated Command Prompt window, choose **Start**, open the shortcut menu for **Command Prompt**, and choose **Run as Administrator**. For more information, see the [Microsoft Web site](http://go.microsoft.com/fwlink/?LinkId=111235).


**Syntax:**

  ```witadmin rebuildcache /collection:CollectionURL [/noprompt]```

**Parameters:**

| Parameter | Description |
| --- | --- |
| **/collection:** *CollectionURL* | Specifies the URI of the project collection or Azure DevOps Services account. For example: </br> **On-premises TFS format:** ```http://ServerName:Port/VirtualDirectoryName/CollectionName``` </br> If no virtual directory is used, then the format for the URI is the following: ```http://ServerName:Port/CollectionName```. </br> **Azure DevOps Services format:** http://AccountName.visualstudio.com.DefaultCollection |
| **/noprompt** | Disables the prompt for confirmation. |
| **/?** or **help** | Displays help about the command in the Command Prompt window. |

**Remarks:**

The **witadmin rebuildcache** command invalidates cached data on all clients for a specified project collection. This causes the cache for each client to be refreshed the next time the client connects to the project collection. 

**Example:**

The following command invalidates the metadata cache for all clients that connect to DefaultCollection that is defined on the server that is named AdventureWorksServer. The client caches are updated the next time they connect to the project collection.

  ```witadmin rebuildcache /collection:http://AdventureWorksServer:8080/tfs/DefaultCollection```

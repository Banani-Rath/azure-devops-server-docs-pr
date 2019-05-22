---
title: Use SQL Server Always-on Availability Groups  
titleSuffix: Azure DevOps Server
description: Use SQL Server Always-on Availability Groups  
ms.manager: jillfra
ms.author: aaronha
author: aaronhallberg
ms.topic: conceptual
ms.date: 05/21/2019
ms.prod: devops-server
ms.technology: tfs-admin
---

# Use SQL Server Always-on Availability Groups

[!INCLUDE [temp](../../_shared/version-tfs-all-versions.md)]

This article provides general guidelines for enabling AlwaysOn Availability Groups with Azure DevOps Server. AlwaysOn Availability Groups requires a small amount of Azure DevOps Server-specific configuration, which can help you provide high availability (HA) to Azure DevOps Server relational databases like the TFS_Configuration and TFS_Collection databases. The Azure DevOps Server-specific configuration sets the MultisubnetFailover option to true in the connection string that Azure DevOps Server uses for the data tier. This configuration is not necessary for providing HA support for reporting or SharePoint. To provide high availability to the Azure DevOps Server report server or SharePoint deployment, see the documentation for those products. 

Azure DevOps Server support for AlwaysOn Availability Groups is an on or off proposition: if you use it, you must include your TFS_Configuration database as well as all of your TFS_Collection databases in the availability group. If you add a project collection in the future, the database for that collection must be added to the availability group in SQL Server.

You can have more than one SQL Server availability group.

See the SQL Server documentation for guidance about configuring AlwaysOn Availability Groups. Azure DevOps Server does not require any specific AlwaysOn Availability Group configuration. Use the configuration that best meets your team’s needs and the recommendations found in SQL Server guidance. For more information, see [Getting started with AlwaysOn Availability Groups (SQL Server)](/sql/database-engine/availability-groups/windows/getting-started-with-always-on-availability-groups-sql-server).

## Set up a new Azure DevOps Server installation with AlwaysOn Availability Groups

The following is a high-level walkthrough of the steps required to implement AlwaysOn Availability Groups during Azure DevOps Server installation.

> [!TIP]
> To set the MultisubnetFailover option to true in the connection string for an already running deployment of Azure DevOps Server, use the `RegisterDB` command of TFSConfig with the `/usesqlalwayson` argument. You'll need to use the TFSService Control Command to stop and start Azure DevOps Server before you can set the MultisubnetFailover option. For more information, see [RegisterDB command](../../command-line/tfsconfig-cmd.md#registerdb) and [TFSServiceControl command](../../command-line/tfsservicecontrol-cmd.md).

### One: set up AlwaysOn Availability Groups

The SQL Server AlwaysOn Availability Group must be ready before you install Azure DevOps Server. For more information, see [Getting started with AlwaysOn Availability Groups (SQL Server)](/sql/database-engine/availability-groups/windows/getting-started-with-always-on-availability-groups-sql-server).

### Two: install Azure DevOps Server by using the Advanced wizard

![Select AlwaysOn checkbox](_img/ic630622.png)

If you’re installing Azure DevOps Server for the first time, use the Advanced configuration wizard, which gives you access to the **SQL AlwaysOn Availability Group** check box (shown above). On this screen, enter the Availability Group Listener in the **SQL Server Instance** text box. Azure DevOps Server creates TFS\_Configuration and the DefaultCollection databases on the Primary replica of your AlwaysOn Availability Group. The databases for SharePoint are also created, if you allow Azure DevOps Server to install SharePoint Foundation.

> [!NOTE]
> Integration with SharePoint Products has been deprecated for TFS 2018 and later versions.

> [!TIP]
> You can also access the **SQL AlwaysOn Availability Group** check box by using the Application-Tier Only or Upgrade wizards. For more information, see [How to: Create an Azure DevOps Server farm (high availability)](../create-tfs-farm.md) or [Upgrade requirements](../../upgrade/get-started.md).

### Three: add the new Azure DevOps Server databases to the AlwaysOn Availability Group

![Add Azure DevOps Server databases to AlwaysOn Availability Group](_img/ic630623.png)

You’ll need to back up any databases that you want to add to the AlwaysOn Availability Group to bring them into compliance for data stored in an AlwaysOn Availability Group. Next, use the Availability Group wizard to add the databases to the group. For more information, see [Creation and configuration of Availability Groups (SQL Server)](/sql/database-engine/availability-groups/windows/creation-and-configuration-of-availability-groups-sql-server), and [Use the Availability Group Wizard (SQL Server Management Studio)](/sql/database-engine/availability-groups/windows/use-the-availability-group-wizard-sql-server-management-studio).

> [!TIP]
> If you add a new project collection to Azure DevOps Server, remember to add the database for the collection to your availability group in SQL Server. You cannot have some databases for project collections in and some outside the availability group.

## AlwaysOn Availability Groups support for reporting and SharePoint

The Azure DevOps Server-specific configurations described in this article are not necessary to provide HA support for reporting or SharePoint. To provide AlwaysOn support for those features, use the guidance available for those products, or implement another Azure DevOps Server-supported HA feature.

**Reporting and AlwaysOn Availability Groups**

-   [Reporting Services with AlwaysOn Availability Groups (SQL Server)](/sql/database-engine/availability-groups/windows/reporting-services-with-always-on-availability-groups-sql-server)
-   [Analysis Services with AlwaysOn Availability Groups](/sql/database-engine/availability-groups/windows/analysis-services-with-always-on-availability-groups)

**SharePoint and HA**

-   [Configure and manage SQL Server Availability Groups for SharePoint Server](/previous-versions/office/sharepoint-server-2010/hh913923(v=office.14))
-   [Plan for availability (SharePoint Server 2010)](/SharePoint/administration/plan-for-high-availability)
-   [SQL Server 2008 R2 and SharePoint 2010 Products: Better Together (white paper) (SharePoint Server 2010)](/previous-versions/office/sharepoint-server-2010/cc990273(v=office.14))
 

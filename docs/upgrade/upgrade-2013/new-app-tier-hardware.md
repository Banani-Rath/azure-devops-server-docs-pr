---
title: Use different hardware for your on-premises deployment
titleSuffix: TFS  
description: TFS Application Tier will use different hardware than it’s using right now
ms.manager: jillfra
ms.author: aaronha
author: aaronhallberg
ms.topic: conceptual
ms.date: 09/01/2016
ms.prod: devops-server
ms.technology: tfs-admin
monikerRange: 'tfs-2013'
---

# TFS Application Tier will use different hardware than it’s using right now

[!INCLUDE [temp](../../_shared/version-tfs-2013-only.md)]

Illustration of migration upgrade

![Illustration of migration upgrade](../../install/_img/ic612479.png)

## To do a hardware swap (migration) upgrade of Team Foundation Server 

![Number 1 in list](../../install/_img/ic756627.png) **Double Check**. Verify that the operating system and hardware meet the requirements for Team Foundation Server. You must use a 64-bit server if you use a server operating system.

Determine the service account you will use for Team Foundation Server. By default, TFS uses Network Service, but you can also use a domain account. In most cases, you should use the same account you used for the previous installation or consider using Network Service.

For more information, see [requirements for Team Foundation Server](/azure/devops/server/requirements), or [Accounts required for installation of Team Foundation Server](setup-sql-server.md).

![Number 2 in list](../../install/_img/ic646325.png) **Set up SQL Server**. You’re going to install all the SQL Server features that TFS requires on the same server where you’ll eventually run TFS.

For more information, see [Set up SQL Server for TFS](setup-sql-server.md)

![SQL server for TFS](../../install/_img/ic665430.png)

![Number 3 in list](../../install/_img/ic646326.png) **Set up SharePoint Products**. If you don’t skip the portal setup, you have two options for how to deal with SharePoint:

**Option one**: [Use the same SharePoint site for TFS that you have right now](use-same-sharepoint-site.md)

If your old SharePoint server is still running, you can continue to use it. Go to the SharePoint server and uninstall the old extensions, and then install the new extensions <span class="parameter">before</span> you upgrade TFS. If SharePoint and the previous version of TFS were on the same computer, you have to uninstall the entire TFS 2010 application tier. In the new upgraded configuration, the only TFS component on the SharePoint server will be the TFS extensions for SharePoint.

For more information, see [Use the same SharePoint site for TFS that you have right now](use-same-sharepoint-site.md)

![Uninstall TFS](../../install/_img/ic612480.png)

**Option two**: [Move SharePoint to New Hardware for TFS](../../install/sharepoint/move-sharepoint-new-hardware.md)

You can install SharePoint Foundation using the TFS extensions for SharePoint wizard. The TFS wizard will install a fresh copy of SharePoint using the installation of SQL Server you just set up, and then configure the TFS extensions for the new installation of TFS. After you install SharePoint, you’ll detach its content database to prepare for the migration of the data from your previous SharePoint installation in step 4, Restore Data.

For more information, see [Move SharePoint to new hardware for TFS](../../install/sharepoint/move-sharepoint-new-hardware.md)

![Install SharePoint products](../../install/_img/ic666062.png)

![Number 4 in list](../../install/_img/ic646327.png) **Restore data**. You can use the TFS custom backup and restore tools to manage your data. First you’re going to back up your data, including the encryption key on the report server. Next, you’re going to restore your data to the SQL Server instance you set up in step 2. With the restore complete, you’ll use the SQL Server Reporting tool to restart the report server database, restore its encryption key, and then verify access. If you installed SharePoint, you’ll use a SharePoint command line tool to attach and upgrade your content database.

For more information, see [Back up and restore data for TFS](backup-and-restore-data.md)

![Backup TFS database complete](../../install/_img/ic612476.png)

![Number 5 in list](../../install/_img/ic646328.png) **Upgrade TFS**. Run the Team Foundation Server install from the product DVD and then use the Upgrade Configuration wizard to upgrade your installation.

For more information, see [Run the TFS Upgrade Wizard](../run-upgrade-wizard.md)

![TFS server in file directory, then select upgrade](../../install/_img/ic612456.png)

> [!TIP]
> If you have Project Server added to TFS, this is the point where you should upgrade the TFS Extensions for Project Server. See the heading "Less-common upgrade tasks" for more information in [TFS upgrade requirements](/azure/devops/server/requirements)

## Next Step: Set up a new build machine

After you upgrade the application tier, you might want to install the new build service. For more information, see [Set up Team Foundation Build Service](https://msdn.microsoft.com/library/ee259687(v=vs.120).aspx).

![Set up new build machine](../../install/_img/ic612464.png)
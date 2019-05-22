---
title: Upgrade Azure DevOps Server Express or TFS Express  
titleSuffix: Azure DevOps Server   
description: Walkthrough of an Express upgrade
ms.prod: devops-server
ms.technology: tfs-admin
ms.manager: jillfra
ms.author: aaronha
author: aaronhallberg
ms.topic: conceptual
monikerRange: '>= tfs-2013'
ms.date: 08/04/2016
---

# Upgrade Azure DevOps Server Express edition

[!INCLUDE [temp](../_shared/version-tfs-all-versions.md)]

Upgrading Azure DevOps Server Express, previously named Team Foundation Server (TFS) Express, is about as simple as an upgrade can get. Because express installations are limited in size and to a single machine, and can't be configured to use multiple machines nor additional integrations such as SharePoint or reporting, the upgrade process. 

You can upgrade your express installation to a later version of Azure DevOps Server Express, or upgrade to a full installation. 

## Prepare your environment

As with any upgrade, you will need to check [system requirements](../requirements.md) to
ensure that your current configuration is supported. For an Express deployment this will mean 
checking the OS. The upgrade process will attempt to upgrade SQL Express to the latest version, which typically requires the latest service pack of whatever version
is currently installed. If in doubt, the upgrade process itself will tell you if you need to do 
something. 

## Expect the best, prepare for the worst

For Azure DevOps Express installations, performing a pre-production upgrade isn't typically worth the time 
because these installations are generally used by only a small number of people. 
However, it's always worth having a complete set of backups, so you should ensure that 
you [take backups](../admin/backup/back-up-restore.md) prior to starting the upgrade. The upgrade wizard provides access to a
database backup tool which can do this for you if you don't already have a process in place for
taking backups.

## Upgrade to a later express version

To upgrade to a later version, download and install the Azure DevOps Server Express version from the [Download page](https://www.visualstudio.com/downloads/download-visual-studio-vs). Install the software 
where you have the older version installed.
You will only need to make a couple of basic decisions. The installation remembers the settings from your previous installation.

::: moniker range="tfs-2015"

By default, the TFS 2015 Express upgrade will install and configure a build agent for the 
[new TFS 2015 build system](/azure/devops/build-release/overview), and will set it up to start automatically
so that you can start using it right away after your upgrade. If you do not want to use the 
new build system, you can uncheck the box to turn the agent off.

::: moniker-end

And that's it. As with all Azure DevOps configuration wizards, readiness checks will run to validate that your
system is ready to configure. When you choose **Configure your databases**, your database will be upgraded. 

## Upgrade to a full Azure DevOps Server version

Upgrading an express installation to a full Azure DevOps Server version, requires that you also upgrade from SQL Express to a SQL Server Standard or Enterprise edition.  
Basic steps are: 

1. [Backup your Azure DevOps databases](../admin/backup/back-up-restore.md)  

2. [Detach your collection(s) (databases)](../admin/move-project-collection.md#detach-coll)  

3. [Upgrade from SQL Express to SQL Server](/sql/database-engine/install-windows/upgrade-to-a-different-edition-of-sql-server-setup)  

	> [!NOTE]   
	> Make sure that you (1) enable the SQL Server Agent service in Windows SCM, and (2) provision the SQL Server Agent service account by using SQL Server Configuration Manager.  

4. [Install Azure DevOps Server (not express)](../install/single-server.md) 

5. [Attach collections (databases)](../admin/move-project-collection.md#attach-coll).  


## Related articles

- [Requirements for Azure DevOps on-premises](../requirements.md)
- [Service account requirements](../account-requirements.md)
- [Install and configure Azure DevOps on-premises](../install/get-started.md)
- [Upgrade get started](get-started.md)
- [Upgrade to a Different Edition of SQL Server (Setup)](/sql/database-engine/install-windows/upgrade-to-a-different-edition-of-sql-server-setup)
---
title: Upgrade Azure DevOps Server Express
titleSuffix: Azure DevOps Server   
description: Walkthrough of an Azure DevOps Server Express upgrade
ms.prod: devops-server
ms.technology: tfs-admin
ms.manager: jillfra
ms.author: aaronha
author: aaronhallberg
ms.topic: conceptual
monikerRange: '>= tfs-2013'
ms.date: 06/06/2019
---

# Upgrade Azure DevOps Server Express

[!INCLUDE [temp](../_shared/version-tfs-all-versions.md)]

Upgrading Azure DevOps Server Express is fairly simple, because Express installations are limited in size and to a single machine, and can't be configured for additional integrations such as reporting. 

You can upgrade your express installation to a later version of Azure DevOps Server Express, or upgrade to a full Azure DevOps Server installation. 

## Prepare your environment

As with any upgrade, first check the [system requirements](../requirements.md) to
ensure that your current configuration is supported. For an Express deployment, check the OS. The upgrade process will attempt to upgrade SQL Express to the latest version, which typically requires the latest service pack of the currently installed version. The upgrade process itself tells you if any required component is missing.

## Expect the best, prepare for the worst

For Azure DevOps Express installations, a pre-production upgrade isn't typically necessary, as these installations are used by only a small number of people. 
Even so, before starting the upgrade, you should [take backups](../admin/backup/back-up-restore.md). The upgrade wizard provides access to a
database backup tool which can do this for you if needed.

## Upgrade to a newer Express version

To upgrade to a newer version, download and install that Azure DevOps Server Express version from the [Download page](https://azure.microsoft.com/en-us/services/devops/server/). Install the software 
where you have the existing version installed.
You will only need to make a couple of basic decisions. The installation remembers the settings from your previous installation.

::: moniker range="tfs-2015"

By default, the TFS 2015 Express upgrade will install and configure a build agent for the 
[new TFS 2015 build system](/azure/devops/build-release/overview), and will set it up to start automatically
so that you can start using it right away after your upgrade. If you do not want to use the 
new build system, you can uncheck the box to turn the agent off.

::: moniker-end

As with all Azure DevOps configuration wizards, readiness checks will run to validate that your
system is ready to configure. When you choose **Configure your databases**, your database will be upgraded. 

## Upgrade to a full Azure DevOps Server version

Upgrading an express installation to a full Azure DevOps Server version requires that you also upgrade from SQL Express to a SQL Server Standard or Enterprise edition.  

The basic steps are: 

1. [Backup your Azure DevOps databases](../admin/backup/back-up-restore.md)  

2. [Detach your collection(s) (databases)](../admin/move-project-collection.md#detach-coll)  

3. [Upgrade from SQL Express to SQL Server](/sql/lp/sql-server/install-sql-and-services)  

	> [!NOTE]   
	> Make sure that you (1) enable the SQL Server Agent service in Windows Service Control Manager, and (2) provision the SQL Server Agent service account by using SQL Server Configuration Manager.  

4. [Install Azure DevOps Server (not Express)](../install/single-server.md) 

5. [Attach collections (databases)](../admin/move-project-collection.md#attach-coll).  


## Related articles

- [Requirements for Azure DevOps Server](../requirements.md)
- [Service account requirements](../account-requirements.md)
- [Install and configure Azure DevOps Server](../install/get-started.md)
- [Upgrade get started](get-started.md)
- [Upgrade to a different edition of SQL Server (setup)](/sql/lp/sql-server/install-sql-and-services)
---
title: Upgrade your deployment
description: Upgrade your instance of Azure DevOps Server or Team Foundation Server to the latest version
ms.prod: devops-server
ms.technology: tfs-admin
toc: show
ms.manager: jillfra
ms.author: aaronha
author: elbatk
ms.topic: conceptual
ms.date: 11/06/2018
---

# Upgrade your deployment to the latest version of Azure DevOps Server or Team Foundation Server

**Azure DevOps Server 2019 RC** | **TFS 2018** | **TFS 2017** | **TFS 2015**

The general process you use to upgrade an existing deployment of Azure DevOps Server is to:

- Prepare your environment.

    New [system requirements](../requirements.md) might require an upgrade to hardware or software. Either way, an upgrade is a good time to consider whether the current environment meets your needs, or if it makes sense to make changes.

- Expect the best, prepare for the worst.

    Even though Azure DevOps Server upgrades are reliable, it always makes sense to prepare for a worst-case scenario. Make sure you have a complete and consistent set of [database backups](../admin/backup/config-backup-sched-plan.md) available.

    > [!NOTE]
    > If you upgrade in place and don't move to new hardware, consider a [dry run](pre-production.md) of your upgrade in a pre-production environment.

- Do the upgrade.

    After you finish your preparation, install the new version of Azure DevOps Server. Get the binaries and run through the installation process to upgrade your servers.

- Configure new features.

    You might need to [configure each project](/azure/devops/work/customize/configure-features-after-upgrade) to gain access to new features that were made available. You don't have to make all configurations immediately, but some features aren't available until they're configured. Based on your project, use the Azure DevOps Server setup wizard to make changes or make changes manually in the Management Console.

## Previous versions

For previous versions of Team Foundation Server (TFS), the following upgrade matrix shows the proper steps to upgrade based on the version you upgrade from:

![TFS 2018 Upgrade path matrix for all versions](../_img/tfs2018upgradematrix.png)

### Before you upgrade to TFS 2018

Since Team Foundation Server 2017.2, the [old work item form <Layout> tag was deprecated](https://blogs.msdn.microsoft.com/devops/2017/05/22/announcing-the-deprecation-of-the-old-work-item-form-in-tfs/) and is no longer supported in Azure DevOps Server. If you upgrade your server and have a collection where the new work item form isn't enabled, you might see the following warning during validation:

> [VS403364]: This release introduces major updates to the work item form layout and functionality and deprecates legacy custom controls. Consequently, the upgrade process will update all work item type definitions to use the new work item form WebLayout element and remove all custom controls. For more information and recommended upgrade steps, see the Deployment Guide.

For more information, see [Handle a TFS 2018 upgrade from the old form to the new form](https://blogs.msdn.microsoft.com/devops/2017/05/22/announcing-the-deprecation-of-the-old-work-item-form-in-tfs).

### Before you upgrade to TFS 2017

If you use TFS with Project Server integration to synchronize your data, review the following articles: 

- [Synchronize TFS with Project Server](/azure/devops/work/tfs-ps-sync/sync-ps-tfs) for information on how native integration with Project Server is no longer supported. Instead, a solution is provided by our partner Tivitie.
- [Remove integration of TFS with Project Server](/azure/devops/work/tfs-ps-sync/remove-tfs-ps-integration) for steps on how to remove the integration. Complete this step after synchronization.

Review the options when you [upgrade from TFS 2008 or TFS 2010](/azure/devops/work/customize/upgrade-tfs-2008-or-2010). Choose between the options described based on how much you customized your work-tracking process.

## Complexity

Upgrading a TFS deployment can differ based on the specifics of your existing deployment. Factors that influence the complexity and duration of your upgrade include the:

- Number of servers involved in the deployment.
- Deployment configuration, which uses SharePoint integration or reporting.
- Size of the databases.
- Version of the upgrade.

In all cases, the general process is logically the same. Make sure your environment is ready. Then prepare and do the upgrade.

## Downtime

Your TFS deployment is offline for the duration of the upgrade. Upgrade times can differ based on the size of the deployment. To keep your upgrades comparably fast, [clean up unnecessary data](/azure/devops/tfs-server/upgrade/clean-up-data). It also helps if you keep up with the latest versions of Azure DevOps Server.

> [!TIP]
> If you upgrade a database to TFS 2015, consider using [TfsPreUpgrade](pre-upgrade.md). It performs the most expensive parts of the upgrade from TFS 2013 QU4/QU5 in the background. In this way, you can continue to use TFS, which can cut offline time significantly for large databases.

## See also

- [Walkthrough of a TFS Express upgrade](express.md)
- [Walkthrough of a standard upgrade scenario](walkthrough.md)
- [Walkthrough of an upgrade from TFS 2005 to TFS 2015](tfs-2005-to-2015.md)
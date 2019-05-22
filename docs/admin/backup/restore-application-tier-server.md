---
title: Restore an application-tier server
description: Restore an application-tier server
ms.topic: conceptual
ms.manager: jillfra
ms.author: aaronha
author: aaronhallberg
ms.prod: devops-server
ms.technology: tfs-admin
monikerRange: '>= tfs-2013'
ms.date: 05/20/2019
---

# Restore an application-tier server

[!INCLUDE [temp](../../_shared/version-tfs-all-versions.md)]

The databases for Azure DevOps store all data for your deployment of Azure DevOps Server. Even if you back up the application-tier server, you will not back up any data for Azure DevOps Server. However, if the hardware of an application-tier server fails, you can install another application-tier server and configure it to use the databases for your deployment. That server will then replace the offline server as the application-tier server for the deployment. If your application-tier server hosted SharePoint Products, you must also restore that software on the new hardware. For more information, see [Backup (SharePoint Foundation)](/previous-versions/office/sharepoint-foundation-2010/ee748624(v=office.14)), [Backup and recovery (SharePoint Server)](/SharePoint/administration/backup-and-recovery-overview), or [Protecting and restoring a farm (Office SharePoint Server 2007)](/previous-versions/office/sharepoint-2007-products-and-technologies/cc263053(v=office.12)).

> [!NOTE]
> After you restore an application tier to new hardware, verify that all users, groups, and service accounts for your deployment are configured with the permissions that they require to perform necessary tasks. For example, administrators for Azure DevOps must be members of the local **Administrators** group on the application-tier server so that they can open the administration console. For more information, see [Add users to projects](/azure/devops/security/add-users-team-project), [Set administrator permissions for project collections](../add-administrator.md), [Set administrator permissions for Azure DevOps Server](../add-administrator.md), and [Service accounts and dependencies in Azure DevOps Server](../service-accounts-dependencies.md).

You can also add more than one application-tier server to a deployment of Azure DevOps Server, but you must configure clients to connect to that server as a separate application tier. You cannot configure automatic load balancing between application-tier servers. For load balancing and transparency to clients, you must first install and configure a hardware or software device for network load balancing (NLB).

### To install and configure a server as the application-tier server

1.  Stop the application pools and services that Azure DevOps Server uses.

    For more information, see [TFSServiceControl command](../../command-line/tfsservicecontrol-cmd.md).

2.  If you are using Network Service as the service account for Azure DevOps (TFSService), on the application-tier server, open a Command Prompt window, and change directories to *Drive*:%programfiles%\\Azure DevOps Server 2019\\Tools. At the command prompt, enter the following command:

    **TfsConfig Accounts /add /account:"NT Authority\\Network Service" /accountType:ApplicationTier /SQLInstance:** *ServerName* **/DatabaseName:** *DatabaseName*

    > [!NOTE]
    >  For more information, see [Accounts command](../../command-line/tfsconfig-cmd.md#accounts).

3.  Install Azure DevOps Server on the new server, and start the **Application-Tier Only** wizard.

4.  If you are using Visual Studio Lab Management, install the System Center Virtual Machine Manager (SCVMM) Administrator Console on the application tier, and configure it to connect to the server that is running SCVMM.

    For more information, see [Configuring Lab Management for SCVMM environments](../config-lab-scvmm-envs.md).

5.  If the computer name has changed, open the administration console for Azure DevOps.

6.  In the navigation bar, select **Application Tier**, and then select **Change URLs**.

    The **Change URLs** window opens.

7.  In **Notification URL**, specify the URL for the new application-tier server, and then select **OK**.

    > [!NOTE]
    >  The name of the old application-tier server will still appear in the list of application-tier servers in the administration console for Azure DevOps. If you select the **Filter out machines that have not connected in more than 3 days** check box, the old server will disappear from the list within three days.

## Related articles

- [Restore Lab Management components](restore-lab-management-components.md) 
- [Azure DevOps Server architecture](../../architecture/architecture.md) 
- [Restore a deployment to new hardware](tut-single-svr-home.md) 
- [Open the Azure DevOps Server Administration Console](../open-admin-console.md) 

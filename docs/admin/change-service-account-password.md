---
title: Change service account credentials 
titleSuffix: Azure DevOps Server
description: Change the service account or password for Azure DevOps Server
ms.topic: conceptual
ms.manager: jillfra
ms.author: aaronha
author: aaronhallberg
ms.date: 04/25/2019
ms.prod: devops-server
ms.technology: tfs-admin
---

# Change the service account or password for Azure DevOps Server

[!INCLUDE [temp](../_shared/version-tfs-all-versions.md)]

You can help improve the security of Azure DevOps Server by changing its service account or the password used for that account. Azure DevOps Server runs services such as its web services and the Team Foundation Background Job Agent in the context of a service account. 

The Azure DevOps Server documentation refers to this service account as *TFSService*, although that is not the actual name of the account unless you specifically create an account with that name. Azure DevOps Server stores a record of the name of the actual account that is used as its service account. By changing the record, you can assign a different account to act as the service account. You can also change the password for that account. Whether you change the account, the password, or both, you stay synchronized with other components in your deployment. For example, if an Active Directory domain policy requires that all passwords expire periodically, you can update the password information for the service account in Azure DevOps Server when that password changes.

> [!NOTE]  
> Azure DevOps Server and its utilities cannot create a new local or domain account to use as *TFSService*, and they cannot update the password for that account in the workgroup or the domain. Instead, the utilities update the records to match the new credentials. If your deployment includes more than one application-tier server, you must manually update each server with any changes to the service account or its password.

For more information about service accounts in Azure DevOps Server, see [Service accounts and dependencies in Azure DevOps Server](service-accounts-dependencies.md). For more information about the accounts required for installation, including the service account for Azure DevOps Server, see [Service account requirements](../account-requirements.md).

## Prerequisites

 * To perform these procedures, you must be a member of the **Administrators** group on the Azure DevOps application-tier server and a member of the **sysadmin** group on the server and instance of SQL Server that hosts the configuration database for Azure DevOps. For more information, see [Azure DevOps Server architecture](../architecture/architecture.md) and [Permission reference for Azure DevOps Server](/azure/devops/security/permissions).

To follow a command-line procedure, you may need to open an elevated Command Prompt window. Open the context menu for Command Prompt and select **Run as Administrator**. For more information, see [User Account Control](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc772207(v=ws.10)).

## Change the password of the service account

To change the password of *TFSService*, you must log on to the application-tier server for Azure DevOps and either use the administration console for Azure DevOps, or open a Command Prompt window and use the TFSConfig command-line utility. If your deployment includes more than one application-tier server, you must perform this task on each server to keep the account information synchronized.

> [!NOTE]
> Depending on your deployment configuration, you may need to restart Internet Information Services (IIS) after you complete the procedure before the changes will take effect.

### Use the administration console to change the password

1.  Open the administration console for Azure DevOps on the server that hosts the application tier.

    For more information, see [Open the Azure DevOps Server Administration Console](open-admin-console.md) .

2.  In the console, expand the server name and select **Application Tier**.

3.  In the Application Tier pane, select **Update Account Password**.

    The **Update Account Password** window opens.

    > [!NOTE]
    > If you used a system account as the service account, you will see an error message when you select **Update Account Password**. You do not need to change the password of that account. System accounts do not have user-managed passwords.

4.  Enter the new password in **Password**, and then select **OK**.

    The **Change Service Account** window opens.

5.  Wait for all the status messages to complete in **Status**, and then select **Close**.

    > [!NOTE]
    > This process may take a few minutes.

**Use the TFSConfig utility to change the password**

1. On the application-tier server, open a Command Prompt window and change directories to the directory that contains the **TFSConfig** utility.

   By default, this utility is located in *Drive*:\\Program Files\\TFS 12.0\\Tools.

2. At the command line, enter **TFSConfig Accounts /UpdatePassword /accountType:ApplicationTier /account:**<em>AccountName</em> **/password:**<em>NewPassword</em>, and then press ENTER.

3. You must specify both the name of the service account (*AccountName*) and the password of the account (*NewPassword*).

## Assign a different account as the service account

To configure Azure DevOps Server to use a different account as the service account for Azure DevOps, you can use either the administration console or the **TFSConfig** command-line utility. If your deployment includes more than one application-tier server, you must perform this task on each server to keep the account information synchronized. Before you use either utility to make the change, consider the following issues:  
-   You must choose a new account that is either a system account or a member of a workgroup or domain that is trusted by every computer in this deployment of Azure DevOps Server.  
-   The configuration utilities grant the **Log on as a service** permission to the new service account. However, the utilities do not revoke this permission from the account previously used as the service account, if another service still uses that account. If the old account no longer needs that permission for the service for which it is still in use, you may want to manually remove that permission from the old account.

For more information, see [Add the Log on as a service right to an account](/previous-versions/windows/it-pro/windows-server-2003/cc739424(v=ws.10)).  

-   You may need to restart IIS after you complete the procedure before the changes will take effect.  
-   The **TFSConfig** utility changes only those services that run under the old account.

**Use the administration console to change the service account**

1.  Open the administration console for Azure DevOps on the server that hosts the application tier.

2.  In the console, expand the server name and select **Application Tier**.

3.  In the **Application Tier** pane, select **Change Account**.

    The **Update Service Account** window opens.

4.  Perform one of the following steps:

    1.  To use a system account, select **Use a system account**, and then select a system account from the drop-down list.

        If your server is a member of an Active Directory domain, the default choice for the system account to use is Network Service. If your server is a member of a workgroup, the default choice is Local Service. Depending on the details of your deployment, the default choice may be the only available choice.

        > [!NOTE]  
        >System accounts do not have user-managed passwords. If you use a system account as *TFSService*, you should not enter a password in the password field.
        
    2.  To use a domain or workgroup account, select **Use a user account**, enter the name of the account in **Account Name**, and then enter the password for that account in **Password**.

5.  Select **OK**.

    The **Change Service Account** window opens.

6.  Wait for all the status messages to complete in **Status**, and then select **Close**.

    > [!NOTE]
    > This process may take a few minutes.

**Use the TFSConfig utility to change the service account**

1. On the application-tier server, open a Command Prompt window and change directories to the directory that contains the **TFSConfig** utility.

   By default, this utility is located in *Drive*:\\Program Files\\TFS 12.0\\Tools.

2. At the command line, enter **TFSConfig Accounts /change /accountType:ApplicationTier /account:**<em>AccountName</em> **/password:**<em>NewPassword</em>, and then press ENTER.

   For more information, see [Accounts command](../command-line/tfsconfig-cmd.md#accounts).

## Related articles

- [Change the service account or password for SQL Server Reporting Services](change-service-account-or-password-sql-reporting.md)  
- [Accounts command](../command-line/tfsconfig-cmd.md#accounts)  
- [Service accounts and dependencies in Azure DevOps Server](service-accounts-dependencies.md)  
- [Managing server configuration with TFSConfig](../command-line/tfsconfig-cmd.md)  
- [How to: Change the password for Visual Studio Team Foundation Build Service](https://msdn.microsoft.com/library/bb778405)
 
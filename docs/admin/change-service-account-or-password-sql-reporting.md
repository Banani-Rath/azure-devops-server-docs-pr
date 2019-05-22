---
title: Change service credentials for SQL Server Reporting Services
titleSuffix: Azure DevOps Server 
description: Change the service account or password for SQL Server Reporting Services
ms.topic: conceptual
ms.manager: jillfra
ms.author: aaronha
author: aaronhallberg
ms.prod: devops-server
ms.technology: tfs-admin
monikerRange: '>= tfs-2013'
ms.date: 05/22/2019
--- 

# Change service credentials for SQL Server Reporting Services

[!INCLUDE [temp](../_shared/version-tfs-all-versions.md)]

You can help improve the security of Azure DevOps Server by
changing the service account that it uses for the data sources for SQL
Server Reporting Services or by changing the password that is used for
that account. Azure DevOps Server acts in the security context of a service account
when it retrieves project data from the data sources in SQL
Server Reporting Services. Azure DevOps Server documentation refers to this service
account by the placeholder *TFSReports*.
The actual account name depends on your installation. You may need to
change the password of that account, or designate a different account.
For example, if the password of the underlying account expires, and you
assign a new password, you must change the password of the 
*TFSReports* account in Azure DevOps Server to match.

You change the password or account used as the *TFSReports* account by using the **TFSConfig** command-line utility with the **Accounts** option.

The **TFSConfig** utility does not create a new account to use as the
data sources account, nor does the utility change the account password.
Instead, the utility updates Azure DevOps Server to use a different set of credentials.

> [!IMPORTANT]
> The **TFSConfig** utility changes only those services that run under the old account.

You can use the same utility to assign a different account to be the
*TFSReports* account, but you may need to
do one or more of the following additional actions:

-   Before you assign an account to use as the 
    *TFSReports* account, verify that it
    is a member of a workgroup or domain that is trusted by every
    computer in the deployment of Azure DevOps.
-   You must manually grant the account that you will use as the 
    *TFSReports* account the 
    **Allow log on locally** permission. The **TFSConfig**
    utility does not grant this permission when it assigns the account.
-   Optionally, after you use **TFSConfig** to specify an account to use as
    the *TFSReports* account, you can
    revoke its **Log on as a service**
    permission, which **TFSConfig** automatically grants to the 
    *TFSReports* account. 
    *TFSReports* does not need this permission,
    but the *TFSService* account does.
    Therefore, you should not remove this permission if you use the same
    domain or workgroup account for both service accounts.

    For more information about the **Log on as a service** permission, see [Add the Log on as a service right to an account](/previous-versions/windows/it-pro/windows-server-2003/cc739424(v=ws.10)). For more
    information about the **Allow log on locally** permission, see [Allow log on locally](/previous-versions/windows/it-pro/windows-server-2003/cc756809(v=ws.10)).

For more information about required service accounts, see 
[Service accounts and dependencies in Azure DevOps Server](service-accounts-dependencies.md) and
also [Accounts required for installation of Azure DevOps Server](service-accounts-dependencies.md).

### Prerequisites

To perform these procedures, you must be a member of the 
**Administrators** group on the server where **TFSConfig**
is installed. You must also be a member of the 
**sysadmin** group on the server that hosts the
configuration database. For more information about permissions, see
[Permission reference for Azure DevOps Server](/azure/devops/security/permissions).

In addition to these permissions, you may need to address the
following requirements:

-   To follow a command-line procedure, you may need to open an
    elevated Command Prompt.
-   To access Report Manager, reports, or websites for SQL
    Server Reporting Services, you may need to add these sites to the
    list of trusted sites in Internet Explorer or start Internet
    Explorer as an administrator.


## Use TFSConfig to update credentials

To change the password of the *TFSReports*
account or to assign a different account, log on to a server
that hosts the application services for Azure DevOps and use the
**TfsConfig Accounts** utility.

> [!NOTE]
> Depending on your deployment configuration, you may need to restart
> Internet Information Services (IIS) after you complete this procedure
> for the changes to take effect.

To change the password using the **TFSConfig** utility:

1.  Open a Command Prompt window and change to the directory that
    contains the **TFSConfig** utility.

    By default, the utility is located in 
    *Drive*:\\Program Files\\TFS 12.0\\Tools.

2.  At the command line, enter 
    **TFSConfig Accounts /UpdatePassword /accountType:ReportingDatasource /account:**
    *AccountName* **/password:** *newPassword*, and then press ENTER.

    Replace *AccountName* with the name of the current *TFSReports* account.
    Replace *newPassword* with the new password of the account.

To use the administration console to change the password:

1.  Open the administration console for Azure DevOps on the server
    that hosts the application tier.

    For more information, see [Configure and manage Azure DevOps Server resources](admin-quick-ref.md).

2.  In the console, expand the server name and select 
    **Application Tier**.

3.  In the Application Tier pane, navigate to 
    **Reporting Services Summary** and select 
    **Update Account Password**.

    The **Update Account Password** window opens.

    > [!NOTE]
    > If you used a system account as the service account, you will see an
    > error message when you select **Update Account
    > Password**. You do not need to change the password of that account.
    > System accounts do not have user-managed passwords.

4.  Enter the new password in **Password**, and
    then select **OK**.

    The **Change Report Reader Account**
    window opens.

5.  Wait for all the status messages to complete in 
    **Status**, and then select 
    **Close**.

    > [!NOTE]
    > This process may take a few minutes.

To assign a new Reporting Services service account to all Azure DevOps Server services using the TFSConfig utility:

1.  Open a Command Prompt window and change to the directory that
    contains the **TFSConfig** utility.

    By default, the utility is located in 
    *Drive*:\\Program Files\\Microsoft Team
    Foundation Server 12.0\\Tools.

2.  At the command line, enter **TFSConfig Accounts /change
    /accountType:ReportingDatasource /account:**
    *NewAccountName* **/password:**
    *newPassword*, and then press ENTER.

    Replace *NewAccountName* with the name
    of the new *TFSReports* account. Replace 
    *newPassword* with the password of
    the account.

## Use the administration console to update credentials

To use the administration console to change the account:

1.  Open the administration console for Azure DevOps on the server
    that hosts the application tier.

2.  In the console, expand the server name and select 
    **Application Tier**.

3.  In the Application Tier pane, navigate to 
    **Reporting Services Summary**, and then select
    **Change Account**.

    The **Change Report Reader Account**
    window opens.

4.  Choose one of the following steps:

    1.  To use a system account, select 
        **Use a system account**, and then select a
        system account from the drop-down list.

        > [!NOTE]
        > System accounts do not have user-managed passwords. If you select to use
        > a system account as *TFSReports*, you should not enter a password in the
        > password field.

    2.  To use a domain or workgroup account, select 
        **Use a user account**, enter the name of the
        account in **Account Name**, and then
        enter the password for that account in 
        **Password**.

5.  Select **OK**.

    The **Change Report Reader Account**
    window opens.

6.  Wait for all the status messages to complete in 
    **Status**, and then select 
    **Close**.

    > [!NOTE]
    > This process may take a few minutes.

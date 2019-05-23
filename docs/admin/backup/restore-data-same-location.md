---
title: Restore data to the same location
description: Restore data to the same location
ms.topic: conceptual
ms.manager: jillfra
ms.author: aaronha
author: aaronhallberg
ms.prod: devops-server
ms.technology: tfs-admin
monikerRange: '>= tfs-2013'
ms.date: 05/20/2019
---

# Restore data to the same location

[!INCLUDE [temp](../../_shared/version-tfs-all-versions.md)]

You can restore data from a backup to the same server and instance of SQL Server for Azure DevOps from which that data was backed up. For example, you may want to restore a corrupted set of databases to the last known good state.

> [!NOTE]
> Check out the [Back up and Restore concepts page](./back-up-restore.md#same-server) for an introduction to restoring data on the same server for Azure DevOps Server. 
>
> SharePoint integration with Azure DevOps Server is deprecated with TFS 2017 and later versions.



<a name="req-permissions"></a>
## Prerequisites

To perform this procedure, you must be a member of the following groups or have the following permissions:

-   A member of the **Administrators** security group on the server or servers running the administration console for Azure DevOps.
-   Either a member of the **SQL Server System Administrator** security group, or your **SQL Server Perform Back Up and Create Maintenance Plan** permission must be set to **Allow** on the instance of SQL Server that hosts the databases.
-   A member of the **sysadmin** security group for the database instance for Azure DevOps and for the Analysis Services instance of the warehouse database.
-   An authorized user of the TFS_Warehouse database.
-   A member of the **TFSEXECROLE** database role.
-   If the deployment uses SharePoint Products, a member of the **Farm Administrators** group for the farm to which the SharePoint Products databases are being restored.

For more information, see [User Account Control](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc772207(v=ws.10)).

<a name="stop-svcs-tfs-uses"></a>
## Step 1: Stop services

Stopping the services helps protect against data loss or corruption during the restoration process, particularly if you rename databases.

1.  On the server that is running the application-tier services for Azure DevOps, open a Command Prompt window, and change directories to *Drive*:\\%programfiles%\\Azure DevOps Server 2019\\Tools.

2.  Enter the following command:

        TFSServiceControl quiesce

    For more information, see [TFSServiceControl command](../../command-line/tfsservicecontrol-cmd.md).

<a name="rename-dbs-to-restore"></a>
## Step 2: Rename databases

Before you can use the Restore wizard to restore a database that Azure DevOps Server, you must first take it offline, and then rename it.

### Stop databases

1.  Open **SQL Server Management Studio**.

    > [!NOTE]  
    > For more information about how to restore databases, see [Implement restore scenarios for SQL Server databases](/previous-versions/sql/sql-server-2008-r2/ms175199(v=sql.105)).

    The **Connect to Server** dialog box opens.

2.  In **Server type**, select **Database Engine**.

3.  In **Server name**, enter or select the name of the data-tier server and database instance, and then select **Connect**.

    > [!NOTE]  
    > If SQL Server is installed on a cluster, the server name is the name of the cluster and not the computer name.

    SQL Server Management Studio opens.

4.  Expand the **Databases** node to show the list of databases that make up the data tier for Azure DevOps.

5.  Rename and then stop each database you want to restore, following [the guidance for your version of SQL Server](https://technet.microsoft.com/library/ms345378.aspx). Give the database a name indicating it is the old version of the database you will replace with the restored version. For example, you could rename TFS_DefaultCollection to TFS\_DefaultCollection\_Old.

<a name="restore-tfs-dbs"></a>
## Step 3: Restore Azure DevOps databases

You can restore data for Azure DevOps Server by using the Restore wizard in the administration console in Azure DevOps Server. The Restore wizard also restores the encryption key used for reporting.

### Restore databases

1.  Open the administration console for Azure DevOps Server, navigate to **Scheduled Backups**, and start the **Restore Databases** wizard.

    ![Start the Restore wizard](../_img/ic654273.png)

2.  Specify the path to the backup set and select the set to use for restoration.

    ![Select the network path, then the restore set](../_img/ic664997.png)

3.  Complete the wizard and restore the databases.

    ![The databases are restored to the new server](../_img/ic664998.png)

<a name="update-all-svc-accts"></a>
## Step 4: Update all service accounts

You must update the service account for Azure DevOps Server (TFSService) and the data sources account (TFSReports). Even if these accounts have not changed, you must update the information to ensure that the identity and the format of the accounts are appropriate.

### Update service accounts

1.  On the server that is running SQL Server Reporting Services, open **Computer Management**, and start the following components if they are not already started:

    -   ReportServer or ReportServer$*InstanceName* (application pool)
    -   SQL Server Reporting Services (*TFSINSTANCE*)

2.  On the application-tier server, open a Command Prompt window, and change directories to *Drive*:\\%programfiles%\\Azure DevOps Server 2019\\Tools.

3.  At the command prompt, enter the following command to add the service account for Azure DevOps, where *DatabaseName* is the name of the configuration database (by default, TFS_Configuration):

    **TfsConfig Accounts /add /AccountType:ApplicationTier /account:** *AccountName*

    For more information, see [Accounts command](../../command-line/tfsconfig-cmd.md#accounts).

4.  Use the **Accounts** command to add the data sources account for the report server and the proxy account for Azure DevOps Proxy Server, if your deployment uses these resources.

<a name="rebuild-the-warehouse"></a>
## Step 5: Rebuild the data warehouse

You can rebuild the data warehouse instead of restoring the TFS_Warehouse and TFS_Analysis databases. It may require a significant amount of time to rebuild the warehouse if your deployment contains a lot of data. However, this strategy helps ensure that all data is properly synchronized. When you rebuild the warehouse, Azure DevOps Server creates an instance of it, which you must then process to populate it by using data from the operational stores.

> [!NOTE]  
> If you restored the TFS_Warehouse and TFS_Analysis databases in the previous section, you do not have to perform the following procedure.

### Rebuild the warehouse

1. On the server that is running the application-tier services for Azure DevOps, open a Command Prompt window, and change directories to *Drive*:\\%programfiles%\\Azure DevOps Server 2019\\Tools.

2. Enter the following command:

    **TFSConfig rebuildwarehouse /all /ReportingDataSourcePassword:**  *Password*

   where *Password* is the password for the data sources account for Reporting Services (TFSReports).

3. Wait until the command completes.

4. On the report server, open Internet Explorer and enter the following string in the Address bar:

   **<http://localhost:8080/>**<em>VirtualDirectory</em>**/TeamFoundation/Administration/v3.0/WarehouseControlService.asmx**

   For *VirtualDirectory*, enter the virtual directory for Internet Information Services (IIS) that was specified when Azure DevOps Server was installed. By default, this directory is named **tfs**.

   The **WarehouseControlWebService** page opens.

   > [!NOTE]  
   > The Microsoft Azure DevOps Server Application Pool must be running for the Warehouse Control web service to be available.

5. Select **GetProcessingStatus**, and then select **Invoke**.

   > [!IMPORTANT]
   > The service should return a value of **Idle** for all jobs, which indicates that the cube is not being processed. If a different value is returned, repeat this step until **Idle** is returned for all jobs.

6. On the **WarehouseControlWebService** page, select **ProcessAnalysisDatabase**, and then select **Invoke**.

   A browser window opens. The service returns **True** when it successfully starts to process the cube and **False** if it is not successful or if the cube is currently being processed.

7. To determine when the cube has been processed, return to the **WarehouseControlWebService** page, select **GetProcessingStatus**, and then select **Invoke**.

   Processing is complete when the **GetProcessingStatus** service returns a value of **Idle** for all jobs.

8. On the application-tier server for Azure DevOps, open **Computer Management**, and start the Visual Studio Team Foundation Background Job Service.

<a name="clear-data-cache-on-servers"></a>
## Step 6: Clear the data cache on application-tier servers

Each application-tier server in your deployment of Azure DevOps uses a file cache so users can quickly download files from the data-tier server. When you restore a deployment, you should clear this cache on each application-tier server. Otherwise, mismatched file IDs could cause problems when users download files from version control. If your deployment uses Azure DevOps Proxy Server, you must also clear the data cache on each server that is configured as a proxy.

> [!NOTE]  
> By clearing the data caches, you can help prevent the download of incorrect versions of files in version control. You should routinely do this unless you are replacing all hardware in your deployment as part of your restoration. If you are replacing all hardware, you can skip this procedure.

### Clear the data cache

1.  On a server that is running the application-tier services for Azure DevOps or that is configured with Azure DevOps Proxy Server, open a Command Prompt window and change directories to *Drive*:\\%programfiles%\\Azure DevOps Server 2019\\Application Tier\\Web Services\\\_tfs\_data.

2.  Delete everything in the \_tfs\_data directory.

3.  Repeat these steps for each application-tier server and each server that is running Azure DevOps Proxy Server in your deployment.

<a name="restart-svcs-tfs"></a>
## Step 7: Restart services  

After you restore the data, you must restart the services to return the server to an operational state.

### Restart services  

1.  On the server that is running the application-tier services for Azure DevOps, open a Command Prompt window, and change directories to *Drive*:\\%programfiles%\\Azure DevOps Server 2019\\Tools.

2.  Enter the following command:

     **TFSServiceControl unquiesce** 

For more information, see [TFSServiceControl command](../../command-line/tfsservicecontrol-cmd.md).

<a name="refresh-caches-clients"></a>
## Step 8: Refresh the caches on client computers

### Refresh the cache for tracking work items on client computers

1.  On the new server, open Internet Explorer.

2.  In the Address bar, enter the following address to connect to the **ClientService** web service:

    **http://** *PublicURL/VirtualDirectory* **:8080/WorkItemTracking/v3.0/ClientService.asmx**

    > [!NOTE]  
    > Even if you are logged on with administrative credentials, you may need to start Internet Explorer as an administrator, and you may be prompted for your credentials.

3.  Select **StampWorkitemCache**, and then select **Invoke**. The StampWorkitemCache method returns no data.

### Refresh the version control cache on client computers

1. On the client computer, open a Command Prompt window with administrative permissions, and change directories to *Drive*:\\Program Files (x86)\\Microsoft Visual Studio 12.0\\Common7\\IDE.

2. At the command prompt, enter the following command, including the URL of the collection, which includes the server name and the port number of the new server:

   **tf workspaces /collection:http://**<em>ServerName:Port/VirtualDirectoryName/CollectionName</em>

   In the example deployment, a developer needs to refresh the version control cache for a project that is a member of the DefaultCollection collection, which is hosted in the FabrikamPrime deployment of Azure DevOps Server:

   **tf workspaces /collection:<http://FabrikamPrime:8080/tfs/DefaultCollection>**

   For more information, see [Workspaces command](/azure/devops/tfvc/workspaces-command).

## Related articles

- [Permission and groups reference](/azure/devops/organizations/security/permissions) 
- [Architecture overview](../../architecture/architecture.md) 
- [Restore the databases](tut-single-svr-restore-dbs.md) 
- [Administrative tasks quick reference](../admin-quick-ref.md) 
- [Restore a deployment to new hardware](tut-single-svr-home.md) 

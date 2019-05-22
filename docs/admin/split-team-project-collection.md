---
title: Split a project collection
titleSuffix: Azure DevOps Server
description: Split a project collection for Azure DevOps Server
ms.topic: conceptual
ms.manager: jillfra
ms.author: aaronha
author: aaronhallberg
ms.date: 05/22/2019
ms.prod: devops-server
ms.technology: tfs-admin
---

# Split a project collection

[!INCLUDE [temp](../_shared/version-tfs-all-versions.md)]

As your business changes, you may want to split a single project collection into multiple project collections. For example:

-   You want the projects in a collection to align with business units in your organization, and the projects in the collection are now owned by separate units.
-   You upgraded from an earlier version of Azure DevOps Server, you have only one collection, and you want to organize your projects into separate collections for security or business alignment reasons.
-   You want to change ownership of some of the projects in the collection to a remote office that has its own deployment of Azure DevOps Server. This scenario requires that you first split a collection and then move one of the resulting collections to the remote office deployment.

	> [!NOTE]
	> The procedures in this article support only splitting a project collection. To move a collection after you split it, see [Move a project collection](move-project-collection.md).

To split a project collection, follow these steps:

1.  **Prepare to split the collection**

    1.  [Detach the collection](#detach-the-coll)

    2.  [Back up the collection database](#backup-coll-db)

2.  **Split the collection**

    1.  [Restore the collection database with a different name](#restor-coll-db-new-name)

    2.  [Attach the original collection database](#attach-original-coll-db)

    3.  [Attach the renamed collection database](#attach-renamed-coll-db)

    4.  [Delete projects from the split collections](#delete-projs-split-colls)

    5.  [Start the collections](#start-team-proj-coll)

3.  **Configure the split collections**

    1.  [Configure Users and Groups for the Split Project Collections](#config-users-split-colls)

    2.  [Configure users and groups for projects in the collections](#config-users-projs)

**Before you begin**

Make sure that you're an administrator on the servers and in SQL Server and Azure DevOps Server. If you're not an administrator, [get added as one](add-administrator.md).

<a name="detach-the-coll"></a>
## 1-a. Detach the collection

First detach the collection from the deployment of Azure DevOps Server on which it is running. Detaching a collection stops all jobs and services as well as the collection database itself. In addition, the detach process copies over the collection-specific data from the configuration database and saves it as part of the project collection database.

### Detach a project collection

1.  Open the administration console for Azure DevOps on the server that hosts the collection to split.

2.  Select **Project Collections**, and in the list of collections, select the collection  to split.

    In this example, the administrator chooses **TestProjects**.

    ![Select collection from list of collections](_img/ic738726.png)

	> [!TIP]
	> The default name for a project collection is **DefaultCollection**. If you are splitting this database, make sure to give the second collection a different name, because this is the default choice at connection.

3.  On the **General** tab, select **Stop Collection**.

    ![Stop collection interface](_img/ic738727.png)

    The **Project Collection Status Reason** dialog box opens. The text you enter will be displayed to your users. Select **Stop**, and wait for the collection to stop. When it is stopped, its status will show as **Offline**.

4.  On the **General** tab, select **Detach Collection**.

    The **Detach Project Collection Wizard** opens.

    ![Detach collection wizard](_img/ic738728.png)

5.  (Optional) On the **Provide a servicing message for the project collection** page, in **Servicing Message**, provide a message for users who may try to connect to projects in this collection.

6.  On the **Review settings that will be used to detach project collection** page, review the details. To change any settings, select **Previous**. If they are correct, select **Verify**.

7.  When all the readiness checks have completed successfully, select **Detach**.

8.  On the **Monitor the project collection detach progress** page, when all processes have completed, select **Next**.

9.  (Optional) On the **Review supplemental information for this project collection** page, select or note the location of the log file, and then close the wizard.

    The project collection no longer appears in the list of collections in the administration console.

<a name="backup-coll-db"></a>
## 1-b. Back up the collection database

After you have detached the collection, you must back up its database before you can restore a copy to the server with a different name. That copy will become the database for the part of the original collection that you want to split into another collection. To perform this task, use the tools that are provided with SQL Server.

![Back up database](_img/ic738721.png)

### Back up a collection database

-   For information about how to manually back up and restore individual databases, see [Back up and restore databases in SQL Server](/previous-versions/sql/sql-server-2008/ms187048(v=sql.100)) and [Create a backup schedule and plan](backup/config-backup-sched-plan.md). Be sure to select the version of SQL Server that matches your deployment.

    > [!IMPORTANT]
    > If your original deployment used the Enterprise or Datacenter editions of SQL Server, and you want to restore the database that you want to split to a server running Standard edition, you must use a backup set that was made with SQL Server compression disabled. Unless you disable data compression, you will not be able to successfully restore Enterprise or Datacenter edition databases to a server running Standard edition. To turn off compression, follow the steps in [Disable SQL Server data compression in Azure DevOps databases](https://support.microsoft.com/help/2712111/disabling-sql-server-data-compression-in-tfs-databases).

<a name="restor-coll-db-new-name"></a>
## 2-a. Restore the collection database

When you split a collection, you must restore the backup of the collection database to an instance of SQL Server that is configured to support the deployment of Azure DevOps Server. When you restore the database, you must give it a different name from the name of the original collection database.

> [!TIP]
> The steps below give a general overview of how to restore a project collection database in SQL Server 2012 using SQL Server Management Studio. For more information about how to manually back up and restore individual databases, see [Back up and restore databases in SQL Server](/previous-versions/sql/sql-server-2008/ms187048(v=sql.100)). Be sure to select the version of SQL Server that matches your deployment.

### Restore the collection database with a new name

1.  Open SQL Server Management Studio and connect to the instance that hosts the database for the project collection to split.

2.  In Object Explorer, expand **Databases**, open the sub-menu for the database to split, and then select **Tasks**, select **Restore**, and then select **Database**.

    The Restore Database window opens on the **General** page.

    ![Restore database option from General pane](_img/ic738729.png)

3.  In **Source**, make sure that the project collection database is chosen. In **Destination**, provide a name for the copy of the database. Keep the Tfs\_ prefix, and add a distinct name. Typically, that name is the name of the split project collection. In **Restore plan**, make sure that the backup sets to restore are the ones you want to restore to. To make sure that these are valid sets, select **Verify Backup Media** and then, in **Select a page**, select **Options**.

4.  In **Restore options**, leave all the check boxes blank. Make sure that **Recovery state** is set to **RESTORE WITH RECOVERY**. In **Tail-Log Backup**, clear the **Leave source database in the restoring state** check box, and then select **OK**.

	> [!TIP]  
	>If the restore operation fails with an error message indicating that the database is in use and cannot be overwritten, you may need to manually configure all the logical file names to reflect the new name for the database. In **Select a page**, select **Files**, select the ellipsis button next to each file being restored, and make sure that the names of the files reflect the new name for the database, not the old one. Then try the restore operation again.

<a name="attach-original-coll-db"></a>
## 2-b. Attach the original collection database

After you have restored the database with a different name, reattach the original collection database to the deployment of Azure DevOps Server.

> [!NOTE]
> If your deployment uses SharePoint Products and the service account for Azure DevOps Server is not a member of the Farm Administrators group, warnings will appear when you attach the collection. This is expected behavior and you can proceed.
>
> Integration with Sharepoint Products has been deprecated for TFS 2018 and later versions.


### Attach the collection

1.  Open the administration console for Azure DevOps.

2.  Select **Project Collections**, and then select **Attach Collection**.

    The **Attach Project Collection Wizard** opens.

3.  On the **Select the project collection database to attach** page, in **SQL Server Instance**, provide the name of the server and the instance that hosts the collection database, if it is not already listed.

4.  In the **Databases** list, select the collection database to attach.

    ![Databases list](_img/ic738730.png)

5.  On the **Enter the project collection information** page, provide a name for the collection in **Name** if one is not already present. Since this is the original collection, you can select to leave the name the same as it was before. In **Description**, optionally provide a description of the collection.

6.  On the **Review settings that will be used to attach the project collection** page, review the information.

7.  To change any settings, select **Previous**. If all the settings are correct, select **Verify**.

8.  When all the readiness checks have completed successfully, select **Attach**.

9.  On the **Monitor the project collection attach progress** page, when all processes have completed, select **Next**.

10. (Optional) On the **Review supplemental information for this project collection** page, select or note the location of the log file, and close the wizard.

11. The project collection appears in the list of collections in the administration console. **If the collection state is listed as** **Online**, **you must stop it before continuing.** Select the collection from the list, and on the **General** tab, select **Stop Collection**.

    ![Stop collection image](_img/ic738731.png)

<a name="attach-renamed-coll-db"></a>
## 2-c. Attach the renamed collection database

After you attach the original collection database, you must attach the renamed collection to the deployment of Azure DevOps Server. When this collection is attached, it will remain stopped. You will not be able to start it until all duplicate projects have been removed.

> [!NOTE]
> Warnings will appear when you attach the collection if your deployment uses SharePoint Products and the service account for Azure DevOps Server is not a member of the Farm Administrators group. This is expected behavior and you can proceed.


### Attach the renamed collection database

1.  Open the administration console for Azure DevOps.

2.  Select **Project Collections**, and then select **Attach Collection** to open the wizard.

3.  On the **Select the project collection database to attach** page, in **SQL Server Instance**, provide the name of the server and the instance that hosts the renamed collection database, if it is not already listed.

4.  In the **Databases** list, select the renamed collection database.

5.  On the **Enter the project collection information** page, enter a name for the renamed collection in **Name** that differs from the name of the original name of the collection. This should match the name you gave the renamed database, without the Tfs\_ prefix.

    ![Attach team project name entry](_img/ic738732.png)

6.  (Optional) In **Description**, enter a description of the collection.

7.  On the **Review settings that will be used to attach the project collection** page, review the information. To change any settings, select **Previous**. If all the settings are correct, select **Verify**.

8.  When all the readiness checks have completed successfully, select **Attach**.

9.  On the **Monitor the project collection attach progress** page, when all processes have completed, select **Next**.

	> [!NOTE]
	> If the collection is supported by a SharePoint web application, a warning icon will appear for the attach status of the SharePoint web application. Similarly, if the original collection included reporting, a warning icon will appear for the attach status for reports. This is expected behavior and you can proceed.

10. (Optional) On the **Review supplemental information for this project collection** page, select or note the location of the log file, and then close the wizard.

11. The name of the collection appears in the list of collections in the administration console, and its status should display as **Offline**.

    ![Attach team project name entry](_img/ic738732.png)

12. To ensure that both collections have attached with unique IDs, in the administration console, go to Event Logs and open the log files for both collection attach operations. The GUIDs for CollectionProperties should **not** match.

    ![Logs that include GUIDs for CollectionProperties](_img/ic740323.png)

    In the unlikely event that the CollectionProperties GUIDs do match, change the ID to a unique ID before continuing by running the TFSConfig [Collection command](../command-line/tfsconfig-cmd.md#collection) on the second collection with the /clone parameter.

<a name="delete-projs-split-colls"></a>
## 2-d. Delete projects on the split collections

Now that you have two copies of the collection attached to Azure DevOps Server, you must delete each project from either the original collection or the renamed collection so that no project remains in both collections.

> [!IMPORTANT]
> A project cannot exist in more than one collection. Until you delete all duplicated projects between the split collections, you will not be able to start the renamed collection.

### Delete projects from the collections

1.  Open the administration console for Azure DevOps.

2.  Select **Project Collections**, and in the list of collections, select the original project collection that you stopped in order to split it.

3.  On the **Projects** tab, in the list of projects, select a project to delete from the collection, and then select **Delete**.

	> [!TIP]
	> You can select more than one project to delete at a time.

    ![TFS Administration console for deleting projects](_img/ic738734.png)

4.  Select the **Delete workspace data** check box, leave the **Delete external artifacts** check box cleared, and then select **Delete**.

    If the **Delete external artifacts** check box is not cleared and your project is configured to use Lab Management, the virtual machines and templates that are associated with the project will be deleted from System Center Virtual Machine Manager. They will no longer be available to the project in the renamed collection. (Note that Lab Management has been deprecated for TFS 2017 and later versions.)

5.  When you have finished deleting the projects you do not want hosted in the original project collection, select the renamed project collection from the list of collections. Then, on the **Projects** tab, delete the unwanted projects from the new collection.

    ![Projects in projects tab](_img/ic738735.png)

6.  Repeat the steps in this section until both collections contain a set of unique projects.

<a name="start-team-proj-coll"></a>
## 2-e. Start the project collections

After you delete projects, restart both collections.

### Start a project collection

1.  Open the administration console for Azure DevOps.

2.  Select **Project Collections**, and in the list of collections, select the collection that you stopped in order to split it.

3.  On the **General** tab, select **Start Collection**.

4.  Repeat step 2 for the collection that you attached with a new name.

    ![TFS Administration console](_img/ic738736.png)

<a name="config-users-split-colls"></a>
## 3-a. Configure users and groups for the split collections

You can skip this procedure if both split collections will remain in the same domain and you want to allow access for the administrators of the original collection to both collections.

After you have split a collection, you must update the permission groups for both collections with users and groups that will administer those collections. For more information, see [Set administrator permissions for project collections](add-administrator.md).

<a name="config-users-projs"></a>
## 3-b. Configure users and groups for projects

You can skip this procedure if the split collections will remain in the same domain and you want to allow access for the users of projects in the original collection to both collections.

After you configure administrators for both collections, either you or those administrators must configure access for users and groups to the projects in each collection. Depending on your deployment, you may also need to configure permissions for those users in SharePoint Products and Reporting Services. For more information, see [Add users to projects or teams](/azure/devops/security/add-users-team-project). 

<a name="q-and-a"></a>
## Q & A

### Q: My deployment uses reporting. Are there any additional steps I need to take when splitting collections?

**A:** Yes, you'll need to split reports after you've finished deleting projects so that both collections have a unique set of projects. You'll also need to rebuild your data warehouse.

After you delete projects, move the reports that the split collection uses into a different folder, and then delete them from the original folder.

> [!IMPORTANT]
> The report folders exist in both locations. Make sure that you move all reports appropriately before you delete any report folders.

### Split reports into separate folders

1.  In Report Manager, move the reports that support the split collection into the appropriate folders for that collection. For more information, see [Move Items Page](/previous-versions/sql/sql-server-2016/ms189988(v=sql.130)).

2.  If your deployment uses a SharePoint web application, you may need to repair the connection again after you move the reports before they will appear correctly. If reports do not appear correctly, follow the steps in the previous procedure to repair the connection.

Once you've split the reports and started both collections, rebuild the warehouse for Azure DevOps and the database for Analysis Services. You must perform this step to ensure that reports and dashboards work correctly for the deployment after you split the collection and that no conflicts occur with other collections in the deployment.

### Rebuild the data warehouse and the Analysis Services database

1.  Open the administration console for Azure DevOps.

2.  In the navigation bar, select **Reporting**.

3.  In **Reporting**, select **Start Rebuild**.

4.  In the **Rebuild the Warehouse and Analysis Services Databases** dialog box, select **OK**.

	> [!NOTE]
	> The warehouses will continue to be rebuilt and the data will continue to be repopulated after the Start Rebuild action finishes. Depending on the size of your deployment and the amount of data, the whole process may take several hours to complete.

::: moniker range="<= tfs-2017"
### Q: Can I split a collection that uses SharePoint Products to support one or more projects in the collection?

**A:** Yes, but you'll need to perform additional steps for the split collection.

After you attach the renamed collection and remove all duplicate projects, repair the connection to the SharePoint web application. Repairing the connection ensures that all connections are correctly set between the web application and the original and renamed collections.

If your deployment uses SharePoint Products, it is strongly recommended that the service account for Azure DevOps Server be a member of the **Farm Administrators** group.

> [!NOTE]
> You can split a project collection without granting this membership to the service account for Azure DevOps Server. However, you will see errors when you attach the collection, and you will need to perform additional steps to reconnect projects with their portals. Even if your operational requirements generally restrict granting this membership to the service account, you should consider adding the service account to the Farm Administrators group for the duration of the split operation.
::: moniker-end

### Repair the connection to a SharePoint web application

1.  Open the administration console for Azure DevOps on the server that hosts the application tier for the deployment to which you'll move the collection.

2.  Select **SharePoint Web Applications**, and in the list of web applications, select the web application that supports the collections that you just attached.

    The **Repair Connection** button appears after you select a web application in the list.

3.  Select **Repair Connection**, and in the **Repair the connection to a SharePoint Web Application** dialog box, select **Repair**.

4.  When the Status window reports **Reconnect operation succeeded**, select **Close**. This may take a few minutes. In addition, you may see some errors as part of this process, since the two collections are still using the same SharePoint default site location for their project portals. This is expected behavior and you can proceed.

After you have repaired the connection and started both collections, you must reconfigure the project portals for projects in each collection so that those portals reflect the correct data for those projects.

<a name="configportals"></a>
### Reconfigure project portals

-   Open Team Explorer, connect to each project collection, and for each project, configure the URL for the SharePoint site. For each project, select **Settings**, select **Portal Settings**, and make sure that the **Reports and dashboards refer to data for this project** check box is selected.

You can continue to use the same site collection in SharePoint Products to support both split collections. Projects in both collections will use the same project portals as before. All portals are hosted on the site collection that supported the original project collection. However, this configuration not only complicates the one-to-one relationship between a project collection and a site collection, but may also make restoring your deployment more difficult. To avoid this complexity, you can split the site collection that supported the original project collection to reflect the split that you made for the project collections.

### Split the site collection and redirect the split project collections to use the split site collections

1.  For information about how to split a site collection, see [Move site collections between databases](https://technet.microsoft.com/library/cc825328(v=office.15).aspx) or the latest guidance for your version of SharePoint Products.

	> [!TIP]
	> Make sure that you configure user permissions and access to the site collections to match the user access to the project collections, as described earlier in this article.

2.  Configure any affected project collection to use the split site collection by opening the administration console, choosing the collection from the list of the project collections, and on the SharePoint Site tab, choosing **Edit Default Site Location**.

3.  Reconfigure the project portals for projects in each collection so that those portals reflect the correct data for those projects.

    For more information, see [Reconfigure project portals](split-team-project-collection.md#configportals) above.



### Q: How do I split a collection configured for Lab Management?

**A:** You'll need to perform several additional steps to split the collection. Before you start the split, you'll need to delete the Lab Management resources from the collection, and then, after the split, you'll have to individually configure Lab Management resources for each of the split collections.

> [!NOTE]
> Lab Management has been deprecated for TFS 2017 and later versions.

Before you start the split, delete the resources that Lab Management uses from the collection database. These resources include virtual machines, templates, project host groups, and project library shares. You will need to re-create the Lab Management assets after you restore and attach the collection.

### Delete the Lab Management resources

-   For information about how to remove all group hosts, library shares, and environments from a specified project collection, see [TFSConfig Lab /Delete command](../command-line/tfsconfig-cmd.md#lab-delete) with the **/External** option.

Once you've completed the split, recreate the project host groups. You must also recreate project library shares in Azure DevOps Server and the virtual machines, templates, and environments in Microsoft Test Manager.

### Configure Lab Management resources

1.  Configure the application tier for Azure DevOps.

    For more information, see [Configure Lab Management for SCVMM environments](config-lab-scvmm-envs.md).

2.  Recreate the golden master virtual machines and templates in the new SCVMM and import virtual machines and templates into the project collection.

    For more information, see [How to: Create and store virtual machines and templates ready for Lab Management](https://msdn.microsoft.com/library/ee702479(v=vs.120).aspx).

3.  Recreate the environments for each project.

    For more information, see [Create an SCVMM environment using stored virtual machines and templates](https://msdn.microsoft.com/library/ee518915(v=vs.120).aspx).

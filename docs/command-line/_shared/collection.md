---
ms.topic: include
---

::: moniker range="azure-devops-2019"

You can use the **collection** command to attach, detach, or delete a project collection from a deployment of Azure DevOps Server.
You can also use the **collection** command to duplicate the database of an existing collection, rename it, and attach it to the deployment.
This process is sometimes referred to as cloning a collection.

```
TfsConfig collection {/attach | /create | /detach | /delete} [/collectionName:<collectionName>]
    [/description:<collectionDescription>]
    [/collectionDB:<serverName>;<databaseName>]
    [/processModel:Inheritance|Xml]
    [/reportingFolder:<reportingFolderPath>]
    [/clone] [/verify] [/continue]
```

|Option|Description|
|---|---|
|attach|Required if neither <strong>/detach</strong> nor <strong>/delete</strong> is used. If you specify this option, you must also use the <strong>/collectionDB</strong> option. As an option, you can also use <strong>/collectionName</strong> and <strong>/clone</strong> with this option. If you use the <strong>/attach</strong> option, the specified collection database will be added to your deployment of Azure DevOps Server.|
|create|Creates a collection.|
|detach|Required if neither <strong>/attach</strong> nor <strong>/delete</strong> is used. If you specify this option, you must also use the <strong>/collectionName</strong> option. If you use the <strong>/detach</strong> option, the database for the specified collection will be stopped, and the collection will be detached from your deployment of Azure DevOps Server.|
|delete|Required if neither <strong>/detach</strong> nor <strong>/attach</strong> is used. If you specify this option, you must also use the <strong>/collectionName</strong> option. If you use the <strong>/delete</strong> option, the database for the specified collection will be stopped, and the collection will be permanently detached from Azure DevOps Server. You will not be able to re-attach the collection database to this or any other deployment.|
|CollectionName|Specifies the name of the project collection. If the name of the collection contains spaces, you must enclose the name in quotation marks (for example, &quot;My Collection&quot;). Required if either <strong>/detach</strong> or <strong>/delete</strong> is used. If you use this option with <strong>/detach</strong> or <strong>/delete</strong>, it specifies the collection that will be detached or deleted. If you use this option with <strong>/attach</strong>, it specifies a new name for the collection. If you use this option with both <strong>/attach</strong> and <strong>/clone</strong>, it specifies the name for the duplicated collection.|
|CollectionDB|Required if <strong>/attach</strong> is used. This option specifies the name of the server that is running SQL Server and the name of the collection database that is hosted on that server.|
|ServerName|Specifies the name of the server that hosts the configuration database for Azure DevOps Server, and the name of the instance if you want to use an instance other than the default instance. If you specify an instance, you must use the format: `ServerName\InstanceName`.|
|DatabaseName|Specifies the name of the configuration database. By default, the name of this database is TFS_ConfigurationDB.|
|clone|If you specify this option, the original collection database will be attached as a clone in SQL Server, and this database will be attached to Azure DevOps Server. This option is primarily used as part of splitting a project collection.|

> [!TIP]
> The <strong>/delete</strong> option will not delete the collection database from SQL Server. After deleting the collection database from Azure DevOps Server, you can delete the database manually from SQL Server.

### Prerequisites

To use the **collections** command, you must be a member of the Team Foundation Administrators security group as well as the local Administrators group on the machine running **TfsConfig**. You must also be a member of the sysadmin security role for all instances of SQL Server used by Azure DevOps Server databases. If your deployment is integrated with SharePoint and you are using the **/delete** option, you must also be a member of the Farm Administrators group for the SharePoint farm from which you are deleting the site collection.

For more information, see [Permission reference for Azure DevOps Server](/azure/devops/security/permissions).

### Remarks

To manage collections interactively or to create a collection, you can use the Project Collections node in the administration console for Azure DevOps.
See [Manage project collections](https://msdn.microsoft.com/library/80848156-fa61-4f13-aea7-2bc47c59d9bf).

### Examples

The following example shows how to permanently remove the `Contoso Summer Intern Projects` project collection from a deployment of Azure DevOps Server.

```
TfsConfig collection /delete /CollectionName:"Contoso Summer Intern Projects"
```

```
TFSConfig - Team Foundation Server Configuration Tool
Copyright � Microsoft Corporation. All rights reserved.
Deleting a project collection is an irreversible operation. A deleted collection cannot be reattached to the same or another Team Foundation Server. Are you sure you want to delete 'Contoso Summer Intern Projects'? (Yes/No)
Yes
Found Collection 'Contoso Summer Intern Projects' Deleting...
The delete of collection 'Contoso Summer Intern Projects' succeeded.
```

The following example shows how to duplicate the `Contoso Summer Interns Projects` project collection, name it `Contoso Winter Interns Projects`, and attach the duplicate collection to the deployment of Azure DevOps Server.

```
TfsConfig collection /attach /collectiondb:"ContosoMain;TFS_Contoso Summer Interns Projects"
    /CollectionName:"Contoso Winter Intern Projects" /clone
```

::: moniker-end

::: moniker range="<= tfs-2018"

You can use the **Collection** command to attach, detach, or delete a project collection from a deployment of TFS.
You can also use the **Collection** command to duplicate the database of an existing collection, rename it, and attach it to the deployment.
This process is sometimes referred to as cloning a collection.
However, you cannot use the **Collection** command to create a project collection.

	TFSConfig Collection {/attach | /detach | /delete} [/collectionName:CollectionName]
		[/collectionDB:ServerName;DatabaseName] [/clone]

### Parameters

<table>
	<thead>
		<tr>
			<th>Option</th>
			<th>Description</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td><strong>/attach</strong></td>
			<td>
				Required if neither <strong>/detach</strong> nor <strong>/delete</strong> is used.
				If you specify this option, you must also use the <strong>/collectionDB</strong> option.
				As an option, you can also use <strong>/collectionName</strong> and <strong>/clone</strong> with this option.
				If you use the <strong>/attach</strong> option, the specified collection database will be added to your deployment of Azure DevOps Server.
			</td>
		</tr>
		<tr>
			<td><strong>/detach</strong></td>
			<td>
				Required if neither <strong>/attach</strong> nor <strong>/delete</strong> is used.
				If you specify this option, you must also use the <strong>/collectionName</strong> option.
				If you use the <strong>/detach</strong> option, the database for the specified collection will be stopped, and the collection will be detached from your deployment of Azure DevOps Server.
			</td>
		</tr>
		<tr>
			<td><strong>/delete</strong></td>
			<td>
				Required if neither <strong>/detach</strong> nor <strong>/attach</strong> is used.
				If you specify this option, you must also use the <strong>/collectionName</strong> option.
				If you use the <strong>/delete</strong> option, the database for the specified collection will be stopped, and the collection will be permanently detached from Azure DevOps Server.
				You will not be able to re-attach the collection database to this or any other deployment.<br /><br />
				<strong>Tip:</strong> The <strong>/delete</strong> option will not delete the collection database from SQL Server.
				After deleting the collection database from Azure DevOps Server, you can delete the database manually from SQL Server.
			</td>
		</tr>
		<tr>
			<td><strong>/CollectionName:</strong> CollectionName</td>
			<td>
				Specifies the name of the project collection. If the name of the collection contains spaces, you must enclose the name in quotation marks (for example, &quot;My Collection&quot;).
				Required if either <strong>/detach</strong> or <strong>/delete</strong> is used.
				If you use this option with <strong>/detach</strong> or <strong>/delete</strong>, it specifies the collection that will be detached or deleted.
				If you use this option with <strong>/attach</strong>, it specifies a new name for the collection.
				If you use this option with both <strong>/attach</strong> and <strong>/clone</strong>, it specifies the name for the duplicated collection.
			</td>
		</tr>
		<tr>
			<td><strong>/CollectionDB:</strong> ServerName;DatabaseName</td>
			<td>
				Required if <strong>/attach</strong> is used.
				This option specifies the name of the server that is running SQL Server and the name of the collection database that is hosted on that server.
				<ul>
					<li>
						<strong>ServerName</strong>: Specifies the name of the server that hosts the configuration database for Azure DevOps Server,
						and the name of the instance if you want to use an instance other than the default instance.
                        If you specify an instance, you must use the format: <code>ServerName\InstanceName</code>.
					</li>
					<li>
						<strong>DatabaseName</strong>: Specifies the name of the configuration database. By default, the name of this database is TFS_ConfigurationDB.
					</li>
				</ul>
			</td>
		</tr>
		<tr>
			<td><strong>/clone</strong></td>
			<td>
				If you specify this option, the original collection database will be attached as a clone in SQL Server,
				and this database will be attached to Azure DevOps Server. This option is primarily used as part of splitting a project collection.
			</td>
		</tr>
	</tbody>
</table>

### Prerequisites

To use the **Collections** command, you must be a member of the Team Foundation Administrators security group as well as the local Administrators group on the machine running **TFSConfig**. You must also be a member of the sysadmin security role for all instances of SQL Server used by Azure DevOps Server databases. If your deployment is integrated with SharePoint and you are using the **/delete** option, you must also be a member of the Farm Administrators group for the SharePoint farm from which you are deleting the site collection. 

For more information, see [Permission reference for Azure DevOps Server](/azure/devops/security/permissions).

### Remarks

To manage collections interactively or to create a collection, you can use the Project Collections node in the administration console for Azure DevOps.
See [Manage project collections](https://msdn.microsoft.com/library/80848156-fa61-4f13-aea7-2bc47c59d9bf).

### Examples

The following example shows how to permanently remove the "Contoso Summer Intern Projects" project collection from a deployment of Azure DevOps Server.

    TFSConfig Collection /delete /CollectionName:"Contoso Summer Intern Projects"

    TFSConfig - Team Foundation Server Configuration Tool
    Copyright � Microsoft Corporation. All rights reserved.
    Deleting a project collection is an irreversible operation. A deleted collection cannot be reattached to the same or another Team Foundation Server. Are you sure you want to delete 'Contoso Summer Intern Projects'? (Yes/No)
    Yes
    Found Collection 'Contoso Summer Intern Projects' Deleting...
    The delete of collection 'Contoso Summer Intern Projects' succeeded.

The following example shows how to duplicate the "Contoso Summer Interns Projects" project collection, name it "Contoso Winter Interns Projects," and attach the duplicate collection to the deployment of Azure DevOps Server.

    TFSConfig Collection /attach /collectiondb:"ContosoMain;TFS_Contoso Summer Interns Projects"
		/CollectionName:"Contoso Winter Intern Projects" /clone

::: moniker-end
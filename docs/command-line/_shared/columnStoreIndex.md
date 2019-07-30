---
ms.topic: include
---

> [!NOTE]
> Command availability: Requires TFS 2015.2 and later versions.

::: moniker range="azure-devops-2019"

You use the **columnStoreIndex** command to enable or disable column store indexes for the databases used by your Azure DevOps Server deployment.

```
TfsConfig columnStoreIndex /enabled:<true|false>
	/sqlInstance:<serverName>
	/databaseName:<databaseName>
```

|Option|Description|
|---|---|
|enabled|Specifies whether you are enabling or disabling column store index for the given SQL instance and database.|
|sqlInstance|Specifies the name of the server that hosts the database for which column store index is being enabled or disabled, and the name of the instance if an instance other than the default is used. If you specify an instance, you must use the format: `ServerName\InstanceName`.|
|databaseName|Specifies the name of the database for which column store index is being enabled or disabled.|

### Prerequisites

To use the **columnStoreIndex** command, you must be a member of the sysadmin role for the specified SQL Server instance.

### Remarks

You would typically use the **columnStoreIndex** command if you were moving a database from a SQL instance which supported column store index to one which did not.
In this case, you would need to disable all column store indexes before you could successfully move the databases.
Similarly, if you were moving a database back to a SQL instance which supported column store index you might wish to re-enable column store index in order to save space and gain performance.

### Example

The following example shows how to enable column store index, for a database named `TFS_DefaultCollection` on a SQL instance running on a server named `ContosoMain` on the named instance `TeamDatabases`.

```
TfsConfig columnStoreIndex /enabled:true /sqlInstance:ContosoMain\TeamDatabases /databaseName:TFS_DefaultCollection
```

::: moniker-end

::: moniker range="<= tfs-2018"

You use the **ColumnStoreIndex** command to enable or disable column store indexes for the databases used by your TFS deployment.

	TfsConfig columnStoreIndex /enabled:{true|false}
		/sqlInstance:ServerName
		/databaseName:DatabaseName

<table>
	<thead>
		<tr>
			<th>Option</th>
			<th>Description</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td><strong>/enabled</strong></td>
			<td>Specifies whether you are enabling or disabling column store index for the given SQL instance and database.</td>
		</tr>
		<tr>
			<td><strong>/sqlInstance</strong></td>
			<td>
				Specifies the name of the server that hosts the database for which column store index is being enabled or disabled,
				and the name of the instance if an instance other than the default is used.
                If you specify an instance, you must use the format: <code>ServerName\InstanceName</code>
			</td>
		</tr>
		<tr>
			<td><strong>/databaseName</strong></td>
			<td>Specifies the name of the database for which column store index is being enabled or disabled.</td>
		</tr>
	</tbody>
</table>

### Prerequisites

To use the **ColumnStoreIndex** command, you must be a member of the sysadmin role for the specified SQL Server instance.

### Remarks

You would typically use the **ColumnStoreIndex** command if you were moving a database from a SQL instance which supported column store index to one which did not.
In this case, you would need to disable all column store indexes before you could successfully move the databases.
Similarly, if you were moving a database back to a SQL instance which supported column store index you might wish to re-enable column store index in order to save space and gain performance. 

### Example

The following example shows how to enable column store index, for a database named TFS\_DefaultCollection on a SQL instance running on a server named "ContosoMain" on the named instance "TeamDatabases".

	TFSConfig columnStoreIndex /enabled:true /sqlInstance:ContosoMain\TeamDatabases /databaseName:TFS_DefaultCollection

::: moniker-end
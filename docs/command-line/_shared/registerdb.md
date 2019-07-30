---
ms.topic: include
---

::: moniker range="azure-devops-2019"

Use **registerDB** to update name of the server that hosts the configuration database in Azure DevOps Server.
You might use this command when restoring the configuration database to new hardware or when changing the domain of a deployment.

```
TfsConfig registerDB /sqlInstance:<serverName> /databaseName:<databaseName>
```

|Option|Description|
|---|---|
|SQLInstance|Required. Specifies the name of the server that is running SQL Server and the name of the instance if you want to use an instance other than the default instance. If you specify an instance, you must use the format: `ServerName\InstanceName`.|
|databaseName|Required. Specifies the name of the configuration database. By default, this is Tfs_Configuration.|

### Prerequisites

To use the **registerDB** command, you must be a member of the Azure DevOps Administrators group on the application-tier server for Azure DevOps and a member of the sysadmin group in SQL Server on the data-tier server for Azure DevOps.
For more information, see [Permission reference for Azure DevOps Server](/azure/devops/security/permissions).

### Remarks

Back up the databases for Azure DevOps Server before you use this command.

For the **registerDB** command to succeed, the following application pools and programs must be running:

- Azure DevOps Server Application Pool (application pool)
- ReportServer (application pool)
- SQL Server Reporting Services (program)

You must provide the exact name or address of the configuration database for this command to operate correctly.
If you must change the server on which this database is stored, you must ensure that Azure DevOps Server points to the new location.

### Example

The following example redirects Azure DevOps Server to a configuration database that is located on the server `ContosoMain` in the SQL Server instance `TeamDatabases`.

```
TfsConfig registerDB /SQLInstance:ContosoMain\TeamDatabases /databaseName:Tfs_Configuration
```

::: moniker-end

::: moniker range="<= tfs-2018"

Use **RegisterDB** to update name of the server that hosts the configuration database in Visual Studio Team Foundation Server (TFS).
You might use this command when restoring the configuration database to new hardware or when changing the domain of a deployment.

	TFSConfig RegisterDB /SQLInstance:ServerName /databaseName: DatabaseName [/usesqlalwayson]

<table>
	<thead>
		<tr>
			<th>Argument</th>
			<th>Description</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td><strong>/SQLInstance:</strong> ServerName</td>
			<td>
				Required. Specifies the name of the server that is running SQL Server and the name of the instance
				if you want to use an instance other than the default instance.
                If you specify an instance, you must use the format: <code>ServerName\InstanceName</code>.
			</td>
		</tr>
		<tr>
			<td><strong>/databaseName:</strong> DatabaseName</td>
			<td>Required. Specifies the name of the configuration database. By default, this is Tfs_Configuration.</td>
		</tr>
		<tr>
			<td><strong>/usesqlalwayson</strong></td>
			<td>
				Optional. Specifies that the databases are part of an AlwaysOn Availability Group in SQL Server.
				If configured, this option sets MultiSubnetFailover in the connection string.<br/><br/>
				For more information, see <a href="http://msdn.microsoft.com/library/hh510230.aspx">AlwaysOn Availability Groups (SQL Server)</a>.
			</td>
		</tr>
	</tbody>
</table>

### Prerequisites

To use the **RegisterDB** command, you must be a member of the Team Foundation Administrators group on the application-tier server
for Azure DevOps and a member of the sysadmin group in SQL Server on the data-tier server for Azure DevOps.
For more information, see [Permission reference for Azure DevOps Server](/azure/devops/security/permissions).

### Remarks

Back up the databases for Azure DevOps Server before you use this command.

For the RegisterDB command to succeed, the following application pools and programs must be running:

-   Azure DevOps Server Application Pool (application pool)
-   ReportServer (application pool)
-   SQL Server Reporting Services (program)

You must provide the exact name or address of the configuration database for this command to operate correctly.
If you must change the server on which this database is stored, you must ensure that Azure DevOps Server points to the new location.

### Example

The following example redirects Azure DevOps Server to a configuration database that is located on the server ContosoMain in the SQL Server instance TeamDatabases.

    TFSConfig RegisterDB /SQLInstance:ContosoMain\TeamDatabases /databaseName:Tfs_Configuration

::: moniker-end
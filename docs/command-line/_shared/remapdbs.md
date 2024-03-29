---
ms.topic: include
---

::: moniker range="azure-devops-2019"

The **remapDBs** command redirects Azure DevOps Server to its databases when they are stored on more than one server and you are restoring, moving, or otherwise changing the configuration of your deployment.
For example, you must redirect Azure DevOps Server to any databases for project collections if they are hosted on a separate server or servers from the configuration database.
You must also redirect Azure DevOps Server to the server or servers that are running SQL Server Analysis Services or SQL Server Reporting Services if those databases are hosted on a separate server or instance from the configuration database.

```
TfsConfig remapDBs /DatabaseName:ServerName;DatabaseName /SQLInstances:ServerName1,ServerName2
	[/AnalysisInstance:<serverName>] [/AnalysisDatabaseName:<databaseName>]
	[/preview] [/continue]
```

|Option|Description|
|---|---|
|DatabaseName|Specifies the name of the server that hosts the database that you want to map for Azure DevOps Server, in addition to the name of the database itself.|
|SQLInstances|Specifies the name of the server that is running SQL Server, in addition to the name of the instance if you want to use an instance other than the default instance.<br/><br/>If you are specifying more than one server, you must use a comma to separate multiple pairs of server and instance names.|
|AnalysisInstance|Optional. Specifies the name of the server and instance that hosts SQL Server Analysis Services. Use this option to specify the server and instance that hosts the Analysis Services database.|
|AnalysisDatabaseName|Optional. Specifies the name of the Analysis Services database that you want to use with Azure DevOps Server if you have more than one such database on the server that you specified with the <strong>/AnalysisInstance</strong> option.|
|preview|Optional. Displays the actions that you must take to update the configuration.|
|continue|Optional. Specifies that the <strong>RemapDB</strong> command should continue even if an error occurs during the attempt to locate one or more databases. If you use the <strong>/continue</strong> option, any collections whose databases are not found on the server or servers that you specify will be reconfigured to use the server and instance that hosts the configuration database.|

### Prerequisites

To use the **remapDBs** command, you must be a member of the Azure DevOps Administrators security group and a member of the sysadmin security group for any SQL Server databases that Azure DevOps Server uses. For more information, see [Permission reference for Azure DevOps Server](/azure/devops/security/permissions).

### Remarks

You use the **remapDBs** command to reconfigure Azure DevOps Server to use different servers and instances of SQL Server from the servers and instances in the original installation.

### Example

The following example shows how to redirect Azure DevOps Server to its configuration database `TFS_Configuration`.
This database is hosted on `ContosoMain` on the named instance `TeamDatabases`.
Its project collection databases are stored on both `ContosoMain\TeamDatabases` and the default instance on `Contoso2`.

```
TfsConfig remapDBs /DatabaseName:ContosoMain\TeamDatabases;TFS_Configuration
	/SQLInstances:ContosoMain\TeamDatabases,Contoso2
```

::: moniker-end

::: moniker range="<= tfs-2018"

The **RemapDBs** command redirects Azure DevOps Server to its databases when they are stored on more than one server and you are restoring, moving, or otherwise changing the configuration of your deployment.
For example, you must redirect TFS to any databases for project collections if they are hosted on a separate server or servers from the configuration database.
You must also redirect TFS to the server or servers that are running SQL Server Analysis Services or SQL Server Reporting Services if those databases are hosted on a separate server or instance from the configuration database.

	TFSConfig RemapDBs /DatabaseName:ServerName;DatabaseName /SQLInstances:ServerName1,ServerName2
		[/AnalysisInstance:ServerName] [/AnalysisDatabaseName:DatabaseName]
		[/preview] [/continue] [/usesqlalwayson]

<table>
	<thead>
		<tr>
			<th>Option</th>
			<th>Description</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td><strong>/DatabaseName</strong></td>
			<td>Specifies the name of the server that hosts the database that you want to map for Azure DevOps Server, in addition to the name of the database itself.</td>
		</tr>
		<tr>
			<td><strong>/SQLInstances:</strong> ServerName1,ServerName2</td>
			<td>
				Specifies the name of the server that is running SQL Server,
				in addition to the name of the instance if you want to use an instance other than the default instance.<br/><br/>
				If you are specifying more than one server, you must use a comma to separate multiple pairs of server and instance names.
			</td>
		</tr>
		<tr>
			<td><strong>/AnalysisInstance:</strong> ServerName</td>
			<td>
				Optional. Specifies the name of the server and instance that hosts SQL Server Analysis Services.
				Use this option to specify the server and instance that hosts the Analysis Services database.
			</td>
		</tr>
		<tr>
			<td><strong>/AnalysisDatabaseName:</strong> DatabaseName</td>
			<td>
				Optional. Specifies the name of the Analysis Services database that you want to use
				with Azure DevOps Server if you have more than one such database on the server that you specified with the <strong>/AnalysisInstance</strong> option.
			</td>
		</tr>
		<tr>
			<td><strong>/preview</strong></td>
			<td>Optional. Displays the actions that you must take to update the configuration.</td>
		</tr>
		<tr>
			<td><strong>/continue</strong></td>
			<td>
				Optional. Specifies that the <strong>RemapDB</strong> command should continue even if an error occurs during the attempt to locate one or more databases.
				If you use the <strong>/continue</strong> option, any collections whose databases are not found on the server or servers that you specify
				will be reconfigured to use the server and instance that hosts the configuration database.
			</td>
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

To use the **RemapDBs** command, you must be a member of the Team Foundation Administrators security group and a member of the sysadmin security group for any SQL Server databases that Azure DevOps Server uses. For more information, see [Permission reference for Azure DevOps Server](/azure/devops/security/permissions).

### Remarks

You use the **RemapDBs** command to reconfigure Azure DevOps Server to use different servers and instances of SQL Server from the servers and instances in the original installation.

### Example

The following example shows how to redirect Azure DevOps Server to its configuration database TFS\_Configuration.
This database is hosted on ContosoMain on the named instance TeamDatabases.
Its project collection databases are stored on both ContosoMain\\TeamDatabases and the default instance on Contoso2.

    TFSConfig RemapDBs /DatabaseName:ContosoMain\TeamDatabases;TFS_Configuration
		/SQLInstances:ContosoMain\TeamDatabases,Contoso2

::: moniker-end
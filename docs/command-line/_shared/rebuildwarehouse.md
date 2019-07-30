---
ms.topic: include
---

::: moniker range="azure-devops-2019"

You can use the **rebuildWarehouse** command to rebuild the SQL Server Reporting Services and SQL Server Analysis Services databases that Azure DevOps Server uses.

```
TfsConfig rebuildWarehouse /analysisServices | /all [/ReportingDataSourcePassword:Password]
```

|Option|Description|
|---|---|
|analysisServices|Required if <strong>/all</strong> is not used. Specifies that only the database for Analysis Services will be rebuilt. If no database exists for Analysis Services, you must also use the <strong>/reportingDataSourcePassword</strong> option.
|all|Required if <strong>/analysisServices</strong> is not used. Specifies that all reporting and analysis databases that Azure DevOps Server uses will be rebuilt.
|reportingDataSourcePassword|Required if the TFS_Analysis database does not exist. Specifies the password of the account that is used as the data sources account for SQL Server Reporting Services (TFSReports). For more information, see <a href="https://msdn.microsoft.com/library/cf314289-96ef-4f70-9c2b-a130d7287442">Service accounts and dependencies in Azure DevOps Server</a>.|

### Prerequisites

To use the **rebuildWarehouse** command, you must be a member of the following groups:

- The Azure DevOps Administrators security group and the Administrators security group on the server or servers that are running the administration console for Azure DevOps

- The sysadmin group on the server or servers that are running the instance of SQL Server that hosts the databases for Azure DevOps Server

For more information, see [Permission reference for Azure DevOps Server](/azure/devops/security/permissions).

### Remarks

You might use this command when moving or splitting a project collection, restoring data, or otherwise changing the configuration of your deployment.

To start the rebuild of these databases interactively, you can use the Reporting node in the administration console for Azure DevOps. For more information, see [Open the Azure DevOps Administration Console](https://msdn.microsoft.com/library/d4e7d06b-fd68-43d1-8baf-ce31c8989a02).

### Example

The following example shows how to rebuild the Analysis Services database for a deployment of Azure DevOps Server.

```
TfsConfig rebuildWarehouse /analysisServices

    TFSConfig - Team Foundation Server Configuration Tool
    Copyright � Microsoft Corporation. All rights reserved.
    The Analysis Services database was successfully rebuilt.
```

::: moniker-end

::: moniker range="<= tfs-2018"

You can use the **RebuildWarehouse** command to rebuild the SQL Server Reporting Services and SQL Server Analysis Services databases that Visual Studio Team Foundation Server (TFS) uses.

	TFSConfig RebuildWarehouse /analysisServices | /all [/ReportingDataSourcePassword:Password]

<table>
	<thead>
		<tr>
			<th>Option</th>
			<th>Description</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td><strong>/analysisServices</strong></td>
			<td>
				Required if <strong>/all</strong> is not used.
				Specifies that only the database for Analysis Services will be rebuilt.
				If no database exists for Analysis Services, you must also use the <strong>/reportingDataSourcePassword</strong> option.
			</td>
		</tr>
		<tr>
			<td><strong>/all</strong></td>
			<td>
				Required if <strong>/analysisServices</strong> is not used.
				Specifies that all reporting and analysis databases that Azure DevOps Server uses will be rebuilt.
			</td>
		</tr>
		<tr>
			<td><strong>/reportingDataSourcePassword:</strong> Password</td>
			<td>
				Required if the TFS_Analysis database does not exist.
				Specifies the password of the account that is used as the data sources account for SQL Server Reporting Services (TFSReports).
				For more information, see <a href="https://msdn.microsoft.com/library/cf314289-96ef-4f70-9c2b-a130d7287442">Service accounts and dependencies in Azure DevOps Server</a>.
			</td>
		</tr>
	</tbody>
</table>

### Prerequisites

To use the **RebuildWarehouse** command, you must be a member of the following groups:

-   the Team Foundation Administrators security group and the Administrators security group on the server or servers that are running the administration console for Azure DevOps

-   the sysadmin group on the server or servers that are running the instance of SQL Server that hosts the databases for Azure DevOps Server

For more information, see [Permission reference for Azure DevOps Server](/azure/devops/security/permissions).

### Remarks

You might use this command when moving or splitting a project collection, restoring data, or otherwise changing the configuration of your deployment.

To start the rebuild of these databases interactively, you can use the Reporting node in the administration console for Azure DevOps. For more information, see [Open the Azure DevOps Administration Console](https://msdn.microsoft.com/library/d4e7d06b-fd68-43d1-8baf-ce31c8989a02)>.

### Example

The following example shows how to rebuild the Analysis Services database for a deployment of Azure DevOps Server.

    TFSConfig RebuildWarehouse /analysisServices

    TFSConfig - Team Foundation Server Configuration Tool
    Copyright � Microsoft Corporation. All rights reserved.
    The Analysis Services database was successfully rebuilt.

::: moniker-end
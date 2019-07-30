---
ms.topic: include
---

::: moniker range="azure-devops-2019"

<a id="license"></a>
### License

You can use the **License** command to display, modify, or extend the licensing key for your deployment of Azure DevOps Server.

```
TFSConfig License [/ProductKey:Key] [/extend [NewTrialID]]
```

<table>
	<thead>
		<tr>
			<th>Option</th>
			<th>Description</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td><strong>/ProductKey:</strong> Key</td>
			<td>Specifies that the license key for the deployment will be updated with the value of Key.</td>
		</tr>
		<tr>
			<td><strong>/extend</strong></td>
			<td>
				Specifies that the trial licensing period for Azure DevOps Server will be extended by 30 days.
				This option can be used only once without a getting a new trial ID.
				If a second extension is required, you must obtain a second trial license from Microsoft.
			</td>
		</tr>
	</tbody>
</table>

### Prerequisites

To use the **License** command, you must be a member of the Azure DevOps Administrators security group. For more information, see [Permission reference for Azure DevOps Server](/azure/devops/security/permissions).

### Remarks

To view, modify, or change the licensing for your deployment interactively, you can use the administration console for Azure DevOps.
For more information, see [Open the Azure DevOps Administration Console](https://msdn.microsoft.com/library/d4e7d06b-fd68-43d1-8baf-ce31c8989a02) and [Locate or Change the Product Key for Azure DevOps Server](https://msdn.microsoft.com/library/64f29927-b520-4c9f-b633-bcb527e562cd).

### Examples

The following example shows how to view the licensing information for a deployment of Azure DevOps Server. In this example, the deployment is using a trial license.

```
TFSConfig License

    TFSConfig - Team Foundation Server Configuration Tool
    Copyright © Microsoft Corporation. All rights reserved.
    Team Foundation Server Standard license
    The following features are installed:
    Team Foundation Server
    Build Services
    Build: 21106.00
    Product ID: 01234-567-8910
    Trial license with 74 days remaining, expiring on 6/30/2010
    Trial ID: ABCD-EFGH-IJKL
```

<a id="tcm"></a>
### TCM

When upgrading to the latest version of Azure DevOps Server, the system automatically attempts to upgrade the Tests Management components, including test plans and suites.
If the automatic migration fails, use the **TCM** command to upgrade your test plans and test suites manually to their respective work item types (WITs).

```
TFSConfig TCM /upgradeTestPlans|upgradeStatus /CollectionName:CollectionName /TeamProject:TeamProjectName
```

<table>
	<thead>
		<tr>
			<th>Option</th>
			<th>Description</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td><strong>/upgradeTestPlans</strong></td>
			<td>
				Required unless <strong>/upgradeStatus</strong> is used.<br/><br/>
				Converts existing test plan and test suites to point to the work item-based test plans and test suites.
				It also updates existing test management data and links between other existing test artifacts such as test points, test runs, and test results.
			</td>
		</tr>
		<tr>
			<td><strong>/upgradeStatus</strong></td>
			<td>
				Required unless <strong>/upgradeTestPlans</strong> is used.<br/><br/>
				Reports the migration status of test data for the specified project.
				It will also indicate whether the specified project has any test plans.
			</td>
		</tr>
		<tr>
			<td><strong>/CollectionName</strong>:CollectionName</td>
			<td>
				Required. Specifies the project collection that contains the project for which you want to migrate test data or check the migration status.<br/><br/>
				If there are spaces in the name of the project collection, enclose the name in quotation marks, for example, &quot;Fabrikam Fiber Collection&quot;.
			</td>
		</tr>
		<tr>
			<td><strong>/TeamProjectName</strong>:TeamProjectName</td>
			<td>
				Required. Specifies the project for which you want to migrate test data or check the migration status.
				This project must be defined in the collection that you specified by using the <strong>/collectionName</strong> parameter.
				<br/><br/>If there are spaces in the name of the project, enclose the name in quotation marks, for example, &quot;My Project&quot;.
			</td>
		</tr>
	</tbody>
</table>

### Prerequisites

You must be a member of the Azure DevOps Administrators security group, and an administrator on the application-tier server.
See [Set administrator permissions for Azure DevOps Server](https://msdn.microsoft.com/library/ed578715-f4d2-4042-b797-5f97abde9973).

### Remarks

Your application-tier server must be upgraded to the latest version of Azure DevOps Server to use this command.

Before you can use the TCM command, you must first import the test plan work item definition and the test plan category into the project.
To learn more about the migration and when to use this command, see [Manual updates to support test management](https://msdn.microsoft.com/library/edbe689d-7863-4273-916f-b7e93b7f00b3).

The TCM command is applied to individual projects. If you need to upgrade test plans in more than one project, you will have to run it against each project individually.

You must run the **TCM** command from the tools directory for Azure DevOps Server. By default, that location is: `drive:\%programfiles%\TFS 12.0\Tools`.

You use the **TCM** command only in the event that automatic migration of existing test data fails.
To learn more about the migration and when to use this command, [Manual updates to support test management](https://msdn.microsoft.com/library/edbe689d-7863-4273-916f-b7e93b7f00b3).

If you can't access test plans or test suites that were defined before the server upgrade occurred, run **TFSConfig TCM upgradeStatus** to determine the status of the migration.

You run the **TCM** command for an individual project. If you need to upgrade more than one project, you will have to run it against each project in turn.

### Examples

The following example shows how to check the status of test plan upgrade on the Fabrikam Fiber project hosted on the default project collection (DefaultCollection):

```
tfsconfig tcm /upgradeStatus /CollectionName:DefaultCollection /TeamProject:"Fabrikam Fiber"
```

<a id="import"></a>
### Import

The import command was deprecated in TFS 2013. Earlier versions are available here:

- [TFS 2012](https://msdn.microsoft.com/library/ff407080%28v=vs.110%29.aspx)
- [TFS 2010](https://msdn.microsoft.com/library/ff407080%28v=vs.100%29.aspx)

If you need assistance with upgrading data and projects from an earlier version of Azure DevOps Server, see [Upgrade Azure DevOps Server](https://msdn.microsoft.com/library/f4cde7d5-4021-4b21-b9b8-ba6e51572243), or contact [Microsoft Support](http://support.microsoft.com/ph/1117).

<a id="preparesql"></a>
### PrepareSQL

The prepareSQL command was depracated in TFS 2012. Earlier versions are available here:

- [TFS 2010](https://msdn.microsoft.com/library/ee349267%28v=vs.100%29.aspx)

<a id="repair"></a>
### Repair

The repair command was depracated in TFS 2012. Earlier versions are available here:

- [TFS 2010](https://msdn.microsoft.com/library/ee349268%28v=vs.100%29.aspx)

If you need to repair your stored procedures after a failed database patch, contact [Microsoft Support](http://support.microsoft.com/ph/1117).

<a id="diagnose"></a>
### Diagnose

The diagnose command was deprecated in TFS 2013. Earlier versions are available here:

- [TFS 2012](https://msdn.microsoft.com/library/ff407076%28v=vs.110%29.aspx)
- [TFS 2010](https://msdn.microsoft.com/library/ff407076%28v=vs.100%29.aspx)

If you need assistance with diagnosing potential mismatches between software updates on your application-tier and data-tier servers for Azure DevOps Server, contact [Developer Community support](https://developercommunity.visualstudio.com/spaces/21/index.html).

<a id="updates"></a>
### Updates

The updates command was deprecated in TFS 2013.Earlier versions are available here:

- [TFS 2012](https://msdn.microsoft.com/library/ff407078%28v=vs.110%29.aspx)
- [TFS 2012](https://msdn.microsoft.com/library/ff407078%28v=vs.100%29.aspx)

If you need assistance with installing any software updates that are missing from the databases for Azure DevOps Server, contact [Microsoft Support](http://support.microsoft.com/ph/1117).

<a id="prepareclone"></a>
### PrepareClone

The PrepareClone command was deprecated in TFS 2017.

The **PrepareClone** command removes information about scheduled backups, SharePoint, and reporting resources from a Azure DevOps Server deployment.
This command is used in two circumstances:
- when you move a deployment to new hardware but want to keep using the old deployment
- when you clone a Azure DevOps Server deployment

In either of these cases it is critical to run this command.
If you don't, the original resources will be used by both the original and the new servers.
If both the original and the new servers are live and point to the same SharePoint or reporting resources for any amount of time, you could end up with corrupted databases.

> [!IMPORTANT]
> This command should be run before configuration, whether you move or clone Azure DevOps Server.
> If you run it after configuration, you could end up with inconsistencies between content in your databases and content in your web.config file.
> These inconsistencies might take your server offline.
> If you have already configured your moved or cloned Azure DevOps Server deployment and realize you need to run the command, follow these steps.
> First, quiesce your server. Next, run PrepareClone command, ChangeServerID command, and then RemapDBs command. Finally, unquiesce your server.

```
TFSConfig PrepareClone /SQLInstance:ServerName /DatabaseName:TFSConfigurationDatabaseName
		[/notificationURL: TFSURL] [/usesqlalwayson]
```

<table>
	<thead>
		<tr>
			<th>Option</th>
			<th>What it does</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td><strong>/DatabaseName</strong></td>
			<td>Specifies the name of the server that hosts the database that you want to map for Azure DevOps Server, in addition to the name of the configuration database itself.</td>
		</tr>
		<tr>
			<td><strong>/SQLInstance:</strong> ServerName</td>
			<td>
				Specifies the name of the server that you want to map as a server that hosts one or more databases for Azure DevOps Server.
				If an instance other than the default instance hosts a database, you must also specify the name of the instance.
                Use this format: ServerName <strong>&lt;/strong&gt; InstanceName.
			</td>
		</tr>
		<tr>
			<td><strong>/NotificationURL:</strong> TFSURL</td>
			<td>Optional. Specifies The notification URL for the application-tier server.</td>
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

To use the **PrepareClone** command, you must be a member of the Azure DevOps Administrators security group and a member of the sysadmin security group for any SQL Server databases that Azure DevOps Server uses.
For more information, see [Permission reference for Azure DevOps Server](/azure/devops/security/permissions).

### Remarks

You use the **PrepareClone** command to reconfigure Azure DevOps Server when you move the original installation to new hardware and want to continue to use the original deployment Azure DevOps Server and hardware, or when you want to clone your Azure DevOps Server deployment for testing purposes. You use TFSConfig PrepareClone in conjunction with TFSConfig RemapDBs and TFSConfig ChangeServerID to support the cloning configuration.

### Example

The following example shows how to use the command on a moved Azure DevOps Server named NewFabrikamTFS to remove old backup, reporting, and SharePoint resource information. If this information isn't removed, the original deployment of Azure DevOps Server still uses those same resources and databases become corrupt. In the example, the SQL Server supporting the moved Azure DevOps Server is also named NewFabrikamTFS, and the instance is the default instance, so no specific instance information is required, just the server name.

```
TFSConfig PrepareClone /SQLInstance:NewFabrikamTFS /DatabaseName:TFS_Configuration
```

::: moniker-end

::: moniker range="<= tfs-2018"

<a id="license"></a>

### License

You can use the **License** command to display, modify, or extend the licensing key for your deployment of Azure DevOps Server.

	TFSConfig License [/ProductKey:Key] [/extend [NewTrialID]]

<table>
	<thead>
		<tr>
			<th>Option</th>
			<th>Description</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td><strong>/ProductKey:</strong> Key</td>
			<td>Specifies that the license key for the deployment will be updated with the value of Key.</td>
		</tr>
		<tr>
			<td><strong>/extend</strong></td>
			<td>
				Specifies that the trial licensing period for Azure DevOps Server will be extended by 30 days.
				This option can be used only once without a getting a new trial ID.
				If a second extension is required, you must obtain a second trial license from Microsoft.
			</td>
		</tr>
	</tbody>
</table>

### Prerequisites

To use the **License** command, you must be a member of the Team Foundation Administrators security group. For more information, see [Permission reference for Azure DevOps Server](/azure/devops/security/permissions).

### Remarks

To view, modify, or change the licensing for your deployment interactively, you can use the administration console for Azure DevOps.
For more information, see [Open the Azure DevOps Administration Console](https://msdn.microsoft.com/library/d4e7d06b-fd68-43d1-8baf-ce31c8989a02) and [Locate or Change the Product Key for Azure DevOps Server](https://msdn.microsoft.com/library/64f29927-b520-4c9f-b633-bcb527e562cd).

### Examples

The following example shows how to view the licensing information for a deployment of Azure DevOps Server. In this example, the deployment is using a trial license.

    TFSConfig License

    TFSConfig - Team Foundation Server Configuration Tool
    Copyright © Microsoft Corporation. All rights reserved.
    Team Foundation Server Standard license
    The following features are installed:
    Team Foundation Server
    Build Services
    Build: 21106.00
    Product ID: 01234-567-8910
    Trial license with 74 days remaining, expiring on 6/30/2010
    Trial ID: ABCD-EFGH-IJKL

::: moniker-end

::: moniker range="<=  tfs-2015"

	TFSConfig TCM /upgradeTestPlans|upgradeStatus /CollectionName:CollectionName /TeamProject:TeamProjectName

<table>
	<thead>
		<tr>
			<th>Option</th>
			<th>Description</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td><strong>/upgradeTestPlans</strong></td>
			<td>
				Required unless <strong>/upgradeStatus</strong> is used.<br/><br/>
				Converts existing test plan and test suites to point to the work item-based test plans and test suites.
				It also updates existing test management data and links
				between other existing test artifacts such as test points, test runs, and test results.
			</td>
		</tr>
		<tr>
			<td><strong>/upgradeStatus</strong></td>
			<td>
				Required unless <strong>/upgradeTestPlans</strong> is used.<br/><br/>
				Reports the migration status of test data for the specified project.
				It will also indicate whether the specified project has any test plans.
			</td>
		</tr>
		<tr>
			<td><strong>/CollectionName</strong>:CollectionName</td>
			<td>
				Required. Specifies the project collection that contains the project
				for which you want to migrate test data or check the migration status.<br/><br/>
				If there are spaces in the name of the project collection,
				enclose the name in quotation marks, for example, &quot;Fabrikam Fiber Collection&quot;.
			</td>
		</tr>
		<tr>
			<td><strong>/TeamProjectName</strong>:TeamProjectName</td>
			<td>
				Required. Specifies the project for which you want to migrate test data or check the migration status.
				This project must be defined in the collection that you specified by using the <strong>/collectionName</strong> parameter.
				<br/><br/>If there are spaces in the name of the project, enclose the name in quotation marks, for example, &quot;My Project&quot;.
			</td>
		</tr>
	</tbody>
</table>

### Prerequisites

You must be a member of the Team Foundation Administrators security group, and an administrator on the application-tier server.
See [Set administrator permissions for Team Foundation Server](https://msdn.microsoft.com/library/ed578715-f4d2-4042-b797-5f97abde9973).

### Remarks

Your application-tier server must be upgraded to the latest version of TFS to use this command.

Before you can use the TCM command, you must first import the test plan work item definition and the test plan category into the project.
To learn more about the migration and when to use this command, see [Manual updates to support test management](https://msdn.microsoft.com/library/edbe689d-7863-4273-916f-b7e93b7f00b3).

The TCM command is applied to individual projects. If you need to upgrade test plans in more than one project, you will have to run it against each project individually.

You must run the **TCM** command from the tools directory for TFS. By default, that location is: `drive:\%programfiles%\TFS 12.0\Tools`.

You use the **TCM** command only in the event that automatic migration of existing test data fails.
To learn more about the migration and when to use this command, [Manual updates to support test management](https://msdn.microsoft.com/library/edbe689d-7863-4273-916f-b7e93b7f00b3).

If you can't access test plans or test suites that were defined before the server upgrade occurred, run **TFSConfig TCM upgradeStatus** to determine the status of the migration.

You run the **TCM** command for an individual project. If you need to upgrade more than one project, you will have to run it against each project in turn.

### Examples

The following example shows how to check the status of test plan upgrade on the Fabrikam Fiber project hosted on the default project collection (DefaultCollection):

    tfsconfig tcm /upgradeStatus /CollectionName:DefaultCollection /TeamProject:"Fabrikam Fiber"

<a id="import"></a>

### Import

The import command was deprecated in TFS 2013. Earlier versions are available here:

- [TFS 2012](https://msdn.microsoft.com/library/ff407080%28v=vs.110%29.aspx)
- [TFS 2010](https://msdn.microsoft.com/library/ff407080%28v=vs.100%29.aspx)

If you need assistance with upgrading data and projects from an earlier version of Azure DevOps Server,
see [Upgrade Azure DevOps Server](https://msdn.microsoft.com/library/f4cde7d5-4021-4b21-b9b8-ba6e51572243),
or contact [Microsoft Support](http://support.microsoft.com/ph/1117).

<a id="preparesql"></a>

### PrepareSQL

The prepareSQL command was depracated in TFS 2012. Earlier versions are available here:

- [TFS 2010](https://msdn.microsoft.com/library/ee349267%28v=vs.100%29.aspx)

<a id="repair"></a>

### Repair

The repair command was depracated in TFS 2012. Earlier versions are available here:

- [TFS 2010](https://msdn.microsoft.com/library/ee349268%28v=vs.100%29.aspx)

If you need to repair your stored procedures after a failed database patch, contact [Microsoft Support](http://support.microsoft.com/ph/1117).

<a id="diagnose"></a>

### Diagnose

The diagnose command was deprecated in TFS 2013. Earlier versions are available here:

- [TFS 2012](https://msdn.microsoft.com/library/ff407076%28v=vs.110%29.aspx)
- [TFS 2010](https://msdn.microsoft.com/library/ff407076%28v=vs.100%29.aspx)

If you need assistance with diagnosing potential mismatches between software updates on your application-tier and data-tier servers for Azure DevOps Server,
contact [Developer Community support](https://developercommunity.visualstudio.com/spaces/21/index.html).

<a id="updates"></a>

### Updates

The updates command was deprecated in TFS 2013. Earlier versions are available here:

- [TFS 2012](https://msdn.microsoft.com/library/ff407078%28v=vs.110%29.aspx)
- [TFS 2012](https://msdn.microsoft.com/library/ff407078%28v=vs.100%29.aspx)

If you need assistance with installing any software updates that are missing from the databases for Azure DevOps Server,
contact [Microsoft Support](http://support.microsoft.com/ph/1117).

<a id="prepareclone"></a>

### PrepareClone

The PrepareClone command was deprecated in TFS 2017. 

>**Command availability:** TFS 2015 and TFS 2013

The **PrepareClone** command removes information about scheduled backups, SharePoint,
and reporting resources from a Azure DevOps Server deployment.
This command is used in two circumstances:
- when you move a deployment to new hardware but want to keep using the old deployment
- when you clone a Azure DevOps Server deployment

In either of these cases it is critical to run this command.
If you don't, the original resources will be used by both the original and the new servers.
If both the original and the new servers are live and point to the same SharePoint or reporting resources for any amount of time,
you could end up with corrupted databases.

>**Important:**  
>This command should be run before configuration, whether you move or clone Azure DevOps Server.
>If you run it after configuration,
>you could end up with inconsistencies between content in your databases and content in your web.config file.
>These inconsistencies might take your server offline.
>If you have already configured your moved or cloned Azure DevOps Server deployment and realize you need to run the command, follow these steps.
>First, quiesce your server. Next, run PrepareClone command, ChangeServerID command, and then RemapDBs command. Finally, unquiesce your server.

    TFSConfig PrepareClone /SQLInstance:ServerName /DatabaseName:TFSConfigurationDatabaseName
		[/notificationURL: TFSURL] [/usesqlalwayson]

<table>
	<thead>
		<tr>
			<th>Option</th>
			<th>What it does</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td><strong>/DatabaseName</strong></td>
			<td>Specifies the name of the server that hosts the database that you want to map for Azure DevOps Server, in addition to the name of the configuration database itself.</td>
		</tr>
		<tr>
			<td><strong>/SQLInstance:</strong> ServerName</td>
			<td>
				Specifies the name of the server that you want to map as a server that hosts one or more databases for Azure DevOps Server.
				If an instance other than the default instance hosts a database, you must also specify the name of the instance.
                Use this format: ServerName <strong>&lt;/strong&gt; InstanceName.
			</td>
		</tr>
		<tr>
			<td><strong>/NotificationURL:</strong> TFSURL</td>
			<td>Optional. Specifies The notification URL for the application-tier server.</td>
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

To use the **PrepareClone** command, you must be a member of the Team Foundation Administrators security group
and a member of the sysadmin security group for any SQL Server databases that Azure DevOps Server uses.
For more information, see [Permission reference for Azure DevOps Server](/azure/devops/security/permissions).

### Remarks

You use the **PrepareClone** command to reconfigure Azure DevOps Server when you move the original installation to new hardware and want to continue to use the original deployment Azure DevOps Server and hardware, or when you want to clone your Azure DevOps Server deployment for testing purposes. You use TFSConfig PrepareClone in conjunction with TFSConfig RemapDBs and TFSConfig ChangeServerID to support the cloning configuration.

### Example

The following example shows how to use the command on a moved Azure DevOps Server named NewFabrikamTFS to remove old backup, reporting, and SharePoint resource information. If this information isn't removed, the original deployment of Azure DevOps Server still uses those same resources and databases become corrupt. In the example, the SQL Server supporting the moved Azure DevOps Server is also named NewFabrikamTFS, and the instance is the default instance, so no specific instance information is required, just the server name.

    TFSConfig PrepareClone /SQLInstance:NewFabrikamTFS /DatabaseName:TFS_Configuration

::: moniker-end
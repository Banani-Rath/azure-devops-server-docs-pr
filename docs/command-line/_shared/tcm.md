---
ms.topic: include
---

::: moniker range="azure-devops-2019"

<a id="tcm"></a>

When upgrading to the latest version of Azure DevOps Server, the system automatically attempts to upgrade the Test Management components, including test plans and suites.
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

You must be a member of the Team Foundation Administrators security group, and an administrator on the application-tier server.
See [Set administrator permissions for Azure DevOps Server](https://msdn.microsoft.com/library/ed578715-f4d2-4042-b797-5f97abde9973).

### Remarks

Your application-tier server must be upgraded to the latest version of Azure DevOps Server 2019 to use this command.

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

::: moniker-end

::: moniker range="<= tfs-2018"

<a id="tcm"></a>


When upgrading to the latest version of Azure DevOps Server, the system automatically attempts to upgrade the Tests Management components, including test plans and suites.
If the automatic migration fails, use the **TCM** command to upgrade your test plans and test suites manually to their respective work item types (WITs).

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

    tfsconfig tcm /upgradeStatus /CollectionName:DefaultCollection /TeamProject:"Fabrikam Fiber"

::: moniker-end

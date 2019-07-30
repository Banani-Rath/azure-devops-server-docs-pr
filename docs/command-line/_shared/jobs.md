---
ms.topic: include
---

::: moniker range="azure-devops-2019"

You can use the **jobs** command to create a log file that provides the details of the most recent job activity for a specific project collection, or to retry a job for one or all project collections.

```
TfsConfig jobs /retry|dumplog [/CollectionName:<collectionName>] [/CollectionId:<id>]
```

|Option|Description|
|---|---|
|retry|Required if <strong>/dumplog</strong> is not used. Specifies that the most recent job will be reattempted for the specified project collection. If you use this option, you must also use either the <strong>/CollectionName</strong> or the <strong>/CollectionID</strong> option.|
|dumplog|Required if <strong>/retry</strong> is not used. Specifies that the most recent job activity for the collection will be sent to a log file. If you use this option, you must also use either the <strong>/CollectionName</strong> or <strong>/CollectionID</strong> option.|
|CollectionName|Required if <strong>/CollectionID</strong> is not used. Specifies the name of the collection for which the most recent job will be either retried (<strong>/retry</strong>) or logged (<strong>/dumplog</strong>). If you want to specify all collections, you can use an asterisk (*).|
|CollectionID|Required if <strong>/CollectionName</strong> is not used. Specifies the identification number of the collection for which the most recent job will be either retried (<strong>/retry</strong>) or logged (<strong>/dumplog</strong>).|

### Prerequisites

To use the **jobs** command, you must be a member of the Azure DevOps Administrators security group. For more information, see [Permission reference for Azure DevOps Server](/azure/devops/security/permissions).

### Remarks

To retry a job interactively, you can open the administration console for Azure DevOps, select the **Status** tab for the collection, and then select **Retry Job**.
For more information, see [Open the Azure DevOps Administration Console](https://msdn.microsoft.com/library/d4e7d06b-fd68-43d1-8baf-ce31c8989a02).

### Example

The following example shows how to create a log file that lists the most recent job activity for the `Contoso Summer Intern Projects` project collection in Azure DevOps Server.

```
TfsConfig jobs /dumplog /CollectionName:"Contoso Summer Intern Projects"
```

::: moniker-end

::: moniker range="<= tfs-2018"

You can use the **Jobs** command to create a log file that provides the details of the most recent job activity for a specific project collection,
or to retry a job for one or all project collections.

	TFSConfig Jobs /retry|dumplog [/CollectionName:CollectionName] [/CollectionID:ID]

<table>
	<thead>
		<tr>
			<th>Option</th>
			<th>Description</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td><strong>/retry</strong></td>
			<td>Required if <strong>/dumplog</strong> is not used. Specifies that the most recent job will be reattempted for the specified project collection. If you use this option, you must also use either the <strong>/CollectionName</strong> or the <strong>/CollectionID</strong> option.</td>
		</tr>
		<tr>
			<td><strong>/dumplog</strong></td>
			<td>Required if <strong>/retry</strong> is not used. Specifies that the most recent job activity for the collection will be sent to a log file. If you use this option, you must also use either the <strong>/CollectionName</strong> or <strong>/CollectionID</strong> option.</td>
		</tr>
		<tr>
			<td><strong>/CollectionName:</strong> CollectionName</td>
			<td>Required if <strong>/CollectionID</strong> is not used. Specifies the name of the collection for which the most recent job will be either retried (<strong>/retry</strong>) or logged (<strong>/dumplog</strong>). If you want to specify all collections, you can use an asterisk (*).</td>
		</tr>
		<tr>
			<td><strong>/CollectionID:</strong> ID</td>
			<td>Required if <strong>/CollectionName</strong> is not used. Specifies the identification number of the collection for which the most recent job will be either retried (<strong>/retry</strong>) or logged (<strong>/dumplog</strong>).</td>
		</tr>
	</tbody>
</table>

### Prerequisites

To use the **Jobs** command, you must be a member of the Team Foundation Administrators security group. For more information, see [Permission reference for Azure DevOps Server](/azure/devops/security/permissions).

### Remarks

To retry a job interactively, you can open the administration console for Azure DevOps, click the Status tab for the collection, and then click Retry Job.
For more information, see [Open the Azure DevOps Administration Console](https://msdn.microsoft.com/library/d4e7d06b-fd68-43d1-8baf-ce31c8989a02).

### Example

The following example shows how to create a log file that lists the most recent job activity for the "Contoso Summer Intern Projects" project collection in Azure DevOps Server.

    TFSConfig Jobs /dumplog /CollectionName:"Contoso Summer Intern Projects"

::: moniker-end
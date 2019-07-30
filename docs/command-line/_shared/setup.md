---
ms.topic: include
---

You use the **setup** command to uninstall features which are currently configured on the machine where you run the command.

```
TfsConfig setup /uninstall:<feature[,feature,...]>
```

::: moniker range="azure-devops-2019"

|Option|Description|
|---|---|
|uninstall|Specifies one or more features to be uninstalled from the machine where you run the command. Options include: All, ApplicationTier, Search, and VersionControlProxy.|

::: moniker-end

::: moniker range="tfs-2018"

<table>
	<thead>
		<tr>
			<th>Option</th>
			<th>Description</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td><strong>/uninstall</strong></td>
			<td>
				Specifies one or more features to be uninstalled from the machine where you run the command.
				Options include: All, ApplicationTier, SharePointExtensions, Search, TeamBuild, and VersionControlProxy.
			</td>
		</tr>
	</tbody>
</table>

::: moniker-end

::: moniker range="<= tfs-2017"

<table>
	<thead>
		<tr>
			<th>Option</th>
			<th>Description</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td><strong>/uninstall</strong></td>
			<td>
				Specifies one or more features to be uninstalled from the machine where you run the command.
				Options include: All, ApplicationTier, SharePointExtensions, TeamBuild, VersionControlProxy.
			</td>
		</tr>
	</tbody>
</table>

::: moniker-end

### Prerequisites

To use the **setup** command, you must be a member of the Azure DevOps Administrators security group.

### Examples

The following example uninstalls all Azure DevOps Server features from the current machine.

```
TfsConfig setup /uninstall:ALL
```

The following example uninstalls the application tier and build features from the current machine.

```
TfsConfig setup /uninstall:ApplicationTier,TeamBuild
```
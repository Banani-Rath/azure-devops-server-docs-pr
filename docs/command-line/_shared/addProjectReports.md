---
ms.topic: include
---

<a id="add-project-reports">  </a>

> [!NOTE]
> The **addProjectReports** command is available with TFS 2017.1 and later versions.

::: moniker range="azure-devops-2019"

You use the **addProjectReports** command to add or overwrite reports for an existing team project.  

```
TfsConfig addProjectReports /collection:<teamProjectCollectionUrl> /teamProject:<projectName> /template:<templateName>
    [/force]
```

|Option|Description|
|---|---|
|collection|Required. URL of Team Project Collection.|
|teamproject|Required. Specifies the name of the team project.|
|template|Required. Specifies the name of the process template. Available options are Agile, CMMI and Scrum.|
|force|Optional. Specifies that reports should be overwritten if they already exist.|

### Prerequisites

To use the **addProjectReports** command, you must have permissions to run **TFSConfig** and to [upload reports to the Reporting Service](/azure/devops/report/admin/grant-permissions-to-reports).

### Remarks

You use the **addProjectReports** command when your project does not have reports or you want to update the reports defined for a process.

You may need to use this command when:

- The project was created in the Azure DevOps portal and not from Visual Studio
- The project was created from Visual Studio, however reporting was not configured in Azure DevOps Server.

If you would like to overwrite reports in your project with default reports because you upgraded Azure DevOps Server and old reports in your project are no longer compatible, use the **/force** option. If you have customized reports, please make a backup before doing this.

To learn more about adding reports to an on-premises Azure DevOps Server, see [Add reports to a project](/azure/devops/report/admin/add-reports-to-a-team-project).

### Example

The following example shows how to add Agile reports to `MyProject` project in `http://myTfsServer:8080/tfs/DefaultCollection` project collection.

```
TFSConfig addProjectReports /collection:http://myTfsServer:8080/tfs/DefaultCollection /teamproject:MyProject /template:Agile
```

::: moniker-end

::: moniker range="<= tfs-2018"

You use the **AddProjectReports** command to add or overwrite reports for an existing project.

	TfsConfig addProjectReports
		/collection:teamProjectCollectionUrl
		/teamProject:projectName
		/template:templateName
		[/force]

<table>
	<thead>
		<tr>
			<th>Option</th>
			<th>Description</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td><strong>/collection</strong></td>
			<td>Required. URL of Project Collection.</td>
		</tr>
		<tr>
			<td><strong>/teamProject</strong></td>
			<td>Required. Specifies the name of the project.</td>
		</tr>
		<tr>
			<td><strong>/template</strong></td>
			<td>Required. Specifies the name of the process template. Available options are Agile, CMMI and Scrum</td>
		</tr>
		<tr>
			<td><strong>/force</strong></td>
			<td>Optional. Specifies that reports should be overwritten if they already exist.</td>
		</tr>
	</tbody>
</table>

### Prerequisites

To use the **AddProjectReports** command, you must have permissions to run **TFSConfig** and to [upload reports to the Reporting Service](/azure/devops/report/admin/grant-permissions-to-reports). 

### Remarks

You use the **AddProjectReports** command when your project does not have reports or you want to update the reports defined for a process. 

You may need to use this command when:
-   the project was created in the web portal and not from Visual Studio
-   the project was created from Visual Studio, however reporting was not configured in Azure DevOps Server.

If you would like to overwrite reports in your project with default reports because you upgraded Azure DevOps Server and old reports in your project are no longer compatible, use the **/force** option. If you have customized reports, please make a backup before doing this. 

To learn more about adding reports to an on-premises Azure DevOps Server, see [Add reports to a project](/azure/devops/report/admin/add-reports-to-a-team-project).

### Example

The following example shows how to add Agile reports to *MyProject* project in http://myTfsServer:8080/tfs/DefaultCollection project collection.
	
	TFSConfig addprojectreports /collection:http://myTfsServer:8080/tfs/DefaultCollection /teamproject:MyProject /template:Agile

::: moniker-end
---
ms.topic: include
---

::: moniker range="<= tfs-2015"

Use the **CreateTeamProjectLibraryShare** command to assign a library share from a project collection to an individual project in the collection. A library share provides access to file-based resources for virtual environments such as ISO images and virtual hard disks.
Library shares are created in System Center Virtual Machine Manager (SCVMM) and assigned to project collection by Visual Studio Lab Management. Use separate **CreateTeamProjectLibraryShare** commands to assign multiple library shares to a project.

> [!NOTE]
> You can automatically assign a library share to all projects in a team project collection by using the [TFSConfig Lab /LibraryShare Commands](../tfsconfig-cmd.md#lab-libraryshare) and [How to: Change the Library Share for Your Project Collections](https://msdn.microsoft.com/library/dd386363(v=vs.120).aspx).

#### Prerequisites

To use the **CreateTeamProjectLibraryShare** command, you must have **Manage Lab Locations** permission at the Project Collection Library Share level. By default, members of the Azure DevOps Server Administrators and Project Collection Administrators groups have this permission. For more information, see [Permission reference for Azure DevOps Server](/azure/devops/security/permissions).

```
TFSLabConfig CreateTeamProjectLibraryShare
    Collection:collectionUrl
    /TeamProject:{* |teamProjectName}
    /TeamProjectCollectionLibraryShare:{* |teamProjectCollectionLibraryShareName} 
    /Name:teamProjectLibraryShareName
        [/Description:teamProjectLibraryShareDescription]
        [/NoPrompt]
```

### Parameters

|Option|Description|
|---|---|
|**Collection**:*collectionUrl*|Required. The URL of the project collection on the application tier of Azure DevOps Server that contains the project. For example, `/collection:http://abc:8080/TFS/DefaultCollection`.|
|**TeamProject:**{ * &#124; *teamProjectName*}|Required. The name of the project. Use quotation marks if there are spaces in the name. Use an asterisk (*) to assign the specified host group to all projects in the collection.|
|**TeamProjectCollectionLibraryShare:**{ * &#124; *teamProjectCollectionHostShareName*}|
|**Name:** *teamProjectHostShareName*|Required. The name to assign to the library share in the project.|
|**Description:** *teamProjectHostGroupDescription* |Optional. A description of the project library share.|
|**NoPrompt**|Optional. Do not prompt the user for confirmation.|

### Example

For increased readability in the example, command options are listed on separate lines. In a command prompt window, type all options for a command on the same line.

In the first example, all the library shares in the project collection are assigned to each of the projects in the collection.
In the second example, one library share in the project collection is assigned to a specific project.

```
TFSLabConfig CreateTeamProjectLibraryShare
    /collection:http://abc:8080/TFS/Collection0
    /TeamProject:*
    /TeamProjectCollectionLibraryShare:*
```

```
TFSLabConfig CreateTeamProjectLibraryShare
    /collection:http://abc:8080/TFS/Collection0
    /TeamProject:Project1
    /TeamProjectCollectionLibraryShare:tpcls1
    /name:ls1
```

::: moniker-end
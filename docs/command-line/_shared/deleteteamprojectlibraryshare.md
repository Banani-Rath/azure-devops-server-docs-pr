---
ms.topic: include
---

::: moniker range="<= tfs-2015"

Use the **DeleteTeamProjectLibraryShare** command to remove the assignment of a library share from an individual project. A library share provides access to file-based resources for virtual environments such as ISO images and virtual hard disks., Library shares are created by System Center Virtual Machine Manager (SCVMM). In Visual Studio Lab Management, library shares are assigned to one or more project collections and then to one or more projects in the collections.
The **DeleteTeamProjectLibraryShare** command does not remove the assignment of the library share to the project collection.

#### Prerequisites

To use the **DeleteTeamProjectLibraryShare** command, you must have **Delete Lab Locations** permission for that Project Library Share.
By default, members of the Team Foundation Server Administrators, Project Collection Administrators and Project Administrators groups have this permission. For more information, see [Permission reference for Azure DevOps Server](/azure/devops/security/permissions).

```
TFSLabConfig DeleteTeamProjectLibraryShare
    Collection:collectionUrl
          /TeamProject:{* |teamProjectName}
          /Name:{* |teamProjectLibraryShareName}
          [/NoPrompt]
```

### Parameters

|Option|Description|
|---|---|
|**Collection**:*collectionUrl*|Required. The URL of the project collection on the application tier of Azure DevOps Server that contains the project. For example, `/collection:http://abc:8080/TFS/DefaultCollection`. |
|**TeamProject:**{ * &#124; *teamProjectName*}|Required. The name of the project that contains the library share that you want to delete. Use quotation marks if there are spaces in the name. Use an asterisk (*) to specify all projects in the project collection.|
|**Name:** *teamProjectHostGroupName* |Required. The name of the library share to delete from a project. Use quotation marks if there are spaces in the name. Use an asterisk (*) to specify all library shares of the project.|
|**NoPrompt**| Optional. Do not prompt the user for confirmation.|

### Example

For increased readability in the example, command options are listed on separate lines. In a command prompt window, type all options for a command on the same line.

In the first example, all the library shares assigned to each of the project in the project collection are removed. In the second example, one library share is removed from a specific project.

```
TFSLabConfig DeleteTeamProjectLibraryShare
    /collection:http://abc:8080/TFS/DefaultCollection
    /teamProject:*
    /name:*
```

```
TFSLabConfig DeleteTeamProjectLibraryShare
    /collection:http://abc:8080/TFS/DefaultCollection
    /teamProject:Project1
    /name:ls1
```

::: moniker-end
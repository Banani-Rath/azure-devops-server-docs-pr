---
ms.topic: include
---

::: moniker range="<= tfs-2015"

Use the **ListTeamProjectHostGroups** command to list the *host groups* that are assigned to a project and that you have read access to.

#### Prerequisites

To use the ListTeamProjectHostGroups command, you must have **View Lab Resources** permissions at the Project level. By default, members of the Team Foundation Server Administrators, Project Collection Administrators, Project Administrators, Project Contributors, and Project Readers groups have this permission. For more information, see [Permission reference for Azure DevOps Server](/azure/devops/security/permissions).

```
TFSLabConfig ListTeamProjectHostGroups
    Collection:collectionUrl
          /TeamProject:teamProjectName
```

### Parameters

|Option|Description|
|---|---|
|**Collection**:*collectionUrl*|Required. The URL of the project collection on the application tier of Azure DevOps Server that contains the project. For example, `/collection:http://abc:8080/TFS/DefaultCollection`.|
|**TeamProject:** *teamProjectName*|Required. The name of the project. Use quotation marks if there are spaces in the name.|

### Example

For increased readability in the example, command options are listed on separate lines. In a command prompt window, type all options for a command on the same line.

```
TFSLabConfig ListTeamProjectHostGroups
    /collection:http://abc:8080/TFS/DefaultCollection
    /teamProject:Project1
```

::: moniker-end
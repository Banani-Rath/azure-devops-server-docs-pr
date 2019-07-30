---
ms.topic: include
---

::: moniker range="<= tfs-2015"

Use the **ListTeamProjectLibraryShares** command to list all *library shares* that are assigned to a team project and that you have access to.

#### Prerequisites

To use the ListTeamProjectLibraryShares command, you must have the **View Lab Resources** permission at Project level. By default, members of the Azure DevOps Administrators, Project Collection Administrators, Project Administrators, Project Contributors, and Project Readers groups have this permission. For more information, see [Permission reference for Azure DevOps Server](/azure/devops/security/permissions).

```
TFSLabConfig ListTeamProjectLibraryShares
    Collection:collectionUrl
     /TeamProject:teamProjectName
```

### Parameters

|Option|Description|
|---|---|
|**Collection**:*collectionUrl*|Required. The URL of the project collection on the application tier of Azure DevOps Server that contains the project. For example, `/collection:http://abc:8080/TFS/DefaultCollection`.|
|**TeamProject:**  *teamProjectName*|Required. The name of the project. Use quotation marks if there are spaces in the name.|

::: moniker-end
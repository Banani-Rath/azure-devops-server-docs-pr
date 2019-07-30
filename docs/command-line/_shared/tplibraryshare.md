---
ms.topic: include
---

::: moniker range="<= tfs-2015"

> ![NOTE]
> These commands only work on SCVMM 2012 server, and are not supported on SCVMM 2008 R2 server.

Use the **TPLibraryShare** command to assign or unassign a library share from a project collection to an individual project in the collection. A library share provides access to file-based resources for virtual environments such as ISO images and virtual hard disks. Library shares are created in System Center Virtual Machine Manager (SCVMM) and assigned to project collection by Visual Studio Lab Management.

To run these commands, you must be a member of Project Collection Administrators group in Azure DevOps Server for the collection you specify. In addition, you must be a member of Administrator or Delegated Administrator role in the SCVMM Server from which you are adding the host groups.

```
TfsLabConfig TPLibraryShare
      /collection:collectionUrl
      /teamProject:* | teamProjectName
          [/add 
                /teamProjectCollectionLibraryShare:* | teamProjectCollectionLibraryShare
                /name:teamProjectLibraryShareName
                [/noprompt]]
          [/delete 
                /name:* | teamProjectLibraryShareName
                [/noprompt]]
          [/list]
```

### Parameters

|Option|Description|
|---|---|
|**Collection**:*collectionUrl*|Required. Specifies the URL of the project collection on the application-tier of the Azure DevOps Server.|
|**add**|Assigns the specified library share to the project.|
|**teamProjectCollectionLibraryShare**: *teamProjectCollectionLibraryShare*|The name of the project collection library share.|
|**name**: *libraryShareName*|The name of the library share.|
|**Delete**|Removes the specified library share from the project collection.|
|**noPrompt**|Suppresses display progress and result data from the command window.|
|**list**|Lists all library shares that are assigned to the specified project collection.|

::: moniker-end
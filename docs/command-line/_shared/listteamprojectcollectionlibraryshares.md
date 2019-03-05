---
ms.topic: include
---

Use the **ListTeamProjectCollectionLibraryShares** command to list the
library shares that have been assigned to a project collection and
that you have read access to. Library shares are created in System
Center Virtual Machine Manager (SCVMM). and are assigned to a team
project collection by using the [TFSConfig Lab /LibraryShare Commands](lab-libraryshare.md). 
Project collection library shares can be added to a project by
using the **CreateTeamProjectLibraryShare** command. For more
information, see [TFSLabConfig CreateTeamProjectLibraryShare Command](createteamprojectlibraryshare.md).

**Required Permissions:**

To use the **ListTeamProjectCollectionLibraryShares** command, you must
have **View Lab Resources** permission at the Project collection
level. By default, members of the TFS Administrators and Project
Collection Administrators groups have this permission. For more
information, see [Permission reference for Team Foundation Server](/azure/devops/security/permissions).


    TFSLabConfig ListTeamProjectCollectionLibraryShares
    Collection:collectionUrl


### Parameter


| Option | Description |
| --- | --- |
| **Collection**:*collectionUrl* | Required. The URL of the project collection on the application tier of Team Foundation Server that contains the project. For example, ```/collection:http://abc:8080/TFS/DefaultCollection```.  |



### Example

For increased readability in the example, command options are listed on
separate lines. In a command prompt window, type all options for a
command on the same line.


    TFSLabConfig ListTeamProjectCollectionLibraryShares
        /collection:http://abc:8080/TFS/Collection0


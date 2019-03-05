---
ms.topic: include
---

Use the **DeleteTeamProjectHostGroup** command to remove the assignment
of a host group from an individual project. Host groups specify one
or more physical machines that are the deployment targets for virtual
environments in Visual Studio Lab Management.

Host groups are created in System Center Virtual Machine Manager
(SCVMM). In Lab Management, host groups are assigned to one or more team
project collections and then to one or more projects in the
collections. The **DeleteTeamProjectHostGroup** command does not remove
the assignment of the host group to the project collection.

**Required Permissions:**

To use the **DeleteTeamProjectHostGroup** command, you must have Delete
Lab Locations permission for the Project host group. By default,
Team Foundation Server Administrators, Project Collection
Administrators and Project Administrators have this permission. For
more information, see [Permission reference for Team Foundation Server](/azure/devops/security/permissions).

    TFSLabConfig DeleteTeamProjectHostGroup
          /Collection:collectionUrl
          /TeamProject:{* |teamProjectName>}
          /Name:{* |teamProjectHostGroupName}
          [/NoPrompt]


### Parameters

| Option | Description |
| --- | --- |
| **Collection**:*collectionUrl* | Required. The URL of the project collection on the application tier of Team Foundation Server that contains the project. For example, ```/collection:http://abc:8080/TFS/DefaultCollection```.  |
| **TeamProject:**{ * &#124; *teamProjectName*} | Required. The name of the project from which you want to remove the host group. Use quotation marks if there are spaces in the name. Use an asterisk (*) to specify all projects in the project collection. |
| **Name:** *teamProjectHostGroupName* | Required. The name of the host group to delete from a project. Use quotation marks if there are spaces in the name. Use an asterisk (*) to specify all host groups in the project. |
| **NoPrompt** | Optional. Do not prompt the user for confirmation. |


### Example 

For increased readability in the example, command options are listed on
separate lines. In a command prompt window, type all options for a
command on the same line.

In the first example, all the host groups assigned to each of the team
project in the project collection are removed. In the second
example, one host group is removed from a specific project.


    REM First example
    TFSLabConfig DeleteTeamProjectLibraryShare
        /collection:http://abc:8080/TFS/DefaultCollection
        /teamProject:*
        /name:*

    REM Second example
    TFSLabConfig DeleteTeamProjectLibraryShare
        /collection:http://abc:8080/TFS/DefaultCollection
        /teamProject:Project1
        /name:hg1


---
ms.topic: include
---

> **Note:**
> These commands only work on SCVMM 2012 server, and are not supported on
> SCVMM 2008 R2 server.

Use the **TPHostGroup** command to assign or unassign a host group from
a project collection to individual projects in the collection.
Host groups specify one or more physical machines that are the
deployment targets for virtual environments in Visual Studio Lab
Management..

To run these commands, you must be a member of Project Collection
Administrators group in Team Foundation Server for the collection you
specify. In addition, you must be a member of Administrator or Delegated
Administrator role in the SCVMM Server from which you are adding the
host groups.

    TfsLabConfig TPHostGroup 
          /collection:collectionUrl
          /teamProject:* | teamProjectName
          [/add 
                /teamProjectCollectionHostGroup:* | teamProjecctCollectionHostGroupFQDN
                /name:teamProjectHostGroupName
                [/description:description]
                [/NoPrompt]]
          [/delete 
                /name:* | teamProjectHostGroupName
                [/noprompt]]
          [/list]


### Parameters


| Option | Description |
| --- | --- |
| **Collection**:*collectionUrl* | Required. Specifies the URL of the project collection on the application-tier of the Team Foundation Server.  |
| **teamProject**: * &#124; *teamProjectName* | The name of the project to which to add or delete host groups. Use quotation marks if there are spaces in the name. Use an asterisk (* ) to assign the specified host group to all projects in the collection. |
| **add** | Adds the specified host group to the projects. |
| **teamProjectCollectionHostGroup**: *teamProjectCollectionHostGroup* | The name of the host group in the project collection. Use quotation marks if there are spaces in the name. Use an asterisk (*) to assign all host groups in the collection to the specified project. |
| **name**: *hostGroupName* | Tthe name of the host group in the project collection. |
| **Delete** | Removes the host group from the project. |
| **noPrompt** | Suppresses display progress and result data from the command window. |
| **list** | Lists all host groups that are assigned to the specified project. |


### Example

In this example, all the host groups in the project collection are
assigned to all the projects in the collection:


    TFSLabConfig TPHostGroup /add
          /collection:http://abc:8080/TFS/Collection0
          /teamProject:*
          /teamProjectCollectionHostGroup:NORTHAMERICA\hostgroup1
          /name:HostGroup1

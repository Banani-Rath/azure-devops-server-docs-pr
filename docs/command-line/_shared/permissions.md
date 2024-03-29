---
ms.topic: include
---

::: moniker range="<= tfs-2015"

Use the **TFSLabConfig Permissions** command to set and get permissions set for a specified user or for multiple users on a specified object in Visual Studio Lab Management. For more information about individual permissions, see the Lab Management Permissions section of [Permission reference for Azure DevOps Server](/azure/devops/security/permissions).

#### Prerequisites

To query permissions on an object, you must have Read permissions for the object. To change permissions on an object the **Permissions** command, you must have the **Manage Permissions** permission. By default, the creator of the object has this permission. For more information, see [Permission reference for Azure DevOps Server](/azure/devops/security/permissions).

```
TFSLabConfig Permissions
    /Collection:collectionUrl
          [objectSpec]
          {[/User:userName1[,userName2][,...]]
          [/Group:groupName1[,groupName2][,...]]}
          [/Allow:{* |perm1[,perm2][,...] }] 
          [/Deny:{* |perm1[,perm2][,...]}]
          [/Remove:{* |perm1[,perm2][,...]}]
          [/Inherit:Yes|No]
```

### Parameters

|Option|Description|
|---|---|
|**Collection**:*collectionUrl*|Required. The URL of the project collection on the application tier of Azure DevOps Server that contains the project. For example, `/collection:http://abc:8080/TFS/DefaultCollection`.|
|*objectSpec*|Optional. Specifies the target object such as a project or library share to which the permissions are applied. For information about how to specify objects, see objectSpec below.|
|**User**: *userName1[,userName2][,...]*|Optional. Specifies one or more users to which the permissions are applied. Use commas to separate multiple user names.|
|**Group**: *groupName1[,groupName2][,...]*|Optional. Specifies one or more groups to which the permissions are applied. Use commas to separate multiple group names.|
|**Allow**: {\* &#124; *perm1*[,*perm2*][,...] }|Optional. Enables the specified permissions for the specified users or groups. Use an asterisk (*) to specify all permissions. To specify an individual permission, use the identifiers in the \*\*Name at command line*\* column of the table in the Lab Management Permissions section of [Permission reference for Azure DevOps Server](/azure/devops/security/permissions). Use commas to separate multiple permissions.|
|**Deny**:{\* &#124; *perm1*[,*perm2*][,...] }| Optional. Denies the specified permissions for the specified users or groups. Use an asterisk (*) to specify all permissions. To specify an individual permission, use the identifiers in the \*\*Name at command line*\* column of the table in the Lab Management Permissions section of [Permission reference for Azure DevOps Server](/azure/devops/security/permissions). Use commas to separate multiple permissions.|
|**Remove**:{\* &#124; *perm1*[,*perm2*][,...] }|Optional. Unsets the specified permissions that were previously granted or denied to the user or group. To specify an individual permission, use the identifiers in the **Name at command line** column of the table in the Lab Management Permissions section of [Permission reference for Azure DevOps Server](/azure/devops/security/permissions). Use commas to separate multiple permissions.|
|**Inherit:Yes &#124; No**|Optional. If you specify **yes**, all permissions associated with a parent ACL are inherited by an item. Cannot be combined with the /**remove**, /**user**, or /**group** options.|

### objectSpec

You can specify the objects that you want to include in the **TFSLabConfig Permissions** command in two ways:

- Use one or more locations options to specify the object in the Lab
    Management hierarchy.

- Use the **/Url** option to specify the object as a Uri.

If the *objectSpec* parameter option is not specified, the permissions are applied to all objects in the team project collection.

#### Object type options

The following table lists the valid combination of options that you can
use to specify an object as the *objectSpec* parameter of a **TFSLabConfig
permissions** command.

|To set permissions on|Use these options|
|---|---|
|A specific host group in a project collection|**/TeamProjectCollectionHostGroup**: *teamProjectCollectionHostGroupName* |
|A specific library share in a project collection|**/TeamProjectCollectionLibraryShare**: *teamProjectCollectionLibraryShareName*|
|All group hosts in a project|**/TeamProject**: *projectName* **/TeamProjectHostGroup**: *|
|A group host in a project|**/TeamProject**: *projectName* **/TeamProjectHostGroup**:*teamProjectHostGroupName*|
|A lab environment in a host group for a project|**/TeamProject**: *projectName*  **/TeamProjectHostGroup**: *teamProjectHostGroupName* **/LabEnvironment**:*labEnvironmentName*|
|All library shares in a project|**/TeamProject**: *projectName* **/TeamProjectLibraryShare**: *|
|A library share in a project|**/TeamProject**: *projectName* **/TeamProjectLibraryShare**:*teamProjectLibraryShareName*|
|A lab template in a library share of a project|**/TeamProject**: *projectName*  **/TeamProjectLibraryShare**: *teamProjectLibraryShareName*  **/LabTemplate**: *labTemplateName*|
|A lab environment in a library share of a project|**/TeamProject**: *projectName*  **/TeamProjectLibraryShare**: *teamProjectLibraryShareName*  **/LabEnvironment**: *labEnvironmentName*|

#### URL

Use the following syntax to specify the *objectSpec* target object of a **TFSLabConfig permissions** command by using the **/Url** option:

**/url:VSTFS:///LabManagement/**
*objectType* **/**
*objectId*

The objectId is the unique numeric identifier of the object.

The following table lists the valid keywords for the *objectType* keyword:

|Object Type|Description|
|---|---|
|**TeamProjectCollectionHostGroup**|A host group of a project collection|
|**TeamProjectCollectionLibraryShare**|A library share of a project collection|
|**TeamProject**|A project|
|**TeamProjectHostGroup**|A host group of a project|
|**TeamProjectLibraryShare**|A library share of a project|
|**LabTemplate**|A virtual machine or template in a project library share|
|**LabEnvironment**|An environment that is deployed on a project host group or stored in a project library share.|

### Prerequisites

You can specify one or more Lab Management permissions as the target of the **/Allow**, **/Deny**, or **/Remove** options. For a lists of available permissions, see the **Lab Management Permissions** section of the <span>[Permission reference for Azure DevOps Server](https://msdn.microsoft.com/library/ms252587(v=vs.120).aspx)</span> topic.

- Use an asterisk (\*) to specify all lab permissions.

- Use commas to separate multiple permissions.

### Remarks

If neither the **/User** or **/Group** option is specified, the current permissions of the specified object is displayed.

If the *objectSpec* parameter option is not specified, the permissions are applied to all objects in the team project collection.

::: moniker-end
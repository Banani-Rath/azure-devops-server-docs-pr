---
title: Change groups and permissions with TFSSecurity
titleSuffix: Azure DevOps Server 
description: Change groups and permissions in Azure DevOps Services from the command-line using TFSSecurity
ms.prod: devops-server
ms.technology: tfs-admin
ms.manager: jillfra
ms.author: aaronha
author: aaronhallberg
ms.topic: conceptual
monikerRange: '<= azure-devops'
ms.date: 05/30/2019
--- 

# Use TFSSecurity to manage groups and permissions for Azure DevOps 

[!INCLUDE [temp](../_shared/version-azure-devops-all-versions.md)]


You can use the **TFSSecurity** command-line tool to create, modify, and delete groups and users in Azure DevOps Server, previously named Visual Studio Team Foundation Server (TFS), and additionally modify permissions for groups and users. For information about how to perform these tasks in the user interface, see [Add users or groups to a project](/azure/devops/organizations/security/add-users-team-project).

[!INCLUDE [temp](_shared/tools-location.md)]


> [!NOTE]
> Even if you are logged on with administrative credentials,
> you must open an elevated Command Prompt to perform this function.


## Use with Azure DevOps Services

The **TFSSecurity** command-line tool can be used with Azure DevOps Services as well. To use it for Azure DevOps Services, use the same commands as documented, but replace the *CollectionURL* with your *AccountURL* (*ServerURL* is not applicable with Azure DevOps Services). To access the **TFSSecurity** command, you must [install Azure DevOps Server Express](../upgrade/express.md). 



### Example:

```
tfssecurity /a+ Namespace Token Action Identity (ALLOW | DENY)[/collection:AccountURL]
```

While **TFSSecurity** is supported, we recommend using our [Security REST API](/rest/api/vsts/security/) when working with security groups and permissions in Azure DevOps Services as our APIs are updated faster and more often.

## Permissions 

<a id="aplus"></a>

### /a+: Add permissions

Use **/a+** to add permissions for a user or a group in a server-level, collection-level, or project-level group. To add users to groups from the user interface, see [Manage users or groups](https://msdn.microsoft.com/library/30493f4c-d3e6-42f0-bca2-2ad749246944).

```
tfssecurity /a+ Namespace Token Action Identity (ALLOW | DENY)[/collection:CollectionURL] [/server:ServerURL]
```

#### Prerequisites

To use the **/a+** command, you must have the View collection-level information or the View instance-level information permission set to Allow, depending on whether you are using the **/collection** or **/server** parameter, respectively. If you are changing permissions for a project, you must also have the Edit project-level information permission for the project set to Allow. For more information, see [Permission reference for Team Foundation Server](/azure/devops/security/permissions).

#### Parameters

| Argument | Description |
| --- | --- |
| Namespace | The namespace that contains the group to which you want to add permissions for a user or group. You can also use the **tfssecurity /a** command to view a list of namespaces at the server, collection, and project level. |
| Identity | The identity of the user or the group. For more information about identity specifiers, see [TFSSecurity Identity and Output Specifiers](#specifiers).<br><ul><li>**ALLOW**<br>The group or user can perform the operation that the Action specifies.</li><li>**DENY**<br>The group or user cannot perform the operation that the Action specifies.</li></ul> |
| **/collection** :CollectionURL | Required if **/server** is not used. Specifies the URL of a project collection in the following format: **http://** ServerName **:** Port **/** VirtualDirectoryName **/** CollectionName |
| **/server** :ServerURL | Required if **/collection** is not used. Specifies the URL of an application-tier server in the following format: **http://** ServerName **:** Port **/** VirtualDirectoryName |

#### Remarks

Run this command on an application-tier server for Azure DevOps.

Access control entries are security mechanisms that determine which operations a user, group, service, or computer is authorized to perform.

#### Examples

The following example displays what namespaces are available at the server level for the application-tier server that is named ADatumCorporation.

> [!NOTE]
> The examples are for illustration only and are fictitious. No real association is intended or inferred.

```
tfssecurity /a /server:ServerURL 
```

Sample output:

```
    TFSSecurity - Team Foundation Server Security Tool
    Copyright (c) Microsoft Corporation.  All rights reserved.

    The target Team Foundation Server is http://ADatumCorporation:8080/.

    The following security namespaces are available to have permissions set on them:

         Registry
         Identity
         Job
         Server
         CollectionManagement
         Warehouse
         Catalog
         EventSubscription
         Lab

    Done.
```

The following example displays what actions are available for the Server namespace at the collection level.

```
tfssecurity /a Server /collection:CollectionURL 
```

Sample output:

    TFSSecurity - Team Foundation Server Security Tool
    Copyright (c) Microsoft Corporation.  All rights reserved.

    The target Team Foundation Server is http://ADatumCorporation:8080/.

    The following actions are available in the security namespace Server:
        GenericRead
        GenericWrite
        Impersonate
        TriggerEvent

    Done.

The following example grants the server-level "View instance-level information" permission to the ADatumCorporation deployment for the Datum1 domain user John Peoples (Datum1\\jpeoples).

     tfssecurity /a+ Server FrameworkGlobalSecurity GenericRead n:Datum1\jpeoples ALLOW /server:http://ADatumCorporation:8080 

Sample output:

    TFSSecurity - Team Foundation Server Security Tool
    Copyright (c) Microsoft Corporation.  All rights reserved.

    The target Team Foundation Server is http://ADatumCorporation:8080/.
    Resolving identity "n:Datum1\jpeoples"...
      [U] Datum1\jpeoples (John Peoples)
    Adding the access control entry...
    Verifying...

    Effective ACL on object "FrameworkGlobalSecurity":
      [+] GenericRead                        [INSTANCE]\Team Foundation Valid Users
      [+] GenericRead                        [INSTANCE]\SharePoint Web Application Services
      [+] Impersonate                        [INSTANCE]\SharePoint Web Application Services
      [+] GenericRead                        [INSTANCE]\Team Foundation Service Accounts
      [+] GenericWrite                       [INSTANCE]\Team Foundation Service Accounts
      [+] Impersonate                        [INSTANCE]\Team Foundation Service Accounts
      [+] TriggerEvent                       [INSTANCE]\Team Foundation Service Accounts
      [+] GenericRead                        [INSTANCE]\Team Foundation Administrators
      [+] GenericWrite                       [INSTANCE]\Team Foundation Administrators
      [+] TriggerEvent                       [INSTANCE]\Team Foundation Administrators
      [+] GenericRead                        DATUM1\jpeoples

    Done.

The following example grants the collection-level "View collection-level information" permission to the Collection0 project collection for Datum1 domain user John Peoples (Datum1\\jpeoples).

     tfssecurity /a+ Server FrameworkGlobalSecurity GenericRead n:Datum1\jpeoples ALLOW /collection:http://ADatumCorporation:8080/Collection0

Sample output:

    TFSSecurity - Team Foundation Server Security Tool
    Copyright (c) Microsoft Corporation.  All rights reserved.
    The target Team Foundation Server is http://ADatumCorporation:8080/COLLECTION0.
    Resolving identity "n:Datum1\jpeoples"...
      [U] DATUM1\jpeoples (John Peoples)
    Adding the access control entry...
    Verifying...

    Effective ACL on object "FrameworkGlobalSecurity":
      [+] GenericRead                        [Collection0]\Project Collection ValidUsers
      [+] GenericRead                        [Collection0]\Project Collection Service Accounts
      [+] GenericWrite                       [Collection0]\Project Collection Service Accounts
      [+] Impersonate                        [Collection0]\Project Collection Service Accounts
      [+] TriggerEvent                       [Collection0]\Project Collection Service Accounts
      [+] GenericRead                        [Collection0]\Project Collection Administrators
      [+] GenericWrite                       [Collection0]\Project Collection Administrators
      [+] TriggerEvent                       [Collection0]\Project Collection Administrators
      [+] GenericRead                        [INSTANCE]\SharePoint Web Application Services
      [+] Impersonate                        [INSTANCE]\SharePoint Web Application Services
      [+] GenericRead                        [Collection0]\Project Collection Build Service Accounts
      [+] GenericRead                        DATUM1\jpeoples

    Done.

<a id="aminus"></a>

### /a-: Remove a user or a group from membership in a group

Use the **/a-** command to remove a user or a group from membership in a server-level, collection-level, or project-level group. To add users to groups from the user interface, see [Manage users or groups](https://msdn.microsoft.com/library/30493f4c-d3e6-42f0-bca2-2ad749246944).

	tfssecurity /a- Namespace Token Action Identity (ALLOW | DENY) [/collection:CollectionURL] [/server:ServerURI]

#### Prerequisites

To use the **/a-** command, you must have the View collection-level information or the View instance-level information permission set to Allow, depending on whether you are using the **/collection** or **/server** parameter, respectively. If you are changing permissions for a project, you must also have the Edit project-level information permission for the project set to Allow.

#### Parameters

| Argument | Description |
| --- | --- |
| Namespace | The namespace that contains the group to which you want to remove permissions for a user or group. You can also use the **tfssecurity /a** command to view a list of namespaces at the server, collection, and project level. |
| Identity | The identity of the user or the group. For more information about identity specifiers, see [TFSSecurity Identity and Output Specifiers](#specifiers).<br><ul><li>**ALLOW**<br>The group or user can perform the operation that the Action specifies.</li><li>**DENY**<br>The group or user cannot perform the operation that the Action specifies.</li></ul> |
| **/collection** :CollectionURL | Required if **/server** is not used. Specifies the URL of a project collection in the following format: **http://** ServerName **:** Port **/** VirtualDirectoryName **/** CollectionName |
| **/server** :ServerURL | Required if **/collection** is not used. Specifies the URL of an application-tier server in the following format: **http://** ServerName **:** Port **/** VirtualDirectoryName |

#### Remarks

Run this command on an application-tier server for Azure DevOps.

Access control entries are security mechanisms that determine which operations a user, group, service, or computer is authorized to perform on a computer or server.

#### Examples

The following example displays what namespaces are available at the server level for the application-tier server that is named ADatumCorporation.

> [!NOTE]
> The examples are for illustration only and are fictitious. No real association is intended or inferred.

     tfssecurity /a /server:ServerURL 

Sample output:

    TFSSecurity - Team Foundation Server Security Tool
    Copyright (c) Microsoft Corporation.  All rights reserved.

    The target Team Foundation Server is http://ADatumCorporation:8080/.

    The following security namespaces are available to have permissions set on them:

         Registry
         Identity
         Job
         Server
         CollectionManagement
         Warehouse
         Catalog
         EventSubscription
         Lab

    Done.

The following example displays what actions are available for the Server namespace at the collection level.

    tfssecurity /a Server /collection:CollectionURL 

Sample output:

    TFSSecurity - Team Foundation Server Security Tool
    Copyright (c) Microsoft Corporation.  All rights reserved.

    The target Team Foundation Server is http://ADatumCorporation:8080/.

    The following actions are available in the security namespace Server:
        GenericRead
        GenericWrite
        Impersonate
        TriggerEvent

    Done.

The following example removes the server-level "View instance-level information" permission to the ADatumCorporation deployment for the Datum1 domain user John Peoples (Datum1\\jpeoples).

    tfssecurity /a- Server FrameworkGlobalSecurity GenericRead n:Datum1\jpeoples ALLOW /server:http://ADatumCorporation:8080 

Sample output:

    TFSSecurity - Team Foundation Server Security Tool
    Copyright (c) Microsoft Corporation.  All rights reserved.

    The target Team Foundation Server is http://ADatumCorporation:8080/.
    Resolving identity "n:Datum1\jpeoples"...
      [U] Datum1\jpeoples (John Peoples)
    Removing the access control entry...
    Verifying...

    Effective ACL on object "FrameworkGlobalSecurity":
      [+] GenericRead                        [INSTANCE]\Team Foundation Valid Users
      [+] GenericRead                        [INSTANCE]\SharePoint Web Application Services
      [+] Impersonate                        [INSTANCE]\SharePoint Web Application Services
      [+] GenericRead                        [INSTANCE]\Team Foundation Service Accounts
      [+] GenericWrite                       [INSTANCE]\Team Foundation Service Accounts
      [+] Impersonate                        [INSTANCE]\Team Foundation Service Accounts
      [+] TriggerEvent                       [INSTANCE]\Team Foundation Service Accounts
      [+] GenericRead                        [INSTANCE]\Team Foundation Administrators
      [+] GenericWrite                       [INSTANCE]\Team Foundation Administrators
      [+] TriggerEvent                       [INSTANCE]\Team Foundation Administrators

    Done.

The following example removes the collection-level "View collection-level information" permission to the Collection0 project collection for Datum1 domain user John Peoples (Datum1\\jpeoples).

    tfssecurity /a+ Server FrameworkGlobalSecurity GenericRead n:Datum1\jpeoples ALLOW /collection:http://ADatumCorporation:8080/Collection0

Sample output:

    TFSSecurity - Team Foundation Server Security Tool
    Copyright (c) Microsoft Corporation.  All rights reserved.
    The target Team Foundation Server is http://ADatumCorporation:8080/COLLECTION0.
    Resolving identity "n:Datum1\jpeoples"...
      [U] DATUM1\jpeoples (John Peoples)
    Removing the access control entry...
    Verifying...

    Effective ACL on object "FrameworkGlobalSecurity":
      [+] GenericRead                        [Collection0]\Project Collection ValidUsers
      [+] GenericRead                        [Collection0]\Project Collection Service Accounts
      [+] GenericWrite                       [Collection0]\Project Collection Service Accounts
      [+] Impersonate                        [Collection0]\Project Collection Service Accounts
      [+] TriggerEvent                       [Collection0]\Project Collection Service Accounts
      [+] GenericRead                        [Collection0]\Project Collection Administrators
      [+] GenericWrite                       [Collection0]\Project Collection Administrators
      [+] TriggerEvent                       [Collection0]\Project Collection Administrators
      [+] GenericRead                        [INSTANCE]\SharePoint Web Application Services
      [+] Impersonate                        [INSTANCE]\SharePoint Web Application Services
      [+] GenericRead                        [Collection0]\Project Collection Build Service Accounts

    Done.

<a id="acl"></a>

### /acl: Display the access control list

Use **/acl** to display the access control list that applies to a particular object.

	tfssecurity /acl Namespace Token [/collection:CollectionURL] [/server:ServerURL]

#### Prerequisites

To use the **/acl** command, you must have the **View collection-level information**
or the **View instance-level information** permission set to **Allow**,
depending on whether you are using the **/collection** or **/server** parameter, respectively.
For more information, see [Permission reference for Azure DevOps Server](/azure/devops/security/permissions).

#### Parameters

| Argument | Description |
| --- | --- |
| Namespace | The namespace that contains the group to which you want to view permissions for a user or group. |
| **/collection** :CollectionURL | Required if **/server** is not used. Specifies the URL of a project collection in the following format: **http://** ServerName **:** Port **/** VirtualDirectoryName **/** CollectionName |
| **/server** :ServerURL | Required if **/collection** is not used. Specifies the URL of an application-tier server in the following format: **http://** ServerName **:** Port **/** VirtualDirectoryName |

#### Remarks  

Run this command on an application-tier server for Azure DevOps.

Access control entries are security mechanisms that determine which operations a user, group, service, or computer is authorized to perform on a computer or server.

#### Examples  
 
The following example displays what users and groups have access to the FrameworkGlobalSecurity token in the Server namespace within the ADatumCorporation deployment.

> [!NOTE]
> The examples are for illustration only and are fictitious. No real association is intended or inferred.

	tfssecurity /acl Server FrameworkGlobalSecurity /server:ServerURL 

Sample output:

	TFSSecurity - Team Foundation Server Security Tool
	Copyright (c) Microsoft Corporation.  All rights reserved.
	The target Team Foundation Server is http://ADatumCorporation:8080/.
	Retrieving the access control list for object "Server"...

	Effective ACL on object "FrameworkGlobalSecurity":
	  [+] GenericRead                        [INSTANCE]\Team Foundation Valid Users
	  [+] GenericRead                        [INSTANCE]\SharePoint Web Application Services
	  [+] Impersonate                        [INSTANCE]\SharePoint Web Application Services
	  [+] GenericRead                        [INSTANCE]\Team Foundation Service Accounts
	  [+] GenericWrite                       [INSTANCE]\Team Foundation Service Accounts
	  [+] Impersonate                        [INSTANCE]\Team Foundation Service Accounts
	  [+] TriggerEvent                       [INSTANCE]\Team Foundation Service Accounts
	  [+] GenericRead                        [INSTANCE]\Team Foundation Administrators
	  [+] GenericWrite                       [INSTANCE]\Team Foundation Administrators
	  [+] TriggerEvent                       [INSTANCE]\Team Foundation Administrators
	  [+] GenericRead                        DATUM1\jpeoples

	Done.

	
## Groups

<a id="g"></a>

### /g: List the groups

Use **/g** to list the groups in a project, in a project collection, or across Azure DevOps Server.

	tfssecurity /g [scope] [/collection:CollectionURL] [/server:ServerURL]

#### Prerequisites

To use the **/g** command, you must have the View collection-level information or the View instance-level information permission set to Allow, depending on whether you are using the **/collection** or **/server** parameter, respectively. To use the /g command within the scope of a single project, you must have the View project-level information permissions set to Allow. For more information, see [Permission reference for Team Foundation Server](https://msdn.microsoft.com/library/39997de5-b7fb-4777-b779-07de0543abe6).

#### Parameters

|Argument|Description|
|---|---|
|scope|Optional. Specifies the URI of the project for which you want to display groups. To obtain the URI for a project, open Team Explorer, right-click the project, click Properties, and copy the entire entry for URL.|
|**/collection** :CollectionURL|Required if **/server** is not used. Specifies the URL of a project collection in the following format: **http://** ServerName **:** Port **/** VirtualDirectoryName **/** CollectionName|
|**/server** :ServerURL|Required if **/collection** is not used. Specifies the URL of an application-tier server in the following format: **http://** ServerName **:** Port **/** VirtualDirectoryName|

#### Remarks

Run this command on an application-tier server for Azure DevOps.

The **/g** command of the **TFSSecurity** command-line utility displays information about every group within the selected scope. This scope can be the project collection (**/server**) or the application-tier server (**/instance**). If used with the scope of a project, it will display information only about the groups associated with that project.

#### Example

The following example displays information for all the groups within a project collection.

    tfssecurity /g /collection:CollectionURL

<a id="gplus"></a>

### /g+: Add a user or another group to an existing group

Use **/g+** to add a user or another group to an existing group.

	tfssecurity /g+ groupIdentity memberIdentity [/collection:CollectionURL] [/server:ServerURL]

#### Prerequisites

To use the **/g+** command, you must have the View collection-level information and Edit collection-level information or the View instance-level information and Edit instance-level information permissions set to Allow, depending on whether you are using the /collection or /server parameter, respectively. For more information, see [Permission reference for Azure DevOps Server](https://msdn.microsoft.com/library/39997de5-b7fb-4777-b779-07de0543abe6).

#### Parameters

|Argument|Description|
|---|---|
|groupIdentity|Specifies the group identity. For more information on valid identity specifiers, see [TFSSecurity Identity and Output Specifiers](#specifiers).|
|memberIdentity|Specifies the member identity. For more information on valid identity specifiers, see [TFSSecurity Identity and Output Specifiers](#specifiers).|
|**/collection** :CollectionURL|Required if **/server** is not used. Specifies the URL of a project collection in the following format: **http://** ServerName **:** Port **/** VirtualDirectoryName **/** CollectionName|
|**/server** :ServerURL|Required if **/collection** is not used. Specifies the URL of an application-tier server in the following format: **http://** ServerName **:** Port **/** VirtualDirectoryName|

#### Remarks

Run this command on an application-tier server for Azure DevOps.

You can also add users and groups to an existing group using Team Explorer. For more information, see [Add Users to a Collection-Level Group](https://msdn.microsoft.com/library/65e3df75-0700-47d2-9877-5a16e3065d22).

#### Examples

The following example adds the Datum1 domain user John Peoples (Datum1\\jpeoples) to the Team Foundation Administrators group.

> [!NOTE]
> The examples are for illustration only and are fictitious. No real association is intended or inferred.

    tfssecurity /g+ "Team Foundation Administrators" n:Datum1\jpeoples /server:http://ADatumCorporation:8080

Sample output:

    TFSSecurity - Team Foundation Server Security Tool
    Copyright (c) Microsoft Corporation.  All rights reserved.

    The target Team Foundation Server is http://ADatumCorporation:8080/.
    Resolving identity "Team Foundation Administrators"...
    a [A] [INSTANCE]\Team Foundation Administrators
    Resolving identity "n:Datum1\jpeoples"...
      [U] DATUM1\jpeoples (John Peoples)
    Adding John Peoples to [INSTANCE]\Team Foundation Administrators...
    Verifying...

    SID: S-1-9-XXXXXXXXXX-XXXXXXXXXX-XXXXXXXXXX-XXXXXXXXXX-0-0-0-0-1

    DN:

    Identity type: Team Foundation Server application group
       Group type: AdministrativeApplicationGroup
    Project scope: Server scope
     Display name: [INSTANCE]\Team Foundation Administrators
      Description: Members of this group can perform all operations on the Team Foundation Application Instance.

    4 member(s):
      [U] Datum1\hholt (Holly Holt)
      [U] Datum1\jpeoples (John Peoples)
      [G] BUILTIN\Administrators (BUILTIN\Administrators)
    s [A] [INSTANCE]\Team Foundation Service Accounts

    Member of 2 group(s):
    a [A] [Collection0]\Project Collection Administrators
    e [A] [INSTANCE]\Team Foundation Valid Users

    Done.

<a id="gminus"></a>

### /g-: Remove a user or group

Use **/g-** to remove a user or a user group from an existing group.

	tfssecurity /g- groupIdentity memberIdentity [/collection:CollectionURL] [/server:ServerURL]

#### Prerequisites

To use the **/g-** command, you must have the View collection-level information and Edit collection-level information or the View instance-level information and Edit instance-level information permissions set to Allow, depending on whether you are using the **/collection** or **/server** parameter, respectively. For more information, see [Permission reference for Azure DevOps Server](https://msdn.microsoft.com/library/39997de5-b7fb-4777-b779-07de0543abe6).

#### Parameters

|Argument|Description|
|---|---|
|groupIdentity|Specifies the group identity. For more information about valid identity specifiers, see [TFSSecurity Identity and Output Specifiers](#specifiers).|
|memberIdentity|Specifies the member identity. For more information about valid identity specifiers, see [TFSSecurity Identity and Output Specifiers](#specifiers).|
|**/collection** :CollectionURL|Required if **/server** is not used. Specifies the URL of a project collection in the following format: **http://** ServerName **:** Port **/** VirtualDirectoryName **/** CollectionName|
|**/server** :ServerURL|Required if **/collection** is not used. Specifies the URL of an application-tier server in the following format: **http://** ServerName **:** Port **/** VirtualDirectoryName|

#### Remarks

Run this command on an application-tier server for Azure DevOps.

You can also add users and groups to an existing group using Team Explorer. For more information, see [Remove users from a project group](/azure/devops/organizations/security/add-users-team-project) or [Set permissions at the project- or collection-level](/azure/devops/organizations/security/set-project-collection-level-permissions).

#### Examples

The following example removes the Datum1 domain user John Peoples (Datum1\\jpeoples) from the Team Foundation Administrators group.

> [!NOTE]
> The examples are for illustration only and are fictitious. No real association is intended or inferred.

    tfssecurity /g- "Team Foundation Administrators" n:Datum1\jpeoples /server:http://ADatumCorporation:8080

Sample output:

    TFSSecurity - Team Foundation Server Security Tool
    Copyright (c) Microsoft Corporation.  All rights reserved.

    The target Team Foundation Server is http://ADatumCorporation:8080/.
    Resolving identity "Team Foundation Administrators"...
    a [A] [INSTANCE]\Team Foundation Administrators
    Resolving identity "n:Datum1\jpeoples"...
      [U] DATUM1\jpeoples (John Peoples)
    Removing John Peoples from [INSTANCE]\Team Foundation Administrators...
    Verifying...

    SID: S-1-9-XXXXXXXXXX-XXXXXXXXXX-XXXXXXXXXX-XXXXXXXXXX-0-0-0-0-1

    DN:

    Identity type: Team Foundation Server application group
       Group type: AdministrativeApplicationGroup
    Project scope: Server scope
     Display name: [INSTANCE]\Team Foundation Administrators
      Description: Members of this group can perform all operations on the Team Foundation Application Instance.

    3 member(s):
      [U] Datum1\hholt (Holly Holt)
      [G] BUILTIN\Administrators (BUILTIN\Administrators)
    s [A] [INSTANCE]\Team Foundation Service Accounts

    Member of 2 group(s):
    a [A] [Collection0]\Project Collection Administrators
    e [A] [INSTANCE]\Team Foundation Valid Users

    Done.

<a id="gc"></a>

### /gc: Create a project-level group

Use **/gc** at a command prompt to create a project-level group. To create a project-level group from the user interface, see <span sdata="link"> Manage users or groups </span>.

	tfssecurity /gc Scope GroupName [GroupDescription] [/collection:CollectionURL]

#### Prerequisites

To use the **/gc** command, you must have the Edit Project-Level Information permission for that project set to Allow. For more information, see <span sdata="link"> Permission reference for Azure DevOps Server </span>.

#### Parameters

|Argument|Description|
|---|---|
|Scope|The URI of the project to which you want to add a project-level group. To obtain the URI for a project, connect to it, and open Team Explorer, hover over the name of the project in Home, and read the address. Alternatively, connect to the project in Web Access and copy the URL.|
|GroupName|The name of the new group.|
|GroupDescription|A description of the project group. Optional.|
|**/collection** :CollectionURL|The URL of the project collection. Required. The group will be created within the project collection. The format for the URL is **http://** ServerName **:** Port **/** VirtualDirectoryName **/** CollectionName|

#### Remarks

Run this command on an application-tier server for Azure DevOps.

A project-level group is a security group for your project. You can use project groups to grant read, write, and administrative permissions that meet the security requirements of your organization.

#### Example

The following example creates a group that is specific to the project that the URI "vstfs://Classification/TeamProject/00000000-0000-0000-0000-000000000000" specifies. The group is named "Test Group" and has the description "This group is for testing."

> [!NOTE]
> The examples are for illustration only and are fictitious. No real association is intended or inferred.

You must replace the placeholder GUID with the URI of the project for which you want to create this group. To obtain the URI for a project, open Team Explorer, right-click the project, click Properties, and copy the entire value of the URL property.

After you run the command, you can verify the group in Team Explorer. Right-click the project that you used in the command, click Project Settings, and then click Group Memberships. In the Project Groups on  TeamProjectName dialog box, the Groups list includes Test Group .

> [!NOTE]
> You can use the **/gc** command to create groups but not to add any users to the groups or assign any permissions. To change the membership of the group, see [/g+: Add a user or another group to an existing group](#gplus) and [/g-: Remove a user or group](#gminus). To change the permissions for the group, see [/a+: Add permissions](#aplus) and [/a-: Remove a user or a group from membership in a group](#aminus).

    tfssecurity /gc "vstfs:///Classification/TeamProject/00000000-0000-0000-0000-000000000000" "Test Group"
		"This group is for team members who test our code" /collection:CollectionURL

<a id="gcg"></a>

### /gcg: Create a server or collection-level group

Use the **/gcg** command to create a server-level or collection-level group. To create a server-level or collection-level group from the user interface, see [Manage users or groups](https://msdn.microsoft.com/library/30493f4c-d3e6-42f0-bca2-2ad749246944).

	tfssecurity /gcg GroupName [GroupDescription] [/collection:CollectionURL] [/server:ServerURL]

#### Prerequisites

To use the **/gcg** command, you must have the Edit project-level information permission for that project set to Allow. For more information, see [Permission reference for Azure DevOps Server](https://msdn.microsoft.com/library/39997de5-b7fb-4777-b779-07de0543abe6).

#### Parameters

|Argument|Description|
|---|---|
|GroupName|The group name.|
|GroupDescription|A description of the group. Optional.|
|**/collection** :CollectionURL|Required if **/server** is not used. Specifies the URL of a project collection in the following format: **http://** ServerName **:** Port **/** VirtualDirectoryName **/** CollectionName|
|**/server** :ServerURL|Required if **/collection** is not used. Specifies the URL of an application-tier server in the following format: **http://** ServerName **:** Port **/** VirtualDirectoryName|

#### Remarks

Run this command on an application-tier server for Azure DevOps.

Server-level groups are created directly on the application tier and apply to all project collections. Collection-level are created at the project collection level. They apply to that collection and have implications for all projects within the collection. In contrast, project groups apply to a specific project within a collection but not any other projects in that collection. You can assign permissions to server-level groups so that members of those groups can perform tasks in Azure DevOps Server itself, such as creating project collections. You can assign permissions to collection-level groups so that members of those groups can perform tasks across a project collection, such as administering users.

> [!NOTE]
> You can use the <b>/gcg</b> command to create groups, but you cannot use it to add any users to the groups or assign any permissions. For information about how to change the membership of a group, see [/g+: Add a user or another group to an existing group](#gplus) and [/g-: Remove a user or group](#gminus). For information about how to change the permissions for the group, see [/a+: Add permissions](#aplus) and [/a-: Remove a user or a group from membership in a group](#aminus).

#### Example

The following example creates a collection-level group that is named "Datum Testers" with the description "A. Datum Corporation Testers."

> [!NOTE]
> The examples are for illustration only and are fictitious. No real association is intended or inferred.

    tfssecurity /gcg "Datum Testers" "A. Datum Corporation Testers" /collection:CollectionURL

The following example creates a server-level group that is named "Datum Auditors" with the description "A. Datum Corporation Auditors."

    tfssecurity /gcg "Datum Auditors" "A. Datum Corporation Auditors" /server:ServerURL

<a id="gd"></a>

### /gd: Delete a server or collection-level group

Use **/gd** to delete a server-level or collection-level group.

	tfssecurity /gd groupIdentity [/collection:CollectionURL] [/server:ServerURL]

#### Prerequisites

To use the **/gd** command, you must have the View collection-level information and Edit collection-level information or the View instance-level information and Edit instance-level information permissions set to Allow, depending on whether you are using the **/collection** or **/server** parameter, respectively. For more information, see [Permission reference for Azure DevOps Server](https://msdn.microsoft.com/library/39997de5-b7fb-4777-b779-07de0543abe6).

#### Parameters

|Argument|Description|
|---|---|
|groupIdentity|Specifies the group identity. |
|**/collection** :CollectionURL|Required if **/server** is not used. Specifies the URL of a project collection in the following format: **http://** ServerName **:** Port **/** VirtualDirectoryName **/** CollectionName|
|**/server** :ServerURL|Required if **/collection** is not used. Specifies the URL of an application-tier server in the following format: **http://** ServerName **:** Port **/** VirtualDirectoryName|

#### Remarks

Run this command on an application-tier server for Azure DevOps.

You can also remove groups on Team Explorer. For more information, see [Remove a Collection-Level Group](https://msdn.microsoft.com/library/68582caf-aa57-47a0-924a-6de7f541c246) and [Remove a Project Group](https://msdn.microsoft.com/library/dfb686ca-5a8b-4da9-bd00-6d68ae85f9fa).

#### Example

The following example deletes a group from the project collection. The group is identified by "S-1-5-21-2127521184-1604012920-1887927527-588340", the security identifier (SID). For more information about finding the SID of a group, see [/im: Display information about identities that compose direct membership](#im). You can also use the friendly name to delete a group.

> [!NOTE]
> The examples are for illustration only and are fictitious. No real association is intended or inferred.

    tfssecurity /gd S-1-5-21-2127521184-1604012920-1887927527-588340 /collection:CollectionURL

<a id="gud"></a>

### /gud: Change the description for a server or collection-level group

Use **/gud** to change the description for a server-level or collection-level group.

	tfssecurity /gud GroupIdentity GroupDescription [/collection:CollectionURL] [/server:ServerURL]

#### Prerequisites

To use the **/gud** command, you must have the Edit project-level information permission set to Allow. For more information, see [Permission reference for Azure DevOps Server](https://msdn.microsoft.com/library/39997de5-b7fb-4777-b779-07de0543abe6).

#### Parameters

|Argument|Description|
|---|---|
|GroupIdentity|Specifies the group identity. For more information about valid identity specifiers, see [TFSSecurity Identity and Output Specifiers](#specifiers).|
|GroupDescription|Specifies the new description for the group.|
|**/collection** :CollectionURL|Required if **/server** is not used. Specifies the URL of a project collection in the following format: **http://** ServerName **:** Port **/** VirtualDirectoryName **/** CollectionName|
|**/server** :ServerURL|Required if **/collection** is not used. Specifies the URL of an application-tier server in the following format: **http://** ServerName **:** Port **/** VirtualDirectoryName|

#### Remarks

Run this command on an application-tier server for Azure DevOps.

#### Example

The following example associates the description "The members of this group test the code for this project" with the group "Datum Testers."

> [!NOTE]
> The examples are for illustration only and are fictitious. No real association is intended or inferred.

    tfssecurity /gud "Datum Testers" "The members of this group test the code for this project" /collection:CollectionURL

<a id="gun"></a>

### /gun: Rename a group

Use **/gun** to rename a server-level or collection-level group.

	tfssecurity /gun GroupIdentity GroupName [/collection:CollectionURL] [/server:ServerURL]

#### Prerequisites

To use the **/gun** command, you must have the View collection-level information and Edit collection-level information or the View instance-level information and Edit instance-level information permissions set to Allow, depending on whether you are using the **/collection** or **/server** parameter, respectively. For more information, see [Permission reference for Azure DevOps Server](https://msdn.microsoft.com/library/39997de5-b7fb-4777-b779-07de0543abe6)>.

#### Parameters

|Argument|Description|
|---|---|
|GroupIdentity|Specifies the group identity. For more information about valid identity specifiers, see [TFSSecurity Identity and Output Specifiers](#specifiers).|
|GroupName|Specifies the new name of the group.|
|**/collection** :CollectionURL|Required if **/server** is not used. Specifies the URL of a project collection in the following format: **http://** ServerName **:** Port **/** VirtualDirectoryName **/** CollectionName|
|**/server** :ServerURL|Required if **/collection** is not used. Specifies the URL of an application-tier server in the following format: **http://** ServerName **:** Port **/** VirtualDirectoryName|

#### Remarks

Run this command on an application-tier server for Azure DevOps.

#### Example

The following example renames the collection-level group "A. Datum Corporation Testers" to "A. Datum Corporation Test Engineers."

> [!NOTE]
> The examples are for illustration only and are fictitious. No real association is intended or inferred.

    tfssecurity /gun "A. Datum Corporation Testers" "A. Datum Corporation Test Engineers" /collection:CollectionURL

## Identities and membership

<a id="i"></a>

### /i: Display identity information for a specified group

Use **/i** to display identity information for a specified group in a deployment of Azure DevOps Server.

	tfssecurity /i Identity [/collection:CollectionURL] [/server:ServerURL]

#### Prerequisites

To use the **/i** command, you must have the View collection-level information or the View instance -level information permission set to Allow, depending on whether you are using the /collection or /server parameter, respectively. For more information, see [Permission reference for Azure DevOps Server](https://msdn.microsoft.com/library/39997de5-b7fb-4777-b779-07de0543abe6).

#### Parameters

|Argument|Description|
|---|---|
|Identity|The identity of the user or the application group. For more information about identity specifiers, see [TFSSecurity Identity and Output Specifiers](#specifiers).|
|**/collection** :CollectionURL|Required if **/server** is not used. Specifies the URL of a project collection in the following format: **http://** ServerName **:** Port **/** VirtualDirectoryName **/** CollectionName|
|**/server** :ServerURL|Required if **/collection** is not used. Specifies the URL of an application-tier server in the following format: **http://** ServerName **:** Port **/** VirtualDirectoryName|

#### Remarks

Run this command on an application-tier server for Azure DevOps.

The **/i** command of the **TFSSecurity** command-line utility displays information about each group within the project collection (/server) or the application-tier server (/instance). It does not display any membership information.

#### Examples

The following example displays identity information for the "Team Foundation Administrators" group.

> [!NOTE]
> The examples are for illustration only and are fictitious. No real association is intended or inferred.

    tfssecurity /i "Team Foundation Administrators" /server:ServerURL 

Sample output:

    Resolving identity "Team Foundation Administrators"...

    SID: S-1-9-XXXXXXXXXX-XXXXXXXXXX-XXXXXXXXXX-XXXXXXXXXX-0-0-0-0-1

    DN:

    Identity type: Team Foundation Server application group
       Group type: AdministrativeApplicationGroup
    Project scope: Server scope
     Display name: Team Foundation Administrators
      Description: Members of this application group can perform all privileged operations on the server.

The following example displays identity information for the Project Collection Administrators group using the adm: identity specifier.

    tfssecurity /i adm: /collection:CollectionURL 

Sample output:

    Resolving identity "adm:"...

    SID: S-1-9-XXXXXXXXXX-XXXXXXXXXX-XXXXXXXXXX-XXXXXXXXXX-0-0-0-0-1

    DN:

    Identity type: Team Foundation Server application group
       Group type: AdministrativeApplicationGroup
    Project scope: Server scope
     Display name: [DatumOne]\Project Collection Administrators
      Description: Members of this application group can perform all privileged operations on the project collection.

The following example displays identity information for the Project Administrators group for the "Datum" project by using the adm: identity specifier.

    tfssecurity /i adm:vstfs:///Classification/TeamProject/ProjectGUID /collection:CollectionURL 

Sample output:

    Resolving identity "adm:vstfs:///Classification/TeamProject/ProjectGUID"...

    SID: S-1-9-XXXXXXXXXX-XXXXXXXXXX-XXXXXXXXXX-XXXXXXXXXX-0-0-0-0-1

    DN:

    Identity type: Team Foundation Server application group
       Group type: AdministrativeApplicationGroup
    Project scope: Datum
     Display name: [Datum]\Project Administrators
      Description: Members of this application group can perform all operations in the project.

<a id="im"></a>

### /im: Display information about identities that compose direct membership

Use **/im** to display information about the identities that compose the direct membership of a group that you specify.

	tfssecurity /im Identity [/collection:CollectionURL] [/server:ServerURL]

#### Prerequisites

To use the **/im** command, you must have the View collection-level information or the View instance-level information permission set to Allow, depending on whether you are using the /collection or /server parameter, respectively. For more information, see [Permission reference for Azure DevOps Server](https://msdn.microsoft.com/library/39997de5-b7fb-4777-b779-07de0543abe6).

#### Parameters

|Argument|Description|
|---|---|
|Identity|The identity of the user or the group. For more information about identity specifiers, see [TFSSecurity Identity and Output Specifiers](#specifiers).|
|**/collection** :CollectionURL|Required if **/server** is not used. Specifies the URL of a project collection in the following format: **http://** ServerName **:** Port **/** VirtualDirectoryName **/** CollectionName|
|**/server** :ServerURL|Required if **/collection** is not used. Specifies the URL of an application-tier server in the following format: **http://** ServerName **:** Port **/** VirtualDirectoryName|

#### Remarks

Run this command on an application-tier server for Azure DevOps.

The **/im** command of **TFSSecurity** displays the direct members of the specified group only. This list includes other groups that are members of the specified group. However, the actual members of the member groups are not listed.

#### Examples

The following example displays direct membership identity information for the "Team Foundation Administrators" group in the domain "Datum1" at the fictitious company "A. Datum Corporation".

> [!NOTE]
> The examples are for illustration only and are fictitious. No real association is intended or inferred.

    tfssecurity /im "Team Foundation Administrators" /server:ServerURL

Sample output:

    Resolving identity "Team Foundation Administrators"...

    SID: S-1-9-XXXXXXXXXX-XXXXXXXXXX-XXXXXXXXXX-XXXXXXXXXX-0-0-0-0-1

    DN:

    Identity type: Team Foundation Server application group
    Group type: AdministrativeApplicationGroup
    Project scope: Server scope
    Display name: Team Foundation Administrators
    Description: Members of this application group can perform all privileged operations on the server.

    3 member(s):
      [U] Datum1\hholt (Holt, Holly)
      [G] BUILTIN\Administrators (BUILTIN\Administrators)
    s [A] [InstanceName]\Team Foundation Service Accounts

    Member of 2 group(s):
    a [A] [DatumOne]\Project Collection Administrators ([DatumOne]\Project Collection Administrators)
    e [A] [InstanceName]\Team Foundation Valid Users

    Done.

The following example displays identity information for the Project Collection Administrators group in the "DatumOne" project collection in the domain "Datum1" at the fictitious company "A. Datum Corporation" by using the adm: identity specifier.

    tfssecurity /im adm: /collection:CollectionURL 

Sample output:

    Resolving identity "adm: "...

    SID: S-1-9-XXXXXXXXXX-XXXXXXXXXX-XXXXXXXXXX-XXXXXXXXXX-0-0-0-0-1

    DN:

    Identity type: Team Foundation Server application group
    Group type: AdministrativeApplicationGroup
    Project scope: Server scope
    Display name: [DatumOne]\Project Collection Administrators
    Description: Members of this application group can perform all privileged operations on the project collection.

    5 member(s):
      [U] Datum1\jpeoples (Peoples, John)
      [U] Datum1\hholt (Holt, Holly)
      [G] BUILTIN\Administrators (BUILTIN\Administrators)
    a [A] [InstanceName]\Team Foundation Administrators
    s [A] [DatumOne]\Project Collection Service Accounts ([DatumOne]\Project Collection Service Accounts)

    Member of 1 group(s):
    e [A] [DatumOne]\Project Collection Valid Users ([DatumOne]\Project Colleciton Valid Users)

    Done.

The following example displays identity information for the Project Administrators group for the "Datum" project in the "DatumOne" project collection in the domain "Datum1" at the fictitious company "A. Datum Corporation" using the adm: identity specifier.

    tfssecurity /im adm:vstfs:///Classification/TeamProject/ProjectGUID /collection:CollectionURL 

Sample output:

    Resolving identity "adm:vstfs:///Classification/TeamProject/ProjectGUID"...

    SID: S-1-9-XXXXXXXXXX-XXXXXXXXXX-XXXXXXXXXX-XXXXXXXXXX-XXXXXXX

    DN:

    Identity type: Team Foundation Server application group
    Group type: AdministrativeApplicationGroup
    Project scope: Datum
    Display name: [Datum]\Project Administrators
    Description: Members of this application group can perform all operations in the project.

    2 member(s):
      [U] Datum1\jpeoples (Peoples, John)
      [U] Datum1\hholt (Holt, Holly)

    Member of 1 group(s):
    e [A] [DatumOne]\Project Collection Valid Users ([DatumOne]\Project Collection Valid Users)

    Done.

<a id="imx"></a>

### /imx: Display information about the identities that the expanded membership

Use **/imx** to display information about the identities that compose the expanded membership of a specified group.

	tfssecurity /imx Identity [/collection:CollectionURL] [/server:ServerURL]

#### Prerequisites

To use the **/imx** command, you must have the View collection-level information or the View instance-level information permission set to Allow, depending on whether you are using the **/collection** or **/server** parameter, respectively. For more information, see [Permission reference for Azure DevOps Server](https://msdn.microsoft.com/library/39997de5-b7fb-4777-b779-07de0543abe6).

#### Parameters

|Argument|Description|
|---|---|
|Identity|The identity of the user or the group. For more information about identity specifiers, see [TFSSecurity Identity and Output Specifiers](#specifiers).|
|**/collection** :CollectionURL|Required if **/server** is not used. Specifies the URL of a project collection in the following format: **http://** ServerName **:** Port **/** VirtualDirectoryName **/** CollectionName|
|**/server** :ServerURL|Required if **/collection** is not used. Specifies the URL of an application-tier server in the following format: **http://** ServerName **:** Port **/** VirtualDirectoryName|

#### Remarks

Run this command on an application-tier server for Azure DevOps.

The **/imx** command of **TFSSecurity** displays the expanded members of the specified group only. This list includes not only other groups that are members of the specified group but also the members of the member groups.

#### Examples

The following example displays expanded membership identity information for the "Team Foundation Administrators" group in the domain "Datum1" at the fictitious company "A. Datum Corporation".

> [!NOTE]
> The examples are for illustration only and are fictitious. No real association is intended or inferred.

    tfssecurity /imx "Team Foundation Administrators" /server:ServerURL

Sample output:

    Resolving identity "Team Foundation Administrators"...

    SID: S-1-9-XXXXXXXXXX-XXXXXXXXXX-XXXXXXXXXX-XXXXXXXXXX-0-0-0-0-1

    DN:

    Identity type: Team Foundation Server application group
    Group type: AdministrativeApplicationGroup
    Project scope: Server scope
    Display name: Team Foundation Administrators
    Description: Members of this application group can perform all privileged operations on the server.

    10 member(s):
      [U] Datum1\hholt (Holly Holt)
      [U] Datum1\jpeoples (John Peoples)
      [U] Datum1\tommyh (Tommy Hartono)
      [U] Datum1\henriea (Henriette Andersen)
      [U] Datum1\djayne (Darcy Jayne)
      [U] Datum1\aprilr (April Reagan)
      [G] Datum1\InfoSec Secure Environment
      [U] Datum1\nbento (Nuno Bento)
      [U] Datum1\cristp (Cristian Petculescu)
      [G] BUILTIN\Administrators (BUILTIN\Administrators)
    s [A] [InstanceName]\Team Foundation Service Accounts

    Member of 3 group(s):
    a [A] [DatumOne]\Project Collection Administrators ([DatumOne]\Project Collection Administrators)
    e [A] [DatumOne]\Project Collection Valid Users ([DatumOne]\Project Collection Valid Users)
    e [A] [InstanceName]\Team Foundation Valid Users

    Done.

The following example displays identity information for the Project Collection Administrators group in the "DatumOne" project collection in the domain "Datum1" at the fictitious company "A. Datum Corporation" using the adm: identity specifier.

    tfssecurity /imx adm: /collection:CollectionURL 

Sample output:

    Resolving identity "adm: "...

    SID: S-1-9-XXXXXXXXXX-XXXXXXXXXX-XXXXXXXXXX-XXXXXXXXXX-0-0-0-0-1

    DN:

    Identity type: Team Foundation Server application group
    Group type: AdministrativeApplicationGroup
    Project scope: Server scope
    Display name: [DatumOne]\Project Collection Administrators
    Description: Members of this application group can perform all privileged operations on the project collection.

    6 member(s):
      [U] Datum1\jpeoples (Peoples, John)
      [U] Datum1\hholt (Holt, Holly)
      [G] BUILTIN\Administrators (BUILTIN\Administrators)
    a [A] [InstanceName]\Team Foundation Administrators
    s [A] [InstanceName]\Team Foundation Service Accounts
    s [A] [DatumOne]\Project Collection Service Accounts ([DatumOne]\Project Collection Service Accounts)

    Member of 1 group(s):
    e [A] [DatumOne]\Project Collection Valid Users ([DatumOne]\Project Collection Valid Users)

    Done.

The following example displays identity information for the Project Administrators group for the "Datum" project in the "DatumOne" project collection in the domain "Datum1" at the fictitious company "A. Datum Corporation" using the adm: identity specifier.

    tfssecurity /imx adm:vstfs:///Classification/TeamProject/ProjectGUID /collection:CollectionURL 

Sample output:

    Resolving identity "adm:vstfs:///Classification/TeamProject/ProjectGUID"...

    SID: S-1-9-XXXXXXXXXX-XXXXXXXXXX-XXXXXXXXXX-XXXXXXXXXX-XXXXXXX

    DN:

    Identity type: Team Foundation Server application group
    Group type: AdministrativeApplicationGroup
    Project scope: Datum
    Display name: [Datum]\Project Administrators
    Description: Members of this application group can perform all operations in the project.

    2 member(s):
      [U] Datum1\jpeoples (Peoples, John)
      [U] Datum1\hholt (Holt, Holly)

    Member of 2 group(s):
    e [A] [DatumOne]\Project Collection Valid Users ([DatumOne]\Project Collection Valid Users)
    e [A] [InstanceName]\Team Foundation Valid Users

    Done.

For more information about the output specifiers, such as [G] and [U], see [TFSSecurity Identity and Output Specifiers](#specifiers).

<a id="m"></a>

### /m: Check explicit and implicit group membership

Use **/m** to check explicit and implicit group membership information for a specified group or user.

	tfssecurity /m GroupIdentity [MemberIdentity] [/collection:CollectionURL] [/server:ServerURL]

#### Prerequisites

To use the **/m** command, you must be a member of the Team Foundation Administrators security group. For more information, see [Permission reference for Azure DevOps Server](https://msdn.microsoft.com/library/39997de5-b7fb-4777-b779-07de0543abe6).

> [!NOTE]
> Even if you are logged on with administrative credentials, you must open an elevated Command Prompt to perform this function.

#### Parameters

|Argument|Description|
|---|---|
|GroupIdentity|Specifies the group identity. For more information on valid identity specifiers, see [TFSSecurity Identity and Output Specifiers](#specifiers).|
|MemberIdentity|Specifies the member identity. By default, the value of this argument is the identity of the user who is running the command. For more information on valid identity specifiers, see [TFSSecurity Identity and Output Specifiers](#specifiers).|
|**/collection** :CollectionURL|Required if **/server** is not used. Specifies the URL of a project collection in the following format: **http://** ServerName **:** Port **/** VirtualDirectoryName **/** CollectionName|
|**/server** :ServerURL|Required if **/collection** is not used. Specifies the URL of an application-tier server in the following format: **http://** ServerName **:** Port **/** VirtualDirectoryName|

#### Remarks

Run this command on the local application-tier computer.

The **/m** command of the **TFSSecurity** command-line utility checks both direct and extended memberships.

#### Examples

The following example verifies whether the user "Datum1\\jpeoples" belongs to the Team Foundation Administrators server-level group.

> [!NOTE]
> The examples are for illustration only and are fictitious. No real association is intended or inferred.

```cmdline
tfssecurity /m "Team Foundation Administrators" n:Datum1\jpeoples /server:http://ADatumCorporation:8080
```

Sample output:

    TFSSecurity - Team Foundation Server Security Tool
    Copyright (c) Microsoft Corporation.  All rights reserved.

    The target Team Foundation Server is http://ADatumCorporation:8080/.
    Resolving identity "Team Foundation Administrators"...
    a [A] [INSTANCE]\Team Foundation Administrators
    Resolving identity "n:Datum1\jpeoples"...
      [U] DATUM1\jpeoples (John Peoples)
    Checking group membership...

    John Peoples IS a member of [INSTANCE]\Team Foundation Administrators.

    Done.

<a id="permissions"></a>

## Permission namespaces and actions

<a id="server-level-permissions"></a>

### Server level

|Permission|Namespace|Action|
|---|---|---|
|[Administer warehouse](/azure/devops/security/permissions#administer-warehouse-permission)|Warehouse|Administer|
|[Create project collection](/azure/devops/security/permissions#create-team-project-collection-permission)|CollectionManagement|CreateCollection|
|[Delete project collection](/azure/devops/security/permissions#delete-team-project-collection-permission)|CollectionManagement|DeleteCollection|
|[Edit instance-level information](/azure/devops/security/permissions#edit-instance-level-information-permission)|Server|GENERIC_WRITE<br /><br />tf: AdminConfiguration<br /><br />tf: AdminConnections|
|[Make requests on behalf of others](/azure/devops/security/permissions#make-requests-on-behalf-of-others-permission)|Server|Impersonate|
|[Trigger events](/azure/devops/security/permissions#trigger-events-permission)|Server|TRIGGER_EVENT|
|[Use full Web Access features](/azure/devops/security/permissions#use-full-web-access-features-permission)|Server|FullAccess|
|[View instance-level information](/azure/devops/security/permissions#view-instance-level-information-permission)|Server|GENERIC_READ|
|[Publish extensions](/azure/devops/extend/publish/overview)| Publisher| **For TFS 2017 or earlier**:<br />Create<br/>Publish<br />Write<br /><br />**For TFS 2017**:<br />CreatePublisher<br />PublishExtension<br />UpdateExtension<br />DeleteExtensions<br />|

<a id="collection-level-permissions"></a>

### Collection level

|Permission|Namespace|Action|
|---|---|---|
|[Administer build resource permissions](/azure/devops/security/permissions#administer-build-resource-permissions-permission)|BuildAdministration|AdministerBuildResourcePermissions|
|[Administer Project Server integration](/azure/devops/security/permissions#administer-Project-Server-integration-permission)|ProjectServerAdministration|AdministerProjectServer|
|[Administer shelved changes](/azure/devops/security/permissions#administer-shelved-changes-permission)|VersionControlPrivileges|AdminShelvesets<br /><br />tf: AdminShelvesets|
|[Administer workspaces](/azure/devops/security/permissions#administer-workspaces-permission)|VersionControlPrivileges|AdminWorkspaces<br /><br />tf: AdminWorkspaces|
|[Alter trace settings](/azure/devops/security/permissions#alter-trace-settings-permission)|Collection|DIAGNOSTIC_TRACE|
|[Create a workspace](/azure/devops/security/permissions#create-a-workspace-permission)|VersionControlPrivileges|tf: CreateWorkspace|
|[Create new projects](/azure/devops/security/permissions#create-new-team-projects-permission)|Collection|CREATE_PROJECTS|
|[Delete project](/azure/devops/security/permissions#delete-team-project-permission)|Project|Delete|
|[Edit collection-level information](/azure/devops/security/permissions#edit-collection-level-information-permission)|Collection<br /><br />VersionControlPrivileges|GENERIC_WRITE<br /><br />tf: AdminConfiguration<br /><br />tf: AdminConnections|
|[Make requests on behalf of others](/azure/devops/security/permissions#make-requests-on-behalf-of-others-permission)|Server|Impersonate|
|[Manage build resources](/azure/devops/security/permissions#manage-build-resources-permission)|BuildAdministration|ManageBuildResources|
|[Manage process template](/azure/devops/security/permissions#manage-process-template-permission)|Collection|MANAGE_TEMPLATE|
|[Manage test controllers](/azure/devops/security/permissions#manage-test-controllers-permission)|Collection|MANAGE_TEST_CONTROLLERS|
|[Trigger events](/azure/devops/security/permissions#trigger-events-permission)|Collection|TRIGGER_EVENT|
|[Use build resources](/azure/devops/security/permissions#use-build-resources-permission)|BuildAdministration|UseBuildResources|
|[View build resources](/azure/devops/security/permissions#view-build-resources-permission)|BuildAdministration|ViewBuildResources|
|[View collection-level information](/azure/devops/security/permissions#view-collection-level-information-permission)|Collection|GENERIC_READ|
|[View system synchronization information](/azure/devops/security/permissions#view-system-synchronization-information-permission)|Collection|SYNCHRONIZE_READ|
|Can create a SOAP-based web service subscription. |EventSubscription|CREATE_SOAP_SUBSCRIPTION|
|Can view subscription events defined for a project. |EventSubscription|GENERIC_READ|
|Can create alerts for other users or for a team. |EventSubscription|GENERIC_WRITE|
|Can unsubscribe from an event subscription. |EventSubscription|UNSUBSCRIBE|

<a id="team-project-level-permissions"></a>

### Project level

|Permission|Namespace|Action|
|---|---|---|
|[Create tag definition](/azure/devops/security/permissions#create-tag-definition-permission)|Tagging|Create|
|[Create test runs](/azure/devops/security/permissions#create-test-runs-permission)|Project| PUBLISH_TEST_RESULTS
|[Delete project](/azure/devops/security/permissions#delete-team-project-permission)|Project|DELETE|
|[Delete work items](/azure/devops/security/permissions#delete-work-items-in-this-project-permission) (TFS 2015.2)| Project | WORK_ITEM_DELETE | 
|[Delete test runs](/azure/devops/security/permissions#delete-test-runs-permission)|Project|DELETE_TEST_RESULTS|
|[Edit project-level information](/azure/devops/security/permissions#edit-team-project-level-information-permission)|Project|GENERIC_WRITE|
|[Move work items out of this project](/azure/devops/security/permissions#move-work-items-out-of-this-project-permission) (TFS 2015.2)| Project| WORK_ITEM_MOVE | 
|[Manage test configurations](/azure/devops/security/permissions#manage-test-configurations-permission)|Project|MANAGE_TEST_CONFIGURATIONS|
|[Manage test environments](/azure/devops/security/permissions#manage-test-environments-permission)|Project|MANAGE_TEST_ENVIRONMENTS|
|[Permanently delete (destroy) work items in this project](/azure/devops/security/permissions#permanently-delete-work-items-in-this-project-permission) (TFS 2015.2)| Project | WORK_ITEM_PERMANENTLY_DELETE | 
|[View project-level information](/azure/devops/security/permissions#view-team-project-level-information-permission)|Project|GENERIC_READ|
|[View test runs](/azure/devops/security/permissions#view-test-runs-permission)|Project|VIEW_TEST_RESULTS|

<a id="build-permissions"></a>

### Build

|Permission|Namespace|Action|
|---|---|---|
|[Administer build permissions](/azure/devops/security/permissions#administer-build-permissions-permission)|Build|AdministerBuildPermissions|
|[Delete build definition](/azure/devops/security/permissions#delete-build-definition-permission)|Build|DeleteBuildDefinition|
|[Delete builds](/azure/devops/security/permissions#delete-builds-permission)|Build|DeleteBuilds|
|[Destroy builds](/azure/devops/security/permissions#destroy-builds-permission)|Build|DestroyBuilds|
|[Edit build definition](/azure/devops/security/permissions#edit-build-definition-permission)|Build|EditBuildDefinition|
|[Edit build quality](/azure/devops/security/permissions#edit-build-quality-permission)|Build|EditBuildDefinition|
|[Manage build qualities](/azure/devops/security/permissions#manage-build-qualities-permission)|Build|ManageBuildQualities|
|[Manage build queue](/azure/devops/security/permissions#manage-build-queue-permission)|Build|ManageBuildQueue|
|[Override check-in validation by build](/azure/devops/security/permissions#override-check-in-validation-by-build-permission)|Build|OverrideBuildCheckInValidation|
|[Queue builds](/azure/devops/security/permissions#queue-builds-permission)|Build|QueueBuilds|
|[Retain indefinitely](/azure/devops/security/permissions#retain-indefinitely-permission)|Build|RetainIndefinitely|
|[Stop builds](/azure/devops/security/permissions#stop-builds-permission)|Build|StopBuilds|
|[Update build information](/azure/devops/security/permissions#update-build-information-permission)|Build|UpdateBuildInformation|
|[View build definition](/azure/devops/security/permissions#view-build-definition-permission)|Build|ViewBuildDefinition|
|[View builds](/azure/devops/security/permissions#view-builds-permission)|Build|ViewBuilds|

<a id="work-item-query-permissions"></a>

### Work item query

|Permission|Namespace|Action|
|---|---|---|
|[Contribute](/azure/devops/security/permissions#workitemqueryfolders-contribute-permission)|WorkItemQueryFolders|CONTRIBUTE|
|[Delete](/azure/devops/security/permissions#workitemqueryfolders-delete-permission)|WorkItemQueryFolders|DELETE|
|[Manage permissions](/azure/devops/security/permissions#workitemqueryfolders-manage-permissions-permission)||MANAGEPERMISSIONS|
|[Read](/azure/devops/security/permissions#workitemqueryfolders-read-permission)|WorkItemQueryFolders|READ|

<a id="tagging-permissions"></a>

### Tagging

|Permission|Namespace|Action|
|---|---|---|
|[Create tag definition](/azure/devops/security/permissions#create-tag-definition-permission)|Tagging|CREATE|
|[Delete tag definition](/azure/devops/security/permissions#delete-tag-definition-permission)|Tagging|DELETE|
|[Enumerate tag definition](/azure/devops/security/permissions#enumerate-tag-definition-permission)|Tagging|ENUMERATE|
|[Update tag definition](/azure/devops/security/permissions#update-tag-definition-permission)|Tagging|UPDATE|


<a id="area-permissions"></a>

### Area

|Permission|Namespace|Action|
|---|---|---|
|[Create child nodes](/azure/devops/security/permissions#area-create-child-nodes-permission)|CSS|CREATE_CHILDREN|
|[Delete this node](/azure/devops/security/permissions#area-delete-this-node-permission)|CSS|DELETE|
|[Edit this node](/azure/devops/security/permissions#area-edit-this-node-permission)|CSS|GENERIC_WRITE|
|[Edit work items in this node](/azure/devops/security/permissions#area-edit-work-items-in-this-node-permission)|CSS|WORK_ITEM_WRITE|
|[Manage test plans](/azure/devops/security/permissions#area-manage-test-plans-permission)|CSS|MANAGE_TEST_PLANS|
|[Manage test suites](/azure/devops/security/permissions#area-manage-test-suites-permission)|CSS|MANAGE_TEST_SUITES|
|[View permissions for this node](/azure/devops/security/permissions#area-view-permissions-for-this-node-permission)|CSS|GENERIC_READ|
|[View work items in this node](/azure/devops/security/permissions#area-view-work-items-in-this-node-permission)|CSS|WORK_ITEM_READ|

<a id="iteration-permissions"></a>

### Iteration

|Permission|Namespace|Action|
|---|---|---|
|[Create child nodes](/azure/devops/security/permissions#iteration-create-child-nodes-permission)|Iteration|CREATE_CHILDREN|
|[Delete this node](/azure/devops/security/permissions#iteration-delete-this-node-permission)|Iteration|DELETE|
|[Edit this node](/azure/devops/security/permissions#iteration-edit-this-node-permission)|Iteration|GENERIC_WRITE|
|[View permissions for this node](/azure/devops/security/permissions#iteration-view-permissions-for-this-node-permission)|Iteration|GENERIC_WRITE|

<a id="tfvc-permissions"></a>

### TFVC

|Permission|Namespace|Action|
|---|---|---|
|[Administer labels](/azure/devops/security/permissions#administer-labels-permission)|VersionControlItems|LabelOthers|
|[Check in](/azure/devops/security/permissions#check-in-permission)|VersionControlItems|Checkin|
|[Check in other users' changes](/azure/devops/security/permissions#check-in-other-users-changes-permission)|VersionControlItems|CheckinOther|
|[Check out](/azure/devops/security/permissions#check-out-permission)|VersionControlItems|PendChange|
|[Label](/azure/devops/security/permissions#label-permission)|VersionControlItems|Label|
|[Lock](/azure/devops/security/permissions#lock-permission)|VersionControlItems|Lock|
|[Manage branch](/azure/devops/security/permissions#manage-branch-permission)|VersionControlItems|ManageBranch|
|[Manage permissions](/azure/devops/security/permissions#manage-permissions-permission)|VersionControlItems|AdminProjectRights|
|[Merge](/azure/devops/security/permissions#merge-permission)|VersionControlItems|VersionControlItems|
|[Read](/azure/devops/security/permissions#read-permission)|VersionControlItems||
|[Revise other users' changes](/azure/devops/security/permissions#revise-other-users-changes-permission)|VersionControlItems|ReviseOther|
|[Undo other users' changes](/azure/devops/security/permissions#undo-other-users-changes-merge-permission)|VersionControlItems|UndoOther|
|[Unlock other users'-changes](/azure/devops/security/permissions#unlock-other-users-changes-permission)|VersionControlItems|UnlockOther|

<a id="git-repo-permissions"></a>

### Git repository

TFS 2017 Update 1 and later

|Permission|Namespace|Action|
|---|---|---|
|[Contribute](/azure/devops/security/permissions#git-contribute-permission)|GitRepositories|GenericContribute|
|[Contribute to Pull Requests](/azure/devops/security/permissions#git-contribute-to-pull-requests-permission)|GitRepositories|PullRequestContribute|
|[Create Branch](/azure/devops/security/permissions#git-create-branch-permission)|GitRepositories|CreateBranch|
|[Create Repository](/azure/devops/security/permissions#git-create-repository-permission)|GitRepositories|CreateRepository|
|[Create Tag](/azure/devops/security/permissions#git-create-tag-permission)|GitRepositories|CreateTag|
|[Delete Repository](/azure/devops/security/permissions#git-delete-repository-permission)|GitRepositories|DeleteRepository|
|[Edit Policies](/azure/devops/security/permissions#git-edit-policies-permission)|GitRepositories|EditPolicies|
|[Exempt From Policy Enforcement](/azure/devops/security/permissions#git-repository)|GitRepositories|PolicyExempt|
|[Force Push (Rewrite History and Delete Branches)](/azure/devops/security/permissions#git-force-push-permission)|GitRepositories|ForcePush|
|[Manage Notes](/azure/devops/security/permissions#git-repository)|GitRepositories|ManageNote|
|[Manage Permissions](/azure/devops/security/permissions#git-repository)|GitRepositories|ManagePermissions|
|[Read](/azure/devops/security/permissions#git-read-permission)|GitRepositories|GenericRead|
|[Remove Others' Locks](/azure/devops/security/permissions#git-remove-others-locks-permission)|GitRepositories|RemoveOthersLocks|
|[Rename Repository](/azure/devops/security/permissions#git-rename-repository-permission)|GitRepositories|RenameRepository|

TFS 2017 RTM and earlier

|Permission|Namespace|Action|
|---|---|---|
|[Administer](/azure/devops/security/git-permissions-before-2017#git-administer-permission)|GitRepositories|Administer|
|[Branch Creation](/azure/devops/security/git-permissions-before-2017#git-branch-creation-permission)|GitRepositories|CreateBranch|
|[Contribute](/azure/devops/security/git-permissions-before-2017#git-contribute-permission)|GitRepositories|GenericContribute|
|[Note Management](/azure/devops/security/git-permissions-before-2017#git-note-management-permission)|GitRepositories|ManageNote|
|[Read](/azure/devops/security/git-permissions-before-2017#git-read-permission)|GitRepositories|GenericRead|
|[Rewrite and destroy history (force push)](/azure/devops/security/git-permissions-before-2017#git-rewrite-and-destroy-history-permission)|GitRepositories|ForcePush|
|[Tag Creation](/azure/devops/security/git-permissions-before-2017#git-tag-creation-permission)|GitRepositories|CreateTag|

<a id="specifiers"></a>

## Identity specifiers

You can reference an identity by using one of the notations in the following table.

|Identity specifier|Description|Example|
|---|---|---|
|**sid:** Sid.|References the identity that has the specified security identifier (SID).|**sid:S-1-5-21-2127521184-1604012920-1887927527-588340**|
|**n:**[D omain\]Name|References the identity that has the specified name. For Windows, Name is the account name. If the referenced identity is in a domain, the domain name is required. For application groups, Name is the group display name, and Domain is the URI or GUID of the containing project. In this context, if Domain is omitted, the scope is assumed to be at the collection level.|To reference the identity of the user &quot;John Peoples&quot; in the domain &quot;Datum1&quot; at the fictitious company &quot;A. Datum Corporation:&quot;<br /><br />**n:DATUM1\jpeoples**<br /><br />To reference application groups:<br /><br />**n:&quot;Full-time Employees&quot;**<br /><br />**n:00a10d23-7d45-4439-981b-d3b3e0b0b1ee\Vendors**|
|**adm:**[Scope]|References the administrative application group for the scope, such as &quot;Team Foundation Administrators&quot; for the server level or &quot;Project Collection Administrators&quot; at the collection level. The optional parameter Scope is a project URI or URL, including its GUID and connection string. If scope is omitted, the server or collection scope is assumed based on whether the /instance or /server parameter is used. In either case, the colon is still required.|**adm:vstfs:///Classification/TeamProject/** GUID|
|**srv:**|References the application group for service accounts.|Not applicable|
|**all:**|References all groups and identities.|Not applicable|
|String|References an unqualified string. If String starts with **S-1-**, it is identified as a SID. If String starts with **CN=** or **LDAP://** it is identified as a distinguished name. Otherwise, String is identified as a name.|&quot;Team testers&quot;|

## Type Markers

The following markers are used to identify types of identities and ACEs in output messages.

### Identity type markers 

|Identity type marker|Description|
|---|---|
|**U**|Windows user.|
|**G**|Windows group.|
|**A**|Azure DevOps Server application group.|
|**a \[** A **\]**|Administrative application group.|
|**s \[** A **\]**|Service account application group.|
|**X**|Identity is not valid.|
|**?**|Identity is unknown.|

 
### Access control entry markers 

|Access control entry marker|Description|
|---|---|
|**+**|ALLOW access control entry.|
|**-**|DENY access control entry.|
|**\* \[\]**|Inherited access control entry.|

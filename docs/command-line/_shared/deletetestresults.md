---
ms.topic: include
---

::: moniker range="azure-devops-2019"

You use the **deleteTestResults** command to delete old stored test results from your collection store.
This is typically done to reduce the store size or to reduce the time taken when migrating test results to a new schema.

```
TfsConfig deleteTestResults /ageInDays:<number> /sqlInstance:<serverName> /databaseName:<databaseName>
    [/type:[automated|manual|all]]
    [/preview]
```

|Option|Description|
|---|---|
|ageInDays|Test results older than the specified number of days will be deleted or previewed.|
|sqlInstance|The name of the server that hosts the database for which test results are being deleted or previewed, and the name of the instance if an instance other than the default is used. If you specify an instance, you must use the format: `ServerName\InstanceName`.|
|databaseName|The name of the database for which test results are being deleted or previewed.|
|type|Optional. The type of test results to delete. Valid values are <strong>automated</strong>, <strong>manual</strong>, and <strong>all</strong>.|
|preview|Optional. Display the number of test results that would be deleted based on the age in days, but do not delete these results.|

### Prerequisites

To use the **deleteTestResults** command, you must be a member of the sysadmin role for the specified SQL Server instance.

### Remarks

Use the **/preview** parameter to see the test results sorted by project name and year without deleting these results.

### Example

The following example shows how to delete manual test results older than 60 days for a database named `TFS_DefaultCollection` on a SQL instance running on a server named `ContosoMain` on the named instance `TeamDatabases`.

```
TfsConfig deleteTestResults /ageInDays:60 /sqlInstance:ContosoMain\TeamDatabases /databaseName:TFS_DefaultCollection /type:manual
```

::: moniker-end

::: moniker range="<= tfs-2018"

>**Command availability:** TFS 2017 and later

You use the **DeleteTestResults** command to 
delete old stored test results from your collection store.
This is typically done to reduce the store size or to
reduce the time taken when migrating test results to a new schema.

    TFSConfig DeleteTestResults /ageInDays:{number} 
        /sqlInstance:ServerName
        /databaseName:DatabaseName
        [/type:{automated|manual|all}]
        [/preview]

<table>
  <thead>
    <tr>
      <th>Option</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><strong>/ageInDays</strong></td>
      <td>Test results older than the specified number of days will be deleted or previewed.</td>
    </tr>
    <tr>
      <td><strong>/sqlInstance</strong></td>
      <td>
        The name of the server that hosts the database for which test results are being deleted or previewed,
        and the name of the instance if an instance other than the default is used.
        If you specify an instance, you must use the format: <code>ServerName\InstanceName</code>
      </td>
    </tr>
    <tr>
      <td><strong>/databaseName</strong></td>
      <td>The name of the database for which test results are being deleted or previewed.</td>
    </tr>
    <tr>
      <td><strong>/type</strong></td>
      <td>Optional. The type of test results to delete. Valid values are <strong>automated</strong>, <strong>manual</strong>, and <strong>all</strong>.</td>
    </tr>
    <tr>
      <td><strong>/preview</strong></td>
      <td>Optional. Display the number of test results that would be deleted based on the age in days, but do not delete these results.</td>
  </tr>
  </tbody>
</table>

### Prerequisites

To use the **DeleteTestResults** command, you must be a member of the sysadmin role for the specified SQL Server instance.

### Remarks

Use the **/preview** parameter to see the test results sorted by project name and year without deleting these results. 

### Example

The following example shows how to delete manual test results older 
than 60 days for a database named TFS\_DefaultCollection on a SQL 
instance running on a server named "ContosoMain" on the named instance "TeamDatabases".

    TFSConfig deleteTestResults /ageInDays:60 /sqlInstance:ContosoMain\TeamDatabases /databaseName:TFS_DefaultCollection /type:manual

::: moniker-end
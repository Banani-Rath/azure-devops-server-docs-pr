---
ms.topic: include
---

::: moniker range="azure-devops-2019"

Use the **accounts** command to manage these Azure DevOps Server service accounts.

- the Azure DevOps Server service account
- the data sources account for SQL Server Reporting Services
- the Azure DevOps Proxy Server service account

You can also use this command to change the ownership of the Azure DevOps Server databases.

```
TfsConfig accounts /change|add|set|delete|updatepassword|resetowner
	[/accountType:<adminConsole|applicationTier|proxy|reportingDataSource>]
	[/account:<accountName>] [/password:<password>]
	[/sqlInstance:<serverName>] [/databaseName:<databaseName>] [/continue]
```

|Operation|Description|
|---|---|
|UpdatePassword|Changes the password of an account that is used as a service account. Changes the existing account and all accountTypes that run as the given account.|
|Change|Changes the account that is used as the service account. Adds the new account to necessary resources and groups, grants the required permissions, then sets the service to use it. This does not remove the old account from the resources.<br/><br/>If you do not use the **accountType** option, the service account for the application tier will be changed.|
|Add|Only adds the new account to the necessary resources. Useful for NLB scenarios. Use the continue flag if some collections are unreachable. Add can be run again later to update any missed collections. Adds an account to the groups that are required for using the account as a service account.|
|Set|Only sets the service to use an account already added to the resources.  Useful for NLB scenarios.|
|Delete|Removes the account from all resources. Precautions should be used when deleting an account since it can cause other servers to get denied service.|
|ResetOwner|If the databases are restored as part of a move, clone, or disaster recovery the database owner can switch to the admin restoring the server. This option iterates through all databases and sets the dbo login to the current owner.|

|AccountType|Description|
|---|---|
|AdminConsole|Administration Console Users are users that have been granted the minimum permissions across various resources to use the console.|
|ApplicationTier|Changes the service account on the appPool for the core web services. (TFSService)|
|Proxy|Changes the service account on the appPool for the proxy web services. (TFSProxy)|
|ReportingDataSource|Changes the account the reports use to access the reporting data. (TFSReports)|

The default value is **ApplicationTier**.

The sqlInstance and databaseName are only appropriate for use when adding an account to databases before the application tier is configured. This is primarily useful in disaster recovery scenarios where another account is needed before running the AT Only configuration wizard.

The continue option is used when adding or changing an account.  For those operations, the account is changed in each collection database. If continue is supplied, it will continue if a collection is unreachable.  It can be run again when they are reachable.

> [!NOTE]
> The accounts must be in domainName\userName format. For system accounts, you must use quotes around the full account name (for example, "NT Authority\Network Service"). System accounts do not require a password.

|Parameter|Description|
|---|---|
|Account|Specifies the name of the account that you want to add, change, or delete from a referenced account type, such as <strong>/AccountType:ApplicationTier</strong>.|
|Password|Specifies the password of the service account. This parameter is optional if you are using a system account or an account that does not have a password, such as Network Service.|
|sqlInstance|Used only with <strong>/ResetOwner</strong>.<br/><br/>Specifies the name of the server that is running SQL Server and the name of the instance if you want to use an instance other than the default instance. You must specify the name and instance in the following format:<br /><br />ServerName\InstanceName.|
|databaseName|Used only with <strong>/ResetOwner</strong>.<br/><br/>Specifies the name of the database whose ownership you want to change. By using this command, you reset the ownership of the database that you specify to the account under which you are running the command.|
|continue|Updates any groups that are not available when you run the command. This option is usually used in NLB scenarios.|

### Prerequisites

To use the **accounts** command, you must be a member of:

- the Azure DevOps Administrators security group
- the sysadmin role for all SQL Server instances that your Azure DevOps Server instance uses.

If you use the **/proxy** option, you must be an administrator on the proxy server.

For more information, see [Permission reference for Azure DevOps Server](/azure/devops/security/permissions).

### Remarks

Use the **accounts** command to automate changes to the service accounts, databases, and service account groups of Azure DevOps Server. You can configure accounts that you have already created, but you can't create accounts.

Before you change the domain or workgroup of an account, the account must have the <span sdata="langKeyword" value="Account is sensitive and cannot be delegated"> Account is sensitive and cannot be delegated </span> permission on the application-tier server. For more information, see this page on the Microsoft Web site: [Enabling Delegated Authentication](http://go.microsoft.com/fwlink/?LinkId=98742).

The **accounts** command supports on-premises Azure DevOps Server deployments. To change the account owner of a Azure DevOps Services account, see [Change account ownership](/azure/devops/accounts/change-account-ownership-vs).

### Examples

Change the service account of data sources for Reporting Services to a new account in the Contoso domain, `Contoso\NewAccount`, and the password, to `Password`.

```
TfsConfig accounts /change /AccountType:ReportingDataSource /Account:Contoso\NewAccount /Password:Password
```

Add the Network Service system account to the service account groups for Azure DevOps Server (system accounts don't have passwords).

```
TfsConfig accounts /add /AccountType:ApplicationTier /Account:"NT Authority\Network Service"
```

Change the ownership of the `TFS_Warehouse` database on the `ContosoMain` SQL Server in the `TeamDatabases` named instance to the user account under which you are running the command.

> [!NOTE]  
>You can't specify what account to set as the owner of the databases when you use this command. The owner will be set to the account under which you are running the command.

```
TfsConfig accounts /ResetOwner /SQLInstance:ContosoMain\TeamDatabases /DatabaseName:TFS_Warehouse
```

::: moniker-end

::: moniker range="<= tfs-2018"

Use the **Accounts** command to manage these TFS service accounts.
- the TFS service account
- the data sources account for SQL Server Reporting Services
- the Azure DevOps Proxy Server service account

You can also use this command to change the ownership of the Azure DevOps Server databases.

	TFSConfig Accounts /change|add|set|delete|updatepassword|resetowner
		[/AccountType:{AdminConsole|ApplicationTier|Proxy|ReportingDataSource}]
		[/Account:AccountName] [/Password:Password]
		[/SQLInstance:ServerName] [/DatabaseName:DatabaseName] [/Continue] [/usesqlalwayson]

<table>
	<thead>
		<tr>
			<th>Option</th>
			<th>Description</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td><strong>/change</strong></td>
			<td>
				Changes the account that is used as the service account.
				This option adds the account that you specify to all the necessary groups, grants it the Prerequisites if possible, and sets the service to use the account.
				If you do not use the <strong>/AccountType</strong> option with this option, the service account for the application tier will be changed.
			</td>
		</tr>
		<tr>
			<td><strong>/add</strong></td>
			<td>
				Adds an account to the groups that are required for using the account as a service account.
				This option adds the account that you specify to the necessary groups and grants it the permissions
				that are required to act as the service account (if possible).
				However, this option will not change the account that is used as the service account.
				This option is usually used in network load balancing (NLB) scenarios.
				You can use this option with /continue if some services or databases might not be available in your environment.
			</td>
		</tr>
		<tr>
			<td><strong>/set</strong></td>
			<td>
				Sets an account as the service account. This option does not add the account to any groups.
				Therefore, you must use this option only with accounts that have already been added to the required groups and have the necessary permissions.
				This option is usually used in NLB scenarios.
			</td>
		</tr>
		<tr>
			<td><strong>/delete</strong></td>
			<td>
				Removes an account from the account type that you specify.
				This option removes the account that you specify from the necessary groups and removes the permissions
				that are required to act as the service account (if possible).
				However, this option will not change the account that is used as the service account.
				Make sure that you do not use this option for an account that the servers in your deployment currently use as a service account.
			</td>
		</tr>
		<tr>
			<td><strong>/ResetOwner</strong></td>
			<td>
				Changes the ownership of the databases that Azure DevOps Server uses to the account that you are using to run this command.
				This option iterates though all the databases and sets the <strong>dbo</strong> login to the account that you are using to run this command.
				You might need to use this option when you move or restore a deployment.</td>
		</tr>
		<tr>
			<td><strong>/UpdatePassword</strong></td>
			<td>
				Changes the password of an account that is used as a service account.
				This option updates the password for the account that you specify for all services in Azure DevOps Server that use that account.
			</td>
		</tr>
		<tr>
			<td><strong>/AccountType:</strong> { AdminConsole | ApplicationTier | ReportingDataSource | Proxy }</td>
			<td>
				<ul>
                    <li><strong>AdminConsole</strong>: the group of users who have the minimum permissions that are required to open and use the administration console for Azure DevOps (AdminConsole)</li>
                    <li><strong>ApplicationTier</strong>: the service account that is used for Azure DevOps Server (TFSService)</li>
                    <li><strong>ReportingDataSource</strong>: the data sources account for Reporting Services (TFSReports)</li>
                    <li><strong>Proxy</strong>: the service account for Azure DevOps Server Proxy (TFSProxy)</li>
				</ul>
				<p>The default value is ApplicationTier.</p>
			</td>
		</tr>
		<tr>
			<td><strong>/Account:</strong> AccountName</td>
			<td>
				Specifies the name of the account that you want to add, change, or delete from a referenced account type,
				such as <strong>/AccountType:ApplicationTier</strong>.
				Specify Account in one of the following forms: Domain\AccountName or Computer\AccountName.
				If you want to use a system account, such as Network Service or Local System, use the Computer\AccountName format.
				For more information about how to specify a system account, see the usage examples later in this topic.
			</td>
		</tr>
		<tr>
			<td><strong>/Password:</strong> Password</td>
			<td>
				Specifies the password of the service account.<br /><br />
				<strong>Note:</strong> This parameter is optional if you are using a system account or an account that does not have a password, such as Network Service.
			</td>
		</tr>
		<tr>
			<td><strong>/SQLInstance:</strong> ServerName</td>
			<td>
				Used only with <strong>/ResetOwner</strong>.
				Specifies the name of the server that is running SQL Server and the name of the instance if you want to use an instance other than the default instance.
				You must specify the name and instance in the following format:<br /><br />ServerName\InstanceName.
			</td>
		</tr>
		<tr>
			<td><strong>/DatabaseName:</strong> DatabaseName</td>
			<td>
				Used only with <strong>/ResetOwner</strong>.
				Specifies the name of the database whose ownership you want to change.
				By using this command, you reset the ownership of the database that you specify to the account under which you are running the command.
			</td>
		</tr>
		<tr>
			<td><strong>/continue</strong></td>
			<td>Updates any groups that are not available when you run the command. This option is usually used in NLB scenarios.</td>
		</tr>
		<tr>
			<td><strong>/usesqlalwayson</strong></td>
			<td>
				Used only with <strong>/ResetOwner</strong> in conjunction with <strong>/SQLInstance</strong> and <strong>/DatabaseName</strong>.
				Specifies that the databases are part of an AlwaysOn Availability Group in SQL Server.
				If configured, this option sets MultiSubnetFailover in the connection string.<br /><br />
				For more information, see <a href="http://msdn.microsoft.com/library/hh510230.aspx">AlwaysOn Availability Groups (SQL Server)</a>.</td>
		</tr>
	</tbody>
</table>

### Prerequisites

To use the **Accounts** command, you must be a member of
- the Team Foundation Administrators security group
- the sysadmin role for all SQL Server instances that your Azure DevOps Server instance uses.

If you use the **/proxy** option, you must be an administrator on the proxy server.

For more information, see [Permission reference for Azure DevOps Server](/azure/devops/security/permissions)>.

### Remarks

Use the **Accounts** command to automate changes to the service accounts, databases, and service account groups of Azure DevOps Server. You can configure accounts that you have already created, but you can't create accounts.

Before you change the domain or workgroup of an account, the account must have the <span sdata="langKeyword" value="Account is sensitive and cannot be delegated"> Account is sensitive and cannot be delegated </span> permission on the application-tier server. For more information, see this page on the Microsoft Web site: [Enabling Delegated Authentication](http://go.microsoft.com/fwlink/?LinkId=98742).

The **Accounts** command supports on-premises Azure DevOps Server deployments. To change the account owner of a Azure DevOps Services account, 
see [Change account ownership](/azure/devops/accounts/change-account-ownership-vs).

### Examples

Change the service account of data sources for Reporting Services to a new account in the Contoso domain, Contoso\\NewAccount, and the password, to Password.

    TFSConfig Accounts /change /AccountType:ReportingDataSource /Account:Contoso\NewAccount /Password:Password

Add the Network Service system account to the service account groups for Azure DevOps Server. (System accounts don't have passwords.)

    TFSConfig Accounts /add /AccountType:ApplicationTier /Account:"NT Authority\Network Service"

Change the ownership of the "TFS\_Warehouse" database on the "ContosoMain" SQL Server in the "TeamDatabases" named instance to the user account under which you are running the command.

> [!NOTE]  
>You can't specify what account to set as the owner of the databases when you use this command. The owner will be set to the account under which you are running the command.

    TFSConfig Accounts /ResetOwner /SQLInstance:ContosoMain\TeamDatabases /DatabaseName:TFS_Warehouse

::: moniker-end
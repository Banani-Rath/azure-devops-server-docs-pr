---
ms.topic: include
---

::: moniker range="azure-devops-2019"

You can use the **proxy** command to update or change the settings used by Azure DevOps Proxy Server.
Azure DevOps Proxy Server provides support for distributed teams to use version control by managing a cache of downloaded version control files in the location of the distributed team.
By configuring Azure DevOps Proxy Server, you can significantly reduce the bandwidth needed across wide area connections.
In addition, you do not have to manage downloading and caching of version files; management of the files is transparent to the developer who is using the files.
Meanwhile, any metadata exchanges and file uploads continue to appear in Azure DevOps Server.
If you use the Azure DevOps Services to host your development project in the cloud, you can use the Proxy command to not only manage the cache for projects in the hosted collection, but also to manage some of the settings used by that service.

For more information about installing Azure DevOps Proxy Server and initial configuration of the proxy,
see <span sdata="link"> How to: Install Azure DevOps Proxy Server and set up a remote site </span>. For more information about configuring proxy on client computers, see [Azure DevOps Version Control Command Reference](http://go.microsoft.com/fwlink/?LinkId=254422).

```
TfsConfig proxy /add|delete|change [/Collection:<teamProjectCollectionURL> /account:<accountName>]
	/Server:<TeamFoundationServerURL> [/inputs:Key1=Value1; Key2=Value2;...] [/continue]
```

|Option|Description|
|---|---|
|add|Adds the specified server or collection to the proxy list in the Proxy.config file. You can run /add multiple times to include more collections or servers. When using /add with a collection hosted on Azure DevOps Services, you will be prompted for your credentials on Azure DevOps Services.
|change|Changes the credentials stored as the service account for Azure DevOps Services. The /change option is only used for Azure DevOps Services; it should not be used for local deployments of Azure DevOps Server.
|delete|Removes the specified server or collection from the proxy list in the Proxy.config file.|
|account|Specifies the account used as the service account for the proxy in Azure DevOps Services. This option is only used for Azure DevOps Services in conjunction with the /change option.<br/><br/>The default service account used for Azure DevOps Services is &quot;Account Service.&quot;
|continue|Continues the execution of the command even if the verification process produces warnings.|
|Collection|Specifies the URL of the project collection that is hosted on Azure DevOps Services, in `AccountName.DomainName/CollectionName` format.|
|account|Specifies the name of the account that is used as the service account for Azure DevOps Services. If the account name has spaces, the name must be enclosed within quotation marks (&quot;&quot;). All special characters in account names must be specified in accordance with command-line syntax.
|account|Specifies the URL of a Azure DevOps Server deployment, in `ServerURL:Port/tfs` format.|
|PersonalAccessTokenFile|Optionally specifies the path to a file that contains a personal access token. This token will be used authenticate to the collection or account while registering a proxy. (Added in TFS 2018 Update 1)|
|inputs|Optional. Specifies additional settings and values to use while configuring the proxy.<br/><br/>For example, values for `GvfsProjectName` and `GvfsRepositoryName` can be used to configure a Git repository for use with <a href="https://gvfs.io">Git Virtual File System</a> (GVFS) (Added in TFS 2018 Update 1)|

### Prerequisites

To use the **proxy** command, you must be a member of the Azure DevOps Administrators security group and an administrator on the proxy server. For more information, see <span sdata="link"> Permission reference for Azure DevOps Server </span>.

### Remarks

You use the **proxy** command to update the existing configuration of Azure DevOps Server Proxy. You cannot use the **proxy** command for initial installation and configuration of the proxy.

### Examples

The following example shows how to add a Azure DevOps Server deployment named `FABRIKAM` to the proxy list.

```
TfsConfig proxy /add /Server:http://www.fabrikam.com:8080/tfs 
```

The following example shows how to add a project collection hosted on Azure DevOps Services to the proxy list using a [Personal Access Token](/azure/devops/accounts/use-personal-access-tokens-to-authenticate) to authenticate. This token will be used only to register the proxy with the Azure DevOps Services account - the default service account will still be used to run the proxy. This parameter was added in TFS 2018 Update 1 to support registering a Proxy with Azure DevOps Services without requiring a login prompt.

```
TfsConfig proxy /add /Collection:https://HelenaPetersen.tfs.visualstudio.com/PhoneSaver
```

The following example shows how to add a project collection to the proxy list. This example uses a personal access token to authenticate against the collection specified with the `/Collection` parameter. The personal access token to be used is saved to a file at `c:\PersonalAccessToken.txt`.

```
TfsConfig proxy /add /Collection:https://HelenaPetersen.tfs.visualstudio.com/PhoneSaver
	/PersonalAccessTokenFile:c:\PersonalAccessToken.txt
```

The following example shows how to change the service account used by the proxy for the project collection hosted on Azure DevOps Services. The collection is named `PhoneSaver`, the account name used for Azure DevOps Services is `HelenaPetersen.fabrikam.com`, and the service account used by the proxy is being changed to `My Proxy Service Account`. Because the account name contains spaces, quotation marks are used to enclose the name.

```
TfsConfig proxy /change /Collection:https://HelenaPetersen.tfs.visualstudio.com/PhoneSaver
	/account:"My Proxy Service Account"
```

The following example shows how to add a Git repository for use with GVFS.

```
TfsConfig proxy /add /Collection:https://HelenaPetersen.tfs.visualstudio.com/PhoneSaver /inputs:GvfsProjectName=PhoneSaver;GvfsRepositoryName=AnotherRepository
```

::: moniker-end

::: moniker range="<= tfs-2018"

You can use the **TFSConfig Proxy** command to update or change the settings used by Team Foundation Server Proxy.
Team Foundation Server Proxy provides support for distributed teams to use version control by managing a cache of downloaded version control files in the location of the distributed team.
By configuring Team Foundation Server Proxy, you can significantly reduce the bandwidth needed across wide area connections.
In addition, you do not have to manage downloading and caching of version files; management of the files is transparent to the developer who is using the files.
Meanwhile, any metadata exchanges and file uploads continue to appear in Azure DevOps Server.
If you use the Azure DevOps Services to host your development project in the cloud,
you can use the Proxy command to not only manage the cache for projects in the hosted collection, but also to manage some of the settings used by that service.

For more information about installing Azure DevOps Proxy Server and initial configuration of the proxy,
see <span sdata="link"> How to: Install Azure DevOps Proxy Server and set up a remote site </span>. For more information about configuring proxy on client computers, see [Team Foundation Version Control Command Reference](http://go.microsoft.com/fwlink/?LinkId=254422).

    TFSConfig Proxy /add|delete|change [/Collection:TeamProjectCollectionURL /account:AccountName]
		/Server:TeamFoundationServerURL [/inputs:Key1=Value1; Key2=Value2;...] [/Continue]

<table>
	<thead>
		<tr>
			<th>Option</th>
			<th>Description</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td><strong>/add</strong></td>
			<td>
				Adds the specified server or collection to the proxy list in the Proxy.config file.
				You can run /add multiple times to include more collections or servers.
				When using /add with a collection hosted on Azure DevOps Services,
				you will be prompted for your credentials on Azure DevOps Services.
			</td>
		</tr>
		<tr>
			<td><strong>/change</strong></td>
			<td>
				Changes the credentials stored as the service account for Azure DevOps Services.
				The /change option is only used for Azure DevOps Services; it should not be used for local deployments of Azure DevOps Server.
			</td>
		</tr>
		<tr>
			<td><strong>/delete</strong></td>
			<td>Removes the specified server or collection from the proxy list in the Proxy.config file.</td>
		</tr>
		<tr>
			<td><strong>/account</strong></td>
			<td>
				Specifies the account used as the service account for the proxy in Azure DevOps Services.
				This option is only used for Azure DevOps Services in conjunction with the /change option.<br/><br/>
				The default service account used for Azure DevOps Services is &quot;Account Service.&quot;
			</td>
		</tr>
		<tr>
			<td><strong>/continue</strong></td>
			<td>Continues the execution of the command even if the verification process produces warnings.</td>
		</tr>
		<tr>
			<td><strong>/Collection</strong>:TeamProjectCollectionURL</td>
            <td>Specifies the URL of the project collection that is hosted on Azure DevOps Services, in <code>AccountName.DomainName/CollectionName</code> format.</td>
		</tr>
		<tr>
			<td><strong>/account</strong>:AccountName</td>
			<td>
				Specifies the name of the account that is used as the service account for Azure DevOps Services.
				If the account name has spaces, the name must be enclosed within quotation marks (&quot;&quot;).
				All special characters in account names must be specified in accordance with command-line syntax.
			</td>
		</tr>
		<tr>
			<td><strong>/account</strong>:ServerURL</td>
            <td>Specifies the URL of a Azure DevOps Server deployment, in <code>ServerURL:Port/tfs</code> format.</td>
		</tr>
		<tr>
			<td><strong>/PersonalAccessTokenFile</strong>:PathToFileWithPAT</td>
			<td>Optionally specifies the path to a file that contains a personal access token. This token will be used authenticate to the collection or account while registering a proxy. (Added in TFS 2018 Update 1)</td>
		</tr>
		<tr>
			<td><strong>/inputs</strong>:Key1=Value1;Key2=Value2;...</td>
			<td>
				Optional. Specifies additional settings and values to use while configuring the proxy.<br/><br/>
                For example, values for &quot;GvfsProjectName&quot; and &quot;GvfsRepositoryName&quot; can be used to configure a Git repository for use with <a href="https://gvfs.io">Git Virtual File System</a> (GVFS)
				(Added in TFS 2018 Update 1)
			</td>
		</tr>
	</tbody>
</table>

### Prerequisites

To use the **Proxy** command, you must be a member of the Team Foundation Administrators security group and an administrator on the proxy server. For more information, see <span sdata="link"> Permission reference for Azure DevOps Server </span>.

### Remarks

You use the **Proxy** command to update the existing configuration of Azure DevOps Proxy Server. You cannot use the Proxy command for initial installation and configuration of the proxy.

### Examples

The following example shows how to add a Azure DevOps Server deployment named FABRIKAM to the proxy list.

    TFSConfig Proxy /add /Server:http://www.fabrikam.com:8080/tfs 

The following example shows how to add a project collection hosted on Azure DevOps Services to the proxy list using a [Personal Access Token](/azure/devops/accounts/use-personal-access-tokens-to-authenticate) to authenticate. This token will be used only to register the proxy with the Azure DevOps Services account - the default service account will still be used to run the proxy. This parameter was added in TFS 2018 Update 1 to support registering a Proxy with Azure DevOps Services without requiring a login prompt.

    TFSConfig Proxy /add /Collection:https://HelenaPetersen.tfs.visualstudio.com/PhoneSaver 

The following example shows how to add a project collection to the proxy list. This example uses a personal access token to authenticate against the collection specified with the "/Collection" parameter. The personal access token to be used is saved to a file at "c:\PersonalAccessToken.txt"

    TFSConfig Proxy /add /Collection:https://HelenaPetersen.tfs.visualstudio.com/PhoneSaver
		/PersonalAccessTokenFile:c:\PersonalAccessToken.txt

The following example shows how to change the service account used by the proxy for the project collection hosted on Azure DevOps Services. The collection is named PhoneSaver, the account name used for Azure DevOps Services is HelenaPetersen.fabrikam.com, and the service account used by the proxy is being changed to "My Proxy Service Account". Because the account name contains spaces, quotation marks are used to enclose the name.

    TFSConfig Proxy /change /Collection:https://HelenaPetersen.tfs.visualstudio.com/PhoneSaver
		/account:"My Proxy Service Account"

The following example shows how to add a Git repository for use with GVFS.

    TFSConfig Proxy /add /Collection:https://HelenaPetersen.tfs.visualstudio.com/PhoneSaver /inputs:GvfsProjectName=PhoneSaver;GvfsRepositoryName=AnotherRepository

::: moniker-end
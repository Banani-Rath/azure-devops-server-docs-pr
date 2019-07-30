---
ms.topic: include
---

::: moniker range="azure-devops-2019"

The **Authentication** command changes the network authentication protocol that the Azure DevOps Server application tier or proxy website uses.

```
TFSConfig Authentication [/provider:NTLM|Negotiate] [/viewAll] [/siteType:ApplicationTier|Proxy]
```

<table>
	<thead>
		<tr>
			<th>Option</th>
			<th>Description</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td><strong>/viewAll</strong></td>
			<td>Displays the current authentication settings for Azure DevOps Server.</td>
		</tr>
		<tr>
			<td><strong>/provider</strong>: { NTLM | Negotiate }</td>
			<td>Specifies the authentication provider you want to configure for the website.
				<ul>
                    <li><strong>NTLM</strong>: Use the NTML authentication protocol</li>
                    <li><strong>Negotiate</strong>: Use the Negotiate (Kerberos) authentication protocol</li>
				</ul>
			</td>
		</tr>
		<tr>
			<td><strong>/siteType</strong></td>
			<td>Specifies the website (application tier or proxy) whose network authentication protocol you want to change. The application tier is the default.</td>
		</tr>
	</tbody>
</table>

### Prerequisites

To use the **Authentication** command, you must be a member of the Azure DevOps Administrators security group and a local administrator on the application-tier server or proxy server, depending on the value of the **siteType** option.

### Remarks

The **Authentication** command is used by an administrator who wants to change the network authentication protocol for one or more websites on which Azure DevOps Server relies.
The administrator runs this command from the application tier to update those websites that require a change in their network authentication protocol.
The command changes the **NTAuthenticationProviders** property in the IIS metabase.

Before you use the <strong>Authentication</strong> command to change the authentication protocol, you can run the command with the <strong>/viewAll</strong> option to see what the existing settings are.

### Example

The following example displays the current value that is assigned for the network authentication protocol.

```
TFSConfig Authentication /viewAll
```

::: moniker-end

::: moniker range="<= tfs-2018"

The **Authentication** command changes the network authentication protocol that the TFS application tier or proxy website uses.

	TFSConfig Authentication [/provider:NTLM|Negotiate] [/viewAll] [/siteType:ApplicationTier|Proxy]

<table>
	<thead>
		<tr>
			<th>Option</th>
			<th>Description</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td><strong>/viewAll</strong></td>
			<td>Displays the current authentication settings for Azure DevOps Server.</td>
		</tr>
		<tr>
			<td><strong>/provider</strong>: { NTLM | Negotiate }</td>
			<td>Specifies the authentication provider you want to configure for the website.
				<ul>
                    <li><strong>NTLM</strong>: Use the NTML authentication protocol</li>
                    <li><strong>Negotiate</strong>: Use the Negotiate (Kerberos) authentication protocol</li>
				</ul>
			</td>
		</tr>
		<tr>
			<td><strong>/siteType</strong></td>
			<td>Specifies the website (application tier or proxy) whose network authentication protocol you want to change. The application tier is the default.</td>
		</tr>
	</tbody>
</table>

### Prerequisites

To use the **Authentication** command, you must be a member of the Team Foundation Administrators security group 
and a local administrator on the application-tier server or proxy server, depending on the value of the **siteType**
option. 

### Remarks

The **Authentication** command is used by an administrator who wants to change the network authentication protocol for one or more websites on which Azure DevOps Server relies.
The administrator runs this command from the application tier to update those websites that require a change in their network authentication protocol.
The command changes the **NTAuthenticationProviders** property in the IIS metabase.

Before you use the <strong>Authentication</strong> command to change the authentication protocol, you can run the command with the <strong>/viewAll</strong> option to see what the existing settings are.

### Example

The following example displays the current value that is assigned for the network authentication protocol.

    TFSConfig Authentication /viewAll

::: moniker-end
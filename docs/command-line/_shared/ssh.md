---
ms.topic: include
---

::: moniker range="azure-devops-2019"

You can use the **ssh** command to regenerate the SSH server host key, get the server key fingerprint or enable/disable the SSH service on Azure DevOps Server deployment.

```
TfsConfig ssh {/regenerateKey | /getKeyFingerprint | /enable | /disable}
```

|Option|Description|
|---|---|
|regenerateKey|Required if <strong>/GetKeyFingerprint</strong> or <strong>/Enable</strong> or <strong>/Disable</strong> is not used. Generates SSH server host key and updates it in the database. The command will replace the old key, if there is any, for the current Azure DevOps deployment.|
|getKeyFingerprint|Required if <strong>/RegenerateKey</strong> or <strong>/Enable</strong> or <strong>/Disable</strong> is not used. Specifies the SSH server host key fingerprint from the current Azure DevOps deployment.|
|enable|Required if <strong>/RegenerateKey</strong> or <strong>/GetKeyFingerprint</strong> or <strong>/Enable</strong> is not used. Enables SSH service for the current Azure DevOps deployment.
> [!TIP]
> The SSH service is installed when Application Tier is configured. The <strong>/Enable</strong> option will only enable SSH service by starting it on all the Application Tier nodes.
|disable|Required if <strong>/RegenerateKey</strong> or <strong>/GetKeyFingerprint</strong> or <strong>/Disable</strong> is not used. Disables SSH service for the current Azure DevOps Server deployment.
> [!TIP]
> The SSH service is uninstalled when Applciation Tier is configured. The <strong>/Disable</strong> option will only disable SSH service by stopping it on all the Application Tier nodes.|

### Prerequisites

To use the **ssh** command, you must be a member of the Team Foundation Administrators security group as well as the local Administrators group on the machine running **TFSConfig**.
You must also be a member of the sysadmin security role for all the SQL Server instances used by the Azure DevOps Server deployment.

For more information, see [Permission reference for Azure DevOps Server](/azure/devops/security/permissions).

### Remarks

The **ssh** command is used by an administrator who wants to update the existing SSH server host key or look up the existing key fingerprint.
The **/Enable** and **/Disable** options enable or disable the SSH service on each Application Tier in the Azure DevOps deployment.

### Examples

To regenerate the SSH server host key.

```
TfsConfig ssh /regenerate
```

To get the existing key fingerprint.

```
TfsConfig ssh /getKeyFingerprint
```

To enable the SSH service on all the application tiers.

```
TfsConfig ssh /enable
```

To disable the SSH service on all the application tiers.

```
TfsConfig ssh /disable
```

::: moniker-end

::: moniker range="<= tfs-2018"

>**Command availability:** TFS 2016

You can use the **ssh** command to regenerate the SSH server host key, get the server key fingerprint or enable/disable the SSH service on Azure DevOps Server deployment.

    TFSConfig SSH {/RegenerateKey | /GetKeyFingerprint | /Enable | /Disable} 

### Parameters

<table>
    <thead>
        <tr>
            <th>Option</th>
            <th>Description</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td><strong>/RegenerateKey</strong></td>
            <td>
                Required if <strong>/GetKeyFingerprint</strong> or <strong>/Enable</strong> or <strong>/Disable</strong> is not used.
                Generates SSH server host key and updates it in the database. The command will replace the old key, if there is any, for the current Azure DevOps Server deployment.<br/>            </td>
        </tr>
        <tr>
            <td><strong>/GetKeyFingerprint</strong></td>
            <td>
                Required if <strong>/RegenerateKey</strong> or <strong>/Enable</strong> or <strong>/Disable</strong> is not used.
                Specifies the SSH server host key fingerprint from the current Azure DevOps Server deployment. 
            </td>
        </tr>
        <tr>
            <td><strong>/Enable</strong></td>
            <td>
                Required if <strong>/RegenerateKey</strong> or <strong>/GetKeyFingerprint</strong> or <strong>/Enable</strong> is not used.
                Enables SSH service for the current Azure DevOps Server deployment.<br /><br />
                <strong>Tip:</strong> The SSH service is installed when Application Tier is configured. The <strong>/Enable</strong> option will only enable SSH service by starting it on all the Application Tier nodes. 
            </td>
        </tr>
        <tr>
            <td><strong>/Disable</strong></td>
            <td>
                Required if <strong>/RegenerateKey</strong> or <strong>/GetKeyFingerprint</strong> or <strong>/Disable</strong> is not used.
                Disables SSH service for the current Azure DevOps Server deployment.<br /><br />
                <strong>Tip:</strong> The SSH service is uninstalled when Applciation Tier is configured. The <strong>/Disable</strong> option will only disable SSH service by stopping it on all the Application Tier nodes.
            </td>
        </tr>
    </tbody>
</table>

### Prerequisites

To use the **SSH** command, you must be a member of the Team Foundation Administrators security group as well as the local Administrators group on the machine running **TFSConfig**. 
You must also be a member of the sysadmin security role for all the SQL Server instances used by the Azure DevOps Server deployment. 

For more information, see [Permission reference for Azure DevOps Server](/azure/devops/security/permissions).

### Remarks

The **SSH** command is used by an administrator who wants to update the existing SSH server host key or look up the existing key fingerprint. 
The **/Enable** and **/Disable** options enable or disable the SSH service on each Application Tier in the Azure DevOps Server deployment.

### Examples

To Regenerate the SSH server host key

    TFSConfig Ssh /Regenerate

To get the existing key fingerprint

    TFSConfig Ssh /GetKeyFingerprint

To Enable the SSH service on all the application tiers

    TFSConfig Ssh /Enable

To Disable the SSH service on all the application tiers

    TFSConfig Ssh /Disable

::: moniker-end
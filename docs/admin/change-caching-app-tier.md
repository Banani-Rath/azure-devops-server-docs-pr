---
title: Cache settings for an app-tier server
titleSuffix: Azure DevOps Server
description: Change cache settings for an application-tier server in Azure DevOps Server
ms.topic: conceptual
ms.manager: jillfra
ms.author: aaronha
author: aaronhallberg
ms.date: 04/25/2019
ms.prod: devops-server
ms.technology: tfs-admin
---

# Change cache settings for an application-tier server

[!INCLUDE [temp](../_shared/version-tfs-all-versions.md)]

You can help increase or balance performance in your deployment of Azure DevOps Server by changing the settings of the cache for files that are under version control on the application-tier server. By default, this cache is enabled so that users can download files quickly from the cache, rather than directly from the database. As an administrator, you can change the settings of this cache any time.

-   [Specify a different cache root folder](#specify-diff-cache-root)  
-   [Change the limit at which old files are removed from the cache](#change-limit-old-files)

You can do these tasks by editing the *web.config* file for version control, which is located in the installation directory on the application-tier server.

> [!NOTE]
> By default, the installation directory for the application tier is *%programfiles%*\Azure DevOps Server 2019\Application Tier\Web Services.

## Prerequisites  

To perform these procedures, you must be a member of the **Administrators** security group on the application-tier server for Azure DevOps.

For more information, see [User Account Control](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc772207(v=ws.10)).

<a name="specify-diff-cache-root"></a>
## Specify a different cache root folder

1.  On the application-tier server, create a cache folder.

    You can create the folder on a local disk, in the UNC path, or on a mounted drive. For example, you might create the following folder:

    *d:\\temp\\cacheroot*

    > [!IMPORTANT]
    > The cache folder stores sensitive information that is not encrypted. Therefore, you should make sure that only the service account of the application tier (*TFSService*) has **Modify** permissions to this folder.

2.  Open the shortcut menu for the folder, and then select **Properties**.

    The **Properties** dialog box for the folder opens.

3.  On the **Security** tab, select **Edit**.

    The **Permissions** dialog box opens.

4.  Select **Add**.

    The **Select Users, Computers, or Groups** dialog box opens.

5.  Add the local group **TFS\_APPTIER\_SERVICE\_WPG**, and then select **OK**.

6.  Select the **Modify** check box, clear all other check boxes, and then select **OK**.

7.  In Windows Explorer (or File Explorer), browse to *%programfiles%*\\Azure DevOps Server 2019\\Application Tier\\Web Services.

8.  Open the *web.config* file in a text or XML editor, and then locate the `<appSettings>` section.

9.  Add a line to the `appSettings` section to point to the folder that you just created:

        <add key="dataDirectory" value="NewCacheRootFolderLocation" />

    For example, you would add the following line if you created a cache root folder that is named *cacheroot* in the temp directory of a hard drive, as in the earlier example:

        <add key="dataDirectory" value="d:\temp\cacheroot" />

10. Save and close the *web.config* file.

    > [!NOTE]
    > To maximize performance, copy the files from the old cache folder to the new cache folder.

11. Open a Command Prompt window, enter **iisreset**, and then press ENTER.

12. Delete the old cache root folder.

    > [!NOTE]
    > By default, the cache root folder is located at *%programfiles%*\Azure DevOps Server 2019\Version Control Proxy\Web Services\VersionControlProxy\Data.


## Change limits for removing files from the cache

You can change the maximum limit on the amount of storage space that the application-tier server can use for caching files. When this limit is reached, a cleanup routine makes room for newly requested files by deleting the files with the oldest access times.

<a name="change-limit-old-files"></a>
### Change the limit at which old files are removed from the cache

1.  On the application-tier server, open Windows Explorer (or File Explorer), and browse to *\\%programfiles%*\\Azure DevOps Server 2019\\Application Tier\\Web Services.

2.  Open the *web.config* file in a text or XML editor, and then locate the `\<appSettings\>` element.

3.  Add one of the following elements:

    -   To specify a percentage of available disk space to fill before old files are removed, add the `PercentageBasedPolicy` element. You must specify a whole number as the value of this element.

        For example, the following line specifies that the cache should fill up to 60% capacity of available disk space before old files are removed:

            <add key="PercentageBasedPolicy" value="60" />

    -   To specify a fixed size in MB for the cache to reach before old files are removed, add the `FixedSizeBasedPolicy` element. You must specify a whole number as the value of this element.

        For example, the following line specifies that the cache should reach 500 MB before old files are removed:

            <add key="FixedSizeBasedPolicy" value="500" />

        > [!NOTE]
		> If both the `FixedSizeBasedPolicy` and `PercentageBasedPolicy` elements are specified, the value of the `FixedSizeBasedPolicy` element is used instead of the value of the `PercentageBasedPolicy` element.

4.  Save and close the *web.config* file.

5.  Open a Command Prompt window, enter **iisreset**, and then press ENTER.

### Change the amount of cache to free when removing old files

1.  On the application-tier server, open Windows Explorer (or File Explorer), and browse to *%programfiles%*\\Azure DevOps Server 2019\\Application Tier\\Web Services\\.

2.  Open the *web.config* file in a text or XML editor, locate the `<appSettings>` element, and then add the `CacheDeletionPercent` element.

    For example, the following line specifies to free 50% of the cache when removing old files:

        <add key="CacheDeletionPercent" value="50" />

3.  Save and close the *web.config* file.

4.  Open a Command Prompt window, enter **iisreset**, and then press ENTER.

## Related article

- [Service accounts and dependencies in Azure DevOps Server](service-accounts-dependencies.md) 
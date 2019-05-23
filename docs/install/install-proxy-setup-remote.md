---
title: How to install Azure DevOps Proxy Server
titleSuffix: Azure DevOps Server
description: How to Install Azure DevOps Proxy Server and set up a remote site
ms.manager: jillfra
ms.author: aaronha
author: aaronhallberg
ms.topic: conceptual
ms.prod: devops-server
ms.technology: tfs-admin
monikerRange: '>=tfs-2013'
ms.date: 05/14/2019
---

# How to install Azure DevOps Proxy Server and set up a remote site

[!INCLUDE [temp](../_shared/version-tfs-all-versions.md)]

If you have developers at a remote site who are sharing code with developers at the main site, you might save bandwidth by caching version control files at the remote location. Azure DevOps Proxy Server distributes popular version control files from its cache at the remote site, rather than having multiple developers from the remote site each download the same file from the main site. Your team at the remote site works like they always have, without managing which version control files get loaded into the cache.

To set this up, you install and configure the proxy server at the remote site, connect the proxy server to the application tier, and then connect the version control feature of Team Explorer to the proxy. Before you can start to cache files at the remote site, you must add the service account for the proxy server to Azure DevOps Server at the main site.

![Azure DevOps Proxy Server](_img/ic588492.png)  

## Cache version control files at a remote site

| | Task | Detailed instructions |
| --- | --- | --- |
| ![Step 1](_img/ic646324.png) | **Check for supported hardware and software**. Verify that the operating system meets requirements for Azure DevOps Proxy Server and that the hardware can run it. | [System requirements for Azure DevOps Proxy Server](../requirements.md#proxy-server) |
| ![Step 2](_img/ic646325.png) | **Set up Azure DevOps Proxy Server**. Install Azure DevOps Proxy Server. After the installation is finished, use the Azure DevOps Server Configuration Center to configure your proxy server. | [Run Azure DevOps Server installation](install-2013/install-tfs.md#installer) <br/> [How to: Configure Azure DevOps Proxy Server Using the Azure DevOps Server Configuration Center](#config--proxy-with-config-tool) |
| ![Step 3](_img/ic646326.png) | **Connect Team Explorer to Azure DevOps Proxy Server**. After you configure the proxy server to connect to Azure DevOps Server, you must configure Team Explorer to access version control files through the proxy server. | [How to: Configure Team Foundation version control to use Proxy server](#config-to-use-proxy) |


<a name="config--proxy-with-config-tool"></a>
## Configure Azure DevOps Proxy Server

You can use the following procedure to configure Azure DevOps Proxy Server with the Azure DevOps Server Configuration Center.

> [!NOTE]  
>You can access the Azure DevOps Server Configuration Center from the **Start** menu by launching Azure DevOps Server Administration Console, selecting **Proxy Server**, and then selecting **Configure Installed Features**.

### Prerequisites

To follow this procedure, you must have the following permission levels:

- Membership in the Administrators security group on the server on which you are configuring Azure DevOps Proxy Server. 
- Membership in the Project Collection Administrators group on Azure DevOps Server. 
- For Azure DevOps Services you either need to be a collection admin, or have manage proxy permissions on the Proxy namespace. You can grant proxy permissions using:

    ```
    tfssecurity /a+ Proxy Proxy Manage <user account> ALLOW /collection:{collection url}
    ```
    
    > [!NOTE]
    > You must have a proxy server at TFS Update 2 or newer to use the preceding command.

To configure Azure DevOps Proxy Server, you must have Azure DevOps Server installed on a server operating system. For more information, see [System requirements for Azure DevOps Server](../requirements.md).

### Configure Azure DevOps Proxy Server by using the Azure DevOps Server Configuration Center

To configure Azure DevOps Proxy Server by using the Azure DevOps Server Configuration Center, follow these steps:

1.  Select **Configure Azure DevOps Proxy Server**, and then select **Start Wizard**.

    The **Azure DevOps Proxy Server Configuration** wizard appears.

2.  Read the Welcome screen, and then select **Next**. If you had a version of TFS 2013 proxy (this feature only works with TFS 2013 proxy and forward) set up on this server, you're prompted to restore your settings. If you want to configure this proxy server with different resources, select **No** and move on to the next step. If you want to connect the proxy to the same Azure DevOps Server servers, select **Yes**. Azure DevOps Server will attempt to authenticate. If Azure DevOps Server successfully authenticates all endpoints, skip to step 4.

    If there is a problem with one or more endpoints, you have the following troubleshooting options for each failed connection:

    -   **Connect**: Use this option to manually authenticate endpoints. Manual authentication is a good place to start with any failed connection.

    -   **Skip**: Use this option to skip authentication. Skip is useful when you don't yet have the password to authenticate this endpoint, and you want to save the connection information for another try later.

    -   **Remove**: Use this option to completely remove the endpoint.

	> [!TIP]  
	> For more details about these options, see this [blog post](http://blogs.msdn.com/b/tfsao/archive/2013/06/27/how-to-verify-skipped-proxy-endpoints.aspx).

3.  Select **Browse**, and then select the project collection to which you want this proxy server to connect. Select **Next**.

	> [!NOTE]  
	> If your project collection is on Azure DevOps Services, you're prompted to authenticate. Enter the Microsoft account you used to set up the service.

4.  Under **Service Account**, select **Use a system account** to use Network Service or **Use a user account** to use a domain or local account. If you are using a user account, you must enter the password. To test the user account and password combination, select **Test.**

    Network Service is the default value for the proxy server service account.

5.  The following optional configurations appear under **Advanced Configuration**:
    - If you're connected to the hosted service, **Account Name** appears here.

        When you created the instance of Azure DevOps Server on the hosted service, Account Name was automatically created for you. This account will be added to the **Project Collection Proxy Service Accounts** group on the hosted service. To use a different account, enter the account name and select **Test**. 

        To reset to the default service account automatically created for you, select **Reset to default service account**. *This is no longer applicable for Azure DevOps Server 2017 Update 2 and newer proxy servers.*

    -   You can change authentication settings. Under **Authentication Method**, select **NTLM** to use NTLM authentication, or **Negotiate (Kerberos)** to first attempt Kerberos authentication, which is the more secure option, and if that fails, fall back to NTLM.

        NTLM is the default value.

6.  Select **Next**.

7.  In **Port**, accept the default value of 8081 or enter a different listener port number for incoming connections to Azure DevOps Proxy Server.

    8081 is the default value.

8.  In **Cache Root Directory**, accept the default value, or enter the path of a different location in which to store cache files.

    The default value is *Drive*:\\Program Files\\TFS 12.0\\Version Control Proxy\\ \_tfs\_data

    *Drive* is the letter of the drive on which you want to store cache files. You can specify a mapped network drive.

9.  Select **Next**.

10. On the Review page, review the settings, and then select **Next**.

    The wizard validates your configuration.

11. Select **Configure** for the wizard to apply configuration settings.

12. Select **Next** on the success screen to read the detailed results on the next success screen. You will also find a link to a log on this screen that contains the results of the configuration.

13. Select **Close** twice and the Azure DevOps Server Administration Console will appear.

<a name="config-to-use-proxy"></a>
## Configure Team Foundation version control

You can configure Team Foundation version control to use a proxy server, which caches copies of version control files in the location of a distributed team. You may reduce bandwidth requirements for remote developers by using a proxy server.

To follow this procedure, you must be a member of the Users security group on the computer on which you are configuring Team Explorer. 

To configure Team Explorer to use Azure DevOps Proxy Server:

0. Launch Visual Studio.

1. On the **Tools** menu, select **Options**.

2. In the **Options** dialog box, expand **Source Control**, and then select **Plug-in Selection**. 

3. For **Current source control plug-in**, ensure the value is **Visual Studio Team Foundation Server**.

4. Under **Source Control**, select **Visual Studio Team Foundation Server**.

5. Select the **Use proxy server for file downloads** check box.

6. In the **Proxy server name** box, enter the name of the server running Azure DevOps Proxy Server.

7. In the **Port** box, enter the listener port for Azure DevOps Proxy Server. By default, Azure DevOps Proxy Server listens for client requests on port 8081.



## Q&A

### Q: Is the proxy server backward compatible with previous versions of TFS?

**A**: Yes. The proxy server is fully compatible with TFS 2010 and TFS 2012. In fact, TFS Proxy 2010, TFS Proxy 2012, and the proxy server are fully compatible with one another in any combination. For example, you can use TFS Proxy 2010 with the proxy server or vice versa.

### Q: Does any version of Azure DevOps Proxy Server have cache cleanup improvements to support disks larger than 1 TB?

**A**: Yes. The proxy server has cache cleanup improvements to support large disks.

### Q: Does the proxy server have corruption detection logic?

**A**: Yes. If a cached file becomes corrupted on a disk after it was stored, the proxy server has logic to detect the corruption.

### Q: Does the proxy server fully support caching against dev.azure.com?

**A**: Yes.

### Q: What happens to the proxy cache when I upgrade from one version of Azure DevOps Proxy Server to another?

**A**: If you upgrade from an earlier version of Azure DevOps Proxy Server or TFS Proxy server, the cache is preserved during upgrade.  You will be able to continue accessing Azure DevOps Server from remote locations right away, without any performance impact, because Azure DevOps Server will not need to recreate or repopulate the cache.
 

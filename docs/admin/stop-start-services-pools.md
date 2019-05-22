---
title: Stop and start services, application pools, and websites
titleSuffix: Azure DevOps Server
description: Stop and start services, application pools, and websites
ms.topic: conceptual
ms.manager: jillfra
ms.author: aaronha
author: aaronhallberg
ms.date: 04/25/2019
ms.prod: devops-server
ms.technology: tfs-admin
---

# Stop and start services, application pools, and websites

[!INCLUDE [temp](../_shared/version-tfs-all-versions.md)]

For Azure DevOps Server to operate correctly, all required services, application pools, and web sites must be running on the appropriate server(s). In single-server deployments, each component must run on the server that runs Azure DevOps Server. In multiple-server deployments, each component runs on the appropriate server. In addition, you may need to stop an element to perform a particular task, such as moving your deployment to a different set of hardware.

For operations such as backing up or restoring databases, you can run the [TFSServiceControl command](../command-line/tfsservicecontrol-cmd.md) to start or stop all Azure DevOps Server services and application pools.

## Stop or start a service, application pool, or web site

1.  If you’re not a member of the **Administrators** group on the server that hosts the service, application pool, or web site that you want to manage, get added now. For more information, see [Set administrator permissions for Azure DevOps Server](add-administrator.md).

2.  Log on to the server that hosts the service, application pool, or web site.

3.  Open **Computer Management**.

4.  In the navigation pane, expand **Services and Applications**.

5.  Perform one of the following actions, depending on the element to stop or start:

    -   For a service, open the navigation menu for the service, and then select **Stop** or **Start**.
    -   For an application pool, open **Internet Information Services (IIS) Manager**, expand the local computer and open **Application Pools**. Open the navigation menu and select **Stop** or **Start**.
    -   For a web site, open **Internet Information Services (IIS) Manager**, expand the local computer, and open **Web Sites** or **Sites**. Open the navigation menu and then select **Stop** or **Start**.

## Location of services, application pools, and web sites

The following table lists the server on which each service, application pool, and web site must be running. The Name column lists the display name for each element with service names in parentheses. The services vary depending on which features of Azure DevOps you have installed.

| Element | Location | Name |
| --- | --- | --- |
| Services | Application-tier server | Code Coverage Analysis Service </br> Internet Information Services Administration Service (IISADMIN) </br> HTTP SSL (HTTPFilter) </br> Visual Studio Team Foundation Build (VSTFBUILD) (only when Team Foundation Build is installed) </br> Visual Studio Team Foundation Background Job Agent (TFSJobAgent) </br> World Wide Web Publishing Service (W3SVC) |
| . | Server that hosts the databases for Azure DevOps | SQL Server (<em>TFSINSTANCE</em>) </br> SQL Server Agent (<em>TFSINSTANCE</em>) (SQLSERVERAGENT) |
| . | Server that hosts SQL Server Reporting Services | IIS Admin Service (IISADMIN) </br> HTTP SSL (HTTPFilter) </br> SQL Server Reporting Services (<em>TFSINSTANCE</em>) (ReportServer) </br> World Wide Web Publishing Service (W3SVC) |
| . | Server that hosts SQL Server Analysis Services | SQL Server Analysis Services |
| . | Server that hosts SharePoint Products  | Internet Information Services Administration (IISADMIN) </br> HTTP SSL (HTTPFilter) </br> Windows SharePoint Services Timer (SPTimer) </br> World Wide Web Publishing Service (W3SVC) |
| Application pools | Application-tier server | Azure DevOps Server Application Pool </br> Azure DevOps Proxy Server Application Pool (only when Azure DevOps Proxy Server is installed) |
| . | Server that hosts SharePoint Products | DefaultAppPool (used by the Project portal) </br> **Note**: The name may vary based on how SharePoint Products was installed. </br> SharePoint Central Administration v3 |
| Web sites | Application-tier server | Azure DevOps Server </br> Azure DevOps Proxy Server (only if Azure DevOps Proxy Server is installed) |
| . | Server that hosts SharePoint Products | Default web site or Team web site </br> **Note**: The name may vary based on how SharePoint Products was installed. </br> SharePoint Central Administration v3 |</tbody>


## Q & A

**Q: Which service account supports each service?**

**A:** See [Service accounts and dependencies in Azure DevOps Server](service-accounts-dependencies.md).

**Q: Are there additional services that Azure DevOps Server supports?**

**A:** Yes, Azure DevOps Server includes a set of web services and application-level services See [Azure DevOps Server architecture](../architecture/architecture.md).

**Q: What services depend on service accounts?**

**A:** See [Service accounts and dependencies in Azure DevOps Server](service-accounts-dependencies.md).

**Q: How do I change the Azure DevOps Server service account or password?**

**A:** See [Change the service account or password for Azure DevOps Server](change-service-account-password.md).

**Q: How do I change the service account or password for SQL Server Reporting Service?**

**A:** See [Change the service account or password for SQL Server Reporting Services](change-service-account-or-password-sql-reporting.md).

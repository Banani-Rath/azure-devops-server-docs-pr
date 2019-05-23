---
title: Ports required for installation 
titleSuffix: Azure DevOps Server
description: Ports required for installation of Azure DevOps Server
ms.manager: jillfra
ms.author: aaronha
author: aaronhallberg
ms.topic: conceptual
ms.date: 03/25/2019
ms.prod: devops-server
ms.technology: tfs-admin
---

# Ports required for Azure DevOps Server

[!INCLUDE [temp](../_shared/version-tfs-all-versions.md)]

Your firewall controls network ports, but Azure DevOps Server requires port access. You must ensure that your firewall does not block Azure DevOps Server from the ports it requires. 

## Firewalls

If you are using Windows Firewall and it is configured to allow exceptions, the installation wizard for Azure DevOps Server opens the ports that Azure DevOps Server requires. If Windows Firewall is configured not to allow exceptions, you should configure it to allow exceptions during the installation of Azure DevOps Server. Otherwise, you'll have to manually open the ports that Azure DevOps Server requires. For more information, see [How to configure Windows Firewall on a single computer](/sql/database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access?view=sql-server-2017).

If you are using some other firewall product, you should check its documentation to determine how to open the ports that Azure DevOps Server requires.

## Required ports for SQL Server

The following table specifies the TCP ports that SQL Server requires.

|**Server or Application Context**|**TCP Port**|
|---|---|
|SQL Service (Database Engine)|1433¹|
|SQL Browser Service (Database Engine)|1434|
|SQL Server Analysis Services Redirector |2382|
|SQL Server Analysis Services|2383|
|SQL Server Reporting Services|80|

¹ SQL Server uses port 1433 for the default instance. For named instances, SQL Server uses a dynamic port that the operating system assigns. Use SQL Server Configuration Manger to determine the SQL Server port number for any named instances. For more information, see this page on the Microsoft website: [Configuring the Windows Firewall to allow SQL Server access](/sql/sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access).

**Report Server port requirements**

You must ensure that the report server contains an exception in Windows Firewall for Windows Management Instrumentation (WMI) if the report server is not on the server that is running Azure DevOps Server. The instructions for completing this task differ based on the operating system that you are using. If you are using Windows Server 2003 or Windows Server 2003 R2, see [Connecting through Windows Firewall](/windows/desktop/WmiSdk/connecting-to-wmi-remotely-with-vbscript). If you are using Windows Server 2008, Windows Server 2008 R2, Windows Vista, or Windows 7, see [Connecting to WMI remotely starting with Windows Vista](/windows/desktop/WmiSdk/connecting-to-wmi-remotely-starting-with-vista).

::: moniker range="<= tfs-2017"
## Required ports for SharePoint Products

The table in this section specifies the TCP ports that SharePoint Foundation uses if it is installed by the installation wizard for Azure DevOps Server. 

These port numbers might be different for existing deployments of SharePoint Products. You can determine which port numbers SharePoint Products uses by opening Internet Information Services (IIS) Manager and looking at the properties of the websites. For more information, see [Verify SharePoint Products for Azure DevOps Server](../install/sharepoint/verify-sharepoint.md).


| **Server or Application Context** | **TCP Port** |
|-----------------------------------|--------------|
|          Default website          |      80      |
| SharePoint Central Administration |    17012     |

::: moniker-end

## Required ports for Azure DevOps Server

By default, Azure DevOps Server uses the following TCP ports:

|**Server or Application Context**|**TCP Port**|
|---|---|
|Azure DevOps Server|8080|
|Azure DevOps Proxy Server|8081|

::: moniker range="<= tfs-2015"
## Required ports for Release Management for Visual Studio 2013

By default, Release Management Server uses the following TCP port:


| **Server or Application Context** | **TCP Port** |
|-----------------------------------|--------------|
|     Release Management Server     |     1000     |

::: moniker-end

## Related articles

- [Install Azure DevOps Server](../install/install-2013/install-tfs.md) 
- [How to: Create an Azure DevOps Server farm (high availability)](../install/create-tfs-farm.md) 
- [Azure DevOps Server upgrade requirements](../upgrade/upgrade-2013/upgrade-2013-requirements.md) 
- [How to: Install Azure DevOps Proxy Server and set up a remote site](../install/install-proxy-setup-remote.md) 
- [Install Release Management for Visual Studio 2013](/previous-versions/visualstudio/visual-studio-2013/dn593700(v=vs.120)) 

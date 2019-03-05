---
title: Look up version compatibility for Azure DevOps clients
titleSuffix: Azure DevOps  
description: Describes compatibility between Azure DevOps servers and client versions, browsers, and build agents and controllers
ms.prod: devops-server
ms.technology: tfs-admin
toc: show
ms.manager: jillfra
ms.author: aaronha
author: aaronhallberg
ms.topic: conceptual
monikerRange: '>= tfs-2013'
ms.date: 03/05/2019
---

# Azure DevOps client compatibility 

[!INCLUDE [temp](_shared/version-tfs-all-versions.md)]

A number of tools and clients connect to Azure DevOps Services and the on-premises platform, Azure DevOps Server, previously named Visual Studio Team Foundation Server (TFS). Here you can learn which versions of browsers and clients can interface with Azure DevOps, as well as the on-premises Azure DevOps build server.  

To learn more about supported clients, see [Which tools and clients connect to Azure DevOps](/azure/devops/user-guide/tools).


<a name="supported-browsers"></a>
## Web portal supported browsers

To connect with the web portal, you can use the following browsers with Azure DevOps Services and Azure DevOps on-premises. Edge, Firefox, and Chrome automatically update themselves, 
so Azure DevOps supports the most recent version.


> [!div class="mx-tdCol2BreakAll"]
> |Version                 | Edge        | Internet Explorer | Safari (Mac)   | Firefox     | Chrome|
> |--------------------------|-------------|-------------------|----------------|-------------|-------------|
> |Azure DevOps Services<br/>Azure DevOps Server 2019<br/>TFS 2018<br/>TFS 2017  | Most recent | 11 and later | 9.1 and later  | Most recent | Most recent|
> |TFS 2015                  | Most recent | 9 and later       | 5 and later    | Most recent | Most recent|
> |TFS 2013                  |             | 9 and later       | 5 and later    | Most recent | Most recent|

<a name="client-compatibility"></a>
## Visual Studio and Team Explorer 

There are three levels of client support for different versions of Visual Studio and Team Explorer. 
Only the latest version has full compatibility with the latest Azure DevOps on-premises server because it's the only client:

- That includes components that can interface with new features for that release.
- You can use to run certain administrative tasks such as creating new projects.

Previous versions have varying levels of support based on how old they are.

The following table describes the level of support that's guaranteed with each client version. Additional functionality other than what's listed here might continue to work if you use older clients. It often does work, but it's outside the scope of what's officially tested and supported.

<!--- TODO: Add Visual Studio 2019 when it GAs  --> 
> [!div class="mx-tdCol2BreakAll"]
> |Visual Studio/Team Explorer | Azure DevOps Services<br/>Azure DevOps Server 2019<br/>TFS 2018<br/>TFS 2017, and  support notes | TFS 2015 support notes   | TFS 2013 support notes   | TFS 2012 support notes  | TFS 2010 support notes |
> |-------------------------------------|---------------------------------------------------------------------------|---------------------------------------------------------------------------|---------------------------------------------------------------------------------|------------------------------------------------------------------------|------------------------------------------------|
> |Visual Studio 2017                   | Full support                                                              | High level of support                                                     | High level of support                                                           | High level of support                                                  | High level of support|
> |Visual Studio 2015                   | High level of support                                                     | Full support                                                              | High level of support                                                           | High level of support                                                  | High level of support|
> |Visual Studio/Team Explorer 2013     | General support                                                           | High level of support                                                     | Full support                                                                    | High level of support                                                  | High level of support|
> |Visual Studio/Team Explorer 2012     | General support. Supports Git with Visual Studio Tools for Git extension. | General support. Supports Git with Visual Studio Tools for Git extension. | High level of support. Supports Git with Visual Studio Tools for Git extension. | Full support. Supports Git with Visual Studio Tools for Git extension. | High level of support|
> |Visual Studio/Team Explorer 2010     | General support (SP1 and Compatibility GDR)                                      | General support (SP1 and Compatibility GDR)                                      | General support (SP1 and Compatibility GDR)                                            | High level of support (SP1 and Compatibility GDR)                             | Full support (SP1 and Compatibility GDR)|
> |Visual Studio/Team Explorer 2008     | Version control available by using MSSCCI provider                           | Version control available by using MSSCCI provider                           | Version control available by using MSSCCI provider                                 | Version control available by using MSSCCI provider                        | Version control available by using MSSCCI provider|
> |Visual Studio 2005                   | Version control available by using MSSCCI provider                           | Version control available by using MSSCCI provider                           | Version control available by using MSSCCI provider                                 | Version control available by using MSSCCI provider                        | Version control available by using MSSCCI provider|

#### Full-featured support

Any Azure DevOps Server or TFS-facing functionality exposed in the UI of Visual Studio and Team Explorer should work. We guarantee full feature support between client and server of the same version.

> [!NOTE]
> If you use the latest version of Visual Studio but plan to continue to use the most recent previous version of Team Foundation Server, either temporarily or permanently, you can expect a high level of compatibility.
All non-administrative scenarios are supported.
>
>

### High level of support

If you're on TFS 2015 and you run the most recent previous version of Visual Studio or Team Explorer, for example, Visual Studio 2013, you can expect support from Visual Studio for most features.
You might need to install the latest update. After installation, mainline scenarios for all non-admin personas are supported.

This support is for features that developers and testers need to continue their daily work. These features are used to queue builds, run queries, view documents, and get, edit, and check in files. Program managers also should be able to continue to use most features relevant to them. They might need to rely on web access for some scenarios. These scenarios occur when they manage areas and iterations and write new queries.

If you use newer versions of Visual Studio against older versions of Team Foundation Server, you can similarly expect most features to be supported. 

Older process templates that were in use with the previous version of Team Foundation Server should continue to be compatible with the new server.

### General support

If a client is two versions older than your server, you can expect general support after you install a compatibility GDR. This support is similar to the high level of support you see when Visual Studio is one release older than Azure DevOps Server or TFS. The experience for some non-mainline scenarios might be degraded but not entirely blocked. Non-admins should be able to continue unimpeded in their daily work. Older process templates should remain compatible with the new server.

### MSSCCI support

Visual Studio/Team Explorer 2008 and Visual Studio 2005 are no longer officially supported.
To connect to the server, these clients must interface through the MSSCCI provider instead.
MSSCCI support only includes support for source control integration and MSSCCI commands.
The goal is to allow developers to continue to work with legacy applications in an upgraded server.

## Team Explorer Everywhere

New versions of Team Explorer Everywhere are released through [GitHub](https://github.com/Microsoft/team-explorer-everywhere)
and the [Eclipse Marketplace](https://marketplace.eclipse.org/content/team-explorer-everywhere).
To maximize compatibility with the latest version of Azure DevOps Server or TFS, use the latest version of Team Explorer Everywhere.
If you need support for an older version of Eclipse, Java, or an operating system,
use an older version of Team Explorer Everywhere that encompasses the range you need.
Multiple versions of Team Explorer Everywhere also can be installed side by side if you run multiple versions of Eclipse.

> [!div class="mx-tdCol2BreakAll"]
> |Team Explorer Everywhere           | Eclipse version | Azure DevOps Services<br/>Azure DevOps Server 2019<br/>TFS 2012 - TFS 2018 | TFS 2010                    | TFS 2008                | TFS 2005|
> |-----------------------------------|-----------------|-----------------------------|-----------------------------|-----------------------------|-----------------------------|
> |Team Explorer Everywhere 14.114.0+ | Eclipse 4.2-4.7 | ![Check](_img/check.png) | ![x](_img/x.png)         | ![x](_img/x.png)         | ![x](_img/x.png)|
> |Team Explorer Everywhere 2015      | Eclipse 3.5-4.3 | ![Check](_img/check.png) | ![Check](_img/check.png) | ![x](_img/x.png)         | ![x](_img/x.png)|
> |Team Explorer Everywhere 2013      | Eclipse 3.5-4.3 | ![Check](_img/check.png) | ![Check](_img/check.png) | ![x](_img/x.png)         | ![x](_img/x.png)|
> |Team Explorer Everywhere 2012      | Eclipse 3.4-4.3 | ![Check](_img/check.png) | ![Check](_img/check.png) | ![Check](_img/check.png) | ![Check](_img/check.png)|
> |Team Explorer Everywhere 2010 SP1  | Eclipse 3.2-3.6 | ![Check](_img/check.png) | ![Check](_img/check.png) | ![Check](_img/check.png) | ![Check](_img/check.png)|
> |Team Explorer Everywhere 2010      | Eclipse 3.0-3.5 | ![Check](_img/check.png) | ![Check](_img/check.png) | ![Check](_img/check.png) | ![Check](_img/check.png)|

## Microsoft Office integration

Microsoft Office integration with Azure DevOps supports the following clients:
 
- [Excel](/azure/devops/work/backlogs/office/bulk-add-modify-work-items-excel) 
- [Project](/azure/devops/work/backlogs/office/create-your-backlog-tasks-using-project) 
- [PowerPoint with Storyboarding](/azure/devops/work/backlogs/office/storyboard-your-ideas-using-powerpoint)

> [!IMPORTANT]  
> Starting with Azure DevOps Server 2019 and Visual Studio 2019, the Team Foundation plug-in for Office is deprecating support for Microsoft Project and Microsoft PowerPoint with Storyboarding. Project integration and the **TFSFieldMapping** command are not supported for Azure DevOps Server 2019 nor for Azure DevOps Services. The plug-in will continue to support Microsoft Excel.  

> [!div class="mx-tdCol2BreakAll"]
> |Azure DevOps version | Supported Office versions|
> |------------|--------------------------|
> |Azure DevOps Services | Office 2016<br/>Office 2013<br/>Office 2010|
> |Azure DevOps Server 2019 | Office 2016<br/>Office 2013<br/>Office 2010|
> |TFS 2018    | Office 2016<br/>Office 2013<br/>Office 2010|
> |TFS 2017    | Office 2016<br/>Office 2013<br/>Office 2010|
> |TFS 2015    | Office 2013<br/>Office 2010<br/>Office 2007|
> |TFS 2013    | Office 2013<br/>Office 2010<br/>Office 2007|
> |TFS 2012    | Office 2010<br/>Office 2007|
> |TFS 2010    | Office 2010<br/>Office 2007|

* If you use SharePoint with TFS 2017 or earlier versions, you must add SP2 to Office 2007 and SP1 to Office 2010 for integration between Office and SharePoint. 
* SharePoint 2010 doesn't support Office 2013.

## TFS Build agents and controllers

A new [scriptable build system](/azure/devops/pipelines/overview) is web based and cross-platform.

<!--- QUESTION: TFS Build compatibility - Update required? see Feedback comments about supported build controllers and agents   --> 

> [!div class="mx-tdCol2BreakAll"]
> |Version | Supported TFS Build versions|
> |------------|--------------------------
> |TFS 2018    | TFS 2018 build agent<br/>TFS 2017 build agent<br/>TFS 2015 XAML controller<br/>TFS 2013 XAML controller<br/>TFS 2010 XAML controller<br/>Note: You must upgrade to TFS 2018.2 or newer to use XAML builds.|
> |TFS 2017    | TFS 2017 build agent<br/>TFS 2015 build agent<br/>TFS 2015 XAML controller<br/>TFS 2013 XAML controller<br/>TFS 2010 XAML controller|
> |TFS 2015    | TFS 2015 build agent<br/>TFS 2015 XAML controller<br/>TFS 2013 XAML controller<br/>TFS 2010 XAML controller|
> |TFS 2013    | TFS 2013 XAML controller<br/>TFS 2012 XAML controller<br/>TFS 2010 XAML controller|
> |TFS 2012    | TFS 2012 XAML controller<br/>TFS 2010 XAML controller|
> |TFS 2010    | TFS 2010 XAML controller|

You might want to use an older version of Build if you plan to continue to use:
- The XAML Build system. 
- Build servers against multiple versions of TFS. 
- Servers with older operating systems in your TFS deployment. 

TFS 2010 XAML controllers support operating systems as far back as Windows XP and Windows Server 2003.


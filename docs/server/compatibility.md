---
title: Version compatibility
description: Describes compatibility for Azure DevOps and TFS -- operating systems, SQL Server, SharePoint, client versions, server versions, browsers
ms.prod: devops-server
ms.technology: tfs-admin
toc: show
ms.manager: jillfra
ms.author: aaronha
author: elbatk
ms.topic: conceptual
ms.date: 11/07/2018
---

# Compatibility with Azure DevOps Server and TFS versions

<a name="client-compatibility"></a>
## Client compatibility

### Visual Studio

We define three levels of client support for different versions of Visual Studio and Team Explorer. 
Only the latest version has "full" compatibility with the latest Team Foundation Server or 
Azure DevOps Server, because it’s the only client that:

- Includes components that can interface with new features for that release
- Lets you run certain administrative tasks such as creating new projects

Previous versions have varying levels of support below that, depending on how old they are.

This table describes the level of support that we guarantee with each client version.
Keep in mind that additional functionality other than what is listed below might continue to work using older clients. In fact,
it often does, but is outside the scope of what we test and support officially.

Visual Studio/ Team Explorer version | Azure DevOps Server 2019 RC1, TFS 2018, TFS 2017, and Azure DevOps Services support notes                                | TFS 2015 support notes                                                    | TFS 2013 support notes                                                          | TFS 2012 support notes                                                 | TFS 2010 support notes
-------------------------------------|---------------------------------------------------------------------------|---------------------------------------------------------------------------|---------------------------------------------------------------------------------|------------------------------------------------------------------------|------------------------------------------------
Visual Studio 2017                   | Full Support                                                              | High level of support                                                     | High level of support                                                           | High level of support                                                  | High level of support
Visual Studio 2015                   | High level of support                                                     | Full support                                                              | High level of support                                                           | High level of support                                                  | High level of support
Visual Studio/Team Explorer 2013     | General support                                                           | High level of support                                                     | Full support                                                                    | High level of support                                                  | High level of support
Visual Studio/Team Explorer 2012     | General support. Supports Git with Visual Studio Tools for Git extension. | General support. Supports Git with Visual Studio Tools for Git extension. | High level of support. Supports Git with Visual Studio Tools for Git extension. | Full support. Supports Git with Visual Studio Tools for Git extension. | High level of support
Visual Studio/Team Explorer 2010     | General support (SP1 and Compatibility GDR)                                      | General support (SP1 and Compatibility GDR)                                      | General support (SP1 and Compatibility GDR)                                            | High level of support (SP1 and Compatibility GDR)                             | Full support (SP1 and Compatibility GDR)
Visual Studio/Team Explorer 2008     | Version Control available using MSSCCI provider                           | Version Control available using MSSCCI provider                           | Version Control available using MSSCCI provider                                 | Version Control available using MSSCCI provider                        | Version Control available using MSSCCI provider
Visual Studio 2005                   | Version Control available using MSSCCI provider                           | Version Control available using MSSCCI provider                           | Version Control available using MSSCCI provider                                 | Version Control available using MSSCCI provider                        | Version Control available using MSSCCI provider

#### Full-featured support

Any Azure DevOps Server or TFS-facing functionality exposed in the UI of Visual Studio and Team Explorer should work.
We guarantee full feature support between client and server of the same version.

> [!NOTE]
> If you're using the latest version of Visual Studio,
but will continue to use the most recent previous version of Team Foundation Server (either temporarily or permanently),
you can expect a high level of compatibility here as well.
All non-administrative scenarios are supported.
>
>

#### High level of support

If you're running the most recent previous version of Visual Studio or Team Explorer
(for example: Visual Studio 2013, if you're on TFS 2015),
then you can expect most features to be supported from Visual Studio.
You might need to install the latest update,
but after doing so, mainline scenarios for all non-admin personas are supported.
This includes features needed for developers and testers to continue their daily work,
such as queuing builds, running queries, viewing documents, and getting, editing, and checking in files.
Program Managers should also be able to continue using most features relevant to them,
but might need to rely on web access for some scenarios, such as managing areas and iterations, and writing new queries.

If you're using newer versions of Visual Studio against older versions of Team Foundation Server,
you can similarly expect most features to be supported. 

Older process templates that were in use with the previous version of Team Foundation Server should continue to be compatible with the new server.

#### General support

If a client is two versions older than your server, you can expect general support (after installing a compatibility GDR).
This is similar to the high level of support you see when Visual Studio is one release older than Azure DevOps Server or TFS. 
However, the experience for some non-mainline scenarios might be degraded but not entirely blocked.
Non-admins should still be able to continue unimpeded in their daily work,
and older process templates should remain compatible with the new server.

#### MSSCCI support

Visual Studio/Team Explorer 2008 and Visual Studio 2005 are no longer officially supported.
To connect to the server, these clients must interface through the MSSCCI provider instead.
MSSCCI support only includes support for source control integration and MSSCCI commands.
The goal is simply to allow developers to continue working with legacy applications in an upgraded server.

### Team Explorer Everywhere

New versions of Team Explorer Everywhere are released through [GitHub](https://github.com/Microsoft/team-explorer-everywhere)
and the [Eclipse Marketplace](https://marketplace.eclipse.org/content/team-explorer-everywhere).
To maximize compatibility with the latest version of Azure DevOps Server or TFS, you should use the latest version of Team Explorer Everywhere.
If you need support for an older version of Eclipse, Java, or an operating system,
you can choose to use an older version of Team Explorer Everywhere that encompasses the range you need.
Multiple versions of Team Explorer Everywhere can also be installed side by side if you're running multiple versions of Eclipse.

Team Explorer Everywhere           | Eclipse version | Azure DevOps Services, Azure DevOps Server 2019 RC1, TFS 2012 - TFS 2018   | TFS 2010                    | TFS 2008                    | TFS 2005
-----------------------------------|-----------------|-----------------------------|-----------------------------|-----------------------------|-----------------------------
Team Explorer Everywhere 14.114.0+ | Eclipse 4.2-4.7 | ![Check](_img/check.png) | ![x](_img/x.png)         | ![x](_img/x.png)         | ![x](_img/x.png)
Team Explorer Everywhere 2015      | Eclipse 3.5-4.3 | ![Check](_img/check.png) | ![Check](_img/check.png) | ![x](_img/x.png)         | ![x](_img/x.png)
Team Explorer Everywhere 2013      | Eclipse 3.5-4.3 | ![Check](_img/check.png) | ![Check](_img/check.png) | ![x](_img/x.png)         | ![x](_img/x.png)
Team Explorer Everywhere 2012      | Eclipse 3.4-4.3 | ![Check](_img/check.png) | ![Check](_img/check.png) | ![Check](_img/check.png) | ![Check](_img/check.png)
Team Explorer Everywhere 2010 SP1  | Eclipse 3.2-3.6 | ![Check](_img/check.png) | ![Check](_img/check.png) | ![Check](_img/check.png) | ![Check](_img/check.png)
Team Explorer Everywhere 2010      | Eclipse 3.0-3.5 | ![Check](_img/check.png) | ![Check](_img/check.png) | ![Check](_img/check.png) | ![Check](_img/check.png)

<a name="supported-browsers"></a>
### Browsers

You can use these browsers with Azure DevOps Services
and to access Azure DevOps Server or TFS with the web client.

Version                   | Edge        | Internet Explorer | Safari (Mac)   | Firefox     | Chrome
--------------------------|-------------|-------------------|----------------|-------------|-------------
Azure DevOps Services, Azure DevOps Server 2019 RC1, TFS 2018, TFS 2017  | most recent | 11 and later      | 9.1 and later  | most recent | most recent
TFS 2015                  | most recent | 9 and later       | 5 and later    | most recent | most recent
TFS 2013                  |             | 9 and later       | 5 and later    | most recent | most recent

Edge, Firefox, and Chrome automatically update themselves, 
so Azure DevOps and TFS support the most recent version.

### Office

Office integration supports the following clients: [Excel](/azure/devops/work/backlogs/office/bulk-add-modify-work-items-excel), [Project](/azure/devops/work/backlogs/office/create-your-backlog-tasks-using-project), and [PowerPoint with Storyboarding](/azure/devops/work/backlogs/office/storyboard-your-ideas-using-powerpoint). 

Azure DevOps Server or TFS version | Supported Office versions
------------|--------------------------
Azure DevOps Server 2019 RC1    | Office 2016<br/>Office 2013<br/>Office 2010
TFS 2018    | Office 2016<br/>Office 2013<br/>Office 2010
TFS 2017    | Office 2016<br/>Office 2013<br/>Office 2010
TFS 2015    | Office 2013<br/>Office 2010<br/>Office 2007
TFS 2013    | Office 2013<br/>Office 2010<br/>Office 2007
TFS 2012    | Office 2010<br/>Office 2007
TFS 2010    | Office 2010<br/>Office 2007

* If you're using SharePoint with Azure DevOps Server or TFS, you must add SP2 to Office 2007 and SP1 to Office 2010 for integration between Office and SharePoint. 
* SharePoint 2010 doesn't support Office 2013.

## TFS Build Compatibility

We've built a brand new [scriptable build system](/vsts/build-release/overview) that's web based and cross-platform.

You may want to use an older version of Build if you plan to continue using the XAML build system, 
if you are using Build servers against multiple versions of TFS, or if you need to leverage servers 
with older operating systems in your TFS deployment. TFS 2010 XAML Controllers support operating 
systems as far back as Windows XP and Windows Server 2003.

TFS Version | Supported Build versions
------------|--------------------------
TFS 2018    | TFS 2018 Build Agent<br/>TFS 2017 Build Agent<br/>TFS 2015 XAML Controller<br/>TFS 2013 XAML Controller<br/>TFS 2010 XAML Controller<br/>Note: You must upgrade to TFS 2018.2 or newer to use XAML builds.
TFS 2017    | TFS 2017 Build Agent<br/>TFS 2015 Build Agent<br/>TFS 2015 XAML Controller<br/>TFS 2013 XAML Controller<br/>TFS 2010 XAML Controller
TFS 2015    | TFS 2015 Build Agent<br/>TFS 2015 XAML Controller<br/>TFS 2013 XAML Controller<br/>TFS 2010 XAML Controller
TFS 2013    | TFS 2013 XAML Controller<br/>TFS 2012 XAML Controller<br/>TFS 2010 XAML Controller
TFS 2012    | TFS 2012 XAML Controller<br/>TFS 2010 XAML Controller
TFS 2010    | TFS 2010 XAML Controller
---
title: Manually install SQL Server for Azure DevOps Server 
description: Manually install SQL Server for Azure DevOps Server or Team Foundation Server
ms.manager: douge
ms.author: elbatk
author: elbatk
ms.topic: conceptual
ms.date: 11/01/2018
ms.prod: devops-server
ms.technology: tfs-admin
---

# Manually install SQL Server for Azure DevOps Server or Team Foundation Server

**Azure DevOps Server 2019 RC** | **TFS 2018** | **TFS 2017** | **TFS 2015** | **TFS 2013**

The steps in this article are for installing SQL Server 2017, but you can use similar steps for installing previous versions. Azure DevOps Server requires SQL Server 2016 and above. We install all the SQL Server features that Azure DevOps Server requires on the same server, however, using the same server isn’t a requirement. Azure DevOps Server is flexible with its use of SQL Server topologies.

> [!TIP]
> You can use an existing installation of SQL Server for Azure DevOps Server, but to do this you need administrative credentials granted by the SQL Server administrator. You must be a member of the sysadmin Server role in SQL Server to install and configure Azure DevOps Server. See blog post [Why does Azure DevOps Server or Team Foundation Server need so much privilege on the SQL Server?](http://blogs.msdn.com/b/bharry/archive/2010/08/20/database-permissions-required-to-configure-tfs.aspx).

## One server or two?

If you’re going to use one server for Azure DevOps Server, you can safely ignore this section.

If you plan on more than 500 users accessing Azure DevOps Server, install SQL Server on a second server. An additional server will split the load between Azure DevOps Server and its configuration database. The SQL Server features that Azure DevOps Server requires, can be installed on the second server or split between the two. One such example installs the report server on the Azure DevOps Server instance, while other components are installed on a second server. This sort of configuration separates the traffic between HTTP and the SQL Server.

There are many different topology choices you can make. Azure DevOps Server allows you to install SQL Server instance features (**Database engine**, **Reporting services**, **Analysis services**) on multiple servers. Here are some SQL Server topology caveats to keep in mind:

- Azure DevOps Server requires the **Database engine** and **Full text search** features. These features must be installed together, though both can go on its own server.
- Azure DevOps Server reporting is optional. If needed, install both **Analysis services** and **Reporting services**, though each can go on its own server.
- If none of the above SQL Server features are installed on the Azure DevOps Server instance, you must install the **Client tools connectivity** feature.

To install SQL Server features on different servers, run the installation for each server. Use the same instructions below, but only install the feature required.

> [!TIP]
> A multi-server installation of Azure DevOps Server requires either an Active Directory domain and domain accounts, or the *Network Service* account. You cannot use local accounts for service accounts.

## To install SQL Server
  
You must be a member of the **Windows Administrators** security group before running the installation.

> [!TIP]
> For previous versions of Windows prior to Windows Server 2016 and Windows 10, you must make sure .NET Framework 3.5 is installed. For Windows Server, you can install the .NET Framework 3.5 by using the **Add Features Wizard** from **Server Manager**. See the following pages, [Adding Server Roles and Features (Windows 2012/Windows 2012 R2)](https://technet.microsoft.com/library/hh831809.aspx)and [Adding Server Roles and Features (Windows Server 2008 R2)](https://technet.microsoft.com/library/cc732263.aspx).

1. Insert the installation DVD for a supported version of SQL Server and launch *setup.exe*.

1. On the **SQL Server Installation Center** page, choose **Installation**. Then choose **New installation or add features to an existing installation**.

    ![New installation of SQL Server](_img/ic665094.png)

    1. On the **Product Key** page, type your product key or specify a free edition, then choose **Next**.

    1. On the **License Terms** page, accept the license agreement, then choose **Next**.

    1. On the **Microsoft Update** page, optionally select **Use Microsoft Update to check for updates**, then choose **Next**.

    1. On the **Install Rules** page, choose **Next**.

        ![Windows Firewall warning](_img/ic688130.png)

        > [!TIP]
        > A Windows Firewall warning might appear, but can safely be ignored if you’re planning to also install Azure DevOps Server on this server. The Azure DevOps Server installation will automatically add this exception to the Windows Firewall. If you’re installing Azure DevOps Server on another server, you’ll need to [Open a port for SQL Server in Windows Firewall on this server](http://elhajj.wordpress.com/2013/02/25/workaround-error-tf255049-punching-a-hole-through-windows-firewall/).
        >
        > For more information about SQL Server ports required for Azure DevOps Server, see [Ports required for installation of Azure DevOps Server or Team Foundation Server](../../architecture/required-ports.md).

    1. On the **Feature Selection** page, select the check boxes for one or more of the following components, depending on the topology you intend to use:

        - Database Engine Services (required)

        - Full-Text and Semantic Extractions for Search (required)

        - Analysis Services (reporting only)

        - Client Tools Connectivity (only if no other SQL Server components are installed on the server that is running Azure DevOps Server)

        > [!NOTE]
        > In previous versions of SQL Server, you can install the Management Tools (Sql Server Management Studio) and Reporting Services by selecting them here in the **Features Selection** page. However, in SQL Server 2017 they are installed separately, see [To install SQL Server Management Studio](#to-install-sql-server-management-studio) and [To install and configure SQL Server Reporting Services](#to-install-and-configure-sql-server-reporting-services).

    1. On the **Instance Configuration** page, choose **Default instance**. If you choose **Named instance**, type the name of the instance.

        ![Instance configuration](_img/ic665098.png)

    1. On the **Server Configuration** page, accept the defaults or enter the name of a domain account. You can use *NT AUTHORITY\\NETWORK SERVICE* in the **Account Name** for every service. If you specify a domain account, type its password in **Password**. If you use *NT AUTHORITY\\NETWORK SERVICE*, leave **Password** blank.

        ![Server Configuration](_img/ic665099.png)

    1. In the **Startup Type** column, verify that **Automatic** appears for all services that you can edit. Click **Next**.

        ![Server Configuration (details)](_img/ic665100.png)

        > [!NOTE]
        > Are you using a non-English version of SQL Server? The default collation settings for U.S. English meet the requirements for Azure DevOps Server, or you can set the collation settings for the **Database Engine** on this page. For more information, see [SQL Server Collation Requirements for Azure DevOps Server or Team Foundation Server](collation-requirements.md).

    1. If you previously selected the **Database Engine Services** check box, on the **Database Engine Configuration** page, choose **Windows authentication mode** and choose **Add Current User**. Otherwise skip to the next step.

        ![Database Engine Configuration](_img/ic665101.png)

    1. If you previously selected the **Analysis Services** check box, on the **Analysis Services Configuration** page, choose **Add Current User**. Otherwise skip to the next step.

        ![Analysis Services Configuration](_img/ic665102.png)

    1. On the **Ready to Install** page, review the list of components to be installed, and then choose **Install**.

        ![Complete](_img/ic662712.png)

    1. Choose **Close** after the installation has finished.

## To install SQL Server Management Studio

To install Azure DevOps Server, **SQL Server Management Studio** isn't required. Only use **SQL Server Management Studio** if you need to verify your installation of SQL Server.

1. On the **SQL Server Installation Center** page, choose **Installation**. Next, choose **Install SQL Server Management Tools**.

1. On the [Download SQL Server Management Studio](/sql/ssms/download-sql-server-management-studio-ssms?view=sql-server-2017) page, follow the instructions to download and install.

## To install and configure SQL Server Reporting Services

If you aren't using Azure DevOps Server reporting, you don't need to install **SQL Server Reporting Services** or **SQL Server Analysis Services**.

If **Reporting services** is installed on the same server as Azure DevOps Server and isn't configured, the Azure DevOps Server installation will have you complete its configuration.

To change a report server manually, you must be member of the **Windows Administrators** on the server where the report database is located.

### To install and configure a report server

1. On the **SQL Server Installation Center** page, choose **Installation**. Then choose **Install SQL Server Reporting Services**.

1. On the **Microsoft SQL Server 2017 Reporting Services** page, click **Download**. Run the installation.

1. After installation completes, choose **Configure report server**.

    The **Reporting Services Configuration Connection** dialog box appears.

1. In **Server Name**, enter the name of the report server. If you're using an instance name, enter the name of the instance in **Report Server Instance**. Choose **Connect**.

    1. On the main page, choose **Start** if the Report Service status reads **Stopped**.

    1. In the navigation bar, choose **Web Service URL**.

        1. Choose **Apply** to accept the default values in the **Virtual Directory**, **IP Address**, and **TCP Port** boxes.

    1. In the navigation bar, choose **Database**.

        1. On the **Report Server Database** page, choose **Change Database**.

            The **Report Server Database Configuration Wizard** appears.

            1. In **Action**, choose **Create a new report server database**.

            1. In **Database Server**, enter the name of a local or remote instance of SQL Server to host the database for the report server in **Server Name**.

            1. In **Database**, accept the default values in the **Database Name**, **Language**, and **Native Mode** boxes.

            1. In **Credentials**, accept the default values in the **Authentication Type**, **User name**, and **Password** boxes.

            1. In **Summary**, verify your information.

            1. In **Progress and Finish**, choose **Finish**.

    1. In the navigation bar, choose **Web Portal URL**.

        1. Choose **Apply** to accept the default value in the **Virtual Directory** box.

## Creating a SQL Server Database for Azure DevOps Server

You can create an empty database for Azure DevOps Server. An empty database is useful for managing the one or many instance databases your Azure DevOps Server requires. This database can be hosted on a single or managed instance of SQL Server. Whatever the reason, this article shows you how to create an empty SQL Server database for use with Azure DevOps Server.

Conceptually, this procedure contains two steps:

1. Create the database and name it based on established guidelines.

1. Identify the database when you install Azure DevOps Server.

Azure DevOps Server has a database that can be used as an empty database during installation:

- Tfs\_*DatabaseLabel*Configuration

This database must use the naming structure as shown. However, you can either remove the string *DatabaseLabel* or use a custom string that uniquely describes this database.

During the Azure DevOps Server installation, when using an existing SQL Server instance, you have the option to use this database. Be sure to select the **Use pre-existing empty database(s)** check box under **Advanced Options** during the install. If you added a label, you must also type it in **Server Databases Label**. The wizard will then use the empty database you created to set up its configuration database.

> [!NOTE]
> Each project collection also requires its own database, but you cannot configure Azure DevOps Server to use empty project collection databases during installation. The collection databases will automatically be created during installation.

## Work with SQL Server Named Instances

You can choose to install Azure DevOps Server using the default instance of SQL Server or a named instance of SQL Server. Depending on the business infrastructure and deployment needs, some prefer to use a named instance. To use a named instance in your deployment of Azure DevOps Server, either create the named instance in SQL Server before installing Azure DevOps Server, or create a project collection that uses that instance. You can't create a named instance during the installation of Azure DevOps Server.

To use a named instance of SQL Server in a deployment of Azure DevOps Server, do one of the following steps:

- Install SQL Server by using a named instance

- Move or restore Azure DevOps Server data to a named instance

- Create a project collection on a named instance

## Verify SQL Server for Azure DevOps Server

To verify your installation of SQL Server will work with Azure DevOps Server, check that the required SQL Server features are available. Also, check the underlying Windows services associated with SQL Server are running and make sure your connection settings are configured and that network ports are open.

To use reporting when **SQL Server Reporting Services** isn't on the server running Azure DevOps Server, install **Client tools connectivity** on Azure DevOps Server.

If the **Database engine**, **Analysis services**, and **Reporting services** are running on different instances of SQL Server, sign in to each server to verify the instances.

### Required Permissions

To run **SQL Server Configuration Manager**, you must be a member of the *Users* security group on the server hosting SQL Server. To use **SQL Server Configuration Manager** to modify services, you must also be a member of the *Administrators* security group.

To run **SQL Server Reporting Services Configuration Manager** or **SQL Server Management Studio**, you must be a member of the *Administrators* security group. This assignment is on the operating system of the server with the SQL Server instance. For **SQL Server Management Studio**, you must also be a member of the *Public* server role on the SQL Server instance needing verification.

### Verify the Database Engine and Analysis Services

On the instance of SQL Server that is running the **Database engine**, you must verify that you have the **Full-text search** feature installed. To verify this functionality, open the **SQL Server Installation Center**. Click the **New SQL Server stand-alone installation or add features to an existing installation**. If **Full-text search** isn't available on the instance of SQL Server that is running the **Database engine**, you must install **Full-text search**.

To verify that Windows services are running by using **SQL Server Configuration Manager**:

1. On the instance of SQL Server on which the **Database engine**, **SQL Server Analysis Services**, or both are running, launch **SQL Server Configuration Manager**.

    1. Choose **SQL Server Services**, and verify that **Running** appears in the **State** column of all services. Verify the **Start Mode** is set to **Automatic** for all services.

       - To change the start mode of a service to start automatically, open the context menu for the service, choose **Properties**, and choose the **Service** tab. Click the drop-down list to the right of **Start Mode,** and choose **Automatic**.

       - To change a stopped service state to running, you must open the context menu for the stopped service and choose **Start**.

    1. Choose **SQL Server Network Configuration**, double-click **Protocols for _MyInstanceName_**, and verify that **Enabled** appears in the **Status** column for **TCP/IP**.

       If you specified the default instance during installation, *MyInstanceName* will be *MSSQLSERVER*.

To complete the following procedure, you must have **SQL Server Management Studio** installed. However, it doesn't have to be installed on the server that's running your instance of SQL Server.

To verify a connection to an instance of SQL Server by using **SQL Server Management Studio**:

1. Launch **SQL Server Management Studio**.

    The **Connect to Server** dialog box opens.

1. In the **Server type** list, choose **Database Engine** or **Analysis Services**, depending on the type of installation that you're verifying.

1. Type the name of the server to which you want to connect, and then choose **Connect**.

    When SQL Server is installed on a cluster, you must specify the server name, not the computer name. If you use named instances of SQL Server, specify the name of the server and the name of the instance. If you can't connect to the server, verify the firewall settings, and then try to connect again.

1. In **Object Explorer**, verify that a green arrow appears next to the server name.

### Verify Reporting Services

To verify that the Windows service is running using **SQL Server Configuration Manager**:

1. On the server that is running **SQL Server Reporting Services**, launch **SQL Server Configuration Manager**.

    1. Choose **SQL Server Services**, and verify that **Running** appears in the **State** column for **SQL Server Reporting Services**.

To verify the report server URLs are running using SQL Server Reporting Services Configuration Manger:

1. On the server that is running SQL Server Reporting Services, launch **Reporting Services Configuration Manager**.

    > [!NOTE]
    > On Windows Server, you must open the context menu for **Reporting Services Configuration Manager** and choose **Run as administrator**.

    The **Reporting Services Configuration Connection** dialog box appears.

    1. In **Server Name**, type the name of the report server. If you're using an instance name, type the name of the instance in **Report Server Instance**. Choose **Connect**.

    1. Choose **Report Manager URL**, and choose the link to the report manager website.

        The report manager website for the report server opens the browser window.

    1. Choose **Web Service URL**, and choose the link to the report server website.

        The report server website opens the browser window.

## See also

[Install Azure DevOps Server or Team Foundation Server](../install-2013/install-tfs.md)  

[Azure DevOps Server or Team Foundation Server upgrade requirements](/tfs/server/upgrade/upgrade-2013/upgrade-2013-requirements)  

[SQL Server Collation Requirements for Azure DevOps Server or Team Foundation Server](collation-requirements.md)

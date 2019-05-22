---
title: Key concepts, glossary of terms 
titleSuffix: Azure DevOps Server 
description: Describes concepts related to Azure DevOps Server
ms.manager: jillfra
ms.author: aaronha
author: aaronhallberg
ms.topic: conceptual
ms.date: 03/12/2019
ms.prod: devops-server
ms.technology: tfs-admin
---


# Components, terms, and key concepts

[!INCLUDE [temp](../_shared/version-tfs-all-versions.md)]

<!--- NEEDS UPDATE, add process model, analytics service, version SP products, and look at how to simplify??? --> 

To deploy and manage Azure DevOps Server effectively, you must understand how it works and communicates with other deployment components. As an Azure DevOps administrator, you should be familiar with Windows authentication, network protocols and traffic, and the structure of the business network on which Azure DevOps is installed. You should also have an understanding of Azure DevOps groups and permissions.

You might also find an understanding of SQL Server, SQL Server Reporting Services, and SharePoint Products useful.
 
You are better able to plan, deploy, and manage Azure DevOps Server if you understand the components and terms described in this article.

::: moniker range=">= azure-devops-2019"

## Analytics service

The Analytics service is the reporting platform of the future for Azure DevOps. It is currently available on Azure DevOps Services and can be installed from the Azure DevOps Marketplace on Azure DevOps Server. For more information, see [What is the Analytics service?](/azure/devops/report/powerbi/what-is-analytics)

::: moniker-end

## Application tier, data tier, and client tier

The logical tiers that compose Azure DevOps Server. These tiers might all be deployed on the same physical computer, or they might be installed across multiple computers. For more information, see [Architecture overview for Azure DevOps Server](architecture.md).

## Project collection

The primary organizational unit for all data in Azure DevOps Server. Collections determine the resources available to the projects added to them. These resources might include SQL Server Reporting Services, Code Search, Marketplace extensions, and more. For more information, see [Manage project collections](../admin/manage-project-collections.md).

## Project

A central point for your team to share team activities that are required to develop a specific software technology or product. Projects are organized in project collections. For more information, see [About projects and scaling your organization](/azure/devops/organizations/projects/about-projects).

## Azure DevOps Server Administration Console

The centralized management tool for Azure DevOps Server administrators to configure and manage resources. For more information, see [Administrative task quick reference](../admin/admin-quick-ref.md).

## Service accounts

The account or accounts that the Web services and applications run by Azure DevOps. Azure DevOps Server requires service accounts to perform operations across servers and Web services. These service accounts have specific requirements. For more information, see [Service accounts and dependencies in Azure DevOps Server](../admin/service-accounts-dependencies.md).

## SharePoint Products

Software that provides support for project portals and dashboards. You can include one or more SharePoint Web applications as part of your deployment of Azure DevOps Server. To include one of these applications, you must install and configure Azure DevOps Server extensions for SharePoint Products, and you must configure permissions across the deployment. For more information, see [Share information using the project portal](/previous-versions/visualstudio/visual-studio-2013/ms242883(v=vs.120)). Integration with SharePoint Products has been deprecated for TFS 2018 and later versions.

## SQL Server and SQL Server Reporting Services

Software that provides a database platform for data warehousing and a business intelligence platform for data integration, analysis, and reporting solutions. Azure DevOps Server stores its data in SQL Server databases. You can also optionally include a server that is running SQL Server Reporting Services and that automatically generates reports for projects. For more information, see [Manage reports, data warehouse, and analysis services cube](/azure/devops/report/admin/manage-reports-data-warehouse-cube).


## Security concepts

To optimize the security of Azure DevOps Server, you should understand the following concepts:

* [Topology](#topos), which includes where and how servers that are running components of Azure DevOps are deployed, the network traffic that passes between Azure DevOps Server and Azure DevOps clients, and the services that must run on Azure DevOps Server.
* [Authentication](#auth), which includes the determination of the validity of users, groups, and services in Azure DevOps Server.
* [Authorization](#authorization), which includes the determination of whether valid users, groups, and services in Azure DevOps Server have the appropriate permissions to perform specific actions.


You should also consider the other components and services on which Azure DevOps Server depends.

When you consider security for Azure DevOps Server, you must understand the difference between authentication and authorization. Authentication is the verification of the credentials of a connection attempt from a client, server, or process. Authorization is the verification that the identity that is trying to connect has permissions to access the object or method. Authorization occurs only after successful authentication. If a connection is not authenticated, it fails before any authorization checking is performed. If authentication of a connection succeeds, a specific action might still be disallowed because the user or group was not authorized to perform that action.

<a name="topos"></a> 

## Topologies, ports, and services  

The first element of deployment and security for Azure DevOps Server is whether the components of your deployment can connect to one another to communicate. Your goal is to enable connections between Azure DevOps clients and Azure DevOps Server and to limit or prevent other connection attempts.

Azure DevOps Server depends on certain ports and services so that it can function. You can secure and monitor these ports to help meet business security needs. You must permit network traffic for Azure DevOps Server to pass between Azure DevOps clients, the servers that host the logical components of the application tier and the data tier, computers for Team Foundation Build, and remote clients that are using Azure DevOps Proxy Server. By default, Azure DevOps Server is configured to use HTTP for its Web services. For a full list of ports and services that Azure DevOps Server uses and how they are used within its architecture, see [Azure DevOps Server architecture](architecture.md). 

You can deploy Azure DevOps Server in an Active Directory domain or in a workgroup. Active Directory provides more built-in security features than workgroups provide. You can use Active Directory features to help secure your deployment of Azure DevOps Server. For example, you can configure Active Directory to prevent duplicate computer names so that a malicious user cannot spoof the computer name with a rogue server that is running Azure DevOps Server. To mitigate the same kind of threat in a workgroup, you must configure computer certificates. 

Whether you deploy Azure DevOps Server in a workgroup or a domain, you must comply with certain constraints imposed by the requirements of Azure DevOps Server itself. For more information about topologies for Azure DevOps Server, see [A Simple Azure DevOps Server Topology](examples-simple-topo.md), [A Moderate Azure DevOps Server Topology](examples-moderate-topo.md), [A Complex Azure DevOps Server Topology, Understanding Windows SharePoint Services](examples-complex-topo.md), and [Understanding SQL Server and SQL Server Reporting Services](sql-server-databases.md).

<a name="auth"></a>

## Authentication  

Security for Azure DevOps Server is integrated with and relies on Windows integrated authentication and the security features of the Windows operating system. You can use Windows integrated authentication to authenticate accounts for connections between Azure DevOps clients and Azure DevOps Server, for Web services on the servers that host the logical application and data tiers, and for connections between application-tier and data-tier servers themselves. 

> [!NOTE]
> You can configure Azure DevOps Server to support Kerberos for mutual authentication of both the client and the server after you install Azure DevOps Server. 
 
You should not configure any SQL Server database connections between Azure DevOps Server and SharePoint Products to use SQL Server Authentication because it is not as secure as Windows authentication. When you connect to the database, the user name and the password for the database administrator account are sent in an unencrypted format. Windows integrated authentication does not send the user name and password. Instead, it uses Windows integrated authentication security protocols to transfer service account identity information that is associated with the host Internet Information Services (IIS) application pool to SQL Server.

<a name="authorization"></a>

## Authorization  

Azure DevOps Server authorization is based on users and groups in Azure DevOps, the permissions that are assigned directly to both those users and groups, and permissions that those users and groups might inherit by belonging to other groups in Azure DevOps Server. Users and groups in Azure DevOps can be local users or groups, Active Directory users or groups, or both.

Azure DevOps Server is preconfigured with default groups at the server, collection, and project level. You can populate these groups by adding individual users. However, you might find management easier if you populate these groups by using Active Directory security groups. By taking this approach, you can manage group membership and permissions more efficiently across multiple computers or applications, such as SharePoint Products and SQL Server.

Your specific deployment might require that you configure users, groups, and permissions on multiple computers and within several applications. For example, you must configure permissions for users and groups in Reporting Services, SharePoint Products, and Azure DevOps Server if you want to include reports and project portals as part of your deployment. In Azure DevOps Server, you can set permissions for each project, for each collection, and across a deployment (at the server level). Additionally, certain permissions are granted by default to any user or group that you add to Azure DevOps Server, as that user or group is automatically added to Azure DevOps Valid Users. For more information, see [Manage users or groups](/azure/devops/security/permissions).

In additon to configuring permissions for authorization in Azure DevOps Server, you might need authorization within version control and work items. You manage these permissions separately at a command prompt, but they are integrated as part of the interface for Team Explorer. 


## Related articles

- [Architecture overview](architecture.md)

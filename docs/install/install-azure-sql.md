---
title: Use Azure SQL Database
titleSuffix: Azure DevOps Server 
description: Use Azure SQL Database with Azure DevOps Server
ms.manager: jillfra
ms.author: aaronha
author: aaronhallberg
ms.topic: conceptual
ms.prod: devops-server
ms.technology: tfs-admin
monikerRange: '>= azure-devops-2019'
ms.date: 02/20/2018
---

# Use Azure SQL Database with Azure DevOps Server

[!INCLUDE [temp](../_shared/version-tfs-2019-only.md)]

Use the steps in this article to configure Azure DevOps Server with [Azure SQL Database](https://docs.microsoft.com/azure/sql-database/). This topology has a few additional steps compared with using an on-premises SQL server.

## Requirements

- Azure SQL Database can only be used with Azure DevOps Server 2019 and later versions.  
- Azure SQL Database can only be used with Azure DevOps Server when you also use Azure Virtual Machines that are domain joined.  

	> [!NOTE]
	> The primary reason for this restriction is that connectivity between Azure DevOps Server and Azure SQL Database is accomplished by using [Managed Service Identity](/azure/active-directory/managed-identities-azure-resources/overview). Using Managed Service Identity avoids the need to use SQL authentication and store usernames and passwords, which presents a security risk.

- Azure SQL databases must be single databases. Managed instances and elastic pools aren't supported.

All General Purpose and Premium SKUs are supported. Standard SKUs S3 and higher also are supported. Basic SKUs and Standard SKUs S2 and below aren't supported.
Azure DevOps Server configurations that use Azure SQL Database don't support older SQL Server Reporting Services with SQL Server Analysis Services reporting features. Instead, you can use the [Azure Analysis Services](/azure/analysis-services/analysis-services-overview). 

<!--- QUESTION: What about the Analytics Service? --> 
Upgrading to Azure DevOps Server is supported only from Team Foundation Server 2015 and newer when you use Azure SQL Database. Azure SQL Database doesn't support encrypted stored procedures.

## Set up Azure SQL Database

1. Configure a managed identity on your virtual machines. We recommend system-managed identities, but user-assigned managed identities also are supported.

    You can run configuration by using all standard mechanisms, including the:

    - [Azure portal](/azure/active-directory/managed-identities-azure-resources/qs-configure-portal-windows-vm)
    - [Azure CLI](/azure/active-directory/managed-identities-azure-resources/qs-configure-cli-windows-vm)
    - [Azure Resource Manager templates](/azure/active-directory/managed-identities-azure-resources/qs-configure-template-windows-vm)

1. To set up a new Azure DevOps Server instance, create two Azure SQL databases:

    - AzureDevOps_Configuration  
    - AzureDevOps_Collection  

    > [!NOTE]
    > You can skip this step if you use existing databases to either:
    >- Upgrade a new version of Azure DevOps Server.
    >- Migrate an up-to-date instance of Azure DevOps Server to Azure SQL Database.

1. Configure [Azure Active Directory authentication](/azure/sql-database/sql-database-aad-authentication) for your Azure SQL Database server. Make yourself the Active Directory administrator on the server. You need administrator permissions on the database to complete the remaining configuration steps. You can change this permission later.

1. Enable your managed identity, or identities if you use multiple servers, to sign in to your Azure SQL database and give it the appropriate permissions. Connect to the database server by using **SQL Server Management Studio**. Connect by using an Azure Active Directory user with **Active Directory** authentication. You can't manipulate Azure Active Directory users if you sign in to Azure SQL Database under SQL authentication.

    a. Run the following T-SQL command on the `master` database:

    ```tsql
    CREATE USER [VMName] FROM EXTERNAL PROVIDER
    ALTER ROLE [dbmanager] ADD MEMBER [VMName]
    ```

    Replace *VMName* with the name of the virtual machine whose managed identity you add to the database. 

    b. Run the following T-SQL command on the configuration and all collection databases:

    ```tsql
    CREATE USER [VMName] FROM EXTERNAL PROVIDER
    ALTER ROLE [db_owner] ADD MEMBER [VMName]
    ```

### Configure Azure DevOps Server

Return to the Azure DevOps Server configuration wizard. If you set up a new instance, select **This is a new Azure DevOps Server deployment**. If you upgrade or migrate and have existing data in your databases, select **I have existing databases to use for this Azure DevOps Server deployment**.

When you get to the **Database** page in the configuration wizard, specify the Azure SQL Database server instance. Typically, the server instance is in the form of *SQLInstanceName*.database.windows.net.

You now have an Azure DevOps Server instance that runs on Azure SQL Database.

## Related articles

- [Install get started](get-started.md)


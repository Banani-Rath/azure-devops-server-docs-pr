---
title: Use Azure SQL Database
description: Using Azure SQL Database with Azure DevOps Server
ms.manager: douge
ms.author: v-masebo
author: v-masebo
ms.topic: conceptual
ms.date: 11/14/2018
ms.prod: devops-server
ms.technology: tfs-admin
---

# Using Azure SQL Database with Azure DevOps Server

**Azure DevOps Server 2019 RC**

The steps in this article are for configuring Azure DevOps Server with [Azure SQL Database](https://docs.microsoft.com/azure/sql-database/). Using this topology has a few additional steps compared with using an on-premises SQL Server.

## Requirements

- Azure SQL Database can only be used with Azure DevOps Server 2019 and newer

- Azure SQL Database can only be used with Azure DevOps Server when also using Azure Virtual Machines

    > [!NOTE]
    > The primary reason for this restriction is that connectivity between Azure DevOps Server and Azure SQL Database is accomplished using [Managed Service Identity](/azure/active-directory/managed-identities-azure-resources/overview). This avoids the need to use SQL Authentication and store usernames and passwords that would present a security risk.

- Azure SQL Databases themselves must be Single Databases – managed instances and elastic pools aren't supported

All General Purpose and Premium SKUs are supported. Standard SKUs S3 and higher are supported as well. Basic SKUs and Standard SKUs S2 and below aren't supported.
Azure DevOps Server configurations using Azure SQL Database don't support older SQL Server Reporting Services with SQL Server Analysis Services reporting features. The newer [Analysis Services](/sql/analysis-services/analysis-services?view=sql-server-2017) reporting features are still supported.  

Upgrading to Azure DevOps Server is only supported from Team Foundation Server 2015 and newer when using Azure SQL Database, since Azure SQL Database doesn't support encrypted stored procedures.

## Setup Azure SQL Database

1. Configure a managed identity on your virtual machine(s). We recommend system-managed identities, but user-assigned managed identities are also supported.

    You can run configuration using all standard mechanisms, including:

    - [Portal](/azure/active-directory/managed-identities-azure-resources/qs-configure-portal-windows-vm)
    - [CLI](/azure/active-directory/managed-identities-azure-resources/qs-configure-cli-windows-vm)
    - [ARM templates](/azure/active-directory/managed-identities-azure-resources/qs-configure-template-windows-vm)

1. If you're setting up a new Azure DevOps Server instance, you need to create two Azure SQL Databases:

    - Tfs_Configuration
    - Tfs_Collection

    > [!NOTE]
    > If you're using existing databases to either upgrade a new version of Azure DevOps Server or to migrate an up-to-date instance of Azure DevOps Server to Azure SQL Database, you can skip this step.

1. Configure [Azure Active Directory authentication](/azure/sql-database/sql-database-aad-authentication) for your Azure SQL Database server. Make yourself the *Active Directory Administrator* on the server. You can change this permission later, but you’ll need the administrator permissions on the database to complete the remaining configuration steps.  

1. Enable your managed identity, or identities, if you're using multiple servers, to sign in to your Azure SQL Databases and give it the appropriate permissions. Connect to the database server using **SQL Server Management Studio**. Connect using an Azure Active Directory user with **Active Directory** authentication. Azure SQL Database doesn't allow manipulating Azure Active Directory users when you're logged in under SQL Authentication.

    1. Run the following T-SQL command on the `master` database:

    ```tsql
    CREATE USER [VMName] FROM EXTERNAL PROVIDER
    ALTER ROLE [dbmanager] ADD MEMBER [VMName]
    ```

    Make sure to replace *VMName* with the name of the virtual machine whose managed identity you're adding to the database.  

    1. Run the following T-SQL command on the configuration and all collection databases:

    ```tsql
    CREATE USER [VMName] FROM EXTERNAL PROVIDER
    ALTER ROLE [db_owner] ADD MEMBER [VMName]
    ```

### Configure Azure DevOps Server

Now return to the Azure DevOps Server configuration wizard. If you’re setting up a new instance, make sure to select **This is a new Azure DevOps Server deployment**. If you’re upgrading or migrating and have existing data in your databases, make sure to select **I have existing databases to use for this Azure DevOps Server deployment**.

When you get to the **Database** page in the configuration wizard, be sure to specify the Azure SQL Database server instance, typically in the form of *SQLInstanceName*.database.windows.net.

That’s it! You now have an Azure DevOps Server instance running on Azure SQL.

## See also

[Install Azure DevOps Server](/tfs/server/install-2013/install-tfs)

[Manually install SQL Server for Azure DevOps Server](/tfs/server/install/sql-server/install-sql-server)

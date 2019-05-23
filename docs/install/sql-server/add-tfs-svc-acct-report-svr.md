---
title: Add the Azure DevOps Server service account to the report server
titleSuffix: Azure DevOps Server  
description: Add the Azure DevOps Server service account to the report server
ms.manager: jillfra
ms.author: aaronha
author: aaronhallberg
ms.topic: conceptual
ms.prod: devops-server
ms.technology: tfs-admin
monikerRange: '>= tfs-2013'
ms.custom: "retire"
ms.date: 05/21/2019
---

# Add the Azure DevOps service account to the report server

[!INCLUDE [temp](../../_shared/version-tfs-all-versions.md)]

If the report server and Azure DevOps Server are not on the same server, you must add the name of your Azure DevOps service account (TFSSERVICE) to the Content Manager group on the report server. This step is done automatically during Azure DevOps setup if the report server is installed on Azure DevOps Server. 

If you are using Network Service for TFSSERVICE, add the machine name of the server that is running Azure DevOps Server instead of Network Service. The machine name is the server name followed by the `$` symbol. For example, *Domain\ServerName$*.

For more information about service accounts, see [Service account requirements](../../account-requirements.md).

## Prerequisite

You must be a member of the **Administrators** security group on the report server. 

## Add service account

To add the service account for Azure DevOps Server to the Content Manager group on the report server:

1. From the **Start** menu, select **Reporting Services Configuration Manager**.

	> [!NOTE]   
	> On Windows Server 2008, open the shortcut menu for **Reporting Services Configuration Manager** and select **Run as administrator**.

	The **Reporting Services Configuration Connection** dialog box appears.

2. In the **Server Name** box, enter the name of the report server. If you are using an instance name, select the name of the instance in the **Report Server Instance** list. Select **Connect**.

3. Select **Report Manager URL**, and then select the link to the report manager website. 

   The report manager website for the report server opens in a web browser window.

4. In the report manager website, select the **Properties** tab, and then select **New Role Assignment**.

5. In the **Group or user name** box, enter the name of the service account that you use for Azure DevOps Server (TFSSERVICE), select the **Content Manager** check box, and then select **OK**.


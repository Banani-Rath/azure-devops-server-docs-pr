---
title: Add the TFS service account to the report server
titleSuffix: Azure DevOps Server & TFS  
description: Add the TFS service account to the report server
ms.manager: jillfra
ms.author: aaronha
author: aaronhallberg
ms.topic: conceptual
ms.prod: devops-server
ms.technology: tfs-admin
monikerRange: '>= tfs-2013'
ms.custom: "retire"
ms.date: 09/01/2016
---

# Add the TFS service account to the report server

[!INCLUDE [temp](../../_shared/version-tfs-all-versions.md)]

If the report server and Azure DevOps Server, previously named Team Foundation Server, are not on the same server, you must add the name of your Azure DevOps service account (TFSSERVICE) to the Content Manager group on the report server. This step is done automatically during Azure DevOps setup if the report server is installed on Team Foundation Server. 

If you are using Network Service for TFSSERVICE, you must add the machine name of the server that is running Azure DevOps Server instead of Network Service. The machine name is the server name followed by the $ symbol. For example, *Domain\ServerName$*.

For more information about service accounts, see [Service account requirements](../../account-requirements.md).

## Prerequisites

To perform this procedure, you must be a member of the **Administrators** security group on the report server. 

To add the service account for Team Foundation Server to the Content Manager group on the report server:

1. From the **Start** menu, choose **Reporting Services Configuration Manager**.

	> [!NOTE]   
	> On Windows Server 2008, open the shortcut menu for **Reporting Services Configuration Manager** and choose **Run as administrator**.

	The **Reporting Services Configuration Connection** dialog box appears.

2. In the **Server Name** box, enter the name of the report server. If you are using an instance name, choose the name of the instance in the **Report Server Instance** list. Choose **Connect**.

3. Choose **Report Manager URL**, and then choose the link to the report manager website. 

  The report manager website for the report server opens in an Internet browser window.

4. In the report manager website, choose the **Properties** tab, and then choose **New Role Assignment**.

5. In the **Group or user name** box, enter the name of the service account that you will use for Team Foundation Server (TFSSERVICE), select the **Content Manager** check box, and then choose **OK**.


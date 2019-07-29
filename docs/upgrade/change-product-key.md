---
title: Locate or change the product key
titleSuffix: Azure DevOps Server
description: Locate or change the product key for Azure DevOps Server
ms.manager: jillfra
ms.author: aaronha
author: aaronhallberg
ms.topic: conceptual
ms.prod: devops-server
ms.technology: tfs-admin
monikerRange: '>= tfs-2013'
ms.date: 07/28/2019
---

# Locate or change the product key for Azure DevOps Server

[!INCLUDE [temp](../_shared/version-tfs-all-versions.md)]

To move from the trial edition to the full edition of Azure DevOps Server, you must have a valid product key for Azure DevOps Server. 

You can review the license type, license expiration date, and product key number of your deployment of Azure DevOps Server. An expired or non-valid product key can disrupt your deployment. If you installed a trial edition of Azure DevOps Server, be careful not to let the license expire. After the license expires, your users will be unable to use Azure DevOps Server until you resolve the situation. You might also need to locate the product key for Azure DevOps Server for support or record-keeping purposes.

::: moniker range=">= azure-devops-2019"

- For information on any existing subscriptions and product keys, see [Visual Studio subscriptions](https://my.visualstudio.com/Subscriptions) and [Visual Studio product keys](https://my.visualstudio.com/ProductKeys).
- For information on licensing, see [Azure DevOps Server licensing](https://azure.microsoft.com/pricing/details/devops/server).
- For support with licensing issues, see [Azure DevOps support](https://azure.microsoft.com/support/devops).
 
::: moniker-end                 

::: moniker range="<= tfs-2018"

> [!NOTE]
> If you have any issues during the licensing upgrade process, see [Team Foundation Server help and support](https://visualstudio.microsoft.com/team-services/tfs-support/) and the [Visual Studio licensing whitepaper](https://visualstudio.microsoft.com/wp-content/uploads/2018/12/Visual-Studio-Licensing-Whitepaper-October-2018.pdf).     

::: moniker-end                 

## Prerequisites

You must be a member of the Administrators security group on the application-tier server for Azure DevOps Server, and a member of the Azure DevOps Administrators group. For more information, see [Add server-level administrators to Azure DevOps Server](/azure/devops/admin/add-administrator).

## Change your product key

1. Open the Azure DevOps Server Administration Console.

2. Expand the name of the server, and review the information in Product ID, License Type, and License Expires.

   The number that appears in Product ID is your product key.

3. To change or update your product key, select **Update License**.

   The Azure DevOps Server License window opens.

4. Enter the new product key, and then select **Activate**.



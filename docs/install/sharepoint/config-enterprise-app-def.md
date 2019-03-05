---
title: Configure the enterprise application definition 
titleSuffix: TFS  
description: Configure the enterprise application definition for Team Foundation Server
ms.prod: devops-server
ms.technology: tfs-admin
ms.manager: jillfra
ms.author: aaronha
author: aaronhallberg
ms.topic: conceptual
monikerRange: '<= tfs-2017'
ms.date: 09/09/2017
---

# Configure the enterprise application definition for Team Foundation Server

[!INCLUDE [temp](../../_shared/version-tfs-2013-2017.md)]

[!INCLUDE [temp](../../_shared/about-sharepoint-deprecation.md)]

If you’re using a supported enterprise edition of SharePoint Server, you must add the enterprise application definition to your deployment of Team Foundation Server. You created the enterprise application definition when you [configured SharePoint for dashboard compatibility](install-sharepoint.md). You must perform this configuration before reports and dashboards will appear correctly in Team Foundation Server. 

### To configure the enterprise application definition

1.  On the server that is running Team Foundation Server Extensions for SharePoint Products, open the administration console for Team Foundation Server.  
2.  Choose **Extensions for SharePoint Products**, and then choose the SharePoint web application for which you want to configure the enterprise application definition.  
3.  Choose **Modify access**, enter the name of the enterprise application definition in **Enterprise Application Definition (optional)**, and then choose **OK**.

## Related articles

 [Install Team Foundation Server](../install-2013/install-tfs.md)  
 [How to: Set up remote SharePoint Products for Team Foundation Server](setup-remote-sharepoint.md)
 
---
title: Team Foundation Background Job Agent
titleSuffix: Azure DevOps Server
description: Team Foundation Background Job Agent for Azure DevOps Server
ms.manager: jillfra
ms.author: aaronha
author: aaronhallberg
ms.topic: conceptual
ms.date: 03/25/2019
ms.prod: devops-server
ms.technology: tfs-admin
---

# Team Foundation Background Job Agent

[!INCLUDE [temp](../_shared/version-tfs-all-versions.md)]

The Visual Studio Team Foundation Background Job Agent service provides a general scheduling mechanism for Web services and jobs for Azure DevOps. This Windows service is also used to run the tasks spawned by various wizards, such as the New Project wizard and Create a Project Collection wizard. The service uses the service account for Azure DevOps Server, referred to as *TFSService*. The service runs on any server that is running a Web service or Web application in the logical application tier for Azure DevOps. To operate correctly, the service account for the Team Foundation Background Job Agent service must have the permissions required for the tasks that it performs.

Some services have tasks that recur at regular intervals. For example, administrators might want to schedule builds on a nightly basis. To accomplish this, build services must be able to set up an automatically scheduled event in the registration database. The Team Foundation Background Job Agent service provides a single Windows-based service to schedule repeating tasks on servers that are running Azure DevOps. The service runs through the registration database, identifies all Azure DevOps Server Web services that have scheduled events, and schedules these tasks.

## Instances

Only one instance of the Team Foundation Background Job Agent service should be running on any application-tier server for Azure DevOps. By default, the service runs under the service account that you specified when you installed Azure DevOps Server. To view the status of this service on an application-tier server, open Services and browse to find the service.

## Permissions

The Team Foundation Background Job Agent service uses the same service account as Azure DevOps Server does, *TFSService*. To operate correctly, this account requires the following permissions:

-   Log on as a service
-   Farm Administrators group for any SharePoint Web applications that Azure DevOps Server uses
-   **TFSExecRole** or both of the following for any databases that Azure DevOps Server uses:
    -   db\_owner
    -   db\_create

For more information, see [Service accounts and dependencies in Azure DevOps Server](../admin/service-accounts-dependencies.md).

## Assumptions and limitations

The Team Foundation Background Job Agent service runs continuously on all application-tier servers. Administrators should not need to manually stop or start this service except during system recovery. For example, you must stop this service before you restore databases. The service should restart automatically when a server is restarted.

Administrators don't directly configure the Team Foundation Background Job Agent service. Tasks that need to be scheduled are configured directly in individual components of Team Foundation, such as Team Foundation Build. When an event is added or deleted, the service automatically reconfigures the tasks scheduled in the registration database.

The Team Foundation Background Job Agent service logs only one instance of any given error until that error is resolved and a success message is recorded in the Event Log, or until the service is manually restarted. If you want to monitor the Event Log for that error message, you must first stop and restart the service.

The Team Foundation Background Job Agent service is not designed to be an all-purpose scheduling mechanism. It is not designed to provide scheduling precision beyond day of the week, hour of the day, and minute of the day. Most administrators don't need to schedule tasks beyond this level of granularity.

## Related articles

- [Change the service account or password for Azure DevOps Server](../admin/change-service-account-password.md) 
- [Change the service account or password for SQL Server Reporting Services](../admin/change-service-account-or-password-sql-reporting.md) 

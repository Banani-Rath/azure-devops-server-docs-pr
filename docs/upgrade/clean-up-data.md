---
title: Clean up Azure DevOps Server data
titleSuffix: Azure DevOps Server  
description: Clean up stale data in Azure DevOps Server 
ms.prod: devops-server
ms.technology: tfs-admin
toc: show
ms.manager: jillfra
ms.author: aaronha
author: aaronhallberg
ms.topic: conceptual
monikerRange: '>= tfs-2013'
ms.date: 06/04/2019
---

# Clean up old data in Azure DevOps Server

[!INCLUDE [temp](../_shared/version-tfs-all-versions.md)]

Over time, Azure DevOps Server instances can build up very large volumes of data, including files, builds, work items, and so forth. 
During the lifetime of a project, this data is valuable as a history of the various artifacts involved in producing software. Eventually the costs involved in maintaining older data - which include performance impacts and increased 
time spent on upgrades, in addition to the increased disk space requirements - may exceed the benefits.

This article provides guidance for cleaning up a variety of different types of data, primarily from Azure DevOps Server collection 
databases. 

Note that the size of any SQL data files will not decrease after cleanup, since SQL Server will reserve the space for future use.


> [!IMPORTANT] 
> In all of the following cases, once the data has been cleaned up it **cannot be recovered** except by 
restoring a database backup. Be careful to only clean up data that you are sure you no longer need. 

### Prequisite

To perform these procedures, you need to be a highly permissioned user, typically a member of a Project 
Collection or Project Administrators group. 

## Projects

If you have entire projects that are no longer needed, deleting them may have a large impact, 
since this will remove all content for the project across all feature areas. There are two ways to delete a 
project:

1. Using the [web portal](/azure/devops/organizations/projects/delete-project).

2. Using the [TfsDeleteProject](/azure/devops/server/command-line/tfsdeleteproject-cmd) tool that is included with Visual 
Studio installations.

::: moniker range="<= tfs-2017"

The primary difference between these two methods of deleting a project is that **TfsDeleteProject** will attempt to 
delete artifacts from the Sharepoint site with which Azure DevOps Server is integrated. If your Azure DevOps Server deployment is not integrated with Sharepoint, the two methods will by default perform the same set of actions.

::: moniker-end

::: moniker range=">= tfs-2018"

The two methods will by default perform the same set of actions

::: moniker-end

## Files

Typically, file contents consume the majority of the space in Azure DevOps Server collection 
databases, so cleaning up unneeded files can have a significant impact on data volume. There are many 
different types of files stored in Azure DevOps Server collection databases, including Team Foundation Version Control files, Git files, work 
item attachments, test case attachments, build outputs, and so on. Most but not all of them support cleanup. 

Note that file contents are not generally cleaned up *immediately* upon deletion, but rather by
a background job that runs on a periodic basis (typically once per day). 

### Team Foundation Version Control content

When Team Foundation Version Control (TFVC) branches, folders, and files are deleted, they are only *logically* deleted - their content 
is still available in history. TFVC branches, folders, or individual files can be physically deleted using the 
[destroy command](/azure/devops/repos/tfvc/destroy-command-team-foundation-version-control) in *tf.exe*.   

### Test attachments

Test attachments created during test runs can be cleaned up using the Test Attachment Cleaner, which is included 
with the [Azure DevOps Server Power Tools](https://visualstudiogallery.msdn.microsoft.com/f017b10c-02b4-4d6d-9845-58a06545627f). 

::: moniker range=">= tfs-2015"

Another option for cleaning up test data is to set the test retention policy for a project. To learn more, see [Control how long to keep test results](/azure/devops/test/how-long-to-keep-test-results).

::: moniker-end

## XAML Builds

When builds in Azure DevOps Server are deleted, a subset of the information they produced is preserved to avoid losing 
reporting data the next time the [warehouse is rebuilt](/azure/devops/report/admin/rebuild-data-warehouse-and-cube). Build 
data can be physically deleted using the [destroy command](/previous-versions/visualstudio/visual-studio-2010/ee794689%28v%3dvs.100%29) in 
*tfsbuild.exe*.

::: moniker range=">= tfs-2015"

In addition, you can set retention policies for your build and release pipelines. To learn more, see [Build and release retention policies](/azure/devops/pipelines/policies/retention).

::: moniker-end
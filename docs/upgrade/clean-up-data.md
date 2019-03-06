---
title: Clean up TFS data
titleSuffix: TFS  
description: Clean up stale data in your Team Foundation Server (TFS) instance
ms.prod: devops-server
ms.technology: tfs-admin
toc: show
ms.manager: jillfra
ms.author: aaronha
author: aaronhallberg
ms.topic: conceptual
monikerRange: '>= tfs-2015'
ms.date: 08/04/2016
---

# Cleaning up old data in Team Foundation Server

[!INCLUDE [temp](../_shared/version-tfs-2015-earlier.md)]

Over time, Team Foundation Server instances can build up very large volumes of data - files, builds, work items, etc. 
For the most part this is a very good thing - a big part of the value of many devops
features, after all, is maintaining a reliable history of the various artifacts involved in producing software. At 
some point, however, the costs involved in maintaining older data - which include performance impacts and increased 
time spent on upgrades in addition to the increased disk space requirements - may exceed the benefits.

This document provides guidance for cleaning up a variety of different types of data, primarily from TFS collection 
databases. Note that in all of these cases, once the data has been cleaned up it *cannot be recovered* except by 
restoring a database backup. As such, be careful to only clean up data that you are sure you will not need in the 
future. Also note that you will need to be a highly permissioned user - typically a member of a Project 
Collection or Project Administrators group - in order to perform these actions. 

Finally, it should be noted that the size of the SQL data files will not decrease after you perform any of the 
below commands, since SQL will reserve the space for later use.

## Projects

If you have whole projects that are no longer needed, deleting them can potentially have a very large impact, 
since this will remove all content for the project across all feature areas. There are two ways to delete a 
project:

1. From the [Team Foundation Server Administration Console](/azure/devops/accounts/delete-team-project#delete-team-proj).
2. Using the [TfsDeleteProject](https://msdn.microsoft.com/library/ms181482.aspx) tool that is included with Visual 
Studio installations.

The primary difference between these two methods of deleting a project is that TfsDeleteProject will attempt to 
delete artifacts from the Sharepoint site with which TFS is integrated. If your TFS deployment is not integrated 
with Sharepoint, the two methods will by default perform the same set of actions.

## Files

In most cases, file contents of one sort or another will consume the majority of the space in TFS collection 
databases, so cleaning up unneeded files can often have a significant impact on data volume. There are many 
different types of files stored in TFS collection databases, including Team Foundation Version Control files, Git files, work 
item attachments, test case attachments, build outputs, etc. Not all of them support cleanup, but check back here 
for updates. Also, note that file contents are not generally cleaned up *immediately* upon deletion, but rather by
a background job that runs on a periodic basis (typically once per day). 

### TFS VC Content

When TFS version control branches, folders, and files are deleted, they are only *logically* deleted - their content 
is still available in history. TFS VC branches, folders, or individual files can be physically deleted using the 
[destroy command](https://msdn.microsoft.com/library/bb386005.aspx) via tf.exe.   

### Test Attachments

Test attachments created during test runs can be cleaned up using the Test Attachment Cleaner, which is included 
with the [TFS Power Tools](https://visualstudiogallery.msdn.microsoft.com/f017b10c-02b4-4d6d-9845-58a06545627f). 

## XAML Builds

When builds in TFS are deleted, a subset of the information they produced is preserved in order to avoid losing 
reporting data the next time the [warehouse is rebuilt](/azure/devops/report/admin/rebuild-data-warehouse-and-cube). Build 
data can be physically deleted using the [destroy command](https://msdn.microsoft.com/library/ee794689.aspx) via 
tfsbuild.exe.

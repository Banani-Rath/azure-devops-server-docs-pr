---
title: Managing file types for Azure DevOps Server
titleSuffix: Azure DevOps Server
description: Manage file types for Azure DevOps Server
ms.topic: conceptual
ms.manager: jillfra
ms.author: aaronha
author: aaronhallberg
ms.prod: devops-server
ms.technology: tfs-admin
ms.date: 04/25/2019
---

# Manage file types with Team Foundation Version Control

[!INCLUDE [temp](../_shared/version-tfs-all-versions.md)]

Team Foundation Version Control (TFVC) provides file type definitions, which determine how files with specified extensions are processed. For example, you can disable selected file types from being merged, to prevent multiple users from checking them out in parallel.

> [!NOTE]
> By default, file merging and multiple check-out is enabled.
> Multiple check-out can be disabled at the project level.

## Prerequisites

- A TFVC repository to work in, rather than a Git repo. If you're in a Git repo, Source Control Explorer is not available.
- To edit, add, or remove a file type association, you must have the **Edit server-level information** permission set to **Allow**. For more information, see [Azure DevOps Server Permissions](/azure/devops/security/permissions).

## File type properties

An Azure DevOps file type definition consists of three properties. The most important of these properties is File Extension, which is the unique identifier for a file type.

| Property | Example |
| --- | --- |
| Name | Visual Basic File |
| File Extension | .vb |
| Enable File Merging and Multiple Checkout | Yes |

As an Azure DevOps administrator, you may want to specify that files of certain types, such as binary Microsoft Excel files (*\*.xls*) for which a merging tool does not exist, cannot be merged when conflicts are detected and can only be checked out by one user at a time. You can control this by selecting **Enable File Merging and Multiple Checkout** in the **Edit File Type** dialog box. For more information, see [Edit file type associations](#edit-file-type). If a file type does not exist for a given extension, files with that extension can be merged.

## File encodings

In addition to these basic file type properties, Azure DevOps also tracks the file encoding for each file on the version control server. You can override the default encoding for a file from the version control **Properties** window opened from **Source Control Explorer**, or using the command line interface. For more information, see [Configure version control file encoding](#config-file-encodings) and [Checkout and Edit commands](/azure/devops/tfvc/checkout-or-edit-command).

<a name="edit-file-type"></a>
## Edit file type associations

File type definitions let you customize the way the Team Foundation Version Control system processes files that have specific extensions. By defining a file type, you control whether files that have a particular extension can have internal keywords expanded during a check-in, and whether multiple users can modify a specific file in parallel. The following procedure demonstrates how to change a file type extension association in version control.

  1. On the **Team** menu, select **Azure DevOps Server Settings**, and then **Source Control File Types**. The **File Types** dialog box displays a listing of the file extensions currently associated with version control.

  2. Select **Edit**.

  3. On the **Edit File Type** dialog box, in the **Name** box, enter a description for the file type. For example, **Word Documents** for adding Microsoft Word document file association to version control.

  4. In the **File Extension** box, enter the file type extension, for example, **doc** for Microsoft Word document files.

  5. Optionally select the **Enable file merging and multiple checkout** box (selected by default).

  6. Select **OK** to return to the **File Types** dialog box and verify the new entry.

> [!TIP]
> You can specify multiple file type extension associations with a single name. For example, you could add **dot** to the **Word Documents** name entered earlier.
 

<a name="config-file-encodings"></a>
## Configure version control file encoding

Team Foundation Version Control properties include general file and folder information and the file encoding type. The properties also list the pending check-in status, security information, and branching history. For more information, see [View version control file and folder properties](/previous-versions/visualstudio/visual-studio-2012/ms245468(v=vs.110)).

> [!NOTE]
> Team Foundation Version Control properties are not viewed in Visual Studio's **Properties** window. They are viewed in their own **Properties** dialog box, as described in the following procedure.
 
To configure version control file encoding:

  1. Open **Source Control Explorer**. 

     On the **View** menu, select **Other Windows**, and then select **Source Control Explorer**.

  2. In **Source Control Explorer**, select the **Workspace** drop-down list box in the toolbar, and select the workspace you want to use.

  3. Go to a file for which you want to view properties, right-click, and then select **Properties**.

  4. In the **Properties** dialog box, select the **General** tab.

  5. In the **General** tab, select **Set Encoding**.

  6. In the **Set Encoding** dialog box, use the **Encoding** drop-down list box to select the encoding base type for the file, for example, utf-8.

      > [!TIP]
      > Select **Detect** to have the system detect the file encoding scheme used with the file and populate the list box.

  7. Select **OK**.

> [!NOTE]
> The set encoding results in a pending change that must be checked in.
 

<a name="add-file-types"></a>
## Add file type associations

File type definitions allow you to customize the way the version control system processes files with specific extensions. By defining a file type, you control whether files with a given extension allow multiple users to be able to modify a specific file in parallel. The following procedure demonstrates how to add a file type extension association in version control.

  1. On the **Team** menu, select **Azure DevOps Server Settings**, and then select **Source Control File Types**. The **File Types** dialog box is displayed listing the file extensions currently associated with version control.

  2. Select **Add**.

  3. From the **Add File Type** dialog box, in the **Name** box, type a description for the new file type, for example, **Word Documents**, to add a Microsoft Word document file association to version control.

  4. In the **File Extension** box, type or select the file type extension, for example **doc**, for Microsoft Word document files.

  5. Optionally, select the **Enable file merging and multiple check out** check box (selected by default).

  6. Select **OK** to return to the **File Types** dialog box and verify the new entry.

> [!TIP]
> You can specify multiple file type extensions to be associated with a single name, for example you could add **dot** to the **Word Documents** name entered in this procedure.
 

<a name="remove-file-types"></a>
## Remove an associated file type 

File type definitions let you customize the way the version control system handles files that have specific extensions. By defining a file type, you control whether files that have a particular extension can have internal keywords expanded during a check-in, and whether multiple users can modify a specific file in parallel. For information about adding file type associations to version control, see [Add file type association with Team Foundation Version Control](#add-file-types). The following procedure demonstrates how to remove a file type extension associated with version control.

  1. On the **Team** menu, select **Azure DevOps Server Settings**, and then select **Source Control File Types**. 

     The **File Types** dialog box displays a list of the file name extensions that are currently associated with version control.

  2. Highlight the file type extension you want to remove and then select **Remove**. 

     The entry is erased and no longer appears in the **File Types** dialog box.

  3. Select **OK**.

## Related articles

- [Team Foundation Version Control documentation](https://dev.azure.com/azure/devops/repos/TFVC/index)

---
title: SQL Server Collation Requirements for Team Foundation Server
description: SQL Server Collation Requirements for Team Foundation Server
ms.manager: jillfra
ms.author: aaronha
author: aaronhallberg
ms.topic: conceptual
ms.date: 09/01/2016
ms.prod: devops-server
ms.technology: tfs-admin
---

# SQL Server collation requirements, Azure DevOps on-premises

[!INCLUDE [temp](../../_shared/version-tfs-all-versions.md)]

When you install SQL Server, you must consider two factors regarding collation settings that could affect your Team Foundation Server deployment:

-   Requirements for Team Foundation Server 

-   All databases in all instances of SQL Server used by your Team Foundation Server deployment must have the same collation settings

You can set collation settings for the Database Engine and SQL Server Analysis Services. Collation settings include character set, sort order, and other locale-specific settings, that are fundamental to the structure and function of SQL Server databases. You cannot change these settings after installation.

## Requirements  

To work with Team Foundation Server, the collation settings for SQL Server must be case insensitive, accent sensitive, and not binary. If multiple SQL Server are running an instance of Database Engine or SQL Server Analysis Services for Team Foundation Server, the collation settings that you use must be the same across all these servers.

SQL Server bases your default collation settings on the locale of your operating system. The default setting for U.S. English and most other locales often meets the requirements for Team Foundation Server. However, those settings might not support all of the data that your organization must store in Team Foundation Server. In that case, you must find a setting that supports your data and is accent sensitive, not case sensitive, and not binary.

If you install Database Engine Services or Analysis Services, you can change collation settings on the **Server Configuration** page, by clicking the **Collation** tab and then clicking **Customize**. You may want to specify an option under **Windows collation designator and sort order**. For example, you can specify **Latin1\_General**, and select the **AS** checkbox, if you require support for additional characters.

For most other locales, the default setting is an option under **Windows collation designator and sort order**. Make sure that the settings match the requirements for Team Foundation Server. If you must change this setting, you should specify the option that is named for your locale with "\_100" after it, where possible. For example, you can use Japanese\_100 collation if you use Unicode CJK Extension A characters or Unicode surrogates in the following ways:

-   Names of objects, such as queries or projects, in Azure DevOps
-   Files or paths that are checked into the version control system
-   Any work item field that is used for searches.

To avoid problems with double-width or hiragana/katakana-equivalent characters, you should select the check boxes to enable Kana and width sensitivity when you install SQL Server.

For more information, see the Microsoft website: [Collation Settings in Setup](https://msdn.microsoft.com/library/ms143508.aspx).

## Full-Text search queries and collation settings

To support full-text search queries, the collation settings of the SQL Server database should correspond to a language that has a word breaker registered with SQL Server. If you use an unsupported language, you could receive unexpected results when you run a work item query that specifies the **Contains** or **Contains Words** operators with text strings.

To learn more, see one of the following topics:

-   [sys.fulltext\_languages (Transact-SQL)](https://docs.microsoft.com/en-us/sql/relational-databases/system-catalog-views/sys-fulltext-languages-transact-sql?view=sql-server-2017)

-   [ALTER FULLTEXT INDEX (Transact-SQL)](https://docs.microsoft.com/en-us/sql/t-sql/statements/alter-fulltext-index-transact-sql?view=sql-server-2017)

-   [SQL Server 2008 Full-Text Search: Internals and Enhancements](https://docs.microsoft.com/en-us/previous-versions/sql/sql-server-2008/cc721269(v=sql.100))

-   [Query Fields, Operators, Values, and Variables](https://docs.microsoft.com/en-us/sql/t-sql/language-elements/language-elements-transact-sql?view=sql-server-2017)

## Related articles

[Manually install SQL Server for Team Foundation Server](install-sql-server.md) 

[Install Team Foundation Server](../install-2013/install-tfs.md) 

[TFS upgrade requirements](../../upgrade/upgrade-2013/upgrade-2013-requirements.md) 

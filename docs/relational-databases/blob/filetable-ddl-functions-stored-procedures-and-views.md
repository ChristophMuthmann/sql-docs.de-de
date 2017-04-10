---
title: "FileTable-DDL, Funktionen, gespeicherte Prozeduren und Sichten | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-blob"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "FileTables [SQL Server], Datenbankobjekte"
ms.assetid: 7e2e0f7f-94a8-4178-8bc7-d2e14ac8528c
caps.latest.revision: 13
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 13
---
# FileTable-DDL, Funktionen, gespeicherte Prozeduren und Sichten
  Listet die [!INCLUDE[tsql](../../includes/tsql-md.md)] -Anweisungen und die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbankobjekte auf, die zur Unterstützung der FileTable-Funktion in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]hinzugefügt oder geändert wurden.  
  
 Die Spalte "Status" in den folgenden Tabellen gibt an, ob das Element in [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]neu ist oder in früheren Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] vorhanden war und in [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] geändert wurde, um die semantische Suche zu unterstützen.  
  
 Eine Liste der Anweisungen und Datenbankobjekte, die FILESTREAM unterstützen, finden Sie unter [FILESTREAM DDL, Functions, Stored Procedures, and Views](../../relational-databases/blob/filestream-ddl-functions-stored-procedures-and-views.md).  
  
##  <a name="ddl"></a> Transact-SQL-DDL-Anweisungen (Data Definition Language, Datendefinitionssprache)  
  
|Objekt|Status|Weitere Informationen|  
|------------|------------|----------------------|  
|[ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)<br /><br /> [ALTER DATABASE SET-Optionen &#40;Transact-SQL&#41;](../Topic/ALTER%20DATABASE%20SET%20Options%20\(Transact-SQL\).md)|Geändert|[Aktivieren der erforderlichen Komponenten für FileTable](../../relational-databases/blob/enable-the-prerequisites-for-filetable.md)<br /><br /> [Verwalten von FileTables](../../relational-databases/blob/manage-filetables.md)|  
|[ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)|Geändert|[Erstellen, Ändern und Löschen von FileTables](../../relational-databases/blob/create-alter-and-drop-filetables.md)<br /><br /> [Verwalten von FileTables](../../relational-databases/blob/manage-filetables.md)|  
|[CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)|Geändert|[Aktivieren der erforderlichen Komponenten für FileTable](../../relational-databases/blob/enable-the-prerequisites-for-filetable.md)|  
|[CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)|Geändert|[Erstellen, Ändern und Löschen von FileTables](../../relational-databases/blob/create-alter-and-drop-filetables.md)|  
|[RESTORE &#40;Transact-SQL&#41;](../Topic/RESTORE%20\(Transact-SQL\).md)<br /><br /> [RESTORE-Argumente &#40;Transact-SQL&#41;](../Topic/RESTORE%20Arguments%20\(Transact-SQL\).md)|Geändert||  
  
##  <a name="func"></a> Funktionen  
  
|Objekt|Status|Weitere Informationen|  
|------------|------------|----------------------|  
|[FileTableRootPath &#40;Transact-SQL&#41;](../../relational-databases/system-functions/filetablerootpath-transact-sql.md)|**Hinzugefügt**|[Arbeiten mit Verzeichnissen und Pfaden in FileTables](../../relational-databases/blob/work-with-directories-and-paths-in-filetables.md)|  
|[GetFileNamespacePath &#40;Transact-SQL&#41;](../../relational-databases/system-functions/getfilenamespacepath-transact-sql.md)|**Hinzugefügt**|[Arbeiten mit Verzeichnissen und Pfaden in FileTables](../../relational-databases/blob/work-with-directories-and-paths-in-filetables.md)|  
|[GetPathLocator &#40;Transact-SQL&#41;](../../relational-databases/system-functions/getpathlocator-transact-sql.md)|**Hinzugefügt**|[Arbeiten mit Verzeichnissen und Pfaden in FileTables](../../relational-databases/blob/work-with-directories-and-paths-in-filetables.md)|  
  
##  <a name="sproc"></a> Gespeicherte Prozeduren  
  
|Objekt|Status|Weitere Informationen|  
|------------|------------|----------------------|  
|[sp_kill_filestream_non_transacted_handles &#40;Transact-SQL&#41;](../Topic/sp_kill_filestream_non_transacted_handles%20\(Transact-SQL\).md)|**Hinzugefügt**|[Verwalten von FileTables](../../relational-databases/blob/manage-filetables.md)|  
  
##  <a name="cv"></a> Katalogsichten  
  
|Objekt|Status|Weitere Informationen|  
|------------|------------|----------------------|  
|[sys.database_filestream_options &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-filestream-options-transact-sql.md)|**Hinzugefügt**|[Aktivieren der erforderlichen Komponenten für FileTable](../../relational-databases/blob/enable-the-prerequisites-for-filetable.md)|  
|[sys.filetable_system_defined_objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-filetable-system-defined-objects-transact-sql.md)|**Hinzugefügt**|[Erstellen, Ändern und Löschen von FileTables](../../relational-databases/blob/create-alter-and-drop-filetables.md)<br /><br /> [Verwalten von FileTables](../../relational-databases/blob/manage-filetables.md)|  
|[sys.filetables &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-filetables-transact-sql.md)|**Hinzugefügt**|[Verwalten von FileTables](../../relational-databases/blob/manage-filetables.md)|  
|[sys.tables &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-tables-transact-sql.md)|Geändert|[Verwalten von FileTables](../../relational-databases/blob/manage-filetables.md)|  
  
##  <a name="dmv"></a> Dynamische Verwaltungssichten  
  
|Objekt|Status|Weitere Informationen|  
|------------|------------|----------------------|  
|[sys.dm_filestream_non_transacted_handles &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-filestream-non-transacted-handles-transact-sql.md)|**Hinzugefügt**|[Verwalten von FileTables](../../relational-databases/blob/manage-filetables.md)|  
  
## Siehe auch  
 [Verwalten von FileTables](../../relational-databases/blob/manage-filetables.md)  
  
  
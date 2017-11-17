---
title: DROP DATABASE (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 09/15/2017
ms.prod: sql-non-specified
ms.prod_service: sql-data-warehouse, database-engine, pdw, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DROP DATABASE
- DROP_DATABASE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- snapshots [SQL Server database snapshots], deleting
- removing databases
- database snapshots [SQL Server], removing
- deleting databases
- dropping databases
- databases [SQL Server], dropping
- DROP DATABASE statement
- database removal [SQL Server], DROP DATABASE statement
ms.assetid: 477396a9-92dc-43c9-9b97-42c8728ede8e
caps.latest.revision: 83
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: aecf422ca2289b2a417147eb402921bb8530d969
ms.openlocfilehash: 6e1a96bb64c8cb6a81311f422d370e36d9489ca4
ms.contentlocale: de-de
ms.lasthandoff: 10/24/2017

---
# <a name="drop-database-transact-sql"></a>DROP DATABASE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-asdb-asdw-pdw-md.md)]

  Entfernt eine oder mehrere Benutzerdatenbanken oder Datenbank-Momentaufnahmen aus einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
-- SQL Server Syntax  
DROP DATABASE [ IF EXISTS ] { database_name | database_snapshot_name } [ ,...n ] [;]  
```  
  
```  
-- Azure SQL Database, Azure SQL Data Warehouse and Parallel Data Warehouse Syntax   
DROP DATABASE database_name [;]  
```  
  
## <a name="arguments"></a>Argumente  
 *IF VORHANDEN IST*  
 **Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] bis zur [aktuellen Version](http://go.microsoft.com/fwlink/p/?LinkId=299658)).  
  
 Bedingt löscht die Datenbank nur dann, wenn sie bereits vorhanden ist.  
  
 *database_name*  
 Gibt den Namen der zu entfernenden Datenbank an. Um eine Liste der Datenbanken anzuzeigen, verwenden Sie die [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) -Katalogsicht angezeigt.  
  
 *database_snapshot_name*  
 **Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Gibt den Namen der zu entfernenden Datenbankmomentaufnahme an.  
  
## <a name="general-remarks"></a>Allgemeine Hinweise  
 Eine Datenbank kann unabhängig von ihrem Status (offline, schreibgeschützt, fehlerverdächtig usw.) gelöscht werden. Um den aktuellen Status einer Datenbank anzuzeigen, verwenden Sie die **sys.databases** -Katalogsicht angezeigt.  
  
 Eine gelöschte Datenbank kann neu erstellt werden, nur von einer Sicherung wiederherstellen. Datenbankmomentaufnahmen können nicht gesichert und somit nicht wiederhergestellt werden.  
  
 Wenn eine Datenbank gelöscht wird, die [master-Datenbank](../../relational-databases/databases/master-database.md) sollte gesichert werden.  
  
 Beim Löschen einer Datenbank wird die Datenbank von der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz entfernt, und die von der Datenbank verwendeten physischen Datenträgerdateien werden gelöscht. Wenn die Datenbank oder eine ihrer Dateien beim Löschen offline ist, werden die Datenträgerdateien nicht gelöscht. Diese Dateien können manuell mit dem Windows-Explorers gelöscht werden. Um eine Datenbank aus dem aktuellen Server zu entfernen, ohne die Dateien aus dem Dateisystem zu löschen, verwenden Sie [Sp_detach_db](../../relational-databases/system-stored-procedures/sp-detach-db-transact-sql.md).  
  
> [!WARNING]  
>  Löschen eine Datenbank mit FILE_SNAPSHOT Sicherungen ist erfolgreich, aber die Datenbankdateien, die Momentaufnahmen zugeordnet sind werden nicht entfernt werden, um zu vermeiden, dass die Sicherungen auf diese Datenbankdateien verweisen. Die Datei wird abgeschnitten, jedoch nicht physisch gelöscht, um die Sicherungen FILE_SNAPSHOT intakt zu halten. Weitere Informationen finden Sie unter [SQL Server Backup and Restore with Windows Azure Blob Storage Service](../../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md). **Gilt für**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] über [aktuelle Version](http://go.microsoft.com/fwlink/p/?LinkId=299658).  
  
### [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 Wenn Sie eine Datenbankmomentaufnahme löschen, wird diese aus einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz gelöscht. Außerdem werden die Sparsedateien des physischen NTFS-Dateisystems gelöscht, die von der Momentaufnahme verwendet werden. Informationen zum Verwenden von Dateien mit geringer Dichte von datenbankmomentaufnahmen finden Sie unter [Datenbankmomentaufnahmen &#40; SQLServer &#41; ](../../relational-databases/databases/database-snapshots-sql-server.md). Durch das Löschen einer Datenbankmomentaufnahme wird der Plancache für die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gelöscht. Durch das Löschen des Plancaches wird eine Neukompilierung aller nachfolgenden Ausführungspläne verursacht, und möglicherweise entsteht plötzlich eine temporäre Verringerung der Abfrageleistung. Für jeden gelöschten Cachespeicher im Plancache enthält das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Fehlerprotokoll folgende Informationsmeldung: "[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] hat für den %s-Cachespeicher (Bestandteil des Plancache) %d Leerungen des Cachespeichers gefunden, die von Datenbankwartungs- oder Neukonfigurierungsvorgängen ausgelöst wurden". Diese Meldung wird alle fünf Minuten protokolliert, solange der Cache innerhalb dieses Zeitintervalls geleert wird.  
  
## <a name="interoperability"></a>Interoperabilität  
  
### <a name="sql-server"></a>SQL Server  
 Zum Löschen einer für die Transaktionsreplikation oder die Mergereplikation veröffentlichten Datenbank bzw. einer von der Mergereplikation abonnierten Datenbank müssen Sie zunächst die Replikation von der Datenbank entfernen. Wenn eine Datenbank beschädigt ist oder die Replikation nicht zuerst entfernt werden kann, oder wenn beides zutrifft, können Sie die Datenbank dennoch mithilfe von ALTER DATABASE löschen. Sie legen hierzu den Status der Datenbank auf offline fest und löschen diese dann.  
  
 Wenn die Datenbank für den Protokollversand verwendet wird, müssen Sie den Protokollversand vor dem Löschen der Datenbank entfernen. Weitere Informationen finden Sie unter [Informationen zum Protokollversand &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md).  
  
  
## <a name="limitations-and-restrictions"></a>Einschränkungen  
 [Systemdatenbanken](../../relational-databases/databases/system-databases.md) kann nicht gelöscht werden.  
  
 Die DROP DATABASE-Anweisung muss im Autocommitmodus ausgeführt werden und ist in einer expliziten oder impliziten Transaktion nicht zulässig. Der Autocommitmodus ist der Standardmodus für die Transaktionsverwaltung.  
  
 Sie können eine aktuell verwendete Datenbank nicht löschen. Dies bezieht sich auf eine von einem beliebigen Benutzer für Schreib- oder Lesevorgänge geöffnete Datei. Zum Entfernen von Benutzern aus der Datenbank legen Sie die Datenbank mithilfe von ALTER DATABASE auf SINGLE_USER fest.  
  
### [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 Alle Datenbankmomentaufnahmen in einer Datenbank müssen vor dem Löschen der Datenbank gelöscht werden.  
  
 Löschen eine Datenbank aktivieren, für Stretch-Datenbank entfernt die Remotedaten nicht. Wenn Sie die Remotedaten löschen möchten, müssen Sie manuell entfernen.  
  
### [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]  
 Sie müssen mit der master-Datenbank verbunden sein, um eine Datenbank zu löschen.
  
 Die DROP DATABASE-Anweisung muss die einzige Anweisung in einem SQL-Batch sein, und es darf jeweils nur eine Datenbank gelöscht werden.
  
### [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]  
 Sie müssen mit der master-Datenbank verbunden sein, um eine Datenbank zu löschen.
  
 Die DROP DATABASE-Anweisung muss die einzige Anweisung in einem SQL-Batch sein, und es darf jeweils nur eine Datenbank gelöscht werden.

## <a name="permissions"></a>Berechtigungen  
  
### [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 Erfordert die **Steuerelement** Berechtigung für die Datenbank oder **ALTER ANY DATABASE** Berechtigung oder die Mitgliedschaft in der **Db_owner** festen Datenbankrolle "".  
  
### [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]  
 Nur der prinzipalanmeldung auf Serverebene (vom im Rahmen des Bereitstellungsprozesses erstellt) oder Mitglieder der **Dbmanager** Datenbankrolle kann eine Datenbank löschen.  
  
### [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 Erfordert die **Steuerelement** Berechtigung für die Datenbank oder **ALTER ANY DATABASE** Berechtigung oder die Mitgliedschaft in der **Db_owner** festen Datenbankrolle "".  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-dropping-a-single-database"></a>A. Löschen einer einzelnen Datenbank  
 Im folgenden Beispiel wird die Datenbank `Sales` entfernt.  
  
```  
DROP DATABASE Sales;  
```  
  
### <a name="b-dropping-multiple-databases"></a>B. Löschen mehrerer Datenbanken  
  
**Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Im folgenden Beispiel wird jede der aufgelisteten Datenbanken entfernt.  
  
```  
DROP DATABASE Sales, NewSales;  
```  
  
### <a name="c-dropping-a-database-snapshot"></a>C. Löschen einer Datenbankmomentaufnahme  
  
**Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Im folgenden Beispiel wird eine Datenbankmomentaufnahme namens `sales_snapshot0600`, ohne Auswirkungen auf die Quelldatenbank.  
  
```  
DROP DATABASE sales_snapshot0600;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)  
  
  


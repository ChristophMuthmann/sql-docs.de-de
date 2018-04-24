---
title: Anzeigen von Informationen zum Daten- und Protokollspeicherplatz einer Datenbank | Microsoft-Dokumentation
ms.custom: ''
ms.date: 08/01/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: databases
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- logs [SQL Server], space
- status information [SQL Server], space
- displaying space information
- disk space [SQL Server], displaying
- databases [SQL Server], space used
- viewing space information
- space allocation [SQL Server], displaying
- data space [SQL Server]
ms.assetid: c7b99463-4bab-4e9b-9217-fcb0898dc757
caps.latest.revision: 28
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Active
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 854bd5c89a60ae459d2427207af9fecd2980e398
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="display-data-and-log-space-information-for-a-database"></a>Anzeigen von Informationen zum Daten- und Protokollspeicherplatz einer Datenbank
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  In diesem Thema wird beschrieben, wie die Informationen zum Daten- und Protokollspeicherplatz einer Datenbank in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] oder [!INCLUDE[tsql](../../includes/tsql-md.md)]angezeigt werden.  

  
##  <a name="BeforeYouBegin"></a> Vorbereitungsmaßnahmen  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
 Die Berechtigung zum Ausführen von **sp_spaceused** wird der **public** -Rolle erteilt. Nur Mitglieder der festen Datenbankrolle **db_owner** können den Parameter **@updateusage** angeben.  
  
##  <a name="SSMSProcedure"></a> Verwenden von SQL Server Management Studio  
  
#### <a name="to-display-data-and-log-space-information-for-a-database"></a>So zeigen Sie Informationen zum Daten- und Protokollspeicherplatz einer Datenbank an  
  
1.  Stellen Sie im Objekt-Explorer eine Verbindung mit einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] her, und erweitern Sie dann diese Instanz.  
  
2.  Erweitern Sie **Datenbanken**.  
  
3.  Klicken Sie mit der rechten Maustaste auf eine Datenbank, zeigen Sie auf **Berichte**, zeigen Sie auf **Standardberichte**, und klicken Sie dann auf **Datenträgerverwendung**.  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
  
#### <a name="to-display-data-and-log-space-information-for-a-database-by-using-spspaceused"></a>So zeigen Sie Informationen zum Daten- und Protokollspeicherplatz einer Datenbank mit sp_spaceused an  
  
1.  Stellen Sie eine Verbindung mit dem [!INCLUDE[ssDE](../../includes/ssde-md.md)]her.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Kopieren Sie das folgende Beispiel, fügen Sie es in das Abfragefenster ein, und klicken Sie auf **Ausführen**. In diesem Beispiel wird die gespeicherte Systemprozedur [sp_spaceused](../../relational-databases/system-stored-procedures/sp-spaceused-transact-sql.md) verwendet, um Speicherplatzinformationen für die `Vendor` -Tabelle und ihre Indizes zu melden.  
  
```sql  
USE AdventureWorks2012;  
GO  
EXEC sp_spaceused N'Purchasing.Vendor';  
GO  
```  
  
#### <a name="to-display-data-and-log-space-information-for-a-database-by-querying-sysdatabasefiles"></a>So zeigen Sie Daten und Protokollspeicherplatzinformationen für eine Datenbank durch das Abfragen von sys.database_files an  
  
1.  Stellen Sie eine Verbindung mit dem [!INCLUDE[ssDE](../../includes/ssde-md.md)]her.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Kopieren Sie das folgende Beispiel, fügen Sie es in das Abfragefenster ein, und klicken Sie auf **Ausführen**. In diesem Beispiel wird die Katalogsicht [sys.database_files](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md) abgefragt, um bestimmte Informationen zu den Daten- und Protokolldateien in der [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] -Datenbank zurückzugeben.  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT file_id, name, type_desc, physical_name, size, max_size  
FROM sys.database_files ;  
GO  
  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [sys.database_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)   
 [sp_spaceused &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-spaceused-transact-sql.md)   
 [Hinzufügen von Daten- oder Protokolldateien zu einer Datenbank](../../relational-databases/databases/add-data-or-log-files-to-a-database.md)   
 [Löschen von Daten- oder Protokolldateien aus einer Datenbank](../../relational-databases/databases/delete-data-or-log-files-from-a-database.md)  
  
  

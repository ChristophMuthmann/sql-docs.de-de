---
title: DBCC UPDATEUSAGE (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 11/14/2017
ms.prod: sql
ms.prod_service: sql-database
ms.service: ''
ms.component: t-sql|database-console-commands
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- UPDATEUSAGE
- UPDATEUSAGE_TSQL
- DBCC_UPDATEUSAGE_TSQL
- DBCC UPDATEUSAGE
dev_langs:
- TSQL
helpviewer_keywords:
- inaccurate page or row counts [SQL Server]
- space [SQL Server], usage reports
- updating space usage information
- updating row counts
- disk space [SQL Server], inaccurate counts
- counting pages
- reporting count inaccuracies
- updating page counts
- synchronization [SQL Server], inaccurate counts
- incorrect space usage reports [SQL Server]
- DBCC UPDATEUSAGE statement
- integrity [SQL Server], database objects
- counting rows
- row count accuracy [SQL Server]
- page count accuracy [SQL Server]
ms.assetid: b8752ecc-db45-4e23-aee7-13b8bc3cbae2
caps.latest.revision: 56
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 3338bfa3aaf532d639184b78554240228e077428
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="dbcc-updateusage-transact-sql"></a>DBCC UPDATEUSAGE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Meldet und behebt Ungenauigkeiten bei den Seiten- und Zeilenzahlen in den Katalogsichten. Diese Ungenauigkeiten können falsche Berichte über die Speicherplatzverwendung verursachen, die von der gespeicherten Systemprozedur sp_spaceused zurückgegeben werden.
  
![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Syntax  
  
```sql
DBCC UPDATEUSAGE   
(   { database_name | database_id | 0 }   
    [ , { table_name | table_id | view_name | view_id }   
    [ , { index_name | index_id } ] ]   
) [ WITH [ NO_INFOMSGS ] [ , ] [ COUNT_ROWS ] ]   
```  
  
## <a name="arguments"></a>Argumente  
*database_name* | *database_id* | 0  
Name oder ID der Datenbank, deren Statistiken zur Speicherverwendung mitgeteilt und korrigiert werden sollen. Wird 0 angegeben, wird die aktuelle Datenbank verwendet. Datenbanknamen müssen den Regeln für [Bezeichner](../../relational-databases/databases/database-identifiers.md) entsprechen.  
  
*table_name* | *table_id* | *view_name* | *view_id*  
Name oder ID der Tabelle oder indizierten Sicht, deren Statistiken zur Speicherverwendung mitgeteilt und korrigiert werden sollen. Tabellen- und Sichtnamen müssen den Regeln für Bezeichner entsprechen.  
  
*index_id* | *index_name*  
ID oder Name des zu verwendenden Indexes. Falls nicht angegeben, werden von der Anweisung alle Indizes der angegebenen Tabelle oder Sicht verarbeitet.  
  
mit  
Ermöglicht die Angabe von Optionen.  
  
NO_INFOMSGS  
Alle Informationsmeldungen werden unterdrückt.  
  
COUNT_ROWS  
Gibt an, dass die row count-Spalte mit der aktuellen Anzahl von Tabellen- oder Sichtzeilen aktualisiert wird.  
  
## <a name="remarks"></a>Remarks  
DBCC UPDATEUSAGE korrigiert die Anzahl der Zeilen, verwendeten Seiten, reservierten Seiten, Blattseiten und Datenseiten jeder Partition in Tabellen und Indizes. Wurden keine Ungenauigkeiten in den Systemtabellen festgestellt, werden von DBCC UPDATEUSAGE keine Daten zurückgegeben. Wurden Ungenauigkeiten gefunden und korrigiert und wurde WITH NO_INFOMSGS nicht verwendet, gibt DBCC UPDATEUSAGE die Zeilen und Spalten zurück, die in den Systemtabellen aktualisiert wurden.
  
DBCC CHECKDB wurde verbessert, sodass nun erkannt wird, wenn Seiten- oder Zeilenzähler negativ werden. Wenn dies festgestellt wird, enthält die Ausgabe von DBCC CHECKDB eine Warnung und die Empfehlung, DBCC UPDATEUSAGE auszuführen, um das Problem zu beseitigen.
  
## <a name="best-practices"></a>Bewährte Methoden  
Es wird Folgendes empfohlen:
-   Führen Sie DBCC UPDATEUSAGE nicht routinemäßig aus. Da das Ausführen von DBCC UPDATEUSAGE für große Tabellen oder Datenbanken einige Zeit in Anspruch nehmen kann, sollte es nur dann verwendet werden, wenn Sie vermuten, dass falsche Werte von sp_spaceused zurückgegeben werden.
-   Führen Sie DBCC UPDATEUSAGE nur dann routinemäßig (z. B. wöchentlich) aus, wenn die Datenbank häufig mithilfe der Datendefinitionssprache (Data Definition Language, DDL) z. B. durch die Anweisungen CREATE, ALTER oder DROP geändert wird.  
  
## <a name="result-sets"></a>Resultsets  
DBCC UPDATEUSAGE gibt Folgendes zurück (die tatsächlichen Werte können davon abweichen):
  
`DBCC execution completed. If DBCC printed error messages, contact your system administrator.`
  
## <a name="permissions"></a>Berechtigungen  
Erfordert die Mitgliedschaft in der festen Serverrolle **sysadmin** oder der festen Datenbankrolle **db_owner** .
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-updating-page-or-row-counts-or-both-for-all-objects-in-the-current-database"></a>A. Aktualisieren von Seiten- oder Zeilenzahlen oder beidem für alle Objekte in der aktuellen Datenbank  
Im folgenden Beispiel wird `0` für den Datenbanknamen angegeben, und `DBCC UPDATEUSAGE` meldet aktualisierte Informationen zur Seiten- oder Zeilenzahl für die aktuelle Datenbank.
  
```sql
DBCC UPDATEUSAGE (0);  
GO  
```  
  
### <a name="b-updating-page-or-row-counts-or-both-for-adventureworks-and-suppressing-informational-messages"></a>B. Aktualisieren von Seiten- oder Zeilenzahlen oder beidem für AdventureWorks und Unterdrücken von Informationsmeldungen  
Im folgenden Beispiel wird [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] als Datenbankname angegeben, und es werden alle Informationsmeldungen unterdrückt.
  
```sql
DBCC UPDATEUSAGE (AdventureWorks2012) WITH NO_INFOMSGS;   
GO  
```  
  
### <a name="c-updating-page-or-row-counts-or-both-for-the-employee-table"></a>C. Aktualisieren von Seiten- oder Zeilenzahlen oder beidem für die Employee-Tabelle  
Im folgenden Beispiel werden aktualisierte Informationen zur Seiten- oder Zeilenzahl für die `Employee`-Tabelle in der [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]-Datenbank gemeldet.
  
```sql
DBCC UPDATEUSAGE (AdventureWorks2012,'HumanResources.Employee');  
GO  
```  
  
### <a name="d-updating-page-or-row-counts-or-both-for-a-specific-index-in-a-table"></a>D. Aktualisieren von Seiten- oder Zeilenzahlen oder beidem für einen bestimmten Index in einer Tabelle  
 Im folgenden Beispiel wird `IX_Employee_ManagerID` als Indexname angegeben.  
  
```sql
DBCC UPDATEUSAGE (AdventureWorks2012, 'HumanResources.Employee', IX_Employee_OrganizationLevel_OrganizationNode);  
GO  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
[sp_spaceused &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-spaceused-transact-sql.md)  
[UPDATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/update-statistics-transact-sql.md)
  
  

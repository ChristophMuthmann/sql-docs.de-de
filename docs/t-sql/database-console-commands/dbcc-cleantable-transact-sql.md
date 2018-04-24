---
title: DBCC CLEANTABLE (Transact-SQL) | Microsoft-Dokumentation
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
- CLEANTABLE_TSQL
- DBCC_CLEANTABLE_TSQL
- DBCC CLEANTABLE
- CLEANTABLE
dev_langs:
- TSQL
helpviewer_keywords:
- disk space [SQL Server], reclaiming
- reclaiming space
- reallocating space
- removing columns
- DBCC CLEANTABLE statement
- space [SQL Server], reclaiming
- deleting columns
- dropping columns
ms.assetid: 0dbbc956-15b1-427b-812c-618a044d07fa
caps.latest.revision: 53
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 9c8402749a51331741335139efffb1195218152e
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="dbcc-cleantable-transact-sql"></a>DBCC CLEANTABLE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]
Gibt Speicherplatz wieder frei, der von gelöschten Spalten mit variabler Länge in Tabellen oder indizierten Sichten belegt wurde.
![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Syntax  
  
```sql
  
DBCC CLEANTABLE  
(  
    { database_name | database_id | 0 }  
    , { table_name | table_id | view_name | view_id }  
    [ , batch_size ]  
)  
[ WITH NO_INFOMSGS ]  
```  
  
## <a name="arguments"></a>Argumente  
 *database_name* | *database_id* | 0  
 Die Datenbank, zu der die Tabelle gehört, für die ein Cleanup ausgeführt werden soll. Wird 0 angegeben, wird die aktuelle Datenbank verwendet. Datenbanknamen müssen den Regeln für [Bezeichner](../../relational-databases/databases/database-identifiers.md) entsprechen.  
  
 *table_name* | *table_id* | *view_name*| *view_id*  
 Die Tabelle oder indizierte Sicht, für die ein Cleanup ausgeführt werden soll.  
  
 *batch_size*  
 Die Anzahl von Zeilen, die pro Transaktion verarbeitet werden sollen. Wird dieser Parameter nicht angegeben oder der Wert 0 angegeben, verarbeitet die Anweisung die gesamte Tabelle in einer Transaktion.  
  
 WITH NO_INFOMSGS  
 Alle Informationsmeldungen werden unterdrückt.  
  
## <a name="remarks"></a>Remarks  
DBCC CLEANTABLE gibt Speicherplatz wieder frei, nachdem eine Spalte mit variabler Länge gelöscht wurde. Eine Spalte mit variabler Länge kann einem der folgenden Datentypen entsprechen: **varchar**, **nvarchar**, **varchar(max)**, **nvarchar(max)**, **varbinary**, **varbinary(max)**, **text**, **ntext**, **image**, **sql_variant** und **xml**. Nach dem Löschen einer Spalte mit fester Länge wird jedoch kein Speicherplatz geschaffen.
Falls die gelöschten Spalten innerhalb von Zeilen gespeichert waren, gibt DBCC CLEANTABLE Speicherplatz aus der IN_ROW_DATA-Zuordnungseinheit der Tabelle frei. Waren die Spalten außerhalb von Zeilen gespeichert, wird Speicherplatz je nach dem Datentyp der gelöschten Spalte aus einer der Zuordnungseinheiten ROW_OVERFLOW_DATA oder LOB_DATA freigegeben. Falls durch das Freigeben von Speicherplatz aus einer ROW_OVERFLOW_DATA- oder LOB_DATA-Seite eine leere Seite entsteht, wird diese durch DBCC CLEANTABLE entfernt.
DBCC CLEANTABLE wird als eine oder mehrere Transaktionen ausgeführt. Wird keine Batchgröße angegeben, verarbeitet der Befehl die gesamte Tabelle in einer Transaktion, und die Tabelle wird während des Vorgangs exklusiv gesperrt. Für einige große Tabellen sind eine einzige Transaktion und der erforderliche Protokollspeicherplatz möglicherweise zu groß. Wenn eine Batchgröße angegeben wurde, wird der Befehl in einer Reihe von Transaktionen ausgeführt, wobei jede die angegebene Zeilenanzahl einschließt. DBCC CLEANTABLE kann nicht als eine Transaktion innerhalb einer anderen Transaktion ausgeführt werden.
Diese Operation wird vollständig protokolliert.
DBCC CLEANTABLE wird nicht für die Verwendung in Systemtabellen, temporären Tabellen oder im speicheroptimierten xVelocity-columnstore-Indexbereich einer Tabelle unterstützt.
  
## <a name="best-practices"></a>Bewährte Methoden  
DBCC CLEANTABLE sollte nicht als routinemäßiger Wartungstask ausgeführt werden. Verwenden Sie DBCC CLEANTABLE, wenn Sie wesentliche Änderungen an Spalten mit variabler Länge in einer Tabelle oder indizierten Sicht vorgenommen haben und den nicht verwendeten Speicherplatz sofort freigeben müssen. Alternativ können Sie auch die Indizes für die Tabelle oder Sicht neu erstellen. Dies ist jedoch ein ressourcenintensiverer Vorgang.
  
## <a name="result-sets"></a>Resultsets  
DBCC CLEANTABLE gibt Folgendes zurück:
  
```sql
DBCC execution completed. If DBCC printed error messages, contact your system administrator.  
```  
  
## <a name="permissions"></a>Berechtigungen  
 Bei dem Aufrufer muss es sich um den Besitzer der Tabelle bzw. der indizierten Sicht oder um ein Mitglied der festen Serverrolle **sysadmin**, der festen Datenbankrolle **db_owner** oder der festen Datenbankrolle **db_ddladmin** handeln.  
  
## <a name="examples"></a>Beispiele  
### <a name="a-using-dbcc-cleantable-to-reclaim-space"></a>A. Freigeben von Speicherplatz mit DBCC CLEANTABLE  
Im folgenden Beispiel wird DBCC CLEANTABLE für die `Production.Document`-Tabelle in der [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]-Beispieldatenbank ausgeführt.
  
```sql  
DBCC CLEANTABLE (AdventureWorks2012,'Production.Document', 0)  
WITH NO_INFOMSGS;  
GO  
```  
  
### <a name="b-using-dbcc-cleantable-and-verifying-results"></a>B. Verwenden von DBCC CLEANTABLE und Überprüfen von Ergebnissen  
Im folgenden Beispiel wird eine Tabelle mit mehreren Spalten variabler Länge erstellt und aufgefüllt. Anschließend werden zwei Spalten gelöscht, und DBCC CLEANTABLE wird ausgeführt, um den nicht verwendeten Speicherplatz freizugeben. Es wird eine Abfrage ausgeführt, um die Werte für die Seitenanzahl und den verwendeten Speicherplatz vor und nach der Ausführung des DBCC CLEANTABLE-Befehls zu überprüfen.
  
```sql  
USE AdventureWorks2012;  
GO  
IF OBJECT_ID ('dbo.CleanTableTest', 'U') IS NOT NULL  
    DROP TABLE dbo.CleanTableTest;  
GO  
CREATE TABLE dbo.CleanTableTest  
    (FileName nvarchar(4000),   
    DocumentSummary nvarchar(max),  
    Document varbinary(max)  
    );  
GO  
-- Populate the table with data from the Production.Document table.  
INSERT INTO dbo.CleanTableTest  
    SELECT REPLICATE(FileName, 1000),   
           DocumentSummary,   
           Document  
    FROM Production.Document;  
GO  
-- Verify the current page counts and average space used in the dbo.CleanTableTest table.  
DECLARE @db_id SMALLINT;  
DECLARE @object_id INT;  
SET @db_id = DB_ID(N'AdventureWorks2012');  
SET @object_id = OBJECT_ID(N'AdventureWorks2012.dbo.CleanTableTest');  
SELECT alloc_unit_type_desc,   
       page_count,   
       avg_page_space_used_in_percent,   
       record_count  
FROM sys.dm_db_index_physical_stats(@db_id, @object_id, NULL, NULL , 'Detailed');  
GO  
-- Drop two variable-length columns from the table.  
ALTER TABLE dbo.CleanTableTest  
DROP COLUMN FileName, Document;  
GO  
-- Verify the page counts and average space used in the dbo.CleanTableTest table  
-- Notice that the values have not changed.  
DECLARE @db_id SMALLINT;  
DECLARE @object_id INT;  
SET @db_id = DB_ID(N'AdventureWorks2012');  
SET @object_id = OBJECT_ID(N'AdventureWorks2012.dbo.CleanTableTest');  
SELECT alloc_unit_type_desc,   
       page_count,   
       avg_page_space_used_in_percent,   
       record_count  
FROM sys.dm_db_index_physical_stats(@db_id, @object_id, NULL, NULL , 'Detailed');  
GO  
-- Run DBCC CLEANTABLE.  
DBCC CLEANTABLE (AdventureWorks2012,'dbo.CleanTableTest');  
GO  
-- Verify the values in the dbo.CleanTableTest table after the DBCC CLEANTABLE command.  
DECLARE @db_id SMALLINT;  
DECLARE @object_id INT;  
SET @db_id = DB_ID(N'AdventureWorks2012');  
SET @object_id = OBJECT_ID(N'AdventureWorks2012.dbo.CleanTableTest');  
SELECT alloc_unit_type_desc,   
       page_count,   
       avg_page_space_used_in_percent,   
       record_count  
FROM sys.dm_db_index_physical_stats(@db_id, @object_id, NULL, NULL , 'Detailed');  
GO  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
 [sys.allocation_units &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-allocation-units-transact-sql.md)  
  
  

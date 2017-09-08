---
title: DBCC INDEXDEFRAG (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/16/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- INDEXDEFRAG
- DBCC INDEXDEFRAG
- DBCC_INDEXDEFRAG_TSQL
- INDEXDEFRAG_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- defragmenting indexes
- DBCC INDEXDEFRAG statement
- leaf level defragmenting
- fragmentation [SQL Server]
- index defragmenting [SQL Server]
ms.assetid: 3c7df676-4843-44d0-8c1c-a9ab7e593b70
caps.latest.revision: 49
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: a1adc4da20dca615254f43c08282ee597b8dad17
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="dbcc-indexdefrag-transact-sql"></a>DBCC INDEXDEFRAG (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

Defragmentiert Indizes der angegebenen Tabelle oder Sicht.
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]Verwendung [ALTER INDEX](../../t-sql/statements/alter-index-transact-sql.md) stattdessen.  
  
**Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] über [aktuelle Version](http://go.microsoft.com/fwlink/p/?LinkId=299658))
  
![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Syntax  
  
```sql
DBCC INDEXDEFRAG  
(  
    { database_name | database_id | 0 }   
    , { table_name | table_id | view_name | view_id }   
    [ , { index_name | index_id } [ , { partition_number | 0 } ] ]  
)  
    [ WITH NO_INFOMSGS ]   
```  
  
## <a name="arguments"></a>Argumente  
 *Database_name* | *Database_id* | 0  
 Die Datenbank, die den zu defragmentierenden Index enthält. Wird 0 angegeben, wird die aktuelle Datenbank verwendet. Datenbanknamen müssen den Regeln für entsprechen [Bezeichner](../../relational-databases/databases/database-identifiers.md).  
  
 *TABLE_NAME* | *Table_id* | *View_name* | *View_id*  
 Die Tabelle oder Sicht, die den zu defragmentierenden Index enthält. Tabellen- und Sichtnamen müssen den Regeln für Bezeichner entsprechen.  
  
 *Index_name* | *Index_id*  
 Der Name oder die ID für den Index, der defragmentiert werden soll. Falls nicht angegeben, werden von der Anweisung alle Indizes der angegebenen Tabelle oder Sicht defragmentiert. Indexnamen müssen den Regeln für Bezeichner entsprechen.  
  
 *Partitionsnummer* | 0  
 Die Partitionsnummer des Indexes, der defragmentiert werden soll. Falls nichts oder 0 angegeben ist, werden von der Anweisung alle Partitionen im angegebenen Index defragmentiert.  
  
 WITH NO_INFOMSGS  
 Unterdrückt alle Informationsmeldungen mit einem Schweregrad von 0 bis 10.  
  
## <a name="remarks"></a>Hinweise  
DBCC INDEXDEFRAG defragmentiert die Blattebene eines Indexes, sodass die physische Reihenfolge der Seiten mit der logischen Reihenfolge (von links nach rechts) der Blattknoten übereinstimmt. Dadurch wird die Leistung beim Durchsuchen des Indexes verbessert.
  
> [!NOTE]  
>  Wenn DBCC INDEXDEFRAG ausgeführt wird, tritt die Indexdefragmentierung seriell auf. Das bedeutet, dass der Vorgang bei einem einzelnen Index mit einem einzigen Thread ausgeführt wird. Es tritt keine Parallelität auf. Außerdem werden Vorgänge für mehrere Indizes aus derselben DBCC INDEXDEFRAG-Anweisung nur für jeweils einen Index ausgeführt.  
  
DBCC INDEXDEFRAG komprimiert auch die Seiten eines Indexes, wobei auch der beim Erstellen des Indexes angegebene Füllfaktor beachtet wird. Alle leeren Seiten, die durch diese Komprimierung erstellt wurden, werden entfernt. Weitere Informationen finden Sie unter [Angeben des Füllfaktors für einen Index](../../relational-databases/indexes/specify-fill-factor-for-an-index.md).
  
Wenn sich ein Index über mehr als eine Datei erstreckt, defragmentiert DBCC INDEXDEFRAG nur eine Datei zu einem Zeitpunkt. Seiten werden nicht zwischen Dateien verschoben.
  
Alle fünf Minuten sendet DBCC INDEXDEFRAG einen Bericht an den Benutzer mit dem bereits fertig gestellten Prozentsatz. DBCC INDEXDEFRAG kann an jeder Stelle des Vorgangs beendet werden, wobei der fertig gestellte Anteil erhalten bleibt.
  
Im Gegensatz zu DBCC DBREINDEX (oder der Indexerstellung allgemein) ist DBCC INDEXDEFRAG ein Onlinevorgang. Es werden keine Sperren über längere Zeit errichtet. Daher blockiert DBCC INDEXDEFRAG keine aktiven Abfragen oder Updates. Ein relativ unfragmentierter Index kann schneller defragmentiert werden, als ein neuer Index erstellt werden kann, da die Defragmentierungszeit im Zusammenhang mit der Fragmentierungsebene steht. Das Defragmentieren eines stark fragmentierten Indexes kann wesentlich länger dauern als das erneute Erstellen.
  
Die Defragmentierung wird immer vollständig protokolliert, unabhängig von der Einstellung des Datenbank-Wiederherstellungsmodells. Weitere Informationen zu dieser Einstellung finden Sie unter [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md). Bei der Defragmentierung eines stark fragmentierten Indexes werden möglicherweise mehr Protokolleinträge erstellt als bei der Indexerstellung mit vollständiger Protokollierung. Die Defragmentierung wird jedoch als eine Reihe von kurzen Transaktionen ausgeführt und benötigt somit kein großes Protokoll, wenn häufig eine Protokollsicherung durchgeführt wird oder SIMPLE als Einstellung für das Wiederherstellungsmodell festgelegt ist.
  
## <a name="restrictions"></a>Einschränkungen  
DBCC INDEXDEFRAG verschiebt Indexblattseiten an andere Stellen. Daher führt das Ausführen von DBCC INDEXDEFRAG für einen Index, der mit anderen Indizes auf dem Datenträger verzahnt ist, nicht dazu, dass die Blattseiten im Index zusammenhängen. Erstellen Sie den Index neu, um das Gruppieren von Seiten zu verbessern.
DBCC INDEXDEFRAG kann nicht verwendet werden, um die folgenden Indizes zu defragmentieren:
-   Ein deaktivierter Index.  
-   Indizes, für die für das Seitensperren die Einstellung OFF festgelegt ist.  
-   Räumliche Indizes  
  
Die Verwendung von DBCC INDEXDEFRAG bei Systemtabellen wird nicht unterstützt.
  
## <a name="result-sets"></a>Resultsets  
DBCC INDEXDEFRAG gibt das folgende Resultset zurück (die Werte können abweichen), wenn ein Index in der Anweisung angegeben ist (sofern nicht WITH NO_INFOMSGS angegeben ist):
  
```sql
Pages Scanned Pages Moved Pages Removed  
------------- ----------- -------------  
359           346         8  
  
(1 row(s) affected)  
  
DBCC execution completed. If DBCC printed error messages, contact your system administrator.  
```  
  
## <a name="permissions"></a>Berechtigungen  
Bei dem Aufrufer muss es sich um den Besitzer der Tabelle oder um ein Mitglied der festen Serverrolle **sysadmin** , der festen Datenbankrolle **db_owner** oder der festen Datenbankrolle **db_ddladmin** handeln.
  
## <a name="examples"></a>Beispiele  
### <a name="a-using-dbcc-indexdefrag-to-defragment-an-index"></a>A. Defragmentieren eines Indexes mit DBCC INDEXDEFRAG  
Im folgende Beispiel werden alle Partitionen des defragmentiert die `PK_Product`_`ProductID` index in der `Production.Product` -Tabelle in der `AdventureWorks` Datenbank.
  
```sql  
DBCC INDEXDEFRAG (AdventureWorks2012, 'Production.Product', PK_Product_ProductID);  
GO  
```  
  
### <a name="b-using-dbcc-showcontig-and-dbcc-indexdefrag-to-defragment-the-indexes-in-a-database"></a>B. Mit DBCC SHOWCONTIG und DBCC INDEXDEFRAG die Indizes in einer Datenbank defragmentieren  
 Das folgende Beispiel zeigt eine einfache Möglichkeit, alle Indizes in einer Datenbank, deren Fragmentierung einen deklarierten Schwellenwert überschreitet, zu defragmentieren.  
  
```sql  
/*Perform a 'USE <database name>' to select the database in which to run the script.*/  
-- Declare variables  
SET NOCOUNT ON;  
DECLARE @tablename varchar(255);  
DECLARE @execstr   varchar(400);  
DECLARE @objectid  int;  
DECLARE @indexid   int;  
DECLARE @frag      decimal;  
DECLARE @maxfrag   decimal;  
  
-- Decide on the maximum fragmentation to allow for.  
SELECT @maxfrag = 30.0;  
  
-- Declare a cursor.  
DECLARE tables CURSOR FOR  
   SELECT TABLE_SCHEMA + '.' + TABLE_NAME  
   FROM INFORMATION_SCHEMA.TABLES  
   WHERE TABLE_TYPE = 'BASE TABLE';  
  
-- Create the table.  
CREATE TABLE #fraglist (  
   ObjectName char(255),  
   ObjectId int,  
   IndexName char(255),  
   IndexId int,  
   Lvl int,  
   CountPages int,  
   CountRows int,  
   MinRecSize int,  
   MaxRecSize int,  
   AvgRecSize int,  
   ForRecCount int,  
   Extents int,  
   ExtentSwitches int,  
   AvgFreeBytes int,  
   AvgPageDensity int,  
   ScanDensity decimal,  
   BestCount int,  
   ActualCount int,  
   LogicalFrag decimal,  
   ExtentFrag decimal);  
  
-- Open the cursor.  
OPEN tables;  
  
-- Loop through all the tables in the database.  
FETCH NEXT  
   FROM tables  
   INTO @tablename;  
  
WHILE @@FETCH_STATUS = 0  
BEGIN  
-- Do the showcontig of all indexes of the table  
   INSERT INTO #fraglist   
   EXEC ('DBCC SHOWCONTIG (''' + @tablename + ''')   
      WITH FAST, TABLERESULTS, ALL_INDEXES, NO_INFOMSGS');  
   FETCH NEXT  
      FROM tables  
      INTO @tablename;  
END;  
  
-- Close and deallocate the cursor.  
CLOSE tables;  
DEALLOCATE tables;  
  
-- Declare the cursor for the list of indexes to be defragged.  
DECLARE indexes CURSOR FOR  
   SELECT ObjectName, ObjectId, IndexId, LogicalFrag  
   FROM #fraglist  
   WHERE LogicalFrag >= @maxfrag  
      AND INDEXPROPERTY (ObjectId, IndexName, 'IndexDepth') > 0;  
  
-- Open the cursor.  
OPEN indexes;  
  
-- Loop through the indexes.  
FETCH NEXT  
   FROM indexes  
   INTO @tablename, @objectid, @indexid, @frag;  
  
WHILE @@FETCH_STATUS = 0  
BEGIN  
   PRINT 'Executing DBCC INDEXDEFRAG (0, ' + RTRIM(@tablename) + ',  
      ' + RTRIM(@indexid) + ') - fragmentation currently '  
       + RTRIM(CONVERT(varchar(15),@frag)) + '%';  
   SELECT @execstr = 'DBCC INDEXDEFRAG (0, ' + RTRIM(@objectid) + ',  
       ' + RTRIM(@indexid) + ')';  
   EXEC (@execstr);  
  
   FETCH NEXT  
      FROM indexes  
      INTO @tablename, @objectid, @indexid, @frag;  
END;  
  
-- Close and deallocate the cursor.  
CLOSE indexes;  
DEALLOCATE indexes;  
  
-- Delete the temporary table.  
DROP TABLE #fraglist;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
[sys.dm_db_index_physical_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md)  
[CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)  
[ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)  
[ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)
  
  



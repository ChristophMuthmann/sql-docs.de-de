---
title: DBCC SHOWCONTIG (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/17/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|database-console-commands
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DBCC_SHOWCONTIG_TSQL
- DBCC SHOWCONTIG
- SHOWCONTIG
- SHOWCONTIG_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- displaying defragmentation information
- DBCC SHOWCONTIG statement
- defragmenting indexes
- leaf level defragmenting
- fragmentation [SQL Server]
- index defragmenting [SQL Server]
ms.assetid: 1df2123a-1197-4fff-91a3-25e3d8848aaa
caps.latest.revision: 78
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: aecf422ca2289b2a417147eb402921bb8530d969
ms.openlocfilehash: 901067b9bd9c85887b66ea8d32999cf439873952
ms.contentlocale: de-de
ms.lasthandoff: 10/24/2017

---
# <a name="dbcc-showcontig-transact-sql"></a>DBCC SHOWCONTIG (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

Zeigt Fragmentierungsinformationen für die Daten und Indizes der angegebenen Tabelle oder Sicht an.
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]Verwendung [Sys. dm_db_index_physical_stats](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md) stattdessen.  
  
**Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] über [aktuelle Version](http://go.microsoft.com/fwlink/p/?LinkId=299658))
  
![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Syntax  
  
```sql
DBCC SHOWCONTIG   
[ (   
    { table_name | table_id | view_name | view_id }   
    [ , index_name | index_id ]   
) ]   
    [ WITH   
        {   
         [ , [ ALL_INDEXES ] ]   
         [ , [ TABLERESULTS ] ]   
         [ , [ FAST ] ]  
         [ , [ ALL_LEVELS ] ]   
         [ NO_INFOMSGS ]  
         }  
    ]  
```  
  
## <a name="arguments"></a>Argumente  
 *TABLE_NAME* | *Table_id* | *View_name* | *View_id*  
 Die Tabelle oder Sicht, für die die Fragmentierungsinformationen überprüft werden sollen. Falls nicht angegeben, werden alle Tabellen und indizierten Sichten der aktuellen Datenbank überprüft. Um die Tabelle zu erhalten, oder ID anzuzeigen, verwenden Sie die [OBJECT_ID](../../t-sql/functions/object-id-transact-sql.md) Funktion.  
  
 *Index_name* | *Index_id*  
 Der Index, für den die Fragmentierungsinformationen überprüft werden sollen. Falls nicht angegeben, wird der Basisindex der angegebenen Tabelle oder Sicht von der Anweisung verarbeitet. Um die Index-ID zu erhalten, verwenden die [sys.indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md) -Katalogsicht angezeigt.  
  
 mit  
 Gibt die Optionen für den von der DBCC-Anweisung zurückgegebenen Informationstyp an.  
  
 FAST  
 Gibt an, ob ein schneller Scan des Indexes durchgeführt und minimale Informationen ausgegeben werden sollen. Bei einem schnellen Scan werden die Seiten auf Blatt- oder Datenebene des Indexes nicht gelesen.  
  
 ALL_INDEXES  
 Zeigt Ergebnisse für alle Indizes für die angegebenen Tabellen und Sichten an, selbst wenn ein bestimmter Index angegeben ist.  
  
 TABLERESULTS  
 Zeigt die Ergebnisse als Rowset mit zusätzlichen Informationen an.  
  
 ALL_LEVELS  
 Nur aus Gründen der Abwärtskompatibilität beibehalten. Auch wenn ALL_LEVELS angegeben ist, wird nur die Blattebene des Indexes oder die Datenebene der Tabelle verarbeitet.  
  
 NO_INFOMSGS  
 Unterdrückt alle Informationsmeldungen mit einem Schweregrad von 0 bis 10.  
  
## <a name="result-sets"></a>Resultsets  
In der folgenden Tabelle finden Sie eine Beschreibung der Informationen des Resultsets:
  
|Statistik|Description|  
|---|---|
|**Gescannte Seiten**|Anzahl der Seiten in der Tabelle oder im Index.|  
|**Gescannte Blöcke**|Anzahl der Blöcke in der Tabelle oder im Index.|  
|**Blockwechsel**|Gibt an, wie oft die DBCC-Anweisung von einem Block zu einem anderen gewechselt hat, während die Anweisung die Seiten der Tabelle oder des Indexes durchlaufen hat.|  
|**Mittlere Seiten pro Block**|Die Anzahl der Seiten pro Block in der Seitenkette.|  
|**Scandichte [Bester Wert: Tatsächlicher Wert]**|Ein Prozentwert. Dies ist das Verhältnis **Bester Wert** auf **tatsächlicher Wert**. Dieser Wert ist 100, wenn alle Daten zusammenhängen. Liegt der Wert unter 100, sind sie fragmentiert.<br /><br /> **Bester Wert** ist die ideale Anzahl von Blockwechseln, wenn alle Daten zusammenhängend verknüpft sind. **Tatsächliche Anzahl** ist die tatsächliche Anzahl von Blockwechseln.|  
|**Logische Scanfragmentierung**|Prozentsatz der Seiten, die beim Scannen der Blattseiten eines Indexes nicht richtig einsortiert waren. Diese Zahl ist für Heaps nicht relevant. Eine außerhalb der normalen Reihenfolge ist eine Seite für die ist die nächste physische Seite zugeordnet, die dem Index nicht der Seite auf den weiter-Pag zeigt*e* Zeiger in der aktuellen Blattseite.|  
|**Blockscanfragmentierung**|Prozentsatz der Blöcke, die beim Scannen der Blattseiten eines Indexes nicht richtig einsortiert waren. Diese Zahl ist für Heaps nicht relevant. Ein nicht richtig einsortierter Block ist ein Block, für den der Block, der die aktuelle Seite eines Indexes enthält, physisch nicht der nächste Block nach dem Block ist, der die vorherige Seite des Indexes enthält.<br /><br /> Hinweis: Diese Zahl ist bedeutungslos, wenn der Index mehrere Dateien erstreckt.|  
|**Mittlere Bytes frei pro Seite**|Die durchschnittliche Anzahl von freien Bytes auf den gescannten Seiten. Je größer die Zahl, desto weniger sind die Seiten belegt. Kleinere Zahlen sind besser, wenn der Index nur über wenige zufällige Einfügungen verfügt. Diese Zahl wird auch von der Zeilengröße beeinflusst. Große Zeilen können einen höheren Wert verursachen.|  
|**Mittlere Seitendichte (voll)**|Die durchschnittliche Seitendichte in Prozent. Dieser Wert berücksichtigt die Zeilengröße. Daher informiert der Wert genauer über den Füllungsgrad der Seiten. Je höher die Prozentwerte, desto besser.|  
  
Wenn *Table_id* und die Option FAST angegeben sind, ist DBCC SHOWCONTIG gibt ein Resultset mit folgenden Spalten zurück.
-   **Gescannte Seiten**  
-   **Blockwechsel**  
-   **Scandichte [Bester Wert: Tatsächlicher Wert]**  
-   **Blockscanfragmentierung**  
-   **Logische Scanfragmentierung**  
  
Wenn TABLERESULTS angegeben ist, gibt DBCC SHOWCONTIG die neun in der ersten Tabelle beschriebenen Spalten sowie die folgenden Spalten zurück.
  
|Statistik|Description|  
|---|---|
|**Objektnamen**|Der Name der verarbeiteten Tabelle oder Sicht.|  
|**ObjectID**|ID des Objektnamens.|  
|**IndexName**|Der Name des verarbeiteten Indexes. Für einen Heap lautet der Wert NULL.|  
|**IndexId**|Die ID des Index. Für einen Heap lautet der Wert 0.|  
|**Level**|Ebene des Indexes. Ebene 0 ist die Blatt- oder Datenebene des Indexes.<br /><br /> Die Ebene für einen Heap ist 0.|  
|**Seiten**|Anzahl von Seiten, die zu dieser Indexebene oder zum gesamten Heap gehören.|  
|**Zeilen**|Anzahl der Daten- oder Indexdatensätze auf dieser Ebene des Indexes. Für einen Heap ist dies die Anzahl von Datensätzen im gesamten Heap.<br /><br /> Bei einem Heap stimmt die Anzahl der Datensätze, die von dieser Funktion zurückgegeben wird, möglicherweise nicht mit der Anzahl der Zeilen überein, die beim Ausführen von SELECT COUNT(*) für den Heap zurückgegeben werden. Das liegt daran, dass eine Zeile möglicherweise mehrere Datensätze enthält. So kann in bestimmten Updatesituationen eine einzelne Heapzeile möglicherweise über einen Weiterleitungsdatensatz und einen weitergeleiteten Datensatz als Ergebnis des Updates verfügen. Außerdem werden die meisten großen LOB-Zeilen im LOB_DATA-Speicher in mehrere Datensätze geteilt.|  
|**MinimumRecordSize**|Die minimale Größe der Datensätze in dieser Indexebene oder im gesamten Heap.|  
|**MaximumRecordSize**|Die maximale Größe der Datensätze in dieser Indexebene oder im gesamten Heap.|  
|**AverageRecordSize**|Die durchschnittliche Größe der Datensätze in dieser Indexebene oder im gesamten Heap.|  
|**ForwardedRecords**|Anzahl der weitergeleiteten Datensätze in dieser Indexebene oder im gesamten Heap.|  
|**Blöcke**|Anzahl von Blöcken in dieser Indexebene oder im gesamten Heap.|  
|**ExtentSwitches**|Gibt an, wie oft die DBCC-Anweisung von einem Block zu einem anderen gewechselt hat, während die Anweisung die Seiten der Tabelle oder des Indexes durchlaufen hat.|  
|**AverageFreeBytes**|Die durchschnittliche Anzahl von freien Bytes auf den gescannten Seiten. Je größer die Zahl, desto weniger sind die Seiten belegt. Kleinere Zahlen sind besser, wenn der Index nur über wenige zufällige Einfügungen verfügt. Diese Zahl wird auch von der Zeilengröße beeinflusst. Große Zeilen können einen höheren Wert verursachen.|  
|**AveragePageDensity**|Die durchschnittliche Seitendichte in Prozent. Dieser Wert berücksichtigt die Zeilengröße. Daher informiert der Wert genauer über den Füllungsgrad der Seiten. Je höher die Prozentwerte, desto besser.|  
|**ScanDensity**|Ein Prozentwert. Dies ist das Verhältnis **BestCount** auf **ActualCount**. Dieser Wert ist 100, wenn alle Daten zusammenhängen. Liegt der Wert unter 100, sind sie fragmentiert.|  
|**BestCount**|Ist die ideale Anzahl von Blockwechseln, wenn alle Daten zusammenhängend verknüpft sind.|  
|**ActualCount**|Die tatsächliche Anzahl von Blockwechseln.|  
|**LogicalFragmentation**|Prozentsatz der Seiten, die beim Scannen der Blattseiten eines Indexes nicht richtig einsortiert waren. Diese Zahl ist für Heaps nicht relevant. Eine außerhalb der normalen Reihenfolge ist eine Seite für die ist die nächste physische Seite zugeordnet, die dem Index nicht der Seite auf den weiter-Pag zeigt*e* Zeiger in der aktuellen Blattseite.|  
|**ExtentFragmentation**|Prozentsatz der Blöcke, die beim Scannen der Blattseiten eines Indexes nicht richtig einsortiert waren. Diese Zahl ist für Heaps nicht relevant. Ein nicht richtig einsortierter Block ist ein Block, für den der Block, der die aktuelle Seite eines Indexes enthält, physisch nicht der nächste Block nach dem Block ist, der die vorherige Seite des Indexes enthält.<br /><br /> Hinweis: Diese Zahl ist bedeutungslos, wenn der Index mehrere Dateien erstreckt.|  
  
Wenn WITH TABLERESULTS und FAST angegeben sind, ist das Resultset dasselbe wie bei Angabe von WITH TABLERESULTS mit Ausnahme der folgenden Spalten, die NULL-Werte enthalten werden:

| Zeilen| Extents |
|---|---|
|**MinimumRecordSize**|**AverageFreeBytes**|  
|**MaximumRecordSize**|**AveragePageDensity**|  
|**AverageRecordSize**|**ExtentFragmentation**|  
|**ForwardedRecords**||  
  
## <a name="remarks"></a>Hinweise  
Die DBCC SHOWCONTIG-Anweisung durchläuft die Seitenkette auf der Blattebene des angegebenen index, wenn *Index_id* angegeben ist. Wenn nur *Table_id* angegeben ist oder wenn *Index_id* gleich 0 ist, werden die Datenseiten der angegebenen Tabelle gescannt. Dieser Vorgang erfordert nur eine beabsichtigte gemeinsame Tabellensperre (IS). Auf diese Weise können alle Updates und Einfügungen ausgeführt werden, außer jenen, die eine exklusive Tabellensperre (X) erfordern. Dies schafft einen Kompromiss zwischen der Ausführungsgeschwindigkeit ohne Verringerung der Parallelität und der Anzahl der zurückgegebenen Statistiken. Wenn der Befehl jedoch nur zum Messen der Fragmentierung verwendet wird, wird die Verwendung der WITH FAST-Option empfohlen, um eine optimale Leistung zu erreichen. Bei einem schnellen Scan werden die Seiten auf Blatt- oder Datenebene des Indexes nicht gelesen. Die Option WITH FAST gilt nicht für einen Heap.
  
## <a name="restrictions"></a>Einschränkungen  
DBCC SHOWCONTIG zeigt keine Daten mit **Ntext**, **Text**, und **Image** -Datentypen. Dies liegt daran, dass Textindizes, die Text- und Imagedaten speichern, nicht mehr verwendet werden.
  
Zudem bietet DBCC SHOWCONTIG keine Unterstützung für einige neue Funktionen. Beispiel:
-   Falls die angegebene Tabelle oder der angegebene Index partitioniert ist, zeigt DBCC SHOWCONTIG nur die erste Partition der angegebenen Tabelle oder des angegebenen Indexes an.  
-   DBCC SHOWCONTIG zeigt keine Zeilenüberlauf-Speicherinformationen und andere neue Typen der Datenknoten außerhalb von Zeilen, wie z. B. **nvarchar(max)**, **varchar(max)**, **varbinary(max)**, und **Xml**.  
-   Räumliche Indizes werden von DBCC SHOWCONTIG nicht unterstützt.  
  
Alle neue Funktionen werden vollständig unterstützt, indem Sie die [Sys. dm_db_index_physical_stats &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md) -verwaltungssicht.
  
## <a name="table-fragmentation"></a>Tabellenfragmentierung  
DBCC SHOWCONTIG findet heraus, ob die Tabelle stark fragmentiert ist. Eine Tabellenfragmentierung wird durch Datenänderungen (mithilfe der Anweisungen INSERT, UPDATE oder DELETE) in der Tabelle hervorgerufen. Da diese Änderungen normalerweise nicht gleichmäßig über alle Zeilen der Tabelle verteilt vorgenommen werden, kann sich mit der Zeit der Füllungsgrad jeder Seite ändern. Diese Tabellenfragmentierung kann bei Abfragen, bei denen eine Tabelle teilweise oder ganz gescannt wird, zu zusätzlichen Seitenlesevorgängen führen. Dies behindert das parallele Scannen von Daten.
  
Bei einer starken Fragmentierung eines Indexes gibt es folgende Möglichkeiten zum Reduzieren der Fragmentierung:
-   Löschen und Neuerstellen eines gruppierten Indexes.  
     Durch das erneute Erstellen eines gruppierten Indexes wird eine Reorganisation der Daten durchgeführt, was zu vollen Datenseiten führt. Der Füllungsgrad kann über die Option FILLFACTOR in CREATE INDEX konfiguriert werden. Die Nachteile dieser Methode liegen darin, dass der Index während des Löschens und Neuerstellens offline und der Vorgang atomar ist. Wenn die Indexerstellung unterbrochen wird, wird der Index nicht neu erstellt.  
-   Neuordnen der Indexseiten auf Blattebene in einer logischen Reihenfolge.  
     Verwenden Sie ALTER INDEX…REORGANIZE, um die Indexseiten auf Blattebene in einer logischen Reihenfolge neu zu sortieren. Da es sich hierbei um einen Onlinevorgang handelt, steht der Index bei Ausführung der Anweisung zur Verfügung. Der Vorgang kann auch unterbrochen werden, jedoch führt dies nicht zu einem Verlust des bereits fertig gestellten Anteils. Der Nachteil dieser Methode besteht darin, dass die Daten nicht so gut neu organisiert werden wie beim Löschen oder Neuerstellen eines gruppierten Indexes.  
-   Neuerstellen des Indexes an.  
     Verwenden Sie ALTER INDEX mit REBUILD, um den Index neu zu erstellen. Weitere Informationen finden Sie unter [ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md).  
  
Die Statistiken **Bytes Bytes frei pro Seite** und **durchschn. Seitendichte (voll)** Statistik im Resultset zeigen den Füllungsgrad der Indexseiten. Die Statistiken **Bytes Bytes frei pro Seite** niedrig und die **durchschn. Seitendichte (voll)** Anzahl sollte groß sein, wenn ein Index, der nur über wenige zufällige einfügungen verfügt. Durch Löschen und Neuerstellen eines Indexes mit der angegebenen FILLFACTOR-Option können diese Statistiken verbessert werden. Außerdem komprimiert ALTER INDEX mit REORGANIZE einen Index, wobei der Wert für FILLFACTOR berücksichtigt wird. Dadurch wird diese Statistik verbessert.
  
> [!NOTE]  
>  Ein Index mit zahlreichen zufälligen Einfügungen und sehr vollen Seiten verfügt über eine höhere Anzahl von Seitenteilungen. Dadurch entsteht mehr Fragmentierung.  
  
Zum Festlegen der Fragmentierungsebene eines Indexes gibt es folgende Möglichkeiten:
-   Durch Vergleichen der Werte von **Blockwechsel** und **Gescannte Blöcke**.  
     Der Wert der **Blockwechsel** sollte so nah wie möglich an der **Gescannte Blöcke**. Dieses Verhältnis wird berechnet als die **Scandichte** Wert. Dieser Wert sollte so hoch wie möglich sein, er kann durch das Verringern der Indexfragmentierung verbessert werden.  
  
    > [!NOTE]  
    >  Diese Methode funktioniert nicht, wenn sich der Index über mehrere Dateien erstreckt.  
  
-   Grundlegendes über **logische Scanfragmentierung** und **Blockscanfragmentierung** Werte.  
     **Logische Scanfragmentierung** und in geringerem Maße, **Blockscanfragmentierung** Werte sind die besten Indikatoren die Fragmentierungsebene einer Tabelle. Beide Werte sollten so nahe wie möglich bei Null liegen, ein Wert von 0 % bis 10 % ist jedoch akzeptabel.  
  
    > [!NOTE]  
    >  Die **Blockscanfragmentierung** Wert wird hoch sein, wenn der Index mehrere Dateien erstreckt. Sie können diese Werte verringern, wenn Sie die Indexfragmentierung verringern.  
  
## <a name="permissions"></a>Berechtigungen  
Benutzer muss Besitzer der Tabelle oder ein Mitglied der **Sysadmin** festen Serverrolle die **Db_owner** feste Datenbankrolle oder der **Db_ddladmin** festen Datenbankrolle "".
  
## <a name="examples"></a>Beispiele  
### <a name="a-displaying-fragmentation-information-for-a-table"></a>A. Anzeigen von Fragmentierungsinformationen für eine Tabelle  
Im folgenden Beispiel werden die Fragmentierungsinformationen für die `Employee`-Tabelle angezeigt.
  
```sql  
USE AdventureWorks2012;  
GO  
DBCC SHOWCONTIG ('HumanResources.Employee');  
GO  
```  
  
### <a name="b-using-objectid-to-obtain-the-table-id-and-sysindexes-to-obtain-the-index-id"></a>B. Abrufen der Tabellen-ID mit OBJECT_ID und der Index-ID mit sys.indexes  
Im folgenden Beispiel wird `OBJECT_ID` und `sys.indexes` Katalogsicht, um die Tabellen-ID zu erhalten und index-ID für die `AK_Product_Name` Index des der `Production.Product` -Tabelle in der [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] Datenbank.
  
```sql  
USE AdventureWorks2012;  
GO  
DECLARE @id int, @indid int  
SET @id = OBJECT_ID('Production.Product')  
SELECT @indid = index_id   
FROM sys.indexes  
WHERE object_id = @id   
   AND name = 'AK_Product_Name'  
DBCC SHOWCONTIG (@id, @indid);  
GO  
```  
  
### <a name="c-displaying-an-abbreviated-result-set-for-a-table"></a>C. Anzeigen eines verkürzten Resultsets für eine Tabelle  
Das folgende Beispiel gibt ein verkürztes Resultset für die `Product` -Tabelle in der [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] Datenbank.
  
```sql  
USE AdventureWorks2012;  
GO  
DBCC SHOWCONTIG ('Production.Product', 1) WITH FAST;  
GO  
```  
  
### <a name="d-displaying-the-full-result-set-for-every-index-on-every-table-in-a-database"></a>D. Anzeigen des vollständigen Resultsets für alle Indizes in jeder Tabelle der Datenbank  
Im folgenden Beispiel wird ein vollständiges Resultset für jeden Index aller Tabellen in der [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]-Datenbank zurückgegeben.
  
```sql  
USE AdventureWorks2012;  
GO  
DBCC SHOWCONTIG WITH TABLERESULTS, ALL_INDEXES;  
GO  
```  
  
### <a name="e-using-dbcc-showcontig-and-dbcc-indexdefrag-to-defragment-the-indexes-in-a-database"></a>E. Mit DBCC SHOWCONTIG und DBCC INDEXDEFRAG die Indizes in einer Datenbank defragmentieren  
Das folgende Beispiel zeigt eine einfache Möglichkeit zum Defragmentieren aller Indizes in einer Datenbank, die über einem deklarierten Schwellenwert fragmentiert ist.
  
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
[ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)  
[CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)  
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
[DROP INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/drop-index-transact-sql.md)  
[sys.dm_db_index_physical_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md)  
[OBJECT_ID &#40;Transact-SQL&#41;](../../t-sql/functions/object-id-transact-sql.md)  
[sys.indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)
  
  



---
title: UPDATE STATISTICS (Transact-SQL) | Microsoft-Dokumentation
ms.custom: 
ms.date: 01/04/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- UPDATE STATISTICS
- UPDATE_STATISTICS_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- updating statistics
- query optimization statistics [SQL Server], updating
- UPDATE STATISTICS statement
- statistical information [SQL Server], updating
ms.assetid: 919158f2-38d0-4f68-82ab-e1633bd0d308
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 7c69949773ff1dae533c98d087780a2f4b436b62
ms.sourcegitcommit: 4aeedbb88c60a4b035a49754eff48128714ad290
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/05/2018
---
# <a name="update-statistics-transact-sql"></a>UPDATE STATISTICS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Aktualisiert eine Abfrageoptimierungsstatistik für eine Tabelle oder indizierte Sicht. Standardmäßig nimmt der Abfrageoptimierer erforderliche Updates der Statistiken automatisch vor, um den Abfrageplan zu verbessern. In einigen Fällen können Sie die Abfrageleistung mit UPDATE STATISTICS oder der gespeicherten Prozedur [sp_updatestats](../../relational-databases/system-stored-procedures/sp-updatestats-transact-sql.md) verbessern, um Statistiken häufiger zu aktualisieren als von der Standardeinstellung vorgegeben.  
  
 Durch das Update von Statistiken wird sichergestellt, dass Abfragen anhand aktueller Statistiken kompiliert werden. Dies führt jedoch dazu, dass Abfragen neu kompiliert werden. Es empfiehlt sich, Statistiken nicht zu oft zu aktualisieren und die Vorteile optimierter Abfragepläne gegen den Zeitaufwand für die Neukompilierung von Abfragen abzuwägen. Die Entscheidung hängt von der verwendeten Anwendung ab. UPDATE STATISTICS-Vorgänge können mithilfe von tempdb die Stichprobenzeilen zum Erstellen von Statistiken sortieren.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
UPDATE STATISTICS table_or_indexed_view_name   
    [   
        {   
            { index_or_statistics__name }  
          | ( { index_or_statistics_name } [ ,...n ] )   
                }  
    ]   
    [    WITH   
        [  
            FULLSCAN   
              [ [ , ] PERSIST_SAMPLE_PERCENT = { ON | OFF } ]    
            | SAMPLE number { PERCENT | ROWS }   
              [ [ , ] PERSIST_SAMPLE_PERCENT = { ON | OFF } ]    
            | RESAMPLE   
              [ ON PARTITIONS ( { <partition_number> | <range> } [, …n] ) ]  
            | <update_stats_stream_option> [ ,...n ]  
        ]   
        [ [ , ] [ ALL | COLUMNS | INDEX ]   
        [ [ , ] NORECOMPUTE ]   
        [ [ , ] INCREMENTAL = { ON | OFF } ] 
        [ [ , ] MAXDOP = max_degree_of_parallelism ] 
    ] ;  
  
<update_stats_stream_option> ::=  
    [ STATS_STREAM = stats_stream ]  
    [ ROWCOUNT = numeric_constant ]  
    [ PAGECOUNT = numeric_contant ]  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
UPDATE STATISTICS schema_name . ] table_name   
    [ ( { statistics_name | index_name } ) ]  
    [ WITH   
       {  
              FULLSCAN   
            | SAMPLE number PERCENT   
            | RESAMPLE   
        }  
    ]  
[;]  
```  
  
## <a name="arguments"></a>Argumente  
 *table_or_indexed_view_name*  
 Der Name der Tabelle oder der indizierten Sicht, die das Statistikobjekt enthält.  
  
 *index_or_statistics_name*  
 Der Name des Index, für den die Statistik aktualisiert werden soll, oder der Name der zu aktualisierenden Statistik. Wenn *index_or_statistics_name* nicht angegeben ist, aktualisiert der Abfrageoptimierer alle Statistiken für die Tabelle oder indizierte Sicht. Dies schließt Statistiken ein, die mithilfe der CREATE STATISTICS-Anweisung erstellt wurden, Statistiken für einzelne Spalten, die mit aktivierter AUTO_CREATE_STATISTICS-Option erstellt wurden, sowie für Indizes erstellte Statistiken.  
  
 Weitere Informationen über AUTO_CREATE_STATISTICS finden Sie unter [ALTER DATABASE SET-Optionen &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md). Zum Anzeigen aller Indizes einer Tabelle oder Sicht können Sie [sp_helpindex](../../relational-databases/system-stored-procedures/sp-helpindex-transact-sql.md) verwenden.  
  
 FULLSCAN  
 Berechnen Sie die Statistik, indem Sie alle Zeilen in der Tabelle oder indizierten Sicht scannen. FULLSCAN und SAMPLE 100 PERCENT führen zu gleichen Ergebnissen. FULLSCAN kann nicht in Verbindung mit der SAMPLE-Option verwendet werden.  
  
 SAMPLE *Zahl* { PERCENT | ROWS }  
 Gibt den ungefähren Prozentsatz oder die ungefähre Anzahl von Zeilen in der Tabelle oder indizierten Sicht an, die vom Abfrageoptimierer beim Aktualisieren von Statistiken verwendet werden soll. Für PERCENT kann *Zahlenwerte* von 0 bis 100 annehmen, für ROWS kann *Zahlenwerte* von 0 bis zur Gesamtanzahl der Zeilen annehmen. Der tatsächliche Prozentsatz oder die tatsächliche Anzahl von Zeilen, die vom Abfrageoptimierer als Stichprobe entnommen werden, stimmt möglicherweise nicht mit dem angegebenen Prozentsatz oder der angegebenen Anzahl überein. Der Abfrageoptimierer scannt z. B. alle Zeilen auf einer Datenseite.  
  
 SAMPLE eignet sich für Sonderfälle, in denen der auf Standardstichproben beruhende Abfrageplan nicht optimal ist. In den meisten Situationen muss SAMPLE nicht angegeben werden, da der Abfrageoptimierer standardmäßig Stichproben verwendet und die statistisch signifikante Stichprobengröße ermittelt, wie zum Erstellen hochwertiger Abfragepläne erforderlich. 
 
Beginnend mit [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] werden Datenstichproben zum Erstellen von Statistiken parallel gewonnen, wenn der Kompatibilitätsgrad 130 verwendet wird, um die Leistung von Statistiken zu verbessern. Der Abfrageoptimierer verwendet parallele Beispielstatistiken, wenn die Größe einer Tabelle einen gewissen Grenzwert überschreitet. 
   
 SAMPLE kann nicht in Verbindung mit der Option FULLSCAN verwendet werden. Wenn weder SAMPLE noch FULLSCAN angegeben wurde, verwendet der Abfrageoptimierer Stichprobendaten und berechnet die Stichprobengröße anhand der Standardeinstellungen.  
  
 Es wird davon abgeraten, 0 PERCENT oder 0 ROWS anzugeben. Wenn 0 PERCENT oder ROWS angegeben ist, wird das Statistikobjekt aktualisiert, es enthält jedoch keine Statistikdaten.  
  
 Bei den meisten Arbeitsauslastungen ist keine vollständige Überprüfung erforderlich und Standardstichproben sind ausreichend.  
Allerdings sind bestimmte Arbeitsauslastungen gegenüber stark variierenden Datenverteilungen empfindlich und können deshalb eine erhöhte Anzahl an Stichproben oder sogar eine vollständige Überprüfung erfordern.  
Weitere Informationen finden Sie in diesem Eintrag im [CSS SQL Escalation Services-Blog](http://blogs.msdn.com/b/psssql/archive/2010/07/09/sampling-can-produce-less-accurate-statistics-if-the-data-is-not-evenly-distributed.aspx).  
  
 RESAMPLE  
 Aktualisieren Sie alle Statistiken mithilfe ihrer letzten Samplingraten.  
  
 Die Verwendung von RESAMPLE kann zu einem vollständigen Tabellenscan führen. Zum Beispiel verwenden die Statistiken für Indizes einen vollständigen Tabellenscan für ihre Beispielrate. Wenn keine der Stichprobenoptionen (SAMPLE, FULLSCAN, RESAMPLE) angegeben wurde, verwendet der Abfrageoptimierer Stichprobendaten und berechnet standardmäßig die Stichprobengröße.  

PERSIST_SAMPLE_PERCENT = { ON | OFF }  
Bei **ON** behalten die Statistiken den festgelegten Prozentsatz für die Stichprobenentnahme für nachfolgende Updates bei, die keinen expliziten Prozentsatz für die Stichprobenentnahme angeben. Bei **OFF** wird der Prozentsatz für die Stichprobenentnahme in nachfolgenden Updates auf den Standardwert zurückgesetzt, sofern diese keinen expliziten Prozentsatz für die Stichprobenentnahme angeben. Der Standardwert ist **OFF**. 
 
 > [!NOTE]
 > Wenn AUTO_UPDATE_STATISTICS ausgeführt wird, wird der beibehaltene Prozentsatz für die Stichprobenentnahme verwendet, wenn er verfügbar ist. Wenn er nicht verfügbar ist, wird der Standardprozentsatz verwendet.
 > Das Verhalten von RESAMPLE wird von dieser Option nicht beeinflusst.
 
 > [!TIP] 
 > [DBCC SHOW_STATISTICS](../../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md) und [sys.dm_db_stats_properties](../../relational-databases/system-dynamic-management-views/sys-dm-db-stats-properties-transact-sql.md) machen den beibehaltenen Prozentwert für die Stichprobenentnahme der ausgewählten Statistik verfügbar.
 
 **Gilt für**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] (ab [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1 CU4) bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] (ab [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU1).  
 
 ON PARTITIONS ( { \<partition_number> | \<range> } [, …n] ) ] erzwingt, dass die Statistiken auf Blattebene, die die in der ON PARTITIONS-Klausel angegebenen Partitionen umfassen, erneut berechnet und dann zusammengeführt werden, um die globale Statistik zu bilden. WITH RESAMPLE ist erforderlich, da mit unterschiedlichen Stichprobenraten erstellte Partitionsstatistiken nicht zusammengeführt werden können.  
  
**Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
 ALL | COLUMNS | INDEX  
 Aktualisieren Sie alle vorhandenen Statistiken, für eine oder mehrere Spalten erstellte Statistiken oder für Indizes erstellte Statistiken. Wenn keine der Optionen angegeben wird, aktualisiert die UPDATE STATISTICS-Anweisung alle Statistiken für die Tabelle oder indizierte Sicht.  
  
 NORECOMPUTE  
 Deaktiviert die AUTO_UPDATE_STATISTICS-Option zum automatischen Statistikupdate für die angegebene Statistik. Wenn diese Option angegeben wird, schließt der Abfrageoptimierer dieses Statistikupdate ab und deaktiviert zukünftige Updates.  
  
 Um das Verhalten der AUTO_UPDATE_STATISTICS-Option wieder zu aktivieren, führen Sie UPDATE STATISTICS erneut ohne die NORECOMPUTE-Option aus, oder führen **sp_autostats** aus.  
  
> [!WARNING]  
>  Bei Verwendung dieser Option können suboptimale Abfragepläne entstehen. Es wird empfohlen, diese Option nur in Einzelfällen von einem qualifizierten Systemadministrator vornehmen zu lassen.  
  
 Weitere Informationen über die Option AUTO_STATISTICS_UPDATE finden Sie unter [ALTER DATABASE SET-Optionen &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md).  
  
 INCREMENTAL = { ON | OFF }  
 Bei **ON** werden die Statistiken als Statistiken pro Partition neu erstellt. Bei **OFF** wird die Statistikstruktur gelöscht und [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] berechnet die Statistiken erneut. Der Standardwert ist **OFF**.  
  
 Wenn Statistiken pro Partition nicht unterstützt werden, wird ein Fehler generiert. Inkrementelle Statistiken werden für folgende Statistiktypen nicht unterstützt:  
  
-   Statistiken, die mit Indizes erstellt wurden, die über keine Partitionsausrichtung mit der Basistabelle verfügen.  
-   Statistiken, die für lesbare sekundäre Always On-Datenbanken erstellt wurden.  
-   Statistiken, die für schreibgeschützte Datenbanken erstellt wurden.  
-   Statistiken, die für gefilterte Indizes erstellt wurden.  
-   Statistiken, die für Sichten erstellt wurden.  
-   Statistiken, die für interne Tabellen erstellt wurden.  
-   Statistiken, die mit räumlichen Indizes oder XML-Indizes erstellt wurden.  
  
**Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]

MAXDOP = *max_degree_of_parallelism*  
**Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (ab [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU3).  
  
 Überschreibt die Konfigurationsoption **max degree of parallelism** (Max. Grad an Parallelität) für die Dauer des Statistikvorgangs. Weitere Informationen finden Sie unter [Configure the max degree of parallelism Server Configuration Option](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md). Sie können mit MAXDOP die Anzahl der Prozessoren begrenzen, die bei der Ausführung paralleler Pläne verwendet werden. Maximal sind 64 Prozessoren zulässig.  
  
 *max_degree_of_parallelism* kann folgende Werte haben:  
  
 1  
 Unterdrückt das Generieren paralleler Pläne.  
  
 \>1  
 Beschränkt die maximale Anzahl der Prozessoren, die bei einem parallelen Statistikvorgang verwendet werden, je nach aktueller Systemauslastung auf die angegebene Zahl oder einen niedrigeren Wert.  
  
 0 (Standard)  
 Verwendet abhängig von der aktuellen Systemarbeitsauslastung die tatsächliche Anzahl von Prozessoren oder weniger Prozessoren.  
  
 \<update_stats_stream_option> [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  

## <a name="remarks"></a>Remarks  
  
## <a name="when-to-use-update-statistics"></a>Wann UPDATE STATISTICS verwendet werden sollte  
 Weitere Informationen dazu, wann UPDATE STATISTICS verwendet werden sollte, finden Sie unter [Statistik](../../relational-databases/statistics/statistics.md).  

## <a name="limitations-and-restrictions"></a>Einschränkungen  
* Das Aktualisieren von Statistiken bei externen Tabellen wird nicht unterstützt. Zum Aktualisieren einer Statistik müssen Sie die Statistik löschen und neu erstellen.  
* Die Option MAXDOP ist nicht mit den Optionen STATS_STREAM, ROWCOUNT und PAGECOUNT kompatibel.

## <a name="updating-all-statistics-with-spupdatestats"></a>Aktualisieren aller Statistiken mit "sp_updatestats"  
 Informationen zum Aktualisieren von Statistiken für alle benutzerdefinierten und internen Tabellen in der Datenbank finden Sie in der Beschreibung der gespeicherten Prozedur [sp_updatestats &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-updatestats-transact-sql.md). Durch den folgenden Befehl wird beispielsweise sp_updatestats zum Aktualisieren aller Statistiken für die Datenbank aufgerufen.  
  
```sql  
EXEC sp_updatestats;  
```  
  
## <a name="determining-the-last-statistics-update"></a>Ermitteln des letzten Statistikupdates  
 Um zu ermitteln, wann Statistiken zuletzt aktualisiert wurden, verwenden Sie die [STATS_DATE](../../t-sql/functions/stats-date-transact-sql.md) -Funktion.  
  
## <a name="pdw--sql-data-warehouse"></a>PDW (SQL Data Warehouse)  
 Die folgende Syntax wird nicht von PDW bzw. SQL Data Warehouse unterstützt.  
  
```sql  
update statistics t1 (a,b);   
```  
  
```sql  
update statistics t1 (a) with sample 10 rows;  
```  
  
```sql  
update statistics t1 (a) with NORECOMPUTE;  
```  
  
```sql  
update statistics t1 (a) with INCREMENTAL=ON;  
```  
  
```sql  
update statistics t1 (a) with stats_stream = 0x01;  
```  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die ALTER-Berechtigung in der Tabelle oder Sicht.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-update-all-statistics-on-a-table"></a>A. Update aller Statistiken für eine Tabelle  
 Im folgenden Beispiel wird die Statistik für alle Indizes in der Tabelle `SalesOrderDetail` aktualisiert.  
  
```sql  
USE AdventureWorks2012;  
GO  
UPDATE STATISTICS Sales.SalesOrderDetail;  
GO  
```  
  
### <a name="b-update-the-statistics-for-an-index"></a>B. Aktualisieren der Statistiken für einen Index  
 Im folgenden Beispiel wird die Statistik für den `AK_SalesOrderDetail_rowguid`-Index der `SalesOrderDetail`-Tabelle aktualisiert.  
  
```sql  
USE AdventureWorks2012;  
GO  
UPDATE STATISTICS Sales.SalesOrderDetail AK_SalesOrderDetail_rowguid;  
GO  
```  
  
### <a name="c-update-statistics-by-using-50-percent-sampling"></a>C. Aktualisieren von Statistiken mit einer Stichprobengröße von 50 %  
 Im folgenden Beispiel wird die Statistik für die `Name`-Spalte und die `ProductNumber`-Spalte in der `Product`-Tabelle erstellt.  
  
```sql  
USE AdventureWorks2012;  
GO  
CREATE STATISTICS Products  
    ON Production.Product ([Name], ProductNumber)  
    WITH SAMPLE 50 PERCENT  
-- Time passes. The UPDATE STATISTICS statement is then executed.  
UPDATE STATISTICS Production.Product(Products)   
    WITH SAMPLE 50 PERCENT;  
```  
  
### <a name="d-update-statistics-by-using-fullscan-and-norecompute"></a>D. Aktualisieren von Statistiken mit FULLSCAN und NORECOMPUTE  
 Im folgenden Beispiel wird die `Products`-Statistik in der `Product`-Tabelle aktualisiert, ein vollständiger Scan aller Zeilen in der `Product`-Tabelle erzwungen und alle automatischen Statistiken für die `Products`-Statistik deaktiviert.  
  
```sql  
USE AdventureWorks2012;  
GO  
UPDATE STATISTICS Production.Product(Products)  
    WITH FULLSCAN, NORECOMPUTE;  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Beispiele: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] und [!INCLUDE[ssPDW](../../includes/sspdw-md.md)].  
  
### <a name="e-update-statistics-on-a-table"></a>E. Aktualisieren aller Statistiken für eine Tabelle  
 Im folgenden Beispiel wird die Statistik `CustomerStats1` in der Tabelle `Customer` aktualisiert.  
  
```sql  
UPDATE STATISTICS Customer ( CustomerStats1 );  
```  
  
### <a name="f-update-statistics-by-using-a-full-scan"></a>F. Aktualisieren von Statistiken mithilfe einer vollständigen Überprüfung  
 Im folgenden Beispiel wird die Statistik `CustomerStats1` basierend auf allen Zeilen in der Tabelle `Customer` aktualisiert.  
  
```sql  
UPDATE STATISTICS Customer (CustomerStats1) WITH FULLSCAN;  
```  
  
### <a name="g-update-all-statistics-on-a-table"></a>G. Update aller Statistiken für eine Tabelle  
 Im folgenden Beispiel werden alle Statistiken in der Tabelle `Customer` aktualisiert.  
  
```sql  
UPDATE STATISTICS Customer;  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Statistik](../../relational-databases/statistics/statistics.md)   
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [CREATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/create-statistics-transact-sql.md)   
 [DBCC SHOW_STATISTICS &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md)   
 [DROP STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/drop-statistics-transact-sql.md)   
 [sp_autostats &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-autostats-transact-sql.md)   
 [sp_updatestats &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-updatestats-transact-sql.md)   
 [STATS_DATE &#40;Transact-SQL&#41;](../../t-sql/functions/stats-date-transact-sql.md)  
 [sys.dm_db_stats_properties (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-db-stats-properties-transact-sql.md) [sys.dm_db_stats_histogram (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-db-stats-histogram-transact-sql.md) 
  




---
title: UPDATE STATISTICS (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 11/20/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- UPDATE STATISTICS
- UPDATE_STATISTICS_TSQL
dev_langs: TSQL
helpviewer_keywords:
- updating statistics
- query optimization statistics [SQL Server], updating
- UPDATE STATISTICS statement
- statistical information [SQL Server], updating
ms.assetid: 919158f2-38d0-4f68-82ab-e1633bd0d308
caps.latest.revision: "74"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 96ace864a1cff7724451b521db4b184323db6d8e
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="update-statistics-transact-sql"></a>UPDATE STATISTICS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Aktualisiert eine Abfrageoptimierungsstatistik für eine Tabelle oder indizierte Sicht. Standardmäßig aktualisiert der Abfrageoptimierer Statistiken bereits als nötig, um den Abfrageplan zu verbessern; In einigen Fällen können Sie die abfrageleistung verbessern, indem Sie UPDATE STATISTICS oder der gespeicherten Prozedur [Sp_updatestats](../../relational-databases/system-stored-procedures/sp-updatestats-transact-sql.md) so aktualisieren Sie Statistiken häufiger als die Standardeinstellung.  
  
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
 Ist der Name der Tabelle oder indizierten Sicht, der die Statistik-Objekt enthält.  
  
 *index_or_statistics_name*  
 Der Name des Index, für den die Statistik aktualisiert werden soll, oder der Name der zu aktualisierenden Statistik. Wenn *Index_or_statistics_name* nicht angegeben ist, wird der Abfrageoptimierer aktualisiert alle Statistiken für die Tabelle oder indizierte Sicht. Dies schließt Statistiken ein, die mithilfe der CREATE STATISTICS-Anweisung erstellt wurden, Statistiken für einzelne Spalten, die mit aktivierter AUTO_CREATE_STATISTICS-Option erstellt wurden, sowie für Indizes erstellte Statistiken.  
  
 Weitere Informationen zu AUTO_CREATE_STATISTICS finden Sie unter [ALTER DATABASE SET-Optionen &#40; Transact-SQL &#41; ](../../t-sql/statements/alter-database-transact-sql-set-options.md). Um alle Indizes für eine Tabelle oder Sicht anzuzeigen, können Sie [Sp_helpindex](../../relational-databases/system-stored-procedures/sp-helpindex-transact-sql.md).  
  
 FULLSCAN  
 Berechnen Sie die Statistik, indem Sie alle Zeilen in der Tabelle oder indizierten Sicht scannen. FULLSCAN und SAMPLE 100 PERCENT führen zu gleichen Ergebnissen. FULLSCAN kann nicht in Verbindung mit der SAMPLE-Option verwendet werden.  
  
 Beispiel *Anzahl* {Prozent | ZEILEN}  
 Gibt den ungefähren Prozentsatz oder die ungefähre Anzahl von Zeilen in der Tabelle oder indizierten Sicht an, die vom Abfrageoptimierer beim Aktualisieren von Statistiken verwendet werden soll. Für PERCENT *Anzahl* kann einen Wert von 0 bis 100 und für Zeilen, *Anzahl* Werte von 0 bis die Gesamtzahl der Zeilen. Der tatsächliche Prozentsatz oder die tatsächliche Anzahl von Zeilen, die vom Abfrageoptimierer als Stichprobe entnommen werden, stimmt möglicherweise nicht mit dem angegebenen Prozentsatz oder der angegebenen Anzahl überein. Der Abfrageoptimierer scannt z. B. alle Zeilen auf einer Datenseite.  
  
 Beispiel eignet sich für Spezialfälle, in denen der auf standardstichproben beruhende Abfrageplan nicht optimal ist. In den meisten Situationen muss SAMPLE nicht angegeben werden, da der Abfrageoptimierer standardmäßig Stichproben verwendet und die statistisch signifikante Stichprobengröße ermittelt, wie zum Erstellen hochwertiger Abfragepläne erforderlich. 
 
Beginnend mit [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], Stichprobenentnahme von Daten zum Erstellen von Statistiken erfolgt gleichzeitig bei Kompatibilitätsgrad 130 zur Verfügung, zum Verbessern der Leistung der Sammlung von Statistikdaten zur Verwendung. Wenn die Tabellengröße einer einen bestimmten Schwellenwert überschreitet, verwendet der Abfrageoptimierer Statistiken parallel-Beispiels. 
   
 SAMPLE kann nicht in Verbindung mit der Option FULLSCAN verwendet werden. Wenn weder SAMPLE noch FULLSCAN angegeben wurde, verwendet der Abfrageoptimierer Stichprobendaten und berechnet die Stichprobengröße anhand der Standardeinstellungen.  
  
 Es wird davon abgeraten, 0 PERCENT oder 0 ROWS anzugeben. Wenn 0 PERCENT oder ROWS angegeben ist, wird das Statistikobjekt aktualisiert, es enthält jedoch keine Statistikdaten.  
  
 Eine vollständige Überprüfung ist nicht erforderlich, und Standardstichprobe ist ausreichend, für die meisten Arbeitslasten.  
Bestimmte arbeitsauslastungen, die empfindlich gegenüber verschiedenen datenverteilungen sind erfordern jedoch eine höhere Stichprobengröße oder sogar eine vollständige Überprüfung.  
Weitere Informationen finden Sie unter der [Blog von CSS SQL Eskalation Services](http://blogs.msdn.com/b/psssql/archive/2010/07/09/sampling-can-produce-less-accurate-statistics-if-the-data-is-not-evenly-distributed.aspx).  
  
 RESAMPLE  
 Aktualisieren Sie alle Statistiken mithilfe ihrer letzten Samplingraten.  
  
 Die Verwendung von RESAMPLE kann zu einem vollständigen Tabellenscan führen. Zum Beispiel verwenden die Statistiken für Indizes einen vollständigen Tabellenscan für ihre Beispielrate. Wenn keine der Stichprobenoptionen (SAMPLE, FULLSCAN, RESAMPLE) angegeben wurde, verwendet der Abfrageoptimierer Stichprobendaten und berechnet standardmäßig die Stichprobengröße.  

PERSIST_SAMPLE_PERCENT = {ON | {OFF}  
Wenn **ON**, behält die Statistiken den Satz Sampling Prozentsatz für nachfolgende Updates, die einen Sampling Prozentsatz nicht explizit angeben. Wenn **OFF**, Statistiken Sampling Prozentsatz wird auf standardstichproben bei nachfolgenden Updates, die nicht explizit einen Prozentsatz für die Stichprobe angeben zurückgesetzt abrufen. Die Standardeinstellung ist **OFF**. 
 
 > [!NOTE]
 > Wenn AUTO_UPDATE_STATISTICS ausgeführt wird, verwendet den beibehaltenen Sampling-Prozentsatz, falls verfügbar, oder verwenden Sampling Standardprozentsatz, ist dies nicht.
 > Führen Sie ein RESAMPLING Verhalten wird durch diese Option nicht betroffen.
 
 > [!TIP] 
 > [DBCC SHOW_STATISTICS](../../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md) und [dm_db_stats_properties](../../relational-databases/system-dynamic-management-views/sys-dm-db-stats-properties-transact-sql.md) verfügbar zu machen den persistenten Beispiel Prozentwert für die ausgewählte Statistik.
 
 **Gilt für**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] (beginnend mit [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1 CU4) über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] (beginnend mit [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU1).  
 
 PARTITIONEN ({ \<Partitionsnummer > | \<Bereich >} [,... n]) ] Erzwingt, dass die Statistiken auf Blattebene, die für die Partitionen, angegeben in der ON PARTITIONS-Klausel neu berechnet werden, und klicken Sie dann zusammengeführt, um die globale Statistik zu bilden. WITH RESAMPLE ist erforderlich, da mit unterschiedlichen Stichprobenraten erstellte Partitionsstatistiken nicht zusammengeführt werden können.  
  
**Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] über[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
 ALL | COLUMNS | INDEX  
 Aktualisieren Sie alle vorhandenen Statistiken, für eine oder mehrere Spalten erstellte Statistiken oder für Indizes erstellte Statistiken. Wenn keine der Optionen angegeben wird, aktualisiert die UPDATE STATISTICS-Anweisung alle Statistiken für die Tabelle oder indizierte Sicht.  
  
 NORECOMPUTE  
 Deaktiviert die AUTO_UPDATE_STATISTICS-Option zum automatischen Statistikupdate für die angegebene Statistik. Wenn diese Option angegeben wird, schließt der Abfrageoptimierer dieses Statistikupdate ab und deaktiviert zukünftige Updates.  
  
 Das Verhalten der AUTO_UPDATE_STATISTICS-Option wieder zu aktivieren, führen Sie UPDATE STATISTICS erneut ohne die NORECOMPUTE-Option oder ausführen **Sp_autostats**.  
  
> [!WARNING]  
>  Bei Verwendung dieser Option können suboptimale Abfragepläne entstehen. Es wird empfohlen, diese Option nur in Einzelfällen von einem qualifizierten Systemadministrator vornehmen zu lassen.  
  
 Weitere Informationen zur AUTO_STATISTICS_UPDATE-Option finden Sie unter [ALTER DATABASE SET-Optionen &#40; Transact-SQL &#41; ](../../t-sql/statements/alter-database-transact-sql-set-options.md).  
  
 INCREMENTAL = { ON | OFF }  
 Wenn **ON**, die Statistiken als Statistiken pro Partition neu erstellt werden. Wenn **OFF**, wird die statistikstruktur gelöscht und [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] die Statistiken neu berechnet. Die Standardeinstellung ist **OFF**.  
  
 Wenn Statistiken pro Partition nicht unterstützt werden, wird ein Fehler generiert. Inkrementelle Statistiken werden für folgende Statistiktypen nicht unterstützt:  
  
-   Statistiken, die mit Indizes erstellt wurden, die über keine Partitionsausrichtung mit der Basistabelle verfügen.  
  
-   Statistiken, die für lesbare sekundäre Always On-Datenbanken erstellt wurden.  
  
-   Statistiken, die für schreibgeschützte Datenbanken erstellt wurden.  
  
-   Statistiken, die für gefilterte Indizes erstellt wurden.  
  
-   Statistiken, die für Sichten erstellt wurden.  
  
-   Statistiken, die für interne Tabellen erstellt wurden.  
  
-   Statistiken, die mit räumlichen Indizes oder XML-Indizes erstellt wurden.  
  
**Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] über[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
 \<Update_stats_stream_option >[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
## <a name="remarks"></a>Hinweise  
  
## <a name="when-to-use-update-statistics"></a>Wann UPDATE STATISTICS verwendet werden sollte  
 Weitere Informationen zur Verwendung von UPDATE STATISTICS, finden Sie unter [Statistiken](../../relational-databases/statistics/statistics.md).  
  
## <a name="updating-all-statistics-with-spupdatestats"></a>Aktualisieren aller Statistiken mit "sp_updatestats"  
 Informationen zum Aktualisieren von Statistiken für alle benutzerdefinierten und internen Tabellen in der Datenbank finden Sie in der Beschreibung der gespeicherten Prozedur [sp_updatestats &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-updatestats-transact-sql.md). Durch den folgenden Befehl wird beispielsweise sp_updatestats zum Aktualisieren aller Statistiken für die Datenbank aufgerufen.  
  
```t-sql  
EXEC sp_updatestats;  
```  
  
## <a name="determining-the-last-statistics-update"></a>Ermitteln des letzten Statistikupdates  
 Um zu ermitteln, wann Statistiken zuletzt aktualisiert wurden, verwenden Sie die [STATS_DATE](../../t-sql/functions/stats-date-transact-sql.md) -Funktion.  
  
## <a name="pdw--sql-data-warehouse"></a>PDW / SQL Data Warehouse  
 Die folgende Syntax wird von PDW nicht unterstützt / SQL Data Warehouse  
  
```t-sql  
update statistics t1 (a,b);   
```  
  
```t-sql  
update statistics t1 (a) with sample 10 rows;  
```  
  
```t-sql  
update statistics t1 (a) with NORECOMPUTE;  
```  
  
```t-sql  
update statistics t1 (a) with INCREMENTAL=ON;  
```  
  
```t-sql  
update statistics t1 (a) with stats_stream = 0x01;  
```  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die ALTER-Berechtigung in der Tabelle oder Sicht.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-update-all-statistics-on-a-table"></a>A. Update aller Statistiken für eine Tabelle  
 Das folgende Beispiel aktualisiert die Statistiken für alle Indizes auf die `SalesOrderDetail` Tabelle.  
  
```t-sql  
USE AdventureWorks2012;  
GO  
UPDATE STATISTICS Sales.SalesOrderDetail;  
GO  
```  
  
### <a name="b-update-the-statistics-for-an-index"></a>B. Aktualisieren der Statistiken für einen Index  
 Im folgenden Beispiel wird die Statistik für den `AK_SalesOrderDetail_rowguid`-Index der `SalesOrderDetail`-Tabelle aktualisiert.  
  
```t-sql  
USE AdventureWorks2012;  
GO  
UPDATE STATISTICS Sales.SalesOrderDetail AK_SalesOrderDetail_rowguid;  
GO  
```  
  
### <a name="c-update-statistics-by-using-50-percent-sampling"></a>C. Aktualisieren von Statistiken mit einer Stichprobengröße von 50 %  
 Im folgenden Beispiel wird die Statistik für die `Name`-Spalte und die `ProductNumber`-Spalte in der `Product`-Tabelle erstellt.  
  
```t-sql  
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
  
```t-sql  
USE AdventureWorks2012;  
GO  
UPDATE STATISTICS Production.Product(Products)  
    WITH FULLSCAN, NORECOMPUTE;  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Beispiele: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] und[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="e-update-statistics-on-a-table"></a>E. Aktualisieren von Statistiken für eine Tabelle  
 Das folgende Beispiel aktualisiert die `CustomerStats1` Statistiken für die `Customer` Tabelle.  
  
```t-sql  
UPDATE STATISTICS Customer ( CustomerStats1 );  
```  
  
### <a name="f-update-statistics-by-using-a-full-scan"></a>F. Aktualisieren von Statistiken mit einer vollständigen Überprüfung  
 Das folgende Beispiel aktualisiert die `CustomerStats1` Statistiken, basierend auf das Scannen aller Zeilen in der `Customer` Tabelle.  
  
```t-sql  
UPDATE STATISTICS Customer (CustomerStats1) WITH FULLSCAN;  
```  
  
### <a name="g-update-all-statistics-on-a-table"></a>G. Update aller Statistiken für eine Tabelle  
 Das folgende Beispiel aktualisiert alle Statistiken für die `Customer` Tabelle.  
  
```t-sql  
UPDATE STATISTICS Customer;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Statistiken](../../relational-databases/statistics/statistics.md)   
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [CREATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/create-statistics-transact-sql.md)   
 [DBCC SHOW_STATISTICS &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md)   
 [DROP STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/drop-statistics-transact-sql.md)   
 [Sp_autostats &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-autostats-transact-sql.md)   
 [sp_updatestats &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-updatestats-transact-sql.md)   
 [STATS_DATE &#40; Transact-SQL &#41;](../../t-sql/functions/stats-date-transact-sql.md)  
 [Sys. dm_db_stats_properties &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-db-stats-properties-transact-sql.md) [sys.dm_db_stats_histogram &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-stats-histogram-transact-sql.md) 
  




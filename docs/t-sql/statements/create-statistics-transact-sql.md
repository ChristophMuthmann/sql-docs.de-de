---
title: CREATE STATISTICS (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/10/2017
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
- STATISTICS
- STATISTICS_TSQL
- CREATE STATISTICS
- CREATE_STATISTICS_TSQL
dev_langs: TSQL
helpviewer_keywords:
- query optimization statistics [SQL Server], creating
- indexed views [SQL Server], statistics
- FULLSCAN option
- CREATE STATISTICS statement
- filtered statistics [SQL Server]
- creating statistics [SQL Server]
- NORECOMPUTE clause
ms.assetid: b23e2f6b-076c-4e6d-9281-764bdb616ad2
caps.latest.revision: "105"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: b34ea1ffe5a61b8cb7a0ba8b695015a8655c8709
ms.sourcegitcommit: 2208a909ab09af3b79c62e04d3360d4d9ed970a7
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/02/2018
---
# <a name="create-statistics-transact-sql"></a>CREATE STATISTICS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Erstellt abfrageoptimierungsstatistiken für eine oder mehrere Spalten einer Tabelle, einer indizierten Sicht oder eine externe Tabelle. Bei den meisten Abfragen generiert der Abfrageoptimierer automatisch die notwendigen Statistiken für einen hochwertigen Abfrageplan; in einigen Fällen müssen Sie weitere Statistiken mithilfe von CREATE STATISTICS erstellen oder den Abfrageentwurf ändern, um die Abfrageleistung zu verbessern.  
  
 Weitere Informationen finden Sie unter [Statistiken](../../relational-databases/statistics/statistics.md).  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
-- Create statistics on an external table  
CREATE STATISTICS statistics_name   
ON { table_or_indexed_view_name } ( column [ ,...n ] )   
    [ WITH FULLSCAN ] ;  
  
-- Create statistics on a regular table or indexed view  
CREATE STATISTICS statistics_name   
ON { table_or_indexed_view_name } ( column [ ,...n ] )   
    [ WHERE <filter_predicate> ]  
    [ WITH   
        [ [ FULLSCAN   
            [ [ , ] PERSIST_SAMPLE_PERCENT = { ON | OFF } ]    
          | SAMPLE number { PERCENT | ROWS }   
            [ [ , ] PERSIST_SAMPLE_PERCENT = { ON | OFF } ]    
          | STATS_STREAM = stats_stream ] ]   
        [ [ , ] NORECOMPUTE ]   
        [ [ , ] INCREMENTAL = { ON | OFF } ]  
    ] ;  
  
<filter_predicate> ::=   
    <conjunct> [AND <conjunct>]  
  
<conjunct> ::=  
    <disjunct> | <comparison>  
  
<disjunct> ::=  
        column_name IN (constant ,…)  
  
<comparison> ::=  
        column_name <comparison_op> constant  
  
<comparison_op> ::=  
    IS | IS NOT | = | <> | != | > | >= | !> | < | <= | !<  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
CREATE STATISTICS statistics_name   
    ON [ database_name . [schema_name ] . | schema_name. ] table_name   
    ( column_name  [ ,...n ] )   
    [ WHERE <filter_predicate> ]  
    [ WITH {  
           FULLSCAN   
           | SAMPLE number PERCENT   
      }  
    ]  
[;]  
  
<filter_predicate> ::=   
    <conjunct> [AND <conjunct>]  
  
<conjunct> ::=  
    <disjunct> | <comparison>  
  
<disjunct> ::=  
        column_name IN (constant ,…)  
  
<comparison> ::=  
        column_name <comparison_op> constant  
  
<comparison_op> ::=  
    IS | IS NOT | = | <> | != | > | >= | !> | < | <= | !<  
```  
  
## <a name="arguments"></a>Argumente  
 *statistics_name*  
 Der Name der zu erstellenden Statistik.  
  
 *table_or_indexed_view_name*  
 Ist der Name der Tabelle, indizierten Sicht oder externen Tabelle, für die die Statistik erstellt. Um Statistiken auf einer anderen Datenbank zu erstellen, geben Sie einen vollqualifizierten Tabellennamen an.  
  
 *Spalte [,... n]*  
 Mindestens eine Spalte, in der Statistik eingeschlossen werden sollen. Die Spalten muss in der Reihenfolge ihrer Priorität von links nach rechts. Nur die erste Spalte dient zum Erstellen des Histogramms. Alle Spalten werden für spaltenübergreifende korrelationsstatistiken, die genannte dichten verwendet.  
  
 Sie können beliebige Spalten angeben, die von folgenden Ausnahmen abgesehen als Indexschlüsselspalte angegeben werden können:  
  
-   **XML**Full- Text, und FILESTREAM-Spalten können nicht angegeben werden.  
  
-   Berechnete Spalten können nur angegeben werden, wenn die DARITHABORT-Datenbankeinstellung und die QUOTED_IDENTIFIER-Datenbankeinstellung auf ON festgelegt sind.  
  
-   Spalten des CLR-benutzerdefiniertne Typs können angegeben werden, wenn der Typ die binäre Reihenfolge unterstützt. Berechnete Spalten, die als Methodenaufrufe einer Spalte eines benutzerdefinierten Typs definiert sind, können angegeben werden, wenn die Methoden als deterministisch gekennzeichnet sind.  
  
 WOBEI \<Filter_predicate > Gibt einen Ausdruck für die Auswahl einer Teilmenge von Zeilen, die beim Erstellen des statistikobjekts eingeschlossen. Statistiken, die mit einem Filterprädikat erstellt werden, werden als gefilterte Statistiken bezeichnet. Das Filterprädikat verwendet einfache Vergleichslogik und kann nicht auf eine berechnete Spalte, eine UDT-Spalte, eine Spalte für räumliche Daten geben, verweisen oder eine **HierarchyID** -Datentypspalte. Vergleiche mit NULL-Literalen sind mit den Vergleichsoperatoren nicht zulässig. Verwenden Sie stattdessen den IS NULL-Operator und den IS NOT NULL-Operator.  
  
 Es folgen einige Beispiele für Filterprädikate für die Production.BillOfMaterials-Tabelle:  
  
 `WHERE StartDate > '20000101' AND EndDate <= '20000630'`  
  
 `WHERE ComponentID IN (533, 324, 753)`  
  
 `WHERE StartDate IN ('20000404', '20000905') AND EndDate IS NOT NULL`  
  
 Weitere Informationen zu Filterprädikaten finden Sie unter [Create Filtered Indexes](../../relational-databases/indexes/create-filtered-indexes.md).  
  
 FULLSCAN  
 Berechnen von Statistiken durch das Scannen aller Zeilen. FULLSCAN und SAMPLE 100 PERCENT führen zu gleichen Ergebnissen. FULLSCAN kann nicht in Verbindung mit der SAMPLE-Option verwendet werden.  
  
 Wenn nicht angegeben ist, SQL Server Stichproben verwendet, um die Statistiken zu erstellen und bestimmt die Größe der Stichprobe, die erforderlich sind, um einen hochwertigen Abfrageplan zu erstellen.  
  
 Beispiel *Anzahl* {Prozent | ZEILEN}  
 Gibt den ungefähren Prozentsatz oder die ungefähre Anzahl von Zeilen in der Tabelle oder indizierten Sicht an, die vom Abfrageoptimierer beim Erstellen von Statistiken verwendet werden sollen. Für PERCENT *Anzahl* kann einen Wert von 0 bis 100 und für Zeilen, *Anzahl* Werte von 0 bis die Gesamtzahl der Zeilen. Der tatsächliche Prozentsatz oder die tatsächliche Anzahl von Zeilen, die vom Abfrageoptimierer als Stichprobe entnommen werden, stimmt möglicherweise nicht mit dem angegebenen Prozentsatz oder der angegebenen Anzahl überein. Der Abfrageoptimierer scannt z. B. alle Zeilen auf einer Datenseite.  
  
 Beispiel eignet sich für Spezialfälle, in denen der auf standardstichproben beruhende Abfrageplan nicht optimal ist. In den meisten Situationen muss SAMPLE nicht angegeben werden, da der Abfrageoptimierer automatisch Stichproben verwendet und die statistisch signifikante Stichprobengröße ermittelt, wie zum Erstellen hochwertiger Abfragepläne erforderlich.  
  
 SAMPLE kann nicht in Verbindung mit der Option FULLSCAN verwendet werden. Wenn weder SAMPLE noch FULLSCAN angegeben wurde, verwendet der Abfrageoptimierer Stichprobendaten und berechnet die Stichprobengröße anhand der Standardeinstellungen.  
  
 Es wird davon abgeraten, 0 PERCENT oder 0 ROWS anzugeben. Wenn 0 PERCENT oder ROWS angegeben ist, wird das Statistikobjekt erstellt, es enthält jedoch keine Statistikdaten.  
 
 PERSIST_SAMPLE_PERCENT = {ON | {OFF}  
 Wenn **ON**, behält die Statistiken den Erstellung Sampling-Prozentsatz für nachfolgende Updates, die einen Sampling Prozentsatz nicht explizit angeben. Wenn **OFF**, Statistiken Sampling Prozentsatz wird auf standardstichproben bei nachfolgenden Updates, die nicht explizit einen Prozentsatz für die Stichprobe angeben zurückgesetzt abrufen. Die Standardeinstellung ist **OFF**. 
 
 **Gilt für**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] (beginnend mit [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1 CU4) über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] (beginnend mit [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU1).    
  
 STATS_STREAM  **=**  *Stats_stream*  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
 NORECOMPUTE  
 Deaktiviert die automatische Option, statistikaktualisierung für *Statistics_name*. Wenn diese Option angegeben wird, schließt der Abfrageoptimierer alle laufenden Statistikupdates für *Statistics_name* und deaktiviert zukünftige Updates.  
  
 Um Statistikupdates wieder zu aktivieren, entfernen Sie die Statistiken mit [DROP STATISTICS](../../t-sql/statements/drop-statistics-transact-sql.md) und führen Sie CREATE STATISTICS ohne die NORECOMPUTE-Option.  
  
> [!WARNING]  
>  Bei Verwendung dieser Option können suboptimale Abfragepläne entstehen. Es wird empfohlen, diese Option nur in Einzelfällen von einem qualifizierten Systemadministrator vornehmen zu lassen.  
  
 Weitere Informationen zur AUTO_STATISTICS_UPDATE-Option finden Sie unter [ALTER DATABASE SET-Optionen &#40; Transact-SQL &#41; ](../../t-sql/statements/alter-database-transact-sql-set-options.md). Weitere Informationen zu deaktivieren und erneutes Aktivieren von Statistikupdates finden Sie unter [Statistiken](../../relational-databases/statistics/statistics.md).  
  
 INCREMENTAL = { ON | OFF }  
 Wenn **ON**, die Statistiken erstellt werden, pro Partition. Wenn **OFF**, werden Statistiken für alle Partitionen kombiniert. Die Standardeinstellung ist **OFF**.  
  
 Wenn Statistiken pro Partition nicht unterstützt werden, wird ein Fehler generiert. Inkrementelle Statistiken werden für folgende Statistiktypen nicht unterstützt:  
  
-   Statistiken, die mit Indizes erstellt wurden, die über keine Partitionsausrichtung mit der Basistabelle verfügen.  
  
-   Statistiken, die für lesbare sekundäre Always On-Datenbanken erstellt wurden.  
  
-   Statistiken, die für schreibgeschützte Datenbanken erstellt wurden.  
  
-   Statistiken, die für gefilterte Indizes erstellt wurden.  
  
-   Statistiken, die für Sichten erstellt wurden.  
  
-   Statistiken, die für interne Tabellen erstellt wurden.  
  
-   Statistiken, die mit räumlichen Indizes oder XML-Indizes erstellt wurden.  
  
**Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert eine der folgenden Berechtigungen:  
  
-   ALTER TABLE  
  
-   Benutzer ist der Besitzer der Tabelle  
  
-   Mitgliedschaft in der **Db_ddladmin** festen Datenbankrolle ""  
  
## <a name="general-remarks"></a>Allgemeine Hinweise  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]können Tempdb als Stichprobe entnommenen Zeilen vor dem Erstellen von Statistiken sortieren.  
  
### <a name="statistics-for-external-tables"></a>Statistiken für externe Tabellen  
 Beim Erstellen von Statistiken für externe Tabellen, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] importiert Sie die externe Tabelle in eine temporäre [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Tabelle, und klicken Sie dann die Statistik erstellt. Für Beispiele Statistiken werden nur die als Stichprobe entnommenen Zeilen importiert. Wenn Sie eine große externe Tabelle verfügen, werden wesentlich schneller, die standardmäßigen stichprobenraten anstelle der vollständigen Scan-Option verwendet.  
  
### <a name="statistics-with-a-filtered-condition"></a>Statistiken mit der eine gefilterte Bedingung  
 Gefilterte Statistiken können die Abfrageleistung für Abfragen verbessern, bei denen aus klar definierten Teilmengen von Daten ausgewählt wird. Gefilterte Statistiken verwenden ein Filterprädikat in der WHERE-Klausel, um die Teilmenge von Daten auszuwählen, die in den Statistiken enthalten ist.  
  
### <a name="when-to-use-create-statistics"></a>Verwendung von CREATE STATISTICS  
 Weitere Informationen zur Verwendung von CREATE STATISTICS finden Sie unter [Statistiken](../../relational-databases/statistics/statistics.md).  
  
### <a name="referencing-dependencies-for-filtered-statistics"></a>Verweisen auf Abhängigkeiten für gefilterte Statistiken  
 Die [Sys. sql_expression_dependencies](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md) -Katalogsicht kennzeichnet jede Spalte im gefilterten statistikprädikat als eine verweisende Abhängigkeit. Überlegen Sie genau, welche Vorgänge Sie für Tabellenspalten ausführen, bevor Sie eine gefilterte Statistik erstellen, da Sie die Definition einer Tabellenspalte, die für ein Prädikat einer gefilterten Statistik definiert wurde, nicht löschen, umbenennen oder ändern können.  
  
## <a name="limitations-and-restrictions"></a>Einschränkungen  
*  Aktualisieren von Statistiken wird in externen Tabellen nicht unterstützt. Zum Aktualisieren der Statistiken für eine externe Tabelle löschen und Neuerstellen von Statistiken.  
*  Sie können bis zu 64 Spalten pro Statistikobjekt auflisten.
  
## <a name="examples"></a>Beispiele  

### <a name="examples-use-the-adventureworks-database"></a>Beispiele verwenden die AdventureWorks-Datenbank.  

### <a name="a-using-create-statistics-with-sample-number-percent"></a>A. Verwenden von CREATE STATISTICS mit SAMPLE number PERCENT  
 Im folgenden Beispiel wird die `ContactMail1`-Statistik erstellt. Dabei wird eine zufällige Stichprobe von 5 Prozent der Spalten `BusinessEntityID` und `EmailPromotion` aus der Tabelle `Contact` der [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]-Datenbank verwendet.  
  
```sql  
CREATE STATISTICS ContactMail1  
    ON Person.Person (BusinessEntityID, EmailPromotion)  
    WITH SAMPLE 5 PERCENT;  
```  
  
### <a name="b-using-create-statistics-with-fullscan-and-norecompute"></a>B. Verwenden von CREATE STATISTICS mit FULLSCAN und NORECOMPUTE  
 Im folgenden Beispiel werden die `ContactMail2`-Statistiken für alle Zeilen in der `BusinessEntityID`-Spalte und der `EmailPromotion`-Spalte der `Contact`-Tabelle erstellt. Dabei wird die automatische Neuberechnung von Statistiken deaktiviert.  
  
```sql  
CREATE STATISTICS NamePurchase  
    ON AdventureWorks2012.Person.Person (BusinessEntityID, EmailPromotion)  
    WITH FULLSCAN, NORECOMPUTE;  
```  
  
### <a name="c-using-create-statistics-to-create-filtered-statistics"></a>C. Erstellen gefilterter Statistiken mithilfe von CREATE STATISTICS  
 Im folgenden Beispiel wird die gefilterte Statistik `ContactPromotion1` erstellt. Das [!INCLUDE[ssDE](../../includes/ssde-md.md)] nimmt 50 Prozent der Daten in die Stichprobe auf und wählt dann die Zeilen aus, in denen `EmailPromotion` gleich 2 ist.  
  
```sql  
CREATE STATISTICS ContactPromotion1  
    ON Person.Person (BusinessEntityID, LastName, EmailPromotion)  
WHERE EmailPromotion = 2  
WITH SAMPLE 50 PERCENT;  
GO  
```  
  
### <a name="d-create-statistics-on-an-external-table"></a>D. Erstellen von Statistiken für eine externe Tabelle  
 Die einzige Entscheidung, die bei der Erstellung von Statistiken für eine external Table, neben der Bereitstellung der Liste der Spalten, benötigten ist, ob die Statistiken durch Stichproben von Zeilen oder durch das Scannen aller Zeilen erstellt.  
  
 Da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] importiert Daten aus der externen Tabelle in eine temporäre Tabelle zum Erstellen von Statistiken, die vollständigen Scan-Option werden deutlich länger dauern. Für eine große Tabelle ist die Standardmethode für die Stichprobenentnahme in der Regel ausreichend.  
  
```sql  
--Create statistics on an external table and use default sampling.  
CREATE STATISTICS CustomerStats1 ON DimCustomer (CustomerKey, EmailAddress);  
  
--Create statistics on an external table and scan all the rows  
CREATE STATISTICS CustomerStats1 ON DimCustomer (CustomerKey, EmailAddress) WITH FULLSCAN;  
```  

### <a name="e-using-create-statistics-with-fullscan-and-persistsamplepercent"></a>E. Verwenden von CREATE STATISTICS mit FULLSCAN und PERSIST_SAMPLE_PERCENT  
 Das folgende Beispiel erstellt die `ContactMail2` Statistiken für alle Zeilen in der `BusinessEntityID` und `EmailPromotion` Spalten von der `Contact` -Tabelle und legt fest, 100 Prozent Sampling Prozentsatz sämtliche nachfolgenden Updates, die nicht explizit eine Stichprobe angeben Prozentsatz.  
  
```sql  
CREATE STATISTICS NamePurchase  
    ON AdventureWorks2012.Person.Person (BusinessEntityID, EmailPromotion)  
    WITH FULLSCAN, PERSIST_SAMPLE_PERCENT = ON;  
```  
  
### <a name="examples-using-adventureworksdw-database"></a>Beispiele zur Verwendung der AdventureWorksDW-Datenbank. 
  
### <a name="f-create-statistics-on-two-columns"></a>F. Erstellen von Statistiken für zwei Spalten  
 Das folgende Beispiel erstellt die `CustomerStats1` Statistiken, basierend auf den `CustomerKey` und `EmailAddress` Spalten von der `DimCustomer` Tabelle. Die Statistiken werden basierend auf der Zeilen in eine statistisch signifikante Stichprobe erstellt die `Customer` Tabelle.  
  
```sql  
CREATE STATISTICS CustomerStats1 ON DimCustomer (CustomerKey, EmailAddress);  
```  
  
### <a name="g-create-statistics-by-using-a-full-scan"></a>G. Erstellen von Statistiken mit einer vollständigen Überprüfung  
 Das folgende Beispiel erstellt die `CustomerStatsFullScan` Statistiken, basierend auf das Scannen aller Zeilen in der `DimCustomer` Tabelle.  
  
```sql  
CREATE STATISTICS CustomerStatsFullScan 
ON DimCustomer (CustomerKey, EmailAddress) WITH FULLSCAN;  
```  
  
### <a name="h-create-statistics-by-specifying-the-sample-percentage"></a>H. Statistiken zu erstellen, indem Sie den Prozentsatz angeben, Beispiel  
 Das folgende Beispiel erstellt die `CustomerStatsSampleScan` Statistiken, die basierend auf Scannen von 50 Prozent der Zeilen in der `DimCustomer` Tabelle.  
  
```sql  
CREATE STATISTICS CustomerStatsSampleScan 
ON DimCustomer (CustomerKey, EmailAddress) WITH SAMPLE 50 PERCENT;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Statistiken](../../relational-databases/statistics/statistics.md)   
 [UPDATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/update-statistics-transact-sql.md)   
 [sp_updatestats &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-updatestats-transact-sql.md)   
 [DBCC SHOW_STATISTICS &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md)   
 [DROP STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/drop-statistics-transact-sql.md)   
 [sys.stats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-stats-transact-sql.md)   
 [Sys. stats_columns &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-stats-columns-transact-sql.md)  
  
  


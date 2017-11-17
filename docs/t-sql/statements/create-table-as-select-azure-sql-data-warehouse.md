---
title: Erstellen der Tabelle als Option (Azure SQL Datawarehouse) | Microsoft Docs
ms.custom: 
ms.date: 10/07/2016
ms.prod: 
ms.prod_service: sql-data-warehouse, pdw
ms.reviewer: 
ms.service: sql-data-warehouse
ms.component: t-sql|statements
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: d1e08f88-64ef-4001-8a66-372249df2533
caps.latest.revision: 40
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 2f95f9bc6975593f2536848e2bb3a2b346eca538
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="create-table-as-select-azure-sql-data-warehouse"></a>Erstellen der Tabelle als Option (Azure SQL Datawarehouse)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

Erstellen Sie Tabelle AS auswählen (CTAS) ist eine der wichtigsten T-SQL-Funktionen verfügbar. Es ist ein vollständig parallelisierte Vorgang, der eine neue Tabelle basierend auf der Ausgabe von einer SELECT-Anweisung erstellt. CTAS ist die schnellste und einfachste Möglichkeit, eine Kopie einer Tabelle zu erstellen.   
 
 Verwenden Sie z. B. CTAS an:  
  
-   Erstellen Sie eine Tabelle mit einem anderen Hash-verteilungsspalte erneut.
-   Neuerstellen einer Tabellenstatus als repliziert.   
-   Erstellen Sie einen columnstore-Index auf nur einige der Spalten in der Tabelle.  
-   Abfragen oder externe Daten zu importieren.  

> [!NOTE]  
> Da die Funktionen zum Erstellen einer Tabellenstatus CTAS hinzufügt, versucht, in diesem Thema nicht die CREATE TABLE-Thema zu wiederholen. Stattdessen wird hier beschrieben, die Unterschiede zwischen der CTAS und CREATE TABLE-Anweisung. Die CREATE TABLE-Details finden Sie unter [CREATE TABLE (Azure SQL Data Warehouse)](https://msdn.microsoft.com/library/mt203953/) Anweisung. 
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
<a name="syntax-bk"></a>

## <a name="syntax"></a>Syntax   

```  
CREATE TABLE [ database_name . [ schema_name ] . | schema_name. ] table_name   
    [ ( column_name [ ,...n ] ) ]  
    WITH ( 
      <distribution_option> -- required
      [ , <table_option> [ ,...n ] ]    
    )  
    AS <select_statement>   
[;]  

<distribution_option> ::=
    { 
        DISTRIBUTION = HASH ( distribution_column_name ) 
      | DISTRIBUTION = ROUND_ROBIN 
      | DISTRIBUTION = REPLICATE
    }   

<table_option> ::= 
    {   
        CLUSTERED COLUMNSTORE INDEX --default for SQL Data Warehouse 
      | HEAP --default for Parallel Data Warehouse   
      | CLUSTERED INDEX ( { index_column_name [ ASC | DESC ] } [ ,...n ] ) --default is ASC 
    }  
    | PARTITION ( partition_column_name RANGE [ LEFT | RIGHT ] --default is LEFT  
        FOR VALUES ( [ boundary_value [,...n] ] ) ) 
  
<select_statement> ::=  
    [ WITH <common_table_expression> [ ,...n ] ]  
    SELECT select_criteria  

```  

<a name="arguments-bk"></a>
  
## <a name="arguments"></a>Argumente  
Einzelheiten finden Sie in der [Abschnitt "Argumente"](https://msdn.microsoft.com/library/mt203953/#Arguments) in CREATE TABLE.  

<a name="column-options-bk"></a>

### <a name="column-options"></a>Spaltenoptionen
`column_name` [ ,...`n` ]   
 Spaltennamen dürfen keine der [Spaltenoptionen](https://msdn.microsoft.com/library/mt203953/#ColumnOptions) erwähnt in CREATE TABLE.  Stattdessen können Sie eine optionale Liste mit mindestens einem Spaltennamen für die neue Tabelle bereitstellen. Die Spalten in der neuen Tabelle werden die Namen verwenden, die Sie angeben. Wenn Sie den Spaltennamen angeben, muss die Anzahl der Spalten in der Spaltenliste der Anzahl der Spalten in der select-Ergebnisse überein. Wenn Sie alle Spaltennamen angeben, wird die neue Zieltabelle die Spaltennamen in den Ergebnissen des select-Anweisung verwenden. 
  
 Sie können keine anderen Spaltenoptionen z. B. Datentypen, Sortierung oder NULL-Zulässigkeit angeben. Jedem dieser Attribute aus den Ergebnissen der stammt die `SELECT` Anweisung. Die SELECT-Anweisung können Sie jedoch um die Attribute zu ändern. Ein Beispiel finden Sie unter [CTAS verwenden, so ändern Sie die Spaltenattribute](#ctas-change-column-attributes-bk).   

<a name="table-distribution-options-bk"></a>

### <a name="table-distribution-options"></a>Tabelle Verteilungsoptionen

`DISTRIBUTION` = `HASH`( *Distribution_column_name* ) | ROUND_ROBIN | REPLIZIEREN      
Die CTAS-Anweisung erfordert eine Option zur Verteilung und keine Standardwerte. Dies unterscheidet sich von CREATE TABLE die Standardwerte aufweist. 

Weitere Informationen und erfahren, wie die optimale verteilungsspalte auswählen, finden Sie unter der [Tabelle Verteilungsoptionen](https://msdn.microsoft.com/library/mt203953/#TableDistributionOptions) Abschnitt in CREATE TABLE. 

<a name="table-partition-options-bk"></a>

### <a name="table-partition-options"></a>Tabellenoptionen für die partition
Die CTAS-Anweisung erstellt eine nicht partitionierte Tabelle wird standardmäßig, selbst wenn die Quelltabelle partitioniert ist. Um eine partitionierte Tabelle mit der CTAS-Anweisung zu erstellen, müssen Sie die Partitionsoption angeben. 

Einzelheiten finden Sie in der [Tabelle Partitionsoptionen](https://msdn.microsoft.com/library/mt203953/#TablePartitionOptions) Abschnitt in CREATE TABLE.

<a name="select-options-bk"></a>

### <a name="select-options"></a>Wählen Sie Optionen
Die select-Anweisung ist der wesentliche Unterschied zwischen CTAS und CREATE TABLE.  

 `WITH`*Common_table_expression*  
 Gibt ein temporäres benanntes Resultset an, das als allgemeiner Tabellenausdruck (CTE, Common Table Expression) bekannt ist. Weitere Informationen finden Sie unter [WITH Common_table_expression &#40; Transact-SQL &#41; ](../../t-sql/queries/with-common-table-expression-transact-sql.md).  
  
 `SELECT`*Select_criteria*  
 Füllt die neue Tabelle mit den Ergebnissen einer SELECT-Anweisung. *Select_criteria* ist der Hauptteil der SELECT-Anweisung, der bestimmt, welche Daten in die neue Tabelle kopieren. Informationen zur SELECT-Anweisungen finden Sie unter [SELECT &#40; Transact-SQL &#41; ](../../t-sql/queries/select-transact-sql.md).  
  
<a name="permissions-bk"></a>  
  
## <a name="permissions"></a>Berechtigungen  
Erfordert CTAS `SELECT` -Berechtigung für alle Objekte der *Select_criteria*.

Berechtigungen für eine Tabelle zu erstellen, finden Sie unter [Berechtigungen](https://msdn.microsoft.com/library/mt203953/#Permissions) in CREATE TABLE. 
  
<a name="general-remarks-bk"></a>
  
## <a name="general-remarks"></a>Allgemeine Hinweise
Weitere Informationen finden Sie unter [allgemeine Hinweise](https://msdn.microsoft.com/library/mt203953/#GeneralRemarks) in CREATE TABLE.

<a name="limitations-bk"></a>

## <a name="limitations-and-restrictions"></a>Einschränkungen  
Azure SQL Data Warehouse ist noch nicht Unterstützung automatisch erstellen bzw. die automatische Update Statistics.  Um die beste Leistung von Abfragen zu erhalten, ist es wichtig, die Statistiken für alle Spalten aller Tabellen zu erstellen, nachdem Sie CTAS ausführen und wesentlichen Änderungen in der Datenquelle auftreten. Weitere Informationen finden Sie unter [CREATE STATISTICS (Transact-SQL)](../../t-sql/statements/create-statistics-transact-sql.md).

[SET ROWCOUNT &#40; Transact-SQL &#41; ](../../t-sql/statements/set-rowcount-transact-sql.md) hat keine Auswirkung auf CTAS. Um ein ähnliches Verhalten zu erzielen, verwenden [nach oben &#40; Transact-SQL &#41; ](../../t-sql/queries/top-transact-sql.md).  
 
Weitere Informationen finden Sie unter [Einschränkungen](https://msdn.microsoft.com/library/mt203953/#LimitationsRestrictions) in CREATE TABLE.

<a name="locking-behavior-bk"></a>
  
## <a name="locking-behavior"></a>Sperrverhalten  
 Weitere Informationen finden Sie unter [Sperrverhalten](https://msdn.microsoft.com/library/mt203953/#LockingBehavior) in CREATE TABLE.
 
<a name="performance-bk"></a>
 
 ## <a name="performance"></a>Leistung 

Für eine Tabelle Hash distributed können Sie CTAS zum Auswählen einer anderen Verteilungspunkt Spalte um eine bessere Leistung für Joins und Aggregationen zu erzielen. Wenn auswählen, dass eine andere Verteilung-Spalte nicht Ihr Ziel ist, müssen Sie die beste CTAS-Leistung, wenn Sie die gleichen verteilungsspalte angeben, da dies vermieden werden, erneut verteilen von Zeilen. 

Wenn Sie CTAS verwenden, um die Tabelle zu erstellen und die Leistung kein Faktor ist, können Sie angeben `ROUND_ROBIN` zu vermeiden, dass eine verteilungsspalte festlegen.

Um die datenverschiebung in nachfolgenden Abfragen zu vermeiden, können Sie angeben `REPLICATE` wird mehr Speicher für eine vollständige Kopie der Tabelle auf jeder Serverknoten laden.  


<a name="examples-copy-table-bk"></a>

## <a name="examples-for-copying-a-table"></a>Beispiele für das Kopieren einer Tabelle

<a name="ctas-copy-table-bk"></a>

### <a name="a-use-ctas-to-copy-a-table"></a>A. Verwenden Sie CTAS, um eine Tabelle kopieren 
Gilt für: Azure SQL Datawarehouse und Parallel Datawarehouse

Vielleicht eine der am häufigsten verwendeten verwendet der `CTAS` ist das Erstellen einer Kopie einer Tabelle, damit Sie die DDL-Anweisungen ändern können. Wenn z. B. ursprünglich die Tabelle als erstellt `ROUND_ROBIN` und jetzt möchten, ändern Sie ihn in eine Tabelle, die auf eine Spalte verteilt `CTAS` ist, wie Sie die verteilungsspalte ändern würde. `CTAS`kann auch so ändern Sie die Partitionierung, Indizierung oder Spalte Typen verwendet werden.

Nehmen wir an diese Tabelle mit den Standardtyp für die Verteilung der Erstellung `ROUND_ROBIN` verteilt werden, da keine verteilungsspalte, in angegeben wurde der `CREATE TABLE`.

```sql
CREATE TABLE FactInternetSales
(
    ProductKey int NOT NULL,
    OrderDateKey int NOT NULL,
    DueDateKey int NOT NULL,
    ShipDateKey int NOT NULL,
    CustomerKey int NOT NULL,
    PromotionKey int NOT NULL,
    CurrencyKey int NOT NULL,
    SalesTerritoryKey int NOT NULL,
    SalesOrderNumber nvarchar(20) NOT NULL,
    SalesOrderLineNumber tinyint NOT NULL,
    RevisionNumber tinyint NOT NULL,
    OrderQuantity smallint NOT NULL,
    UnitPrice money NOT NULL,
    ExtendedAmount money NOT NULL,
    UnitPriceDiscountPct float NOT NULL,
    DiscountAmount float NOT NULL,
    ProductStandardCost money NOT NULL,
    TotalProductCost money NOT NULL,
    SalesAmount money NOT NULL,
    TaxAmt money NOT NULL,
    Freight money NOT NULL,
    CarrierTrackingNumber nvarchar(25),
    CustomerPONumber nvarchar(25)
);
```

Nun möchten Sie eine neue Kopie dieser Tabelle mit einem gruppierten columnstore-Index zu erstellen, sodass Sie die Leistung von gruppierten columnstore-Tabellen nutzen können. Außerdem soll in der Tabelle auf "ProductKey" verteilt werden, da Sie von Joins für diese Spalte vorhersehen und Verschieben von Daten während des Joins auf "ProductKey" vermeiden möchten. Abschließend möchten auch Partitionierung für OrderDateKey, sodass Sie schnell alte Daten löschen können, durch das Löschen der ALTER Partitionen hinzufügen. Hier ist die CTAS-Anweisung, die die alten Tabelle in eine neue Tabelle kopieren möchten.

```sql
CREATE TABLE FactInternetSales_new
WITH
(
    CLUSTERED COLUMNSTORE INDEX,
    DISTRIBUTION = HASH(ProductKey),
    PARTITION
    (
        OrderDateKey RANGE RIGHT FOR VALUES
        (
        20000101,20010101,20020101,20030101,20040101,20050101,20060101,20070101,20080101,20090101,
        20100101,20110101,20120101,20130101,20140101,20150101,20160101,20170101,20180101,20190101,
        20200101,20210101,20220101,20230101,20240101,20250101,20260101,20270101,20280101,20290101
        )
    )
)
AS SELECT * FROM FactInternetSales;
```

Schließlich können Sie die Tabellen aus, um den Austausch in der neuen Tabelle aus, und löschen die alte Tabelle umbenennen.

```sql
RENAME OBJECT FactInternetSales TO FactInternetSales_old;
RENAME OBJECT FactInternetSales_new TO FactInternetSales;

DROP TABLE FactInternetSales_old;
```

<a name="examples-column-bk"></a>

## <a name="examples-for-column-options"></a>Beispiele für Spaltenoptionen

<a name="ctas-change-column-attributes-bk"></a>

### <a name="b-use-ctas-to-change-column-attributes"></a>B. Verwenden Sie so ändern Sie die Spaltenattribute CTAS 
Gilt für: Azure SQL Datawarehouse und Parallel Datawarehouse

Dieses Beispiel verwendet die CTAS-Datentypen, die NULL-Zulässigkeit und die Sortierung für mehrere Spalten in der Tabelle DimCustomer2 ändern.  
  
```  
-- Original table 
CREATE TABLE [dbo].[DimCustomer2] (  
    [CustomerKey] int NOT NULL,  
    [GeographyKey] int NULL,  
    [CustomerAlternateKey] nvarchar(15) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL  
)  
WITH (CLUSTERED COLUMNSTORE INDEX, DISTRIBUTION = HASH([CustomerKey]));  
  
-- CTAS example to change data types, nullability, and column collations  
CREATE TABLE test  
WITH (HEAP, DISTRIBUTION = ROUND_ROBIN)  
AS  
SELECT  
    CustomerKey AS CustomerKeyNoChange,  
    CustomerKey*1 AS CustomerKeyChangeNullable,  
    CAST(CustomerKey AS DECIMAL(10,2)) AS CustomerKeyChangeDataTypeNullable,  
    ISNULL(CAST(CustomerKey AS DECIMAL(10,2)),0) AS CustomerKeyChangeDataTypeNotNullable,  
    GeographyKey AS GeographyKeyNoChange,  
    ISNULL(GeographyKey,0) AS GeographyKeyChangeNotNullable,  
    CustomerAlternateKey AS CustomerAlternateKeyNoChange,  
    CASE WHEN CustomerAlternateKey = CustomerAlternateKey 
        THEN CustomerAlternateKey END AS CustomerAlternateKeyNullable,  
    CustomerAlternateKey COLLATE Latin1_General_CS_AS_KS_WS AS CustomerAlternateKeyChangeCollation  
FROM [dbo].[DimCustomer2]  
  
-- Resulting table 
CREATE TABLE [dbo].[test] (
    [CustomerKeyNoChange] int NOT NULL, 
    [CustomerKeyChangeNullable] int NULL, 
    [CustomerKeyChangeDataTypeNullable] decimal(10, 2) NULL, 
    [CustomerKeyChangeDataTypeNotNullable] decimal(10, 2) NOT NULL, 
    [GeographyKeyNoChange] int NULL, 
    [GeographyKeyChangeNotNullable] int NOT NULL, 
    [CustomerAlternateKeyNoChange] nvarchar(15) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL, 
    [CustomerAlternateKeyNullable] nvarchar(15) COLLATE SQL_Latin1_General_CP1_CI_AS NULL, 
    [CustomerAlternateKeyChangeCollation] nvarchar(15) COLLATE Latin1_General_CS_AS_KS_WS NOT NULL
)
WITH (DISTRIBUTION = ROUND_ROBIN);
```
 
Als letzten Schritt können Sie [&#40; umbenennen Transact-SQL &#41; ](../../t-sql/statements/rename-transact-sql.md) um den Tabellennamen zu wechseln. Auf diese Weise werden die neue Tabelle DimCustomer2.

```
RENAME OBJECT DimCustomer2 TO DimCustomer2_old;
RENAME OBJECT test TO DimCustomer2;

DROP TABLE DimCustomer2_old;
```

<a name="examples-table-distribution-bk"></a>

## <a name="examples-for-table-distribution"></a>Beispiele für die Verteilung der Tabelle

<a name="ctas-change-distribution-method-bk"></a>

### <a name="c-use-ctas-to-change-the-distribution-method-for-a-table"></a>C. Verwenden Sie CTAS, um die Verteilungsmethode für eine Tabelle zu ändern
Gilt für: Azure SQL Datawarehouse und Parallel Datawarehouse

Dieses einfache Beispiel zeigt, wie die Verteilungsmethode für eine Tabelle zu ändern. Um die Funktionsweise der hierzu anzuzeigen, eine Tabelle mit Hash distributed Roundrobin-ändert und anschließend wieder in Hash verteilt die Roundrobin-Tabelle geändert. Die endgültige Tabelle entspricht die ursprüngliche Tabelle. 

In den meisten Fällen müssen Sie wird keine Hash-distributed-Tabelle in eine Roundrobin-Tabelle zu ändern. Je öfter, müssen Sie eine Roundrobin-Tabelle in einer verteilten Hashtabelle zu ändern. Z. B. möglicherweise Sie zunächst eine neue Tabelle als Round-Robin-Prinzip laden und dann später zu einer Tabelle Hash distributed abzurufenden Leistungssteigerung Join verschieben.

Dieses Beispiel verwendet die AdventureWorksDW-Beispieldatenbank. Um die SQL Data Warehouse-Version zu laden, verwenden Sie [Laden Sie Beispieldaten in SQL Data Warehouse](https://azure.microsoft.com/documentation/articles/sql-data-warehouse-load-sample-databases/)
 
```
-- DimSalesTerritory is hash-distributed.
-- Copy it to a round-robin table.
CREATE TABLE [dbo].[myTable]   
WITH   
  (   
    CLUSTERED COLUMNSTORE INDEX,  
    DISTRIBUTION = ROUND_ROBIN  
  )  
AS SELECT * FROM [dbo].[DimSalesTerritory]; 

-- Switch table names

RENAME OBJECT [dbo].[DimSalesTerritory] to [DimSalesTerritory_old];
RENAME OBJECT [dbo].[myTable] TO [DimSalesTerritory];

DROP TABLE [dbo].[DimSalesTerritory_old];

```  
Als Nächstes ändern Sie ihn wieder zu einer verteilten Hashtabelle.

```
-- You just made DimSalesTerritory a round-robin table.
-- Change it back to the original hash-distributed table. 
CREATE TABLE [dbo].[myTable]   
WITH   
  (   
    CLUSTERED COLUMNSTORE INDEX,  
    DISTRIBUTION = HASH(SalesTerritoryKey) 
  )  
AS SELECT * FROM [dbo].[DimSalesTerritory]; 

-- Switch table names

RENAME OBJECT [dbo].[DimSalesTerritory] to [DimSalesTerritory_old];
RENAME OBJECT [dbo].[myTable] TO [DimSalesTerritory];

DROP TABLE [dbo].[DimSalesTerritory_old];
```
 
<a name="ctas-change-to-replicated-bk"></a>

### <a name="d-use-ctas-to-convert-a-table-to-a-replicated-table"></a>D. Verwenden Sie CTAS, um eine Tabelle in einer replizierten Tabelle konvertieren  
Gilt für: Azure SQL Datawarehouse und Parallel Datawarehouse 

In diesem Beispiel gilt für das Konvertieren von Roundrobin-Verfahren oder Hash verteilte Tabellen in einer replizierten Tabelle. In diesem Beispiel wird der vorherigen Methode zum Ändern der Verteilung Typ einen Schritt weiter.  Da DimSalesTerritory einer Dimension und wahrscheinlich auf eine kleinere Tabelle ist, können Sie auswählen, um die Tabelle neu zu erstellen, als zum Verschieben von Daten zu vermeiden, bei der Verknüpfung mit anderen Tabellen repliziert. 

```
-- DimSalesTerritory is hash-distributed.
-- Copy it to a replicated table.
CREATE TABLE [dbo].[myTable]   
WITH   
  (   
    CLUSTERED COLUMNSTORE INDEX,  
    DISTRIBUTION = REPLICATE 
  )  
AS SELECT * FROM [dbo].[DimSalesTerritory]; 

-- Switch table names

RENAME OBJECT [dbo].[DimSalesTerritory] to [DimSalesTerritory_old];
RENAME OBJECT [dbo].[myTable] TO [DimSalesTerritory];

DROP TABLE [dbo].[DimSalesTerritory_old];
```
 
### <a name="e-use-ctas-to-create-a-table-with-fewer-columns"></a>E. Verwenden Sie zum Erstellen einer Tabelle mit weniger Spalten CTAS
Gilt für: Azure SQL Datawarehouse und Parallel Datawarehouse 

Das folgende Beispiel erstellt eine verteilte Round-Robin-Tabelle namens `myTable (c, ln)`. Die neue Tabelle hat nur zwei Spalten. Die Spaltenaliase verwendet für die Namen der Spalten in der SELECT-Anweisung.  
  
```  
CREATE TABLE myTable  
WITH   
  (   
    CLUSTERED COLUMNSTORE INDEX,  
    DISTRIBUTION = ROUND_ROBIN  
  )  
AS SELECT CustomerKey AS c, LastName AS ln  
    FROM dimCustomer;  
  
```  

<a name="examples-query-hints-bk"></a>

## <a name="examples-for-query-hints"></a>Beispiele für Abfragehinweise

<a name="ctas-query-hint-bk"></a>

### <a name="f-use-a-query-hint-with-create-table-as-select-ctas"></a>F. Verwenden mit CREATE für Tabelle als Abfragehinweis auswählen (CTAS)  
Gilt für: Azure SQL Datawarehouse und Parallel Datawarehouse
  
Diese Abfrage zeigt die grundlegende Syntax für die Verwendung eines Join-Abfragehinweis mit der CTAS-Anweisung. Nachdem die Abfrage gesendet wird, [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] gilt die Hash-Join-Strategie beim Generieren des Abfrageplans für jede einzelne Verteilung. Weitere Informationen zu den Hash Join-Abfragehinweis, finden Sie unter [OPTION-Klausel &#40; Transact-SQL &#41; ](../../t-sql/queries/option-clause-transact-sql.md).  
  
```  
CREATE TABLE dbo.FactInternetSalesNew  
WITH   
  (   
    CLUSTERED COLUMNSTORE INDEX,  
    DISTRIBUTION = ROUND_ROBIN   
  )  
AS SELECT T1.* FROM dbo.FactInternetSales T1 JOIN dbo.DimCustomer T2  
ON ( T1.CustomerKey = T2.CustomerKey )  
OPTION ( HASH JOIN );  
```  

<a name="examples-external-tables"></a>

## <a name="examples-for-external-tables"></a>Beispiele für externe Tabellen

<a name="ctas-azure-blob-storage-bk"></a>

### <a name="g-use-ctas-to-import-data-from-azure-blob-storage"></a>G. Verwenden Sie zum Importieren von Daten aus dem Azure-Blob-Speicher CTAS  
Gilt für: Azure SQL Datawarehouse und Parallel Datawarehouse  

Zum Importieren von Daten aus einer externen Tabelle einfach mit der CREATE TABLE AS SELECT in der externen Tabelle auswählen. Die Syntax zum Auswählen von Daten aus einer externen Tabelle in [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] ist identisch mit der Syntax zum Auswählen von Daten aus einer regulären Tabelle.  
  
 Das folgende Beispiel definiert eine externe Tabelle, auf Daten in einem Azure Blob Storage-Konto. Er verwendet dann CREATE TABLE AS SELECT in der externen Tabelle auswählen. Dadurch werden die Daten aus Azure-Blob-Speicher Texttrennzeichen Dateien importiert und speichert die Daten in eine neue [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] Tabelle.  
  
```  
--Use your own processes to create the text-delimited files on Azure blob storage.  
--Create the external table called ClickStream.  
CREATE EXTERNAL TABLE ClickStreamExt (   
    url varchar(50),  
    event_date date,  
    user_IP varchar(50)  
)  
WITH (  
    LOCATION='/logs/clickstream/2015/',  
    DATA_SOURCE = MyAzureStorage,  
    FILE_FORMAT = TextFileFormat)  
;  
  
--Use CREATE TABLE AS SELECT to import the Azure blob storage data into a new   
--SQL Data Warehouse table called ClickStreamData  
CREATE TABLE ClickStreamData   
WITH  
  (  
    CLUSTERED COLUMNSTORE INDEX,  
    DISTRIBUTION = HASH (user_IP)  
  )  
AS SELECT * FROM ClickStreamExt  
;  
```  

<a name="ctas-import-Hadoop-bk"></a>
  
### <a name="h-use-ctas-to-import-hadoop-data-from-an-external-table"></a>H. Verwenden Sie zum Importieren von Hadoop-Daten aus einer externen Tabelle CTAS  
Gilt für:[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
Zum Importieren von Daten aus einer externen Tabelle einfach mit der CREATE TABLE AS SELECT in der externen Tabelle auswählen. Die Syntax zum Auswählen von Daten aus einer externen Tabelle in [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] ist identisch mit der Syntax zum Auswählen von Daten aus einer regulären Tabelle.  
  
 Das folgende Beispiel definiert eine externe Tabelle in einem Hadoop-Cluster. Er verwendet dann CREATE TABLE AS SELECT in der externen Tabelle auswählen. Dadurch werden die Daten aus Hadoop Texttrennzeichen Dateien importiert und speichert die Daten in eine neue [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] Tabelle.  
  
```  
-- Create the external table called ClickStream.  
CREATE EXTERNAL TABLE ClickStreamExt (   
    url varchar(50),  
    event_date date,  
    user_IP varchar(50)  
)  
WITH (  
    LOCATION = 'hdfs://MyHadoop:5000/tpch1GB/employee.tbl',  
    FORMAT_OPTIONS ( FIELD_TERMINATOR = '|')  
)  
;  
  
-- Use your own processes to create the Hadoop text-delimited files 
-- on the Hadoop Cluster.  
  
-- Use CREATE TABLE AS SELECT to import the Hadoop data into a new 
-- table called ClickStreamPDW  
CREATE TABLE ClickStreamPDW   
WITH  
  (  
    CLUSTERED COLUMNSTORE INDEX,  
    DISTRIBUTION = HASH (user_IP)  
  )  
AS SELECT * FROM ClickStreamExt  
;   
```  
 
<a name="examples-workarounds-bk"></a>
 
## <a name="examples-using-ctas-to-replace-sql-server-code"></a>Beispiele für die Verwendung von CTAS zum Ersetzen des SQL Server

Verwenden Sie CTAS, um einige nicht unterstützten Funktionen umgehen. Der Code für das Datawarehouse ausgeführt, sondern verbessert umschreiben vorhandener Code, um CTAS in der Regel Leistung. Dies ist das Ergebnis von dem vollständig parallelisierte Entwurf. 

> [!NOTE]
> Denken Sie daran "CTAS erste". Wenn Sie vermuten, Sie lösen können dass, ein Problem mit `CTAS` , die ist, in der Regel die beste Methode für die - Vorgehensweise selbst wenn Sie daher mehr Daten schreiben.
>

<a name="ctas-replace-select-into-bk"></a>

### <a name="i-use-ctas-instead-of-selectinto"></a>I. Verwenden Sie CTAS anstelle von SELECT... IN  
Gilt für: Azure SQL Datawarehouse und Parallel Datawarehouse

SQL Server-Code verwendet in der Regel auswählen... INTO zum Auffüllen einer Tabelle mit den Ergebnissen einer SELECT-Anweisung. Dies ist ein Beispiel für eine SQL Server-SELECT... INTO-Anweisung.

```sql
SELECT *
INTO    #tmp_fct
FROM    [dbo].[FactInternetSales]
```

Diese Syntax wird in SQL Data Warehouse und Parallel Data Warehouse nicht unterstützt. Dieses Beispiel zeigt, wie die vorherige SELECT-Anweisung zu schreiben... INTO-Anweisung als CTAS-Anweisung. Sie können eine der Optionen für die Verteilung in der CTAS-Syntax beschrieben. Dieses Beispiel verwendet die Verteilungsmethode ROUND_ROBIN.

```sql
CREATE TABLE #tmp_fct
WITH
(
    DISTRIBUTION = ROUND_ROBIN
)
AS
SELECT  *
FROM    [dbo].[FactInternetSales]
;
```

<a name="ctas-replace-implicit-joins-bk"></a>

### <a name="j-use-ctas-and-implicit-joins-to-replace-ansi-joins-in-the-from-clause-of-an-update-statement"></a>J. Verwenden Sie zum Ersetzen von ANSI-Joins in CTAS und impliziten Joins der `FROM` -Klausel eine `UPDATE` Anweisung  
Gilt für: Azure SQL Datawarehouse und Parallel Datawarehouse  

Sie können möglicherweise, dass Sie ein komplexes Update verfügen, das mehr als zwei Tabellen, die zusammen mit ANSI-Syntax verknüpfen die Update- oder DELETE ausführen verknüpft.

Stellen Sie sich vor, dass mussten Sie diese Tabelle zu aktualisieren:

```sql
CREATE TABLE [dbo].[AnnualCategorySales]
(   [EnglishProductCategoryName]    NVARCHAR(50)    NOT NULL
,   [CalendarYear]                  SMALLINT        NOT NULL
,   [TotalSalesAmount]              MONEY           NOT NULL
)
WITH
(
    DISTRIBUTION = ROUND_ROBIN
)
;
```

Die ursprüngliche Abfrage könnte etwa so aussehen besprochen haben:

```sql
UPDATE  acs
SET     [TotalSalesAmount] = [fis].[TotalSalesAmount]
FROM    [dbo].[AnnualCategorySales]     AS acs
JOIN    (
        SELECT  [EnglishProductCategoryName]
        ,       [CalendarYear]
        ,       SUM([SalesAmount])              AS [TotalSalesAmount]
        FROM    [dbo].[FactInternetSales]       AS s
        JOIN    [dbo].[DimDate]                 AS d    ON s.[OrderDateKey]             = d.[DateKey]
        JOIN    [dbo].[DimProduct]              AS p    ON s.[ProductKey]               = p.[ProductKey]
        JOIN    [dbo].[DimProductSubCategory]   AS u    ON p.[ProductSubcategoryKey]    = u.[ProductSubcategoryKey]
        JOIN    [dbo].[DimProductCategory]      AS c    ON u.[ProductCategoryKey]       = c.[ProductCategoryKey]
        WHERE   [CalendarYear] = 2004
        GROUP BY
                [EnglishProductCategoryName]
        ,       [CalendarYear]
        ) AS fis
ON  [acs].[EnglishProductCategoryName]  = [fis].[EnglishProductCategoryName]
AND [acs].[CalendarYear]                = [fis].[CalendarYear]
;
```

Da SQL Data Warehouse nicht unterstützt ANSI-joins in der `FROM` -Klausel eine `UPDATE` -Anweisung können nicht Sie dieser SQL Server-Code über verwenden, ohne ihn leicht ändern.

Sie können eine Kombination aus einer `CTAS` und eines impliziten Joins mit diesem Code ersetzen:

```sql
-- Create an interim table
CREATE TABLE CTAS_acs
WITH (DISTRIBUTION = ROUND_ROBIN)
AS
SELECT  ISNULL(CAST([EnglishProductCategoryName] AS NVARCHAR(50)),0)    AS [EnglishProductCategoryName]
,       ISNULL(CAST([CalendarYear] AS SMALLINT),0)                      AS [CalendarYear]
,       ISNULL(CAST(SUM([SalesAmount]) AS MONEY),0)                     AS [TotalSalesAmount]
FROM    [dbo].[FactInternetSales]       AS s
JOIN    [dbo].[DimDate]                 AS d    ON s.[OrderDateKey]             = d.[DateKey]
JOIN    [dbo].[DimProduct]              AS p    ON s.[ProductKey]               = p.[ProductKey]
JOIN    [dbo].[DimProductSubCategory]   AS u    ON p.[ProductSubcategoryKey]    = u.[ProductSubcategoryKey]
JOIN    [dbo].[DimProductCategory]      AS c    ON u.[ProductCategoryKey]       = c.[ProductCategoryKey]
WHERE   [CalendarYear] = 2004
GROUP BY
        [EnglishProductCategoryName]
,       [CalendarYear]
;

-- Use an implicit join to perform the update
UPDATE  AnnualCategorySales
SET     AnnualCategorySales.TotalSalesAmount = CTAS_ACS.TotalSalesAmount
FROM    CTAS_acs
WHERE   CTAS_acs.[EnglishProductCategoryName] = AnnualCategorySales.[EnglishProductCategoryName]
AND     CTAS_acs.[CalendarYear]               = AnnualCategorySales.[CalendarYear]
;

--Drop the interim table
DROP TABLE CTAS_acs
;
```

<a name="ctas-replace-ansi-joins-bk"></a>

### <a name="k-use-ctas-to-specify-which-data-to-keep-instead-of-using-ansi-joins-in-the-from-clause-of-a-delete-statement"></a>K. Verwenden Sie CTAS, um anzugeben, welche Daten behalten anstelle von ANSI in der FROM-Klausel einer DELETE-Anweisung verknüpft  
Gilt für: Azure SQL Datawarehouse und Parallel Datawarehouse  

Der beste Ansatz zum Löschen von Daten in einigen Fällen ist die Verwendung `CTAS`. Wählen Sie die Daten, die Sie beibehalten möchten, anstatt die Daten einfach löschen. Diese gilt insbesondere für `DELETE` Anweisungen, die Ansi verknüpfen Syntax verwenden, da SQL Data Warehouse nicht ANSI unterstützt, in verknüpft der `FROM` -Klausel eine `DELETE` Anweisung.

Ein Beispiel für eine konvertierte DELETE-Anweisung ist verfügbar unter:

```sql
CREATE TABLE dbo.DimProduct_upsert
WITH
(   Distribution=HASH(ProductKey)
,   CLUSTERED INDEX (ProductKey)
)
AS -- Select Data you wish to keep
SELECT     p.ProductKey
,          p.EnglishProductName
,          p.Color
FROM       dbo.DimProduct p
RIGHT JOIN dbo.stg_DimProduct s
ON         p.ProductKey = s.ProductKey
;

RENAME OBJECT dbo.DimProduct        TO DimProduct_old;
RENAME OBJECT dbo.DimProduct_upsert TO DimProduct;
```

<a name="ctas-simplify-merge-bk"></a>

### <a name="l-use-ctas-to-simplify-merge-statements"></a>L. Verwenden Sie CTAS zur Vereinfachung der Merge-Anweisungen  
Gilt für: Azure SQL Datawarehouse und Parallel Datawarehouse  

Merge-Anweisungen können ersetzt werden, mindestens im Webpart mit `CTAS`. Sie konsolidieren können die `INSERT` und `UPDATE` in einer einzigen Anweisung. Alle gelöschten Datensätze müssten deaktivieren, die in einer zweiten Anweisung geschlossen werden.

Ein Beispiel für eine `UPSERT` ist verfügbar unter:

```sql
CREATE TABLE dbo.[DimProduct_upsert]
WITH
(   DISTRIBUTION = HASH([ProductKey])
,   CLUSTERED INDEX ([ProductKey])
)
AS
-- New rows and new versions of rows
SELECT      s.[ProductKey]
,           s.[EnglishProductName]
,           s.[Color]
FROM      dbo.[stg_DimProduct] AS s
UNION ALL  
-- Keep rows that are not being touched
SELECT      p.[ProductKey]
,           p.[EnglishProductName]
,           p.[Color]
FROM      dbo.[DimProduct] AS p
WHERE NOT EXISTS
(   SELECT  *
    FROM    [dbo].[stg_DimProduct] s
    WHERE   s.[ProductKey] = p.[ProductKey]
)
;

RENAME OBJECT dbo.[DimProduct]          TO [DimProduct_old];
RENAME OBJECT dbo.[DimpProduct_upsert]  TO [DimProduct];

```

<a name="ctas-data-type-and-nullability-bk"></a>

### <a name="m-explicitly-state-data-type-and-nullability-of-output"></a>M. Datentyp und NULL-Zulässigkeit der Ausgabe explizit  
Gilt für: Azure SQL Datawarehouse und Parallel Datawarehouse  

Wenn SQL Server-Code zu SQL Data Warehouse zu migrieren, finden Sie möglicherweise, dass Sie über diese Art von Codierungsmuster ausgeführt werden:

```sql
DECLARE @d decimal(7,2) = 85.455
,       @f float(24)    = 85.455

CREATE TABLE result
(result DECIMAL(7,2) NOT NULL
)
WITH (DISTRIBUTION = ROUND_ROBIN)

INSERT INTO result
SELECT @d*@f
;
```

Sie können instinktiv vorstellen, Migrieren von dieser Code sollte in einer CTAS und Sie das richtige werden würde. Es ist jedoch ein ausgeblendetes Problem hier.

Der folgende Code ist nicht das gleiche Ergebnis erzielt:

```sql
DECLARE @d decimal(7,2) = 85.455
,       @f float(24)    = 85.455
;

CREATE TABLE ctas_r
WITH (DISTRIBUTION = ROUND_ROBIN)
AS
SELECT @d*@f as result
;
```

Beachten Sie, dass die Spalte "Ergebnis" Vorwärts die Datenwerte Type und NULL-Zulässigkeit des Ausdrucks führt. Dies kann auf geringfügige abweichungen in Werten führen, wenn Sie nicht sorgfältig sind.

Versuchen Sie Folgendes Beispiel:

```sql
SELECT result,result*@d
from result
;

SELECT result,result*@d
from ctas_r
;
```

Der Wert für das Ergebnis gespeichert ist unterschiedlich. Der beibehaltene Wert in der Ergebnisspalte in anderen Ausdrücken verwendet wird wird der Fehler sogar wichtiger.

![CREATE TABLE AS SELECT-Ergebnisse](../../t-sql/statements/media/create-table-as-select-results.png)

Dies ist besonders wichtig für die Datenmigration. Obwohl die zweite Abfrage wohl genauere ist ein Problem vorliegt. Daten wären unterschiedlich im Vergleich zu dem Quellsystem und Fragen der Integrität der Migration führt. Dies ist eine von den seltenen Fällen, in denen die Antwort "falsche" tatsächlich richtig ist.

Der Grund, dass wir sehen, dass diese Abweichung zwischen den zwei Ergebnissen ist auf implizite Typumwandlung. Im ersten Beispiel definiert die Tabelle die Spaltendefinition. Tritt auf, eine implizite Konvertierung, wenn die Zeile eingefügt wird. Im zweiten Beispiel wird keine implizite Typumwandlung wie der Ausdruck den Datentyp der Spalte definiert. Beachten Sie außerdem, dass die Spalte im zweiten Beispiel während der im ersten Beispiel ist es nicht als eine NULL zulassende Spalte definiert wurde. Bei der Erstellung der Tabelle in der ersten Beispiel Spalte NULL-Zulässigkeit wurde explizit definiert. In der zweiten würde z. B. sie einfach auf den Ausdruck und standardmäßig dies angehalten wurde in der Definition eines NULL.  

Zum Beheben dieser Probleme müssen Sie explizit die typkonvertierung und NULL-Zulässigkeit in Festlegen der `SELECT` Teil der `CTAS` Anweisung. Diese Eigenschaften können nicht in den Bereich der erstellen-Tabelle festgelegt werden.

Im folgenden Beispiel wird veranschaulicht, wie den Code diesen Fehler beheben:

```sql
DECLARE @d decimal(7,2) = 85.455
,       @f float(24)    = 85.455

CREATE TABLE ctas_r
WITH (DISTRIBUTION = ROUND_ROBIN)
AS
SELECT ISNULL(CAST(@d*@f AS DECIMAL(7,2)),0) as result
```

Beachten Sie Folgendes:
- CAST oder CONVERT konnte verwendet wurden
- ISNULL wird verwendet, um NULL-Zulässigkeit nicht COALESCE erzwingen
- ISNULL ist die äußerste Funktion
- Der zweite Teil der ISNULL ist eine Konstante d. h. 0

> [!NOTE]
> Für die NULL-Zulässigkeit ordnungsgemäß festzulegenden ist ausschlaggebend, verwenden Sie `ISNULL` und nicht `COALESCE`. `COALESCE`ist keine deterministische Funktion und daher das Ergebnis des Ausdrucks ist immer NULL-Werte zulässt. `ISNULL`unterscheidet. Es ist deterministisch. Daher bei der zweite Teil der `ISNULL` -Funktion ist eine Konstante oder ein Literal wird der resultierende Wert nicht NULL.

Dieser Tipp eignet sich nicht nur zum Sicherstellen der Integrität von Berechnungen. Es ist auch wichtig für den partitionswechsel Tabelle. Stellen Sie sich vor, dass Sie diese Tabelle wie die Tatsache definiert haben:

```sql
CREATE TABLE [dbo].[Sales]
(
    [date]      INT     NOT NULL
,   [product]   INT     NOT NULL
,   [store]     INT     NOT NULL
,   [quantity]  INT     NOT NULL
,   [price]     MONEY   NOT NULL
,   [amount]    MONEY   NOT NULL
)
WITH
(   DISTRIBUTION = HASH([product])
,   PARTITION   (   [date] RANGE RIGHT FOR VALUES
                    (20000101,20010101,20020101
                    ,20030101,20040101,20050101
                    )
                )
)
;
```

Allerdings ist das Wertfeld berechneteter Ausdruck er nicht Teil der Quelldaten ist.

So erstellen Sie Ihre partitionierte Dataset dazu werden sollen:

```sql
CREATE TABLE [dbo].[Sales_in]
WITH    
(   DISTRIBUTION = HASH([product])
,   PARTITION   (   [date] RANGE RIGHT FOR VALUES
                    (20000101,20010101
                    )
                )
)
AS
SELECT
    [date]    
,   [product]
,   [store]
,   [quantity]
,   [price]   
,   [quantity]*[price]  AS [amount]
FROM [stg].[source]
OPTION (LABEL = 'CTAS : Partition IN table : Create')
;
```

Die Abfrage würde hervorragenden ausgeführt werden. Das Problem tritt beim Versuch der partitionswechsel ausführen. Die Tabellendefinitionen stimmen nicht überein. Um die Tabellendefinitionen entsprechen den CTAS Stellen geändert werden müssen.

```sql
CREATE TABLE [dbo].[Sales_in]
WITH    
(   DISTRIBUTION = HASH([product])
,   PARTITION   (   [date] RANGE RIGHT FOR VALUES
                    (20000101,20010101
                    )
                )
)
AS
SELECT
    [date]    
,   [product]
,   [store]
,   [quantity]
,   [price]   
,   ISNULL(CAST([quantity]*[price] AS MONEY),0) AS [amount]
FROM [stg].[source]
OPTION (LABEL = 'CTAS : Partition IN table : Create');
```

Sie können daher sehen, dass typkonsistenz und Verwalten von NULL-Zulässigkeit Eigenschaften auf einer CTAS gute engineering empfohlen. Sie können Sie um in Ihren Berechnungen Integrität zu wahren und stellt zudem sicher, dass der partitionswechsel möglich ist.
 
## <a name="see-also"></a>Siehe auch  
 [CREATE EXTERNAL DATA SOURCE &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-data-source-transact-sql.md)   
 [CREATE EXTERNAL FILE FORMAT &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-file-format-transact-sql.md)   
 [CREATE EXTERNAL TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-table-transact-sql.md)   
 [Erstellen Sie die externe Tabelle AS SELECT &#40; Transact-SQL &#41;](../../t-sql/statements/create-external-table-as-select-transact-sql.md)   
 [Erstellen von Tabellen &#40; Azure SQL Datawarehouse &#41; ](../../t-sql/statements/create-table-azure-sql-data-warehouse.md) [DROP TABLE &#40; Transact-SQL &#41;](../../t-sql/statements/drop-table-transact-sql.md)   
 [DROP EXTERNAL TABLE &#40; Transact-SQL &#41;](../../t-sql/statements/drop-external-table-transact-sql.md)   
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [ALTER EXTERNAL TABLE &#40; Transact-SQL &#41;](http://msdn.microsoft.com/library/4ae1b23c-67f6-41d0-b614-7a8de914d145)  
  
  




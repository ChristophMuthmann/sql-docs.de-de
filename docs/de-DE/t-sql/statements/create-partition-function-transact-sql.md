---
title: CREATE PARTITION FUNCTION (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 08/10/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- CREATE PARTITION FUNCTION
- PARTITION
- PARTITION FUNCTION
- PARTITION_FUNCTION_TSQL
- PARTITION_TSQL
- CREATE_PARTITION_FUNCTION_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- RANGE RIGHT partition functions
- RANGE LEFT partition functions
- partitioned indexes [SQL Server], functions
- functions [SQL Server], creating
- partition functions [SQL Server], creating
- partitioned tables [SQL Server], functions
- CREATE PARTITION FUNCTION statement
ms.assetid: 9dfe8b76-721e-42fd-81ae-14e22258c4f2
caps.latest.revision: 57
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 0e2cefd0e5687429603ad80c75ee3cb7fa321b51
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="create-partition-function-transact-sql"></a>CREATE PARTITION FUNCTION (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Erstellt eine Funktion in der aktuellen Datenbank, die Zeilen einer Tabelle oder eines Indexes Partitionen zuordnet. Dies erfolgt auf Grundlage der Werte einer angegebenen Spalte. Das Verwenden von CREATE PARTITION FUNCTION ist der erste Schritt beim Erstellen einer partitionierten Tabelle oder eines partitionierten Index. Eine Tabelle oder ein Index in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] kann maximal 15.000 Partitionen aufweisen.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
CREATE PARTITION FUNCTION partition_function_name ( input_parameter_type )  
AS RANGE [ LEFT | RIGHT ]   
FOR VALUES ( [ boundary_value [ ,...n ] ] )   
[ ; ]  
```  
  
## <a name="arguments"></a>Argumente  
 *partition_function_name*  
 Der Name der Partitionsfunktion. Partitionsfunktionsnamen müssen innerhalb der Datenbank eindeutig sein und den Regeln für [Bezeichner](../../relational-databases/databases/database-identifiers.md) entsprechen.  
  
 *input_parameter_type*  
 Der Datentyp der zum Partitionieren verwendeten Spalte. Als Partitionierungsspalte sind alle Datentypen außer **text**, **ntext**, **image**, **xml**, **timestamp**, **varchar(max)**, **nvarchar(max)**, **varbinary(max)**, Aliasdatentypen oder CLR-benutzerdefinierten Datentypen, zulässig.  
  
 Die eigentliche Spalte, Partitionierungsspalte genannt, wird in der CREATE TABLE- oder CREATE INDEX-Anweisung angegeben.  
  
 *boundary_value*  
 Gibt die Grenzwerte für jede Partition einer partitionierten Tabelle oder eines partitionierten Index an, die bzw. der *partition_function_name* verwendet. Wenn *boundary_value* leer bleibt, ordnet die Partitionsfunktion die gesamte Tabelle oder den gesamten Index mithilfe von *partition_function_name* einer Partition zu. Nur eine einzige, in einer CREATE TABLE- oder CREATE INDEX-Anweisung angegebene Partitionierungsspalte kann verwendet werden.  
  
 *boundary_value* ist ein konstanter Ausdruck, der auf Variablen verweisen kann. Dazu gehören Variablen des benutzerdefinierten Typs oder Funktionen und benutzerdefinierte Funktionen. Er kann nicht auf [!INCLUDE[tsql](../../includes/tsql-md.md)]-Ausdrücke verweisen. *boundary_value* muss entweder mit dem in *input_parameter_type* enthaltenen Datentyp übereinstimmen oder implizit in diesen konvertiert werden. Während der impliziten Konvertierung kann der Wert nicht so abgeschnitten werden, dass dessen Größe und Dezimalstellen mit denen des entsprechenden *input_parameter_type*-Werts nicht übereinstimmen.  
  
> [!NOTE]  
>  Wenn *boundary_value* aus den Literalen **datetime** oder **smalldatetime** besteht, werden diese Literale ausgewertet, wobei angenommen wird, dass us_english die Sitzungssprache darstellt. Dieses Verhalten ist als veraltet markiert. Wenn Sie sicherstellen möchten, dass sich die Definition der Partitionsfunktion für alle Sitzungssprachen wie erwartet verhält, wird empfohlen, dass Sie die Konstanten verwenden, die für alle Sprachen gleich interpretiert werden, z. B. das Format yyyymmdd, oder dass Sie die Literale explizit in ein bestimmtes Format konvertieren. Führen Sie `SELECT @@LANGUAGE` aus, um die Sitzungssprache des Servers zu bestimmen.  
  
 *...n*  
 Gibt die Anzahl der von *boundary_value* bereitgestellten Werte an, wobei 14.999 nicht überschritten werden darf. Die Anzahl der erstellten Partitionen entspricht *n* + 1. Die Werte müssen nicht der Reihenfolge nach angegeben werden. Wenn die Werte nicht der Reihenfolge nach aufgeführt sind, werden sie von [!INCLUDE[ssDE](../../includes/ssde-md.md)] sortiert, die Funktion wird erstellt und eine Warnung zurückgegeben, die besagt, dass die Werte nicht der Reihenfolge nach bereitgestellt werden. Die Datenbank-Engine gibt einen Fehler zurück, wenn *n* doppelte Werte enthält.  
  
 **LEFT** | RIGHT  
 Gibt an, zu welcher Seite (links oder rechts) die einzelnen Grenzwertintervalle *boundary_value* [ **,***...n* ] gehören, wenn Intervallwerte von [!INCLUDE[ssDE](../../includes/ssde-md.md)] in aufsteigender Reihenfolge von links nach rechts sortiert werden. Fehlt die Angabe, ist LEFT der Standardwert.  
  
## <a name="remarks"></a>Remarks  
 Der Bereich einer Partitionsfunktion beschränkt sich auf die Datenbank, in der sie erstellt wird. Innerhalb der Datenbank befinden sich Partitionsfunktionen in einem von anderen Funktionen abgetrennten Namespace.  
  
 Jede Zeile, deren Partitionierungsspalte NULL-Werte enthält, wird in die Partition ganz links platziert, es sei denn, NULL wurde als Grenzwert angegeben, und RIGHT wird angezeigt. In diesem Fall ist die Partition ganz links eine leere Partition, und NULL-Werte werden in die sich anschließende Partition platziert.  
  
## <a name="permissions"></a>Berechtigungen  
 Jede der folgenden Berechtigungen kann zum Ausführen von CREATE PARTITION FUNCTION verwendet werden:  
  
-   ALTER ANY DATASPACE-Berechtigung. Diese Berechtigung gilt standardmäßig für Mitglieder der festen Serverrolle **sysadmin** und für Mitglieder der festen Datenbankrollen **db_owner** und **db_ddladmin** .  
  
-   CONTROL- oder ALTER-Berechtigung für die Datenbank, in der die Partitionsfunktion erstellt wird.  
  
-   CONTROL SERVER- oder ALTER ANY DATABASE-Berechtigung für die Datenbank, in der die Partitionsfunktion erstellt wird.  
  
##  <a name="BKMK_examples"></a> Beispiele  
  
### <a name="a-creating-a-range-left-partition-function-on-an-int-column"></a>A. Erstellen einer RANGE LEFT-Partitionsfunktion für eine int-Spalte  
 Mit der folgenden Partitionsfunktion wird eine Tabelle oder ein Index in vier Partitionen partitioniert.  
  
```sql  
CREATE PARTITION FUNCTION myRangePF1 (int)  
AS RANGE LEFT FOR VALUES (1, 100, 1000);  
```  
  
 In der folgenden Tabelle wird gezeigt, wie eine Tabelle, die diese Partitionsfunktion auf der Partitionierungsspalte **col1** verwendet, partitioniert würde.  
  
|Partition|1|2|3|4|  
|---------------|-------|-------|-------|-------|  
|**Werte**|**col1** <= `1`|**col1** > `1` AND **col1** <= `100`|**col1** > `100` AND **col1** <=`1000`|**col1** > `1000`|  
  
### <a name="b-creating-a-range-right-partition-function-on-an-int-column"></a>B. Erstellen einer RANGE RIGHT-Partitionsfunktion für eine int-Spalte  
 In der folgenden Partitionsfunktion werden dieselben Werte für *boundary_value* [ **,***...n* ] wie in der Partitionsfunktion im vorherigen Beispiel verwendet, mit dem Unterschied, dass RANGE RIGHT angegeben wird.  
  
```sql  
CREATE PARTITION FUNCTION myRangePF2 (int)  
AS RANGE RIGHT FOR VALUES (1, 100, 1000);  
```  
  
 In der folgenden Tabelle wird gezeigt, wie eine Tabelle, die diese Partitionsfunktion auf der Partitionierungsspalte **col1** verwendet, partitioniert würde.  
  
|Partition|1|2|3|4|  
|---------------|-------|-------|-------|-------|  
|**Werte**|**col1** \< `1`|**col1** >= `1` AND **col1** \< `100`|**col1** >= `100` AND **col1** \< `1000`|**col1** >= `1000`| 
  
### <a name="c-creating-a-range-right-partition-function-on-a-datetime-column"></a>C. Erstellen einer RANGE RIGHT-Partitionsfunktion für eine datetime-Spalte  
 Die folgende Partitionsfunktion partitioniert eine Tabelle oder einen Index in 12 Partitionen, d.h. eine für die Menge an Werten eines jeden Monats des Jahres in einer **datetime**-Spalte.  
  
```sql  
CREATE PARTITION FUNCTION [myDateRangePF1] (datetime)  
AS RANGE RIGHT FOR VALUES ('20030201', '20030301', '20030401',  
               '20030501', '20030601', '20030701', '20030801',   
               '20030901', '20031001', '20031101', '20031201');  
```  
  
 In der folgenden Tabelle wird dargestellt, wie eine Tabelle oder ein Index, die bzw. der diese Partitionsfunktion auf der **datecol**-Partitionierungsspalte verwendet, partitioniert wird.  
  
|Partition|1|2|...|11|12|  
|---------------|-------|-------|---------|--------|--------|  
|**Werte**|**datecol** \< `February 1, 2003`|**datecol** >= `February 1, 2003` AND **datecol** \< `March 1, 2003`||**datecol** >= `November 1, 2003` AND **col1** \< `December 1, 2003`|**datecol** >= `December 1, 2003`| 
  
### <a name="d-creating-a-partition-function-on-a-char-column"></a>D. Erstellen einer Partitionsfunktion für eine char-Spalte  
 Mit der folgenden Partitionsfunktion wird eine Tabelle oder ein Index in vier Partitionen partitioniert.  
  
```sql  
CREATE PARTITION FUNCTION myRangePF3 (char(20))  
AS RANGE RIGHT FOR VALUES ('EX', 'RXE', 'XR');  
```  
  
 In der folgenden Tabelle wird gezeigt, wie eine Tabelle, die diese Partitionsfunktion auf der Partitionierungsspalte **col1** verwendet, partitioniert würde.  
  
|Partition|1|2|3|4|  
|---------------|-------|-------|-------|-------|  
|**Werte**|**col1** \< `EX`...|**col1** >= `EX` AND **col1** \< `RXE`...|**col1** >= `RXE` AND **col1** \< `XR`...|**col1** >= `XR`| 
  
### <a name="e-creating-15000-partitions"></a>E. Erstellen von 15.000 Partitionen  
 Mit der folgenden Partitionsfunktion wird eine Tabelle oder ein Index in 15.000 Partitionen partitioniert.  
  
```sql  
--Create integer partition function for 15,000 partitions.  
DECLARE @IntegerPartitionFunction nvarchar(max) = 
    N'CREATE PARTITION FUNCTION IntegerPartitionFunction (int) 
    AS RANGE RIGHT FOR VALUES (';  
DECLARE @i int = 1;  
WHILE @i < 14999  
BEGIN  
SET @IntegerPartitionFunction += CAST(@i as nvarchar(10)) + N', ';  
SET @i += 1;  
END  
SET @IntegerPartitionFunction += CAST(@i as nvarchar(10)) + N');';  
EXEC sp_executesql @IntegerPartitionFunction;  
GO  
```  
  
### <a name="f-creating-partitions-for-multiple-years"></a>F. Erstellen von Partitionen für mehrere Jahre  
 Die folgende Partitionsfunktion partitioniert eine Tabelle oder einen Index in einer **datetime2**-Spalte in 50 Partitionen. Für jeden Monat zwischen Januar 2007 und Januar 2011 gibt es eine Partition.  
  
```sql  
--Create date partition function with increment by month.  
DECLARE @DatePartitionFunction nvarchar(max) = 
    N'CREATE PARTITION FUNCTION DatePartitionFunction (datetime2) 
    AS RANGE RIGHT FOR VALUES (';  
DECLARE @i datetime2 = '20070101';  
WHILE @i < '20110101'  
BEGIN  
SET @DatePartitionFunction += '''' + CAST(@i as nvarchar(10)) + '''' + N', ';  
SET @i = DATEADD(MM, 1, @i);  
END  
SET @DatePartitionFunction += '''' + CAST(@i as nvarchar(10))+ '''' + N');';  
EXEC sp_executesql @DatePartitionFunction;  
GO  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Partitionierte Tabellen und Indizes](../../relational-databases/partitions/partitioned-tables-and-indexes.md)   
 [$PARTITION &#40;Transact-SQL&#41;](../../t-sql/functions/partition-transact-sql.md)   
 [ALTER PARTITION FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-partition-function-transact-sql.md)   
 [DROP PARTITION FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/drop-partition-function-transact-sql.md)   
 [CREATE PARTITION SCHEME &#40;Transact-SQL&#41;](../../t-sql/statements/create-partition-scheme-transact-sql.md)   
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)   
 [ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [sys.partition_functions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-partition-functions-transact-sql.md)   
 [sys.partition_parameters &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-partition-parameters-transact-sql.md)   
 [sys.partition_range_values &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-partition-range-values-transact-sql.md)   
 [sys.partitions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-partitions-transact-sql.md)   
 [sys.tables &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-tables-transact-sql.md)   
 [sys.indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)   
 [sys.index_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-index-columns-transact-sql.md)  
  
  


---
title: CREATE TABLE (Azure SQL Data Warehouse) | Microsoft-Dokumentation
ms.custom: 
ms.date: 07/14/2017
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
ms.assetid: ea21c73c-40e8-4c54-83d4-46ca36b2cf73
caps.latest.revision: 
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: f6e639bf97ed132b6ace7128b4cbe9b6f3ce474e
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="create-table-azure-sql-data-warehouse"></a>CREATE TABLE (Azure SQL Data Warehouse)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Erstellt eine neue Tabelle in [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] oder [!INCLUDE[ssPDW](../../includes/sspdw-md.md)].  
 
Informationen zu Tabellen und deren Verwendung finden Sie unter [Einführung in das Entwerfen von Tabellen in Azure SQL Data Warehouse](https://azure.microsoft.com/documentation/articles/sql-data-warehouse-tables-overview/).

HINWEIS: Sofern nicht anders angegeben, beziehen sich die Beschreibungen von SQL Data Warehouse in diesem Artikel sowohl auf SQL Data Warehouse als auch auf Parallel Data Warehouse. 
 
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  

<a name="Syntax"></a>   
## <a name="syntax"></a>Syntax  
  
```  
-- Create a new table. 
CREATE TABLE [ database_name . [ schema_name ] . | schema_name. ] table_name   
    ( 
      { column_name <data_type>  [ <column_options> ] } [ ,...n ]   
    )  
    [ WITH [ <table_option> [ ,...n ] ) ]  
[;]  
   
<column_options> ::=
    [ COLLATE Windows_collation_name ]  
    [ NULL | NOT NULL ] -- default is NULL  
    [ [ CONSTRAINT constraint_name ] DEFAULT constant_expression  ]
  
<table_option> ::= 
    {   
        CLUSTERED COLUMNSTORE INDEX --default for SQL Data Warehouse 
      | HEAP --default for Parallel Data Warehouse   
      | CLUSTERED INDEX ( { index_column_name [ ASC | DESC ] } [ ,...n ] ) -- default is ASC 
    }  
    { 
        DISTRIBUTION = HASH ( distribution_column_name ) 
      | DISTRIBUTION = ROUND_ROBIN -- default for SQL Data Warehouse
      | DISTRIBUTION = REPLICATE -- default for Parallel Data Warehouse
    }   
    | PARTITION ( partition_column_name RANGE [ LEFT | RIGHT ] -- default is LEFT  
        FOR VALUES ( [ boundary_value [,...n] ] ) )  
  
<data type> ::=   
      datetimeoffset [ ( n ) ]  
    | datetime2 [ ( n ) ]  
    | datetime  
    | smalldatetime  
    | date  
    | time [ ( n ) ]  
    | float [ ( n ) ]  
    | real [ ( n ) ]  
    | decimal [ ( precision [ , scale ] ) ]   
    | numeric [ ( precision [ , scale ] ) ]   
    | money  
    | smallmoney  
    | bigint  
    | int   
    | smallint  
    | tinyint  
    | bit  
    | nvarchar [ ( n | max ) ]  -- max applies only to SQL Data Warehouse 
    | nchar [ ( n ) ]  
    | varchar [ ( n | max )  ] -- max applies only to SQL Data Warehouse  
    | char [ ( n ) ]  
    | varbinary [ ( n | max ) ] -- max applies only to SQL Data Warehouse  
    | binary [ ( n ) ]  
    | uniqueidentifier  
```  

<a name="Arguments"></a>   
## <a name="arguments"></a>Argumente  
 *database_name*  
 Der Name der Datenbank, die die neue Tabelle enthält. Gemäß Standardeinstellung die aktuelle Datenbank.  
  
 *schema_name*  
 Das Schema der Tabelle. Die Angabe von *schema* ist optional. Wenn keine Angabe gemacht wird, wird das Standardschema verwendet.  
  
 *table_name*  
 Der Name der neuen Tabelle. Stellen Sie dem Tabellennamen das Zeichen # voran, um eine temporäre lokale Tabelle zu erstellen.  Erläuterungen und einen Leitfaden zu temporären Tabellen finden Sie unter [Temporäre Tabellen in SQL Data Warehouse](https://azure.microsoft.com/documentation/articles/sql-data-warehouse-tables-temporary/). 
 
 *column_name*  
 Der Name einer Tabellenspalte.
   
### <a name="ColumnOptions"></a> Spaltenoptionen

 `COLLATE` *Windows_collation_name*  
 Gibt die Sortierung für den Ausdruck an. Bei der Sortierung muss es sich um eine von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] unterstützte Windows-Sortierung handeln. Eine Liste mit von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] unterstützten Windows-Sortierungen finden Sie unter [Name der Windows-Sortierung (Transact-SQL)](http://msdn.microsoft.com/library/ms188046\(v=sql11\)/).  
  
 `NULL` | `NOT NULL`  
 Gibt an, ob `NULL`-Werte in der Spalte zulässig sind. Der Standardwert ist `NULL`.  
  
 [ `CONSTRAINT` *constraint_name* ] `DEFAULT` *constant_expression*  
 Gibt den Standardspaltenwert an.  
  
 | Argument | Erklärung |
 | -------- | ----------- |
 | *constraint_name* | Der optionale Name für die Einschränkung. Der Einschränkungsname ist innerhalb der Datenbank eindeutig. Der Name kann in anderen Datenbanken wiederverwendet werden. |
 | *constant_expression* | Der Standardwert für die Spalte. Bei dem Ausdruck muss es sich um einen Literalwert oder um eine Konstante handeln. Folgende konstanten Ausdrücke sind beispielsweise zulässig: `'CA'`, `4`. Folgende Ausdrücke sind nicht zulässig: `2+3`, `CURRENT_TIMESTAMP`. |
  

### <a name="TableOptions"></a> Tabellenstrukturoptionen
Einen Leitfaden zum Auswählen des Tabellentyps finden Sie unter [Indizieren von Tabellen in SQL Data Warehouse](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-tables-index/).
  
 `CLUSTERED COLUMNSTORE INDEX`  
Speichert die Tabelle als gruppierten Columnstore-Index. Der gruppierte Columnstore-Index gilt für alle Tabellendaten. Dies ist die Standardeinstellung für [!INCLUDE[ssSDW](../../includes/sssdw-md.md)].   
 
 `HEAP`   
  Speichert die Tabelle als Heap. Dies ist die Standardeinstellung für [!INCLUDE[ssPDW](../../includes/sspdw-md.md)].  
  
 `CLUSTERED INDEX` ( *index_column_name* [ ,...*n* ] )  
 Speichert die Tabelle als gruppierten Index mit mindestens einer Schlüsselspalte. Damit werden die Daten zeilenweise gespeichert. Verwenden Sie *index_column_name*, um den Namen einer oder mehrerer Schlüsselspalten im Index anzugeben.  Weitere Informationen finden Sie im Abschnitt über Rowstore-Tabellen unter den allgemeinen Hinweisen.
 
 `LOCATION = USER_DB`   
 Diese Option ist veraltet. Sie ist syntaktisch zulässig, aber nicht mehr erforderlich und hat keine Auswirkungen auf das Verhalten.   
  
### <a name="TableDistributionOptions"></a> Tabellenverteilungsoptionen
Informationen zum Auswählen der besten Verteilungsmethode und zur Verwendung von verteilten Tabellen finden Sie unter [Leitfaden für das Entwerfen verteilter Tabellen in Azure SQL Data Warehouse](https://azure.microsoft.com/documentation/articles/sql-data-warehouse-tables-distribute/).

`DISTRIBUTION = HASH` ( *distribution_column_name* )   
Weist jede Zeile einer Verteilung zu, indem für den in *distribution_column_name* gespeicherten Wert ein Hashvorgang durchgeführt wird. Der Algorithmus ist deterministisch. Das bedeutet, er erzeugt für gleiche Verteilungen immer die gleichen Hashwerte.  Die Verteilungsspalte muss als NOT NULL definiert sein, da alle Zeilen, die NULL enthalten, derselben Verteilung zugewiesen werden.

`DISTRIBUTION = ROUND_ROBIN`   
Verteilt die Zeilen im Roundrobinverfahren gleichmäßig auf alle Verteilungen. Dies ist die Standardeinstellung für [!INCLUDE[ssSDW](../../includes/sssdw-md.md)].

`DISTRIBUTION = REPLICATE`    
Speichert in jedem Computeknoten eine Kopie der Tabelle. Bei [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] wird die Tabelle in einer Verteilungsdatenbank auf den einzelnen Computeknoten gespeichert. Bei [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] wird die Tabelle in einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Dateigruppe gespeichert, die sich über den gesamten Computeknoten erstreckt. Dies ist die Standardeinstellung für [!INCLUDE[ssPDW](../../includes/sspdw-md.md)].
  
### <a name="TablePartitionOptions"></a> Tabellenpartitionsoptionen
Einen Leitfaden zur Verwendung von Tabellenpartitionen finden Sie unter [Partitionieren von Tabellen in SQL Data Warehouse](https://azure.microsoft.com/documentation/articles/sql-data-warehouse-tables-partition/).

 `PARTITION` ( *partition_column_name* `RANGE` [ `LEFT` | `RIGHT` ] `FOR VALUES` ( [ *boundary_value* [,...*n*] ] ))   
Erstellt eine oder mehrere Tabellenpartitionen. Hierbei handelt es sich um horizontale Tabellenslices, mit deren Hilfe Sie Vorgänge für Teilmengen von Zeilen ausführen können, unabhängig davon, ob die Tabelle als Heap, gruppierter Index oder gruppierter Columnstore-Index gespeichert ist. Im Gegensatz zur Verteilungsspalte bestimmen Tabellenpartitionen nicht die Verteilung für den Speicherort der einzelnen Zeilen. Vielmehr bestimmten Tabellenpartitionen, wie die Zeilen in den einzelnen Verteilungen gruppiert und gespeichert werden.  
 
| Argument | Erklärung |
| -------- | ----------- |
|*partition_column_name*| Gibt die Spalte an, die von [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] zum Partitionieren der Zeilen verwendet wird. Diese Spalte kann einen beliebigen Datentyp aufweisen. [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] sortiert die Werte der Partitionsspalte in aufsteigender Reihenfolge. Die Sortierung vom niedrigsten zum höchsten Wert erfolgt zur Erfüllung der `RANGE`-Spezifikation von `LEFT` nach `RIGHT`. |  
| `RANGE LEFT` | Gibt den Begrenzungswert an, der zur Partition auf der linken Seite (niedrigere Werte) gehört. Die Standardeinstellung ist LEFT. |
| `RANGE RIGHT` | Gibt den Begrenzungswert an, der zur Partition auf der rechten Seite (höhere Werte) gehört. | 
| `FOR VALUES` ( *boundary_value* [,...*n*] ) | Gibt die Begrenzungswerte für die Partition an. *boundary_value* ist ein konstanter Ausdruck. Er darf nicht NULL sein. Er muss entweder dem Datentyp *partition_column_name* entsprechen oder implizit in diesen Datentyp konvertierbar sein. Er darf bei der impliziten Konvertierung nicht abgeschnitten werden, sodass die Größe und Dezimalstellen des Werts nicht mehr dem Datentyp von *partition_column_name* entsprechen.<br></br><br></br>Wenn Sie die `PARTITION`-Klausel, aber keinen Begrenzungswert angeben, erstellt [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] eine partitionierte Tabelle mit einer Partition. Ggf. können Sie die Tabelle später in zwei Partitionen teilen.<br></br><br></br>Wenn Sie einen Begrenzungswert angeben, weist die resultierende Tabelle zwei Partitionen auf, eine für die im Vergleich zum Begrenzungswert niedrigeren Werte und eine für die im Vergleich zum Begrenzungswert höheren Werte. Wenn Sie eine Partition in eine nicht partitionierte Tabelle verschieben, empfängt die nicht partitionierte Tabelle die Daten, jedoch sind in den Metadaten keine Partitionsbegrenzungen enthalten.| 
 
 Informationen hierzu finden Sie unter [Erstellen einer partitionierten Tabelle](#PartitionedTable) im Abschnitt mit den Beispielen.

### <a name="DataTypes"></a> Datentypen
[!INCLUDE[ssSDW](../../includes/sssdw-md.md)] unterstützt die am häufigsten verwendeten Datentypen. Im Folgenden finden Sie eine Liste der unterstützten Datentypen mit entsprechenden Informationen und Angaben zum Speicherplatz in Byte. Ausführlichere Informationen zu Datentypen und deren Verwendung finden Sie unter [Leitfaden zum Definieren von Datentypen für Tabellen in SQL Data Warehouse](https://azure.microsoft.com/documentation/articles/sql-data-warehouse-tables-data-types).

Eine Tabelle mit Datentypkonvertierungen finden Sie im Abschnitt über implizite Konvertierungen unter [CAST und CONVERT (Transact-SQL)](http://msdn.microsoft.com/library/ms187928/).

`datetimeoffset` [ ( *n* ) ]  
 Der Standardwert für *n* lautet 7.  
  
 `datetime2` [ ( *n* ) ]  
Entspricht `datetime`, jedoch mit der Ausnahme, dass die Anzahl von Sekundenbruchteilen angegeben werden kann. Der Standardwert für *n* lautet `7`.  
  
|*n*-Wert|Genauigkeit|Dezimalstellen|  
|--:|--:|-:|  
|`0`|19|0|  
|`1`|21|1|  
|`2`|22|2|  
|`3`|23|3|  
|`4`|24|4|  
|`5`|25|5|  
|`6`|26|6|  
|`7`|27|7|  
  
 `datetime`  
 Speichert das Datum und die Uhrzeit mit 19 bis 23 Zeichen entsprechend dem gregorianischen Kalender. Das Datum kann das Jahr, den Monat und den Tag enthalten. Die Uhrzeit enthält die Stunde, die Minute und die Sekunde. Optional können drei Ziffern für die Sekundenbruchteile angezeigt werden. Die Speichergröße beträgt 8 Byte.  
  
 `smalldatetime`  
 Speichert ein Datum und eine Uhrzeit. Die Speichergröße beträgt 4 Byte.  
  
 `date`  
 Speichert ein Datum mit maximal 10 Zeichen für das Jahr, den Monat und den Tag gemäß dem gregorianischen Kalender. Die Speichergröße beträgt 3 Byte. Das Datum wird als ganze Zahl gespeichert.  
  
 `time` [ ( *n* ) ]  
 Der Standardwert für *n* lautet `7`.  
  
 `float` [ ( *n* ) ]  
 Ungefähre Zahlendatentypen für numerische Gleitkommadaten. Gleitkommadaten sind Näherungswerte. Deshalb können nicht alle Werte im Bereich des Datentyps exakt dargestellt werden. *n* gibt die Anzahl der Bits zum Speichern der Mantisse von `float` in wissenschaftlicher Schreibweise an. Somit bestimmt *n* die Genauigkeit und die Speichergröße. Wenn *n* angegeben ist, muss es sich um einen Wert zwischen `1` und `53` handeln. Der Standardwert von *n* lautet `53`.  
  
| *n*-Wert | Genauigkeit | Speichergröße |  
| --------: | --------: | -----------: |  
| 1-24   | 7 Stellen  | 4 Byte      |  
| 25-53  | 15 Stellen | 8 Byte      |  
  
 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] verarbeitet *n* als einen von zwei möglichen Werten. Wenn `1`<= *n* <= `24`, wird *n* als `24` verarbeitet. Wenn `25` <= *n* <= `53`, wird *n* als `53` verarbeitet.  
  
 Der [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] `float`-Datentyp entspricht dem ISO-Standard für alle Werte von *n* zwischen `1` und `53`. Das Synonym für double precision lautet `float(53)`.  
  
 `real` [ ( *n* ) ]  
 Die Definition von „real“ entspricht der von „float“. Das ISO-Synonym für `real` ist `float(24)`.  
  
 `decimal` [ ( *precision* [ *, scale* ] ) ] | `numeric` [ ( *precision* [ *, scale* ] ) ]  
 Speichert Zahlen mit fester Genauigkeit und mit fester Anzahl von Dezimalstellen.  
  
 *precision*  
 Die maximal speicherbare Gesamtzahl an Dezimalstellen, sowohl links als auch rechts vom Dezimalkomma. Die Genauigkeit muss ein Wert zwischen `1` und der maximalen Genauigkeit von `38` sein. Die Standardgenauigkeit beträgt `18`.  
  
 *scale*  
 Die maximal speicherbare Zahl an Dezimalstellen rechts vom Dezimalkomma. *Scale* muss in einem Bereich zwischen `0` und *precision* liegen. *scale* kann nur angegeben werden, wenn *precision* angegeben wird. Der Standardwert lautet `0`; daher gilt: `0` <= *scale* <= *precision*. Die maximalen Speichergrößen variieren abhängig von der Genauigkeit.  
  
| Genauigkeit | Speicherplatz in Bytes  |  
| ---------: |-------------: |  
|  1-9       |             5 |  
| 10–19      |             9 |  
| 20–28      |            13 |  
| 29–38      |            17 |  
  
 `money` | `smallmoney`  
 Datentypen zur Darstellung von Währungswerten.  
  
| Datentyp | Speicherplatz in Bytes |  
| --------- | ------------: |  
| `money`|8|  
| `smallmoney` |4|  
  
 `bigint` | `int` | `smallint` | `tinyint`  
 Exakte Zahlendatentypen für ganzzahlige Daten. Der Speicherplatz wird wie in der folgenden Tabelle dargestellt.  
  
| Datentyp | Speicherplatz in Bytes |  
| --------- | ------------: |  
| `bigint`|8|  
| `int` |4|  
| `smallint` |2|  
| `tinyint` |1|  
  
 `bit`  
 Ein ganzzahliger Datentyp, der den Wert `1`, `0` oder NULL annehmen kann. [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] optimiert das Speichern von bit-Spalten. Wenn in einer Tabelle 8 oder weniger bit-Spalten vorhanden sind, werden die Spalten als 1 Byte gespeichert. Sind zwischen 9 und 16 bit-Spalten vorhanden, werden diese als 2 Byte gespeichert usw.  
  
 `nvarchar` [ ( *n* | `max` ) ]  -- `max` applies only to [!INCLUDE[ssSDW](../../includes/sssdw-md.md)].  
 Unicode-Daten variabler Länge. *n* muss ein Wert zwischen 1 und 4000 sein. `max` gibt an, dass die maximale Speichergröße 2^31-1 Byte (2 GB) beträgt. Die Speichergröße in Byte ist doppelt so groß wie die Anzahl eingegebener Zeichen + 2 Byte. Die eingegebenen Daten können 0 Zeichen lang sein.  
  
 `nchar` [ ( *n* ) ]  
 Unicode-Zeichendaten mit einer festen Länge von *n* Zeichen. *n* muss ein Wert zwischen `1` und `4000` sein. Die Speichergröße beträgt zweimal *n* Byte.  
  
 `varchar` [ ( *n*  | `max` ) ]  -- `max` applies only to [!INCLUDE[ssSDW](../../includes/sssdw-md.md)].   
 Nicht-Unicode-Zeichendaten mit einer variablen Länge von *n* Byte. *n* muss ein Wert zwischen `1` und `8000` sein. `max` gibt an, dass die maximale Speichergröße 2^31-1 Byte (2 GB) beträgt. Die Speichergröße ist die tatsächliche Länge der eingegebenen Daten + 2 Byte.  
  
 `char` [ ( *n* ) ]  
 Nicht-Unicode-Zeichendaten mit einer festen Länge von *n* Byte. *n* muss ein Wert zwischen `1` und `8000` sein. Die Speichergröße beträgt *n* Byte. Der Standardwert für *n* lautet `1`.  
  
 `varbinary` [ ( *n*  | `max` ) ]  -- `max` applies only to [!INCLUDE[ssSDW](../../includes/sssdw-md.md)].  
 Binärdaten mit variabler Länge. *n* kann ein Wert zwischen `1` und `8000` sein. `max` gibt an, dass die maximale Speichergröße 2^31-1 Byte (2 GB) beträgt. Die Speichergröße ist die tatsächliche Länge der eingegebenen Daten + 2 Byte. Der Standardwert für *n* lautet 7.  
  
 `binary` [ ( *n* ) ]  
 Binärdaten fester Länge mit einer Länge von *n* Byte. *n* kann ein Wert zwischen `1` und `8000` sein. Die Speichergröße beträgt *n* Byte. Der Standardwert für *n* lautet `7`.  
  
 `uniqueidentifier`  
 Ein 16-Byte-GUID.  
   
<a name="Permissions"></a>  
## <a name="permissions"></a>Berechtigungen  
 Zum Erstellen einer Tabelle sind Berechtigungen in der festen Datenbankrolle `db_ddladmin` oder folgende Berechtigungen erforderlich:
 - `CREATE TABLE`-Berechtigung für die Datenbank
 - `ALTER SCHEMA`-Berechtigung für das Schema, das die Tabelle enthält. 

Zum Erstellen einer partitionierten Tabelle sind Berechtigungen in der festen Datenbankrolle `db_ddladmin` oder folgende Berechtigungen erforderlich:

- `ALTER ANY DATASPACE`-Berechtigung
  
 Der Anmeldename, der eine lokale temporäre Tabelle erstellt, erhält die Berechtigungen `CONTROL`, `INSERT`, `SELECT` und `UPDATE` für die Tabelle.  
 
<a name="GeneralRemarks"></a>  
## <a name="general-remarks"></a>Allgemeine Hinweise  
 
Informationen zu Unter- und Obergrenzen finden Sie unter [Kapazitätsgrenzen von SQL Data Warehouse](https://azure.microsoft.com/documentation/articles/sql-data-warehouse-service-capacity-limits/). 
 
### <a name="determining-the-number-of-table-partitions"></a>Bestimmen der Anzahl der Tabellenpartitionen
Jede benutzerdefinierte Tabelle ist in mehrere kleinere Tabellen aufgeteilt, die in getrennten entfernten Speicherorten, so genannten Verteilungen, gespeichert sind. [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] verwendet 60 Verteilungen. Bei [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] hängt die Anzahl der Verteilungen von der Anzahl der Computeknoten ab.
 
Jede Verteilung enthält alle Tabellenpartitionen. Bei 60 Verteilungen und vier Tabellenpartitionen sind beispielsweise 320 Partitionen vorhanden. Wenn es sich bei der Tabelle um einen gruppierten Columnstore-Index handelt, gibt es einen Columnstore-Index pro Partition und somit 320 Columnstore-Indizes.

Es wird empfohlen, weniger Tabellenpartitionen zu verwenden, um sicherzustellen, dass jeder Columnstore-Index genügend Zeilen aufweist, um von den Vorteilen der Columnstore-Indizes zu profitieren. Weitere Informationen finden Sie unter [Partitionieren von Tabellen in SQL Data Warehouse](https://azure.microsoft.com/documentation/articles/sql-data-warehouse-tables-partition/) und [Indizieren von Tabellen in SQL Data Warehouse](https://azure.microsoft.com/en-us/documentation/articles/sql-data-warehouse-tables-index/).  

  
 ### <a name="rowstore-table-heap-or-clustered-index"></a>Rowstore-Tabelle (Heap oder gruppierter Index)  
 Eine Rowstore-Tabelle ist eine in zeilenweiser Reihenfolge gespeicherte Tabelle. Es handelt sich um einen Heap oder gruppierten Index. [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] erstellt alle Rowstore-Tabellen mit Seitenkomprimierung. Diese Einstellung kann vom Benutzer nicht konfiguriert werden.   
 
 ### <a name="columnstore-table-columnstore-index"></a>Columnstore-Tabelle (Columnstore Index)
Eine Columnstore-Tabelle ist eine in spaltenweiser Reihenfolge gespeicherte Tabelle. Dabei stellt der Columnstore-Index eine Technologie zum Verwalten von Daten dar, die in einer Columnstore-Tabelle gespeichert sind.  Der gruppierte Columnstore-Index hat keine Auswirkungen auf die Verteilung der Daten. Er bestimmt vielmehr, wie die Daten in den einzelnen Verteilungen gespeichert werden.

Um aus einer Rowstore-Tabelle eine Columnstore-Tabelle zu machen, müssen alle in der Tabelle vorhandenen Indizes gelöscht und ein gruppierter Columnstore-Index erstellt werden. Ein Beispiel hierzu finden Sie unter [CREATE COLUMNSTORE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-columnstore-index-transact-sql.md).

Weitere Informationen dazu finden Sie in diesen Artikeln:
- [Columnstore-Indizes: Zusammenfassung der Features für Produktversionen](https://msdn.microsoft.com/library/dn934994/)
- [Indizieren von Tabellen in SQL Data Warehouse](https://azure.microsoft.com/en-us/documentation/articles/sql-data-warehouse-tables-index/)
- [Beschreibung von Columnstore-Indizes](~/relational-databases/indexes/columnstore-indexes-overview.md) 
 
<a name="LimitationsRestrictions"></a>  
## <a name="limitations-and-restrictions"></a>Einschränkungen  
 Für eine Verteilungsspalte darf keine DEFAULT-Einschränkung definiert werden.  
  
 ### <a name="partitions"></a>Partitionen
 Bei Verwendung von Partitionen darf die Partitionsspalte keine reine Unicode-Sortierung aufweisen. So schlägt die folgende Anweisung beispielsweise fehl.  
  
 `CREATE TABLE t1 ( c1 varchar(20) COLLATE Divehi_90_CI_AS_KS_WS) WITH (PARTITION (c1 RANGE FOR VALUES (N'')))`  
 
 Wenn *boundary_value* ein Literalwert ist, der implizit in den Datentyp in *partition_column_name* konvertiert werden muss, ergibt sich eine Abweichung. Zwar wird über die [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]-Systemsichten der Literalwert angezeigt, für [!INCLUDE[tsql](../../includes/tsql-md.md)]-Vorgänge wird jedoch der konvertierte Wert verwendet. 
 
  
 ### <a name="temporary-tables"></a>Temporäre Tabellen 
 Globale temporäre Tabellen, die mit ## beginnen, werden nicht unterstützt.  
  
 Lokale temporäre Tabellen weisen die folgenden Einschränkungen auf:  
  
-   Sie sind nur für die aktuelle Sitzung sichtbar. Am Ende der Sitzung werden sie von [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] automatisch gelöscht. Verwenden Sie zum Löschen von lokalen temporären Tabellen die DROP TABLE-Anweisung.   
-   Sie können nicht umbenannt werden. 
-   Sie dürfen keine Partitionen oder Sichten enthalten.  
-   Deren Berechtigungen können nicht geändert werden. Im Zusammenhang mit lokalen temporären Tabellen können die Anweisungen `GRANT`, `DENY` und `REVOKE` nicht verwendet werden.   
-   Datenbankkonsolenbefehle sind für temporäre Tabellen gesperrt.   
-   Wenn in einem Batch mehrere lokale temporäre Tabellen verwendet werden, muss jede einen eindeutigen Namen aufweisen. Wenn ein Batch von mehreren Sitzungen ausgeführt und dabei jeweils eine lokale temporäre Tabelle erstellt wird, wird von [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] intern ein numerisches Suffix an den Namen der lokalen temporären Tabelle angehängt, sodass jede lokale temporäre Tabelle einen eindeutigen Name aufweist.  
    
<a name="LockingBehavior"></a>   
## <a name="locking-behavior"></a>Sperrverhalten  
 Wendet auf die Tabelle eine exklusive Sperre an. Wendet auf die Objekte DATABASE, SCHEMA und SCHEMARESOLUTION eine gemeinsame Sperre an.  
 

<a name="ExamplesColumn"></a>   
## <a name="examples-for-columns"></a>Beispiele für Spalten

### <a name="ColumnCollation"></a> A. Festlegen einer Spaltensortierung 
 Im folgenden Beispiel wird die Tabelle `MyTable` mit zwei verschiedenen Spaltensortierungen erstellt. Standardmäßig weist die Spalte `mycolumn1` die Standardsortierung Latin1_General_100_CI_AS_KS_WS auf. Die Spalte `mycolumn2` weist die Sortierung Frisian_100_CS_AS auf.  
  
```  
CREATE TABLE MyTable   
  (  
    mycolumnnn1 nvarchar,  
    mycolumn2 nvarchar COLLATE Frisian_100_CS_AS )  
WITH ( CLUSTERED COLUMNSTORE INDEX )  
;  
  
```  
  
### <a name="DefaultConstraint"></a> B. Festlegen einer DEFAULT-Einschränkung für eine Spalte  
 Im folgenden Beispiel ist die Syntax zum Festlegen eines Standardwerts für eine Spalte dargestellt. Die Spalte colA weist eine Standardeinschränkung mit dem Namen constraint_colA und den Standardwert 0 auf.  
  
```  
  
CREATE TABLE MyTable   
  (  
    colA int CONSTRAINT constraint_colA DEFAULT 0,  
    colB nvarchar COLLATE Frisian_100_CS_AS   
  )  
WITH ( CLUSTERED COLUMNSTORE INDEX )  
;  
```  

<a name="ExamplesTemporaryTables"></a> 
## <a name="examples-for-temporary-tables"></a>Beispiele für temporäre Tabellen

### <a name="TemporaryTable"></a> C. Erstellen einer lokalen temporären Tabelle  
 Im folgenden Beispiel wird eine lokale temporäre Tabelle namens #myTable erstellt. Die Tabelle wird mit einem dreiteiligen Namen angegeben. Der Name der temporären Tabelle beginnt mit einem #.   
  
```  
CREATE TABLE AdventureWorks.dbo.#myTable   
  (  
   id int NOT NULL,  
   lastName varchar(20),  
   zipCode varchar(6)  
  )  
WITH  
  (   
    DISTRIBUTION = HASH (id),  
    CLUSTERED COLUMNSTORE INDEX   
  )  
;  
```

<a name="ExTableStructure"></a>  
## <a name="examples-for-table-structure"></a>Beispiele für die Tabellenstruktur

### <a name="ClusteredColumnstoreIndex"></a> D. Erstellen einer Tabelle mit einem gruppierten Columnstore-Index  
 Im folgende Beispiel wird eine verteilte Tabelle mit einem gruppierten Columnstore-Index erstellt. Jede Verteilung wird als Columnstore gespeichert.  
  
 Der gruppierte Columnstore-Index hat keine Auswirkung auf die Verteilung der Daten, da die Daten immer zeilenweise verteilt werden. Der gruppierte Columnstore-Index bestimmt jedoch, wie die Daten in den einzelnen Verteilungen gespeichert werden.  
  
```  
  
CREATE TABLE MyTable   
  (  
    colA int CONSTRAINT constraint_colA DEFAULT 0,  
    colB nvarchar COLLATE Frisian_100_CS_AS   
  )  
WITH   
  (   
    DISTRIBUTION = HASH ( colB ),  
    CLUSTERED COLUMNSTORE INDEX   
  )  
;  
```  
 
<a name="ExTableDistribution"></a> 
## <a name="examples-for-table-distribution"></a>Beispiele für die Tabellenverteilung

### <a name="RoundRobin"></a> E. Erstellen einer ROUND_ROBIN-Tabelle  
 Im folgenden Beispiel wird eine ROUND_ROBIN-Tabelle mit drei Spalten und ohne Partitionen erstellt. Die Daten werden in allen Verteilungen verteilt. Die Tabelle wird mit einem gruppierten Columnstore-Index erstellt, der im Vergleich zu einem Heap oder einem gruppierten Rowstore-Index eine bessere Leistung und Datensicherung gewährleistet.  
  
```  
CREATE TABLE myTable   
  (  
    id int NOT NULL,  
    lastName varchar(20),  
    zipCode varchar(6)  
  )  
WITH ( CLUSTERED COLUMNSTORE INDEX );  
```  
  
### <a name="HashDistributed"></a> F. Erstellen einer mittels Hash verteilten Tabelle  
 Im folgenden Beispiel wird dieselbe Tabelle wie im vorherigen Beispiel erstellt. Allerdings werden bei dieser Tabelle die Zeilen (in der `id`-Spalte) gezielt verteilt statt wie bei einer ROUND_ROBIN-Tabelle zufällig verteilt. Die Tabelle wird mit einem gruppierten Columnstore-Index erstellt, der im Vergleich zu einem Heap oder einem gruppierten Rowstore-Index eine bessere Leistung und Datensicherung gewährleistet.  
  
```  
CREATE TABLE myTable   
  (  
    id int NOT NULL,  
    lastName varchar(20),  
    zipCode varchar(6)  
  )  
WITH  
  (   
    DISTRIBUTION = HASH (id),   
    CLUSTERED COLUMNSTORE INDEX  
  );  
```  
  
### <a name="Replicated"></a> G. Erstellen einer replizierten Tabelle  
 Im folgenden Beispiel wird eine replizierte Tabelle ähnlich wie im vorherigen Beispiel erstellt. Replizierte Tabellen werden vollständig auf alle Computeknoten kopiert. Dank dieser Kopie auf allen Computeknoten wird die Anzahl der Datenverschiebungen für Abfragen reduziert. In diesem Beispiel wird ein CLUSTERED INDEX erstellt, der im Vergleich zu einem Heap eine bessere Datenkomprimierung gewährleistet und der möglicherweise nicht genügend Zeilen für eine gute CLUSTERED COLUMNSTORE INDEX-Komprimierung aufweist.  
  
```  
CREATE TABLE myTable   
  (  
    id int NOT NULL,  
    lastName varchar(20),  
    zipCode varchar(6)  
  )  
WITH  
  (   
    DISTRIBUTION = REPLICATE,   
    CLUSTERED INDEX (lastName)  
  );  
```  

<a name="ExTablePartitions"></a> 
## <a name="examples-for-table-partitions"></a>Beispiele für Tabellenpartitionen

###  <a name="PartitionedTable"></a> H. Erstellen einer partitionierten Tabelle  
 Im folgenden Beispiel wird dieselbe Tabelle wie in Beispiel A erstellt, jedoch mit einer RANGE LEFT-Partitionierung für die `id`-Spalte. Es werden vier Partitionsbegrenzungswerte angegeben, sodass sich fünf Partitionen ergeben.  
  
```  
CREATE TABLE myTable   
  (  
    id int NOT NULL,  
    lastName varchar(20),  
    zipCode int)  
WITH   
  (   
  
    PARTITION ( id RANGE LEFT FOR VALUES (10, 20, 30, 40 )),  
    CLUSTERED COLUMNSTORE INDEX      
  )  
;  
```  
  
 In diesem Beispiel werden die Daten in die folgenden Partitionen sortiert:  
  
-   Partition 1: col <= 10   
-   Partition 2: 10 < col <= 20   
-   Partition 3: 20 < col <= 30   
-   Partition 4: 30 < col <= 40   
-   Partition 5: 40 < col  
  
 Wenn diese Tabelle statt mit RANGE LEFT (Standardeinstellung) mit RANGE RIGHT partitioniert wird, werden die Daten in die folgenden Partitionen sortiert:  
  
-   Partition 1: col < 10  
-   Partition 2: 10 <= col < 20   
-   Partition 3: 20 <= col < 30    
-   Partition 4: 30 <= col < 40   
-   Partition 5: 40 <= col  
  
### <a name="OnePartition"></a> I. Erstellen einer partitionierten Tabelle mit einer Partition  
 Im folgende Beispiel wird eine partitionierte Tabelle mit einer Partition erstellt. Es werden keine Begrenzungswerte angegeben, sodass sich nur eine Partition ergibt.  
  
```  
CREATE TABLE myTable (  
    id int NOT NULL,  
    lastName varchar(20),  
    zipCode int)  
WITH   
    (   
      PARTITION ( id RANGE LEFT FOR VALUES ( )),  
      CLUSTERED COLUMNSTORE INDEX  
    )  
;  
```  
  
### <a name="DatePartition"></a> J. Erstellen einer Tabelle mit Datumspartitionierung  
 Im folgenden Beispiel wird eine neue Tabelle mit dem Namen `myTable` mit Partitionierung in einer `date`-Spalte erstellt. Durch die Verwendung von RANGE RIGHT und Datumsangaben für die Begrenzungswerte werden in alle Partitionen die Daten eines Monats eingefügt.  
  
```  
CREATE TABLE myTable (  
    l_orderkey      bigint,       
    l_partkey       bigint,                                             
    l_suppkey       bigint,                                           
    l_linenumber    bigint,        
    l_quantity      decimal(15,2),  
    l_extendedprice decimal(15,2),  
    l_discount      decimal(15,2),  
    l_tax           decimal(15,2),  
    l_returnflag    char(1),  
    l_linestatus    char(1),  
    l_shipdate      date,  
    l_commitdate    date,  
    l_receiptdate   date,  
    l_shipinstruct  char(25),  
    l_shipmode      char(10),  
    l_comment       varchar(44))  
WITH   
  (   
    DISTRIBUTION = HASH (l_orderkey),  
    CLUSTERED COLUMNSTORE INDEX,  
    PARTITION ( l_shipdate  RANGE RIGHT FOR VALUES   
      (  
        '1992-01-01','1992-02-01','1992-03-01','1992-04-01','1992-05-01',
        '1992-06-01','1992-07-01','1992-08-01','1992-09-01','1992-10-01',
        '1992-11-01','1992-12-01','1993-01-01','1993-02-01','1993-03-01',
        '1993-04-01','1993-05-01','1993-06-01','1993-07-01','1993-08-01',
        '1993-09-01','1993-10-01','1993-11-01','1993-12-01','1994-01-01',
        '1994-02-01','1994-03-01','1994-04-01','1994-05-01','1994-06-01',
        '1994-07-01','1994-08-01','1994-09-01','1994-10-01','1994-11-01',
        '1994-12-01'  
      ))
  );  
```  
  
<a name="SeeAlso"></a>    
## <a name="see-also"></a>Siehe auch 
 
 [CREATE TABLE AS SELECT &#40;Azure SQL Data Warehouse&#41;](../../t-sql/statements/create-table-as-select-azure-sql-data-warehouse.md)   
 [DROP TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-table-transact-sql.md)   
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)  
  
  

---
title: Erstellen der Tabelle (Azure SQL Datawarehouse) | Microsoft Docs
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
 
Zum Verständnis von Tabellen und deren Verwendung finden Sie unter [Tabellen in SQL Data Warehouse](https://azure.microsoft.com/documentation/articles/sql-data-warehouse-tables-overview/).

Hinweis: Diskussionen zu SQL Data Warehouse in diesem Artikel gelten für SQL Data Warehouse und Parallel Data Warehouse, sofern nicht anders angegeben. 
 
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
 Der Name der Datenbank, die die neue Tabelle angelegt werden soll. Gemäß Standardeinstellung die aktuelle Datenbank.  
  
 *schema_name*  
 Das Schema der Tabelle. Angeben von *Schema* ist optional. Wenn leer, wird das Standardschema verwendet.  
  
 *table_name*  
 Der Name der neuen Tabelle. Um eine lokale temporäre Tabelle zu erstellen, der Tabellenname muss mit # vorangestellt werden.  Weitere erläuterungen und Hinweise für temporäre Tabellen finden Sie unter [temporäre Tabellen in Azure SQL Data Warehouse](https://azure.microsoft.com/documentation/articles/sql-data-warehouse-tables-temporary/). 
 
 *column_name*  
 Der Name einer Tabellenspalte.
   
### <a name="ColumnOptions"></a>Spaltenoptionen

 `COLLATE`*Windows_collation_name*  
 Gibt die Sortierung für den Ausdruck. Die Sortierung muss eine unterstützte Windows-Sortierung [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Eine Liste von unterstützten Windows-Sortierungen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], finden Sie unter [Windows-Sortierungsname (Transact-SQL)](http://msdn.microsoft.com/library/ms188046\(v=sql11\)/).  
  
 `NULL` | `NOT NULL`  
 Gibt an, ob `NULL` Werte in der Spalte zulässig sind. Der Standardwert ist `NULL`.  
  
 [ `CONSTRAINT` *constraint_name* ] `DEFAULT` *constant_expression*  
 Gibt den Standardwert für die Spalte an.  
  
 | Argument | Erklärung |
 | -------- | ----------- |
 | *constraint_name* | Der optionale Name für die Einschränkung. Den Namen der Einschränkung wird in der Datenbank eindeutig. Der Name kann in anderen Datenbanken erneut verwendet werden. |
 | *constant_expression* | Der Standardwert für die Spalte. Der Ausdruck muss einen Literalwert oder eine Konstante. Beispielsweise diese Konstante Ausdrücke sind zulässig: `'CA'`, `4`. Diese sind nicht zulässig: `2+3`, `CURRENT_TIMESTAMP`. |
  

### <a name="TableOptions"></a>Tabellenoptionen-Struktur
Hilfestellung bei der Auswahl des Typs der Tabelle finden Sie unter [Indizierung von Tabellen in Azure SQL Data Warehouse](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-tables-index/).
  
 `CLUSTERED COLUMNSTORE INDEX`  
Die Tabelle als gruppierten columnstore-Index gespeichert. Der gruppierte columnstore-Index gilt für alle Daten der Tabelle. Dies ist die Standardeinstellung für [!INCLUDE[ssSDW](../../includes/sssdw-md.md)].   
 
 `HEAP`   
  Die Tabelle als Heap gespeichert. Dies ist die Standardeinstellung für [!INCLUDE[ssPDW](../../includes/sspdw-md.md)].  
  
 `CLUSTERED INDEX`( *Index_column_name* [,... *n* ] )  
 Speichert die Tabelle einen gruppierten Index mit ein oder mehrere Schlüsselspalten. Speichert die Daten zeilenweise. Verwendung *Index_column_name* auf den Namen der ein oder mehrere Schlüsselspalten im Index angeben.  Weitere Informationen finden Sie in der Rowstore-Tabellen in der allgemeinen hinweisen.
 
 `LOCATION = USER_DB`   
 Diese Option ist veraltet. Es syntaktisch zulässig, jedoch nicht mehr erforderlich und wirkt sich nicht mehr auf das Verhalten.   
  
### <a name="TableDistributionOptions"></a>Tabelle Verteilungsoptionen
Um zu verstehen, wie die beste Verteilungsmethode auszuwählen und verteilte Tabellen zu verwenden, finden Sie unter [Verteilen von Tabellen in Azure SQL Data Warehouse](https://azure.microsoft.com/documentation/articles/sql-data-warehouse-tables-distribute/).

`DISTRIBUTION = HASH` ( *distribution_column_name* )   
Weist jede Zeile an einen Verteilungspunkt durch den Wert in gespeicherten hashing *Distribution_column_name*. Der Algorithmus ist deterministisch, was bedeutet, dass immer den gleichen Wert für die gleiche Verteilung Hashs.  Die verteilungsspalte sollten seit alle Zeilen, die NULL wurde für die gleiche Verteilung zugewiesen werden, haben, als NOT NULL definiert werden.

`DISTRIBUTION = ROUND_ROBIN`   
Die Zeilen verteilt gleichmäßig auf alle Verteilungen im Round-Robin. Dies ist die Standardeinstellung für [!INCLUDE[ssSDW](../../includes/sssdw-md.md)].

`DISTRIBUTION = REPLICATE`    
Speichert eine Kopie der Tabelle auf jeder Compute-Knoten. Für [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] ist die Tabelle in einer Verteilungsdatenbank für jeden Compute-Knoten gespeichert. Für [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], die Tabelle befindet sich in einem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Dateigruppe, die den Compute-Knoten erstreckt. Dies ist die Standardeinstellung für [!INCLUDE[ssPDW](../../includes/sspdw-md.md)].
  
### <a name="TablePartitionOptions"></a>Tabellenoptionen für die partition
Anleitung zur Verwendung von Tabellenpartitionen, finden Sie unter [Partitionierung von Tabellen in SQL Data Warehouse](https://azure.microsoft.com/documentation/articles/sql-data-warehouse-tables-partition/).

 `PARTITION` ( *partition_column_name* `RANGE` [ `LEFT` | `RIGHT` ] `FOR VALUES` ( [ *boundary_value* [,...*n*] ] ))   
Erstellt ein oder mehrere Tabellenpartitionen. Hierbei handelt es sich um horizontale Slices, mit denen Sie Vorgänge auf Teilmengen von Zeilen unabhängig davon, ob die Tabelle als Heap, gruppierter Index oder gruppierten columnstore-Index gespeichert wird. Im Gegensatz zu der verteilungsspalte bestimmen Tabellenpartitionen nicht die Verteilung, in dem jede Zeile gespeichert wird. Stattdessen bestimmen Tabellenpartitionen, wie Zeilen gruppiert und innerhalb jedes Verteilungspunkts gespeichert sind.  
 
| Argument | Erklärung |
| -------- | ----------- |
|*partition_column_name*| Gibt die Spalte, die [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] verwendet, um die Zeilen zu partitionieren. Diese Spalte kann einen beliebigen Datentyp aufweisen. [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]wird die Partition-Spaltenwerte in aufsteigender Reihenfolge sortiert. Die Reihenfolge von niedrig zu hoch wechselt von `LEFT` auf `RIGHT` für die `RANGE` Spezifikation. |  
| `RANGE LEFT` | Gibt an, dass der Grenzwert für die Partition auf der linken Seite (niedrigere Werte) gehört. Der Standardwert ist links. |
| `RANGE RIGHT` | Gibt an, dass der Grenzwert für die Partition auf der rechten Seite (höher Werte) gehört. | 
| `FOR VALUES`( *Boundary_value* [,... *n*] ) | Gibt die Begrenzungswerte für die Partition an. *Boundary_value* ist ein konstanter Ausdruck. Es darf nicht NULL sein. Er muss übereinstimmen oder werden implizit in den Datentyp der *Partition_column_name*. Es kann nicht abgeschnitten werden während der impliziten Konvertierung, damit die Größe und Dezimalstellen des Werts nicht den Datentyp des übereinstimmen *Partition_column_name*<br></br><br></br>Bei Angabe der `PARTITION` -Klausel, aber geben Sie einen Begrenzungswert an, keine [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] erstellen Sie eine partitionierte Tabelle mit einer Partition. Sofern zutreffend, Sie einer geteilten Tabelle in zwei Partitionen zu einem späteren Zeitpunkt.<br></br><br></br>Wenn Sie einen Begrenzungswert angeben, hat die resultierende Tabelle zwei Partitionen; eine für die Werte, die niedriger ist als der Begrenzungswert und einen für die Werte, die höher als der Begrenzungswert. Beachten Sie, dass wenn Sie eine Partition in eine nicht partitionierte Tabelle verschieben, die nicht partitionierten Tabelle die Daten erhalten, aber keinen die Partitionsgrenzen in seinen Metadaten.| 
 
 Finden Sie unter [erstellen Sie eine partitionierte Tabelle](#PartitionedTable) im Abschnitt "Beispiele".

### <a name="DataTypes"></a>Datentypen
[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]die am häufigsten verwendeten unterstützt die Datentypen. Es folgt eine Liste der unterstützten Datentypen zusammen mit ihren Details und Speicherplatz in Bytes. Zum besseren Verständnis von Datentypen und deren Verwendung finden Sie unter [ Datentypen für Tabellen in SQL Data Warehouse](https://azure.microsoft.com/documentation/articles/sql-data-warehouse-tables-data-types).

Bei einer Tabelle von datentypkonvertierungen finden Sie im Abschnitt implizite Konvertierungen von [CAST und CONVERT (Transact-SQL)](http://msdn.microsoft.com/library/ms187928/).

`datetimeoffset` [ ( *n* ) ]  
 Der Standardwert für  *n*  ist 7.  
  
 `datetime2` [ ( *n* ) ]  
Identisch mit `datetime`, außer dass Sie die Anzahl der Bruchteile von Sekunden angeben können. Der Standardwert für  *n*  ist `7`.  
  
|*n*Wert|Genauigkeit|Dezimalstellen|  
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
 Speichert Datum und Uhrzeit mit 19 bis 23 Zeichen nach dem gregorianischen Kalender. Das Datum kann Jahr, Monat und Tag enthalten. Die Zeit enthält Stunde, Minuten und Sekunden. Optional können Sie drei Ziffern für Sekundenbruchteile anzeigen. Die Speichergröße beträgt 8 Byte.  
  
 `smalldatetime`  
 Speichert ein Datum und eine Uhrzeit. Die Speichergröße beträgt 4 Byte.  
  
 `date`  
 Speichert ein Datum unter Verwendung von maximal 10 Zeichen für Jahr, Monat und Tag nach dem gregorianischen Kalender. Die Speichergröße beträgt 3 Bytes. Datum wird als eine ganze Zahl gespeichert.  
  
 `time` [ ( *n* ) ]  
 Der Standardwert für  *n*  ist `7`.  
  
 `float` [ ( *n* ) ]  
 Ungefähre numerische Daten geben Sie für die Verwendung mit numerische Gleitkommadaten. Gleitkommadaten sind ungefähre, was bedeutet, dass nicht alle Werte im Bereich Datentyps exakt dargestellt werden können. *n*Gibt die Anzahl der Bits, die zum Speichern der Mantisse der der `float` in der wissenschaftlichen Schreibweise. Aus diesem Grund  *n*  bestimmt, die Genauigkeit und Speichergröße. Wenn  *n*  angegeben wird, muss er einen Wert zwischen `1` und `53`. Der Standardwert von  *n*  ist `53`.  
  
| *n*Wert | Genauigkeit | Speichergröße |  
| --------: | --------: | -----------: |  
| 1-24   | 7 Dezimalstellen  | 4 bytes      |  
| 25-53  | 15 Stellen | 8 Byte      |  
  
 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]behandelt  *n*  als einen von zwei möglichen Werten. Wenn `1` <=   *n*   <=  `24`,  *n*  so behandelt, als `24`. Wenn `25`  <=   *n*   <=  `53`,  *n*  so behandelt, als `53`.  
  
 Die [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] `float` -Datentyp entspricht dem ISO-Standard für alle Werte des  *n*  aus `1` über `53`. Das Synonym für mit doppelter Genauigkeit ist `float(53)`.  
  
 `real` [ ( *n* ) ]  
 Die Definition von Real ist identisch mit "float". Das ISO-Synonym für `real` ist `float(24)`.  
  
 `decimal`[( *Genauigkeit* [ *, Skalierung* ])] | `numeric` [( *Genauigkeit* [ *, Skalierung* ])]  
 Speichert feste Genauigkeit und Dezimalstellenanzahl Zahlen.  
  
 *precision*  
 Die maximal speicherbare Gesamtzahl an Dezimalstellen, sowohl links als auch rechts vom Dezimalkomma. Die Genauigkeit muss ein Wert aus `1` und der maximalen Genauigkeit von `38`. Die standardgenauigkeit beträgt `18`.  
  
 *scale*  
 Die maximal speicherbare Zahl an Dezimalstellen rechts vom Dezimalkomma. *Skalierung* muss ein Wert aus `0` über *Genauigkeit*. Sie können nur angeben, *Skalierung* Wenn *Genauigkeit* angegeben ist. Der Standardwert ist `0`daher `0`  <=  *Skalierung* <= *Genauigkeit*. Die maximalen Speichergrößen variieren abhängig von der Genauigkeit.  
  
| Genauigkeit | Speicherplatz in Bytes  |  
| ---------: |-------------: |  
|  1-9       |             5 |  
| 10-19      |             9 |  
| 20-28      |            13 |  
| 29-38      |            17 |  
  
 `money` | `smallmoney`  
 Datentypen, die Währungswerte darstellen.  
  
| Datentyp | Speicherplatz in Bytes |  
| --------- | ------------: |  
| `money`|8|  
| `smallmoney` |4|  
  
 `bigint` | `int` | `smallint` | `tinyint`  
 Exakte Zahlendatentypen für ganzzahlige Daten. Der Speicher wird in der folgenden Tabelle gezeigt.  
  
| Datentyp | Speicherplatz in Bytes |  
| --------- | ------------: |  
| `bigint`|8|  
| `int` |4|  
| `smallint` |2|  
| `tinyint` |1|  
  
 `bit`  
 Ein Integer-Datentyp, der den Wert annehmen kann `1`, `0`, oder "NULL. [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]optimiert das Speichern von Bitspalten. Wenn in einer Tabelle 8 oder weniger Bitspalten vorhanden sind, werden die Spalten als 1 Byte gespeichert. Wenn sind zwischen 9 und 16-Bit-Spalten vorhanden, die Spalten werden als 2 Byte gespeichert usw.  
  
 `nvarchar`[(  *n*   |  `max` )]-- `max` gilt nur für [!INCLUDE[ssSDW](../../includes/sssdw-md.md)].  
 Unicode-Daten variabler Länge. *n*ein Wert zwischen 1 und 4000 kann sein. `max` gibt an, dass die maximale Speichergröße 2^31-1 Byte (2 GB) beträgt. Speichergröße in Bytes ist zweimal die Anzahl eingegebener Zeichen + 2 Byte. Die eingegebenen Daten können 0 Zeichen lang sein.  
  
 `nchar` [ ( *n* ) ]  
 Fester Länge, die Unicode-Zeichendaten mit einer Länge von  *n*  Zeichen. *n*muss ein Wert aus `1` über `4000`. Die Speichergröße beträgt zweimal  *n*  Bytes.  
  
 `varchar`[(  *n*    |  `max` )]-- `max` gilt nur für [!INCLUDE[ssSDW](../../includes/sssdw-md.md)].   
 Variabler Länge, nicht-Unicode-Zeichendaten mit einer Länge von  *n*  Bytes. *n*muss ein Wert aus `1` auf `8000`. `max`Gibt an, dass die maximale Speichergröße 2 ^ 31-1 Bytes (2 GB). Die Speichergröße beträgt die tatsächliche Länge der eingegebenen Daten + 2 Byte.  
  
 `char` [ ( *n* ) ]  
 Fester Länge, nicht-Unicode-Zeichendaten mit einer Länge von  *n*  Bytes. *n*muss ein Wert aus `1` auf `8000`. Die Speichergröße beträgt  *n*  Bytes. Die Standardeinstellung für  *n*  ist `1`.  
  
 `varbinary`[(  *n*    |  `max` )]-- `max` gilt nur für [!INCLUDE[ssSDW](../../includes/sssdw-md.md)].  
 Binärdaten mit variabler Länge. *n*kann ein Wert von `1` auf `8000`. `max` gibt an, dass die maximale Speichergröße 2^31-1 Byte (2 GB) beträgt. Die Speichergröße ist die tatsächliche Länge der eingegebenen Daten + 2 Byte. Der Standardwert für  *n*  ist 7.  
  
 `binary` [ ( *n* ) ]  
 Binärdaten fester Länge, mit einer Länge von  *n*  Bytes. *n*kann ein Wert von `1` auf `8000`. Die Speichergröße beträgt  *n*  Bytes. Der Standardwert für  *n*  ist `7`.  
  
 `uniqueidentifier`  
 Ein 16-Byte-GUID.  
   
<a name="Permissions"></a>  
## <a name="permissions"></a>Berechtigungen  
 Erstellen einer Tabelle erfordert die Berechtigung in den `db_ddladmin` feste Datenbankrolle oder:
 - `CREATE TABLE`Berechtigung für die Datenbank
 - `ALTER SCHEMA`Berechtigung für das Schema, das die Tabelle enthalten ist. 

Erstellen einer partitionierten Tabelle erfordert die Berechtigung in den `db_ddladmin` feste Datenbankrolle oder

- `ALTER ANY DATASPACE` permission
  
 Die Anmeldung, die eine lokale temporäre Tabelle erstellt `CONTROL`, `INSERT`, `SELECT`, und `UPDATE` Berechtigungen für die Tabelle.  
 
<a name="GeneralRemarks"></a>  
## <a name="general-remarks"></a>Allgemeine Hinweise  
 
Minimalen und maximalen Grenzwerte, finden Sie unter [SQL Data Warehouse-Kapazitätsgrenzen](https://azure.microsoft.com/documentation/articles/sql-data-warehouse-service-capacity-limits/). 
 
### <a name="determining-the-number-of-table-partitions"></a>Bestimmen der Anzahl der Tabellenpartitionen
Jede benutzerdefinierte Tabelle ist in mehrere kleinere Tabellen aufgeteilt, die im voneinander entfernten Standorten aus aufgerufen Verteilungen gespeichert sind. [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]verwendet die 60-Distributionen. In [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], die Anzahl der Verteilungen hängt die Anzahl der Serverknoten.
 
Jede Verteilung enthält alle Tabellenpartitionen. Z. B. wenn 60 Verteilungen und vier Tabellenpartitionen vorhanden sind, wird 320 Partitionen. Wenn die Tabelle einen gruppierten columnstore-Index ist, werden über einen columnstore-Index pro Partition, d. h. Sie 320 columnstore-Indizes verfügbar werden.

Es wird empfohlen, dass weniger Tabellenpartitionen verwenden, um sicherzustellen, dass jede columnstore-Index zu nutzen der Vorteile von columnstore-Indizes genügend Zeilen verfügt. Weitere Anleitungen finden Sie unter [Partitionierung von Tabellen in SQL Data Warehouse](https://azure.microsoft.com/documentation/articles/sql-data-warehouse-tables-partition/) und [Indizierung von Tabellen in SQL Data Warehouse](https://azure.microsoft.com/en-us/documentation/articles/sql-data-warehouse-tables-index/)  

  
 ### <a name="rowstore-table-heap-or-clustered-index"></a>Rowstore-Tabelle (Heap oder gruppierter Index)  
 Eine Rowstore-Tabelle ist eine Tabelle in der Zeile für Zeile Reihenfolge gespeichert. Es ist ein Heap oder gruppierten Index. [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]erstellt alle Rowstore-Tabellen mit Page-Komprimierung an. Dies ist nicht BenutzerKonfigurierbar.   
 
 ### <a name="columnstore-table-columnstore-index"></a>Columnstore-Tabelle (Columnstore Index)
Eine columnstore-Tabelle ist eine Tabelle in der Spalte für Spalte Reihenfolge gespeichert. Der columnstore-Index ist die Technologie, die in eine columnstore-Tabelle gespeicherte Daten verwaltet.  Der gruppierte columnstore-Index wirkt sich nicht darauf aus, wie die Daten verteilt sind; wirkt sich wie die Daten innerhalb jedes Verteilungspunkts gespeichert werden.

Um eine Rowstore-Tabelle in eine columnstore-Tabelle zu ändern, löschen Sie alle vorhandenen Indizes für die Tabelle, und erstellen Sie einen gruppierten columnstore-Index. Ein Beispiel finden Sie unter [CREATE COLUMNSTORE INDEX &#40; Transact-SQL &#41; ](../../t-sql/statements/create-columnstore-index-transact-sql.md).

Weitere Informationen dazu finden Sie in diesen Artikeln:
- [Columnstore-Indizes, Zusammenfassung Versionsangabe](https://msdn.microsoft.com/library/dn934994/)
- [Volltextindizierung von Tabellen in SQL Data Warehouse](https://azure.microsoft.com/en-us/documentation/articles/sql-data-warehouse-tables-index/)
- [Beschreibung von Columnstore-Indizes](~/relational-databases/indexes/columnstore-indexes-overview.md) 
 
<a name="LimitationsRestrictions"></a>  
## <a name="limitations-and-restrictions"></a>Einschränkungen  
 Sie können keine DEFAULT-Einschränkung für eine verteilungsspalte definieren.  
  
 ### <a name="partitions"></a>Partitionen
 Wenn Sie Partitionen verwenden, sind keine die Partitionsspalte eine nur-Unicode-Sortierung. Beispielsweise schlägt die folgende Anweisung aus.  
  
 `CREATE TABLE t1 ( c1 varchar(20) COLLATE Divehi_90_CI_AS_KS_WS) WITH (PARTITION (c1 RANGE FOR VALUES (N'')))`  
 
 Wenn *Boundary_value* ein Literalwert, der implizit in den Datentyp in konvertiert werden müssen *Partition_column_name*, eine Diskrepanz erfolgt. Der Literalwert wird angezeigt, über die [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] Systemsichten verwendet, sondern der konvertierte Wert wird zur [!INCLUDE[tsql](../../includes/tsql-md.md)] Vorgänge. 
 
  
 ### <a name="temporary-tables"></a>Temporäre Tabellen 
 Globale temporäre Tabellen, die mit beginnen ## werden nicht unterstützt.  
  
 Lokale temporäre Tabellen weisen die folgenden Einschränkungen:  
  
-   Sie sind nur für die aktuelle Sitzung sichtbar. [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]Löscht diese automatisch am Ende der Sitzung. Verwenden Sie zum Verwerfen von Explicitlt DROP TABLE-Anweisung.   
-   Weil sie können nicht umbenannt werden. 
-   Sie können keine Partitionen oder Ansichten haben.  
-   Ihre Berechtigungen können nicht geändert werden. `GRANT`, `DENY`, und `REVOKE` Anweisungen können nicht mit lokalen temporären Tabellen verwendet werden.   
-   Datenbank-Konsolenbefehle sind für temporäre Tabellen blockiert.   
-   Wenn mehr als eine lokale temporäre Tabelle innerhalb eines Batches verwendet wird, muss jede einen eindeutigen Namen haben. Wenn mehrere Sitzungen die gleichen Batch ausführen und die gleiche lokale temporäre Tabelle erstellen [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] fügt intern ein numerisches Suffix an den Namen der lokalen temporären Tabelle einen eindeutigen Namen für jede lokale temporäre Tabelle zu verwalten.  
    
<a name="LockingBehavior"></a>   
## <a name="locking-behavior"></a>Sperrverhalten  
 Akzeptiert eine exklusive Sperre für die Tabelle an. Akzeptiert eine gemeinsame Sperre für die Datenbank, SCHEMA und SCHEMARESOLUTION-Objekte.  
 

<a name="ExamplesColumn"></a>   
## <a name="examples-for-columns"></a>Beispiele für Spalten

### <a name="ColumnCollation"></a> A. Geben Sie eine spaltensortierung 
 Im folgenden Beispiel, in der Tabelle `MyTable` mit zwei verschiedenen spaltensortierungen erstellt wird. Standardmäßig wird die Spalte `mycolumn1`, weist die standardsortierung Latin1_General_100_CI_AS_KS_WS. Die Spalte `mycolumn2` Frisian_100_CS_AS Sortierung aufweist.  
  
```  
CREATE TABLE MyTable   
  (  
    mycolumnnn1 nvarchar,  
    mycolumn2 nvarchar COLLATE Frisian_100_CS_AS )  
WITH ( CLUSTERED COLUMNSTORE INDEX )  
;  
  
```  
  
### <a name="DefaultConstraint"></a> B. Geben Sie eine DEFAULT-Einschränkung für eine Spalte  
 Das folgende Beispiel zeigt die Syntax, um einen Standardwert für eine Spalte angeben. Die Spalte ColA verfügt über eine Default-Einschränkung mit dem Namen Constraint_colA und den Standardwert 0.  
  
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

### <a name="TemporaryTable"></a> C. Erstellen Sie eine lokale temporäre Tabelle  
 Im folgenden wird eine lokale temporäre Tabelle mit dem Namen #myTable erstellt. Die Tabelle wird mit einem 3 zweiteilige Namen angegeben. Der Name der temporären Tabelle beginnt mit einem #.   
  
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

### <a name="ClusteredColumnstoreIndex"></a> D. Erstellen Sie eine Tabelle mit einem gruppierten columnstore-index  
 Im folgende Beispiel wird eine verteilte Tabelle mit einem gruppierten columnstore-Index erstellt. Jeder Verteilungspunkt wird als Columnstore gespeichert werden.  
  
 Der gruppierte columnstore-Index hat keinen Einfluss auf die Verteilung der Daten; Daten werden immer zeilenweise verteilt. Der gruppierte columnstore-Index wirkt sich auf, wie die Daten innerhalb jedes Verteilungspunkts gespeichert ist.  
  
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
## <a name="examples-for-table-distribution"></a>Beispiele für die Verteilung der Tabelle

### <a name="RoundRobin"></a> E. Erstellen Sie eine Tabelle ROUND_ROBIN  
 Das folgende Beispiel erstellt eine ROUND_ROBIN-Tabelle mit drei Spalten und ohne Partitionen. Die Daten ist alle Verteilungen verteilt. Die Tabelle wird mit einem gruppierten columnstore-INDEX erstellt, die eine bessere Leistung und der datenkomprimierung als bei einem Heap oder Rowstore gruppierten Index enthält.  
  
```  
CREATE TABLE myTable   
  (  
    id int NOT NULL,  
    lastName varchar(20),  
    zipCode varchar(6)  
  )  
WITH ( CLUSTERED COLUMNSTORE INDEX );  
```  
  
### <a name="HashDistributed"></a> F. Erstellen Sie eine Tabelle mit Hash verteilt  
 Das folgende Beispiel erstellt die gleiche Tabelle wie im vorherigen Beispiel. Allerdings für diese Tabelle Zeilen verteilt werden (auf der `id` Spalte) nach dem Zufallsprinzip anstelle von verteilt, wie eine Tabelle ROUND_ROBIN. Die Tabelle wird mit einem gruppierten columnstore-INDEX erstellt, die eine bessere Leistung und der datenkomprimierung als bei einem Heap oder Rowstore gruppierten Index enthält.  
  
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
  
### <a name="Replicated"></a> G. Erstellen Sie eine replizierte Tabelle  
 Das folgende Beispiel erstellt eine replizierte Tabelle wie in den vorherigen Beispielen. Replizierte Tabellen werden vollständig in jeder Serverknoten kopiert. Mit dieser Kopie auf jedem Knoten der COMPUTE-wird die datenverschiebung für Abfragen reduziert. In diesem Beispiel wird mit einem gruppierten INDEX erstellt, der bietet bessere datenkomprimierung als einen Heap und enthält möglicherweise nicht genügend Zeilen um gute CLUSTERED COLUMNSTORE INDEX-Komprimierung zu erreichen.  
  
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

###  <a name="PartitionedTable"></a> H. Erstellen Sie eine partitionierte Tabelle  
 Das folgende Beispiel erstellt die gleiche Tabelle wie im Beispiel ein, durch das Hinzufügen von RANGE LEFT Partitionierung für die `id` Spalte. Es gibt vier Partitionsbegrenzungswerte ansprechen fünf Partitionen.  
  
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
  
 In diesem Beispiel werden die Daten in die folgenden Partitionen sortiert werden:  
  
-   Partition 1: Col < = 10   
-   Partitionieren von 2:10 < Col < = 20   
-   Partitionieren von 3:20 < Col < = 30   
-   Partitionieren von 4:30 < Col < = 40   
-   Partition 5:40 < Col  
  
 Wenn in der gleichen Tabelle partitioniert wurde RANGE RIGHT anstelle von RANGE LEFT (Standard), die Daten in die folgenden Partitionen sortiert werden:  
  
-   Partition 1: Col < 10  
-   Partitionieren von 2:10 < = Col < 20   
-   Partitionieren von 3:20 < = Col < 30    
-   Partitionieren von 4:30 < Col 40 < =   
-   Partition 5:40 < = Col  
  
### <a name="OnePartition"></a> I. Erstellen Sie eine partitionierte Tabelle mit einer partition  
 Im folgende Beispiel wird eine partitionierte Tabelle mit einer Partition erstellt. Es gibt keine Begrenzungswerte an, was dazu führt zu einer einzigen Partition.  
  
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
  
### <a name="DatePartition"></a> J. Erstellen Sie eine Tabelle mit der Partitionierung Datum  
 Das folgende Beispiel erstellt eine neue Tabelle namens `myTable`, mit der Partitionierung für eine `date` Spalte. Mit RANGE RIGHT und Datumsangaben für die Begrenzungswerte, legt er die Daten ein Monats in jeder Partition.  
  
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
 
 [Erstellen Sie die Tabelle als SELECT &#40; Azure SQL Datawarehouse &#41;](../../t-sql/statements/create-table-as-select-azure-sql-data-warehouse.md)   
 [DROP TABLE &#40; Transact-SQL &#41;](../../t-sql/statements/drop-table-transact-sql.md)   
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)  
  
  

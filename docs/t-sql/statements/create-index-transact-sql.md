---
title: Erstellen des INDEX (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 12/21/2017
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
- CREATE INDEX
- INDEX
- INDEX_TSQL
- CREATE_INDEX_TSQL
dev_langs: TSQL
helpviewer_keywords:
- CREATE XML INDEX statement
- PRIMARY XML INDEX statement
- indexes [SQL Server], creating
- online index operations
- index keys [SQL Server]
- PROPERTY INDEX statement
- computed columns, index creation
- clustered indexes, creating
- indexed views [SQL Server], index creation
- partitioned indexes [SQL Server], creating
- VALUE INDEX statement
- index creation [SQL Server], CREATE INDEX statement
- DROP_EXISTING clause
- row locks [SQL Server]
- composite indexes
- MAXDOP index option, CREATE INDEX statement
- filtered indexes [SQL Server], creating
- PATH INDEX statement
- locking [SQL Server], indexes
- unique indexes, creating
- primary indexes [SQL Server]
- CREATE PRIMARY XML INDEX statement
- SET statement, index creation
- index options [SQL Server]
- included columns
- ONLINE option
- nonclustered indexes [SQL Server], creating
- CREATE INDEX statement
- IGNORE_DUP_KEY option
- deterministic functions
- keys [SQL Server], index
- SECONDARY XML INDEX statement
- page locks [SQL Server]
- secondary indexes [SQL Server]
- XML indexes [SQL Server], creating
ms.assetid: d2297805-412b-47b5-aeeb-53388349a5b9
caps.latest.revision: "223"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 48d755dcd5257a3208c087db44df1e9fd262ddcc
ms.sourcegitcommit: 4aeedbb88c60a4b035a49754eff48128714ad290
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/05/2018
---
# <a name="create-index-transact-sql"></a>CREATE INDEX (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Erstellt einen relationalen Index für eine Tabelle oder Sicht an. Auch als einen Rowstore-Index bezeichnet, da es sich um ein gruppierter oder nicht gruppierter B-Struktur-Index handelt. Sie können einen Rowstore-Index erstellen, bevor Daten in der Tabelle vorhanden ist. Verwenden Sie einen Rowstore-Index, um die abfrageleistung zu verbessern, besonders bei der die Abfragen bestimmte Spalten auswählen oder erfordern Werte, die in einer bestimmten Reihenfolge sortiert werden.  
  
> [!NOTE]  
> [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]und [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] unterstützen derzeit keine Unique-Einschränkungen. Alle Beispiele verweisen auf die Unique-Einschränkungen gelten nur für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] und [!INCLUDE[ssSDS](../../includes/sssds-md.md)].    

> [!TIP]
> Informationen zu Richtlinien zum Entwerfen Indizes, finden Sie in der [SQL Server Handbuch zum Indexentwurf](../../relational-databases/sql-server-index-design-guide.md).

 **Einfache Beispiele:**  
  
```  
-- Create a nonclustered index on a table or view  
CREATE INDEX i1 ON t1 (col1);  
```  
  
```  
--Create a clustered index on a table and use a 3-part name for the table  
CREATE CLUSTERED INDEX i1 ON d1.s1.t1 (col1);  
```  
  
```  
-- Syntax for SQL Server and Azure SQL Database
-- Create a nonclustered index with a unique constraint 
-- on 3 columns and specify the sort order for each column  
CREATE UNIQUE INDEX i1 ON t1 (col1 DESC, col2 ASC, col3 DESC);  
```  
  
 **Wichtige Szenarien:**  
  
-   Beginnend mit [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] und [!INCLUDE[ssSDS](../../includes/sssds-md.md)], einen nicht gruppierten Index für einen columnstore-Index verwenden, um die Data Warehouse-abfrageleistung zu verbessern. Weitere Informationen finden Sie unter [columnstore-Indizes - Data Warehouse](../../relational-databases/indexes/columnstore-indexes-data-warehouse.md).  
  
**Muss eine andere Art von Index erstellen?**  
  
-   [Erstellen von XML-INDEX &#40; Transact-SQL &#41;](../../t-sql/statements/create-xml-index-transact-sql.md)  
-   [CREATE SPATIAL INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-spatial-index-transact-sql.md)  
-   [CREATE COLUMNSTORE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-columnstore-index-transact-sql.md)     
  
![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
-- Syntax for SQL Server and Azure SQL Database
  
CREATE [ UNIQUE ] [ CLUSTERED | NONCLUSTERED ] INDEX index_name   
    ON <object> ( column [ ASC | DESC ] [ ,...n ] )   
    [ INCLUDE ( column_name [ ,...n ] ) ]  
    [ WHERE <filter_predicate> ]  
    [ WITH ( <relational_index_option> [ ,...n ] ) ]  
    [ ON { partition_scheme_name ( column_name )   
         | filegroup_name   
         | default   
         }  
    ]  
    [ FILESTREAM_ON { filestream_filegroup_name | partition_scheme_name | "NULL" } ]  
  
[ ; ]  
  
<object> ::=  
{  
    [ database_name. [ schema_name ] . | schema_name. ]   
    table_or_view_name  
}  
  
<relational_index_option> ::=  
{  
    PAD_INDEX = { ON | OFF }  
  | FILLFACTOR = fillfactor  
  | SORT_IN_TEMPDB = { ON | OFF }  
  | IGNORE_DUP_KEY = { ON | OFF }  
  | STATISTICS_NORECOMPUTE = { ON | OFF }  
  | STATISTICS_INCREMENTAL = { ON | OFF }  
  | DROP_EXISTING = { ON | OFF }  
  | ONLINE = { ON | OFF }  
  | ALLOW_ROW_LOCKS = { ON | OFF }  
  | ALLOW_PAGE_LOCKS = { ON | OFF }  
  | MAXDOP = max_degree_of_parallelism  
  | DATA_COMPRESSION = { NONE | ROW | PAGE}   
     [ ON PARTITIONS ( { <partition_number_expression> | <range> }   
     [ , ...n ] ) ]  
}  
  
<filter_predicate> ::=   
    <conjunct> [ AND <conjunct> ]  
  
<conjunct> ::=  
    <disjunct> | <comparison>  
  
<disjunct> ::=  
        column_name IN (constant ,...n)  
  
<comparison> ::=  
        column_name <comparison_op> constant  
  
<comparison_op> ::=  
    { IS | IS NOT | = | <> | != | > | >= | !> | < | <= | !< }  
  
<range> ::=   
<partition_number_expression> TO <partition_number_expression>  
  
Backward Compatible Relational Index

> [!IMPORTANT]
> The backward compatible relational index syntax structure will be removed in a future version of [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. 
> Avoid using this syntax structure in new development work, and plan to modify applications that currently use the feature. 
> Use the syntax structure specified in <relational_index_option> instead.  
  
CREATE [ UNIQUE ] [ CLUSTERED | NONCLUSTERED ] INDEX index_name   
    ON <object> ( column_name [ ASC | DESC ] [ ,...n ] )   
    [ WITH <backward_compatible_index_option> [ ,...n ] ]  
    [ ON { filegroup_name | "default" } ]  
  
<object> ::=  
{  
    [ database_name. [ owner_name ] . | owner_name. ]   
    table_or_view_name  
}  
  
<backward_compatible_index_option> ::=  
{   
    PAD_INDEX  
  | FILLFACTOR = fillfactor  
  | SORT_IN_TEMPDB  
  | IGNORE_DUP_KEY  
  | STATISTICS_NORECOMPUTE   
  | DROP_EXISTING   
}  
```  

  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
CREATE [ CLUSTERED | NONCLUSTERED ] INDEX index_name   
    ON [ database_name . [ schema ] . | schema . ] table_name   
        ( { column [ ASC | DESC ] } [ ,...n ] )  
    WITH ( DROP_EXISTING = { ON | OFF } )  
[;]  
```  
  
## <a name="arguments"></a>Argumente  
UNIQUE  
Erstellt einen eindeutigen Index für eine Tabelle oder Sicht. Ein eindeutiger Index ist ein Index, bei dem zwei Zeilen nicht den gleichen Indexschlüsselwert haben dürfen. Ein gruppierter Index für eine Sicht muss eindeutig sein.  
  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] lässt das Erstellen eines eindeutigen Index für Spalten, die bereits doppelte Werte enthalten, nicht zu. Dies ist unabhängig davon, ob IGNORE_DUP_KEY auf ON festgelegt ist. Wenn Sie dies versuchen, wird in [!INCLUDE[ssDE](../../includes/ssde-md.md)] eine Fehlermeldung angezeigt. Doppelte Werte müssen entfernt werden, bevor ein eindeutiger Index für die Spalte oder Spalten erstellt werden kann. In einem eindeutigen Index verwendete Spalten müssen auf NOT NULL festgelegt werden, da mehrere NULL-Werte beim Erstellen eines eindeutigen Index als Duplikate angesehen werden.  
  
CLUSTERED  
Erstellt einen Index, in dem die logische Reihenfolge der Schlüsselwerte die physische Reihenfolge der entsprechenden Zeilen in einer Tabelle bestimmt. Die unterste Ebene oder Blattebene des gruppierten Indexes enthält die eigentlichen Datenzeilen der Tabelle. Eine Tabelle oder Sicht kann nur über jeweils einen gruppierten Index verfügen.  
  
 Eine Sicht mit einem eindeutigen gruppierten Index wird als indizierte Sicht bezeichnet. Durch das Erstellen eines eindeutigen gruppierten Index für eine Sicht wird die Sicht physisch materialisiert. Ein eindeutiger gruppierter Index muss für eine Sicht erstellt werden, bevor ein anderer Index für dieselbe Sicht definiert werden kann. Weitere Informationen finden Sie unter [Erstellen von indizierten Sichten](../../relational-databases/views/create-indexed-views.md).  
  
 Erstellen Sie den gruppierten Index, bevor Sie irgendeinen nicht gruppierten Index erstellen. Für eine Tabelle vorhandene nicht gruppierte Indizes werden neu erstellt, wenn ein gruppierter Index erstellt wird.  
  
 Ist CLUSTERED nicht angegeben, wird ein nicht gruppierter Index erstellt.  
  
> [!NOTE]  
> Da die Blattebene eines gruppierten Indexes und die Datenseiten sind per Definition identisch, einen gruppierten Index erstellen und Verwenden der ON *Partition_scheme_name* oder ON *Filegroup_name* -Klausel effektiv wird eine Tabelle aus der Dateigruppe, in der die Tabelle erstellt wurde, das neue Partitionsschema oder die Dateigruppe verschoben. Bevor Sie Tabellen oder Indizes für bestimmte Dateigruppen erstellen, überprüfen Sie, welche Dateigruppen verfügbar sind, und stellen Sie sicher, dass in ihnen ausreichend freier Speicherplatz für den Index vorhanden ist.  
  
 In einigen Fällen können durch das Erstellen eines gruppierten Indexes zuvor deaktivierte Indizes aktiviert werden. Weitere Informationen finden Sie unter [Enable Indexes and Constraints](../../relational-databases/indexes/enable-indexes-and-constraints.md) und [Deaktivieren von Indizes und Einschränkungen](../../relational-databases/indexes/disable-indexes-and-constraints.md).  
  
**NICHT GRUPPIERTE**  
Erstellt einen Index, der die logische Reihenfolge einer Tabelle angibt. Bei einem nicht gruppierten Index ist die physische Reihenfolge der Datenzeilen unabhängig von deren indizierter Reihenfolge.  
  
 Jede Tabelle kann über bis zu 999 nicht gruppierte Indizes verfügen, unabhängig davon, wie die Indizes erstellt werden: implizit mit PRIMARY KEY- und UNIQUE-Einschränkungen oder explizit mit CREATE INDEX.  
  
 Für indizierte Sichten können nicht gruppierte Indizes nur erstellt werden, wenn bereits ein eindeutiger gruppierter Index für die entsprechende Sicht definiert ist.  
  
 Wenn nicht anders angegeben, ist der Standard-Indextyp NONCLUSTERED.  
  
 *index_name*  
 Der Name des Indexes. Indexnamen müssen für eine Tabelle oder Sicht eindeutig sein, können aber innerhalb einer Datenbank mehrfach vorkommen. Indexnamen müssen den Regeln der [Bezeichner](../../relational-databases/databases/database-identifiers.md).  
  
 *column*  
 Gibt die Spalte(n) an, auf der bzw. denen der Index basiert. Geben Sie zwei oder mehr Spaltennamen an, um einen zusammengesetzten Index für die kombinierten Werte der angegebenen Spalten zu erstellen. Listet die Spalten im zusammengesetzten Index in der Reihenfolge der Sortierpriorität in den Klammern hinter einzuschließenden *Table_or_view_name*.  
  
 Bis zu 32 Spalten können in einem einzigen zusammengesetzten Indexschlüssel kombiniert werden. Alle Spalten in einem zusammengesetzten Indexschlüssel müssen sich in derselben Tabelle oder Sicht befinden. Die maximale zulässige Größe der kombinierten Indexwerte ist 900 Bytes für einen gruppierten Index oder 1.700 Bytes für einen nicht gruppierten Index. Die Grenzwerte sind 16 Spalten und 900 Byte für Versionen vor [!INCLUDE[ssSDS](../../includes/sssds-md.md)] V12 und [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)].  
  
 Spalten, die die Datentypen für große Objekte (LOB) **Ntext**, **Text**, **varchar(max)**, **nvarchar(max)**,  **varbinary(max)**, **Xml**, oder **Image** kann nicht als Schlüsselspalten für einen Index angegeben werden. Eine Sichtdefinition darf nicht enthalten sind, **Ntext**, **Text**, oder **Image** Spalten, auch wenn sie nicht in der CREATE INDEX-Anweisung verwiesen werden.  
  
 Sie können Indizes für Spalten mit dem CLR-benutzerdefinierten Typ erstellen, wenn durch den Typ Binärreihenfolgen unterstützt werden. Außerdem können Sie Indizes für berechnete Spalten erstellen, die als Methodenaufrufe aus einer Spalte mit dem benutzerdefinierten Typ definiert sind, vorausgesetzt, die Methoden sind als deterministisch markiert und führen keine Datenzugriffe durch. Weitere Informationen zum Indizieren von CLR-UDT-Spalten finden Sie unter [CLR-benutzerdefinierte Typen](../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md).  
  
 [ **ASC** | "DESC"]  
 Bestimmt für die entsprechende Indexspalte die aufsteigende oder absteigende Sortierreihenfolge. Die Standardeinstellung ist ASC.  
  
 UMFASSEN **(***Spalte* [ **,**... *n* ] **)**  
 Gibt die Nichtschlüsselspalten an, die zur Blattebene des nicht gruppierten Index hinzugefügt werden sollen. Der nicht gruppierte Index kann eindeutig oder nicht eindeutig sein.  
  
 Die Spaltennamen dürfen in der INCLUDE-Liste nicht wiederholt und nicht gleichzeitig als Schlüssel- und Nichtschlüsselspalten verwendet werden. Nicht gruppierte Indizes enthalten stets die Spalten des gruppierten Index, wenn ein gruppierter Index für die Tabelle definiert ist. Weitere Informationen finden Sie unter [Create Indexes with Included Columns](../../relational-databases/indexes/create-indexes-with-included-columns.md).  
  
 Mit Ausnahme von **text**, **ntext**und **image**sind alle Datentypen zulässig. Der Index erstellt oder neu erstellt, offline geschaltet werden muss (ONLINE = OFF), wenn eine der angegebenen Nichtschlüsselspalten sind **varchar(max)**, **nvarchar(max)**, oder **varbinary(max)** Daten Typen.  
  
 Bei berechneten Spalten, die deterministisch und präzise oder unpräzise sind, kann es sich um eingeschlossene Spalten handeln. Berechnete Spalten abgeleitet **Image**, **Ntext**, **Text**, **varchar(max)**, **nvarchar(max)**, **varbinary(max)**, und **Xml** Datentypen können in Nichtschlüsselspalten eingeschlossen werden, solange die Datentypen für die berechnete Spalte als eingeschlossene Spalte zulässig ist. Weitere Informationen finden Sie unter [Indexes on Computed Columns](../../relational-databases/indexes/indexes-on-computed-columns.md).  
  
 Informationen zum Erstellen eines XML-Indexes finden Sie unter [CREATE XML INDEX &#40; Transact-SQL &#41; ](../../t-sql/statements/create-xml-index-transact-sql.md).  
  
 WOBEI \<Filter_predicate > erstellt Sie einen gefilterten Index, indem Sie festlegen, welche Zeilen in den Index aufgenommen. Der gefilterte Index muss ein nicht gruppierter Index für eine Tabelle sein. Erstellt gefilterte Statistikdaten für die Datenzeilen im gefilterten Index.  
  
 Im Filterprädikat werden einfache Vergleichsoperatoren verwendet. Es darf darin nicht auf eine berechnete Spalte, eine UDT-Spalte, eine Spalte mit einem räumlichen Datentyp oder eine Spalten mit dem hierarchyID-Datentyp verwiesen werden. Vergleiche mit NULL-Literalen sind mit den Vergleichsoperatoren nicht zulässig. Verwenden Sie stattdessen den IS NULL-Operator und den IS NOT NULL-Operator.  
  
 Es folgen einige Beispiele für Filterprädikate für die `Production.BillOfMaterials`-Tabelle:  
  
 * `WHERE StartDate > '20000101' AND EndDate <= '20000630'`  
  
 * `WHERE ComponentID IN (533, 324, 753)`  
  
 * `WHERE StartDate IN ('20000404', '20000905') AND EndDate IS NOT NULL`  
  
 Gefilterte Indizes gelten nicht für XML-Indizes und Volltextindizes. Bei UNIQUE-Indizes müssen nur die ausgewählten Zeilen über eindeutige Indexwerte verfügen. Bei gefilterten Indizes ist die IGNORE_DUP_KEY-Option nicht zulässig.  
  
ON *Partition_scheme_name* **( *Column_name* )**  
**Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] und [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
 Gibt das Partitionsschema an, das die Dateigruppen definiert, denen die Partitionen eines partitionierten Index zugeordnet werden. Das Partitionsschema muss in der Datenbank vorhanden, durch Ausführen [CREATE PARTITION SCHEME](../../t-sql/statements/create-partition-scheme-transact-sql.md) oder [ALTER PARTITION SCHEME](../../t-sql/statements/alter-partition-scheme-transact-sql.md). *Column_name* gibt die Spalte für die ein partitionierter Index partitioniert werden. Diese Spalte muss den Datentyp, Länge, übereinstimmen und der Genauigkeit des Arguments der Partition, *Partition_scheme_name* verwendet. *Column_name* ist nicht auf die Spalten in der Indexdefinition beschränkt. Jede Spalte in der Basistabelle angegeben werden, außer beim Partitionieren von eines EINDEUTIGEN Indexes *Column_name* muss ausgewählt werden, die als eindeutige Schlüssel verwendet. Mit dieser Einschränkung kann [!INCLUDE[ssDE](../../includes/ssde-md.md)] die Eindeutigkeit der Schlüsselwerte in nur einer einzigen Partition überprüfen.  
  
> [!NOTE]  
> Beim Partitionieren eines nicht eindeutigen gruppierten Index fügt [!INCLUDE[ssDE](../../includes/ssde-md.md)] standardmäßig die Partitionierungsspalte zu der Liste der gruppierten Indexschlüssel hinzu, sofern sie dort noch nicht angegeben wurde. Beim Partitionieren eines nicht eindeutigen, nicht gruppierten Indexes fügt [!INCLUDE[ssDE](../../includes/ssde-md.md)] die Partitionierungsspalte als (eingeschlossene) Nichtschlüsselspalte des Indexes hinzu, sofern sie noch nicht angegeben wurde.  
  
 Wenn *Partition_scheme_name* oder *Dateigruppe* nicht angegeben wird und die Tabelle partitioniert ist, wird der Index in demselben Partitionsschema, mit der gleichen Partitionsspalte, wie die zugrunde liegende Tabelle platziert.  
  
> [!NOTE]  
> Sie können kein Partitionierungsschema für einen XML-Index angeben. Beim Partitionieren der Basistabelle verwendet der XML-Index dasselbe Partitionsschema wie die Tabelle.  
  
 Weitere Informationen zum Partitionieren von Indizes [Partitioned Tables and Indexes](../../relational-databases/partitions/partitioned-tables-and-indexes.md).  
  
 ON *Filegroup_name*  
 **Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Erstellt den angegebenen Index für die angegebene Dateigruppe. Wenn kein Speicherort angegeben und die Tabelle oder Sicht nicht partitioniert ist, verwendet der Index dieselbe Dateigruppe wie die zugrunde liegende Tabelle oder Sicht. Die Dateigruppe muss bereits vorhanden sein.  
  
 ON **"**Standard**"**  
 **Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] und [!INCLUDE[ssCurrent](../../includes/sssdsfull-md.md)].  
  
 Erstellt den angegebenen Index für die Standarddateigruppe.  
  
 Die Benennung default ist in diesem Kontext kein Schlüsselwort. Es ist ein Bezeichner für die Standarddateigruppe und muss begrenzt sein, wie in ON **"**Standard**"** oder ON **[**Standard**]**. Wenn "default" angegeben wird, muss die Option QUOTED_IDENTIFIER für die aktuelle Sitzung auf ON festgelegt sein. Dies ist die Standardeinstellung. Weitere Informationen finden Sie unter [SET QUOTED_IDENTIFIER &#40;Transact-SQL&#41;](../../t-sql/statements/set-quoted-identifier-transact-sql.md).  
  
 [FILESTREAM_ON { *Filestream_filegroup_name* | *Partition_scheme_name* | "NULL"}]  
 **Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Gibt die Platzierung der FILESTREAM-Daten für die Tabelle an, wenn ein gruppierter Index erstellt wird. Die FILESTREAM_ON-Klausel lässt zu, dass FILESTREAM-Daten in eine andere FILESTREAM-Dateigruppe oder ein anderes Partitionsschema verschoben werden.  
  
 *Filestream_filegroup_name* ist der Name einer FILESTREAM-Dateigruppe. Die Dateigruppe muss eine Datei, die für die Dateigruppe mit definiert haben eine [CREATE DATABASE](../../t-sql/statements/create-database-sql-server-transact-sql.md) oder [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql.md) Anweisung; andernfalls wird ein Fehler ausgelöst.  
  
 Wenn die Tabelle partitioniert ist, muss die FILESTREAM_ON-Klausel eingeschlossen werden und ein Partitionsschema von FILESTREAM-Dateigruppen angeben, das die gleiche Partitionsfunktion und die gleichen Partitionsspalten wie das Partitionsschema der Tabelle enthält. Andernfalls wird ein Fehler ausgelöst.  
  
 Wenn die Tabelle nicht partitioniert ist, kann die FILESTREAM-Spalte nicht partitioniert werden. Die FILESTREAM-Daten für die Tabelle müssen in einer einzigen Dateigruppe gespeichert werden, die in der FILESTREAM_ON-Klausel angegeben wird.  
  
 FILESTREAM_ON NULL kann in einer CREATE INDEX-Anweisung angegeben werden, wenn ein gruppierter Index erstellt wird und die Tabelle keine FILESTREAM-Spalte enthält.  
  
 Weitere Informationen finden Sie unter [FILESTREAM &#40;SQL Server&#41;](../../relational-databases/blob/filestream-sql-server.md).  
  
 **\<Objekt >:: =**  
  
 Gibt das vollqualifizierte oder nicht vollqualifizierte Objekt an, das indiziert werden soll.  
  
 *database_name*  
 Der Name der Datenbank.  
  
 *schema_name*  
 Der Name des Schemas, zu dem die Tabelle oder Sicht gehört.  
  
 *table_or_view_name*  
 Gibt den Namen der zu indizierenden Tabelle oder Sicht an.  
  
 Die Sicht muss mit SCHEMABINDING definiert werden, um einen Index für sie zu erstellten. Ein eindeutiger gruppierter Index muss für eine Sicht erstellt werden, bevor ein nicht gruppierter Index erstellt wird. Weitere Informationen zu indizierten Sichten finden Sie im Abschnitt mit den Hinweisen.  
  
 Beginnend mit [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], das Objekt eine Tabelle mit einem gruppierten columnstore-Index gespeichert werden kann.  
  
 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]unterstützt die drei Teilen bestehende Namensformat *Database_name***.** [*Schema_name*]**.** *Object_name* bei der *Database_name* wird von die aktuelle Datenbank oder der *Database_name* tempdb und den *Object_name*mit # beginnt.  
  
 **\<Relational_index_option >:: =**  
  
 Gibt die Optionen an, die beim Erstellen des Indexes verwendet werden sollen.  
  
 PAD_INDEX = {ON | **OFF** }  
 **Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] und [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
 Gibt die Auffüllung von Indizes an. Der Standardwert ist OFF.  
  
 ON  
 Der Prozentsatz des freien Speicherplatzes, der angegebenen *Fillfactor* auf die zwischenebenenseiten des Indexes angewendet wird.  
  
 Deaktivieren oder *Fillfactor* ist nicht angegeben.  
 Die Zwischenebenenseiten sind nahezu vollständig aufgefüllt. Allerdings ist ausreichend Speicherplatz vorhanden, um mindestens eine Zeile in der maximal für den Index möglichen Größe aufzunehmen, wenn der Schlüsselsatz auf den Zwischenseiten berücksichtigt wird.  
  
 Die Option PAD_INDEX ist nur dann hilfreich, wenn FILLFACTOR angegeben ist, da PAD_INDEX den durch FILLFACTOR angegebenen Prozentsatz verwendet. Wenn der für FILLFACTOR angegebene Prozentsatz nicht groß genug ist, um eine Zeile aufzunehmen, überschreibt [!INCLUDE[ssDE](../../includes/ssde-md.md)] diesen Prozentsatz intern, um das Minimum zuzulassen. Die Anzahl der Zeilen auf jeder Zwischenindexseite ist nie kleiner als zwei, unabhängig davon, wie Niedrig der Wert der *Fillfactor*.  
  
 In abwärtskompatibler Syntax ist WITH PAD_INDEX gleichwertig mit WITH PAD_INDEX = ON.  
  
 FILLFACTOR  **=**  *Fillfactor*  
 **Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] und [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
 Gibt einen Prozentsatz an, der angibt, wie weit das [!INCLUDE[ssDE](../../includes/ssde-md.md)] die Blattebene jeder Indexseite während der Indexerstellung oder -neuerstellung füllen soll. *FILLFACTOR* muss ein ganzzahliger Wert zwischen 1 und 100 sein. Wenn *Fillfactor* ist 100, der [!INCLUDE[ssDE](../../includes/ssde-md.md)] Indizes mit vollständig aufgefüllten Blattseiten erstellt.  
  
 Die FILLFACTOR-Einstellung gilt nur, wenn der Index erstellt oder neu erstellt wird. [!INCLUDE[ssDE](../../includes/ssde-md.md)] hält den angegebenen Prozentsatz des Speicherplatzes nicht dynamisch auf den Seiten frei. Verwenden Sie zum Anzeigen der füllfaktoreinstellung der [sys.indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md) -Katalogsicht angezeigt.  
  
> [!IMPORTANT]  
> Das Erstellen eines gruppierten Indexes mit einem FILLFACTOR-Wert unter 100 wirkt sich auf den Speicherplatz aus, den die Daten belegen, da [!INCLUDE[ssDE](../../includes/ssde-md.md)] die Daten beim Erstellen des gruppierten Indexes neu verteilt.  
  
 Weitere Informationen finden Sie unter [Angeben des Füllfaktors für einen Index](../../relational-databases/indexes/specify-fill-factor-for-an-index.md).  
  
 SORT_IN_TEMPDB = {ON | **OFF** }  
 **Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] und [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
 Gibt an, ob temporäre Sortierergebnisse in gespeichert **Tempdb**. Der Standardwert ist OFF.  
  
 ON  
 Die Zwischenergebnisse, die zum Erstellen des Indexes verwendet werden, sind in gespeicherten **Tempdb**. Dies kann die erforderliche Zeit zum Erstellen eines Indexes, wenn verringern **Tempdb** wird auf einem anderen Datenträgersatz befindet als die Benutzerdatenbank. Sie erhöht jedoch den Betrag an Speicherplatz, der während der Indexerstellung verwendet wird.  
  
 OFF  
 Die Zwischenergebnisse der Sortierung werden in derselben Datenbank gespeichert wie der Index.  
  
 Zusätzlich zu dem Speicherplatz, der in der Benutzerdatenbank zum Erstellen des Indexes erforderlich **Tempdb** ungefähr die gleiche Menge an zusätzlichem Speicherplatz zum Speichern der Zwischenergebnisse benötigen. Weitere Informationen finden Sie unter [SORT_IN_TEMPDB-Option für Indizes](../../relational-databases/indexes/sort-in-tempdb-option-for-indexes.md).  
  
 In abwärtskompatibler Syntax ist WITH SORT_IN_TEMPDB gleichwertig mit WITH SORT_IN_TEMPDB = ON.  
  
 IGNORE_DUP_KEY = {ON | **OFF** }  
 Gibt die Fehlermeldung an, wenn ein Einfügevorgang versucht, doppelte Schlüsselwerte in einen eindeutigen Index einzufügen. Die IGNORE_DUP_KEY-Option gilt nur für Einfügevorgänge nach dem Erstellen oder Neuerstellen des Index. Die Option hat keine Auswirkungen, bei der Ausführung [CREATE INDEX](../../t-sql/statements/create-index-transact-sql.md), [ALTER INDEX](../../t-sql/statements/alter-index-transact-sql.md), oder [UPDATE](../../t-sql/queries/update-transact-sql.md). Der Standardwert ist OFF.  
  
 ON  
 Eine Warnmeldung wird ausgegeben, wenn doppelte Schlüsselwerte in einen eindeutigen Index eingefügt werden. Es schlagen nur die Zeilen fehl, die gegen die Eindeutigkeitseinschränkung verstoßen.  
  
 OFF  
 Eine Fehlermeldung wird ausgegeben, wenn doppelte Schlüsselwerte in einen eindeutigen Index eingefügt werden. Für den gesamten INSERT-Vorgang wird ein Rollback ausgeführt.  
  
 IGNORE_DUP_KEY kann für Indizes, die für eine Sicht erstellt werden, nicht eindeutige Indizes, XML-Indizes, räumliche und gefilterte Indizes nicht auf ON festgelegt werden.  
  
 Um IGNORE_DUP_KEY anzuzeigen, verwenden Sie [sys.indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md).  
  
 In abwärtskompatibler Syntax ist WITH IGNORE_DUP_KEY gleichwertig mit WITH IGNORE_DUP_KEY = ON.  
  
 STATISTICS_NORECOMPUTE = {ON | **OFF**}  
 Gibt an, ob Verteilungsstatistiken neu berechnet werden. Der Standardwert ist OFF.  
  
 ON  
 Veraltete Indexstatistiken werden nicht automatisch neu berechnet.  
  
 OFF  
 Die automatischen Updates der Statistiken sind aktiviert.  
  
 Um das automatische Aktualisieren von Statistiken wiederherzustellen, müssen Sie STATISTICS_NORECOMPUTE auf OFF festlegen oder die UPDATE STATISTICS-Anweisung ohne die NORECOMPUTE-Klausel ausführen.  
  
> [!IMPORTANT]  
> Wenn Sie die automatische Neuberechnung von Verteilungsstatistiken deaktivieren, wählt der Abfrageoptimierer möglicherweise nicht die optimalen Ausführungspläne für Abfragen, an denen die Tabelle beteiligt ist.  
  
 In abwärtskompatibler Syntax ist WITH STATISTICS_NORECOMPUTE gleichwertig mit WITH STATISTICS_NORECOMPUTE = ON.  
  
STATISTICS_INCREMENTAL = {ON | **OFF** }  
Wenn **ON**, die Statistiken erstellt werden, pro Partition. Wenn **OFF**, wird die statistikstruktur gelöscht und [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] die Statistiken neu berechnet. Die Standardeinstellung ist **OFF**.  
  
 Wenn Statistiken pro Partition nicht unterstützt werden, wird die Option ignoriert und eine Warnung generiert. Inkrementelle Statistiken werden für folgende Statistiktypen nicht unterstützt:  
  
-   Statistiken, die mit Indizes erstellt wurden, die über keine Partitionsausrichtung mit der Basistabelle verfügen.  
-   Statistiken, die für lesbare sekundäre Always On-Datenbanken erstellt wurden.  
-   Statistiken, die für schreibgeschützte Datenbanken erstellt wurden.  
-   Statistiken, die für gefilterte Indizes erstellt wurden.  
-   Statistiken, die für Sichten erstellt wurden.  
-   Statistiken, die für interne Tabellen erstellt wurden.  
-   Statistiken, die mit räumlichen Indizes oder XML-Indizes erstellt wurden.  
  
DROP_EXISTING = {ON | **OFF** }  
Ist eine Option zum Löschen und erstellen Sie den vorhandenen gruppierten oder nicht gruppierten Index mit den Angaben in der geänderten Spalte neu, und behalten Sie den gleichen Namen für den Index an. Der Standardwert ist OFF.  
  
 ON  
 Gibt an, dass löschen und Neuerstellen des vorhandenen Indexes, mit dem gleichen Namen wie der Parameter muss *Index_name*.  
  
 OFF  
 Gibt an, nicht löschen und den vorhandenen Index neu erstellen. SQL Server wird einen Fehler angezeigt, wenn der angegebene Indexname bereits vorhanden ist.  
  
Mit DROP_EXISTING können Sie Folgendes ändern:  
  
-   Ein nicht gruppierter Rowstore-Index in einen gruppierten Rowstore-Index.  
  
Mit DROP_EXISTING können Sie nicht ändern:  
  
-   Ein gruppierter Rowstore-Index in einen nicht gruppierten Rowstore-Index.  
-   Ein gruppierter columnstore-Index mit jeder Art von Rowstore-Index.  
  
In abwärtskompatibler Syntax ist WITH DROP_EXISTING gleichwertig mit WITH DROP_EXISTING = ON.  
  
ONLINE = {ON | **OFF** }  
Gibt an, ob die zugrunde liegenden Tabellen und zugeordneten Indizes für Abfragen und Datenänderungen während des Indexvorgangs verfügbar sind. Der Standardwert ist OFF.  
  
> [!NOTE]  
> Onlineindexvorgänge sind nicht in jeder Edition von [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verfügbar. Eine Liste der Funktionen, die von den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Editionen unterstützt werden, finden Sie unter [Editionen und unterstütze Funktionen für den SQL Server 2016](../../sql-server/editions-and-supported-features-for-sql-server-2016.md).  
  
 ON  
 Lang andauernde Sperren werden nicht für die Dauer des Indexvorgangs aufrechterhalten. Während der Hauptphase des Indexvorgangs wird nur eine beabsichtigte freigegebene Sperre (IS) für die Quelltabelle aufrechterhalten. Dadurch können Abfragen oder Updates für die zugrunde liegende Tabelle und die Indizes fortgesetzt werden. Zu Beginn des Vorgangs wird für sehr kurze Zeit eine freigegebene Sperre (S) für das Quellobjekt aufrechterhalten. Am Ende des Vorgangs wird für die Quelle für kurze Zeit eine freigegebene Sperre (S) aktiviert, wenn ein nicht gruppierter Index erstellt wird. Eine Schemaänderungssperre (SCH-M) wird aktiviert, wenn ein gruppierter Index online erstellt oder gelöscht und wenn ein gruppierter oder nicht gruppierter Index neu erstellt wird. ONLINE kann nicht auf ON festgelegt werden, wenn ein Index auf einer lokalen temporären Tabelle erstellt wird.  
  
 OFF  
 Die Tabellensperren werden für die Dauer des Indexvorgangs angewendet. Ein Offlineindexvorgang, bei dem ein gruppierter Index erstellt, neu erstellt oder gelöscht bzw. ein nicht gruppierter Index neu erstellt oder gelöscht wird, aktiviert eine Schemaänderungssperre (SCH-M) für die Tabelle. Dadurch wird verhindert, dass Benutzer für die Dauer des Vorgangs auf die zugrunde liegende Tabelle zugreifen können. Ein Offlineindexvorgang, bei dem ein nicht gruppierter Index erstellt wird, aktiviert eine freigegebene Sperre (S) für die Tabelle. Dadurch werden Updates der zugrunde liegenden Tabelle verhindert. Lesevorgänge, wie SELECT-Anweisungen, sind jedoch zulässig.  
  
 Weitere Informationen finden Sie unter [wie Onlineindexvorgängen](../../relational-databases/indexes/how-online-index-operations-work.md).  
  
 Indizes, einschließlich Indizes für globale temporäre Tabellen, können mit den folgenden Ausnahmen online erstellt werden:  
  
-   XML-Index  
-   Index für eine lokale temporäre Tabelle.  
-   Eindeutiger gruppierter Anfangsindex für eine Sicht.  
-   Deaktivierte gruppierte Indizes.  
-   Gruppierter Index, sofern die zugrunde liegende Tabelle LOB-Datentypen enthält: **Image**, **Ntext**, **Text**, und räumliche Typen.  
-   **varchar(max)** und **varbinary(max)** Spalten nicht Teil eines Indexes sein. In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (beginnend mit [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]) und im [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)], wenn eine Tabelle enthält **varchar(max)** oder **varbinary(max)** Spalten ein gruppierter Index mit anderen Spalten möglich. erstellt oder neu erstellt, mit der **ONLINE** Option. [!INCLUDE[ssSDS](../../includes/sssds-md.md)]lässt nicht zu den **ONLINE** option, wenn die Basistabelle enthält **varchar(max)** oder **varbinary(max)** Spalten.  
  
Weitere Informationen finden Sie unter [Perform Index Operations Online](../../relational-databases/indexes/perform-index-operations-online.md).  
  
ALLOW_ROW_LOCKS = { **ON** | {OFF}  
**Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] und [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
 Gibt an, ob Zeilensperren zulässig sind. Der Standardwert ist ON.  
  
 ON  
 Zeilensperren sind beim Zugriff auf den Index zulässig. Das [!INCLUDE[ssDE](../../includes/ssde-md.md)] bestimmt, wann Zeilensperren verwendet werden.  
  
 OFF  
 Zeilensperren werden nicht verwendet.  
  
ALLOW_PAGE_LOCKS = { **ON** | {OFF}  
**Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] und [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
 Gibt an, ob Seitensperren zulässig sind. Der Standardwert ist ON.  
  
 ON  
 Seitensperren sind beim Zugriff auf den Index zulässig. Das [!INCLUDE[ssDE](../../includes/ssde-md.md)] bestimmt, wann Seitensperren verwendet werden.  
  
 OFF  
 Seitensperren werden nicht verwendet.  
  
MAXDOP = *Max_degree_of_parallelism*  
**Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] und [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
 Überschreibt die **Max. Grad an Parallelität** Konfigurationsoption für die Dauer des Indexvorgangs. Weitere Informationen finden Sie unter [Konfigurieren der Serverkonfigurationsoption Max. Grad an Parallelität](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md). Sie können mit MAXDOP die Anzahl der Prozessoren begrenzen, die bei der Ausführung paralleler Pläne verwendet werden. Maximal sind 64 Prozessoren zulässig.  
  
 *Max_degree_of_parallelism* sind möglich:  
  
 1  
 Unterdrückt das Generieren paralleler Pläne.  
  
 \>1  
 Beschränkt die maximale Anzahl der Prozessoren, die bei einem parallelen Indexvorgang verwendet werden, je nach aktueller Systemauslastung auf die angegebene Zahl oder einen niedrigeren Wert.  
  
 0 (Standard)  
 Verwendet abhängig von der aktuellen Systemarbeitsauslastung die tatsächliche Anzahl von Prozessoren oder weniger Prozessoren.  
  
 Weitere Informationen finden Sie unter [Konfigurieren von Parallelindexvorgängen](../../relational-databases/indexes/configure-parallel-index-operations.md).  
  
> [!NOTE]  
> Parallele Indexvorgänge sind nicht verfügbar in jeder Edition von [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Eine Liste der Funktionen, die von den Editionen unterstützt werden [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], finden Sie unter [Editionen und unterstützte Funktionen für SQL Server 2016](../../sql-server/editions-and-supported-features-for-sql-server-2016.md) und [Editionen und unterstützte Funktionen für SQL Server-2017](../../sql-server/editions-and-components-of-sql-server-2017.md).  
  
 DATA_COMPRESSION  
 Gibt die Datenkomprimierungsoption für den angegebenen Index, die Partitionsnummer oder den Bereich von Partitionen an. Folgende Optionen stehen zur Verfügung:  
  
 Keine  
 Der Index oder die angegebenen Partitionen werden nicht komprimiert.  
  
 ROW  
 Der Index oder die angegebenen Partitionen werden mit Zeilenkomprimierung komprimiert.  
  
 PAGE  
 Der Index oder die angegebenen Partitionen werden mit Seitenkomprimierung komprimiert.  
  
 Weitere Informationen zur Komprimierung finden Sie unter [Datenkomprimierung](../../relational-databases/data-compression/data-compression.md).  
  
AUF PARTITIONEN **(** { \<Partition_number_expression > | \<Bereich >} [ **,**... *n* ] **)**      
**Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] und [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
 Gibt die Partitionen an, für die die DATA_COMPRESSION-Einstellung gilt. Wenn der Index nicht partitioniert ist, erzeugt das ON PARTITIONS-Argument einen Fehler. Wenn die ON PARTITIONS-Klausel nicht angegeben wird, gilt die DATA_COMPRESSION-Option für alle Partitionen eines partitionierten Indexes.  
  
 \<Partition_number_expression > kann auf folgende Weise angegeben werden:  
  
-   Geben Sie die Nummer der Partition an, beispielsweise: ON PARTITIONS (2).  
-   Geben Sie die Partitionsnummern mehrerer einzelner Partitionen durch Trennzeichen getrennt an, beispielsweise: ON PARTITIONS (1, 5).  
-   Geben Sie sowohl Bereiche als auch einzelne Partitionen an, beispielsweise: ON PARTITIONS (2, 4, 6 TO 8).  
  
 \<Range > können durch das Wort TO, z. B. getrennte Partitionsnummern angegeben werden: ON PARTITIONS (6 TO 8).  
  
 Wenn Sie für verschiedene Partitionen unterschiedliche Datenkomprimierungstypen festlegen möchten, geben Sie die Option DATA_COMPRESSION mehrmals an, beispielsweise:  
 
```  
REBUILD WITH   
(  
DATA_COMPRESSION = NONE ON PARTITIONS (1),   
DATA_COMPRESSION = ROW ON PARTITIONS (2, 4, 6 TO 8),   
DATA_COMPRESSION = PAGE ON PARTITIONS (3, 5)  
);  
```  
  
## <a name="remarks"></a>Hinweise  
 Die CREATE INDEX-Anweisung wird so optimiert wie jede andere Abfrage. Um weniger E/A-Vorgänge zu benötigen, entscheidet der Abfrageprozessor möglicherweise, einen anderen Index zu scannen, statt einen Tabellenscan auszuführen. Der Sortiervorgang wird in einigen Situationen möglicherweise umgangen. Auf einem Multiprozessorcomputer kann CREATE INDEX mehr Prozessoren verwenden, um die mit dem Erstellen des Index zusammenhängenden Scan- und Sortiervorgänge auszuführen. Dies geschieht in gleicher Weise wie für andere Abfragen. Weitere Informationen finden Sie unter [Konfigurieren von Parallelindexvorgängen](../../relational-databases/indexes/configure-parallel-index-operations.md).  
  
 Der Indexerstellungsvorgang kann minimal protokolliert werden, wenn das Wiederherstellungsmodell der Datenbank auf die massenprotokollierte oder einfache Wiederherstellung festgelegt ist.  
  
 Indizes können für temporäre Tabellen erstellt werden. Wenn die Tabelle gelöscht oder die Sitzung beendet wird, werden die Indizes gelöscht.  
  
 Durch Indizes werden erweiterte Eigenschaften unterstützt.  
  
## <a name="clustered-indexes"></a>Gruppierte Indizes  
 Für das Erstellen eines gruppierten Index für eine Tabelle (Heap) oder das Löschen und Neuerstellen eines vorhandenen gruppierten Index muss zusätzlicher Arbeitsbereich in der Datenbank verfügbar sein, um das Sortieren von Daten und das Speichern einer temporären Kopie der ursprünglichen Tabelle oder von vorhandenen gruppierten Indexdaten zu ermöglichen. Weitere Informationen zu gruppierten Indizes finden Sie unter [gruppierte Indizes erstellen](../../relational-databases/indexes/create-clustered-indexes.md).  
  
## <a name="nonclustered-indexes"></a>Nicht gruppierte Indizes  
 Beginnend mit [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] und [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)], Sie können einen nicht gruppierten Index für eine Tabelle als gruppierten columnstore-Index gespeicherte erstellen. Wenn Sie zuerst einen nicht gruppierten Index für eine Tabelle gespeicherten erstellen als Heap oder gruppierten Index, der Index bleiben erhalten, wenn die Tabelle später in einen gruppierten columnstore-Index zu konvertieren. Es ist auch nicht notwendig, den nicht gruppierten Index zu löschen, wenn Sie den gruppierten columnstore-Index neu erstellen.  
  
 Einschränkungen:  
  
-   Die FILESTREAM_ON-Option gilt nicht, wenn Sie einen nicht gruppierten Index für eine Tabelle als gruppierten columnstore-Index gespeicherte erstellen.  
  
## <a name="unique-indexes"></a>Eindeutige Indizes  
 Wenn ein eindeutiger Index vorhanden ist, prüft [!INCLUDE[ssDE](../../includes/ssde-md.md)] jedes Mal, wenn Daten mithilfe von Einfügevorgängen hinzugefügt werden, auf doppelte Werte. Für Einfügevorgänge, die doppelte Schlüsselwerte generieren würden, wird ein Rollback ausgeführt. In [!INCLUDE[ssDE](../../includes/ssde-md.md)] wird in diesem Fall eine Fehlermeldung angezeigt. Dies trifft auch dann zu, wenn beim Einfügevorgang viele Zeilen geändert werden, aber nur ein doppelter Wert verursacht wird. Wenn versucht wird, Daten einzugeben, für die ein eindeutiger Index vorhanden ist, und die IGNORE_DUP_KEY-Klausel auf ON festgelegt ist, schlagen nur die Zeilen fehl, die den UNIQUE-Index verletzen.  
  
## <a name="partitioned-indexes"></a>Partitionierte Indizes  
 Partitionierte Indizes werden ähnlich wie partitionierte Tabellen erstellt und verwaltet. Aber wie gewöhnliche Indizes werden sie wie separate Datenobjekte behandelt. Sie können einen partitionierten Index für eine nicht partitionierte Tabelle erstellen, und Sie können einen nicht partitionierten Index für eine partitionierte Tabelle erstellen.  
  
 Wenn Sie einen Index für eine partitionierte Tabelle erstellen und keine Dateigruppe angeben, in die der Index platziert werden soll, wird der Index auf die gleiche Weise partitioniert wie die zugrunde liegende Tabelle. Der Grund hierfür ist, dass Indizes standardmäßig in dieselben Dateigruppen wie die zugrunde liegenden Tabellen platziert werden. Bei partitionierten Tabellen werden Indizes in dasselbe Partitionsschema platziert, das dieselben Partitionierungsspalten verwendet. Wenn der Index das gleiche Partitionsschema und Partitionierungsspalte wie die Tabelle verwendet, wird der Index *ausgerichtet* mit der Tabelle.  
  
> [!WARNING]  
> Das Erstellen bzw. Neuerstellen von nicht ausgerichteten Indizes für eine Tabelle mit mehr als 1.000 Partitionen ist möglich, wird aber nicht unterstützt. Dies hätte Leistungseinbußen oder eine zu hohe Speicherauslastung während der Vorgänge zur Folge. Es empfiehlt sich, bei mehr als 1.000 Partitionen nur ausgerichtete Indizes zu verwenden.  
  
 Beim Partitionieren eines nicht eindeutigen gruppierten Index fügt [!INCLUDE[ssDE](../../includes/ssde-md.md)] standardmäßig alle Partitionierungsspalten zu der Liste der gruppierten Indexschlüssel hinzu, sofern sie dort noch nicht angegeben wurden.  
  
 Indizierte Sichten können für partitionierte Tabellen auf die gleiche Weise wie Indizes für Tabellen erstellt werden. Weitere Informationen zu partitionierten Indizes finden Sie unter [Partitioned Tables and Indexes](../../relational-databases/partitions/partitioned-tables-and-indexes.md).  
  
 In [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], Statistiken nicht durch das Scannen aller Zeilen in der Tabelle aus, wenn ein partitionierter Index erstellt oder neu erstellt wird erstellt. Der Abfrageoptimierer generiert stattdessen Statistiken mithilfe des Standardalgorithmus zur Stichprobenentnahme. Um Statistiken zu partitionierten Indizes durch das Scannen aller Zeilen in der Tabelle abzurufen, verwenden Sie CREATE STATISTICS oder UPDATE STATISTICS mit der FULLSCAN-Klausel.  
  
## <a name="filtered-indexes"></a>Gefilterten Indizes  
 Ein gefilterter Index ist ein optimierter nicht gruppierter Index, der sich für Abfragen eignet, mit denen ein kleiner Prozentsatz von Zeilen in einer Tabelle ausgewählt wird. Es wird ein Filterprädikat verwendet, um einen Teil der Daten in der Tabelle zu indizieren. Ein gut entworfener gefilterter Index kann die Abfrageleistung verbessern, den Speicheraufwand verringern und Wartungskosten reduzieren.  
  
### <a name="required-set-options-for-filtered-indexes"></a>Erforderliche SET-Optionen für gefilterte Indizes  
 Die SET-Optionen in der Spalte Erforderlicher Wert sind immer dann erforderlich, wenn eine der folgenden Bedingungen auftritt:  
  
-   Es wird ein gefilterter Index erstellt.  
-   Ein INSERT-, UPDATE-, DELETE- oder MERGE-Vorgang ändert die Daten in einem gefilterten Index.  
-   Der gefilterte Index wird vom Abfrageoptimierer verwendet, um den Abfrageplan zu erstellen.  
  
    |SET-Optionen|Erforderlicher Wert|Standardserverwert|Default<br /><br /> OLE DB- und ODBC-Wert|Default<br /><br /> DB-Library-Wert|  
    |-----------------|--------------------|--------------------------|---------------------------------------|-----------------------------------|  
    |ANSI_NULLS|ON|ON|ON|OFF|  
    |ANSI_PADDING|ON|ON|ON|OFF|  
    |ANSI_WARNINGS*|ON|ON|ON|OFF|  
    |ARITHABORT|ON|ON|OFF|OFF|  
    |CONCAT_NULL_YIELDS_NULL|ON|ON|ON|OFF|  
    |NUMERIC_ROUNDABORT|OFF|OFF|OFF|OFF|  
    |QUOTED_IDENTIFIER|ON|ON|ON|OFF|   
  
     *Durch Festlegen von ANSI_WARNINGS auf ON wird implizit ARITHABORT auf ON festgelegt, wenn der Kompatibilitätsgrad der Datenbank auf 90 oder höher festgelegt ist. Wird der Kompatibilitätsgrad der Datenbank auf 80 oder niedriger festgelegt, muss die ARITHABORT-Option explizit auf ON festgelegt werden.  
  
 Wenn die SET-Optionen falsch sind, können die folgenden Bedingungen auftreten:  
  
-   Der gefilterte Index wird nicht erstellt.  
-   [!INCLUDE[ssDE](../../includes/ssde-md.md)] generiert einen Fehler und führt ein Rollback aller INSERT-, UPDATE-, DELETE- oder MERGE-Anweisungen aus, die im Index gespeicherte Daten ändern.  
-   Der Abfrageoptimierer berücksichtigt den Index des Abfrageausführungsplans von Transact-SQL-Anweisungen nicht.  
  
 Weitere Informationen zu gefilterten Indizes finden Sie unter [Create Filtered Indexes](../../relational-databases/indexes/create-filtered-indexes.md).  
  
## <a name="spatial-indexes"></a>Räumliche Indizes  
 Informationen zu räumlichen Indizes finden Sie unter [CREATE SPATIAL INDEX &#40; Transact-SQL &#41; ](../../t-sql/statements/create-spatial-index-transact-sql.md) und [Übersicht über räumliche Indizes](../../relational-databases/spatial/spatial-indexes-overview.md).  
  
## <a name="xml-indexes"></a>XML-Indizes  
 Informationen zu XML finden Sie unter Indizes [CREATE XML INDEX &#40; Transact-SQL &#41; ](../../t-sql/statements/create-xml-index-transact-sql.md) und [XML Indizes &#40; SQLServer &#41; ](../../relational-databases/xml/xml-indexes-sql-server.md).  
  
## <a name="index-key-size"></a>Indexschlüsselgröße  
 Die maximale Größe für einen Indexschlüssel beträgt 900 Bytes für einen gruppierten Index und 1.700 Bytes für einen nicht gruppierten Index. (Vor dem [!INCLUDE[ssSDS](../../includes/sssds-md.md)] V12 und [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] der Grenzwert wurde immer 900 Bytes.) Indizes für **Varchar** Spalten, die die Byte-Grenze überschreiten können erstellt werden, wenn die vorhandenen Daten in den Spalten nicht den Grenzwert zum Zeitpunkt länger der Index erstellt als wird; allerdings nachfolgende INSERT- oder Update-Aktionen für die Spalten, die dazu führen, dass die Gesamtgröße größer sein als der Grenzwert schlägt fehl. Der Indexschlüssel eines gruppierten Indexes kann keine Spalten des Datentyps **varchar** enthalten, bei denen Daten in der Zuordnungseinheit ROW_OVERFLOW_DATA vorhanden sind. Wird ein gruppierter Index für eine **varchar**-Spalte erstellt, bei der in der Zuordnungseinheit IN_ROW_DATA Daten vorhanden sind, erzeugen alle nachfolgenden Einfügungen und Updates der Spalte einen Fehler, bei der diese Daten aus der Zeile entfernt werden.  
  
 Nicht gruppierte Indizes können Nichtschlüsselspalten auf der Blattebene des Indexes enthalten. Diese Spalten werden nicht berücksichtigt, indem Sie die [!INCLUDE[ssDE](../../includes/ssde-md.md)] bei der Berechnung der Größe des Indexschlüssels. Weitere Informationen finden Sie unter [Create Indexes with Included Columns](../../relational-databases/indexes/create-indexes-with-included-columns.md).  
  
> [!NOTE]  
> Falls beim Partitionieren der Tabellen die Partitionierungsschlüsselspalten nicht bereits in einem nicht eindeutigen gruppierten Index vorhanden sind, werden Sie mithilfe von [!INCLUDE[ssDE](../../includes/ssde-md.md)] dem Index hinzugefügt. Die kombinierte Größe der indizierten Spalten (eingeschlossene Spalten werden nicht gezählt), zzgl. beliebiger hinzugefügter Partitionierungsspalten dürfen 1800 Byte in einem nicht eindeutigen gruppierten Index nicht übersteigen.  
  
## <a name="computed-columns"></a>Berechnete Spalten  
 Indizes können für berechnete Spalten erstellt werden. Zudem können berechnete Spalten die Eigenschaft PERSISTED besitzen. Das bedeutet, dass [!INCLUDE[ssDE](../../includes/ssde-md.md)] die berechneten Werte in der Tabelle speichert und sie aktualisiert, wenn andere Spalten, von denen die berechnete Spalte abhängt, aktualisiert werden. [!INCLUDE[ssDE](../../includes/ssde-md.md)] verwendet diese persistenten Werte, wenn ein Index für die Spalte erstellt wird und wenn in einer Abfrage auf den Index verwiesen wird.  
  
 Zum Indizieren einer berechneten Spalte muss diese deterministisch und präzise sein. Allerdings wird mithilfe der PERSISTED-Eigenschaft der Typ der indizierbaren berechneten Spalten um Folgendes erweitert:  
  
-   Auf [!INCLUDE[tsql](../../includes/tsql-md.md)] und CLR-Funktionen basierte berechnete Spalten und Methoden des CLR-benutzerdefinierten Typs, die vom Benutzer als deterministisch markiert sind.  
-   Berechnete Spalten, die auf Ausdrücken basieren, die gemäß der Definition von [!INCLUDE[ssDE](../../includes/ssde-md.md)] deterministisch, aber unpräzise sind.  
  
 Für persistente berechnete Spalten müssen die folgenden SET-Optionen wie im vorherigen Abschnitt zu den erforderlichen SET-Optionen für indizierte Sichten dargestellt festgelegt werden.  
  
 Die jeweilige UNIQUE- oder PRIMARY KEY-Einschränkung kann eine berechnete Spalte enthalten, sofern diese alle Bedingungen für das Indizieren erfüllt. Die berechnete Spalte muss insbesondere deterministisch und präzise oder deterministisch und persistent sein. Weitere Informationen zum Determinismus finden Sie unter [Deterministic and Nondeterministic Functions](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md).  
  
 Berechnete Spalten abgeleitet **Image**, **Ntext**, **Text**, **varchar(max)**, **nvarchar(max)**, **varbinary(max)**, und **Xml** Daten können Typen werden als indiziert eine Schlüsselspalte oder eingeschlossene Nichtschlüsselspalte als Datentyp der berechneten Spalte als indexschlüsselspalte oder Nichtschlüsselspalte zulässig ist. Sie können keine z. B. einen primären XML-Index erstellen, für eine berechnete **Xml** Spalte. Wenn der Indexschlüssel die zulässige Größe von 900 Byte überschreitet, wird eine Warnmeldung angezeigt.  
  
 Das Erstellen eines Indexes für eine berechnete Spalte kann bei einem Einfüge- oder Updatevorgang einen Fehler erzeugen, wenn der Einfüge- oder Updatevorgang zuvor funktioniert hat. Ein solcher Fehler tritt möglicherweise auf, wenn die berechnete Spalte einen arithmetischen Fehler zur Folge hat. In der folgenden Tabelle wird zum Beispiel die `c`-Anweisung erfolgreich ausgeführt, obwohl die berechnete Spalte `INSERT` einen arithmetischen Fehler zur Folge hat.  
  
```sql  
CREATE TABLE t1 (a int, b int, c AS a/b);  
INSERT INTO t1 VALUES (1, 0);  
```  
  
 Wenn Sie allerdings nach dem Erstellen der Tabelle einen Index für die berechnete Spalte `c` erstellen, meldet die gleiche `INSERT`-Anweisung einen Fehler.  
  
```sql  
CREATE TABLE t1 (a int, b int, c AS a/b);  
CREATE UNIQUE CLUSTERED INDEX Idx1 ON t1(c);  
INSERT INTO t1 VALUES (1, 0);  
```  
  
 Weitere Informationen finden Sie unter [Indexes on Computed Columns](../../relational-databases/indexes/indexes-on-computed-columns.md).  
  
## <a name="included-columns-in-indexes"></a>Eingeschlossene Spalten in Indizes  
 Nichtschlüsselspalten werden als eingeschlossene Spalten bezeichnet und können zur Blattebene eines nicht gruppierten Index hinzugefügt werden, um die Abfrageleistung durch Abdecken der Abfrage zu verbessern. Das heißt, alle Spalten, auf die in der Abfrage verwiesen wird, sind im Index als Schlüssel- oder Nichtschlüsselspalten enthalten. Dadurch kann der Abfrageoptimierer alle erforderlichen Informationen über einen Indexscan suchen. Es erfolgt kein Zugriff auf die Daten der Tabelle oder des gruppierten Index. Weitere Informationen finden Sie unter [Create Indexes with Included Columns](../../relational-databases/indexes/create-indexes-with-included-columns.md).  
  
## <a name="specifying-index-options"></a>Angeben von Indexoptionen  
 Mit [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] wurden neue Indexoptionen eingeführt. Außerdem werden die Optionen auf andere Weise angegeben. In abwärtskompatibler Syntax ist WITH *Option_name* ist gleichbedeutend mit WITH **(** \<Option_name > **= ON)**. Beim Festlegen von Indexoptionen gelten folgende Regeln: 
  
-   Neue Indexoptionen können nur angegeben werden, mithilfe von WITH (***Option_name* = ON | OFF**).  
-   Optionen können nicht mithilfe der abwärtskompatiblen und der neuen Syntax in derselben Anweisung angegeben werden. Z. B. Angeben von WITH (**DROP_EXISTING, ONLINE = ON**) bewirkt, dass die Anweisung fehlschlägt.  
-   Wenn Sie einen XML-Index erstellen, müssen die Optionen angegeben werden, mithilfe von WITH (***Option_name*= ON | OFF**).  
  
## <a name="dropexisting-clause"></a>DROP_EXISTING (Klausel)  
 Mit der DROP_EXISTING-Klausel können Sie den Index neu erstellen, Spalten hinzufügen oder löschen, Optionen ändern, die Sortierreihenfolge für Spalten ändern sowie das Partitionsschema oder die Dateigruppe ändern.  
  
 Wenn der Index eine PRIMARY KEY- oder UNIQUE-Einschränkung erzwingt und die Indexdefinition in keiner Weise geändert wurde, wird der Index gelöscht und neu erstellt. Dabei wird die vorhandene Einschränkung beibehalten. Wenn die Indexdefinition jedoch geändert wird, schlägt die Anweisung fehl. Zum Ändern der Definition einer PRIMARY KEY- oder UNIQUE-Einschränkung müssen Sie die Einschränkung löschen und eine Einschränkung mit der neuen Definition hinzufügen.  
  
 Die DROP_EXISTING-Klausel erhöht die Leistung beim Neuerstellen eines gruppierten Index (mit der gleichen oder einer anderen Schlüsselmenge) für eine Tabelle, die auch nicht gruppierte Indizes besitzt. Die DROP_EXISTING-Klausel ersetzt die Ausführung einer DROP INDEX-Anweisung für den alten gruppierten Index mit anschließender Ausführung einer CREATE INDEX-Anweisung für den neuen gruppierten Index. Die nicht gruppierten Indizes werden einmal neu erstellt, dies aber nur dann, wenn die Indexdefinition geändert wurde. Die DROP_EXISTING-Klausel erstellt die nicht gruppierten Indizes nicht neu, wenn die Indexdefinition denselben Indexnamen, dieselben Schlüssel- und Partitionsspalten, dasselbe Eindeutigkeitsattribut und dieselbe Sortierreihenfolge wie der ursprüngliche Index aufweist.  
  
 Unabhängig davon, ob die nicht gruppierten Indizes neu erstellt werden, verbleiben sie immer in ihren ursprünglichen Dateigruppen oder Partitionsschemas und verwenden die ursprünglichen Partitionsfunktionen. Wenn ein gruppierter Index in einer anderen Dateigruppe oder einem anderen Partitionsschema neu erstellt wird, werden die nicht gruppierten Indizes nicht an den neuen Standort des gruppierten Index verschoben. Daher können auch die nicht gruppierten Indizes, die zuvor mit dem gruppierten Index ausgerichtet waren, möglicherweise nicht mehr damit ausgerichtet sein. Weitere Informationen zur partitionierten Indexausrichtung finden Sie unter .  
  
 Die DROP_EXISTING-Klausel sortiert die Daten nicht erneut, wenn dieselben Indexschlüsselspalten in derselben Reihenfolge und mit derselben aufsteigenden oder absteigenden Reihenfolge verwendet werden, es sei denn, in der Indexanweisung ist ein nicht gruppierter Index angegeben und die ONLINE-Option ist auf OFF festgelegt. Wenn der gruppierte Index deaktiviert ist, muss der CREATE INDEX WITH DROP_EXISTING-Vorgang mit der ONLINE-Einstellung OFF durchgeführt werden. Wenn ein nicht gruppierter Index deaktiviert ist und keinem deaktivierten gruppierten Index zugeordnet ist, kann der CREATE INDEX WITH DROP_EXISTING-Vorgang mit der ONLINE-Einstellung OFF oder ON durchgeführt werden.  
  
 Wenn Indizes mit 128 oder mehr Blöcken gelöscht oder neu erstellt werden, verzögert [!INCLUDE[ssDE](../../includes/ssde-md.md)] die eigentlichen Seitenzuordnungsaufhebungen und die zugehörigen Sperren bis zu einem Zeitpunkt nach dem Transaktionscommit.  
  
## <a name="online-option"></a>ONLINE (Option)  
 Die folgenden Regeln gelten für das Durchführen von Onlineindexvorgängen:  
  
-   Die zugrunde liegende Tabelle kann nicht geändert, abgeschnitten oder gelöscht werden, wenn ein Onlineindexvorgang verarbeitet wird.  
-   Beim Indexvorgang ist zusätzlicher temporärer Speicherplatz erforderlich.  
-   Onlinevorgänge können für partitionierte Indizes und Indizes durchgeführt werden, die persistente berechnete Spalten oder eingeschlossene Spalten enthalten.  
  
 Weitere Informationen finden Sie unter [Perform Index Operations Online](../../relational-databases/indexes/perform-index-operations-online.md).  
  
## <a name="row-and-page-locks-options"></a>Zeilen- und Seitensperren (Optionen)  
 Wenn ALLOW_ROW_LOCKS = ON und ALLOW_PAGE_LOCK = ON ist, sind beim Zugreifen auf den Index Sperren auf Zeilen-, Seiten- und Tabellenebene zulässig. Das [!INCLUDE[ssDE](../../includes/ssde-md.md)] wählt die geeignete Sperre aus und kann die Sperre von einer Zeilen- oder Seitensperre auf eine Tabellensperre ausweiten.  
  
 Wenn ALLOW_ROW_LOCKS = OFF und ALLOW_PAGE_LOCK = OFF ist, ist beim Zugreifen auf den Index nur eine Sperre auf Tabellenebene zulässig.  
  
## <a name="viewing-index-information"></a>Anzeigen von Indexinformationen  
 Informationen zu Indizes können Sie mithilfe von Katalogsichten, Systemfunktionen und gespeicherten Systemprozeduren zurückgeben.  
  
## <a name="data-compression"></a>Datenkomprimierung  
 Die datenkomprimierung wird in diesem Thema beschriebenen [Datenkomprimierung](../../relational-databases/data-compression/data-compression.md). Die folgenden wichtigen Punkte sind zu berücksichtigen:  
  
-   Die Komprimierung kann es ermöglichen, dass mehr Zeilen auf einer Seite gespeichert werden, die maximale Zeilengröße wird durch sie allerdings nicht geändert.  
-   Nicht-Blattseiten eines Index sind nicht seitenkomprimiert, können jedoch zeilenkomprimiert sein.  
-   Jeder nicht gruppierte Index verfügt über eine eigenen Komprimierungseinstellung und erbt die Komprimierungseinstellung nicht von der zugrunde liegenden Tabelle.  
-   Wenn ein gruppierter Index auf einem Heap erstellt wird, erbt der gruppierte Index den Komprimierungsstatus des Heaps, sofern kein anderer Komprimierungsstatus angegeben wird.  
  
 Für partitionierte Indizes gelten die folgenden Einschränkungen:  
  
-   Sie können die Komprimierungseinstellung einer einzelnen Partition nicht ändern, wenn die Tabelle nicht ausgerichtete Indizes aufweist.  
-   Die ALTER INDEX \<Index >... REBUILD PARTITION ...-Syntax wird die angegebene Partition des Indexes neu erstellt.  
-   Die ALTER INDEX \<Index >... REBUILD WITH ...-Syntax werden alle Partitionen des Indexes neu erstellt.  
  
 Mit der gespeicherten Prozedur [sp_estimate_data_compression_savings](../../relational-databases/system-stored-procedures/sp-estimate-data-compression-savings-transact-sql.md) können Sie einschätzen, wie sich eine Änderung des Komprimierungsstatus auf eine Tabelle, einen Index oder eine Partition auswirkt.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die ALTER-Berechtigung in der Tabelle oder Sicht. Der Benutzer muss ein Mitglied der festen Serverrolle **sysadmin** bzw. der festen Datenbankrollen **db_ddladmin** und **db_owner** sein.  
  
## <a name="limitations-and-restrictions"></a>Einschränkungen  
 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]und [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], Sie können nicht erstellt werden:  
  
-   Ein gruppierter oder nicht gruppierter Rowstore-Index für eine Datawarehouse-Tabelle, wenn ein columnstore-Index ist bereits vorhanden. Dieses Verhalten unterscheidet sich von SMP [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] können Rowstore und columnstore-Indizes für dieselbe Tabelle koexistieren.  
-   Einen Index kann nicht für eine Sicht erstellt werden.  
  
## <a name="metadata"></a>Metadaten  
 Informationen zu vorhandenen Indizes können, können Sie Abfragen der [sys.indexes &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md) -Katalogsicht angezeigt.  
  
## <a name="version-notes"></a>Die Anmerkungen zu dieser Version  
 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]unterstützt keine Dateigruppe und die Filestream-Optionen.  
  
## <a name="examples-all-versions-uses-the-adventureworks-database"></a>Beispiele: Alle Versionen. Wird die AdventureWorks-Datenbank verwendet.  
  
### <a name="a-create-a-simple-nonclustered-rowstore-index"></a>A. Erstellen eines einfachen nicht gruppierten Rowstore-Indexes  
 Die folgenden Beispiele erstellen Sie einen nicht gruppierten Index auf die `VendorID` Spalte die `Purchasing.ProductVendor` Tabelle.  
  
```sql  
CREATE INDEX IX_VendorID ON ProductVendor (VendorID);  
CREATE INDEX IX_VendorID ON dbo.ProductVendor (VendorID DESC, Name ASC, Address DESC);  
CREATE INDEX IX_VendorID ON Purchasing..ProductVendor (VendorID);  
```  
  
### <a name="b-create-a-simple-nonclustered-rowstore-composite-index"></a>B. Erstellen Sie einen zusammengesetzten einfachen nicht gruppierten Rowstore-index  
 Das folgende Beispiel erstellt einen nicht gruppierten zusammengesetzten Index für die `SalesQuota` und `SalesYTD` Spalten von der `Sales.SalesPerson` Tabelle.  
  
```sql  
CREATE NONCLUSTERED INDEX IX_SalesPerson_SalesQuota_SalesYTD ON Sales.SalesPerson (SalesQuota, SalesYTD);  
```  
  
### <a name="c-create-an-index-on-a-table-in-another-database"></a>C. Erstellen Sie einen Index für eine Tabelle in einer anderen Datenbank  
 Im folgende Beispiel erstellt einen nicht gruppierten Index für die `VendorID` Spalte die `ProductVendor` -Tabelle in der `Purchasing` Datenbank.  
  
```sql  
CREATE CLUSTERED INDEX IX_ProductVendor_VendorID ON Purchasing..ProductVendor (VendorID);   
```  
  
### <a name="d-add-a-column-to-an-index"></a>D. Hinzufügen einer Spalte auf einen index  
 Das folgende Beispiel erstellt Index IX_FF mit zwei Spalten aus das "Dbo". FactFinance-Tabelle.  Die nächste Anweisung erstellt den Index mit der eine weitere Spalte neu und behält den vorhandenen Namen.  
  
```sql  
CREATE INDEX IX_FF ON dbo.FactFinance ( FinanceKey ASC, DateKey ASC );  
  
--Rebuild and add the OrganizationKey  
CREATE INDEX IX_FF ON dbo.FactFinance ( FinanceKey, DateKey, OrganizationKey DESC)  
WITH ( DROP_EXISTING = ON );  
 ```  
  
## <a name="examples-sql-server-azure-sql-database"></a>Beispiele: SQLServer, Azure SQL-Datenbank  
  
### <a name="e-create-a-unique-nonclustered-index"></a>E. Erstellen Sie einen eindeutigen nicht gruppierten index  
 Im folgenden Beispiel wird ein eindeutiger nicht gruppierter Index für die `Name`-Spalte der `Production.UnitMeasure`-Tabelle in der [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]-Datenbank erstellt. Der Index erzwingt Eindeutigkeit für die Daten, die in die Spalte `Name` eingefügt werden.  
  
```sql  
CREATE UNIQUE INDEX AK_UnitMeasure_Name   
    ON Production.UnitMeasure(Name);  
```  
  
 In der folgenden Abfrage wird die Eindeutigkeitseinschränkung getestet, indem eine Zeile mit demselben Wert wie in einer vorhandenen Zeile eingefügt wird.  
  
```sql  
--Verify the existing value.  
SELECT Name FROM Production.UnitMeasure WHERE Name = N'Ounces';  
GO  
INSERT INTO Production.UnitMeasure (UnitMeasureCode, Name, ModifiedDate)  
    VALUES ('OC', 'Ounces', GetDate());  
```  
  
 Die folgende Fehlermeldung wird angezeigt:  
  
```  
Server: Msg 2601, Level 14, State 1, Line 1  
Cannot insert duplicate key row in object 'UnitMeasure' with unique index 'AK_UnitMeasure_Name'. The statement has been terminated.  
```  
  
### <a name="f-use-the-ignoredupkey-option"></a>F. Verwenden Sie die IGNORE_DUP_KEY-option  
 Das folgende Beispiel veranschaulicht die Wirkung der Option `IGNORE_DUP_KEY`, indem mehrere Zeilen zunächst mit dem Optionswert `ON` und anschließend mit dem Optionswert `OFF` in eine temporäre Tabelle eingefügt werden. Eine einzelne Zeile wird in die `#Test`-Tabelle eingefügt, die absichtlich einen doppelten Wert erzeugt, wenn die zweite mehrzeilige `INSERT`-Anweisung ausgeführt wird. Eine Zählung der Zeilen in der Tabelle gibt die Anzahl der eingefügten Zeilen zurück.  
  
```sql  
CREATE TABLE #Test (C1 nvarchar(10), C2 nvarchar(50), C3 datetime);  
GO  
CREATE UNIQUE INDEX AK_Index ON #Test (C2)  
    WITH (IGNORE_DUP_KEY = ON);  
GO  
INSERT INTO #Test VALUES (N'OC', N'Ounces', GETDATE());  
INSERT INTO #Test SELECT * FROM Production.UnitMeasure;  
GO  
SELECT COUNT(*)AS [Number of rows] FROM #Test;  
GO  
DROP TABLE #Test;  
GO  
```  
  
 Im Folgenden werden die Ergebnisse der zweiten `INSERT`-Anweisung aufgeführt.  
  
```  
Server: Msg 3604, Level 16, State 1, Line 5 Duplicate key was ignored.  
  
Number of rows   
--------------   
38  
```  
  
 Beachten Sie, dass die aus der Tabelle `Production.UnitMeasure` eingefügten Zeilen, die die Eindeutigkeitseinschränkung nicht verletzten, erfolgreich eingefügt wurden. Es wurde eine Warnung ausgegeben, und die doppelte Zeile wurde ignoriert, aber es wurde kein Rollback für die gesamte Transaktion ausgeführt.  
  
 Dieselben Anweisungen werden erneut ausgeführt. Dabei ist die Option `IGNORE_DUP_KEY` allerdings auf `OFF` festgelegt.  
  
```sql  
CREATE TABLE #Test (C1 nvarchar(10), C2 nvarchar(50), C3 datetime);  
GO  
CREATE UNIQUE INDEX AK_Index ON #Test (C2)  
    WITH (IGNORE_DUP_KEY = OFF);  
GO  
INSERT INTO #Test VALUES (N'OC', N'Ounces', GETDATE());  
INSERT INTO #Test SELECT * FROM Production.UnitMeasure;  
GO  
SELECT COUNT(*)AS [Number of rows] FROM #Test;  
GO  
DROP TABLE #Test;  
GO  
```  
  
 Im Folgenden werden die Ergebnisse der zweiten `INSERT`-Anweisung aufgeführt.  
  
```  
Server: Msg 2601, Level 14, State 1, Line 5  
Cannot insert duplicate key row in object '#Test' with unique index  
'AK_Index'. The statement has been terminated.  
  
Number of rows   
--------------   
1  
```  
  
 Beachten Sie, dass keine Zeilen aus der `Production.UnitMeasure`-Tabelle in die Tabelle eingefügt wurden, obwohl nur eine Zeile in der Tabelle die `UNIQUE`-Einschränkung für den Index verletzte.  
  
### <a name="g-using-dropexisting-to-drop-and-re-create-an-index"></a>G. Verwenden von DROP_EXISTING zum Löschen und Neuerstellen eines Index  
 Im folgenden Beispiel wird ein vorhandener Index für die `ProductID`-Spalte der `Production.WorkOrder`-Tabelle in der [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]-Datenbank mithilfe der `DROP_EXISTING`-Option gelöscht und neu erstellt. Die Optionen `FILLFACTOR` und `PAD_INDEX` sind ebenfalls festgelegt.  
  
```sql  
CREATE NONCLUSTERED INDEX IX_WorkOrder_ProductID  
    ON Production.WorkOrder(ProductID)  
    WITH (FILLFACTOR = 80,  
        PAD_INDEX = ON,  
        DROP_EXISTING = ON);  
GO  
```  
  
### <a name="h-create-an-index-on-a-view"></a>H. Erstellen Sie einen Index für eine Sicht  
 Im folgenden Beispiel werden eine Sicht und ein Index für diese Sicht erstellt. Dies beinhaltet zwei Abfragen, in denen die indizierte Sicht verwendet wird.  
  
```sql  
--Set the options to support indexed views.  
SET NUMERIC_ROUNDABORT OFF;  
SET ANSI_PADDING, ANSI_WARNINGS, CONCAT_NULL_YIELDS_NULL, ARITHABORT,  
    QUOTED_IDENTIFIER, ANSI_NULLS ON;  
GO  
--Create view with schemabinding.  
IF OBJECT_ID ('Sales.vOrders', 'view') IS NOT NULL  
DROP VIEW Sales.vOrders ;  
GO  
CREATE VIEW Sales.vOrders  
WITH SCHEMABINDING  
AS  
    SELECT SUM(UnitPrice*OrderQty*(1.00-UnitPriceDiscount)) AS Revenue,  
        OrderDate, ProductID, COUNT_BIG(*) AS COUNT  
    FROM Sales.SalesOrderDetail AS od, Sales.SalesOrderHeader AS o  
    WHERE od.SalesOrderID = o.SalesOrderID  
    GROUP BY OrderDate, ProductID;  
GO  
--Create an index on the view.  
CREATE UNIQUE CLUSTERED INDEX IDX_V1   
    ON Sales.vOrders (OrderDate, ProductID);  
GO  
--This query can use the indexed view even though the view is   
--not specified in the FROM clause.  
SELECT SUM(UnitPrice*OrderQty*(1.00-UnitPriceDiscount)) AS Rev,   
    OrderDate, ProductID  
FROM Sales.SalesOrderDetail AS od  
    JOIN Sales.SalesOrderHeader AS o ON od.SalesOrderID=o.SalesOrderID  
        AND ProductID BETWEEN 700 and 800  
        AND OrderDate >= CONVERT(datetime,'05/01/2002',101)  
GROUP BY OrderDate, ProductID  
ORDER BY Rev DESC;  
GO  
--This query can use the above indexed view.  
SELECT  OrderDate, SUM(UnitPrice*OrderQty*(1.00-UnitPriceDiscount)) AS Rev  
FROM Sales.SalesOrderDetail AS od  
    JOIN Sales.SalesOrderHeader AS o ON od.SalesOrderID=o.SalesOrderID  
        AND DATEPART(mm,OrderDate)= 3  
        AND DATEPART(yy,OrderDate) = 2002  
GROUP BY OrderDate  
ORDER BY OrderDate ASC;  
GO  
```  
  
### <a name="i-create-an-index-with-included-non-key-columns"></a>I. Erstellen Sie einen Index mit eingeschlossenen (nichtschlüssel-) Spalten  
 Im folgenden Beispiel wird ein nicht gruppierter Index mit einer Schlüsselspalte (`PostalCode`) und vier Nichtschlüsselspalten (`AddressLine1`, `AddressLine2`, `City`, `StateProvinceID`) erstellt. Es folgt eine Abfrage, die vom Index abgedeckt wird. Index anzeigen, die durch den Abfrageoptimierer ausgewählt ist, auf die **Abfrage** im Menü [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]Option **tatsächlichen Ausführungsplan anzeigen** vor Ausführung der Abfrage.  
  
```sql  
CREATE NONCLUSTERED INDEX IX_Address_PostalCode  
    ON Person.Address (PostalCode)  
    INCLUDE (AddressLine1, AddressLine2, City, StateProvinceID);  
GO  
SELECT AddressLine1, AddressLine2, City, StateProvinceID, PostalCode  
FROM Person.Address  
WHERE PostalCode BETWEEN N'98000' and N'99999';  
GO  
```  
  
### <a name="j-create-a-partitioned-index"></a>J. Erstellen Sie einen partitionierten index  
 Im folgenden Beispiel wird ein nicht gruppierter partitionierter Index für `TransactionsPS1` (ein vorhandenes Partitionsschema in der [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]-Datenbank) erstellt. Dieses Beispiel setzt voraus, dass das Beispiel für einen partitionierten Index installiert wurde.  
  
**Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] und [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
```sql  
CREATE NONCLUSTERED INDEX IX_TransactionHistory_ReferenceOrderID  
    ON Production.TransactionHistory (ReferenceOrderID)  
    ON TransactionsPS1 (TransactionDate);  
GO  
```  
  
### <a name="k-creating-a-filtered-index"></a>K. Erstellen eines gefilterten Index  
 Im folgenden Beispiel wird ein gefilterter Index für die Production.BillOfMaterials-Tabelle in der [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]-Datenbank erstellt. Das Filterprädikat kann Spalten einschließen, die keine Schlüsselspalten im gefilterten Index sind. Das Prädikat in diesem Beispiel wählt nur die Zeilen aus, in denen EndDate nicht NULL ist.  
  
```sql  
CREATE NONCLUSTERED INDEX "FIBillOfMaterialsWithEndDate"  
    ON Production.BillOfMaterials (ComponentID, StartDate)  
    WHERE EndDate IS NOT NULL;  
```  
  
### <a name="l-create-a-compressed-index"></a>L. Erstellen eines komprimierten Indexes  
 Im folgenden Beispiel wird ein Index für eine nicht partitionierte Tabelle unter Verwendung der Zeilenkomprimierung erstellt.  
  
```sql  
CREATE NONCLUSTERED INDEX IX_INDEX_1   
    ON T1 (C2)  
WITH ( DATA_COMPRESSION = ROW ) ;   
GO  
```  
  
 Im folgenden Beispiel wird ein Index für eine partitionierte Tabelle unter Verwendung der Zeilenkomprimierung für alle Partitionen des Indexes erstellt.  
  
```sql  
CREATE CLUSTERED INDEX IX_PartTab2Col1  
ON PartitionTable1 (Col1)  
WITH ( DATA_COMPRESSION = ROW ) ;  
GO  
```  
  
 Im folgenden Beispiel wird ein Index für eine partitionierte Tabelle erstellt, wobei die Seitenkomprimierung für Partition `1` des Indexes und die Zeilenkomprimierung für die Partitionen `2` bis `4` des Indexes verwendet wird.  
  
```sql  
CREATE CLUSTERED INDEX IX_PartTab2Col1  
ON PartitionTable1 (Col1)  
WITH (DATA_COMPRESSION = PAGE ON PARTITIONS(1),  
    DATA_COMPRESSION = ROW ON PARTITIONS (2 TO 4 ) ) ;  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Beispiele: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] und[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="m-basic-syntax"></a>M. Grundlegende Syntax  
  
```sql  
CREATE INDEX IX_VendorID   
    ON ProductVendor (VendorID);  
CREATE INDEX IX_VendorID   
    ON dbo.ProductVendor (VendorID DESC, Name ASC, Address DESC);  
CREATE INDEX IX_VendorID   
    ON Purchasing..ProductVendor (VendorID);  
```  
  
### <a name="n-create-a-non-clustered-index-on-a-table-in-the-current-database"></a>N. Erstellen Sie einen nicht gruppierten Index für eine Tabelle in der aktuellen Datenbank  
 Im folgende Beispiel erstellt einen nicht gruppierten Index für die `VendorID` Spalte die `ProductVendor` Tabelle.  
  
```sql  
CREATE INDEX IX_ProductVendor_VendorID   
    ON ProductVendor (VendorID);   
```  
  
### <a name="o-create-a-clustered-index-on-a-table-in-another-database"></a>O. Erstellen Sie einen gruppierten Index für eine Tabelle in einer anderen Datenbank  
 Im folgende Beispiel erstellt einen nicht gruppierten Index für die `VendorID` Spalte die `ProductVendor` -Tabelle in der `Purchasing` Datenbank.  
  
```sql  
CREATE CLUSTERED INDEX IX_ProductVendor_VendorID   
    ON Purchasing..ProductVendor (VendorID);   
```  
  
## <a name="see-also"></a>Siehe auch  
 [Handbuch zum SQL Server Indexentwurf](../../relational-databases/sql-server-index-design-guide.md)   
 [Indizes und ALTER TABLE-Anweisung](../../t-sql/statements/alter-table-transact-sql.md#indexes-and-alter-table)     
 [ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)   
 [CREATE PARTITION FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/create-partition-function-transact-sql.md)   
 [CREATE PARTITION SCHEME &#40;Transact-SQL&#41;](../../t-sql/statements/create-partition-scheme-transact-sql.md)   
 [Erstellen Sie SPATIAL INDEX &#40; Transact-SQL &#41;](../../t-sql/statements/create-spatial-index-transact-sql.md)   
 [CREATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/create-statistics-transact-sql.md)   
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [Erstellen von XML-INDEX &#40; Transact-SQL &#41;](../../t-sql/statements/create-xml-index-transact-sql.md)   
 [Datentypen &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [DBCC SHOW_STATISTICS &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md)   
 [DROP INDEX &#40; Transact-SQL &#41;](../../t-sql/statements/drop-index-transact-sql.md)   
 [XML-Indizes &#40;SQL Server&#41;](../../relational-databases/xml/xml-indexes-sql-server.md)   
 [sys.indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)   
 [sys.index_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-index-columns-transact-sql.md)   
 [Sys. xml_indexes &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-xml-indexes-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
 


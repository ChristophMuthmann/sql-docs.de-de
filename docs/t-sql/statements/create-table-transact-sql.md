---
title: Erstellen der Tabelle (Transact-SQL) | Microsoft Docs
ms.custom:
- SQL2016_New_Updated
ms.date: 08/10/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- FILESTREAM_TSQL
- TABLE
- CREATE_TABLE_TSQL
- CREATE TABLE
- FILESTREAM
- TABLE_TSQL
- FILESTREAM_ON
- FILESTREAM_ON_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CHECK constraints
- global temporary tables [SQL Server]
- local temporary tables [SQL Server]
- size [SQL Server], tables
- UNIQUE constraints [SQL Server], creating
- constraints [SQL Server], columns
- maximum number of indexes per table
- number of tables per database
- number of indexes per table
- table creation [SQL Server], CREATE TABLE
- temporary tables [SQL Server], creating
- table size [SQL Server]
- nullability [SQL Server]
- partitioned tables [SQL Server], creating
- DEFAULT definition
- null values [SQL Server], columns
- number of rows per table
- maximum number of columns per table
- FOREIGN KEY constraints, creating
- PRIMARY KEY constraints
- number of bytes per row
- CREATE TABLE statement
- number of columns per table
- maximum number of bytes per row
ms.assetid: 1e068443-b9ea-486a-804f-ce7b6e048e8b
caps.latest.revision: 256
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 0978041b1c2683f6af3f6c531ddc10edc6b9bcbf
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="create-table-transact-sql"></a>CREATE TABLE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Erstellt eine neue Tabelle in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] und [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
> [!NOTE]   
>  Für [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] -Syntax finden Sie unter [CREATE TABLE (Azure SQL Data Warehouse)](../../t-sql/statements/create-table-azure-sql-data-warehouse.md).
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
--Simple CREATE TABLE Syntax (common if not using options)  
CREATE TABLE   
    [ database_name . [ schema_name ] . | schema_name . ] table_name   
    ( { <column_definition> } [ ,...n ] )   
[ ; ]  
```  
  
## <a name="syntax"></a>Syntax  
  
```  
--Disk-Based CREATE TABLE Syntax  
CREATE TABLE   
    [ database_name . [ schema_name ] . | schema_name . ] table_name   
    [ AS FileTable ]  
    ( {   <column_definition>   
        | <computed_column_definition>    
        | <column_set_definition>   
        | [ <table_constraint> ]   
        | [ <table_index> ] }  
          [ ,...n ]    
          [ PERIOD FOR SYSTEM_TIME ( system_start_time_column_name   
             , system_end_time_column_name ) ]  
      )  
    [ ON { partition_scheme_name ( partition_column_name )   
           | filegroup   
           | "default" } ]   
    [ TEXTIMAGE_ON { filegroup | "default" } ]   
    [ FILESTREAM_ON { partition_scheme_name   
           | filegroup   
           | "default" } ]  
    [ WITH ( <table_option> [ ,...n ] ) ]  
[ ; ]  
  
<column_definition> ::=  
column_name <data_type>  
    [ FILESTREAM ]  
    [ COLLATE collation_name ]   
    [ SPARSE ]  
    [ MASKED WITH ( FUNCTION = ' mask_function ') ]  
    [ CONSTRAINT constraint_name [ DEFAULT constant_expression ] ]   
    [ IDENTITY [ ( seed,increment ) ]  
    [ NOT FOR REPLICATION ]   
    [ GENERATED ALWAYS AS ROW { START | END } [ HIDDEN ] ]   
    [ NULL | NOT NULL ]  
    [ ROWGUIDCOL ]  
    [ ENCRYPTED WITH   
        ( COLUMN_ENCRYPTION_KEY = key_name ,  
          ENCRYPTION_TYPE = { DETERMINISTIC | RANDOMIZED } ,   
          ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256'  
        ) ]  
    [ <column_constraint> [ ...n ] ]   
    [ <column_index> ]  
  
<data type> ::=   
[ type_schema_name . ] type_name   
    [ ( precision [ , scale ] | max |   
        [ { CONTENT | DOCUMENT } ] xml_schema_collection ) ]   
  
<column_constraint> ::=   
[ CONSTRAINT constraint_name ]   
{     { PRIMARY KEY | UNIQUE }   
        [ CLUSTERED | NONCLUSTERED ]   
        [   
            WITH FILLFACTOR = fillfactor    
          | WITH ( < index_option > [ , ...n ] )   
        ]   
        [ ON { partition_scheme_name ( partition_column_name )   
            | filegroup | "default" } ]  
  
  | [ FOREIGN KEY ]   
        REFERENCES [ schema_name . ] referenced_table_name [ ( ref_column ) ]   
        [ ON DELETE { NO ACTION | CASCADE | SET NULL | SET DEFAULT } ]   
        [ ON UPDATE { NO ACTION | CASCADE | SET NULL | SET DEFAULT } ]   
        [ NOT FOR REPLICATION ]   
  
  | CHECK [ NOT FOR REPLICATION ] ( logical_expression )   
}   
  
<column_index> ::=   
 INDEX index_name [ CLUSTERED | NONCLUSTERED ]  
    [ WITH ( <index_option> [ ,... n ] ) ]  
    [ ON { partition_scheme_name (column_name )   
         | filegroup_name  
         | default   
         }  
    ]   
    [ FILESTREAM_ON { filestream_filegroup_name | partition_scheme_name | "NULL" } ]  
  
<computed_column_definition> ::=  
column_name AS computed_column_expression   
[ PERSISTED [ NOT NULL ] ]  
[   
    [ CONSTRAINT constraint_name ]  
    { PRIMARY KEY | UNIQUE }  
        [ CLUSTERED | NONCLUSTERED ]  
        [   
            WITH FILLFACTOR = fillfactor   
          | WITH ( <index_option> [ , ...n ] )  
        ]  
        [ ON { partition_scheme_name ( partition_column_name )   
        | filegroup | "default" } ]  
  
    | [ FOREIGN KEY ]   
        REFERENCES referenced_table_name [ ( ref_column ) ]   
        [ ON DELETE { NO ACTION | CASCADE } ]   
        [ ON UPDATE { NO ACTION } ]   
        [ NOT FOR REPLICATION ]   
  
    | CHECK [ NOT FOR REPLICATION ] ( logical_expression )   
]   
  
<column_set_definition> ::=  
column_set_name XML COLUMN_SET FOR ALL_SPARSE_COLUMNS  
  
< table_constraint > ::=  
[ CONSTRAINT constraint_name ]   
{   
    { PRIMARY KEY | UNIQUE }   
        [ CLUSTERED | NONCLUSTERED ]   
        (column [ ASC | DESC ] [ ,...n ] )   
        [   
            WITH FILLFACTOR = fillfactor   
           |WITH ( <index_option> [ , ...n ] )   
        ]  
        [ ON { partition_scheme_name (partition_column_name)  
            | filegroup | "default" } ]   
    | FOREIGN KEY   
        ( column [ ,...n ] )   
        REFERENCES referenced_table_name [ ( ref_column [ ,...n ] ) ]   
        [ ON DELETE { NO ACTION | CASCADE | SET NULL | SET DEFAULT } ]   
        [ ON UPDATE { NO ACTION | CASCADE | SET NULL | SET DEFAULT } ]   
        [ NOT FOR REPLICATION ]   
    | CHECK [ NOT FOR REPLICATION ] ( logical_expression )  
 

  
< table_index > ::=   
{  
    {  
      INDEX index_name [ CLUSTERED | NONCLUSTERED ]   
         (column_name [ ASC | DESC ] [ ,... n ] )   
    | INDEX index_name CLUSTERED COLUMNSTORE  
    | INDEX index_name [ NONCLUSTERED ] COLUMNSTORE (column_name [ ,... n ] )  
    }  
    [ WITH ( <index_option> [ ,... n ] ) ]   
    [ ON { partition_scheme_name (column_name )   
         | filegroup_name  
         | default   
         }  
    ]   
    [ FILESTREAM_ON { filestream_filegroup_name | partition_scheme_name | "NULL" } ]  
  
}   


<table_option> ::=  
{  
    [DATA_COMPRESSION = { NONE | ROW | PAGE }  
      [ ON PARTITIONS ( { <partition_number_expression> | <range> }   
      [ , ...n ] ) ]]  
    [ FILETABLE_DIRECTORY = <directory_name> ]   
    [ FILETABLE_COLLATE_FILENAME = { <collation_name> | database_default } ]  
    [ FILETABLE_PRIMARY_KEY_CONSTRAINT_NAME = <constraint_name> ]  
    [ FILETABLE_STREAMID_UNIQUE_CONSTRAINT_NAME = <constraint_name> ]  
    [ FILETABLE_FULLPATH_UNIQUE_CONSTRAINT_NAME = <constraint_name> ]  
    [ SYSTEM_VERSIONING = ON [ ( HISTORY_TABLE = schema_name . history_table_name  
        [, DATA_CONSISTENCY_CHECK = { ON | OFF } ] ) ] ]  
    [ REMOTE_DATA_ARCHIVE =   
      {   
          ON [ ( <table_stretch_options> [,...n] ) ]  
        | OFF ( MIGRATION_STATE = PAUSED )   
      }   
    ]  
}  
  
<table_stretch_options> ::=  
{  
     [ FILTER_PREDICATE = { null | table_predicate_function } , ]  
       MIGRATION_STATE = { OUTBOUND | INBOUND | PAUSED }  
 }  
  
<index_option> ::=  
{   
    PAD_INDEX = { ON | OFF }   
  | FILLFACTOR = fillfactor   
  | IGNORE_DUP_KEY = { ON | OFF }   
  | STATISTICS_NORECOMPUTE = { ON | OFF }   
  | ALLOW_ROW_LOCKS = { ON | OFF}   
  | ALLOW_PAGE_LOCKS ={ ON | OFF}   
  | COMPRESSION_DELAY= {0 | delay [Minutes]}  
  | DATA_COMPRESSION = { NONE | ROW | PAGE | COLUMNSTORE | COLUMNSTORE_ARCHIVE }  
       [ ON PARTITIONS ( { <partition_number_expression> | <range> }   
       [ , ...n ] ) ]  
}  
<range> ::=   
<partition_number_expression> TO <partition_number_expression>  
```  
  
```  
  
      --Memory optimized CREATE TABLE Syntax  
CREATE TABLE  
    [database_name . [schema_name ] . | schema_name . ] table_name  
    ( { <column_definition>  
    | [ <table_constraint> ] [ ,... n ]  
    | [ <table_index> ]  
      [ ,... n ] }   
      [ PERIOD FOR SYSTEM_TIME ( system_start_time_column_name   
        , system_end_time_column_name ) ]  
)  
    [ WITH ( <table_option> [ ,... n ] ) ]  
 [ ; ]  
  
<column_definition> ::=  
column_name <data_type>  
    [ COLLATE collation_name ]  
    [ GENERATED ALWAYS AS ROW { START | END } [ HIDDEN ] ]   
    [ NULL | NOT NULL ]  
[  
    [ CONSTRAINT constraint_name ] DEFAULT memory_optimized_constant_expression ]  
    | [ IDENTITY [ ( 1, 1 ) ]  
]  
    [ <column_constraint> ]  
    [ <column_index> ]  
  
<data type> ::=  
 [type_schema_name . ] type_name [ (precision [ , scale ]) ]  
  
<column_constraint> ::=  
 [ CONSTRAINT constraint_name ]  
{   
  { PRIMARY KEY | UNIQUE }    
      {   NONCLUSTERED   
        | NONCLUSTERED HASH WITH (BUCKET_COUNT = bucket_count)   
      }   
  | [ FOREIGN KEY ]   
        REFERENCES [ schema_name . ] referenced_table_name [ ( ref_column ) ]   
  | CHECK ( logical_expression )   
}  
  
< table_constraint > ::=  
 [ CONSTRAINT constraint_name ]  
{    
   { PRIMARY KEY | UNIQUE }  
     {   
       NONCLUSTERED (column [ ASC | DESC ] [ ,... n ])  
       | NONCLUSTERED HASH (column [ ,... n ] ) WITH ( BUCKET_COUNT = bucket_count )   
                    }   
    | FOREIGN KEY   
        ( column [ ,...n ] )   
        REFERENCES referenced_table_name [ ( ref_column [ ,...n ] ) ]   
    | CHECK ( logical_expression )   
}  
  
<column_index> ::=  
  INDEX index_name  
{ [ NONCLUSTERED ] | [ NONCLUSTERED ] HASH WITH (BUCKET_COUNT = bucket_count)  }  
  
<table_index> ::=  
  INDEX index_name  
{   [ NONCLUSTERED ] HASH (column [ ,... n ] ) WITH (BUCKET_COUNT = bucket_count)   
  | [ NONCLUSTERED ] (column [ ASC | DESC ] [ ,... n ] )   
      [ ON filegroup_name | default ]  
  | CLUSTERED COLUMNSTORE [WITH ( COMPRESSION_DELAY = {0 | delay [Minutes]})]  
      [ ON filegroup_name | default ]  
  
}  
  
<table_option> ::=  
{  
    MEMORY_OPTIMIZED = ON   
  | DURABILITY = {SCHEMA_ONLY | SCHEMA_AND_DATA}  
  | SYSTEM_VERSIONING = ON [ ( HISTORY_TABLE = schema_name . history_table_name  
        [, DATA_CONSISTENCY_CHECK = { ON | OFF } ] ) ]   
  
}  
```  
  
## <a name="arguments"></a>Argumente  
 *database_name*  
 Der Name der Datenbank, in der die Tabelle erstellt wird. *Database_name* müssen den Namen einer vorhandenen Datenbank angeben. Wenn nicht angegeben, *Database_name* Standardwerte auf die aktuelle Datenbank. Der Anmeldename für die aktuelle Verbindung muss einer vorhandenen Benutzer-ID in der durch den angegebenen Datenbank zugeordnet werden *Database_name*, und diese Benutzer-ID muss über CREATE TABLE-Berechtigungen verfügen.  
  
 *schema_name*  
 Der Name des Schemas, zu dem die neue Tabelle gehört.  
  
 *table_name*  
 Der Name der neuen Tabelle. Tabellennamen müssen den Regeln für [Bezeichner](../../relational-databases/databases/database-identifiers.md). *TABLE_NAME* kann maximal 128 Zeichen enthalten, mit Ausnahme von lokalen temporären Tabellennamen (Namen mit dem Präfix ein einzelnen Nummernzeichen (#)), die 116 Zeichen nicht überschreiten.  
  
 AS FileTable 
 
**Gilt für**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. 
 
 Erstellt die neue Tabelle als FileTable. Sie geben keine Spalten an, da eine FileTable über ein festes Schema verfügt. Weitere Informationen zu FileTables finden Sie unter [FileTables &#40; SQLServer &#41; ](../../relational-databases/blob/filetables-sql-server.md).  
  
 *Spaltenname*  
 *computed_column_expression*  
 Ein Ausdruck, der den Wert einer berechneten Spalte definiert. Eine berechnete Spalte ist eine virtuelle Spalte, die nicht physisch in der Tabelle gespeichert ist, es sei denn, die Spalte wurde (mit PERSISTED) als persistente Spalte markiert. Die Spalte wird anhand eines Ausdrucks berechnet, der andere Spalten in derselben Tabelle verwendet. Beispielsweise kann eine berechnete Spalte die Definition besitzen: **Kosten** AS **Preis** \* **Qty**. Der Ausdruck kann der Name einer nicht berechneten Spalte, eine Konstante, eine Funktion, eine Variable oder eine beliebige durch einen oder mehrere Operatoren verbundene Kombination der genannten Möglichkeiten sein. Der Ausdruck darf keine Unterabfrage sein oder Aliasdatentypen enthalten.  
  
 Berechnete Spalten können in SELECT-Listen, WHERE-Klauseln, ORDER BY-Klauseln oder an anderen Stellen verwendet werden, an denen reguläre Ausdrücke verwendet werden können. Dabei gelten folgende Ausnahmen:  
  
-   Berechnete Spalten müssen als PERSISTED gekennzeichnet sein, um Teil einer FOREIGN KEY- oder CHECK-Einschränkung zu sein.  
  
-   Eine berechnete Spalte kann als Schlüsselspalte in einem Index oder als Teil einer PRIMARY KEY- oder UNIQUE-Einschränkung verwendet werden, wenn der Wert der berechneten Spalte durch einen deterministischen Ausdruck definiert ist und der Datentyp des Ergebnisses in Indexspalten zulässig ist.  
  
     Angenommen, wenn die Tabelle Ganzzahlspalten **eine** und **b**, die berechnete Spalte **a + b** indiziert werden kann, aber die berechnete Spalte **a + DATEPART (Dd, GETDATE())**  kann nicht indiziert werden, da der Wert in späteren Aufrufen ändern kann.  
  
-   Eine berechnete Spalte kann nicht das Ziel einer INSERT- oder UPDATE-Anweisung sein.  
  
> [!NOTE]  
>  Jede Zeile in einer Tabelle kann unterschiedliche Werte in den Spalten aufweisen, die für eine berechnete Spalte herangezogen werden, daher enthält die berechnete Spalte möglicherweise nicht in jeder Zeile den gleichen Wert.  
  
 Die NULL-Zulässigkeit berechneter Spalten wird automatisch von [!INCLUDE[ssDE](../../includes/ssde-md.md)] auf Grundlage der verwendeten Ausdrücke bestimmt. Für das Ergebnis der meisten Ausdrücke wird die NULL-Zulässigkeit angenommen, und zwar auch dann, wenn nur Spalten vorhanden sind, die keine NULL-Werte zulassen, da mögliche Unter- oder Überläufe ebenfalls zu NULL-Ergebnissen führen. Verwenden Sie die COLUMNPROPERTY-Funktion mit dem **AllowsNull** Eigenschaft, die NULL-Zulässigkeit von berechneten Spalten in einer Tabelle zu untersuchen. Ein Ausdruck, der NULL-Werte zulässt, die in einer nur durch die Angabe von ISNULL mit aktiviert werden kann die *"check_expression"* -Konstante, die Konstante, in dem ein Wert ungleich NULL ist für NULL-Ergebnis ersetzt. Für berechnete Spalten, die auf CLR-benutzerdefinierten Typausdrücken (Common Language Runtime) basieren, ist die REFERENCES-Berechtigung für den Typ erforderlich.  
  
 PERSISTED  
 Gibt an, dass das [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] die berechneten Werte physisch in der Tabelle speichert und die Werte aktualisiert, wenn Spalten, von denen die berechnete Spalte abhängt, aktualisiert werden. Wenn Sie eine berechnete Spalte (mit PERSISTED) als persistente Spalte markieren, können Sie einen Index für eine berechnete Spalte erstellen, die deterministisch, jedoch nicht genau ist. Weitere Informationen finden Sie unter [Indexes on Computed Columns](../../relational-databases/indexes/indexes-on-computed-columns.md). Alle berechneten Spalten, die als Partitionierungsspalten einer partitionierten Tabelle verwendet werden, müssen ausdrücklich als PERSISTED gekennzeichnet sein. *Computed_column_expression* muss deterministisch sein, wenn PERSISTED angegeben wird.  
  
 ON { *Partition_scheme* | *Dateigruppe* | **"**Standard**"** }  

 Gibt das Partitionsschema oder die Dateigruppe an, in der die Tabelle gespeichert wird. Wenn *Partition_scheme* angegeben wird, die Tabelle eine partitionierte Tabelle sein, deren Partitionen sich auf einem Satz von einem befinden, oder mehr Dateigruppen im angegebenen *Partition_scheme*. Wenn *Dateigruppe* angegeben ist, wird die Tabelle in der genannten Dateigruppe gespeichert ist. Die Dateigruppe muss in der Datenbank vorhanden sein. Wenn **"**Standard**"** angegeben ist, oder ON überhaupt nicht angegeben ist, wird die Tabelle in der Standarddateigruppe gespeichert. Der in CREATE TABLE angegebene Speichermechanismus einer Tabelle kann nachfolgend nicht mehr geändert werden.  
  
 ON {*Partition_scheme* | *Dateigruppe* | **"**Standard**"**} kann auch in einem PRIMÄRSCHLÜSSEL angegeben werden oder UNIQUE-Einschränkung. Diese Einschränkungen erstellen Indizes. Wenn *Dateigruppe* angegeben ist, wird der Index in der genannten Dateigruppe gespeichert ist. Wenn **"**Standard**"** angegeben ist, oder ON überhaupt nicht angegeben ist, wird der Index in derselben Dateigruppe wie die Tabelle gespeichert. Wenn die PRIMARY KEY- oder die UNIQUE-Einschränkung einen gruppierten Index erstellt, werden die Datenseiten für die Tabelle in derselben Dateigruppe wie der Index gespeichert. Wenn CLUSTERED angegeben wird, oder die Einschränkung andernfalls wird einen gruppierten Index erstellt, und eine *Partition_scheme* wird angegeben, die unterscheidet sich von der *Partition_scheme* oder *Dateigruppe* der Tabelle (Definition) oder umgekehrt, wird nur die Einschränkungsdefinition berücksichtigt werden, und die anderen werden ignoriert.  
  
> [!NOTE]  
>  In diesem Zusammenhang ist DEFAULT kein Schlüsselwort. Es ist ein Bezeichner für die Standarddateigruppe und muss begrenzt sein, wie in ON **"**Standard**"** oder ON **[**Standard**]**. Wenn **"**Standard**"** angegeben ist, muss die QUOTED_IDENTIFIER-Option ON sein, für die aktuelle Sitzung. Dies ist die Standardeinstellung. Weitere Informationen finden Sie unter [SET QUOTED_IDENTIFIER &#40;Transact-SQL&#41;](../../t-sql/statements/set-quoted-identifier-transact-sql.md).  
  
> [!NOTE]  
>  Nachdem Sie eine partitionierte Tabelle erstellt haben, erwägen Sie, die LOCK_ESCALATION-Option für die Tabelle auf AUTO festzulegen. Dies kann die Parallelität verbessern, indem die Sperren auf Partitionsebene (HoBT) statt auf Tabellenebene aktiviert werden. Weitere Informationen finden Sie unter [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md).  
  
 TEXTIMAGE_ON { *Dateigruppe*| **"**Standard**"** }  
 Gibt an, dass die **Text**, **Ntext**, **Image**, **Xml**, **varchar(max)**,  **nvarchar(max)**, **varbinary(max)**, und der CLR-UDT-Spalten (einschließlich Geometrie und Geografie) in der angegebenen Dateigruppe gespeichert werden.  
  
 TEXTIMAGE_ON ist nicht zulässig, wenn die Tabelle keine Spalten für umfangreiche Werte enthält. TEXTIMAGE_ON kann nicht angegeben werden, wenn *Partition_scheme* angegeben ist. Wenn **"**Standard**"** angegeben wird, oder TEXTIMAGE_ON überhaupt nicht angegeben ist, werden die Spalten für umfangreiche Werte in der Standarddateigruppe gespeichert. Die in CREATE TABLE angegebene Speicherung einer Spalte für umfangreiche Werte kann nachfolgend nicht mehr geändert werden.  

> [!NOTE]  
> Varchar(max), nvarchar(max), varbinary(max), Xml und große UDT-Werte werden direkt in der Datenzeile gespeichert, bis zu einem Höchstwert von 8.000 Bytes und sofern der Wert des Datensatzes anpassen können. Wenn der Wert des Datensatzes nicht passt, wird ein Zeiger sortiert in Zeilen und die übrigen Knoten außerhalb von Zeilen im LOB-Speicherbereich gespeichert wird. 0 ist der Standardwert.
TEXTIMAGE_ON ändert nur die Position eines "LOB-Speicherbereich", er hat keine Auswirkung, wenn Daten in der Zeile gespeichert sind. Verwenden Sie zum Speichern des gesamten LOB-Werts außerhalb der Zeile large Value Types Out of Row-Option von Sp_tableoption. 


> [!NOTE]  
>  In diesem Zusammenhang ist DEFAULT kein Schlüsselwort. Es ist ein Bezeichner für die Standarddateigruppe und muss begrenzt sein, wie in TEXTIMAGE_ON **"**Standard**"** oder TEXTIMAGE_ON **[**Standard**]**. Wenn **"**Standard**"** angegeben ist, muss die QUOTED_IDENTIFIER-Option ON sein, für die aktuelle Sitzung. Dies ist die Standardeinstellung. Weitere Informationen finden Sie unter [SET QUOTED_IDENTIFIER &#40;Transact-SQL&#41;](../../t-sql/statements/set-quoted-identifier-transact-sql.md).  
  
 FILESTREAM_ON { *Partition_scheme_name* | Filegroup | **"**Standard**"** } **betrifft**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. 
 
 Gibt die Dateigruppe für FILESTREAM-Daten an.  
  
 Wenn die Tabelle FILESTREAM-Daten enthält und partitioniert ist, muss die FILESTREAM_ON-Klausel eingeschlossen werden und ein Partitionsschema von FILESTREAM-Dateigruppen angeben. Dieses Partitionsschema muss die gleiche Partitionsfunktion und die gleichen Partitionsspalten wie das Partitionsschema der Tabelle verwenden. Andernfalls wird ein Fehler ausgelöst.  
  
 Wenn die Tabelle nicht partitioniert ist, kann die FILESTREAM-Spalte nicht partitioniert werden. Die FILESTREAM-Daten für die Tabelle müssen in einer einzigen Dateigruppe gespeichert werden. Diese Dateigruppe wird in der FILESTREAM_ON-Klausel angegeben.  
  
 Wenn die Tabelle nicht partitioniert und die FILESTREAM_ON-Klausel nicht angegeben ist, wird die FILESTREAM-Dateigruppe mit dem DEFAULT-Eigenschaftensatz verwendet. Wenn keine FILESTREAM-Dateigruppe vorhanden ist, wird ein Fehler ausgelöst.  
  
-   Wie auch bei ON und TEXTIMAGE_ON kann der mit CREATE TABLE für FILESTREAM_ON festgelegte Wert nur in den folgenden Fällen geändert werden:  
  
-   Ein [CREATE INDEX](../../t-sql/statements/create-index-transact-sql.md) -Anweisung konvertiert einen Heap in einen gruppierten Index. In diesem Fall kann eine andere FILESTREAM-Dateigruppe, ein anderes Partitionsschema oder NULL angegeben werden.  
  
-   Ein [DROP INDEX](../../t-sql/statements/drop-index-transact-sql.md) -Anweisung konvertiert einen gruppierten Index in einem Heap. In diesem Fall, eine andere FILESTREAM-Dateigruppe, Partitionsschema oder **"**Standard**"** kann angegeben werden.  
  
 Die Dateigruppe in der `FILESTREAM_ON <filegroup>` -Klausel, oder jede FILESTREAM-Dateigruppe mit dem Namen des Partitionsschemas muss jeweils eine Datei für die Dateigruppe definiert haben. Diese Datei muss definiert werden, indem eine [CREATE DATABASE](../../t-sql/statements/create-database-sql-server-transact-sql.md) oder [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql.md) Anweisung; andernfalls wird ein Fehler ausgelöst.  
  
 Verwandte FILESTREAM-Themen finden Sie unter [Binary Large Object &#40; BLOB &#41; Daten &#40; SQLServer &#41; ](../../relational-databases/blob/binary-large-object-blob-data-sql-server.md).  
  
 [ *Type_schema_name***.** ] *Type_name*  
 Gibt den Datentyp der Spalte sowie das Schema an, zu dem er gehört. Für datenträgerbasierte Tabellen kann der Datentyp einer der folgenden sein:  
  
-   Systemdatentyp  
  
-   Ein Aliastyp, der auf einem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Systemdatentyp basiert. Aliasdatentypen werden mit der CREATE TYPE-Anweisung erstellt, bevor sie in einer Tabellendefinition verwendet werden können. Die NULL- oder NOT NULL-Zuweisung für einen Aliasdatentyp lässt sich durch die entsprechende Angabe in einer CREATE TABLE-Anweisung überschreiben. Die Längenangabe kann jedoch nicht geändert werden; die Länge eines Aliasdatentyps kann nicht in einer CREATE TABLE-Anweisung angegeben werden.  
  
-   Ein CLR-benutzerdefinierter Typ. CLR-benutzerdefinierte Typen werden mit der CREATE TYPE-Anweisung erstellt, bevor sie in einer Tabellendefinition verwendet werden können. Zum Erstellen einer Spalte, die auf einem CLR-benutzerdefinierten Typ basiert, ist die REFERENCES-Berechtigung für den Typ erforderlich.  
  
 Wenn *Type_schema_name* nicht angegeben wird, die [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] Verweise *Type_name* in der folgenden Reihenfolge:  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Systemdatentyp.  
  
-   Das Standardschema des aktuellen Benutzers in der aktuellen Datenbank  
  
-   Das **dbo** -Schema in der aktuellen Datenbank  
  
 Speicheroptimierte Tabellen finden Sie unter [unterstützte Datentypen für In-Memory OLTP](../../relational-databases/in-memory-oltp/supported-data-types-for-in-memory-oltp.md) eine Liste unterstützter Systemtypen.  
  
 *precision*  
 Die Genauigkeit für den angegebenen Datentyp. Weitere Informationen über gültige Genauigkeitswerte finden Sie unter [mit einfacher Genauigkeit, Dezimalstellen und Länge](../../t-sql/data-types/precision-scale-and-length-transact-sql.md).  
  
 *scale*  
 Die Dezimalstellen für den angegebenen Datentyp. Weitere Informationen zu gültigen Dezimalstellenwerten finden Sie unter [mit einfacher Genauigkeit, Dezimalstellen und Länge](../../t-sql/data-types/precision-scale-and-length-transact-sql.md).  
  
 **Max**  
 Gilt nur für die **Varchar**, **Nvarchar**, und **Varbinary** -Datentyp zum Speichern von 2 ^ 31 Byte an Zeichen- und Binärdaten und 2 ^ 30 Bytes an Unicode-Daten.  
  
 CONTENT  
 Gibt an, dass jede Instanz die **Xml** -Datentyp im *Column_name* können mehrere Elemente der obersten Ebene enthalten. CONTENT gilt nur für die **Xml** Daten geben, und kann angegeben werden, nur dann, wenn *Xml_schema_collection* ist ebenfalls angegeben. Wird der Parameter nicht angegeben, entspricht CONTENT dem Standardverhalten.  
  
 DOCUMENT  
 Gibt an, dass jede Instanz die **Xml** -Datentyp im *Column_name* kann nur ein Element der obersten Ebene enthalten. DOCUMENT gilt nur für die **Xml** Daten geben, und kann angegeben werden, nur dann, wenn *Xml_schema_collection* ist ebenfalls angegeben.  
  
 *xml_schema_collection*  
 Gilt nur für die **Xml** Datentyp für den Typ eine XML-schemaauflistung zuordnen. Vor der Eingabe einer **Xml** Spalte an ein Schema, das Schema muss zuerst erstellt werden in der Datenbank mithilfe von [CREATE XML SCHEMA COLLECTION](../../t-sql/statements/create-xml-schema-collection-transact-sql.md).  
  
 DEFAULT  
 Gibt den Wert an, der für die Spalte bereitgestellt wird, wenn kein Wert explizit angegeben wurde. DEFAULT-Definitionen können angewendet werden, um alle Spalten außer den als definierten **Zeitstempel**, sowie von Spalten mit der IDENTITY-Eigenschaft. Wenn ein Standardwert für eine UDT-Spalte angegeben wird, muss der Typ eine implizite Konvertierung von unterstützen *Constant_expression* in den benutzerdefinierten Typ. DEFAULT-Definitionen werden entfernt, wenn die Tabelle gelöscht wird. Es kann nur ein konstanter Wert (z. B. eine Zeichenfolge), eine Skalarfunktion (entweder eine System-, eine benutzerdefinierte oder eine CLR-Funktion) oder NULL als Standardwert verwendet werden. Um die Kompatibilität mit früheren Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aufrechtzuerhalten, ist es möglich, einer DEFAULT-Definition einen Einschränkungsnamen zuzuweisen.  
  
 *constant_expression*  
 Ist eine Konstante, NULL oder eine Systemfunktion, die als Standardwert für die Spalte verwendet wird.  
  
 *memory_optimized_constant_expression*  
 Eine Konstante, ein NULL-Wert oder eine Systemfunktion, die bzw. der als Standardwert für die Spalte verwendet wird. Muss in systemintern kompilierten gespeicherten Prozeduren unterstützt werden. Weitere Informationen zu integrierten Funktionen in systemintern kompilierten gespeicherten Prozeduren finden Sie unter [unterstützte Funktionen für nativ kompilierte T-SQL-Module](../../relational-databases/in-memory-oltp/supported-features-for-natively-compiled-t-sql-modules.md).  
  
 IDENTITY  
 Gibt an, dass es sich bei der neuen Spalte um eine Identitätsspalte handelt. Wenn eine neue Zeile zur Tabelle hinzugefügt wird, stellt [!INCLUDE[ssDE](../../includes/ssde-md.md)] einen eindeutigen, inkrementellen Wert für die Spalte bereit. Identitätsspalten werden üblicherweise zusammen mit PRIMARY KEY-Einschränkungen verwendet, um als eindeutiger Zeilenbezeichner für die Tabelle zu dienen. Die IDENTITY-Eigenschaft zugewiesen werden kann **"tinyint"**, **"smallint"**, **Int**, **"bigint"**, **decimal(p,0)**, oder **numeric(p,0)** Spalten. Es kann nur eine Identitätsspalte pro Tabelle erstellt werden. Gebundene Standardwerte und DEFAULT-Einschränkungen können nicht mit einer Identitätsspalte verwendet werden. Entweder müssen sowohl Ausgangswert als auch Schrittweite oder keines von beiden angegeben werden. Wurden Ausgangswert und inkrementeller Wert nicht angegeben, ist der Standardwert (1,1).  
  
 In einer speicheroptimierten Tabelle die einzige zulässige Wert für beide *Ausgangswert* und *Inkrement* ist 1. (1,1) ist der Standardwert für *Ausgangswert* und *Inkrement*.  
  
 *Startwert*  
 Der Wert, der für die erste in die Tabelle geladene Zeile verwendet wird.  
  
 *Inkrement*  
 Der Schrittweitenwert, der zum Identitätswert der zuvor Zeile wird geladen werden.  
  
 NOT FOR REPLICATION  
 In der CREATE TABLE-Anweisung kann die NOT FOR REPLICATION-Klausel für die IDENTITY-Eigenschaft, für FOREIGN KEY-Einschränkungen und für CHECK-Einschränkungen angegeben werden. Wenn diese Klausel für die IDENTITY-Eigenschaft angegeben wird, werden Werte in Identitätsspalten nicht inkrementiert, wenn Replikations-Agents Einfügevorgänge ausführen. Wenn diese Klausel für eine Einschränkung angegeben wird, wird die Einschränkung nicht erzwungen, wenn Replikations-Agents Einfüge-, Update- oder Löschvorgänge ausführen.  
  
 DIE GENERATED ALWAYS AS ZEILE {STARTEN | ENDEN} [AUSGEBLENDETE] [NOT NULL]  
 **Gilt für**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] und [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
 Gibt an, dass eine angegebene datetime2-Spalte vom System verwendet werden soll, zum Aufzeichnen der Startzeit für die ein Datensatz gültig ist oder die Endzeit für die ein Datensatz gültig ist. Die Spalte definiert werden muss als NOT NULL. Wenn Sie versuchen, diese als NULL angeben, wird das System ein Fehler ausgelöst. Wenn Sie NOT NULL für eine Period-Spalte nicht explizit angeben, wird das System standardmäßig die Spalte als NOT NULL definiert. Verwenden Sie dieses Argument zusammen mit der PERIOD FOR SYSTEM_TIME und mit SYSTEM_VERSIONING = ON Argumente für die systemversionsverwaltung für eine Tabelle zu aktivieren. Weitere Informationen finden Sie unter [Temporal Tables](../../relational-databases/tables/temporal-tables.md).  
  
 Sie können eine oder beide zeitraumspalten mit kennzeichnen **HIDDEN** Flag diese Spalten implizit ausgeblendet werden so, dass **wählen \* FROM**  *`<table>`*  nicht für diese Spalten einen Wert zurückgeben. Standardmäßig werden die Periode-Spalten nicht ausgeblendet. Um verwendet werden, müssen ausgeblendete Spalten explizit in allen Abfragen eingeschlossen werden, die direkt auf die temporale Tabelle verweisen. So ändern Sie die **HIDDEN** Attribut für eine vorhandene zeitraumspalte **Zeitraum** muss gelöscht und neu erstellt, mit einem anderen ausgeblendete Flag.  
  
 `INDEX *index_name* [ CLUSTERED | NONCLUSTERED ] (*column_name* [ ASC | DESC ] [ ,... *n* ] )`  
     
**Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] und [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].

Gibt an, um einen Index für die Tabelle zu erstellen. Dies kann ein gruppierter Index oder ein nicht gruppierter Index sein. Der Index die aufgelisteten Spalten enthält, und die Daten in aufsteigender oder absteigender Reihenfolge sortiert wird.  
  
 INDEX *Index_name* CLUSTERED COLUMNSTORE  
   
  
**Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] und [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].
  
 Gibt an, um die gesamte Tabelle im Spaltenformat mit einem gruppierten columnstore-Index zu speichern. Dies beinhaltet immer alle Spalten in der Tabelle an. Die Daten ist nicht in alphabetisch oder numerisch sortiert, da die Zeilen organisiert werden, um Columnstore Komprimierung Vorteilen profitieren zu können.  
  
 INDEX *Index_name* [NONCLUSTERED] COLUMNSTORE (*Column_name* [,... *n* ] )  
   
  
**Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] und [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].
  
 Gibt an, um einen nicht gruppierten columnstore-Index für die Tabelle zu erstellen. Die zugrunde liegende Tabelle kann einen Rowstore-Heap oder gruppierten Index oder einen gruppierten columnstore-Index sind möglich. In allen Fällen speichert erstellen einen nicht gruppierten columnstore-Index für eine Tabelle eine zweite Kopie der Daten für die Spalten im Index aus.  
  
 Der nicht gruppierten columnstore-Index gespeichert und verwaltet werden als gruppierten columnstore-Index. Sie wird in einen nicht gruppierten columnstore-Index aufgerufen, da die Spalten beschränkt sein können, und sie als sekundären Index für eine Tabelle vorhanden ist.  
  
 ON *Partition_scheme_name***(***Column_name***)**  
 Gibt das Partitionsschema an, das die Dateigruppen definiert, denen die Partitionen eines partitionierten Index zugeordnet werden. Das Partitionsschema muss in der Datenbank vorhanden, durch Ausführen [CREATE PARTITION SCHEME](../../t-sql/statements/create-partition-scheme-transact-sql.md) oder [ALTER PARTITION SCHEME](../../t-sql/statements/alter-partition-scheme-transact-sql.md). *Column_name* gibt die Spalte für die ein partitionierter Index partitioniert werden. Diese Spalte muss den Datentyp, Länge, übereinstimmen und der Genauigkeit des Arguments der Partition, *Partition_scheme_name* verwendet. *Column_name* ist nicht auf die Spalten in der Indexdefinition beschränkt. Jede Spalte in der Basistabelle angegeben werden, außer beim Partitionieren von eines EINDEUTIGEN Indexes *Column_name* muss ausgewählt werden, die als eindeutige Schlüssel verwendet. Mit dieser Einschränkung kann [!INCLUDE[ssDE](../../includes/ssde-md.md)] die Eindeutigkeit der Schlüsselwerte in nur einer einzigen Partition überprüfen.  
  
> [!NOTE]  
>  Beim Partitionieren eines nicht eindeutigen gruppierten Index fügt [!INCLUDE[ssDE](../../includes/ssde-md.md)] standardmäßig die Partitionierungsspalte zu der Liste der gruppierten Indexschlüssel hinzu, sofern sie dort noch nicht angegeben wurde. Beim Partitionieren eines nicht eindeutigen, nicht gruppierten Indexes fügt [!INCLUDE[ssDE](../../includes/ssde-md.md)] die Partitionierungsspalte als (eingeschlossene) Nichtschlüsselspalte des Indexes hinzu, sofern sie noch nicht angegeben wurde.  
  
 Wenn *Partition_scheme_name* oder *Dateigruppe* nicht angegeben wird und die Tabelle partitioniert ist, wird der Index in demselben Partitionsschema, mit der gleichen Partitionsspalte, wie die zugrunde liegende Tabelle platziert.  
  
> [!NOTE]  
>  Sie können kein Partitionierungsschema für einen XML-Index angeben. Beim Partitionieren der Basistabelle verwendet der XML-Index dasselbe Partitionsschema wie die Tabelle.  
  
 Weitere Informationen zum Partitionieren von Indizes [Partitioned Tables and Indexes](../../relational-databases/partitions/partitioned-tables-and-indexes.md).  
  
 ON *Filegroup_name*  
 Erstellt den angegebenen Index für die angegebene Dateigruppe. Wenn kein Speicherort angegeben und die Tabelle oder Sicht nicht partitioniert ist, verwendet der Index dieselbe Dateigruppe wie die zugrunde liegende Tabelle oder Sicht. Die Dateigruppe muss bereits vorhanden sein.  
  
 ON **"**Standard**"**  
 Erstellt den angegebenen Index für die Standarddateigruppe.  
  
 Die Benennung default ist in diesem Kontext kein Schlüsselwort. Es ist ein Bezeichner für die Standarddateigruppe und muss begrenzt sein, wie in ON **"**Standard**"** oder ON **[**Standard**]**. Wenn "default" angegeben wird, muss die Option QUOTED_IDENTIFIER für die aktuelle Sitzung auf ON festgelegt sein. Dies ist die Standardeinstellung. Weitere Informationen finden Sie unter [SET QUOTED_IDENTIFIER &#40;Transact-SQL&#41;](../../t-sql/statements/set-quoted-identifier-transact-sql.md).  
  
 [FILESTREAM_ON { *Filestream_filegroup_name* | *Partition_scheme_name* | "NULL"}]  
   
**Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion.md)].

 Gibt die Platzierung der FILESTREAM-Daten für die Tabelle an, wenn ein gruppierter Index erstellt wird. Die FILESTREAM_ON-Klausel lässt zu, dass FILESTREAM-Daten in eine andere FILESTREAM-Dateigruppe oder ein anderes Partitionsschema verschoben werden.  
  
 *Filestream_filegroup_name* ist der Name einer FILESTREAM-Dateigruppe. Die Dateigruppe muss eine Datei, die für die Dateigruppe mit definiert haben eine [CREATE DATABASE](../../t-sql/statements/create-database-sql-server-transact-sql.md) oder [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql.md) Anweisung; andernfalls wird ein Fehler ausgelöst.  
  
 Wenn die Tabelle partitioniert ist, muss die FILESTREAM_ON-Klausel eingeschlossen werden und ein Partitionsschema von FILESTREAM-Dateigruppen angeben, das die gleiche Partitionsfunktion und die gleichen Partitionsspalten wie das Partitionsschema der Tabelle enthält. Andernfalls wird ein Fehler ausgelöst.  
  
 Wenn die Tabelle nicht partitioniert ist, kann die FILESTREAM-Spalte nicht partitioniert werden. Die FILESTREAM-Daten für die Tabelle müssen in einer einzigen Dateigruppe gespeichert werden, die in der FILESTREAM_ON-Klausel angegeben wird.  
  
 FILESTREAM_ON NULL kann in einer CREATE INDEX-Anweisung angegeben werden, wenn ein gruppierter Index erstellt wird und die Tabelle keine FILESTREAM-Spalte enthält.  
  
 Weitere Informationen finden Sie unter [FILESTREAM &#40;SQL Server&#41;](../../relational-databases/blob/filestream-sql-server.md).  
  
 ROWGUIDCOL  
 Gibt an, dass die neue Spalte eine Spalte mit Zeilen-GUIDs ist. Nur ein **"uniqueidentifier"** -Spalte pro Tabelle kann als ROWGUIDCOL-Spalte gekennzeichnet werden. Nach der Anwendung der ROWGUIDCOL-Eigenschaft kann mit $ROWGUID auf die Spalte verwiesen werden. Die ROWGUIDCOL-Eigenschaft kann nur für zugewiesen werden eine **"uniqueidentifier"** Spalte. Spalten eines benutzerdefinierten Datentyps können nicht mit ROWGUIDCOL gekennzeichnet werden.  
  
 Die ROWGUIDCOL-Eigenschaft erzwingt keine Eindeutigkeit der in der Spalte gespeicherten Werte. ROWGUIDCOL erzeugt auch nicht automatisch Werte für neue Zeilen, die in die Tabelle eingefügt werden. Um eindeutige Werte für jede Spalte zu generieren, verwenden Sie entweder die [NEWID](../../t-sql/functions/newid-transact-sql.md) oder [NEWSEQUENTIALID](../../t-sql/functions/newsequentialid-transact-sql.md) Funktion [einfügen](../../t-sql/statements/insert-transact-sql.md) Anweisungen oder verwenden Sie diese Funktionen als Standard für die die Spalte.  
  
 MIT VERSCHLÜSSELT  
 Gibt an, zum Verschlüsseln verwendete Spalten mithilfe der [Always Encrypted](../../relational-databases/security/encryption/always-encrypted-database-engine.md) Funktion.  
  
 COLUMN_ENCRYPTION_KEY = *Key_name*  
 Gibt den spaltenverschlüsselungsschlüssel an. Weitere Informationen finden Sie unter [CREATE COLUMN ENCRYPTION KEY &#40; Transact-SQL &#41; ](../../t-sql/statements/create-column-encryption-key-transact-sql.md).  
  
 ENCRYPTION_TYPE = {DETERMINISTISCH | ZUFÄLLIGE}  
 Die**deterministische Verschlüsselung** verwendet eine Methode, die immer denselben verschlüsselten Wert für jeden angegebenen Klartextwert generiert. Verwendung der deterministischen Verschlüsselung ermöglicht die Suche mithilfe der Gleichheitsvergleich, gruppieren und das Verknüpfen von Tabellen mit gleichheitsverknüpfung basierend auf verschlüsselten Werten jedoch erlaubt Sie nicht autorisierte Benutzer Informationen zu verschlüsselten Werten erraten, indem Sie Muster untersuchen die verschlüsselte Spalte. Verknüpfen von zwei Tabellen auf deterministisch verschlüsselten Spalten ist nur möglich, wenn beide Spalten mit demselben spaltenverschlüsselungsschlüssel verschlüsselt sind. Die deterministische Verschlüsselung muss eine Spaltensortierung mit einer binary2-Sortierreihenfolge für Zeichenspalten verwenden.  
  
 Die**zufällige Verschlüsselung** verwendet eine Methode, die Daten in einer weniger vorhersagbaren Weise verschlüsselt. Die zufällige Verschlüsselung ist sicherer, verhindert aber die Gleichheitssuche, Gruppierung und Verknüpfung für verschlüsselte Spalten. Nach dem Zufallsprinzip Spalten können nicht indiziert werden.  
  
 Verwenden Sie die deterministische Verschlüsselung für Spalten für die Suchparameter oder gruppierungsparameter, z. B. eine Personalausweisnummer. Verwenden nach dem Zufallsprinzip, für die Daten z. B. eine Kreditkartennummer, die nicht mit anderen Datensätzen gruppiert, oder zum Verknüpfen von Tabellen und die nicht für durchsucht wird, da Sie andere Spalten (z. B. eine Transaktionsnummer) verwenden, um die Zeile zu finden, die was die enthält das verschlüsselte der betreffenden Spalte.  
  
 Spalten müssen einen qualifizierenden Datentyp aufweisen.  
  
 ALGORITHMUS  
 Muss **'AEAD_AES_256_CBC_HMAC_SHA_256'**.  
  
 Weitere Informationen einschließlich Feature Einschränkungen finden Sie unter [Always Encrypted &#40; Datenbankmodul &#41;](../../relational-databases/security/encryption/always-encrypted-database-engine.md).  
  
 **Gilt für**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 SPARSE  
 Gibt an, dass die Spalte eine Spalte mit geringer Dichte ist. Der Speicher für Spalten mit geringer Dichte ist für NULL-Werte optimiert. Spalten mit geringer Dichte können nicht als NOT NULL festgelegt werden. Zusätzliche Einschränkungen und Weitere Informationen zu Spalten mit geringer Dichte finden Sie unter [Use Sparse Columns](../../relational-databases/tables/use-sparse-columns.md).  
  
 MASKIERTE mit (Funktion = " *Mask_function* ")  
 **Gilt für**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Gibt an, einer dynamischen Datenmaske. *Mask_function* ist der Name der Maskierungsfunktion mit den entsprechenden Parametern. Drei Funktionen sind verfügbar:  
  
-   default()  
  
-   Email()  
  
-   partial()  
  
-   Zufallsvariable()  
  
 Funktionsparameter, finden Sie unter [Dynamic Data Masking](../../relational-databases/security/dynamic-data-masking.md).  
  
 FILESTREAM  
   
**Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion.md)].

 Gilt nur für **varbinary(max)** Spalten. Gibt an, für die FILESTREAM-Speicherung der **varbinary(max)** BLOB-Daten.  
  
 Die Tabelle benötigen auch eine Spalte mit der **"uniqueidentifier"** -Datentyp, der das ROWGUIDCOL-Attribut enthält. Diese Spalte darf keine NULL-Werte zulassen und muss eine UNIQUE- oder eine PRIMARY KEY-Einschränkung für einzelne Spalten enthalten. Der GUID-Wert für die Spalte muss entweder beim Einfügen von Daten von einer Anwendung oder durch eine DEFAULT-Einschränkung mit der NEWID ()-Funktion bereitgestellt werden.  
  
 Die Spalte ROWGUIDCOL kann nicht gelöscht, und die zugehörigen Einschränkungen können nicht geändert werden, wenn für die Tabelle eine FILESTREAM-Spalte definiert ist. Die Spalte ROWGUIDCOL kann nur gelöscht werden, nachdem die letzte FILESTREAM-Spalte gelöscht wurde.  
  
 Wenn das FILESTREAM-Speicherattribut für eine Spalte angegeben wird, werden alle Werte dieser Spalte in einem FILESTREAM-Datencontainer des Dateisystems gespeichert.  
  
 COLLATE *Collation_name*  
 Gibt die Sortierung für die Spalte an. Sortierungsname kann entweder der Name einer Windows-Sortierreihenfolge oder ein SQL-Sortierungsname sein. *Collation_name* gilt nur für Spalten von der **Char**, **Varchar**, **Text**, **Nchar**, **Nvarchar**, und **Ntext** Datentypen. Wenn collation_name nicht angegeben ist, wird der Spalte die Sortierung des benutzerdefinierten Datentyps zugewiesen, wenn es sich um eine Spalte von einem benutzerdefinierten Datentyp handelt, oder es wird die Standardsortierung der Datenbank zugewiesen.  
  
 Weitere Informationen zu den Windows- und SQL-Sortierungsnamen finden Sie unter [Windows-Sortierungsname](../../t-sql/statements/windows-collation-name-transact-sql.md) und [SQL-Sortierungsname](../../t-sql/statements/sql-server-collation-name-transact-sql.md).  
  
 Weitere Informationen zur COLLATE-Klausel finden Sie unter [COLLATE &#40; Transact-SQL &#41; ](~/t-sql/statements/collations.md).  
  
 CONSTRAINT  
 Ein optionales Schlüsselwort, das den Anfang der Definition einer PRIMARY KEY-, NOT NULL-, UNIQUE-, FOREIGN KEY- oder CHECK-Einschränkung anzeigt.  
  
 *constraint_name*  
 Der Name einer Einschränkung. Einschränkungsnamen müssen innerhalb des Schemas, zu dem die Tabelle gehört, eindeutig sein.  
  
 NULL | NOT NULL  
 Bestimmt, ob NULL-Werte in der Spalte zulässig sind. NULL ist genau genommen keine Einschränkung, kann jedoch wie NOT NULL verwendet werden. NOT NULL kann nur für berechnete Spalten angegeben werden, wenn auch PERSISTED angegeben ist.  
  
 PRIMARY KEY  
 Eine Einschränkung, die die Entitätsintegrität für eine bestimmte Spalte (oder Spalten) durch einen eindeutigen Index erzwingt. Es kann nur eine PRIMARY KEY-Einschränkung pro Tabelle erstellt werden.  
  
 UNIQUE  
 Eine Einschränkung, die Entitätsintegrität für eine angegebene Spalte (oder Spalten) durch einen eindeutigen Index bereitstellt. Eine Tabelle kann mehrere UNIQUE-Einschränkungen haben.  
  
 CLUSTERED | NONCLUSTERED  
 Gibt an, dass ein gruppierter oder nicht gruppierter Index für die PRIMARY KEY- oder UNIQUE-Einschränkung erstellt wird. Für PRIMARY KEY-Einschränkungen wird standardmäßig CLUSTERED verwendet; für UNIQUE-Einschränkungen wird standardmäßig NONCLUSTERED verwendet.  
  
 In einer CREATE TABLE-Anweisung kann CLUSTERED nur für eine einzige Einschränkung angegeben werden. Wenn Sie CLUSTERED für eine UNIQUE-Einschränkung angeben und außerdem eine PRIMARY KEY-Einschränkung angeben, wird für PRIMARY KEY standardmäßig NONCLUSTERED verwendet.  
  
 Im Folgenden wird gezeigt, wie NONCLUSTERED in einer datenträgerbasierten Tabelle verwendet wird:  
  
```  
CREATE TABLE t1 ( c1 int, INDEX ix_1 NONCLUSTERED (c1))   
CREATE TABLE t2( c1 int INDEX ix_1 NONCLUSTERED (c1))   
CREATE TABLE t3( c1 int, c2 int INDEX ix_1 NONCLUSTERED)   
CREATE TABLE t4( c1 int, c2 int, INDEX ix_1 NONCLUSTERED (c1,c2))  
```  
  
 FOREIGN KEY REFERENCES  
 Eine Einschränkung, die referenzielle Integrität für die Daten in der Spalte oder den Spalten bereitstellt. FOREIGN KEY-Einschränkungen erfordern, dass jeder Wert in der Spalte in den entsprechenden Spalten, auf die verwiesen wird, in der Tabelle, auf die verwiesen wird, vorhanden ist. FOREIGN KEY-Einschränkungen können nur auf Spalten verweisen, die PRIMARY KEY- oder UNIQUE-Einschränkungen in der Tabelle sind, auf die verwiesen wird; oder auf Spalten, auf die in einer UNIQUE INDEX-Einschränkung in der Tabelle, auf die verwiesen wird, verwiesen wird. Fremdschlüssel für berechnete Spalten müssen auch als PERSISTED markiert werden.  
  
 [ *Schema_name***.**] *Referenced_table_name*]  
 Der Name der Tabelle, auf die in der FOREIGN KEY-Einschränkung verwiesen wird, sowie das Schema, zu dem sie gehört.  
  
 **(** *Ref_column* [ **,**... *n* ] **)**  
 Eine Spalte oder Liste von Spalten aus der Tabelle, auf die die FOREIGN KEY-Einschränkung verweist.  
  
 ON DELETE { **NICHTS** | CASCADE | SET NULL | STANDARD FESTLEGEN}  
 Gibt an, welche Aktion für Zeilen in der erstellten Tabelle ausgeführt werden soll, wenn diese Zeilen eine referenzielle Beziehung aufweisen und die Zeile, auf die verwiesen wird, aus der übergeordneten Tabelle gelöscht wird. Der Standardwert ist NO ACTION.  
  
 NO ACTION  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] löst einen Fehler aus, und für die Aktion zum Löschen der Zeile in der übergeordneten Tabelle wird ein Rollback ausgeführt.  
  
 CASCADE  
 Wenn diese Zeile aus der übergeordneten Tabelle gelöscht wird, werden die entsprechenden Zeilen aus der verweisenden Tabelle gelöscht.  
  
 SET NULL  
 Alle Werte, die sich der Fremdschlüssel zusammensetzt, werden auf NULL festgelegt, wenn die entsprechende Zeile in der übergeordneten Tabelle gelöscht wird. Die Fremdschlüsselspalten müssen NULL-Werte zulassen, um diese Einschränkung auszuführen.  
  
 SET DEFAULT  
 Alle Werte, aus denen sich der Fremdschlüssel zusammensetzt, werden auf ihre Standardwerte festgelegt, wenn die entsprechende Zeile in der übergeordneten Tabelle gelöscht wird. Alle Fremdschlüsselspalten müssen Standarddefinitionen aufweisen, damit diese Einschränkung ausgeführt wird. Wenn eine Spalte NULL-Werte zulässt, und es ist kein expliziter Standardwert festgelegt, wird NULL als der implizite Standardwert für die Spalte verwendet.  
  
 Geben Sie CASCADE nicht an, wenn die Tabelle in eine Mergeveröffentlichung einbezogen werden soll, bei der logische Datensätze verwendet werden. Weitere Informationen zu logischen Datensätzen finden Sie unter [Gruppieren von Änderungen an verknüpften Zeilen mithilfe von logischen Datensätzen](../../relational-databases/replication/merge/group-changes-to-related-rows-with-logical-records.md).  
  
 ON DELETE CASCADE kann nicht definiert werden, wenn für ON DELETE bereits ein INSTEAD OF-Trigger für die Tabelle vorhanden ist.  
  
 Z. B. in der [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] Datenbank, die **ProductVendor** Tabelle verfügt über eine referenzielle Beziehung zu den **Hersteller** Tabelle. Die **ProductVendor.BusinessEntityID** -Fremdschlüssel verweist auf die **Vendor.BusinessEntityID** Primärschlüssel.  
  
 Wenn eine DELETE-Anweisung, auf eine Zeile in ausgeführt wird der **Hersteller** Tabelle und eine ON DELETE CASCADE-Aktion für angegeben wird **ProductVendor.BusinessEntityID**, die [!INCLUDE[ssDE](../../includes/ssde-md.md)] Überprüfungen für eine oder mehrere abhängige Zeilen in der **ProductVendor** Tabelle. Falls vorhanden, die abhängigen Zeilen in der **ProductVendor** Tabelle gelöscht wurden, und die Zeile wird auch in der **Hersteller** Tabelle.  
  
 Umgekehrt, wenn NO ACTION angegeben ist, die [!INCLUDE[ssDE](../../includes/ssde-md.md)] löst einen Fehler aus und ein Rollback für die Delete-Aktion aus, auf die **Hersteller** Zeile, wenn es mindestens eine Zeile in der **ProductVendor** Tabelle, die darauf verweist.  
  
 BEI UPDATE { **NICHTS** | CASCADE | SET NULL | STANDARD FESTLEGEN}  
 Gibt an, welche Aktion für eine Zeile der geänderten Tabelle ausgeführt werden soll, wenn diese Zeile eine referenzielle Beziehung hat und die Zeile, auf die verwiesen wird, in der übergeordneten Tabelle aktualisiert wird. Der Standardwert ist NO ACTION.  
  
 NO ACTION  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] löst einen Fehler aus, und für die Updateaktion der Zeile in der übergeordneten Tabelle wird ein Rollback ausgeführt.  
  
 CASCADE  
 Wenn diese Zeile in der übergeordneten Tabelle aktualisiert wird, werden die entsprechenden Zeilen in der verweisenden Tabelle aktualisiert.  
  
 SET NULL  
 Alle Werte, aus denen sich der Fremdschlüssel zusammensetzt, werden auf NULL festgelegt, wenn die entsprechende Zeile in der übergeordneten Tabelle aktualisiert wird. Die Fremdschlüsselspalten müssen NULL-Werte zulassen, um diese Einschränkung auszuführen.  
  
 SET DEFAULT  
 Alle Werte, aus denen sich der Fremdschlüssel zusammensetzt, werden auf die Standardwerte festgelegt, wenn die entsprechende Zeile in der übergeordneten Tabelle aktualisiert wird. Alle Fremdschlüsselspalten müssen Standarddefinitionen aufweisen, damit diese Einschränkung ausgeführt wird. Wenn eine Spalte NULL-Werte zulässt, und es ist kein expliziter Standardwert festgelegt, wird NULL als der implizite Standardwert für die Spalte verwendet.  
  
 Geben Sie CASCADE nicht an, wenn die Tabelle in eine Mergeveröffentlichung einbezogen werden soll, bei der logische Datensätze verwendet werden. Weitere Informationen zu logischen Datensätzen finden Sie unter [Gruppieren von Änderungen an verknüpften Zeilen mithilfe von logischen Datensätzen](../../relational-databases/replication/merge/group-changes-to-related-rows-with-logical-records.md).  
  
 ON UPDATE CASCADE, SET NULL oder SET DEFAULT können nicht definiert werden, wenn für ON UPDATE schon ein INSTEAD OF-Trigger für die Tabelle vorhanden ist, die geändert wird.  
  
 Z. B. in der [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] Datenbank, die **ProductVendor** Tabelle verfügt über eine referenzielle Beziehung zu den **Hersteller** Tabelle: **ProductVendor.BusinessEntity** -Fremdschlüssel verweist auf die **Vendor.BusinessEntityID** Primärschlüssel.  
  
 Wenn eine UPDATE-Anweisung, auf eine Zeile in ausgeführt wird der **Hersteller** Tabelle und eine ON UPDATE CASCADE-Aktion für angegeben wird **ProductVendor.BusinessEntityID**, die [!INCLUDE[ssDE](../../includes/ssde-md.md)] Überprüfungen für eine oder mehrere abhängige Zeilen in der **ProductVendor** Tabelle. Falls vorhanden, die abhängigen Zeilen in der **ProductVendor** Tabelle aktualisiert werden, und die Zeile wird auch in der **Hersteller** Tabelle.  
  
 Umgekehrt, wenn NO ACTION angegeben ist, die [!INCLUDE[ssDE](../../includes/ssde-md.md)] löst einen Fehler aus und ein Rollback für die Updateaktion aus, auf die **Hersteller** Zeile, wenn es mindestens eine Zeile in der **ProductVendor** Tabelle, die darauf verweist.  
  
 CHECK  
 Eine Einschränkung, die Domänenintegrität erzwingt, indem die möglichen Eingabewerte für eine oder mehrere Spalten beschränkt wird. CHECK-Einschränkungen für berechnete Spalten müssen auch als PERSISTED markiert werden.  
  
 *Logical_Expression*  
 Ein logischer Ausdruck, der TRUE oder FALSE zurückgibt. Aliasdatentypen können nicht Teil des Ausdrucks sein.  
  
 *Spalte*  
 Eine Spalte oder Liste von Spalten in Klammern, die in Tabelleneinschränkungen verwendet wird, um anzuzeigen, welche Spalten in der Einschränkungsdefinition verwendet werden.  
  
 [ **ASC** | "DESC"]  
 Gibt die Reihenfolge an, in der die Spalte oder die Spalten, die in der Tabelleneinschränkung enthalten sind, sortiert werden. Die Standardeinstellung ist ASC.  
  
 *partition_scheme_name*  
 Der Name des Partitionsschemas, das die Dateigruppen definiert, denen die Partitionen einer partitionierten Tabelle zugeordnet werden. Das Partitionsschema muss in der Datenbank vorhanden sein.  
  
 [ *Partition_column_name***.** ]  
 Gibt die Spalte an, auf deren Grundlage eine partitionierte Tabelle partitioniert wird. Die Spalte übereinstimmen, die in der Partition angegeben, die Funktion *Partition_scheme_name* im Hinblick auf Datentyp, Länge und Genauigkeit. Berechnete Spalten, die in eine Partitionsfunktion einbezogen werden, müssen explizit als PERSISTED gekennzeichnet sein.  
  
> [!IMPORTANT]  
>  Es wird empfohlen, NOT NULL für die Partitionierungsspalte von partitionierten Tabellen sowie von nicht partitionierten Tabellen anzugeben, die als Quelle oder Ziel für ALTER TABLE...SWITCH-Vorgänge fungieren. Damit stellen Sie sicher, dass mit CHECK-Einschränkungen für Partitionierungsspalten keine Überprüfung auf NULL-Werte ausgeführt werden muss.  
  
 MIT FILLFACTOR  **=**  *Fillfactor*  
 Gibt an, wie weit das [!INCLUDE[ssDE](../../includes/ssde-md.md)] die einzelnen Indexseiten füllen soll, die zum Speichern der Indexdaten verwendet werden. Benutzerdefiniertes *Fillfactor* Werte können zwischen 1 und 100 sein. Wenn kein Wert angegeben ist, lautet der Standardwert 0. Die Füllfaktorwerte 0 und 100 sind in jeder Hinsicht identisch.  
  
> [!IMPORTANT]  
>  Dokumentieren mit FILLFACTOR = *Fillfactor* als einzige Indexoption, für die PRIMARY KEY- oder UNIQUE-Einschränkungen gilt wird aus Gründen der Abwärtskompatibilität beibehalten, jedoch nicht auf diese Weise in Zukunft dokumentiert wird frei.  
  
 *spaltensatzname* XML COLUMN_SET FOR ALL_SPARSE_COLUMNS  
 Der Name des Spaltensatzes. Bei einem Spaltensatz handelt es sich um eine nicht typisierte XML-Darstellung, die alle Tabellenspalten mit geringer Dichte in einer strukturierten Ausgabe kombiniert. Weitere Informationen zu Spaltensätzen finden Sie unter [Verwenden von Spaltensätzen](../../relational-databases/tables/use-column-sets.md).  
  
 PERIOD FOR SYSTEM_TIME (*System_start_time_column_name* , *System_end_time_column_name* )  
   
**Gilt für**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] und [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].
  
 Gibt die Namen der Spalten, die vom System verwendet wird, um den Zeitraum aufzuzeichnen, für den ein Datensatz gültig ist. Verwenden Sie dieses Argument zusammen mit der GENERIERTEN immer AS Zeile {starten | END} ' und ' mit SYSTEM_VERSIONING = auf die Argumente für die systemversionsverwaltung für eine Tabelle zu aktivieren. Weitere Informationen finden Sie unter [Temporal Tables](../../relational-databases/tables/temporal-tables.md).  
  
 COMPRESSION_DELAY  
   
**Gilt für**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] und [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].
  
 Für eine Speicheroptimierte Verzögerung gibt die minimale Anzahl von Minuten, die eine Zeile muss bleiben in der Tabelle unverändert, bevor er für die Komprimierung in den columnstore-Index geeignet ist. SQL Server wählt bestimmte Zeilen gemäß ihrer Uhrzeit der letzten Aktualisierung zu komprimieren. Z. B., wenn Zeilen während der ein Zeitraum von zwei Stunden Zeit häufig ändern, Sie konnte legen Sie COMPRESSION_DELAY = 120 Minuten, um sicherzustellen, dass Updates abgeschlossen sind, bevor Sie SQL Server die Zeile komprimiert.  
  
 Verzögerung gibt die minimale Anzahl von Minuten an, die eine Delta-Zeilengruppen in den GESCHLOSSENEN Zustand verbleiben muss für eine datenträgerbasierte Tabelle in der deltazeilengruppe, vor SQL Server in der komprimierten Zeilengruppe komprimiert werden können. Da es sich bei datenträgerbasierten Tabellen nicht nachverfolgen einfügen und aktualisieren Zeiten für einzelne Zeilen, SQL Server gilt die Verzögerung in Delta-Zeilengruppen in den GESCHLOSSENEN Zustand übergeht.  
  
 Der Standardwert beträgt 0 Minuten.  
  
 Für Empfehlungen dazu, wann verwenden Sie COMPRESSION_DELAY, finden Sie unter [erste Schritte mit Columnstore für operative Echtzeitanalyse](../../relational-databases/indexes/get-started-with-columnstore-for-real-time-operational-analytics.md)  
  
 \<Table_option >:: = Gibt eine oder mehrere Tabellenoptionen an.  
  
 DATA_COMPRESSION  
 Gibt die Datenkomprimierungsoption für die angegebene Tabelle, die Partitionsnummer oder den Bereich von Partitionen an. Folgende Optionen stehen zur Verfügung:  
  
 NONE  
 Die Tabelle oder die angegebenen Partitionen werden nicht komprimiert.  
  
 ROW  
 Die Tabelle oder die angegebenen Partitionen werden mit Zeilenkomprimierung komprimiert.  
  
 PAGE  
 Die Tabelle oder die angegebenen Partitionen werden mit Seitenkomprimierung komprimiert.  
  
 COLUMNSTORE  
   
  
**Gilt für**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] und [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].
  
 Gilt nur für columnstore-Indizes, einschließlich nicht gruppierter und gruppierter columnstore-Indizes. COLUMNSTORE gibt an, um mit der meisten leistungsfähiger columnstore-Komprimierung zu komprimieren. Dies ist die typische Wahl.  
  
 COLUMNSTORE_ARCHIVE  
   
  
**Gilt für**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] und [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
 Gilt nur für columnstore-Indizes, einschließlich nicht gruppierter und gruppierter columnstore-Indizes. COLUMNSTORE_ARCHIVE wird weiter auf die Tabelle oder Partition auf eine kleinere Größe komprimiert. Dies empfiehlt sich bei der Archivierung und in Situationen, in denen es auf eine geringere Speichergröße und nicht auf den zusätzlichen Zeitaufwand für das Speichern und Abrufen ankommt.  
  
 Weitere Informationen zur Komprimierung finden Sie unter [Datenkomprimierung](../../relational-databases/data-compression/data-compression.md).  
  
 AUF PARTITIONEN **(** { `<partition_number_expression>` | [ **,**... *n* ] **)**  
 Gibt die Partitionen an, für die die DATA_COMPRESSION-Einstellung gilt. Wenn die Tabelle nicht partitioniert ist, erzeugt das ON PARTITIONS-Argument einen Fehler. Wenn die ON PARTITIONS-Klausel nicht angegeben wird, gilt die DATA_COMPRESSION-Option für alle Partitionen einer partitionierten Tabelle.  
  
 *Partition_number_expression* kann auf folgende Weise angegeben werden:  
  
-   Geben Sie die Partitionsnummer einer Partition an, beispielsweise: ON PARTITIONS (2).  
  
-   Geben Sie die Partitionsnummern mehrerer einzelner Partitionen durch Trennzeichen getrennt an, beispielsweise: ON PARTITIONS (1, 5).  
  
-   Geben Sie sowohl Bereiche als auch einzelne Partitionen an, beispielsweise: ON PARTITIONS (2, 4, 6 TO 8)  
  
 `<range>`durch das Wort TO, z. B. getrennte Partitionsnummern angegeben werden können: ON PARTITIONS (6 TO 8).  
  
 Wenn Sie für verschiedene Partitionen unterschiedliche Datenkomprimierungstypen festlegen möchten, geben Sie die Option DATA_COMPRESSION mehrmals an, beispielsweise:  
  
```  
WITH   
(  
DATA_COMPRESSION = NONE ON PARTITIONS (1),   
DATA_COMPRESSION = ROW ON PARTITIONS (2, 4, 6 TO 8),   
DATA_COMPRESSION = PAGE ON PARTITIONS (3, 5)  
)  
```  
  
 \<Index_option >:: =  
 Gibt eine oder mehrere Indexoptionen an. Eine vollständige Beschreibung dieser Optionen, finden Sie unter [CREATE INDEX &#40; Transact-SQL &#41; ](../../t-sql/statements/create-index-transact-sql.md).  
  
 PAD_INDEX = {ON | **OFF** }  
 Bei der Einstellung ON wird der durch FILLFACTOR angegebene Prozentsatz des freien Speicherplatzes auf die Zwischenebenenseiten des Indexes angewendet. Wenn die Einstellung OFF verwendet wird oder kein FILLFACTOR-Wert angegeben wurde, werden die Zwischenebenenseiten fast bis zu ihrer Kapazitätsgrenze gefüllt, wobei ausreichend Speicherplatz für mindestens eine Zeile mit der maximal für diesen Index möglichen Größe frei bleibt; diese ergibt sich aus der Schlüsselmenge auf den Zwischenseiten. Der Standardwert ist OFF.  
  
 FILLFACTOR  **=**  *Fillfactor*  
 Gibt einen Prozentwert an, der dem Füllfaktor entspricht. Dieser Faktor legt fest, wie weit die [!INCLUDE[ssDE](../../includes/ssde-md.md)] die Blattebene jeder Indexseite während der Indexerstellung oder -änderung auffüllen soll.  *FILLFACTOR* muss ein ganzzahliger Wert zwischen 1 und 100 sein. Die Standardeinstellung ist 0. Die Füllfaktorwerte 0 und 100 sind in jeder Hinsicht identisch.  
  
 IGNORE_DUP_KEY = {ON | **OFF** }  
 Gibt die Fehlermeldung an, wenn ein Einfügevorgang versucht, doppelte Schlüsselwerte in einen eindeutigen Index einzufügen. Die IGNORE_DUP_KEY-Option gilt nur für Einfügevorgänge nach dem Erstellen oder Neuerstellen des Index. Die Option hat keine Auswirkungen, bei der Ausführung [CREATE INDEX](../../t-sql/statements/create-index-transact-sql.md), [ALTER INDEX](../../t-sql/statements/alter-index-transact-sql.md), oder [UPDATE](../../t-sql/queries/update-transact-sql.md). Der Standardwert ist OFF.  
  
 ON  
 Eine Warnmeldung wird ausgegeben, wenn doppelte Schlüsselwerte in einen eindeutigen Index eingefügt werden. Es schlagen nur die Zeilen fehl, die gegen die Eindeutigkeitseinschränkung verstoßen.  
  
 OFF  
 Eine Fehlermeldung wird ausgegeben, wenn doppelte Schlüsselwerte in einen eindeutigen Index eingefügt werden. Für den gesamten INSERT-Vorgang wird ein Rollback ausgeführt.  
  
 IGNORE_DUP_KEY kann für Indizes, die für eine Sicht erstellt werden, nicht eindeutige Indizes, XML-Indizes, räumliche und gefilterte Indizes nicht auf ON festgelegt werden.  
  
 Um IGNORE_DUP_KEY anzuzeigen, verwenden Sie [sys.indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md).  
  
 In abwärtskompatibler Syntax ist WITH IGNORE_DUP_KEY gleichwertig mit WITH IGNORE_DUP_KEY = ON.  
  
 STATISTICS_NORECOMPUTE  **=**  {ON | **OFF** }  
 Bei der Einstellung ON werden veraltete Indexstatistiken nicht automatisch neu berechnet. Bei der Einstellung OFF sind automatische Statistikupdates aktiviert. Der Standardwert ist OFF.  
  
 ALLOW_ROW_LOCKS  **=**  { **ON** | {OFF}  
 Bei der Einstellung ON sind Zeilensperren beim Zugriff auf den Index zulässig. Das [!INCLUDE[ssDE](../../includes/ssde-md.md)] bestimmt, wann Zeilensperren verwendet werden. Bei OFF werden Zeilensperren nicht verwendet. Der Standardwert ist ON.  
  
 ALLOW_PAGE_LOCKS  **=**  { **ON** | {OFF}  
 Bei der Einstellung ON sind Seitensperren beim Zugriff auf den Index zulässig. Das [!INCLUDE[ssDE](../../includes/ssde-md.md)] bestimmt, wann Seitensperren verwendet werden. Bei der Einstellung OFF werden Seitensperren nicht verwendet. Der Standardwert ist ON.  
  
 FILETABLE_DIRECTORY = *Directory_name*  
   
  
**Gilt für**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. 
  
 Gibt den Namen der Windows-kompatiblen FileTable-Verzeichnis. Dieser Name sollte für alle FileTable-Verzeichnisnamen in der Datenbank eindeutig sein. Bei Eindeutigkeitsvergleichen wird unabhängig von den Sortiereinstellungen die Groß-/Kleinschreibung nicht beachtet. Wenn dieser Wert nicht angegeben ist, wird Name der Dateitabelle verwendet.  
  
 FILETABLE_COLLATE_FILENAME = { *Collation_name* | Database_default}  
   
  
**Gilt für**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. 
  
 Gibt den Namen der Sortierung an, die auf die **Name** -Spalte in der FileTable angewendet werden soll. Zur Einhaltung der Windows-Dateinamensemantik darf bei der Sortierung die Groß-/Kleinschreibung nicht beachtet werden. Wenn dieser Wert nicht angegeben ist, wird die Standardsortierung für die Datenbank verwendet. Wenn bei der Datenbank-Standardsortierung die Groß-/Kleinschreibung beachtet wird, wird ein Fehler ausgelöst, und der CREATE TABLE-Vorgang kann nicht durchgeführt werden.  
  
 *Sortierungsname*  
 Der Name einer Sortierung, bei der die Groß-/Kleinschreibung nicht beachtet wird.  
  
 database_default  
 Gibt an, dass die Standardsortierung für die Datenbank verwendet werden soll. Bei dieser Sortierung darf die Groß-/Kleinschreibung nicht beachtet werden.  
  
 FILETABLE_PRIMARY_KEY_CONSTRAINT_NAME = *Constraint_name*  
   
**Gilt für**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. 
  
 Gibt den Namen an, der für die Primärschlüsseleinschränkung verwendet werden soll, die automatisch für die FileTable erstellt wird. Wenn dieser Wert nicht angegeben ist, wird ein Name für die Einschränkung generiert.  
  
 FILETABLE_STREAMID_UNIQUE_CONSTRAINT_NAME = *Constraint_name*  
   
  
**Gilt für**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. 
  
 Gibt den Namen für die unique-Einschränkung verwendet werden soll, die automatisch auf die **Stream_id** Spalte in der FileTable. Wenn dieser Wert nicht angegeben ist, wird ein Name für die Einschränkung generiert.  
  
 FILETABLE_FULLPATH_UNIQUE_CONSTRAINT_NAME = *Constraint_name*  
   
  
**Gilt für**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. 
  
 Gibt den Namen für die unique-Einschränkung verwendet werden soll, die automatisch auf die **Parent_path_locator** und **Namen** Spalten in der FileTable. Wenn dieser Wert nicht angegeben ist, wird ein Name für die Einschränkung generiert.  
  
 SYSTEM_VERSIONING  **=**  ON [(HISTORY_TABLE  **=**  *Schema_name* .  *History_table_name* [, DATA_CONSISTENCY_CHECK  **=**  { **ON** | {OFF}])]  
   
  
**Gilt für**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] und [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].   
  
 Ermöglicht versionsverwaltung durch das System der Tabelle an, wenn der Datentyp, NULL-Zulässigkeit Einschränkung und primary Key-Einschränkung-Anforderungen erfüllt sind. Wenn die **HISTORY_TABLE** nicht verwendet wird, das System generiert eine neuen Verlaufstabelle, die dem Schema der aktuellen Tabelle in derselben Dateigruppe wie die aktuelle Tabelle, erstellen eine Verknüpfung zwischen den beiden Tabellen entsprechen und kann das System Notieren Sie den Verlauf jeder Datensatz in der aktuellen Tabelle in der Verlaufstabelle. Der Name dieser Verlaufstabelle `MSSQL_TemporalHistoryFor<primary_table_object_id>`. Standardmäßig ist die Verlaufstabelle **PAGE** -komprimiert. Wenn das Argument HISTORY_TABLE einen Link zu erstellen und verwenden eine vorhandene Verlaufstabelle verwendet wird, wird die Verknüpfung zwischen der aktuellen Tabelle und der angegebenen Tabelle erstellt. Falls die aktuelle Tabelle partitioniert wurde, kann die Verlaufstabelle auf der Standarddateigruppe erstellt werden, da die Partitionierungskonfiguration nicht automatisch von der aktuellen auf die Verlaufstabelle repliziert wird. Falls der Name einer Verlaufstabelle während der Erstellung der Verlaufstabelle angegeben wird, müssen Sie das Schema und den Tabellennamen angeben. Wenn Sie einen Link zu einer vorhandenen Verlaufstabelle erstellen, können Sie eine Datenkonsistenzprüfung durchführen. Diese datenkonsistenzprüfung stellt sicher, dass vorhandene Einträge sich nicht überlappen. Die Datenkonsistenzprüfung ist standardmäßig aktiviert. Verwenden Sie dieses Argument zusammen mit der PERIOD FOR SYSTEM_TIME und generiert immer als Zeile {starten | END}-Argumente für die systemversionsverwaltung für eine Tabelle zu aktivieren. Weitere Informationen finden Sie unter [Temporal Tables](../../relational-databases/tables/temporal-tables.md).  
  
 REMOTE_DATA_ARCHIVE = {ON [( *Table_stretch_options* [,... n])] | DEAKTIVIERT (MIGRATION_STATE = ANGEHALTEN)}  
   
  
**Gilt für**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Erstellt die neue Tabelle für Stretch-Datenbank aktiviert oder deaktiviert. Weitere Informationen finden Sie unter [Stretch Database](../../sql-server/stretch-database/stretch-database.md).  
  
 **Aktivieren von Stretch-Datenbank für eine Tabelle**  
  
 Wenn Sie Stretch für eine Tabelle durch Angabe aktivieren `ON`, Sie können optional angeben, `MIGRATION_STATE = OUTBOUND` beginnen sofort, Migrieren von Daten oder `MIGRATION_STATE = PAUSED` um die Datenmigration zu verschieben. Der Standardwert lautet `MIGRATION_STATE = OUTBOUND`. Weitere Informationen zum Aktivieren von Stretch für eine Tabelle finden Sie unter [Aktivieren von Stretch-Datenbank für eine Tabelle](../../sql-server/stretch-database/enable-stretch-database-for-a-table.md).  
  
 **Voraussetzungen**. Bevor Sie Stretch für eine Tabelle aktivieren, müssen Sie Stretch aktivieren, auf dem Server und in der Datenbank. Weitere Informationen finden Sie unter [Enable Stretch Database for a database](../../sql-server/stretch-database/enable-stretch-database-for-a-database.md).  
  
 **Berechtigungen**. Aktivieren von Stretch für eine Datenbank oder einer Tabelle erfordert Db_owner-Berechtigungen. Aktivieren von Stretch für eine Tabelle benötigen Sie außerdem ALTER-Berechtigungen für die Tabelle.  
  
 [FILTER_PREDICATE = {null | *Prädikat* }]  
   
  
**Gilt für**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Gibt optional ein Filterprädikat zum Auswählen von Zeilen aus einer Tabelle zu migrieren, die Verlaufsdaten und aktuelle Daten enthält. Das Prädikat muss eine deterministische Inline-Tabellenwertfunktion aufrufen. Weitere Informationen finden Sie unter [Aktivieren von Stretch-Datenbank für eine Tabelle](../../sql-server/stretch-database/enable-stretch-database-for-a-table.md) und [auswählen zu migrierender mithilfe einer Filterfunktion Zeilen](../../sql-server/stretch-database/select-rows-to-migrate-by-using-a-filter-function-stretch-database.md). 
   
> [!IMPORTANT]  
>  Wenn Sie ein schwaches Filterprädikat angeben, wird die Datenmigration ebenfalls unzureichend ausgeführt. Stretch-Datenbank wendet das Filterprädikat über den CROSS APPLY-Operator auf die Tabelle an.  
  
 Wenn Sie kein Filterprädikat angeben, wird die gesamte Tabelle migriert.  
  
 Wenn Sie kein Filterprädikat angeben, müssen Sie auch angeben *MIGRATION_STATE*.  
  
 MIGRATION_STATE = {AUSGEHENDE |  EINGEHENDE | ANGEHALTEN}  
   
  
**Gilt für**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], und SQL Azure. 
  
-   Geben Sie `OUTBOUND` zum Migrieren von Daten aus SQL Server in Azure.  
  
-   Geben Sie `INBOUND` So kopieren Sie die Remote-Daten für die Tabelle aus Azure zu SQL Server und zum Deaktivieren von Stretch für die Tabelle zurück. Weitere Informationen finden Sie unter [Deaktivieren von Stretch Database und Zurückholen von Remotedaten](../../sql-server/stretch-database/disable-stretch-database-and-bring-back-remote-data.md).  
  
     Dieser Vorgang verursacht Datenübertragungskosten und kann nicht abgebrochen werden.  
  
-   Geben Sie `PAUSED` anhalten oder Zurückstellen der Datenmigration. Weitere Informationen finden Sie unter [anhalten und Fortsetzen der Datenmigration &#40; Stretch-Datenbank &#41; ](../../sql-server/stretch-database/pause-and-resume-data-migration-stretch-database.md).  
  
 MEMORY_OPTIMIZED  
   
  
**Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] und [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
 Die Wert ON gibt an, dass die Tabelle speicheroptimiert ist. Speicheroptimierte Tabellen sind Teil des In-Memory-OLTP-Features, die optimiert die Leistung der transaktionsverarbeitung verwendet wird. Erste Schritte mit In-Memory OLTP finden Sie unter [Schnellstart 1: In-Memory-OLTP-Technologien für schneller Transact-SQL-Leistung](../../relational-databases/in-memory-oltp/survey-of-initial-areas-in-in-memory-oltp.md). Ausführlichere Informationen zu speicheroptimierten Tabellen finden Sie unter [speicheroptimierter Tabellen](../../relational-databases/in-memory-oltp/memory-optimized-tables.md).  
  
 Der Standardwert zeigt OFF an, dass die Tabelle datenträgerbasierte.  
  
 DURABILITY  
   
  
**Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] und [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].   
  
 Der Wert von SCHEMA_AND_DATA gibt an, dass die Tabelle dauerhaft ist, was bedeutet, dass Änderungen auf dem Datenträger beibehalten werden und Neustart oder ein Failover überstehen.  SCHEMA_AND_DATA ist der Standardwert.  
  
 Der Wert von SCHEMA_ONLY gibt an, dass die Tabelle nicht dauerhaft ist. Das Tabellenschema wird beibehalten, aber Datenupdates werden nach einem Neustart oder ein Failover der Datenbank nicht beibehalten. DURABILITY = SCHEMA_ONLY ist nur zulässig, mit MEMORY_OPTIMIZED = ON.  
  
> [!WARNING]  
>  Wenn eine Tabelle erstellt wird, mit **DURABILITY = SCHEMA_ONLY**, und **READ_COMMITTED_SNAPSHOT** wird anschließend mit geändert **ALTER DATABASE**, Daten in der Tabelle gehen verloren.  
  
 BUCKET_COUNT  
   
  
**Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] und [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]. 
  
 Gibt die Anzahl der Buckets an, die im Hashindex erstellt werden sollen. Der maximale Wert für BUCKET_COUNT in Hashindizes beträgt 1.073.741.824. Weitere Informationen zu bucketanzahlen finden Sie unter [Indizes für Speicheroptimierte Tabellen](../../relational-databases/in-memory-oltp/indexes-for-memory-optimized-tables.md).  
  
 Bucket_count ist ein erforderliches Argument.  
  
 INDEX  
   
  
**Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] und [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]. 
  
Spalten- und Tabellenindizes können als Teil der CREATE TABLE-Anweisung angegeben werden. Informationen zum Hinzufügen und Entfernen von Indizes für Speicheroptimierte Tabellen finden Sie unter: [Ändern von speicheroptimierten Tabellen](../../relational-databases/in-memory-oltp/altering-memory-optimized-tables.md)
  
 HASH  
   
  
**Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] und [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]. 
  
 Gibt an, dass ein HASH-Index erstellt wird.  
  
 Hashindizes werden nur für speicheroptimierte Tabellen unterstützt.  
  
## <a name="remarks"></a>Hinweise  
 Informationen über die Anzahl der zulässigen Tabellen, Spalten, Einschränkungen und Indizes finden Sie unter [Maximum Capacity Specifications for SQL Server](../../sql-server/maximum-capacity-specifications-for-sql-server.md).  
  
 Der Speicherplatz für Tabellen und Indizes wird i. A. jeweils blockweise zugeordnet. Wenn die Option SET MIXED_PAGE_ALLOCATION von ALTER DATABASE auf festgelegt ist "true" oder immer vor [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], wenn eine Tabelle oder ein Index erstellt wird, wird Seiten aus gemischten Blöcken zugeordnet werden, bis es genügend Seiten für einen einheitlichen Block ausreichen vorhanden sind. Wenn genügend Seiten für einen einheitlichen Block vorhanden sind, wird jedes Mal dann ein weiterer Block zugeordnet, wenn die bereits zugeordneten Blöcke voll sind. Führen Sie für einen Bericht über die Menge des Speicherplatzes, die von einer Tabelle belegten und verwendeten **Sp_spaceused**.  
  
 Das [!INCLUDE[ssDE](../../includes/ssde-md.md)] erzwingt keine Reihenfolge für die Angabe von DEFAULT, IDENTITY, ROWGUIDCOL oder Spalteneinschränkungen in einer Spaltendefinition.  
  
 Beim Erstellen einer Tabelle wird die Option QUOTED IDENTIFIER immer mit der Einstellung ON in den Metadaten der Tabelle gespeichert, und zwar auch dann, wenn die Option beim Erstellen der Tabelle auf OFF festgelegt ist.  
  
## <a name="temporary-tables"></a>Temporäre Tabellen  
 Sie können sowohl lokale als auch globale temporäre Tabellen erstellen. Lokale temporäre Tabellen sind nur während der aktuellen Sitzung sichtbar; globale temporäre Tabellen sind von allen Sitzungen aus sichtbar. Temporäre Tabellen können nicht partitioniert werden.  
  
 Präfix der lokalen temporären Tabellennamen ein einzelnes Nummernzeichen (#*Table_name*), globalen temporären Tabellennamen ein doppelten Nummernzeichen voran (##*Table_name*).  
  
 SQL-Anweisungen die temporäre Tabelle verweisen, indem der angegebene Wert für *Table_name* in der CREATE TABLE-Anweisung für Beispiel ###:  
  
```  
CREATE TABLE #MyTempTable (cola INT PRIMARY KEY);  
  
INSERT INTO #MyTempTable VALUES (1);  
```  
  
 Wenn mehr als eine temporäre Tabelle innerhalb einer einzigen gespeicherten Prozedur oder innerhalb eines Batches erstellt wird, müssen verschiedene Namen für die temporären Tabellen verwendet werden.  
  
 Wenn eine lokale temporäre Tabelle in einer gespeicherten Prozedur oder einer Anwendung erstellt wird, die von mehreren Benutzern gleichzeitig ausgeführt werden kann, muss es dem [!INCLUDE[ssDE](../../includes/ssde-md.md)] möglich sein, die von den verschiedenen Benutzern erstellten Tabellen zu unterscheiden. Zu diesem Zweck fügt das [!INCLUDE[ssDE](../../includes/ssde-md.md)] intern ein numerisches Suffix an alle Namen lokaler temporärer Tabellen an. Der vollständige Name einer temporären Tabelle als gespeicherte in der **Sysobjects** in Tabelle **Tempdb** setzt sich aus den Tabellennamen in der CREATE TABLE-Anweisung und die vom System generierten numerischen Suffix angegeben. Das Suffix sicherungsspeicherverwendung *Table_name* angegebene für ein lokaler temporären Namen 116 Zeichen nicht überschreiten darf.  
  
 Temporäre Tabellen werden automatisch gelöscht, wenn sie nicht mehr gültig sind, es sei denn, sie wurden bereits explizit mithilfe von DROP TABLE gelöscht:  
  
-   Eine lokale temporäre Tabelle, die in einer gespeicherten Prozedur erstellt wurde, wird bei Beendigung der gespeicherten Prozedur automatisch gelöscht. Auf die Tabelle kann durch geschachtelte gespeicherte Prozeduren verwiesen werden, die von der gespeicherten Prozedur ausgeführt werden, die die Tabelle erstellt hat. Auf die Tabelle kann nicht durch den Vorgang verwiesen werden, der die gespeicherte Prozedur, die die Tabelle erstellt hat, aufgerufen hat.  
  
-   Alle anderen lokalen temporären Tabellen werden am Ende der aktuellen Sitzung automatisch gelöscht.  
  
-   Eine globale temporäre Tabelle wird automatisch gelöscht, wenn die Sitzung, die die betreffende Tabelle erstellt hat, beendet wird und kein Task mehr auf die Tabelle verweist. Die Zuordnung zwischen einem Task und einer Tabelle wird nur für die Dauer einer einzelnen [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisung aufrechterhalten. Das bedeutet, dass eine globale temporäre Tabelle bei Beendigung der letzten [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisung gelöscht wird, die aktiv auf die Tabelle verwiesen hat, als die Sitzung, die die Tabelle erstellt hat, beendet wurde.  
  
 Eine lokale temporäre Tabelle, die in einer gespeicherten Prozedur oder einem Trigger erstellt wurde, kann den gleichen Namen wie eine temporäre Tabelle haben, die vor dem Aufruf der gespeicherten Prozedur oder des Triggers erstellt wurde. Wenn jedoch eine Abfrage auf eine temporäre Tabelle verweist und zu diesem Zeitpunkt zwei temporäre Tabellen mit demselben Namen vorhanden sind, ist nicht definiert, anhand welcher Tabelle die Abfrage aufgelöst werden soll. Eine geschachtelte gespeicherte Prozedur kann ebenfalls eine temporäre Tabelle mit demselben Namen wie eine temporäre Tabelle erstellen, die von der gespeicherten Prozedur erstellt wurde, die die geschachtelte gespeicherte Prozedur aufgerufen hat. Damit jedoch Änderungsanweisungen anhand der Tabelle aufgelöst werden können, die in der geschachtelten Prozedur erstellt wurde, muss die Tabelle die gleiche Struktur mit den gleichen Spaltennamen wie die Tabelle aufweisen, die in der aufrufenden Prozedur erstellt wurde. Dies wird im folgenden Beispiel gezeigt.  
  
```  
CREATE PROCEDURE dbo.Test2  
AS  
    CREATE TABLE #t(x INT PRIMARY KEY);  
    INSERT INTO #t VALUES (2);  
    SELECT Test2Col = x FROM #t;  
GO  
  
CREATE PROCEDURE dbo.Test1  
AS  
    CREATE TABLE #t(x INT PRIMARY KEY);  
    INSERT INTO #t VALUES (1);  
    SELECT Test1Col = x FROM #t;  
EXEC Test2;  
GO  
  
CREATE TABLE #t(x INT PRIMARY KEY);  
INSERT INTO #t VALUES (99);  
GO  
  
EXEC Test1;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 (1 row(s) affected) 
 Test1Col 
 ----------- 
 1 

 (1 row(s) affected) 
 Test2Col 
 ----------- 
 2 
 ```
  
 Beim Erstellen lokaler oder globaler temporärer Tabellen unterstützt die Syntax der CREATE TABLE-Anweisung Einschränkungsdefinitionen mit Ausnahme von FOREIGN KEY-Einschränkungen. Wenn eine FOREIGN KEY-Einschränkung in einer temporären Tabelle angegeben wird, gibt die Anweisung ein Warnmeldung zurück, die besagt, dass die Einschränkung nicht berücksichtigt wurde. Die Tabelle wird dennoch, jedoch ohne die FOREIGN KEY-Einschränkungen erstellt. In FOREIGN KEY-Einschränkungen kann nicht auf temporäre Tabellen verwiesen werden.  
  
 Wenn eine temporäre Tabelle mit einer benannten Einschränkung und innerhalb des Bereichs einer benutzerdefinierten Transaktion erstellt wird, kann jeweils nur ein Benutzer die Anweisung ausführen, mit der die temporäre Tabelle erstellt wird. Wenn zum Beispiel eine gespeicherte Prozedur eine temporäre Tabelle mit einer benannten Primärschlüsseleinschränkung erstellt, kann die gespeicherte Prozedur nicht von mehreren Benutzern gleichzeitig ausgeführt werden.  


## <a name="database-scoped-global-temporary-tables-azure-sql-database"></a>Datenbankweit gültige globale temporäre Tabellen (Azure SQL-Datenbank)

Globale temporäre Tabellen für SQL Server (mit initiiert ## Tabellennamen) werden in Tempdb gespeichert und für alle Benutzer Sitzungen freigegeben werden, in der gesamten SQL Server-Instanz. Informationen für SQL-Tabellentypen finden Sie unter im obigen Abschnitt für Tabellen zu erstellen.  

Azure SQL-Datenbank unterstützt globale temporäre Tabellen, die auch in Tempdb gespeichert und auf Datenbankebene beschränkt.  Dies bedeutet, dass globale temporäre Tabellen für alle Benutzer Sitzungen innerhalb der gleichen Azure SQL-Datenbank gemeinsam genutzt werden. Benutzersitzungen, die von anderen Azure SQL-Datenbanken können nicht globale temporäre Tabellen zugreifen.

Globale temporäre Tabellen für Azure SQL-Datenbank führen Sie die gleichen Syntax und Semantik, die SQL Server für temporäre Tabellen verwendet.  Auf ähnliche Weise sind globale temporäre gespeicherte Prozeduren auch auf Datenbankebene in Azure SQL-Datenbank beschränkt. Lokale temporäre Tabellen (eingeleitet mit # Tabellennamen) auch für Azure SQL-Datenbank unterstützt werden, und folgen Sie der gleichen Syntax und Semantik, die SQL Server verwendet.  Finden Sie im obigen Abschnitt [temporäre Tabellen](#temporary-tables).  

> [!IMPORTANT]
> Dieses Feature ist in der öffentlichen Vorschau und steht für die Azure SQL-Datenbank.
>

### <a name="troubleshooting-global-temporary-tables-for-azure-sql-db"></a>Problembehandlung bei globalen temporären Tabellen für Azure SQL-Datenbank 

Die Problembehandlung der Tempdb, finden Sie unter [nicht genügend Speicherplatz zur Problembehandlung verfügbar in ' tempdb '](https://technet.microsoft.com/library/ms176029%28v=sql.105%29.aspx?f=255&MSPPError=-2147217396). Um die Problembehandlung DMVs in Azure SQL-Datenbank zuzugreifen, müssen Sie ein Serveradministrator sein.
  
### <a name="permissions"></a>Berechtigungen  

 Jeder Benutzer kann die globale temporäre Objekte erstellen. Benutzer haben nur Zugriff auf ihre eigenen Objekte, es sei denn, ihnen wurden zusätzliche Berechtigungen zugewiesen. zugreifen.  
  
### <a name="examples"></a>Beispiele 

- Sitzung A erstellt eine globale temporäre Tabelle ##test in Azure SQL-Datenbank testdb1 und fügt die Zeile 1

```tsql
CREATE TABLE ##test ( a int, b int);
INSERT INTO ##test values (1,1);

--Obtain object ID for temp table ##test 
SELECT OBJECT_ID('tempdb.dbo.##test') AS 'Object ID'; 

---Result
1253579504

---Obtain global temp table name for a given object ID 1253579504 in tempdb (2)
SELECT name FROM tempdb.sys.objects WHERE object_id = 1253579504

---Result
##test
```
- Sitzung B testdb1 Azure SQL-Datenbank her und kann auf die Tabelle erstellt, indem die Sitzung ein ##test zugreifen

```tsql
SELECT * FROM ##test
---Results
1,1
```

- C-Sitzung in eine andere Datenbank in Azure SQL-Datenbank testdb2 her und erstellt in testdb&#1;#test zugreifen möchte. Wählen Sie diese ein Fehler auftritt, aufgrund des Datenbankbereichs für die globalen temporären Tabellen 

```tsql
SELECT * FROM ##test
---Results
Msg 208, Level 16, State 0, Line 1
Invalid object name '##test'
```

- Systemobjekt in Azure SQL-Datenbank Tempdb vom aktuellen Benutzer Datenbank testdb1 Adressierung

```tsql
SELECT * FROM tempdb.sys.objects
SELECT * FROM tempdb.sys.columns
SELECT * FROM tempdb.sys.database_files
```



## <a name="partitioned-tables"></a>Partitionierte Tabellen  
 Bevor eine partitionierte Tabelle mithilfe von CREATE TABLE erstellt wird, müssen Sie zuerst eine Partitionsfunktion erstellen, um anzugeben, wie die Tabelle partitioniert werden soll. Eine Partitionsfunktion wird erstellt, indem Sie mithilfe von [CREATE PARTITION FUNCTION](../../t-sql/statements/create-partition-function-transact-sql.md). Darüber hinaus müssen Sie ein Partitionsschema erstellen, um die Dateigruppen anzugeben, die die von der Partitionsfunktion angegebenen Partitionen aufnehmen. Ein Partitionsschema wird erstellt, indem Sie mithilfe von [CREATE PARTITION SCHEME](../../t-sql/statements/create-partition-scheme-transact-sql.md). Das Platzieren von PRIMARY KEY- oder UNIQUE-Einschränkungen in verschiedenen Dateigruppen ist bei partitionierten Tabellen nicht möglich. Weitere Informationen finden Sie unter [Partitioned Tables and Indexes](../../relational-databases/partitions/partitioned-tables-and-indexes.md).  
  
## <a name="primary-key-constraints"></a>PRIMARY KEY-Einschränkungen  
  
-   Eine Tabelle kann nur eine PRIMARY KEY-Einschränkung enthalten.  
  
-   Der durch eine PRIMARY KEY-Einschränkung generierte Index kann nicht dazu führen, dass die Anzahl der Indizes der Tabelle 999 nicht gruppierte Indizes und 1 gruppierten Index übersteigt.  
  
-   Wenn CLUSTERED oder NONCLUSTERED für eine PRIMARY KEY-Einschränkung nicht angegeben ist, wird CLUSTERED verwendet, sofern keine gruppierten Indizes für UNIQUE-Einschränkungen angegeben sind.  
  
-   Alle Spalten, für die eine PRIMARY KEY-Einschränkung definiert wurde, müssen als NOT NULL definiert sein. Falls weder NULL noch NOT NULL angegeben ist, wird für alle Spalten, auf die eine PRIMARY KEY-Einschränkung angewendet wird, die NULL-Zulässigkeit auf NOT NULL festgelegt.  
  
    > [!NOTE]  
    >  Für Speicheroptimierte Tabellen ist die NULLable-Spalte zulässig.  
  
-   Wenn ein Primärschlüssel für eine Spalte eines CLR-benutzerdefinierten Typs definiert wird, muss die Implementierung des Typs eine binäre Sortierreihenfolge unterstützen. Weitere Informationen finden Sie unter [Benutzerdefinierte CLR-Typen](../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md).  
  
## <a name="unique-constraints"></a>UNIQUE-Einschränkungen  
  
-   Wenn CLUSTERED oder NONCLUSTERED für eine UNIQUE-Einschränkung nicht angegeben ist, wird standardmäßig NONCLUSTERED verwendet.  
  
-   Jede UNIQUE-Einschränkung erzeugt einen Index. Die Anzahl der UNIQUE-Einschränkungen kann nicht dazu führen, dass die Anzahl der Indizes der Tabelle 999 nicht gruppierte Indizes und 1 gruppierten Index übersteigt.  
  
-   Wenn eine UNIQUE-Einschränkung für eine Spalte eines CLR-benutzerdefinierten Typs definiert wird, muss die Implementierung des Typs eine binäre oder operatorbasierte Sortierreihenfolge unterstützen. Weitere Informationen finden Sie unter [Benutzerdefinierte CLR-Typen](../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md).  
  
## <a name="foreign-key-constraints"></a>FOREIGN KEY-Einschränkungen  
  
-   Wenn ein anderer Wert als NULL in die Spalte einer FOREIGN KEY-Einschränkung eingegeben wird, muss der Wert in der Spalte vorhanden sein, auf die verwiesen wird; andernfalls wird eine Fremdschlüsselverletzungs-Fehlermeldung zurückgegeben.  
  
-   FOREIGN KEY-Einschränkungen werden auf die vorangegangene Spalte angewendet, es sei denn, es werden Quellspalten angegeben.  
  
-   FOREIGN KEY-Einschränkungen können nur auf Tabellen verweisen, die sich innerhalb derselben Datenbank auf demselben Server befinden. Datenbankübergreifende referenzielle Integrität muss durch Trigger implementiert werden. Weitere Informationen finden Sie unter [CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md).  
  
-   FOREIGN KEY-Einschränkungen können auf eine andere Spalte in derselben Tabelle verweisen. Ein solcher Verweis wird als Eigenverweis bezeichnet.  
  
-   Die REFERENCES-Klausel einer FOREIGN KEY-Einschränkung auf Spaltenebene kann nur eine Verweisspalte auflisten. Diese Spalte muss denselben Datentyp aufweisen wie die Spalte, für die die Einschränkung definiert wurde.  
  
-   Die REFERENCES-Klausel einer FOREIGN KEY-Einschränkung auf Tabellenebene muss ebenso viele Verweisspalten haben, wie sich Spalten in der Einschränkungsspaltenliste befinden. Der Datentyp jeder Verweisspalte muss ebenfalls mit dem der entsprechenden Spalte in der Spaltenliste übereinstimmen.  
  
-   CASCADE, SET NULL oder SET DEFAULT kann nicht angegeben werden, wenn eine Spalte vom Typ **Zeitstempel** ist Teil des Fremdschlüssels oder des Schlüssels auf die verwiesen wird.  
  
-   CASCADE, SET NULL, SET DEFAULT und NO ACTION können für Tabellen kombiniert werden, die referenzielle Beziehungen untereinander aufweisen. Wenn das [!INCLUDE[ssDE](../../includes/ssde-md.md)] die Einstellung NO ACTION feststellt, wird die Verarbeitung beendet und ein Rollback für verbundene CASCADE-, SET NULL- und SET DEFAULT-Aktionen ausgeführt. Wenn eine DELETE-Anweisung eine Kombination aus CASCADE-, SET NULL-, SET DEFAULT- und NO ACTION-Aktionen bewirkt, werden alle CASCADE-, SET NULL- und SET DEFAULT-Aktionen angewendet, bevor das [!INCLUDE[ssDE](../../includes/ssde-md.md)] nach der möglichen Angabe von NO ACTION sucht.  
  
-   Das [!INCLUDE[ssDE](../../includes/ssde-md.md)] verfügt über keine vordefinierte Grenze hinsichtlich der Anzahl von FOREIGN KEY-Einschränkungen, die eine Tabelle, die auf andere Tabellen verweist, enthalten kann, oder hinsichtlich der Anzahl von FOREIGN KEY-Einschränkungen im Besitz anderer Tabellen, die auf eine bestimmte Tabelle verweisen.  
  
     Nichtsdestotrotz ist die tatsächliche Anzahl von FOREIGN KEY-Einschränkungen , die verwendet werden können, durch die Hardwarekonfiguration und den Entwurf der Datenbank und der Anwendung begrenzt. Als Empfehlung gilt, dass eine Tabelle maximal 253 FOREIGN KEY-Einschränkungen enthalten sollte und dass maximal 253 FOREIGN KEY-Einschränkungen auf eine Tabelle verweisen sollten. Die in Ihrem Fall tatsächlich gültige Grenze kann je nach Anwendung und Hardware darüber oder darunter liegen. Beim Entwerfen von Datenbank und Anwendungen sollten Sie die Kosten für das Erzwingen von FOREIGN KEY-Einschränkungen berücksichtigen.  
  
-   FOREIGN KEY-Einschränkungen werden nicht auf temporäre Tabellen angewendet.  
  
-   FOREIGN KEY-Einschränkungen können nur auf Spalten in PRIMARY KEY- oder UNIQUE-Einschränkungen in der Tabelle, auf die verwiesen wird, oder auf eine UNIQUE INDEX-Einschränkung für die Tabelle, auf die verwiesen wird, verweisen.  
  
-   Wenn ein Fremdschlüssel für eine Spalte eines CLR-benutzerdefinierten Typs definiert wird, muss die Implementierung des Typs eine binäre Sortierreihenfolge unterstützen. Weitere Informationen finden Sie unter [Benutzerdefinierte CLR-Typen](../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md).  
  
-   Für Spalten, die an einer Fremdschlüsselbeziehung beteiligt sind, muss die gleiche Länge und Skala definiert sein.  
  
## <a name="default-definitions"></a>DEFAULT-Definitionen  
  
-   Eine Spalte kann nur eine DEFAULT-Definition haben.  
  
-   Eine DEFAULT-Definition kann konstante Werte, Funktionen, standardmäßige NILADIC-SQL-Funktionen oder NULL enthalten. Die folgende Tabelle zeigt die Funktionen ohne Argumente und die Werte, die sie während einer INSERT-Anweisung für den Standardwert zurückgeben.  
  
    |SQL-92-Funktion ohne Argumente|Rückgabewert|  
    |------------------------------|--------------------|  
    |CURRENT_TIMESTAMP|Aktuelles Datum und aktuelle Uhrzeit.|  
    |CURRENT_USER|Name des Benutzers, der einen Einfügevorgang ausführt.|  
    |SESSION_USER|Name des Benutzers, der einen Einfügevorgang ausführt.|  
    |SYSTEM_USER|Name des Benutzers, der einen Einfügevorgang ausführt.|  
    |Benutzer|Name des Benutzers, der einen Einfügevorgang ausführt.|  
  
-   *Constant_expression* Definition kann nicht in einer STANDARDMÄßIGEN verweisen, auf eine andere Spalte in der Tabelle oder auf andere Tabellen, Sichten oder gespeicherte Prozeduren.  
  
-   DEFAULT-Definitionen können nicht erstellt werden, für Spalten mit einem **Zeitstempel** -Datentyp oder Spalten mit einer IDENTITY-Eigenschaft.  
  
-   DEFAULT-Definitionen können nicht für Spalten mit Aliasdatentypen erstellt werden, wenn der Aliasdatentyp an ein Standardobjekt gebunden ist.  
  
## <a name="check-constraints"></a>CHECK-Einschränkungen  
  
-   Eine Spalte kann beliebig viele CHECK-Einschränkungen haben, und die Bedingung kann mehrere logische Ausdrücke enthalten, die mit AND und OR verknüpft sind. Mehrere CHECK-Einschränkungen für eine Spalte werden in der Reihenfolge überprüft, in der sie erstellt wurden.  
  
-   Die Suchbedingung muss einen booleschen Ausdruck ergeben und darf nicht auf eine andere Tabelle verweisen.  
  
-   Eine CHECK-Einschränkung auf Spaltenebene kann nur auf die von der Einschränkung betroffene Spalte verweisen, und eine CHECK-Einschränkung auf Tabellenebene kann nur auf Spalten derselben Tabelle verweisen.  
  
     CHECK-Einschränkungen und Regeln dienen beide zur Überprüfung der Daten während INSERT- und UPDATE-Anweisungen.  
  
-   Sobald eine Regel und mindestens eine CHECK-Einschränkung für eine oder mehrere Spalten vorhanden sind, werden alle Einschränkungen ausgewertet.  
  
-   CHECK-Einschränkungen können nicht definiert werden **Text**, **Ntext**, oder **Image** Spalten.  
  
## <a name="additional-constraint-information"></a>Weitere Informationen zu Einschränkungen  
  
-   Ein für eine Einschränkung erstellter Index kann nicht mit der DROP INDEX-Anweisung gelöscht werden. Die Einschränkung muss mithilfe von ALTER TABLE gelöscht werden. Ein Index, der für eine Einschränkung erstellt wurde und von ihr verwendet wird, kann mithilfe von ALTER INDEX...REBUILD neu erstellt werden. Weitere Informationen finden Sie unter [Neuorganisieren und Neuerstellen von Indizes](../../relational-databases/indexes/reorganize-and-rebuild-indexes.md).  
  
-   Einschränkungsnamen müssen die Regeln für [Bezeichner](../../relational-databases/databases/database-identifiers.md), außer dass der Name nicht werden mit einem Nummernzeichen gestartet (#). Wenn *Constraint_name* ist nicht angegeben wird, wird die Einschränkung eine vom System generierter Name zugewiesen. Der Einschränkungsname wird in jeder Fehlermeldung über Einschränkungsverletzungen angezeigt.  
  
-   Wenn eine Einschränkung in einer INSERT-, UPDATE- oder DELETE-Anweisung verletzt wird, wird die Anweisung beendet. Wenn SET XACT_ABORT jedoch auf OFF festgelegt ist, wird die Verarbeitung der Transaktion – falls die Anweisung Teil einer expliziten Transaktion ist – fortgesetzt. Wenn SET XACT_ABORT auf ON festgelegt ist, wird für die ganze Transaktion ein Rollback ausgeführt. Sie können auch die ROLLBACK TRANSACTION-Anweisung mit der Transaktionsdefinition verwenden, indem Sie überprüfen den @@ERROR -Systemfunktion.  
  
-   Wenn ALLOW_ROW_LOCKS auf ON und ALLOW_PAGE_LOCK auf ON festgelegt ist, sind Sperren auf Zeilen-, Seiten- und Tabellenebene beim Zugriff auf den Index zulässig. Das [!INCLUDE[ssDE](../../includes/ssde-md.md)] wählt die geeignete Sperre aus und kann die Sperre von einer Zeilen- oder Seitensperre auf eine Tabellensperre ausweiten. Wenn ALLOW_ROW_LOCKS auf OFF und ALLOW_PAGE_LOCK auf OFF festgelegt sind, sind beim Zugriff auf den Index nur Sperren auf Tabellenebene zulässig.  
  
-   Wenn eine Tabelle FOREIGN KEY- oder CHECK-Einschränkungen und Trigger hat, werden die Einschränkungsbedingungen ausgewertet, bevor der Trigger ausgeführt wird.  
  
 Verwenden Sie für einen Bericht auf eine Tabelle und deren Spalten, **Sp_help** oder **Sp_helpconstraint**. Verwenden Sie zum Umbenennen einer Tabelle **"Sp_rename"**. Verwenden Sie für einen Bericht zu den Sichten und gespeicherte Prozeduren, die von einer Tabelle abhängen, [Sys. dm_sql_referenced_entities](../../relational-databases/system-dynamic-management-views/sys-dm-sql-referenced-entities-transact-sql.md) und [dm_sql_referencing_entities](../../relational-databases/system-dynamic-management-views/sys-dm-sql-referencing-entities-transact-sql.md).  
  
## <a name="nullability-rules-within-a-table-definition"></a>NULL-Zulässigkeitsregeln in einer Tabellendefinition  
 Die NULL-Zulässigkeit einer Spalte bestimmt, ob diese Spalte NULL als Datenwert enthalten kann. NULL ist nicht Null oder leer. NULL bedeutet, dass kein Eintrag vorgenommen oder explizit NULL angegeben wurde, und impliziert üblicherweise, dass der Wert entweder unbekannt oder nicht anwendbar ist.  
  
 Wenn Sie CREATE TABLE- oder ALTER TABLE verwenden, um eine Tabelle zu erstellen bzw. zu ändern, wird die NULL-Zulässigkeit des in einer Spaltendefinition verwendeten Datentyps durch Datenbank- und Sitzungseinstellungen beeinflusst und möglicherweise überschrieben. Es empfiehlt sich, bei nicht berechneten Spalten stets explizit NULL oder NOT NULL für die Spalte anzugeben oder, im Falle eines benutzerdefinierten Datentyps, zuzulassen, dass die Spalte die standardmäßige NULL-Zulässigkeit des Datentyps verwendet. Spalten mit geringer Dichte müssen immer NULL zulassen.  
  
 Wenn die NULL-Zulässigkeit der Spalte nicht explizit angegeben ist, wird sie gemäß den in der folgenden Tabelle aufgeführten Regeln hergeleitet.  
  
|Spaltendatentyp|Rule|  
|----------------------|----------|  
|Alias-Datentyp|Das [!INCLUDE[ssDE](../../includes/ssde-md.md)] verwendet die NULL-Zulässigkeit, die beim Erstellen des Datentyps angegeben wurde. Um die standardmäßige NULL-Zulässigkeit des Datentyps zu bestimmen, verwenden Sie **Sp_help**.|  
|CLR-benutzerdefinierter Typ|Die NULL-Zulässigkeit wird gemäß der Spaltendefinition bestimmt.|  
|Vom System bereitgestellten Datentyp|Wenn es für den vom System bereitgestellten Datentyp nur eine Option gibt, hat diese Vorrang. **Zeitstempel** NOT NULL-Daten, die Benutzerdatentypen müssen vorhanden sein. Wenn Sitzungseinstellungen mithilfe von SET auf ON festgelegt werden, gilt Folgendes:<br />**ANSI_NULL_DFLT_ON** = ON verwenden, wird NULL zugewiesen.  <br />**ANSI_NULL_DFLT_OFF** = ON verwenden, nicht NULL zugewiesen.<br /><br /> Wenn Datenbankeinstellungen mithilfe von ALTER DATABASE konfiguriert werden, gilt Folgendes:<br />**ANSI_NULL_DEFAULT_ON** = ON verwenden, wird NULL zugewiesen.  <br />**ANSI_NULL_DEFAULT_OFF** = ON verwenden, nicht NULL zugewiesen.<br /><br /> Verwenden Sie zum Anzeigen der datenbankeinstellungen für ANSI_NULL_DEFAULT der **sys.databases** Katalogsicht|  
  
 Wenn keine der ANSI_NULL_DFLT-Optionen für die Sitzung festgelegt wurde und für die Datenbank die Standardeinstellung gilt (ANSI_NULL_DEFAULT ist auf OFF festgelegt), wird der Standardwert NOT NULL zugewiesen.  
  
 Wenn es sich bei der Spalte um eine berechnete Spalte handelt, wird die NULL-Zulässigkeit stets automatisch durch das [!INCLUDE[ssDE](../../includes/ssde-md.md)] bestimmt. Um herauszufinden, die NULL-Zulässigkeit dieser Art von Spalte, verwenden Sie die COLUMNPROPERTY-Funktion mit dem **AllowsNull** Eigenschaft.  
  
> [!NOTE]  
>  Für den SQL Server-ODBC-Treiber und den Microsoft OLE DB Provider für SQL Server ist ANSI_NULL_DFLT_ON standardmäßig auf ON festgelegt. ODBC- und OLE DB-Benutzer können dies in ODBC-Datenquellen oder mit von der Anwendung festgelegten Verbindungsattributen oder -eigenschaften konfigurieren.  
  
## <a name="data-compression"></a>Datenkomprimierung  
 Für Systemtabellen ist die Komprimierung nicht verfügbar. Bei Erstellung einer Tabelle wird die Datenkomprimierung auf NONE festgelegt, falls nicht anders angegeben. Wenn Sie eine Partitionsliste bzw. eine Partition außerhalb des zulässigen Bereichs angeben, wird ein Fehler generiert. Weitere Informationen zur Datenkomprimierung finden Sie unter [Datenkomprimierung](../../relational-databases/data-compression/data-compression.md).  
  
 Mit der gespeicherten Prozedur [sp_estimate_data_compression_savings](../../relational-databases/system-stored-procedures/sp-estimate-data-compression-savings-transact-sql.md) können Sie einschätzen, wie sich eine Änderung des Komprimierungsstatus auf eine Tabelle, einen Index oder eine Partition auswirkt.  
  
## <a name="permissions"></a>Berechtigungen  
 Es sind die CREATE TABLE-Berechtigung in der Datenbank und die ALTER-Berechtigung für das Schema erforderlich, in der die Tabelle erstellt wird.  
  
 Wenn in der CREATE TABLE-Anweisung eine Spalte als Spalte eines CLR-benutzerdefinierten Typs definiert wird, ist entweder der Besitz des Typs oder die REFERENCES-Berechtigung für den Typ erforderlich.  
  
 Wenn einer Spalte in der CREATE TABLE-Anweisung eine XML-Schemaauflistung zugeordnet ist, ist entweder der Besitz der XML-Schemaauflistung oder die REFERENCES-Berechtigung für die Auflistung erforderlich.  
  
 Jeder Benutzer kann temporäre Tabellen in ' tempdb ' erstellen.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-create-a-primary-key-constraint-on-a-column"></a>A. Erstellen einer PRIMARY KEY-Einschränkung für eine Spalte  
 Im folgenden Beispiel ist die Spaltendefinition für eine PRIMARY KEY-Einschränkung dargestellt, die über einen gruppierten Index für die `EmployeeID`-Spalte der `Employee`-Tabelle verfügt. Da kein Einschränkungsname angegeben ist, wird der Einschränkungsname vom System angegeben.  
  
```  
CREATE TABLE dbo.Employee (EmployeeID int  
PRIMARY KEY CLUSTERED);  
```  
  
### <a name="b-using-foreign-key-constraints"></a>B. Verwenden von FOREIGN KEY-Einschränkungen  
 Eine FOREIGN KEY-Einschränkung wird zum Verweisen auf eine andere Tabelle verwendet. Fremdschlüssel können einspaltige oder mehrspaltige Schlüssel sein. Dieses Beispiel zeigt eine einspaltige FOREIGN KEY-Einschränkung für die `SalesOrderHeader`-Tabelle, die auf die `SalesPerson`-Tabelle verweist. Für eine einspaltige FOREIGN KEY-Einschränkung wird nur die REFERENCES-Klausel benötigt.  
  
```  
SalesPersonID int NULL  
REFERENCES SalesPerson(SalesPersonID)  
```  
  
 Sie können auch explizit die FOREIGN KEY-Klausel verwenden und das Spaltenattribut nochmals nennen. Beachten Sie, dass der Spaltenname in den beiden Tabellen nicht identisch sein muss.  
  
```  
FOREIGN KEY (SalesPersonID) REFERENCES SalesPerson(SalesPersonID)  
```  
  
 Einschränkungen für mehrspaltige Schlüssel werden als Tabelleneinschränkungen erstellt. Die `SpecialOfferProduct`-Tabelle in der [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]-Datenbank enthält einen mehrspaltigen Primärschlüssel. Das folgende Beispiel zeigt, wie von einer anderen Tabelle aus auf diesen Schlüssel verwiesen wird; die Angabe eines expliziten Einschränkungsnamens ist optional.  
  
```  
CONSTRAINT FK_SpecialOfferProduct_SalesOrderDetail FOREIGN KEY  
 (ProductID, SpecialOfferID)  
REFERENCES SpecialOfferProduct (ProductID, SpecialOfferID)  
```  
  
### <a name="c-using-unique-constraints"></a>C. Verwenden von UNIQUE-Einschränkungen  
 UNIQUE-Einschränkungen werden verwendet, um Eindeutigkeit für Nicht-Primärschlüsselspalten zu erzwingen. Im folgenden Beispiel wird eine Einschränkung erzwungen, durch die festgelegt wird, dass die `Name`-Spalte der `Product`-Tabelle eindeutig sein muss.  
  
```  
Name nvarchar(100) NOT NULL  
UNIQUE NONCLUSTERED  
```  
  
### <a name="d-using-default-definitions"></a>D. Verwenden von DEFAULT-Definitionen  
 Standardwerte stellen jeweils einen Wert bereit (in INSERT- und UPDATE-Anweisungen), wenn kein Wert angegeben ist. Die [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]-Datenbank könnte beispielsweise eine Nachschlagetabelle enthalten, in der die verschiedenen Tätigkeiten aufgelistet sind, die Mitarbeiter in dem Unternehmen ausüben können. In einer Spalte, in der jede Tätigkeit beschrieben wird, könnte ein Zeichenfolgen-Standardwert eine Beschreibung bereitstellen, falls keine explizite Angabe einer Beschreibung erfolgt.  
  
```  
DEFAULT 'New Position - title not formalized yet'  
```  
  
 Neben Konstanten können DEFAULT-Definitionen auch Funktionen enthalten. Verwenden Sie das folgende Beispiel, um das aktuelle Datum für einen Eintrag zu erhalten.  
  
```  
DEFAULT (getdate())  
```  
  
 Eine Funktion ohne Argumente kann ebenfalls zur Verbesserung der Datenintegrität beitragen. Verwenden Sie die Funktion ohne Argumente für USER, um den Benutzer nachzuverfolgen, der eine Zeile einfügt. Schließen Sie die Funktionen ohne Argumente nicht in Klammern ein.  
  
```  
DEFAULT USER  
```  
  
### <a name="e-using-check-constraints"></a>E. Verwenden von CHECK-Einschränkungen  
 Im folgenden Beispiel wird eine Einschränkung gezeigt, die für Werte gilt, die in die `CreditRating`-Spalte der `Vendor`-Tabelle eingegeben werden. Die Einschränkung ist nicht benannt.  
  
```  
CHECK (CreditRating >= 1 and CreditRating <= 5)  
```  
  
 Dieses Beispiel zeigt eine benannte Einschränkung mit Mustereinschränkung für die Zeichendaten, die in eine Spalte einer Tabelle eingegeben werden.  
  
```  
CONSTRAINT CK_emp_id CHECK (emp_id LIKE   
'[A-Z][A-Z][A-Z][1-9][0-9][0-9][0-9][0-9][FM]'   
OR emp_id LIKE '[A-Z]-[A-Z][1-9][0-9][0-9][0-9][0-9][FM]')  
```  
  
 Dieses Beispiel gibt an, dass die Werte in einer speziellen Liste enthalten sein müssen oder einem bestimmten Muster entsprechen müssen.  
  
```  
CHECK (emp_id IN ('1389', '0736', '0877', '1622', '1756')  
OR emp_id LIKE '99[0-9][0-9]')  
```  
  
### <a name="f-showing-the-complete-table-definition"></a>F. Anzeigen der vollständigen Tabellendefinition  
 Im folgenden Beispiel werden die vollständigen Tabellendefinitionen mit allen Einschränkungsdefinitionen für die in der [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]-Datenbank erstellte `PurchaseOrderDetail`-Tabelle angezeigt. Beachten Sie, dass zum Ausführen des Beispiels das Tabellenschema nach `dbo` geändert wird.  
  
```  
CREATE TABLE dbo.PurchaseOrderDetail  
(  
    PurchaseOrderID int NOT NULL  
        REFERENCES Purchasing.PurchaseOrderHeader(PurchaseOrderID),  
    LineNumber smallint NOT NULL,  
    ProductID int NULL   
        REFERENCES Production.Product(ProductID),  
    UnitPrice money NULL,  
    OrderQty smallint NULL,  
    ReceivedQty float NULL,  
    RejectedQty float NULL,  
    DueDate datetime NULL,  
    rowguid uniqueidentifier ROWGUIDCOL  NOT NULL  
        CONSTRAINT DF_PurchaseOrderDetail_rowguid DEFAULT (newid()),  
    ModifiedDate datetime NOT NULL   
        CONSTRAINT DF_PurchaseOrderDetail_ModifiedDate DEFAULT (getdate()),  
    LineTotal  AS ((UnitPrice*OrderQty)),  
    StockedQty  AS ((ReceivedQty-RejectedQty)),  
    CONSTRAINT PK_PurchaseOrderDetail_PurchaseOrderID_LineNumber  
               PRIMARY KEY CLUSTERED (PurchaseOrderID, LineNumber)  
               WITH (IGNORE_DUP_KEY = OFF)  
)   
ON PRIMARY;  
```  
  
### <a name="g-creating-a-table-with-an-xml-column-typed-to-an-xml-schema-collection"></a>G. Erstellen einer Tabelle mit einer XML-Spalte, die mit einer XML-Schemaauflistung typisiert wird  
 Im folgenden Beispiel wird eine Tabelle mit einer `xml`-Spalte erstellt, die mit der XML-Schemaauflistung `HRResumeSchemaCollection` typisiert wird. Die `DOCUMENT` Schlüsselwort Gibt an, dass jede Instanz von der `xml` -Datentyp im *Column_name* kann nur ein Element der obersten Ebene enthalten.  
  
```  
CREATE TABLE HumanResources.EmployeeResumes   
   (LName nvarchar(25), FName nvarchar(25),   
    Resume xml( DOCUMENT HumanResources.HRResumeSchemaCollection) );  
```  
  
### <a name="h-creating-a-partitioned-table"></a>H. Erstellen einer partitionierten Tabelle  
 Im folgenden Beispiel wird eine Partitionsfunktion zum Partitionieren einer Tabelle oder eines Indexes in vier Partitionen erstellt. Anschließend wird im Beispiel ein Partitionsschema erstellt, das die Dateigruppen angibt, die jede der vier Partitionen aufnehmen sollen. Schließlich wird eine Tabelle erstellt, die das Partitionsschema verwendet. In diesem Beispiel wird davon ausgegangen, dass die Dateigruppen bereits in der Datenbank vorhanden sind.  
  
```  
CREATE PARTITION FUNCTION myRangePF1 (int)  
    AS RANGE LEFT FOR VALUES (1, 100, 1000) ;  
GO  
  
CREATE PARTITION SCHEME myRangePS1  
    AS PARTITION myRangePF1  
    TO (test1fg, test2fg, test3fg, test4fg) ;  
GO  
  
CREATE TABLE PartitionTable (col1 int, col2 char(10))  
    ON myRangePS1 (col1) ;  
GO  
```  
  
 Basierend auf den Werten der `col1`-Spalte von `PartitionTable` werden die Partitionen folgendermaßen zugewiesen.  
  
|Dateigruppe|test1fg|test2fg|test3fg|test4fg|  
|---------------|-------------|-------------|-------------|-------------|  
|**Partition**|1|2|3|4|  
|**Werte**|SP 1 \<= 1|col1 > 1 AND col1 \<= 100|col1 > 100 AND col1 \<= 1.000|col1 > 1000|  
  
### <a name="i-using-the-uniqueidentifier-data-type-in-a-column"></a>I. Verwenden des uniqueidentifier-Datentyps in einer Spalte  
 Im folgenden Beispiel wird eine Tabelle mit einer `uniqueidentifier`-Spalte erstellt. In dem Beispiel wird eine PRIMARY KEY-Einschränkung verwendet, um zu verhindern, dass Benutzer doppelte Werte in die Tabelle einfügen. Mithilfe der `NEWSEQUENTIALID()`-Funktion in der `DEFAULT`-Einschränkung werden Werte für neue Zeilen bereitgestellt. Die ROWGUIDCOL-Eigenschaft wird auf die `uniqueidentifier`-Spalte angewendet, sodass mit dem $ROWGUID-Schlüsselwort auf sie verwiesen werden kann.  
  
```  
CREATE TABLE dbo.Globally_Unique_Data  
    (guid uniqueidentifier   
        CONSTRAINT Guid_Default DEFAULT   
        NEWSEQUENTIALID() ROWGUIDCOL,  
    Employee_Name varchar(60)  
    CONSTRAINT Guid_PK PRIMARY KEY (guid) );  
```  
  
### <a name="j-using-an-expression-for-a-computed-column"></a>J. Verwenden eines Ausdrucks für eine berechnete Spalte  
 Im folgenden Beispiel wird die Verwendung eines Ausdrucks (`(low + high)/2`) zum Berechnen der berechneten Spalte `myavg` verwendet.  
  
```  
CREATE TABLE dbo.mytable   
    ( low int, high int, myavg AS (low + high)/2 ) ;  
```  
  
### <a name="k-creating-a-computed-column-based-on-a-user-defined-type-column"></a>K. Erstellen einer berechneten Spalte basierend auf einer Spalte eines benutzerdefinierten Typs  
 Im folgenden Beispiel wird eine Tabelle mit einer Spalte erstellt, die als Spalte des benutzerdefinierten Typs `utf8string` definiert ist. Hierbei wird vorausgesetzt, dass die Assembly des Typs und der Typ selbst bereits in der aktuellen Datenbank erstellt wurden. Eine zweite Spalte ist definiert basierend auf `utf8string`, und verwendet die Methode `ToString()` von **type(class)** `utf8string` auf einen Wert für die Spalte zu berechnen.  
  
```  
CREATE TABLE UDTypeTable   
    ( u utf8string, ustr AS u.ToString() PERSISTED ) ;  
```  
  
### <a name="l-using-the-username-function-for-a-computed-column"></a>L. Verwenden der USER_NAME-Funktion für eine berechnete Spalte  
 Im folgenden Beispiel wird die `USER_NAME()`-Funktion in der `myuser_name`-Spalte verwendet.  
  
```  
CREATE TABLE dbo.mylogintable  
    ( date_in datetime, user_id int, myuser_name AS USER_NAME() ) ;  
```  
  
### <a name="m-creating-a-table-that-has-a-filestream-column"></a>M. Erstellen einer Tabelle mit einer FILESTREAM-Spalte  
 Im folgenden Beispiel wird eine Tabelle mit der `FILESTREAM`-Spalte `Photo` erstellt. Eine Tabelle mit einer oder mehreren `FILESTREAM`-Spalten muss eine `ROWGUIDCOL`-Spalte enthalten.  
  
```  
CREATE TABLE dbo.EmployeePhoto  
    (  
    EmployeeId int NOT NULL PRIMARY KEY,  
    ,Photo varbinary(max) FILESTREAM NULL  
    ,MyRowGuidColumn uniqueidentifier NOT NULL ROWGUIDCOL  
        UNIQUE DEFAULT NEWID()  
    );  
```  
  
### <a name="n-creating-a-table-that-uses-row-compression"></a>N. Erstellen einer Tabelle, in der Zeilenkomprimierung verwendet wird  
 Im folgenden Beispiel wird eine Tabelle erstellt, in der Zeilenkomprimierung verwendet wird.  
  
```  
CREATE TABLE dbo.T1   
(c1 int, c2 nvarchar(200) )  
WITH (DATA_COMPRESSION = ROW);  
```  
  
 Zusätzliche Beispiele zur datenkomprimierung finden Sie unter [Datenkomprimierung](../../relational-databases/data-compression/data-compression.md).  
  
### <a name="o-creating-a-table-that-has-sparse-columns-and-a-column-set"></a>O. Erstellen einer Tabelle mit Spalten mit geringer Dichte und einem Spaltensatz  
 Anhand der folgenden Beispiele wird gezeigt, wie Sie eine Tabelle mit einer Spalte mit geringer Dichte und eine Tabelle mit zwei Spalten mit geringer Dichte und einem Spaltensatz erstellen. In den Beispielen wird die grundlegende Syntax verwendet. Komplexere Beispiele finden Sie unter [Use Sparse Columns](../../relational-databases/tables/use-sparse-columns.md) und [Verwenden von Spaltensätzen](../../relational-databases/tables/use-column-sets.md).  
  
 In diesem Beispiel wird eine Tabelle erstellt, die eine Spalte mit geringer Dichte enthält.  
  
```  
CREATE TABLE dbo.T1  
    (c1 int PRIMARY KEY,  
    c2 varchar(50) SPARSE NULL ) ;  
```  
  
 In diesem Beispiel wird eine Tabelle erstellt, die zwei Spalten mit geringer Dichte und einen Spaltensatz mit dem Namen `CSet` enthält.  
  
```  
CREATE TABLE T1  
    (c1 int PRIMARY KEY,  
    c2 varchar(50) SPARSE NULL,  
    c3 int SPARSE NULL,  
    CSet XML COLUMN_SET FOR ALL_SPARSE_COLUMNS ) ;  
```  
  
### <a name="p-creating-a-system-versioned-disk-based-temporal-table"></a>P. Erstellen einer datenträgerbasierten temporalen Tabelle mit systemversionsverwaltung  
   
  
**Gilt für**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] und [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].
  
 Den folgenden Beispielen wird veranschaulicht, wie eine temporale Tabelle mit einer neuen Verlaufstabelle verknüpfte Tabelle erstellen und zum Erstellen einer temporalen Tabelle mit einer vorhandenen Verlaufstabelle verknüpft. Beachten Sie, dass die temporale Tabelle einen Primärschlüssel definiert, um die Tabelle aktiviert sein, damit die versionsverwaltung durch das System aktiviert werden muss. Beispiele für die Darstellung des hinzufügen oder Entfernen von versionsverwaltung durch das System für eine vorhandene Tabelle finden Sie unter Versionsverwaltung durch das System in [Beispiele](../../t-sql/statements/alter-table-transact-sql.md#Example_Top). Anwendungsfälle, finden Sie unter [Zeittabellen](../../relational-databases/tables/temporal-tables.md).  
  
 In diesem Beispiel erstellt eine neue temporale Tabelle mit einer neuen Verlaufstabelle verknüpft.  
  
```  
CREATE TABLE Department   
(  
    DepartmentNumber char(10) NOT NULL PRIMARY KEY CLUSTERED,   
    DepartmentName varchar(50) NOT NULL,   
    ManagerID int  NULL,   
    ParentDepartmentNumber char(10) NULL,   
    SysStartTime datetime2 GENERATED ALWAYS AS ROW START HIDDEN NOT NULL,   
    SysEndTime datetime2 GENERATED ALWAYS AS ROW END HIDDEN NOT NULL,     
    PERIOD FOR SYSTEM_TIME (SysStartTime,SysEndTime)     
)  
WITH (SYSTEM_VERSIONING = ON);  
```  
  
 In diesem Beispiel erstellt eine neue temporale Tabelle mit einer vorhandenen Verlaufstabelle verknüpft.  
  
```  
  
--Existing table   
CREATE TABLE Department_History   
(  
    DepartmentNumber char(10) NOT NULL,   
    DepartmentName varchar(50) NOT NULL,   
    ManagerID int  NULL,   
    ParentDepartmentNumber char(10) NULL,   
    SysStartTime datetime2 NOT NULL,   
    SysEndTime datetime2 NOT NULL   
);  
--Temporal table  
CREATE TABLE Department   
(  
    DepartmentNumber char(10) NOT NULL PRIMARY KEY CLUSTERED,   
    DepartmentName varchar(50) NOT NULL,   
    ManagerID INT  NULL,   
    ParentDepartmentNumber char(10) NULL,   
    SysStartTime datetime2 GENERATED ALWAYS AS ROW START HIDDEN NOT NULL,   
    SysEndTime datetime2 GENERATED ALWAYS AS ROW END HIDDEN NOT NULL,     
    PERIOD FOR SYSTEM_TIME (SysStartTime,SysEndTime)    
)  
WITH   
    (SYSTEM_VERSIONING = ON   
        (HISTORY_TABLE = dbo.Department_History, DATA_CONSISTENCY_CHECK = ON )  
    );  
```  
  
### <a name="q-creating-a-system-versioned-memory-optimized-temporal-table"></a>Q. Erstellen eine Speicheroptimierte temporale Tabelle mit systemversionsverwaltung  
   
  
**Gilt für**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] und [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].
  
 Im folgende Beispiel wird gezeigt, wie zum Erstellen einer speicheroptimierten temporalen Tabelle mit systemversionsverwaltung mit einer neuen datenträgerbasierten Verlaufstabelle verknüpft wird.  
  
 In diesem Beispiel erstellt eine neue temporale Tabelle mit einer neuen Verlaufstabelle verknüpft.  
  
```  
CREATE SCHEMA History  
GO  
CREATE TABLE dbo.Department   
(  
    DepartmentNumber char(10) NOT NULL PRIMARY KEY CLUSTERED,   
    DepartmentName varchar(50) NOT NULL,   
    ManagerID int  NULL,   
    ParentDepartmentNumber char(10) NULL,   
    SysStartTime datetime2 GENERATED ALWAYS AS ROW START HIDDEN NOT NULL,   
    SysEndTime datetime2 GENERATED ALWAYS AS ROW END HIDDEN NOT NULL,     
    PERIOD FOR SYSTEM_TIME (SysStartTime,SysEndTime)     
)  
WITH   
    (  
        MEMORY_OPTIMIZED = ON, DURABILITY = SCHEMA_AND_DATA,  
            SYSTEM_VERSIONING = ON ( HISTORY_TABLE = History.DepartmentHistory )   
    );  
```  
  
 In diesem Beispiel erstellt eine neue temporale Tabelle mit einer vorhandenen Verlaufstabelle verknüpft.  
  
```  
  
--Existing table   
CREATE TABLE Department_History   
(  
    DepartmentNumber char(10) NOT NULL,   
    DepartmentName varchar(50) NOT NULL,   
    ManagerID int  NULL,   
    ParentDepartmentNumber char(10) NULL,   
    SysStartTime datetime2 NOT NULL,   
    SysEndTime datetime2 NOT NULL   
);  
--Temporal table  
CREATE TABLE Department   
(  
    DepartmentNumber char(10) NOT NULL PRIMARY KEY CLUSTERED,   
    DepartmentName varchar(50) NOT NULL,   
    ManagerID INT  NULL,   
    ParentDepartmentNumber char(10) NULL,   
    SysStartTime datetime2 GENERATED ALWAYS AS ROW START HIDDEN NOT NULL,   
    SysEndTime datetime2 GENERATED ALWAYS AS ROW END HIDDEN NOT NULL,     
    PERIOD FOR SYSTEM_TIME (SysStartTime,SysEndTime)    
)  
WITH   
    (SYSTEM_VERSIONING = ON   
        (HISTORY_TABLE = dbo.Department_History, DATA_CONSISTENCY_CHECK = ON )  
    );  
```  
  
### <a name="r-creating-a-table-with-encrypted-columns"></a>R. Erstellen einer Tabelle mit verschlüsselten Spalten  
 Das folgende Beispiel erstellt eine Tabelle mit zwei verschlüsselte Spalten. Weitere Informationen finden Sie unter [Always Encrypted &#40;Datenbankmodul&#41;](../../relational-databases/security/encryption/always-encrypted-database-engine.md).  
  
```  
CREATE TABLE Customers (  
    CustName nvarchar(60)   
        ENCRYPTED WITH   
            (  
             COLUMN_ENCRYPTION_KEY = MyCEK,  
             ENCRYPTION_TYPE = RANDOMIZED,  
             ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256'  
            ),   
    SSN varchar(11) COLLATE  Latin1_General_BIN2  
        ENCRYPTED WITH   
            (  
             COLUMN_ENCRYPTION_KEY = MyCEK,  
             ENCRYPTION_TYPE = DETERMINISTIC ,  
             ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256'  
            ),   
    Age int NULL  
);  
```

### <a name="s-create-an-inline-filtered-index"></a>S. Inline gefilterten Index erstellen 
Erstellt eine Tabellen mit einem Inline gefilterten Index.
  
  ```
  CREATE TABLE t1 
 (
      c1 int,
      index IX1  (c1) WHERE c1 > 0   
 )
GO
 ```
 
  
## <a name="see-also"></a>Siehe auch  
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [COLUMNPROPERTY &#40; Transact-SQL &#41;](../../t-sql/functions/columnproperty-transact-sql.md)   
 [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)   
 [CREATE VIEW &#40;Transact-SQL&#41;](../../t-sql/statements/create-view-transact-sql.md)   
 [Datentypen &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [DROP INDEX &#40; Transact-SQL &#41;](../../t-sql/statements/drop-index-transact-sql.md)   
 [sys.dm_sql_referenced_entities &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-sql-referenced-entities-transact-sql.md)   
 [sys.dm_sql_referencing_entities &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-sql-referencing-entities-transact-sql.md)   
 [DROP TABLE &#40; Transact-SQL &#41;](../../t-sql/statements/drop-table-transact-sql.md)   
 [CREATE PARTITION FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/create-partition-function-transact-sql.md)   
 [CREATE PARTITION SCHEME &#40;Transact-SQL&#41;](../../t-sql/statements/create-partition-scheme-transact-sql.md)   
 [CREATE TYPE &#40;Transact-SQL&#41;](../../t-sql/statements/create-type-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [sp_help &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-transact-sql.md)   
 [Sp_helpconstraint &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-helpconstraint-transact-sql.md)   
 [sp_rename &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-rename-transact-sql.md)   
 [Sp_spaceused &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-spaceused-transact-sql.md)  
  
  




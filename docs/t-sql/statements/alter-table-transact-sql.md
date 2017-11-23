---
title: ALTER TABLE-Anweisung (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/07/2017
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
- WAIT_AT_LOW_PRIORITY
- ABORT_AFTER_WAIT
- ABORT_AFTER_WAIT_TSQL
- ALTER_TABLE_TSQL
- ALTER TABLE
- WAIT_AT_LOW_PRIORITY_TSQL
- ALTER_COLUMN_TSQL
dev_langs: TSQL
helpviewer_keywords:
- columns [SQL Server], resizing
- changing column size
- MAXDOP index option, ALTER TABLE statement
- table modifications [SQL Server], ALTER TABLE
- ALTER TABLE statement
- modifying tables
- partitioned tables [SQL Server], lock escalation
- resizing columns
- removing columns
- switching partitions
- reassigning partitions
- removing constraints
- triggers [SQL Server], disabling
- columns [SQL Server], adding
- LOCK_ESCALATION option of ALTER TABLE
- constraints [SQL Server], deleting
- constraints [SQL Server], disabling
- triggers [SQL Server], enabling
- re-enabling constraints
- index modifications [SQL Server]
- disabling constraints
- columns [SQL Server], removing
- max degree of parallelism option
- locking [SQL Server], tables
- ONLINE option
- disabling triggers
- constraints [SQL Server], adding
- deleting constraints
- adding constraints
- adding columns
- SWITCH partitions
- partitioned tables [SQL Server], switching
- lock escalation [SQL Server], option of ALTER TABLE
- constraints [SQL Server], enabling
- dropping constraints
- dropping columns
- table changes [SQL Server]
ms.assetid: f1745145-182d-4301-a334-18f799d361d1
caps.latest.revision: "281"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: fc00fddf50d7f3261d0af09b755c1eb6b4c314d2
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="alter-table-transact-sql"></a>ALTER TABLE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Ändert eine Tabellendefinition durch Ändern, Hinzufügen oder Löschen von Spalten und Einschränkungen, Neuzuweisen und Neuerstellen von Partitionen oder Deaktivieren bzw. Aktivieren von Einschränkungen und Triggern.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
ALTER TABLE [ database_name . [ schema_name ] . | schema_name . ] table_name   
{   
    ALTER COLUMN column_name   
    {   
        [ type_schema_name. ] type_name   
            [ (   
                {   
                   precision [ , scale ]   
                 | max   
                 | xml_schema_collection   
                }   
            ) ]   
        [ COLLATE collation_name ]   
        [ NULL | NOT NULL ] [ SPARSE ]  
      | { ADD | DROP }   
          { ROWGUIDCOL | PERSISTED | NOT FOR REPLICATION | SPARSE | HIDDEN }  
      | { ADD | DROP } MASKED [ WITH ( FUNCTION = ' mask_function ') ]  
    }   
    [ WITH ( ONLINE = ON | OFF ) ]  
    | [ WITH { CHECK | NOCHECK } ]  
  
    | ADD   
    {   
        <column_definition>  
      | <computed_column_definition>  
      | <table_constraint>   
      | <column_set_definition>   
    } [ ,...n ]  
      | [ system_start_time_column_name datetime2 GENERATED ALWAYS AS ROW START   
                   [ HIDDEN ] [ NOT NULL ] [ CONSTRAINT constraint_name ] 
           DEFAULT constant_expression [WITH VALUES] ,  
            system_end_time_column_name datetime2 GENERATED ALWAYS AS ROW END   
                   [ HIDDEN ] [ NOT NULL ]  [ CONSTRAINT constraint_name ] 
           DEFAULT constant_expression [WITH VALUES] ,  
         ]  
       PERIOD FOR SYSTEM_TIME ( system_start_time_column_name, system_end_time_column_name )  
    | DROP   
     [ {  
         [ CONSTRAINT ]  [ IF EXISTS ]  
         {   
              constraint_name   
              [ WITH   
               ( <drop_clustered_constraint_option> [ ,...n ] )   
              ]   
          } [ ,...n ]  
          | COLUMN  [ IF EXISTS ]  
          {  
              column_name   
          } [ ,...n ]  
          | PERIOD FOR SYSTEM_TIME  
     } [ ,...n ]  
    | [ WITH { CHECK | NOCHECK } ] { CHECK | NOCHECK } CONSTRAINT   
        { ALL | constraint_name [ ,...n ] }   
  
    | { ENABLE | DISABLE } TRIGGER   
        { ALL | trigger_name [ ,...n ] }  
  
    | { ENABLE | DISABLE } CHANGE_TRACKING   
        [ WITH ( TRACK_COLUMNS_UPDATED = { ON | OFF } ) ]  
  
    | SWITCH [ PARTITION source_partition_number_expression ]  
        TO target_table   
        [ PARTITION target_partition_number_expression ]  
        [ WITH ( <low_lock_priority_wait> ) ]  
    | SET   
        (  
            [ FILESTREAM_ON =   
                { partition_scheme_name | filegroup | "default" | "NULL" } ]  
            | SYSTEM_VERSIONING =   
                  {   
                      OFF   
                  | ON   
                      [ ( HISTORY_TABLE = schema_name . history_table_name   
                          [, DATA_CONSISTENCY_CHECK = { ON | OFF } ] 
                          [, HISTORY_RETENTION_PERIOD = 
                          { 
                               INFINITE | number {DAY | DAYS | WEEK | WEEKS 
                 | MONTH | MONTHS | YEAR | YEARS } 
                          } 
                          ]  
                        )  
                      ]  
                  }  
          )  
    | REBUILD   
      [ [PARTITION = ALL]  
        [ WITH ( <rebuild_option> [ ,...n ] ) ]   
      | [ PARTITION = partition_number   
           [ WITH ( <single_partition_rebuild_option> [ ,...n ] ) ]  
        ]  
      ]  
  
    | <table_option>  
  
    | <filetable_option>  
  
    | <stretch_configuration>  
  
}  
[ ; ]  
  
-- ALTER TABLE options  
  
<column_set_definition> ::=   
    column_set_name XML COLUMN_SET FOR ALL_SPARSE_COLUMNS  
  
<drop_clustered_constraint_option> ::=    
    {   
        MAXDOP = max_degree_of_parallelism  
      | ONLINE = { ON | OFF }  
      | MOVE TO   
         { partition_scheme_name ( column_name ) | filegroup | "default" }  
    }  
<table_option> ::=  
    {  
        SET ( LOCK_ESCALATION = { AUTO | TABLE | DISABLE } )  
    }  
  
<filetable_option> ::=  
    {  
       [ { ENABLE | DISABLE } FILETABLE_NAMESPACE ]  
       [ SET ( FILETABLE_DIRECTORY = directory_name ) ]  
    }  
  
<stretch_configuration> ::=  
    {  
      SET (  
        REMOTE_DATA_ARCHIVE   
        {  
            = ON (  <table_stretch_options>  )  
          | = OFF_WITHOUT_DATA_RECOVERY ( MIGRATION_STATE = PAUSED )  
          | ( <table_stretch_options> [, ...n] )  
        }  
            )  
    }  
  
<table_stretch_options> ::=  
    {  
     [ FILTER_PREDICATE = { null | table_predicate_function } , ]  
       MIGRATION_STATE = { OUTBOUND | INBOUND | PAUSED }  
    }  
  
<single_partition_rebuild__option> ::=  
{  
      SORT_IN_TEMPDB = { ON | OFF }  
    | MAXDOP = max_degree_of_parallelism  
    | DATA_COMPRESSION = { NONE | ROW | PAGE | COLUMNSTORE | COLUMNSTORE_ARCHIVE} }  
    | ONLINE = { ON [( <low_priority_lock_wait> ) ] | OFF }  
}  
  
<low_priority_lock_wait>::=  
{  
    WAIT_AT_LOW_PRIORITY ( MAX_DURATION = <time> [ MINUTES ], 
        ABORT_AFTER_WAIT = { NONE | SELF | BLOCKERS } )   
}  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
ALTER TABLE [ database_name . [schema_name ] . | schema_name. ] source_table_name   
{  
    ALTER COLUMN column_name  
        {   
            type_name [ ( precision [ , scale ] ) ]   
            [ COLLATE Windows_collation_name ]   
            [ NULL | NOT NULL ]   
        }  
    | ADD { <column_definition> | <column_constraint> FOR column_name} [ ,...n ]  
    | DROP { COLUMN column_name | [CONSTRAINT] constraint_name } [ ,...n ]  
    | REBUILD {  
            [ PARTITION = ALL [ WITH ( <rebuild_option> ) ] ] 
          | [ PARTITION = partition_number [ WITH ( <single_partition_rebuild_option> ] ]
      } 
    | { SPLIT | MERGE } RANGE (boundary_value)  
    | SWITCH [ PARTITION source_partition_number  
        TO target_table_name [ PARTITION target_partition_number ]  
}  
[;]  
  
<column_definition>::=  
{  
    column_name  
    type_name [ ( precision [ , scale ] ) ]   
    [ <column_constraint> ]  
    [ COLLATE Windows_collation_name ]  
    [ NULL | NOT NULL ]  
}  
  
<column_constraint>::=  
    [ CONSTRAINT constraint_name ] DEFAULT constant_expression  

<rebuild_option > ::=   
{  
    DATA_COMPRESSION = { COLUMNSTORE | COLUMNSTORE_ARCHIVE }
        [ ON PARTITIONS ( {<partition_number> [ TO <partition_number>] } [ , ...n ] ) ]   
}

<single_partition_rebuild_option > ::=   
{  
    DATA_COMPRESSION = { COLUMNSTORE | COLUMNSTORE_ARCHIVE }  
}  
```    

   
## <a name="arguments"></a>Argumente  
 *database_name*  
 Name der Datenbank, in der die Tabelle erstellt wurde.  
  
 *schema_name*  
 Der Name des Schemas, zu dem die Tabelle gehört.  
  
 *table_name*  
 Der Name der Tabelle, die geändert werden soll. Wenn die Tabelle nicht in der aktuellen Datenbank oder nicht in dem Schema enthalten ist, das dem aktuellen Benutzer gehört, müssen die Datenbank und das Schema explizit angegeben werden.  
  
 ALTER COLUMN  
 Gibt an, dass die benannte Spalte geändert werden soll.  
  
 Für die geänderte Spalte gilt Folgendes:  
  
-   Eine Spalte mit einem **Zeitstempel** -Datentyp.  
  
-   Die Spalte darf nicht die ROWGUIDCOL-Spalte der Tabelle sein.  
  
-   Die Spalte darf keine berechnete Spalte sein und nicht in einer berechneten Spalte verwendet werden.  
  
-   Verwendet in Statistiken, die von der CREATE STATISTICS-Anweisung generiert werden, es sei denn, die Spalte ist eine **Varchar**, **Nvarchar**, oder **Varbinary** -Datentyp, der Datentyp wird nicht geändert, und die neue Größe ist gleich oder größer als die alte Größe, oder wenn die Spalte von not Null in Null geändert wird. Entfernen Sie die Statistiken zunächst mithilfe der DROP STATISTICS-Anweisung. Vom Abfrageoptimierer automatisch generierte Statistiken werden von ALTER COLUMN automatisch gelöscht.  
  
-   Die Spalte darf nicht in einer PRIMARY KEY- oder [FOREIGN KEY] REFERENCES-Einschränkung verwendet werden.  
  
-   Die Spalte darf nicht in einer CHECK- oder UNIQUE-Einschränkung verwendet werden. Das Ändern der Länge einer Spalte mit variabler Länge, die in einer CHECK- oder UNIQUE-Einschränkung verwendet wird, ist dagegen zulässig.  
  
-   Der Spalte darf keine Standarddefinition zugeordnet sein. Die Länge, die Genauigkeit oder die Dezimalstellen einer Spalte können jedoch geändert werden, sofern der Datentyp nicht geändert wird.  
  
Der Datentyp des **Text**, **Ntext** und **Image** Spalten können nur auf folgende Weise geändert werden:  
  
    -   **Text** auf **varchar(max)**, **nvarchar(max)**, oder **Xml**  
  
    -   **Ntext** auf **varchar(max)**, **nvarchar(max)**, oder **Xml**  
  
    -   **Bild** auf **varbinary(max)**  
  
Änderungen des Datentyps können Datenänderungen zur Folge haben. Ändern Sie z. B. ein **Nchar** oder **Nvarchar** Spalte **Char** oder **Varchar** kann dazu führen, dass die Konvertierung erweiterter Zeichen. Weitere Informationen finden Sie unter [CAST und CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md). Das Reduzieren der Genauigkeit und der Dezimalstellen einer Spalte kann zum Abschneiden von Daten führen.  
  
     The data type of a column of a partitioned table cannot be changed.  
  
 Der Datentyp der Spalten in einem Index kann nicht geändert werden, es sei denn, die Spalte ist eine **Varchar**, **Nvarchar**, oder **Varbinary** -Datentyp, und die neue Größe ist größer oder gleich als die alte Größe.  
  
 Eine in einer primary Key-Einschränkung enthaltenen Spalten kann nicht geändert werden, von **NOT NULL** auf **NULL**.  
  
 Wenn die Spalte geändert wird mit VERSCHLÜSSELT verschlüsselt ist, können Sie den Datentyp in einen kompatiblen Datentyp (z. B. INT, BIGINT) ändern, jedoch Einstellungen für die Verschlüsselung kann nicht geändert werden.  
  
 *Spaltenname*  
 Der Name der Spalte, die geändert, hinzugefügt oder gelöscht werden soll. *Column_name* kann maximal 128 Zeichen sein. Bei neuen Spalten *Column_name* kann ausgelassen werden, für Spalten erstellt, die mit einem **Zeitstempel** -Datentyp. Der Name **Zeitstempel** wird verwendet, wenn keine *Column_name* für angegeben wird eine **Zeitstempel** -Datentypspalte.  
  
 [ *Type_schema_name***.** ] *Type_name*  
 Der neue Datentyp für die geänderte Spalte oder der Datentyp für die hinzugefügte Spalte. *TYPE_NAME* kann nicht für vorhandene Spalten von partitionierten Tabellen angegeben werden. *TYPE_NAME* kann eine der folgenden sein:  
  
-   Ein [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Systemdatentyp.  
  
-   Ein Aliasdatentyp, der auf einem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Systemdatentyp basiert. Aliasdatentypen werden mit der CREATE TYPE-Anweisung erstellt, bevor sie in einer Tabellendefinition verwendet werden können.  
  
-   Ein benutzerdefinierter [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]-Datentyp und das Schema, zu dem er gehört. Benutzerdefinierte [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]-Typen werden mit der CREATE TYPE-Anweisung erstellt, bevor sie in einer Tabellendefinition verwendet werden können.  
  
Im folgenden sind die Kriterien für *Type_name* einer geänderten Spalte:  
  
-   Der vorherige Datentyp muss implizit in den neuen Datentyp konvertiert werden können.  
  
-   *TYPE_NAME* nicht **Zeitstempel**.  
  
-   ANSI NULL DEFAULT ist für ALTER COLUMN immer aktiviert. Fehlt die Angabe, so lässt die Spalte NULL-Werte zu.  
  
-   ANSI_PADDING ist für ALTER COLUMN immer auf ON festgelegt.  
  
-   Wenn die geänderte Spalte eine Identitätsspalte ist *New_data_type* muss ein Datentyp, der die Identity-Eigenschaft unterstützt werden.  
  
-   Die aktuelle Einstellung für SET ARITHABORT wird ignoriert. ALTER TABLE wird ausgeführt, als sei ARITHABORT aktiviert.  
  
> [!NOTE]  
>  Falls die COLLATE-Klausel nicht angegeben wird, bewirkt das Ändern des Datentyps einer Spalte die Änderung der Sortierung in die Standardsortierung der Datenbank.  
  
 *precision*  
 Die Genauigkeit für den angegebenen Datentyp. Weitere Informationen über gültige Genauigkeitswerte finden Sie unter [mit einfacher Genauigkeit, Dezimalstellen und Länge &#40; Transact-SQL &#41; ](../../t-sql/data-types/precision-scale-and-length-transact-sql.md).  
  
 *scale*  
 Die Dezimalstellen für den angegebenen Datentyp. Weitere Informationen zu gültigen Dezimalstellenwerten finden Sie unter [mit einfacher Genauigkeit, Dezimalstellen und Länge &#40; Transact-SQL &#41; ](../../t-sql/data-types/precision-scale-and-length-transact-sql.md).  
  
 **Max**  
 Gilt nur für die **Varchar**, **Nvarchar**, und **Varbinary** -Datentyp zum Speichern von 2 ^ 31-1 Bytes von Zeichen-, binär-, und der Unicode-Daten.  
  
 *xml_schema_collection*  
 **Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] und [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
 Gilt nur für die **Xml** Datentyp für den Typ ein XML-Schemas zuordnen. Vor der Eingabe einer **Xml** Spalte einer schemaauflistung, die schemaauflistung muss zuerst erstellt werden in der Datenbank mithilfe von [CREATE XML SCHEMA COLLECTION](../../t-sql/statements/create-xml-schema-collection-transact-sql.md).  
  
COLLATE \< *Collation_name* > Gibt die neue Sortierung für die geänderte Spalte. Wenn keine Sortierung angegeben ist, wird der Spalte die Standardsortierung der Datenbank zugewiesen. Als Sortierungsname kann entweder der Name einer Windows-Sortierreihenfolge oder ein SQL-Sortierungsname verwendet werden. Eine Liste und Weitere Informationen finden Sie unter [Windows-Sortierungsname &#40; Transact-SQL &#41; ](../../t-sql/statements/windows-collation-name-transact-sql.md) und [SQL Server-Sortierungsname &#40; Transact-SQL &#41; ](../../t-sql/statements/sql-server-collation-name-transact-sql.md).  
  
 Die COLLATE-Klausel kann verwendet werden, so ändern Sie nur die Sortierungen von Spalten von der **Char**, **Varchar**, **Nchar**, und **Nvarchar** Datentypen. Wenn Sie die Sortierung einer Spalte eines benutzerdefinierten Aliasdatentyps ändern möchten, müssen Sie zunächst mit separaten ALTER TABLE-Anweisungen die Spalte in einen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Systemdatentyp ändern und ihre Sortierung ändern. Anschließend können Sie die Spalte zurück in einen Aliasdatentyp ändern.  
  
 Mit ALTER COLUMN kann die Sortierung nicht geändert werden, wenn eine der folgenden Bedingungen zutrifft:  
  
-   Wenn eine CHECK-Einschränkung, eine FOREIGN KEY-Einschränkung oder berechnete Spalten auf die geänderte Spalte verweisen.  
  
-   Wenn ein Index, eine Statistik oder ein Volltextindex für die Spalte erstellt werden. Statistiken, die automatisch für die geänderte Spalte erstellt wurden, werden gelöscht, wenn die Spaltensortierung geändert wird.  
  
-   Wenn eine schemagebundene Sicht oder Funktion auf die Spalte verweist.  
  
 Weitere Informationen finden Sie unter [COLLATE &#40;Transact-SQL&#41;](~/t-sql/statements/collations.md).  
  
NULL | NOT NULL  
 Gibt an, ob die Spalte NULL-Werte akzeptiert. Spalten, die keine NULL-Werte zulassen, können mit ALTER TABLE nur hinzugefügt werden, wenn für sie ein Standardwert angegeben ist oder wenn die Tabelle leer ist. NOT NULL kann nur für berechnete Spalten angegeben werden, wenn auch PERSISTED angegeben ist. Wenn die neue Spalte NULL-Werte zulässt und kein Standardwert angegeben ist, enthält sie einen NULL-Wert für jede Zeile in der Tabelle. Wenn die neue Spalte NULL-Werte zulässt und eine Standarddefinition mit der neuen Spalte hinzugefügt wird, kann WITH VALUES verwendet werden, um den Standardwert in der neuen Spalte für jede vorhandene Zeile in der Tabelle zu speichern.  
  
 Wenn die neue Spalte keine NULL-Werte zulässt und die Tabelle nicht leer ist, muss eine DEFAULT-Definition mit der neuen Spalte hinzugefügt werden. Die neue Spalte wird dann automatisch in jeder vorhandenen Zeile mit dem Standardwert geladen.  
  
 Durch die Angabe von NULL in ALTER COLUMN kann erzwungen werden, dass eine NOT NULL-Spalte, mit Ausnahme von Spalten in PRIMARY KEY-Einschränkungen, NULL-Werte zulässt. NOT NULL kann nur in ALTER COLUMN angegeben werden, wenn die Spalte keine NULL-Werte enthält. Die NULL-Werte müssen auf einen beliebigen Wert aktualisiert werden, damit ALTER COLUMN NOT NULL zulässig ist. Beispiel:  
  
```  
UPDATE MyTable SET NullCol = N'some_value' WHERE NullCol IS NULL;  
ALTER TABLE MyTable ALTER COLUMN NullCOl NVARCHAR(20) NOT NULL;  
```  
  
 Wenn Sie eine Tabelle mit der CREATE TABLE- oder ALTER TABLE-Anweisung erstellen bzw. ändern, beeinflussen die Datenbank- und Sitzungseinstellungen die NULL-Zulässigkeit des in einer Spaltendefinition verwendeten Datentyps und überschreiben diese möglicherweise. Es wird empfohlen, eine nicht berechnete Spalte stets explizit als NULL oder NOT NULL zu definieren.  
  
 Wenn Sie eine Spalte mit einem benutzerdefinierten Datentyp hinzufügen, wird empfohlen, dass Sie die Spalte mit der gleichen NULL-Zulässigkeit wie der des benutzerdefinierten Datentyps definieren und einen Standardwert für die Spalte angeben. Weitere Informationen finden Sie unter [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md).  
  
> [!NOTE]  
>  Wenn NULL oder NOT NULL mit ALTER COLUMN angegeben *New_data_type* [(*Genauigkeit* [, *Skalierung* ])] muss auch angegeben werden. Wenn Datentyp, Genauigkeit und Dezimalstellen nicht geändert werden, geben Sie die aktuellen Spaltenwerte an.  
  
 [ {ADD | DROP} ROWGUIDCOL ]  
 **Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] und [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
 Gibt an, dass die ROWGUIDCOL-Eigenschaft der angegebenen Spalte hinzugefügt oder aus ihr gelöscht wird. ROWGUIDCOL zeigt an, dass die Spalte eine GUID-Spalte für eine Zeile darstellt. Nur ein **"uniqueidentifier"** -Spalte pro Tabelle kann als ROWGUIDCOL-Spalte gekennzeichnet werden, und die ROWGUIDCOL-Eigenschaft kann nur für zugewiesen werden eine **"uniqueidentifier"** Spalte. ROWGUIDCOL kann keiner Spalte eines benutzerdefinierten Datentyps zugewiesen werden.  
  
 ROWGUIDCOL erzwingt keine Eindeutigkeit der in der Spalte gespeicherten Werte und generiert nicht automatisch Werte für neue Zeilen, die in die Tabelle eingefügt werden. Verwenden Sie entweder die NEWID-Funktion in INSERT-Anweisungen, oder geben Sie die NEWID-Funktion als Standard für die Spalte an, um eindeutige Werte für jede Spalte zu generieren.  
  
 [ {ADD | DROP} PERSISTED ]  
 Gibt an, dass die PERSISTED-Eigenschaft der angegebenen Spalte hinzugefügt oder aus ihr gelöscht wird. Die Spalte muss eine berechnete Spalte sein, die durch einen deterministischen Ausdruck definiert ist. Für Spalten, die als PERSISTED angegeben werden, speichert das [!INCLUDE[ssDE](../../includes/ssde-md.md)] die berechneten Werte physisch in der Tabelle und aktualisiert die Werte, wenn andere Spalten, von denen die berechnete Spalte abhängt, aktualisiert werden. Durch Kennzeichnen einer berechneten Spalte als PERSISTED können Sie Indizes für berechnete Spalten erstellen, die durch deterministische, aber nicht genaue Ausdrücke definiert sind. Weitere Informationen finden Sie unter [Indexes on Computed Columns](../../relational-databases/indexes/indexes-on-computed-columns.md).  
  
 Jede berechnete Spalte, die als Partitionierungsspalte einer partitionierten Tabelle verwendet wird, muss explizit als PERSISTED gekennzeichnet sein.  
  
 DROP NOT FOR REPLICATION  
 **Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] und [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
 Gibt an, dass Werte in Identitätsspalten inkrementiert werden, wenn Replikations-Agents Einfügevorgänge ausführen. Diese Klausel kann angegeben werden, nur wenn *Column_name* Identitätsspalte ist.  
  
 SPARSE  
 Gibt an, dass die Spalte eine Sparsespalte ist. Der Speicher für Sparsespalten ist für NULL-Werte optimiert. Spalten mit geringer Dichte können nicht als NOT NULL festgelegt werden. Beim Umwandeln einer Spalte mit geringer Dichte in eine Spalte ohne geringe Dichte oder umgekehrt wird die Tabelle für die Dauer der Befehlsausführung gesperrt. Sie müssen möglicherweise die REBUILD-Klausel verwenden, um Speicherplatzeinsparungen freizugeben. Zusätzliche Einschränkungen und Weitere Informationen zu Spalten mit geringer Dichte finden Sie unter [Use Sparse Columns](../../relational-databases/tables/use-sparse-columns.md).  
  
 MASKIERTE hinzufügen mit (Funktion = " *Mask_function* ")  
 **Gilt für**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] und [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
 Gibt an, einer dynamischen Datenmaske. *Mask_function* ist der Name der Maskierungsfunktion mit den entsprechenden Parametern. Drei Funktionen sind verfügbar:  
  
-   default()  
-   Email()  
-   partial()  
-   Zufallsvariable()  
  
 Verwenden Sie zum Löschen einer Maske `DROP MASKED`. Funktionsparameter, finden Sie unter [Dynamic Data Masking](../../relational-databases/security/dynamic-data-masking.md).  
  
MIT (ONLINE = ON | OFF) \<wie beim Ändern einer Spalteninhalts >  
 **Gilt für**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] und [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
 Ermöglicht verschiedene Aktionen zum Ändern einer Spalte, während die Tabelle verfügbar bleibt. Die Standardeinstellung ist OFF. ALTER COLUMN kann online für Spaltenänderungen in Bezug auf Datentyp, Spaltenlänge, Genauigkeit, NULL-Zulässigkeit, geringe Dichte und Sortierung ausgeführt werden.  
  
 Die Onlineänderung ermöglicht, dass vom Benutzer und automatisch erstellte Statistiken weiterhin während des ALTER COLUMN-Vorgangs auf die geänderte Spalte verweisen. Dadurch können Abfragen wie gewohnt ausgeführt werden. Nach dem Beenden des Vorgangs werden automatisch erstellte Statistiken, die auf die Spalte verweisen, gelöscht, und vom Benutzer erstellte Statistiken werden ungültig. Der Benutzer muss benutzergenerierte Statistiken manuell aktualisieren, nachdem der Vorgang abgeschlossen wurde. Wenn die Spalte Teil eines Filterausdrucks für Statistiken oder Indizes ist, und klicken Sie dann einen Alter-Spalte-Vorgang nicht ausgeführt werden kann.  
  
-   Während des Onlineänderungsvorgangs werden alle Vorgänge blockiert, die von der Spalte abhängig sein könnten (Index, Ansichten usw.), oder es tritt ein Fehler mit einer entsprechenden Fehlermeldung auf. Dadurch wird sichergestellt, dass bei der Onlineänderung der Spalte kein Fehler aufgrund von Abhängigkeiten auftritt, die während des Vorgangs entstanden sind.  
  
-   Das Ändern einer Spalte von NOT NULL auf NULL ist bei einem Onlinevorgang nicht möglich, wenn nicht gruppierte Indizes auf die geänderte Spalte verweisen.  
  
-   Die Onlineänderung wird nicht unterstützt, wenn auf die Spalte mit einer CHECK-Einschränkung verwiesen wird und der Änderungsvorgang die Genauigkeit der Spalte („numeric“ oder „datetime“) einschränkt.  
  
-   Die **Low_priority_lock_wait** Option kann nicht verwendet werden, mit der onlinespaltenänderung.  
  
-   ALTER COLUMN … ADD/DROP PERSISTED wird bei der Onlinespaltenänderung nicht unterstützt.  
  
-   ALTER COLUMN … ADD/DROP ROWGUIDCOL/NOT FOR REPLICATION wird von der Onlinespaltenänderung nicht beeinflusst.  
  
-   Die Onlinespaltenänderung von Tabellen mit Änderungsnachverfolgung und von Tabellen, die ein Mergereplikationsverleger sind, wird nicht unterstützt.  
  
-   Die Onlinespaltenänderung unterstützt nicht das Ändern von oder in CLR-Datentypen.  
  
-   Die Änderung in einen XML-Datentyp mit einer von der aktuellen Schemaauflistung abweichenden Auflistung wird von der Onlinespaltenänderung nicht unterstützt.  
  
-   Durch die Onlinespaltenänderung werden die Einschränkungen, die festlegen, wann eine Spalte geändert werden kann, nicht verringert. Durch Verweise von Index/Statistiken usw. tritt möglicherweise ein Fehler beim Änderungsvorgang auf.  
  
-   Mit der Onlinespaltenänderung können nicht mehrere Spalten gleichzeitig geändert werden.  
  
-   Onlinespaltenänderung Spalte wirkt sich nicht im Falle der systemversionsverwaltung unterliegende temporal-Tabelle. Die Operation ALTER COLUMN wird nicht im Modus „online“ durchgeführt. Dies gilt unabhängig vom Wert, der für die Option ONLINE festgelegt wurde.  
  
Für die Onlinespaltenänderung gelten ähnliche Anforderungen, Einschränkungen und Funktionen wie für die Online-Indexneuerstellung. Dies schließt Folgendes ein:  
  
-   Die Online-Indexneuerstellung wird nicht unterstützt, wenn die Tabelle ältere LOB- oder Filestream-Spalten enthält oder die Tabelle über einen Columnstore-Index verfügt. Die gleichen Einschränkungen gelten für die Onlinespaltenänderung.  
  
-   Eine vorhandene Spalte, die geändert wird, erfordert die doppelte Speicherplatzzuordnung: für die ursprüngliche Spalte und für die neu erstellte, ausgeblendete Spalte.  
  
-   Die Sperrstrategie während eines Onlinevorgangs zur Spaltenänderung folgt demselben Sperrmuster wie die Onlineindexerstellung.  
  
WITH CHECK | WITH NOCHECK  
 Gibt an, ob die Daten in der Tabelle bei einer neu hinzugefügten oder erneut aktivierten FOREIGN KEY- oder CHECK-Einschränkung überprüft werden. Fehlt die Angabe, so wird WITH CHECK für neue Einschränkungen und WITH NOCHECK für erneut aktivierte Einschränkungen angenommen.  
  
 Verwenden Sie WITH NOCHECK, wenn neue CHECK- oder FOREIGN KEY-Einschränkungen nicht für vorhandene Daten überprüft werden sollen. Diese Vorgehensweise wird nur in seltenen Fällen empfohlen. Die neue Einschränkung wird bei allen späteren Datenupdates ausgewertet. Einschränkungsverletzungen, die beim Hinzufügen der Einschränkung durch WITH NOCHECK unterdrückt werden, können zu Fehlern bei zukünftigen Updates führen, wenn Zeilen mit Daten aktualisiert werden, die der Einschränkung nicht entsprechen.  
  
 Der Abfrageoptimierer berücksichtigt mit WITH NOCHECK definierte Einschränkungen nicht. Diese Einschränkungen werden ignoriert, bis sie mithilfe von `ALTER TABLE table WITH CHECK CHECK CONSTRAINT ALL` erneut aktiviert werden.  
  
 ADD  
 Gibt an, dass eine oder mehrere Spaltendefinitionen, Definitionen berechneter Spalten oder tabelleneinschränkungen hinzugefügt werden, oder die Spalten, die vom System für die versionsverwaltung durch das System verwendet wird.  
  
 PERIOD FOR SYSTEM_TIME (System_start_time_column_name, System_end_time_column_name)  
 **Gilt für**: [!INCLUDE[ssCurrentLong](../../includes/sscurrentlong-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] und [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
 Gibt die Namen der Spalten, die vom System verwendet wird, um den Zeitraum aufzuzeichnen, für den ein Datensatz gültig ist. Sie können vorhandene Spalten angeben oder erstellen neue Spalten als Teil des ADD PERIOD FOR SYSTEM_TIME-Arguments. Die Spalten muss den datetime2-Datentyp aufweisen und muss definiert werden, als NOT NULL. Wenn die Period-Spalte als NULL definiert ist, wird ein Fehler ausgelöst. Sie können definieren, eine [Column_constraint &#40; Transact-SQL &#41; ](../../t-sql/statements/alter-table-column-constraint-transact-sql.md) und/oder [angeben von Standardwerten für Spalten](../../relational-databases/tables/specify-default-values-for-columns.md) für die Spalten System_start_time und System_end_time. Siehe Beispiel A in die [Systemversionsverwaltung](#system_versioning) Beispiele unten veranschaulicht die Verwendung eines standardmäßigen Werts für die Spalte System_end_time.  
  
 Verwenden Sie dieses Argument zusammen mit dem Festlegen von SYSTEM_VERSIONING-Argument, zum Aktivieren der systemversionsverwaltung für eine vorhandene Tabelle. Weitere Informationen finden Sie unter [Zeittabellen](../../relational-databases/tables/temporal-tables.md) und [Einstieg in temporale Tabellen in Azure SQL-Datenbank](https://azure.microsoft.com/documentation/articles/sql-database-temporal-tables/).  
  
 Als der [!INCLUDE[ssCurrentLong](../../includes/sscurrentlong-md.md)], Benutzer werden in der Lage, markieren Sie eine oder beide zeitraumspalten mit **HIDDEN** Flag diese Spalten implizit ausgeblendet werden, dass **wählen \* FROM**  *\<Tabelle >* gibt einen Wert für diese Spalten nicht zurück. Standardmäßig werden die Periode-Spalten nicht ausgeblendet. Um verwendet werden, müssen ausgeblendete Spalten explizit in allen Abfragen eingeschlossen werden, die direkt auf die temporale Tabelle verweisen.  
  
 DROP  
 Gibt an, dass eine oder mehrere Spaltendefinitionen, Definitionen berechneter Spalten oder tabelleneinschränkungen abgelegt werden, oder die Spezifikation für die Spalten zu löschen, die vom System für die versionsverwaltung durch das System verwendet wird.  
  
 Einschränkung *Constraint_name*  
 Gibt an, dass *Constraint_name* aus der Tabelle entfernt wird. Es können mehrere Einschränkungen aufgelistet werden.  
  
 Der benutzerdefinierte oder vom System bereitgestellte Name der Einschränkung kann bestimmt werden, durch Abfragen der **check_constraint**, **Sys. default_constraints**, **Sys. key_constraints**, und **Sys. Foreign_Keys** Katalogsichten.  
  
 Eine PRIMARY KEY-Einschränkung kann nicht gelöscht werden, wenn ein XML-Index für die Tabelle vorhanden ist.  
  
 Spalte *Column_name*  
 Gibt an, dass *Constraint_name* oder *Column_name* aus der Tabelle entfernt wird. Es können mehrere Spalten aufgeführt werden.  
  
 Unter folgenden Umständen kann eine Spalte nicht gelöscht werden:  
  
-   Wenn sie in einem Index verwendet wird.  
  
-   Wenn sie in einer CHECK-, FOREIGN KEY-, UNIQUE- oder PRIMARY KEY-Einschränkung verwendet wird.  
  
-   Wenn ihr ein mit dem DEFAULT-Schlüsselwort definierter Standardwert zugeordnet ist oder sie an ein Standardobjekt gebunden ist.  
  
-   Wenn sie an eine Regel gebunden ist.  
  
> [!NOTE]  
>  Durch Löschen einer Spalte wird der Speicherplatz der Spalte nicht freigegeben. Unter Umständen müssen Sie den Speicherplatz einer gelöschten Spalte freigeben, wenn das Limit der Zeilengröße einer Tabelle fast erreicht oder überschritten ist. Zum Freigeben des Speicherplatzes für die Tabelle einen gruppierten Index erstellen oder Neuerstellen eines vorhandenen gruppierten Indexes mit [ALTER INDEX](../../t-sql/statements/alter-index-transact-sql.md). Informationen zu den Auswirkungen gelöschter LOB-Datentypen, finden Sie in diesem [CSS-Blogeintrag](http://blogs.msdn.com/b/psssql/archive/2012/12/03/how-it-works-gotcha-varchar-max-caused-my-queries-to-be-slower.aspx).  
  
 PERIOD FOR SYSTEM_TIME  
 **Gilt für**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] und [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
 Löscht die Spezifikation für die Spalten, die vom System für die versionsverwaltung durch das System verwendet wird.  
  
 MIT \<Drop_clustered_constraint_option >  
 Gibt an, dass mindestens eine Option zum Löschen einer gruppierten Einschränkung festgelegt wurde.  
  
 MAXDOP = *Max_degree_of_parallelism*  
 **Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] und [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
 Überschreibt die **Max. Grad an Parallelität** Konfigurationsoption nur für die Dauer des Vorgangs. Weitere Informationen finden Sie unter [Konfigurieren der Serverkonfigurationsoption Max. Grad an Parallelität](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md).  
  
 Verwenden Sie die MAXDOP-Option, um die Anzahl der Prozessoren zu beschränken, die für die Ausführung paralleler Pläne verwendet werden. Maximal sind 64 Prozessoren zulässig.  
  
 *Max_degree_of_parallelism* kann einen der folgenden Werte sein:  
  
 1  
 Unterdrückt das Generieren paralleler Pläne.  
  
 \>1  
 Begrenzt die Höchstzahl von Prozessoren in einem parallelen Indexvorgang auf die angegebene Zahl  
  
 0 (Standard)  
 Verwendet abhängig von der aktuellen Systemarbeitsauslastung die tatsächliche Anzahl von Prozessoren oder weniger Prozessoren.  
  
 Weitere Informationen finden Sie unter [Konfigurieren von Parallelindexvorgängen](../../relational-databases/indexes/configure-parallel-index-operations.md).  
  
> [!NOTE]  
>  Parallele Indexvorgänge sind nicht in jeder Edition von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verfügbar. Weitere Informationen finden Sie unter [Editionen und unterstützte Funktionen für SQL Server 2016](../../sql-server/editions-and-supported-features-for-sql-server-2016.md).  
  
 ONLINE  **=**  {ON | **OFF** } \<wie für Drop_clustered_constraint_option >  
 Gibt an, ob die zugrunde liegenden Tabellen und zugeordneten Indizes für Abfragen und Datenänderungen während des Indexvorgangs verfügbar sind. Der Standardwert ist OFF. REBUILD kann als ONLINE-Vorgang ausgeführt werden.  
  
 ON  
 Lang andauernde Sperren werden nicht für die Dauer des Indexvorgangs aufrechterhalten. Während der Hauptphase des Indexvorgangs wird nur eine beabsichtigte freigegebene Sperre (IS) für die Quelltabelle aufrechterhalten. So können Abfragen oder Updates der zugrunde liegenden Tabelle und Indizes fortgesetzt werden. Zu Beginn des Vorgangs wird das Quellobjekt für sehr kurze Zeit mit einer gemeinsamen Sperre (S) belegt. Am Ende des Vorgangs wird für kurze Zeit eine gemeinsame Sperre (S) für die Quelle eingerichtet, wenn ein nicht gruppierter Index erstellt wird. Eine Schemaänderungssperre (SCH-M) wird dagegen eingerichtet, wenn ein gruppierter Index online erstellt oder gelöscht wird und wenn ein gruppierter oder nicht gruppierter Index neu erstellt wird. ONLINE kann nicht auf ON festgelegt werden, wenn ein Index auf einer lokalen temporären Tabelle erstellt wird. Nur ein Heap-Neuerstellungsvorgang mit einem einzelnen Thread ist zulässig.  
  
 Zum Ausführen der DDL-Code für **SWITCH** oder Neuerstellung von Onlineindizes, alle aktiven blockierenden Transaktionen, die für eine bestimmte Tabelle abgeschlossen werden muss. Bei der Ausführung der **SWITCH** oder Neuerstellungsvorgang wird verhindert, dass neue Transaktion gestartet und kann den Durchsatz arbeitsauslastung beeinträchtigen und Zugriff auf die zugrunde liegende Tabelle vorübergehend zu verzögern.  
  
 OFF  
 Die Tabellensperren werden für die Dauer des Indexvorgangs angewendet. Ein Offlineindexvorgang, bei dem ein gruppierter Index erstellt, neu erstellt oder gelöscht bzw. ein nicht gruppierter Index neu erstellt oder gelöscht wird, aktiviert eine Schemaänderungssperre (SCH-M) für die Tabelle. Dadurch wird verhindert, dass Benutzer für die Dauer des Vorgangs auf die zugrunde liegende Tabelle zugreifen können. Ein Offlineindexvorgang, bei dem ein nicht gruppierter Index erstellt wird, aktiviert eine freigegebene Sperre (S) für die Tabelle. Dadurch werden Updates der zugrunde liegenden Tabelle verhindert. Lesevorgänge, wie SELECT-Anweisungen, sind jedoch zulässig. Heap-Neuerstellungsvorgänge mit mehreren Threads sind zulässig.  
  
 Weitere Informationen finden Sie unter [wie Onlineindexvorgängen](../../relational-databases/indexes/how-online-index-operations-work.md).  
  
> [!NOTE]  
>  Onlineindexvorgänge sind nicht in jeder Edition von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]verfügbar. Weitere Informationen finden Sie unter [Editionen und unterstützte Funktionen für SQL Server 2016](../../sql-server/editions-and-supported-features-for-sql-server-2016.md).  
  
 MOVE TO { *Partition_scheme_name***(***Column_name* [1**,** ...  *n* ] **)** | *Dateigruppe* | **"**Standard**"**  }  
 **Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] und [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
 Gibt einen Speicherort an, an den die Datenzeilen verschoben werden sollen, die sich aktuell auf der Blattebene des gruppierten Indexes befinden. Die Tabelle wird an den neuen Speicherort verschoben. Diese Option gilt nur für Einschränkungen, durch die ein gruppierter Index erstellt wird.  
  
> [!NOTE]  
>  In diesem Zusammenhang ist DEFAULT kein Schlüsselwort. Es ist ein Bezeichner für die Standarddateigruppe und muss begrenzt sein, wie in MOVE TO **"**Standard**"** oder MOVE TO **[**Standard**]**. Wenn **"**Standard**"** angegeben ist, muss die QUOTED_IDENTIFIER-Option ON sein, für die aktuelle Sitzung. Dies ist die Standardeinstellung. Weitere Informationen finden Sie unter [SET QUOTED_IDENTIFIER &#40;Transact-SQL&#41;](../../t-sql/statements/set-quoted-identifier-transact-sql.md).  
  
 { CHECK | NOCHECK } CONSTRAINT  
 Gibt an, dass *Constraint_name* aktiviert oder deaktiviert ist. Diese Option kann nur mit FOREIGN KEY- und CHECK-Einschränkungen verwendet werden. Wenn NOCHECK angegeben wird, wird die Einschränkung deaktiviert, und zukünftige Einfügungen oder Updates der Spalte werden nicht anhand der Einschränkungsbedingungen überprüft. DEFAULT-, PRIMARY KEY- und UNIQUE-Einschränkungen können nicht deaktiviert werden.  
  
 ALL  
 Gibt an, dass alle Einschränkungen entweder mit der NOCHECK-Option deaktiviert oder mit der CHECK-Option aktiviert werden.  
  
 { ENABLE | DISABLE } TRIGGER  
 Gibt an, dass *Form Trigger_name* aktiviert oder deaktiviert ist. Ein Trigger bleibt auch dann für die Tabelle definiert, wenn er deaktiviert ist. Wenn jedoch INSERT-, UPDATE- oder DELETE-Anweisungen in der Tabelle ausgeführt werden, werden die Aktionen im Trigger erst durchgeführt, wenn der Trigger erneut aktiviert wird.  
  
 ALL  
 Gibt an, dass alle Trigger in der Tabelle aktiviert oder deaktiviert werden.  
  
 *Form trigger_name*  
 Gibt den Namen des Triggers an, der deaktiviert oder aktiviert werden soll.  
  
 { ENABLE | DISABLE } CHANGE_TRACKING  
 **Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] und [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
 Gibt an, ob die Änderungsnachverfolgung für die Tabelle deaktiviert bzw. aktiviert wurde. Standardmäßig ist die Änderungsnachverfolgung deaktiviert.  
  
 Diese Option ist nur dann verfügbar, wenn die Änderungsnachverfolgung für die Datenbank aktiviert ist. Weitere Informationen zu dieser Einstellung finden Sie unter [ALTER DATABASE SET-Optionen &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md).  
  
 Um die Änderungsnachverfolgung zu aktivieren, muss die Tabelle über einen Primärschlüssel verfügen.  
  
 MIT **(** TRACK_COLUMNS_UPDATED  **=**  {ON | **OFF** } **)**  
 **Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] und [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
 Gibt an, ob das [!INCLUDE[ssDE](../../includes/ssde-md.md)] verfolgt, welche Spalten mit Änderungsnachverfolgung aktualisiert wurden. Der Standardwert ist OFF.  
  
 SWITCH [PARTITION *Source_partition_number_expression* ] TO [ *Schema_name***.** ] *Target_table* [PARTITION *Target_partition_number_expression* ]  
 **Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] und [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
 Verlagert einen Datenblock auf eine der folgenden Arten:  
  
-   Weist alle Daten einer Tabelle als Partition einer bereits vorhandenen partitionierten Tabelle neu zu.  
  
-   Wechselt eine Partition von einer partitionierten Tabelle zu einer anderen.  
  
-   Weist alle Daten aus einer Partition einer partitionierten Tabelle einer bereits vorhandenen nicht partitionierten Tabelle neu zu.  
  
Wenn *Tabelle* ist eine partitionierte Tabelle *Source_partition_number_expression* muss angegeben werden. Wenn *Target_table* partitioniert ist, *Target_partition_number_expression* muss angegeben werden. Wenn die Daten einer Tabelle als Partition einer vorhandenen partitionierten Tabelle neu zugewiesen werden oder eine Partition von einer partitionierten Tabelle zu einer anderen gewechselt wird, muss die Zielpartition vorhanden und leer sein.  
  
 Wenn die Daten einer Partition neu zugewiesen werden, sodass sie eine einzelne Tabelle bilden, muss die Zieltabelle bereits erstellt und leer sein. Die Quelltabelle oder -partition und die Zieltabelle oder -partition müssen sich in derselben Dateigruppe befinden. Die entsprechenden Indizes oder Indexpartitionen müssen sich ebenfalls in derselben Dateigruppe befinden. Darüber hinaus gelten weitere Einschränkungen für das Wechseln von Partitionen. *Tabelle* und *Target_table* darf nicht identisch sein. *Target_table* kann ein mehrteiliger Bezeichner sein.  
  
 *Source_partition_number_expression* und *Target_partition_number_expression* sind Konstante Ausdrücke, Variablen und Funktionen verweisen können. Diese enthalten benutzerdefinierte Typvariablen und benutzerdefinierte Funktionen. Sie können nicht auf [!INCLUDE[tsql](../../includes/tsql-md.md)]-Ausdrücke verweisen.  
  
 Eine partitionierte Tabelle mit einem gruppierten rowstore-Index verhält sich wie einen partitionierten Heap:  
  
-   Der primäre Schlüssel muss den Partitionsschlüssel enthalten.  
  
-   Ein eindeutiger Index muss den Partitionsschlüssel enthalten.  Beachten Sie, einschließlich des partitionsschlüssels zu einem vorhandenen eindeutigen Index die Eindeutigkeit ändern kann.  
  
-   Um Partitionen zu wechseln, müssen alle nicht gruppierten Indizes den Partitionsschlüssel enthalten.  
  
Für **SWITCH** -Einschränkung beim Verwenden der Replikation finden Sie unter [replizieren partitionierter Tabellen und Indizes](../../relational-databases/replication/publish/replicate-partitioned-tables-and-indexes.md).  
  
 Nicht gruppierte columnstore-Indizes für erstellten [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016 CTP1, und für SQL-Datenbank vor Version V12 wurden in einem nur-Lese Format. Nicht gruppierte columnstore-Indizes müssen neu erstellt werden auf das aktuelle Format (die aktualisiert werden kann) vor jeder PARTITION-Vorgänge ausgeführt werden können.  
  
 Legen Sie **(** FILESTREAM_ON = { *Partition_scheme_name* | *Filestream_filegroup_name* |         **"** standardmäßige**"** | **"**NULL**"** }**)**  
 **Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. |  
  
 Gibt an, wo FILESTREAM-Daten gespeichert werden.  
  
 ALTER TABLE mit der SET FILESTREAM_ON-Klausel ist nur erfolgreich, wenn die Tabelle keine FILESTREAM-Spalten enthält. Die FILESTREAM-Spalten können mit einer zweiten ALTER TABLE-Anweisung hinzugefügt werden.  
  
 Wenn *Partition_scheme_name* angegeben wird, den Regeln für [CREATE TABLE](../../t-sql/statements/create-table-transact-sql.md) anwenden. Die Tabelle sollte bereits für Zeilendaten partitioniert sein, und das Partitionsschema muss die gleiche Partitionsfunktion und die gleichen Partitionsspalten wie das FILESTREAM-Partitionsschema verwenden.  
  
 *Filestream_filegroup_name* gibt den Namen einer FILESTREAM-Dateigruppe. Die Dateigruppe muss eine Datei, die definiert wird, für die Dateigruppe enthalten, mithilfe einer [CREATE DATABASE](../../t-sql/statements/create-database-sql-server-transact-sql.md) oder [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql.md) -Anweisung oder ein Fehler wird ausgelöst.  
  
 **"**Standard**"** gibt an, die FILESTREAM-Dateigruppe mit dem DEFAULT-Eigenschaftensatz. Wenn keine FILESTREAM-Dateigruppe vorhanden ist, wird ein Fehler ausgelöst.  
  
 **"**NULL**"** gibt an, dass alle Verweise auf FILESTREAM-Dateigruppen für die Tabelle entfernt werden. Alle FILESTREAM-Spalten müssen zuerst gelöscht werden. Sie müssen SET FILESTREAM_ON verwenden**= "**NULL**"** alle FILESTREAM-Daten zu löschen, die einer Tabelle zugeordnet ist.  
  
 Legen Sie **(** SYSTEM_VERSIONING  **=**  {OFF | ON [(HISTORY_TABLE = Schema_name. History_table_name [, DATA_CONSISTENCY_CHECK = { **ON** | OFF}])]} **)**  
 **Gilt für**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] und [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
 Entweder versionsverwaltung durch das System einer Tabelle aktiviert oder deaktiviert versionsverwaltung durch das System einer Tabelle. Zum Aktivieren einer Tabelle versionsverwaltung durch das System überprüft, dass der Datentyp, NULL-Zulässigkeit Einschränkung und primary Key-Einschränkung-Anforderungen für die versionsverwaltung durch das System erfüllt sind. Wenn das Argument HISTORY_TABLE nicht verwendet wird, wird das System generiert eine neuen Verlaufstabelle, die dem Schema der aktuellen Tabelle aus, erstellen eine Verknüpfung zwischen den beiden Tabellen entsprechen und kann das System den Verlauf jeder Datensatz in der aktuellen Tabelle in der Verlaufstabelle aufgezeichnet. Der Name dieser Verlaufstabelle `MSSQL_TemporalHistoryFor<primary_table_object_id>`. Wenn das Argument HISTORY_TABLE einen Link zu erstellen und verwenden eine vorhandene Verlaufstabelle verwendet wird, wird die Verknüpfung zwischen der aktuellen Tabelle und der angegebenen Tabelle erstellt. Wenn Sie einen Link zu einer vorhandenen Verlaufstabelle erstellen, können Sie eine Datenkonsistenzprüfung durchführen. Diese datenkonsistenzprüfung stellt sicher, dass vorhandene Einträge sich nicht überlappen. Die Datenkonsistenzprüfung ist standardmäßig aktiviert. Weitere Informationen finden Sie unter [Temporal Tables](../../relational-databases/tables/temporal-tables.md).  
  
HISTORY_RETENTION_PERIOD = { **UNENDLICHE** | Anzahl {Tag | TAGE | WOCHE |  WOCHEN | MONAT | MONATE | JAHR | Jahre}} **betrifft**: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  

Gibt die begrenzter oder Infinite Aufbewahrung Verlaufsdaten in temporalen Tabelle mit. Wenn nicht angegeben, wird eine unbegrenzte Aufbewahrungsdauer ausgegangen.
  
 LEGEN SIE **(** LOCK_ESCALATION = {AUTOMATISCH | TABELLE | DEAKTIVIEREN SIE} **)**  
 **Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] und [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
 Gibt die zulässigen Methoden der Sperrenausweitung für eine Tabelle an.  
  
 AUTO  
 Mit dieser Option kann vom [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] die für das Tabellenschema geeignete Granularität der Sperrenausweitung ausgewählt werden.  
  
-   Wenn die Tabelle partitioniert ist, wird die Sperrenausweitung bis zur Partition erlaubt. Nach der Ausweitung der Sperre auf die Partitionsebene wird die Sperrenausweitung nicht bis zur TABLE-Granularität fortgeführt.  
  
-   Wenn die Tabelle nicht partitioniert ist, wird die Sperre bis zur TABLE-Granularität ausgeweitet.  
  
TABLE  
 Die Sperrenausweitung wird immer mit der Granularität der Tabellenebene ausgeführt, unabhängig davon, ob die Tabelle partitioniert ist. TABLE ist der Standardwert.  
  
 DISABLE  
 Verhindert die Sperrenausweitung in den meisten Fällen. Sperren auf Tabellenebene sind jedoch nicht völlig ausgeschlossen. Wenn Sie z. B. eine Tabelle scannen, die keinen gruppierten Index unter der Serializable-Isolationsstufe aufweist, muss das [!INCLUDE[ssDE](../../includes/ssde-md.md)] eine Tabellensperre zulassen, damit die Datenintegrität gewahrt wird.  
  
 REBUILD  
 Verwenden Sie die REBUILD WITH-Syntax, um eine gesamte Tabelle neu zu erstellen, einschließlich aller Partitionen in einer partitionierten Tabelle. Wenn die Tabelle einen gruppierten Index besitzt, erstellt die REBUILD-Option den gruppierten Index neu. REBUILD kann als ONLINE-Vorgang ausgeführt werden.  
  
 Verwenden Sie die REBUILD PARTITION-Syntax, um eine einzelne Partition in einer partitionierten Tabelle neu zu erstellen.  
  
 PARTITION = ALL  
 **Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] und [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
 Erstellt alle Partitionen neu, wenn die Komprimierungseinstellungen für die Partition geändert werden.  
  
 REBUILD WITH ( \<Rebuild_option >)  
 Alle Optionen gelten für eine Tabelle mit einem gruppierten Index. Wenn die Tabelle nicht über einen gruppierten Index verfügt, wird die Heapstruktur nur von einigen der Optionen beeinflusst.  
  
 Wenn mit dem REBUILD-Vorgang keine bestimmte Komprimierungseinstellung angegeben wird, wird die aktuelle Komprimierungseinstellung für die Partition verwendet. Um die aktuelle Einstellung zurückzugeben, Fragen den **Data_compression** Spalte in der **sys.partitions** -Katalogsicht angezeigt.  
  
 Eine vollständige Beschreibung der Optionen für die Neuerstellung finden Sie unter [Index_option &#40; Transact-SQL &#41; ](../../t-sql/statements/alter-table-index-option-transact-sql.md).  
  
 DATA_COMPRESSION  
 **Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] und [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
 Gibt die Datenkomprimierungsoption für die angegebene Tabelle, die Partitionsnummer oder den Bereich von Partitionen an. Folgende Optionen stehen zur Verfügung:  
  
 NONE  
 Die Tabelle oder die angegebenen Partitionen werden nicht komprimiert. Gilt nicht für columnstore-Tabellen.  
  
 ROW  
 Die Tabelle oder die angegebenen Partitionen werden mit Zeilenkomprimierung komprimiert. Gilt nicht für columnstore-Tabellen.  
  
 PAGE  
 Die Tabelle oder die angegebenen Partitionen werden mit Seitenkomprimierung komprimiert. Gilt nicht für columnstore-Tabellen.  
  
 COLUMNSTORE  
 **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] und [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
 Gilt nur für columnstore-Tabellen. COLUMNSTORE gibt an, dass eine Partition, die mit der COLUMNSTORE_ARCHIVE-Option komprimiert wurde, dekomprimiert werden soll. Nachdem die Daten wiederhergestellt wurden, sind sie weiterhin mit der columnstore-Komprimierung komprimiert, die für alle columnstore-Tabellen verwendet wird.  
  
 COLUMNSTORE_ARCHIVE  
 **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] und [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
 Gilt nur für columnstore-Tabellen. Dies sind Tabellen, die mit einem gruppierten columnstore-Index gespeichert wurden. Durch COLUMNSTORE_ARCHIVE wird die angegebene Partition weiter in eine geringere Größe komprimiert. Dies empfiehlt sich bei der Archivierung und in Situationen, in denen es auf eine geringere Speicherbelegung und nicht auf den zusätzlichen Zeitaufwand für das Speichern und Abrufen ankommt.  
  
 Um mehrere Partitionen gleichzeitig neu zu erstellen, finden Sie unter [Index_option &#40; Transact-SQL &#41; ](../../t-sql/statements/alter-table-index-option-transact-sql.md). Wenn die Tabelle nicht über einen gruppierten Index verfügt, werden bei Änderungen an der Datenkomprimierung der Heap und die nicht gruppierten Indizes neu erstellt. Weitere Informationen zur Komprimierung finden Sie unter [Datenkomprimierung](../../relational-databases/data-compression/data-compression.md).  
  
 ONLINE  **=**  {ON | **OFF** } \<wie für Single_partition_rebuild_option >  
 Gibt an, ob eine einzelne Partition der zugrunde liegenden Tabellen und der zugeordneten Indizes für Abfragen und Datenänderungen während des Indexvorgangs verfügbar sind. Der Standardwert ist OFF. REBUILD kann als ONLINE-Vorgang ausgeführt werden.  
  
 ON  
 Lang andauernde Sperren werden nicht für die Dauer des Indexvorgangs aufrechterhalten. Erfordert eine S-Sperre für die Tabelle am Anfang der Indexneuerstellung und eine Sch-M-Sperre für die Tabelle am Ende der Onlineneuerstellung des Indexes. Obwohl beide Sperren kurze Metadatensperren sind, muss insbesondere die Sch-M-Sperre auf den Abschluss aller blockierenden Transaktionen warten. Während der Wartezeit sperrt die Sch-M-Sperre alle anderen Transaktionen, die an dieser Sperre warten, wenn sie auf die gleiche Tabelle zugreifen.  
  
> [!NOTE]  
>  Neuerstellung von Onlineindizes kann festlegen, die *Low_priority_lock_wait* weiter unten in diesem Abschnitt beschriebenen Optionen.  
  
 OFF  
 Die Tabellensperren werden für die Dauer des Indexvorgangs angewendet. Dadurch wird verhindert, dass Benutzer für die Dauer des Vorgangs auf die zugrunde liegende Tabelle zugreifen können.  
  
 *spaltensatzname* XML COLUMN_SET FOR ALL_SPARSE_COLUMNS  
 **Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] und [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
 Der Name des Spaltensatzes. Bei einem Spaltensatz handelt es sich um eine nicht typisierte XML-Darstellung, die alle Sparsespalten einer Tabelle in einer strukturierten Ausgabe kombiniert. Sie können einer Tabelle, die Sparsespalten enthält, keinen Spaltensatz hinzufügen. Weitere Informationen zu Spaltensätzen finden Sie unter [Verwenden von Spaltensätzen](../../relational-databases/tables/use-column-sets.md).  
  
 { ENABLE | DISABLE } FILETABLE_NAMESPACE  
 **Gilt für**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Aktiviert oder deaktiviert die systemdefinierten Einschränkungen für eine FileTable. Kann nur mit einer FileTable verwendet werden.  
  
 Legen Sie (FILETABLE_DIRECTORY = *Directory_name* )  
 **Gilt für**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Gibt den Windows-kompatiblen FileTable-Verzeichnisnamen an. Dieser Name sollte für alle FileTable-Verzeichnisnamen in der Datenbank eindeutig sein. Bei Eindeutigkeitsvergleichen wird die Groß-/Kleinschreibung nicht beachtet, unabhängig von den SQL-Sortiereinstellungen. Kann nur mit einer FileTable verwendet werden.  
```    
 SET (  
        REMOTE_DATA_ARCHIVE   
        {  
            = ON (  <table_stretch_options> )  
          | = OFF_WITHOUT_DATA_RECOVERY  
          ( MIGRATION_STATE = PAUSED ) | ( <table_stretch_options> [, ...n] )  
        } )  
```    
**Gilt für**: [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Aktiviert oder deaktiviert die Stretch-Datenbank für eine Tabelle. Weitere Informationen finden Sie unter [Stretch Database](../../sql-server/stretch-database/stretch-database.md).  
  
 **Aktivieren von Stretch-Datenbank für eine Tabelle**  
  
 Wenn Sie Stretch für eine Tabelle durch Angabe aktivieren `ON`, müssen Sie auch angeben `MIGRATION_STATE = OUTBOUND` beginnen sofort, Migrieren von Daten oder `MIGRATION_STATE = PAUSED` um die Datenmigration zu verschieben. Der Standardwert lautet `MIGRATION_STATE = OUTBOUND`. Weitere Informationen zum Aktivieren von Stretch für eine Tabelle finden Sie unter [Aktivieren von Stretch-Datenbank für eine Tabelle](../../sql-server/stretch-database/enable-stretch-database-for-a-table.md).  
  
 **Voraussetzungen**. Bevor Sie Stretch für eine Tabelle aktivieren, müssen Sie Stretch aktivieren, auf dem Server und in der Datenbank. Weitere Informationen finden Sie unter [Enable Stretch Database for a database](../../sql-server/stretch-database/enable-stretch-database-for-a-database.md).  
  
 **Berechtigungen**. Aktivieren von Stretch für eine Datenbank oder einer Tabelle erfordert Db_owner-Berechtigungen. Aktivieren von Stretch für eine Tabelle benötigen Sie außerdem ALTER-Berechtigungen für die Tabelle.  
  
 **Deaktivieren von Stretch-Datenbank für eine Tabelle**  
  
 Wenn Sie Stretch für eine Tabelle deaktivieren, haben Sie zwei Optionen für die Remotedaten, die bereits zu Azure migriert wurde. Weitere Informationen finden Sie unter [Deaktivieren von Stretch Database und Zurückholen von Remotedaten](../../sql-server/stretch-database/disable-stretch-database-and-bring-back-remote-data.md).  
  
-   Führen Sie den folgenden Befehl aus, um Stretch für eine Tabelle zu deaktivieren und die Remotedaten einer Tabelle aus Azure zurück zu SQL Server zu kopieren. Dieser Befehl kann nicht abgebrochen werden.  
  
    ```tsql  
ALTER TABLE \<table name>
       SET ( REMOTE_DATA_ARCHIVE ( MIGRATION_STATE = INBOUND ) ) ;  
    ```  
  
     Dieser Vorgang verursacht Datenübertragungskosten und kann nicht abgebrochen werden. Weitere Informationen finden Sie unter [Datenübertragungen – Preisdetails](https://azure.microsoft.com/en-us/pricing/details/data-transfers/).  
  
     Nachdem die Remotedaten von Azure zurück zu SQL Server kopiert wurden, wird Stretch für die Tabelle deaktiviert.  
  
-   Führen Sie den folgenden Befehl aus, um Stretch für eine Tabelle zu deaktivieren und die Remotedaten zu verwerfen.  
  
    ```tsql  
ALTER TABLE \<table_name>
       SET ( REMOTE_DATA_ARCHIVE = OFF_WITHOUT_DATA_RECOVERY ( MIGRATION_STATE = PAUSED ) ) ;  
    ```  
  
 Nachdem Sie Stretch Database für eine Tabelle deaktiviert haben, wird die Datenmigration beendet und die Abfrageergebnisse enthalten keine Ergebnisse aus der Remotetabelle mehr.  
  
 Das Deaktivieren von Stretch wird die Remotetabelle nicht entfernt werden. Wenn Sie die Remotetabelle löschen möchten, müssen Sie sie mithilfe des Azure-Verwaltungsportals löschen.  
  
[FILTER_PREDICATE = {null | *Prädikat* }]  
 **Gilt für**: [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Gibt optional ein Filterprädikat zum Auswählen von Zeilen aus einer Tabelle zu migrieren, die Verlaufsdaten und aktuelle Daten enthält. Das Prädikat muss eine deterministische Inline-Tabellenwertfunktion aufrufen. Weitere Informationen finden Sie unter [Aktivieren von Stretch-Datenbank für eine Tabelle](../../sql-server/stretch-database/enable-stretch-database-for-a-table.md) und [auswählen zu migrierender mithilfe einer Filterfunktion &#40; Zeilen Stretch-Datenbank &#41; ](../../sql-server/stretch-database/select-rows-to-migrate-by-using-a-filter-function-stretch-database.md).   
  
> [!IMPORTANT]  
>  Wenn Sie ein schwaches Filterprädikat angeben, wird die Datenmigration ebenfalls unzureichend ausgeführt. Stretch-Datenbank wendet das Filterprädikat über den CROSS APPLY-Operator auf die Tabelle an.  
  
 Wenn Sie kein Filterprädikat angeben, wird die gesamte Tabelle migriert.  
  
 Wenn Sie kein Filterprädikat angeben, müssen Sie auch angeben *MIGRATION_STATE*.  
  
 MIGRATION_STATE = {AUSGEHENDE |  EINGEHENDE | ANGEHALTEN}  
 **Gilt für**: [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
-   Geben Sie `OUTBOUND` zum Migrieren von Daten aus SQL Server in Azure.  
  
-   Geben Sie `INBOUND` So kopieren Sie die Remote-Daten für die Tabelle aus Azure zu SQL Server und zum Deaktivieren von Stretch für die Tabelle zurück. Weitere Informationen finden Sie unter [Deaktivieren von Stretch Database und Zurückholen von Remotedaten](../../sql-server/stretch-database/disable-stretch-database-and-bring-back-remote-data.md).  
  
     Dieser Vorgang verursacht Datenübertragungskosten und kann nicht abgebrochen werden.  
  
-   Geben Sie `PAUSED` anhalten oder Zurückstellen der Datenmigration. Weitere Informationen finden Sie unter [anhalten und Fortsetzen der Datenmigration &#40; Stretch-Datenbank &#41; ](../../sql-server/stretch-database/pause-and-resume-data-migration-stretch-database.md).  
  
WAIT_AT_LOW_PRIORITY  
 **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] und [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
 Bei der Onlineindexneuerstellung muss auf blockierende Vorgänge für diese Tabelle gewartet werden. **WAIT_AT_LOW_PRIORITY** gibt an, dass der Vorgang zur onlineindexneuerstellung Sperren mit niedriger Priorität, sodass andere Vorgänge, während die onlineindexerstellung wartet gewartet wird. Das Weglassen der **WAIT AT LOW PRIORITY** -Option ist gleichwertig mit WA`IT_AT_LOW_PRIORITY ( MAX_DURATION = 0 minutes, ABORT_AFTER_WAIT = NONE)`.  
  
 MAX_DURATION = *Zeit* [**Minuten** ]  
 **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] und [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
 Die Wartezeit (ein Integerwert in Minuten angegeben), die die **SWITCH** oder Sperren der onlineindexneuerstellung mit niedriger Priorität warten, wenn den DDL-Befehl ausgeführt. Wenn der Vorgang blockiert wird die **MAX_DURATION** Zeit, eines der **ABORT_AFTER_WAIT** -Aktionen ausgeführt. **MAX_DURATION** ist immer in Minuten, und das Wort **Minuten** kann ausgelassen werden.  
  
 ABORT_AFTER_WAIT = [**NONE** | **SELF** | **BLOCKERN** }]  
 **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] und [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
 Keine  
 Es wird weiterhin mit normaler (regulärer) Priorität auf die Sperre gewartet.  
  
 SELF  
 Beenden der **SWITCH** oder DDL-Vorgang zur onlineindexneuerstellung derzeit ausgeführt wird, ohne eine Aktion auszuführen.  
  
 BLOCKERS  
 Bricht alle Benutzertransaktionen, die derzeit Blockieren der **SWITCH** oder Onlineindex-DDL-Vorgang neu zu erstellen, damit der Vorgang fortgesetzt werden kann.  
  
 Erfordert **ALTER ANY CONNECTION** Berechtigung.  
  
IF VORHANDEN IST  
 **Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] über [aktuelle Version](http://go.microsoft.com/fwlink/p/?LinkId=299658)) und [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
 Löscht die Spalte oder Einschränkung bedingt, nur dann, wenn sie bereits vorhanden ist.  
  
## <a name="remarks"></a>Hinweise  
 Verwenden Sie zum Hinzufügen von neuer Datenzeilen [einfügen](../../t-sql/statements/insert-transact-sql.md). Verwenden Sie zum Entfernen von Datenzeilen [löschen](../../t-sql/statements/delete-transact-sql.md) oder [TRUNCATE TABLE](../../t-sql/statements/truncate-table-transact-sql.md). Um die Werte in vorhandenen Zeilen zu ändern, verwenden [UPDATE](../../t-sql/queries/update-transact-sql.md).  
  
 Wenn der Prozedurcache Ausführungspläne enthält, die auf die Tabelle verweisen, kennzeichnet ALTER TABLE diese für die erneute Kompilierung bei der nächsten Ausführung.  
  
## <a name="changing-the-size-of-a-column"></a>Ändern der Größe einer Spalte  
 Sie können Länge, Präzision oder Dezimalstellen einer Spalte ändern, indem Sie die neue Größe für den Spaltendatentyp in der ALTER COLUMN-Klausel angeben. Wenn die Spalte Daten enthält, darf die neue Größe nicht unter der maximalen Datenmenge liegen. Die Spalte kann nicht auch in einem Index definiert werden, es sei denn, die Spalte ist eine **Varchar**, **Nvarchar**, oder **Varbinary** -Datentyp und der Index ist nicht das Ergebnis eines PRIMÄRSCHLÜSSELS Einschränkung. Siehe Beispiel P.  
  
## <a name="locks-and-alter-table"></a>Sperren und ALTER TABLE  
 Die in ALTER TABLE angegebenen Änderungen werden sofort implementiert. Wenn die Änderungen Änderungen der Zeilen in der Tabelle erfordern, aktualisiert ALTER TABLE die Zeilen. ALTER TABLE belegt die Tabelle mit einer Schemaänderungssperre (SCH-M), um sicherzustellen, dass andere Verbindungen während der Änderung noch nicht einmal auf die Metadaten der Tabelle verweisen können. Eine Ausnahme sind Onlineindexvorgänge, die am Ende eine sehr kurze SCH-M-Sperre erfordern. Bei einem ALTER TABLE…SWITCH-Vorgang werden sowohl die Quell- als auch die Zieltabelle mit der Sperre belegt. Die an der Tabelle vorgenommenen Änderungen werden protokolliert und sind vollständig wiederherstellbar. Änderungen, die sich auf sämtliche Zeilen einer sehr großen Tabelle auswirken (z. B. das Löschen einer Spalte oder in einigen Editionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] das Hinzufügen einer NOT NULL-Spalte mit einem Standardwert) kann viel Zeit in Anspruch nehmen und dazu führen, dass viele Protokolldatensätze generiert werden. Diese ALTER TABLE-Anweisungen sollten ebenso vorsichtig ausgeführt werden wie jede INSERT-, UPDATE- oder DELETE-Anweisung, die sich auf viele Zeilen auswirkt.  
  
### <a name="adding-not-null-columns-as-an-online-operation"></a>Hinzufügen von NOT NULL-Spalten als Onlinevorgang  
 Beginnend mit [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Enterprise Edition ist das Hinzufügen eine NOT NULL-Spalte hat den Standardwert ist ein Onlinevorgang, wenn der Standardwert ist eine *laufzeitkonstante*. Dies bedeutet, dass der Vorgang unabhängig von der Anzahl von Zeilen in der Tabelle nahezu sofort abgeschlossen wird. Dies liegt daran, dass die vorhandenen Zeilen in der Tabelle während des Vorgangs nicht aktualisiert werden. Stattdessen wird der Standardwert nur in den Metadaten der Tabelle gespeichert und der Wert in Abfragen, die auf diese Zeilen zugreifen, nur nach Bedarf gesucht. Dieses Verhalten ist automatisch. Es ist keine zusätzliche Syntax erforderlich, um den Onlinevorgang außerhalb der ADD COLUMN-Syntax zu implementieren. Eine Laufzeitkonstante ist ein Ausdruck, der zur Laufzeit unabhängig vom Determinismus den gleichen Wert für jede Zeile in der Tabelle erzeugt. Der konstante Ausdruck "My temporary data" oder die GETUTCDATETIME()-Systemfunktion sind z. B. Laufzeitkonstanten. Im Gegensatz dazu sind die Funktionen NEWID() oder NEWSEQUENTIALID() keine Laufzeitkonstanten, da für jede Zeile in der Tabelle ein eindeutiger Wert erzeugt wird. Das Hinzufügen einer NOT NULL-Spalte mit einem Standardwert, der keine Laufzeitkonstante ist, wird immer offline ausgeführt, und dabei wird eine exklusive (SCH-M)-Sperre für die Dauer des Vorgangs abgerufen.  
  
 Während die vorhandenen Zeilen auf den in Metadaten gespeicherten Wert verweisen, wird der Standardwert für alle neu eingefügten Zeilen in der Zeile gespeichert, ohne einen anderen Wert für die Spalte anzugeben. Der in Metadaten gespeicherte Standardwert wird in eine vorhandene Zeile verschoben, wenn die Zeile aktualisiert wird (auch wenn die tatsächliche Spalte nicht in der UPDATE-Anweisung angegeben wird) oder wenn die Tabelle oder der gruppierte Index neu erstellt wird.  
  
 Spalten vom Typ **varchar(max)**, **nvarchar(max)**, **varbinary(max)**, **Xml**, **Text**, **Ntext**, **Image**, **Hierarchyid**, **Geometrie**, **Geography**, noch können Sie CLR-UDTS in einem Onlinevorgang hinzugefügt werden. Eine Spalte kann nicht online hinzugefügt werden, wenn dies dazu führt, dass die maximal mögliche Zeilengröße den Grenzwert von 8.060 Bytes überschreitet. Die Spalte wird in diesem Fall als Offlinevorgang hinzugefügt.  
  
## <a name="parallel-plan-execution"></a>Ausführung paralleler Pläne  
 In [!INCLUDE[ssEnterpriseEd11](../../includes/ssenterpriseed11-md.md)] und höher wird die Anzahl der Prozessoren zum Ausführen einer einzelnen ALTER TABLE ADD (Index basiert) Einschränkung oder DROP (gruppierter Index) CONSTRAINT Anweisung richtet sich nach der **Max. Grad an Parallelität** Konfiguration Option und die aktuelle Arbeitslast. Wenn das [!INCLUDE[ssDE](../../includes/ssde-md.md)] erkennt, dass das System ausgelastet ist, wird der Grad an Parallelität für den Vorgang automatisch reduziert, bevor mit der Ausführung der Anweisung begonnen wird. Sie können die Anzahl der Prozessoren, die zur Ausführung der Anweisung verwendet werden, durch Angeben der MAXDOP-Option manuell konfigurieren. Weitere Informationen finden Sie unter [Konfigurieren der Serverkonfigurationsoption Max. Grad an Parallelität](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md).  
  
## <a name="partitioned-tables"></a>Partitionierte Tabellen  
 Neben dem Ausführen von SWITCH-Vorgängen mit partitionierten Tabellen können mit ALTER TABLE der Status der Spalten, Einschränkungen und Trigger einer partitionierten Tabelle genau wie bei nicht partitionierten Tabellen geändert werden. Die Partitionierung der Tabelle selbst kann jedoch mit der Anweisung nicht geändert werden. Verwenden Sie zum Neupartitionieren einer partitionierten Tabelle [ALTER PARTITION SCHEME](../../t-sql/statements/alter-partition-scheme-transact-sql.md) und [ALTER PARTITION FUNCTION](../../t-sql/statements/alter-partition-function-transact-sql.md). Zudem können Sie den Datentyp einer Spalte einer partitionierten Tabelle nicht ändern.  
  
## <a name="restrictions-on-tables-with-schema-bound-views"></a>Einschränkungen für Tabellen mit schemagebundenen Sichten  
 Die Einschränkungen, die für ALTER TABLE-Anweisungen für Tabellen mit schemagebundenen Sichten gelten, sind dieselben, die derzeit beim Ändern von Tabellen mit einem einfachen Index angewendet werden. Das Hinzufügen einer Spalte ist zulässig. Das Entfernen oder Ändern einer Spalte, die Bestandteil einer schemagebundenen Sicht ist, ist dagegen nicht zulässig. Wenn für die ALTER TABLE-Anweisung das Ändern einer in einer schemagebundenen Sicht verwendeten Spalte erforderlich ist, schlägt ALTER TABLE fehl, und das [!INCLUDE[ssDE](../../includes/ssde-md.md)] löst eine Fehlermeldung aus. Weitere Informationen zu schemabindung und indizierten Sichten, finden Sie unter [CREATE VIEW &#40; Transact-SQL &#41; ](../../t-sql/statements/create-view-transact-sql.md).  
  
 Das Hinzufügen oder Entfernen von Triggern für Basistabellen wird durch das Erstellen einer schemagebundenen Sicht, die auf die Tabellen verweist, nicht beeinflusst.  
  
## <a name="indexes-and-alter-table"></a>Indizes und ALTER TABLE  
 Als Teil einer Einschränkung erstellte Indizes werden gelöscht, wenn die Einschränkung gelöscht wird. Mit CREATE INDEX erstellte Indizes müssen mit DROP INDEX gelöscht werden. Die ALTER INDEX-Anweisung kann verwendet werden, um einen Index neu zu erstellen, der Teil einer Einschränkungsdefinition ist. Die Einschränkung muss nicht gelöscht und mit ALTER TABLE erneut hinzugefügt werden.  
  
 Alle auf einer Spalte basierenden Indizes und Einschränkungen müssen entfernt werden, bevor die Spalte entfernt werden kann.  
  
 Wenn eine Einschränkung, für die ein gruppierter Index erstellt wurde, gelöscht wird, werden die Datenzeilen, die auf der Blattebene des gruppierten Indexes gespeichert waren, in einer nicht gruppierten Tabelle gespeichert. Sie können den gruppierten Index löschen und die daraus resultierende Tabelle in einer einzigen Transaktion in eine andere Dateigruppe oder in ein anderes Partitionsschema verschieben, indem Sie die MOVE TO-Option angeben. Die MOVE TO-Option weist die folgenden Einschränkungen auf:  
  
-   MOVE TO ist für indizierte Sichten oder nicht gruppierte Indizes nicht gültig.  
  
-   Das Partitionsschema oder die Dateigruppe muss bereits vorhanden sein.  
  
-   Wird MOVE TO nicht angegeben, wird die Tabelle in demselben Partitionsschema oder derselben Dateigruppe platziert, das bzw. die für den gruppierten Index definiert war.  
  
Wenn Sie einen gruppierten Index löschen, können Sie angeben, dass ONLINE  **=**  Option, damit die DROP INDEX-Transaktion Abfragen und Änderungen an den zugrunde liegenden Daten und die zugehörigen nicht gruppierten Indizes nicht blockiert.  
  
 ONLINE  **=**  ON gelten folgenden Einschränkungen:  
  
-   ONLINE  **=**  ON ist nicht gültig für gruppierte Indizes, die auch deaktiviert werden. Deaktivierte Indizes müssen mit ONLINE gelöscht werden  **=**  OFF.  
  
-   Es können nicht mehrere Indizes gleichzeitig gelöscht werden.  
  
-   ONLINE  **=**  ON ist nicht gültig für indizierte Sichten, nicht gruppierte Indizes oder Indizes für lokale temporäre Tabellen.  
  
-   ONLINE  **=**  ON ist nicht gültig für columnstore-Indizes.  
  
Zum Löschen eines gruppierten Indexes ist temporärer Speicherplatz im Umfang des vorhandenen gruppierten Indexes erforderlich. Dieser zusätzliche Speicherplatz wird nach Abschluss des Vorgangs freigegeben.  
  
> [!NOTE]  
>  Die unter aufgeführten Optionen  *\<Drop_clustered_constraint_option >* gelten für gruppierte Indizes für Tabellen und nicht auf gruppierte Indizes für Sichten oder nicht gruppierte Indizes angewendet werden.  
  
## <a name="replicating-schema-changes"></a>Replizieren von Schemaänderungen  
 Wenn Sie ALTER TABLE für eine veröffentlichte Tabelle auf einem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Verleger ausführen, wird diese Änderung standardmäßig an alle [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Abonnenten weitergegeben. Für diese Funktionalität bestehen einige Einschränkungen, und sie kann deaktiviert werden. Weitere Informationen finden Sie unter [Vornehmen von Schemaänderungen in Veröffentlichungsdatenbanken](../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md).  
  
## <a name="data-compression"></a>Datenkomprimierung  
 Für Systemtabellen ist die Komprimierung nicht verfügbar. Wenn die Tabelle ein Heap ist, erfolgt der Neuerstellungsvorgang für den ONLINE-Modus mit einem einzelnen Thread. Verwenden Sie den OFFLINE-Modus für einen Multithreaded-Neuerstellungsvorgang von Heaps. Weitere Informationen zur datenkomprimierung finden Sie unter[Datenkomprimierung](../../relational-databases/data-compression/data-compression.md).  
  
 Mit der gespeicherten Prozedur [sp_estimate_data_compression_savings](../../relational-databases/system-stored-procedures/sp-estimate-data-compression-savings-transact-sql.md) können Sie einschätzen, wie sich eine Änderung des Komprimierungsstatus auf eine Tabelle, einen Index oder eine Partition auswirkt.  
  
 Für partitionierte Tabellen gelten die folgenden Einschränkungen:  
  
-   Sie können die Komprimierungseinstellung einer einzelnen Partition nicht ändern, wenn die Tabelle nicht ausgerichtete Indizes aufweist.  
  
-   Die Syntax ALTER TABLE \<Tabelle > REBUILD PARTITION...-Syntax wird die angegebene Partition.  
  
-   Die Syntax ALTER TABLE \<Tabelle > REBUILD WITH...-Syntax werden alle Partitionen neu erstellt..  
  
## <a name="dropping-ntext-columns"></a>Löschen von NTEXT-Spalten  
 Wenn NTEXT-Spalten gelöscht werden, wird das Cleanup der gelöschten Daten als serialisierter Vorgang für alle Zeilen durchgeführt. Das kann einige Zeit dauern. Wenn Sie eine NTEXT-Spalte in einer Tabelle mit einer großen Zeilenanzahl löschen, aktualisieren Sie die NTEXT-Spalte zunächst auf den Wert NULL und löschen dann die Spalte. Dieses Verfahren kann mit parallelen Vorgängen ausgeführt werden und kostet deutlich weniger Zeit.  
  
## <a name="online-index-rebuild"></a>Onlineneuerstellung von Indizes  
 Um die DDL-Anweisung für eine Onlineindexneuerstellung auszuführen, müssen alle aktiven blockierenden Transaktionen, die für eine bestimmte Tabelle ausgeführt werden, abgeschlossen sein. Wenn die Onlineindexneuerstellung ausgeführt wird, werden alle neuen Transaktionen, die zur Ausführung in dieser Tabelle bereit sind, blockiert. Obwohl die Sperre für die Onlineindexneuerstellung nur kurz dauert, kann das Warten auf den Abschluss aller noch offenen Transaktionen und das Blockieren aller neuen, zu startenden Transaktionen für eine bestimmte Tabelle den Durchsatz beeinträchtigen, eine Verlangsamung oder einen Ausfall der Arbeitsauslastung verursachen und den Zugriff auf die zugrunde liegende Tabelle deutlich einschränken. Die **WAIT_AT_LOW_PRIORITY** -Option können Datenbankadministratoren zum Verwalten der s- und Sch-M-Sperren muss für die onlineneuerstellung von Indizes und zum Auswählen eines 3-Optionen angegeben. In allen drei Fällen gilt: Wenn während der Wartezeit ( `(MAX_DURATION =n [minutes])` ) keine blockierenden Aktivitäten vorhanden sind, wird die Onlineindexneuerstellung ohne Wartezeit sofort ausgeführt, und die DDL-Anweisung wird abgeschlossen.  
  
## <a name="compatibility-support"></a>Kompatibilitätsunterstützung  
 Die ALTER TABLE-Anweisung lässt nur zweiteilige Tabellennamen (schema.object) zu. In [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] schlägt die Angabe eines Tabellennamens mit den folgenden Formaten zur Kompilierzeit mit Fehler 117 fehl.  
  
-   server.database.schema.table  
  
-   .database.schema.table  
  
-   ..schema.table  
  
Bei früheren Versionen wurde durch die Angabe des Formats "server.database.schema.table" der Fehler 4902 zurückgegeben. Die Angabe des Formats ".database.schema.table" oder "..schema.table" war erfolgreich.  
  
 Um das Problem zu beheben, vermeiden Sie die Verwendung eines vierteiligen Präfixes.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die ALTER-Berechtigung für die Tabelle.  
  
 ALTER TABLE-Berechtigungen gelten für beide an einer ALTER TABLE SWITCH-Anweisung beteiligten Tabellen. Alle verschobenen Daten erben die Sicherheitseinstellungen der Zieltabelle.  
  
 Falls Spalten in der ALTER TABLE-Anweisung mit einem benutzerdefinierten CLR-Typ (Common Language Runtime) oder Aliasdatentyp definiert sind, ist die REFERENCES-Berechtigung für den Typ erforderlich.  
  
 Hinzufügen einer Spalte, die die Zeilen der Tabelle aktualisiert erfordert **UPDATE** Berechtigung für die Tabelle. Z. B. Hinzufügen einer **NOT NULL** Spalte mit einem Standardwert oder das Hinzufügen einer Identitätsspalte aus, wenn die Tabelle nicht leer ist.  
  
##  <a name="Example_Top"></a> Beispiele  
  
|Kategorie|Funktionssyntaxelemente|  
|--------------|------------------------------|  
|[Hinzufügen von Spalten und Einschränkungen](#add)|ADD • PRIMARY KEY mit Indexoptionen • Sparsespalten und Spaltensätze •|  
|[Löschen von Spalten und Einschränkungen](#Drop)|DROP|  
|[Ändern einer Spaltendefinition](#alter_column)|Ändern des Datentyps • Ändern der Spaltengröße • Sortierung|  
|[Ändern einer Tabelle (Definition)](#alter_table)|DATA_COMPRESSION • SWITCH PARTITION • LOCK ESCALATION • Änderungsnachverfolgung|  
|[Deaktivieren und Aktivieren von Einschränkungen und Trigger](#disable_enable)|CHECK • NO CHECK • ENABLE TRIGGER • DISABLE TRIGGER|  
  
###  <a name="add"></a>Hinzufügen von Spalten und Einschränkungen  
 Die Beispiele in diesem Abschnitt veranschaulichen das Hinzufügen von Spalten und Einschränkungen zu einer Tabelle.  
  
#### <a name="a-adding-a-new-column"></a>A. Hinzufügen einer neuen Spalte  
 Im folgenden Beispiel wird eine Spalte hinzugefügt, die NULL-Werte zulässt und für die keine Werte durch eine DEFAULT-Definition bereitgestellt werden. Jede Zeile in der neuen Spalte erhält einen `NULL`-Wert.  
  
```  
CREATE TABLE dbo.doc_exa (column_a INT) ;  
GO  
ALTER TABLE dbo.doc_exa ADD column_b VARCHAR(20) NULL ;  
GO  
  
```  
  
#### <a name="b-adding-a-column-with-a-constraint"></a>B. Hinzufügen einer Spalte mit einer Einschränkung  
 Im folgenden Beispiel wird eine neue Spalte mit einer `UNIQUE`-Einschränkung hinzugefügt.  
  
```  
CREATE TABLE dbo.doc_exc (column_a INT) ;  
GO  
ALTER TABLE dbo.doc_exc ADD column_b VARCHAR(20) NULL   
    CONSTRAINT exb_unique UNIQUE ;  
GO  
EXEC sp_help doc_exc ;  
GO  
DROP TABLE dbo.doc_exc ;  
GO  
```  
  
#### <a name="c-adding-an-unverified-check-constraint-to-an-existing-column"></a>C. Hinzufügen einer nicht überprüften CHECK-Einschränkung zu einer vorhandenen Spalte  
 Im folgenden Beispiel wird einer vorhandenen Spalte in der Tabelle eine Einschränkung hinzugefügt. Die Spalte hat einen Wert, der die Einschränkung verletzt. Deshalb wird `WITH NOCHECK` verwendet, um zu verhindern, dass die Einschränkung für vorhandene Zeilen überprüft wird, und um das Hinzufügen der Einschränkung zu ermöglichen.  
  
```  
CREATE TABLE dbo.doc_exd ( column_a INT) ;  
GO  
INSERT INTO dbo.doc_exd VALUES (-1) ;  
GO  
ALTER TABLE dbo.doc_exd WITH NOCHECK   
ADD CONSTRAINT exd_check CHECK (column_a > 1) ;  
GO  
EXEC sp_help doc_exd ;  
GO  
DROP TABLE dbo.doc_exd ;  
GO  
```  
  
#### <a name="d-adding-a-default-constraint-to-an-existing-column"></a>D. Hinzufügen einer DEFAULT-Einschränkung zu einer vorhandenen Spalte  
 Im folgenden Beispiel wird eine Tabelle mit zwei Spalten erstellt und ein Wert in die erste Spalte eingefügt, während die andere Spalte NULL bleibt. Anschließend wird der zweiten Spalte eine `DEFAULT`-Einschränkung hinzugefügt. Um zu überprüfen, ob der Standardwert angewendet wird, wird ein weiterer Wert in die erste Spalte eingefügt und die Tabelle abgefragt.  
  
```  
CREATE TABLE dbo.doc_exz ( column_a INT, column_b INT) ;  
GO  
INSERT INTO dbo.doc_exz (column_a)VALUES ( 7 ) ;  
GO  
ALTER TABLE dbo.doc_exz  
ADD CONSTRAINT col_b_def  
DEFAULT 50 FOR column_b ;  
GO  
INSERT INTO dbo.doc_exz (column_a) VALUES ( 10 ) ;  
GO  
SELECT * FROM dbo.doc_exz ;  
GO  
DROP TABLE dbo.doc_exz ;  
GO  
```  
  
#### <a name="e-adding-several-columns-with-constraints"></a>E. Hinzufügen mehrerer Spalten mit Einschränkungen  
 Im folgenden Beispiel werden mehrere Spalten mit Einschränkungen hinzugefügt, die mit der neuen Spalte definiert werden. Die erste neue Spalte weist eine `IDENTITY`-Eigenschaft auf. Jede Zeile in der Tabelle besitzt neue inkrementelle Werte in der Identitätsspalte.  
  
```  
CREATE TABLE dbo.doc_exe ( column_a INT CONSTRAINT column_a_un UNIQUE) ;  
GO  
ALTER TABLE dbo.doc_exe ADD   
  
-- Add a PRIMARY KEY identity column.  
column_b INT IDENTITY  
CONSTRAINT column_b_pk PRIMARY KEY,   
  
-- Add a column that references another column in the same table.  
column_c INT NULL    
CONSTRAINT column_c_fk   
REFERENCES doc_exe(column_a),  
  
-- Add a column with a constraint to enforce that   
-- nonnull data is in a valid telephone number format.  
column_d VARCHAR(16) NULL   
CONSTRAINT column_d_chk  
CHECK   
(column_d LIKE '[0-9][0-9][0-9]-[0-9][0-9][0-9][0-9]' OR  
column_d LIKE  
'([0-9][0-9][0-9]) [0-9][0-9][0-9]-[0-9][0-9][0-9][0-9]'),  
  
-- Add a nonnull column with a default.  
column_e DECIMAL(3,3)  
CONSTRAINT column_e_default  
DEFAULT .081 ;  
GO  
EXEC sp_help doc_exe ;  
GO  
DROP TABLE dbo.doc_exe ;  
GO  
```  
  
#### <a name="f-adding-a-nullable-column-with-default-values"></a>F. Hinzufügen einer Spalte, die NULL-Werte zulässt, mit Standardwerten  
 Im folgenden Beispiel wird eine Spalte, die NULL-Werte zulässt, mit einer `DEFAULT`-Definition hinzugefügt und `WITH VALUES` verwendet, um Werte für jede vorhandene Zeile in der Tabelle bereitzustellen. Ohne WITH VALUES hat jede Zeile in der neuen Spalte den Wert NULL.  
  
```  
  
CREATE TABLE dbo.doc_exf ( column_a INT) ;  
GO  
INSERT INTO dbo.doc_exf VALUES (1) ;  
GO  
ALTER TABLE dbo.doc_exf   
ADD AddDate smalldatetime NULL  
CONSTRAINT AddDateDflt  
DEFAULT GETDATE() WITH VALUES ;  
GO  
DROP TABLE dbo.doc_exf ;  
GO  
```  
  
#### <a name="g-creating-a-primary-key-constraint-with-index-options"></a>G. Erstellen einer PRIMARY KEY-Einschränkung mit Indexoptionen  
 Im folgenden Beispiel wird die PRIMARY KEY-Einschränkung `PK_TransactionHistoryArchive_TransactionID` erstellt, und es werden die Optionen `FILLFACTOR`, `ONLINE` und `PAD_INDEX` festgelegt. Der entstehende gruppierte Index hat denselben Namen wie die Einschränkung.  
  
**Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] und [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
```  
USE AdventureWorks2012;  
GO  
ALTER TABLE Production.TransactionHistoryArchive WITH NOCHECK   
ADD CONSTRAINT PK_TransactionHistoryArchive_TransactionID PRIMARY KEY CLUSTERED (TransactionID)  
WITH (FILLFACTOR = 75, ONLINE = ON, PAD_INDEX = ON);  
GO  
```  
  
#### <a name="h-adding-a-sparse-column"></a>H. Hinzufügen einer Sparsespalte  
 In den folgenden Beispielen wird gezeigt, wie Sparsespalten der Tabelle T1 hinzugefügt und geändert werden. Der Code zum Erstellen der Tabelle `T1` lautet wie folgt.  
  
```  
CREATE TABLE T1  
(C1 int PRIMARY KEY,  
C2 varchar(50) SPARSE NULL,  
C3 int SPARSE NULL,  
C4 int ) ;  
GO  
```  
  
 Um eine zusätzliche Sparsespalte `C5` hinzuzufügen, führen Sie die folgende Anweisung aus.  
  
```  
ALTER TABLE T1  
ADD C5 char(100) SPARSE NULL ;  
GO  
```  
  
 Um die Nicht-Sparsespalte `C4` in eine Sparsespalte umzuwandeln, führen Sie die folgende Anweisung aus.  
  
```  
ALTER TABLE T1  
ALTER COLUMN C4 ADD SPARSE ;  
GO  
```  
  
 Konvertiert die `C4` Spalte mit geringer Dichte, eine Spalte ohne geringe Dichte, die folgende Anweisung ausführen.  
  
```  
ALTER TABLE T1  
ALTER COLUMN C4 DROP SPARSE;  
GO  
```  
  
#### <a name="i-adding-a-column-set"></a>I. Hinzufügen eines Spaltensatzes  
 In den folgenden Beispielen wird veranschaulicht, wie eine Spalte der Tabelle `T2` hinzugefügt wird. Sie können einer Tabelle, die bereits Sparsespalten enthält, keinen Spaltensatz hinzufügen. Der Code zum Erstellen der Tabelle `T2` lautet wie folgt.  
  
```  
CREATE TABLE T2  
(C1 int PRIMARY KEY,  
C2 varchar(50) NULL,  
C3 int NULL,  
C4 int ) ;  
GO  
```  
  
 Durch die folgenden drei Anweisungen werden der Spaltensatz `CS` hinzugefügt und dann die Spalten `C2` und `C3` in `SPARSE` geändert.  
  
```  
ALTER TABLE T2  
ADD CS XML COLUMN_SET FOR ALL_SPARSE_COLUMNS ;  
GO  
  
ALTER TABLE T2  
ALTER COLUMN C2 ADD SPARSE ;   
GO  
  
ALTER TABLE T2  
ALTER COLUMN C3 ADD SPARSE ;  
GO  
```  
  
#### <a name="j-adding-an-encrypted-column"></a>J. Eine verschlüsselte Spalte hinzufügen  
 Die folgende Anweisung fügt eine verschlüsselte Spalte mit dem Namen `PromotionCode`.  
  
```  
ALTER TABLE Customers ADD  
    PromotionCode nvarchar(100)   
    ENCRYPTED WITH (COLUMN_ENCRYPTION_KEY = MyCEK,  
    ENCRYPTION_TYPE = RANDOMIZED,  
    ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256') ;  
```  
  
###  <a name="Drop"></a>Löschen von Spalten und Einschränkungen  
 In den Beispielen in diesem Abschnitt wird das Löschen von Spalten und Einschränkungen veranschaulicht.  
  
#### <a name="a-dropping-a-column-or-columns"></a>A. Löschen einer oder mehrerer Spalten  
 Im ersten Beispiel wird eine Tabelle durch Entfernen einer Spalte geändert. Im zweiten Beispiel werden mehrere Spalten entfernt.  
  
```  
CREATE TABLE dbo.doc_exb   
    (column_a INT  
     ,column_b VARCHAR(20) NULL  
     ,column_c datetime  
     ,column_d int) ;  
GO  
-- Remove a single column.  
ALTER TABLE dbo.doc_exb DROP COLUMN column_b ;  
GO  
-- Remove multiple columns.  
ALTER TABLE dbo.doc_exb DROP COLUMN column_c, column_d;  
  
```  
  
#### <a name="b-dropping-constraints-and-columns"></a>B. Löschen von Einschränkungen und Spalten  
 Im ersten Beispiel wird eine `UNIQUE`-Einschränkung aus einer Tabelle entfernt. Im zweiten Beispiel werden zwei Einschränkungen und eine einzelne Spalte entfernt.  
  
```  
CREATE TABLE dbo.doc_exc ( column_a int NOT NULL CONSTRAINT my_constraint UNIQUE) ;  
GO  
  
-- Example 1. Remove a single constraint.  
ALTER TABLE dbo.doc_exc DROP my_constraint ;  
GO  
  
DROP TABLE dbo.doc_exc;  
GO  
  
CREATE TABLE dbo.doc_exc ( column_a int    
                          NOT NULL CONSTRAINT my_constraint UNIQUE  
                          ,column_b int   
                          NOT NULL CONSTRAINT my_pk_constraint PRIMARY KEY) ;  
GO  
  
-- Example 2. Remove two constraints and one column  
-- The keyword CONSTRAINT is optional. The keyword COLUMN is required.  
ALTER TABLE dbo.doc_exc   
  
    DROP CONSTRAINT CONSTRAINT my_constraint, my_pk_constraint, COLUMN column_b ;  
GO  
  
```  
  
#### <a name="c-dropping-a-primary-key-constraint-in-the-online-mode"></a>C. Löschen einer PRIMARY KEY-Einschränkung im ONLINE-Modus  
 Im folgenden Beispiel wird eine PRIMARY KEY-Einschränkung gelöscht, wobei die `ONLINE`-Option auf `ON` festgelegt wird.  
  
```  
  
ALTER TABLE Production.TransactionHistoryArchive  
DROP CONSTRAINT PK_TransactionHistoryArchive_TransactionID  
WITH (ONLINE = ON);  
GO  
```  
  
#### <a name="d-adding-and-dropping-a-foreign-key-constraint"></a>D. Hinzufügen und Löschen einer FOREIGN KEY-Einschränkung  
 Im folgenden Beispiel wird die `ContactBackup`-Tabelle erstellt und dann geändert, indem zuerst eine `FOREIGN KEY`-Einschränkung hinzugefügt wird, die auf die `Person.Person`-Tabelle verweist, und dann die `FOREIGN KEY`-Einschränkung gelöscht wird.  
  
```  
CREATE TABLE Person.ContactBackup  
    (ContactID int) ;  
GO  
  
ALTER TABLE Person.ContactBackup  
ADD CONSTRAINT FK_ContactBacup_Contact FOREIGN KEY (ContactID)  
    REFERENCES Person.Person (BusinessEntityID) ;  
GO  
  
ALTER TABLE Person.ContactBackup  
DROP CONSTRAINT FK_ContactBacup_Contact ;  
GO  
  
DROP TABLE Person.ContactBackup ;  
```  
  
 ![Pfeilsymbol mit Back Link zum Anfang verwendet](../../analysis-services/instances/media/uparrow16x16.gif "Pfeilsymbol mit Back Link zum Anfang verwendet") [Beispiele](#Example_Top)  
  
###  <a name="alter_column"></a>Ändern einer Spaltendefinition  
  
#### <a name="a-changing-the-data-type-of-a-column"></a>A. Ändern des Datentyps einer Spalte  
 Im folgenden Beispiel wird eine Spalte einer Tabelle von `INT` in `DECIMAL` geändert.  
  
```  
CREATE TABLE dbo.doc_exy (column_a INT ) ;  
GO  
INSERT INTO dbo.doc_exy (column_a) VALUES (10) ;  
GO  
ALTER TABLE dbo.doc_exy ALTER COLUMN column_a DECIMAL (5, 2) ;  
GO  
DROP TABLE dbo.doc_exy ;  
GO  
```  
  
#### <a name="b-changing-the-size-of-a-column"></a>B. Ändern der Größe einer Spalte  
 Im folgenden Beispiel wird die Größe des eine **Varchar** Spalte und die Genauigkeit und Skalierung einer **decimal** Spalte. Da die Spalten Daten enthalten, kann die Spaltengröße nur erhöht werden. Beachten Sie auch, dass `col_a` in einem eindeutigen Index definiert ist. Die Größe des `col_a` kann weiterhin erhöht werden, da der Datentyp ist ein **Varchar** und der Index ist nicht das Ergebnis einer PRIMARY KEY-Einschränkung.  
  
```  
-- Create a two-column table with a unique index on the varchar column.  
CREATE TABLE dbo.doc_exy ( col_a varchar(5) UNIQUE NOT NULL, col_b decimal (4,2));  
GO  
INSERT INTO dbo.doc_exy VALUES ('Test', 99.99);  
GO  
-- Verify the current column size.  
SELECT name, TYPE_NAME(system_type_id), max_length, precision, scale  
FROM sys.columns WHERE object_id = OBJECT_ID(N'dbo.doc_exy');  
GO  
-- Increase the size of the varchar column.  
ALTER TABLE dbo.doc_exy ALTER COLUMN col_a varchar(25);  
GO  
-- Increase the scale and precision of the decimal column.  
ALTER TABLE dbo.doc_exy ALTER COLUMN col_b decimal (10,4);  
GO  
-- Insert a new row.  
INSERT INTO dbo.doc_exy VALUES ('MyNewColumnSize', 99999.9999) ;  
GO  
-- Verify the current column size.  
SELECT name, TYPE_NAME(system_type_id), max_length, precision, scale  
FROM sys.columns WHERE object_id = OBJECT_ID(N'dbo.doc_exy');  
```  
  
#### <a name="c-changing-column-collation"></a>C. Ändern von Spaltensortierungen  
 Im folgenden Beispiel wird gezeigt, wie die Sortierung einer Spalte geändert wird. Zuerst wird eine Tabelle mit der standardmäßigen Benutzersortierung erstellt.  
  
```  
CREATE TABLE T3  
(C1 int PRIMARY KEY,  
C2 varchar(50) NULL,  
C3 int NULL,  
C4 int ) ;  
GO  
```  
  
 Anschließend wird die Sortierung der Spalte `C2` in Latin1_General_BIN geändert. Beachten Sie, dass der Datentyp erforderlich ist, auch wenn er nicht geändert wird.  
  
```  
ALTER TABLE T3  
ALTER COLUMN C2 varchar(50) COLLATE Latin1_General_BIN;  
GO  
  
```  

  
###  <a name="alter_table"></a>Ändern einer Tabelle (Definition)  
 Die Beispiele in diesem Abschnitt veranschaulichen, wie die Definition einer Tabelle geändert wird.  
  
#### <a name="a-modifying-a-table-to-change-the-compression"></a>A. Ändern einer Tabelle, um die Komprimierung zu ändern  
 Im folgenden Beispiel wird die Komprimierung einer nicht partitionierten Tabelle geändert. Der Heap oder der gruppierte Index wird neu erstellt. Wenn die Tabelle ein Heap ist, werden alle nicht gruppierten Indizes neu erstellt.  
  
```  
ALTER TABLE T1   
REBUILD WITH (DATA_COMPRESSION = PAGE);  
```  
  
 Im folgenden Beispiel wird die Komprimierung einer partitionierten Tabelle geändert. Die `REBUILD PARTITION = 1`-Syntax bewirkt, dass nur die Partition `1` neu erstellt wird.  
  
**Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] und [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
```  
ALTER TABLE PartitionTable1   
REBUILD PARTITION = 1 WITH (DATA_COMPRESSION =  NONE) ;  
GO  
```  
  
Mit der folgenden alternativen Syntax werden im gleichen Vorgang alle Partitionen in der Tabelle neu erstellt.  
  
**Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] und [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
```  
ALTER TABLE PartitionTable1   
REBUILD PARTITION = ALL   
WITH (DATA_COMPRESSION = PAGE ON PARTITIONS(1) ) ;  
```  
  
 Zusätzliche Beispiele zur datenkomprimierung finden Sie unter [Datenkomprimierung](../../relational-databases/data-compression/data-compression.md).  
  
#### <a name="b-modifying-a-columnstore-table-to-change-archival-compression"></a>B. Ändern einer columnstore-Tabelle, um die Archivierungskomprimierung zu ändern  
 Im folgenden Beispiel wird eine columnstore-Tabellenpartition weiter komprimiert, indem ein zusätzlicher Komprimierungsalgorithmus angewendet wird. Dadurch wird zwar die Tabellengröße reduziert, allerdings erhöht sich auch die zum Speichern und Abrufen benötigte Zeit. Dies empfiehlt sich bei der Archivierung und in Situationen, in denen es auf eine geringere Speicherbelegung und nicht auf den zusätzlichen Zeitaufwand für das Speichern und Abrufen ankommt.  
  
**Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] und [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
```  
ALTER TABLE PartitionTable1   
REBUILD PARTITION = 1 WITH (DATA_COMPRESSION =  COLUMNSTORE_ARCHIVE) ;  
GO  
```  
  
Im folgenden Beispiel wird eine columnstore-Tabellenpartition, die mit der COLUMNSTORE_ARCHIVE-Option komprimiert wurde, dekomprimiert. Nachdem die Daten wiederhergestellt wurden, sind sie weiterhin mit der columnstore-Komprimierung komprimiert, die für alle columnstore-Tabellen verwendet wird.  
  
**Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] und [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
```  
ALTER TABLE PartitionTable1   
REBUILD PARTITION = 1 WITH (DATA_COMPRESSION =  COLUMNSTORE) ;  
GO  
```  
  
#### <a name="c-switching-partitions-between-tables"></a>C. Wechseln von Partitionen zwischen Tabellen  
 Im folgenden Beispiel wird eine partitionierte Tabelle erstellt, wobei vorausgesetzt wird, dass das `myRangePS1`-Partitionsschema bereits in der Datenbank erstellt wurde. Anschließend wird eine nicht partitionierte Tabelle mit derselben Struktur wie die partitionierte Tabelle und in derselben Dateigruppe wie `PARTITION 2` der `PartitionTable`-Tabelle erstellt. Die Daten von `PARTITION 2` der `PartitionTable`-Tabelle werden dann in die `NonPartitionTable`-Tabelle verschoben.  
  
```  
CREATE TABLE PartitionTable (col1 int, col2 char(10))  
ON myRangePS1 (col1) ;  
GO  
CREATE TABLE NonPartitionTable (col1 int, col2 char(10))  
ON test2fg ;  
GO  
ALTER TABLE PartitionTable SWITCH PARTITION 2 TO NonPartitionTable ;  
GO  
```  
  
#### <a name="d-allowing-lock-escalation-on-partitioned-tables"></a>D. Zulassen der Sperrenausweitung in partitionierten Tabellen  
 Im folgenden Beispiel wird die Sperrenausweitung auf die Partitionsebene einer partitionierten Tabelle ermöglicht. Wenn die Tabelle nicht partitioniert ist, wird die Sperrenausweitung auf der TABLE-Ebene festgelegt.  
  
**Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] und [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
```  
ALTER TABLE dbo.T1 SET (LOCK_ESCALATION = AUTO);  
GO  
```  
  
#### <a name="e-configuring-change-tracking-on-a-table"></a>E. Konfigurieren der Änderungsnachverfolgung in einer Tabelle  
 Im folgenden Beispiel wird die Änderungsnachverfolgung für die `Person.Person`-Tabelle aktiviert.  
  
**Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] und [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
```  
USE AdventureWorks2012;  
ALTER TABLE Person.Person  
ENABLE CHANGE_TRACKING;  
```  
  
Im folgenden Beispiel werden die Änderungsnachverfolgung sowie die Verfolgung von Spalten aktiviert, die während einer Änderung aktualisiert werden.  
  
**Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
```  
USE AdventureWorks2012;  
GO  
ALTER TABLE Person.Person  
ENABLE CHANGE_TRACKING  
WITH (TRACK_COLUMNS_UPDATED = ON)  
```  
  
Im folgenden Beispiel wird die Änderungsnachverfolgung für die `Person.Person`-Tabelle deaktiviert.  
  
**Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] und [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
```  
USE AdventureWorks2012;  
Go  
ALTER TABLE Person.Person  
DISABLE CHANGE_TRACKING;  
```  

  
###  <a name="disable_enable"></a>Deaktivieren und Aktivieren von Einschränkungen und Trigger  
  
#### <a name="a-disabling-and-re-enabling-a-constraint"></a>A. Deaktivieren und erneutes Aktivieren einer Einschränkung  
 Im folgenden Beispiel wird eine Einschränkung deaktiviert, die die in den Daten akzeptierten Gehälter begrenzt. `NOCHECK CONSTRAINT` wird mit `ALTER TABLE` verwendet, um die Einschränkung zu deaktivieren und eine Einfügung zuzulassen, die die Einschränkung normalerweise verletzen würde. Mit `CHECK CONSTRAINT` wird die Einschränkung wieder aktiviert.  
  
```  
CREATE TABLE dbo.cnst_example   
(id INT NOT NULL,  
 name VARCHAR(10) NOT NULL,  
 salary MONEY NOT NULL  
    CONSTRAINT salary_cap CHECK (salary < 100000)  
);  
  
-- Valid inserts  
INSERT INTO dbo.cnst_example VALUES (1,'Joe Brown',65000);  
INSERT INTO dbo.cnst_example VALUES (2,'Mary Smith',75000);  
  
-- This insert violates the constraint.  
INSERT INTO dbo.cnst_example VALUES (3,'Pat Jones',105000);  
  
-- Disable the constraint and try again.  
ALTER TABLE dbo.cnst_example NOCHECK CONSTRAINT salary_cap;  
INSERT INTO dbo.cnst_example VALUES (3,'Pat Jones',105000);  
  
-- Re-enable the constraint and try another insert; this will fail.  
ALTER TABLE dbo.cnst_example CHECK CONSTRAINT salary_cap;  
INSERT INTO dbo.cnst_example VALUES (4,'Eric James',110000) ;  
```  
  
#### <a name="b-disabling-and-re-enabling-a-trigger"></a>B. Deaktivieren und erneutes Aktivieren eines Triggers  
 Im folgenden Beispiel wird die `DISABLE TRIGGER`-Option von `ALTER TABLE` verwendet, um den Trigger zu deaktivieren und eine Einfügung zuzulassen, die den Trigger normalerweise verletzen würde. Anschließend wird der Trigger mithilfe von `ENABLE TRIGGER` wieder aktiviert.  
  
```  
CREATE TABLE dbo.trig_example   
(id INT,   
name VARCHAR(12),  
salary MONEY) ;  
GO  
-- Create the trigger.  
CREATE TRIGGER dbo.trig1 ON dbo.trig_example FOR INSERT  
AS  
IF (SELECT COUNT(*) FROM INSERTED  
WHERE salary > 100000) > 0  
BEGIN  
    print 'TRIG1 Error: you attempted to insert a salary > $100,000'  
    ROLLBACK TRANSACTION  
END ;  
GO  
-- Try an insert that violates the trigger.  
INSERT INTO dbo.trig_example VALUES (1,'Pat Smith',100001) ;  
GO  
-- Disable the trigger.  
ALTER TABLE dbo.trig_example DISABLE TRIGGER trig1 ;  
GO  
-- Try an insert that would typically violate the trigger.  
INSERT INTO dbo.trig_example VALUES (2,'Chuck Jones',100001) ;  
GO  
-- Re-enable the trigger.  
ALTER TABLE dbo.trig_example ENABLE TRIGGER trig1 ;  
GO  
-- Try an insert that violates the trigger.  
INSERT INTO dbo.trig_example VALUES (3,'Mary Booth',100001) ;  
GO  
```  
 
  
### <a name="online-operations"></a>Onlinevorgänge  
  
#### <a name="a-online-index-rebuild-using-low-priority-wait-options"></a>A. Onlineindexneuerstellung mit LOW_PRIORITY_WAIT-Optionen  
 Im folgenden Beispiel wird gezeigt, wie eine Onlineindexneuerstellung mithilfe der LOW_PRIORITY_WAIT-Optionen ausgeführt wird.  
  
**Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] und [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
```  
ALTER TABLE T1   
REBUILD WITH   
(  
    PAD_INDEX = ON,  
    ONLINE = ON ( WAIT_AT_LOW_PRIORITY ( MAX_DURATION = 4 MINUTES, 
                                         ABORT_AFTER_WAIT = BLOCKERS ) )  
)  
;  
```  
  
#### <a name="b-online-alter-column"></a>B. Onlinespaltenänderung  
 Das folgende Beispiel zeigt, wie Sie einen ALTER COLUMN-Vorgang mit der Option ONLINE ausführen.  
  
**Gilt für**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] und [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
```  
CREATE TABLE dbo.doc_exy (column_a INT ) ;  
GO  
INSERT INTO dbo.doc_exy (column_a) VALUES (10) ;  
GO  
ALTER TABLE dbo.doc_exy   
    ALTER COLUMN column_a DECIMAL (5, 2) WITH (ONLINE = ON);  
GO  
sp_help doc_exy;  
DROP TABLE dbo.doc_exy ;  
GO  
```  
  
##  <a name="system_versioning"></a>Versionsverwaltung durch das System  
 Die folgenden vier Beispielen können Sie mit der Syntax für die Verwendung von versionsverwaltung durch das System vertraut machen. Zusätzliche Unterstützung finden Sie unter [erste Schritte mit Temporalen Tabellen mit Systemversionsverwaltung](../../relational-databases/tables/getting-started-with-system-versioned-temporal-tables.md).  
  
**Gilt für**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] und [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
### <a name="a-add-system-versioning-to-existing-tables"></a>A. Versionsverwaltung durch das System vorhandenen Tabellen hinzufügen  
 Im folgende Beispiel wird die versionsverwaltung durch das System zu einer vorhandenen Tabelle hinzufügen, und erstellen eine zukünftige Verlaufstabelle veranschaulicht. In diesem Beispiel wird vorausgesetzt, dass eine vorhandene Tabelle aufgerufen `InsurancePolicy` mit einem Primärschlüssel definiert. In diesem Beispiel füllt die neu erstellten Perioden-Spalten für die versionsverwaltung durch das System mit Standardwerten für die Start- und Endzeiten, da diese Werte darf nicht null sein. Dieses Beispiel verwendet die HIDDEN-Klausel, um sicherzustellen, dass keine Auswirkungen auf vorhandene Anwendungen, die Interaktion mit der aktuellen Tabelle.  Darüber hinaus verwendet HISTORY_RETENTION_PERIOD, die verfügbar ist [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] nur. 
  
```  
--Alter non-temporal table to define periods for system versioning  
ALTER TABLE InsurancePolicy  
ADD PERIOD FOR SYSTEM_TIME (SysStartTime, SysEndTime),   
SysStartTime datetime2 GENERATED ALWAYS AS ROW START HIDDEN NOT NULL 
    DEFAULT GETUTCDATE(),   
SysEndTime datetime2 GENERATED ALWAYS AS ROW END HIDDEN NOT NULL 
    DEFAULT CONVERT(DATETIME2, '9999-12-31 23:59:59.99999999');  
--Enable system versioning with 1 year retention for historical data
ALTER TABLE InsurancePolicy 
SET (SYSTEM_VERSIONING = ON (HISTORY_RETENTION_PERIOD = 1 YEAR));  
```  
  
### <a name="b-migrate-an-existing-solution-to-use-system-versioning"></a>B. Migrieren einer vorhandenen Projektmappe um Versionsverwaltung durch das System zu verwenden.  
 Das folgende Beispiel zeigt, wie zum Migrieren zu versionsverwaltung durch das System aus einer Projektmappe, die Trigger verwendet temporalen Unterstützung zu imitieren. Im Beispiel wird vorausgesetzt, es wird eine vorhandene Lösung, die verwendet eine `ProjectTaskCurrent` Tabelle und eine `ProjectTaskHistory` Spalten der Tabelle für ihre vorhandene Lösung, die verwendet wird das Datum wurde überarbeitet und Änderungsdatum für die Zeiträume, diese zeitraumspalten den datetime2-Datentyp nicht verwenden und dass die `ProjectTaskCurrent` Tabelle wurde kein Primärschlüssel definiert.  
  
```  
-- Drop existing trigger  
DROP TRIGGER ProjectTaskCurrent_Trigger;  
-- Adjust the schema for current and history table  
-- Change data types for existing period columns  
ALTER TABLE ProjectTaskCurrent ALTER COLUMN [Changed Date] datetime2 NOT NULL;  
ALTER TABLE ProjectTaskCurrent ALTER COLUMN [Revised Date] datetime2 NOT NULL;  
  
ALTER TABLE ProjectTaskHistory ALTER COLUMN [Changed Date] datetime2 NOT NULL;  
ALTER TABLE ProjectTaskHistory ALTER COLUMN [Revised Date] datetime2 NOT NULL;  
  
-- Add SYSTEM_TIME period and set system versioning with linking two existing tables  
-- (a certain set of data checks happen in the background)  
ALTER TABLE ProjectTaskCurrent  
ADD PERIOD FOR SYSTEM_TIME ([Changed Date], [Revised Date])  
  
ALTER TABLE ProjectTaskCurrent  
SET (SYSTEM_VERSIONING = ON (HISTORY_TABLE = dbo.ProjectTaskHistory, DATA_CONSISTENCY_CHECK = ON))  
```  
  
### <a name="c-disabling-and-re-enabling-system-versioning-to-change-table-schema"></a>C. Deaktivieren und erneutes Aktivieren der Systemversionsverwaltung Tabellenschema ändern  
 In diesem Beispiel wird gezeigt, wie zum Deaktivieren der versionsverwaltung durch das System auf die `Department` Tabelle, eine Spalte hinzufügen und versionsverwaltung durch das System erneut zu aktivieren. Deaktivieren von versionsverwaltung durch das System ist erforderlich, um das Tabellenschema zu ändern. Führen Sie diese Schritte innerhalb einer Transaktion, um zu verhindern, dass Updates für beide Tabellen beim Aktualisieren des Tabellenschemas, wodurch der Datenbankadministrator, überspringen Sie die Konsistenz der Daten überprüfen, wenn Sie versionsverwaltung durch das System erneut zu aktivieren und eine Leistung zu erhalten profitieren. Beachten Sie, dass Aufgaben wie das Erstellen von Statistiken, wechseln von Partitionen oder Komprimierung anwenden, um eine oder beide Tabellen erfordert keine versionsverwaltung durch das System zu deaktivieren.  
  
```  
BEGIN TRAN  
/* Takes schema lock on both tables */  
ALTER TABLE Department  
    SET (SYSTEM_VERSIONING = OFF);  
/* expand table schema for temporal table */  
ALTER TABLE Department  
     ADD Col5 int NOT NULL DEFAULT 0;  
/* Expand table schema for history table */  
ALTER TABLE DepartmentHistory  
    ADD Col5 int NOT NULL DEFAULT 0;  
/* Re-establish versioning again  */
ALTER TABLE Department  
    SET (SYSTEM_VERSIONING = ON (HISTORY_TABLE=dbo.DepartmentHistory, 
                                 DATA_CONSISTENCY_CHECK = OFF));  
COMMIT   
```  
  
### <a name="d-removing-system-versioning"></a>D. Entfernen von Versionsverwaltung durch das System  
 In diesem Beispiel wird gezeigt, wie entfernen Sie die versionsverwaltung durch das System vollständig aus der Department-Tabelle und Drop der `DepartmentHistory` Tabelle. Möglicherweise möchten Sie optional auch die Perioden-Spalten zum Aufzeichnen von Versionsinformationen für System zu löschen. Beachten Sie, dass Sie entweder gelöscht werden können die `Department` oder `DepartmentHistory` Tabellen während der versionsverwaltung durch das System aktiviert ist.  
  
```  
ALTER TABLE Department  
    SET (SYSTEM_VERSIONING = OFF);  
ALTER TABLE Department  
DROP PEROD FOR SYSTEM_TIME;  
DROP TABLE DepartmentHistory;  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Beispiele: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] und[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 In den folgenden Beispielen A bis C verwendet die FactResellerSales-Tabelle in der [!INCLUDE[ssawPDW](../../includes/ssawpdw-md.md)] Datenbank.  
  
### <a name="e-determining-if-a-table-is-partitioned"></a>E. Bestimmen, ob eine Tabelle partitioniert ist  
 Die folgende Abfrage gibt mindestens eine Zeile zurück, wenn die `FactResellerSales` -Tabelle partitioniert ist. Wenn die Tabelle nicht partitioniert ist, werden keine Zeilen zurückgegeben.  
  
```  
SELECT * FROM sys.partitions AS p  
JOIN sys.tables AS t  
    ON  p.object_id = t.object_id  
WHERE p.partition_id IS NOT NULL  
    AND t.name = 'FactResellerSales';  
```  
  
### <a name="f-determining-boundary-values-for-a-partitioned-table"></a>F. Bestimmen der Begrenzungswerte für eine partitionierte Tabelle  
 Die folgende Abfrage gibt die Begrenzungswerte für jede Partition in der `FactResellerSales` -Tabelle zurück.  
  
```  
SELECT t.name AS TableName, i.name AS IndexName, p.partition_number, 
    p.partition_id, i.data_space_id, f.function_id, f.type_desc, 
    r.boundary_id, r.value AS BoundaryValue   
FROM sys.tables AS t  
JOIN sys.indexes AS i  
    ON t.object_id = i.object_id  
JOIN sys.partitions AS p  
    ON i.object_id = p.object_id AND i.index_id = p.index_id   
JOIN  sys.partition_schemes AS s   
    ON i.data_space_id = s.data_space_id  
JOIN sys.partition_functions AS f   
    ON s.function_id = f.function_id  
LEFT JOIN sys.partition_range_values AS r   
    ON f.function_id = r.function_id and r.boundary_id = p.partition_number  
WHERE t.name = 'FactResellerSales' AND i.type <= 1  
ORDER BY p.partition_number;  
```  
  
### <a name="g-determining-the-partition-column-for-a-partitioned-table"></a>G. Bestimmen die Partitionsspalte für eine partitionierte Tabelle  
 Die folgende Abfrage gibt den Namen der Partitionierungsspalte für die Tabelle zurück. `FactResellerSales`.  
  
```  
SELECT t.object_id AS Object_ID, t.name AS TableName, 
    ic.column_id as PartitioningColumnID, c.name AS PartitioningColumnName   
FROM sys.tables AS t  
JOIN sys.indexes AS i  
    ON t.object_id = i.object_id  
JOIN sys.columns AS c  
    ON t.object_id = c.object_id  
JOIN sys.partition_schemes AS ps  
    ON ps.data_space_id = i.data_space_id  
JOIN sys.index_columns AS ic  
    ON ic.object_id = i.object_id 
    AND ic.index_id = i.index_id AND ic.partition_ordinal > 0  
WHERE t.name = 'FactResellerSales'  
AND i.type <= 1  
AND c.column_id = ic.column_id;  
```  
  
### <a name="h-merging-two-partitions"></a>H. Zusammenführen von zwei Partitionen  
 Im folgenden Beispiel werden zwei Partitionen auf einer Tabelle.  
  
 Die `Customer` Tabelle weist folgende Definition:  
  
```  
CREATE TABLE Customer (  
    id int NOT NULL,  
    lastName varchar(20),  
    orderCount int,  
    orderDate date)  
WITH   
    ( DISTRIBUTION = HASH(id),  
    PARTITION ( orderCount RANGE LEFT  
    FOR VALUES (1, 5, 10, 25, 50, 100)));  
```  
  
 Der folgende Befehl kombiniert die Partitionsgrenzen 10 und 25.  
  
```  
ALTER TABLE Customer MERGE RANGE (10);  
```  
  
 Die neue DDL-Code für die Tabelle ist:  
  
```  
CREATE TABLE Customer (  
    id int NOT NULL,  
    lastName varchar(20),  
    orderCount int,  
    orderDate date)  
WITH   
    ( DISTRIBUTION = HASH(id),  
    PARTITION ( orderCount RANGE LEFT  
    FOR VALUES (1, 5, 25, 50, 100)));  
```  
  
### <a name="i-splitting-a-partition"></a>I. Teilen der partition  
 Im folgenden Beispiel wird eine neue Partition auf einer Tabelle.  
  
 Die `Customer` Tabelle wurde der folgende DDL-Code:  
  
```  
DROP TABLE Customer;  
  
CREATE TABLE Customer (  
    id int NOT NULL,  
    lastName varchar(20),  
    orderCount int,  
    orderDate date)  
WITH   
    ( DISTRIBUTION = HASH(id),  
    PARTITION ( orderCount RANGE LEFT  
    FOR VALUES (1, 5, 10, 25, 50, 100 )));  
```  
  
 Der folgende Befehl erstellt eine neue Partition, die durch den Wert 75, zwischen 50 und 100 gebunden.  
  
```  
ALTER TABLE Customer SPLIT RANGE (75);  
```  
  
 Die neue DDL-Code für die Tabelle ist:  
  
```  
CREATE TABLE Customer (  
   id int NOT NULL,  
   lastName varchar(20),  
   orderCount int,  
   orderDate date)  
   WITH DISTRIBUTION = HASH(id),  
   PARTITION ( orderCount (RANGE LEFT  
      FOR VALUES (1, 5, 10, 25, 50, 75, 100 )));  
```  
  
### <a name="j-using-switch-to-move-a-partition-to-a-history-table"></a>J. Verwenden SWITCH so verschieben Sie eine Partition in einer Verlaufstabelle  
 Im folgenden Beispiel werden die Daten in einer Partition die `Orders` Tabelle zu einer Partition in der `OrdersHistory` Tabelle.  
  
 Die `Orders` Tabelle wurde der folgende DDL-Code:  
  
```  
CREATE TABLE Orders (  
    id INT,  
    city VARCHAR (25),  
    lastUpdateDate DATE,  
    orderDate DATE )  
WITH   
    (DISTRIBUTION = HASH ( id ),  
    PARTITION ( orderDate RANGE RIGHT   
    FOR VALUES ('2004-01-01', '2005-01-01', '2006-01-01', '2007-01-01' )));  
```  
  
 In diesem Beispiel wird die `Orders` Tabelle verfügt über die folgenden Partitionen. Jede Partition enthält Daten.  
  
|Partition|Verfügt über Daten?|Bereich der Grenze|  
|---------------|---------------|--------------------|  
|1|ja|OrderDate < "2004-01-01"|  
|2|ja|"2004-01-01' < = OrderDate <" 2005-01-01 "|  
|3|ja|"2005-01-01' < = OrderDate <" 2006-01-01 "|  
|4|ja|"2006-01-01'< = OrderDate <" 2007-01-01 "|  
|5|ja|"2007-01-01' < = OrderDate|  
  
-   Partition 1 (enthält Daten): OrderDate < "2004-01-01"  
-   Partition 2 (enthält Daten): "2004-01-01' < = OrderDate <" 2005-01-01 "  
-   Partition 3 (enthält Daten): ' 2005-01-01' < = OrderDate < "2006-01-01"  
-   Partition 4 (enthält Daten): "2006-01-01'< = OrderDate <" 2007-01-01 "  
-   Partition 5 (Daten hat): ' 2007-01-01' < = OrderDate  
  
Die `OrdersHistory` Tabelle hat die folgende DDL, die identischen Spalten und Spaltennamen aufweist als die `Orders` Tabelle. Beide sind auf Hash verteilt die `id` Spalte.  
  
```  
CREATE TABLE OrdersHistory (  
   id INT,  
   city VARCHAR (25),  
   lastUpdateDate DATE,  
   orderDate DATE )  
WITH   
    (DISTRIBUTION = HASH ( id ),  
    PARTITION ( orderDate RANGE RIGHT   
    FOR VALUES ( '2004-01-01' )));  
```  
  
 Obwohl die Spalten und die Spaltennamen identisch sein müssen, müssen die Partitionsgrenzen nicht identisch sein. In diesem Beispiel wird die `OrdersHistory` Tabelle verfügt über die folgenden zwei Partitionen, und beide Partitionen leer sind:  
  
-   Partition 1 (keine Daten): OrderDate < "2004-01-01"  
-   Partition 2 (leer): "2004-01-01' < = OrderDate  
  
Für den vorherigen zwei Tabellen, der folgende Befehl verschiebt alle Zeilen mit `OrderDate < '2004-01-01'` aus der `Orders` Tabelle, auf die `OrdersHistory` Tabelle.  
  
```  
ALTER TABLE Orders SWITCH PARTITION 1 TO OrdersHistory PARTITION 1;  
```  
  
 Daher die erste partition im `Orders` leer ist und die erste Partition in `OrdersHistory` Daten enthält. Die Tabellen werden jetzt wie folgt angezeigt:  
  
 `Orders`Tabelle  
  
-   Partition 1 (leer): OrderDate < "2004-01-01"  
-   Partition 2 (enthält Daten): "2004-01-01' < = OrderDate <" 2005-01-01 "  
-   Partition 3 (enthält Daten): ' 2005-01-01' < = OrderDate < "2006-01-01"  
-   Partition 4 (enthält Daten): "2006-01-01'< = OrderDate <" 2007-01-01 "  
-   Partition 5 (Daten hat): ' 2007-01-01' < = OrderDate  
  
 `OrdersHistory`Tabelle  
  
-   Partition 1 (enthält Daten): OrderDate < "2004-01-01"  
-   Partition 2 (leer): "2004-01-01' < = OrderDate  
  
Zum Bereinigen der `Orders` Tabelle können Sie die leere Partition entfernen, indem Sie das Zusammenführen von Partitionen 1 und 2 ist wie folgt:  
  
```  
ALTER TABLE Orders MERGE RANGE ('2004-01-01');  
```  
  
 Nach der Zusammenführung der `Orders` Tabelle verfügt über die folgenden Partitionen:  
  
 `Orders`Tabelle  
  
-   Partition 1 (enthält Daten): OrderDate < "2005-01-01"  
-   Partition 2 (enthält Daten): ' 2005-01-01' < = OrderDate < "2006-01-01"  
-   Partition 3 (enthält Daten): "2006-01-01'< = OrderDate <" 2007-01-01 "  
-   Partition 4 (enthält Daten): ' 2007-01-01' < = OrderDate  
  
Angenommen, ein weiteres Jahr übergibt, und Sie bereit sind, die das Jahr 2005 zu archivieren. Sie können eine leere Partition zuordnen, für das Jahr 2005 in der `OrdersHistory` Tabelle, und teilen Sie die leere Partition wie folgt:  
  
```  
ALTER TABLE OrdersHistory SPLIT RANGE ('2005-01-01');  
```  
  
 Nach der Unterteilung der `OrdersHistory` Tabelle verfügt über die folgenden Partitionen:  
  
 `OrdersHistory`Tabelle  
  
-   Partition 1 (enthält Daten): OrderDate < "2004-01-01"  
-   Partition 2 (leer): "2004-01-01" < "2005-01-01"  
-   Partition 3 (leer): ' 2005-01-01' < = OrderDate  
  
## <a name="see-also"></a>Siehe auch  
 [sys.tables &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-tables-transact-sql.md)   
 [sp_rename &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-rename-transact-sql.md)   
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [DROP TABLE &#40; Transact-SQL &#41;](../../t-sql/statements/drop-table-transact-sql.md)   
 [sp_help &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-transact-sql.md)   
 [ALTER PARTITION SCHEME &#40; Transact-SQL &#41;](../../t-sql/statements/alter-partition-scheme-transact-sql.md)   
 [ALTER PARTITION FUNCTION &#40; Transact-SQL &#41;](../../t-sql/statements/alter-partition-function-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  


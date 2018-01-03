---
title: Sys. dm_sql_referenced_entities (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 11/09/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- dm_sql_referenced_entities_TSQL
- dm_sql_referenced_entities
- sys.dm_sql_referenced_entities
- sys.dm_sql_referenced_entities_TSQL
dev_langs: TSQL
helpviewer_keywords: sys.dm_sql_referenced_entities dynamic management function
ms.assetid: 077111cb-b860-4d61-916f-bac5d532912f
caps.latest.revision: "46"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: ba6329fb017dd398e9ff17586c8bbbab8f3ba455
ms.sourcegitcommit: 2208a909ab09af3b79c62e04d3360d4d9ed970a7
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/02/2018
---
# <a name="sysdmsqlreferencedentities-transact-sql"></a>sys.dm_sql_referenced_entities (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Gibt eine Zeile für jede benutzerdefinierte Entität aus, auf die in der Definition der angegebenen verweisenden Entität in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] anhand des Namens verwiesen wird. Eine Abhängigkeit zwischen zwei Entitäten wird erstellt, wenn eine benutzerdefinierte Entität, die *Entität verwiesen*, angezeigt wird, namentlich in einem persistenten SQL-Ausdruck einer anderen benutzerdefinierten Entität aufgerufen, die *verweisende Entität* . Handelt es sich beispielsweise bei einer gespeicherten Prozedur um die angegebene verweisende Entität, gibt diese Funktion alle benutzerdefinierten Entitäten zurück, auf die die gespeicherte Prozedur verweist, z. B. Tabellen, Sichten, benutzerdefinierte Typen (UDTs) oder andere gespeicherte Prozeduren.  
  
 Verwenden Sie diese dynamische Verwaltungsfunktion, um zu folgenden Entitätstypen, auf die in der verweisenden Entität verwiesen wird, einen Bericht zu erstellen.  
  
-   Schemagebundene Entitäten  
  
-   Nicht schemagebundene Entitäten  
  
-   Datenbankübergreifende und serverübergreifende Entitäten  
  
-   Abhängigkeiten auf Spaltenebene von schemagebundenen und nicht schemagebundenen Entitäten  
  
-   Benutzerdefinierte Typen (Alias und CLR UDT)  
  
-   XML-Schemaauflistungen  
  
-   Partitionsfunktionen  
  
**Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]), [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].  
  
## <a name="syntax"></a>Syntax  
  
```  
sys.dm_sql_referenced_entities (  
    ' [ schema_name. ] referencing_entity_name ' , ' <referencing_class> ' )  
  
<referencing_class> ::=  
{  
    OBJECT  
  | DATABASE_DDL_TRIGGER  
  | SERVER_DDL_TRIGGER  
}  
```  
  
## <a name="arguments"></a>Argumente  
 [ *Schema_name*. ] *Referencing_entity_name*  
 Der Name der verweisenden Entität. *Schema_name* ist erforderlich, wenn die verweisende Klasse OBJECT ist.  
  
 *schema_name.referencing_entity_name* ist **nvarchar(517)**.  
  
 *< Referencing_class >* :: = {OBJECT | DATABASE_DDL_TRIGGER | SERVER_DDL_TRIGGER}  
 Klasse der angegebenen verweisenden Entität. Pro Anweisung kann nur eine Klasse angegeben werden.  
  
 *< Referencing_class >* ist **nvarchar(60)**.  
  
## <a name="table-returned"></a>Zurückgegebene Tabelle  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|referencing_minor_id|**int**|Die Spalten-ID, wenn es sich bei der verweisenden Entität um eine Spalte handelt. Andernfalls ist der Wert 0. Lässt keine NULL-Werte zu.|  
|referenced_server_name|**sysname**|Servername der Entität, auf die verwiesen wird.<br /><br /> Diese Spalte wird für serverübergreifende Abhängigkeiten aufgefüllt, die auf der Angabe eines gültigen vierteiligen Namens basieren. Informationen zu mehrteiligen Namen finden Sie unter [Transact-SQL-Syntaxkonventionen &#40; Transact-SQL &#41; ](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md).<br /><br /> NULL für nicht schemagebundene Abhängigkeiten, für die ohne Angabe eines vierteiligen Namens auf die Entität verwiesen wurde.<br /><br /> NULL für schemagebundene Entitäten, da sich müssen in derselben Datenbank und aus diesem Grund können nur definiert werden mithilfe ein zweiteiligen (*schema.object*) Namen.|  
|referenced_database_name|**sysname**|Datenbankname der Entität, auf die verwiesen wird.<br /><br /> Diese Spalte wird für datenbankübergreifende oder serverübergreifende Verweise aufgefüllt, die auf der Angabe eines gültigen dreiteiligen oder vierteiligen Namens basieren.<br /><br /> NULL für nicht schemagebundene Verweise, wenn auf Basis eines einteiligen oder zweiteiligen Namens angegeben.<br /><br /> NULL für schemagebundene Entitäten, da sich müssen in derselben Datenbank und aus diesem Grund können nur definiert werden mithilfe ein zweiteiligen (*schema.object*) Namen.|  
|referenced_schema_name|**sysname**|Schema, in das die Entität gehört, auf die verwiesen wird.<br /><br /> NULL für nicht schemagebundene Verweise, in denen ohne Angabe des Schemanamens auf die Entität verwiesen wird.<br /><br /> Niemals NULL für schemagebundene Verweise.|  
|referenced_entity_name|**sysname**|Name der Entität, auf die verwiesen wird. Lässt keine NULL-Werte zu.|  
|referenced_minor_name|**sysname**|Der Spaltenname, wenn es sich bei der Entität, auf die verwiesen wird, um eine Spalte handelt. Andernfalls ist der Wert NULL. Beispielsweise hat referenced_minor_name den Wert NULL in der Zeile, in der die Entität, auf die verwiesen wird, selbst aufgeführt wird.<br /><br /> Eine Entität, auf die verwiesen wird, ist eine Spalte, wenn diese in der verweisenden Entität namentlich identifiziert wird oder wenn die übergeordnete Entität in einer SELECT *-Anweisung verwendet wird.|  
|referenced_id|**int**|ID der Entität, auf die verwiesen wird. Wenn referenced_minor_id nicht 0 ist, ist referenced_id die Entität, in der die Spalte definiert wird.<br /><br /> Immer NULL für serverübergreifende Verweise.<br /><br /> NULL für datenbankübergreifende Verweise, wenn die ID nicht bestimmt werden kann, weil die Datenbank offline ist oder die Entität nicht gebunden werden kann.<br /><br /> NULL für Verweise innerhalb der Datenbank, wenn die ID nicht bestimmt werden kann. Für nicht schemagebundene Verweise kann die ID nicht aufgelöst werden, wenn die Entität, auf die verwiesen wird in der Datenbank, oder wenn die namensauflösung hängt vom Aufrufer ist nicht vorhanden ist.  Im letzteren Fall wird Is_caller_dependent auf 1 festgelegt.<br /><br /> Niemals NULL für schemagebundene Verweise.|  
|referenced_minor_id|**int**|Die Spalten-ID, wenn es sich bei der Entität, auf die verwiesen wird, um eine Spalte handelt. Andernfalls ist der Wert 0. Beispielsweise hat referenced_minor_is den Wert NULL in der Zeile, in der die Entität, auf die verwiesen wird, selbst aufgeführt wird.<br /><br /> Für nicht schemagebundene Verweise werden Spaltenabhängigkeiten nur gemeldet, wenn alle Entitäten, auf die verwiesen wird, gebunden werden können. Kann eine der Entitäten, auf die verwiesen wird, nicht gebunden werden, werden keine Abhängigkeiten auf Spaltenebene gemeldet, und referenced_minor_id wird auf 0 gesetzt. Siehe Beispiel D.|  
|referenced_class|**tinyint**|Klasse der Entität, auf die verwiesen wird.<br /><br /> 1 = Objekt oder Spalte<br /><br /> 6 = Typ<br /><br /> 10 = XML-Schemaauflistung<br /><br /> 21 = Partitionsfunktion|  
|referenced_class_desc|**nvarchar(60)**|Klassenbeschreibung der Entität, auf die verwiesen wird.<br /><br /> OBJECT_OR_COLUMN<br /><br /> TYPE<br /><br /> XML_SCHEMA_COLLECTION<br /><br /> PARTITION_FUNCTION|  
|is_caller_dependent|**bit**|Gibt an, dass die Schemabindung für die Entität, auf die verwiesen wird, zur Laufzeit erfolgt. Deshalb hängt die Auflösung der Entitäts-ID vom Schema des Aufrufers ab. Dies ist der Fall, wenn es sich bei der Entität, auf die verwiesen wird, um eine gespeicherte Prozedur, eine erweiterte gespeicherte Prozedur oder um eine benutzerdefinierte Funktion handelt, die in einer EXECUTE-Anweisung aufgerufen wird.<br /><br /> 1 = Die Entität, auf die verwiesen wird, hängt vom Aufrufer ab und wird zur Laufzeit aufgelöst. In diesem Fall ist referenced_id gleich NULL.<br /><br /> 0 = Die Entitäts-ID, auf die verwiesen wird, ist nicht aufruferabhängig. Immer 0 für schemagebundene Verweise sowie für datenbankübergreifende und serverübergreifende Verweise, die explizit einen Schemanamen angeben. Zum Beispiel ist ein Verweis auf eine Entität im Format `EXEC MyDatabase.MySchema.MyProc` nicht aufruferabhängig. Ein Verweis im Format `EXEC MyDatabase..MyProc` ist jedoch aufruferabhängig.|  
|is_ambiguous|**bit**|Gibt an, der Verweis ist mehrdeutig und kann zur Laufzeit in eine benutzerdefinierte Funktion, einen benutzerdefinierten Typ (UDT) oder ein Xquery-Verweis auf eine Spalte vom Typ aufgelöst **Xml**. Nehmen wir beispielsweise an die Anweisung `SELECT Sales.GetOrder() FROM Sales.MySales` in einer gespeicherten Prozedur definiert wird. Bis zur Ausführung der gespeicherten Prozedur ist unbekannt, ob `Sales.GetOrder()` eine benutzerdefinierte Funktion im Schema `Sales` oder in der Spalte namens `Sales` vom Typ UDT mit einer Methode namens `GetOrder()` ist.<br /><br /> 1 = Verweis auf eine benutzerdefinierte Funktion oder Spalte, für die die benutzerdefinierte Typmethode (UDT) mehrdeutig ist.<br /><br /> 0 = Verweis ist eindeutig, oder die Entität kann beim Aufruf der Funktion erfolgreich gebunden werden.<br /><br /> Immer 0 für schemagebundene Verweise.|  
|is_selected|**bit**|**Gilt für**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> 1 = Gibt an, dass das Objekt oder die Spalte ausgewählt ist.|  
|is_updated|**bit**|**Gilt für**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> 1 = Gibt an, dass das Objekt oder die Spalte geändert wurde.|  
|is_select_all|**bit**|**Gilt für**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> 1 = Gibt an, dass das Objekt in einer SELECT *-Klausel verwendet wird (nur auf Objektebene).|  
|is_all_columns_found|**bit**|**Gilt für**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> 1 = Alle Spaltenabhängigkeiten für das Objekt konnten gefunden werden.<br /><br /> 0 = Spaltenabhängigkeiten für das Objekt konnten nicht gefunden werden.|
|is_insert_all|**bit**|**Gilt für**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> 1 = das Objekt in einer INSERT-Anweisung ohne Spaltenliste (nur Objektebene) verwendet wird.|  
|is_incomplete|**bit**|**Gilt für**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP2 bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> 1 = das Objekt oder Spalte hat einen Bindungsfehler und ist daher unvollständig.|
  
## <a name="exceptions"></a>Ausnahmen  
 Gibt unter den folgenden Bedingungen ein leeres Resultset zurück:  
  
-   Ein Systemobjekt wird angegeben.  
  
-   Die angegebene Entität ist in der Datenbank nicht vorhanden.  
  
-   Die angegebene Entität verweist auf keine Entitäten.  
  
-   Ein ungültiger Parameter wird übergeben.  
  
 Gibt einen Fehler zurück, wenn die angegebene verweisende Entität eine nummerierte gespeicherte Prozedur ist.  
  
 Gibt Fehler 2020 zurück, wenn Spaltenabhängigkeiten nicht aufgelöst werden können. Dieser Fehler verhindert nicht, dass die Abfrage Abhängigkeiten auf Objektebene zurückgibt.  
  
## <a name="remarks"></a>Hinweise  
 Diese Funktion kann im Kontext jeder beliebigen Datenbank ausgeführt werden, um die Entitäten zurückzugeben, die auf einen DDL-Trigger auf Serverebene verweisen.  
  
 In der folgenden Tabelle werden die Typen von Entitäten aufgelistet, für die Abhängigkeitsinformationen erstellt und verwaltet werden. Für Regeln, Standardwerte, temporäre Tabellen, temporär gespeicherte Prozeduren oder Systemobjekte werden keine Abhängigkeitsinformationen erstellt oder verwaltet.  
  
|Entitätstyp|Verweisende Entität|Entität, auf die verwiesen wird|  
|-----------------|------------------------|-----------------------|  
|Tabelle|Ja*|ja|  
|Anzeigen|ja|ja|  
|In [!INCLUDE[tsql](../../includes/tsql-md.md)] gespeicherte Prozedur**|ja|ja|  
|Gespeicherte CLR-Prozedur|nein|ja|  
|Benutzerdefinierte Funktion in [!INCLUDE[tsql](../../includes/tsql-md.md)]|ja|ja|  
|CLR-benutzerdefinierte Funktion|nein|ja|  
|CLR-Trigger (DML und DDL)|nein|nein|  
|DML-Trigger in [!INCLUDE[tsql](../../includes/tsql-md.md)]|ja|nein|  
|DDL-Trigger auf Datenbankebene in [!INCLUDE[tsql](../../includes/tsql-md.md)]|ja|nein|  
|DDL-Trigger auf Serverebene in [!INCLUDE[tsql](../../includes/tsql-md.md)]|ja|nein|  
|Erweiterte gespeicherte Prozeduren|nein|ja|  
|Warteschlange|nein|ja|  
|Synonym|nein|ja|  
|Typ (Alias und CLR-benutzerdefinierter Typ)|nein|ja|  
|XML-Schemaauflistung|nein|ja|  
|Partitionsfunktion|nein|ja|  
  
 \*Eine Tabelle als verweisende Entität nachverfolgt wird, nur, wenn er verweist auf eine [!INCLUDE[tsql](../../includes/tsql-md.md)] -Modul, einen benutzerdefinierten Typ oder XML-schemaauflistung in der Definition eines berechnete Spalte, einer CHECK-Einschränkung oder einer DEFAULT-Einschränkung.  
  
 ** Nummerierte gespeicherte Prozeduren mit einem ganzzahligen Wert größer als 1 werden weder als verweisende Entität noch als Entität, auf die verwiesen wird, aufgezeichnet.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die SELECT-Berechtigung für sys.dm_sql_referenced_entities und die VIEW DEFINITION-Berechtigung für die verweisende Entität. Standardmäßig wird die SELECT-Berechtigung der public-Rolle erteilt. Erfordert die Berechtigung VIEW DEFINITION oder ALTER DATABASE DDL TRIGGER für die Datenbank, wenn es sich bei der verweisenden Entität um einen DDL-Trigger auf Datenbankebene handelt. Erfordert die VIEW ANY DEFINITION-Berechtigung für den Server, wenn es sich bei der verweisenden Entität um einen DDL-Trigger auf Serverebene handelt.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-returning-entities-that-are-referenced-by-a-database-level-ddl-trigger"></a>A. Zurückgeben von Entitäten, auf die von einem DDL-Trigger auf Datenbankebene verwiesen wird  
 Im folgenden Beispiel werden die Entitäten (Tabellen und Spalten) zurückgegeben, auf die vom DDL-Trigger auf Datensatzebene  `ddlDatabaseTriggerLog` verwiesen wird.  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT referenced_schema_name, referenced_entity_name, referenced_minor_name,   
    referenced_minor_id, referenced_class_desc  
FROM sys.dm_sql_referenced_entities ('ddlDatabaseTriggerLog', 'DATABASE_DDL_TRIGGER');  
GO  
```  
  
### <a name="b-returning-entities-that-are-referenced-by-an-object"></a>B. Zurückgeben von Entitäten, auf die von einem Objekt verwiesen wird  
 Im folgenden Beispiel werden die Entitäten zurückgegeben, auf die von der benutzerdefinierten Funktion `dbo.ufnGetContactInformation` verwiesen wird.  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT referenced_schema_name, referenced_entity_name, referenced_minor_name,   
    referenced_minor_id, referenced_class_desc, is_caller_dependent, is_ambiguous  
FROM sys.dm_sql_referenced_entities ('dbo.ufnGetContactInformation', 'OBJECT');  
GO  
```  
  
### <a name="c-returning-column-dependencies"></a>C. Zurückgeben von Spaltenabhängigkeiten  
 Im folgenden Beispiel wird die `Table1`-Tabelle mit der berechneten Spalte `c`, die als Summe der Spalten `a` und `b` definiert ist, erstellt. Anschließend wird die `sys.dm_sql_referenced_entities`-Sicht aufgerufen. Die Sicht gibt zwei Zeilen zurück: eine für jede in der berechneten Spalte definierte Spalte.  
  
```sql  
USE AdventureWorks2012;  
GO  
CREATE TABLE dbo.Table1 (a int, b int, c AS a + b);  
GO  
SELECT referenced_schema_name AS schema_name,  
    referenced_entity_name AS table_name,  
    referenced_minor_name AS referenced_column,  
    COALESCE(COL_NAME(OBJECT_ID(N'dbo.Table1'),referencing_minor_id), 'N/A') AS referencing_column_name  
FROM sys.dm_sql_referenced_entities ('dbo.Table1', 'OBJECT');  
GO

-- Remove the table.  
DROP TABLE dbo.Table1;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 schema_name table_name referenced_column referencing_column  
 ----------- ---------- ----------------- ------------------  
 dbo         Table1     a                 c  
 dbo         Table1     b                 c  
```

### <a name="d-returning-non-schema-bound-column-dependencies"></a>D. Zurückgeben von nicht schemagebundenen Spaltenabhängigkeiten  
 Im folgenden Beispiel wird die `Table1`-Tabelle gelöscht und die `Table2`-Tabelle sowie die gespeicherte Prozedur `Proc1` erstellt. Die Prozedur verweist auf die `Table2`-Tabelle und auf die nicht vorhandene `Table1`-Tabelle. Die `sys.dm_sql_referenced_entities`-Sicht wird mit der gespeicherten Prozedur ausgeführt, die als verweisende Entität angegeben ist. Das Resultset zeigt eine Zeile für `Table1` und drei Zeilen für `Table2` an. Da `Table1` nicht vorhanden ist, können die Spaltenabhängigkeiten nicht aufgelöst werden, und es wird der Fehler 2020 zurückgegeben. Die Spalte `is_all_columns_found` gibt 0 für `Table1` zurück. Damit wird angegeben, dass einige Spalten nicht ermittelt werden konnten.  
  
```sql  
USE AdventureWorks2012;  
GO  
IF OBJECT_ID ( 'dbo.Table1', 'U' ) IS NOT NULL   
    DROP TABLE dbo.Table1;  
GO  
CREATE TABLE dbo.Table2 (c1 int, c2 int);  
GO  
CREATE PROCEDURE dbo.Proc1 AS  
    SELECT a, b, c FROM Table1;  
    SELECT c1, c2 FROM Table2;  
GO  
SELECT referenced_id, referenced_entity_name AS table_name, referenced_minor_name AS referenced_column_name, is_all_columns_found  
FROM sys.dm_sql_referenced_entities ('dbo.Proc1', 'OBJECT');  
GO  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 referenced_id table_name   referenced_column_name  is_all_columns_found  
 ------------- ------------ ----------------------- --------------------  
 935674381     Table2       NULL                    1  
 935674381     Table2       C1                      1  
 935674381     Table2       C2                      1  
 NULL          Table1       NULL                    0  

 Msg 2020, Level 16, State 1, Line 1The dependencies reported for entity "dbo.Proc1" might not include references to all columns. This is either because the entity references an object that does not exist or because of an error in one or more statements in the entity.  Before rerunning the query, ensure that there are no errors in the entity and that all objects referenced by the entity exist.
 ```
  
### <a name="e-demonstrating-dynamic-dependency-maintenance"></a>E. Veranschaulichen der dynamischen Verwaltung von Abhängigkeiten  
 Das folgende Beispiel stellt eine Erweiterung von Beispiel D dar und zeigt, dass Abhängigkeiten dynamisch verwaltet werden. Zunächst wird die in Beispiel D gelöschte `Table1`-Tabelle neu erstellt. Danach wird `sys.dm_sql_referenced_entities` erneut ausgeführt. Dabei wird die gespeicherte Prozedur als verweisende Entität angegeben. Das Resultset zeigt, dass beide Tabellen zusammen mit den in der gespeicherten Prozedur definierten zugehörigen Spalten zurückgegeben werden. Außerdem gibt die Spalte `is_all_columns_found` für alle Objekte und Spalten 1 zurück.  
  
```sql  
USE AdventureWorks2012;  
GO  
CREATE TABLE Table1 (a int, b int, c AS a + b);  
GO   
SELECT referenced_id, referenced_entity_name AS table_name, referenced_minor_name as column_name, is_all_columns_found  
FROM sys.dm_sql_referenced_entities ('dbo.Proc1', 'OBJECT');  
GO  
DROP TABLE Table1, Table2;  
DROP PROC Proc1;  
GO  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 referenced_id table_name   referenced_column_name  is_all_columns_found  
 ------------- ------------ ----------------------- --------------------  
 935674381     Table2       NULL                    1 
 935674381     Table2       c1                      1 
 935674381     Table2       c2                      1 
 967674495     Table1       NULL                    1 
 967674495     Table1       a                       1  
 967674495     Table1       b                       1  
 967674495     Table1       c                       1  
 ```
 
### <a name="f-returning-object-or-column-usage"></a>F. Zurückgeben von Objekten und Spalten (Verwendung)  
 Im folgenden Beispiel werden die Objekte und die Spaltenabhängigkeiten der gespeicherten Prozedur `HumanResources.uspUpdateEmployeePersonalInfo` zurückgegeben. Diese Prozedur aktualisiert die Spalten `NationalIDNumber`, `BirthDate,``MaritalStatus`, und `Gender` von der `Employee` Tabelle auf der Grundlage eines angegebenen `BusinessEntityID` Wert. Eine andere gespeicherte Prozedur, `upsLogError`, wird in einem Block vom Typ "TRY…CATCH" definiert, um Ausführungsfehler zu erfassen. Die Spalten `is_selected`, `is_updated` und `is_select_all` geben Informationen darüber zurück, wie diese Objekte und Spalten innerhalb des verweisenden Objekts verwendet werden. Die Tabelle und geänderten Spalten werden mit 1 in der Spalte "is_updated" angegeben. Die Spalte `BusinessEntityID` wird nur ausgewählt und die gespeicherte Prozedur `uspLogError` wird weder ausgewählt noch geändert.  
  
**Gilt für**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
```sql  
SELECT referenced_entity_name AS table_name, referenced_minor_name as column_name, is_selected, is_updated, is_select_all  
FROM sys.dm_sql_referenced_entities ('HumanResources.uspUpdateEmployeePersonalInfo', 'OBJECT');  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 table_name    column_name         is_selected is_updated is_select_all  
 ------------- ------------------- ----------- ---------- -------------  
 uspLogError   NULL                0           0          0  
 Employee      NULL                0           1          0  
 Employee      BusinessEntityID    1           0          0  
 Employee      NationalIDNumber    0           1          0  
 Employee      BirthDate           0           1          0  
 Employee      MaritalStatus       0           1          0  
 Employee      Gender              0           1          0
 ```
  
## <a name="see-also"></a>Siehe auch  
 [sys.dm_sql_referencing_entities &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-sql-referencing-entities-transact-sql.md)   
 [sys.sql_expression_dependencies &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md)  
  
  

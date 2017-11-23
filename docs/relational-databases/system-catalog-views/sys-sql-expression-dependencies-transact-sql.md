---
title: Sys. sql_expression_dependencies (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.sql_expression_dependencies
- sql_expression_dependencies_TSQL
- sql_expression_dependencies
- sys.sql_expression_dependencies_TSQL
dev_langs: TSQL
helpviewer_keywords: sys.sql_expression_dependencies catalog view
ms.assetid: 78a218e4-bf99-4a6a-acbf-ff82425a5946
caps.latest.revision: "42"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 099229e10b875d738e970d8f2c4a0c9ac3e7b5e6
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="syssqlexpressiondependencies-transact-sql"></a>sys.sql_expression_dependencies (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  Enthält eine Zeile für jede Namensabhängigkeit in einer benutzerdefinierten Entität in der aktuellen Datenbank. Dies schließt Abhängigkeiten zwischen systemintern kompilierte, skalare benutzerdefinierte Funktionen und andere [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Module. Eine Abhängigkeit zwischen zwei Entitäten wird erstellt, wenn eine Entität, die *Entität verwiesen*, angezeigt wird, namentlich in einem persistenten SQL-Ausdruck, der einer anderen Entität, die mit dem Namen der *verweisende Entität*. Wird beispielsweise in der Definition einer Sicht auf eine Tabelle verwiesen, hängt die Sicht als verweisende Entität von der Tabelle ab, der Entität, auf die verwiesen wird. Wenn die Tabelle gelöscht wird, ist die Sicht unbrauchbar.  
  
 Weitere Informationen finden Sie unter [Skalarfunktionen für In-Memory OLTP](../../relational-databases/in-memory-oltp/scalar-user-defined-functions-for-in-memory-oltp.md).  
  
 Sie können diese Katalogsicht verwenden, um einen Bericht mit den Abhängigkeitsinformationen für die folgenden Entitäten zu erstellen:  
  
-   Schemagebundene Entitäten.  
  
-   Nicht schemagebundene Entitäten.  
  
-   Datenbankübergreifende und serverübergreifende Entitäten. Entitätsnamen werden gemeldet; Entitäts-IDs werden jedoch nicht aufgelöst.  
  
-   Abhängigkeiten auf Spaltenebene für schemagebundene Entitäten. Abhängigkeiten auf Spaltenebene für nicht schemagebundene Objekte zurückgegeben werden können, mithilfe von [Sys. dm_sql_referenced_entities](../../relational-databases/system-dynamic-management-views/sys-dm-sql-referenced-entities-transact-sql.md).  
  
-   DDL-Trigger auf Serverebene im Kontext der Masterdatenbank.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|referencing_id|**int**|ID der verweisenden Entität. Lässt keine NULL-Werte zu.|  
|referencing_minor_id|**int**|Die Spalten-ID, wenn es sich bei der verweisenden Entität um eine Spalte handelt. Andernfalls ist der Wert 0. Lässt keine NULL-Werte zu.|  
|referencing_class|**tinyint**|Klasse der verweisenden Entität.<br /><br /> 1 = Objekt oder Spalte<br /><br /> 12 = DDL-Trigger auf Datenbankebene<br /><br /> 13 = DDL-Trigger auf Serverebene<br /><br /> Lässt keine NULL-Werte zu.|  
|referencing_class_desc|**nvarchar(60)**|Klassenbeschreibung der verweisenden Entität.<br /><br /> OBJECT_OR_COLUMN<br /><br /> DATABASE_DDL_TRIGGER<br /><br /> SERVER_DDL_TRIGGER<br /><br /> Lässt keine NULL-Werte zu.|  
|is_schema_bound_reference|**bit**|1 = Entität, auf die verwiesen wird, ist schemagebunden.<br /><br /> 0 = Entität, auf die verwiesen wird, ist nicht schemagebunden.<br /><br /> Lässt keine NULL-Werte zu.|  
|referenced_class|**tinyint**|Klasse der Entität, auf die verwiesen wird.<br /><br /> 1 = Objekt oder Spalte<br /><br /> 6 = Typ<br /><br /> 10 = XML-Schemaauflistung<br /><br /> 21 = Partitionsfunktion<br /><br /> Lässt keine NULL-Werte zu.|  
|referenced_class_desc|**nvarchar(60)**|Klassenbeschreibung der Entität, auf die verwiesen wird.<br /><br /> OBJECT_OR_COLUMN<br /><br /> TYPE<br /><br /> XML_SCHEMA_COLLECTION<br /><br /> PARTITION_FUNCTION<br /><br /> Lässt keine NULL-Werte zu.|  
|referenced_server_name|**sysname**|Servername der Entität, auf die verwiesen wird.<br /><br /> Diese Spalte wird für serverübergreifende Abhängigkeiten aufgefüllt, die auf der Angabe eines gültigen vierteiligen Namens basieren. Informationen zu mehrteiligen Namen finden Sie unter [Transact-SQL-Syntaxkonventionen &#40; Transact-SQL &#41; ](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md).<br /><br /> NULL für nicht schemagebundene Entitäten, für die ohne Angabe eines vierteiligen Namens auf die Entität verwiesen wurde.<br /><br /> NULL für schemagebundene Entitäten, da sich müssen in derselben Datenbank und aus diesem Grund können nur definiert werden mithilfe ein zweiteiligen (*schema.object*) Namen.|  
|referenced_database_name|**sysname**|Datenbankname der Entität, auf die verwiesen wird.<br /><br /> Diese Spalte wird für datenbankübergreifende oder serverübergreifende Verweise aufgefüllt, die auf der Angabe eines gültigen dreiteiligen oder vierteiligen Namens basieren.<br /><br /> NULL für nicht schemagebundene Verweise, wenn auf Basis eines einteiligen oder zweiteiligen Namens angegeben.<br /><br /> NULL für schemagebundene Entitäten, da sich müssen in derselben Datenbank und aus diesem Grund können nur definiert werden mithilfe ein zweiteiligen (*schema.object*) Namen.|  
|referenced_schema_name|**sysname**|Schema, in das die Entität gehört, auf die verwiesen wird.<br /><br /> NULL für nicht schemagebundene Verweise, in denen ohne Angabe des Schemanamens auf die Entität verwiesen wird.<br /><br /> Niemals NULL für schemagebundene Verweise, da schemagebundene Entitäten mit einem zweiteiligen Namen definiert werden müssen und mit diesem zweiteiligen Namen auf sie verwiesen werden muss.|  
|referenced_entity_name|**sysname**|Name der Entität, auf die verwiesen wird. Lässt keine NULL-Werte zu.|  
|referenced_id|**int**|ID der Entität, auf die verwiesen wird. Der Wert dieser Spalte ist niemals NULL für schemagebundene Verweise. Der Wert dieser Spalte ist immer NULL für serverübergreifende und datenbankübergreifende Verweise.<br /><br /> NULL für Verweise innerhalb der Datenbank, wenn die ID nicht bestimmt werden kann. Für nicht schemagebundene Verweise kann die ID in den folgenden Fällen nicht aufgelöst werden:<br /><br /> Die Entität, auf die verwiesen wird, ist in der Datenbank nicht vorhanden.<br /><br /> Das Schema der Entität, auf die verwiesen wird, hängt vom Schema des Aufrufers ab und wird zur Laufzeit aufgelöst. In diesem Fall wird is_caller_dependent auf 1 festgelegt.|  
|referenced_minor_id|**int**|ID der Spalte, auf die verwiesen wird, wenn es sich bei der verweisenden Entität um eine Spalte handelt. Andernfalls ist der Wert 0. Lässt keine NULL-Werte zu.<br /><br /> Eine Entität, auf die verwiesen wird, ist eine Spalte, wenn diese in der verweisenden Entität namentlich identifiziert wird oder wenn die übergeordnete Entität in einer SELECT *-Anweisung verwendet wird.|  
|is_caller_dependent|**bit**|Gibt an, dass die Schemabindung für die Entität, auf die verwiesen wird, zur Laufzeit erfolgt. Deshalb hängt die Auflösung der Entitäts-ID vom Schema des Aufrufers ab. Dies ist der Fall, wenn es sich bei der Entität, auf die verwiesen wird, um eine gespeicherte Prozedur, eine erweiterte gespeicherte Prozedur oder um eine nicht schemagebundene benutzerdefinierte Funktion handelt, die in einer EXECUTE-Anweisung aufgerufen wird.<br /><br /> 1 = Die Entität, auf die verwiesen wird, hängt vom Aufrufer ab und wird zur Laufzeit aufgelöst. In diesem Fall ist referenced_id gleich NULL.<br /><br /> 0 = Die Entitäts-ID, auf die verwiesen wird, ist nicht aufruferabhängig.<br /><br /> Immer 0 für schemagebundene Verweise sowie für datenbankübergreifende und serverübergreifende Verweise, die explizit einen Schemanamen angeben. Zum Beispiel ist ein Verweis auf eine Entität im Format `EXEC MyDatabase.MySchema.MyProc` nicht aufruferabhängig. Ein Verweis im Format `EXEC MyDatabase..MyProc` ist jedoch aufruferabhängig.|  
|is_ambiguous|**bit**|Gibt an, der Verweis ist mehrdeutig und kann zur Laufzeit in eine benutzerdefinierte Funktion, einen benutzerdefinierten Typ (UDT) oder ein Xquery-Verweis auf eine Spalte vom Typ aufgelöst **Xml**.<br /><br /> Angenommen, die `SELECT Sales.GetOrder() FROM Sales.MySales`-Anweisung ist in einer gespeicherten Prozedur definiert. Bis zur Ausführung der gespeicherten Prozedur ist unbekannt, ob `Sales.GetOrder()` eine benutzerdefinierte Funktion im Schema `Sales` oder in der Spalte namens `Sales` vom Typ UDT mit einer Methode namens `GetOrder()` ist.<br /><br /> 1 = Verweis ist mehrdeutig.<br /><br /> 0 = Verweis ist eindeutig, oder die Entität kann beim Aufruf der Sicht erfolgreich gebunden werden.<br /><br /> 0 für das Schema wird immer Verweise gebunden.|  
  
## <a name="remarks"></a>Hinweise  
 In der folgenden Tabelle werden die Typen von Entitäten aufgelistet, für die Abhängigkeitsinformationen erstellt und verwaltet werden. Für Regeln, Standardwerte, temporäre Tabellen, temporär gespeicherte Prozeduren oder Systemobjekte werden keine Abhängigkeitsinformationen erstellt oder verwaltet.  
  
|Entitätstyp|Verweisende Entität|Entität, auf die verwiesen wird|  
|-----------------|------------------------|-----------------------|  
|Tabelle|Ja*|ja|  
|Sicht|ja|ja|  
|Gefilterter Index|Ja**|Nein|  
|Gefilterte Statistik|Ja**|Nein|  
|Gespeicherte [!INCLUDE[tsql](../../includes/tsql-md.md)]-Prozedur***|ja|ja|  
|Gespeicherte CLR-Prozedur|Nein|ja|  
|Benutzerdefinierte Funktion in [!INCLUDE[tsql](../../includes/tsql-md.md)]|ja|ja|  
|CLR-benutzerdefinierte Funktion|Nein|ja|  
|CLR-Trigger (DML und DDL)|Nein|Nein|  
|DML-Trigger in [!INCLUDE[tsql](../../includes/tsql-md.md)]|ja|Nein|  
|DDL-Trigger auf Datenbankebene in [!INCLUDE[tsql](../../includes/tsql-md.md)]|ja|Nein|  
|DDL-Trigger auf Serverebene in [!INCLUDE[tsql](../../includes/tsql-md.md)]|ja|Nein|  
|Erweiterte gespeicherte Prozeduren|Nein|ja|  
|Warteschlange|Nein|ja|  
|Synonym|Nein|ja|  
|Typ (Alias und CLR-benutzerdefinierter Typ)|Nein|ja|  
|XML-Schemaauflistung|Nein|ja|  
|Partitionsfunktion|Nein|ja|  
  
 \*Eine Tabelle als verweisende Entität nachverfolgt wird, nur, wenn er verweist auf eine [!INCLUDE[tsql](../../includes/tsql-md.md)] -Modul, einen benutzerdefinierten Typ oder XML-schemaauflistung in der Definition eines berechnete Spalte, einer CHECK-Einschränkung oder einer DEFAULT-Einschränkung.  
  
 ** Jede im Filterprädikat verwendete Spalte wird als verweisende Entität aufgezeichnet.  
  
 *** Nummerierte gespeicherte Prozeduren mit einem ganzzahligen Wert größer 1 werden weder als verweisende Entität noch als Entität, auf die verwiesen wird, aufgezeichnet.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die VIEW DEFINITION-Berechtigung für die Datenbank und die SELECT-Berechtigung für sys.sql_expression_dependencies für die Datenbank. Standardmäßig wird die SELECT-Berechtigung nur Mitgliedern der festen Datenbankrolle db_owner gewährt. Wenn einem anderen Benutzer die SELECT-Berechtigung und die VIEW DEFINITION-Berechtigung erteilt werden, kann dieser Berechtigte alle Abhängigkeiten in der Datenbank anzeigen.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-returning-entities-that-are-referenced-by-another-entity"></a>A. Zurückgeben von Entitäten, auf die von einer anderen Entität verwiesen wird  
 Im folgenden Beispiel werden die Tabellen und Spalten zurückgegeben, auf die in der Sicht `Production.vProductAndDescription` verwiesen wird. Die Sicht hängt von den Entitäten (Tabellen und Spalten) ab, die in den Spalten `referenced_entity_name` und `referenced_column_name` zurückgegeben werden.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT OBJECT_NAME(referencing_id) AS referencing_entity_name,   
    o.type_desc AS referencing_desciption,   
    COALESCE(COL_NAME(referencing_id, referencing_minor_id), '(n/a)') AS referencing_minor_id,   
    referencing_class_desc,  
    referenced_server_name, referenced_database_name, referenced_schema_name,  
    referenced_entity_name,   
    COALESCE(COL_NAME(referenced_id, referenced_minor_id), '(n/a)') AS referenced_column_name,  
    is_caller_dependent, is_ambiguous  
FROM sys.sql_expression_dependencies AS sed  
INNER JOIN sys.objects AS o ON sed.referencing_id = o.object_id  
WHERE referencing_id = OBJECT_ID(N'Production.vProductAndDescription');  
GO  
  
```  
  
### <a name="b-returning-entities-that-reference-another-entity"></a>B. Zurückgeben von Entitäten, die auf eine andere Entität verweisen  
 Im folgenden Beispiel werden die Entitäten zurückgegeben, die auf die Tabelle `Production.Product` verweisen. Die in der `referencing_entity_name`-Spalte zurückgegebenen Entitäten hängen von der `Product`-Tabelle ab.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT OBJECT_SCHEMA_NAME ( referencing_id ) AS referencing_schema_name,  
    OBJECT_NAME(referencing_id) AS referencing_entity_name,   
    o.type_desc AS referencing_desciption,   
    COALESCE(COL_NAME(referencing_id, referencing_minor_id), '(n/a)') AS referencing_minor_id,   
    referencing_class_desc, referenced_class_desc,  
    referenced_server_name, referenced_database_name, referenced_schema_name,  
    referenced_entity_name,   
    COALESCE(COL_NAME(referenced_id, referenced_minor_id), '(n/a)') AS referenced_column_name,  
    is_caller_dependent, is_ambiguous  
FROM sys.sql_expression_dependencies AS sed  
INNER JOIN sys.objects AS o ON sed.referencing_id = o.object_id  
WHERE referenced_id = OBJECT_ID(N'Production.Product');  
GO  
  
```  
  
### <a name="c-returning-cross-database-dependencies"></a>C. Zurückgeben von datenbankübergreifenden Abhängigkeiten  
 Im folgenden Beispiel werden alle datenbankübergreifenden Abhängigkeiten zurückgegeben. Im Beispiel werden zuerst die Datenbank `db1` sowie zwei gespeicherte Prozeduren erstellt, die auf Tabellen in den Datenbanken `db2` und `db3` verweisen. Die `sys.sql_expression_dependencies`-Tabelle wird dann abgefragt, um die datenbankübergreifenden Abhängigkeiten zwischen den Prozeduren und den Tabellen zu berichten. Beachten Sie, dass für die Entität `referenced_schema_name`, auf die verwiesen wird, in der Spalte `t3` NULL zurückgegeben wird, weil in der Definition der Prozedur kein Schemaname für diese Entität angegeben wurde.  
  
```  
CREATE DATABASE db1;  
GO  
USE db1;  
GO  
CREATE PROCEDURE p1 AS SELECT * FROM db2.s1.t1;  
GO  
CREATE PROCEDURE p2 AS  
    UPDATE db3..t3  
    SET c1 = c1 + 1;  
GO  
SELECT OBJECT_NAME (referencing_id),referenced_database_name,   
    referenced_schema_name, referenced_entity_name  
FROM sys.sql_expression_dependencies  
WHERE referenced_database_name IS NOT NULL;  
GO  
USE master;  
GO  
DROP DATABASE db1;  
GO  
  
```  
  
## <a name="see-also"></a>Siehe auch  
 [sys.dm_sql_referenced_entities &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-sql-referenced-entities-transact-sql.md)   
 [sys.dm_sql_referencing_entities &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-sql-referencing-entities-transact-sql.md)  
  
  

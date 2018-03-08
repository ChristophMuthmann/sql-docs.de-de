---
title: sys.dm_sql_referencing_entities (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.dm_sql_referencing_entities
- dm_sql_referencing_entities_TSQL
- sys.dm_sql_referencing_entities_TSQL
- dm_sql_referencing_entities
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_sql_referencing_entities dynamic management function
ms.assetid: c16f8f0a-483f-4feb-842e-da90426045ae
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 35e2f1be36365c2b1f5c8801a9e0d7749c70de7d
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/03/2018
---
# <a name="sysdmsqlreferencingentities-transact-sql"></a>sys.dm_sql_referencing_entities (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Gibt eine Zeile für jede Entität in der aktuellen Datenbank zurück, die anhand des Namens auf eine andere benutzerdefinierte Entität verweist. Eine Abhängigkeit zwischen zwei Entitäten wird erstellt, wenn eine Entität, die *Entität verwiesen*, angezeigt wird, namentlich in einem persistenten SQL-Ausdruck, der einer anderen Entität, die mit dem Namen der *verweisende Entität*. Wird z. B. ein benutzerdefinierter Typ (User-Defined Type; UDT) als Entität angegeben, auf die verwiesen wird, gibt diese Funktion jede benutzerdefinierte Entität zurück, die anhand des Namens in der zugehörigen Definition auf diesen Typ verweist. Die Funktion gibt keine Entitäten in anderen Datenbanken zurück, die möglicherweise auf die angegebene Entität verweisen. Diese Funktion muss zusammen mit der master-Datenbank ausgeführt werden, um einen DDL-Trigger auf Serverebene als verweisende Entität zurückzugeben.  
  
 Verwenden Sie diese dynamische Verwaltungsfunktion, um zu folgenden Entitätstypen in der aktuellen Datenbank, die auf die angegebene Entität verweisen, einen Bericht zu erstellen:  
  
-   Schemagebundene oder nicht schemagebundene Entitäten  
  
-   DDL-Trigger auf Datenbankebene  
  
-   DDL-Trigger auf Serverebene  
  
**Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]), [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
sys.dm_sql_referencing_entities (  
    ' schema_name.referenced_entity_name ' , ' <referenced_class> ' )  
  
<referenced_class> ::=  
{  
    OBJECT  
  | TYPE  
  | XML_SCHEMA_COLLECTION  
  | PARTITION_FUNCTION  
}  
```  
  
## <a name="arguments"></a>Argumente  
 *schema_name.referenced*_*entity_name*  
 Der Name der Entität, auf die verwiesen wird.  
  
 *Schema_name* außer erforderlich, wenn die referenzierte Klasse PARTITION_FUNCTION ist.  
  
 *schema_name.referenced_entity_name* ist **nvarchar(517)**.  
  
 *< Referenced_class >* :: = {OBJECT | TYP | XML_SCHEMA_COLLECTION | UM PARTITION_FUNCTION}  
 Die Klasse der Entität, auf die verwiesen wird. Pro Anweisung kann nur eine Klasse angegeben werden.  
  
 *< Referenced_class >* ist **Nvarchar**(60).  
  
## <a name="table-returned"></a>Zurückgegebene Tabelle  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|referencing_schema_name|**sysname**|Schema, in das die verweisende Entität gehört. Lässt NULL-Werte zu.<br /><br /> NULL für DDL-Trigger auf Datenbankebene und Serverebene.|  
|referencing_entity_name|**sysname**|Name der verweisenden Entität. Lässt keine NULL-Werte zu.|  
|referencing_id|**int**|ID der verweisenden Entität. Lässt keine NULL-Werte zu.|  
|referencing_class|**tinyint**|Klasse der verweisenden Entität. Lässt keine NULL-Werte zu.<br /><br /> 1 = Objekt<br /><br /> 12 = Datenbankebene DDL-Trigger<br /><br /> 13 = Serverebene DDL-Trigger|  
|referencing_class_desc|**nvarchar(60)**|Klassenbeschreibung der verweisenden Entität.<br /><br /> OBJECT<br /><br /> DATABASE_DDL_TRIGGER<br /><br /> SERVER_DDL_TRIGGER|  
|is_caller_dependent|**bit**|Gibt an, dass die Auflösung der Entität, auf die verwiesen wird, zur Laufzeit erfolgt, weil sie vom Schema des Aufrufers abhängt.<br /><br /> 1 = Die verweisende Entität kann zwar auf die Entität verweisen, doch die Auflösung der ID der Entität, auf die verwiesen wird, hängt vom Aufrufer ab und kann nicht bestimmt werden. Dies gilt nur für nicht schemagebundene Verweise auf eine gespeicherte Prozedur, eine erweiterte gespeicherte Prozedur oder eine benutzerdefinierte Funktion, die in einer EXECUTE-Anweisung aufgerufen wird.<br /><br /> 0 = Die Entität, auf die verwiesen wird, ist kein aufruferabhängiges Element.|  
  
## <a name="exceptions"></a>Ausnahmen  
 Gibt unter den folgenden Bedingungen ein leeres Resultset zurück:  
  
-   Ein Systemobjekt wird angegeben.  
  
-   Die angegebene Entität ist in der Datenbank nicht vorhanden.  
  
-   Die angegebene Entität verweist auf keine Entitäten.  
  
-   Ein ungültiger Parameter wird übergeben.  
  
 Gibt einen Fehler zurück, wenn die angegebene Entität, auf die verwiesen wird, eine nummerierte gespeicherte Prozedur ist.  
  
## <a name="remarks"></a>Hinweise  
 In der folgenden Tabelle werden die Typen von Entitäten aufgelistet, für die Abhängigkeitsinformationen erstellt und verwaltet werden. Für Regeln, Standardwerte, temporäre Tabellen, temporär gespeicherte Prozeduren oder Systemobjekte werden keine Abhängigkeitsinformationen erstellt oder verwaltet.  
  
|Entitätstyp|Verweisende Entität|Entität, auf die verwiesen wird|  
|-----------------|------------------------|-----------------------|  
|Tabelle|Ja*|ja|  
|Sicht|ja|ja|  
|[!INCLUDE[tsql](../../includes/tsql-md.md)] gespeicherte Prozedur **|ja|ja|  
|Gespeicherte CLR-Prozedur|nein|ja|  
|[!INCLUDE[tsql](../../includes/tsql-md.md)] Benutzerdefinierte Funktion (user-defined function)|ja|ja|  
|CLR-benutzerdefinierte Funktion|nein|ja|  
|CLR-Trigger (DML und DDL)|nein|nein|  
|[!INCLUDE[tsql](../../includes/tsql-md.md)] DML-Trigger|ja|nein|  
|[!INCLUDE[tsql](../../includes/tsql-md.md)] DDL-Trigger auf Datenbankebene|ja|nein|  
|[!INCLUDE[tsql](../../includes/tsql-md.md)] DDL-Trigger auf Serverebene|ja|nein|  
|Erweiterte gespeicherte Prozeduren|nein|ja|  
|Warteschlange|nein|ja|  
|Synonym|nein|ja|  
|Typ (Alias und CLR-benutzerdefinierter Typ)|nein|ja|  
|XML-Schemaauflistung|nein|ja|  
|Partitionsfunktion|nein|ja|  
  
 \*Eine Tabelle als verweisende Entität nachverfolgt wird, nur, wenn er verweist auf eine [!INCLUDE[tsql](../../includes/tsql-md.md)] -Modul, einen benutzerdefinierten Typ oder XML-schemaauflistung in der Definition eines berechnete Spalte, einer CHECK-Einschränkung oder einer DEFAULT-Einschränkung.  
  
 ** Nummerierte gespeicherte Prozeduren mit einem ganzzahligen Wert größer als 1 werden weder als verweisende Entität noch als Entität, auf die verwiesen wird, aufgezeichnet.  
  
## <a name="permissions"></a>Berechtigungen  
  
### <a name="includesskatmaiincludessskatmai-mdmd--includesssql11includessssql11-mdmd"></a>[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] – [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]  
  
-   Erfordert die CONTROL-Berechtigung für das Objekt, auf das verwiesen wird. Wenn es sich bei der Entität, auf die verwiesen wird, um eine Partitionsfunktion handelt, ist die CONTROL-Berechtigung für die Datenbank erforderlich.  
  
-   Erfordert SELECT-Berechtigung für Sys. dm_sql_referencing_entities. Standardmäßig wird die SELECT-Berechtigung der public-Rolle erteilt.  
  
### <a name="includesssql14includessssql14-mdmd---includesscurrentincludessscurrent-mdmd"></a>[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] - [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]  
  
-   Erfordert keine Berechtigungen für das Objekt, auf das verwiesen wird. Teilergebnisse können zurückgegeben werden, wenn der Benutzer über die VIEW DEFINITION-Berechtigung auf nur einigen der verweisenden Entitäten verfügt.  
  
-   Erfordert die VIEW DEFINITION-Berechtigung für das Objekt, wenn es sich bei der verweisenden Entität um ein Objekt handelt.  
  
-   Erfordert die VIEW DEFINITION-Berechtigung für die Datenbank, wenn es sich bei der verweisenden Entität um einen DDL-Trigger auf Datenbankebene handelt.  
  
-   Erfordert die VIEW ANY DEFINITION-Berechtigung für den Server, wenn es sich bei der verweisenden Entität um einen DDL-Trigger auf Serverebene handelt.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-returning-the-entities-that-refer-to-a-given-entity"></a>A. Zurückgeben der Entitäten, die auf eine bestimmte Entität verweisen  
 Im folgenden Beispiel werden die Entitäten in der aktuellen Datenbank zurückgegeben, die auf die angegebene Tabelle verweisen.  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT referencing_schema_name, referencing_entity_name, referencing_id, referencing_class_desc, is_caller_dependent  
FROM sys.dm_sql_referencing_entities ('Production.Product', 'OBJECT');  
GO  
```  
  
### <a name="b-returning-the-entities-that-refer-to-a-given-type"></a>B. Zurückgeben der Entitäten, die auf einen bestimmten Typ verweisen  
 Im folgenden Beispiel werden die Entitäten zurückgegeben, die auf den Aliastyp `dbo.Flag` verweisen. Das Resultset zeigt an, dass zwei gespeicherte Prozeduren diesen Typ verwenden. Die `dbo.Flag` Typ wird auch verwendet, in der Definition mehrerer Spalten in der `HumanResources.Employee` Tabelle ist jedoch, da der Typ nicht in der Definition einer berechneten Spalte, einer CHECK-Einschränkung oder einer DEFAULT-Einschränkung in der Tabelle vorhanden ist, werden keine Zeilen zurückgegeben für die `HumanResources.Employee`Tabelle.  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT referencing_schema_name, referencing_entity_name, referencing_id, referencing_class_desc, is_caller_dependent  
FROM sys.dm_sql_referencing_entities ('dbo.Flag', 'TYPE');  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 referencing_schema_name referencing_entity_name   referencing_id referencing_class_desc is_caller_dependent  
 ----------------------- -------------------------  ------------- ---------------------- -------------------  
 HumanResources          uspUpdateEmployeeHireInfo  1803153469    OBJECT_OR_COLUMN       0  
 HumanResources          uspUpdateEmployeeLogin     1819153526    OBJECT_OR_COLUMN       0  
 (2 row(s) affected)`  
 ``` 
 
## <a name="see-also"></a>Siehe auch  
 [sys.dm_sql_referenced_entities &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-sql-referenced-entities-transact-sql.md)   
 [sys.sql_expression_dependencies &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md)  
  
  

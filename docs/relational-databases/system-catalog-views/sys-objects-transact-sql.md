---
title: Sys.Objects (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 0/30/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.objects_TSQL
- objects
- sys.objects
- objects_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.objects catalog view
- table-valued parameters, sys.objects catalog view
- user-defined table types [SQL Server]
- table types [SQL Server]
ms.assetid: f8d6163a-2474-410c-a794-997639f31b3b
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 99d4a8338f389fcabbff4a7ffa5bcb594a9149c7
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="sysobjects-transact-sql"></a>sys.objects (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Enthält eine Zeile für jedes benutzerdefinierte, mit Schemabereich-Objekt, das innerhalb einer Datenbank, einschließlich systemintern skalare benutzerdefinierte Funktion erstellt wird.  
  
 Weitere Informationen finden Sie unter [Skalarfunktionen für In-Memory OLTP](../../relational-databases/in-memory-oltp/scalar-user-defined-functions-for-in-memory-oltp.md).  
  
> [!NOTE]  
>  sys.objects zeigt keine DDL-Trigger an, da diese keine Schemabereiche besitzen. Alle Trigger, sowohl DML-als auch DDL-Trigger finden Sie im [sys.triggers](../../relational-databases/system-catalog-views/sys-triggers-transact-sql.md). Sys.Triggers unterstützt eine Mischung von namensbereichsregeln für die verschiedenen Arten von Triggern.  
  
|Spaltenname|Datentyp|Beschreibung|  
|-----------------|---------------|-----------------|  
|name|**sysname**|Objektname.|  
|object_id|**int**|Objekt-ID. Ist innerhalb einer Datenbank eindeutig.|  
|principal_id|**int**|ID des einzelnen Besitzers, sofern es sich bei diesem nicht um den Schemabesitzer handelt. Standardmäßig gehören Objekte mit Schemabereich dem Schemabesitzer. Mit der ALTER AUTHORIZATION-Anweisung kann jedoch ein anderer Besitzer angegeben werden.<br /><br /> Ist NULL, wenn kein alternativer einzelner Besitzer vorhanden ist.<br /><br /> Ist NULL, wenn der Objekttyp einen der folgenden Werte aufweist:<br /><br /> C = CHECK-Einschränkung<br /><br /> D = DEFAULT (Einschränkung oder eigenständig)<br /><br /> F = FOREIGN KEY-Einschränkung<br /><br /> PK = PRIMARY KEY-Einschränkung<br /><br /> R = Regel (vom alten Typ, eigenständig)<br /><br /> TA = Assemblytrigger (CLR-Integration)<br /><br /> TR = SQL-Trigger<br /><br /> UQ = UNIQUE-Einschränkung|  
|schema_id|**int**|Die ID des Schemas, in dem das Objekt enthalten ist.<br /><br /> Systemobjekte mit Schemabereich sind immer in den sys-Schemas oder INFORMATION_SCHEMA-Schemas enthalten.|  
|parent_object_id|**int**|ID des Objekts, zu dem dieses Objekt gehört.<br /><br /> 0 = Kein untergeordnetes Objekt.|  
|Typ|**char(2)**|Objekttyp:<br /><br /> AF = Aggregatfunktion (CLR)<br /><br /> C = CHECK-Einschränkung<br /><br /> D = DEFAULT (Einschränkung oder eigenständig)<br /><br /> F = FOREIGN KEY-Einschränkung<br /><br /> FN = SQL-Skalarfunktion<br /><br /> FS = Assemblyskalarfunktion (CLR)<br /><br /> FT = Assembly-Tabellenwertfunktion (CLR)<br /><br /> IF = SQL-Inlinefunktion mit Tabellenrückgabe<br /><br /> IT = Interne Tabelle<br /><br /> P = Gespeicherte SQL-Prozedur<br /><br /> PC = Gespeicherte Assemblyprozedur (CLR)<br /><br /> PG = Planhinweisliste<br /><br /> PK = PRIMARY KEY-Einschränkung<br /><br /> R = Regel (vom alten Typ, eigenständig)<br /><br /> RF = Replikationsfilterprozedur<br /><br /> S = Systembasistabelle<br /><br /> SN = Synonym<br /><br /> SO = Sequenzobjekt<br /><br /> U = Tabelle (benutzerdefiniert)<br /><br /> V = Sicht<br /><br /> <br /><br /> **Gilt für**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> <br /><br /> SQ = Dienstwarteschlange<br /><br /> TA = Assembly-DML-Trigger (CLR)<br /><br /> TF = Tabellenwertfunktion von SQL<br /><br /> TR = SQL-DML-Trigger<br /><br /> TT = Tabellentyp<br /><br /> UQ = UNIQUE-Einschränkung<br /><br /> X = Erweiterte gespeicherte Prozedur<br /><br /> <br /><br /> **Gilt für**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)], [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)].<br /><br /> <br /><br /> ET = externe Tabelle|  
|type_desc|**nvarchar(60)**|Beschreibung des Objekttyps:<br /><br /> AGGREGATE_FUNCTION<br /><br /> CHECK_CONSTRAINT<br /><br /> CLR_SCALAR_FUNCTION<br /><br /> CLR_STORED_PROCEDURE<br /><br /> CLR_TABLE_VALUED_FUNCTION<br /><br /> CLR_TRIGGER<br /><br /> DEFAULT_CONSTRAINT<br /><br /> EXTENDED_STORED_PROCEDURE<br /><br /> FOREIGN_KEY_CONSTRAINT<br /><br /> INTERNAL_TABLE<br /><br /> PLAN_GUIDE<br /><br /> PRIMARY_KEY_CONSTRAINT<br /><br /> REPLICATION_FILTER_PROCEDURE<br /><br /> RULE<br /><br /> SEQUENCE_OBJECT<br /><br /> <br /><br /> **Gilt für**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> <br /><br /> SERVICE_QUEUE<br /><br /> SQL_INLINE_TABLE_VALUED_FUNCTION<br /><br /> SQL_SCALAR_FUNCTION<br /><br /> SQL_STORED_PROCEDURE<br /><br /> SQL_TABLE_VALUED_FUNCTION<br /><br /> SQL_TRIGGER<br /><br /> SYNONYM<br /><br /> SYSTEM_TABLE<br /><br /> TABLE_TYPE<br /><br /> UNIQUE_CONSTRAINT<br /><br /> USER_TABLE<br /><br /> VIEW|  
|create_date|**datetime**|Datum, an dem das Objekt erstellt wurde.|  
|modify_date|**datetime**|Das Datum, an dem das Objekt zuletzt mithilfe einer ALTER-Anweisung geändert wurde. Ist das Objekt eine Tabelle oder Sicht, wird modify_date auch geändert, wenn ein gruppierter Index für die Tabelle oder Sicht erstellt oder geändert wird.|  
|is_ms_shipped|**bit**|Das Objekt wird von einer internen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Komponente erstellt.|  
|is_published|**bit**|Objekt wurde veröffentlicht.|  
|is_schema_published|**bit**|Nur das Schema des Objekts wird veröffentlicht.|  
  
## <a name="remarks"></a>Hinweise  
 Sie können Anwenden der [OBJECT_ID](../../t-sql/functions/object-id-transact-sql.md), [OBJECT_NAME](../../t-sql/functions/object-name-transact-sql.md), und [OBJECTPROPERTY](../../t-sql/functions/objectproperty-transact-sql.md)integrierte Funktionen (), um die in sys.objects angezeigten Objekte.  
  
 Es ist eine Version dieser Sicht mit dem gleichen Schema, namens [system_objects](../../relational-databases/system-catalog-views/sys-system-objects-transact-sql.md), Systemobjekte angezeigt. Es wird eine andere Sicht mit dem Namen [all_objects](../../relational-databases/system-catalog-views/sys-all-objects-transact-sql.md) , System- und Benutzerobjekte anzeigt. Alle drei Katalogsichten weisen die gleiche Struktur auf.  
  
 In dieser Version von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] wird ein erweiterter Index, beispielsweise ein XML-Index oder Räumlichkeitsindex, als interne Tabelle in sys.objects (type = IT and type_desc = INTERNAL_TABLE) betrachtet. Für einen erweiterten Index gilt:  
  
-   name ist der interne Name der Indextabelle.  
  
-   parent_object_id ist der object_id-Wert der Basistabelle.  
  
-   Die Spalten is_ms_shipped, is_published und is_schema_published werden auf 0 festgelegt.  

**Verwandte nützlich Systemsichten**  
Teilmengen der Objekte können mithilfe von Systemsichten für einen bestimmten Typ des Objekts, z. B. angezeigt werden:  
- [sys.tables](sys-tables-transact-sql.md)  
- [sys.views](sys-views-transact-sql.md)  
- [sys.procedures](sys-procedures-transact-sql.md)  
  
## <a name="permissions"></a>Berechtigungen  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Weitere Informationen finden Sie unter [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-returning-all-the-objects-that-have-been-modified-in-the-last-n-days"></a>A. Zurückgeben aller Objekte, die in den letzten N Tagen geändert wurden  
 Vor dem Ausführen der folgenden Abfrage ersetzen Sie `<database_name>` und `<n_days>` durch gültige Werte.  
  
```sql  
USE <database_name>;  
GO  
SELECT name AS object_name   
  ,SCHEMA_NAME(schema_id) AS schema_name  
  ,type_desc  
  ,create_date  
  ,modify_date  
FROM sys.objects  
WHERE modify_date > GETDATE() - <n_days>  
ORDER BY modify_date;  
GO  
```  
  
### <a name="b-returning-the-parameters-for-a-specified-stored-procedure-or-function"></a>B. Zurückgeben der Parameter für eine angegebene gespeicherte Prozedur oder Funktion  
 Ersetzen Sie vor dem Ausführen der folgenden Abfrage `<database_name>` und `<schema_name.object_name>` durch gültige Namen.  
  
```sql  
USE <database_name>;  
GO  
SELECT SCHEMA_NAME(schema_id) AS schema_name  
    ,o.name AS object_name  
    ,o.type_desc  
    ,p.parameter_id  
    ,p.name AS parameter_name  
    ,TYPE_NAME(p.user_type_id) AS parameter_type  
    ,p.max_length  
    ,p.precision  
    ,p.scale  
    ,p.is_output  
FROM sys.objects AS o  
INNER JOIN sys.parameters AS p ON o.object_id = p.object_id  
WHERE o.object_id = OBJECT_ID('<schema_name.object_name>')  
ORDER BY schema_name, object_name, p.parameter_id;  
GO  
```  
  
### <a name="c-returning-all-the-user-defined-functions-in-a-database"></a>C. Zurückgeben aller benutzerdefinierten Funktionen in einer Datenbank  
 Vor dem Ausführen der folgenden Abfrage ersetzen Sie `<database_name>` durch einen gültigen Datenbanknamen.  
  
```sql  
USE <database_name>;  
GO  
SELECT name AS function_name   
  ,SCHEMA_NAME(schema_id) AS schema_name  
  ,type_desc  
  ,create_date  
  ,modify_date  
FROM sys.objects  
WHERE type_desc LIKE '%FUNCTION%';  
GO  
```  
  
### <a name="d-returning-the-owner-of-each-object-in-a-schema"></a>D. Zurückgeben des Besitzers jedes Objekts in einem Schema  
 Vor dem Ausführen der folgenden Abfrage ersetzen Sie alle Vorkommen von `<database_name>` und `<schema_name>` durch gültige Namen.  
  
```sql  
USE <database_name>;  
GO  
SELECT 'OBJECT' AS entity_type  
    ,USER_NAME(OBJECTPROPERTY(object_id, 'OwnerId')) AS owner_name  
    ,name   
FROM sys.objects WHERE SCHEMA_NAME(schema_id) = '<schema_name>'  
UNION   
SELECT 'TYPE' AS entity_type  
    ,USER_NAME(TYPEPROPERTY(SCHEMA_NAME(schema_id) + '.' + name, 'OwnerId')) AS owner_name  
    ,name   
FROM sys.types WHERE SCHEMA_NAME(schema_id) = '<schema_name>'   
UNION  
SELECT 'XML SCHEMA COLLECTION' AS entity_type   
    ,COALESCE(USER_NAME(xsc.principal_id),USER_NAME(s.principal_id)) AS owner_name  
    ,xsc.name   
FROM sys.xml_schema_collections AS xsc JOIN sys.schemas AS s  
    ON s.schema_id = xsc.schema_id  
WHERE s.name = '<schema_name>';  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Katalogsichten &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Sys. all_objects &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-all-objects-transact-sql.md)   
 [Sys. system_objects &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-system-objects-transact-sql.md)   
 [sys.triggers &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-triggers-transact-sql.md)   
 [Katalogsichten für Objekte &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [Abfragen von SQL Server-Systemkatalogs – häufig gestellte Fragen](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)   
 [Sys. internal_tables &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-internal-tables-transact-sql.md)  
  
  

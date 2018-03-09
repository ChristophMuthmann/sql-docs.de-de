---
title: Sys. all_objects (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
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
- sys.all_objects
- all_objects_TSQL
- all_objects
- sys.all_objects_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.all_objects catalog view
ms.assetid: 547e4be4-a8e4-48ce-9d8d-37b169985081
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: fd8082ebb9b69aec413209096775d0d3c565f837
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="sysallobjects-transact-sql"></a>sys.all_objects (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Zeigt UNION für alle benutzerdefinierten Objekte und Systemobjekte mit Schemabereich an.  
  
|Spaltenname|Datentyp|Beschreibung|  
|-----------------|---------------|-----------------|  
|name|**sysname**|Objektname.|  
|object_id|**int**|Objekt-ID. Ist innerhalb einer Datenbank eindeutig.|  
|principal_id|**int**|ID des einzelnen Besitzers, falls dieser nicht mit dem Schemabesitzer identisch ist. Standardmäßig gehören Objekte mit Schemabereich dem Schemabesitzer. Es kann jedoch ein anderer Besitzer mithilfe der ALTER AUTHORIZATION-Anweisung angegeben werden, wenn der Besitzer geändert werden soll.<br /><br /> Ist NULL, wenn kein anderer einzelner Besitzer vorhanden ist.<br /><br /> Ist NULL, wenn der Objekttyp einen der folgenden Werte aufweist:<br /><br /> C = CHECK-Einschränkung<br /><br /> D = DEFAULT (Einschränkung oder eigenständig)<br /><br /> F = FOREIGN KEY-Einschränkung<br /><br /> PK = PRIMARY KEY-Einschränkung<br /><br /> R = Regel (vom alten Typ, eigenständig)<br /><br /> TA = Assembly (CLR) Trigger<br /><br /> TR = SQL-Trigger<br /><br /> UQ = UNIQUE-Einschränkung|  
|schema_id|**int**|ID des Schemas, das das Objekt enthält.<br /><br /> Bei allen Systemobjekten mit Schemabereich in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ist dieser Wert immer in (schema_id('sys'), schema_id('INFORMATION_SCHEMA')) enthalten.|  
|parent_object_id|**int**|ID des Objekts, zu dem dieses Objekt gehört.<br /><br /> 0 = Kein untergeordnetes Objekt.|  
|Typ|**char(2)**|Objekttyp:<br /><br /> AF = Aggregatfunktion (CLR)<br /><br /> C = CHECK-Einschränkung<br /><br /> D = DEFAULT (Einschränkung oder eigenständig)<br /><br /> F = FOREIGN KEY-Einschränkung<br /><br /> FN = SQL-Skalarfunktion<br /><br /> FS = Assemblyskalarfunktion (CLR)<br /><br /> FT = Assembly-Tabellenwertfunktion (CLR)<br /><br /> IF = SQL-Inlinefunktion mit Tabellenrückgabe<br /><br /> IT = Interne Tabelle<br /><br /> P = Gespeicherte SQL-Prozedur<br /><br /> PC = Gespeicherte Assemblyprozedur (CLR)<br /><br /> PG = Planhinweisliste<br /><br /> PK = PRIMARY KEY-Einschränkung<br /><br /> R = Regel (vom alten Typ, eigenständig)<br /><br /> RF = Replikationsfilterprozedur<br /><br /> S = Systembasistabelle<br /><br /> SN = Synonym<br /><br /> SQ = Dienstwarteschlange<br /><br /> TA = Assembly-DML-Trigger (CLR)<br /><br /> TF = Tabellenwertfunktion von SQL<br /><br /> TR = SQL-DML-Trigger<br /><br /> TT = Tabellentyp<br /><br /> U = Tabelle (benutzerdefiniert)<br /><br /> UQ = UNIQUE-Einschränkung<br /><br /> V = Sicht<br /><br /> X = Erweiterte gespeicherte Prozedur|  
|type_desc|**nvarchar(60)**|Beschreibung des Objekttyps. AGGREGATE_FUNCTION<br /><br /> CHECK_CONSTRAINT<br /><br /> DEFAULT_CONSTRAINT<br /><br /> FOREIGN_KEY_CONSTRAINT<br /><br /> SQL_SCALAR_FUNCTION<br /><br /> CLR_SCALAR_FUNCTION<br /><br /> CLR_TABLE_VALUED_FUNCTION<br /><br /> SQL_INLINE_TABLE_VALUED_FUNCTION<br /><br /> INTERNAL_TABLE<br /><br /> SQL_STORED_PROCEDURE<br /><br /> CLR_STORED_PROCEDURE<br /><br /> PLAN_GUIDE<br /><br /> PRIMARY_KEY_CONSTRAINT<br /><br /> RULE<br /><br /> REPLICATION_FILTER_PROCEDURE<br /><br /> SYSTEM_TABLE<br /><br /> SYNONYM<br /><br /> SERVICE_QUEUE<br /><br /> CLR_TRIGGER<br /><br /> SQL_TABLE_VALUED_FUNCTION<br /><br /> SQL_TRIGGER<br /><br /> TABLE_TYPE<br /><br /> USER_TABLE<br /><br /> UNIQUE_CONSTRAINT<br /><br /> VIEW<br /><br /> EXTENDED_STORED_PROCEDURE|  
|create_date|**datetime**|Datum, an dem das Objekt erstellt wurde.|  
|modify_date|**datetime**|Das Datum, an dem das Objekt zuletzt mithilfe einer ALTER-Anweisung geändert wurde. Handelt es sich bei dem Objekt um eine Tabelle oder Sicht, wird modify_date auch geändert, wenn ein gruppierter Index in der Tabelle oder Sicht erstellt oder geändert wird.|  
|is_ms_shipped|**bit**|Erstellt eine interne Objekt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Komponente.|  
|is_published|**bit**|Objekt wurde veröffentlicht.|  
|is_schema_published|**bit**|Nur das Schema des Objekts wird veröffentlicht.|  
  
## <a name="permissions"></a>Berechtigungen  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Weitere Informationen finden Sie unter [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Katalogsichten für Objekte &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [Katalogsichten &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Sys.Objects &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [Sys. system_objects &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-system-objects-transact-sql.md)  
  
  

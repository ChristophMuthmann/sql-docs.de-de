---
title: OBJECT_SCHEMA_NAME (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- OBJECT_SCHEMA_NAME
- OBJECT_SCHEMA_NAME_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- objects [SQL Server], names
- schemas [SQL Server], names
- displaying schema names
- database objects [SQL Server], names
- OBJECT_SCHEMA_NAME function
ms.assetid: 5ba90bb9-d045-4164-963e-e9e96c0b1e8b
caps.latest.revision: 11
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 621a58fcc00b95626f3e4eb7d34d79af608436fe
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="objectschemaname-transact-sql"></a>OBJECT_SCHEMA_NAME (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Gibt den Namen des Datenbankschemas für schemabezogene Objekte zurück. Eine Liste der Objekte mit Schemabereich, finden Sie unter [sys.objects &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md).  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
OBJECT_SCHEMA_NAME ( object_id [, database_id ] )  
```  
  
## <a name="arguments"></a>Argumente  
 *object_id*  
 Die ID des zu verwendenden Objekts. *Object_id* ist **Int** und wird davon ausgegangen, dass ein Objekt mit Schemabereich in der angegebenen Datenbank oder im Kontext aktuellen Datenbank.  
  
 *database_id*  
 Die ID der Datenbank, in der das Objekt gesucht werden soll. *Database_id* ist **Int**.  
  
## <a name="return-types"></a>Rückgabetypen  
 **sysname**  
  
## <a name="exceptions"></a>Ausnahmen  
 Gibt NULL bei einem Fehler zurück oder wenn ein Aufrufer nicht über Berechtigungen zum Anzeigen des Objekts verfügt. Wenn für die Zieldatenbank AUTO_CLOSE auf ON festgelegt wurde, wird die Datenbank mithilfe der Funktion geöffnet.  
  
 Ein Benutzer kann nur die Metadaten sicherungsfähiger Elemente anzeigen, bei denen der Benutzer entweder der Besitzer ist oder für die dem Benutzer eine Berechtigung erteilt wurde. Dies bedeutet, dass Metadaten ausgebende integrierte Funktionen, z. B. OBJECT_SCHEMA_NAME, möglicherweise NULL zurückgeben, wenn dem Benutzer für das Objekt keine Berechtigung erteilt wurde. Weitere Informationen finden Sie unter [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die ANY-Berechtigung für das Objekt. Zum Angeben einer Datenbank-ID ist eine CONNECT-Berechtigung erforderlich, oder das Gastkonto muss aktiviert werden.  
  
## <a name="remarks"></a>Hinweise  
 Systemfunktionen können in der SELECT-Liste, in einer WHERE-Klausel und überall dort verwendet werden, wo ein Ausdruck zulässig ist. Weitere Informationen finden Sie unter [Ausdrücke](../../t-sql/language-elements/expressions-transact-sql.md) und [, in denen](../../t-sql/queries/where-transact-sql.md).  
  
 Für das von dieser Systemfunktion zurückgegebene Resultset wird die Sortierung der aktuellen Datenbank verwendet.  
  
 Wenn *Database_id* nicht angegeben wird, die [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] setzt voraus, dass *Object_id* wird im Kontext der aktuellen Datenbank. Eine Abfrage, die verweist auf ein *Object_id* in einer anderen Datenbank NULL oder falsche Ergebnisse zurückgegeben. Beispielsweise ist in der folgenden Abfrage [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] der Kontext der aktuellen Datenbank. [!INCLUDE[ssDE](../../includes/ssde-md.md)] versucht, einen Objektschemanamen für die angegebene Objekt-ID in dieser Datenbank zurückzugeben, statt in der in der FROM-Klausel der Abfrage angegebenen Datenbank. Deshalb werden fehlerhafte Informationen zurückgegeben.  
  
```  
SELECT DISTINCT OBJECT_SCHEMA_NAME(object_id)  
FROM master.sys.objects;  
  
```  
  
 Im folgenden Beispiel wird die Datenbank-ID für die `master`-Datenbank in der `OBJECT_SCHEMA_NAME`-Funktion angegeben, und die richtigen Ergebnisse werden zurückgegeben.  
  
```  
SELECT DISTINCT OBJECT_SCHEMA_NAME(object_id, 1) AS schema_name  
FROM master.sys.objects;  
  
```  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-returning-the-object-schema-name-and-object-name"></a>A. Zurückgeben des Objektschemanamens und des Objektnamens  
 Im folgenden Beispiel werden der Schemaname des Objekts, der Objektname und SQL-Text für alle zwischengespeicherten Abfragepläne zurückgegeben, bei denen es sich nicht um Ad-hoc- oder vorbereitete Anweisungen handelt.  
  
```  
SELECT DB_NAME(st.dbid) AS database_name,   
    OBJECT_SCHEMA_NAME(st.objectid, st.dbid) AS schema_name,  
    OBJECT_NAME(st.objectid, st.dbid) AS object_name,   
    st.text AS query_statement  
FROM sys.dm_exec_query_stats AS qs  
CROSS APPLY sys.dm_exec_sql_text(qs.sql_handle) AS st  
WHERE st.objectid IS NOT NULL;  
GO  
```  
  
### <a name="b-returning-three-part-object-names"></a>B. Zurückgeben von Objektnamen, die aus drei Teilen bestehen  
 Im folgenden Beispiel werden für alle Objekte in allen Datenbanken die Datenbank, das Schema und der Objektname sowie alle anderen Spalten in der dynamischen Verwaltungssicht `sys.dm_db_index_operational_stats` zurückgegeben.  
  
```  
SELECT QUOTENAME(DB_NAME(database_id))   
    + N'.'   
    + QUOTENAME(OBJECT_SCHEMA_NAME(object_id, database_id))   
    + N'.'   
    + QUOTENAME(OBJECT_NAME(object_id, database_id))  
    , *   
FROM sys.dm_db_index_operational_stats(null, null, null, null);  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Metadatenfunktionen &#40; Transact-SQL &#41;](../../t-sql/functions/metadata-functions-transact-sql.md)   
 [OBJECT_DEFINITION &#40;Transact-SQL&#41;](../../t-sql/functions/object-definition-transact-sql.md)   
 [Object_id &#40; Transact-SQL &#41;](../../t-sql/functions/object-id-transact-sql.md)   
 [Object_name &#40; Transact-SQL &#41;](../../t-sql/functions/object-name-transact-sql.md)   
 [Sicherungsfähige Elemente](../../relational-databases/security/securables.md)  
  
  


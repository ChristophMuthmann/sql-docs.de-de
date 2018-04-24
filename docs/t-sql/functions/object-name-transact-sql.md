---
title: OBJECT_NAME (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- OBJECT_NAME
- OBJECT_NAME_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- OBJECT_NAME function
- viewing database object names
- objects [SQL Server], names
- database objects [SQL Server], names
- displaying database object names
- database objects [SQL Server]
- names [SQL Server], database objects
ms.assetid: 7d5b923f-0c3e-4af9-b39b-132807a6d5b3
caps.latest.revision: 45
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: cea150168359628fa5e3d83e331f0227f0ae6aab
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="objectname-transact-sql"></a>OBJECT_NAME (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Gibt den Namen des Datenbankobjekts für Objekte mit Schemabereich zurück. Eine Liste der schemabezogenen Objekte finden Sie unter [sys.objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md).  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
OBJECT_NAME ( object_id [, database_id ] )  
```  
  
## <a name="arguments"></a>Argumente  
 *object_id*  
 Die ID des zu verwendenden Objekts. *object_id* ist vom Datentyp **int**, und es wird davon ausgegangen, dass es sich um ein schemabezogenes Objekt in der angegebenen Datenbank oder im aktuellen Datenbankkontext handelt.  
  
 *database_id*  
 Die ID der Datenbank, in der das Objekt gesucht werden soll. *database_id* ist vom Datentyp **int**.  
  
## <a name="return-types"></a>Rückgabetypen  
 **sysname**  
  
## <a name="exceptions"></a>Ausnahmen  
 Gibt NULL bei einem Fehler zurück oder wenn ein Aufrufer nicht über Berechtigungen zum Anzeigen des Objekts verfügt. Wenn für die Zieldatenbank AUTO_CLOSE auf ON festgelegt wurde, wird die Datenbank mithilfe der Funktion geöffnet.  
  
 Ein Benutzer kann nur die Metadaten sicherungsfähiger Elemente anzeigen, bei denen der Benutzer entweder der Besitzer ist oder für die dem Benutzer eine Berechtigung erteilt wurde. Dies bedeutet, dass Metadaten ausgebende integrierte Funktionen, z. B. OBJECT_NAME, möglicherweise NULL zurückgeben, wenn dem Benutzer für das Objekt keine Berechtigung erteilt wurde. Weitere Informationen finden Sie unter [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die ANY-Berechtigung für das Objekt. Zum Angeben einer Datenbank-ID ist eine CONNECT-Berechtigung erforderlich, oder das Gastkonto muss aktiviert werden.  
  
## <a name="remarks"></a>Remarks  
 Systemfunktionen können in der SELECT-Liste, in einer WHERE-Klausel und überall dort verwendet werden, wo ein Ausdruck zulässig ist. Weitere Informationen finden Sie unter [Ausdrücke](../../t-sql/language-elements/expressions-transact-sql.md) und [WHERE](../../t-sql/queries/where-transact-sql.md).  
  
 Für den von dieser Systemfunktion zurückgegebenen Wert wird die Sortierung der aktuellen Datenbank verwendet.  
  
 In [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] wird standardmäßig davon ausgegangen, dass sich *object_id* im Kontext der aktuellen Datenbank befindet. Eine Abfrage, die auf einen Wert für *object_id* in einer anderen Datenbank verweist, gibt entweder NULL oder falsche Ergebnisse zurück. Beispielsweise ist in der folgenden Abfrage [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] der Kontext der aktuellen Datenbank. [!INCLUDE[ssDE](../../includes/ssde-md.md)] versucht, einen Objektnamen für die angegebene Objekt-ID in dieser Datenbank statt in der in der FROM-Klausel der Abfrage angegebenen Datenbank zurückzugeben. Deshalb werden fehlerhafte Informationen zurückgegeben.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT DISTINCT OBJECT_NAME(object_id)  
FROM master.sys.objects;  
GO  
```  
  
 Sie können Objektnamen im Kontext einer anderen Datenbank auflösen, indem Sie eine Datenbank-ID angeben. Im folgenden Beispiel wird die Datenbank-ID für die `master`-Datenbank in der `OBJECT_SCHEMA_NAME`-Funktion angegeben, und die richtigen Ergebnisse werden zurückgegeben.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT DISTINCT OBJECT_SCHEMA_NAME(object_id, 1) AS schema_name  
FROM master.sys.objects;  
GO  
```  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-using-objectname-in-a-where-clause"></a>A. Verwenden von OBJECT_NAME in einer WHERE-Klausel  
 Das folgende Beispiel gibt Spalten aus der `sys.objects`-Katalogsicht für das durch `OBJECT_NAME` in der `WHERE`-Klausel der `SELECT`-Anweisung angegebene Objekt zurück.  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @MyID int;  
SET @MyID = (SELECT OBJECT_ID('AdventureWorks2012.Production.Product',  
    'U'));  
SELECT name, object_id, type_desc  
FROM sys.objects  
WHERE name = OBJECT_NAME(@MyID);  
GO  
```  
  
### <a name="b-returning-the-object-schema-name-and-object-name"></a>B. Zurückgeben des Objektschemanamens und des Objektnamens  
 Im folgenden Beispiel werden der Schemaname des Objekts, der Objektname und SQL-Text für alle zwischengespeicherten Abfragepläne zurückgegeben, bei denen es sich nicht um Ad-hoc- oder vorbereitete Anweisungen handelt.  
  
```  
SELECT DB_NAME(st.dbid) AS database_name,   
    OBJECT_SCHEMA_NAME(st.objectid, st.dbid) AS schema_name,  
    OBJECT_NAME(st.objectid, st.dbid) AS object_name,   
    st.text AS query_text  
FROM sys.dm_exec_query_stats AS qs  
CROSS APPLY sys.dm_exec_sql_text(qs.sql_handle) AS st  
WHERE st.objectid IS NOT NULL;  
GO  
```  
  
### <a name="c-returning-three-part-object-names"></a>C. Zurückgeben von Objektnamen, die aus drei Teilen bestehen  
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
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Beispiele: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] und [!INCLUDE[ssPDW](../../includes/sspdw-md.md)].  
  
### <a name="d-using-objectname-in-a-where-clause"></a>D. Verwenden von OBJECT_NAME in einer WHERE-Klausel  
 Das folgende Beispiel gibt Spalten aus der `sys.objects`-Katalogsicht für das durch `OBJECT_NAME` in der `WHERE`-Klausel der `SELECT`-Anweisung angegebene Objekt zurück. (Ihre Objektnummer wird sich von der im untenstehenden Beispiel unterscheiden (hier: 274100017).)  Wenn Sie dieses Beispiel testen möchten, suchen Sie nach einer gültigen Objektnummer, indem Sie `SELECT name, object_id FROM sys.objects;` in Ihrer Datenbank ausführen.)  
  
```  
SELECT name, object_id, type_desc  
FROM sys.objects  
WHERE name = OBJECT_NAME(274100017);  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Metadata Functions &#40;Transact-SQL&#41; (Metadatenfunktionen &#40;Transact-SQL&#41;)](../../t-sql/functions/metadata-functions-transact-sql.md)   
 [OBJECT_DEFINITION &#40;Transact-SQL&#41;](../../t-sql/functions/object-definition-transact-sql.md)   
 [OBJECT_ID &#40;Transact-SQL&#41;](../../t-sql/functions/object-id-transact-sql.md)  
  
  


---
title: DROP XML SCHEMA COLLECTION (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 11/25/2015
ms.prod: sql
ms.prod_service: sql-database
ms.service: ''
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- DROP XML SCHEMA COLLECTION
- DROP_XML_SCHEMA_COLLECTION_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- deleting XML schema collections
- XML schema collections [SQL Server], removing
- schema collections [SQL Server], removing
- removing XML schema collections
- dropping XML schema collections
- DROP XML SCHEMA COLLECTION statement
ms.assetid: d686f2f5-e03a-4ffe-a566-6036628f46f1
caps.latest.revision: 15
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: dd78f0f99758a8b570a9d54466c3a46b1133f5d2
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="drop-xml-schema-collection-transact-sql"></a>DROP XML SCHEMA COLLECTION (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Löscht die gesamte XML-Schemaauflistung und alle zugehörigen Komponenten.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
DROP XML SCHEMA COLLECTION [ relational_schema. ]sql_identifier  
```  
  
## <a name="arguments"></a>Argumente  
 *relational_schema*  
 Identifiziert den Namen des relationalen Schemas. Wenn kein Name angegeben ist, wird das relationale Standardschema verwendet.  
  
 *sql_identifier*  
 Der Name der zu löschenden XML-Schemaauflistung.  
  
## <a name="remarks"></a>Remarks  
 Das Löschen einer XML-Schemaauflistung ist ein Transaktionsvorgang. Das heißt, wenn Sie eine XML-Schemaauflistung innerhalb einer Transaktion löschen und später ein Rollback für die Transaktion ausführen, wird die XML-Schemaauflistung nicht gelöscht.  
  
 Eine XML-Schemaauflistung, die verwendet wird, kann nicht gelöscht werden. Das heißt, Folgendes darf für die zu löschende Auflistung nicht zutreffen:  
  
-   Sie darf keinem Parameter bzw. keiner Spalte vom Typ **xml** zugeordnet sein.  
  
-   Sie darf nicht in Tabelleneinschränkungen angegeben sein.  
  
-   In einer schemagebundenen Funktion oder gespeicherten Prozedur darf nicht darauf verwiesen werden. Beispielsweise sperrt die folgende Funktion die XML-Schemaauflistung `MyCollection`, weil die Funktion `WITH SCHEMABINDING` angibt. Wenn Sie dies entfernen, ist für XML SCHEMA COLLECTION keine Sperre vorhanden.  
  
    ```  
    CREATE FUNCTION dbo.MyFunction()  
    RETURNS int  
    WITH SCHEMABINDING  
    AS  
    BEGIN  
       ...  
       DECLARE @x XML(MyCollection)  
       ...  
    END;  
    ```  
  
## <a name="permissions"></a>Berechtigungen  
 Zum Löschen von XML SCHEMA COLLECTION ist die DROP-Berechtigung für die Auflistung erforderlich.  
  
## <a name="examples"></a>Beispiele  
 Das folgende Beispiel zeigt, wie eine XML-Schemaauflistung entfernt wird.  
  
```  
DROP XML SCHEMA COLLECTION ManuInstructionsSchemaCollection;  
GO  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [CREATE XML SCHEMA COLLECTION &#40;Transact-SQL&#41;](../../t-sql/statements/create-xml-schema-collection-transact-sql.md)   
 [ALTER XML SCHEMA COLLECTION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-xml-schema-collection-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [Vergleichen von typisiertem XML mit nicht typisiertem XML](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)   
 [Anforderungen und Einschränkungen für XML-Schemaauflistungen auf dem Server](../../relational-databases/xml/requirements-and-limitations-for-xml-schema-collections-on-the-server.md)  
  
  

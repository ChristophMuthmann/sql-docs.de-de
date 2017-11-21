---
title: DROP SCHEMA (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 05/11/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DROP SCHEMA
- DROP_SCHEMA_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- deleting schemas
- schemas [SQL Server], removing
- DROP SCHEMA statement
- dropping schemas
- removing schemas
ms.assetid: 874aa29e-c8ad-41e4-a672-900fdc58f1f6
caps.latest.revision: 51
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 584aea443e3263f44367ede24d7a59b8564e92c1
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="drop-schema-transact-sql"></a>DROP SCHEMA (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Entfernt ein Schema aus der Datenbank.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
DROP SCHEMA  [ IF EXISTS ] schema_name  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
DROP SCHEMA schema_name  
```  
  
## <a name="arguments"></a>Argumente  
 *IF VORHANDEN IST*  
 **Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] bis zur [aktuellen Version](http://go.microsoft.com/fwlink/p/?LinkId=299658)).  
  
 Das Schema gelöscht bedingt nur, wenn sie bereits vorhanden ist.  
  
 *schema_name*  
 Der Name des Schemas in der Datenbank.  
  
## <a name="remarks"></a>Hinweise  
 Das zu löschende Schema darf keine Objekte enthalten. Falls das Schema Objekte enthält, erzeugt die DROP-Anweisung einen Fehler.  
  
 Informationen zu Schemas werden in der [sys.schemas](../../relational-databases/system-catalog-views/schemas-catalog-views-sys-schemas.md) -Katalogsicht angezeigt.  
  
 **Vorsicht**[!INCLUDE[ssCautionUserSchema](../../includes/sscautionuserschema-md.md)]  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die CONTROL-Berechtigung für das Schema oder die ALTER ANY SCHEMA-Berechtigung für die Datenbank.  
  
## <a name="examples"></a>Beispiele  
 Das folgende Beispiel beginnt mit einer einzelnen `CREATE SCHEMA`-Anweisung. Von der Anweisung werden das `Sprockets`-Schema, das sich im Besitz von `Krishna` befindet, und die `Sprockets.NineProngs`-Tabelle erstellt. Anschließend wird die `SELECT`-Berechtigung für `Anibal` erteilt und die `SELECT`-Berechtigung für `Hung-Fu` verweigert.  
  
```  
CREATE SCHEMA Sprockets AUTHORIZATION Krishna   
    CREATE TABLE NineProngs (source int, cost int, partnumber int)  
    GRANT SELECT TO Anibal   
    DENY SELECT TO Hung-Fu;  
GO  
```  
  
 Mit den folgenden Anweisungen wird das Schema gelöscht. Beachten Sie, dass zunächst die Tabelle gelöscht werden muss, die sich im Schema befindet.  
  
```  
DROP TABLE Sprockets.NineProngs;  
DROP SCHEMA Sprockets;  
GO  
```  
  
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen Sie SCHEMA &#40; Transact-SQL &#41;](../../t-sql/statements/create-schema-transact-sql.md)   
 [ALTER SCHEMA &#40; Transact-SQL &#41;](../../t-sql/statements/alter-schema-transact-sql.md)   
 [DROP SCHEMA (Transact-SQL)](../../t-sql/statements/drop-schema-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  


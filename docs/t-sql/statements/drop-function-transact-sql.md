---
title: DROP FUNCTION (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 06/28/2017
ms.prod: sql
ms.prod_service: sql-data-warehouse, database-engine, pdw, sql-database
ms.service: ''
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- DROP_FUNCTION_TSQL
- DROP FUNCTION
dev_langs:
- TSQL
helpviewer_keywords:
- user-defined functions [SQL Server], removing
- removing user-defined functions
- DROP FUNCTION statement
- dropping user-defined functions
- deleting user-defined functions
ms.assetid: ee5ad283-9e44-4109-902f-0ce12669ee11
caps.latest.revision: 49
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 75e7395703cc048790fb8cab52e39daeeb21f03c
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="drop-function-transact-sql"></a>DROP FUNCTION (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-asdb-asdw-pdw-md.md)]

  Entfernt eine oder mehrere benutzerdefinierte Funktionen aus der aktuellen Datenbank. Benutzerdefinierte Funktionen werden mithilfe von [CREATE FUNCTION](../../t-sql/statements/create-function-transact-sql.md) erstellt und mithilfe von [ALTER FUNCTION](../../t-sql/statements/alter-function-transact-sql.md) geändert.  
  
 Die DROP-Funktion unterstützt nativ kompilierte benutzerdefinierte Skalarfunktionen. Weitere Informationen dazu finden Sie unter [Benutzerdefinierte Skalarfunktionen für In-Memory-OLTP](../../relational-databases/in-memory-oltp/scalar-user-defined-functions-for-in-memory-oltp.md).  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
 -- SQL Server, Azure SQL Database 

DROP FUNCTION [ IF EXISTS ] { [ schema_name. ] function_name } [ ,...n ]   
[;]
```

```  
 -- Azure SQL Data Warehouse, Parallel Data Warehouse 

DROP FUNCTION [ schema_name. ] function_name
[;] 
```  
   
  
## <a name="arguments"></a>Argumente  
 *IF EXISTS*    
 Ändert die Funktion nur, sofern diese bereits vorhanden ist. Ab [!INCLUDE[ssnoversion_md](../../includes/ssnoversion_md.md)] 2016 in [!INCLUDE[sssds_md](../../includes/sssds_md.md)] verfügbar.
  
 *schema_name*  
 Der Name des Schemas, zu dem die benutzerdefinierte Funktion gehört.  
  
 *function_name*  
 Der Name der benutzerdefinierten Funktion oder Funktionen, die entfernt werden sollen. Die Angabe des Schemanamens ist optional. Der Servername und der Datenbankname können nicht angegeben werden.  
  
## <a name="remarks"></a>Remarks  
 DROP FUNCTION erzeugt einen Fehler, wenn [!INCLUDE[tsql](../../includes/tsql-md.md)]-Funktionen oder -Sichten in der Datenbank vorhanden sind, die auf diese Funktion verweisen und mithilfe von SCHEMABINDING erstellt wurden, oder wenn berechnete Spalten, CHECK-Einschränkungen oder DEFAULT-Einschränkungen vorhanden sind, die auf die Funktion verweisen.  
  
 DROP FUNCTION erzeugt außerdem einen Fehler, wenn berechnete Spalten vorhanden sind, die auf diese Funktion verweisen und indiziert wurden.  
  
## <a name="permissions"></a>Berechtigungen  
 Um DROP FUNCTION ausführen zu können, benötigt ein Benutzer mindestens ALTER-Berechtigungen für das Schema, zu dem die Funktion gehört, oder CONTROL-Berechtigungen für die Funktion.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-dropping-a-function"></a>A. Löschen einer Funktion  
 Im folgenden Beispiel wird die benutzerdefinierte Funktion `fn_SalesByStore` aus dem `Sales`-Schema in der [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]-Beispieldatenbank gelöscht. Informationen zum Erstellen dieser Funktion finden Sie in Beispiel B unter [CREATE FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/create-function-transact-sql.md).  
  
```  
DROP FUNCTION Sales.fn_SalesByStore;  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [ALTER FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-function-transact-sql.md)   
 [CREATE FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/create-function-transact-sql.md)   
 [OBJECT_ID &#40;Transact-SQL&#41;](../../t-sql/functions/object-id-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [sys.sql_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)   
 [sys.parameters &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-parameters-transact-sql.md)  
  
  

---
title: DROP-Funktion (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/28/2017
ms.prod: sql-non-specified
ms.prod_service: sql-data-warehouse, database-engine, pdw, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 3b85cb68749cdcf88d62d9d8fbf136a37e845519
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="drop-function-transact-sql"></a>DROP FUNCTION (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-asdb-asdw-pdw-md.md)]

  Entfernt eine oder mehrere benutzerdefinierte Funktionen aus der aktuellen Datenbank. Benutzerdefinierte Erstellung erfolgt mithilfe von [CREATE FUNCTION](../../t-sql/statements/create-function-transact-sql.md) und mithilfe von geändert [ALTER FUNCTION](../../t-sql/statements/alter-function-transact-sql.md).  
  
 Die DROP-Funktion unterstützt systemintern kompilierte, skalare benutzerdefinierte Funktionen. Weitere Informationen finden Sie unter [Skalarfunktionen für In-Memory OLTP](../../relational-databases/in-memory-oltp/scalar-user-defined-functions-for-in-memory-oltp.md).  
  
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
 *IF VORHANDEN IST*    
 Bedingt löscht die Funktion nur dann, wenn sie bereits vorhanden ist. Verfügbar ab [!INCLUDE[ssnoversion_md](../../includes/ssnoversion_md.md)] 2016 und in [!INCLUDE[sssds_md](../../includes/sssds_md.md)].
  
 *schema_name*  
 Der Name des Schemas, zu dem die benutzerdefinierte Funktion gehört.  
  
 *Funktionsname*  
 Der Name der benutzerdefinierten Funktion oder Funktionen, die entfernt werden sollen. Die Angabe des Schemanamens ist optional. Der Servername und der Datenbankname können nicht angegeben werden.  
  
## <a name="remarks"></a>Hinweise  
 DROP FUNCTION erzeugt einen Fehler, wenn [!INCLUDE[tsql](../../includes/tsql-md.md)]-Funktionen oder -Sichten in der Datenbank vorhanden sind, die auf diese Funktion verweisen und mithilfe von SCHEMABINDING erstellt wurden, oder wenn berechnete Spalten, CHECK-Einschränkungen oder DEFAULT-Einschränkungen vorhanden sind, die auf die Funktion verweisen.  
  
 DROP FUNCTION erzeugt außerdem einen Fehler, wenn berechnete Spalten vorhanden sind, die auf diese Funktion verweisen und indiziert wurden.  
  
## <a name="permissions"></a>Berechtigungen  
 Um DROP FUNCTION ausführen zu können, benötigt ein Benutzer mindestens ALTER-Berechtigungen für das Schema, zu dem die Funktion gehört, oder CONTROL-Berechtigungen für die Funktion.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-dropping-a-function"></a>A. Löschen einer Funktion  
 Das folgende Beispiel löscht die `fn_SalesByStore` User-defined Function, aus der `Sales` Schema in der [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] -Beispieldatenbank. Um diese Funktion zu erstellen, finden Sie unter Beispiel B im [CREATE FUNCTION &#40; Transact-SQL &#41; ](../../t-sql/statements/create-function-transact-sql.md).  
  
```  
DROP FUNCTION Sales.fn_SalesByStore;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [ALTER FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-function-transact-sql.md)   
 [CREATE FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/create-function-transact-sql.md)   
 [Object_id &#40; Transact-SQL &#41;](../../t-sql/functions/object-id-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [sys.sql_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)   
 [Sys.Parameters &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-parameters-transact-sql.md)  
  
  


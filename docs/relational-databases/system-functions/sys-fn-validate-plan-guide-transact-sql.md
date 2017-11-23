---
title: Sys. fn_validate_plan_guide (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.fn_validate_plan_guide
- sys.fn_validate_plan_guide_TSQL
- fn_validate_plan_guide
- fn_validate_plan_guide_TSQL
dev_langs: TSQL
helpviewer_keywords:
- fn_validate_plan_guide function
- sys.fn_validate_plan_guide function
ms.assetid: 3af8b47a-936d-4411-91d1-d2d16dda5623
caps.latest.revision: "19"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: fbca0ca02e994a3c286cea445965edd9cd53bfcf
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="sysfnvalidateplanguide-transact-sql"></a>sys.fn_validate_plan_guide (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Überprüft die Gültigkeit der angegebenen Planhinweisliste. Die sys.fn_validate_plan_guide-Funktion gibt die erste Fehlermeldung zurück, die beim Anwenden der Planhinweisliste auf ihre Abfrage gefunden wird. Ein leeres Rowset wird zurückgegeben, wenn die Planhinweisliste gültig ist. Planhinweislisten können ungültig werden, nachdem Änderungen am physischen Entwurf der Datenbank vorgenommen wurden. Wenn beispielsweise eine Planhinweisliste einen bestimmten Index angibt, und dieser Index anschließend gelöscht wird, kann die Abfrage die Planhinweisliste nicht länger verwenden.  
  
 Durch Überprüfen der Gültigkeit einer Planhinweisliste können Sie feststellen, ob die Planhinweisliste ohne Änderungen durch den Optimierer verwendet werden kann. Auf der Basis der Ergebnisse der Funktion können Sie entscheiden, dass die Planhinweisliste gelöscht wird und die Abfrage neu optimiert wird, oder Sie können den Datenbankentwurf ändern, indem Sie beispielsweise den in der Planhinweisliste angegebenen Index neu erstellen.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
sys.fn_validate_plan_guide ( plan_guide_id )  
```  
  
## <a name="arguments"></a>Argumente  
 *plan_guide_id*  
 Ist die ID der Planhinweisliste, wie Sie in der [plan_guides](../../relational-databases/system-catalog-views/sys-plan-guides-transact-sql.md) -Katalogsicht angezeigt. *plan_guide_id* ist vom Datentyp **int** und besitzt keinen Standardwert.  
  
## <a name="table-returned"></a>Zurückgegebene Tabelle  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|msgnum|**int**|ID der Fehlermeldung.|  
|severity|**tinyint**|Schweregrad des Fehlers, der zwischen 1 und 25 liegen kann.|  
|state|**smallint**|Statusnummer des Fehlers, welche die Stelle im Code angibt, an der der Fehler aufgetreten ist.|  
|message|**nvarchar(2048)**|Meldungstext des Fehlers.|  
  
## <a name="permissions"></a>Berechtigungen  
 Für Planhinweislisten mit dem Bereich OBJECT ist die VIEW DEFINITION- oder die ALTER-Berechtigung für das Objekt erforderlich, auf das verwiesen wird, ebenso wie Berechtigungen zur Kompilierung der Abfrage oder des Batches, die in der Planhinweisliste bereitgestellt werden. Wenn ein Batch z. B. SELECT-Anweisungen enthält, sind SELECT-Berechtigungen für die Objekte erforderlich, auf die verwiesen wird.  
  
 Für Planhinweislisten mit dem Bereich SQL oder TEMPLATE ist die ALTER-Berechtigung für die Datenbank erforderlich, ebenso wie Berechtigungen zur Kompilierung der Abfrage oder des Batches, die in der Planhinweisliste bereitgestellt werden. Wenn ein Batch z. B. SELECT-Anweisungen enthält, sind SELECT-Berechtigungen für die Objekte erforderlich, auf die verwiesen wird.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-validating-all-plan-guides-in-a-database"></a>A. Überprüfen aller Planhinweislisten in einer Datenbank  
 Im folgenden Beispiel wird die Gültigkeit aller Planhinweislisten in der aktuellen Datenbank überprüft. Wenn ein leeres Resultset zurückgegeben wird, sind alle Planhinweislisten gültig.  
  
```tsql  
USE AdventureWorks2012;  
GO  
SELECT plan_guide_id, msgnum, severity, state, message  
FROM sys.plan_guides  
CROSS APPLY fn_validate_plan_guide(plan_guide_id);  
GO  
```  
  
### <a name="b-testing-plan-guide-validation-before-implementing-a-change-to-the-database"></a>B. Testen der Gültigkeitsüberprüfung der Planhinweislisten vor dem Implementieren von Änderungen an der Datenbank  
 Im folgenden Beispiel wird eine explizite Transaktion verwendet, um einen Index zu löschen. Die `sys.fn_validate_plan_guide` -Funktion wird ausgeführt, um zu bestimmen, ob diese Aktion Planhinweislisten in der Datenbank ungültig gemacht wird. Auf der Basis der Ergebnisse der Funktion wird entweder ein Commit der `DROP INDEX` -Anweisung oder ein Rollback der Transaktion ausgeführt, sodass der Index nicht gelöscht wird.  
  
```tsql  
USE AdventureWorks2012;  
GO  
BEGIN TRANSACTION;  
DROP INDEX IX_SalesOrderHeader_CustomerID ON Sales.SalesOrderHeader;  
-- Check for invalid plan guides.  
IF EXISTS (SELECT plan_guide_id, msgnum, severity, state, message  
           FROM sys.plan_guides  
           CROSS APPLY sys.fn_validate_plan_guide(plan_guide_id))  
    ROLLBACK TRANSACTION;  
ELSE  
    COMMIT TRANSACTION;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Planhinweislisten](../../relational-databases/performance/plan-guides.md)   
 [sp_create_plan_guide &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md)   
 [sp_create_plan_guide_from_handle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql.md)  
  
  

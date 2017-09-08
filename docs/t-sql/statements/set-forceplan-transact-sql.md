---
title: SET FORCEPLAN (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/26/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SET_FORCEPLAN_TSQL
- SET FORCEPLAN
- FORCEPLAN
- FORCEPLAN_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- joins [SQL Server], overriding query optimizer process
- FORCEPLAN option
- SET FORCEPLAN statement
- query optimizer [SQL Server], optimizing process
- overriding query optimizer process
ms.assetid: b6c0b08f-2060-4696-9e12-50cb7e674321
caps.latest.revision: 40
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: df0bb88faa940a54f3b3eb14c34998b1982879c6
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="set-forceplan-transact-sql"></a>SET FORCEPLAN (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Wenn FORCEPLAN auf ON festgelegt wird, verarbeitet der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Abfrageoptimierer einen Join in der Reihenfolge, in der die Tabellen in der FROM-Klausel einer Abfrage aufgeführt sind. Darüber hinaus wird durch Festlegen von FORCEPLAN auf ON die Verwendung eines Nested Loops-Joins erzwungen, sofern nicht andere Jointypen zum Erstellen eines Plans für die Abfrage erforderlich sind oder durch Join- bzw. Abfragehinweise angefordert werden.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
SET FORCEPLAN { ON | OFF }  
```  
  
## <a name="remarks"></a>Hinweise  
 SET FORCEPLAN überschreibt im Wesentlichen die Logik, die der Abfrageoptimierer beim Verarbeiten einer [!INCLUDE[tsql](../../includes/tsql-md.md)]-SELECT-Anweisung verwendet hat. Die SELECT-Anweisung gibt unabhängig von dieser Einstellung dieselben Daten zurück. Der einzige Unterschied besteht darin, wie [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] die Tabellen bei der Ausführung der Abfrage verarbeitet.  
  
 Auch Hinweise für den Abfrageoptimierer können in Abfragen verwendet werden, um das Verarbeiten der SELECT-Anweisung durch [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] zu beeinflussen.  
  
 SET FORCEPLAN wird zur Ausführungszeit und nicht zur Analysezeit angewendet.  
  
## <a name="permissions"></a>Berechtigungen  
 Die SET FORCEPLAN-Berechtigungen erhalten standardmäßig alle Benutzer.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel werden vier Tabellen verknüpft. Die `SHOWPLAN_TEXT`-Einstellung ist aktiviert. Daher gibt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Informationen dazu zurück, wie die Abfrage anders verarbeitet wird, sobald die `SET FORCE_PLAN`-Einstellung aktiviert wird.  
  
```  
USE AdventureWorks2012;  
GO  
-- Make sure FORCEPLAN is set to OFF.  
SET SHOWPLAN_TEXT OFF;  
GO  
SET FORCEPLAN OFF;  
GO  
SET SHOWPLAN_TEXT ON;  
GO  
-- Example where the query plan is not forced.  
SELECT p.LastName, p.FirstName, v.Name  
FROM Person.Person AS p  
   INNER JOIN HumanResources.Employee AS e  
   ON e.BusinessEntityID = p.BusinessEntityID  
   INNER JOIN Purchasing.PurchaseOrderHeader AS poh  
   ON e.BusinessEntityID = poh.EmployeeID  
   INNER JOIN Purchasing.Vendor AS v  
   ON poh.VendorID = v.BusinessEntityID;  
GO  
-- SET FORCEPLAN to ON.  
SET SHOWPLAN_TEXT OFF;  
GO  
SET FORCEPLAN ON;  
GO  
SET SHOWPLAN_TEXT ON;  
GO  
-- Reexecute inner join to see the effect of SET FORCEPLAN ON.  
SELECT p.LastName, p.FirstName, v.Name  
FROM Person.Person AS p  
   INNER JOIN HumanResources.Employee AS e   
   ON e.BusinessEntityID = p.BusinessEntityID  
   INNER JOIN Purchasing.PurchaseOrderHeader AS poh  
   ON e.BusinessEntityID = poh.EmployeeID  
   INNER JOIN Purchasing.Vendor AS v  
   ON poh.VendorID = v.BusinessEntityID;  
GO  
SET SHOWPLAN_TEXT OFF;  
GO  
SET FORCEPLAN OFF;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [SET-Anweisungen (Transact-SQL)](../../t-sql/statements/set-statements-transact-sql.md)   
 [SET SHOWPLAN_ALL &#40; Transact-SQL &#41;](../../t-sql/statements/set-showplan-all-transact-sql.md)   
 [SET SHOWPLAN_TEXT &#40; Transact-SQL &#41;](../../t-sql/statements/set-showplan-text-transact-sql.md)  
  
  


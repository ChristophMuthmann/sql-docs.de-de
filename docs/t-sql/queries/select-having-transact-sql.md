---
title: (Transact-SQL) mit | Microsoft Docs
ms.custom: 
ms.date: 08/09/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- HAVING
- HAVING_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- restricting conditions for result set
- search conditions [SQL Server], HAVING clause
- HAVING clause
- HAVING clause, about HAVING clause
ms.assetid: 55650709-001e-42f4-902f-ead09a3c34af
caps.latest.revision: 27
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 9bff75a84689090f6e416db052a2561e57fa98a6
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="select---having-transact-sql"></a>SELECT - müssen (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Gibt eine Suchbedingung für eine Gruppe oder ein Aggregat an. HAVING kann nur mit der SELECT-Anweisung verwendet werden. HAVING wird in der Regel in einer GROUP BY-Klausel verwendet. Wenn GROUP BY nicht verwendet wird, verhält sich HAVING wie eine WHERE-Klausel.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
[ HAVING <search condition> ]  
```  
  
## <a name="arguments"></a>Argumente  
\<Search_condition > Gibt die Suchbedingung für die Gruppe oder das Aggregat an.  
  
 Die **Text**, **Image**, und **Ntext** Datentypen können nicht in einer HAVING-Klausel verwendet werden.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel, in dem eine einfache `HAVING`-Klausel verwendet wird, werden die Gesamtsummen für `SalesOrderID` aus der `SalesOrderDetail`-Tabelle abgerufen, die `$100000.00` überschreiten.  
  
```  
USE AdventureWorks2012 ;  
GO  
SELECT SalesOrderID, SUM(LineTotal) AS SubTotal  
FROM Sales.SalesOrderDetail  
GROUP BY SalesOrderID  
HAVING SUM(LineTotal) > 100000.00  
ORDER BY SalesOrderID ;  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Beispiele: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] und[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 Im folgenden Beispiel wird eine `HAVING` -Klausel, um die Gesamtsumme für jeden rufen `SalesAmount` aus der `FactInternetSales` bei Verwendung der `OrderDateKey` im Jahr 2004 oder höher ist.  
  
```  
-- Uses AdventureWorks  
  
SELECT OrderDateKey, SUM(SalesAmount) AS TotalSales   
FROM FactInternetSales  
GROUP BY OrderDateKey   
HAVING SUM(SalesAmount) > 80000  
ORDER BY OrderDateKey;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [GROUP BY &#40; Transact-SQL &#41;](../../t-sql/queries/select-group-by-transact-sql.md)   
 [WOBEI &#40; Transact-SQL &#41;](../../t-sql/queries/where-transact-sql.md)  
  
  



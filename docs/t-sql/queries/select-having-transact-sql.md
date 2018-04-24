---
title: HAVING (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 11/28/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: t-sql|queries
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
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
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Active
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 7975851cc55a0d59472c93b4cd4753d7b6c408c1
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="select---having-transact-sql"></a>SELECT – HAVING (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Gibt eine Suchbedingung für eine Gruppe oder ein Aggregat an. HAVING kann nur mit der SELECT-Anweisung verwendet werden. HAVING wird in der Regel mit einer GROUP BY-Klausel verwendet. Wenn GROUP BY nicht verwendet wird, gibt es eine implizite einzelne, aggregierte Gruppe.   
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
[ HAVING <search condition> ]  
```  
  
## <a name="arguments"></a>Argumente  
\<search_condition> gibt ein oder mehrere Prädikate für Gruppen und Aggregate an, die erfüllt werden müssen. Weitere Informationen zu Suchbedingungen und Prädikaten finden Sie unter [Suchbedingung &#40;Transact-SQL&#41;](../../t-sql/queries/search-condition-transact-sql.md).  
  
 Die Datentypen **text**, **image** und **ntext** können in einer HAVING-Klausel nicht verwendet werden.  
  
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
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Beispiele: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] und [!INCLUDE[ssPDW](../../includes/sspdw-md.md)].  
 Im folgenden Beispiel wird mit einer `HAVING`-Klausel die Gesamtsumme für jeden `SalesAmount` aus der `FactInternetSales`-Tabelle abgerufen, wenn `OrderDateKey` im Jahr 2004 oder später ist.  
  
```  
-- Uses AdventureWorks  
  
SELECT OrderDateKey, SUM(SalesAmount) AS TotalSales   
FROM FactInternetSales  
GROUP BY OrderDateKey   
HAVING SUM(SalesAmount) > 80000  
ORDER BY OrderDateKey;  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [GROUP BY &#40;Transact-SQL&#41;](../../t-sql/queries/select-group-by-transact-sql.md)   
 [WHERE &#40;Transact-SQL&#41;](../../t-sql/queries/where-transact-sql.md)  
  
  


---
title: GROUPING (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- GROUPING
- GROUPING_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- null values [SQL Server], GROUPING function
- grouping columns
- ROLLUP operator
- GROUP BY clause, GROUPING function
- GROUPING function
- CUBE operator
ms.assetid: 4efa3868-1fc4-4626-8fb1-e863cc03e422
caps.latest.revision: 32
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 6876950bc8411678230a62366a112b4b5b68bc74
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="grouping-transact-sql"></a>GROUPING (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Gibt an, ob ein angegebener Spaltenausdruck in einer GROUP BY-Liste aggregiert wird oder nicht. GROUPING gibt im Resultset 1 für aggregiert oder 0 für nicht aggregiert zurück. GROUPING kann nur in der SELECT-\<Auswahlliste>, der HAVING- und der ORDER BY-Klausel verwendet werden, wenn GROUP BY angegeben wurde.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
GROUPING ( <column_expression> )  
```  
  
## <a name="arguments"></a>Argumente  
 \<column_expression>  
 Eine Spalte oder ein Ausdruck, der eine Spalte in einer [GROUP BY](../../t-sql/queries/select-group-by-transact-sql.md)-Klausel enthält.  
  
## <a name="return-types"></a>Rückgabetypen  
 **tinyint**  
  
## <a name="remarks"></a>Remarks  
 GROUPING wird verwendet, um die von ROLLUP, CUBE oder GROUPING SETS zurückgegebenen NULL-Werte von NULL-Standardwerten zu unterscheiden. Der Wert NULL, der als Ergebnis eines ROLLUP, CUBE oder GROUPING SETS-Vorgangs zurückgegeben wird, stellt eine besondere Verwendung von NULL dar. Der Wert fungiert als Spaltenplatzhalter im Resultset und bedeutet alle.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel werden `SalesQuota` gruppiert und `SaleYTD`-Beträge in der [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]-Datenbank aggregiert. Die `GROUPING`-Funktion wird auf die `SalesQuota`-Spalte angewendet.  
  
```  
SELECT SalesQuota, SUM(SalesYTD) 'TotalSalesYTD', GROUPING(SalesQuota) AS 'Grouping'  
FROM Sales.SalesPerson  
GROUP BY SalesQuota WITH ROLLUP;  
GO  
```  
  
 Das Resultset zeigt zwei NULL-Werte unter `SalesQuota` an. Der erste `NULL`-Wert stellt die Gruppe der NULL-Werte aus dieser Spalte in der Tabelle dar. Der zweite `NULL`-Wert befindet sich in der Summenzeile, die vom ROLLUP-Vorgang hinzugefügt wurde. Die Summenzeile enthält die `TotalSalesYTD`-Gesamtsummen für alle `SalesQuota`-Gruppen und ist durch `1` in der `Grouping`-Spalte gekennzeichnet.  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 SalesQuota     TotalSalesYTD       Grouping  
------------   -----------------   --------  
NULL           1533087.5999          0  
250000.00      33461260.59           0  
300000.00      9299677.9445          0  
NULL           44294026.1344         1  

(4 row(s) affected)
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [GROUPING_ID &#40;Transact-SQL&#41;](../../t-sql/functions/grouping-id-transact-sql.md)   
 [GROUP BY &#40;Transact-SQL&#41;](../../t-sql/queries/select-group-by-transact-sql.md)  
  
  

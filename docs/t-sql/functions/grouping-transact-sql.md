---
title: Gruppierung (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: d83b68d9d5fb52c67ca3a1910fe9541dfd6f5552
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="grouping-transact-sql"></a>GROUPING (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Gibt an, ob ein angegebener Spaltenausdruck in einer GROUP BY-Liste aggregiert wird oder nicht. GROUPING gibt im Resultset 1 für aggregiert oder 0 für nicht aggregiert zurück. Gruppierung kann nur in die SELECT-Anweisung verwendet werden \<auswählen > aufzulisten, HAVING und ORDER BY-Klauseln, wenn GROUP BY angegeben ist.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
GROUPING ( <column_expression> )  
```  
  
## <a name="arguments"></a>Argumente  
 \<Spaltenausdruck >  
 Ist eine Spalte oder ein Ausdruck, der eine Spalte enthält eine [GROUP BY](../../t-sql/queries/select-group-by-transact-sql.md) Klausel.  
  
## <a name="return-types"></a>Rückgabetypen  
 **tinyint**  
  
## <a name="remarks"></a>Hinweise  
 GROUPING wird verwendet, um die von ROLLUP, CUBE oder GROUPING SETS zurückgegebenen NULL-Werte von NULL-Standardwerten zu unterscheiden. Der Wert NULL, der als Ergebnis eines ROLLUP, CUBE oder GROUPING SETS-Vorgangs zurückgegeben wird, stellt eine besondere Verwendung von NULL dar. Der Wert fungiert als Spaltenplatzhalter im Resultset und bedeutet alle.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel werden `SalesQuota` gruppiert und `SaleYTD`-Beträge in der [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]-Datenbank aggregiert. Die `GROUPING`-Funktion wird auf die `SalesQuota`-Spalte angewendet.  
  
```  
SELECT SalesQuota, SUM(SalesYTD) 'TotalSalesYTD', GROUPING(SalesQuota) AS 'Grouping'  
FROM Sales.SalesPerson  
GROUP BY SalesQuota WITH ROLLUP;  
GO  
```  
  
 Das Resultset zeigt zwei NULL-Werte unter `SalesQuota` an. Der erste `NULL`-Wert stellt die Gruppe der NULL-Werte aus dieser Spalte in der Tabelle dar. Der zweite `NULL`-Wert befindet sich in der Summenzeile, die vom ROLLUP-Vorgang hinzugefügt wurde. Die Summenzeile enthält die `TotalSalesYTD` -Gesamtsummen für alle `SalesQuota` gruppiert und wird von `1` in der `Grouping` Spalte.  
  
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
  
## <a name="see-also"></a>Siehe auch  
 [GROUPING_ID &#40; Transact-SQL &#41;](../../t-sql/functions/grouping-id-transact-sql.md)   
 [GROUP BY &#40; Transact-SQL &#41;](../../t-sql/queries/select-group-by-transact-sql.md)  
  
  

---
title: ISNULL (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- ISNULL
- ISNULL_TSQL
- IFNULL_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- replacing null values
- null values [SQL Server], ISNULL
- null values [SQL Server], replacement values
- ISNULL function
ms.assetid: 6f3e5802-864b-4e77-9862-657bb5430b68
caps.latest.revision: 42
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: c3a43c2da306098e3b3b0dd0d7f9a4bb0f17b40b
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="isnull-transact-sql"></a>ISNULL (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Ersetzt NULL durch den angegebenen Ersatzwert.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
ISNULL ( check_expression , replacement_value )  
```  
  
## <a name="arguments"></a>Argumente  
 *check_expression*  
 Dies ist der [Ausdruck](../../t-sql/language-elements/expressions-transact-sql.md), der auf NULL überprüft werden soll. *check_expression* kann ein beliebiger Typ sein.  
  
 *replacement_value*  
 Der Ausdruck, der zurückgegeben werden soll, wenn *Prüfausdruck* NULL ist. *replacement_value* (Ersatzwert) muss einen Typ aufweisen, der implizit in den Typ von *Prüfausdruck* konvertiert werden kann.  
  
## <a name="return-types"></a>Rückgabetypen  
 Gibt denselben Typ wie der Ausdruck *check_expression* zurück. Wenn ein literaler NULL-Wert als *check_expression* bereitgestellt wird, wird der Datentyp des Ersatzwerts *replacement_value* zurückgegeben. Wenn ein literaler NULL-Wert als *check_expression* bereitgestellt wird und kein *replacement_value* bereitgestellt wird, wird **int** zurückgegeben.  
  
## <a name="remarks"></a>Remarks  
 Der Wert von *check_expression* wird zurückgegeben, wenn er nicht NULL ist, andernfalls wird *replacement_value* zurückgegeben, nachdem er implizit in den Typ von *check_expression* konvertiert wurde, falls die Typen unterschiedlich sind. *replacement_value* kann gekürzt werden, wenn *replacement_value* länger als *check_expression* ist.  
  
> [!NOTE]  
>  Verwenden Sie [COALESCE &#40;Transact-SQL&#41;](../../t-sql/language-elements/coalesce-transact-sql.md), um den ersten Wert zurückzugeben, der nicht NULL ist.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-using-isnull-with-avg"></a>A. Verwenden von ISNULL mit AVG  
 Im folgenden Beispiel wird das Durchschnittsgewicht aller Produkte gesucht. Alle NULL-Einträge in der `50`-Spalte der `Weight`-Tabelle werden durch den Wert `Product` ersetzt.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT AVG(ISNULL(Weight, 50))  
FROM Production.Product;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 -------------------------- 
59.79  
  
 (1 row(s) affected)
 ```  
  
### <a name="b-using-isnull"></a>B. Verwenden von ISNULL  
 Im folgenden Beispiel werden die Beschreibung, der Prozentsatz des Rabatts, die Mindestmenge und die Höchstmenge für alle Sonderangebote in `AdventureWorks2012` ausgewählt. Wenn die Höchstmenge für ein bestimmtes Sonderangebot NULL ist, wird für `MaxQty` im Resultset `0.00` angezeigt.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT Description, DiscountPct, MinQty, ISNULL(MaxQty, 0.00) AS 'Max Quantity'  
FROM Sales.SpecialOffer;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
|  Description       |  DiscountPct    |   MinQty    |   Höchstmenge       |
|  ---------------   |  -------------  |   --------  |   ---------------    |
|  No Discount       |  0.00           |   0         |   0                  |
|  Volume Discount   |  0,02           |   11        |   14                 |
|  Volume Discount   |  0.05           |   15        |   4                  |
|  Volume Discount   |  0,10           |   25        |   0                  |
|  Volume Discount   |  0.15           |   41        |   0                  |
|  Volume Discount   |  0,20           |   61        |   0                  |
|  Mountain-100 Cl   |  0,35           |   0         |   0                  |
|  Sport Helmet Di   |  0,10           |   0         |   0                  |
|  Road-650 Overst   |  0,30           |   0         |   0                  |
|  Mountain Tire S   |  0.50           |   0         |   0                  |
|  Sport Helmet Di   |  0.15           |   0         |   0                  |
|  LL Road Frame S   |  0,35           |   0         |   0                  |
|  Touring-3000 Pr   |  0.15           |   0         |   0                  |
|  Touring-1000 Pr   |  0,20           |   0         |   0                  |
|  Half-Price Peda   |  0.50           |   0         |   0                  |
|  Mountain-500 Si   |  0,40           |   0         |   0                  |

 `(16 row(s) affected)`  
  
### <a name="c-testing-for-null-in-a-where-clause"></a>C. Testen auf NULL in einer WHERE-Klausel  
 ISNULL sollte nicht für die Suche nach NULL-Werten verwendet werden. Verwenden Sie stattdessen IS NULL. Im folgenden Beispiel werden alle Produkte gesucht, die in der Weight-Spalte `NULL` enthalten. Beachten Sie den Leerraum zwischen `IS` und `NULL`.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT Name, Weight  
FROM Production.Product  
WHERE Weight IS NULL;  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Beispiele: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] und [!INCLUDE[ssPDW](../../includes/sspdw-md.md)].  
  
### <a name="d-using-isnull-with-avg"></a>D. Verwenden von ISNULL mit AVG  
 Im folgenden Beispiel wird das Durchschnittsgewicht aller Produkte in der selben Tabelle gesucht. Alle NULL-Einträge in der `50`-Spalte der `Weight`-Tabelle werden durch den Wert `Product` ersetzt.  
  
```  
-- Uses AdventureWorks  
  
SELECT AVG(ISNULL(Weight, 50))  
FROM dbo.DimProduct;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
--------------------------   
52.88   
```  
  
### <a name="e-using-isnull"></a>E. Verwenden von ISNULL  
 Im folgenden Beispiel wird ISNULL verwendet, um auf NULL-Werte in der Spalte `MinPaymentAmount` zu prüfen, und um den Wert `0.00` für diese Zeilen anzuzeigen.  
  
```  
-- Uses AdventureWorks  
  
SELECT ResellerName,   
       ISNULL(MinPaymentAmount,0) AS MinimumPayment  
FROM dbo.DimReseller  
ORDER BY ResellerName;  
  
```  
  
 Dies ist ein Auszug aus dem Resultset.  
  
|  ResellerName                |  MinimumPayment    |
|  -------------------------   |  --------------    |
|  A Bicycle Association       |     0,0000         |
|  A Bike Store                |     0,0000         |
|  A Cycle Shop                |     0,0000         |
|  A Great Bicycle Company     |     0,0000         |
|  A Typical Bike Shop         |   200,0000         |
|  Acceptable Sales & Service  |     0,0000         |
  
### <a name="f-using-is-null-to-test-for-null-in-a-where-clause"></a>F. Verwenden von IS NULL für die Überprüfung auf NULL in einer WHERE-Klausel  
 Im folgenden Beispiel werden alle Produkte gesucht, die in der `Weight`-Spalte `NULL` enthalten. Beachten Sie den Leerraum zwischen `IS` und `NULL`.  
  
```  
-- Uses AdventureWorks  
  
SELECT EnglishProductName, Weight  
FROM dbo.DimProduct  
WHERE Weight IS NULL;  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Ausdrücke &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [IS NULL &#40;Transact-SQL&#41;](../../t-sql/queries/is-null-transact-sql.md)   
 [Systemfunktionen &#40;Transact-SQL&#41;](../../relational-databases/system-functions/system-functions-for-transact-sql.md)   
 [WHERE &#40;Transact-SQL&#41;](../../t-sql/queries/where-transact-sql.md)   
 [COALESCE &#40;Transact-SQL&#41;](../../t-sql/language-elements/coalesce-transact-sql.md)  
  
  


---
title: ISNULL (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ISNULL
- ISNULL_TSQL
- IFNULL_TSQL
dev_langs: TSQL
helpviewer_keywords:
- replacing null values
- null values [SQL Server], ISNULL
- null values [SQL Server], replacement values
- ISNULL function
ms.assetid: 6f3e5802-864b-4e77-9862-657bb5430b68
caps.latest.revision: "42"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: ad067dd6df83e49c3a46fd5955945f79c20d1b96
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
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
 *"check_expression"*  
 Ist die [Ausdruck](../../t-sql/language-elements/expressions-transact-sql.md) auf NULL überprüft werden soll. *"check_expression"* kann einen beliebigen Typ sein.  
  
 *"replacement_value"*  
 Der Ausdruck, der zurückgegeben werden, wenn *"check_expression"* ist NULL. *"replacement_value"* muss ein Typ, der implizit in den Typ des *Check_expresssion*.  
  
## <a name="return-types"></a>Rückgabetypen  
 Gibt den gleichen Typ wie *"check_expression"*. Wenn eine literale NULL, als angegeben wird *"check_expression"*, gibt den Datentyp der *"replacement_value"*. Wenn eine literale NULL, als angegeben wird *"check_expression"* und keine *"replacement_value"* bereitgestellt wird, gibt ein **Int**.  
  
## <a name="remarks"></a>Hinweise  
 Der Wert der *"check_expression"* zurückgegeben wird, ist er nicht NULL ist, andernfalls *"replacement_value"* wird zurückgegeben, nachdem es implizit in den Typ konvertiert wird *"check_expression"*, wenn die Typen unterschiedlich sind. *"replacement_value"* können abgeschnitten werden, wenn *"replacement_value"* ist länger als *"check_expression"*.  
  
> [!NOTE]  
>  Verwendung [COALESCE &#40; Transact-SQL &#41; ](../../t-sql/language-elements/coalesce-transact-sql.md) der erste Wert ungleich Null zurückgegeben.  
  
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
  
|  Description       |  DiscountPct    |   MinQty    |   Maximale Menge       |
|  ---------------   |  -------------  |   --------  |   ---------------    |
|  No Discount       |  0.00           |   0         |   0                  |
|  Volume Discount   |  0.02           |   11        |   14                 |
|  Volume Discount   |  0.05           |   15        |   4                  |
|  Volume Discount   |  0.10           |   25        |   0                  |
|  Volume Discount   |  0.15           |   41        |   0                  |
|  Volume Discount   |  0.20           |   61        |   0                  |
|  Mountain-100 Cl   |  0.35           |   0         |   0                  |
|  Sport Helmet Di   |  0.10           |   0         |   0                  |
|  Road-650 Overst   |  0.30           |   0         |   0                  |
|  Mountain Tire, S   |  0.50           |   0         |   0                  |
|  Sport Helmet Di   |  0.15           |   0         |   0                  |
|  LL Road Frame S   |  0.35           |   0         |   0                  |
|  Touring-3000 Pr   |  0.15           |   0         |   0                  |
|  Touring-1000 Pr   |  0.20           |   0         |   0                  |
|  Halben Preis Peda   |  0.50           |   0         |   0                  |
|  Mountain-500 Si   |  0.40           |   0         |   0                  |

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
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Beispiele: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] und[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="d-using-isnull-with-avg"></a>D. Verwenden von ISNULL mit AVG  
 Das folgende Beispiel sucht den Durchschnitt der Gewichtung aller Produkte in eine Beispieltabelle enthält. Alle NULL-Einträge in der `50`-Spalte der `Weight`-Tabelle werden durch den Wert `Product` ersetzt.  
  
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
 Im folgenden Beispiel wird die ISNULL So testen Sie für NULL-Werte in der Spalte `MinPaymentAmount` und zeigt den Wert `0.00` für die Zeilen.  
  
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
|  Ein Fahrrad-Zuordnung       |     0.0000         |
|  Eine Bike Store                |     0.0000         |
|  Ein Zyklus kaufen                |     0.0000         |
|  Eine gute Bicycle Unternehmen     |     0.0000         |
|  Eine Typische Fahrrad kaufen         |   200.0000         |
|  Akzeptable Vertriebs- und Dienst  |     0.0000         |
  
### <a name="f-using-is-null-to-test-for-null-in-a-where-clause"></a>F. Verwenden Sie IS NULL für NULL-Zeichen in einer WHERE-Klausel testen  
 Das folgende Beispiel findet alle Produkte mit `NULL` in der `Weight` Spalte. Beachten Sie den Leerraum zwischen `IS` und `NULL`.  
  
```  
-- Uses AdventureWorks  
  
SELECT EnglishProductName, Weight  
FROM dbo.DimProduct  
WHERE Weight IS NULL;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Ausdrücke &#40; Transact-SQL &#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [IST NULL &#40; Transact-SQL &#41;](../../t-sql/queries/is-null-transact-sql.md)   
 [Systemfunktionen &#40;Transact-SQL&#41;](../../relational-databases/system-functions/system-functions-for-transact-sql.md)   
 [WOBEI &#40; Transact-SQL &#41;](../../t-sql/queries/where-transact-sql.md)   
 [COALESCE &#40; Transact-SQL &#41;](../../t-sql/language-elements/coalesce-transact-sql.md)  
  
  


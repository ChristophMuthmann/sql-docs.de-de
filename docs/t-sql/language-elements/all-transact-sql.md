---
title: ALL (Transact-SQL) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- Azure SQL Database
- SQL Server (starting with 2008)
f1_keywords:
- ALL_TSQL
- ALL
dev_langs:
- TSQL
helpviewer_keywords:
- single-column set of values [SQL Server]
- ALL (Transact-SQL)
ms.assetid: 4b0c002e-1ffd-4425-a980-11fdc1f24af7
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 142fbd5b352a73e382f89a61f60fba6373902172
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="all-transact-sql"></a>ALL (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Vergleicht einen Skalarwert mit Werten, die sich in einer einzelnen Spalte befinden.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
scalar_expression { = | <> | != | > | >= | !> | < | <= | !< } ALL ( subquery )  
```  
  
## <a name="arguments"></a>Argumente  
 *scalar_expression*  
 Ein gültiger [Ausdruck](../../t-sql/language-elements/expressions-transact-sql.md)  
  
 { = | <> | != | > | >= | !> | < | <= | !< }  
 Ein Vergleichsoperator  
  
 *subquery*  
 Eine Unterabfrage, die ein Resultset einer Spalte zurückgibt. Der Datentyp der zurückgegebenen Spalte muss dem Datentyp von *scalar_expression* entsprechen.  
  
 Ist eine beschränkte SELECT-Anweisung, in der die ORDER BY-Klausel und das INTO-Schlüsselwort nicht zulässig sind.  
  
## <a name="result-types"></a>Ergebnistypen  
 **Boolean**  
  
## <a name="result-value"></a>Ergebniswert  
 Gibt TRUE zurück, wenn der angegebene Vergleich für alle Paare (*scalar_expression***,***x)* TRUE ergibt, wenn *x* ein Wert im Einspaltensatz ist. Andernfalls wird FALSE zurückgegeben.  
  
## <a name="remarks"></a>Remarks  
 ALL erfordert, dass der Vergleich von *scalar_expression* mit jedem der von der Unterabfrage zurückgegebenen Wert positiv ausfällt. Wenn die Unterabfrage beispielsweise die Werte 2 und 3 zurückgibt, ergibt *scalar_expression* <= ALL (Unterabfrage) für *scalar_expression* = 2 TRUE. Wenn die Unterabfrage beispielsweise die Werte 2 und 3 zurückgibt, ergibt *scalar_expression* = ALL (Unterabfrage) FALSE, da einige Werte der Unterabfrage (der Wert 3) die Kriterien des Ausdrucks nicht erfüllen.  
  
 Anweisungen, die erfordern, dass *scalar_expression* mit nur einem von der Unterabfrage zurückgegebenen Wert positiv verglichen wird, finden Sie unter [SOME &#124; ANY &#40;Transact-SQL&#41;](../../t-sql/language-elements/some-any-transact-sql.md).  
  
 Dieses Thema bezieht sich auf ALL bei Verwendung mit einer Unterabfrage. ALL kann auch mit [UNION](../../t-sql/language-elements/set-operators-union-transact-sql.md) und [SELECT](../../t-sql/queries/select-transact-sql.md) verwendet werden.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird eine gespeicherte Prozedur erstellt, die bestimmt, ob alle Komponenten einer angegebenen `SalesOrderID` in der [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]-Datenbank innerhalb der angegebenen Anzahl von Tagen gefertigt werden können. Im Beispiel wird eine Unterabfrage verwendet, um eine Liste mit der Anzahl des `DaysToManufacture`-Wertes für alle Komponenten der bestimmten `SalesOrderID` zu erstellen. Anschließend wird bestätigt, dass alle `DaysToManufacture` innerhalb der Anzahl der angegebenen Tage liegen.  
  
```  
-- Uses AdventureWorks  
  
CREATE PROCEDURE DaysToBuild @OrderID int, @NumberOfDays int  
AS  
IF   
@NumberOfDays >= ALL  
   (  
    SELECT DaysToManufacture  
    FROM Sales.SalesOrderDetail  
    JOIN Production.Product   
    ON Sales.SalesOrderDetail.ProductID = Production.Product.ProductID   
    WHERE SalesOrderID = @OrderID  
   )  
PRINT 'All items for this order can be manufactured in specified number of days or less.'  
ELSE   
PRINT 'Some items for this order cannot be manufactured in specified number of days or less.' ;  
  
```  
  
 Zum Testen der Prozedur führen Sie die Prozedur aus, indem Sie die `SalesOrderID 49080` verwenden, die über eine Komponente verfügt, die `2` Tage erfordert und über zwei Komponenten verfügt, die 0 Tage erfordern. Die erste im Folgenden genannte Anweisung erfüllt die Kriterien. Die zweite Abfrage erfüllt sie nicht.  
  
```  
EXECUTE DaysToBuild 49080, 2 ;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `All items for this order can be manufactured in specified number of days or less.`  
  
```  
EXECUTE DaysToBuild 49080, 1 ;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `Some items for this order cannot be manufactured in specified number of days or less.`  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [CASE &#40;Transact-SQL&#41;](../../t-sql/language-elements/case-transact-sql.md)   
 [Ausdrücke &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [Integrierte Funktionen &#40;Transact-SQL&#41;](~/t-sql/functions/functions.md)   
 [LIKE &#40;Transact-SQL&#41;](../../t-sql/language-elements/like-transact-sql.md)   
 [Operators &#40;Transact-SQL&#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [WHERE &#40;Transact-SQL&#41;](../../t-sql/queries/where-transact-sql.md)   
 [IN &#40;Transact-SQL&#41;](../../t-sql/language-elements/in-transact-sql.md)  
  
  

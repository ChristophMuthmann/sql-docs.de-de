---
title: SOME | ANY (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: t-sql|language-elements
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- Azure SQL Database
- SQL Server (starting with 2008)
f1_keywords:
- SOME
- SOME_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- scalar values
- comparing scalar with single-column set
- ANY operator
- SOME | ANY keyword
- single-column set of values [SQL Server]
ms.assetid: 1f717ad6-f67b-4980-9397-577ecb0e5789
caps.latest.revision: 41
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 0a79c7a06edb70b694481e4c30b0244ebd39e2ef
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="some--any-transact-sql"></a>SOME | ANY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Vergleicht einen Skalarwert mit Werten, die sich in einer einzelnen Spalte befinden. SOME und ANY sind identisch.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
scalar_expression { = | < > | ! = | > | > = | ! > | < | < = | ! < }   
     { SOME | ANY } ( subquery )   
```  
  
## <a name="arguments"></a>Argumente  
 *scalar_expression*  
 Ein gültiger [Ausdruck](../../t-sql/language-elements/expressions-transact-sql.md)  
  
 { = | <> | != | > | >= | !> | < | <= | !< }  
 Ein gültiger Vergleichsoperator.  
  
 SOME | ANY  
 Legt fest, dass ein Vergleich durchgeführt werden soll.  
  
 *subquery*  
 Ist eine Unterabfrage mit einem Resultset, das aus einer Spalte besteht. Der Datentyp der zurückgegebenen Spalte muss mit dem Datentyp von *scalar_expression* übereinstimmen.  
  
## <a name="result-types"></a>Ergebnistypen  
 **Boolean**  
  
## <a name="result-value"></a>Ergebniswert  
 SOME oder ANY geben **TRUE** zurück, wenn der angegebene Vergleich für ein Paar (*scalar_expression ***,*** x*) TRUE ergibt, wenn *x* ein Wert im Einspaltensatz ist. Andernfalls wird **FALSE** zurückgegeben.  
  
## <a name="remarks"></a>Remarks  
 SOME erfordert, dass *scalar_expression* mit mindestens einem von der Unterabfrage zurückgegebenen Wert positiv verglichen wird. Anweisungen, die erfordern, dass *scalar_expression* mit jedem von der Unterabfrage zurückgegebenen Wert positiv verglichen wird, finden Sie unter [ALL &#40;Transact-SQL&#41;](../../t-sql/language-elements/all-transact-sql.md). Wenn die Unterabfrage beispielsweise die Werte 2 und 3 zurückgibt, ergibt *scalar_expression* = SOME (Unterabfrage) für *scalar_express* = 2 TRUE. Wenn die Unterabfrage beispielsweise die Werte 2 und 3 zurückgibt, ergibt *scalar_expression* = ALL (Unterabfrage) FALSE, da einige Werte der Unterabfrage (der Wert 3) die Kriterien des Ausdrucks nicht erfüllen.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-running-a-simple-example"></a>A. Ausführen eines einfachen Beispiels  
 Mit den folgenden Anweisungen wird eine einfache Tabelle erstellt, und der `1`-Spalte werden die Werte `2`, `3`, `4` und `ID` hinzugefügt.  
  
```  
CREATE TABLE T1  
(ID int) ;  
GO  
INSERT T1 VALUES (1) ;  
INSERT T1 VALUES (2) ;  
INSERT T1 VALUES (3) ;  
INSERT T1 VALUES (4) ;  
```  
  
 Die folgende Abfrage gibt `TRUE` zurück, da `3` kleiner als einige der Werte in der Tabelle ist.  
  
```  
IF 3 < SOME (SELECT ID FROM T1)  
PRINT 'TRUE'   
ELSE  
PRINT 'FALSE' ;  
```  
  
 Die folgende Abfrage gibt `FALSE` zurück, da `3` nicht kleiner als sämtliche Werte in der Tabelle ist.  
  
```  
IF 3 < ALL (SELECT ID FROM T1)  
PRINT 'TRUE'   
ELSE  
PRINT 'FALSE' ;  
```  
  
### <a name="b-running-a-practical-example"></a>B. Ausführen eines praktischen Beispiels  
 Im folgenden Beispiel wird eine gespeicherte Prozedur erstellt, die bestimmt, ob alle Komponenten einer angegebenen `SalesOrderID` in der `AdventureWorks2012`-Datenbank innerhalb der angegebenen Anzahl von Tagen gefertigt werden können. Im Beispiel wird eine Unterabfrage verwendet, um eine Liste mit der Anzahl der `DaysToManufacture`-Werte für alle Komponenten einer bestimmten `SalesOrderID` zu erstellen. Anschließend wird geprüft, ob einer der von der Unterabfrage zurückgegebenen Werte größer ist als die Anzahl der angegebenen Tage. Wenn jeder Wert von `DaysToManufacture`, der zurückgegeben wird, kleiner ist als die angegebene Anzahl, ist die Bedingung TRUE, und die erste Meldung wird ausgegeben.  
  
```  
-- Uses AdventureWorks  
  
CREATE PROCEDURE ManyDaysToComplete @OrderID int, @NumberOfDays int  
AS  
IF   
@NumberOfDays < SOME  
   (  
    SELECT DaysToManufacture  
    FROM Sales.SalesOrderDetail  
    JOIN Production.Product   
    ON Sales.SalesOrderDetail.ProductID = Production.Product.ProductID   
    WHERE SalesOrderID = @OrderID  
   )  
PRINT 'At least one item for this order cannot be manufactured in specified number of days.'  
ELSE   
PRINT 'All items for this order can be manufactured in the specified number of days or less.' ;  
  
```  
  
 Zum Testen der Prozedur führen Sie diese aus, indem Sie die `SalesOrderID``49080` verwenden, die über eine Komponente verfügt, die `2` Tage erfordert, und über zwei Komponenten, die 0 Tage erfordern. Die erste Anweisung erfüllt die Kriterien. Die zweite Abfrage erfüllt sie nicht.  
  
```  
EXECUTE ManyDaysToComplete 49080, 2 ;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `All items for this order can be manufactured in the specified number of days or less.`  
  
```  
EXECUTE ManyDaysToComplete 49080, 1 ;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `At least one item for this order cannot be manufactured in specified number of days.`  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [ALL &#40;Transact-SQL&#41;](../../t-sql/language-elements/all-transact-sql.md)   
 [CASE &#40;Transact-SQL&#41;](../../t-sql/language-elements/case-transact-sql.md)   
 [Integrierte Funktionen &#40;Transact-SQL&#41;](~/t-sql/functions/functions.md)   
 [Operatoren &#40;Transact-SQL&#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [WHERE &#40;Transact-SQL&#41;](../../t-sql/queries/where-transact-sql.md)   
 [IN &#40;Transact-SQL&#41;](../../t-sql/language-elements/in-transact-sql.md)  
  
  

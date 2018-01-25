---
title: EINIGE | Alle (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- Azure SQL Database
- SQL Server (starting with 2008)
f1_keywords:
- SOME
- SOME_TSQL
dev_langs: TSQL
helpviewer_keywords:
- scalar values
- comparing scalar with single-column set
- ANY operator
- SOME | ANY keyword
- single-column set of values [SQL Server]
ms.assetid: 1f717ad6-f67b-4980-9397-577ecb0e5789
caps.latest.revision: "41"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: d81a0d9fb87a11aa7bc109c003d7b723c20c8e77
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
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
 Ist ein beliebiger gültiger [Ausdruck](../../t-sql/language-elements/expressions-transact-sql.md).  
  
 { = | <> | != | > | >= | !> | < | <= | !< }  
 Ein gültiger Vergleichsoperator.  
  
 SOME | ANY  
 Legt fest, dass ein Vergleich durchgeführt werden soll.  
  
 *subquery*  
 Ist eine Unterabfrage mit einem Resultset, das aus einer Spalte besteht. Der Datentyp der zurückgegebenen Spalte muss denselben Datentyp wie *"scalar_expression"*.  
  
## <a name="result-types"></a>Ergebnistypen  
 **Boolean**  
  
## <a name="result-value"></a>Ergebniswert  
 SOME oder ANY gibt **"true"** Wenn der angegebene Vergleich "true" ist für ein beliebiges Paar (*"scalar_expression"***,***x*), in denen *x* ist ein Wert in der einspaltigen Resultset; andernfalls gibt **"false"**.  
  
## <a name="remarks"></a>Hinweise  
 SOME erfordert, dass die *"scalar_expression"* auf mindestens ein von der Unterabfrage zurückgegebenen Wert positiv verglichen. Für Anweisungen, benötigen die *"scalar_expression"* positiv zu den einzelnen Werten verglichen, die von der Unterabfrage zurückgegeben wird, finden Sie unter [alle &#40; Transact-SQL &#41; ](../../t-sql/language-elements/all-transact-sql.md). Für die Instanz, wenn die Unterabfrage die Werte 2 und 3 zurückgibt *"scalar_expression"* = SOME (Unterabfrage) für "true" ausgewertet einen *Scalar_express* von 2. Wenn die Unterabfrage die Werte 2 und 3 zurückgibt *"scalar_expression"* = ALL (Unterabfrage) als "false" ausgewertet, da einige der Werte der Unterabfrage (der Wert von 3) die Kriterien des Ausdrucks nicht erfüllen.  
  
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
 Das folgende Beispiel erstellt eine gespeicherte Prozedur, der bestimmt, ob alle Komponenten einer angegebenen `SalesOrderID` in der `AdventureWorks2012` Datenbank in die angegebene Anzahl von Tagen gefertigt werden kann. Im Beispiel wird eine Unterabfrage verwendet, um eine Liste mit der Anzahl der `DaysToManufacture`-Werte für alle Komponenten einer bestimmten `SalesOrderID` zu erstellen. Anschließend wird geprüft, ob einer der von der Unterabfrage zurückgegebenen Werte größer ist als die Anzahl der angegebenen Tage. Wenn jeder Wert von `DaysToManufacture`, der zurückgegeben wird, kleiner ist als die angegebene Anzahl, ist die Bedingung TRUE, und die erste Meldung wird ausgegeben.  
  
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
  
 Zum Testen der Prozedur führen Sie die Prozedur mit der `SalesOrderID``49080`, die eine Komponente, die benötigt wurde `2` Tage und zwei Komponenten, die 0 Tage erfordern. Die erste Anweisung erfüllt die Kriterien. Die zweite Abfrage erfüllt sie nicht.  
  
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
  
## <a name="see-also"></a>Siehe auch  
 [ALL &#40;Transact-SQL&#41;](../../t-sql/language-elements/all-transact-sql.md)   
 [CASE &#40;Transact-SQL&#41;](../../t-sql/language-elements/case-transact-sql.md)   
 [Integrierte Funktionen &#40;Transact-SQL&#41;](~/t-sql/functions/functions.md)   
 [Operators &#40;Transact-SQL&#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [WHERE &#40;Transact-SQL&#41;](../../t-sql/queries/where-transact-sql.md)   
 [IN &#40;Transact-SQL&#41;](../../t-sql/language-elements/in-transact-sql.md)  
  
  

---
title: Alle (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
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
caps.latest.revision: 40
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 1fd1b250a30b83a3b014384aafee6c40ff4f1a5a
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="all-transact-sql"></a>ALL (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Vergleicht einen Skalarwert mit Werten, die sich in einer einzelnen Spalte befinden.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
scalar_expression { = | <> | != | > | >= | !> | < | <= | !< } ALL ( subquery )  
```  
  
## <a name="arguments"></a>Argumente  
 *"scalar_expression"*  
 Ist ein beliebiger gültiger [Ausdruck](../../t-sql/language-elements/expressions-transact-sql.md).  
  
 { = | <> | != | > | >= | !> | < | <= | !< }  
 Ist ein Vergleichsoperator.  
  
 *Unterabfrage*  
 Eine Unterabfrage, die ein Resultset einer Spalte zurückgibt. Der Datentyp der zurückgegebenen Spalte muss den gleichen Datentyp wie der Datentyp des *"scalar_expression"*.  
  
 Ist eine beschränkte SELECT-Anweisung, in der die ORDER BY-Klausel und das INTO-Schlüsselwort nicht zulässig sind.  
  
## <a name="result-types"></a>Ergebnistypen  
 **Boolean**  
  
## <a name="result-value"></a>Ergebniswert  
 Gibt "true" zurück, wenn der angegebene Vergleich "true" ist für alle Paare (*"scalar_expression"***,***X)*Wenn *x* ist ein Wert in der einspaltigen Resultset; Andernfalls wird "false" zurückgegeben.  
  
## <a name="remarks"></a>Hinweise  
 ALL erfordert die *"scalar_expression"* zu jedem Wert positiv verglichen, die von der Unterabfrage zurückgegeben wird. Für die Instanz, wenn die Unterabfrage die Werte 2 und 3 zurückgibt *"scalar_expression"* < = ALL (Unterabfrage) für "true" ausgewertet einen *"scalar_expression"* von 2. Wenn die Unterabfrage die Werte 2 und 3 zurückgibt *"scalar_expression"* = ALL (Unterabfrage) als "false" ausgewertet, da einige der Werte der Unterabfrage (der Wert von 3) die Kriterien des Ausdrucks nicht erfüllen.  
  
 Für Anweisungen, benötigen die *"scalar_expression"* zum einzigen Wert positiv verglichen, die von der Unterabfrage zurückgegeben wird, finden Sie unter [einige &#124; Alle &#40; Transact-SQL &#41; ](../../t-sql/language-elements/some-any-transact-sql.md).  
  
 Dieses Thema bezieht sich auf ALL bei Verwendung mit einer Unterabfrage. Alle auch verwendet werden können [UNION](../../t-sql/language-elements/set-operators-union-transact-sql.md) und [wählen](../../t-sql/queries/select-transact-sql.md).  
  
## <a name="examples"></a>Beispiele  
 Das folgende Beispiel erstellt eine gespeicherte Prozedur, der bestimmt, ob alle Komponenten einer angegebenen `SalesOrderID` in der [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] Datenbank in die angegebene Anzahl von Tagen gefertigt werden kann. Im Beispiel wird eine Unterabfrage verwendet, um eine Liste mit der Anzahl des `DaysToManufacture`-Wertes für alle Komponenten der bestimmten `SalesOrderID` zu erstellen. Anschließend wird bestätigt, dass alle `DaysToManufacture` innerhalb der Anzahl der angegebenen Tage liegen.  
  
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
  
## <a name="see-also"></a>Siehe auch  
 [Groß-/KLEINSCHREIBUNG &#40; Transact-SQL &#41;](../../t-sql/language-elements/case-transact-sql.md)   
 [Ausdrücke &#40; Transact-SQL &#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [Integrierte Funktionen &#40;Transact-SQL&#41;](~/t-sql/functions/functions.md)   
 [WIE &#40; Transact-SQL &#41;](../../t-sql/language-elements/like-transact-sql.md)   
 [Operatoren &#40; Transact-SQL &#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [WOBEI &#40; Transact-SQL &#41;](../../t-sql/queries/where-transact-sql.md)   
 [SOF &#40; Transact-SQL &#41;](../../t-sql/language-elements/in-transact-sql.md)  
  
  


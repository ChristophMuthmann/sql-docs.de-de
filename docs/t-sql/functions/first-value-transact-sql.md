---
title: FIRST_VALUE-Funktion (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 11/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- FIRST_VALUE_TSQL
- FIRST_VALUE
dev_langs:
- TSQL
helpviewer_keywords:
- FIRST_VALUE function
- analytic functions, FIRST_VALUE
ms.assetid: 1990c3c7-dad2-48db-b2cd-3e8bd2c49d17
caps.latest.revision: 15
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: ea4c10a63ec38eebd7f1f6f9d318742c9891c3ed
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="firstvalue-transact-sql"></a>FIRST_VALUE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all-md](../../includes/tsql-appliesto-ss2012-all-md.md)]

  Gibt den ersten Wert in einer geordneten Menge von Werten in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] zurück.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
FIRST_VALUE ( [scalar_expression ] )   
    OVER ( [ partition_by_clause ] order_by_clause [ rows_range_clause ] )  
  
```  
  
## <a name="arguments"></a>Argumente  
 *"scalar_expression"*  
 Der zurückzugebende Wert. *"scalar_expression"* kann eine Spalte, Unterabfrage oder anderer willkürlicher Ausdruck sein, die sich in einem einzelnen Wert ergibt. Andere analytische Funktionen sind nicht zulässig.  
  
 ÜBER **(** [ *Partition_by_clause* ] *Order_by_clause* [ *Rows_range_clause* ] **)**  
 *Partition_by_clause* teilt das Resultset, das von der FROM-Klausel erstellt wird, in Partitionen, die auf die die Funktion angewendet wird. Wird dies nicht angegeben, verarbeitet die Funktion alle Zeilen des Abfrageresultsets als einzelne Gruppe. *Order_by_clause* bestimmt die logische Reihenfolge, in dem der Vorgang ausgeführt wird. *Order_by_clause* ist erforderlich. *Rows_range_clause* weiter schränkt die Zeilen in der Partition durch Angabe der Start- und Endpunkt. Weitere Informationen finden Sie unter [Klausel "OVER" &#40; Transact-SQL &#41; ](../../t-sql/queries/select-over-clause-transact-sql.md).  
  
## <a name="return-types"></a>Rückgabetypen  
 Ist vom selben Typ wie *"scalar_expression"*.  
  
## <a name="general-remarks"></a>Allgemeine Hinweise  
 FIRST_VALUE ist nicht deterministisch. Weitere Informationen finden Sie unter [Deterministic and Nondeterministic Functions](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md).  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-using-firstvalue-over-a-query-result-set"></a>A. Verwenden von FIRST_VALUE für ein Abfrageresultset  
 Im folgenden Beispiel wird der Name des günstigsten Produkts in einer bestimmten Produktkategorie mithilfe von FIRST_VALUE zurückgegeben.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT Name, ListPrice,   
       FIRST_VALUE(Name) OVER (ORDER BY ListPrice ASC) AS LeastExpensive   
FROM Production.Product  
WHERE ProductSubcategoryID = 37;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
  
Name                    ListPrice             LeastExpensive  
----------------------- --------------------- --------------------  
Patch Kit/8 Patches     2.29                  Patch Kit/8 Patches  
Road Tire Tube          3.99                  Patch Kit/8 Patches  
Touring Tire Tube       4.99                  Patch Kit/8 Patches  
Mountain Tire Tube      4.99                  Patch Kit/8 Patches  
LL Road Tire            21.49                 Patch Kit/8 Patches  
ML Road Tire            24.99                 Patch Kit/8 Patches  
LL Mountain Tire        24.99                 Patch Kit/8 Patches  
Touring Tire            28.99                 Patch Kit/8 Patches  
ML Mountain Tire        29.99                 Patch Kit/8 Patches  
HL Road Tire            32.60                 Patch Kit/8 Patches  
HL Mountain Tire        35.00                 Patch Kit/8 Patches  
  
```  
  
### <a name="b-using-firstvalue-over-partitions"></a>B. Verwenden von FIRST_VALUE über Partitionen  
 Im folgenden Beispiel werden die Mitarbeiter mit der geringsten Anzahl von Urlaubsstunden im Vergleich zu anderen Angestellten mit der gleichen Berufsbezeichnung mithilfe von FIRST_VALUE zurückgegeben. Die PARTITION BY-Klausel partitioniert die Mitarbeiter nach Berufsbezeichnung, und die FIRST_VALUE-Funktion wird unabhängig auf jede Partition angewendet. Die in der OVER-Klausel angegebene ORDER BY-Klausel bestimmt die logische Reihenfolge, in der die FIRST_VALUE-Funktion auf die Zeilen in jeder Partition angewendet wird. Die ROWS UNBOUNDED PRECEDING-Klausel gibt den Ausgangspunkt des Fensters als erste Zeile jeder Partition an.  
  
```  
USE AdventureWorks2012;   
GO  
SELECT JobTitle, LastName, VacationHours,   
       FIRST_VALUE(LastName) OVER (PARTITION BY JobTitle   
                                   ORDER BY VacationHours ASC  
                                   ROWS UNBOUNDED PRECEDING  
                                  ) AS FewestVacationHours  
FROM HumanResources.Employee AS e  
INNER JOIN Person.Person AS p   
    ON e.BusinessEntityID = p.BusinessEntityID  
ORDER BY JobTitle;  
```  
  
 Dies ist ein Auszug aus dem Resultset.  
  
```  
  
JobTitle                            LastName                  VacationHours FewestVacationHours  
----------------------------------- ------------------------- ------------- -------------------  
Accountant                          Moreland                  58            Moreland  
Accountant                          Seamans                   59            Moreland  
Accounts Manager                    Liu                       57            Liu  
Accounts Payable Specialist         Tomic                     63            Tomic  
Accounts Payable Specialist         Sheperdigian              64            Tomic  
Accounts Receivable Specialist      Poe                       60            Poe  
Accounts Receivable Specialist      Spoon                     61            Poe  
Accounts Receivable Specialist      Walton                    62            Poe  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Failover-Klausel &#40; Transact-SQL &#41;](../../t-sql/queries/select-over-clause-transact-sql.md)  
  
  


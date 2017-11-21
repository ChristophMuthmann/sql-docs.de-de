---
title: PERCENT_RANK (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 10/20/2015
ms.prod: sql-non-specified
ms.prod_service: sql-data-warehouse, database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- PERCENT_RANK_TSQL
- PERCENT_RANK
dev_langs:
- TSQL
helpviewer_keywords:
- PERCENT_RANK function
- analytic functions, PERCENT_RANK
ms.assetid: e361c2d4-c01f-4da4-8e89-1ddc724a2629
caps.latest.revision: 14
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 8c789a5cd6fc0e438a4e35ade9ccc4c5b849367b
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="percentrank-transact-sql"></a>PERCENT_RANK (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-asdw-xxx-md.md)]

  Berechnet den relativen Rang einer Zeile innerhalb einer Gruppe von Zeilen in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Mit PERCENT_RANK können Sie den relativen Rang eines Werts innerhalb eines Abfrageresultsets oder einer Partition ermitteln. PERCENT_RANK ähnelt der CUME_DIST-Funktion.  
  
## <a name="syntax"></a>Syntax  
  
```  
PERCENT_RANK( )  
    OVER ( [ partition_by_clause ] order_by_clause )  
  
```  
  
## <a name="arguments"></a>Argumente  
 ÜBER **(** [ *Partition_by_clause* ] *Order_by_clause***)**  
 *Partition_by_clause* teilt das Resultset, das von der FROM-Klausel erstellt wird, in Partitionen, die auf die die Funktion angewendet wird. Wird dies nicht angegeben, verarbeitet die Funktion alle Zeilen des Abfrageresultsets als einzelne Gruppe. *Order_by_clause* bestimmt die logische Reihenfolge, in dem der Vorgang ausgeführt wird. Die *Order_by_clause* ist erforderlich. Die \<Zeilen- oder Bereichsklausel > der OVER-Syntax kann nicht in einer PERCENT_RANK-Funktion angegeben werden.  Weitere Informationen finden Sie unter [Klausel "OVER" &#40; Transact-SQL &#41; ](../../t-sql/queries/select-over-clause-transact-sql.md).  
  
## <a name="return-types"></a>Rückgabetypen  
 **float(53)**  
  
## <a name="general-remarks"></a>Allgemeine Hinweise  
 Der von PERCENT_RANK zurückgegebene Wertebereich ist größer als 0 und kleiner oder gleich 1. Die erste Zeile in einem Satz hat einen PERCENT_RANK von 0. NULL-Werte sind standardmäßig eingeschlossen und werden als niedrigste mögliche Werte behandelt.  
  
 PERCENT_RANK ist nicht deterministisch. Weitere Informationen finden Sie unter [Deterministic and Nondeterministic Functions](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md).  
  
## <a name="examples"></a>Beispiele  
 Das folgende Beispiel berechnet das Gehaltsquantil für jeden Mitarbeiter innerhalb einer angegebenen Abteilung mithilfe der CUME_DIST-Funktion. Der von der CUME_DIST-Funktion zurückgegebene Wert stellt den Prozentsatz der Mitarbeiter dar, deren Gehalt kleiner oder gleich dem des aktuellen Mitarbeiters in derselben Abteilung ist. Die PERCENT_RANK-Funktion berechnet den Rang des Gehalts des Mitarbeiters innerhalb einer Abteilung als Prozentsatz. Um die Zeilen im Resultset nach Abteilung zu partitionieren, wird die PARTITION BY-Klausel angegeben. Die ORDER BY-Klausel in der OVER-Klausel sortiert die Zeilen in jeder Partition. Die ORDER BY-Klausel in der SELECT-Anweisung sortiert die Zeilen im gesamten Resultset.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT Department, LastName, Rate,   
       CUME_DIST () OVER (PARTITION BY Department ORDER BY Rate) AS CumeDist,   
       PERCENT_RANK() OVER (PARTITION BY Department ORDER BY Rate ) AS PctRank  
FROM HumanResources.vEmployeeDepartmentHistory AS edh  
    INNER JOIN HumanResources.EmployeePayHistory AS e    
    ON e.BusinessEntityID = edh.BusinessEntityID  
WHERE Department IN (N'Information Services',N'Document Control')   
ORDER BY Department, Rate DESC;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
  
Department             LastName               Rate                  CumeDist               PctRank  
---------------------- ---------------------- --------------------- ---------------------- ----------------------  
Document Control       Arifin                 17.7885               1                      1  
Document Control       Norred                 16.8269               0.8                    0.5  
Document Control       Kharatishvili          16.8269               0.8                    0.5  
Document Control       Chai                   10.25                 0.4                    0  
Document Control       Berge                  10.25                 0.4                    0  
Information Services   Trenary                50.4808               1                      1  
Information Services   Conroy                 39.6635               0.9                    0.888888888888889  
Information Services   Ajenstat               38.4615               0.8                    0.666666666666667  
Information Services   Wilson                 38.4615               0.8                    0.666666666666667  
Information Services   Sharma                 32.4519               0.6                    0.444444444444444  
Information Services   Connelly               32.4519               0.6                    0.444444444444444  
Information Services   Berg                   27.4038               0.4                    0  
Information Services   Meyyappan              27.4038               0.4                    0  
Information Services   Bacon                  27.4038               0.4                    0  
Information Services   Bueno                  27.4038               0.4                    0  
(15 row(s) affected)  
```  
  
## <a name="see-also"></a>Siehe auch  
 [CUME_DIST &#40; Transact-SQL &#41;](../../t-sql/functions/cume-dist-transact-sql.md)  
  
  


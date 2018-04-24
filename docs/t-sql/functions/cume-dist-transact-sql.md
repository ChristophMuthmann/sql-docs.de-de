---
title: CUME_DIST (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: sql-data-warehouse, database-engine, sql-database
ms.service: ''
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- CUME_DIST
- CUME_DIST_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CUME_DIST function
- analytic functions, CUME_DIST
ms.assetid: 491b07f3-9ffd-4cdd-93e5-5abb636fc5ef
caps.latest.revision: 19
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
monikerRange: = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: cc8aa5d921d0d72dc32453143c42a29c28a553b3
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="cumedist-transact-sql"></a>CUME_DIST (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-asdw-xxx-md.md)]

Berechnet die kumulierte Verteilung eines Werts innerhalb einer Gruppe von Werte in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. CUME_DIST berechnet somit die relative Position eines angegebenen Werts in einer Gruppe von Werten. Für eine Zeile *r* bei aufsteigender Reihenfolge entspricht der CUME_DIST-Wert von *r* der Anzahl der Zeilen mit Werten, die niedriger oder gleich dem Wert von *r*, geteilt durch die Anzahl der in der Partition oder dem Abfrageresultset ausgewerteten Zeilen sind. CUME_DIST ähnelt der PERCENT_RANK-Funktion.
  
![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Syntax  
  
```sql
CUME_DIST( )  
    OVER ( [ partition_by_clause ] order_by_clause )  
  
```  
  
## <a name="arguments"></a>Argumente  
OVER **(** [ *partition_by_clause* ] *order_by_clause***)**  
*partition_by_clause* unterteilt das von der FROM-Klausel erzeugte Resultset in Partitionen, auf die die Funktion angewendet wird. Wird dies nicht angegeben, verarbeitet die Funktion alle Zeilen des Abfrageresultsets als einzelne Gruppe. *order_by_clause* bestimmt die logische Reihenfolge, in der der Vorgang ausgeführt wird. *order_by_clause* ist erforderlich. Die \<Zeilen- oder Bereichsklausel> der OVER-Syntax kann für die CUME_DIST-Funktion nicht angegeben werden. Weitere Informationen finden Sie unter [OVER-Klausel &#40;Transact-SQL&#41;](../../t-sql/queries/select-over-clause-transact-sql.md).
  
## <a name="return-types"></a>Rückgabetypen
**float(53)**
  
## <a name="remarks"></a>Remarks  
Der von CUME_DIST zurückgegebene Wertebereich ist größer als 0 und kleiner oder gleich 1. Gleichwertige Werte ergeben immer den gleichen kumulierten Verteilungswert. NULL-Werte sind standardmäßig eingeschlossen und werden als niedrigste mögliche Werte behandelt.
  
CUME_DIST ist nicht deterministisch. Weitere Informationen finden Sie unter [Deterministic and Nondeterministic Functions](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md).
  
## <a name="examples"></a>Beispiele  
Das folgende Beispiel berechnet das Gehaltsquantil für jeden Mitarbeiter innerhalb einer angegebenen Abteilung mithilfe der CUME_DIST-Funktion. Der von der CUME_DIST-Funktion zurückgegebene Wert stellt den Prozentsatz der Mitarbeiter dar, deren Gehalt kleiner oder gleich dem des aktuellen Mitarbeiters in derselben Abteilung ist. Die PERCENT_RANK-Funktion berechnet den prozentualen Rang des Gehalts des Mitarbeiters innerhalb einer Abteilung. Um die Zeilen im Resultset nach Abteilung zu partitionieren, wird die PARTITION BY-Klausel angegeben. Die ORDER BY-Klausel in der OVER-Klausel sortiert die Zeilen in jeder Partition logisch. Die ORDER BY-Klausel in der SELECT-Anweisung bestimmt die Anzeigereihenfolge des Resultsets.
  
```sql
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
  
```sql
  
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
[PERCENT_RANK &#40;Transact-SQL&#41;](../../t-sql/functions/percent-rank-transact-sql.md)
  
  

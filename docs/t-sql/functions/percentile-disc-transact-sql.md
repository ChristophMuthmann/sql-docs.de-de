---
title: PERCENTILE_DISC (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 10/20/2015
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
- PERCENTILE_DISC
- PERCENTILE_DISC_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- PERCENTILE_DISC function
- analytic functions,PERCENTILE_DISC
ms.assetid: b545413d-c4f7-4c8e-8617-607599a26680
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: a1e7ebdd2303108fbf63578a288d95eb2f3f7fe4
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="percentiledisc-transact-sql"></a>PERCENTILE_DISC (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all-md](../../includes/tsql-appliesto-ss2012-all-md.md)]

  Berechnet für sortierte Werte in einem gesamten Rowset oder innerhalb bestimmter Partitionen eines Rowsets in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ein bestimmtes Quantil. Für einen angegebenen Prozentwert *P*, PERCENTILE_DISC die Werte des Ausdrucks in der ORDER BY-Klausel sortiert, und gibt den Wert mit dem kleinsten CUME_DIST-Wert (in Bezug auf die gleiche sortierspezifikation), die größer als oder gleich *P*. Beispiel: PERCENTILE_DISC (0.5) berechnet das 50. Quantil (d. h. den Mittelwert) eines Ausdrucks. PERCENTILE_DISC berechnet das Quantil auf Grundlage einer diskreten Verteilung der Spaltenwerte. Das Ergebnis entspricht einem bestimmten Wert in der Spalte.  
  
 ![Symbol für Themenlink](../../database-engine/configure-windows/media/topic-link.gif "Thema Linksymbol") [Transact-SQL-Syntaxkonventionen &#40; Transact-SQL &#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
PERCENTILE_DISC ( numeric_literal ) WITHIN GROUP ( ORDER BY order_by_expression [ ASC | DESC ] )  
    OVER ( [ <partition_by_clause> ] )  
```  
  
## <a name="arguments"></a>Argumente  
 *Zeichenfolgenliterale*  
 Das zu berechnende Quantil. Der Wert muss zwischen 0,0 und 1,0 liegen.  
  
 IN den Gruppen **(** ORDER BY *Order_by_expression* [ **ASC** | "DESC"]**)**  
 Gibt eine Liste von Werten zu sortieren und Berechnung des Quantils an. Nur ein *Order_by_expression* ist zulässig. Die Standardsortierreihenfolge ist Aufsteigend. Die Liste der Werte kann eines der Datentypen, die für den Sortiervorgang gültig sind.  
  
 ÜBER **(** \<Partition_by_clause > **)**  
 Teilt das von der FROM-Klausel erzeugte Resultset in Partitionen, auf die die Quantilfunktion angewendet wird. Weitere Informationen finden Sie unter [Klausel "OVER" &#40; Transact-SQL &#41; ](../../t-sql/queries/select-over-clause-transact-sql.md). Die \<ORDER BY-Klausel > und \<Zeilen- oder Bereichsklausel > können nicht in einer PERCENTILE_DISC-Funktion angegeben werden.  
  
## <a name="return-types"></a>Rückgabetypen  
 Der Rückgabetyp wird bestimmt, indem die *Order_by_expression* Typ.  
  
## <a name="compatibility-support"></a>Kompatibilitätsunterstützung  
 Unter Kompatibilitätsgrad 110 und höher ist WITHIN GROUP ein reserviertes Schlüsselwort. Weitere Informationen finden Sie unter [ALTER DATABASE-Kompatibilitätsgrad &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md).  
  
## <a name="general-remarks"></a>Allgemeine Hinweise  
 Alle NULL-Werte im Dataset werden ignoriert.  
  
 PERCENTILE_DISC ist nicht deterministisch. Weitere Informationen finden Sie unter [Deterministic and Nondeterministic Functions](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md).  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-basic-syntax-example"></a>A. Einfaches Syntaxbeispiel  
 Im folgenden Beispiel wird das durchschnittliche Mitarbeitergehalt in jeder Abteilung mithilfe von PERCENTILE_CONT und PERCENTILE_DISC ermittelt. Beachten Sie, dass diese Funktionen möglicherweise nicht den gleichen Wert zurückgeben. Ursache hierfür ist, dass PERCENTILE_CONT den geeigneten Wert interpoliert, unabhängig davon, ob dieser im Dataset vorhanden ist oder nicht, während PERCENTILE_DISC immer einen Istwert aus dem Dataset zurückgibt.  
  
```  
USE AdventureWorks2012;  
  
SELECT DISTINCT Name AS DepartmentName  
      ,PERCENTILE_CONT(0.5) WITHIN GROUP (ORDER BY ph.Rate)   
                            OVER (PARTITION BY Name) AS MedianCont  
      ,PERCENTILE_DISC(0.5) WITHIN GROUP (ORDER BY ph.Rate)   
                            OVER (PARTITION BY Name) AS MedianDisc  
FROM HumanResources.Department AS d  
INNER JOIN HumanResources.EmployeeDepartmentHistory AS dh   
    ON dh.DepartmentID = d.DepartmentID  
INNER JOIN HumanResources.EmployeePayHistory AS ph  
    ON ph.BusinessEntityID = dh.BusinessEntityID  
WHERE dh.EndDate IS NULL;  
```  
  
 Dies ist ein Auszug aus dem Resultset.  
  
 ```
DepartmentName        MedianCont    MedianDisc
--------------------   ----------   ----------
Document Control       16.8269      16.8269
Engineering            34.375       32.6923
Executive              54.32695     48.5577
Human Resources        17.427850    16.5865
```
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Beispiele: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] und[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="b-basic-syntax-example"></a>B. Einfaches Syntaxbeispiel  
 Im folgenden Beispiel wird das durchschnittliche Mitarbeitergehalt in jeder Abteilung mithilfe von PERCENTILE_CONT und PERCENTILE_DISC ermittelt. Beachten Sie, dass diese Funktionen möglicherweise nicht den gleichen Wert zurückgeben. Ursache hierfür ist, dass PERCENTILE_CONT den geeigneten Wert interpoliert, unabhängig davon, ob dieser im Dataset vorhanden ist oder nicht, während PERCENTILE_DISC immer einen Istwert aus dem Dataset zurückgibt.  
  
```  
-- Uses AdventureWorks  
  
SELECT DISTINCT DepartmentName  
       ,PERCENTILE_CONT(0.5) WITHIN GROUP (ORDER BY BaseRate)  
        OVER (PARTITION BY DepartmentName) AS MedianCont  
       ,PERCENTILE_DISC(0.5) WITHIN GROUP (ORDER BY BaseRate)  
        OVER (PARTITION BY DepartmentName) AS MedianDisc  
FROM dbo.DimEmployee;  
  
```  
  
 Dies ist ein Auszug aus dem Resultset.  
  
 ```
DepartmentName        MedianCont    MedianDisc  
--------------------   ----------   ----------  
Document Control       16.826900    16.8269  
Engineering            34.375000    32.6923  
Human Resources        17.427850    16.5865  
Shipping and Receiving  9.250000     9.0000
```  
  
## <a name="see-also"></a>Siehe auch  
 [PERCENTILE_CONT &#40; Transact-SQL &#41;](../../t-sql/functions/percentile-cont-transact-sql.md)  
  
  



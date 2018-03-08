---
title: PERCENTILE_CONT (Transact-SQL) | Microsoft Docs
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
- PERCENTILE_CONT_TSQL
- PERCENTILE_CONT
dev_langs:
- TSQL
helpviewer_keywords:
- analytic functions, PERCENTILE_CONT
- PERCENTILE_CONT function
ms.assetid: d019419e-5297-4994-97d5-e9c8fc61bbf4
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: d55a4036849fb1dfccb281956b8f9f3313a95e72
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="percentilecont-transact-sql"></a>PERCENTILE_CONT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all-md](../../includes/tsql-appliesto-ss2012-all-md.md)]

  Berechnet ein Quantil auf Grundlage einer kontinuierlichen Verteilung des Spaltenwerts in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Das Ergebnis wird interpoliert und stimmt möglicherweise mit keinem der konkreten Werte in der Spalte überein.  
  
 ![Symbol für Themenlink](../../database-engine/configure-windows/media/topic-link.gif "Thema Linksymbol") [Transact-SQL-Syntaxkonventionen &#40; Transact-SQL &#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
PERCENTILE_CONT ( numeric_literal )   
    WITHIN GROUP ( ORDER BY order_by_expression [ ASC | DESC ] )  
    OVER ( [ <partition_by_clause> ] )  
```  
  
## <a name="arguments"></a>Argumente  
 *numeric_literal*  
 Das zu berechnende Quantil. Der Wert muss zwischen 0,0 und 1,0 liegen.  
  
 IN den Gruppen **(** ORDER BY *Order_by_expression* [ **ASC** | "DESC"]**)**  
 Gibt eine Liste von numerischen Werten für die Sortierung und Berechnung des Quantils an. Nur ein *Order_by_expression* ist zulässig. Der Ausdruck ausgewertet werden muss, um einen exakten numerischen Typ (**Int**, **"bigint"**, **"smallint"**, **"tinyint"**, **numerische**, **Bit**, **decimal**, **Smallmoney**, **Money**) oder einen ungefähren numerischen Typ ( **"float"**, **real**). Andere Datentypen sind nicht zulässig. Die Standardsortierreihenfolge ist Aufsteigend.  
  
 ÜBER **(** \<Partition_by_clause > **)**  
 Teilt das von der FROM-Klausel erzeugte Resultset in Partitionen, auf die die Quantilfunktion angewendet wird. Weitere Informationen finden Sie unter [Klausel "OVER" &#40; Transact-SQL &#41; ](../../t-sql/queries/select-over-clause-transact-sql.md). Die \<ORDER BY-Klausel > und \<Zeilen- oder Bereichsklausel > der OVER-Syntax kann nicht in einer PERCENTILE_CONT-Funktion angegeben werden.  
  
## <a name="return-types"></a>Rückgabetypen  
 **float(53)**  
  
## <a name="compatibility-support"></a>Kompatibilitätsunterstützung  
 Unter Kompatibilitätsgrad 110 und höher ist WITHIN GROUP ein reserviertes Schlüsselwort. Weitere Informationen finden Sie unter [ALTER DATABASE-Kompatibilitätsgrad &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md).  
  
## <a name="general-remarks"></a>Allgemeine Hinweise  
 Alle NULL-Werte im Dataset werden ignoriert.  
  
 PERCENTILE_CONT ist nicht deterministisch. Weitere Informationen finden Sie unter [Deterministic and Nondeterministic Functions](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md).  
  
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
Shipping and Receiving 9.250000      9.0000
```  
  
## <a name="see-also"></a>Siehe auch  
 [PERCENTILE_DISC &#40; Transact-SQL &#41;](../../t-sql/functions/percentile-disc-transact-sql.md)  
  
  



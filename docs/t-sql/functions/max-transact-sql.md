---
title: MAX (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 08/23/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- MAX
- MAX_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MAX function [Transact-SQL]
- values [SQL Server], maximum
- maximum values [SQL Server]
ms.assetid: 9b002b69-ab5e-472d-b12e-dc2fbe35ef42
caps.latest.revision: 38
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: b015e233023781b47c9bb633f5e45103ed1384d6
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="max-transact-sql"></a>MAX (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Gibt den größten Wert im Ausdruck zurück.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
MAX ( [ ALL | DISTINCT ] expression )  
   OVER ( [ partition_by_clause ] order_by_clause )     
```  
  
## <a name="arguments"></a>Argumente  
 **ALL**  
 Wendet die Aggregatfunktion auf alle Werte an. ALL ist die Standardeinstellung.  
  
 DISTINCT  
 Gibt an, dass jeder eindeutige Wert berücksichtigt wird. DISTINCT ist bei MAX ohne Bedeutung und nur aus Gründen der ISO-Kompatibilität verfügbar.  
  
 *expression*  
 Dies ist eine Konstante, ein Spaltenname oder eine Funktion und eine beliebige Kombination aus arithmetischen, bitweisen und Zeichenfolgenoperatoren. MAX kann mit Spalten vom Typ **numeric**, **character**, **uniqueidentifier** und **datetime**, jedoch nicht mit Spalten vom Typ **bit** verwendet werden. Aggregatfunktionen und Unterabfragen sind nicht zulässig.  
  
 Weitere Informationen finden Sie unter [Expressions &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md).  
  
 OVER **(** [ *partition_by_clause* ] *order_by_clause***)**  
 *partition_by_clause* unterteilt das von der FROM-Klausel erzeugte Resultset in Partitionen, auf die die Funktion angewendet wird. Wird dies nicht angegeben, verarbeitet die Funktion alle Zeilen des Abfrageresultsets als einzelne Gruppe. *order_by_clause* bestimmt die logische Reihenfolge, in der der Vorgang ausgeführt wird. *order_by_clause* ist erforderlich. Weitere Informationen finden Sie unter [OVER-Klausel &#40;Transact-SQL&#41;](../../t-sql/queries/select-over-clause-transact-sql.md).  
  
## <a name="return-types"></a>Rückgabetypen  
 Gibt einen Wert zurück, der mit *expression* identisch ist.  
  
## <a name="remarks"></a>Remarks  
 MAX ignoriert alle NULL-Werte.  
  
 Bei Zeichenspalten sucht MAX den höchsten Wert gemäß der Sortierreihenfolge.  
  
 MAX ist eine deterministische Funktion, wenn sie ohne die OVER- und ORDER BY-Klauseln angegeben wird. Sie ist nicht deterministisch, wenn sie mit den OVER- und ORDER BY-Klauseln angegeben wird. Weitere Informationen finden Sie unter [Deterministic and Nondeterministic Functions](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md).  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-simple-example"></a>A. Einfaches Beispiel  
 Im folgenden Beispiel wird der höchste (maximale) Steuersatz in der [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]-Datenbank zurückgegeben.  
  
```sql  
SELECT MAX(TaxRate)  
FROM Sales.SalesTaxRate;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```  
 -------------------  
 19.60  
 Warning, null value eliminated from aggregate.  
  
 (1 row(s) affected)  
 ```  
  
### <a name="b-using-the-over-clause"></a>B. Verwenden der OVER-Klausel  
 Im folgenden Beispiel werden die Funktionen MIN, MAX, AVG und COUNT mit der OVER-Klausel verwendet, um aggregierte Werte für jede Abteilung in der `HumanResources.Department`-Tabelle der [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]-Datenbank bereitzustellen.  
  
```sql  
SELECT DISTINCT Name  
       , MIN(Rate) OVER (PARTITION BY edh.DepartmentID) AS MinSalary  
       , MAX(Rate) OVER (PARTITION BY edh.DepartmentID) AS MaxSalary  
       , AVG(Rate) OVER (PARTITION BY edh.DepartmentID) AS AvgSalary  
       ,COUNT(edh.BusinessEntityID) OVER (PARTITION BY edh.DepartmentID) AS EmployeesPerDept  
FROM HumanResources.EmployeePayHistory AS eph  
JOIN HumanResources.EmployeeDepartmentHistory AS edh  
     ON eph.BusinessEntityID = edh.BusinessEntityID  
JOIN HumanResources.Department AS d  
 ON d.DepartmentID = edh.DepartmentID  
WHERE edh.EndDate IS NULL  
ORDER BY Name;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Name                          MinSalary             MaxSalary             AvgSalary             EmployeesPerDept  
----------------------------- --------------------- --------------------- --------------------- ----------------  
Document Control              10.25                 17.7885               14.3884               5  
Engineering                   32.6923               63.4615               40.1442               6  
Executive                     39.06                 125.50                68.3034               4  
Facilities and Maintenance    9.25                  24.0385               13.0316               7  
Finance                       13.4615               43.2692               23.935                10  
Human Resources               13.9423               27.1394               18.0248               6  
Information Services          27.4038               50.4808               34.1586               10  
Marketing                     13.4615               37.50                 18.4318               11  
Production                    6.50                  84.1346               13.5537               195  
Production Control            8.62                  24.5192               16.7746               8  
Purchasing                    9.86                  30.00                 18.0202               14  
Quality Assurance             10.5769               28.8462               15.4647               6  
Research and Development      40.8654               50.4808               43.6731               4  
Sales                         23.0769               72.1154               29.9719               18  
Shipping and Receiving        9.00                  19.2308               10.8718               6  
Tool Design                   8.62                  29.8462               23.5054               6  
  
 (16 row(s) affected)  
```  
  
### <a name="c-using-max-with-character-data"></a>C. Verwenden von MAX mit Zeichendaten   
Im folgenden Beispiel werden Datenbanknamen zurückgegeben. Dabei wird der letzte Name alphabetisch sortiert. In diesem Beispiel wird `WHERE database_id < 5` verwendet, um nur Systemdatenbanken zu berücksichtigen.  
```sql   
SELECT MAX(name) FROM sys.databases WHERE database_id < 5;
```
Die letzte Systemdatenbank ist `tempdb`.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Aggregate Functions &#40;Transact-SQL&#41; (Aggregatfunktionen (Transact-SQL))](../../t-sql/functions/aggregate-functions-transact-sql.md)   
 [OVER-Klausel &#40;Transact-SQL&#41;](../../t-sql/queries/select-over-clause-transact-sql.md)  
  
  


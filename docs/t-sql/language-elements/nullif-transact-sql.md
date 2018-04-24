---
title: NULLIF (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 09/08/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: t-sql|language-elements
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- NULLIF
- NULLIF_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- null values [SQL Server], equivalent expressions
- expressions [SQL Server], null values
- NULLIF function
- equivalent expressions [SQL Server]
ms.assetid: 44c7b67e-74c7-4bb9-93a4-7a3016bd2feb
caps.latest.revision: 48
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Active
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 55b05bf5c783d5e0f64c83b6483e478826de1083
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="nullif-transact-sql"></a>NULLIF (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Gibt einen NULL-Wert zurück, wenn die beiden angegebenen Ausdrücke gleich sind. Beispielsweise gibt `SELECT NULLIF(4,4) AS Same, NULLIF(5,7) AS Different;` für die erste Spalte (4 und 4) NULL zurück, da die zwei Eingabewerte identisch sind. Die zweite Spalte gibt den ersten Wert (5) zurück, da die beiden Werte sich unterscheiden. 
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
NULLIF ( expression , expression )  
```  
  
## <a name="arguments"></a>Argumente  
 *expression*  
 Alle gültigen [Skalarausdrücke](../../t-sql/language-elements/expressions-transact-sql.md).  
  
## <a name="return-types"></a>Rückgabetypen  
 Gibt denselben Typ wie der erste *Ausdruck* zurück.  
  
 NULLIF gibt den ersten *Ausdruck* zurück, wenn sich die zwei Ausdrücke voneinander unterscheiden. Wenn die Ausdrücke identisch sind, gibt NULLIF einen NULL-Wert mit dem Typ des ersten *Ausdrucks* zurück.  
  
## <a name="remarks"></a>Remarks  
 NULLIF entspricht einem komplexen CASE-Ausdruck, in dem die beiden Ausdrücke gleich sind und der sich ergebende Ausdruck NULL ist.  
  
 Es empfiehlt sich nicht, zeitabhängige Funktionen wie RAND() innerhalb einer NULLIF-Funktion zu verwenden. Dies könnte dazu führen, dass die Funktion zweimal ausgewertet wird und aus den beiden Aufrufen unterschiedliche Ergebnisse zurückgibt.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-returning-budget-amounts-that-have-not-changed"></a>A. Zurückgeben von Budgetsummen, die sich nicht geändert haben  
 Im folgenden Beispiel wird eine `budgets`-Tabelle erstellt, die eine Abteilung (`dept`), ihr aktuelles Jahresbudget (`current_year`) und ihr Budget vom Vorjahr (`previous_year`) anzeigt. Für das laufende Jahr wird `NULL` verwendet, wenn sich das Budget einer Abteilung gegenüber dem Vorjahr nicht verändert hat. Der Wert `0` wird verwendet, wenn das Budget noch nicht festgelegt wurde. Wenn Sie nur für die Abteilungen, die ein Budget erhalten, den Durchschnittswert ermitteln und außerdem die Budgethöhe des vergangenen Jahres einschließen möchten (d. h., wenn Sie den Wert von `previous_year` verwenden möchten, in dem der Wert für `current_year` gleich `NULL` ist), kombinieren Sie die Funktionen `NULLIF` und `COALESCE`.  
  
```sql  
CREATE TABLE dbo.budgets  
(  
   dept            tinyint   IDENTITY,  
   current_year      decimal   NULL,  
   previous_year   decimal   NULL  
);  
INSERT budgets VALUES(100000, 150000);  
INSERT budgets VALUES(NULL, 300000);  
INSERT budgets VALUES(0, 100000);  
INSERT budgets VALUES(NULL, 150000);  
INSERT budgets VALUES(300000, 250000);  
GO    
SET NOCOUNT OFF;  
SELECT AVG(NULLIF(COALESCE(current_year,  
   previous_year), 0.00)) AS 'Average Budget'  
FROM budgets;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 Average Budget  
 --------------  
 212500.000000  
 (1 row(s) affected)
 ```  
  
### <a name="b-comparing-nullif-and-case"></a>B. Vergleichen von NULLIF und CASE  
 Als Beispiel für die Ähnlichkeit von `NULLIF` und `CASE` wird in den folgenden Abfragen ausgewertet, ob die Werte in den Spalten `MakeFlag` und `FinishedGoodsFlag` gleich sind. In der ersten Abfrage wird `NULLIF` verwendet. In der zweiten Abfrage wird der `CASE`-Ausdruck verwendet.  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT ProductID, MakeFlag, FinishedGoodsFlag,   
   NULLIF(MakeFlag,FinishedGoodsFlag)AS 'Null if Equal'  
FROM Production.Product  
WHERE ProductID < 10;  
GO  
  
SELECT ProductID, MakeFlag, FinishedGoodsFlag,'Null if Equal' =  
   CASE  
       WHEN MakeFlag = FinishedGoodsFlag THEN NULL  
       ELSE MakeFlag  
   END  
FROM Production.Product  
WHERE ProductID < 10;  
GO  
```  

### <a name="c-returning-budget-amounts-that-contain-no-data"></a>C: Zurückgeben von Budgetsummen, die keine Daten enthalten  
 Im folgenden Beispiel wird eine `budgets`-Tabelle erstellt, Daten geladen und `NULLIF` verwendet, um NULL zurückzugeben, wenn weder `current_year` noch `previous_year` Daten enthalten.  
  
```sql  
CREATE TABLE budgets (  
   dept           tinyint,  
   current_year   decimal(10,2),  
   previous_year  decimal(10,2)  
);  
  
INSERT INTO budgets VALUES(1, 100000, 150000);  
INSERT INTO budgets VALUES(2, NULL, 300000);  
INSERT INTO budgets VALUES(3, 0, 100000);  
INSERT INTO budgets VALUES(4, NULL, 150000);  
INSERT INTO budgets VALUES(5, 300000, 300000);  
  
SELECT dept, NULLIF(current_year,  
   previous_year) AS LastBudget  
FROM budgets;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 dept   LastBudget  
 ----   -----------  
 1      100000.00  
 2      null 
 3      0.00  
 4      null  
 5      null
 ```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [CASE &#40;Transact-SQL&#41;](../../t-sql/language-elements/case-transact-sql.md)   
 [decimal und numeric &#40;Transact-SQL&#41;](../../t-sql/data-types/decimal-and-numeric-transact-sql.md)   
 [Systemfunktionen &#40;Transact-SQL&#41;](../../relational-databases/system-functions/system-functions-for-transact-sql.md)  
  
  


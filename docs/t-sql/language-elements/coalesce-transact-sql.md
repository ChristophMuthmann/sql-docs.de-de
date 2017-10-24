---
title: COALESCE (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/30/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- COALESCE
- COALESCE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- expressions [SQL Server], nonnull
- COALESCE function
- first nonnull expressions [SQL Server]
- nonnull expressions
ms.assetid: fafc0dba-f8a8-4aad-9b7f-908e34b74d88
caps.latest.revision: 52
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: d597c347b0b608b69c5d435fbf58b2779d462a32
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="coalesce-transact-sql"></a>COALESCE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Wertet die Argumente in der Reihenfolge und gibt den aktuellen Wert des ersten Ausdrucks, das anfänglich nicht ergibt `NULL`. Beispielsweise `SELECT COALESCE(NULL, NULL, 'third_value', 'fourth_value');` der dritten Wert zurückgegeben, weil der dritte Wert den ersten Wert, der nicht null ist. 
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
COALESCE ( expression [ ,...n ] )   
```  
  
## <a name="arguments"></a>Argumente  
 *expression*  
 Ist ein [Ausdruck](../../t-sql/language-elements/expressions-transact-sql.md) eines beliebigen Typs.  
  
## <a name="return-types"></a>Rückgabetypen  
 Gibt den Datentyp der *Ausdruck* mit der höchsten Rangfolge der Datentypen. Falls für alle Ausdrücke NULL nicht zulässig ist, wird das Ergebnis entsprechend eingegeben.  
  
## <a name="remarks"></a>Hinweise  
 Wenn alle Argumente sind `NULL`, `COALESCE` gibt `NULL`. Muss mindestens eine der null-Werte einer typisierten `NULL`.  
  
## <a name="comparing-coalesce-and-case"></a>Vergleich zwischen COALESCE und CASE  
 Die `COALESCE` Ausdruck ist eine syntaktische Kurzform für die `CASE` Ausdruck.  D. h. den Code `COALESCE`(*expression1*,*.. ...n*) wird vom Abfrageoptimierer wie folgt umgeschrieben `CASE` Ausdruck:  
  
 ```sql  
 CASE  
 WHEN (expression1 IS NOT NULL) THEN expression1  
 WHEN (expression2 IS NOT NULL) THEN expression2  
 ...  
 ELSE expressionN  
 END  
 ```  
  
 Dies bedeutet, dass die Eingabewerte (*expression1*, *expression2*, *ExpressionN*usw.) mehrmals ausgewertet werden. Außerdem wird ein Wertausdruck, der eine Unterabfrage enthält, gemäß dem SQL-Standard als nicht deterministisch angesehen und die Unterabfrage zweimal ausgewertet. In beiden Fällen können zwischen der ersten Auswertung und nachfolgenden Auswertungen unterschiedliche Ergebnisse zurückgegeben werden.  
  
 Beispiel: Wenn der Code `COALESCE((subquery), 1)` ausgeführt wird, wird die Unterabfrage zweimal ausgewertet. Folglich können Sie abhängig von der Isolationsstufe der Abfrage unterschiedliche Ergebnisse erhalten. Beispielsweise kann der Code zurückgeben `NULL` unter der `READ COMMITTED` Isolationsstufe in einer mehrbenutzerumgebung. Um sicherzustellen, dass beständige Ergebnisse zurückgegeben werden, verwenden die `SNAPSHOT ISOLATION` Isolationsstufe oder ersetzen `COALESE` mit der `ISNULL` Funktion. Alternativ können Sie die Abfrage aus, um die Unterabfrage in einer untergeordneten SELECT-Anweisung zu verschieben, wie im folgenden Beispiel gezeigt unterteilen:  
  
```sql  
SELECT CASE WHEN x IS NOT NULL THEN x ELSE 1 END  
from  
(  
SELECT (SELECT Nullable FROM Demo WHERE SomeCol = 1) AS x  
) AS T;  
  
```  
  
## <a name="comparing-coalesce-and-isnull"></a>Vergleich zwischen COALESCE und ISNULL  
 Die `ISNULL` Funktion und die `COALESCE` Ausdruck einen ähnlichen Zweck haben, jedoch können sich unterschiedlich Verhalten.  
  
1.  Da `ISNULL` eine Funktion ist, wird nur einmal ausgewertet.  Wie oben beschrieben, die Eingabe-Werte für die `COALESCE` Ausdruck mehrmals ausgewertet werden kann.  
  
2.  Die Datentypen des resultierenden Ausdrucks werden auf unterschiedliche Weise bestimmt. `ISNULL`verwendet den Datentyp des ersten Parameters `COALESCE` folgt die `CASE` Ausdruck Regeln und gibt den Datentyp des Werts mit der höchsten Rangfolge.  
  
3.  Die NULL-Zulässigkeit des Ergebnisausdrucks unterscheidet sich für `ISNULL` und `COALESCE`. Die `ISNULL` Rückgabewerte immer als nicht NULL-Werte zulässt (vorausgesetzt, der Rückgabewert ist ein NULL-Werte zulässt) hingegen `COALESCE` mit Parametern ungleich Null wird als betrachtet `NULL`. Daher die Ausdrücke `ISNULL(NULL, 1)` und `COALESCE(NULL, 1)`, obwohl Sie äquivalent, NULL-Zulässigkeit unterscheidet Werte aufweisen. Dies ist entscheidend dafür, wenn Sie diese Ausdrücke in berechneten Spalten verwenden, erstellen Key-Einschränkungen oder den Rückgabewert einer Skalar-UDF deterministisch vornehmen, sodass er indiziert werden kann, wie im folgenden Beispiel gezeigt:  
  
    ```sql  
    USE tempdb;  
    GO  
    -- This statement fails because the PRIMARY KEY cannot accept NULL values  
    -- and the nullability of the COALESCE expression for col2   
    -- evaluates to NULL.  
    CREATE TABLE #Demo   
    (   
    col1 integer NULL,   
    col2 AS COALESCE(col1, 0) PRIMARY KEY,   
    col3 AS ISNULL(col1, 0)   
    );   
  
    -- This statement succeeds because the nullability of the   
    -- ISNULL function evaluates AS NOT NULL.  
  
    CREATE TABLE #Demo   
    (   
    col1 integer NULL,   
    col2 AS COALESCE(col1, 0),   
    col3 AS ISNULL(col1, 0) PRIMARY KEY   
    );  
    ```  
  
4.  Überprüfungen für `ISNULL` und `COALESCE` sind ebenfalls unterschiedlich. Z. B. eine `NULL` Wert für `ISNULL` konvertiert **Int** hingegen für `COALESCE`, müssen Sie einen Datentyp angeben.  
  
5.  `ISNULL`akzeptiert nur zwei Parameter, wohingegen `COALESCE` nimmt eine Variable Anzahl von Parametern.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-running-a-simple-example"></a>A. Ausführen eines einfachen Beispiels  
 Im folgenden Beispiel wird veranschaulicht, wie `COALESCE` die Daten aus der ersten Spalte auswählt, die einen Wert ungleich NULL aufweist. In diesem Beispiel wird die [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]-Datenbank verwendet.  
  
```sql  
SELECT Name, Class, Color, ProductNumber,  
COALESCE(Class, Color, ProductNumber) AS FirstNotNull  
FROM Production.Product;  
```  
  
### <a name="b-running-a-complex-example"></a>B. Ausführen eines komplexen Beispiels  
 Im folgenden Beispiel enthält die `wages`-Tabelle drei Spalten mit Informationen zu den Jahresgehältern der Angestellten: den Stundensatz, das Gehalt und die Provision. Allerdings wird ein Angestellter nur nach einem dieser Gehaltstypen bezahlt. Um die Gesamtsumme aller Auszahlungen an die Angestellten zu bestimmen, verwenden Sie `COALESCE`, damit Sie nur die Werte ungleich NULL in den Spalten `hourly_wage`, `salary` und `commission` erhalten.  
  
```sql  
SET NOCOUNT ON;  
GO  
USE tempdb;  
IF OBJECT_ID('dbo.wages') IS NOT NULL  
    DROP TABLE wages;  
GO  
CREATE TABLE dbo.wages  
(  
    emp_id        tinyint   identity,  
    hourly_wage   decimal   NULL,  
    salary        decimal   NULL,  
    commission    decimal   NULL,  
    num_sales     tinyint   NULL  
);  
GO  
INSERT dbo.wages (hourly_wage, salary, commission, num_sales)  
VALUES  
    (10.00, NULL, NULL, NULL),  
    (20.00, NULL, NULL, NULL),  
    (30.00, NULL, NULL, NULL),  
    (40.00, NULL, NULL, NULL),  
    (NULL, 10000.00, NULL, NULL),  
    (NULL, 20000.00, NULL, NULL),  
    (NULL, 30000.00, NULL, NULL),  
    (NULL, 40000.00, NULL, NULL),  
    (NULL, NULL, 15000, 3),  
    (NULL, NULL, 25000, 2),  
    (NULL, NULL, 20000, 6),  
    (NULL, NULL, 14000, 4);  
GO  
SET NOCOUNT OFF;  
GO  
SELECT CAST(COALESCE(hourly_wage * 40 * 52,   
   salary,   
   commission * num_sales) AS money) AS 'Total Salary'   
FROM dbo.wages  
ORDER BY 'Total Salary';  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```   
 Total Salary  
 ------------  
 10000.00  
 20000.00  
 20800.00  
 30000.00  
 40000.00  
 41600.00  
 45000.00  
 50000.00  
 56000.00  
 62400.00  
 83200.00  
 120000.00  
  
 (12 row(s) affected)
 ```  
  
### <a name="c-simple-example"></a>"C:" einfaches Beispiel  
 Im folgende Beispiel wird veranschaulicht, wie `COALESCE` wählt Daten aus der ersten Spalte, die einen Wert ungleich Null aufweist. In diesem Beispiel wird angenommen, die die `Products` Tabelle enthält, diese Daten:  
  
 ```  
 Name         Color      ProductNumber  
 ------------ ---------- -------------  
 Socks, Mens  NULL       PN1278  
 Socks, Mens  Blue       PN1965  
 NULL         White      PN9876
 ```  
  
 Wir führen Sie dann die folgenden COALESCE-Abfrage aus:  
  
```sql  
SELECT Name, Color, ProductNumber, COALESCE(Color, ProductNumber) AS FirstNotNull   
FROM Products ;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```  
 Name         Color      ProductNumber  FirstNotNull  
 ------------ ---------- -------------  ------------  
 Socks, Mens  NULL       PN1278         PN1278  
 Socks, Mens  Blue       PN1965         Blue  
 NULL         White      PN9876         White
 ```  
  
 Beachten Sie, dass in der ersten Zeile der `FirstNotNull` Wert `PN1278`, nicht `Socks, Mens`. Grund hierfür ist die `Name` Spalte wurde nicht angegeben, als Parameter für `COALESCE` im Beispiel.  
  
### <a name="d-complex-example"></a>D: komplexen Beispiels  
 Im folgenden Beispiel wird `COALESCE` zu vergleichen Sie die Werte in drei Spalten nur die nicht-Null-Wert, der in den Spalten gefunden.  
  
```sql  
CREATE TABLE dbo.wages  
(  
    emp_id        tinyint   NULL,  
    hourly_wage   decimal   NULL,  
    salary        decimal   NULL,  
    commission    decimal   NULL,  
    num_sales     tinyint   NULL  
);  
INSERT INTO dbo.wages (emp_id, hourly_wage, salary, commission, num_sales)  
VALUES (1, 10.00, NULL, NULL, NULL);  
  
INSERT INTO dbo.wages (emp_id, hourly_wage, salary, commission, num_sales)  
VALUES (2, 20.00, NULL, NULL, NULL);  
  
INSERT INTO dbo.wages (emp_id, hourly_wage, salary, commission, num_sales)  
VALUES (3, 30.00, NULL, NULL, NULL);  
  
INSERT INTO dbo.wages (emp_id, hourly_wage, salary, commission, num_sales)  
VALUES (4, 40.00, NULL, NULL, NULL);  
  
INSERT INTO dbo.wages (emp_id, hourly_wage, salary, commission, num_sales)  
VALUES (5, NULL, 10000.00, NULL, NULL);  
  
INSERT INTO dbo.wages (emp_id, hourly_wage, salary, commission, num_sales)  
VALUES (6, NULL, 20000.00, NULL, NULL);  
  
INSERT INTO dbo.wages (emp_id, hourly_wage, salary, commission, num_sales)  
VALUES (7, NULL, 30000.00, NULL, NULL);  
  
INSERT INTO dbo.wages (emp_id, hourly_wage, salary, commission, num_sales)  
VALUES (8, NULL, 40000.00, NULL, NULL);  
  
INSERT INTO dbo.wages (emp_id, hourly_wage, salary, commission, num_sales)  
VALUES (9, NULL, NULL, 15000, 3);  
  
INSERT INTO dbo.wages (emp_id, hourly_wage, salary, commission, num_sales)  
VALUES (10,NULL, NULL, 25000, 2);  
  
INSERT INTO dbo.wages (emp_id, hourly_wage, salary, commission, num_sales)  
VALUES (11, NULL, NULL, 20000, 6);  
  
INSERT INTO dbo.wages (emp_id, hourly_wage, salary, commission, num_sales)  
VALUES (12, NULL, NULL, 14000, 4);  
  
SELECT CAST(COALESCE(hourly_wage * 40 * 52,   
   salary,   
   commission * num_sales) AS decimal(10,2)) AS TotalSalary   
FROM dbo.wages  
ORDER BY TotalSalary;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 Total Salary  
 ------------  
 10000.00  
 20000.00  
 20800.00  
 30000.00  
 40000.00  
 41600.00  
 45000.00  
 50000.00  
 56000.00  
 62400.00  
 83200.00  
 120000.00
 ```  
  
## <a name="see-also"></a>Siehe auch  
 [ISNULL &#40; Transact-SQL &#41;](../../t-sql/functions/isnull-transact-sql.md)   
 [CASE &#40;Transact-SQL&#41;](../../t-sql/language-elements/case-transact-sql.md)  
  
  


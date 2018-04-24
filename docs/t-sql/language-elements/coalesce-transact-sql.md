---
title: COALESCE (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 08/30/2017
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
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Active
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 7360a1927ce460c96c127d6a4f2d5d59668337e0
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="coalesce-transact-sql"></a>COALESCE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Wertet die Argumente in der vorliegenden Reihenfolge aus und gibt den aktuellen Wert des ersten Ausdrucks zurück, der anfangs nicht `NULL` ergibt. `SELECT COALESCE(NULL, NULL, 'third_value', 'fourth_value');` gibt beispielsweise den dritten Wert zurück, weil der dritte der erste Wert ist, der nicht NULL ist. 
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
COALESCE ( expression [ ,...n ] )   
```  
  
## <a name="arguments"></a>Argumente  
 *expression*  
 Ein [Ausdruck](../../t-sql/language-elements/expressions-transact-sql.md) beliebigen Typs.  
  
## <a name="return-types"></a>Rückgabetypen  
 Gibt den Datentyp des *expression*-Ausdrucks zurück, der in der Datentyprangfolge am höchsten steht. Falls für alle Ausdrücke NULL nicht zulässig ist, wird das Ergebnis entsprechend eingegeben.  
  
## <a name="remarks"></a>Remarks  
 `COALESCE` gibt `NULL` zurück, wenn alle Argumente `NULL` sind. Mindestens einer der NULL-Werte muss ein typisierter `NULL`-Wert sein.  
  
## <a name="comparing-coalesce-and-case"></a>Vergleich zwischen COALESCE und CASE  
 Der `COALESCE`-Ausdruck ist eine syntaktische Kurzform für den `CASE`-Ausdruck.  Dies bedeutet, dass der Code `COALESCE`(*expression1*,*...n*) vom Abfrageoptimierer in den folgenden `CASE`-Ausdruck umgeschrieben wird:  
  
 ```sql  
 CASE  
 WHEN (expression1 IS NOT NULL) THEN expression1  
 WHEN (expression2 IS NOT NULL) THEN expression2  
 ...  
 ELSE expressionN  
 END  
 ```  
  
 Das bedeutet, dass die Eingabewerte (*expression1*, *expression2*, *expressionN* usw.) mehrmals ausgewertet werden. Außerdem wird ein Wertausdruck, der eine Unterabfrage enthält, gemäß dem SQL-Standard als nicht deterministisch angesehen und die Unterabfrage zweimal ausgewertet. In beiden Fällen können zwischen der ersten Auswertung und nachfolgenden Auswertungen unterschiedliche Ergebnisse zurückgegeben werden.  
  
 Beispiel: Wenn der Code `COALESCE((subquery), 1)` ausgeführt wird, wird die Unterabfrage zweimal ausgewertet. Folglich können Sie abhängig von der Isolationsstufe der Abfrage unterschiedliche Ergebnisse erhalten. Beispielsweise kann der Code auf der `READ COMMITTED`-Isolationsstufe in einer Mehrbenutzerumgebung `NULL` zurückgeben. Um sicherzustellen, dass beständige Ergebnisse zurückgegeben werden, verwenden Sie die `SNAPSHOT ISOLATION`-Isolationsstufe oder ersetzen `COALESCE` durch die `ISNULL`-Funktion. Alternativ können Sie die Abfrage umschreiben, um die Unterabfrage wie im folgenden Beispiel gezeigt in eine untergeordnete SELECT-Anweisung zu verschieben.  
  
```sql  
SELECT CASE WHEN x IS NOT NULL THEN x ELSE 1 END  
from  
(  
SELECT (SELECT Nullable FROM Demo WHERE SomeCol = 1) AS x  
) AS T;  
  
```  
  
## <a name="comparing-coalesce-and-isnull"></a>Vergleich zwischen COALESCE und ISNULL  
 Die `ISNULL`-Funktion und der `COALESCE`-Ausdruck dienen einem ähnlichen Zweck, können jedoch ein unterschiedliches Verhalten aufweisen.  
  
1.  Da `ISNULL` eine Funktion ist, wird sie nur einmal ausgewertet.  Die Eingabewerte können wie oben beschrieben für den `COALESCE`-Ausdruck mehrmals ausgewertet werden.  
  
2.  Die Datentypen des resultierenden Ausdrucks werden auf unterschiedliche Weise bestimmt. `ISNULL` verwendet den Datentyp des ersten Parameters, während bei `COALESCE` die Regeln des `CASE`-Ausdrucks befolgt werden und der Datentyp des Werts mit der höchsten Rangfolge zurückgegeben wird.  
  
3.  Die NULL-Zulässigkeit des Ergebnisausdrucks ist bei `ISNULL` und `COALESCE` unterschiedlich. Beim `ISNULL`-Rückgabewert wird (in der Annahme, dass er keine NULL-Werte zulässt) immer davon ausgegangen, dass er NOT NULL ist, während `COALESCE` mit Parametern ungleich NULL als `NULL` betrachtet wird. Daher weisen der `ISNULL(NULL, 1)`-Ausdruck und der `COALESCE(NULL, 1)`-Ausdruck unterschiedliche Werte für die NULL-Zulässigkeit auf, obwohl sie äquivalent sind. Dieser Unterschied macht sich bemerkbar, wenn Sie die Ausdrücke in berechneten Spalten verwenden, Schlüsseleinschränkungen erstellen oder den Rückgabewert einer Skalar-UDF als deterministisch festlegen, sodass er wie im folgenden Beispiel veranschaulicht indiziert werden kann:  
  
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
  
4.  Überprüfungen für `ISNULL` und `COALESCE` sind ebenfalls unterschiedlich. Beispielsweise wird ein `NULL`-Wert für `ISNULL` in **int** konvertiert, während Sie für `COALESCE` einen Datentyp angeben müssen.  
  
5.  `ISNULL` akzeptiert nur zwei Parameter, während für `COALESCE` eine beliebige Anzahl von Parametern verwendet werden kann.  
  
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
  
### <a name="c-simple-example"></a>C. Einfaches Beispiel  
 Im folgenden Beispiel wird veranschaulicht, wie `COALESCE` die Daten aus der ersten Spalte auswählt, die einen Wert ungleich NULL aufweist. In diesem Beispiel wird angenommen, dass die `Products`-Tabelle die folgenden Daten enthält:  
  
 ```  
 Name         Color      ProductNumber  
 ------------ ---------- -------------  
 Socks, Mens  NULL       PN1278  
 Socks, Mens  Blue       PN1965  
 NULL         White      PN9876
 ```  
  
 Wir führen anschließend die folgende COALESCE-Abfrage aus:  
  
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
  
 Beachten Sie, dass der `FirstNotNull`-Wert in der ersten Zeile `PN1278`, nicht `Socks, Mens` ist. Grund hierfür ist, dass die `Name`-Spalte im Beispiel nicht als Parameter für `COALESCE` angegeben wurde.  
  
### <a name="d-complex-example"></a>D. Komplexes Beispiel  
 Im folgenden Beispiel werden die Werte in drei Spalten mit `COALESCE` verglichen und nur die Werte ungleich NULL zurückgegeben, die in den Spalten gefunden wurden.  
  
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
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [ISNULL &#40;Transact-SQL&#41;](../../t-sql/functions/isnull-transact-sql.md)   
 [CASE &#40;Transact-SQL&#41;](../../t-sql/language-elements/case-transact-sql.md)  
  
  

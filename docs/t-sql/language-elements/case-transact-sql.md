---
title: Fall (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/28/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CASE_TSQL
- CASE
dev_langs: TSQL
helpviewer_keywords:
- CASE expression [Transact-SQL]
- simple CASE expression
- comparing expressions
- searched CASE expression
ms.assetid: 658039ec-8dc2-4251-bc82-30ea23708cee
caps.latest.revision: "59"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 4d5241ddc65de92d7588e4c8d1ddb7c2e6b08528
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="case-transact-sql"></a>CASE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Wertet eine Liste von Bedingungen aus und gibt einen von mehreren möglichen Ergebnisausdrücken zurück.  
  
 Der CASE-Ausdruck verfügt über zwei Formate:  
  
-   Der einfache CASE-Ausdruck vergleicht einen Ausdruck mit mehreren einfachen Ausdrücken, um das Ergebnis zu bestimmen.  
  
-   Der komplexe CASE-Ausdruck wertet eine Menge boolescher Ausdrücke aus, um das Ergebnis zu bestimmen.  
  
 Bei beiden Formaten wird ein optionales ELSE-Argument unterstützt.  
  
 CASE kann in einer beliebigen Anweisung oder Klausel verwendet werden, die einen gültigen Ausdruck zulässt. Beispielsweise können CASE-Anweisungen wie SELECT, UPDATE, DELETE und SET und Klauseln wie select_list, IN, WHERE, ORDER BY und HAVING verwendet werden.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
Simple CASE expression:   
CASE input_expression   
     WHEN when_expression THEN result_expression [ ...n ]   
     [ ELSE else_result_expression ]   
END   
Searched CASE expression:  
CASE  
     WHEN Boolean_expression THEN result_expression [ ...n ]   
     [ ELSE else_result_expression ]   
END  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
CASE  
     WHEN when_expression THEN result_expression [ ...n ]   
     [ ELSE else_result_expression ]   
END  
```  
  
## <a name="arguments"></a>Argumente  
 *input_expression*  
 Der Ausdruck, der ausgewertet wird, wenn das einfache CASE-Format verwendet wird. *Input_expression* ist ein beliebiger gültiger [Ausdruck](../../t-sql/language-elements/expressions-transact-sql.md).  
  
 Wenn *When_expression*  
 Ein einfacher Ausdruck, der *Input_expression* verglichen wird, wenn das einfache CASE-Format verwendet wird. *When_expression* kann jeder gültige Ausdruck. Die Datentypen der *Input_expression* und jede *When_expression* müssen identisch sein oder muss eine implizite Konvertierung.  
  
 Klicken Sie dann *Result_expression*  
 Wird der Ausdruck zurückgegeben, wenn *Input_expression* gleich *When_expression* TRUE ergibt, oder *Boolean_expression* auf "true" ergibt. *-Ergebnisausdrücke* ist ein beliebiger gültiger [Ausdruck](../../t-sql/language-elements/expressions-transact-sql.md).  
  
 ELSE *Else_result_expression*  
 Der Ausdruck, der zurückgegeben wird, wenn keine Vergleichsoperation TRUE ergibt. Wenn dieses Argument weggelassen wird und keine Vergleichsoperation als TRUE ausgewertet wird, gibt die CASE-Funktion NULL zurück. *Else_result_expression* kann jeder gültige Ausdruck. Die Datentypen der *Else_result_expression* und ein beliebiger *Result_expression* müssen identisch sein oder muss eine implizite Konvertierung.  
  
 Wenn *Boolean_expression*  
 Der boolesche Ausdruck, der ausgewertet wird, wenn das komplexe CASE-Format verwendet wird. *Boolean_expression* kann jeder gültiger boolesche Ausdruck.  
  
## <a name="return-types"></a>Rückgabetypen  
 Gibt den Typ der höchsten Rangfolge aus dem Satz von Typen in *Result_expressions* und dem optionalen *Else_result_expression*. Weitere Informationen finden Sie unter [Rangfolge der Datentypen &#40;Transact-SQL&#41;](../../t-sql/data-types/data-type-precedence-transact-sql.md).  
  
### <a name="return-values"></a>Rückgabewerte  
 **Einfache CASE-Ausdruck:**  
  
 Beim einfachen CASE-Ausdruck wird verglichen, ob der erste Ausdruck mit dem Ausdruck in den einzelnen WHEN-Klauseln gleichwertig ist. Wenn diese Ausdrücke gleichwertig sind, wird der Ausdruck in der THEN-Klausel zurückgegeben.  
  
-   Lässt nur eine Gleichheitsüberprüfung zu.  
  
-   In der angegebenen Reihenfolge die input_expression = When_expression für jede WHEN-Klausel.  
  
-   Gibt die *Result_expression* des ersten *Input_expression* = *When_expression* , der auf "true" ausgewertet wird.  
  
-   Wenn kein *Input_expression* = *When_expression* auf "true", wertet der [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] gibt die *Else_result_expression* ist eine ELSE-Klausel angegeben wird, oder ein NULL-Wert, wenn keine ELSE-Klausel angegeben wird.  
  
 **Komplexer CASE-Ausdruck:**  
  
-   Ausgewertet wird, in der angegebenen Reihenfolge *Boolean_expression* für jede WHEN-Klausel.  
  
-   Gibt *Result_expression* des ersten *Boolean_expression* , der auf "true" ausgewertet wird.  
  
-   Wenn kein *Boolean_expression* TRUE ergibt, der [!INCLUDE[ssDE](../../includes/ssde-md.md)] gibt die *Else_result_expression* Falls eine ELSE-Klausel angegeben wird, oder ein NULL-Wert, wenn keine ELSE-Klausel angegeben wird.  
  
## <a name="remarks"></a>Hinweise  
 In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ist für CASE-Ausdrücke nur eine Schachtelung von 10 Ebenen zulässig.  
  
 Der CASE-Ausdruck kann nicht verwendet werden, um den Ablauf bei der Ausführung von Transact-SQL-Anweisungen, Anweisungsblöcken, benutzerdefinierten Funktionen und gespeicherten Prozeduren zu steuern. Eine Liste der Control-of-Flow-Methoden, finden Sie unter [Control-of-Flow-Sprache &#40; Transact-SQL &#41; ](~/t-sql/language-elements/control-of-flow.md).  
  
 Die CASE-Anweisung bewertet ihre Bedingungen sequenziell und hält bei der ersten Bedingung an, deren Bedingung erfüllt ist. In einigen Situationen wird ein Ausdruck bewertet, bevor eine CASE-Anweisung die Ergebnisse des Ausdrucks als Eingabe empfängt. Bei der Bewertung dieser Ausdrücke sind Fehler möglich. Aggregierte Ausdrücke, die in WHEN-Argumenten zu einer CASE-Anweisung angezeigt werden, werden zuerst bewertet und dann der CASE-Anweisung bereitgestellt. Beim Erzeugen des MAX-Aggregat-Werts erzeugt die folgende Abfrage beispielsweise einen Fehler aufgrund einer Division durch Null. Dies erfolgt vor dem Auswerten des CASE-Ausdrucks.  
  
```tsql  
WITH Data (value) AS   
(   
SELECT 0   
UNION ALL   
SELECT 1   
)   
SELECT   
   CASE   
      WHEN MIN(value) <= 0 THEN 0   
      WHEN MAX(1/value) >= 100 THEN 1   
   END   
FROM Data ;  
```  
  
 Sie sollten nur von der Reihenfolge der Bewertung der WHEN-Bedingungen für skalare Ausdrücke abhängig sein (einschließlich nicht korrelierter Unterabfragen, die Skalare zurückgeben), nicht für aggregierte Ausdrücke.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-using-a-select-statement-with-a-simple-case-expression"></a>A. Verwenden einer SELECT-Anweisung mit einem einfachen CASE-Ausdruck  
 Innerhalb einer `SELECT`-Anweisung ermöglicht ein einfacher `CASE`-Ausdruck nur eine Überprüfung auf Gleichheit. Andere Vergleiche werden nicht angestellt. Im folgenden Beispiel wird ein `CASE`-Ausdruck verwendet, um die Anzeige von Produktkategorien so zu ändern, dass sie leichter verständlich werden.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT   ProductNumber, Category =  
      CASE ProductLine  
         WHEN 'R' THEN 'Road'  
         WHEN 'M' THEN 'Mountain'  
         WHEN 'T' THEN 'Touring'  
         WHEN 'S' THEN 'Other sale items'  
         ELSE 'Not for sale'  
      END,  
   Name  
FROM Production.Product  
ORDER BY ProductNumber;  
GO  
  
```  
  
### <a name="b-using-a-select-statement-with-a-searched-case-expression"></a>B. Verwenden einer SELECT-Anweisung mit einem komplexen CASE-Ausdruck  
 Innerhalb einer `SELECT`-Anweisung können mit dem komplexen `CASE`-Ausdruck Werte im Resultset basierend auf den Vergleichsergebnissen ersetzt werden. Im folgenden Beispiel wird anstelle des Listenpreises ein Kommentar angezeigt, der vom Preisbereich der einzelnen Produkte abhängt.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT   ProductNumber, Name, "Price Range" =   
      CASE   
         WHEN ListPrice =  0 THEN 'Mfg item - not for resale'  
         WHEN ListPrice < 50 THEN 'Under $50'  
         WHEN ListPrice >= 50 and ListPrice < 250 THEN 'Under $250'  
         WHEN ListPrice >= 250 and ListPrice < 1000 THEN 'Under $1000'  
         ELSE 'Over $1000'  
      END  
FROM Production.Product  
ORDER BY ProductNumber ;  
GO  
  
```  
  
### <a name="c-using-case-in-an-order-by-clause"></a>C. Verwenden von CASE in einer ORDER BY-Klausel  
 In den folgenden Beispielen wird der CASE-Ausdruck in einer ORDER BY-Klausel verwendet, um die Sortierreihenfolge der Zeilen auf Grundlage eines angegebenen Spaltenwerts zu bestimmen. Im ersten Beispiel wird der Wert in der `SalariedFlag`-Spalte der `HumanResources.Employee`-Tabelle ausgewertet. Mitarbeiter, deren `SalariedFlag` auf 1 festgelegt wurde, werden nach `BusinessEntityID` in absteigender Folge zurückgegeben. Mitarbeiter, deren `SalariedFlag` auf 0 festgelegt wurde, werden nach `BusinessEntityID` in aufsteigender Folge zurückgegeben. Im zweiten Beispiel wird das Resultset nach der `TerritoryName`-Spalte sortiert, wenn die `CountryRegionName`-Spalte gleich 'United States' ist, und bei allen anderen Zeilen nach `CountryRegionName`.  
  
```  
SELECT BusinessEntityID, SalariedFlag  
FROM HumanResources.Employee  
ORDER BY CASE SalariedFlag WHEN 1 THEN BusinessEntityID END DESC  
        ,CASE WHEN SalariedFlag = 0 THEN BusinessEntityID END;  
GO  
  
```  
  
```  
SELECT BusinessEntityID, LastName, TerritoryName, CountryRegionName  
FROM Sales.vSalesPerson  
WHERE TerritoryName IS NOT NULL  
ORDER BY CASE CountryRegionName WHEN 'United States' THEN TerritoryName  
         ELSE CountryRegionName END;  
  
```  
  
### <a name="d-using-case-in-an-update-statement"></a>D. Verwenden von CASE in einer UPDATE-Anweisung  
 Im folgenden Beispiel wird der CASE-Ausdruck in einer UPDATE-Anweisung verwendet, um den Wert zu bestimmen, der für die `VacationHours`-Spalte für Mitarbeiter mit `SalariedFlag` gleich 0 festgelegt wurde. Wenn von `VacationHours` 10 Stunden subtrahiert werden, und dies einen negativen Wert ergibt, wird `VacationHours` um 40 Stunden erhöht; andernfalls wird `VacationHours` um 20 Stunden erhöht. Die OUTPUT-Klausel wird verwendet, um die Werte vor und nach dem Urlaub anzuzeigen.  
  
```  
USE AdventureWorks2012;  
GO  
UPDATE HumanResources.Employee  
SET VacationHours =   
    ( CASE  
         WHEN ((VacationHours - 10.00) < 0) THEN VacationHours + 40  
         ELSE (VacationHours + 20.00)  
       END  
    )  
OUTPUT Deleted.BusinessEntityID, Deleted.VacationHours AS BeforeValue,   
       Inserted.VacationHours AS AfterValue  
WHERE SalariedFlag = 0;  
  
```  
  
### <a name="e-using-case-in-a-set-statement"></a>E. Verwenden von CASE in einer SET-Anweisung  
 Im folgenden Beispiel wird der CASE-Ausdruck in einer SET-Anweisung in der Tabellenwertfunktion `dbo.GetContactInfo` verwendet. In der [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]-Datenbank werden alle Daten zu Personen in der `Person.Person`-Tabelle gespeichert. Die Person kann z. B. ein Mitarbeiter, herstellerkontakt oder Kunde sein. Die Funktion gibt den vor- und Nachnamen von einem bestimmten `BusinessEntityID` und den Kontakttyp für diese Person. Der CASE-Ausdruck in der SET-Anweisung bestimmt den Wert, der für die Spalte angezeigt `ContactType` basierend auf dem Vorhandensein der `BusinessEntityID` Spalte in der `Employee`, `Vendor`, oder `Customer` Tabellen.  
  
```  
  
USE AdventureWorks2012;  
GO  
CREATE FUNCTION dbo.GetContactInformation(@BusinessEntityID int)  
    RETURNS @retContactInformation TABLE   
(  
BusinessEntityID int NOT NULL,  
FirstName nvarchar(50) NULL,  
LastName nvarchar(50) NULL,  
ContactType nvarchar(50) NULL,  
    PRIMARY KEY CLUSTERED (BusinessEntityID ASC)  
)   
AS   
-- Returns the first name, last name and contact type for the specified contact.  
BEGIN  
    DECLARE   
        @FirstName nvarchar(50),   
        @LastName nvarchar(50),   
        @ContactType nvarchar(50);  
  
    -- Get common contact information  
    SELECT   
        @BusinessEntityID = BusinessEntityID,   
@FirstName = FirstName,   
        @LastName = LastName  
    FROM Person.Person   
    WHERE BusinessEntityID = @BusinessEntityID;  
  
    SET @ContactType =   
        CASE   
            -- Check for employee  
            WHEN EXISTS(SELECT * FROM HumanResources.Employee AS e   
                WHERE e.BusinessEntityID = @BusinessEntityID)   
                THEN 'Employee'  
  
            -- Check for vendor  
            WHEN EXISTS(SELECT * FROM Person.BusinessEntityContact AS bec  
                WHERE bec.BusinessEntityID = @BusinessEntityID)   
                THEN 'Vendor'  
  
            -- Check for store  
            WHEN EXISTS(SELECT * FROM Purchasing.Vendor AS v            
                WHERE v.BusinessEntityID = @BusinessEntityID)   
                THEN 'Store Contact'  
  
            -- Check for individual consumer  
            WHEN EXISTS(SELECT * FROM Sales.Customer AS c   
                WHERE c.PersonID = @BusinessEntityID)   
                THEN 'Consumer'  
        END;  
  
    -- Return the information to the caller  
    IF @BusinessEntityID IS NOT NULL   
    BEGIN  
        INSERT @retContactInformation  
        SELECT @BusinessEntityID, @FirstName, @LastName, @ContactType;  
    END;  
  
    RETURN;  
END;  
GO  
  
SELECT BusinessEntityID, FirstName, LastName, ContactType  
FROM dbo.GetContactInformation(2200);  
GO  
SELECT BusinessEntityID, FirstName, LastName, ContactType  
FROM dbo.GetContactInformation(5);  
  
```  
  
### <a name="f-using-case-in-a-having-clause"></a>F. Verwenden von CASE in einer HAVING-Klausel  
 Im folgenden Beispiel wird der CASE-Ausdruck in einer HAVING-Klausel verwendet, um die von der SELECT-Anweisung zurückgegebenen Zeilen einzuschränken. Die Anweisung gibt den maximalen Stundensatz für jede Berufsbezeichnung in der `HumanResources.Employee` Tabelle. Die HAVING-Klausel beschränkt die Bezeichnungen auf diejenigen Positionen, die von Männern mit einem maximalen Stundensatz von über 40 Dollar bzw. von Frauen mit einem maximalen Stundensatz von über 42 Dollar besetzt werden.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT JobTitle, MAX(ph1.Rate)AS MaximumRate  
FROM HumanResources.Employee AS e  
JOIN HumanResources.EmployeePayHistory AS ph1 ON e.BusinessEntityID = ph1.BusinessEntityID  
GROUP BY JobTitle  
HAVING (MAX(CASE WHEN Gender = 'M'   
        THEN ph1.Rate   
        ELSE NULL END) > 40.00  
     OR MAX(CASE WHEN Gender  = 'F'   
        THEN ph1.Rate    
        ELSE NULL END) > 42.00)  
ORDER BY MaximumRate DESC;  
  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Beispiele: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] und[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="g-using-a-select-statement-with-a-case-expression"></a>G. Verwenden eine SELECT-Anweisung mit einer CASE-Ausdruck  
 Innerhalb einer SELECT-Anweisung können der CASE-Ausdruck für die Werte im Resultset basierend auf den Vergleichsergebnissen ersetzt werden. Im folgenden Beispiel wird den CASE-Ausdruck so ändern Sie die Anzeige von Produktkategorien, die leichter verständlich zu machen. Wenn kein Wert vorhanden, den Text "nicht für den Verkauf" wird angezeigt.  
  
```  
-- Uses AdventureWorks  
  
SELECT   ProductAlternateKey, Category =  
      CASE ProductLine  
         WHEN 'R' THEN 'Road'  
         WHEN 'M' THEN 'Mountain'  
         WHEN 'T' THEN 'Touring'  
         WHEN 'S' THEN 'Other sale items'  
         ELSE 'Not for sale'  
      END,  
   EnglishProductName  
FROM dbo.DimProduct  
ORDER BY ProductKey;  
```  
  
### <a name="h-using-case-in-an-update-statement"></a>H. Verwenden von CASE in einer UPDATE-Anweisung  
 Im folgenden Beispiel wird der CASE-Ausdruck in einer UPDATE-Anweisung verwendet, um den Wert zu bestimmen, der für die `VacationHours`-Spalte für Mitarbeiter mit `SalariedFlag` gleich 0 festgelegt wurde. Wenn von `VacationHours` 10 Stunden subtrahiert werden, und dies einen negativen Wert ergibt, wird `VacationHours` um 40 Stunden erhöht; andernfalls wird `VacationHours` um 20 Stunden erhöht.  
  
```  
-- Uses AdventureWorks   
  
UPDATE dbo.DimEmployee  
SET VacationHours =   
    ( CASE  
         WHEN ((VacationHours - 10.00) < 0) THEN VacationHours + 40  
         ELSE (VacationHours + 20.00)   
       END  
    )   
WHERE SalariedFlag = 0;  
  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Ausdrücke &#40; Transact-SQL &#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [COALESCE &#40; Transact-SQL &#41;](../../t-sql/language-elements/coalesce-transact-sql.md)   
 [IIF &#40; Transact-SQL &#41;](../../t-sql/functions/logical-functions-iif-transact-sql.md)   
 [Wählen Sie &#40; Transact-SQL &#41;](../../t-sql/functions/logical-functions-choose-transact-sql.md)  
  
  




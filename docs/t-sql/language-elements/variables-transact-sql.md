---
title: Variablen (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 09/12/2017
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
dev_langs:
- TSQL
ms.assetid: f372ae86-a003-40af-92de-fa52e3eea13f
caps.latest.revision: 12
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: baf5682919538d5b3ef593726bdebb1f7cb7fbcc
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="variables-transact-sql"></a>Variablen (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Eine lokale Transact-SQL-Variable ist ein Objekt, das einen einzelnen Datenwert eines bestimmten Typs aufnehmen kann. Variablen in Batches und Skripts werden in der Regel wie folgt verwendet: 

* Als Zähler, der entweder zählt, wie häufig eine Schleife durchlaufen wird, oder der steuert, wie häufig die Schleife durchlaufen werden soll.
* Zur Aufnahme eines Datenwerts, der von einer Anweisung zur Ablaufsteuerung getestet werden soll.
* Zum Speichern eines Datenwerts, der vom Rückgabecode einer gespeicherten Prozedur oder vom Funktionsrückgabewert zurückgegeben werden soll.

> [!NOTE]
> Die Namen einiger Transact-SQL-Systemfunktionen beginnen mit zwei *@*-Zeichen (@@). Obwohl die @@functions in früheren Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] als globale Variablen bezeichnet wurden, handelt es sich dabei keineswegs um Variablen, und sie verhalten sich auch nicht wie Variablen. Die @@functions sind Systemfunktionen, deren Syntaxverwendung den Regeln für Funktionen entspricht.

Das folgende Skript erstellt eine kleine Testtabelle, die mit 26 Zeilen aufgefüllt wird. Das Skript verwendet eine Variable zur Durchführung von drei Aufgaben: 

* Steuern, wie viele Zeilen eingefügt werden, indem gesteuert wird, wie oft die Schleife durchlaufen wird.
* Bereitstellen des Werts, der in die Spalte mit ganzen Zahlen eingefügt wird.
* Fungieren als Teil des Ausdrucks, der Buchstaben generiert, die in die Zeichenspalte eingefügt werden sollen.  

```sql
-- Create the table.
CREATE TABLE TestTable (cola int, colb char(3));
GO
SET NOCOUNT ON;
GO
-- Declare the variable to be used.
DECLARE @MyCounter int;

-- Initialize the variable.
SET @MyCounter = 0;

-- Test the variable to see if the loop is finished.
WHILE (@MyCounter < 26)
BEGIN;
   -- Insert a row into the table.
   INSERT INTO TestTable VALUES
       -- Use the variable to provide the integer value
       -- for cola. Also use it to generate a unique letter
       -- for each row. Use the ASCII function to get the
       -- integer value of 'a'. Add @MyCounter. Use CHAR to
       -- convert the sum back to the character @MyCounter
       -- characters after 'a'.
       (@MyCounter,
        CHAR( ( @MyCounter + ASCII('a') ) )
       );
   -- Increment the variable to count this iteration
   -- of the loop.
   SET @MyCounter = @MyCounter + 1;
END;
GO
SET NOCOUNT OFF;
GO
-- View the data.
SELECT cola, colb
FROM TestTable;
GO
DROP TABLE TestTable;
GO
```

## <a name="declaring-a-transact-sql-variable"></a>Deklarieren einer Transact-SQL-Variablen
Die DECLARE-Anweisung initialisiert eine Transact-SQL-Variable auf die folgende Weise: 
* Zuweisen eines Namens. Der Name muss ein einzelnes @-Zeichen als erstes Zeichen enthalten.
* Zuweisen eines vom System bereitgestellten oder benutzerdefinierten Datentyps und einer Länge. Für numerische Variablen werden außerdem die Genauigkeit und die Dezimalstellen zugewiesen. Für Variablen des Typs XML kann eine optionale Schemaauflistung zugewiesen werden.
* Festlegen des Werts auf NULL.

Beispielsweise erstellt die folgende **DECLARE**-Anweisung eine lokale Variable namens **@mycounter** vom int-Datentyp.  
```sql
DECLARE @MyCounter int;
```
Zum Deklarieren von mehreren lokalen Variablen verwenden Sie ein Komma nach der ersten definierten lokalen Variablen und geben dann den Namen und den Datentyp der nächsten lokalen Variablen an.

Die folgende **DECLARE**-Anweisung erstellt z.B. drei lokale Variablen mit den Namen **@LastName**, **@FirstName** und **@StateProvince** und initialisiert alle mit NULL:  
```sql
DECLARE @LastName nvarchar(30), @FirstName nvarchar(20), @StateProvince nchar(2);
```

Der Gültigkeitsbereich einer Variablen ist der Bereich von Transact-SQL-Anweisungen, die auf die Variable verweisen können. Der Gültigkeitsbereich einer Variablen reicht von dem Punkt, an dem sie deklariert wurde, bis zum Ende des Batches oder der gespeicherten Prozedur, in dem bzw. der sie deklariert wurde. Das folgende Skript generiert z. B. einen Syntaxfehler, weil die Variable in einem Batch deklariert wird und dann in einem anderen Batch auf sie verwiesen wird:  
```sql
USE AdventureWorks2014;
GO
DECLARE @MyVariable int;
SET @MyVariable = 1;
-- Terminate the batch by using the GO keyword.
GO 
-- @MyVariable has gone out of scope and no longer exists.

-- This SELECT statement generates a syntax error because it is
-- no longer legal to reference @MyVariable.
SELECT BusinessEntityID, NationalIDNumber, JobTitle
FROM HumanResources.Employee
WHERE BusinessEntityID = @MyVariable;
```

Variablen haben einen lokalen Gültigkeitsbereich und sind nur im Batch bzw. in der Prozedur sichtbar, in dem bzw. in der sie definiert sind. Im folgenden Beispiel bietet der zur Ausführung von sp_executesql erstellte geschachtelte Gültigkeitsbereich keinen Zugriff auf die Variable, die im höheren Geltungsbereich deklariert ist, und gibt einen Fehler zurück.  

```sql
DECLARE @MyVariable int;
SET @MyVariable = 1;
EXECUTE sp_executesql N'SELECT @MyVariable'; -- this produces an error
```

## <a name="setting-a-value-in-a-transact-sql-variable"></a>Festlegen eines Werts in einer Transact-SQL-Variablen

Für eine Variable, die deklariert wird, wird der Wert anfangs auf NULL festgelegt. Verwenden Sie die SET-Anweisung, um einer Variablen einen Wert zuzuweisen. Diese Methode ist für die Zuweisung eines Werts zu einer Variablen zu bevorzugen. Einer Variablen kann außerdem ein Wert zugewiesen werden, indem auf sie in der Auswahlliste einer SELECT-Anweisung verwiesen wird.

Wenn Sie einer Variablen einen Wert mit der SET-Anweisung zuweisen, geben Sie den Variablennamen und den Wert an, der der Variablen zugewiesen werden soll. Diese Methode ist für die Zuweisung eines Werts zu einer Variablen zu bevorzugen. Der folgende Batch deklariert z. B. zwei Variablen, weist ihnen Werte zu und verwendet sie dann in der `WHERE`-Klausel einer `SELECT`-Anweisung:  

```sql
USE AdventureWorks2014;
GO
-- Declare two variables.
DECLARE @FirstNameVariable nvarchar(50),
   @PostalCodeVariable nvarchar(15);

-- Set their values.
SET @FirstNameVariable = N'Amy';
SET @PostalCodeVariable = N'BA5 3HX';

-- Use them in the WHERE clause of a SELECT statement.
SELECT LastName, FirstName, JobTitle, City, StateProvinceName, CountryRegionName
FROM HumanResources.vEmployee
WHERE FirstName = @FirstNameVariable
   OR PostalCode = @PostalCodeVariable;
GO
```

Einer Variablen kann außerdem ein Wert zugewiesen werden, indem auf sie in einer Auswahlliste verwiesen wird. Wenn auf eine Variable in einer Auswahlliste verwiesen wird, sollte ihr ein Skalarwert zugewiesen werden, oder die SELECT-Anweisung sollte nur eine Zeile zurückgeben. Zum Beispiel:  

```sql
USE AdventureWorks2014;
GO
DECLARE @EmpIDVariable int;

SELECT @EmpIDVariable = MAX(EmployeeID)
FROM HumanResources.Employee;
GO
```

> [!WARNING]
> Wenn es in einer einzelnen SELECT-Anweisung mehrere Zuordnungsklauseln gibt, kann SQL Server die Bewertungsreihenfolge der Ausdrücke nicht sicherstellen. Beachten Sie, dass die Auswirkungen nur dann sichtbar sind, wenn es Verweise zwischen den Zuordnungen gibt.

Wenn eine SELECT-Anweisung mehrere Zeilen zurückgibt und die Variable auf einen nicht skalaren Ausdruck verweist, wird die Variable auf den Wert festgelegt, der für den Ausdruck in der letzten Zeile des Resultsets zurückgegeben wurde. Im folgenden Batch wird z.B. **@EmpIDVariable** auf den **BusinessEntityID**-Wert der zuletzt zurückgegebenen Zeile festgelegt, der 1 ist:  

```sql
USE AdventureWorks2014;
GO
DECLARE @EmpIDVariable int;

SELECT @EmpIDVariable = BusinessEntityID
FROM HumanResources.Employee
ORDER BY BusinessEntityID DESC;

SELECT @EmpIDVariable;
GO
```

## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Declare @local_variable](../../t-sql/language-elements/declare-local-variable-transact-sql.md)  
 [SET@local_variable](../../t-sql/language-elements/set-local-variable-transact-sql.md)  
 [SELECT @local_variable](../../t-sql/language-elements/select-local-variable-transact-sql.md)  
 [Ausdrücke &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [Verbundoperatoren &#40;Transact-SQL&#41;](../../t-sql/language-elements/compound-operators-transact-sql.md)   
  
  

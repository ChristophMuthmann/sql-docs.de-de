---
title: Table (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/23/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- table data type [SQL Server]
- table variables [SQL Server]
ms.assetid: 1ef0b60e-a64c-4e97-847b-67930e3973ef
caps.latest.revision: 48
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b22ecfa04f949af77df974abc3359b7bc5144a82
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="table-transact-sql"></a>table (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Entspricht einem speziellen Datentyp, der verwendet werden kann, um ein Resultset für die Verarbeitung zu einem späteren Zeitpunkt zu speichern. **Tabelle** dient in erster Linie für die temporäre Speicherung einer Reihe von Zeilen, die als Resultset einer Tabellenwertfunktion zurückgegeben. Funktionen und Variablen vom Typ deklariert werden **Tabelle**. **Tabelle** Variablen können in Funktionen, gespeicherte Prozeduren und Batches verwendet werden. Deklarieren von Variablen des Typs **Tabelle**, verwenden Sie [DECLARE @local_variable ](../../t-sql/language-elements/declare-local-variable-transact-sql.md).
  

**Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis zur [aktuellen Version](http://go.microsoft.com/fwlink/p/?LinkId=299658)), [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].
  
![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Syntax  
  
```sql
table_type_definition ::=   
    TABLE ( { <column_definition> | <table_constraint> } [ ,...n ] )   
  
<column_definition> ::=   
    column_name scalar_data_type   
    [ COLLATE <collation_definition> ]   
    [ [ DEFAULT constant_expression ] | IDENTITY [ ( seed , increment ) ] ]   
    [ ROWGUIDCOL ]   
    [ column_constraint ] [ ...n ]   
  
 <column_constraint> ::=   
    { [ NULL | NOT NULL ]   
    | [ PRIMARY KEY | UNIQUE ]   
    | CHECK ( logical_expression )   
    }   
  
<table_constraint> ::=   
     { { PRIMARY KEY | UNIQUE } ( column_name [ ,...n ] )  
     | CHECK ( logical_expression )   
     }   
```  
  
## <a name="arguments"></a>Argumente  
*table_type_definition*  
Dieselbe Teilmenge von Informationen, die zum Definieren einer Tabelle in CREATE TABLE verwendet wird. Die Tabellendeklaration schließt Spaltendefinitionen, Namen, Datentypen und Einschränkungen ein. Die einzigen zulässigen Einschränkungstypen sind PRIMARY KEY, UNIQUE KEY und NULL.  
Weitere Informationen zur Syntax finden Sie unter [CREATE TABLE &#40; Transact-SQL &#41; ](../../t-sql/statements/create-table-transact-sql.md), [Erstellen FUNCTION &#40; Transact-SQL &#41; ](../../t-sql/statements/create-function-transact-sql.md), und [DECLARE @local_variable &#40; Transact-SQL &#41; ](../../t-sql/language-elements/declare-local-variable-transact-sql.md).
  
*collation_definition*  
Ist die Sortierung der Spalte, die an eine [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows-Gebietsschema und einer Vergleichsart, einem Windows-Gebietsschema und der Binärschreibweise oder einer [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Sortierung. Wenn *Collation_definition* nicht angegeben ist, erbt die Spalte die Sortierung der aktuellen Datenbank. Wenn die Spalte als CLR-benutzerdefinierter Typ (Common Language Runtime) definiert ist, erbt die Spalte die Sortierung des benutzerdefinierten Typs.
  
## <a name="remarks"></a>Hinweise  
**Tabelle** Variablen können anhand des Namens in der FROM-Klausel eines Batches verwiesen werden, wie im folgende Beispiel gezeigt:
  
```sql
SELECT Employee_ID, Department_ID FROM @MyTableVar;  
```  
  
Außerhalb einer FROM-Klausel **Tabelle** Variablen müssen mit einem Alias verwiesen werden, wie im folgenden Beispiel gezeigt:
  
```sql
SELECT EmployeeID, DepartmentID   
FROM @MyTableVar m  
JOIN Employee on (m.EmployeeID =Employee.EmployeeID AND  
   m.DepartmentID = Employee.DepartmentID);  
```  
  
**Tabelle** -Variablen bieten die folgenden Vorteile für kleine Abfragen mit Abfragepläne, die nicht ändern und wenn Neukompilierung Bedenken bestimmende sind:
-   Ein **Tabelle** -Variable verhält sich wie eine lokale Variable. Sie hat einen fest definierten Bereich. Dies ist die Funktion, die gespeicherte Prozedur oder der Batch, in der bzw. dem sie deklariert ist.  
     Innerhalb ihres Bereichs eine **Tabelle** -Variable wie eine reguläre Tabelle verwendet werden kann. Sie kann überall angewendet werden, wo eine Tabelle oder ein Tabellenausdruck in SELECT-, INSERT-, UPDATE- und DELETE-Anweisungen verwendet wird. Allerdings **Tabelle** kann nicht verwendet werden, in der folgenden Anweisung:  
  
```sql
SELECT select_list INTO table_variable;
```
  
**Tabelle** Variablen werden automatisch bereinigt, am Ende der Funktion, der gespeicherten Prozedur oder des Batches, die in der sie definiert sind.
  
-   **Tabelle** Variablen, die in gespeicherten Prozeduren verwendet werden, verursachen weniger neukompilierungen der gespeicherten Prozeduren als wenn die temporäre Tabellen verwendet werden, wenn es sind keine kostenbasierten Optionen, die die Leistung beeinträchtigen.  
-   Transaktionen, die im Zusammenhang mit **Tabelle** Variablen zuletzt nur für die Dauer eines Updates auf die **Tabelle** Variable. Aus diesem Grund **Tabelle** Variablen erfordern weniger Sperr- und protokollierungsressourcen.  
  
## <a name="limitations-and-restrictions"></a>Einschränkungen
**Tabelle** Variablen keine Verteilungsstatistiken, sie werden nicht ausgelöst, erneut kompiliert. Daher erstellt der Optimierer in vielen Fällen einen Abfrageplan unter der Annahme, dass die Tabellenvariable keine Zeilen enthält. Aus diesem Grund sollten Sie Tabellenvariablen mit Vorsicht verwenden, wenn Sie von einer großen Anzahl von Zeilen (mehr als 100) ausgehen. Für solche Fälle sind temporäre Tabellen möglicherweise die bessere Lösung. Verwenden Sie für Abfragen, die die Tabellenvariable mit anderen Tabellen verknüpfen alternativ den RECOMPILE-Hinweis, wodurch der Optimierer die korrekte Kardinalität für die Tabellenvariable verwendet.
  
**Tabelle** Variablen werden nicht unterstützt, der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] kostenbasierten ansatzmodell des Optimierers. Daher sollten sie nicht verwendet werden, wenn kostenbasierte Optionen erforderlich sind, um einen effizienten Abfrageplan zu erzielen. Temporäre Tabellen werden bevorzugt, wenn kostenbasierte Optionen erforderlich sind. Dies schließt in der Regel Abfragen mit Joins, Parallelverarbeitungsentscheidungen und Indexauswahloptionen ein.
  
Abfragen, die ändern **Tabelle** Variablen keine parallelen Abfrageausführungsplänen generiert. Leistung kann beeinträchtigt werden, wenn sehr große **Tabelle** Variablen oder **Tabelle** -Variablen in komplexen Abfragen geändert werden. Erwägen Sie in vergleichbaren Situationen stattdessen die Verwendung temporärer Tabellen. Weitere Informationen finden Sie unter [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md). Abfragen, die gelesen **Tabelle** Variablen, ohne sie zu ändern, können weiterhin parallelisiert werden.
  
Indizes können nicht erstellt werden explizit auf **Tabelle** Variablen und keine Statistiken bleiben auf **Tabelle** Variablen. In einigen Fällen kann die Leistung möglicherweise verbessert werden, indem stattdessen temporäre Tabellen verwendet werden, die Indizes und Statistiken unterstützen. Weitere Informationen zu temporären Tabellen finden Sie unter [CREATE TABLE &#40; Transact-SQL &#41; ](../../t-sql/statements/create-table-transact-sql.md).
  
CHECK-Einschränkungen, Standardwerte und berechnete Spalten in der **Tabelle** Typdeklaration von benutzerdefinierten Funktionen kann nicht aufgerufen werden.
  
Zuweisungsvorgänge zwischen **Tabelle** Variablen wird nicht unterstützt.
  
Da **Tabelle** Variablen einen beschränkten Bereich haben und nicht Teil der persistenten Datenbank sind, sind sie von Transaktionsrollbacks nicht betroffen.
  
Tabellenvariablen können nicht geändert werden, nachdem sie erstellt wurden.
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-declaring-a-variable-of-type-table"></a>A. Deklarieren einer Variablen vom Typ "table"  
Im folgenden Beispiel wird eine `table`-Variable erstellt, die die in der OUTPUT-Klausel der UPDATE-Anweisung angegebenen Werte speichert. Es folgen zwei `SELECT`-Anweisungen, die die Werte in `@MyTableVar` und die Ergebnisse des Updatevorgangs in der `Employee`-Tabelle zurückgeben. Beachten Sie, dass die Ergebnisse in die `INSERTED.ModifiedDate` Spalte unterscheiden sich von den Werten in der `ModifiedDate` Spalte in der `Employee` Tabelle. Der Grund dafür ist, dass der `AFTER UPDATE`-Trigger, der den Wert von `ModifiedDate` auf das aktuelle Datum aktualisiert, in der `Employee`-Tabelle definiert wird. Die von `OUTPUT` zurückgegebenen Spalten spiegeln jedoch die Daten wider, bevor Trigger ausgelöst werden. Weitere Informationen finden Sie unter [OUTPUT-Klausel &#40; Transact-SQL &#41; ](../../t-sql/queries/output-clause-transact-sql.md).
  
```sql
USE AdventureWorks2012;  
GO  
DECLARE @MyTableVar table(  
    EmpID int NOT NULL,  
    OldVacationHours int,  
    NewVacationHours int,  
    ModifiedDate datetime);  
UPDATE TOP (10) HumanResources.Employee  
SET VacationHours = VacationHours * 1.25   
OUTPUT INSERTED.BusinessEntityID,  
       DELETED.VacationHours,  
       INSERTED.VacationHours,  
       INSERTED.ModifiedDate  
INTO @MyTableVar;  
--Display the result set of the table variable.  
SELECT EmpID, OldVacationHours, NewVacationHours, ModifiedDate  
FROM @MyTableVar;  
GO  
--Display the result set of the table.  
--Note that ModifiedDate reflects the value generated by an  
--AFTER UPDATE trigger.  
SELECT TOP (10) BusinessEntityID, VacationHours, ModifiedDate  
FROM HumanResources.Employee;  
GO  
```  
  
### <a name="b-creating-an-inline-table-valued-function"></a>B. Erstellen einer Inline-Tabellenwertfunktion  
Das folgende Beispiel gibt eine Inline-Tabellenwertfunktion zurück. Es gibt drei Spalten `ProductID`, `Name` sowie das Aggregat der Jahr-bis-heute Summen nach Geschäft als `YTD Total` für jedes Produkt, das an das Geschäft verkauft wurde.
  
```sql
USE AdventureWorks2012;  
GO  
IF OBJECT_ID (N'Sales.ufn_SalesByStore', N'IF') IS NOT NULL  
    DROP FUNCTION Sales.ufn_SalesByStore;  
GO  
CREATE FUNCTION Sales.ufn_SalesByStore (@storeid int)  
RETURNS TABLE  
AS  
RETURN   
(  
    SELECT P.ProductID, P.Name, SUM(SD.LineTotal) AS 'Total'  
    FROM Production.Product AS P   
    JOIN Sales.SalesOrderDetail AS SD ON SD.ProductID = P.ProductID  
    JOIN Sales.SalesOrderHeader AS SH ON SH.SalesOrderID = SD.SalesOrderID  
    JOIN Sales.Customer AS C ON SH.CustomerID = C.CustomerID  
    WHERE C.StoreID = @storeid  
    GROUP BY P.ProductID, P.Name  
);  
GO  
```  
  
Rufen Sie die Funktion mit dieser Abfrage auf.
  
```sql
SELECT * FROM Sales.ufn_SalesByStore (602);  
```  
  
## <a name="see-also"></a>Siehe auch
[COLLATE &#40; Transact-SQL &#41;](http://msdn.microsoft.com/library/4ba6b7d8-114a-4f4e-bb38-fe5697add4e9)  
[CREATE FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/create-function-transact-sql.md)  
[Benutzerdefinierte Funktionen](../../relational-databases/user-defined-functions/user-defined-functions.md)  
[CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)  
[DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)  
[Verwenden des Table-Valued Parameters &#40; Datenbankmodul &#41;](../../relational-databases/tables/use-table-valued-parameters-database-engine.md)  
[Abfragehinweise &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-query.md)
  
  


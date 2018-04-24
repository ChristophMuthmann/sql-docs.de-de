---
title: table (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 7/23/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: t-sql|data-types
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- table data type [SQL Server]
- table variables [SQL Server]
ms.assetid: 1ef0b60e-a64c-4e97-847b-67930e3973ef
caps.latest.revision: 48
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: c36bc6a6cf7b1d44dfa480932d850b945b1d7056
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="table-transact-sql"></a>table (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Entspricht einem speziellen Datentyp, der verwendet werden kann, um ein Resultset für die Verarbeitung zu einem späteren Zeitpunkt zu speichern. **table** wird hauptsächlich für die temporäre Speicherung von einem Zeilensatz verwendet, der als Resultset einer Tabellenwertfunktion zurückgegeben wurde. Für Funktionen und Variablen kann der Typ **table** angegeben werden. **table**-Variablen können in Funktionen, gespeicherten Prozeduren und Batches verwendet werden. Verwenden Sie zum Deklarieren von Variablen des **table**-Typs die Anweisung [DECLARE @local_variable](../../t-sql/language-elements/declare-local-variable-transact-sql.md).
  

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
Weitere Informationen zur Syntax finden Sie unter [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md), [CREATE FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/create-function-transact-sql.md) und [DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md).
  
*collation_definition*  
Die Sortierung einer Spalte, die aus einem [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows-Gebietsschema und einer Vergleichsart, einem Windows-Gebietsschema und der Binärschreibweise oder einer [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Sortierung besteht. Wenn *collation_definition* nicht angegeben ist, erbt die Spalte die Sortierung der aktuellen Datenbank. Wenn die Spalte als CLR-benutzerdefinierter Typ (Common Language Runtime) definiert ist, erbt die Spalte die Sortierung des benutzerdefinierten Typs.
  
## <a name="remarks"></a>Remarks  
Auf Variablen vom Typ **table** kann anhand des Namens in der FROM-Klausel eines Batches verwiesen werden, wie im folgenden Beispiel gezeigt wird:
  
```sql
SELECT Employee_ID, Department_ID FROM @MyTableVar;  
```  
  
Außerhalb einer FROM-Klausel muss ein Alias für Verweise auf **table**-Variablen verwendet werden, wie im folgenden Beispiel gezeigt wird:
  
```sql
SELECT EmployeeID, DepartmentID   
FROM @MyTableVar m  
JOIN Employee on (m.EmployeeID =Employee.EmployeeID AND  
   m.DepartmentID = Employee.DepartmentID);  
```  
  
**table**-Variablen bieten die folgenden Vorteile für Abfragen mit kleinerem Umfang, die über Abfragepläne verfügen, die sich nicht ändern (gilt auch für Szenarios mit vorwiegend vorhandenen Neukompilierungsaspekten):
-   Eine **table**-Variable verhält sich wie eine lokale Variable. Sie hat einen fest definierten Bereich. Dies ist die Funktion, die gespeicherte Prozedur oder der Batch, in der bzw. dem sie deklariert ist.  
     Innerhalb dieses Bereichs kann eine **table**-Variable wie eine reguläre Tabelle verwendet werden. Sie kann überall angewendet werden, wo eine Tabelle oder ein Tabellenausdruck in SELECT-, INSERT-, UPDATE- und DELETE-Anweisungen verwendet wird. **table** kann jedoch nicht in der folgenden Anweisung verwendet werden:  
  
```sql
SELECT select_list INTO table_variable;
```
  
Für **table**-Variablen wird automatisch am Ende der Funktion, der gespeicherten Prozedur oder des Batches, in der bzw. dem sie definiert sind, ein Cleanup ausgeführt.
  
-   In gespeicherten Prozeduren verwendete **table**-Variablen verursachen weniger Neukompilierungen der gespeicherten Prozeduren als im Fall der Verwendung von temporären Tabellen, wenn keine kostenbasierten Optionen vorhanden sind, die die Leistung beeinflussen.  
-   Transaktionen, an denen **table**-Variablen beteiligt sind, dauern nur so lange wie das Update der **table**-Variablen. Daher sind für **table**-Variablen weniger Sperr- und Protokollierungsressourcen erforderlich.  
  
## <a name="limitations-and-restrictions"></a>Einschränkungen
**table**-Variablen verfügen über keine Verteilungsstatistiken und lösen kein erneutes Kompilieren aus. Daher erstellt der Optimierer in vielen Fällen einen Abfrageplan unter der Annahme, dass die Tabellenvariable keine Zeilen enthält. Aus diesem Grund sollten Sie Tabellenvariablen mit Vorsicht verwenden, wenn Sie von einer großen Anzahl von Zeilen (mehr als 100) ausgehen. Für solche Fälle sind temporäre Tabellen möglicherweise die bessere Lösung. Sie können bei Abfragen, die einen Join der Tabelle mit anderen Tabellen ausführen, auch den RECOMPILE-Hinweis verwenden. Dieser führt dazu, dass der Optimierer die korrekte Kardinalität für die Tabellenvariable verwendet.
  
**table**-Variablen werden im kostenbasierten Ansatzmodell des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Optimierers nicht unterstützt. Daher sollten sie nicht verwendet werden, wenn kostenbasierte Optionen erforderlich sind, um einen effizienten Abfrageplan zu erzielen. Temporäre Tabellen werden bevorzugt, wenn kostenbasierte Optionen erforderlich sind. Dies schließt in der Regel Abfragen mit Joins, Parallelverarbeitungsentscheidungen und Indexauswahloptionen ein.
  
Abfragen, die **table**-Variablen ändern, generieren keine Pläne für die parallele Abfrageausführung. Die Leistung kann beeinträchtigt sein, wenn sehr große **table**-Variablen oder **table**-Variablen in komplexen Abfragen geändert werden. Erwägen Sie in vergleichbaren Situationen stattdessen die Verwendung temporärer Tabellen. Weitere Informationen finden Sie unter [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md). Abfragen, die **table**-Variablen lesen, ohne sie zu ändern, können weiterhin parallelisiert werden.
  
Die explizite Erstellung von Indizes für **table**-Variablen ist nicht möglich, zudem werden für **table**-Variablen keine Statistiken geführt. In einigen Fällen kann die Leistung möglicherweise verbessert werden, indem stattdessen temporäre Tabellen verwendet werden, die Indizes und Statistiken unterstützen. Weitere Informationen zu temporären Tabellen finden Sie unter [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md).
  
CHECK-Einschränkungen, DEFAULT-Werte und berechnete Spalten in der **table**-Typdeklaration können keine benutzerdefinierten Funktionen aufrufen.
  
Zuweisungsvorgänge zwischen **table**-Variablen werden nicht unterstützt.
  
Transaktionsrollbacks wirken sich nicht auf **table**-Variablen aus, da diese Variablen einen beschränkten Bereich haben und kein Teil der permanenten Datenbank sind.
  
Tabellenvariablen können nicht geändert werden, nachdem sie erstellt wurden.
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-declaring-a-variable-of-type-table"></a>A. Deklarieren einer Variablen vom Typ "table"  
Im folgenden Beispiel wird eine `table`-Variable erstellt, die die in der OUTPUT-Klausel der UPDATE-Anweisung angegebenen Werte speichert. Es folgen zwei `SELECT`-Anweisungen, die die Werte in `@MyTableVar` und die Ergebnisse des Updatevorgangs in der `Employee`-Tabelle zurückgeben. Beachten Sie, dass sich die Ergebnisse in der `INSERTED.ModifiedDate`-Spalte von den Werten in der `ModifiedDate`-Spalte in der `Employee`-Tabelle unterscheiden. Der Grund dafür ist, dass der `AFTER UPDATE`-Trigger, der den Wert von `ModifiedDate` auf das aktuelle Datum aktualisiert, in der `Employee`-Tabelle definiert wird. Die von `OUTPUT` zurückgegebenen Spalten spiegeln jedoch die Daten wider, bevor Trigger ausgelöst werden. Weitere Informationen finden Sie unter [OUTPUT-Klausel &#40;Transact-SQL&#41;](../../t-sql/queries/output-clause-transact-sql.md).
  
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
Das folgende Beispiel gibt eine Inline-Tabellenwertfunktion zurück. Die Funktion gibt drei Spalten `ProductID`, `Name` und das Aggregat der gesamten Verkäufe des Jahres (nach Filiale sortiert) als `YTD Total` für jedes Produkt zurück, das an die Filiale verkauft wurde.
  
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
[COLLATE &#40;Transact-SQL&#41;](http://msdn.microsoft.com/library/4ba6b7d8-114a-4f4e-bb38-fe5697add4e9)  
[CREATE FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/create-function-transact-sql.md)  
[Benutzerdefinierte Funktionen](../../relational-databases/user-defined-functions/user-defined-functions.md)  
[CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)  
[DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)  
[Verwenden von Tabellenwertparametern &#40;Datenbank-Engine&#41;](../../relational-databases/tables/use-table-valued-parameters-database-engine.md)  
[Abfragehinweise &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-query.md)
  
  

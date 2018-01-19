---
title: Deklarieren Sie @local_variable (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/24/2017
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
- DECLARE
- DECLARE_TSQL
dev_langs: TSQL
helpviewer_keywords:
- table-valued parameters
- variables [SQL Server], declaring
- DECLARE statement
- declaring variables
ms.assetid: d1635ebb-f751-4de1-8bbc-cae161f90821
caps.latest.revision: "76"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 70bfea2777f5f96769d4296c8fbb7f2acbd20e4f
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/19/2018
---
# <a name="declare-localvariable-transact-sql"></a>Deklarieren Sie @local_variable (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Variablen werden im Hauptteil eines Batchs oder einer Prozedur mit einer DECLARE-Anweisung deklariert. Die Werte werden mithilfe einer SET- oder SELECT-Anweisung zugewiesen. Cursorvariablen können mit dieser Anweisung deklariert und mit anderen cursorspezifischen Anweisungen verwendet werden. Nach der Deklaration werden alle Variablen mit NULL initialisiert, es sei denn, ein Wert wurde als Teil der Deklaration angegeben.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
DECLARE   
{   
    { @local_variable [AS] data_type  [ = value ] }  
  | { @cursor_variable_name CURSOR }  
} [,...n]   
| { @table_variable_name [AS] <table_type_definition> }   
  
<table_type_definition> ::=   
     TABLE ( { <column_definition> | <table_constraint> } [ ,...n] )   
  
<column_definition> ::=   
     column_name { scalar_data_type | AS computed_column_expression }  
     [ COLLATE collation_name ]   
     [ [ DEFAULT constant_expression ] | IDENTITY [ (seed ,increment ) ] ]   
     [ ROWGUIDCOL ]   
     [ <column_constraint> ]   
  
<column_constraint> ::=   
     { [ NULL | NOT NULL ]   
     | [ PRIMARY KEY | UNIQUE ]   
     | CHECK ( logical_expression )   
     | WITH ( <index_option > )  
     }   
  
<table_constraint> ::=   
     { { PRIMARY KEY | UNIQUE } ( column_name [ ,...n] )   
     | CHECK ( search_condition )   
     }   
  
<index_option> ::=  
See CREATE TABLE for index option syntax.  
  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
DECLARE   
{{ @local_variable [AS] data_type } [ =value [ COLLATE <collation_name> ] ] } [,...n]  
  
```  
  
## <a name="arguments"></a>Argumente  
@*local_variable*  
 Der Name einer Variablen. Variablennamen müssen mit einem at-Zeichen (@) beginnen. Namen lokaler Variable müssen den Regeln für entsprechen [Bezeichner](../../relational-databases/databases/database-identifiers.md).  
  
*data_type*  
 Ein vom System bereitgestellter, CLR-benutzerdefinierter Tabellentyp (Common Language Runtime) oder Aliasdatentyp. Eine Variable kann nicht vom **Text**, **Ntext**, oder **Image** -Datentyp.  
  
 Weitere Informationen zu Systemdatentypen finden Sie unter [Datentypen &#40; Transact-SQL &#41; ](../../t-sql/data-types/data-types-transact-sql.md). Weitere Informationen zu benutzerdefinierten CLR-Typen oder Aliasdatentypen finden Sie unter [CREATE TYPE &#40; Transact-SQL &#41; ](../../t-sql/statements/create-type-transact-sql.md).  
  
 =*value*  
 Weist der Variablen inline einen Wert zu. Der Wert kann eine Konstante oder ein Ausdruck sein; auf jeden Fall muss er mit dem Typ der Variablendeklaration übereinstimmen oder implizit in diesen Typ konvertiert werden können. Weitere Informationen finden Sie unter [Expressions &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md).  
  
@*cursor_variable_name*  
 Ist der Name einer Cursorvariablen. Cursorvariablennamen müssen mit einem at-Zeichen (@) beginnen und den Regeln für Bezeichner entsprechen.  
  
CURSOR  
 Gibt an, dass die Variable eine lokale Cursorvariable ist.  
  
@*table_variable_name*  
 Der Name einer Variablen des Typs **Tabelle**. Variablennamen müssen mit einem at-Zeichen (@) beginnen und den Regeln für Bezeichner entsprechen.  
  
<table_type_definition>  
Definiert die **Tabelle** -Datentyp. Die Tabellendeklaration schließt Spaltendefinitionen, Namen, Datentypen und Einschränkungen ein. Die einzigen zulässigen Einschränkungstypen sind PRIMARY KEY, UNIQUE, NULL und CHECK. Ein Aliasdatentyp kann nicht als Skalar-Spaltendatentyp verwendet werden, wenn eine Regel oder Standarddefinition an den Typ gebunden ist.
  
\<Table_type_definiton > ist eine Teilmenge der Informationen, die zum Definieren einer Tabelle in CREATE TABLE verwendet. Darin sind Elemente und wichtige Definitionen eingeschlossen. Weitere Informationen finden Sie unter [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md).  
  
 *n*  
 Ein Platzhalter, der angibt, dass mehrere Variablen angegeben und ihnen Werte zugewiesen werden können. Beim Deklarieren von **Tabelle** Variablen, die **Tabelle** Variable muss die einzige Variable in der DECLARE-Anweisung deklariert wird.  
  
 *column_name*  
 Der Name der Spalte in der Tabelle.  
  
 *scalar_data_type*  
 Gibt an, dass die Spalte ein skalarer Datentyp ist.  
  
 *computed_column_expression*  
 Ein Ausdruck, der den Wert einer berechneten Spalte definieren. Sie wird mithilfe anderer Spalten derselben Tabelle mit einem Ausdruck berechnet. Beispielsweise kann eine berechnete Spalte die Definition besitzen **Kosten** AS **Preis \* Qty**. Der Ausdruck kann der Name einer nicht berechneten Spalte, eine Konstante, eine integrierte Funktion, eine Variable oder eine beliebige durch einen oder mehrere Operatoren verbundene Kombination der genannten Möglichkeiten sein. Der Ausdruck kann keine Unterabfrage oder benutzerdefinierte Funktion sein. Der Ausdruck kann nicht auf einen CLR-benutzerdefinierten Typ verweisen.  
  
 [COLLATE *Collation_name*]  
 Gibt die Sortierung für die Spalte an. *Collation_name* kann entweder der Name einer Windows-Sortierreihenfolge oder ein SQL-Sortierungsname sein und gilt nur für Spalten von der **Char**, **Varchar**, **Text** , **Nchar**, **Nvarchar**, und **Ntext** Datentypen. Wenn collation_name nicht angegeben ist, wird der Spalte die Sortierung des benutzerdefinierten Datentyps zugewiesen, wenn es sich um eine Spalte von einem benutzerdefinierten Datentyp handelt, oder es wird die Sortierung der aktuellen Datenbank zugewiesen.  
  
 Weitere Informationen zu den Windows- und SQL-Sortierungsnamen finden Sie unter [COLLATE &#40; Transact-SQL &#41; ](~/t-sql/statements/collations.md).  
  
 DEFAULT  
 Gibt den Wert an, der für die Spalte bereitgestellt wird, wenn kein Wert explizit angegeben wurde. DEFAULT-Definitionen können angewendet werden, um alle Spalten außer den als definierten **Zeitstempel** sowie von Spalten mit der IDENTITY-Eigenschaft. DEFAULT-Definitionen werden entfernt, wenn die Tabelle gelöscht wird. Es kann nur ein konstanter Wert wie eine Zeichenfolge, eine Systemfunktion, z. B. SYSTEM_USER(), oder NULL als Standardwert verwendet werden. Um die Kompatibilität mit früheren Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aufrechtzuerhalten, ist es möglich, einer DEFAULT-Definition einen Einschränkungsnamen zuzuweisen.  
  
 *constant_expression*  
 Ist eine Konstante, NULL oder eine Systemfunktion, die für die Spalte als Standardwert verwendet.  
  
 IDENTITY  
 Gibt an, dass es sich bei der neuen Spalte um eine Identitätsspalte handelt. Wenn die Tabelle eine neue Zeile hinzugefügt wird [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] einen eindeutigen, inkrementellen Wert für die Spalte bereitstellt. Identitätsspalten werden in der Regel in Verbindung mit PRIMARY KEY-Einschränkungen verwendet, um als eindeutiger Zeilenbezeichner für die Tabelle zu dienen. Die IDENTITY-Eigenschaft zugewiesen werden kann **"tinyint"**, **"smallint"**, **Int**, **decimal(p,0)**, oder **numeric(p,0)** Spalten. Es kann nur eine Identitätsspalte pro Tabelle erstellt werden. Gebundene Standardwerte und DEFAULT-Einschränkungen können nicht mit einer Identitätsspalte verwendet werden. Sie müssen entweder den Ausgangswert und den Schrittweitenwert oder keinen von beiden angeben. Wurden Ausgangswert und inkrementeller Wert nicht angegeben, ist der Standardwert (1,1).  
  
 *seed*  
 Der Wert, der für die erste in die Tabelle geladene Zeile verwendet wird.  
  
 *increment*  
 Der Schrittweitenwert, der zum Identitätswert der zuvor geladenen Zeile addiert wird.  
  
 ROWGUIDCOL  
 Gibt an, dass die neue Spalte eine Spalte mit für alle Zeilen global eindeutigen Bezeichnern ist. Nur ein **"uniqueidentifier"** -Spalte pro Tabelle kann als ROWGUIDCOL-Spalte gekennzeichnet werden. Die ROWGUIDCOL-Eigenschaft kann nur für zugewiesen werden eine **"uniqueidentifier"** Spalte.  
  
 NULL | NOT NULL  
 Gibt an, ob NULL in der Variablen zulässig ist. Die Standardeinstellung ist NULL.  
  
 PRIMARY KEY  
 Eine Einschränkung, die Entitätsintegrität für eine bestimmte Spalte (oder Spalten) durch einen eindeutigen Index erzwingt. Es kann nur eine PRIMARY KEY-Einschränkung pro Tabelle erstellt werden.  
  
 UNIQUE  
 Eine Einschränkung, die Entitätsintegrität für eine bestimmte Spalte (oder Spalten) durch einen eindeutigen Index bereitstellt. Eine Tabelle kann mehrere UNIQUE-Einschränkungen haben.  
  
 CHECK  
 Eine Einschränkung, die Domänenintegrität erzwingt, indem die möglichen Eingabewerte für eine oder mehrere Spalten beschränkt wird.  
  
 *logical_expression*  
 Ein logischer Ausdruck, der TRUE oder FALSE zurückgibt.  
  
## <a name="remarks"></a>Hinweise  
 Variablen werden oft in einem Batch oder einer Prozedur als Zähler für WHILE, LOOP oder für IF...ELSE-Blöcke verwendet.  
  
 Variablen können nur in Ausdrücken kann nicht anstelle von Objektnamen oder Schlüsselwörtern verwendet werden. Um dynamische SQL-Anweisungen zu erstellen, verwenden Sie EXECUTE.  
  
 Der Gültigkeitsbereich einer lokalen Variablen ist der Batch, in dem sie deklariert ist.  
 
 Eine Variable für Tabellenname ist nicht notwendigerweise speicherresident. Nicht genügend Arbeitsspeicher vorhanden können der Seiten, die in einer Tabellenvariablen gehören tempdb abgelegt werden.
  
 Auf eine Cursorvariable, der aktuell ein Cursor zugewiesen ist, kann in folgenden Anweisungen als Quelle verwiesen werden:  
  
-   CLOSE-Anweisung.  
  
-   DEALLOCATE-Anweisung.  
  
-   FETCH-Anweisung.  
  
-   OPEN-Anweisung.  
  
-   Positionierte DELETE- oder UPDATE-Anweisung.  
  
-   SET CURSOR VARIABLE-Anweisung (auf der rechten Seite).  
  
 Bei all diesen Anweisungen wird von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ein Fehler ausgelöst, wenn eine Cursorvariable vorhanden ist, auf die verwiesen wird, für die aber aktuell kein Cursor zugeordnet ist. Ist keine Cursorvariable vorhanden, auf die verwiesen wird, wird von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] der gleiche Fehler ausgelöst wie für eine nicht deklarierte Variable eines anderen Typs.  
  
 Eine Cursorvariable hat folgende Eigenschaften:  
  
-   Sie kann das Ziel eines Cursortyps oder einer anderen Cursorvariablen sein. Weitere Informationen finden Sie unter [festgelegt @local_variable &#40; Transact-SQL &#41; ](../../t-sql/language-elements/set-local-variable-transact-sql.md).  
  
-   Auf sie kann als Ziel eines Ausgabecursorparameters in einer EXECUTE-Anweisung verwiesen werden, wenn der Cursorvariablen aktuell kein Cursor zugewiesen ist.  
  
-   Sie sollte als Zeiger auf den Cursor verstanden werden.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-using-declare"></a>A. Verwenden von DECLARE  
 Im folgenden Beispiel werden mithilfe der lokalen Variablen `@find` Kontaktinformationen für alle Nachnamen abgerufen, die mit `Man` beginnen.  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @find varchar(30);   
/* Also allowed:   
DECLARE @find varchar(30) = 'Man%';   
*/  
SET @find = 'Man%';   
SELECT p.LastName, p.FirstName, ph.PhoneNumber  
FROM Person.Person AS p   
JOIN Person.PersonPhone AS ph ON p.BusinessEntityID = ph.BusinessEntityID  
WHERE LastName LIKE @find;  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
LastName            FirstName               Phone
------------------- ----------------------- -------------------------
Manchepalli         Ajay                    1 (11) 500 555-0174
Manek               Parul                   1 (11) 500 555-0146
Manzanares          Tomas                   1 (11) 500 555-0178
  
(3 row(s) affected)
```  
  
### <a name="b-using-declare-with-two-variables"></a>B. Verwenden von DECLARE mit zwei Variablen  
 Im folgenden Beispiel werden die Namen von Vertriebsmitarbeitern von [!INCLUDE[ssSampleDBCoFull](../../includes/sssampledbcofull-md.md)] abgerufen, die in der Vertriebsregion Nordamerika tätig sind und im laufenden Jahr bereits einen Umsatz von mindestens 2.000.000 USD erzielt haben.  
  
```  
USE AdventureWorks2012;  
GO  
SET NOCOUNT ON;  
GO  
DECLARE @Group nvarchar(50), @Sales money;  
SET @Group = N'North America';  
SET @Sales = 2000000;  
SET NOCOUNT OFF;  
SELECT FirstName, LastName, SalesYTD  
FROM Sales.vSalesPerson  
WHERE TerritoryGroup = @Group and SalesYTD >= @Sales;  
```  
  
### <a name="c-declaring-a-variable-of-type-table"></a>C. Deklarieren einer Variablen vom Typ "table"  
 Im folgenden Beispiel wird eine `table`-Variable erstellt, die die in der OUTPUT-Klausel der UPDATE-Anweisung angegebenen Werte speichert. Es folgen zwei `SELECT`-Anweisungen, die die Werte in `@MyTableVar` und die Ergebnisse des Updatevorgangs in der `Employee`-Tabelle zurückgeben. Beachten Sie, dass die Ergebnisse in die `INSERTED.ModifiedDate` Spalte unterscheiden sich von den Werten in der `ModifiedDate` Spalte in der `Employee` Tabelle. Der Grund dafür ist, dass der `AFTER UPDATE`-Trigger, der den Wert von `ModifiedDate` auf das aktuelle Datum aktualisiert, in der `Employee`-Tabelle definiert wird. Die von `OUTPUT` zurückgegebenen Spalten spiegeln jedoch die Daten wider, bevor Trigger ausgelöst werden. Weitere Informationen finden Sie unter [OUTPUT-Klausel &#40; Transact-SQL &#41; ](../../t-sql/queries/output-clause-transact-sql.md).  
  
```  
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
  
### <a name="d-declaring-a-variable-of-user-defined-table-type"></a>D. Deklarieren einer Variablen vom Typ 'user-defined table'  
 Im folgenden Beispiel wird ein Tabellenwertparameter oder eine Tabellenvariable mit dem Namen `@LocationTVP` erstellt. Dies erfordert einen entsprechenden benutzerdefinierten Tabellentyp mit dem Namen `LocationTableType`. Weitere Informationen zum Erstellen eines benutzerdefinierten Tabellentyps finden Sie unter [CREATE TYPE &#40; Transact-SQL &#41; ](../../t-sql/statements/create-type-transact-sql.md). Weitere Informationen zu Tabellenwertparametern finden Sie unter [Tabellenwertparametern &#40; Datenbankmodul &#41;](../../relational-databases/tables/use-table-valued-parameters-database-engine.md).  
  
```  
DECLARE @LocationTVP   
AS LocationTableType;  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Beispiele: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] und[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="e-using-declare"></a>E. Verwenden von DECLARE  
 Im folgenden Beispiel werden mithilfe der lokalen Variablen `@find` Kontaktinformationen für alle Nachnamen abgerufen, die mit `Walt` beginnen.  
  
```  
-- Uses AdventureWorks  
  
DECLARE @find varchar(30);  
/* Also allowed:   
DECLARE @find varchar(30) = 'Man%';  
*/  
SET @find = 'Walt%';  
  
SELECT LastName, FirstName, Phone  
FROM DimEmployee   
WHERE LastName LIKE @find;  
```  
  
### <a name="f-using-declare-with-two-variables"></a>F. Verwenden von DECLARE mit zwei Variablen  
 Das folgende Beispiel ruft verwendet Variablen, um anzugeben, die vor- und Nachnamen Namen von Mitarbeitern in der `DimEmployee` Tabelle.  
  
```  
-- Uses AdventureWorks  
  
DECLARE @lastName varchar(30), @firstName varchar(30);  
  
SET @lastName = 'Walt%';  
SET @firstName = 'Bryan';  
  
SELECT LastName, FirstName, Phone  
FROM DimEmployee   
WHERE LastName LIKE @lastName AND FirstName LIKE @firstName;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [EXECUTE &#40;Transact-SQL&#41;](../../t-sql/language-elements/execute-transact-sql.md)   
 [Integrierte Funktionen &#40;Transact-SQL&#41;](~/t-sql/functions/functions.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [table &#40;Transact-SQL&#41;](../../t-sql/data-types/table-transact-sql.md)   
 [Vergleichen von typisiertem XML mit nicht typisiertem XML](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)  
  
  





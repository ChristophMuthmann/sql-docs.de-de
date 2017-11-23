---
title: Tabellenwertkonstruktor (Transact-SQL) Tabelle | Microsoft Docs
ms.custom: 
ms.date: 08/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|queries
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
helpviewer_keywords:
- inserting multiple rows
- row value expression
- row constructor [SQL Server]
- table value constructor [SQL Server]
ms.assetid: e57cd31d-140e-422f-8178-2761c27b9deb
caps.latest.revision: "14"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: af168279367215e96be2989a5b5e8f8326baab76
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="table-value-constructor-transact-sql"></a>Tabellenwertkonstruktor (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Gibt eine Gruppe mit Zeilenwertausdrücken an, die in einer Tabelle erstellt werden sollen. Der [!INCLUDE[tsql](../../includes/tsql-md.md)]-Tabellenwertkonstruktor ermöglicht das Angeben mehrerer Datenzeilen in nur einer DML-Anweisung. Der tabellenwertkonstruktor kann angegeben werden, in der VALUES-Klausel der INSERT-Anweisung, in der USING \<Quelltabelle >-Klausel der MERGE-Anweisung und in der Definition einer abgeleiteten Tabelle in der FROM-Klausel.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
VALUES ( <row value expression list> ) [ ,...n ]   
  
<row value expression list> ::=  
    {<row value expression> } [ ,...n ]  
  
<row value expression> ::=  
    { DEFAULT | NULL | expression }  
```  
  
## <a name="arguments"></a>Argumente  
 VALUES  
 Bietet eine Einführung in die Zeilenwertausdruckslisten. Die einzelnen Listen müssen in Klammern gesetzt und durch ein Trennzeichen getrennt werden.  
  
 Die Anzahl der in jeder Liste angegebenen Werte muss übereinstimmen, und die Werte müssen in der gleichen Reihenfolge wie die Spalten in der Tabelle vorliegen. Für jede Spalte in der Tabelle muss ein Wert angegeben werden, oder in der Spaltenliste müssen explizit die Spalten für jeden eingehenden Wert angegeben werden.  
  
 DEFAULT  
 Erzwingt, dass [!INCLUDE[ssDE](../../includes/ssde-md.md)] den für eine Spalte definierten Standardwert einfügt. Wenn für die Spalte kein Standardwert vorhanden ist und die Spalte NULL-Werte zulässt, wird NULL eingefügt. DEFAULT ist für eine Identitätsspalte nicht zulässig. Wenn DEFAULT in einem Tabellenwertkonstruktor angegeben wird, ist diese Variable nur in einer INSERT-Anweisung zulässig.  
  
 *expression*  
 Eine Konstante, eine Variable oder ein Ausdruck. Der Ausdruck darf keine EXECUTE-Anweisung enthalten.  
  
## <a name="limitations-and-restrictions"></a>Einschränkungen  
 Tabellenwertkonstruktoren können auf zwei Arten verwendet werden: direkt in der VALUES-Liste einer INSERT... Anweisung Werte oder als abgeleitete Tabelle überall, die abgeleitete Tabellen zulässig sind. Fehler 10738 wird zurückgegeben, wenn die Anzahl der Zeilen die maximale Größe überschreitet. Verwenden Sie zum Einfügen von mehr Zeilen als die Grenze ermöglicht, eine der folgenden Methoden aus:  
  
-   Erstellen mehrerer INSERT-Anweisungen  
  
-   Verwenden Sie eine abgeleitete Tabelle  
  
-   Massenimport der Daten mithilfe der **Bcp** Hilfsprogramm oder BULK INSERT-Anweisung  
  
 Nur einzelne Skalarwerte sind als Zeilenwertausdruck zulässig. Eine Unterabfrage, die mehrere Spalten umfasst, ist nicht als Zeilenwertausdruck zulässig. Der folgende Code verursacht z. B. einen Syntaxfehler, weil die dritte Zeilenwertausdrucksliste eine Unterabfrage mit mehreren Spalten enthält.  
  
```  
USE AdventureWorks2012;  
GO  
CREATE TABLE dbo.MyProducts (Name varchar(50), ListPrice money);  
GO  
-- This statement fails because the third values list contains multiple columns in the subquery.  
INSERT INTO dbo.MyProducts (Name, ListPrice)  
VALUES ('Helmet', 25.50),  
       ('Wheel', 30.00),  
       (SELECT Name, ListPrice FROM Production.Product WHERE ProductID = 720);  
GO  
  
```  
  
 Die Anweisung kann jedoch umgeschrieben werden, indem jede Spalte getrennt in der Unterabfrage angegeben wird. Im folgenden Beispiel werden drei Zeilen erfolgreich in die `MyProducts`-Tabelle eingefügt.  
  
```  
INSERT INTO dbo.MyProducts (Name, ListPrice)  
VALUES ('Helmet', 25.50),  
       ('Wheel', 30.00),  
       ((SELECT Name FROM Production.Product WHERE ProductID = 720),  
        (SELECT ListPrice FROM Production.Product WHERE ProductID = 720));  
GO  
  
```  
  
## <a name="data-types"></a>Datentypen  
 Die in einer aus mehreren Zeilen bestehenden INSERT-Anweisung angegebenen Werte befolgen die Datentypkonvertierungseigenschaften der UNION ALL-Syntax. Dies führt zur impliziten Konvertierung nicht übereinstimmender Typen in den Typ der höheren [Rangfolge](../../t-sql/data-types/data-type-precedence-transact-sql.md). Wenn es sich bei der Konvertierung nicht um eine unterstützte implizite Konvertierung handelt, gibt das System einen Fehler zurück. Z. B. die folgende Anweisung fügt einen ganzzahligen Wert und ein Zeichenwert in eine Spalte vom Typ **Char**.  
  
```  
CREATE TABLE dbo.t (a int, b char);  
GO  
INSERT INTO dbo.t VALUES (1,'a'), (2, 1);  
GO  
```  
  
 Bei Ausführung der INSERT-Anweisung versucht [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], "a" in eine ganze Zahl zu konvertieren, da die Rangfolge der Datentypen angibt, dass eine ganze Zahl einen höherrangigen Typ hat als ein Zeichen. Die Konvertierung schlägt fehl, und es wird ein Fehler zurückgegeben. Sie können den Fehler vermeiden, indem Sie Werte nach Bedarf explizit konvertieren. Die vorherige Anweisung kann beispielsweise folgendermaßen geschrieben werden.  
  
```  
INSERT INTO dbo.t VALUES (1,'a'), (2, CONVERT(CHAR,1));  
```  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-inserting-multiple-rows-of-data"></a>A. Einfügen mehrerer Datenzeilen  
 Im folgenden Beispiel wird die `dbo.Departments`-Tabelle erstellt; anschließend werden unter Verwendung des Tabellenwertkonstruktors fünf Zeilen in die Tabelle eingefügt. Da Werte für alle Spalten bereitgestellt werden und in der Reihenfolge der Spalten in der Tabelle aufgelistet sind, müssen die Spaltennamen nicht in der Spaltenliste angegeben werden.  
  
```  
USE AdventureWorks2012;  
GO  
INSERT INTO Production.UnitMeasure  
VALUES (N'FT2', N'Square Feet ', '20080923'), (N'Y', N'Yards', '20080923'), (N'Y3', N'Cubic Yards', '20080923');  
GO  
  
```  
  
### <a name="b-inserting-multiple-rows-with-default-and-null-values"></a>B. Einfügen mehrerer Zeilen mit DEFAULT- und NULL-Werten  
 Im folgenden Beispiel wird das Angeben von DEFAULT und NULL gezeigt, wenn mithilfe des Tabellenwertkonstruktors Zeilen in eine Tabelle eingefügt werden.  
  
```  
USE AdventureWorks2012;  
GO  
CREATE TABLE Sales.MySalesReason(  
SalesReasonID int IDENTITY(1,1) NOT NULL,  
Name dbo.Name NULL ,  
ReasonType dbo.Name NOT NULL DEFAULT 'Not Applicable' );  
GO  
INSERT INTO Sales.MySalesReason   
VALUES ('Recommendation','Other'), ('Advertisement', DEFAULT), (NULL, 'Promotion');  
  
SELECT * FROM Sales.MySalesReason;  
  
```  
  
### <a name="c-specifying-multiple-values-as-a-derived-table-in-a-from-clause"></a>C. Angeben mehrerer Werte als abgeleitete Tabelle in einer FROM-Klausel  
 Die folgenden Beispiele verwenden des tabellenwertkonstruktors mehrere Werte in der FROM-Klausel einer SELECT-Anweisung angeben.  
  
```  
SELECT a, b FROM (VALUES (1, 2), (3, 4), (5, 6), (7, 8), (9, 10) ) AS MyTable(a, b);  
GO  
-- Used in an inner join to specify values to return.  
SELECT ProductID, a.Name, Color  
FROM Production.Product AS a  
INNER JOIN (VALUES ('Blade'), ('Crown Race'), ('AWC Logo Cap')) AS b(Name)   
ON a.Name = b.Name;  
  
```  
  
### <a name="d-specifying-multiple-values-as-a-derived-source-table-in-a-merge-statement"></a>D. Angeben mehrerer Werte als abgeleitete Quelltabelle in einer MERGE-Anweisung  
 Im folgenden Beispiel wird die `SalesReason`-Tabelle durch das Aktualisieren oder Einfügen von Zeilen mithilfe von MERGE geändert. Wenn der Wert von `NewName` in der Quelltabelle einem Wert in der `Name`-Spalte der Zieltabelle entspricht (`SalesReason`), wird die `ReasonType`-Spalte in der Zieltabelle aktualisiert. Wenn der Wert von `NewName` jedoch nicht übereinstimmt, wird die Quellzeile in die Zieltabelle eingefügt. Die Quelltabelle ist eine abgeleitete Tabelle, die mithilfe des [!INCLUDE[tsql](../../includes/tsql-md.md)]-Tabellenwertkonstruktors mehrere Zeilen für die Quelltabelle angibt.  
  
```  
USE AdventureWorks2012;  
GO  
-- Create a temporary table variable to hold the output actions.  
DECLARE @SummaryOfChanges TABLE(Change VARCHAR(20));  
  
MERGE INTO Sales.SalesReason AS Target  
USING (VALUES ('Recommendation','Other'), ('Review', 'Marketing'), ('Internet', 'Promotion'))  
       AS Source (NewName, NewReasonType)  
ON Target.Name = Source.NewName  
WHEN MATCHED THEN  
UPDATE SET ReasonType = Source.NewReasonType  
WHEN NOT MATCHED BY TARGET THEN  
INSERT (Name, ReasonType) VALUES (NewName, NewReasonType)  
OUTPUT $action INTO @SummaryOfChanges;  
  
-- Query the results of the table variable.  
SELECT Change, COUNT(*) AS CountPerChange  
FROM @SummaryOfChanges  
GROUP BY Change;  
  
```  
  
## <a name="see-also"></a>Siehe auch  
 [INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)   
 [MERGE &#40; Transact-SQL &#41;](../../t-sql/statements/merge-transact-sql.md)   
 [FROM &#40;Transact-SQL&#41;](../../t-sql/queries/from-transact-sql.md)  
  
  

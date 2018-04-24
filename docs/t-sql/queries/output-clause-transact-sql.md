---
title: OUTPUT-Klausel (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 08/09/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: t-sql|queries
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- OUTPUT_TSQL
- OUTPUT
dev_langs:
- TSQL
helpviewer_keywords:
- displaying updated rows
- INSERT statement [SQL Server], OUTPUT clause
- outputs [SQL Server]
- OUTPUT clause
- row additions [SQL Server], OUTPUT clause
- viewing updated rows
- row deletions [SQL Server], OUTPUT clause
- viewing deleted rows
- DELETE statement [SQL Server], OUTPUT clause
- row updates [SQL Server]
- displaying inserted rows
- viewing inserted rows
- displaying deleted rows
- UPDATE statement [SQL Server], OUTPUT clause
ms.assetid: 41b9962c-0c71-4227-80a0-08fdc19f5fe4
caps.latest.revision: 94
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Active
ms.openlocfilehash: 87906714cbca4fc62a1593e19772d8c9c8a8354c
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="output-clause-transact-sql"></a>OUTPUT-Klausel (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Gibt Informationen aus bzw. Ausdrücke basierend auf den einzelnen Zeilen zurück, auf die eine INSERT-, UPDATE-, DELETE- oder MERGE-Anweisung Auswirkungen hat. Diese Ergebnisse können an die verarbeitende Anwendung zurückgegeben werden, die sie z. B. für Bestätigungen, Archivierungen und andere Anwendungsanforderungen verwendet. Die Ergebnisse können auch in eine Tabelle oder Tabellenvariable eingefügt werden. Darüber hinaus können Sie die Ergebnisse einer OUTPUT-Klausel in einer geschachtelten INSERT-, UPDATE-, DELETE- oder MERGE-Anweisung aufzeichnen und diese Ergebnisse in eine Zieltabelle oder -sicht einfügen.  
  
> [!NOTE]  
>  Eine INSERT-, UPDATE- oder DELETE-Anweisung mit einer OUTPUT-Klausel gibt Zeilen auch dann an den Client zurück, wenn bei der Anweisung ein Fehler auftritt und ein Rollback ausgeführt wird. Wenn bei der Ausführung der Anweisung ein Fehler auftritt, sollte das Ergebnis nicht verwendet werden.  
  
 **Verwendung in:**  
  
 [DELETE](../../t-sql/statements/delete-transact-sql.md)  
  
 [INSERT](../../t-sql/statements/insert-transact-sql.md)  
  
 [UPDATE](../../t-sql/queries/update-transact-sql.md)  
  
 [MERGE](../../t-sql/statements/merge-transact-sql.md)  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
<OUTPUT_CLAUSE> ::=  
{  
    [ OUTPUT <dml_select_list> INTO { @table_variable | output_table } [ ( column_list ) ] ]  
    [ OUTPUT <dml_select_list> ]  
}  
<dml_select_list> ::=  
{ <column_name> | scalar_expression } [ [AS] column_alias_identifier ]  
    [ ,...n ]  
  
<column_name> ::=  
{ DELETED | INSERTED | from_table_name } . { * | column_name }  
    | $action  
```  
  
## <a name="arguments"></a>Argumente  
 @*table_variable*  
 Gibt eine **table**-Variable an, in die die zurückgegebenen Zeilen eingefügt werden, statt an den Aufrufer zurückgegeben zu werden. @*table_variable* muss vor der INSERT-, UPDATE-, DELETE- oder MERGE-Anweisung deklariert werden.  
  
 Wenn *column_list* nicht angegeben wird, muss die **table**-Variable dieselbe Anzahl von Spalten wie das OUTPUT-Resultset aufweisen. Ausnahmen bilden Identitätsspalten sowie berechnete Spalten, die ausgelassen werden müssen. Wenn *column_list* angegeben wird, müssen alle ausgelassenen Spalten entweder NULL-Werte zulassen oder über zugewiesene Standardwerte verfügen.  
  
 Weitere Informationen zu **table**-Variablen finden Sie unter [table &#40;Transact-SQL&#41;](../../t-sql/data-types/table-transact-sql.md).  
  
 *output_table*  
 Gibt eine Tabelle an, in die die zurückgegebenen Zeilen eingefügt werden, statt an den Aufrufer zurückgegeben zu werden. *output_table* kann eine temporäre Tabelle sein.  
  
 Wenn *column_list* nicht angegeben wird, muss die Tabelle dieselbe Anzahl von Spalten wie das OUTPUT-Resultset aufweisen. Ausnahmen bilden Identitätsspalten sowie berechnete Spalten. Diese müssen ausgelassen werden. Wenn *column_list* angegeben wird, müssen alle ausgelassenen Spalten entweder NULL-Werte zulassen oder über zugewiesene Standardwerte verfügen.  
  
 Für *output_table* ist gilt Folgendes:  
  
-   Keine Definition von aktivierten Triggern.  
  
-   Keine Beteiligung an einer der Seiten einer FOREIGN KEY-Einschränkung.  
  
-   Keine CHECK-Einschränkungen oder aktivierten Regeln.  
  
*column_list*  
 Ist eine optionale Liste mit Spaltennamen in der Zieltabelle der INTO-Klausel. Ist analog zu der in der [INSERT](../../t-sql/statements/insert-transact-sql.md)-Anweisung zulässigen Spaltenliste.  
  
 *scalar_expression*  
 Ist eine beliebige Kombination von Symbolen und Operatoren, die zu genau einem Wert ausgewertet werden. Aggregatfunktionen sind in *scalar_expression* nicht zulässig.  
  
 Alle Verweise auf Spalten in der Tabelle, die geändert wird, müssen mit dem INSERTED- oder DELETED-Präfix gekennzeichnet werden.  
  
 *column_alias_identifier*  
 Ist ein alternativer Name, über den auf den Spaltennamen verwiesen wird.  
  
 DELETED  
 Ist ein Spaltenpräfix, das den durch den Update- oder Löschvorgang gelöschten Wert angibt. Spalten mit dem DELETED-Präfix spiegeln den Wert vor dem Abschluss der UPDATE-, DELETE- oder MERGE-Anweisung wider.  
  
 DELETED kann nicht mit der OUTPUT-Klausel in der INSERT-Anweisung verwendet werden.  
  
 INSERTED  
 Ist ein Spaltenpräfix, das den durch den Einfüge- oder Updatevorgang hinzugefügten Wert angibt. Spalten mit dem INSERTED-Präfix spiegeln den Wert nach Abschluss der UPDATE-, INSERT- oder MERGE-Anweisung wider, jedoch vor dem Ausführen von Triggern.  
  
 INSERTED kann nicht mit der OUTPUT-Klausel in der DELETE-Anweisung verwendet werden.  
  
 *from_table_name*  
 Ist ein Spaltenpräfix, das eine Tabelle angibt, die in der FROM-Klausel einer DELETE-, UPDATE- oder MERGE-Anweisung enthalten ist, die wiederum zur Angabe der zu aktualisierenden oder zu löschenden Zeilen verwendet wird.  
  
 Wird die Tabelle, der geändert wird, auch in der FROM-Klausel angegeben, müssen alle Verweise auf Spalten in dieser Tabelle durch das INSERTED- oder DELETED-Präfix gekennzeichnet werden.  
  
 \*  
 Gibt an, dass alle vom Lösch-, Einfüge- oder Updatevorgang betroffenen Spalten in der Reihenfolge zurückgegeben werden, in der sie in der Tabelle vorkommen.  
  
 So gibt beispielsweise `OUTPUT DELETED.*` in der folgenden DELETE-Anweisung alle aus der `ShoppingCartItem`-Tabelle zurückgegebenen Spalten zurück:  
  
```  
DELETE Sales.ShoppingCartItem  
    OUTPUT DELETED.*;  
```  
  
 *column_name*  
 Ist ein expliziter Spaltenverweis. Alle Verweise auf die Tabelle, die geändert wird, müssen entweder durch das INSERTED- oder das DELETED-Präfix richtig gekennzeichnet werden, z.B. INSERTED**.***column_name*.  
  
 $action  
 Ist verfügbar nur für die MERGE-Anweisung. Gibt in der OUTPUT-Klausel in einer MERGE-Anweisung, die einen der drei folgenden Werte für jede Zeile zurückgibt, eine Spalte des Typs **nvarchar(10)** an: 'INSERT', 'UPDATE' oder 'DELETE'. Der zurückgegebene Wert hängt von der für diese Zeile ausgeführten Aktion ab.  
  
## <a name="remarks"></a>Remarks  
 Die OUTPUT \<dml_select_list>-Klausel und die OUTPUT \<dml_select_list> INTO { **@***table_variable* | *output_table* }-Klausel können in einer einzelnen INSERT-, UPDATE-, DELETE- oder MERGE-Anweisung definiert werden.  
  
> [!NOTE]  
>  Sofern nicht anderweitig angegeben, beziehen sich Verweise auf die OUTPUT-Klausel sowohl auf die OUTPUT- als auch die OUTPUT INTO-Klausel.  
  
 Die OUTPUT-Klausel kann zum Abrufen des Werts von Identitätsspalten oder berechneten Spalten nach einem INSERT- oder UPDATE-Vorgang genutzt werden.  
  
 Wenn eine berechnete Spalte in der \<dml_select_list> enthalten ist, ist die entsprechende Spalte in der Ausgabetabelle oder Tabellenvariablen keine berechnete Spalte. Die Werte in der neuen Spalte entsprechen den Werten, die zum Zeitpunkt der Ausführung der Anweisung berechnet wurden.  
  
 Es kann nicht sichergestellt werden, dass die Reihenfolge, in der die Änderungen auf die Tabelle angewendet werden, der Reihenfolge entspricht, in der die Zeilen in die Ausgabetabelle oder -tabellenvariable eingefügt werden.  
  
 Wenn Parameter oder Variablen im Rahmen einer UPDATE-Anweisung geändert werden, gibt die OUTPUT-Klausel immer den Wert des Parameters oder der Variablen vor der Ausführung der Anweisung zurück, statt des geänderten Werts.  
  
 OUTPUT kann mit einer UPDATE- oder DELETE-Anweisung auf einem Cursor mit WHERE CURRENT OF-Syntax verwendet werden.  
  
 Die OUTPUT-Klausel wird von den folgenden Anweisungen nicht unterstützt:  
  
-   DML-Anweisungen, die auf lokale partitionierte Sichten, verteilte partitionierte Sichten oder Remotetabellen verweisen.  
  
-   INSERT-Anweisungen, die eine EXECUTE-Anweisung enthalten.  
  
-   Volltextprädikate sind in der OUTPUT-Klausel nicht zulässig, wenn der Kompatibilitätsgrad der Datenbank auf 100 festgelegt ist.  
  
-   Die OUTPUT INTO-Klausel kann nicht zum Einfügen in eine Sicht oder eine Rowsetfunktion verwendet werden.  
  
-   Eine benutzerdefinierte Funktion kann nicht erstellt werden, wenn eine OUTPUT INTO-Klausel enthalten ist, deren Ziel eine Tabelle ist.  
  
 Um ein nicht deterministisches Verhalten zu verhindern, kann die OUTPUT-Klausel die folgenden Verweise nicht enthalten:  
  
-   Unterabfragen oder benutzerdefinierte Funktionen, die auf Benutzer- oder Systemdaten zugreifen bzw. bei denen davon ausgegangen wird, dass sie einen solchen Zugriff ausführen. Bei benutzerdefinierten Funktionen wird davon ausgegangen, dass sie auf Daten zugreifen, wenn sie nicht schemagebunden sind.  
  
-   Eine Spalte aus einer Sicht oder Inline-Tabellenwertfunktion, wenn diese Spalte durch eine der folgenden Methoden definiert wird:  
  
    -   Eine Unterabfrage.  
  
    -   Eine benutzerdefinierte Funktion, die auf Benutzer- oder Systemdaten zugreift bzw. bei der davon ausgegangen wird, dass sie einen solchen Zugriff ausführt.  
  
    -   Eine berechnete Spalte, die eine benutzerdefinierte Funktion enthält, die in ihrer Definition auf Benutzer- oder Systemdaten zugreift.  
  
     Wenn [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] eine solche Spalte in der OUTPUT-Klausel erkennt, wird der Fehler 4186 ausgelöst.   
  
## <a name="inserting-data-returned-from-an-output-clause-into-a-table"></a>Einfügen von Daten aus einer OUTPUT-Klausel in eine Tabelle  
 Wenn Sie die Ergebnisse einer OUTPUT-Klausel in einer geschachtelten INSERT-, UPDATE-, DELETE- oder MERGE-Anweisung aufzeichnen und diese Ergebnisse in eine Zieltabelle einfügen, müssen Sie Folgendes beachten:  
  
-   Der ganze Vorgang ist unteilbar. Entweder werden sowohl die äußere INSERT-Anweisung als auch die geschachtelte DML-Anweisung mit der OUTPUT-Klausel ausgeführt, oder die gesamte Anweisung schlägt fehl.  
  
-   Die folgenden Einschränkungen gelten für das Ziel der äußeren INSERT-Anweisung:  
  
    -   Das Ziel darf keine Remotetabelle, keine Remotesicht und kein allgemeiner Tabellenausdruck sein.  
  
    -   Das Ziel darf keine FOREIGN KEY-Einschränkung aufweisen, und es darf nicht durch eine FOREIGN KEY-Einschränkung darauf verwiesen werden.  
  
    -   Trigger können für das Ziel nicht definiert werden.  
  
    -   Das Ziel darf nicht Teil von Mergereplikationen oder aktualisierbaren Abonnements für Transaktionsreplikationen sein.  
  
-   Die folgenden Einschränkungen gelten für die geschachtelte DML-Anweisung:  
  
    -   Das Ziel darf keine Remotetabelle und keine partitionierte Sicht sein.  
  
    -   Die Quelle selbst darf keine \<dml_table_source>-Klausel enthalten.  
  
-   Die OUTPUT INTO-Klausel wird nicht in INSERT-Anweisungen unterstützt, die eine \<dml_table_source>-Klausel enthalten.  
  
-   @@ROWCOUNT gibt nur die Zeilen zurück, die von der äußeren INSERT-Anweisung eingefügt wurden.  
  
-   @@IDENTITY, SCOPE_IDENTITY und IDENT_CURRENT geben nur die von der geschachtelten DML-Anweisung generierten und nicht die von der äußeren INSERT-Anweisung generierten Identitätswerte zurück.  
  
-   In Abfragebenachrichtigungen gilt die Anweisung als einzelne Entität, und der Typ aller erstellten Benachrichtigungen wird auf den Typ der geschachtelten DML-Anweisung festgelegt, selbst wenn die signifikante Änderung von der äußeren INSERT-Anweisung stammt.  
  
-   Die SELECT-Klausel und die WHERE-Klausel dürfen in der \<dml_table_source>-Klausel keine Unterabfragen, Aggregatfunktionen, Rangfolgefunktionen, Volltextprädikate oder benutzerdefinierten Funktionen für den Datenzugriff enthalten; die TEXTPTR-Funktion darf ebenfalls nicht enthalten sein.  

## <a name="parallelism"></a>Parallelism
 Eine OUTPUT-Klausel, die Ergebnisse an den Client zurückgibt, verwendet immer einen seriellen Plan.

Wenn im Kontext einer Datenbank, für die ein Kompatibilitätsgrad von mindestens 130 festgelegt wurde, ein INSERT...SELECT-Vorgang einen WITH (TABLOCK)-Hinweis für die SELECT-Anweisung und darüber hinaus auch OUTPUT…INTO zum Einfügen einer temporären oder Benutzertabelle verwendet, erfüllt die Zieltabelle für den INSERT…SELECT-Vorgang je nach Unterstrukturkosten die Kriterien für Parallelität.  Die Zieltabelle, die in der OUTPUT INTO-Klausel referenziert wird, erfüllt die Kriterien für Parallelität nicht. 
 
## <a name="triggers"></a>Trigger  
 Von OUTPUT zurückgegebene Spalten spiegeln die Daten nach Abschluss der INSERT-, UPDATE- oder DELETE-Anweisung wider, jedoch vor der Ausführung der Trigger.  
  
 Bei INSTEAD OF-Triggern werden die zurückgegebenen Ergebnisse so generiert, als ob die INSERT-, UPDATE- oder DELETE-Anweisung tatsächlich stattgefunden hat, selbst wenn keine Änderungen als Folge des Triggervorgangs vorgenommen werden. Wird eine Anweisung, die eine OUTPUT-Klausel enthält, innerhalb eines Triggers verwendet, müssen Tabellenaliase zum Verweisen auf die Tabellen inserted und deleted des Triggers verwendet werden, um das Duplizieren von Spaltenverweisen mithilfe der OUTPUT zugeordneten Tabellen INSERTED und DELETED zu vermeiden.  
  
 Wird die OUTPUT-Klausel angegeben, ohne auch das INTO-Schlüsselwort anzugeben, kann für das Ziel des DML-Vorgangs kein aktivierter Trigger für die bestimmte DML-Aktion definiert werden. Wird beispielsweise die OUTPUT-Klausel in einer UPDATE-Anweisung definiert, können keine aktivierten UPDATE-Trigger für die Zieltabelle festgelegt werden.  
  
 Wird die sp_configure-Option Ergebnisse von Triggern nicht zulassen festgelegt, hat eine OUTPUT-Klausel ohne INTO-Klausel zur Folge, dass die Anweisung fehlschlägt, wenn sie aus einem Trigger heraus aufgerufen wird.  
  
## <a name="data-types"></a>Datentypen  
 Die OUTPUT-Klausel unterstützt die LOB-Datentypen: **nvarchar(max)**, **varchar(max)**, **varbinary(max)**, **text**, **ntext**, **image** und **xml**. Wird die .WRITE-Klausel in der UPDATE-Anweisung zum Ändern einer **nvarchar(max)**-, **varchar(max)**- oder **varbinary(max)**-Spalte verwendet, werden die vollständigen Anfangs- und Endimages der Werte zurückgegeben, wenn auf sie verwiesen wird. Die TEXTPTR( )-Funktion kann nicht im Rahmen eines Ausdrucks in einer **text**, **ntext**- oder **image**-Spalte in der OUTPUT-Klausel angezeigt werden.  
  
## <a name="queues"></a>Warteschlangen  
 OUTPUT kann in Anwendungen, die Tabellen als Warteschlangen verwenden, oder zum Aufbewahren von Zwischenresultsets verwendet werden. Die Anwendung fügt der Tabelle somit kontinuierlich Zeilen hinzu oder entfernt sie daraus. Im folgenden Beispiel wird die OUTPUT-Klausel in einer DELETE-Anweisung verwendet, um die gelöschte Zeile an die aufrufende Anwendung zurückzugeben.  
  
```  
USE AdventureWorks2012;  
GO  
DELETE TOP(1) dbo.DatabaseLog WITH (READPAST)  
OUTPUT deleted.*  
WHERE DatabaseLogID = 7;  
GO  
  
```  
  
 In diesem Beispiel wird eine Zeile aus einer als Warteschlange verwendeten Tabelle entfernt und die gelöschten Werte in einer einzigen Aktion an die verarbeitende Anwendung zurückgegeben. Zusätzliche Semantik kann ebenfalls implementiert werden, wie z. B. die Verwendung einer Tabelle zum Implementieren eines Stapels. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] stellt jedoch die Reihenfolge nicht sicher, in der Zeilen verarbeitet und von DML-Anweisungen mithilfe der OUTPUT-Klausel zurückgegeben werden. Es hängt von der Anwendung ab, eine entsprechende WHERE-Klausel einzufügen, die die gewünschte Semantik sicherstellen kann. Wenn mehrere Zeilen Anspruch auf den DML-Vorgang haben, kann keine bestimmte Reihenfolge sichergestellt werden. Im folgenden Beispiel wird eine Unterabfrage verwendet und davon ausgegangen, dass die `DatabaseLogID`-Spalte eindeutig ist, um die gewünschte Reihenfolgensemantik zu implementieren.  
  
```  
USE tempdb;  
GO  
CREATE TABLE dbo.table1  
(  
    id INT,  
    employee VARCHAR(32)  
);  
GO  
  
INSERT INTO dbo.table1 VALUES   
      (1, 'Fred')  
     ,(2, 'Tom')  
     ,(3, 'Sally')  
     ,(4, 'Alice');  
GO  
  
DECLARE @MyTableVar TABLE  
(  
    id INT,  
    employee VARCHAR(32)  
);  
  
PRINT 'table1, before delete'   
SELECT * FROM dbo.table1;  
  
DELETE FROM dbo.table1  
OUTPUT DELETED.* INTO @MyTableVar  
WHERE id = 4 OR id = 2;  
  
PRINT 'table1, after delete'  
SELECT * FROM dbo.table1;  
  
PRINT '@MyTableVar, after delete'  
SELECT * FROM @MyTableVar;  
  
DROP TABLE dbo.table1;  
  
--Results  
--table1, before delete  
--id          employee  
------------- ------------------------------  
--1           Fred  
--2           Tom  
--3           Sally  
--4           Alice  
--  
--table1, after delete  
--id          employee  
------------- ------------------------------  
--1           Fred  
--3           Sally  
--@MyTableVar, after delete  
--id          employee  
------------- ------------------------------  
--2           Tom  
--4           Alice  
  
```  
  
> [!NOTE]  
>  Verwenden Sie den READPAST-Tabellenhinweis in UPDATE- und DELETE-Anweisungen, wenn es in Ihrem Szenario möglich ist, dass mehrere Anwendungen einen destruktiven Lesevorgang aus einer Tabelle ausführen. So werden Sperrkonflikte verhindert, die entstehen, wenn eine andere Anwendung bereits den ersten berechtigten Datensatz in der Tabelle liest.  
  
## <a name="permissions"></a>Berechtigungen  
 SELECT-Berechtigungen sind für alle Spalten erforderlich, die über \<dml_select_list> abgerufen oder in \<scalar_expression> verwendet werden.  
  
 INSERT-Berechtigungen sind für alle Tabellen erforderlich, die in \<output_table> angegeben werden.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-using-output-into-with-a-simple-insert-statement"></a>A. Verwenden von OUTPUT INTO mit einer einfachen INSERT-Anweisung  
 Im folgenden Beispiel wird eine Zeile in die `ScrapReason`-Tabelle eingefügt, und die `OUTPUT`-Klausel wird verwendet, um die Ergebnisse der Anweisung an die `@MyTableVar``table`-Variable zurückzugeben. Da die `ScrapReasonID`-Spalte mit einer IDENTITY-Eigenschaft definiert wurde, wird kein Wert in der `INSERT`-Anweisung für diese Spalte angegeben. Der von [!INCLUDE[ssDE](../../includes/ssde-md.md)] für diese Spalte generierte Wert wird jedoch in der `OUTPUT`-Klausel in der `inserted.ScrapReasonID`-Spalte zurückgegeben.  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @MyTableVar table( NewScrapReasonID smallint,  
                           Name varchar(50),  
                           ModifiedDate datetime);  
INSERT Production.ScrapReason  
    OUTPUT INSERTED.ScrapReasonID, INSERTED.Name, INSERTED.ModifiedDate  
        INTO @MyTableVar  
VALUES (N'Operator error', GETDATE());  
  
--Display the result set of the table variable.  
SELECT NewScrapReasonID, Name, ModifiedDate FROM @MyTableVar;  
--Display the result set of the table.  
SELECT ScrapReasonID, Name, ModifiedDate   
FROM Production.ScrapReason;  
GO  
  
```  
  
### <a name="b-using-output-with-a-delete-statement"></a>B. Verwenden von OUTPUT mit einer DELETE-Anweisung  
 Im folgenden Beispiel werden alle Zeilen in der `ShoppingCartItem`-Tabelle gelöscht. Die `OUTPUT deleted.*`-Klausel gibt an, dass die Ergebnisse der `DELETE`-Anweisung, also alle Spalten in den gelöschten Zeilen, an die aufrufende Anweisung zurückgegeben werden. Die nachfolgende `SELECT`-Anweisung überprüft die Ergebnisse des Löschvorgangs in der `ShoppingCartItem`-Tabelle.  
  
```  
USE AdventureWorks2012;  
GO  
DELETE Sales.ShoppingCartItem  
OUTPUT DELETED.*   
WHERE ShoppingCartID = 20621;  
  
--Verify the rows in the table matching the WHERE clause have been deleted.  
SELECT COUNT(*) AS [Rows in Table] FROM Sales.ShoppingCartItem WHERE ShoppingCartID = 20621;  
GO  
  
```  
  
### <a name="c-using-output-into-with-an-update-statement"></a>C. Verwenden von OUTPUT INTO mit einer UPDATE-Anweisung  
 Im folgenden Beispiel werden die ersten zehn Zeilen der `VacationHours`-Spalte in der `Employee`-Tabelle um 25% aktualisiert. Die `OUTPUT`-Klausel gibt den `VacationHours`-Wert vor dem Anwenden der `UPDATE`-Anweisung in der `deleted.VacationHours`-Spalte sowie den aktualisierten Wert in der `inserted.VacationHours`-Spalte an die `@MyTableVar``table`-Variable zurück.  
  
 Es folgen zwei `SELECT`-Anweisungen, die die Werte in `@MyTableVar` und die Ergebnisse des Updatevorgangs in der `Employee`-Tabelle zurückgeben.  
  
```  
USE AdventureWorks2012;  
GO  
  
DECLARE @MyTableVar table(  
    EmpID int NOT NULL,  
    OldVacationHours int,  
    NewVacationHours int,  
    ModifiedDate datetime);  
  
UPDATE TOP (10) HumanResources.Employee  
SET VacationHours = VacationHours * 1.25,  
    ModifiedDate = GETDATE()   
OUTPUT inserted.BusinessEntityID,  
       deleted.VacationHours,  
       inserted.VacationHours,  
       inserted.ModifiedDate  
INTO @MyTableVar;  
  
--Display the result set of the table variable.  
SELECT EmpID, OldVacationHours, NewVacationHours, ModifiedDate  
FROM @MyTableVar;  
GO  
--Display the result set of the table.  
SELECT TOP (10) BusinessEntityID, VacationHours, ModifiedDate  
FROM HumanResources.Employee;  
GO  
  
```  
  
### <a name="d-using-output-into-to-return-an-expression"></a>D. Verwenden von OUTPUT INTO zum Zurückgeben eines Ausdrucks  
 Das folgende Beispiel baut auf Beispiel C auf, indem ein Ausdruck in der `OUTPUT`-Klausel definiert wird, der die Differenz zwischen dem aktualisierten `VacationHours`-Wert und dem `VacationHours`-Wert vor dem Update beschreibt. Der Wert dieses Ausdrucks wird an die `@MyTableVar``table`-Variable in der `VacationHoursDifference`-Spalte zurückgegeben.  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @MyTableVar table(  
    EmpID int NOT NULL,  
    OldVacationHours int,  
    NewVacationHours int,  
    VacationHoursDifference int,  
    ModifiedDate datetime);  
  
UPDATE TOP (10) HumanResources.Employee  
SET VacationHours = VacationHours * 1.25,  
    ModifiedDate = GETDATE()  
OUTPUT inserted.BusinessEntityID,  
       deleted.VacationHours,  
       inserted.VacationHours,  
       inserted.VacationHours - deleted.VacationHours,  
       inserted.ModifiedDate  
INTO @MyTableVar;  
  
--Display the result set of the table variable.  
SELECT EmpID, OldVacationHours, NewVacationHours,   
    VacationHoursDifference, ModifiedDate  
FROM @MyTableVar;  
GO  
SELECT TOP (10) BusinessEntityID, VacationHours, ModifiedDate  
FROM HumanResources.Employee;  
GO  
  
```  
  
### <a name="e-using-output-into-with-fromtablename-in-an-update-statement"></a>E. Verwenden von OUTPUT INTO mit from_table_name in einer UPDATE-Anweisung  
 Im folgenden Beispiel werden alle Arbeitsaufträge in der `ScrapReasonID`-Spalte der `WorkOrder`-Tabelle aktualisiert, für die `ProductID` und `ScrapReasonID` angegeben wurde. Die `OUTPUT INTO`-Klausel gibt Werte aus der Tabelle, die aktualisiert wird (`WorkOrder`), sowie aus der `Product`-Tabelle zurück. Die `Product`-Tabelle wird in der `FROM`-Klausel zur Angabe der zu aktualisierenden Zeilen verwendet. Da für die `WorkOrder`-Tabelle ein `AFTER UPDATE`-Trigger definiert wurde, wird das `INTO`-Schlüsselwort benötigt.  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @MyTestVar table (  
    OldScrapReasonID int NOT NULL,   
    NewScrapReasonID int NOT NULL,   
    WorkOrderID int NOT NULL,  
    ProductID int NOT NULL,  
    ProductName nvarchar(50)NOT NULL);  
  
UPDATE Production.WorkOrder  
SET ScrapReasonID = 4  
OUTPUT deleted.ScrapReasonID,  
       inserted.ScrapReasonID,   
       inserted.WorkOrderID,  
       inserted.ProductID,  
       p.Name  
    INTO @MyTestVar  
FROM Production.WorkOrder AS wo  
    INNER JOIN Production.Product AS p   
    ON wo.ProductID = p.ProductID   
    AND wo.ScrapReasonID= 16  
    AND p.ProductID = 733;  
  
SELECT OldScrapReasonID, NewScrapReasonID, WorkOrderID,   
    ProductID, ProductName   
FROM @MyTestVar;  
GO  
  
```  
  
### <a name="f-using-output-into-with-fromtablename-in-a-delete-statement"></a>F. Verwenden von OUTPUT INTO mit from_table_name in einer DELETE-Anweisung  
 Im folgenden Beispiel werden Zeilen in der `ProductProductPhoto`-Tabelle auf der Grundlage von in der `FROM`-Klausel der `DELETE`-Anweisung definierten Suchkriterien gelöscht. Die `OUTPUT`-Klausel gibt Spalten aus der Tabelle zurück, die gelöscht wird (`deleted.ProductID`, `deleted.ProductPhotoID`), sowie Spalten aus der `Product`-Tabelle. Diese Tabelle wird in der `FROM`-Klausel zur Angabe der zu löschenden Zeilen verwendet.  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @MyTableVar table (  
    ProductID int NOT NULL,   
    ProductName nvarchar(50)NOT NULL,  
    ProductModelID int NOT NULL,   
    PhotoID int NOT NULL);  
  
DELETE Production.ProductProductPhoto  
OUTPUT DELETED.ProductID,  
       p.Name,  
       p.ProductModelID,  
       DELETED.ProductPhotoID  
    INTO @MyTableVar  
FROM Production.ProductProductPhoto AS ph  
JOIN Production.Product as p   
    ON ph.ProductID = p.ProductID   
    WHERE p.ProductModelID BETWEEN 120 and 130;  
  
--Display the results of the table variable.  
SELECT ProductID, ProductName, ProductModelID, PhotoID   
FROM @MyTableVar  
ORDER BY ProductModelID;  
GO  
  
```  
  
### <a name="g-using-output-into-with-a-large-object-data-type"></a>G. Verwenden von OUTPUT INTO mit einem großen Objektdatentyp  
 Im folgenden Beispiel wird ein Teilwert in `DocumentSummary`, eine `nvarchar(max)`-Spalte in der `Production.Document`-Tabelle, mithilfe der `.WRITE`-Klausel aktualisiert. Der Begriff `components` wird durch den Begriff `features` ersetzt, indem der Ersatzbegriff, die Anfangsposition (offset) des zu ersetzenden Begriffs in den vorhandenen Daten und die Anzahl der zu ersetzenden Zeichen (length) angegeben werden. Im Beispiel wird die `OUTPUT`-Klausel zur Rückgabe der Anfangs- und Endimages der `DocumentSummary`-Spalte an die `@MyTableVar``table`-Variable verwendet. Hierbei werden die vollständigen Anfangs- und Endimages der `DocumentSummary`-Spalte zurückgegeben.  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @MyTableVar table (  
    SummaryBefore nvarchar(max),  
    SummaryAfter nvarchar(max));  
  
UPDATE Production.Document  
SET DocumentSummary .WRITE (N'features',28,10)  
OUTPUT deleted.DocumentSummary,   
       inserted.DocumentSummary   
    INTO @MyTableVar  
WHERE Title = N'Front Reflector Bracket Installation';  
  
SELECT SummaryBefore, SummaryAfter   
FROM @MyTableVar;  
GO  
  
```  
  
### <a name="h-using-output-in-an-instead-of-trigger"></a>H. Verwenden von OUTPUT in einem INSTEAD OF-Trigger  
 Im folgenden Beispiel werden die Ergebnisse des Triggervorgangs mithilfe der `OUTPUT`-Klausel in einem Trigger zurückgegeben. Zunächst wird eine Sicht in der `ScrapReason`-Tabelle erstellt und anschließend ein `INSTEAD OF INSERT`-Trigger für die Sicht definiert, der nur zulässt, dass Benutzer die `Name`-Spalte der Basistabelle ändern können. Da die `ScrapReasonID`-Spalte eine `IDENTITY`-Spalte in der Basistabelle ist, ignoriert der Trigger den vom Benutzer bereitgestellten Wert. Dadurch kann [!INCLUDE[ssDE](../../includes/ssde-md.md)] automatisch den richtigen Wert generieren. Darüber hinaus wird der vom Benutzer für `ModifiedDate` bereitgestellte Wert ignoriert und auf das aktuelle Datum festgelegt. Die `OUTPUT`-Klausel gibt die tatsächlich in die `ScrapReason`-Tabelle eingefügten Werte zurück.  
  
```  
USE AdventureWorks2012;  
GO  
IF OBJECT_ID('dbo.vw_ScrapReason','V') IS NOT NULL  
    DROP VIEW dbo.vw_ScrapReason;  
GO  
CREATE VIEW dbo.vw_ScrapReason  
AS (SELECT ScrapReasonID, Name, ModifiedDate  
    FROM Production.ScrapReason);  
GO  
CREATE TRIGGER dbo.io_ScrapReason   
    ON dbo.vw_ScrapReason  
INSTEAD OF INSERT  
AS  
BEGIN  
--ScrapReasonID is not specified in the list of columns to be inserted   
--because it is an IDENTITY column.  
    INSERT INTO Production.ScrapReason (Name, ModifiedDate)  
        OUTPUT INSERTED.ScrapReasonID, INSERTED.Name,   
               INSERTED.ModifiedDate  
    SELECT Name, getdate()  
    FROM inserted;  
END  
GO  
INSERT vw_ScrapReason (ScrapReasonID, Name, ModifiedDate)  
VALUES (99, N'My scrap reason','20030404');  
GO  
  
```  
  
 Dies ist das am 12. April 2004 ('`2004-04-12'`) generierte Resultset. Die Spalten `ScrapReasonIDActual` und `ModifiedDate` spiegeln die vom Triggervorgang generierten Werte wider, anstelle der von der `INSERT`-Anweisung bereitgestellten Werte.  
  
 ```
 ScrapReasonID  Name             ModifiedDate  
 -------------  ---------------- -----------------------  
 17             My scrap reason  2004-04-12 16:23:33.050
 ```  
  
### <a name="i-using-output-into-with-identity-and-computed-columns"></a>I. Verwenden von OUTPUT INTO mit Identitätsspalten und berechneten Spalten  
 Im folgenden Beispiel wird die `EmployeeSales`-Tabelle erstellt, und anschließend werden mehrere Zeilen unter Verwendung einer `INSERT`-Anweisung mit einer `SELECT`-Anweisung in die Tabelle eingefügt, um Daten aus Quelltabellen abzurufen. Die `EmployeeSales`-Tabelle enthält eine Identitätsspalte (`EmployeeID`) und eine berechnete Spalte (`ProjectedSales`).  
  
```  
USE AdventureWorks2012 ;  
GO  
IF OBJECT_ID ('dbo.EmployeeSales', 'U') IS NOT NULL  
    DROP TABLE dbo.EmployeeSales;  
GO  
CREATE TABLE dbo.EmployeeSales  
( EmployeeID   int IDENTITY (1,5)NOT NULL,  
  LastName     nvarchar(20) NOT NULL,  
  FirstName    nvarchar(20) NOT NULL,  
  CurrentSales money NOT NULL,  
  ProjectedSales AS CurrentSales * 1.10   
);  
GO  
DECLARE @MyTableVar table(  
  EmployeeID   int NOT NULL,  
  LastName     nvarchar(20) NOT NULL,  
  FirstName    nvarchar(20) NOT NULL,  
  CurrentSales money NOT NULL,  
  ProjectedSales money NOT NULL  
  );  
  
INSERT INTO dbo.EmployeeSales (LastName, FirstName, CurrentSales)  
  OUTPUT INSERTED.LastName,   
         INSERTED.FirstName,   
         INSERTED.CurrentSales  
  INTO @MyTableVar  
    SELECT c.LastName, c.FirstName, sp.SalesYTD  
    FROM Sales.SalesPerson AS sp  
    INNER JOIN Person.Person AS c  
        ON sp.BusinessEntityID = c.BusinessEntityID  
    WHERE sp.BusinessEntityID LIKE '2%'  
    ORDER BY c.LastName, c.FirstName;  
  
SELECT EmployeeID, LastName, FirstName, CurrentSales, ProjectedSales  
FROM @MyTableVar;  
GO  
SELECT EmployeeID, LastName, FirstName, CurrentSales, ProjectedSales  
FROM dbo.EmployeeSales;  
GO  
  
```  
  
### <a name="j-using-output-and-output-into-in-a-single-statement"></a>J. Verwenden von OUTPUT und OUTPUT INTO in einer einzelnen Anweisung  
 Im folgenden Beispiel werden Zeilen in der `ProductProductPhoto`-Tabelle auf der Grundlage von in der `FROM`-Klausel der `DELETE`-Anweisung definierten Suchkriterien gelöscht. Die `OUTPUT INTO`-Klausel gibt Spalten aus der Tabelle, die gelöscht wird (`deleted.ProductID`, `deleted.ProductPhotoID`), sowie Spalten aus der `Product`-Tabelle an die `@MyTableVar``table`-Variable zurück. Die `Product`-Tabelle wird in der `FROM`-Klausel zur Angabe der zu löschenden Zeilen verwendet. Die `OUTPUT`-Klausel gibt die Spalten `deleted.ProductID` und `deleted.ProductPhotoID` sowie das Datum und die Uhrzeit des Löschens der Zeile aus der `ProductProductPhoto`-Tabelle an die aufrufende Anwendung zurück.  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @MyTableVar table (  
    ProductID int NOT NULL,   
    ProductName nvarchar(50)NOT NULL,  
    ProductModelID int NOT NULL,   
    PhotoID int NOT NULL);  
  
DELETE Production.ProductProductPhoto  
OUTPUT DELETED.ProductID,  
       p.Name,  
       p.ProductModelID,  
       DELETED.ProductPhotoID  
    INTO @MyTableVar  
OUTPUT DELETED.ProductID, DELETED.ProductPhotoID, GETDATE() AS DeletedDate   
FROM Production.ProductProductPhoto AS ph  
JOIN Production.Product as p   
    ON ph.ProductID = p.ProductID   
WHERE p.ProductID BETWEEN 800 and 810;  
  
--Display the results of the table variable.  
SELECT ProductID, ProductName, PhotoID, ProductModelID   
FROM @MyTableVar;  
GO  
  
```  
  
### <a name="k-inserting-data-returned-from-an-output-clause"></a>K. Einfügen von Daten, die von einer OUTPUT-Klausel zurückgegeben wurden  
 Im folgenden Beispiel werden von der `OUTPUT`-Klausel einer `MERGE`-Anweisung zurückgegebene Daten erfasst und in eine andere Tabelle eingefügt. Die `MERGE`-Anweisung aktualisiert die `Quantity`-Spalte der `ProductInventory`-Tabelle täglich auf Grundlage der Bestellungen, die in der `SalesOrderDetail`-Tabelle verarbeitet werden. Außerdem werden die Zeilen für Produkte gelöscht, deren Bestand auf `0` oder darunter fällt. Das Beispiel erfasst die gelöschten Zeilen und fügt sie in einer anderen Tabelle (`ZeroInventory`) ein, in der Produkte ohne Bestand gespeichert werden.  
  
```  
USE AdventureWorks2012;  
GO  
IF OBJECT_ID(N'Production.ZeroInventory', N'U') IS NOT NULL  
    DROP TABLE Production.ZeroInventory;  
GO  
--Create ZeroInventory table.  
CREATE TABLE Production.ZeroInventory (DeletedProductID int, RemovedOnDate DateTime);  
GO  
  
INSERT INTO Production.ZeroInventory (DeletedProductID, RemovedOnDate)  
SELECT ProductID, GETDATE()  
FROM  
(   MERGE Production.ProductInventory AS pi  
    USING (SELECT ProductID, SUM(OrderQty) FROM Sales.SalesOrderDetail AS sod  
           JOIN Sales.SalesOrderHeader AS soh  
           ON sod.SalesOrderID = soh.SalesOrderID  
           AND soh.OrderDate = '20070401'  
           GROUP BY ProductID) AS src (ProductID, OrderQty)  
    ON (pi.ProductID = src.ProductID)  
    WHEN MATCHED AND pi.Quantity - src.OrderQty <= 0  
        THEN DELETE  
    WHEN MATCHED  
        THEN UPDATE SET pi.Quantity = pi.Quantity - src.OrderQty  
    OUTPUT $action, deleted.ProductID) AS Changes (Action, ProductID)  
WHERE Action = 'DELETE';  
IF @@ROWCOUNT = 0  
PRINT 'Warning: No rows were inserted';  
GO  
SELECT DeletedProductID, RemovedOnDate FROM Production.ZeroInventory;  
  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [DELETE &#40;Transact-SQL&#41;](../../t-sql/statements/delete-transact-sql.md)   
 [INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)   
 [UPDATE (Transact-SQL)](../../t-sql/queries/update-transact-sql.md)   
 [table &#40;Transact-SQL&#41;](../../t-sql/data-types/table-transact-sql.md)   
 [CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  

---
title: DELETE (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 05/10/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- DELETE
- DELETE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- row removal [SQL Server]
- DELETE statement [SQL Server], about DELETE statement
- views [SQL Server], deleting rows
- removing rows
- tables [SQL Server], deleting rows
- DELETE statement [SQL Server]
- deleting rows
- row removal [SQL Server], DELETE statement
- deleting data
ms.assetid: ed6b2105-0f35-408f-ba51-e36ade7ad5b2
caps.latest.revision: 78
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: a30704357c724c3a7e5ecc78569aecdd62687e8d
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="delete-transact-sql"></a>DELETE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Entfernt mindestens eine Zeile aus einer Tabelle oder Sicht in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
[ WITH <common_table_expression> [ ,...n ] ]  
DELETE   
    [ TOP ( expression ) [ PERCENT ] ]   
    [ FROM ]   
    { { table_alias  
      | <object>   
      | rowset_function_limited   
      [ WITH ( table_hint_limited [ ...n ] ) ] }   
      | @table_variable  
    }  
    [ <OUTPUT Clause> ]  
    [ FROM table_source [ ,...n ] ]   
    [ WHERE { <search_condition>   
            | { [ CURRENT OF   
                   { { [ GLOBAL ] cursor_name }   
                       | cursor_variable_name   
                   }   
                ]  
              }  
            }   
    ]   
    [ OPTION ( <Query Hint> [ ,...n ] ) ]   
[; ]  
  
<object> ::=  
{   
    [ server_name.database_name.schema_name.   
      | database_name. [ schema_name ] .   
      | schema_name.  
    ]  
    table_or_view_name   
}  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
DELETE FROM [database_name . [ schema ] . | schema. ] table_name    
    [ WHERE <search_condition> ]   
    [ OPTION ( <query_options> [ ,...n ]  ) ]  
[; ]  
```  
  
## <a name="arguments"></a>Argumente  
 WITH \<common_table_expression>  
 Gibt das temporäre benannte Resultset, auch als allgemeiner Tabellenausdruck bezeichnet, an, das im Rahmen der DELETE-Anweisung definiert wurde. Das Resultset wird von einer SELECT-Anweisung abgeleitet.  
  
 Allgemeine Tabellenausdrücke können außerdem mit SELECT-, INSERT-, UPDATE- und CREATE VIEW-Anweisungen verwendet werden. Weitere Informationen finden Sie unter [WITH common_table_expression &#40;Transact-SQL&#41;](../../t-sql/queries/with-common-table-expression-transact-sql.md).  
  
 TOP **(***expression***)** [ PERCENT ]  
 Gibt die Anzahl oder den Prozentsatz willkürlicher Zeilen an, die gelöscht werden. *expression* kann eine Anzahl oder ein Prozentsatz der Zeilen sein. Die Zeilen, auf die im TOP-Ausdruck für die Anweisung INSERT, UPDATE oder DELETE verwiesen wird, sind nicht auf bestimmte Weise angeordnet. Weitere Informationen finden Sie unter [TOP &#40;Transact-SQL&#41;](../../t-sql/queries/top-transact-sql.md).  
  
 FROM  
 Ein optionales Schlüsselwort, das zwischen dem DELETE-Schlüsselwort und den Zielen *table_or_view_name* oder *rowset_function_limited* verwendet werden kann.  
  
 *table_alias*  
 Der in der FROM-*table_source*-Klausel angegebene Alias, der die Tabelle oder Sicht darstellt, aus der die Zeilen gelöscht werden sollen.  
  
 *server_name*  
 **Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Der Name des Servers (der einen Verbindungsservernamen oder die Funktion [OPENDATASOURCE](../../t-sql/functions/opendatasource-transact-sql.md) als Servernamen verwendet), auf dem sich die Tabelle oder die Sicht befindet. Wenn *server_name* angegeben ist, sind *database_name* und *schema_name* erforderlich.  
  
 *database_name*  
 Der Name der Datenbank.  
  
 *schema_name*  
 Der Name des Schemas, zu dem die Tabelle oder Sicht gehören.  
  
 *table_or_view_name*  
 Der Name der Tabelle oder Sicht, aus der die Zeilen entfernt werden sollen.  
  
 In ihrem Gültigkeitsbereich kann eine Tabellenvariable auch als Quelltabelle in einer DELETE-Anweisung verwendet werden.  
  
 Die Sicht, auf die *table_or_view_name* verweist, muss aktualisierbar sein und auf genau eine Basistabelle in der FROM-Klausel der Sichtdefinition verweisen. Weitere Informationen zu aktualisierbaren Sichten finden Sie unter [CREATE VIEW &#40;Transact-SQL&#41;](../../t-sql/statements/create-view-transact-sql.md).  
  
 *rowset_function_limited*  
 **Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Entweder die Funktion [OPENQUERY](../../t-sql/functions/openquery-transact-sql.md) oder [OPENROWSET](../../t-sql/functions/openrowset-transact-sql.md), abhängig von den Funktionen des Anbieters.  
  
 WITH **(** \<table_hint_limited> [... *n*] **)**  
 Gibt mindestens einen Tabellenhinweis an, der für eine Zieltabelle zulässig ist. Das WITH-Schlüsselwort und die Klammern sind erforderlich. NOLOCK und READUNCOMMITTED sind nicht zulässig. Weitere Informationen zu Tabellenhinweisen finden Sie unter [Tabellenhinweise &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-table.md).  
  
 \<OUTPUT_Clause>  
 Gibt gelöschte Zeilen bzw. auf diesen basierende Ausdrücke als Teil der DELETE-Operation zurück. Die OUTPUT-Klausel wird in DML-Anweisungen, deren Ziel Sichten oder Remotetabellen sind, nicht unterstützt. Weitere Informationen finden Sie unter [OUTPUT-Klausel &#40;Transact-SQL&#41;](../../t-sql/queries/output-clause-transact-sql.md).  
  
 FROM *table_source*  
 Gibt eine zusätzliche FROM-Klausel an. Diese [!INCLUDE[tsql](../../includes/tsql-md.md)]-Erweiterung für DELETE ermöglicht es Ihnen, Daten aus \<table_source> anzugeben und die entsprechenden Zeilen aus der Tabelle in der ersten FROM-Klausel zu löschen.  
  
 Diese Erweiterung, die einen Join angibt, kann anstelle einer Unterabfrage in der WHERE-Klausel verwendet werden, um zu entfernende Zeilen zu identifizieren.  
  
 Weitere Informationen finden Sie unter [FROM &#40;Transact-SQL&#41;](../../t-sql/queries/from-transact-sql.md).  
  
 WHERE  
 Gibt die Bedingungen an, die zur Beschränkung der Anzahl der gelöschten Zeilen verwendet werden. Wird keine WHERE-Klausel angegeben, werden mit DELETE alle Zeilen aus der Tabelle entfernt.  
  
 Es gibt zwei Formen von Löschoperationen, die darauf basieren, was in der WHERE-Klausel angegeben wird:  
  
-   Gesuchte Löschungen geben eine Suchbedingung an, um die zu löschenden Zeilen zu kennzeichnen. Zum Beispiel WHERE *column_name* = *value*.  
  
-   Positionierte Löschungen verwenden die CURRENT OF-Klausel, um einen Cursor anzugeben. Die Löschoperation wird an der aktuellen Position des Cursors ausgeführt. Dies kann genauer sein als eine gesuchte DELETE-Anweisung, die eine WHERE *search_condition*-Klausel zur Qualifizierung der zu löschenden Zeilen verwendet. Eine gesuchte DELETE-Anweisung löscht mehrere Zeilen, wenn die Suchbedingung nicht eindeutig eine einzelne Zeile identifiziert.  
  
\<search_condition>  
 Gibt die Einschränkungsbedingungen für die zu löschenden Zeilen an. Es gibt keinen Höchstwert hinsichtlich der Anzahl von Prädikaten in einer Suchbedingung. Weitere Informationen finden Sie unter [Suchbedingung &#40;Transact-SQL&#41;](../../t-sql/queries/search-condition-transact-sql.md).  
  
 CURRENT OF  
 Gibt an, dass DELETE an der aktuellen Position des angegebenen Cursors durchgeführt wird.  
  
 GLOBAL  
 Gibt an, dass *cursor_name* auf einen globalen Cursor verweist.  
  
 *cursor_name*  
 Der Name des geöffneten Cursors, von dem der Abruf erfolgt. Wenn sowohl ein globaler als auch ein lokaler Cursor namens *cursor_name* vorhanden sind, bezieht sich dieses Argument auf den globalen Cursor, wenn GLOBAL angegeben ist. Andernfalls bezieht es sich auf den lokalen Cursor. Der Cursor muss Updates zulassen.  
  
 *cursor_variable_name*  
 Der Name einer Cursorvariablen. Die Cursorvariable muss auf einen Cursor verweisen, der Updates zulässt.  
  
 OPTION **(** \<query_hint> [ **,**... *n*] **)**  
 Schlüsselwörter, die angeben, dass Hinweise für den Optimierer verwendet werden, um die Verarbeitung der Anweisung durch [!INCLUDE[ssDE](../../includes/ssde-md.md)] anzupassen. Weitere Informationen finden Sie unter [Abfragehinweise &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-query.md).  
  
## <a name="best-practices"></a>Bewährte Methoden  
 Um alle Zeilen in einer Tabelle zu löschen, verwenden Sie TRUNCATE TABLE. TRUNCATE TABLE ist schneller als DELETE und verwendet weniger Systemressourcen und Ressourcen für die Transaktionsprotokollierung. Für TRUNCATE TABLE gelten Einschränkungen, beispielsweise kann die Tabelle nicht in Replikationen verwendet werden. Weitere Informationen finden Sie unter [TRUNCATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/truncate-table-transact-sql.md).  
  
 Verwenden Sie die @@ROWCOUNT-Funktion, um die Anzahl der gelöschten Zeilen an die Clientanwendung zurückzugeben. Weitere Informationen finden Sie unter [@@ROWCOUNT &#40;Transact-SQL&#41;](../../t-sql/functions/rowcount-transact-sql.md).  
  
## <a name="error-handling"></a>Fehlerbehandlung  
 Sie können die Fehlerbehandlung für die DELETE-Anweisung durch Angeben der Anweisung in einem TRY…CATCH-Konstrukt implementieren.  
  
 Die DELETE-Anweisung erzeugt möglicherweise einen Fehler, wenn sie gegen einen Trigger verstößt oder versucht, eine Zeile zu entfernen, auf die von Daten einer anderen Tabelle mit einer FOREIGN KEY-Einschränkung verwiesen wird. Entfernt die DELETE-Anweisung mehrere Zeilen und verstößt eine der entfernten Zeilen gegen einen Trigger oder eine Einschränkung, wird die Anweisung abgebrochen, ein Fehler gemeldet und keine Zeilen entfernt.  
  
 Wenn in einer DELETE-Anweisung bei der Auswertung eines Ausdrucks ein arithmetischer Fehler (Überlauf, Division durch null oder Domänenfehler) auftritt, behandelt [!INCLUDE[ssDE](../../includes/ssde-md.md)] den Fehler so, als wäre SET ARITHABORT auf ON festgelegt. Der Rest des Batches wird abgebrochen, und eine Fehlermeldung wird zurückgegeben.  
  
## <a name="interoperability"></a>Interoperabilität  
 DELETE kann im Textkörper einer benutzerdefinierten Funktion verwendet werden, wenn es sich bei dem geänderten Objekt um eine Tabellenvariable handelt.  
  
 Wenn Sie eine Zeile mit einer FILESTREAM-Spalte löschen, löschen Sie auch die zugrunde liegenden Dateisystemdateien. Die zugrunde liegenden Dateien werden vom FILESTREAM Garbage Collector entfernt. Weitere Informationen finden Sie unter [Zugreifen auf FILESTREAM-Daten mit Transact-SQL](../../relational-databases/blob/access-filestream-data-with-transact-sql.md).  
  
 Die FROM-Klausel kann nicht für eine DELETE-Anweisung angegeben werden, die entweder direkt oder indirekt auf eine Sicht verweist, für die ein INSTEAD OF-Trigger definiert wurde. Weitere Informationen zu INSTEAD OF-Triggern finden Sie unter [CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md).  
  
## <a name="limitations-and-restrictions"></a>Einschränkungen  
 Wenn TOP mit ENTF verwendet wird, werden die Zeilen, auf die verwiesen wird, nicht auf bestimmte Weise angeordnet, und die ORDER BY-Klausel kann in dieser Anweisung nicht direkt angegeben werden. Wenn Sie die TOP-Klausel verwenden müssen, um Zeilen in einer sinnvollen Reihenfolge zu löschen, müssen Sie sie zusammen mit einer ORDER BY-Klausel in einer untergeordneten SELECT-Anweisung verwenden. Weitere Informationen finden Sie im Abschnitt "Beispiele" in diesem Thema.  
  
 TOP kann nicht in einer DELETE-Anweisung mit partitionierten Sichten verwendet werden.  
  
## <a name="locking-behavior"></a>Sperrverhalten  
 Eine DELETE-Anweisung ruft immer eine exklusive (X) Sperre für die von ihr geänderte Tabelle ab und hält diese Sperre bis zum Abschluss der Transaktion aufrecht. Eine exklusive Sperre (X) bewirkt, dass keine andere Transaktion Daten ändern kann. Lesevorgänge können nur mithilfe des NOLOCK-Hinweises oder der READ UNCOMMITTED-Isolationsstufe ausgeführt werden. Sie können Tabellenhinweise angeben, um dieses Standardverhalten für die Dauer der DELETE-Anweisung zu überschreiben, indem Sie eine andere Sperrmethode angeben. Es wird jedoch empfohlen, dass Hinweise nur von erfahrenen Entwicklern und Datenbankadministratoren und nur als letzte Möglichkeit verwendet werden. Weitere Informationen finden Sie unter [Tabellenhinweise &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-table.md).  
  
 Wenn Zeilen aus einem Heap gelöscht werden, können von [!INCLUDE[ssDE](../../includes/ssde-md.md)] Zeilen- oder Seitensperren für den Vorgang verwendet werden. Demzufolge bleiben die durch den Löschvorgang geleerten Seiten dem Heap zugeordnet. Wenn die Zuordnung leerer Seiten nicht aufgehoben wird, kann der zugehörige Speicherplatz nicht für andere Objekte in der Datenbank verwendet werden.  
  
 Verwenden Sie eine der folgenden Methoden, um Zeilen in einem Heap zu löschen und die Zuordnung der Seiten aufzuheben:  
  
-   Geben Sie den TABLOCK-Hinweis in der DELETE-Anweisung an. Mithilfe des TABLOCK-Hinweises wird durch den Löschvorgang eine exklusive Sperre für die Tabelle statt einer Zeilen- oder Seitensperre angefordert. Dadurch ist es möglich, die Zuordnung der Seiten aufzuheben. Weitere Informationen zu dem TABLOCK-Hinweis finden Sie unter [Tabellenhinweise &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-table.md).  
  
-   Verwenden Sie TRUNCATE TABLE, wenn alle Zeilen aus der Tabelle gelöscht werden sollen.  
  
-   Erstellen Sie einen gruppierten Index für den Heap, bevor Sie die Zeilen löschen. Nach dem Löschen der Zeilen können Sie den gruppierten Index löschen. Diese Methode ist zeitaufwändiger als die vorherigen Methoden und beansprucht mehr temporäre Ressourcen.  
  
> [!NOTE]  
>  Leere Seiten können zu jeder Zeit mithilfe der Anweisung `ALTER TABLE <table_name> REBUILD` aus einem Heap gelöscht werden.  
  
## <a name="logging-behavior"></a>Protokollierungsverhalten  
 Die DELETE-Anweisung wird immer vollständig protokolliert.  
  
## <a name="security"></a>Security  
  
### <a name="permissions"></a>Berechtigungen  
 Für die Zieltabelle sind DELETE-Berechtigungen erforderlich. SELECT-Berechtigungen werden ebenfalls benötigt, wenn die Anweisung eine WHERE-Klausel enthält.  
  
 Mitglieder der festen Serverrolle **sysadmin**, der festen Datenbankrollen **db_owner** und **db_datawriter** und der Tabellenbesitzer erhalten standardmäßig DELETE-Berechtigungen. Mitglieder der Rollen **sysadmin**, **db_owner** und **db_securityadmin** sowie der Tabellenbesitzer können Berechtigungen an andere Benutzer übertragen.  
  
## <a name="examples"></a>Beispiele  
  
|Kategorie|Funktionssyntaxelemente|  
|--------------|------------------------------|  
|[Grundlegende Syntax](#BasicSyntax)|Delete|  
|[Beschränken von zu löschenden Zeilen](#LimitRows)|WHERE • FROM • Cursor •|  
|[Löschen von Zeilen aus einer Remotetabelle](#RemoteTables)|Verbindungsserver • OPENQUERY-Rowsetfunktion • OPENDATASOURCE-Rowsetfunktion|  
|[Erfassen der Ergebnisse der DELETE-Anweisung](#CaptureResults)|OUTPUT-Klausel|  
  
###  <a name="BasicSyntax"></a> Grundlegende Syntax  
 Anhand von Beispielen in diesem Abschnitt wird die grundlegende Funktion der DELETE-Anweisung mithilfe der mindestens erforderlichen Syntax veranschaulicht.  
  
#### <a name="a-using-delete-with-no-where-clause"></a>A. Verwenden von DELETE ohne WHERE-Klausel  
 Im folgenden Beispiel werden alle Zeilen aus der `SalesPersonQuotaHistory`-Tabelle in der [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]-Datenbank gelöscht, da keine WHERE-Klausel verwendet wird, um die Anzahl der gelöschten Zeilen zu begrenzen.  
  
```  
DELETE FROM Sales.SalesPersonQuotaHistory;  
GO  
```  
  
###  <a name="LimitRows"></a> Beschränken von zu löschenden Zeilen  
 In den Beispielen in diesem Abschnitt wird veranschaulicht, wie die Anzahl von Zeilen beschränkt wird, die gelöscht werden.  
  
#### <a name="b-using-the-where-clause-to-delete-a-set-of-rows"></a>B. Löschen einer Reihe von Zeilen mithilfe der WHERE-Klausel  
 Im folgenden Beispiel werden alle Zeilen der Tabelle `ProductCostHistory` aus der Datenbank [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] gelöscht, bei denen der Wert `1000.00` in der Spalte `StandardCost` überschritten wird.  
  
```    
DELETE FROM Production.ProductCostHistory  
WHERE StandardCost > 1000.00;  
GO  
```  
  
 Im folgenden Beispiel wird eine komplexere WHERE-Klausel veranschaulicht. Die WHERE-Klausel definiert zwei Bedingungen, die erfüllt werden müssen, um die zu löschenden Zeilen zu bestimmen. Der Wert in der `StandardCost` -Spalte muss zwischen `12.00` und `14.00` liegen, und der Wert in der `SellEndDate` -Spalte muss NULL sein. Im Beispiel wird auch der Wert der **@@ROWCOUNT**-Funktion ausgegeben, um die Anzahl der gelöschten Zeilen zurückzugeben.  
  
```  
DELETE Production.ProductCostHistory  
WHERE StandardCost BETWEEN 12.00 AND 14.00  
      AND EndDate IS NULL;  
PRINT 'Number of rows deleted is ' + CAST(@@ROWCOUNT as char(3));  
```  
  
#### <a name="c-using-a-cursor-to-determine-the-row-to-delete"></a>C. Bestimmen der zu löschenden Zeile mithilfe eines Cursors  
 Im folgenden Beispiel wird eine einzelne Zeile aus der Tabelle `EmployeePayHistory` in der Datenbank [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] mithilfe eines Cursors namens `my_cursor` gelöscht. Von der Löschoperation ist nur die Zeile betroffen, die aktuell durch den Cursor abgerufen wird.  
  
```  
DECLARE complex_cursor CURSOR FOR  
    SELECT a.BusinessEntityID  
    FROM HumanResources.EmployeePayHistory AS a  
    WHERE RateChangeDate <>   
         (SELECT MAX(RateChangeDate)  
          FROM HumanResources.EmployeePayHistory AS b  
          WHERE a.BusinessEntityID = b.BusinessEntityID) ;  
OPEN complex_cursor;  
FETCH FROM complex_cursor;  
DELETE FROM HumanResources.EmployeePayHistory  
WHERE CURRENT OF complex_cursor;  
CLOSE complex_cursor;  
DEALLOCATE complex_cursor;  
GO  
```  
  
#### <a name="d-using-joins-and-subqueries-to-data-in-one-table-to-delete-rows-in-another-table"></a>D. Verwenden von Joins und Unterabfragen für Daten in einer Tabelle, um Zeilen in einer anderen Tabelle zu löschen  
 In den folgenden Beispielen werden zwei Möglichkeiten veranschaulicht, Zeilen in einer Tabelle anhand von Daten in einer anderen Tabelle zu löschen. In beiden Beispielen werden Zeilen aus der Tabelle `SalesPersonQuotaHistory` aus der Datenbank [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] anhand der Verkaufszahlen des laufenden Jahres gelöscht, die in der Tabelle `SalesPerson` gespeichert sind. Die erste Anweisung `DELETE` zeigt die Lösung mit einer ISO-kompatiblen Unterabfrage, die zweite Anweisung `DELETE` zeigt die FROM-Erweiterung [!INCLUDE[tsql](../../includes/tsql-md.md)] zum Verknüpfen der beiden Tabellen an.  
  
```  
-- SQL-2003 Standard subquery  
  
DELETE FROM Sales.SalesPersonQuotaHistory   
WHERE BusinessEntityID IN   
    (SELECT BusinessEntityID   
     FROM Sales.SalesPerson   
     WHERE SalesYTD > 2500000.00);  
GO  
```  
  
```  
-- Transact-SQL extension  
  
DELETE FROM Sales.SalesPersonQuotaHistory   
FROM Sales.SalesPersonQuotaHistory AS spqh  
INNER JOIN Sales.SalesPerson AS sp  
ON spqh.BusinessEntityID = sp.BusinessEntityID  
WHERE sp.SalesYTD > 2500000.00;  
GO  
```  
  
```  
-- No need to mention target table more than once.  
  
DELETE spqh  
  FROM  
        Sales.SalesPersonQuotaHistory AS spqh  
    INNER JOIN Sales.SalesPerson AS sp  
        ON spqh.BusinessEntityID = sp.BusinessEntityID  
  WHERE  sp.SalesYTD > 2500000.00;  
```  
  
#### <a name="e-using-top-to-limit-the-number-of-rows-deleted"></a>E. Verwenden von TOP, um die Anzahl der zu löschenden Zeilen einzuschränken  
 Wenn eine TOP (*n*)-Klausel zusammen mit DELETE verwendet wird, wird der Löschvorgang für eine zufällige Auswahl von *n* Zeilen ausgeführt. Im folgenden Beispiel werden `20` zufällige Zeilen aus der Tabelle `PurchaseOrderDetail` in der Datenbank [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] gelöscht, die ein Fälligkeitsdatum vor dem 1. Juli 2006 aufweisen.  
  
```  
DELETE TOP (20)   
FROM Purchasing.PurchaseOrderDetail  
WHERE DueDate < '20020701';  
GO  
```  
  
 Wenn Sie die TOP-Klausel verwenden müssen, um Zeilen in einer sinnvollen Reihenfolge zu löschen, müssen Sie sie zusammen mit ORDER BY in einer untergeordneten SELECT-Anweisung verwenden. Die folgende Abfrage löscht die zehn Zeilen der `PurchaseOrderDetail` -Tabelle mit den frühesten Fälligkeitsdaten. Die in der untergeordneten SELECT-Anweisung angegebene Spalte (`PurchaseOrderID`) ist der Primärschlüssel der Tabelle, um sicherzustellen, dass nur 10 Zeilen gelöscht werden. Wird in der untergeordneten SELECT-Anweisung eine Nichtschlüsselspalte verwendet, werden möglicherweise mehr als 10 Zeilen gelöscht, wenn die angegebene Spalte doppelte Werte enthält.  
  
```  
DELETE FROM Purchasing.PurchaseOrderDetail  
WHERE PurchaseOrderDetailID IN  
   (SELECT TOP 10 PurchaseOrderDetailID   
    FROM Purchasing.PurchaseOrderDetail   
    ORDER BY DueDate ASC);  
GO  
```  
  
###  <a name="RemoteTables"></a> Löschen von Zeilen aus einer Remotetabelle  
 In den Beispielen in diesem Abschnitt wird veranschaulicht, wie Zeilen mit einem [Verbindungsserver](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md) oder einer [Rowsetfunktion](../../t-sql/functions/rowset-functions-transact-sql.md) aus einer Remotezieltabelle gelöscht werden, um auf die Remotetabelle zu verweisen. Eine Remotetabelle ist auf einem anderen Server oder in einer anderen Instanz von SQL Server vorhanden.  
  
**Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
#### <a name="f-deleting-data-from-a-remote-table-by-using-a-linked-server"></a>F. Löschen von Daten aus einer Remotetabelle mithilfe eines Verbindungsservers  
 Im folgenden Beispiel werden Zeilen aus einer Remotetabelle gelöscht. In diesem Beispiel wird zunächst mithilfe von [sp_addlinkedserver](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md) ein Link zur Remotedatenquelle erstellt. Der Name des Verbindungsservers (`MyLinkServer`) wird anschließend als Teil des vierteiligen Objektnamens in der Form *server.catalog.schema.object* angegeben.  
  
```  
USE master;  
GO  
-- Create a link to the remote data source.   
-- Specify a valid server name for @datasrc as 'server_name' or 'server_name\instance_name'.  
  
EXEC sp_addlinkedserver @server = N'MyLinkServer',  
    @srvproduct = N' ',  
    @provider = N'SQLNCLI',   
    @datasrc = N'server_name',  
    @catalog = N'AdventureWorks2012';  
GO  
```  
  
```  
-- Specify the remote data source using a four-part name   
-- in the form linked_server.catalog.schema.object.  
  
DELETE MyLinkServer.AdventureWorks2012.HumanResources.Department 
WHERE DepartmentID > 16;  
GO  
```  
  
#### <a name="g-deleting-data-from-a-remote-table-by-using-the-openquery-function"></a>G. Löschen von Daten aus einer Remotetabelle mithilfe der OPENQUERY-Funktion  
 Im folgenden Beispiel werden durch Angabe der Rowsetfunktion [OPENQUERY](../../t-sql/functions/openquery-transact-sql.md) Zeilen aus einer Remotetabelle gelöscht. Der im vorherigen Beispiel erstellte Name des Verbindungsservers wird hier verwendet.  
  
```  
DELETE OPENQUERY (MyLinkServer, 'SELECT Name, GroupName 
FROM AdventureWorks2012.HumanResources.Department  
WHERE DepartmentID = 18');  
GO  
```  
  
#### <a name="h-deleting-data-from-a-remote-table-by-using-the-opendatasource-function"></a>H. Löschen von Daten aus einer Remotetabelle mithilfe der OPENDATASOURCE-Funktion  
 Im folgenden Beispiel werden durch Angabe der Rowsetfunktion [OPENDATASOURCE](../../t-sql/functions/opendatasource-transact-sql.md) Zeilen aus einer Remotetabelle gelöscht. Geben Sie im Format *server_name* oder *server_name\instance_name* einen gültigen Servernamen für die Datenquelle an.  
  
```  
DELETE FROM OPENDATASOURCE('SQLNCLI',  
    'Data Source= <server_name>; Integrated Security=SSPI')  
    .AdventureWorks2012.HumanResources.Department   
WHERE DepartmentID = 17;'  
```  
  
###  <a name="CaptureResults"></a> Erfassen der Ergebnisse der DELETE-Anweisung  
  
#### <a name="i-using-delete-with-the-output-clause"></a>I. Verwenden von DELETE mit der OUTPUT-Klausel  
 Im folgenden Beispiel wird gezeigt, wie die Ergebnisse einer `DELETE`-Anweisung in einer Tabellenvariablen in der Datenbank [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] gespeichert werden.  
  
```  
DELETE Sales.ShoppingCartItem  
OUTPUT DELETED.*   
WHERE ShoppingCartID = 20621;  
  
--Verify the rows in the table matching the WHERE clause have been deleted.  
SELECT COUNT(*) AS [Rows in Table] 
FROM Sales.ShoppingCartItem 
WHERE ShoppingCartID = 20621;  
GO  
```  
  
#### <a name="j-using-output-with-fromtablename-in-a-delete-statement"></a>J. Verwenden von OUTPUT mit <from_table_name> in einer DELETE-Anweisung  
 Im folgenden Beispiel werden Zeilen in der Tabelle `ProductProductPhoto` aus der Datenbank [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] basierend auf Suchkriterien gelöscht, die in der Klausel `FROM` der Anweisung `DELETE` definiert wurden. Die `OUTPUT` -Klausel gibt die Spalten aus der zu löschenden Tabelle, `DELETED.ProductID`und `DELETED.ProductPhotoID`, sowie Spalten aus der `Product` -Tabelle zurück. Diese werden in der `FROM` -Klausel verwendet, um die zu löschenden Zeilen anzugeben.  
  
```  
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
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Beispiele: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] und [!INCLUDE[ssPDW](../../includes/sspdw-md.md)].  
  
### <a name="k-delete-all-rows-from-a-table"></a>K. Löschen aller Zeilen einer Tabelle  
 Im folgenden Beispiel werden alle Zeilen aus der `Table1`-Tabelle gelöscht, da keine WHERE-Klausel verwendet wird, um die Anzahl der gelöschten Zeilen zu begrenzen.  
  
```  
DELETE FROM Table1;  
```  
  
### <a name="l-delete-a-set-of-rows-from-a-table"></a>L. Löschen einer Reihe von Zeilen einer Tabelle mit DELETE  
 Im folgenden Beispiel werden alle Zeilen aus der Tabelle `Table1` gelöscht, die in der Spalte `StandardCost` einen Wert enthalten, der höher als 1000 ist.  
  
```  
DELETE FROM Table1  
WHERE StandardCost > 1000.00;  
```  
  
### <a name="m-using-label-with-a-delete-statement"></a>M. Verwenden von LABEL mit einer DELETE-Anweisung  
 Im folgenden Beispiel wird eine Bezeichnung mit der Anweisung DELETE verwendet.  
  
```  
DELETE FROM Table1  
OPTION ( LABEL = N'label1' );  
  
```  
  
### <a name="n-using-a-label-and-a-query-hint-with-the-delete-statement"></a>N. Verwenden einer Bezeichnung und eines Abfragehinweises mit der Anweisung DELETE  
 Diese Abfrage zeigt die grundlegende Syntax für die Verwendung eines Join-Abfragehinweises mit der DELETE-Anweisung. Weitere Informationen zu Joinhinweisen und der Verwendung der OPTION-Klausel finden Sie unter [OPTION (SQL Server PDW)](http://msdn.microsoft.com/en-us/72bbce98-305b-42fa-a19f-d89620621ecc).  
  
```  
-- Uses AdventureWorks  
  
DELETE FROM dbo.FactInternetSales  
WHERE ProductKey IN (   
    SELECT T1.ProductKey FROM dbo.DimProduct T1   
    JOIN dbo.DimProductSubcategory T2  
    ON T1.ProductSubcategoryKey = T2.ProductSubcategoryKey  
    WHERE T2.EnglishProductSubcategoryName = 'Road Bikes' )  
OPTION ( LABEL = N'CustomJoin', HASH JOIN ) ;  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)   
 [INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [TRUNCATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/truncate-table-transact-sql.md)   
 [UPDATE (Transact-SQL)](../../t-sql/queries/update-transact-sql.md)   
 [WITH common_table_expression &#40;Transact-SQL&#41;](../../t-sql/queries/with-common-table-expression-transact-sql.md)   
 [@@ROWCOUNT &#40;Transact-SQL&#41;](../../t-sql/functions/rowcount-transact-sql.md)  
  
  


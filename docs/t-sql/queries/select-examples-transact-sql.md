---
title: Beispiele für SELECT (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/16/2017
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
dev_langs:
- TSQL
helpviewer_keywords:
- parentheses [SQL Server]
- GROUP BY clause, SELECT statement
- query hints [SQL Server]
- ALL keyword
- ROLLUP operator
- SELECT statement [SQL Server], examples
- correlated subqueries, SELECT statement
- SELECT INTO statement
- ORDER BY clause [Transact-SQL]
- GROUPING function
- index hints [SQL Server]
- HAVING clause, SELECT statement
- DISTINCT keyword
- CUBE operator
- UNION operator [SQL Server]
- computed sums
- WHERE clause, SELECT statement
ms.assetid: 9b9caa3d-e7d0-42e1-b60b-a5572142186c
caps.latest.revision: 45
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Active
ms.openlocfilehash: 8e800f33fc7c079050ed19a430667098d6666ac4
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="select-examples-transact-sql"></a>SELECT-Beispiele (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  In diesem Thema werden Beispiele für die Verwendung der [SELECT](../../t-sql/queries/select-transact-sql.md)-Anweisung bereitgestellt.  
  
## <a name="a-using-select-to-retrieve-rows-and-columns"></a>A. Verwenden von SELECT zum Abrufen von Zeilen und Spalten  
 Im folgenden Beispiel werden drei Codebeispiele aufgeführt. Im ersten Codebeispiel werden alle Zeilen (es ist keine WHERE-Klausel angegeben) und alle Spalten (mit `*`) aus der `Product`-Tabelle in der [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]-Datenbank zurückgegeben.  
  
 [!code-sql[Select#SelectExamples1](../../t-sql/queries/codesnippet/tsql/select-examples-transact_1.sql)]  
  
 In diesem Beispiel werden alle Zeilen (keine WHERE-Klausel angegeben) und nur eine Teilmenge der Spalten (`Name`, `ProductNumber`, `ListPrice`) aus der `Product`-Tabelle in der [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]-Datenbank zurückgegeben. Außerdem werden Spaltenüberschriften hinzugefügt.  
  
 [!code-sql[Select#SelectExamples2](../../t-sql/queries/codesnippet/tsql/select-examples-transact_2.sql)]  
  
 In diesem Beispiel werden nur die Zeilen für `Product` zurückgegeben, die über die Produktgruppe `R` verfügen und für die die Anzahl von Fertigungstagen weniger als `4` beträgt.  
  
 [!code-sql[Select#SelectExamples3](../../t-sql/queries/codesnippet/tsql/select-examples-transact_3.sql)]  
  
## <a name="b-using-select-with-column-headings-and-calculations"></a>B. Verwenden von SELECT mit Spaltenüberschriften und Berechnungen  
 In diesen Beispielen werden alle Zeilen aus der `Product`-Tabelle zurückgegeben. Im ersten Beispiel werden die Gesamtumsatzzahlen und die Rabatte für jedes Produkt zurückgegeben. Im zweiten Beispiel werden die gesamten Einnahmen für jedes Produkt berechnet.  
  
 [!code-sql[Select#SelectExamples4](../../t-sql/queries/codesnippet/tsql/select-examples-transact_4.sql)]  
  
 Diese Abfrage berechnet die Einnahmen für jedes Produkt in dem jeweiligen Kaufauftrag.  
  
 [!code-sql[Select#SelectExamples5](../../t-sql/queries/codesnippet/tsql/select-examples-transact_5.sql)]  
  
## <a name="c-using-distinct-with-select"></a>C. Verwenden von DISTINCT mit SELECT  
 Im folgenden Beispiel wird `DISTINCT` verwendet, um das Abrufen von doppelten Titeln zu verhindern.  
  
 [!code-sql[Select#SelectExamples6](../../t-sql/queries/codesnippet/tsql/select-examples-transact_6.sql)]  
  
## <a name="d-creating-tables-with-select-into"></a>D. Erstellen von Tabellen mit SELECT INTO  
 Im ersten Beispiel wird eine temporäre Tabelle namens `#Bicycles` in `tempdb` erstellt.  
  
 [!code-sql[Select#SelectExamples7](../../t-sql/queries/codesnippet/tsql/select-examples-transact_7.sql)]  
  
 In diesem zweiten Beispiel wird eine dauerhafte Tabelle namens `NewProducts` erstellt.  
  
 [!code-sql[Select#SelectExamples8](../../t-sql/queries/codesnippet/tsql/select-examples-transact_8.sql)]  
  
## <a name="e-using-correlated-subqueries"></a>E. Verwenden von abhängigen Unterabfragen  
 Im folgenden Beispiel werden Abfragen, die semantisch ähnlich sind, gezeigt und der Unterschied zwischen dem Verwenden des `EXISTS`-Schlüsselworts und des `IN`-Schlüsselworts veranschaulicht. In beiden Fällen handelt es sich um eine gültige Unterabfrage, die eine Instanz von jedem Produktnamen abruft, für den als Produktmodell ein langärmeliges Logo-T-Shirt angegeben ist und für den die `ProductModelID`-Nummern in den `Product`- und `ProductModel`-Tabellen übereinstimmen.  
  
 [!code-sql[Select#SelectExamples9](../../t-sql/queries/codesnippet/tsql/select-examples-transact_9.sql)]  
  
 Im folgenden Beispiel wird `IN` in einer abhängigen oder sich wiederholenden Unterabfrage verwendet. Die Werte dieser Abfrage sind von der äußeren Abfrage abhängig. Die Abfrage wird wiederholt ausgeführt, und zwar einmal für jede Zeile, die von der äußeren Abfrage ausgewählt wird. Diese Abfrage ruft eine Instanz des Vor- und Nachnamens der einzelnen Mitarbeiter ab, für die der Bonus in der `SalesPerson`-Tabelle `5000.00` beträgt und für die die Mitarbeiter-IDs in der `Employee`- und `SalesPerson`-Tabelle übereinstimmen.  
  
 [!code-sql[Select#SelectExamples10](../../t-sql/queries/codesnippet/tsql/select-examples-transact_10.sql)]  
  
 Die vorherige Unterabfrage in dieser Anweisung kann nicht unabhängig von der äußeren Abfrage ausgewertet werden. Sie benötigt einen Wert für `Employee.EmployeeID`, wobei sich dieser Wert jedoch ändert, während [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] unterschiedliche Zeilen in `Employee` untersucht.  
  
 Eine abhängige Unterabfrage kann auch in der `HAVING`-Klausel einer äußeren Abfrage verwendet werden. Mit diesem Beispiel können Sie die Produktmodelle ermitteln, bei denen der maximale Listenpreis mehr als doppelt so hoch ist wie der Durchschnittpreis für das Modell.  
  
 [!code-sql[Select#SelectExamples11](../../t-sql/queries/codesnippet/tsql/select-examples-transact_11.sql)]  
  
 In diesem Beispiel werden zwei abhängige Unterabfragen verwendet, um die Namen von Mitarbeitern zu finden, die ein bestimmtes Produkt verkauft haben.  
  
 [!code-sql[Select#SelectExamples12](../../t-sql/queries/codesnippet/tsql/select-examples-transact_12.sql)]  
  
## <a name="f-using-group-by"></a>F. Verwenden von GROUP BY  
 Im folgenden Beispiel wird die jeweilige Summe der einzelnen Kaufaufträge in der Datenbank ermittelt.  
  
 [!code-sql[Select#SelectExamples13](../../t-sql/queries/codesnippet/tsql/select-examples-transact_13.sql)]  
  
 Wegen der `GROUP BY`-Klausel wird für jede Bestellung nur eine Zeile zurückgegeben, die die Summe aller Kaufaufträge enthält.  
  
## <a name="g-using-group-by-with-multiple-groups"></a>G. Verwenden von GROUP BY mit mehreren Gruppen  
 Dieses Beispiel ermittelt den Durchschnittspreis und die Summe der Jahr-bis-heute-Verkäufe, die nach Produkt-ID und Sonderangebots-ID gruppiert sind:  
  
 [!code-sql[Select#SelectExamples14](../../t-sql/queries/codesnippet/tsql/select-examples-transact_14.sql)]  
  
## <a name="h-using-group-by-and-where"></a>H. Verwenden von GROUP BY und WHERE  
 In diesem Beispiel werden die Ergebnisse in Gruppen zusammengefasst, nachdem nur die Zeilen mit Listenpreisen von mehr als `$1000` abgerufen wurden.  
  
 [!code-sql[Select#SelectExamples15](../../t-sql/queries/codesnippet/tsql/select-examples-transact_15.sql)]  
  
## <a name="i-using-group-by-with-an-expression"></a>I. Verwenden von GROUP BY mit einem Ausdruck  
 Im folgenden Beispiel wird nach einem Ausdruck gruppiert. Sie können nach einem Ausdruck gruppieren, wenn dieser keine Aggregatfunktionen enthält.  
  
 [!code-sql[Select#SelectExamples16](../../t-sql/queries/codesnippet/tsql/select-examples-transact_16.sql)]  
  
## <a name="j-using-group-by-with-order-by"></a>J. Verwenden von GROUP BY mit ORDER BY  
 Im folgenden Beispiel wird zu jedem Produkttyp der Durchschnittspreis ermittelt, nach dem anschließend die Ergebnisse geordnet werden:  
  
 [!code-sql[Select#SelectExamples18](../../t-sql/queries/codesnippet/tsql/select-examples-transact_17.sql)]  
  
## <a name="k-using-the-having-clause"></a>K. Verwenden der HAVING-Klausel  
 Im ersten Beispiel wird eine `HAVING`-Klausel mit einer Aggregatfunktion gezeigt. Sie gruppiert die Zeilen in der `SalesOrderDetail`-Tabelle nach Produkt-ID und entfernt Produkte, deren durchschnittliche Bestellmenge mit 5 oder weniger angegeben ist. Im zweiten Beispiel wird eine `HAVING`-Klausel ohne Aggregatfunktionen gezeigt.  
  
 [!code-sql[Select#SelectExamples19](../../t-sql/queries/codesnippet/tsql/select-examples-transact_18.sql)]  
  
 Diese Abfrage verwendet die `LIKE`-Klausel in der `HAVING`-Klausel.  
  
```  
USE AdventureWorks2012 ;  
GO  
SELECT SalesOrderID, CarrierTrackingNumber   
FROM Sales.SalesOrderDetail  
GROUP BY SalesOrderID, CarrierTrackingNumber  
HAVING CarrierTrackingNumber LIKE '4BD%'  
ORDER BY SalesOrderID ;  
GO  
```  
  
## <a name="l-using-having-and-group-by"></a>L. Verwenden von HAVING und GROUP BY  
 Im folgenden Beispiel wird die Verwendung der Klauseln `GROUP BY`, `HAVING`, `WHERE` und `ORDER BY` in einer `SELECT`-Anweisung gezeigt. Sie erzeugt Gruppen und Summenwerte jedoch erst, nachdem alle Produkte entfernt wurden, deren Preise über 25 $ liegen und für die Bestellmengen unter 5 angegeben sind. Außerdem werden die Ergebnisse nach der `ProductID`-Spalte sortiert.  
  
 [!code-sql[Select#SelectExamples21](../../t-sql/queries/codesnippet/tsql/select-examples-transact_19.sql)]  
  
## <a name="m-using-having-with-sum-and-avg"></a>M. Verwenden von HAVING mit SUM und AVG  
 Im folgenden Beispiel wird die `SalesOrderDetail`-Tabelle nach Produkt-ID gruppiert und nur die Produktgruppen eingeschlossen, für die Bestellungen mit einem Gesamtwert von mehr als `$1000000.00` vorliegen und deren durchschnittliche Bestellmenge mit weniger als `3` angegeben ist.  
  
 [!code-sql[Select#SelectExamples22](../../t-sql/queries/codesnippet/tsql/select-examples-transact_20.sql)]  
  
 Mit der folgenden Abfrage können Sie alle Produkte abfragen, für die Verkäufe im Gesamtwert von über `$2000000.00` verzeichnet wurden:  
  
 [!code-sql[Select#SelectExamples23](../../t-sql/queries/codesnippet/tsql/select-examples-transact_21.sql)]  
  
 Wenn Sie sicherstellen möchten, dass in die Berechnungen zu jedem Produkt mindestens 1.500 Artikel einfließen, entfernen Sie mit `HAVING COUNT(*) > 1500` die Produkte, die Summen mit weniger als `1500` verkauften Artikeln zurückgeben. Die Abfrage lautet folgendermaßen:  
  
 [!code-sql[Select#SelectExamples24](../../t-sql/queries/codesnippet/tsql/select-examples-transact_22.sql)]  
  
## <a name="n-using-the-index-optimizer-hint"></a>N. Verwenden des INDEX-Optimiererhinweises  
 Im folgenden Beispiel werden zwei Möglichkeiten zum Verwenden des `INDEX`-Optimiererhinweises gezeigt. Das erste Beispiel zeigt, wie erzwungen werden kann, dass der Optimierer einen nicht gruppierten Index verwendet, um Zeilen aus einer Tabelle abzurufen. Im zweiten Beispiel wird ein Tabellenscan erzwungen, indem ein Index von 0 verwendet wird.  
  
 [!code-sql[Select#SelectExamples45](../../t-sql/queries/codesnippet/tsql/select-examples-transact_23.sql)]  
  
## <a name="m-using-option-and-the-group-hints"></a>M. Verwenden der OPTION- und GROUP-Hinweise  
 Im folgenden Beispiel wird gezeigt, wie die `OPTION (GROUP)`-Klausel in Verbindung mit einer `GROUP BY`-Klausel verwendet wird.  
  
 [!code-sql[Select#SelectExamples46](../../t-sql/queries/codesnippet/tsql/select-examples-transact_24.sql)]  
  
## <a name="o-using-the-union-query-hint"></a>O. Verwenden des UNION-Abfragehinweises  
 Im folgenden Beispiel wird der `MERGE UNION`-Abfragehinweis verwendet.  
  
 [!code-sql[Select#SelectExamples47](../../t-sql/queries/codesnippet/tsql/select-examples-transact_25.sql)]  
  
## <a name="p-using-a-simple-union"></a>P. Verwenden einer einfachen UNION-Klausel  
 Das Resultset im folgenden Beispiel enthält den Inhalt der Spalten `ProductModelID` und `Name` der Tabellen `ProductModel` und `Gloves`.  
  
 [!code-sql[Select#SelectExamples48](../../t-sql/queries/codesnippet/tsql/select-examples-transact_26.sql)]  
  
## <a name="q-using-select-into-with-union"></a>Q. Verwenden von SELECT INTO mit UNION  
 Im folgenden Beispiel gibt die `INTO`-Klausel in der zweiten `SELECT`-Anweisung an, dass die `ProductResults`-Tabelle das endgültige Resultset der Union der angegebenen Spalten aus den Tabellen `ProductModel` und `Gloves` enthält. Beachten Sie, dass die `Gloves`-Tabelle in der ersten `SELECT`-Anweisung erstellt wird.  
  
 [!code-sql[Select#SelectExamples49](../../t-sql/queries/codesnippet/tsql/select-examples-transact_27.sql)]  
  
## <a name="r-using-union-of-two-select-statements-with-order-by"></a>R. Verwenden von UNION in zwei SELECT-Anweisungen mit ORDER BY  
 Die Reihenfolge bestimmter Parameter, die mit der UNION-Klausel verwendet werden, ist von Bedeutung. Im folgenden Beispiel werden die ordnungsgemäße und die falsche Verwendung von `UNION` in zwei `SELECT`-Anweisungen veranschaulicht, in denen eine Spalte in der Ausgabe umbenannt werden soll.  
  
 [!code-sql[Select#SelectExamples50](../../t-sql/queries/codesnippet/tsql/select-examples-transact_28.sql)]  
  
## <a name="s-using-union-of-three-select-statements-to-show-the-effects-of-all-and-parentheses"></a>S. Verwenden von UNION mit drei SELECT-Anweisungen, wobei die Auswirkung von ALL und Klammern gezeigt wird  
 In den folgenden Beispielen wird `UNION` verwendet, um die Ergebnisse aus drei Tabellen zu kombinieren, wobei in allen Tabellen 5 identische Datenzeilen vorhanden sind. Im ersten Beispiel wird `UNION ALL` verwendet, um doppelte Datensätze anzuzeigen, und alle 15 Zeilen zurückgegeben. Im zweiten Beispiel wird `UNION` ohne `ALL` verwendet, um die doppelten Zeilen aus den kombinierten Ergebnissen der drei `SELECT`-Anweisungen zu löschen, und 5 Zeilen zurückgegeben.  
  
 Im dritten Beispiel wird `ALL` mit dem ersten `UNION` verwendet; das zweite `UNION` verwendet `ALL` nicht und ist in Klammern eingeschlossen. Da die zweite `UNION`-Anweisung in Klammern steht, wird sie zuerst verarbeitet; sie gibt 5 Zeilen zurück, weil die Option `ALL` nicht verwendet wird und Duplikate gelöscht werden. Diese 5 Zeilen werden mit den Ergebnissen der ersten `SELECT`-Anweisung mithilfe der `UNION ALL`-Schlüsselwörter kombiniert. Dabei werden die Duplikate in den beiden aus 5 Zeilen bestehenden Resultsets nicht gelöscht. Das Endergebnis enthält 10 Zeilen.  
  
 [!code-sql[Select#SelectExamples51](../../t-sql/queries/codesnippet/tsql/select-examples-transact_29.sql)]  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)   
 [CREATE VIEW &#40;Transact-SQL&#41;](../../t-sql/statements/create-view-transact-sql.md)   
 [DELETE &#40;Transact-SQL&#41;](../../t-sql/statements/delete-transact-sql.md)   
 [EXECUTE &#40;Transact-SQL&#41;](../../t-sql/language-elements/execute-transact-sql.md)   
 [Ausdrücke &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)   
 [LIKE &#40;Transact-SQL&#41;](../../t-sql/language-elements/like-transact-sql.md)   
 [UNION &#40;Transact-SQL&#41;](../../t-sql/language-elements/set-operators-union-transact-sql.md)   
 [EXCEPT und INTERSECT &#40;Transact-SQL&#41;](../../t-sql/language-elements/set-operators-except-and-intersect-transact-sql.md)   
 [UPDATE (Transact-SQL)](../../t-sql/queries/update-transact-sql.md)   
 [WHERE &#40;Transact-SQL&#41;](../../t-sql/queries/where-transact-sql.md)   
 [PathName &#40;Transact-SQL&#41;](../../relational-databases/system-functions/pathname-transact-sql.md)   
 [INTO-Klausel &#40;Transact-SQL&#41;](../../t-sql/queries/select-into-clause-transact-sql.md)  
  
  

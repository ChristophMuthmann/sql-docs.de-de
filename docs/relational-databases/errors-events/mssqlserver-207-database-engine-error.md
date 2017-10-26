---
title: MSSQLSERVER_207 | Microsoft-Dokumentation
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 207 (Database Engine error)
ms.assetid: d1ab00c7-0331-437a-84fe-bae53b82feec
caps.latest.revision: 17
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: ba320288a06dd8498d9699712a6e53e34ae93c09
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="mssqlserver207"></a>MSSQLSERVER_207
  
## <a name="details"></a>Details  
  
|||  
|-|-|  
|Produktname|SQL Server|  
|Ereignis-ID|207|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|SQLEngine|  
|Symbolischer Name|SQ_BADCOL|  
|Meldungstext|Ungültiger Spaltenname '%.*ls'.|  
  
## <a name="explanation"></a>Erklärung  
Dieser Abfragefehler kann durch eines der folgenden Probleme verursacht werden.  
  
-   Der Spaltenname ist falsch geschrieben, oder die Spalte ist in keiner der angegebenen Tabellen vorhanden.  
  
-   Bei der Sortierung der Datenbank wird nach Groß-/Kleinschreibung unterschieden, und die in der Abfrage angegebene Schreibweise entspricht nicht der Schreibweise, die in der Tabelle für die Spalte definiert ist. Wenn eine Spalte z.B. als **LastName** angegeben ist und die Datenbank eine Sortierung verwendet, die nach Groß-/Kleinschreibung unterscheidet, geben Abfragen, die auf die Spalte als **Lastname** oder **lastname** verweisen, den Fehler 207 zurück, da der Spaltenname nicht übereinstimmt.  
  
-   Auf einen in der SELECT-Klausel definierten Spaltenalias wird in einer anderen Klausel, beispielsweise WHERE oder GROUP BY, verwiesen. Beispielsweise wird in der folgenden Abfrage der Spaltenalias `Year` in der SELECT-Klausel definiert, und in der GROUP BY-Klausel wird auf diesen verwiesen.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    SELECT DATEPART(yyyy,OrderDate) AS Year, SUM(TotalDue) AS Total  
    FROM Sales.SalesOrderHeader  
    GROUP BY Year;  
    ```  
  
    Aufgrund der Reihenfolge, in der die Abfrageklauseln verarbeitet werden, wird in diesem Beispiel der Fehler 207 zurückgegeben. Die Verarbeitungsreihenfolge ist die Folgende:  
  
    1.  FROM  
  
    2.  ON  
  
    3.  JOIN  
  
    4.  WHERE  
  
    5.  GROUP BY  
  
    6.  WITH CUBE oder WITH ROLLUP  
  
    7.  HAVING  
  
    8.  SELECT  
  
    9. DISTINCT  
  
    10. ORDER BY  
  
    11. NACH OBEN  
  
    Da vor dem Verarbeiten der SELECT-Klausel kein Spaltenalias definiert wird, ist der Aliasname beim Verarbeiten der GROUP BY-Klausel unbekannt.  
  
-   Die MERGE-Anweisung löst diesen Fehler aus, wenn die *<merge_matched>*-Klausel auf Spalten in der Quelltabelle verweist, jedoch von der Quelltabelle in der WHEN NOT MATCHED BY SOURCE-Klausel keine Zeilen zurückgegeben werden. Dieser Fehler tritt auf, da auf die Spalten in der Quelltabelle nicht zugegriffen werden kann, wenn in der Abfrage keine Zeilen zurückgegeben werden. Die Klausel `WHEN NOT MATCHED BY SOURCE THEN UPDATE SET TargetTable.Col1 = SourceTable.Col1` kann beispielsweise dazu führen, dass die Anweisung fehlschlägt, wenn der Zugriff auf `Col1` in der Quelltabelle nicht möglich ist.  
  
## <a name="user-action"></a>Benutzeraktion  
Überprüfen Sie die folgenden Informationen, und korrigieren Sie die Anweisung entsprechend.  
  
-   Der Spaltenname ist in der Tabelle vorhanden und korrekt geschrieben. Im folgenden Beispiel wird die **sys.columns**-Katalogsicht abgefragt, um alle Spaltennamen der angegebenen Tabelle zurückzugeben.  
  
    ```  
    SELECT name FROM sys.columns WHERE object_id = OBJECT_ID('schema_name.table_name');  
    ```  
  
-   Die Unterscheidung nach Groß-/Kleinschreibung der Datenbanksortierung. Mit der folgenden Anweisung wird die Sortierung der angegebenen Datenbank zurückgegeben.  
  
    ```  
    SELECT collation_name FROM sys.databases WHERE name = 'database_name';  
    ```  
  
    Die Abkürzung CS im Sortierungsnamen gibt an, dass bei der Sortierung nach Groß-/Kleinschreibung unterschieden wird. Beispiel: Latin1_General_CS_AS ist eine Sortierung, bei der nach Groß-/Kleinschreibung und nach Akzent unterschieden wird. Ändern Sie den Spaltennamen zu der in der Tabelle definierten Schreibweise des Spaltennamens.  
  
-   Ein Verweis auf einen Spaltenalias ist ungültig. Ändern Sie die Anweisung, indem Sie den Ausdruck wiederholen, mit dem der Alias in der entsprechenden Klausel definiert wird, oder indem Sie eine abgeleitete Tabelle verwenden. Im folgenden Beispiel werden die Ausdrücke wiederholt, mit denen in der GROUP BY-Klausel der Alias `Year` definiert wird.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    SELECT DATEPART(yyyy,OrderDate) AS Year ,SUM(TotalDue) AS Total  
    FROM Sales.SalesOrderHeader  
    GROUP BY DATEPART(yyyy,OrderDate);  
    ```  
  
    Im folgenden Beispiel wird eine abgeleitete Tabelle verwendet, um den Aliasnamen für andere Klauseln in der Abfrage verfügbar zu machen. Beachten Sie, dass der Alias `Year` in der FROM-Klausel definiert wird, die zuerst verarbeitet wird. Dadurch ist der Alias für die Verwendung in anderen Klauseln der Abfrage verfügbar.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    SELECT d.Year, SUM(TotalDue) AS Total  
    FROM (SELECT DATEPART(yyyy,OrderDate) AS Year, TotalDue  
          FROM Sales.SalesOrderHeader)AS d  
    GROUP BY Year;  
    ```  
  
-   Die WHEN NOT MATCHED BY SOURCE-Klausel in der MERGE-Anweisung verweist auf einen Wert, auf den zugegriffen werden kann. Ändern Sie die MERGE-Anweisung so, dass die Quelltabelle in der WHEN NOT MATCHED BY SOURCE-Klausel mindestens eine Zeile zurückgibt. Möglicherweise müssen Sie z. B. die für die Klausel angegebene Suchbedingung hinzufügen oder überarbeiten. Wahlweise können Sie die Klausel so ändern, dass diese einen Wert angibt, der nicht auf die Quelltabelle verweist. Beispiel: `WHEN NOT MATCHED BY SOURCE THEN UPDATE SET TargetTable.Col1 = <expression, or other available value>`.  
  
## <a name="see-also"></a>Siehe auch  
[MERGE &#40;Transact-SQL&#41;](~/t-sql/statements/merge-transact-sql.md)  
[FROM &#40;Transact-SQL&#41;](~/t-sql/queries/from-transact-sql.md)  
[SELECT &#40;Transact-SQL&#41;](~/t-sql/queries/select-transact-sql.md)  
[UPDATE &#40;Transact-SQL&#41;](~/t-sql/queries/update-transact-sql.md)  
  


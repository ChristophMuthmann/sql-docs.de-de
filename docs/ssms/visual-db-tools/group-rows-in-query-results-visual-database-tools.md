---
title: Gruppieren von Zeilen in Abfrageergebnissen (Visual Database Tools) | Microsoft-Dokumentation
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- summarizing table subsets
- grouping rows
- grouping query results
ms.assetid: b07082d5-4d55-4903-9af9-4c470554c6d3
caps.latest.revision: "5"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a879bdc95cda0812fcc7d3f43f4d7e99c183337f
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="group-rows-in-query-results-visual-database-tools"></a>Gruppieren von Zeilen in Abfrageergebnissen (Visual Database Tools)
Zum Bilden von Teilergebnissen oder zum Anzeigen weiterer Kurzinformationen für Teilbereiche einer Tabelle erstellen Sie Gruppen mithilfe einer Aggregatabfrage. In jeder Gruppe werden die Daten aus allen Zeilen der Tabelle mit demselben Wert zusammengefasst.  
  
Angenommen, Sie möchten den durchschnittlichen Preis für ein Buch in der Tabelle `titles` anzeigen lassen, wobei die Ergebnisse nach Herausgeber aufgeteilt werden sollen. Dazu gruppieren Sie die Abfrage nach Herausgeber (z. B. `pub_id`). Hierfür kann folgende Abfrageausgabe formuliert werden:  
  
![Abfrageergebnisse: Durchschnittspreis gruppiert nach Verleger](../../ssms/visual-db-tools/media/dv3w9e1.gif "Query results: average price grouped by publisher")  
  
Beim Gruppieren von Daten können nur Daten aus Zusammenfassungen bzw. gruppierte Daten angezeigt werden, z. B.:  
  
-   Die Werte der gruppierten Spalten (die in der GROUP BY-Klausel auftreten). Im oben angeführten Beispiel ist `pub_id` die gruppierte Spalte.  
  
-   Die Werte, die von Aggregatfunktionen wie SUM( ) und AVG( ) erzeugt werden. Im oben aufgeführten Beispiel wird die zweite Spalte erstellt, indem die Funktion AVG( ) auf die Spalte `price` angewendet wird.  
  
Werte aus einzelnen Zeilen können nicht angezeigt werden. Wenn Sie z. B. nur nach Herausgeber gruppieren, können nicht gleichzeitig die einzelnen Titel in der Abfrage angezeigt werden. Wenn Sie daher dem Abfrageergebnis Spalten hinzufügen, fügt der [Abfrage- und Sicht-Designer](../../ssms/visual-db-tools/query-and-view-designer-tools-visual-database-tools.md) diese automatisch der GROUP BY-Klausel der Anweisung im [SQL-Bereich](../../ssms/visual-db-tools/sql-pane-visual-database-tools.md)hinzu. Wenn eine Spalte stattdessen aggregiert werden soll, können Sie für diese Spalte eine Aggregatfunktion angeben.  
  
Wenn Sie nach mehreren Spalten gruppieren, werden von jeder Gruppe der Abfrage die Aggregatwerte für alle Gruppenspalten angezeigt.  
  
In der folgenden Abfrage für die Tabelle `titles` sind die Zeilen beispielsweise sowohl nach Herausgeber (`pub_id`) als auch nach Buchtyp (`type`) gruppiert. Die Abfrageergebnisse sind nach Herausgeber geordnet und zeigen für jeden Buchtyp des jeweiligen Herausgebers Kurzinformationen an:  
  
```  
SELECT pub_id, type, SUM(price) Total_price  
FROM titles  
GROUP BY pub_id, type  
```  
  
Die entsprechende Ausgabe könnte folgendermaßen aussehen:  
  
![Abfrageergebnisse: Preis gruppiert nach Verleger und Typ](../../ssms/visual-db-tools/media/dv3w9e2.gif "Query results: price grouped by publisher and type")  
  
### <a name="to-group-rows"></a>So gruppieren Sie Zeilen  
  
1.  Starten Sie die Abfrage, indem Sie dem Diagrammbereich die Tabellen hinzufügen, die zusammengefasst werden sollen.  
  
2.  Klicken Sie mit der rechten Maustaste auf den Hintergrund des Diagrammbereichs, und wählen Sie im Kontextmenü die Option **Gruppe hinzufügen nach** aus. Der Abfrage- und Sicht-Designer fügt dem Datenblatt im Kriterienbereich die Spalte **Gruppieren nach** hinzu.  
  
3.  Fügen Sie dem Kriterienbereich die Spalte(n) hinzu, die gruppiert werden soll(en). Wenn die Spalte im Abfrageergebnis aufgeführt werden soll, muss die Spalte **Ausgabe** für die Ausgabe aktiviert sein.  
  
    Der Abfrage- und Sicht-Designer fügt der Anweisung im SQL-Bereich eine GROUP BY-Klausel hinzu. Die SQL-Anweisung könnte z. B. folgendermaßen aussehen:  
  
    ```  
    SELECT pub_id  
    FROM titles  
    GROUP BY pub_id  
    ```  
  
4.  Fügen Sie dem Kriterienbereich die Spalte(n) hinzu, die aggregiert werden soll(en). Vergewissern Sie sich, dass die Spalte für die Ausgabe ausgewählt ist.  
  
5.  Wählen Sie in der Datenblattzelle **Gruppieren nach** der zu aggregierenden Spalte die entsprechende Aggregatfunktion aus.  
  
    Der Abfrage- und Sicht-Designer weist der Spalte, die zusammengefasst wird, automatisch einen Spaltenalias zu. Sie können diesen automatisch generierten durch einen aussagekräftigeren Alias ersetzen. Weitere Informationen finden Sie unter [Erstellen von Spaltenaliasen (Visual Database Tools)](../../ssms/visual-db-tools/create-column-aliases-visual-database-tools.md).  
  
    ![Hinzufügen eines Spaltenalias zum Abfrageresultset](../../ssms/visual-db-tools/media/dv3w9e3.gif "Adding a column alias to the query result set")  
  
    Die entsprechende Anweisung im Bereich **SQL** könnte folgendermaßen aussehen:  
  
    ```  
    SELECT   pub_id, SUM(price) AS Totalprice  
    FROM     titles  
    GROUP BY pub_id  
    ```  
  
## <a name="see-also"></a>Siehe auch  
[Sortieren und Gruppieren von Abfrageergebnissen (Visual Database Tools)](../../ssms/visual-db-tools/sort-and-group-query-results-visual-database-tools.md)  
  

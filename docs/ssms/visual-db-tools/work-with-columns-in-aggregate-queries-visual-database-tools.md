---
title: Verwenden von Spalten in Aggregatabfragen (Visual Database Tools) | Microsoft-Dokumentation
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- HAVING clause, query summary results
- GROUP BY clause, query summary results
- aggregate queries [SQL Server]
- WHERE clause, query summary results
ms.assetid: 1b82681f-3d4f-4b9a-bb1d-2060e44f2577
caps.latest.revision: 3
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 64aee66141249bc2a1848f6a65ec9683c73dc429
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="work-with-columns-in-aggregate-queries-visual-database-tools"></a>Verwenden von Spalten in Aggregatabfragen (Visual Database Tools)
Wenn Sie Aggregatabfragen erstellen, geht der [Abfrage- und Sicht-Designer](../../ssms/visual-db-tools/query-and-view-designer-tools-visual-database-tools.md) von bestimmten Annahmen aus, sodass eine gültige Abfrage konstruiert werden kann. Wenn Sie z. B. eine Aggregatabfrage erstellen und eine Datenspalte für die Ausgabe kennzeichnen, nimmt der Abfrage- und Sicht-Designer die Spalte automatisch in die GROUP BY-Klausel auf und verhindert so, dass der Inhalt einer einzelnen Zeile in einer Zusammenfassung angezeigt werden kann.  
  
## <a name="using-group-by"></a>Verwenden von Gruppieren nach  
Der Abfrage- und Sicht-Designer greift beim Arbeiten mit Spalten auf folgende Richtlinien zurück:  
  
-   Wenn Sie die Option Gruppieren nach auswählen oder einer Abfrage eine Aggregatfunktion hinzufügen, werden alle für die Ausgabe gekennzeichneten oder in Sortiervorgängen verwendeten Spalten automatisch in die GROUP BY-Klausel aufgenommen. Spalten werden nicht automatisch in die GROUP BY-Klausel aufgenommen, wenn sie bereits Teil einer Aggregatfunktion sind.  
  
    Wenn Sie eine bestimmte Spalte aus der GROUP BY-Klausel herausnehmen möchten, müssen Sie im Kriterienbereich in der Spalte Gruppieren nach manuell eine andere Option auswählen. Der Abfrage- und Sicht-Designer prüft hierbei jedoch nicht, ob die Abfrage mit der von Ihnen ausgewählten Option nach wie vor ausgeführt werden kann.  
  
-   Wenn Sie einer Aggregatfunktion im Kriterien- oder SQL-Bereich manuell eine Ausgabespalte für die Abfrage hinzufügen, entfernt der Abfrage- und Sicht-Designer andere Ausgabespalten nicht automatisch aus der Abfrage. Sie müssen die verbleibenden Spalten daher manuell aus der Abfrageausgabe entfernen oder sie in die GROUP BY-Klausel einer Aggregatfunktion aufnehmen.  
  
Wenn Sie eine Suchbedingung im Kriterienbereich in die Spalte Filter eingeben, folgt der Abfrage- und Sicht-Designer bestimmten Regeln:  
  
-   Wenn die Spalte **Gruppieren nach** des Datenblatts nicht angezeigt wird (weil Sie die Abfrage noch nicht als Aggregatabfrage definiert haben), wird die Suchbedingung in der WHERE-Klausel platziert.  
  
-   Wenn Sie bereits in einer Aggregatabfrage arbeiten und in der Spalte **Gruppieren nach** die Option **Ort** ausgewählt haben, wird die Suchbedingung in der WHERE-Klausel platziert.  
  
-   Wenn die Spalte **Gruppieren nach** einen anderen Wert als **Ort**enthält, wird die Suchbedingung in der HAVING-Klausel platziert.  
  
## <a name="using-the-having-and-where-clauses"></a>Verwenden der HAVING- und WHERE-Klauseln  
Die folgenden Prinzipien beschreiben, wie Sie in einer Aggregatabfrage beim Festlegen von Suchbedingungen auf Spalten verweisen können. Im Allgemeinen können Sie eine Spalte in einer Suchbedingung verwenden, um die zusammengefassten Zeilen zu filtern (WHERE-Klausel) oder um zu bestimmen, welche gruppierten Ergebnisse in der endgültigen Ausgabe angezeigt werden sollen (HAVING-Klausel).  
  
-   Einzelne Datenspalten können entweder in der WHERE- oder in der HAVING-Klausel angegeben werden. Dies hängt davon ab, wie die Spalten an anderer Stelle in der Abfrage verwendet wurden.  
  
-   WHERE-Klauseln dienen zum Auswählen einer Teilmenge der Zeilen für die Zusammenfassung und Gruppierung. Sie werden daher angewendet, bevor Gruppierungsvorgänge ausgeführt werden. Aus diesem Grund können Sie eine Datenspalte auch dann in einer WHERE-Klausel verwenden, wenn sie nicht in der GROUP BY-Klausel oder in einer Aggregatfunktion enthalten ist. Beispielsweise gibt die folgende Anweisung alle Titel mit einem Preis über $10,00 zurück und berechnet den Durchschnittspreis:  
  
    ```  
    SELECT AVG(price)  
    FROM titles  
    WHERE price > 10  
    ```  
  
-   Wenn Sie beim Erstellen einer Suchbedingung eine Spalte verwenden, die ebenfalls Bestandteil einer GROUP BY-Klausel oder Aggregatfunktion ist, kann die Suchbedingung entweder als WHERE- oder als HAVING-Klausel eingebunden werden. Sie können dies entscheiden, sobald Sie die Bedingung erstellen. Die folgende Anweisung erstellt z. B. einen Durchschnittspreis aller Bücher für jeden Herausgeber und zeigt anschließend den Mittelwert derjenigen Herausgeber an, bei denen der Durchschnittspreis über 10,00 $ liegt:  
  
    ```  
    SELECT pub_id, AVG(price)  
    FROM titles  
    GROUP BY pub_id  
    HAVING (AVG(price) > 10)  
    ```  
  
-   Wenn Sie eine Aggregatfunktion in einer Suchbedingung verwenden, beinhaltet die Bedingung eine Zusammenfassung und muss somit Teil der HAVING-Klausel sein.  
  
## <a name="see-also"></a>Siehe auch  
[Zusammenfassen von Abfrageergebnissen &amp;#40;Visual Database Tools&amp;#41;](../../ssms/visual-db-tools/summarize-query-results-visual-database-tools.md)  
[Sortieren und Gruppieren von Abfrageergebnissen &amp;#40;Visual Database Tools&amp;#41;](../../ssms/visual-db-tools/sort-and-group-query-results-visual-database-tools.md)  
  


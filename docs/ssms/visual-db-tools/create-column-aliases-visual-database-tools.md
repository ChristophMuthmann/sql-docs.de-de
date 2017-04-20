---
title: Erstellen von Spaltenaliasen (Visual Database Tools) | Microsoft-Dokumentation
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
- columns [SQL Server], aliases
- aliases [SQL Server], columns
ms.assetid: e2e1c166-8ea7-47a2-b6a7-e419bf0fa3bb
caps.latest.revision: 3
author: stevestein
ms.author: sstein
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: bbbf69c55fcd0225583c43b3b4ae4089cc2f40ea
ms.lasthandoff: 04/11/2017

---
# <a name="create-column-aliases-visual-database-tools"></a>Erstellen von Spaltenaliasen (Visual Database Tools)
Zur Arbeitserleichterung können Sie Aliase für Spaltennamen, Berechnungen und zusammengefasste Werte erstellen. Beispielsweise können Sie einen Spaltenalias mit folgenden Funktionen erstellen:  
  
-   Erstellen eines Spaltennamens, z. B. "Total Amount" für einen Ausdruck wie `(quantity * unit_price)` oder für eine Aggregatfunktion.  
  
-   Erstellen einer Kurzform für einen Spaltennamen, z. B. `"d_id"` für `"discounts.stor_id."`  
  
Wenn Sie einen Spaltenalias definiert haben, können Sie den Alias in einer SELECT-Abfrage zum Angeben der Ausgabe der Abfrageergebnisse verwenden.  
  
### <a name="to-create-a-column-alias"></a>So erstellen Sie einen Spaltenalias  
  
1.  Suchen Sie im Bereich **Kriterien**die Zeile mit der Datenspalte, für die Sie einen Alias erstellen möchten, und markieren Sie diese ggf. für die Ausgabe. Wenn die Datenspalte noch nicht im Datenblatt vorhanden ist, fügen Sie sie hinzu.  
  
2.  Geben Sie in der zu dieser Zeile gehörigen Spalte **Alias** den Alias ein. Der Alias muss allen Namenskonventionen für SQL entsprechen. Wenn der eingegebene Aliasname Leerzeichen enthält, wird er vom Abfrage- und Sicht-Designer automatisch in Trennzeichen eingeschlossen.  
  
## <a name="see-also"></a>Siehe auch  
[Hinzufügen von Spalten zu Abfragen &amp;#40;Visual Database Tools&amp;#41;](../../ssms/visual-db-tools/add-columns-to-queries-visual-database-tools.md)  
[Sortieren und Gruppieren von Abfrageergebnissen &amp;#40;Visual Database Tools&amp;#41;](../../ssms/visual-db-tools/sort-and-group-query-results-visual-database-tools.md)  
[Zusammenfassen von Abfrageergebnissen &amp;#40;Visual Database Tools&amp;#41;](../../ssms/visual-db-tools/summarize-query-results-visual-database-tools.md)  
[Ausführen grundlegender Vorgänge mit Abfragen &amp;#40;Visual Database Tools&amp;#41;](../../ssms/visual-db-tools/perform-basic-operations-with-queries-visual-database-tools.md)  
  


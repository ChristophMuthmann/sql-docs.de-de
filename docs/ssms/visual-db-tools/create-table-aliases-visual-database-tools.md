---
title: Erstellen von Tabellenaliasen (Visual Database Tools) | Microsoft-Dokumentation
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
- table aliases [SQL Server]
- aliases [SQL Server], tables
ms.assetid: 49e61e85-8abf-4ca7-8c70-7e9f8f1078bd
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: d76ede0538ac5fb723e35fb32f045f3b14cd86ca
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="create-table-aliases-visual-database-tools"></a>Erstellen von Tabellenaliasen (Visual Database Tools)
Aliase können das Arbeiten mit Tabellennamen erleichtern. Das Verwenden von Aliasen ist in folgenden Fällen hilfreich:  
  
-   Sie möchten die Anweisung im [SQL-Bereich](../../ssms/visual-db-tools/sql-pane-visual-database-tools.md) kürzen und lesbarer machen.  
  
-   Sie verweisen in der Abfrage häufig auf den Tabellennamen, z. B. in qualifizierenden Spaltennamen, und möchten sicherstellen, dass in der Abfrage eine bestimmte Anzahl von Zeichen nicht überschritten wird. (In einigen Datenbanken ist eine maximale Länge für Abfragen festgelegt.)  
  
-   Sie verwenden mehrere Instanzen derselben Tabelle (z. B. in einem Selbstjoin) und suchen nach einer Möglichkeit, um auf die eine oder andere Instanz zu verweisen.  
  
Sie können z. B. einen Alias `"e"` für einen Tabellennamen `employee`_`information`erstellen und in der restlichen Abfrage mit `"e"` auf die Tabelle verweisen.  
  
### <a name="to-create-an-alias-for-a-table-or-table-valued-object"></a>So erstellen Sie einen Alias für eine Tabelle oder ein Tabellenwertobjekt  
  
1.  Fügen Sie der Abfrage die Tabelle oder das Tabellenwertobjekt hinzu.  
  
2.  Klicken Sie im **Diagrammbereich**mit der rechten Maustaste auf das Objekt, für das Sie einen Alias erstellen möchten, und wählen Sie anschließend im Kontextmenü **Eigenschaften** aus.  
  
3.  Geben Sie im **Eigenschaftenfenster** den Alias in das Feld **Alias** ein.  
  
## <a name="see-also"></a>Siehe auch  
[Hinzufügen von Tabellen zu Abfragen &amp;#40;Visual Database Tools&amp;#41;](../../ssms/visual-db-tools/add-tables-to-queries-visual-database-tools.md)  
[Sortieren und Gruppieren von Abfrageergebnissen &amp;#40;Visual Database Tools&amp;#41;](../../ssms/visual-db-tools/sort-and-group-query-results-visual-database-tools.md)  
[Zusammenfassen von Abfrageergebnissen &amp;#40;Visual Database Tools&amp;#41;](../../ssms/visual-db-tools/summarize-query-results-visual-database-tools.md)  
[Ausführen grundlegender Vorgänge mit Abfragen &amp;#40;Visual Database Tools&amp;#41;](../../ssms/visual-db-tools/perform-basic-operations-with-queries-visual-database-tools.md)  
  


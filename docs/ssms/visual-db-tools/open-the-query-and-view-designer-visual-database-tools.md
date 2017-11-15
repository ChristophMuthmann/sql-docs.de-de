---
title: "Öffnen des Abfrage- und Sicht-Designers (Visual Database Tools) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- opening View Designer
- View Designer, opening
- Query Designer [SQL Server], opening
- opening Query Designer
ms.assetid: b473f258-d53c-41c0-9ad9-528a2ff141f4
caps.latest.revision: "4"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: a884c10eb96fbab9a9202427643cb3d1262e6477
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="open-the-query-and-view-designer-visual-database-tools"></a>Öffnen des Abfrage- und Sicht-Designers (Visual Database Tools)
Der Abfrage- und Sicht-Designer wird automatisch geöffnet, wenn Sie die Definition einer Sicht öffnen, die Ergebnisse für eine Abfrage oder Sicht anzeigen bzw. eine Abfrage erstellen oder öffnen. Er besteht aus vier separaten Bereichen:  
  
-   Der Diagrammbereich liefert eine grafische Darstellung der Tabellen bzw. Tabellenwertobjekte, die Sie aus der Datenverbindung ausgewählt haben. Weiterhin werden alle Joinbeziehungen zwischen ihnen angezeigt.  
  
-   Im Kriterienbereich können Sie Abfrageoptionen angeben, d. h. welche Datenspalten angezeigt oder wie die Ergebnisse sortiert werden und welche Zeilen ausgewählt werden sollen. Hierzu geben Sie die gewünschten Optionen in einem Datenblatt ähnlich einer Kalkulationstabelle ein.  
  
-   Sie können den SQL-Bereich verwenden, um eine eigene SQL-Anweisung zu erstellen. Sie können auch den Kriterienbereich und den Diagrammbereich verwenden, um die Anweisung zu erstellen, wobei dadurch die SQL-Anweisungen im SQL-Bereich erstellt werden. Beim Erstellen einer Abfrage wird der SQL-Bereich automatisch aktualisiert und zur besseren Lesbarkeit neu formatiert.  
  
-   Im Ergebnisbereich werden die Ergebnisse der zuletzt ausgeführten SELECT-Abfrage angezeigt. (Die Ergebnisse anderer Abfragetypen werden in Meldungsfeldern angezeigt.)  
  
-   Diese Bereiche sind sowohl beim Verwenden von Abfragen als auch beim Verwenden von Sichten nützlich.  
  
-   Beim Öffnen einer Sicht oder Abfrage werden gleichzeitig einige oder alle Bereiche geöffnet. Welche Bereiche geöffnet werden, hängt von den Einstellungen im Dialogfeld **Optionen** und von dem Datenbankmanagementsystem ab, mit dem Sie verbunden sind. Standardmäßig werden alle vier Bereiche geöffnet.  
  
### <a name="to-open-the-query-and-view-designer-for-a-view"></a>So öffnen Sie den Abfrage- und Sicht-Designer für eine Sicht  
  
1.  Klicken Sie im Objekt-Explorer mit der rechten Maustaste auf die Sicht, die Sie öffnen möchten, und klicken Sie dann auf **Entwerfen** oder **Sicht öffnen**.  
  
    Wenn Sie **Entwerfen**auswählen, werden die Bereiche des Abfrage- und Sicht-Designers entsprechend den Einstellungen im Dialogfeld **Optionen** geöffnet. Wenn Sie **Sicht öffnen**auswählen, wird standardmäßig nur der Ergebnisbereich geöffnet.  
  
### <a name="to-open-the-query-and-view-designer-for-an-existing-query"></a>So öffnen Sie den Abfrage- und Sicht-Designer für eine vorhandene Abfrage  
  
1.  Erweitern Sie im Projektmappen-Explorer den Ordner **Abfragen** .  
  
2.  Doppelklicken Sie auf die Abfrage, die Sie öffnen möchten.  
  
3.  Markieren Sie die Abfrageanweisung(en), klicken Sie mit der rechten Maustaste auf den markierten Bereich, und klicken Sie auf **Abfrage in Editor entwerfen**.  
  
## <a name="see-also"></a>Siehe auch  
[Themen zur Vorgehensweise: Entwerfen von Abfragen und Sichten &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
[Tools im Abfrage- und Sicht-Designer &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/query-and-view-designer-tools-visual-database-tools.md)  
  

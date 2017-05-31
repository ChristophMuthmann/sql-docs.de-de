---
title: "Hinzufügen neuer Zeilen im Ergebnisbereich (Visual Database Tools) | Microsoft-Dokumentation"
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
- View Designer, Results pane
- inserting rows
- Query Designer [SQL Server], Results pane
- Results pane
- adding rows
- row additions [SQL Server], Results pane
ms.assetid: 59891c84-3f54-4ab9-8b86-72c59627b480
caps.latest.revision: 3
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 0ba11f05536a52023c382e040738b8d9f9a4a215
ms.contentlocale: de-de
ms.lasthandoff: 04/11/2017

---
# <a name="add-new-rows-in-the-results-pane-visual-database-tools"></a>Hinzufügen neuer Zeilen im Ergebnisbereich (Visual Database Tools)
Sie können neue Daten hinzufügen, indem Sie sie eintippen oder aus einem anderen Programm, z. B. Editor oder Excel, einfügen. Eine einzufügende Zeile muss genau dieselbe Anzahl und denselben Typ von Spalten wie die Tabelle aufweisen, in die Sie die Zeile einfügen. Sie können mehrere Zeilen gleichzeitig in den Ergebnisbereich einfügen.  
  
Informationen zum Eingeben von Daten finden Sie unter [Regeln zum Aktualisieren von Ergebnissen &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/rules-for-updating-results-visual-database-tools.md).  
  
### <a name="to-add-a-new-data-row"></a>So fügen Sie eine neue Datenzeile ein  
  
1.  Wechseln Sie in den unteren Teil des Ergebnisbereichs, in dem eine leere Zeile für das Hinzufügen einer neuen Datenzeile verfügbar ist.  
  
    Die Anfangswerte aller Spalten sind *NULL*.  
  
    > [!TIP]  
    > Um sofort zur ersten Leerzeile zu wechseln, benutzen Sie die Navigationsleiste am unteren Rand des Ergebnisbereichs.  
  
2.  Wenn Sie Zeilen aus der Zwischenablage einfügen, markieren Sie die neue Zeile, indem Sie auf die Schaltfläche auf der linken Seite klicken.  
  
    > [!NOTE]  
    > Wenn eine oder mehrere der eingefügten Zeilen nicht in die Datenbank eingetragen werden können, wird eine Meldung ausgegeben, die darüber Auskunft gibt, welche Zeile(n) nicht eingetragen werden konnte(n).  
  
3.  Geben Sie die Daten für die neue Zeile ein. Beim Einfügen aus der Zwischenablage wählen Sie im Menü **Bearbeiten** die Option **Einfügen** aus.  
  
4.  Bewegen Sie den Zeiger aus der Zeile heraus, damit sie in die Datenbank eingetragen wird.  
  
Falls beim Speichern der Zeile ein Fehler auftritt, zeigt der Abfrage- und Sicht-Designer eine Meldung an und setzt den Zeiger in die Zeile, die Sie in Bearbeitung hatten. Sie können anschließend folgende Aktionen durchführen:  
  
-   Auflösen des Fehlers durch weitere Bearbeitungen der Zeile.  
  
-   Abbrechen der Bearbeitung durch Drücken von ESC. Wenn Sie sich beim Drücken von ESC in einer geänderten Zelle befinden, werden die Änderungen an dieser Zelle abgebrochen. Befinden Sie sich beim Drücken von ESC in einer nicht geänderten Zelle, werden die Änderungen für die gesamte Zeile verworfen.  
  
## <a name="see-also"></a>Siehe auch  
[Verwenden von Daten im Ergebnisbereich &amp;#40;Visual Database Tools&amp;#41;](../../ssms/visual-db-tools/work-with-data-in-the-results-pane-visual-database-tools.md)  
[Ausführen grundlegender Vorgänge mit Abfragen &amp;#40;Visual Database Tools&amp;#41;](../../ssms/visual-db-tools/perform-basic-operations-with-queries-visual-database-tools.md)  
  


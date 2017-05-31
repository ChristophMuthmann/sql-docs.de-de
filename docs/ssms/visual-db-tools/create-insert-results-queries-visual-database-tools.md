---
title: "Erstellen von Abfragen zum Einfügen von Ergebnissen (Visual Database Tools) | Microsoft-Dokumentation"
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
- queries [SQL Server], types
- result sets [SQL Server], queries
- results [SQL Server], query
- Insert Results query
- queries [SQL Server], results
ms.assetid: 8770d630-09cc-47ec-a0e9-e9de2d7bbc89
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: ef3e0b90a01079e974ed687656bf51448abcc66d
ms.contentlocale: de-de
ms.lasthandoff: 04/11/2017

---
# <a name="create-insert-results-queries-visual-database-tools"></a>Erstellen von Abfragen zum Einfügen von Ergebnissen (Visual Database Tools)
Mit einer Abfrage zum Einfügen von Ergebnissen können Sie Zeilen aus einer Tabelle in eine andere oder innerhalb einer Tabelle kopieren. Aus der Tabelle `titles` können Sie beispielsweise mit einer Abfrage zum Einfügen von Ergebnissen Informationen über alle Titel eines Herausgebers in eine zweite Tabelle kopieren, die dem betreffenden Herausgeber zur Verfügung gestellt werden kann. Das Erstellen einer Abfrage zum Einfügen von Ergebnissen ähnelt dem Erstellen von Abfragen zum Erstellen von Tabellen. Im Unterschied dazu werden jedoch Zeilen in eine vorhandene Tabelle kopiert.  
  
> [!TIP]  
> Sie können Zeilen auch durch Ausschneiden und Einfügen von einer Tabelle in eine andere kopieren. Erstellen Sie eine Abfrage für jede Tabelle, und führen Sie die Abfragen aus. Kopieren Sie die gewünschten Zeilen von einem Ergebnisdatenblatt in ein anderes.  
  
Beim Erstellen einer Abfrage zum Einfügen von Ergebnissen müssen folgende Angaben gemacht werden:  
  
-   Die Datenbanktabelle, in die Zeilen kopiert werden sollen (die Zieltabelle)  
  
-   Die Tabelle oder Tabellen, aus der Zeilen kopiert werden sollen (die Quelltabelle) Die Quelltabelle oder -tabellen werden Teil einer Unterabfrage. Wenn Sie innerhalb einer Tabelle kopieren, ist die Quelltabelle auch die Zieltabelle.  
  
-   Die Spalten der Quelltabelle, deren Inhalt Sie kopieren möchten  
  
-   Die Spalten der Zieltabelle, in die die Daten kopiert werden sollen  
  
-   Suchbedingungen zum Definieren der zu kopierenden Zeilen  
  
-   Die Sortierreihenfolge, wenn die Zeilen in einer besonderen Reihenfolge kopiert werden sollen  
  
-   Gruppierungsoptionen, wenn Sie nur Kurzinformationen kopieren möchten.  
  
Beispielsweise kopiert die folgende Abfrage Titelinformationen aus der Tabelle `titles` in eine Archivtabelle mit dem Namen `archivetitles`. Die Abfrage kopiert den Inhalt von vier Spalten für alle Titel eines bestimmten Herausgebers:  
  
```  
INSERT INTO archivetitles   
   (title_id, title, type, pub_id)  
SELECT title_id, title, type, pub_id  
FROM titles  
WHERE (pub_id = '0766')  
```  
  
> [!NOTE]  
> Verwenden Sie eine Abfrage zum Einfügen von Werten, um Werte in eine neue Zeile einzufügen.  
  
Sie können den Inhalt ausgewählter Spalten oder aller Spalten einer Zeile kopieren. In beiden Fällen müssen die kopierten Daten mit den Spalten der Zeilen kompatibel sein, in die sie eingefügt werden. Wenn Sie z. B. den Inhalt einer Spalte wie `price`kopieren, müssen von der Spalte in der Zeile, in die kopiert wird, numerische Daten mit Dezimalstellen angenommen werden. Beim Kopieren einer vollständigen Zeile müssen in der Zieltabelle kompatible Spalten in derselben physischen Position wie in der Quelltabelle vorhanden sein.  
  
Wenn Sie eine Abfrage zum Einfügen von Ergebnissen erstellen, ändert sich der Kriterienbereich und zeigt die für das Kopieren von Daten verfügbaren Optionen an. Eine Spalte Anfügen wird hinzugefügt, in der Sie die Spalten angeben können, in die Daten kopiert werden sollen.  
  
> [!CAUTION]  
> Eine ausgeführte Abfrage zum Einfügen von Ergebnissen kann nicht rückgängig gemacht werden. Erstellen Sie vorsichtshalber vor Ausführung der Abfrage eine Sicherungskopie der Daten.  
  
### <a name="to-create-an-insert-results-query"></a>So erstellen Sie eine Abfrage zum Einfügen von Ergebnissen  
  
1.  Erstellen Sie eine neue Abfrage, und fügen Sie die Tabelle hinzu, aus der Zeilen kopiert werden sollen (die Quelltabelle). Wenn Sie Zeilen innerhalb einer Tabelle kopieren, können Sie die Quelltabelle als Zieltabelle hinzufügen.  
  
2.  Zeigen Sie im Menü **Abfrage-Designer** auf **Typ ändern**, und klicken Sie dann auf **Ergebnisse einfügen**.  
  
3.  Wählen Sie im [Dialogfeld „Zieltabelle für Anfügeabfrage auswählen“](../../ssms/visual-db-tools/choose-target-table-for-insert-results-dialog-box-visual-database-tools.md)die Tabelle aus, in die die Zeilen kopiert werden sollen (die Zieltabelle).  
  
    > [!NOTE]  
    > Der Abfrage- und Sicht-Designer kann nicht im Voraus bestimmen, welche Tabellen und Sichten aktualisiert werden können. Daher werden im Dialogfeld **Zieltabelle für Anfügeabfrage auswählen** in der Liste **Tabellenname** alle in der abgefragten Datenverbindung verfügbaren Tabellen und Sichten angezeigt, d. h. auch diejenigen, in die möglicherweise keine Zeilen kopiert werden können.  
  
4.  Wählen Sie in dem Rechteck, das die Tabelle oder das Tabellenwertobjekt darstellt, die Namen der Spalten aus, deren Inhalt kopiert werden soll. Klicken Sie auf **\&#42; (Alle Spalten)**, um vollständige Zeilen zu kopieren.  
  
    Der Abfrage- und Sicht-Designer fügt die ausgewählten Spalten zur Spalte **Spalte** im Kriterienbereich hinzu.  
  
5.  Wählen Sie im Kriterienbereich in der Spalte **Anfügen** für jede zu kopierende Spalte eine Zielspalte in der Zieltabelle aus. Wählen Sie *Tabellenname.\&#42;* aus, wenn Sie vollständige Zeilen kopieren. Die Spalten der Zieltabelle und der Quelltabelle müssen dieselben (oder kompatible) Datentypen aufweisen.  
  
6.  Geben Sie eine Sortierreihenfolge an, falls Sie die Zeilen in einer bestimmten Reihenfolge kopieren möchten. Ausführliche Informationen finden Sie unter [Sortieren und Gruppieren von Abfrageergebnissen &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/sort-and-group-query-results-visual-database-tools.md).  
  
7.  Geben Sie durch Eingabe von Suchbedingungen in der Spalte **Filter** die zu kopierenden Zeilen an. Weitere Informationen finden Sie unter [Angeben von Suchbedingungen &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/specify-search-criteria-visual-database-tools.md).  
  
    Wenn Sie keine Suchbedingung festlegen, werden alle Zeilen der Quelltabelle in die Zieltabelle kopiert.  
  
    > [!NOTE]  
    > Wenn Sie dem Kriterienbereich eine zu durchsuchende Spalte hinzufügen, wird diese vom Abfrage- und Sicht-Designer ebenfalls in die Liste der zu kopierenden Spalten aufgenommen. Wenn Sie eine Spalte für eine Suche verwenden, aber nicht kopieren möchten, deaktivieren Sie das Kontrollkästchen neben dem Spaltennamen in dem Rechteck, das die Tabelle oder das Tabellenwertobjekt darstellt.  
  
8.  Geben Sie Gruppierungsoptionen an, wenn Sie Kurzinformationen kopieren möchten. Weitere Informationen finden Sie unter [Zusammenfassen von Abfrageergebnissen &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/summarize-query-results-visual-database-tools.md).  
  
Beim Ausführen einer Abfrage zum Einfügen von Ergebnissen werden im [Ergebnisbereich](../../ssms/visual-db-tools/results-pane-visual-database-tools.md) keine Ergebnisse angezeigt. Stattdessen wird eine Meldung mit der Anzahl der kopierten Zeilen ausgegeben.  
  
## <a name="see-also"></a>Siehe auch  
[Typen von Abfragen &amp;#40;Visual Database Tools&amp;#41;](../../ssms/visual-db-tools/types-of-queries-visual-database-tools.md)  
[Themen zur Vorgehensweise: Entwerfen von Abfragen und Sichten &amp;#40;Visual Database Tools&amp;#41;](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
  


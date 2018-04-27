---
title: Erstellen von Tabellenerstellungsabfragen (Visual Database Tools) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssms-visual-db
ms.reviewer: ''
ms.suite: sql
ms.technology:
- tools-ssms
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- queries [SQL Server], types
- table creation [SQL Server], Make Table query
- inserting tables
- Make Table query
- adding tables
ms.assetid: 4493cffa-7b2d-4c24-8ef0-d49329198972
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 7cf7bb80f3680c6205342b20b0f6a1cdf7e46614
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="create-make-table-queries-visual-database-tools"></a>Erstellen von Tabellenerstellungsabfragen (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Mit einer Tabellenerstellungsabfrage können Sie Zeilen in eine neue Tabelle kopieren. Dies ist hilfreich, wenn Datenteilmengen als Arbeitsgrundlage erstellt oder der Inhalt einer Tabelle von einer Datenbank in eine andere kopiert werden soll. Eine Tabellenerstellungsabfrage ähnelt einer Abfrage zum Einfügen von Ergebnissen. Jedoch wird im Unterschied dazu eine neue Tabelle erstellt, in die Zeilen kopiert werden sollen.  
  
Beim Erstellen einer Tabellenerstellungsabfrage müssen folgende Angaben gemacht werden:  
  
-   Der Name der neuen Datenbanktabelle (der Zieltabelle)  
  
-   Die Tabelle oder Tabellen, aus der Zeilen kopiert werden sollen (die Quelltabelle) Das Kopieren ist aus einer einzelnen oder aus verknüpften Tabellen möglich.  
  
-   Die Spalten der Quelltabelle, deren Inhalt Sie kopieren möchten  
  
-   Die Sortierreihenfolge, wenn die Zeilen in einer besonderen Reihenfolge kopiert werden sollen  
  
-   Suchbedingungen zum Definieren der zu kopierenden Zeilen  
  
-   Gruppierungsoptionen, wenn Sie nur Kurzinformationen kopieren möchten.  
  
Die folgende Abfrage erstellt z.B. eine neue Tabelle mit dem Namen `uk_customers` und kopiert Informationen aus der Tabelle `customers` hinein:  
  
```  
SELECT *   
INTO uk_customers  
FROM customers  
WHERE country = 'UK'  
```  
  
Folgende Bedingungen müssen erfüllt sein, damit eine Tabellenerstellungsabfrage erfolgreich verwendet werden kann:  
  
-   Die Datenbank muss die SELECT...INTO-Syntax unterstützen.  
  
-   Sie müssen über eine Berechtigung zum Erstellen von Tabellen in der Zieldatenbank verfügen.  
  
### <a name="to-create-a-make-table-query"></a>So erstellen Sie eine Tabellenerstellungsabfrage  
  
1.  Fügen Sie dem Diagrammbereich die Quelltabellen hinzu.  
  
2.  Zeigen Sie im Menü **Abfrage-Designer** auf **Typ ändern**, und klicken Sie dann auf **Tabelle erstellen**.  
  
3.  Geben Sie im Dialogfeld **Tabelle erstellen** den Namen der Zieltabelle ein. Der Abfrage- und Sicht-Designer überprüft nicht, ob der Name bereits verwendet wird oder ob Sie über eine Berechtigung zum Erstellen der Tabelle verfügen.  
  
    Geben Sie zum Erstellen einer Zieltabelle in einer anderen Datenbank einen vollständigen Tabellennamen an, der den Namen der Zieldatenbank, den Besitzer (falls erforderlich) und den Namen der Tabelle enthält.  
  
4.  Legen Sie die zu kopierenden Spalten fest, indem Sie diese der Abfrage hinzufügen. Ausführliche Informationen finden Sie unter [Hinzufügen von Spalten zu Abfragen (Visual Database Tools)](../../ssms/visual-db-tools/add-columns-to-queries-visual-database-tools.md). Spalten werden nur kopiert, wenn sie der Abfrage hinzugefügt werden. Klicken Sie auf **\&#42; (Alle Spalten)**, um vollständige Zeilen zu kopieren.  
  
    Der Abfrage- und Sicht-Designer fügt die ausgewählten Spalten der Spalte **Spalte** im Kriterienbereich hinzu.  
  
5.  Geben Sie eine Sortierreihenfolge an, falls Sie die Zeilen in einer bestimmten Reihenfolge kopieren möchten. Weitere Informationen finden Sie unter **Sortieren und Gruppieren von Abfrageergebnissen**.  
  
6.  Geben Sie die zu kopierenden Zeilen durch Eingabe von Suchbedingungen an. Weitere Informationen finden Sie unter [Angeben von Suchbedingungen (Visual Database Tools)](../../ssms/visual-db-tools/specify-search-criteria-visual-database-tools.md).  
  
    Wenn Sie keine Suchbedingung festlegen, werden alle Zeilen der Quelltabelle in die Zieltabelle kopiert.  
  
    > [!NOTE]  
    > Wenn Sie dem Kriterienbereich eine zu durchsuchende Spalte hinzufügen, wird diese vom Abfrage- und Sicht-Designer ebenfalls in die Liste der zu kopierenden Spalten aufgenommen. Wenn Sie eine Spalte für eine Suche verwenden, aber nicht kopieren möchten, deaktivieren Sie das Kontrollkästchen in dem Rechteck neben dem Spaltennamen, das die Tabelle oder das Objekt mit Tabellenstruktur darstellt.  
  
7.  Geben Sie Gruppierungsoptionen an, wenn Sie Kurzinformationen kopieren möchten. Weitere Informationen finden Sie unter [Zusammenfassen von Abfrageergebnissen (Visual Database Tools)](../../ssms/visual-db-tools/summarize-query-results-visual-database-tools.md).  
  
Beim Ausführen einer Tabellenerstellungsabfrage werden keine Ergebnisse im [Ergebnisbereich](../../ssms/visual-db-tools/results-pane-visual-database-tools.md)angezeigt. Stattdessen wird eine Meldung mit der Anzahl der kopierten Zeilen ausgegeben.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
[Themen zur Vorgehensweise: Entwerfen von Abfragen und Sichten (Visual Database Tools)](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
[Typen von Abfragen (Visual Database Tools)](../../ssms/visual-db-tools/types-of-queries-visual-database-tools.md)  
  

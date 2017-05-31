---
title: "Angeben mehrerer Suchbedingungen für mehrere Spalten | Microsoft-Dokumentation"
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
- search criteria [SQL Server], multiple conditions
- multiple search conditions
- search conditions [SQL Server], multiple
- OR operator
- AND, Criteria pane
ms.assetid: 06617729-0d0b-4da2-9890-b7e2f5cdbc7b
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 041d9a3c2a204d8413d755ec69946859195b5c0a
ms.contentlocale: de-de
ms.lasthandoff: 04/11/2017

---
# <a name="specify-multiple-search-conditions-for-multiple-columns-visual-database-tools"></a>Angeben mehrerer Suchbedingungen für mehrere Spalten (Visual Database Tools)
Sie können den Bereich der Abfrage erweitern oder einschränken, indem Sie verschiedene Spalten in die Suchbedingung aufnehmen. Auf diese Weise können Sie beispielsweise folgende Vorgänge durchführen:  
  
-   Sie können nach Mitarbeitern suchen, die entweder seit mehr als fünf Jahren in der Firma arbeiten oder bestimmte Tätigkeiten ausführen.  
  
-   Sie können nach einem Buch suchen, das von einem bestimmten Herausgeber veröffentlicht wurde und gleichzeitig ein Kochbuch ist.  
  
Für einer Abfrage, die in zwei oder mehr Spalten nach Werten sucht, wird eine OR-Bedingung verwendet. Demgegenüber wird zur Erstellung einer Abfrage, die alle Bedingungen in zwei oder mehr Spalten erfüllen muss, eine AND-Bedingung eingesetzt.  
  
## <a name="specifying-an-or-condition"></a>Angeben einer OR-Bedingung  
Wenn Sie mehrere mit OR verknüpfte Bedingungen erstellen möchten, setzen Sie jede Bedingung in eine andere Spalte des Kriterienbereichs.  
  
#### <a name="to-specify-an-or-condition-for-two-different-columns"></a>So geben Sie eine OR-Bedingung für zwei verschiedene Spalten an  
  
1.  Fügen Sie dem [Kriterienbereich](../../ssms/visual-db-tools/criteria-pane-visual-database-tools.md)die Spalten hinzu, die durchsucht werden sollen.  
  
2.  Geben Sie in der Spalte **Filter** für die erste zu durchsuchende Spalte die erste Bedingung an.  
  
3.  Geben Sie in der Spalte **Oder** für die zweite zu durchsuchende Datenspalte die zweite Bedingung an, und lassen Sie die Spalte **Filter** leer.  
  
    Der Abfrage- und Sicht-Designer erstellt eine WHERE-Klausel mit einer OR-Bedingung, z. B.:  
  
    ```  
    SELECT job_lvl, hire_date  
    FROM employee  
    WHERE (job_lvl >= 200) OR   
      (hire_date < '01/01/1998')  
    ```  
  
4.  Wiederholen Sie die Schritte 2 und 3 für jede weitere Bedingung, die hinzugefügt werden soll. Verwenden Sie für jede neue Bedingung eine neue Spalte **Oder...** .  
  
## <a name="specifying-an-and-condition"></a>Angeben einer AND-Bedingung  
Um verschiedene Datenspalten nach Bedingungen zu durchsuchen, die mit AND verknüpft sind, setzen Sie alle Bedingungen in die Datenblattspalte **Filter** .  
  
#### <a name="to-specify-an-and-condition-for-two-different-columns"></a>So geben Sie eine AND-Bedingung für zwei verschiedene Spalten an  
  
1.  Fügen Sie dem [Kriterienbereich](../../ssms/visual-db-tools/criteria-pane-visual-database-tools.md)die Spalten hinzu, die durchsucht werden sollen.  
  
2.  Geben Sie in der Spalte **Filter** für die erste zu durchsuchende Datenspalte die erste Bedingung an.  
  
3.  Geben Sie in der Spalte **Filter** für die zweite Datenspalte die zweite Bedingung an.  
  
    Der Abfrage- und Sicht-Designer erstellt eine WHERE-Klausel mit einer AND-Bedingung, z. B.:  
  
    ```  
    SELECT pub_id, title  
    FROM titles  
    WHERE (pub_id = '0877') AND (title LIKE '%Cook%')  
    ```  
  
4.  Wiederholen Sie die Schritte 2 und 3 für jede weitere Bedingung, die hinzugefügt werden soll.  
  
## <a name="see-also"></a>Siehe auch  
[Kombinieren von Bedingungen, wenn AND Vorrang hat (Visual Database Tools)](../../ssms/visual-db-tools/combine-conditions-when-and-has-precedence-visual-database-tools.md)  
[Kombinieren von Bedingungen, wenn OR Vorrang hat (Visual Database Tools)](../../ssms/visual-db-tools/combine-conditions-when-or-has-precedence-visual-database-tools.md)  
[Konventionen für das Kombinieren von Suchbedingungen im Kriterienbereich (Visual Database Tools)](../../ssms/visual-db-tools/conventions-combine-search-conditions-in-criteria-pane-visual-db-tools.md)  
[Angeben von Suchkriterien (Visual Database Tools)](../../ssms/visual-db-tools/specify-search-criteria-visual-database-tools.md)  
  


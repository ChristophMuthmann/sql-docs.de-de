---
title: "Kombinieren von Bedingungen, wenn „OR“ Vorrang hat (Visual Database Tools) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssms-visual-db
ms.reviewer: 
ms.suite: sql
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- search conditions [SQL Server], combining
- precedence [SQL Server], Criteria pane
- search criteria [SQL Server], combining conditions
- combining search conditions
- OR operator
ms.assetid: b30f5ac9-25e7-4163-80ed-44e4bccb455d
caps.latest.revision: "4"
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 85774366530b325149474e2dbb527fdc33b01cad
ms.sourcegitcommit: b6116b434d737d661c09b78d0f798c652cf149f3
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/17/2018
---
# <a name="combine-conditions-when-or-has-precedence-visual-database-tools"></a>Kombinieren von Bedingungen, wenn OR Vorrang hat (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] Wenn die mit OR verbundene Bedingungen den Vorrang vor den mit AND verbundenen Bedingungen haben sollen, muss die AND-Bedingung für jede OR-Bedingung wiederholt werden.  
  
Angenommen, Sie möchten alle Mitarbeiter suchen, die der Firma seit mehr als fünf Jahren angehören und gering qualifizierte Tätigkeiten auf unterer Betriebsebene ausführen oder im Ruhestand sind. Diese Abfrage erfordert drei Bedingungen: eine einzelne Bedingung, die mit zwei weiteren Bedingungen durch AND verknüpft ist:  
  
-   Mitarbeiter, deren Einstellungsdatum mehr als fünf Jahre zurückliegt und  
  
-   Mitarbeiter mit einer Tätigkeitsstufe von 100 oder Mitarbeiter, deren Status "R" (Ruhestand) ist.  
  
Das folgende Verfahren illustriert die Erstellung einer derartigen Abfrage im Kriterienbereich.  
  
### <a name="to-combine-conditions-when-or-has-precedence"></a>So kombinieren Sie Bedingungen, wenn OR Vorrang hat  
  
1.  Fügen Sie dem [Kriterienbereich](../../ssms/visual-db-tools/criteria-pane-visual-database-tools.md)die Datenspalten hinzu, die durchsucht werden sollen. Wenn Sie dieselbe Spalte nach zwei oder mehr mit AND verbundenen Bedingungen durchsuchen möchten, müssen Sie den Namen der Datenspalte für jeden zu suchenden Wert einmal in das Datenblatt einfügen.  
  
2.  Erstellen Sie die Bedingungen, die mit OR verknüpft werden sollen, indem Sie die erste Bedingung in die Datenblattspalte **Filter** und die zweite (sowie alle weiteren) Bedingungen in jeweils unterschiedliche Spalten **Oder...** eingeben. Geben Sie `job_lvl` in die Spalte `status` Filter `= 100` für **und** in die Spalte `job_lvl` Oder... `= 'R'` für **ein, um beispielsweise Bedingungen mit OR zum Durchsuchen der Spalten** und `status`zu verknüpfen.  
  
    Wenn Sie diese Werte im Datenblatt eingeben, wird die folgende WHERE-Klausel in der Anweisung im SQL-Bereich erstellt:  
  
    ```  
    WHERE (job_lvl = 100) OR (status = 'R')  
    ```  
  
3.  Erstellen Sie die AND-Bedingung, indem Sie sie für jede OR-Bedingungen einmal eingeben. Nehmen Sie den Eintrag jeweils in der Datenblattspalte der entsprechenden OR-Bedingung vor. Geben Sie beispielsweise `hire_date` sowohl in die Spalte „Kriterien“ als auch in die Spalte `< '1/1/91'` Oder... **ein, um eine AND-Bedingung hinzuzufügen, die in der Spalte** sucht und für beide OR-Bedingungen gilt.  
  
    Wenn Sie diese Werte im Datenblatt eingeben, wird die folgende WHERE-Klausel in der Anweisung im SQL-Bereich erstellt:  
  
    ```  
    WHERE (job_lvl = 100) AND   
      (hire_date < '01/01/91' ) OR  
      (status = 'R') AND   
      (hire_date < '01/01/91' )  
    ```  
  
    > [!TIP]  
    > Sie können eine AND-Bedingung wiederholen, indem Sie sie einmal einfügen und dann mithilfe der Befehle **Ausschneiden** und **Einfügen** aus dem Menü **Bearbeiten** für die anderen OR-Bedingungen kopieren.  
  
Die WHERE-Klausel, die vom Abfrage- und Sicht-Designer erstellt wird, entspricht der folgenden WHERE-Klausel, in der zum Festlegen des Vorrangs von OR vor AND Klammern verwendet werden:  
  
```  
WHERE (job_lvl = 100 OR status = 'R') AND  
   (hire_date < '01/01/91')  
```  
  
> [!NOTE]  
> Wenn Sie die Suchbedingungen im unmittelbar oberhalb des [SQL-Bereichs](../../ssms/visual-db-tools/sql-pane-visual-database-tools.md)angezeigten Format eingeben und dann im Diagramm- oder Kriterienbereich Änderungen an der Abfrage vornehmen, wird die SQL-Anweisung vom Abfrage- und Sicht-Designer neu erstellt, damit sie mit dem Formular übereinstimmt, das die explizit auf beide OR-Bedingungen verteilte AND-Bedingung enthält.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
[Konventionen für das Kombinieren von Suchbedingungen im Kriterienbereich &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/conventions-combine-search-conditions-in-criteria-pane-visual-db-tools.md)  
[Angeben von Suchkriterien &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/specify-search-criteria-visual-database-tools.md)  
  

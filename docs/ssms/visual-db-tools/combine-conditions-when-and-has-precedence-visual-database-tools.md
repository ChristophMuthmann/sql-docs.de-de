---
title: "Kombinieren von Bedingungen, wenn „AND“ Vorrang hat (Visual Database Tools) | Microsoft-Dokumentation"
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
- AND, Criteria pane
ms.assetid: 450eb2eb-6ea3-405b-8dd2-1ff926c016e7
caps.latest.revision: "5"
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2f5ca94d7be22a9bd8635edf453709d4beefdb80
ms.sourcegitcommit: b6116b434d737d661c09b78d0f798c652cf149f3
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/17/2018
---
# <a name="combine-conditions-when-and-has-precedence-visual-database-tools"></a>Kombinieren von Bedingungen, wenn AND Vorrang hat (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] Um Bedingungen mit AND zu kombinieren, fügen Sie die Spalte zur Abfrage zweimal hinzu – je einmal für jede Bedingung. Um Bedingungen mit OR zu kombinieren, setzen Sie die erste Bedingung in die Filterspalte und die weiteren Bedingungen in eine Spalte **Oder...** .  
  
Angenommen, Sie möchten nach Mitarbeitern suchen, die entweder seit mehr als fünf Jahren in der Firma beschäftigt sind und gering qualifizierte Tätigkeiten auf unterer Betriebsebene ausüben oder unabhängig vom Einstellungsdatum auf mittlerer Betriebsebene tätig sind. Diese Abfrage erfordert drei Bedingungen, von denen zwei mit AND verknüpft sind:  
  
-   Mitarbeiter, die vor weniger als fünf Jahren eingestellt wurden UND deren Tätigkeitsstufe 100 beträgt.  
  
    -oder-  
  
-   Mitarbeiter mit der Tätigkeitsstufe 200.  
  
### <a name="to-combine-conditions-when-and-has-precedence"></a>So kombinieren Sie Bedingungen, wenn AND Vorrang hat  
  
1.  Fügen Sie dem [Kriterienbereich](../../ssms/visual-db-tools/criteria-pane-visual-database-tools.md)die Datenspalten hinzu, die durchsucht werden sollen. Wenn Sie dieselbe Spalte nach zwei oder mehr mit AND verbundenen Bedingungen durchsuchen möchten, müssen Sie den Namen der Datenspalte für jeden zu suchenden Wert einmal in das Datenblatt einfügen.  
  
2.  Geben Sie in der Spalte **Kriterien** sämtliche Bedingungen ein, die mit AND verknüpft werden sollen. Um beispielsweise Bedingungen mit AND zu verknüpfen, nach denen in den Spalten `hire_date` und `job_lvl` gesucht werden soll, geben Sie in die Filterspalte die Werte `< '1/1/91'` und `= 100`ein.  
  
    Diese Datenblatteinträge generieren die folgende WHERE-Klausel in der Anweisung im [SQL-Bereich](../../ssms/visual-db-tools/sql-pane-visual-database-tools.md):  
  
    ```  
    WHERE (hire_date < '01/01/91') AND  
      (job_lvl = 100)  
    ```  
  
3.  Geben Sie in der Datenblattspalte **Oder...** Bedingungen ein, die mit OR verknüpft werden sollen. Wenn beispielsweise eine Bedingung hinzugefügt werden soll, die nach einem anderen Wert in der Spalte `job_lvl` sucht, fügen Sie einen zusätzlichen Wert in die Spalte **Oder...** ein, z. B. `= 200`.  
  
    Durch das Hinzufügen eines Werts in der Spalte **Oder...** wird der WHERE-Klausel in der Anweisung im SQL-Bereich eine weitere Bedingung hinzugefügt:  
  
    ```  
    WHERE (hire_date < '01/01/91' ) AND  
      (job_lvl = 100) OR   
      (job_lvl = 200)  
    ```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
[Kombinieren von Bedingungen, wenn OR Vorrang hat (Visual Database Tools)](../../ssms/visual-db-tools/combine-conditions-when-or-has-precedence-visual-database-tools.md)  
[Konventionen für das Kombinieren von Suchbedingungen im Kriterienbereich (Visual Database Tools)](../../ssms/visual-db-tools/conventions-combine-search-conditions-in-criteria-pane-visual-db-tools.md)  
[Regeln für das Eingeben von Suchwerten (Visual Database Tools)](../../ssms/visual-db-tools/rules-for-entering-search-values-visual-database-tools.md)  
[Angeben von Suchkriterien (Visual Database Tools)](../../ssms/visual-db-tools/specify-search-criteria-visual-database-tools.md)  
  

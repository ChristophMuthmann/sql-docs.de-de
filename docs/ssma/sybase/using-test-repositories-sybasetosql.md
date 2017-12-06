---
title: Mithilfe von Test-Repositorys (SybaseToSQL) | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: ssma-sybase
ms.reviewer: 
ms.suite: sql
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords: Tester Component,Test Repositories
ms.assetid: c359c25c-db2a-4a20-afa9-62d87a62df72
caps.latest.revision: "7"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7fc0391764e4accadb6c333cd554b9ad11a2d806
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/05/2017
---
# <a name="using-test-repositories-sybasetosql"></a>Mithilfe von Test-Repositorys (SybaseToSQL)
Die SSMA testen Repository-Speicher SSMA Tester Testfälle und die Testergebnisse für die spätere Verwendung. Die Repository-Daten werden in der SQL Server-Tabellen gespeichert **TestCaseRepository** und **RunTestCaseResultRepository** im Schema **Ssma_sybase_utilities** von **Ssmatesterdb_syb** Datenbank.  
  
Die folgenden Schaltflächen stehen im Dialogfeld Repository Testfälle zur Verfügung:  
  
-   Klicken Sie auf die **aktualisieren** Schaltfläche, um die Liste von Testfällen oder Tests Ergebnisse zu aktualisieren.  
  
-   Klicken Sie auf die **schließen** Schaltfläche, um das Repository Testfälle-Dialogfeld zu schließen.  
  
## <a name="test-cases-repository"></a>Testfälle Repository  
Sie können Testfälle Repository anzeigen, indem Sie auf **Testfälle...** aus der **Tester** Menü. SSMA zeigt dann die **Repository Testfälle** Dialogfenster mit einer Liste von gespeicherten Testfälle auf die **Testfälle** Seite.  
  
Das Raster zeigt die folgende Informationen zu jedem Testfall muss:  
  
-   Name: Der Name des Testfalls.  
  
-   Erstellt: Der Testfall Erstellungsdatum.  
  
-   Geänderte: Testfall Datum der letzten Änderung.  
  
-   Beschreibung: Die Testfall-Beschreibungen  
  
Die folgenden Schaltflächen stehen auf der Seite "Testfälle" zur Verfügung:  
  
-   Klicken Sie auf die **hinzufügen** Schaltfläche, um den Testfall-Assistenten ausführen, und erstellen einen neuen Test.  
  
-   Klicken Sie auf die **entfernen** Schaltfläche, um den ausgewählten Test aus dem Repository zu löschen. Wenn ein Testfall gelöscht wird, werden alle zugehörigen Testergebnisse ebenfalls gelöscht.  
  
-   Klicken Sie auf die **bearbeiten** Schaltfläche, um den Testfall-Assistenten ausführen und ändern den ausgewählten Test.  
  
-   Klicken Sie auf die **ausführen** die Schaltfläche, um die [Ausführen von Testfällen &#40; SybaseToSQL &#41; ](../../ssma/sybase/running-test-cases-sybasetosql.md) Dialogfeld, und führen Sie den ausgewählten Test.  
  
## <a name="test-results-repository"></a>Ergebnisrepository  
Sehen Sie die Ergebnisrepository auf die **Testergebnisse** auf der Seite der **Repository Testfälle** Fenster. Öffnen Sie sie durch Klicken auf **Testergebnisse...** aus der **Tester** Menü.  
  
Sie können zwei Filter auf **Testergebnisse** Seite:  
  
-   Der Name des Testfalls Filter: ermöglicht die Auswahl von Testergebnissen nach dem Namen des Testfalls. Dieser Filter **alle Testfall** Wert ermöglicht das Anzeigen von Testergebnissen für alle Testfälle.  
  
-   Der Testfall Ausführung Datumsfilter: Filter Testergebnisse nach dem Datum speichern. Dieser Filter **alle Zeitraum** Wert ermöglicht das Anzeigen von Testergebnissen für alle Datum speichern.  
  
Die folgende Informationen zu Testergebnissen wird im Raster angezeigt.  
  
-   Name: Name des Testfalls.  
  
-   Schritte: Testen Sie Groß-/Kleinschreibung Datum der ausgeführt wird.  
  
-   Ergebnis: Eine kurze Zusammenfassung der Ausführung des Tests (diese Zelle QuickInfo zeigt eine vollständige Zusammenfassung der Ausführung des Tests).  
  
Die folgenden Schaltflächen stehen auf der Seite "Testergebnis" zur Verfügung:  
  
-   Klicken Sie auf die **Ansicht** die Schaltfläche, um [Testfall Berichte anzeigen &#40; SybaseToSQL &#41; ](../../ssma/sybase/viewing-test-case-reports-sybasetosql.md) des aktuellen Testfall Ergebnisses.  
  
-   Klicken Sie auf die **löschen** Schaltfläche, um das ausgewählte Testergebnis löschen  
  
## <a name="see-also"></a>Siehe auch  
[Ausführen von Testfällen &#40; SybaseToSQL &#41;](../../ssma/sybase/running-test-cases-sybasetosql.md)  
[Testen von migriert Datenbankobjekte &#40; SybaseToSQL &#41;](../../ssma/sybase/testing-migrated-database-objects-sybasetosql.md)  
  

---
title: Mithilfe von Test-Repositorys (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-oracle
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Test Cases Repository
- Test Results Repository
ms.assetid: f941cce4-d3e3-4aeb-a88a-4f101a97a9f4
caps.latest.revision: 8
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: 1f8336d7328d7423cf7b3356fd6229a9ac99496d
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="using-test-repositories-oracletosql"></a>Mithilfe von Test-Repositorys (OracleToSQL)
Die SSMA testen Repository-Speicher SSMA Tester Testfälle und die Testergebnisse für die spätere Verwendung. Die Repository-Daten werden in der SQL Server-Tabellen gespeichert **TestCaseRepository** und **RunTestCaseResultRepository** im Schema **Ssma_oracle_utilities** von **Ssmatesterdb** Datenbank.  
  
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
  
-   Klicken Sie auf die **ausführen** die Schaltfläche, um die [Ausführen von Testfällen (OracleToSQL)](http://msdn.microsoft.com/en-us/fc208cdb-7373-4f6b-8f6c-cdff9d3dcd02) Dialogfeld, und führen Sie den ausgewählten Test.  
  
## <a name="test-results-repository"></a>Ergebnisrepository  
Sehen Sie die Ergebnisrepository auf die **Testergebnisse** auf der Seite der **Repository Testfälle** Fenster. Öffnen Sie sie durch Klicken auf **Testergebnisse...** aus der **Tester** Menü.  
  
Sie können zwei Filter auf **Testergebnisse** Seite:  
  
-   Der Name des Testfalls Filter: ermöglicht die Auswahl von Testergebnissen nach dem Namen des Testfalls. Dieser Filter **aller Testfälle** Wert ermöglicht das Anzeigen von Testergebnissen für alle Testfälle.  
  
-   Der Testfall Ausführung Datumsfilter: Filter Testergebnisse nach dem Datum speichern. Dieser Filter **alle Zeitraum** Wert ermöglicht das Anzeigen von Testergebnissen für alle Datum speichern.  
  
Die folgende Informationen zu Testergebnissen wird im Raster angezeigt.  
  
-   Name: Name des Testfalls.  
  
-   Gespeichert: Testen Sie Groß-/Kleinschreibung Datum speichern.  
  
-   Ergebnisse: Eine kurze Zusammenfassung der Ausführung des Tests (diese Zelle QuickInfo zeigt eine vollständige Zusammenfassung der Ausführung des Tests).  
  
Die folgenden Schaltflächen stehen auf der Seite "Testergebnis" zur Verfügung:  
  
-   Klicken Sie auf die **Ansicht** die Schaltfläche, um [Testfall Berichte anzeigen &#40;OracleToSQL&#41; ](../../ssma/oracle/viewing-test-case-reports-oracletosql.md) des aktuellen Testfallergebnis.  
  
-   Klicken Sie auf die **löschen** Schaltfläche, um das ausgewählte Testergebnis löschen  
  
## <a name="see-also"></a>Siehe auch  
[Ausführen von Testfällen &#40;OracleToSQL&#41;](../../ssma/oracle/running-test-cases-oracletosql.md)  
[Testen von Datenbankobjekten migriert &#40;OracleToSQL&#41;](../../ssma/oracle/testing-migrated-database-objects-oracletosql.md)  
  

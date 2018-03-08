---
title: "Auswählen und Konfigurieren von betroffene Objekte (OracleToSQL) | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssma-oracle
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Columns Comparison Settings
- Selection of Affected Objects
ms.assetid: 545eeda2-9829-4187-a858-619a96b4b71d
caps.latest.revision: "8"
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.workload: Inactive
ms.openlocfilehash: 1a4fe479f53c914b4417cd0069335fa8bb0da027
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="selecting-and-configuring-affected-objects-oracletosql"></a>Auswählen und Konfigurieren von betroffene Objekte (OracleToSQL)
Auf dieser Seite können Sie Tabellen auswählen und Fremdschlüsseln, Änderungen in der verglichen werden sollen, wenn SSMA wird überprüft, die Ergebnisse der Ausführung für die Objekte, die in den vorherigen Schritt ausgewählt wurde ob. Darüber hinaus können Sie die Überprüfung der Parameter anpassen.  
  
## <a name="selection-of-affected-objects"></a>Auswahl der betroffenen Objekte  
In der Oracle-Objektstruktur auf der linken Seite des Fensters befinden, überprüfen Sie die Tabellen und Fremdschlüsseln, Änderungen in der für den identischen verglichen werden sollen.  
  
Wenn Tester SSMA eines dieser Objekte nicht überprüft werden kann, sehen Sie die Verknüpfung mit der Bezeichnung **einige ausgewählte Objekte enthalten Fehler** unter der Struktur der Objekte. Klicken Sie auf diesen Link an die Gründe, warum diese Objekte nicht verglichen werden können, und um die Auswahl der falschen Objekte zu löschen.  
  
## <a name="table"></a>Tabelle  
Die Registerkarte "Tabelle" enthält die Rasteransicht der ausgewählten Tabelle an. Das Raster enthält die folgende Informationen über die ausgewählte Tabelle an:  
  
-   Spaltenname  
  
-   Datentyp  
  
-   Genauigkeit  
  
-   Dezimalstellen  
  
-   Regel  
  
-   Default  
  
-   Identität  
  
-   NULL zulassen  
  
## <a name="sql"></a>Sql  
Registerkarte "SQL" enthält die Tabelle"erstellen" SQL der ausgewählten Tabelle.  
  
## <a name="data"></a>data  
Registerkarte "Daten" zeigt die ausgewählte Tabelle vorhandenen Daten.  
  
## <a name="properties"></a>Eigenschaften  
Registerkarte "Eigenschaften" zeigt die Eigenschaften der ausgewählten Tabelle an. Die folgenden Felder sind vorhanden, unter der Registerkarte "Eigenschaften":  
  
-   Erstellt oder zuletzt geändert  
  
-   Objektnamen  
  
## <a name="columns-comparison-settings"></a>Vergleichseinstellungen Spalten  
Einrichten der Vergleichsregeln für Tabellenspalten auf **Spalten Vergleich** Seite. Sie können die folgenden Einstellungen vornehmen.  
  
### <a name="use-during-test-comparisons"></a>Verwendung während der Testvergleiche  
Bestimmt, ob diese Spalte in den Ergebnissen testüberprüfung einbezogen werden.  
  
-   Falls gewünscht **"true"**, SSMA wird der Inhalt dieser Spalte vergleichen, nach dem Ausführen des Tests auf Oracle mit dem Inhalt der Spalte in SQL Server. 
  
-   Falls gewünscht**"false"**, die Spalte vom Ergebnisbereich Überprüfung ausgeschlossen werden.  
  
### <a name="use-custom-scale"></a>Benutzerdefinierte Skalierung verwenden  
Für Spalten mit numerischen Datentyp aufweisen können Sie einen benutzerdefinierten Maßstab für den Vergleich festlegen.  
  
-   Falls gewünscht **"true"**, numerische Werte werden entsprechend dem gerundet werden die **vergleichen Skalierung** Wert, bevor diese verglichen werden.  
  
-   Falls gewünscht**"false"**, genauen numerische Vergleich werden.  
  
### <a name="comparing-scale"></a>Vergleichen von Skala  
  
-   Nur verfügbar, wenn die **Verwenden benutzerdefinierter Maßstab** Option wird festgelegt, um **"true"**. Dies ist die Genauigkeit für einen numerischen Vergleich.  
  
### <a name="date-time-comparing"></a>Datum Uhrzeit vergleichen  
Definiert, wie Datum/Uhrzeit-Werte verglichen werden.  
  
-   Bei Auswahl des **gesamte Datum vergleichen**, vollständigen Vergleich von Werten aus beiden Plattformen ausgeführt werden.  
  
-   Bei Auswahl des **nur Datum vergleichen**, wird die Uhrzeit, die Teil werden ignoriert.  
  
-   Bei Auswahl des **nur Zeit vergleichen**, das Datum Teil werden ignoriert.  
  
-   Bei Auswahl des **ignorieren Millisekunden**, werden die Ergebnisse bis zur Sekunden verglichen.  
  
-   Bei Auswahl des **Datum ignorieren und die Millisekunden**, das Ergebnis wird im Vergleich nur von Time-Teil und wird ignoriert Bruchteile einer Sekunde sein.  
  
### <a name="ignore-strings-case"></a>Zeichenfolgen Groß-/Kleinschreibung ignorieren  
Steuert den Vergleich Groß-/Kleinschreibung berücksichtigt.  
  
-   Falls gewünscht **"true"**, wird der Vergleich Groß-/Kleinschreibung beachtet werden.  
  
-   Falls gewünscht **"false"**, der Vergleich für Groß-/Kleinschreibung berücksichtigt wird.  
  
## <a name="comparing-sql"></a>Vergleichen von SQL  
Sehen Sie die SELECT-Anweisungen generiert von SSMA Tester auf die **SQL vergleichen** Seite. Der Tester werden die Resultsets dieser Anweisungen pro Zeile für Zeile verglichen. Jede nächste Zeile von einem Oracle-Resultset sollte die nächste Zeile des Resultsets in SQL Server erstellten gleich sein.
  
Sie können diese SELECT-Anweisungen für die benutzerdefinierte Überprüfung bearbeiten. Verwenden Sie zum Speichern der Änderungen in Oracle und SQL Server-Anweisungen, die **übernehmen** Schaltflächen unter den Quell- und Zielservern SQL "oder" entsprechend angepasst.  
  
## <a name="next-step"></a>Nächster Schritt  
[Anpassen der Reihenfolge der Aufrufe &#40; OracleToSQL &#41;](../../ssma/oracle/customizing-calls-order-oracletosql.md)  
  
## <a name="see-also"></a>Siehe auch  
[Beenden Testfall Vorbereitung &#40; OracleToSQL &#41;](../../ssma/oracle/finishing-test-case-preparation-oracletosql.md)  
[Ausführen von Testfällen &#40; OracleToSQL &#41;](../../ssma/oracle/running-test-cases-oracletosql.md)  
[Testen von migriert Datenbankobjekte &#40; OracleToSQL &#41;](../../ssma/oracle/testing-migrated-database-objects-oracletosql.md)  
  

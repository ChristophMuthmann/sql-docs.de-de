---
title: "Auswählen und Konfigurieren von betroffene Objekte (SybaseToSQL) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Tester Component,Affected Objects
ms.assetid: a219df74-543a-4aec-aeeb-79f90ac3e2ee
caps.latest.revision: 8
author: sabotta
ms.author: carlasab
manager: lonnyb
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 8e5f4fcb5af81da2b78520542e2b57bd66bc4fd1
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="selecting-and-configuring-affected-objects-sybasetosql"></a>Auswählen und Konfigurieren von betroffene Objekte (SybaseToSQL)
Auf dieser Seite können Sie Tabellen auswählen und Fremdschlüsseln, Änderungen in der verglichen werden sollen, wenn SSMA wird überprüft, die Ergebnisse der Ausführung für die Objekte, die in den vorherigen Schritt ausgewählt wurde ob. Darüber hinaus können Sie die Überprüfung der Parameter anpassen.  
  
## <a name="selection-of-affected-objects"></a>Auswahl der betroffenen Objekte  
In der Objektstruktur für die Sybase befindet sich auf der linken Seite des Fensters, überprüfen Sie die Tabellen und Fremdschlüsseln, Änderungen in der für den identischen verglichen werden sollen.  
  
Wenn Tester SSMA eines dieser Objekte nicht überprüft werden kann, sehen Sie die Verknüpfung mit der Bezeichnung **einige ausgewählte Objekte enthalten Fehler** unter der Struktur der Objekte. Klicken Sie auf diesen Link an die Gründe, warum diese Objekte nicht verglichen werden können, und um die Auswahl der falschen Objekte zu löschen.  
  
## <a name="table"></a>Tabelle  
Die Registerkarte "Tabelle" enthält die Rasteransicht der ausgewählten Tabelle an. Das Raster enthält die folgende Informationen über die ausgewählte Tabelle an:  
  
-   Spaltenname  
  
-   Datentyp  
  
-   Genauigkeit  
  
-   Dezimalstellen  
  
-   Rule  
  
-   Standardwert  
  
-   Identität  
  
-   NULL zulassen  
  
## <a name="sql"></a>Sql  
Registerkarte "SQL" enthält die Tabelle"erstellen" SQL der ausgewählten Tabelle.  
  
## <a name="data"></a>Daten  
Registerkarte "Daten" zeigt die ausgewählte Tabelle vorhandenen Daten.  
  
## <a name="properties"></a>Eigenschaften  
Registerkarte "Eigenschaften" zeigt die Eigenschaften der ausgewählten Tabelle an. Die folgenden Felder sind vorhanden, unter der Registerkarte "Eigenschaften":  
  
-   Erstellt oder zuletzt geändert  
  
-   Objektname  
  
## <a name="table-comparison-settings"></a>Vergleich von Tabelleneinstellungen  
Einrichten der Vergleichsregeln für die Tabelle auf **Tabellenvergleiche** Seite. Sie können die folgenden Einstellungen vornehmen.  
  
### <a name="comparison-mode"></a>Vergleichsmodus  
Definiert den Tabelleninhalt auf die den Vergleich ausgeführt.  
  
-   Bei Auswahl des **nur geänderte Objekte**, vollständigen Vergleich der Tabellenzeilen wird ausgeführt.  
  
-   Bei Auswahl des **vollständige**, erfolgt der Vergleich nur die Zeilen, die geändert wurden.  
  
## <a name="column-comparison-settings"></a>Spalteneinstellungen-Vergleich  
Einrichten der Vergleichsregeln für Tabellenspalten auf **Spalte Vergleiche** Seite. Sie können die folgenden Einstellungen vornehmen.  
  
### <a name="use-during-test-comparisons"></a>Verwendung während der Testvergleiche  
Bestimmt, ob diese Spalte in den Ergebnissen testüberprüfung einbezogen werden.  
  
-   Falls gewünscht **"true"**, SSMA wird der Inhalt dieser Spalte vergleichen, nach dem Ausführen des Tests auf Sybase mit dem Inhalt der Spalte in SQL Server.
  
-   Falls gewünscht **"false"**, die Spalte vom Ergebnisbereich Überprüfung ausgeschlossen werden.  
  
### <a name="use-custom-scale"></a>Benutzerdefinierte Skalierung verwenden  
Für Spalten mit numerischen Datentyp aufweisen können Sie einen benutzerdefinierten Maßstab für den Vergleich festlegen.  
  
-   Falls gewünscht **"true"**, numerische Werte werden entsprechend dem gerundet werden die **vergleichen Skalierung** Wert, bevor diese verglichen werden.  
  
-   Falls gewünscht **"false"**, genauen numerische Vergleich werden.  
  
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
Sehen Sie die SELECT-Anweisungen generiert von SSMA Tester auf die **SQL vergleichen** Seite. Der Tester werden die Resultsets dieser Anweisungen pro Zeile für Zeile verglichen. Jede nächste Zeile eines Resultsets Sybase auf die nächste Zeile des Resultsets in erstellten gleich sein sollten [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
Sie können diese SELECT-Anweisungen für die benutzerdefinierte Überprüfung bearbeiten. Zum Speichern der Änderungen im Sybase und [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Anweisungen können mithilfe der **übernehmen** Schaltflächen unter den Quell- und Zielservern SQL "oder" entsprechend angepasst.  
  
## <a name="next-step"></a>Nächster Schritt  
[Anpassen der Reihenfolge der Aufrufe &#40; SybaseToSQL &#41;](../../ssma/sybase/customizing-calls-order-sybasetosql.md)  
  
## <a name="see-also"></a>Siehe auch  
[Ausführen von Testfällen &#40; SybaseToSQL &#41;](../../ssma/sybase/running-test-cases-sybasetosql.md)  
[Testen von migriert Datenbankobjekte &#40; SybaseToSQL &#41;](../../ssma/sybase/testing-migrated-database-objects-sybasetosql.md)  
  


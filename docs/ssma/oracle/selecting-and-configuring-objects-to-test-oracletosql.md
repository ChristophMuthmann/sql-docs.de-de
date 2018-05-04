---
title: Auswählen und Konfigurieren von Objekten mit Test (OracleToSQL) | Microsoft Docs
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
- Selection of Objects to Test,Parameter Comparison Settings
ms.assetid: 29fb6542-5c1f-4b14-a822-87700beb7623
caps.latest.revision: 8
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: 38ba7b34ac299601b6eede28ea2d5343030ce23e
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="selecting-and-configuring-objects-to-test-oracletosql"></a>Auswählen und Konfigurieren von Objekten mit Test (OracleToSQL)
In diesem Schritt wählen Sie die Objekte zu testen, und konfigurieren Einstellungen für den Vergleich von Prozeduren und Funktionen Output-Parameter als auch die Rückgabewerte von Funktionen.  
  
## <a name="selection-of-objects-to-test"></a>Auswahl von Objekten, die Tests  
Überprüfen Sie in der Oracle-Objektstruktur befindet sich auf der linken Seite des Fensters die Objekte, die Sie während des Testens aufrufen möchten. Die vollständige Liste der getestet werden Objekte in der [migriert Datenbankobjekte testen &#40;OracleToSQL&#41; ](../../ssma/oracle/testing-migrated-database-objects-oracletosql.md) Thema.  
  
Wenn Tester SSMA eines der Objekte, die zu Testzwecken ausgewählt nicht unterstützt wird, sehen Sie die Verknüpfung mit der Bezeichnung **einige ausgewählte Objekte enthalten Fehler** unter der Struktur der Objekte. Klicken Sie auf diesen Link an die Gründe, warum diese Objekte nicht getestet werden können, und um die Auswahl der falschen Objekte zu löschen.  
  
Auf der rechten Seite sehen Sie mehrere Seiten der **SQL** Seite zeigt die Definition für das aktuelle Objekt. Die **Parameter** Seite listet die Parameter auf, wenn das Objekt eine gespeicherte Prozedur oder eine Funktion handelt. Die **Eigenschaften** Seite zeigt die zusätzliche Eigenschaften des Objekts. Siehe die Beschreibung der **Parameter Vergleiche** und **rufen Werte** nachfolgenden Seiten.  
  
## <a name="parameter-comparison-settings"></a>Vergleich von Parametereinstellungen  
Einrichten der Vergleichsregeln für Output-Parameter und Rückgabewerte in der **Parameter Vergleiche** Seite. Sie können die folgenden Einstellungen vornehmen.  
  
### <a name="use-during-test-comparisons"></a>Verwendung während der Testvergleiche  
Aktivieren Sie die von den ausgewählten Parameter in Vergleichsberichte für Ergebnisse verwenden.  
  
-   Falls gewünscht **"true"**, SSMA wird den Ausgabewert dieses Parameters vergleichen, nach dem Ausführen der Prozedur auf Oracle mit den entsprechenden Wert für SQL Server.
  
-   Falls gewünscht **"false"**, der Parameter vom Ergebnisbereich Überprüfung ausgeschlossen werden.  
  
### <a name="use-custom-scale"></a>Benutzerdefinierte Skalierung verwenden  
Für Parameter des numerischen Datentyp aufweisen können Sie einen benutzerdefinierten Maßstab für den Vergleich festlegen.  
  
-   Falls gewünscht **"true"**, numerische Werte werden entsprechend dem gerundet werden die **vergleichen Skalierung** Wert, bevor diese verglichen werden.  
  
-   Falls gewünscht **"false"**, genauen numerische Vergleich werden.  
  
### <a name="comparing-scale"></a>Vergleichen von Skala  
Nur verfügbar, wenn die **Verwenden benutzerdefinierter Maßstab** Option wird festgelegt, um **"true"**. Dies ist die Genauigkeit für einen numerischen Vergleich.  
  
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
  
-   Falls gewünscht **"false"**, wird der Vergleich Groß-/Kleinschreibung beachtet werden.  
  
### <a name="ignore-trailing-spaces"></a>Nachfolgende Leerzeichen ignorieren  
Steuert, wie nachfolgende Leerzeichen werden während des Vergleichs behandelt.  
  
-   Falls gewünscht **"true"**, bevor diese verglichen werden die verglichenen Zeichenfolgen werden rechts abgeschnitten.  
  
-   Falls gewünscht **"false"**, die verglichenen Zeichenfolgen werden nachfolgende Leerzeichen beibehalten.  
  
## <a name="specify-input-values-for-procedures-and-functions-call-values"></a>Geben Sie die Eingabewerte für Prozeduren und Funktionen (rufen Werte)  
Sie können die Werte der Eingabeparameter angeben, auf die **rufen Werte** Seite. Die **Aufruf hinzufügen** Schaltfläche wird einen neuen Aufruf mit leeren Parameterwerten hinzugefügt. Die **entfernen Aufrufe** Schaltfläche entfernt den aktuellen Aufruf.  
  
## <a name="next-step"></a>Nächster Schritt  
[Auswählen und Konfigurieren von betroffene Objekte &#40;OracleToSQL&#41;](../../ssma/oracle/selecting-and-configuring-affected-objects-oracletosql.md)  
  
## <a name="see-also"></a>Siehe auch  
[Testen von Datenbankobjekten migriert &#40;OracleToSQL&#41;](../../ssma/oracle/testing-migrated-database-objects-oracletosql.md)  
  

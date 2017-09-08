---
title: "Auswählen und Konfigurieren von Objekten mit Test (SybaseToSQL) | Microsoft Docs"
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
- Tester Component,Parameter Comparision Setting
- Tester Component,Selecting Objects
ms.assetid: 89c23aad-bfee-4917-bc16-175288390ac0
caps.latest.revision: 7
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: e1cc9bf3ed4348e3875885c1c7bb6face6562753
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="selecting-and-configuring-objects-to-test-sybasetosql"></a>Auswählen und Konfigurieren von Objekten mit Test (SybaseToSQL)
In diesem Schritt wählen Sie die Objekte zu testen, und konfigurieren Einstellungen für den Vergleich von Prozeduren und Funktionen Output-Parameter als auch die Rückgabewerte von Funktionen.  
  
## <a name="selection-of-objects-to-test"></a>Auswahl von Objekten, die Tests  
Überprüfen Sie in der Objektstruktur für die Sybase befindet sich auf der linken Seite des Fensters die Objekte, die Sie während des Testens aufrufen möchten. Die vollständige Liste der getestet werden Objekte in der [migriert Datenbankobjekte testen &#40; SybaseToSQL &#41; ](../../ssma/sybase/testing-migrated-database-objects-sybasetosql.md) Thema.  
  
Wenn Tester SSMA eines der Objekte, die zu Testzwecken ausgewählt nicht unterstützt wird, sehen Sie die Verknüpfung mit der Bezeichnung **einige ausgewählte Objekte enthalten Fehler** unter der Struktur der Objekte. Klicken Sie auf diesen Link an die Gründe, warum diese Objekte nicht getestet werden können, und um die Auswahl der falschen Objekte zu löschen.  
  
Auf der rechten Seite sehen Sie mehrere Seiten der **SQL** Seite zeigt die Definition für das aktuelle Objekt. In der **Pre SQL** und **Post SQL** Seiten können Skripts, die vor und nach dem Aufruf der Test Objekt beginnt ausgeführt angeben. Dies ist möglicherweise nützlich sein, wenn das Objekt zusätzliches Objekt eine solche temporäre Tabellen oder Cursor erfordert. Die **Parameter** Seite listet die Parameter auf, wenn das Objekt eine gespeicherte Prozedur oder eine Funktion handelt. Die **Eigenschaften** Seite zeigt die zusätzliche Eigenschaften des Objekts. Siehe die Beschreibung der **Parameter Comparsions** und **rufen Werte** nachfolgenden Seiten.  
  
## <a name="parameter-comparison-settings"></a>Vergleich von Parametereinstellungen  
Einrichten der Vergleichsregeln für Output-Parameter und Rückgabewerte in der **Parameter vergleichen** Seite. Sie können die folgenden Einstellungen vornehmen.  
  
### <a name="use-during-comparisons"></a>Während der Vergleiche verwenden  
Aktivieren Sie die von den ausgewählten Parameter in Vergleichsberichte für Ergebnisse verwenden.  
  
-   Falls gewünscht **"true"**, SSMA wird nach dem Ausführen der Prozedur für Sybase mit den entsprechenden Wert auf den Ausgabewert dieses Parameters vergleichen[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]  
  
-   Falls gewünscht**"false"**, der Parameter vom Ergebnisbereich Überprüfung ausgeschlossen werden.  
  
### <a name="use-custom-scale"></a>Benutzerdefinierte Skalierung verwenden  
Für Parameter des ungefähre und feste Länge numerischen Datentyp aufweisen können Sie einen benutzerdefinierten Maßstab für den Vergleich festlegen.  
  
-   Falls gewünscht **"true"**, numerische Werte werden entsprechend dem gerundet werden die **vergleichen Skalierung** Wert, bevor diese verglichen werden.  
  
-   Falls gewünscht**"false"**, genauen numerische Vergleich werden.  
  
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
Sie können die Werte der Eingabeparameter angeben, auf die **rufen Werte** Seite. Die **Aufruf hinzufügen** Schaltfläche wird einen neuen Aufruf mit leeren Parameterwerten hinzugefügt. Die **entfernen aufrufen** Schaltfläche entfernt den aktuellen Aufruf.  
  
## <a name="next-step"></a>Nächster Schritt  
[Auswählen und Konfigurieren der betroffenen Objekte &#40; SybaseToSQL &#41;](../../ssma/sybase/selecting-and-configuring-affected-objects-sybasetosql.md)  
  
## <a name="see-also"></a>Siehe auch  
[Testen von migriert Datenbankobjekte &#40; SybaseToSQL &#41;](../../ssma/sybase/testing-migrated-database-objects-sybasetosql.md)  
  


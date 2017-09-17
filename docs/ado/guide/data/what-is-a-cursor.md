---
title: Was ist ein Cursor? | Microsoft-Dokumentation
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- cursors [ADO], about cursors
ms.assetid: 596eb4b6-c22f-4cde-b23f-172dd66c3161
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 03b7d4fe16a379e04fe25fe8fef95802aedabe1d
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="what-is-a-cursor"></a>Was ist ein Cursor?
Vorgänge in einer relationalen Datenbank beziehen sich immer auf eine vollständige Gruppe von Zeilen. Die von einer SELECT-Anweisung zurückgegebene Gruppe von Zeilen besteht aus allen Zeilen, die die Bedingungen der WHERE-Klausel der Anweisung erfüllen. Diese vollständige Gruppe von Zeilen, die von der Anweisung zurückgegeben wird, wird als Resultset bezeichnet. Anwendungen, insbesondere solche, die interaktive und online ist, sind bearbeitet nicht immer effektiv das gesamte Resultset als eine Einheit. Diese Anwendungen benötigen einen Mechanismus, um jeweils eine Zeile oder einen kleinen Zeilenblock zu bearbeiten. Cursor sind eine Erweiterung zu Resultsets und stellen diesen Mechanismus bereit.  
  
 Ein Cursor wird von einer Cursorbibliothek implementiert. Eine Cursorbibliothek ist Software, die häufig als Teil eines Datenbanksystems oder eine Datenzugriffs-API implementiert, der verwendet wird, zur Verwaltung von Attributen von Daten aus einer Datenquelle (ein Resultset) zurückgegeben. Diese Attribute umfassen die Verwaltung der Parallelität, in das Resultset zu positionieren, Anzahl der Zeilen zurückgegeben, und gibt an, ob Sie vorwärts oder rückwärts bewegen können (oder beides) über das Ergebnis festgelegt (bildlauffähigkeit).  
  
 Ein Cursor behält den Überblick über der Position im Resultset und ermöglicht Ihnen, mehrere Vorgänge zeilenweise für ein Resultset, mit oder ohne Rückgabe an die ursprüngliche Tabelle auszuführen. Cursor wird also grundsätzlich einen Resultset auf der Grundlage von Tabellen in den Datenbanken zurück. Der Cursor ist so genannt, da er gibt an, die aktuelle Position im Resultset, ebenso wie die aktuelle Position der Cursor auf einem Computerbildschirm anzeigt.  
  
 Es ist wichtig, vor dem Verschieben auf, um zu erfahren, die Einzelheiten ihre Verwendung in ADO mit dem Konzept von Cursorn vertraut wird.  
  
 Verwenden von Cursorn, können Sie die folgenden Schritte ausführen:  
  
-   Geben Sie die Positionierung an bestimmten Zeilen im Resultset.  
  
-   Rufen Sie eine Zeile oder einen Zeilenblock basierend auf der aktuellen Resultsetposition.  
  
-   Ändern von Daten in den Zeilen an der aktuellen Position im Resultset.  
  
-   Definieren Sie verschiedene Ebenen der Vertraulichkeit von anderen Benutzern vorgenommenen datenänderungen.  
  
 Betrachten Sie beispielsweise eine Anwendung, die eine Liste der verfügbaren Produkte für ein potenzieller Käufer anzeigt. Der Käufer führt einen Bildlauf durch die Liste, um Produktdetails und Kosten anzuzeigen und wählt schließlich ein Produkt erworben werden. Zusätzliche Durchführen eines Bildlaufs und Auswahl tritt auf, für den Rest der Liste. Soweit des Käufers betroffen ist, die Produkte angezeigt werden, einzeln nacheinander, aber die Anwendung einen bildlauffähigen Cursor verwendet, um über das Resultset nach oben oder unten navigieren.  
  
 Sie können Cursor in einer Vielzahl von Möglichkeiten verwenden:  
  
-   Ohne Zeilen überhaupt.  
  
-   Bei einigen oder allen Zeilen in einer einzelnen Tabelle.  
  
-   Bei einigen oder allen Zeilen aus logisch verknüpften Tabellen.  
  
-   Als schreibgeschützt oder aktualisierbar Ebene der Cursor oder ein Feld.  
  
-   Als Vorwärtscursor oder voll bildlauffähigen Cursor.  
  
-   Mit das Keyset des Cursors befindet sich auf dem Server.  
  
-   Empfindlich auf die zugrunde liegende tabellenänderungen, die von anderen Anwendungen (z. B. Mitgliedschaft, sortieren, einfügungen, Updates und löschungen) verursacht werden.  
  
-   Vorhandene auf dem Server oder Client.  
  
 Schreibgeschützte Cursor unterstützen von Benutzern über das Resultset navigieren, und Lese-/Schreibzugriff, dass Cursor einzelne zeilenupdates implementieren können. Komplexe Cursor können mit Keysets definiert werden, die wieder in Tabellenzeilen basieren. Obwohl einige Cursor vorwärts, schreibgeschützt sind, können andere hin-und herwechseln und geben Sie eine dynamische Aktualisierung des Resultsets basierend auf Änderungen, die von anderen Anwendungen in der Datenbank vornehmen.  
  
 Nicht alle Anwendungen müssen Cursor an, die Zugriff oder Aktualisieren von Daten verwenden. Einige Abfragen erfordern keine einfach das Umleiten der Zeile zu aktualisieren, indem Sie einen Cursor zu verwenden. Cursor muss eines der letzten Verfahren Sie zum Abrufen von Daten auswählen, und wählen Sie dann die niedrigsten mögliche Auswirkungen Cursor. Wenn Sie ein Resultset mit einer gespeicherten Prozedur erstellen, ist das Resultset nicht aktualisierbare Cursor verwenden bearbeiten oder Methoden zu aktualisieren.  
  
## <a name="concurrency"></a>Parallelität  
 In einigen Mehrbenutzer Anwendungen ist es sehr wichtig für die Daten angezeigt, die für den Endbenutzer so aktuell wie möglich sein. Ein klassisches Beispiel eines solchen Systems ist eine Airline-Reservierung-System, in dem viele Benutzer konkurriert werden können, für den gleichen Platz für einen bestimmten Flug (und daher einen einzelnen Datensatz). In einem solchen Fall muss der Anwendungsentwurf gleichzeitige Vorgänge auf einem einzelnen Datensatz behandeln.  
  
 In anderen Anwendungen ist die Parallelität nicht so wichtig ist. In solchen Fällen kann nicht der Aufwand es darum geht, die die aktuellen Daten jederzeit ausgerichtet wird.  
  
## <a name="position"></a>Position  
 Ein Cursor der nachverfolgt auch die aktuelle Position in einem Resultset. Stellen Sie sich die Cursorposition als Zeiger auf den aktuellen Datensatz, ähnlich wie ein Array Index verweist auf den Wert an der jeweiligen Position im Array.  
  
## <a name="scrollability"></a>Bildlauffähigkeit  
 Der Typ des von der Anwendung verwendete Cursortyp wirkt sich auch die Möglichkeit, die Zeilen in einem Resultset vorwärts und rückwärts durchlaufen; Dies wird manchmal als scrolloptionen bezeichnet. Die Möglichkeit dann vorwärts bewegt, *und* rückwärts durch ein Ergebnis Satz die Komplexität des Cursors und ist daher teurer implementieren. Aus diesem Grund sollten Sie für einen Cursor mit dieser Funktionalität, die nur bei Bedarf bitten.

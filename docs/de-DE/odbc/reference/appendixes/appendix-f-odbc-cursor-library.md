---
title: 'Anhang F: ODBC-Cursorbibliothek | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- ODBC cursor library [ODBC], about cursor library
- ODBC cursor library [ODBC]
- cursor library [ODBC], about cursor library
- cursor library [ODBC]
ms.assetid: a03084df-4e48-48ef-917d-4a3fae48a605
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ab6ea0ba91b8d62c094a965faaa522b033e05336
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="appendix-f-odbc-cursor-library"></a>Anhang F: ODBC-Cursorbibliothek
> [!IMPORTANT]  
>  Diese Funktion wird in einer zukünftigen Version von Windows entfernt werden. Verwenden Sie diese Funktion beim Entwickeln neuer Anwendungen und Planen von Anwendungen zu ändern, die dieses Feature verwenden. Microsoft empfiehlt die Verwendung der Cursorfunktionalität der Treiber.  
  
 Die ODBC-Cursorbibliothek (Odbccr32.dll) unterstützt Blockcursor bildlauffähigen für alle Treiber, der mit dem Konformitätsgrad Ebene-1-API kompatibel und kann von Entwicklern mit ihren Anwendungen oder Treibern verteilt werden. Die Cursorbibliothek unterstützt auch positionierte Update- und Delete-Anweisungen für die Resultsets von generierten **wählen** Anweisungen. Obwohl es nur statische und Vorwärtscursor Cursor unterstützt, entspricht die Cursorbibliothek die Anforderungen vieler Anwendungen. Darüber hinaus bieten sie gute Leistung, insbesondere bei kleinen und mittelständischen Resultsets und für Anwendungen, die keine gute cursorunterstützung.  
  
 Die Cursorbibliothek ist eine Dynamic Link Library (DLL), die zwischen der Treiber-Manager und der Treiber befindet. Wenn eine Anwendung eine Funktion aufruft, ruft der Treiber-Manager die Funktion in der Cursorbibliothek, die die Funktion ausgeführt, oder ruft es im angegebenen Treiber an. Für eine bestimmte Verbindung gibt eine Anwendung an, ob die Cursorbibliothek immer verwendet wird, verwendet wird, wenn der Treiber bildlauffähige Cursor nicht unterstützt oder nie verwendet.  
  
 Die Cursorbibliothek wird als ein Treiber an den Treiber-Manager angezeigt. Wenn die Cursorbibliothek zwischen der Treiber-Manager und einer ODBC 2. befindet. *x* -Treiber die Cursorbibliothek angezeigt wird, als ein ODBC 2. *X* Treiber. Wenn die Cursorbibliothek zwischen der Treiber-Manager und einem ODBC 3. befindet *.x* -Treiber die Cursorbibliothek angezeigt wird, als ein ODBC 3.*.x* Treiber. Das Verhalten von der Cursorbibliothek richtet sich nach der Version des Treibers, der es funktioniert, mit Ausnahme von Bindung Offsets, der für beide ODBC 2. unterstützt wird. *x* und ODBC-3. *X* Treiber.  
  
 Zum Implementieren von Blockcursor **SQLFetch** und **SQLFetchScroll**, wiederholt die Cursorbibliothek aufruft **SQLFetch** im Treiber. Zum Durchführen eines Bildlaufs zu implementieren, zwischengespeichert die Daten, die er, im Arbeitsspeicher und in Dateien auf Datenträgern abgerufen hat. Wenn eine Anwendung eine neue Rowset anfordert, von die Cursorbibliothek nach Bedarf aus dem Treiber oder dem Cache abgerufen.  
  
 Zum Implementieren von positionierten Updates und delete-Anweisungen, die Cursorbibliothek erstellt ein **aktualisieren** oder **löschen** -Anweisung mit einer **, in dem** -Klausel, die die zwischengespeicherten angibt der Wert für jede gebundene Spalte in der Zeile. Wenn sie eine positioniertes Update-Anweisung ausgeführt wird, aktualisiert die Cursorbibliothek seinem Cache aus den Werten in den Puffern Rowset.  
  
 Weitere Informationen zu den ODBC-Cursorbibliothek finden Sie unter den folgenden Abschnitten in diesem Anhang:  
  
-   [Using the ODBC Cursor Library (Verwenden der ODBC-Cursorbibliothek)](../../../odbc/reference/appendixes/using-the-odbc-cursor-library.md)  
  
-   [Executing Positioned Update and Delete Statements (Ausführen einer positionierten Aktualisierung und von DELETE-Anweisungen)](../../../odbc/reference/appendixes/executing-positioned-update-and-delete-statements.md)  
  
-   [Cursor-Bibliothek-Codebeispiel](../../../odbc/reference/appendixes/cursor-library-code-example.md)  
  
-   [Hinweise zur Implementierung](../../../odbc/reference/appendixes/implementation-notes.md)  
  
-   [ODBC Cursor Library Error Codes (ODBC-Cursorbibliothek – Fehlercodes)](../../../odbc/reference/appendixes/odbc-cursor-library-error-codes.md)

---
title: "Vollständige Parallelität | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- transactions [ODBC], concurrency control
- concurrency control [ODBC]
- optimistic concurrency [ODBC]
ms.assetid: 9d71e09e-bc68-4c1f-9229-ed2a7be7d324
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 3ae017de17892595dac94a0dd4bbb843d6d5f658
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="optimistic-concurrency"></a>Vollständige Parallelität
*Vollständige Parallelität* Name abgeleitet wird, aus der optimistischen Annahme, dass Konflikte zwischen Transaktionen selten treten; als ein Konflikt aufgetreten sind wird, wenn eine andere Transaktion aktualisiert oder eine Zeile mit Daten zwischen dem Zeitpunkt löscht, er wird gelesen, nach der aktuellen Transaktion und der Uhrzeit wird aktualisiert oder gelöscht. Dies ist das Gegenteil von *eingeschränkte Parallelität* oder sperren, in dem Entwickler der Anwendung Meinung ist, dass solche Konflikte üblich sind.  
  
 Bei der vollständigen Parallelität wird eine Zeile nach links nicht gesperrt, bis die Zeit wird zu aktualisieren oder zu löschen. An diesem Punkt wird die Zeile liest und überprüft, um festzustellen, ob es seit dem letzten Lesen geändert wurde. Wenn die Zeile geändert wurde, wird die Update- oder Delete schlägt fehl und wiederholt werden muss.  
  
 Um zu bestimmen, ob eine Zeile geändert wurde, wird die neue Version mit eine zwischengespeicherte Version der Zeile verglichen. Diese Prüfung kann auf die Zeilenversion, z. B. die Timestamp-Spalte in SQL Server oder die Werte der einzelnen Spalten in der Zeile basieren. Viele Datenbankmanagementsysteme unterstützt Zeilenversionen nicht.  
  
 Verletzung der vollständigen Parallelität kann von der Datenquelle oder die Anwendung implementiert werden. In beiden Fällen sollte die Anwendung eine niedrige Transaktionsisolationsstufe z. B. Read Committed verwenden; mit einer höheren Ebene negiert die erhöhte Parallelität durch vollständige Parallelität erzielt.  
  
 Verletzung der vollständigen Parallelität durch die Datenquelle implementiert ist, legt die Anwendung das Anweisungsattribut SQL_ATTR_CONCURRENCY auf SQL_CONCUR_ROWVER oder SQL_CONCUR_VALUES fest. Zum Aktualisieren oder Löschen einer Zeile, führt es ein positioniertes Update oder Delete-Anweisung oder Aufrufe **SQLSetPos** genauso wie mit eingeschränkte Parallelität; gibt der Treiber oder die Datenquelle SQLSTATE 01001 (Cursor Vorgang Konflikt), wenn die Aktualisieren oder löschen ein Fehler auftritt, aufgrund der ein Konflikt.  
  
 Wenn die Anwendung selbst durch vollständige Parallelität implementiert, wird das SQL_ATTR_CONCURRENCY-Anweisungsattribut auf SQL_CONCUR_READ_ONLY, eine Zeile zu lesen. Wenn sie Zeilenversionen verglichen werden und die Zeilenversionsspalte ist nicht bekannt, ruft es **SQLSpecialColumns** SQL_ROWVER Optional können Sie den Namen dieser Spalte zu bestimmen.  
  
 Die Anwendung aktualisiert oder löscht die Zeile infolge einer Erhöhung der Parallelität auf SQL_CONCUR_LOCK (für den Schreibzugriff auf die Zeile Zugriff) und Ausführen einer **UPDATE** oder **löschen** -Anweisung mit einer **, in denen ** -Klausel, die gibt die Version oder die Werte der zeilenupdates wurde beim Lesen der Anwendung. Wenn die Zeile seit geändert wurde, schlägt die Anweisung fehl. Wenn die **, in denen** Klausel wird die Zeile nicht eindeutig identifiziert, die Anweisung kann auch aktualisieren oder Löschen von anderen Zeilen; Zeilenversionen immer eindeutig identifiziert Zeilen, aber Zeilenwerte Zeilen eindeutig zu identifizieren, nur dann, wenn sie den Primärschlüssel enthalten.

---
title: INSERT-Anweisung Einschränkungen | Microsoft Docs
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
- ODBC SQL grammar, INSERT statement limitations
- INSERT statement limitations [ODBC]
- truncation of data [ODBC]
ms.assetid: dea05698-527a-41ab-8729-bbed85556185
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a31c77afe09219e30849131e7920136392b8a442
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="insert-statement-limitations"></a>INSERT-Anweisung
Eingefügte Daten werden auf der rechten Seite ohne Warnung abgeschnitten, falls zu lang ist, um in der Spalte zu passen.  
  
 Bei dem Versuch, einen Wert einfügen, der außerhalb des Bereichs des Datentyps einer Spalte bewirkt, dass eine NULL in die Spalte eingefügt werden soll.  
  
 Wenn eine dBASE, Microsoft Excel, Paradox oder Textdriver verwendet wird, fügt eine Zeichenfolge der Länge 0 (null) in eine Spalte eingefügt. tatsächlich ein NULL-Wert stattdessen.  
  
 Wenn der Microsoft Excel-Treiber verwendet wird, wenn eine leere Zeichenfolge in eine Spalte eingefügt wird, wird die leere Zeichenfolge in NULL konvertiert. eine gesuchte SELECT-Anweisung, die mit einer leeren Zeichenfolge in die WHERE-Klausel für die betreffende Spalte nicht erfolgreich ausgeführt wird.  
  
 Eine Tabelle kann nicht vom Treiber Paradox unter zwei Bedingungen aktualisiert werden:  
  
-   Wenn ein eindeutiger Index nicht für die Tabelle definiert ist. Dies gilt nicht für eine leere Tabelle, die mit einer einzelnen Zeile aktualisiert werden kann, selbst wenn ein eindeutiger Index für die Tabelle nicht definiert ist. Wenn eine einzelne Zeile in eine leere Tabelle, die nicht über einen eindeutigen Index verfügt eingefügt wird, kann keine Anwendung einen eindeutigen Index erstellen oder fügen Sie zusätzliche Daten, nachdem die einzelne Zeile eingefügt wurde.  
  
-   Wenn das Borland-Datenbankmodul nicht implementiert wird, nur lesen und Anfügen-Anweisungen sind zulässig, für die Tabelle Paradox.  
  
 Wenn der Text-Treiber verwendet wird, wird NULL-Werte werden durch eine Zeichenfolge mit Leerzeichen aufgefüllt, in Dateien mit fester Länge dargestellt, jedoch als keine Leerzeichen im durch Trennzeichen getrennte Dateien dargestellt. Beispielsweise ist in der folgenden Zeile, die drei Felder enthält, das zweite Feld einen NULL-Wert auf:  
  
```  
"Smith:,, 123  
```  
  
 Wenn der Text-Treiber verwendet wird, können alle Spaltenwerte mit Leerzeichen aufgefüllt werden. Die Länge des jede Zeile muss kleiner als oder gleich 65,543 Byte sein.

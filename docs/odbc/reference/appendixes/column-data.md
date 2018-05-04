---
title: Spaltendaten | Microsoft Docs
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
- column data [ODBC]
- ODBC cursor library [ODBC], cache
- cursor library [ODBC], cache
- cache [ODBC]
ms.assetid: 0425818c-9469-493f-9e3c-fc03d9411c5c
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1aa5125d58c2d630a9233b5564ad3c58203a669f
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="column-data"></a>Spaltendaten
> [!IMPORTANT]  
>  Diese Funktion wird in einer zukünftigen Version von Windows entfernt werden. Verwenden Sie diese Funktion beim Entwickeln neuer Anwendungen und Planen von Anwendungen zu ändern, die dieses Feature verwenden. Microsoft empfiehlt die Verwendung der Cursorfunktionalität der Treiber.  
  
 Die Cursorbibliothek erstellt einen Puffer im Cache für jeden Datenpuffer gebunden werden, um das Resultset mit **SQLBindCol**. Er verwendet die Werte in diesen Puffern zum Erstellen einer **, in dem** -Klausel, wenn er eine positionierte emuliert update oder delete-Anweisung. Diese Puffer aus dem Rowset Puffern aktualisiert, wenn er ruft Daten aus der Datenquelle und wann es positionierte Update-Anweisungen ausgeführt wird.  
  
 Die Cursorbibliothek zur Aktualisierung der Cache aus dem Rowset-Puffer übertragen Sie die Daten gemäß der C-Datentyp, der im angegebenen **SQLBindCol**. Wenn die C-Datentyp eines Puffers Rowset SQL_C_SLONG ist, überträgt die Cursorbibliothek z. B. vier Byte an Daten; Wenn es sich um SQL_C_CHAR handelt und *Pufferlänge* ist 10, die Cursorbibliothek überträgt 10 Bytes an Daten. Die Cursorbibliothek führt nicht keine typüberprüfung oder Konvertierungen auf die Daten aus, die es überträgt.  
  
> [!NOTE]  
>  Die Cursorbibliothek nicht seinem Cache nach einer Spalte aktualisiert, wenn **StrLen_or_IndPtr* im entsprechenden Rowset Puffer SQL_DATA_AT_EXEC oder das Ergebnis des Makros SQL_LEN_DATA_AT_EXEC ist.  
  
 Wenn sie eine Spalte, eine von Datenquellendaten leer füllt Zeichen fester Länge und NULL-Wert fester Länge, binäre Daten nach Bedarf aktualisiert. Beispielsweise speichert eine Datenquelle als "Smith" "Smith" in einer char(10)-Spalte vom Datentyp. Die Cursorbibliothek ist Daten in die Rowset-Puffer nicht mit Leerzeichen aufgefüllt oder mit Nullen aufgefüllt, wenn er diese Daten in den Cache kopiert, nach der Ausführung einer positioniertes Update-Anweisung. Aus diesem Grund, wenn eine Anwendung erfordert, dass die Werte im Cache für die Cursorbibliothek mit Leerzeichen aufgefüllt oder mit Nullen aufgefüllt sind, muss er mit Leerzeichen aufgefüllt oder mit Nullen aufgefüllt die Werte in den Puffern Rowsets vor der Ausführung einer positioniertes Update-Anweisung.

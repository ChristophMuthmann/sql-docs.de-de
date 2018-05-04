---
title: Erstellen von Anweisungen durchsucht | Microsoft Docs
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
- searched statements [ODBC]
- ODBC cursor library [ODBC], statement processing
- ODBC cursor library [ODBC], searched statements
- SQL statements [ODBC], cursor library
- cursor library [ODBC], statement processing
- cursor library [ODBC], searched statements
- SQL statements [ODBC], searched statements
ms.assetid: e429254c-c43f-4fbf-98b2-5f1ed53501ff
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8fa7d3b27e483ea628dcdf0c9d44766b3142cb94
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="constructing-searched-statements"></a>Erstellen von komplexen Anweisungen
> [!IMPORTANT]  
>  Diese Funktion wird in einer zukünftigen Version von Windows entfernt werden. Verwenden Sie diese Funktion beim Entwickeln neuer Anwendungen und Planen von Anwendungen zu ändern, die dieses Feature verwenden. Microsoft empfiehlt die Verwendung der Cursorfunktionalität der Treiber.  
  
 Um unterstützen positioniertes Update und delete-Anweisungen, die Cursorbibliothek erstellt eine gesuchte **aktualisieren** oder **löschen** positionierte Anweisung. Um Aufrufe unterstützen **SQLGetData** in einem Block von Daten, die Cursorbibliothek erstellt eine gesuchte **wählen** -Anweisung zum Erstellen eines Ergebnisses festgelegt, die die aktuelle Zeile der Daten enthält. In jedem dieser Anweisungen die **, in denen** Klausel Listet die Werte, die im Cache für jede gebundene Spalte, die für die SQL_DESC_SEARCHABLE-Feld-ID in SQL_PRED_SEARCHABLE oder SQL_PRED_BASIC zurückgibt gespeicherten  **SQLColAttribute**.  
  
> [!CAUTION]  
>  Die **, in denen** -Klausel erstellt, indem die Cursorbibliothek zur Identifikation der aktuellen Zeile kann fehlschlagen, um alle Zeilen zu identifizieren, Identifizieren von einer anderen Zeile oder mehr als eine Zeile zu identifizieren.  
  
 Wenn eine positionierte Update- oder Delete-Anweisung mehr als eine Zeile betroffen sind, aktualisiert die Cursorbibliothek die zeilenstatusarray nur für die Zeile, auf der der Cursor positioniert ist, und gibt SQL_SUCCESS_WITH_INFO und SQLSTATE 01001 (Cursor Vorgang Konflikt). Wenn die Anweisung keine Zeilen identifiziert, wird die Cursorbibliothek die zeilenstatusarray nicht aktualisiert, und SQL_SUCCESS_WITH_INFO und SQLSTATE 01001 (Cursor Vorgang Konflikt) zurückgegeben. Eine Anwendung kann Aufrufen **SQLRowCount** die Anzahl der Zeilen zu ermitteln, die aktualisiert oder gelöscht wurden.  
  
 Wenn die **wählen** -Klausel zur Positionierung des Cursors für einen Aufruf **SQLGetData** mehr als eine Zeile identifiziert **SQLGetData** ist nicht unbedingt die richtigen Daten zurückgegeben. Wenn sie keine Zeilen identifiziert **SQLGetData** gibt SQL_NO_DATA zurück.  
  
 Wenn eine Anwendung die folgenden Richtlinien, entspricht die **, in dem** -Klausel erstellt, indem die Cursorbibliothek muss eindeutig identifizieren, die aktuelle Zeile, es sei denn, dies unmöglich, z. B. wenn die Datenquelle enthält, auf Duplikat Zeilen.  
  
-   **Binden von Spalten, die die Zeile eindeutig identifizieren.** Wenn die gebundenen Spalten die Zeile nicht eindeutig identifiziert die **, in denen** -Klausel erstellt, indem die Cursorbibliothek möglicherweise mehr als eine Zeile zu identifizieren. In einem positioniertes Update oder Delete-Anweisung sind möglicherweise eine solche Klausel mehr als eine Zeile aktualisiert oder gelöscht werden. In einem Aufruf von **SQLGetData**, eine solche Klausel möglicherweise dazu führen, dass den Treiber Daten für die falschen Zeile zurückgeben. Binden alle Spalten in einen eindeutigen Schlüssel wird sichergestellt, dass jede Zeile eindeutig identifiziert wird.  
  
-   **Zuordnen von Datenpuffern groß genug ist, die keine Kürzung.** Die Cursorbibliothek-Cache ist eine Kopie der Werte in die Rowset-Puffer gebunden werden, um das Resultset mit **SQLBindCol**. Wenn Daten abgeschnitten werden, wenn er in diesen Puffern platziert wird, wird er auch im Cache abgeschnitten. Ein **, in denen** -Klausel aus abgeschnittene Werte erstellt möglicherweise die zugrunde liegenden Zeile in der Datenquelle nicht richtig identifiziert.  
  
-   **Geben Sie die Länge ungleich Null-Puffer für die C-Binärdaten.** Die Cursorbibliothek ordnet Länge Puffer in der Cache nur, wenn die *StrLen_or_IndPtr* Argument in **SQLBindCol** ungleich Null ist. Wenn die *TargetType* -Argument SQL_C_BINARY ist, die Cursorbibliothek muss die Länge der binären Daten zum Erstellen eine **, in dem** Klausel aus den Daten. Es ist kein Puffer Länge für eine SQL_C_BINARY-Spalte und die Anwendung ruft **SQLGetData** versucht hat, führen Sie ein positioniertes Update oder delete-Anweisung, die Cursor-Bibliothek gibt SQL_ERROR und SQLSTATE SL014 (eine positionierte Anforderung ausgestellt wurde, und nicht alle Spaltenfelder Anzahl gepuffert wurden).  
  
-   **Geben Sie die Länge ungleich Null-Puffer für die Spalten NULL-Werte zulässt.** Die Cursorbibliothek ordnet Länge Puffer in der Cache nur, wenn die *StrLen_or_IndPtr* Argument in **SQLBindCol** ungleich Null ist. Da SQL_NULL_DATA im Puffer Länge gespeichert wird, die Cursorbibliothek wird vorausgesetzt, jede Spalte, für welche keine, die Länge Puffer angegeben wird, NULL-Werte zulässt. Wenn keine Spalte mit der Länge für eine NULL zulassende Spalte angegeben wird, erstellt die Cursorbibliothek eine **, in dem** -Klausel, die den Wert für die Spalte verwendet. Diese Klausel wird die Zeile nicht richtig identifiziert.

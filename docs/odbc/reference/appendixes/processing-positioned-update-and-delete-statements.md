---
title: Verarbeitung positioniert, Update- und Delete-Anweisungen | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- positioned deletes [ODBC]
- ODBC cursor library [ODBC], statement processing
- cursor library [ODBC], positioned update or delete
- positioned updates [ODBC]
- SQL statements [ODBC], cursor library
- ODBC cursor library [ODBC], positioned update or delete
- cursor library [ODBC], statement processing
ms.assetid: 2975dd97-48e6-4d0a-a9c7-40759a7d94c8
caps.latest.revision: "9"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 9061ad8221537eaa00eb40fab56fa10d3357198d
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="processing-positioned-update-and-delete-statements"></a>Verarbeitung positioniert, Update- und Delete-Anweisungen
> [!IMPORTANT]  
>  Diese Funktion wird in einer zukünftigen Version von Windows entfernt werden. Verwenden Sie diese Funktion beim Entwickeln neuer Anwendungen und Planen von Anwendungen zu ändern, die dieses Feature verwenden. Microsoft empfiehlt die Verwendung der Cursorfunktionalität der Treiber.  
  
 Der Cursor Library unterstützt positioniert update und delete-Anweisungen durch Ersetzen der **WHERE CURRENT OF** -Klausel in eine solche Anweisungen mit einer **, in dem** -Klausel, die in seinem Cache nach gespeicherten Werte Listet jede gebundene Spalte. Die Cursorbibliothek übergibt das neu erstellte **UPDATE** und **löschen** Anweisungen an den Treiber für die Ausführung. Für positionierte Update-Anweisungen die Cursorbibliothek anschließend aktualisiert ihren Cache aus den Werten in den Puffern Rowset und den entsprechenden Wert im Array Status Zeile SQL_ROW_UPDATED. Für positionierte Delete-Anweisungen legt er den entsprechenden Wert im Array Zeile Status SQL_ROW_DELETED fest.  
  
> [!CAUTION]  
>  Die **, in denen** -Klausel erstellt, indem die Cursorbibliothek zur Identifikation der aktuellen Zeile kann fehlschlagen, um alle Zeilen zu identifizieren, Identifizieren von einer anderen Zeile oder mehr als eine Zeile zu identifizieren. Weitere Informationen finden Sie unter [durchsucht-Anweisungen konstruieren](../../../odbc/reference/appendixes/constructing-searched-statements.md)weiter unten in diesem Anhang.  
  
 Positioniert, Update- und Delete-Anweisungen sind jedoch mit folgenden Einschränkungen:  
  
-   Positioniert, Update- und Delete Anweisungen können nur in den folgenden Fällen verwendet werden: Wenn eine **auswählen** -Anweisung generiert das Resultset; Wenn der **auswählen** Anweisung enthielt keinen Join eine  **UNION** -Klausel, oder ein **GROUP BY** -Klausel; und wenn alle Spalten, die einen Alias oder ein Ausdruck in der select-Liste verwendet, nicht mit gebunden wurden **SQLBindCol**.  
  
-   Wenn eine Anwendung eine positionierte Update- oder Delete-Anweisung vorbereitet hat, sie müssen dazu nach aufgerufen wurde **SQLFetch** oder **SQLFetchScroll**. Obwohl die Cursorbibliothek die Anweisung den Treiber für die Vorbereitung sendet, schließt der Anweisung und führt sie aus direkt Wenn die Anwendung aufruft, **SQLExecute**.  
  
-   Wenn der Treiber nur eine aktive Anweisung unterstützt, wird die Bibliothek-Cursorn, die der Rest des Ergebnisses festgelegt, und klicken Sie dann das aktuelle Rowset aus dem Cache refetches, bevor eine positionierte ausgeführt wird, update oder delete-Anweisung. Wenn die Anwendung dann eine Funktion aufruft, der Metadaten in einem Resultset zurückgibt (z. B. **SQLNumResultCols** oder **SQLDescribeCol**), die Cursorbibliothek gibt einen Fehler zurück.  
  
-   Wenn eine positionierte Update- oder Delete-Anweisung für eine Spalte einer Tabelle ausgeführt wird, die eine Timestamp-Spalte enthält, die automatisch aktualisiert wird, jedes Mal, wenn ein Update ausgeführt wird, fehl alle nachfolgenden positionierte Update- oder Delete-Anweisungen, wenn die Timestamp-Spalte ist gebunden. Dies tritt auf, wenn der gesuchten update oder delete-Anweisung, die Cursorbibliothek erstellt, die zu aktualisierende Zeile nicht genau identifiziert wird. Der Wert in der komplexen Anweisung für die Timestamp-Spalte wird den automatisch aktualisierten Wert des Timestamp-Spalte nicht überein.

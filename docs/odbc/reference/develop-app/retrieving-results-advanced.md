---
title: Abrufen von Ergebnissen (Erweitert) | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- offsets [ODBC]
- result sets [ODBC], about result sets
- bind offsets [ODBC]
ms.assetid: bc00c379-71a7-407a-975c-898243f39bb6
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 85c3447abebf7ef6eaa538a8a1d5d00edcc007fd
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="retrieving-results-advanced"></a>Abrufen von Ergebnissen (Erweitert)
Eine Anwendung angegeben werden, dass ein Offset hinzugefügt wird, Daten Puffer Adressen und den entsprechenden Längenindikator gebunden Puffer Adressen Wenn **SQLBulkOperations**, **SQLFetch**,  **SQLFetchScroll**, oder **SQLSetPos** aufgerufen wird. Die Ergebnisse dieser Erweiterungen bestimmen, die Adressen, die bei diesen Vorgängen verwendet werden.  
  
 BIND-Offsets, damit eine Anwendung so ändern Sie die Bindungen ohne Aufruf **SQLBindCol** für zuvor gebundenen Spalten. Ein Aufruf von **SQLBindCol** zum Binden von Daten ändert sich der Pufferadresse und den Längenindikator/Zeiger. Das erneute Binden mit einem Versatz addiert andererseits, einfach einen Offset zum die vorhandenen gebundenen Daten Pufferadresse und Längenindikator/Pufferadresse. Wenn Offsets verwendet werden, die Bindungen sind "Template" des wie die Anwendungspuffer angelegt werden, und die Anwendung kann auf unterschiedliche Bereiche des Arbeitsspeichers dieser "Vorlage" verschieben, durch Ändern des Offsets. Ein neuer Offset kann zu einem beliebigen Zeitpunkt angegeben werden und wird immer auf die ursprünglich gebundenen Werte hinzugefügt.  
  
 Zum Angeben eines Bindung Offsets legt die Anwendung das Anweisungsattribut SQL_ATTR_ROW_BIND_OFFSET_PTR an die Adresse des eine SQLINTEGER-Puffers fest. Bevor die Anwendung eine Funktion aufruft, die die Bindungen, wie z. B. verwendet **SQLBulkOperations**, **SQLFetch**, **SQLFetchScroll**, oder **SQLSetPos**, platziert er einen Offset in Bytes, die in diesem Puffer als die Adresse des Puffers weder Pufferadresse Längenindikator/0 ist und als die gebundene Spalte im Resultset festgelegt ist. Die Summe der Adresse und den Offset muss eine gültige Adresse sein. (Dies bedeutet, dass eine oder beide der Offset und die Adresse, die der Offset hinzugefügt wird, ungültig ist, werden können, solange die Summe eine gültige Adresse ist.) Das Anweisungsattribut SQL_ATTR_ROW_BIND_OFFSET_PTR ist ein Zeiger, damit der Offset-Wert mit mehr als einer Gruppe von Binden von Daten, die geändert werden kann, durch einen Offsetwert ändern angewendet werden kann. Eine Anwendung muss sicherstellen, dass der Zeiger gültig bleibt, bis der Cursor geschlossen wird.  
  
> [!NOTE]  
>  Bindung Offsets werden vom ODBC-2 nicht unterstützt. *x* Treiber.  
  
 Dieser Abschnitt enthält die folgenden Themen.  
  
-   [Blockcursor](../../../odbc/reference/develop-app/block-cursors.md)  
  
-   [Scrollbare Cursor](../../../odbc/reference/develop-app/scrollable-cursors.md)  
  
-   [Die ODBC-Cursorbibliothek](../../../odbc/reference/develop-app/the-odbc-cursor-library.md)  
  
-   [Mehrere Ergebnisse](../../../odbc/reference/develop-app/multiple-results.md)

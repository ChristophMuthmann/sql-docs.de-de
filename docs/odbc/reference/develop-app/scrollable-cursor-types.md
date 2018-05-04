---
title: Bildlauffähige Cursortypen | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- scrollable cursors [ODBC]
- cursors [ODBC], scrollable
ms.assetid: dbd32576-0453-4e90-ae45-1a81cee8259d
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 54acbd1010d546649b1ad92a34289fa4d04da162
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="scrollable-cursor-types"></a>Bildlauffähige Cursortypen
Die vier Typen von bildlauffähigen Cursor werden statische, dynamische, keysetgesteuerte und gemischten. Statische Cursor erkennen wenige oder keine Änderungen jedoch relativ billig implementiert werden. Dynamische Cursor erkennen alle Änderungen jedoch aufwendig zu implementieren. Und gemischten, keysetgesteuerter Cursor liegen zwischen, die meisten Änderungen erkennen, aber weniger Kosten als dynamische Cursor.  
  
 Die folgenden Begriffe werden verwendet, um die Merkmale der einzelnen Typen von bildlauffähigen Cursor zu definieren:  
  
-   **Eigene Updates, löschungen und einfügungen.** Updates, löschungen und einfügungen, die über den Cursor, entweder mit einem Aufruf von **SQLBulkOperations** oder **SQLSetPos** oder mit einem positionierte update oder delete-Anweisung.  
  
-   **Andere aktualisiert, gelöscht und fügt ein.** Updates, Löschvorgängen und nicht von der Cursor, die durch andere Vorgänge in derselben Transaktion einschließlich vorgenommene einfügungen durch andere Transaktionen die und die durch andere Anwendungen.  
  
-   **Mitgliedschaft.** Der Satz von Zeilen im Resultset.  
  
-   **Reihenfolge.** Die Reihenfolge, in der Zeilen vom Cursor zurückgegeben werden.  
  
-   **Werte.** Die Werte in jeder Zeile im Resultset.  
  
 Weitere Informationen zu aktualisieren, löschen und Einfügen von Daten finden Sie unter [Übersicht über die Daten Aktualisierung](../../../odbc/reference/develop-app/updating-data-overview.md).  
  
 Dieser Abschnitt enthält die folgenden Themen.  
  
-   [Statische ODBC-Cursor](../../../odbc/reference/develop-app/odbc-static-cursors.md)  
  
-   [Dynamische Cursor von ODBC](../../../odbc/reference/develop-app/odbc-dynamic-cursors.md)  
  
-   [Keysetgesteuerte Cursor](../../../odbc/reference/develop-app/keyset-driven-cursors.md)  
  
-   [Gemischte Cursor](../../../odbc/reference/develop-app/mixed-cursors.md)

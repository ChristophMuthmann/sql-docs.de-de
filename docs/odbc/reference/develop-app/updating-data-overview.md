---
title: Aktualisieren von Daten (Übersicht) | Microsoft Docs
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
- updating data [ODBC], about updating data
- data updates [ODBC]
- updating data [ODBC]
- data updates [ODBC], about data updates
ms.assetid: 062036a4-cda6-4aaa-9765-f1ec3e0b31b1
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ce36f2467ce4da80f726c0f9370180422edddf49
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="updating-data-overview"></a>Übersicht über das Aktualisieren von Daten
Anwendungen können Daten aktualisieren, durch das Ausführen von SQL-Anweisungen oder durch Aufrufen von **SQLSetPos** oder **SQLBulkOperations**. **UPDATE**, **löschen**, und **einfügen** Anweisungen wirken sich direkt auf die Datenquelle und in der Regel vom Treiber unterstützt werden. Durchsucht, Update und Delete-Anweisungen enthalten eine Spezifikation der Zeilen zu ändern. Positioniert Update und delete-Anweisungen und **SQLSetPos** wirken sich auf die Datenquelle mithilfe eines Cursors und weniger häufig unterstützt werden.  
  
 Ob Cursorn dem Resultset mit den Methoden, die in diesem Abschnitt beschriebenen vorgenommenen Änderungen erkannt werden können, hängt von den Typ des Cursors und wie er implementiert wurde ab. Vorwärtscursor werden nicht mehr Zeilen überarbeitet und alle Änderungen werden nicht erkannt. Weitere Informationen dazu, ob Änderungen von bildlauffähige Cursor ermittelt werden können, finden Sie unter [bildlauffähige Cursor](../../../odbc/reference/develop-app/scrollable-cursors.md).  
  
 Dieser Abschnitt enthält die folgenden Themen.  
  
-   [UPDATE-, DELETE- und INSERT-Anweisungen](../../../odbc/reference/develop-app/update-delete-and-insert-statements.md)  
  
-   [Positionierte Aktualisierung und DELETE-Anweisung](../../../odbc/reference/develop-app/positioned-update-and-delete-statements.md)  
  
-   [Simulieren einer positionierten Aktualisierung und von DELETE-Anweisungen](../../../odbc/reference/develop-app/simulating-positioned-update-and-delete-statements.md)  
  
-   [Bestimmen der Anzahl der betroffenen Zeilen](../../../odbc/reference/develop-app/determining-the-number-of-affected-rows.md)  
  
-   [Aktualisieren von Daten mit SQLSetPos](../../../odbc/reference/develop-app/updating-data-with-sqlsetpos.md)  
  
-   [Aktualisieren von Daten mit SQLBulkOperations](../../../odbc/reference/develop-app/updating-data-with-sqlbulkoperations.md)  
  
-   [Long-Daten, SQLSetPos und SQLBulkOperations](../../../odbc/reference/develop-app/long-data-and-sqlsetpos-and-sqlbulkoperations.md)

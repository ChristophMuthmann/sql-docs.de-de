---
title: "Einschränkungen bei der Verwendung keysetgesteuerter Cursor | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ODBC driver for Oracle [ODBC], cursors
- keyset-driven cursors [ODBC]
ms.assetid: 59d86fed-387c-4719-9550-36343e74da44
caps.latest.revision: "9"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 18a0f58ae88da9646ecb98ee899f39fa84f8c0c1
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="limitations-of-using-keyset-driven-cursors"></a>Einschränkungen bei der Verwendung keysetgesteuerter Cursor
> [!IMPORTANT]  
>  Diese Funktion wird in einer zukünftigen Version von Windows entfernt werden. Nutzen Sie diese Funktionen bei Neuentwicklungen nicht mehr, und planen Sie die Änderung von Anwendungen, die diese Funktion zurzeit verwenden. Verwenden Sie stattdessen den ODBC-Treiber von Oracle bereitgestellt.  
  
 Sie müssen eine einzelne Spalte der ROWID für die der abgefragten Tabelle abrufen können. Ein keysetgesteuerter Cursor kann nicht verwendet werden, auf Joins, Abfragen oder Anweisungen mit DISTINCT, GROUP BY, UNION, INTERSECT oder MINUS-Klauseln.  
  
 Auch wenn Ihre Anwendung Tabellenaliasnamen verwendet, funktioniert keysetgesteuerte Cursor nicht. Forward-only- oder statische Cursortypen sind erforderlich. Verwenden das Keyset Cursortyp mit Tabellenaliasnamen führt dazu, dass die folgende Fehlermeldung: "[Microsoft] [ODBC-Treiber für Oracle] können keine keysetgesteuerten Cursors auf die Verknüpfung mit Union, intersect oder minus oder einem schreibgeschützten Resultset."  
  
> [!NOTE]  
>  Aufgrund der Art und Weise der Treiber führt die SQL-Anweisung, die mit dem Oracle-Server gesendet wird, gibt Oracle intern die folgende Fehlermeldung angezeigt: "ORA-00964: Tabelle Name nicht in der Liste."
